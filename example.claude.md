# Project Context for AI Assistants

> **What is this?** This file teaches AI assistants (like Claude) everything about your project so they can help you more effectively. The more you fill out, the better the assistance.

---

## 🚀 Quick Start - Fill This Out First

### 1. What does your app do?

A collaborative recipe sharing platform for home cooks that helps them discover, save, and scale recipes for any number of servings.

### 2. Choose your stack

**Frontend Framework**
- React (with TypeScript)

**UI/Styling**
- Tailwind CSS
- shadcn/ui components

**State Management**
- Zustand for client state
- React Query for server state

**Package Manager**
- pnpm

### 3. Your Supabase setup

**What Supabase features are you using?**
- Database (PostgreSQL)
- Authentication (Google OAuth + email/password)
- Storage (for recipe images)

**Main database tables**:
```
users - User accounts (Supabase Auth)
profiles - Extended user info (display name, avatar, bio)
recipes - Individual recipes
recipe_images - Images associated with recipes
collections - User-created recipe collections
saved_recipes - Many-to-many: users saving recipes
```

### 4. Development commands

```bash
# Install dependencies
pnpm install

# Run development server
pnpm dev

# Build for production
pnpm build

# Run tests
pnpm test

# Run Supabase locally
npx supabase start
```

---

## 📋 Project Information

### Technology Stack

**Build Tool**: Vite
**Backend**: Supabase (PostgreSQL + Auth + Storage)

**Frontend**:
- Framework: React 18 with TypeScript
- Styling: Tailwind CSS + shadcn/ui
- State: Zustand (client) + React Query (server)
- Routing: React Router v6

**TypeScript**: Yes (strict mode enabled)

**Deployment**: Vercel

### Directory Structure

```
/
├── src/
│   ├── components/
│   │   ├── ui/            # shadcn/ui components
│   │   ├── recipes/       # Recipe-specific components
│   │   ├── auth/          # Auth-related components
│   │   └── layout/        # Layout components (nav, footer)
│   ├── pages/
│   │   ├── Home.tsx
│   │   ├── RecipeDetail.tsx
│   │   ├── MyRecipes.tsx
│   │   └── Profile.tsx
│   ├── lib/
│   │   ├── supabase.ts    # Supabase client
│   │   ├── utils.ts       # General utilities
│   │   └── recipe-math.ts # Recipe scaling logic
│   ├── hooks/
│   │   ├── useAuth.ts
│   │   ├── useRecipes.ts
│   │   └── useUpload.ts
│   ├── stores/
│   │   └── authStore.ts   # Zustand auth store
│   ├── types/
│   │   ├── database.types.ts  # Generated from Supabase
│   │   └── index.ts           # Custom types
│   └── styles/
│       └── globals.css
├── supabase/
│   ├── migrations/
│   └── seed.sql
└── public/
```

### Environment Variables

```bash
# .env.local
VITE_SUPABASE_URL=https://yourproject.supabase.co
VITE_SUPABASE_ANON_KEY=your_anon_key_here
```

---

## 🎯 How Claude Should Help You

### Code Style Preferences

**File Naming**:
- Components: `PascalCase.tsx` (e.g., `RecipeCard.tsx`)
- Utilities: `camelCase.ts` or `kebab-case.ts` (e.g., `recipe-math.ts`)
- Pages: `PascalCase.tsx` (e.g., `RecipeDetail.tsx`)
- Hooks: `useCamelCase.ts` (e.g., `useRecipes.ts`)

**Code Conventions**:
- Use functional components (no class components)
- Prefer `const` over `let`
- Use async/await (not .then)
- Handle errors explicitly
- Use TypeScript strict mode
- Prefer named exports over default exports

**Supabase Patterns** - Always use this pattern:
```typescript
const { data, error } = await supabase
  .from('recipes')
  .select('*')

if (error) {
  console.error('Error fetching recipes:', error)
  throw error // or handle appropriately
}

return data
```

**React Query Pattern**:
```typescript
const { data, isLoading, error } = useQuery({
  queryKey: ['recipes', userId],
  queryFn: () => fetchUserRecipes(userId)
})
```

### Important Rules

**What Claude SHOULD do**:
- ✅ Keep code simple and readable
- ✅ Use shadcn/ui components (don't reinvent buttons, inputs, etc.)
- ✅ Use React Query for all server data fetching
- ✅ Handle loading and error states in components
- ✅ Always validate image uploads (type and size)
- ✅ Use TypeScript types from database.types.ts

**What Claude SHOULD NOT do**:
- ❌ Don't create custom UI components if shadcn/ui has them
- ❌ Don't fetch data directly in components (use React Query hooks)
- ❌ Don't store large data in Zustand (use React Query cache)
- ❌ Don't ignore error states in UI
- ❌ Don't use `any` type in TypeScript
- ❌ Don't commit .env.local

---

## 🗄️ Database Information

### Main Tables

**Table**: `profiles`
- Purpose: Extended user information beyond Supabase Auth
- Key columns: id (references auth.users), display_name, avatar_url, bio
- Access: Everyone can read, users can only update their own profile
- RLS: Enabled - `auth.uid() = id` for updates

**Table**: `recipes`
- Purpose: Store all recipes created by users
- Key columns: id, user_id, title, ingredients (jsonb), instructions (text[]), servings (int), prep_time, cook_time
- Access: Everyone can read public recipes, users can CRUD their own
- RLS: Enabled - `is_public = true OR auth.uid() = user_id` for SELECT

**Table**: `recipe_images`
- Purpose: Images for recipes (one recipe can have multiple images)
- Key columns: id, recipe_id (FK), storage_path, display_order, alt_text
- Access: Tied to recipe permissions
- RLS: Enabled - inherits from recipes table

**Table**: `collections`
- Purpose: User-created collections of recipes (like "Weeknight Dinners")
- Key columns: id, user_id, name, description, is_public
- Access: Users can CRUD their own, read public collections
- RLS: Enabled

**Table**: `saved_recipes`
- Purpose: Junction table for users saving recipes
- Key columns: user_id, recipe_id, saved_at
- Access: Users can only see/modify their own saved recipes
- RLS: Enabled - `auth.uid() = user_id`

### Row Level Security (RLS)

**Current approach**:
- [x] Users can only access their own data
- [x] Public read for published content
- [x] Admin role not implemented yet

**Common RLS pattern**:
```sql
-- Users can only edit their own recipes
CREATE POLICY "Users can update own recipes"
ON recipes
FOR UPDATE
USING (auth.uid() = user_id);

-- Everyone can read public recipes
CREATE POLICY "Anyone can read public recipes"
ON recipes
FOR SELECT
USING (is_public = true OR auth.uid() = user_id);
```

---

## 🔧 Development Workflow

### Getting Started

**First time setup**:
```bash
# 1. Install dependencies
pnpm install

# 2. Copy environment variables
cp .env.example .env.local
# Then add your Supabase URL and key to .env.local

# 3. Start local Supabase (optional but recommended)
npx supabase start
npx supabase db reset  # Applies migrations and seeds

# 4. Start dev server
pnpm dev
```

### Common Tasks

**Add a new database table**:
```bash
# Create migration
npx supabase migration new add_table_name

# Edit supabase/migrations/TIMESTAMP_add_table_name.sql
# Then apply it locally
npx supabase db reset

# Generate new TypeScript types
npx supabase gen types typescript --local > src/types/database.types.ts
```

**Upload a new recipe image**:
```typescript
// Use the useUpload hook
const { upload, isUploading } = useUpload()

const handleUpload = async (file: File) => {
  const path = await upload(file, 'recipe-images')
  // path is saved to recipe_images table
}
```

### Git Commits

**Commit message format**:
```
Add recipe scaling feature
Fix image upload validation
Update RLS policies for collections
```

---

## 🎨 Design & UI Guidelines

### UI Patterns

**Colors**:
- Primary: orange-500 (#f97316) - for CTAs and accents
- Secondary: slate-700 (#334155) - for text
- Background: white / slate-950 (dark mode)
- Success: green-500
- Error: red-500

**Spacing**: Use Tailwind's default spacing scale (4px increments)

**Components to reuse**:
- Button: `src/components/ui/button.tsx` (shadcn/ui)
- Card: `src/components/ui/card.tsx` (shadcn/ui)
- Input: `src/components/ui/input.tsx` (shadcn/ui)
- RecipeCard: `src/components/recipes/RecipeCard.tsx` (custom)

**Typography**:
- Headings: font-bold
- Body: font-normal
- All text should be readable in both light and dark mode

---

## 🚨 Known Issues & Gotchas

**Things to be aware of**:
- Recipe images must be under 5MB (enforced client-side)
- Ingredient scaling uses fractional math - round to nearest 1/4
- OAuth redirect URL must be configured in Supabase dashboard for each environment
- Supabase Storage public buckets don't work with RLS - use signed URLs for user uploads

**Technical debt**:
- Need to add optimistic updates for saving recipes
- Should add image compression before upload
- Recipe search is case-sensitive (need to add tsvector search)
- No pagination on recipe lists yet (will be slow with 100+ recipes)

---

## 📚 Project-Specific Context

### Key Features

**Feature 1**: Recipe Scaling
- How it works: Users can scale a recipe from N servings to M servings
- Implementation: `lib/recipe-math.ts` handles fractional conversion
- Important: Always round to practical fractions (1/4, 1/3, 1/2) not decimals
- UI: Scaling happens on RecipeDetail page via a dropdown

**Feature 2**: Recipe Collections
- How it works: Users can create collections and add recipes to them
- Implementation: Many-to-many through `collection_recipes` table
- Important: A recipe can be in multiple collections
- UI: Collections shown as tags on recipe cards

**Feature 3**: Image Upload
- How it works: Direct upload to Supabase Storage, then save path to DB
- Implementation: `hooks/useUpload.ts` handles upload logic
- Important: Images are in 'recipe-images' bucket, which is public
- Validation: Max 5MB, only jpg/png/webp

### Business Logic

**Important rules Claude should know**:
- Free users can create unlimited recipes but max 3 collections
- Images are automatically deleted from storage when recipe is deleted (via trigger)
- Recipe authors can always edit their recipes, even if published
- Saved recipes create a timestamp - used to show "Recently Saved"
- Ingredients are stored as JSONB array: `[{ amount, unit, name }]`

### User Workflows

**Creating a recipe**:
1. User clicks "New Recipe" button (requires auth)
2. Fills out form: title, servings, ingredients, instructions
3. Optionally uploads 1-5 images
4. Clicks "Publish" or "Save as Draft"
5. Recipe appears in "My Recipes"

**Saving a recipe**:
1. User views any public recipe
2. Clicks heart icon
3. Recipe is added to saved_recipes table
4. Heart icon fills in, shows "Saved"

---

## 🧪 Testing

**Testing approach**:
- [x] Unit tests for utilities (lib/recipe-math.ts)
- [x] Component tests for RecipeCard, RecipeForm
- [ ] E2E tests (planned)

**How to run tests**:
```bash
pnpm test           # Run all tests
pnpm test:watch     # Watch mode
pnpm test:coverage  # Coverage report
```

**What we test**:
- Recipe scaling math (critical - must be accurate)
- Ingredient parsing
- Form validation
- Image upload validation (file size, type)

**What we don't test** (yet):
- Supabase queries (mocked)
- Real-time subscriptions
- Full user flows

---

## 🚀 Deployment

**Where the app is deployed**: Vercel
**URL**: https://recipeapp.vercel.app

**Deploy process**:
- [x] Automatic on push to main branch
- Vercel builds and deploys
- Environment variables set in Vercel dashboard

**Pre-deployment checklist**:
- [ ] Tests passing
- [ ] New migrations applied to production Supabase
- [ ] Environment variables updated in Vercel (if changed)
- [ ] Images optimized
- [ ] RLS policies verified in Supabase dashboard

---

## 📖 Resources

**Useful Links**:
- [Vite Documentation](https://vitejs.dev/)
- [Supabase Documentation](https://supabase.com/docs)
- [React Query Docs](https://tanstack.com/query/latest)
- [shadcn/ui](https://ui.shadcn.com/)
- [Tailwind CSS](https://tailwindcss.com/)

**Quick Commands Reference**:
```bash
pnpm dev                                    # Start dev server
pnpm build                                  # Build for production
pnpm preview                                # Preview production build
npx supabase db reset                       # Reset local database
npx supabase gen types typescript --local > src/types/database.types.ts
```

---

## 🤖 For AI Assistants: Progressive Complexity Guide

**When user is just starting (0-1 week into project)**:
- Keep solutions very simple
- Avoid abstractions and helpers
- Inline logic is fine
- Don't suggest tests, optimizations, or advanced patterns

**When project has basic features (1-4 weeks)** ← WE ARE HERE:
- Start suggesting reusable components for repeated patterns
- Can introduce simple abstractions when there's clear duplication
- Basic error handling is good
- Suggest React Query for new data fetching

**When project is maturing (1+ months)**:
- Suggest performance optimizations if needed
- Recommend testing for critical features
- Can suggest more sophisticated patterns when appropriate
- Think about edge cases and error states

**Always**:
- Match the existing code style and complexity level
- Ask before making big architectural changes
- Prefer boring, proven solutions over clever ones
- Use shadcn/ui components instead of building from scratch

---

**Last Updated**: 2025-01-15

---

## 🌟 About This Template

This is a real example of a filled-out claude.md file for a recipe app.

**What makes this example effective**:
- Specific tech stack decisions documented
- Real business logic explained
- Actual gotchas and workarounds listed
- Clear examples of database schema
- Practical workflows documented

This is what your claude.md should look like after you've been working on your project for a few weeks.
