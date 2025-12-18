# Authentication - ShipFree

ShipFree uses Supabase for authentication, providing a secure and scalable solution with multiple authentication methods.

## Setup

### Configuration

1.  Add your Supabase credentials to `.env`:

```
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_role_key
```


## Project Structure

The authentication-related code is organized as follows:

```
src/
├── app/
│   ├── (auth)/
│   │   ├── callback/     # OAuth callback handling
│   │   ├── login/        # Login page
│   │   ├── register/     # Registration page
│   │   └── layout.tsx    # Auth layout with session check
├── components/
│   ├── login-form.tsx    # Login form component
│   └── register-form.tsx # Registration form component
└── lib/
    └── supabase/
        ├── client.ts     # Browser client initialization
        └── server.ts     # Server client initialization
```


## Authentication Methods

### 1\. Email/Password Authentication

```
// Login
const { error } = await supabase.auth.signInWithPassword({
  email,
  password,
});
 
// Registration
const { error } = await supabase.auth.signUp({
  email,
  password,
});
```


### 2\. Magic Link Authentication

```
const { error } = await supabase.auth.signInWithOtp({
  email,
});
```


### 3\. OAuth (Google) Authentication

```
const { error } = await supabase.auth.signInWithOAuth({
  provider: "google",
  options: {
    redirectTo: `${window.location.origin}/auth/callback`,
  },
});
```


## Implementation Details

### Client-Side Setup

```
// lib/supabase/client.ts
import { createBrowserClient } from "@supabase/ssr";
 
export const createClient = () =>
  createBrowserClient(
    process.env.NEXT_PUBLIC_SUPABASE_URL!,
    process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!
  );
```


### Server-Side Setup

```
// lib/supabase/server.ts
import { createServerClient } from "@supabase/ssr";
import { cookies } from "next/headers";
 
export const createClient = () => {
  const cookieStore = cookies();
 
  return createServerClient(
    process.env.NEXT_PUBLIC_SUPABASE_URL!,
    process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!,
    {
      cookies: {
        get(name: string) {
          return cookieStore.get(name)?.value;
        },
      },
    }
  );
};
```


### OAuth Callback Handling

```
// app/(auth)/callback/route.ts
import { createClient } from "@/lib/supabase/server";
import { NextResponse } from "next/server";
 
export async function GET(request: Request) {
  const requestUrl = new URL(request.url);
  const code = requestUrl.searchParams.get("code");
 
  if (code) {
    const supabase = createClient();
    await supabase.auth.exchangeCodeForSession(code);
  }
 
  return NextResponse.redirect(requestUrl.origin + "/dashboard");
}
```


### Protected Routes

```
// app/dashboard/page.tsx
import { createClient } from "@/lib/supabase/server";
import { redirect } from "next/navigation";
 
export default async function Dashboard() {
  const supabase = createClient();
  const {
    data: { user },
  } = await supabase.auth.getUser();
 
  if (!user) {
    redirect("/auth/login");
  }
 
  return (
    // Dashboard content
  );
}
```


## Components

### Login Form

The login form component (`components/login-form.tsx`) provides:

*   Email/password login
*   Magic link authentication
*   Google OAuth sign-in
*   Registration link

### Register Form

The registration form component (`components/register-form.tsx`) handles:

*   New user registration
*   Login link for existing users

## Session Management

### Checking Authentication Status

```
const supabase = createClient();
const {
  data: { user },
} = await supabase.auth.getUser();
 
if (user) {
  // User is authenticated
} else {
  // User is not authenticated
}
```


### Sign Out

```
const handleSignOut = async () => {
  "use server";
  const supabase = createClient();
  await supabase.auth.signOut();
  redirect("/auth/login");
};
```


## Security Best Practices

1.  **Environment Variables**
    
    *   Use `.env` for sensitive credentials
    *   Prefix client-side variables with `NEXT_PUBLIC_`
    *   Keep service role key secure
2.  **Protected Routes**
    
    *   Implement authentication checks
    *   Use server-side redirect
    *   Handle unauthorized access
3.  **Error Handling**
    
    *   Proper error messages
    *   Graceful fallbacks
    *   User-friendly notifications
4.  **Session Management**
    
    *   Secure cookie handling
    *   Proper session cleanup
    *   Token refresh handling

## User Profile Integration

The authentication system is integrated with the user profiles table:

```
CREATE TABLE public.profiles (
    id UUID PRIMARY KEY REFERENCES auth.users(id) ON DELETE CASCADE,
    name TEXT,
    email TEXT,
    image TEXT,
    customer_id TEXT,
    price_id TEXT,
    has_access BOOLEAN DEFAULT false,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT (now() AT TIME ZONE 'UTC'),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT (now() AT TIME ZONE 'UTC')
);
```


### Automatic Profile Creation

```
-- Function to handle new user signup
CREATE OR REPLACE FUNCTION public.handle_new_user()
RETURNS TRIGGER AS $
BEGIN
  INSERT INTO public.profiles (id, email, name, image)
  VALUES (
    NEW.id,
    NEW.email,
    COALESCE(NEW.raw_user_meta_data->>'full_name', NEW.raw_user_meta_data->>'name'),
    NEW.raw_user_meta_data->>'avatar_url'
  );
  RETURN NEW;
END;
$ LANGUAGE plpgsql SECURITY DEFINER;
 
-- Trigger for automatic profile creation
CREATE TRIGGER on_auth_user_created
  AFTER INSERT ON auth.users
  FOR EACH ROW EXECUTE FUNCTION public.handle_new_user();
```


## Troubleshooting

Common issues and solutions:

1.  **Session Issues**
    
    *   Clear browser cookies
    *   Check environment variables
    *   Verify callback URLs
2.  **OAuth Problems**
    
    *   Validate provider settings
    *   Check redirect URLs
    *   Verify credentials
3.  **Profile Creation**
    
    *   Check trigger function
    *   Verify database permissions
    *   Monitor error logs

## Resources

*   [Supabase Auth Documentation](https://supabase.com/docs/guides/auth) 
*   [Next.js Authentication Guide](https://nextjs.org/docs/authentication) 
*   [OAuth Configuration](https://supabase.com/docs/guides/auth/social-login)