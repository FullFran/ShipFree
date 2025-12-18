# SEO - ShipFree

## SEO Features

ShipFree comes with built-in SEO optimization to help your application rank better in search engines.

### Basic Meta Tags

```
// app/layout.tsx
export const metadata: Metadata = {
  title: "Your App Name",
  description: "Your app description",
  keywords: ["keyword1", "keyword2"],
};
```


### Dynamic Meta Tags

For dynamic pages, use generateMetadata:

```
export async function generateMetadata({ params }): Promise<Metadata> {
  return {
    title: `${params.title} | Your App`,
    description: params.description,
    openGraph: {
      title: params.title,
      description: params.description,
      images: [params.image],
    },
  };
}
```


## OpenGraph Support

ShipFree includes comprehensive OpenGraph tags for better social media sharing:

```
export const metadata: Metadata = {
  openGraph: {
    type: "website",
    locale: "en_US",
    url: "https://yourdomain.com",
    siteName: "Your App Name",
    images: [
      {
        url: "https://yourdomain.com/og-image.jpg",
        width: 1200,
        height: 630,
        alt: "Your App Name",
      },
    ],
  },
};
```


## Sitemap Generation

### Automatic Sitemap

ShipFree automatically generates a sitemap for your pages:

```
// app/sitemap.ts
export default async function sitemap() {
  const routes = ["", "/about", "/features", "/pricing"];
 
  return routes.map((route) => ({
    url: `https://yourdomain.com${route}`,
    lastModified: new Date(),
  }));
}
```


### Dynamic Sitemap

For dynamic content:

```
export default async function sitemap() {
  // Fetch your dynamic routes
  const posts = await fetchPosts();
 
  const postUrls = posts.map((post) => ({
    url: `https://yourdomain.com/blog/${post.slug}`,
    lastModified: post.updatedAt,
  }));
 
  return [...postUrls];
}
```


## Structured Data

### JSON-LD Implementation

```
<script
  type="application/ld+json"
  dangerouslySetInnerHTML={{
    __html: JSON.stringify({
      "@context": "https://schema.org",
      "@type": "WebSite",
      name: "Your App Name",
      url: "https://yourdomain.com",
    }),
  }}
/>
```


### Common Schemas

*   Organization
*   Product
*   Article
*   FAQs
*   BreadcrumbList

## Best Practices

1.  **Title Tags**
    
    *   Keep titles under 60 characters
    *   Include main keyword
    *   Make them descriptive and engaging
2.  **Meta Descriptions**
    
    *   Keep under 155 characters
    *   Include call-to-action
    *   Make them unique for each page
3.  **URL Structure**
    
    *   Use kebab-case
    *   Keep them short and descriptive
    *   Include relevant keywords
4.  **Image Optimization**
    
    *   Use descriptive alt tags
    *   Optimize image sizes
    *   Use next/image component

## Performance Optimization

1.  **Core Web Vitals**
    
    *   Optimize LCP (Largest Contentful Paint)
    *   Minimize CLS (Cumulative Layout Shift)
    *   Improve FID (First Input Delay)
2.  **Loading Speed**
    
    *   Use code splitting
    *   Implement lazy loading
    *   Optimize assets
3.  **Mobile Optimization**
    
    *   Ensure responsive design
    *   Test on multiple devices
    *   Optimize touch targets

## Monitoring

1.  **Google Search Console**
    
    *   Monitor search performance
    *   Check indexing status
    *   Fix technical issues
2.  **Analytics Integration**
    
    *   Track user behavior
    *   Monitor conversion rates
    *   Analyze traffic sources

## Tools and Resources

*   [Google Search Console](https://search.google.com/search-console) 
*   [Google Analytics](https://analytics.google.com/) 
*   [Schema Markup Validator](https://validator.schema.org/) 
*   [Mobile-Friendly Test](https://search.google.com/test/mobile-friendly)