# Deployment - ShipFree

To deploy ShipFree, follow these detailed steps:

### 1\. Commit and Push to GitHub

Ensure your code is committed and pushed to a private GitHub repository:

```
git add .
git commit -m "Prepare for deployment"
git push origin main
```


Replace `main` with your default branch name if different.

### 2\. Deploy to Vercel

1.  **Sign Up or Log In**: Access your [Vercel dashboard](https://vercel.com/dashboard) .
    
2.  **Import Project**:
    
    *   Click on **“Add New”** and select **“Project”**.
    *   Choose your GitHub repository containing ShipFree.
3.  **Configure Project**:
    
    *   Vercel will auto-detect your Next.js setup.
    *   In the **“Configure Project”** section, click on **“Environment Variables”**.
4.  **Set Environment Variables**:
    
    *   Add the following variables, ensuring they match those in your local `.env` file:
        
        
|Name                         |Value                         |
|-----------------------------|------------------------------|
|NEXT_PUBLIC_SUPABASE_URL     |your_supabase_url             |
|NEXT_PUBLIC_SUPABASE_ANON_KEY|your_supabase_anon_key        |
|SUPABASE_SERVICE_ROLE_KEY    |your_supabase_service_role_key|
|STRIPE_SECRET_KEY            |your_stripe_secret_key        |
|MAILGUN_API_KEY              |your_mailgun_api_key          |
|MAILGUN_DOMAIN               |your_mailgun_domain           |

        
        Replace `your_*` with your actual credentials.
        
        **Note**: For variables that need to be accessible on the client side, prefix them with `NEXT_PUBLIC_`.
        
5.  **Deploy**:
    
    *   Click **“Deploy”** to start the deployment process.
    *   Vercel will build and deploy your application.

### 3\. Post-Deployment

*   **Verify Deployment**: Once deployed, visit your Vercel-provided URL to ensure ShipFree is running as expected.
    
*   **Environment Variable Management**:
    
    *   To update environment variables in the future:
        *   Navigate to your project in the Vercel dashboard.
        *   Go to **“Settings”** > **“Environment Variables”**.
        *   Add or edit variables as needed.
        *   Redeploy the project to apply changes.

**Important**: Ensure all necessary environment variables are correctly configured in Vercel, as the `.env.local` file is not committed to your repository and won’t be available during deployment.

By following these steps, ShipFree will be live and operational on Vercel.