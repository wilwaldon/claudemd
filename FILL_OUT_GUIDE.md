# 5-Minute Fill-Out Guide

**Goal**: Get your `claude.md` working in 5 minutes. You can always expand it later.

## Minute 1: Describe Your App

```markdown
YOUR APP: A [type of app] for [target users] that [main value proposition]
```

**Examples**:
- "A task manager for solo developers that syncs across devices"
- "A recipe sharing platform for home cooks that uses AI to scale ingredients"
- "A habit tracker for students that gamifies daily routines"

**Your turn**:
```
YOUR APP:


```

---

## Minute 2: Pick Your Stack

Just delete what you DON'T use:

**Frontend Framework**:
- ~~React (with TypeScript)~~
- ~~Vue 3~~
- Svelte ✓
- ~~Vanilla JS~~

**UI/Styling**:
- Tailwind CSS ✓
- ~~shadcn/ui~~
- ~~CSS Modules~~

**State Management**:
- ~~React Context~~
- Zustand ✓
- ~~Redux~~

**Your turn** (delete what you don't use):
```
Frontend Framework:
- React (with TypeScript)
- Vue 3
- Svelte
- Vanilla JS

UI/Styling:
- Tailwind CSS
- shadcn/ui
- CSS Modules
- Styled Components
- Plain CSS

State Management:
- React Context
- Zustand
- Redux Toolkit
- Jotai
- None

Package Manager:
- npm
- pnpm
- yarn
- bun
```

---

## Minute 3: List Your Database Tables

Even if you haven't created them yet, just list what you're planning:

```markdown
users - User accounts (from Supabase Auth)
profiles - Extended user info (avatar, bio, preferences)
projects - User-created projects
tasks - Individual tasks within projects
```

**Your turn**:
```
users -
profiles -
[table_name] -
[table_name] -
[table_name] -
```

---

## Minute 4: Add Your Dev Commands

Just copy-paste your actual commands:

```bash
# Install
npm install

# Dev server
npm run dev

# Build
npm run build
```

**Your turn** (fill in YOUR commands):
```bash
# Install dependencies


# Run development server


# Build for production


# Run tests (if you have them)


```

---

## Minute 5: Add One Important Rule

What's ONE thing Claude should know about your project?

**Examples**:
- "Users must verify email before accessing the dashboard"
- "All images must be uploaded to Supabase Storage, not stored as base64"
- "Use the existing Button component in src/components/ui, don't create new ones"
- "Always show loading states when fetching data"
- "All database queries should have error handling"

**Your turn**:
```
Important Rule:


```

---

## Done! 🎉

You now have a functional `claude.md` that will make AI assistance way more effective.

## Optional: Add More When You Have 5 More Minutes

### Quick Win 1: Add Your Color Scheme
```markdown
**Colors**:
- Primary: blue-600 (#2563eb)
- Secondary: purple-500 (#a855f7)
- Background: white / slate-900 (dark mode)
```

### Quick Win 2: Add RLS Status
```markdown
**RLS Status**:
- [x] Users table: Users can only read their own row
- [x] Profiles table: Public read, own write
- [ ] Projects table: Not yet implemented
```

### Quick Win 3: Add a Key User Flow
```markdown
**Sign-up flow**:
1. User enters email on landing page
2. Magic link sent to email
3. Clicks link → redirected to /onboarding
4. Fills out profile → redirected to /dashboard
```

### Quick Win 4: Add Known Issues
```markdown
**Known Issues**:
- Real-time updates break if user loses connection (need to add reconnect logic)
- Image uploads fail if file is over 5MB (need to add client-side validation)
```

---

## When to Update This File

**Add to it whenever you**:
- ✅ Make an architectural decision
- ✅ Add a new database table
- ✅ Establish a code pattern
- ✅ Discover a gotcha or bug
- ✅ Add a new feature
- ✅ Change your deployment setup

**Don't update it**:
- ❌ Every single day
- ❌ For tiny code changes
- ❌ For fixing typos
- ❌ For normal bug fixes

**Good rule of thumb**: Update it when you learn something you'd want to tell a new teammate.

---

## Expansion Priority (when you have more time)

If you want to keep expanding your `claude.md`, do it in this order:

1. **Database schema details** (10 min)
   - Full table descriptions
   - Relationships between tables
   - RLS policies

2. **Code conventions** (10 min)
   - File naming
   - Component structure
   - Import order

3. **Business logic** (15 min)
   - Key rules and constraints
   - User permissions
   - Important workflows

4. **Known issues** (5 min)
   - Current bugs
   - Workarounds
   - Technical debt

5. **Testing approach** (10 min)
   - What you test
   - How to run tests
   - Testing patterns

6. **Deployment process** (10 min)
   - Where it's deployed
   - How to deploy
   - Environment variables

---

## Real Example: Before & After

### Before (Empty Template)
```markdown
YOUR APP:


**Table**: `[your_table_name]`
- Purpose:
- Key columns:
```

### After (5 Minutes of Work)
```markdown
YOUR APP: A meal planning app for busy parents that generates weekly menus based on dietary preferences


**Table**: `meal_plans`
- Purpose: Weekly meal plans generated for users
- Key columns: id, user_id, week_start_date, meals (jsonb)
- Access: Users can only see their own meal plans

**Table**: `recipes`
- Purpose: Recipe database (shared across all users)
- Key columns: id, title, ingredients, instructions
- Access: Everyone can read, only admins can write
```

---

## Copy-Paste Templates

### Template: Database Table Entry
```markdown
**Table**: `table_name`
- Purpose: [what this stores]
- Key columns: [important columns]
- Access: [who can read/write]
- RLS: [your RLS rule or "not set up yet"]
```

### Template: Feature Entry
```markdown
**Feature**: [Name]
- What it does: [brief description]
- How it works: [technical details]
- Important: [gotchas or special rules]
```

### Template: User Flow
```markdown
**[Flow Name]**:
1. [Step 1]
2. [Step 2]
3. [Step 3]
Result: [what happens at the end]
```

### Template: Known Issue
```markdown
**[Issue Title]**:
- Problem: [what's wrong]
- Impact: [how it affects users]
- Workaround: [temporary solution]
- Fix planned: [yes/no, when]
```

---

**Need help?** Check the main README.md for more examples and tips.

**Stuck?** Just fill out what you can and leave the rest blank. Even a partially filled `claude.md` is 10x better than nothing.
