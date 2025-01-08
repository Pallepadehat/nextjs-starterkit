# Next.js Starter Kit

A modern Next.js starter template with a powerful tech stack and essential features pre-configured.

## Features

- ⚡️ [Next.js 14](https://nextjs.org/) with App Router
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
├── components/         # React components
├── lib/               # Utility functions and configurations
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

## Dark Mode

Dark mode is implemented using `next-themes` and can be toggled using the `ThemeProvider` component. The theme persists across page reloads and respects the user's system preferences by default.

## Database

This project uses Prisma as the ORM with the following features:
- Type-safe database queries
- Auto-generated Prisma Client
- Database migrations
- Prisma Studio for database management

## UI Components

[shadcn/ui](https://ui.shadcn.com/) components are used for the UI. These are built on top of [Radix UI](https://www.radix-ui.com/) and styled with Tailwind CSS.

## Learn More

To learn more about the technologies used in this starter kit:

- [Next.js Documentation](https://nextjs.org/docs)
- [Prisma Documentation](https://www.prisma.io/docs)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [shadcn/ui Documentation](https://ui.shadcn.com)
- [TypeScript Documentation](https://www.typescriptlang.org/docs)

## License

MIT
