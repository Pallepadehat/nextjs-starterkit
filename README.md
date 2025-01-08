# Next.js Starter Kit

A modern Next.js starter template with a powerful tech stack and essential features pre-configured.

## Features

- ⚡️ [Next.js 15](https://nextjs.org/) with App Router
- 🔐 [Auth.js v5](https://authjs.dev/) for authentication
- 🔥 [TypeScript](https://www.typescriptlang.org/) for type safety
- 🎨 [Tailwind CSS](https://tailwindcss.com/) for styling
- 🌙 Dark mode with [next-themes](https://github.com/pacocoursey/next-themes)
- 🎯 [ESLint](https://eslint.org/) and [Prettier](https://prettier.io/) for code quality
- 🗃️ [Prisma](https://www.prisma.io/) for database management
- 🎮 [shadcn/ui](https://ui.shadcn.com/) for beautiful UI components
- ✨ [Geist](https://vercel.com/font) font family by Vercel

## Getting Started

1. Clone this repository:
```bash
git clone <your-repo-url>
cd <your-repo-name>
```

2. Install dependencies:
```bash
npm install
# or
pnpm install
# or
yarn install
```

3. Set up your environment variables:
```bash
cp .env.example .env
```

Update your `.env` file with the following variables:
```bash
# Database
DATABASE_URL="your-database-url"

# Auth.js
AUTH_SECRET="your-auth-secret" # Run: openssl rand -base64 32
AUTH_URL="http://localhost:3000"

# OAuth Providers (optional)
GITHUB_ID="your-github-id"
GITHUB_SECRET="your-github-secret"
GOOGLE_ID="your-google-id"
GOOGLE_SECRET="your-google-secret"
```

4. Set up Prisma:
```bash
# Initialize your database
npx prisma db push

# Generate Prisma Client
npx prisma generate
```

5. Start the development server:
```bash
npm run dev
# or
pnpm dev
# or
yarn dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

## Project Structure

```
├── app/                # Next.js App Router directory
│   ├── api/           # API routes including auth
│   ├── auth/          # Auth.js routes and components
├── components/         # React components
├── lib/               # Utility functions and configurations
│   ├── auth.ts        # Auth.js configuration
├── prisma/            # Prisma schema and migrations
├── public/            # Static assets
└── styles/            # Global styles
```

## Available Scripts

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run start` - Start production server
- `npm run lint` - Run ESLint
- `npm run format` - Format code with Prettier
- `npm run prisma:studio` - Open Prisma Studio

## Code Quality

This project uses:
- ESLint for code linting
- Prettier for code formatting
- TypeScript for type checking

Configuration files:
- `.eslintrc.js` - ESLint configuration
- `.prettierrc.js` - Prettier configuration
- `tsconfig.json` - TypeScript configuration

## Authentication

This project uses Auth.js v5 for authentication with the following features:
- Session-based authentication
- OAuth providers (GitHub, Google) support
- JWT session strategy
- Protected API routes and pages
- TypeScript support
- Integration with Prisma for user data storage

### Session Management & Route Protection

#### Protected Pages

You can protect pages by checking the session using the `auth` function:

```tsx
// app/protected/page.tsx
import { auth } from "@/auth"

export default async function ProtectedPage() {
  const session = await auth()
  if (!session) return <div>Not authenticated</div>

  return (
    <div>
      <h1>Protected Page</h1>
      <pre>{JSON.stringify(session, null, 2)}</pre>
    </div>
  )
}
```

#### Protected API Routes

API routes can be protected using the `auth` wrapper:

```tsx
// app/api/protected/route.ts
import { auth } from "@/auth"
import { NextResponse } from "next/server"

export const GET = auth(function GET(req) {
  if (req.auth) return NextResponse.json(req.auth)
  return NextResponse.json({ message: "Not authenticated" }, { status: 401 })
})
```

#### Middleware Protection

This starter includes global route protection using Next.js middleware:

```tsx
// middleware.ts
export { auth as middleware } from "@/auth"

// Protect all routes except public ones
export const config = {
  matcher: ["/((?!api|_next/static|_next/image|favicon.ico).*)"],
}
```

The middleware is configured in `auth.ts`:

```tsx
// auth.ts
import NextAuth from "next-auth"

export const { auth, handlers } = NextAuth({
  callbacks: {
    authorized: async ({ auth }) => {
      // Logged in users are authenticated, otherwise redirect to login page
      return !!auth
    },
  },
})
```

For more granular control, you can customize the middleware behavior:

```tsx
// middleware.ts
import { auth } from "@/auth"

export default auth((req) => {
  // Allow public routes
  if (
    req.nextUrl.pathname.startsWith("/login") ||
    req.nextUrl.pathname.startsWith("/register")
  ) {
    return null
  }

  // Redirect unauthenticated users to login
  if (!req.auth) {
    const newUrl = new URL("/login", req.nextUrl.origin)
    return Response.redirect(newUrl)
  }
})
```

💡 **Security Note**: While middleware provides a convenient way to protect routes, you should always verify the session as close to your data fetching as possible for maximum security.

## Dark Mode

Dark mode is implemented using `next-themes` and can be toggled using the `ThemeProvider` component. The theme persists across page reloads and respects the user's system preferences by default.

## Database

This project uses Prisma as the ORM with the following features:
- Type-safe database queries
- Auto-generated Prisma Client
- Database migrations
- Prisma Studio for database management
- Built-in Auth.js adapter for user management

## UI Components

[shadcn/ui](https://ui.shadcn.com/) components are used for the UI. These are built on top of [Radix UI](https://www.radix-ui.com/) and styled with Tailwind CSS.

## Learn More

To learn more about the technologies used in this starter kit:

- [Next.js Documentation](https://nextjs.org/docs)
- [Auth.js Documentation](https://authjs.dev/reference/nextjs)
- [Prisma Documentation](https://www.prisma.io/docs)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [shadcn/ui Documentation](https://ui.shadcn.com)
- [TypeScript Documentation](https://www.typescriptlang.org/docs)

## License

MIT
