# Project Context for AI Assistants

> **What is this?** This file teaches AI assistants (like Claude) everything about your project so they can help you more effectively. The more you fill out, the better the assistance.

---

## 🚀 Quick Start - Fill This Out First

### 1. What does your app do?
<!-- In 1-2 sentences, what problem does this solve? -->

**Example**: "A collaborative task management app for remote teams that syncs in real-time."

YOUR APP:



### 2. Choose your stack (delete what you don't use)

**Frontend Framework**
- React (with TypeScript)
- Vue 3
- Svelte
- Vanilla JS

**UI/Styling**
- Tailwind CSS
- shadcn/ui
- CSS Modules
- Styled Components
- Plain CSS

**State Management**
- React Context
- Zustand
- Redux Toolkit
- Jotai
- None (just useState/props)

**Package Manager**
- npm
- pnpm
- yarn
- bun

### 3. Your Supabase setup

**What Supabase features are you using?** (delete what you don't need)
- Database (PostgreSQL)
- Authentication (email/password, OAuth providers, magic links)
- Real-time subscriptions
- Storage
- Edge Functions

**Main database tables** (add yours):
```
users - User accounts
profiles - User profile info
[your table] - [what it stores]
[your table] - [what it stores]
```

### 4. Development commands

Fill in your actual commands:
```bash
# Install dependencies
npm install

# Run development server
npm run dev

# Build for production
npm run build

# Run tests (if you have them)
npm run test
```

---

## 📋 Project Information

### Technology Stack

**Build Tool**: Vite
**Backend**: Supabase (PostgreSQL + Auth + Real-time + Storage)

**Frontend**:
- Framework: [Fill in from above]
- Styling: [Fill in from above]
- State: [Fill in from above]

**TypeScript**: Yes / No

**Deployment**: [Vercel / Netlify / Other - fill in when you deploy]

### Directory Structure

**Your project structure** (update this as your project grows):
```
/
├── src/
│   ├── components/       # Reusable UI components
│   ├── pages/            # Page components
│   ├── lib/              # Utilities and helpers
│   ├── hooks/            # Custom hooks (if React)
│   └── styles/           # Global styles
├── supabase/
│   └── migrations/       # Database migrations
├── public/               # Static files
└── .env.local            # Environment variables (not committed)
```

### Environment Variables

```bash
# Add to .env.local (get these from your Supabase dashboard)
VITE_SUPABASE_URL=your-project-url.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key
```

---

## 🎯 How Claude Should Help You

### Code Style Preferences

**File Naming**:
- Components: `PascalCase.tsx` (e.g., `UserProfile.tsx`)
- Utilities: `camelCase.ts` (e.g., `formatDate.ts`)
- Pages: `PascalCase.tsx` (e.g., `Dashboard.tsx`)

**Code Conventions**:
- Use functional components
- Prefer `const` over `let`
- Use async/await over .then()
- Handle errors explicitly

**Supabase Patterns** - Always use this pattern:
```typescript
const { data, error } = await supabase
  .from('table_name')
  .select('*')

if (error) {
  console.error('Error:', error)
  // Handle error appropriately
  return
}

// Use data
```

### Important Rules

**What Claude SHOULD do**:
- ✅ Keep code simple and readable
- ✅ Follow existing patterns in the codebase
- ✅ Ask questions when unclear
- ✅ Check for errors in Supabase responses
- ✅ Use TypeScript types when possible

**What Claude SHOULD NOT do**:
- ❌ Don't add features I didn't ask for
- ❌ Don't over-engineer simple solutions
- ❌ Don't ignore the `error` property from Supabase
- ❌ Don't add lots of comments (code should be self-explanatory)
- ❌ Don't use the Supabase service_role key in client code

---

## 🗄️ Database Information

### Main Tables

**Table**: `users`
- Purpose: [What this stores]
- Key columns: [Important columns]
- Access: [Who can read/write]

**Table**: `[your_table_name]`
- Purpose:
- Key columns:
- Access:

*Add more tables as you create them*

### Row Level Security (RLS)

**Current approach** (update as you build):
- [ ] RLS not set up yet
- [ ] Users can only access their own data
- [ ] Role-based access (admin, user, etc.)
- [ ] Custom policies per table

**Common RLS pattern you're using**:
```sql
-- Example: Users can only see their own data
CREATE POLICY "Users can view own data"
ON your_table
FOR SELECT
USING (auth.uid() = user_id);
```

---

## 🔧 Development Workflow

### Getting Started

**First time setup**:
```bash
# 1. Install dependencies
npm install

# 2. Copy environment variables
cp .env.example .env.local
# Then add your Supabase URL and key to .env.local

# 3. Start dev server
npm run dev
```

### Common Tasks

**Add a new database table**:
```bash
# Create migration file
npx supabase migration new add_your_table_name

# Edit the migration file in supabase/migrations/
# Then apply it (if using local Supabase)
npx supabase db reset
```

**Update TypeScript types from database**:
```bash
npx supabase gen types typescript --local > src/types/database.types.ts
```

### Git Commits

**Commit message format** (keep it simple):
```
Add user profile page
Fix login button styling
Update database schema for posts
```

---

## 🎨 Design & UI Guidelines

### UI Patterns

**Colors** (update with your actual colors):
- Primary: [your primary color]
- Secondary: [your secondary color]
- Background: [light/dark mode info]

**Spacing**: [Tailwind classes / CSS variables you use]

**Components to reuse**: [List any components you want used consistently]
- Button: [where it's defined]
- Card: [where it's defined]
- Form Input: [where it's defined]

---

## 🚨 Known Issues & Gotchas

**Things to be aware of**:
- [Add issues as you discover them]
- [Example: "User avatars need to be square and under 2MB"]
- [Example: "Real-time updates don't work in Firefox private mode"]

**Technical debt** (things to improve later):
- [Add items here]
- [Example: "Need to add loading states to all data fetches"]
- [Example: "Should add error boundary for better error handling"]

---

## 📚 Project-Specific Context

### Key Features

**Feature 1**: [Name]
- How it works:
- Important notes:

**Feature 2**: [Name]
- How it works:
- Important notes:

*Add more as you build*

### Business Logic

**Important rules Claude should know**:
- [Example: "Users can only create 5 free projects"]
- [Example: "Email must be verified before accessing dashboard"]
- [Add your specific rules]

### User Workflows

**Main user journey**:
1. [Step 1]
2. [Step 2]
3. [Step 3]

---

## 🧪 Testing (if you add tests later)

**Testing approach**:
- [ ] No tests yet
- [ ] Unit tests for utilities
- [ ] Component tests
- [ ] E2E tests for critical flows

**How to run tests**: [Fill in when you add tests]

---

## 🚀 Deployment (fill in when ready)

**Where the app is deployed**: [Vercel / Netlify / etc.]
**URL**: [Your production URL]

**Deploy process**:
- [ ] Automatic on push to main
- [ ] Manual deployment
- [ ] Other: [describe]

**Pre-deployment checklist**:
- [ ] Tests passing (if you have them)
- [ ] Environment variables set in hosting platform
- [ ] Database migrations run on production Supabase
- [ ] [Add other checks]

---

## 📖 Resources

**Useful Links**:
- [Vite Documentation](https://vitejs.dev/)
- [Supabase Documentation](https://supabase.com/docs)
- [Your framework docs]
- [Your UI library docs]

**Quick Commands Reference**:
```bash
npm run dev              # Start dev server
npm run build           # Build for production
npx supabase db reset   # Reset local database
```

---

## 🤖 For AI Assistants: Progressive Complexity Guide

**When user is just starting (0-1 week into project)**:
- Keep solutions very simple
- Avoid abstractions and helpers
- Inline logic is fine
- Don't suggest tests, optimizations, or advanced patterns

**When project has basic features (1-4 weeks)**:
- Start suggesting reusable components for repeated patterns
- Can introduce simple abstractions when there's clear duplication
- Basic error handling is good

**When project is maturing (1+ months)**:
- Suggest performance optimizations if needed
- Recommend testing for critical features
- Can suggest more sophisticated patterns when appropriate
- Think about edge cases and error states

**Always**:
- Match the existing code style and complexity level
- Ask before making big architectural changes
- Prefer boring, proven solutions over clever ones

---

## ✏️ Template Instructions

**How to use this file**:

1. **Start simple**: Just fill out the "Quick Start" section at the top
2. **Fill as you go**: Update sections as you make decisions (don't fill everything at once)
3. **Delete what you don't need**: Remove sections that don't apply
4. **Add what's missing**: Create new sections for project-specific needs
5. **Keep it updated**: Update this file when you make important decisions

**You don't need to fill out everything!** Start with the basics and expand as your project grows.

**Sections you can skip initially**:
- Testing (add when you write tests)
- Deployment (add when you deploy)
- Performance (add when it becomes an issue)
- Advanced architecture (add when your app gets complex)

---

**Last Updated**: [Add date when you make major changes]

---

## 🌟 About This Template

This template is designed to be shared and improved by the community.

**Version**: 2.0 - User-Friendly Edition
**License**: MIT (use freely, modify, share)
**Contribute improvements**: [Your repo URL when you open-source it]

**What makes this effective**:
- Progressive disclosure (start simple, add complexity)
- Examples everywhere (not just placeholders)
- Focused on practical usage
- Designed for real projects, not just demos
