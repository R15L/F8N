# Portfolio Roadmap for a Design Engineer

## Phase 1: Planning and Strategy

### Goals

- Showcase expertise in **product design** and **frontend development**.
- Simplify the addition of portfolio items, case studies, and blog posts using **Markdown/MDX**.
- Build a scalable, performance-optimized, and visually stunning portfolio.

### Key Features

- Dynamic routing for projects and case studies using **Next.js**.
- Tailored UI components with **Tailwind CSS** and **Aceternity UI**.
- **Markdown/MDX** integration for easy content management.
- Responsive design optimized for mobile and desktop.

---

## Phase 2: Setup and Tools

### Tech Stack

- **Framework:** Next.js (React-based, supports server-side rendering and static site generation).
- **Styling:** Tailwind CSS for utility-first styling and Aceternity UI for prebuilt, customizable components.
- **Content Management:** Markdown and MDX for portfolio items and case studies.
- **Hosting:** Vercel (seamless deployment and fast CDN).
- **Analytics:** Google Analytics or Plausible for tracking visitors.

---

## Phase 3: Build the Foundation

### Tasks

1. **Initialize Next.js Project**

   ```bash
   npx create-next-app@latest R16 --ts
   cd my-portfolio
   npm install
   ```

2. **Install Dependencies**

   - **Tailwind CSS**:

     ```bash
     npm install -D tailwindcss postcss autoprefixer
     npx tailwindcss init
     ```

     Update your Tailwind config file (`tailwind.config.js`) to include paths for your components:

     ```javascript
     module.exports = {
       content: [
         "./pages/**/*.{js,ts,jsx,tsx}",
         "./components/**/*.{js,ts,jsx,tsx}",
       ],
       theme: {
         extend: {},
       },
       plugins: [],
     };
     ```

     Add Tailwind to your `globals.css` file:

     ```css
     @tailwind base;
     @tailwind components;
     @tailwind utilities;
     ```

   - **Aceternity UI**:

     ```bash
     npm install aceternity-ui
     ```

     Import specific components where needed and configure the theme if required:

     ```javascript
     import { Button } from "aceternity-ui";
     ```

   - **MDX Support**:

     ```bash
     npm install @next/mdx
     ```

     Configure MDX in `next.config.js`:

     ```javascript
     const withMDX = require('@next/mdx')({
       extension: /\.mdx?$/,
     });

     module.exports = withMDX({
       pageExtensions: ['js', 'jsx', 'ts', 'tsx', 'md', 'mdx'],
     });
     ```

3. Configure Tailwind CSS

   - Update tailwind.config.js with your preferred color palette and customizations.
   - Add Aceternity UI plugins if required.

4. Set Up MDX

   - Enable MDX in next.config.js:

   ```javascript
   const withMDX = require('@next/mdx')({
   extension: /\.mdx?$/,
   });
   ```

5. Folder Structure

   ```
   /R16
       /components         # Reusable React components (e.g., Header, Footer, ProjectCard)
       /content            # Markdown/MDX content for projects and case studies
           /projects       # Markdown/MDX files for portfolio projects
               project-1.md
               project-2.md
           /case-studies   # Markdown/MDX files for detailed case studies
               case-study-1.md
               case-study-2.md
       /pages              # Next.js pages
           /api            # API routes (if needed for forms, etc.)
           /projects       # Dynamic routes for project pages
               [slug].tsx      # Dynamic route for project details
           /case-studies   # Dynamic routes for case study pages
               [slug].tsx      # Dynamic route for case study details
           _app.tsx        # Next.js custom App component
           index.tsx       # Homepage
       /public             # Static assets (images, favicons, etc.)
           /images         # Project images and other media
               project-1.jpg
               project-2.jpg
       /styles             # Global styles or Tailwind configuration
           globals.css
       /utils              # Utility functions (e.g., markdown parsing, date formatting)
       tailwind.config.js  # Tailwind configuration
       next.config.js      # Next.js configuration
       package.json        # Dependencies and scripts
   ```

6. Dynamic Routing

   - Create a [slug].tsx file under the pages/projects/ folder for dynamic project pages.
   - Fetch Markdown/MDX files from a content/projects/ directory.

7. Markdown Content
   Structure your `content/` folder:

   ```
   /content
       /projects
           project-1.md
           project-2.md
       /case-studies
           case-study-1.md
           case-study-2.md
   ```

   ## Example `project-1.md`:

   title: "Design System for SaaS App"
   date: "2025-01-01"
   tags: ["Design System", "Product Design"]

   ***

   # Project Overview

   Designed a scalable design system for a SaaS application to improve UI consistency and development efficiency.

   ## Key Contributions

   - Built reusable Figma components.
   - Integrated Tailwind CSS with a React component library.

8. Portfolio Layout

   - Use getStaticProps and getStaticPaths in Next.js to fetch Markdown/MDX content.
   - Example projects.tsx page:

   ```javascript
   import fs from 'fs';
   import path from 'path';
   import matter from 'gray-matter';

   export async function getStaticProps() {
       const files = fs.readdirSync(path.join('content/projects'));
       const projects = files.map((filename) => {
           const markdownWithMeta = fs.readFileSync(
               path.join('content/projects', filename),
               'utf-8'
           );
           const { data: frontmatter } = matter(markdownWithMeta);

           return {
               frontmatter,
           slug: filename.replace('.md', ''),
           };
       });

       return {
           props: {
           projects,
       },
   };
   }
   ```

### 9. **Case Study Pages**

- Create a dynamic route for case studies under the `pages/case-studies/` folder:

  ```
  /pages
  /case-studies
      [slug].tsx
  ```

- Example `pages/case-studies/[slug].tsx`:

  ```tsx
  import fs from 'fs';
  import path from 'path';
  import matter from 'gray-matter';
  import { MDXRemote } from 'next-mdx-remote';
  import { serialize } from 'next-mdx-remote/serialize';

  export async function getStaticPaths() {
    const files = fs.readdirSync(path.join('content/case-studies'));

    const paths = files.map((filename) => ({
      params: {
        slug: filename.replace('.mdx', '').replace('.md', ''),
      },
    }));

    return {
      paths,
      fallback: false,
    };
  }

  export async function getStaticProps({ params: { slug } }) {
    const markdownWithMeta = fs.readFileSync(
      path.join('content/case-studies', `${slug}.mdx`),
      'utf-8'
    );

    const { data: frontmatter, content } = matter(markdownWithMeta);
    const mdxSource = await serialize(content);

    return {
      props: {
        frontmatter,
        slug,
        mdxSource,
      },
    };
  }

  const CaseStudy = ({ frontmatter, mdxSource }) => {
    return (
      <div className="container mx-auto px-4">
        <h1 className="text-3xl font-bold">{frontmatter.title}</h1>
        <p className="text-gray-600">{frontmatter.date}</p>
        <div className="prose lg:prose-xl mt-6">
          <MDXRemote {...mdxSource} />
        </div>
      </div>
    );
  };

  export default CaseStudy;
  ```

- Example MDX file for a case study (`content/case-studies/case-study-1.mdx`):

  ```markdown
  ---
  title: "Revamping the UX for a SaaS Dashboard"
  date: "2025-02-01"
  tags: ["UX Design", "Product Design", "Frontend Development"]
  ---

  # Overview

  Redesigned the user experience of a SaaS dashboard, focusing on improving user workflows and increasing engagement.

  ## Key Contributions

  - Conducted user research to identify pain points.
  - Designed a modern, responsive interface using Figma.
  - Developed the frontend with React and Tailwind CSS.

  ## Results

  - Increased user task completion rate by 25%.
  - Reduced bounce rate by 15%.

  ## Tools Used

  - Figma, React, Tailwind CSS, Next.js
  ```

- The `MDXRemote` component allows rendering of the MDX content dynamically, making it easy to manage and display case studies.

### 10. SEO Optimization

- Implement structured data for projects and case studies.
- Add meta tags and descriptions to each page.
- Use Next.js's built-in SEO features.
