# Hero - ShipFree

The Hero component serves as the main landing section of the ShipFree website, featuring a compelling value proposition and visual elements.

## Features

*   Eye-catching headline
*   Descriptive subheading
*   Call-to-action buttons
*   Tech stack illustration
*   Responsive layout

## Usage

```
import HeroSection from "@/app/(site)/Hero";
 
export default function HomePage() {
  return (
    <div>
      <HeroSection />
      {/* Other sections */}
    </div>
  );
}
```


## Props

The Hero component is a self-contained component that doesn’t accept any props.

## Structure

### Main Content

*   Headline with value proposition
*   Supporting text explaining benefits
*   Primary and secondary CTAs
*   GitHub stars counter

### Visual Elements

*   Tech stack illustration
*   Background styling
*   Responsive image handling

## Implementation Details

```
import Link from "next/link";
import { Zap } from "lucide-react";
import Image from "next/image";
 
const HeroSection = () => {
  return (
    <div className="bg-[#212121] min-h-screen text-white">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        {/* Hero content */}
      </div>
    </div>
  );
};
 
export default HeroSection;
```


## Styling

The component uses Tailwind CSS for:

*   Dark theme aesthetics
*   Responsive grid layout
*   Typography scaling
*   Spacing and alignment

## Best Practices

1.  **Performance**
    
    *   Next.js Image optimization
    *   Responsive image sizing
    *   Lazy loading support
2.  **Accessibility**
    
    *   Semantic HTML structure
    *   ARIA labels where needed
    *   Keyboard navigation
3.  **Responsiveness**
    
    *   Mobile-first design
    *   Flexible layouts
    *   Breakpoint optimization

## Examples

### Basic Implementation

```
<HeroSection />
```


### With Custom Background

```
<div className="bg-gradient-to-b from-zinc-900 to-black">
  <HeroSection />
</div>
```


## Customization

While the component doesn’t accept props, you can customize it by:

1.  **Modifying Content**
    
    *   Update headline text
    *   Change CTAs
    *   Adjust supporting text
2.  **Styling Changes**
    
    *   Modify color scheme
    *   Adjust spacing
    *   Change typography
3.  **Layout Adjustments**
    
    *   Alter grid structure
    *   Modify breakpoints
    *   Change image placement

*   `Navbar` - Usually placed above the Hero
*   `FeaturesSection` - Often follows the Hero
*   `MakerIntro` - Complements the Hero message