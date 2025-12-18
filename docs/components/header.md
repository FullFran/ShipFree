# Header - ShipFree

The `Header` component is a responsive navigation bar that includes:

*   **Logo (Left)**: Your brand’s logo.
*   **Navigation Links (Center)**: Links to essential pages.
*   **Call-to-Action (Right)**: A primary action button.
*   **Mobile Menu**: Links and CTA are hidden on mobile and accessible via a burger menu.

### Usage

```
import Header from "@/app/(site)/Navbar";
 
export default function Page() {
  return (
    <>
      <Header />
    </>
  );
}
```


### Best Practices

*   Keep your **brand name small** unless you’re a globally recognized brand.
*   Always include a **Pricing** link; users will look for it regardless of your product.

### Customization

*   Update the logo file inside `/app` and match the filename in `<Navbar />` (default: `icon.png`).
*   Modify styles using TailwindCSS or DaisyUI as per project requirements.