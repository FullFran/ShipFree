# Getting Started - ShipFree

Welcome to ShipFree! This documentation will help you understand the project structure, components, and how to use them effectively.

## Project Overview

ShipFree is an open-source alternative to ShipFast, designed to help developers launch their projects faster. It’s built with modern technologies and best practices, offering a complete solution for building full-stack web applications.

## Tech Stack

*   **Frontend**: Next.js 14 with App Router
*   **Styling**: TailwindCSS with shadcn/ui components
*   **Authentication**: Supabase Auth
*   **Database**: Supabase / MongoDB
*   **Payments**: Stripe / LemonSqueezy
*   **Email**: Mailgun
*   **Documentation**: MDX with Nextra

## Project Structure

```
src/
├── app/                    # Next.js app directory
│   ├── (auth)/            # Authentication related pages
│   ├── (docs)/            # Documentation pages
│   ├── (site)/            # Main website components
│   └── globals.css        # Global styles
├── content/               # MDX content
│   ├── components/        # Component documentation
│   └── features/         # Feature documentation
├── components/           # Reusable UI components
└── lib/                  # Utility functions and configs
```


## Key Features

1.  **Modern Authentication**
    
    *   Social login with Google OAuth
    *   Magic link authentication
    *   Role-based access control
2.  **Payment Processing**
    
    *   Stripe integration
    *   LemonSqueezy alternative
    *   Subscription management
    *   Usage-based billing
3.  **Email System**
    
    *   Transactional emails
    *   Newsletter integration
    *   Email templates
    *   Mailgun integration
4.  **SEO Optimization**
    
    *   Meta tags
    *   OpenGraph support
    *   Sitemap generation
    *   Structured data
5.  **Developer Experience**
    
    *   Hot reloading
    *   TypeScript support
    *   ESLint configuration
    *   Prettier formatting

## Getting Started

Follow our [deployment guide](https://shipfree.idee8.agency/docs/deployment) to get your project up and running. For detailed information about specific features, check out the respective documentation sections in the sidebar.

## Community and Support

*   Star us on [GitHub](https://github.com/idee8/shipfree) 

## Contributing

We welcome contributions! Please read our contribution guidelines before submitting pull requests.

## License

ShipFree is open-source software licensed under the MIT license.