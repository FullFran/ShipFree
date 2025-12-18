# Emails - ShipFree

## Email

ShipFree provides robust email functionality through Mailgun integration, offering both transactional and marketing email capabilities.

## Setup

### Configuration

Add your Mailgun credentials to `.env`:

```
MAILGUN_API_KEY=your_api_key
MAILGUN_DOMAIN=your_domain
MAILGUN_FROM_EMAIL=noreply@yourdomain.com
```


## Features

### 1\. Transactional Emails

Built-in templates for common scenarios:

*   Welcome emails
*   Password reset
*   Email verification
*   Order confirmations
*   Payment receipts
*   Account notifications

### 2\. Email Templates

ShipFree uses React Email for beautiful, responsive templates:

```
// emails/WelcomeEmail.tsx
import {
  Body,
  Container,
  Head,
  Heading,
  Html,
  Text,
} from "@react-email/components";
 
export const WelcomeEmail = ({ name }: { name: string }) => (
  <Html>
    <Head />
    <Body>
      <Container>
        <Heading>Welcome to Our App!</Heading>
        <Text>Hi {name}, we're excited to have you on board!</Text>
      </Container>
    </Body>
  </Html>
);
```


### 3\. Email Sending

Simple API for sending emails:

```
import { sendEmail } from "@/lib/email";
 
// Send a single email
await sendEmail({
  to: "user@example.com",
  subject: "Welcome!",
  template: "welcome",
  variables: {
    name: "John",
  },
});
 
// Send bulk emails
await sendBulkEmails({
  recipients: ["user1@example.com", "user2@example.com"],
  subject: "Newsletter",
  template: "newsletter",
  variables: {
    content: "Latest updates...",
  },
});
```


## Best Practices

1.  **Email Deliverability**
    
    *   Set up SPF and DKIM records
    *   Monitor bounce rates
    *   Maintain sender reputation
    *   Use double opt-in
2.  **Template Design**
    
    *   Mobile-responsive layouts
    *   Accessible design
    *   Clear call-to-actions
    *   Brand consistency
3.  **Content Guidelines**
    
    *   Clear subject lines
    *   Preview text optimization
    *   Personalization
    *   Spam trigger avoidance

## Email Types

### Transactional

*   **Authentication**
    
    *   Sign-up confirmation
    *   Password reset
    *   Login notifications
*   **Account Updates**
    
    *   Profile changes
    *   Security alerts
    *   Settings updates
*   **Orders**
    
    *   Order confirmation
    *   Shipping updates
    *   Delivery confirmation

### Marketing

*   **Newsletters**
    
    *   Company updates
    *   Product announcements
    *   Blog digests
*   **Promotional**
    
    *   Special offers
    *   New features
    *   Event invitations

## Analytics

Track email performance:

*   Open rates
*   Click-through rates
*   Bounce rates
*   Spam complaints
*   Unsubscribe rates

## Testing

### Local Development

```
// Configure test mode
if (process.env.NODE_ENV === "development") {
  // Emails will be logged instead of sent
  useTestMailgun();
}
```


### Email Preview

Preview emails during development:

```
npm run email-preview
```


## Troubleshooting

Common issues and solutions:

1.  **Delivery Issues**
    
    *   Check SPF/DKIM setup
    *   Verify domain configuration
    *   Monitor bounce logs
2.  **Template Problems**
    
    *   Test across email clients
    *   Validate HTML
    *   Check image paths
3.  **API Errors**
    
    *   Verify API credentials
    *   Check rate limits
    *   Monitor API logs

## Resources

*   [Mailgun Documentation](https://documentation.mailgun.com/) 
*   [React Email](https://react.email/) 
*   [Email Testing Tools](https://www.mailgun.com/email-testing) 
*   [Deliverability Guide](https://www.mailgun.com/email-deliverability-guide)