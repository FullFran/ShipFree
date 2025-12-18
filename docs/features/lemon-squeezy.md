# LemonSqueezy - ShipFree

ShipFree provides integration with LemonSqueezy as an alternative payment processor, offering a simpler setup for digital products and subscriptions.

## Setup

### Configuration

Add your LemonSqueezy credentials to `.env`:

```
LEMON_SQUEEZY_API_KEY=your_api_key
LEMON_SQUEEZY_STORE_ID=your_store_id
LEMON_SQUEEZY_WEBHOOK_SECRET=your_webhook_secret
```


## Features

### 1\. Product Setup

Create and manage products:

```
import { LemonSqueezy } from "@lemonsqueezy/client";
 
const ls = new LemonSqueezy(process.env.LEMON_SQUEEZY_API_KEY);
 
// Fetch products
const products = await ls.getProducts();
 
// Get specific product
const product = await ls.getProduct(productId);
```


### 2\. Checkout Integration

Create checkout sessions:

```
// Create a checkout
const checkout = await ls.createCheckout({
  storeId: process.env.LEMON_SQUEEZY_STORE_ID,
  variantId: "variant_id",
  customPrice: 2999, // $29.99
  productOptions: {
    name: "Custom Plan",
    description: "Access to premium features",
  },
  checkoutOptions: {
    dark: true,
    logo: "https://yourdomain.com/logo.png",
  },
});
 
// Get checkout URL
const checkoutUrl = checkout.data.attributes.url;
```


### 3\. Subscription Management

Handle subscriptions:

```
// Get subscriptions
const subscriptions = await ls.getSubscriptions({
  filter: {
    userId: "user_123",
  },
});
 
// Update subscription
await ls.updateSubscription(subscriptionId, {
  variantId: "new_variant_id",
});
 
// Cancel subscription
await ls.cancelSubscription(subscriptionId);
```


### 4\. Webhook Handling

Process LemonSqueezy events:

```
// app/api/webhooks/lemonsqueezy/route.ts
import { verifyWebhook } from "@/lib/lemonsqueezy";
import { headers } from "next/headers";
 
export async function POST(req: Request) {
  const body = await req.text();
  const signature = headers().get("X-Signature") as string;
 
  try {
    const event = verifyWebhook(
      body,
      signature,
      process.env.LEMON_SQUEEZY_WEBHOOK_SECRET!
    );
 
    switch (event.type) {
      case "order_created":
        await handleOrderCreated(event.data);
        break;
      case "subscription_created":
        await handleSubscriptionCreated(event.data);
        break;
      case "subscription_updated":
        await handleSubscriptionUpdated(event.data);
        break;
      // Add more event handlers as needed
    }
 
    return new Response(null, { status: 200 });
  } catch (error) {
    console.error("Webhook error:", error);
    return new Response("Webhook verification failed", { status: 400 });
  }
}
```


## Components

### Checkout Button

```
export function LemonSqueezyCheckout({
  variantId,
  customPrice,
}: {
  variantId: string;
  customPrice?: number;
}) {
  const createCheckout = async () => {
    const response = await fetch("/api/create-checkout", {
      method: "POST",
      body: JSON.stringify({ variantId, customPrice }),
    });
    const { checkoutUrl } = await response.json();
    window.location.href = checkoutUrl;
  };
 
  return (
    <button
      onClick={createCheckout}
      className="bg-yellow-400 hover:bg-yellow-500 text-black px-4 py-2 rounded"
    >
      Buy Now
    </button>
  );
}
```


### Subscription Status

```
export function SubscriptionStatus({ userId }: { userId: string }) {
  const [subscription, setSubscription] = useState(null);
 
  useEffect(() => {
    fetchSubscription(userId).then(setSubscription);
  }, [userId]);
 
  return (
    <div className="p-4 border rounded">
      <h3>Subscription Status</h3>
      <div className="mt-2">
        {subscription ? (
          <>
            <p>Plan: {subscription.variant.name}</p>
            <p>Status: {subscription.status}</p>
            <p>
              Renews: {new Date(subscription.renews_at).toLocaleDateString()}
            </p>
          </>
        ) : (
          <p>No active subscription</p>
        )}
      </div>
    </div>
  );
}
```


## Best Practices

1.  **Security**
    
    *   Verify webhook signatures
    *   Use environment variables
    *   Validate checkout parameters
    *   Handle errors gracefully
2.  **User Experience**
    
    *   Clear pricing display
    *   Simple checkout process
    *   Proper loading states
    *   Clear success/error messages
3.  **Implementation**
    
    *   Store subscription status
    *   Handle webhook events
    *   Implement proper error handling
    *   Test checkout flow

## Webhook Events

Important events to handle:

1.  **Order Events**
    
    *   `order_created`
    *   `order_refunded`
2.  **Subscription Events**
    
    *   `subscription_created`
    *   `subscription_updated`
    *   `subscription_cancelled`
    *   `subscription_resumed`
    *   `subscription_expired`
3.  **License Events**
    
    *   `license_key_created`
    *   `license_key_updated`

## Error Handling

```
try {
  // LemonSqueezy operation
} catch (error) {
  if (error.response) {
    // Handle API errors
    console.error("API Error:", error.response.data);
  } else if (error.request) {
    // Handle network errors
    console.error("Network Error:", error.message);
  } else {
    // Handle other errors
    console.error("Error:", error.message);
  }
}
```


## Testing

### Test Mode

```
// Use test mode in development
const ls = new LemonSqueezy(process.env.LEMON_SQUEEZY_API_KEY, {
  testMode: process.env.NODE_ENV === "development",
});
```


### Webhook Testing

```
# Use ngrok for local webhook testing
ngrok http 3000
```


## Resources

*   [LemonSqueezy Documentation](https://docs.lemonsqueezy.com/) 
*   [API Reference](https://docs.lemonsqueezy.com/api) 
*   [Webhooks Guide](https://docs.lemonsqueezy.com/guides/webhooks) 
*   [Testing Guide](https://docs.lemonsqueezy.com/guides/testing)