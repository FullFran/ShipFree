# Features - ShipFree

The Features Section component showcases the main features of ShipFree using an interactive tabbed interface with time-saving metrics.

## Features

*   Interactive tabs navigation
*   Feature categorization
*   Time-saving metrics
*   Icon-based navigation
*   Responsive design

## Usage

```
import FeaturesSection from "@/app/(site)/FeaturesSection";
 
export default function HomePage() {
  return (
    <div>
      <FeaturesSection />
      {/* Other sections */}
    </div>
  );
}
```


## Props

The FeaturesSection component is self-contained and doesn’t accept any props.

## Structure

### Feature Categories

1.  **Emails**
    
    *   Transactional email templates
    *   Email verification flow
    *   Newsletter subscription
    *   Custom email domains
    *   Email analytics
2.  **Payments**
    
    *   Stripe integration
    *   Subscription management
    *   Usage-based billing
    *   Invoice generation
    *   Payment analytics
3.  **Authentication**
    
    *   Social login integration
    *   Two-factor authentication
    *   Password reset flow
    *   Session management
    *   Role-based access
4.  **Database**
    
    *   Schema design
    *   Data migration tools
    *   Backup automation
    *   Query optimization
    *   Real-time sync
5.  **SEO**
    
    *   Blog structure
    *   Meta tags
    *   OpenGraph support
    *   Sitemap generation
    *   Rich snippets
6.  **Styling**
    
    *   Tailwind configuration
    *   Dark mode support
    *   Responsive components
    *   Animation library
    *   Design tokens

## Implementation Details

```
import {
  Mail,
  CreditCard,
  User,
  Database,
  FileJson,
  Paintbrush,
  MoreHorizontal,
  Check,
} from "lucide-react";
import { Tabs, TabsList, TabsTrigger, TabsContent } from "@/components/ui/tabs";
 
export default function FeaturesSection() {
  const features = [
    {
      id: "emails",
      icon: Mail,
      label: "Emails",
      content: {
        title: "Email Integration",
        features: [
          "Transactional email templates",
          "Email verification flow",
          // ...more features
        ],
        timeSaved: "4 hours",
      },
    },
    // ...more feature categories
  ];
 
  return (
    <div className="bg-zinc-900 min-h-screen text-gray-300 py-16 px-4">
      <Tabs defaultValue="seo" className="w-full">
        {/* Tabs content */}
      </Tabs>
    </div>
  );
}
```


## Styling

The component uses Tailwind CSS with:

*   Dark theme colors
*   Custom tab styling
*   Responsive grid layout
*   Icon integration
*   Animation effects

## Best Practices

1.  **Performance**
    
    *   Optimized icon loading
    *   Efficient tab switching
    *   Minimal re-renders
2.  **Accessibility**
    
    *   ARIA roles for tabs
    *   Keyboard navigation
    *   Focus management
    *   Screen reader support
3.  **User Experience**
    
    *   Clear visual hierarchy
    *   Intuitive navigation
    *   Consistent spacing
    *   Smooth transitions

## Examples

### Basic Implementation

```
<FeaturesSection />
```


### With Custom Background

```
<div className="bg-gradient-to-b from-black to-zinc-900">
  <FeaturesSection />
</div>
```


## Customization

The component can be customized by:

1.  **Content Modification**
    
    *   Add/remove features
    *   Update time metrics
    *   Modify descriptions
    *   Change icons
2.  **Visual Adjustments**
    
    *   Color scheme
    *   Tab styling
    *   Icon sizes
    *   Spacing
3.  **Layout Changes**
    
    *   Grid structure
    *   Tab arrangement
    *   Responsive breakpoints
    *   Content flow

*   `Hero` - Often precedes the Features section
*   `Pricing` - Complements feature information
*   `MakerIntro` - Provides context for features