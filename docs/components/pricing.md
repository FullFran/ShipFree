# Pricing - ShipFree

The PricingSection component displays ShipFree’s pricing plans with a focus on the free community edition offering.

## Features

*   Clear pricing display
*   Feature list
*   Call-to-action button
*   Visual highlights
*   Responsive design

## Usage

```
import PricingSection from "@/app/(site)/pricing";
 
export default function HomePage() {
  return (
    <div>
      <PricingSection />
      {/* Other sections */}
    </div>
  );
}
```


## Props

The PricingSection component is self-contained and doesn’t accept any props.

## Structure

*   Pricing title
*   Value proposition
*   Free plan highlight

### Plan Details

1.  **Price Display**
    
    *   $0 USD pricing
    *   “Free Forever” label
    *   No credit card required
2.  **Feature List**
    
    *   NextJS boilerplate
    *   SEO & Blog
    *   Email integration
    *   Payment processing
    *   Database options
    *   Authentication
    *   Components & animations
    *   Documentation
3.  **Call-to-Action**
    
    *   GitHub repository link
    *   Action button
    *   Community message

## Implementation Details

```
export default function PricingSection() {
  return (
    <div
      id="pricing"
      className="min-h-screen bg-[#0F0F0F] text-white px-4 py-16"
    >
      <div className="max-w-7xl mx-auto">
        {/* Header */}
        <div className="text-center mb-16">
          <p className="text-[#FFBE18] font-medium mb-4">Pricing</p>
          <h2 className="text-4xl md:text-5xl font-bold mb-4">
            Save hours of repetitive code,
            <br />
            ship fast, get profitable!
          </h2>
          <p className="text-green-500 flex items-center justify-center gap-2">
            <span className="inline-block">🎉</span>
            100% Free Forever!
          </p>
        </div>
 
        {/* Pricing card */}
        <div className="max-w-md mx-auto">
          <div className="rounded-xl bg-zinc-900 p-6 border border-green-500/50 relative">
            {/* Card content */}
          </div>
        </div>
      </div>
    </div>
  );
}
```


## Styling

The component uses Tailwind CSS for:

*   Dark theme colors
*   Card design
*   Typography scale
*   Spacing system
*   Border effects

## Best Practices

1.  **Pricing Display**
    
    *   Clear value proposition
    *   Transparent pricing
    *   Feature clarity
    *   Strong CTA
2.  **Visual Design**
    
    *   Consistent branding
    *   Visual hierarchy
    *   Whitespace usage
    *   Highlight key features
3.  **User Experience**
    
    *   Simple layout
    *   Clear benefits
    *   Easy action path
    *   Mobile optimization

## Examples

### Basic Implementation

```
<PricingSection />
```


### With Custom Background

```
<div className="bg-gradient-to-b from-black to-zinc-900">
  <PricingSection />
</div>
```


## Customization

The component can be modified through:

1.  **Content Updates**
    
    *   Feature list
    *   Pricing details
    *   CTA message
    *   Value proposition
2.  **Visual Changes**
    
    *   Color scheme
    *   Card design
    *   Typography
    *   Spacing
3.  **Layout Adjustments**
    
    *   Card width
    *   Content arrangement
    *   Responsive behavior
    *   Feature presentation

*   `FeaturesSection` - Details what’s included
*   `FAQ` - Answers pricing questions
*   `CTA` - Drives conversion
*   `Footer` - Contains additional links