# Navbar - ShipFree

The Navbar component provides the main navigation for the ShipFree website, featuring a responsive design with mobile menu support.

## Features

*   Responsive design with mobile menu
*   GitHub stars counter
*   Smooth scroll navigation
*   Dynamic menu state management

## Usage

```
import Navbar from "@/app/(site)/Navbar";
 
export default function Layout() {
  return (
    <div>
      <Navbar />
      {/* Other content */}
    </div>
  );
}
```


## Props

The Navbar component doesn’t accept any props as it’s a self-contained component.

## Structure

*   Logo with link to home
*   Navigation links (Pricing, FAQ)
*   GitHub stars counter
*   Documentation link

*   Hamburger menu toggle
*   Collapsible navigation panel
*   Same links as desktop menu

## Implementation Details

```
"use client";
 
import Link from "next/link";
import { Zap, X } from "lucide-react";
import { useEffect, useState } from "react";
import { getGitHubStars } from "@/utils/github";
 
export default function Navbar() {
  const [isMenuOpen, setIsMenuOpen] = useState(false);
  const [stars, setStars] = useState<number | null>(null);
 
  // Toggle mobile menu
  const toggleMenu = () => setIsMenuOpen(!isMenuOpen);
 
  // Fetch GitHub stars
  useEffect(() => {
    getGitHubStars().then(setStars);
  }, []);
 
  return <nav>{/* Navigation content */}</nav>;
}
```


## Styling

The component uses Tailwind CSS for styling with:

*   Dark theme colors
*   Responsive breakpoints
*   Hover and active states
*   Smooth transitions

## Best Practices

1.  **Accessibility**
    
    *   ARIA labels for menu toggle
    *   Keyboard navigation support
    *   Semantic HTML structure
2.  **Performance**
    
    *   Client-side component
    *   Optimized state management
    *   Lazy-loaded GitHub stars
3.  **Responsiveness**
    
    *   Mobile-first approach
    *   Breakpoint-based layouts
    *   Touch-friendly interactions

## Examples

### Basic Implementation

```
<Navbar />
```


### With Custom Container

```
<div className="fixed top-0 w-full z-50">
  <Navbar />
</div>
```


*   `Hero` - Often used directly below the Navbar
*   `Footer` - Complementary navigation component
*   `Layout` - Parent component that includes Navbar