# Next.js Portfolio Starter

This repository serves as a foundational starting point for building a modern portfolio website using Next.js, Tailwind CSS, and Aceternity UI. It is designed to showcase expertise in product design and frontend development, with a focus on scalability, performance, and visual appeal.

## Overview

The project is structured to simplify the addition of portfolio items, case studies, and blog posts using Markdown/MDX. It leverages Next.js for dynamic routing and static site generation, Tailwind CSS for styling, and Aceternity UI for UI components.

## Key Features

- **Dynamic Routing**: Utilizes Next.js for dynamic routing of projects and case studies.
- **Responsive Design**: Optimized for both mobile and desktop views.
- **Content Management**: Easy management of content using Markdown/MDX.
- **SEO Optimization**: Structured data and meta tags for improved search engine visibility.

## Tech Stack

- **Framework**: Next.js (React-based, supports server-side rendering and static site generation)
- **Styling**: Tailwind CSS and Aceternity UI
- **Content Management**: Markdown and MDX
- **Hosting**: Vercel
- **Analytics**: Google Analytics or Plausible

## Installation

To set up the project locally, follow these steps:

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

   - **Aceternity UI**:

     ```bash
     npm install aceternity-ui
     ```

   - **MDX Support**:

     ```bash
     npm install @next/mdx
     ```

3. **Configure Tailwind CSS**

   Update `tailwind.config.js` to include paths for your components and add Tailwind to your `globals.css` file.

4. **Set Up MDX**

   Configure MDX in `next.config.js` to enable MDX support.

## Folder Structure

The project follows a structured folder layout:

```
/R16
    /components # Reusable React components
    /content # Markdown/MDX content for projects and case studies
    /pages # Next.js pages
    /public # Static assets
    /styles # Global styles
    /utils # Utility functions
    tailwind.config.js # Tailwind configuration
    next.config.js # Next.js configuration
    package.json # Dependencies and scripts
```

## Dynamic Routing

Dynamic routes are set up for project and case study pages. Example files include:

- `pages/projects/[slug].tsx`
- `pages/case-studies/[slug].tsx`

## Content Management

Content is managed using Markdown/MDX files located in the `content/` directory.

## Leveraging .cursorrules

The `.cursorrules` file provides guidelines and standards for maintaining code quality and consistency across the project. Key points include:

- **Code Standards**: Maintain AA A11y standards and follow best practices in performance, security, and maintainability.
- **Optimization**: Use dynamic imports, responsive design, and image optimization techniques.
- **Error Handling**: Implement guard clauses and custom error types for consistent error handling.
- **State Management**: Use modern solutions like Zustand and TanStack React Query.
- **Testing**: Write unit tests using Jest and React Testing Library.

For more details, refer to the `.cursorrules` file in the project.

## Contributing

Contributions are welcome! Please read the [contributing guidelines](CONTRIBUTING.md) for more details.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
