# Adding claude.md to an Existing Project

**You already have a project and want to add a claude.md file?** This guide is for you.

## Why Add This Mid-Project?

Even if your project is already underway, adding a `claude.md` file will:
- Make AI assistance more effective going forward
- Document decisions you've already made
- Help new team members (or future you) understand the codebase
- Create a single source of truth for project context

## 15-Minute Quick Migration

### Step 1: Copy the Template (1 min)
```bash
# Download the template
curl -O https://raw.githubusercontent.com/[your-repo]/claudemd/main/claude.md

# Or just copy/paste into your project root
```

### Step 2: Quick Fill - What You've Already Built (5 min)

**Your app description** - You already know this!
```markdown
YOUR APP: [What does your existing app do?]
```

**Your stack** - Just look at your package.json and delete what you don't use:
```bash
# Quick way to check your stack:
cat package.json | grep -E "(react|vue|svelte|vite)"
```

**Your database tables** - List what you have:
```bash
# If using Supabase local:
npx supabase db dump --schema public

# Or check your Supabase dashboard > Table Editor
```

**Your actual commands** - Copy from your package.json:
```json
"scripts": {
  "dev": "vite",
  "build": "vite build",
  ...
}
```

### Step 3: Document Your Conventions (5 min)

**Look at your existing code and document what you see**:

1. Open a few component files - how are they structured?
2. Check how you name files (PascalCase? camelCase?)
3. Look at a Supabase query - what's your error handling pattern?
4. Check your folder structure

Just write down what you're ALREADY doing, not what you wish you were doing.

### Step 4: Add Key Context (4 min)

**One important rule**:
What's ONE thing that would save AI assistants (and new developers) from making a mistake?

Examples from real projects:
- "Never use Supabase service_role key in client code"
- "All user-uploaded images go through our compression function first"
- "We use React Query for all data fetching, never fetch directly in components"

**Known issues**:
What bugs or quirks exist that you keep running into?

---

## Deep Migration (1-2 hours)

Want to do this thoroughly? Break it into sessions:

### Session 1: Core Info (30 min)
- [ ] Fill out Quick Start section
- [ ] Document technology stack
- [ ] List all database tables with descriptions
- [ ] Document environment variables
- [ ] Add development commands

### Session 2: Patterns & Conventions (30 min)
- [ ] Document code style you're using
- [ ] Add file naming conventions
- [ ] Document component patterns
- [ ] Add Supabase query patterns
- [ ] Document error handling approach

### Session 3: Domain Knowledge (30 min)
- [ ] Document key business rules
- [ ] Add user workflows
- [ ] Explain data relationships
- [ ] Document any non-obvious logic
- [ ] Add glossary of domain terms

### Session 4: Issues & Deployment (30 min)
- [ ] List known issues and workarounds
- [ ] Document technical debt
- [ ] Add deployment process
- [ ] Document testing approach
- [ ] Add monitoring/observability info

---

## Mining Your Existing Codebase

**Use AI to help you fill it out!** Run these prompts:

### Prompt 1: Discover Your Patterns
```
Look at these component files [paste 3-4 components] and tell me:
1. What naming convention am I using?
2. What's the typical component structure?
3. How am I handling errors?
4. What patterns do I repeat?
```

### Prompt 2: Extract Database Schema
```
Look at my Supabase migrations/schema and create a summary of:
1. All tables and their purposes
2. Key relationships between tables
3. What RLS policies exist
```

### Prompt 3: Document Existing Business Logic
```
Read through [key feature files] and explain:
1. What business rules are being enforced?
2. What are the important constraints?
3. What edge cases are handled?
```

---

## Team Migration

**If you have a team**, make this collaborative:

### Option A: Mob Documentation (1 hour meeting)
1. Screen share the claude.md template
2. Go through it section by section
3. Team calls out what to fill in
4. One person types it up live
5. Everyone reviews and agrees

**Benefits**:
- Fast (1 hour and you're done)
- Team alignment
- Captures tribal knowledge

### Option B: Divide and Conquer (async)
1. Assign sections to different team members:
   - Backend dev: Database schema, API patterns
   - Frontend dev: Component patterns, UI guidelines
   - Product: Business logic, user flows
   - DevOps: Deployment, environment setup
2. Everyone fills their section
3. Review together
4. Merge into final document

**Benefits**:
- Less meeting time
- Deep expertise in each section
- Async-friendly

### Option C: Gradual Documentation (2 weeks)
1. Create the file with just Quick Start filled out
2. In every PR, add one thing to claude.md
3. Make it a PR checklist item: "Updated claude.md if needed"
4. After 2 weeks, you have a comprehensive doc

**Benefits**:
- No big time investment
- Documents as you work
- Keeps it accurate

---

## Common Migration Challenges

### Challenge 1: "Our codebase is inconsistent"

**Solution**: Document what you WANT it to be, not what it is.

```markdown
**Current State**: Mix of class and functional components
**Going Forward**: All new components should be functional

**Current State**: Some files use default export, some use named
**Going Forward**: Prefer named exports for all new code
```

This helps AI assistants push you toward consistency.

### Challenge 2: "We have technical debt"

**Good!** Document it:

```markdown
## Known Technical Debt

**Issue**: No error boundaries, errors crash the whole app
- Impact: Poor UX when errors occur
- Fix planned: Yes, in Q2 2025

**Issue**: Using deprecated Supabase auth methods
- Impact: Will break when Supabase removes support
- Fix planned: Migration ticket #234
```

This helps AI avoid the problematic areas or even suggest fixes.

### Challenge 3: "Different team members do things differently"

**Use this as an opportunity to align!**

Schedule a 30-minute meeting:
1. Show the template
2. Ask "What should our conventions be?"
3. Document the agreements
4. Use claude.md as the source of truth going forward

### Challenge 4: "Too much to document"

**Start minimal:**

Just fill out:
1. What the app does
2. Tech stack
3. Main database tables
4. How to run it
5. One important rule

That's it! Expand later as needed.

---

## Migration Checklist

Use this to track your progress:

### Essential (Must Have)
- [ ] Project description filled out
- [ ] Technology stack documented
- [ ] Development commands added
- [ ] Database tables listed
- [ ] Environment variables documented

### Important (Should Have)
- [ ] Code conventions documented
- [ ] File naming patterns added
- [ ] Supabase patterns documented
- [ ] Key business rules explained
- [ ] Known issues listed

### Nice to Have (Can Add Later)
- [ ] Full database schema with relationships
- [ ] Complete user workflows
- [ ] Testing strategy documented
- [ ] Deployment process detailed
- [ ] Performance considerations added

---

## After Migration: Keeping It Updated

### Add a Reminder to Your PR Template

```markdown
## Checklist
- [ ] Tests pass
- [ ] Code reviewed
- [ ] Updated claude.md if needed (new patterns, tables, business rules, etc.)
```

### When to Update

Update claude.md when you:
- ✅ Add a new database table
- ✅ Make an architectural decision
- ✅ Establish a new code pattern
- ✅ Discover a gotcha or workaround
- ✅ Add a new integration or service
- ✅ Change deployment process

Don't update it for:
- ❌ Regular bug fixes
- ❌ Small code changes
- ❌ Typo fixes
- ❌ Daily work

**Rule of thumb**: If you'd mention it in a handoff to a new developer, add it to claude.md.

---

## Success Stories

**Before Migration**:
```
You: "Add a new user profile field"
Claude: "Should I add it to the users table or profiles table?"
You: "Profiles table, we keep auth separate"
Claude: "What's the RLS policy?"
You: "Same as the others... auth.uid() = id"
Claude: "How should I handle errors?"
You: "Same pattern we use everywhere"
```

**After Migration**:
```
You: "Add a new user profile field"
Claude: *Reads claude.md, sees profiles table pattern, RLS approach,
        and error handling - implements correctly on first try*
```

---

**Need help migrating?** Open an issue with:
- Your project type (SaaS, e-commerce, content site, etc.)
- Your tech stack
- Your biggest pain point

We'll help you get set up!
