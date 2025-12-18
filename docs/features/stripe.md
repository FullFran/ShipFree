# Stripe - ShipFree

ShipFree provides seamless integration with Stripe for handling payments, subscriptions, and billing.

## Setup

### Configuration

Add your Stripe credentials to `.env`:

```
STRIPE_SECRET_KEY=sk_test_...
STRIPE_WEBHOOK_SECRET=whsec_...
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_...
```


## Features

### 1\. Payment Processing

Handle one-time payments:

```
import { stripe } from "@/lib/stripe";
 
// Create a payment intent
const paymentIntent = await stripe.paymentIntents.create({
  amount: 2000, // Amount in cents
  currency: "usd",
  payment_method_types: ["card"],
});
 
// Confirm payment
const confirmedPayment = await stripe.paymentIntents.confirm(paymentIntent.id, {
  payment_method: "pm_card_visa",
});
```


### 2\. Subscription Management

Handle recurring payments:

```
// Create a subscription
const subscription = await stripe.subscriptions.create({
  customer: customerId,
  items: [{ price: "price_H5ggYwtDq4fbrJ" }],
  payment_behavior: "default_incomplete",
  payment_settings: { save_default_payment_method: "on_subscription" },
  expand: ["latest_invoice.payment_intent"],
});
 
// Update subscription
await stripe.subscriptions.update(subscriptionId, {
  items: [{ price: "price_new" }],
});
 
// Cancel subscription
await stripe.subscriptions.del(subscriptionId);
```


### 3\. Webhook Handling

Process Stripe events:

```
// app/api/webhooks/stripe/route.ts
import { stripe } from "@/lib/stripe";
import { headers } from "next/headers";
 
export async function POST(req: Request) {
  const body = await req.text();
  const signature = headers().get("Stripe-Signature") as string;
 
  let event;
 
  try {
    event = stripe.webhooks.constructEvent(
      body,
      signature,
      process.env.STRIPE_WEBHOOK_SECRET!
    );
  } catch (err) {
    return new Response(
      `Webhook Error: ${err instanceof Error ? err.message : "Unknown Error"}`,
      { status: 400 }
    );
  }
 
  try {
    switch (event.type) {
      case "customer.subscription.created":
        await handleSubscriptionCreated(event.data.object);
        break;
      case "customer.subscription.updated":
        await handleSubscriptionUpdated(event.data.object);
        break;
      case "customer.subscription.deleted":
        await handleSubscriptionDeleted(event.data.object);
        break;
      // Add more event handlers as needed
    }
 
    return new Response(null, { status: 200 });
  } catch (error) {
    console.error("Error processing webhook:", error);
    return new Response("Webhook handler failed", { status: 500 });
  }
}
```


## Components

### Payment Form

```
import { Elements } from "@stripe/stripe-js";
import { PaymentElement } from "@stripe/stripe-js/elements";
 
export function CheckoutForm() {
  return (
    <Elements stripe={stripePromise}>
      <form>
        <PaymentElement />
        <button type="submit">Pay Now</button>
      </form>
    </Elements>
  );
}
```


### Subscription Management UI

```
export function SubscriptionManager() {
  return (
    <div>
      <h2>Manage Subscription</h2>
      <div className="space-y-4">
        <PlanSelector />
        <PaymentMethodSelector />
        <BillingDetails />
      </div>
    </div>
  );
}
```


## Best Practices

1.  **Security**
    
    *   Use webhook signatures
    *   Validate amounts server-side
    *   Handle errors gracefully
    *   Use Strong Customer Authentication (SCA)
2.  **User Experience**
    
    *   Clear pricing display
    *   Smooth checkout flow
    *   Proper error messaging
    *   Loading states
3.  **Testing**
    
    *   Use test API keys
    *   Test webhook handling
    *   Verify error scenarios
    *   Check email notifications

## Webhook Events

Important events to handle:

1.  **Subscription Events**
    
    *   `customer.subscription.created`
    *   `customer.subscription.updated`
    *   `customer.subscription.deleted`
2.  **Payment Events**
    
    *   `payment_intent.succeeded`
    *   `payment_intent.payment_failed`
    *   `charge.succeeded`
    *   `charge.failed`
3.  **Customer Events**
    
    *   `customer.created`
    *   `customer.updated`
    *   `customer.deleted`

## Error Handling

Common errors and solutions:

```
try {
  // Stripe operation
} catch (error) {
  if (error instanceof Stripe.errors.CardError) {
    // Handle card errors
  } else if (error instanceof Stripe.errors.InvalidRequestError) {
    // Handle invalid parameters
  } else if (error instanceof Stripe.errors.AuthenticationError) {
    // Handle authentication errors
  } else {
    // Handle unexpected errors
  }
}
```


## Testing

### Test Cards

```
const TEST_CARDS = {
  success: "4242424242424242",
  decline: "4000000000000002",
  insufficient_funds: "4000000000009995",
  requires_authentication: "4000002500003155",
};
```


### Webhook Testing

```
stripe listen --forward-to localhost:3000/api/webhooks/stripe
```


## Resources

*   [Stripe Documentation](https://stripe.com/docs) 
*   [Testing Guide](https://stripe.com/docs/testing) 
*   [API Reference](https://stripe.com/docs/api) 
*   [Elements Documentation](https://stripe.com/docs/stripe-js) 

```

```