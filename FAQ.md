# Frequently Asked Questions

## General Questions

### What is a claude.md file?

A `claude.md` file is a markdown document in your project root that provides context to AI assistants (like Claude, ChatGPT, etc.) about your project. Think of it as a "README for AI" - it teaches the AI about your tech stack, conventions, patterns, and business logic.

### Why not just use comments in code?

Comments are great for explaining *how* code works. claude.md explains:
- *Why* architectural decisions were made
- *What* patterns to follow across files
- *Where* things are located
- Business rules that span multiple files
- Context that doesn't belong in any single file

### Do other AI tools besides Claude use this?

While it's called `claude.md`, the concept works with any AI assistant that can read files in your project:
- Claude (Desktop, API, CLI)
- Cursor
- GitHub Copilot (indirectly - helps maintain consistent patterns)
- ChatGPT with code analysis
- Any future AI coding tools

The file format is just markdown, so it's universally readable.

### How is this different from README.md?

| README.md | claude.md |
|-----------|-----------|
| For humans (users, contributors) | For AI assistants |
| What the project does, how to install | How to work ON the project |
| User-facing documentation | Developer context |
| Stays relatively stable | Updates as you code |

They complement each other!

---

## Usage Questions

### How often should I update it?

**Update when you**:
- Add a new database table or major schema change
- Make an architectural decision
- Establish a new code pattern
- Add a third-party integration
- Discover an important gotcha
- Change deployment process

**Don't update every day** - only when you have context worth documenting.

**Good rule**: If you'd mention it to a new team member, add it.

### How long should it be?

**Minimum**: 5 minutes of work (Quick Start section)
**Sweet spot**: 1-2 pages of actually useful context
**Maximum**: Whatever is useful - don't pad it

Quality over quantity. A focused 1-page doc is better than a rambling 10-page doc.

### Do I need to fill out every section?

No! Delete sections that don't apply to your project.

**Minimal viable claude.md**:
- What your app does
- Tech stack
- Database tables (if applicable)
- How to run dev server
- One important rule

Everything else is optional and should be added when relevant.

### Should my team use one claude.md or multiple files?

**One file** is usually best:
- ✅ Single source of truth
- ✅ Easy to find
- ✅ AI assistants can read it all at once

**Multiple files** if your project is huge:
- `claude.md` - Main context
- `claude-backend.md` - Backend-specific
- `claude-frontend.md` - Frontend-specific

But start with one file - only split if it becomes unwieldy (5+ pages).

---

## Technical Questions

### Where should I put this file?

**In your project root**, alongside `README.md`, `package.json`, etc.

```
your-project/
├── claude.md         ← Here
├── README.md
├── package.json
├── src/
└── ...
```

For monorepos, you can have one in each package:
```
monorepo/
├── claude.md         ← Overall project context
├── apps/
│   ├── web/
│   │   └── claude.md ← Web app specific
│   └── mobile/
│       └── claude.md ← Mobile app specific
└── packages/
    └── shared/
        └── claude.md ← Shared library specific
```

### What format should I use?

**Markdown** (`.md` file). It's:
- Human-readable
- AI-friendly
- Supported everywhere
- Easy to edit
- Works with version control

Use standard markdown - headings, lists, code blocks, links, etc.

### Should I commit this to git?

**YES!** Absolutely commit it.

- ✅ It's not a secret (no sensitive data)
- ✅ It should version with your code
- ✅ Team members should all have it
- ✅ It's part of your documentation

`.env.local` → Don't commit
`claude.md` → Do commit

### How do I handle sensitive information?

**Never put secrets in claude.md!**

❌ Don't include:
- API keys
- Passwords
- Database connection strings
- Service role keys
- Internal URLs (if private)

✅ Do include:
- *Which* services you use
- *How* to configure them (not actual values)
- *Where* to get the keys
- Example/template format

**Example**:
```markdown
## Stripe Integration

API Key: Get from Stripe Dashboard → Developers → API Keys
Add to .env.local as VITE_STRIPE_PUBLIC_KEY

Use test mode key (starts with pk_test_) in development
```

---

## Content Questions

### What if I'm just starting and don't have conventions yet?

Perfect time to set them! Use claude.md to declare your intentions:

```markdown
## Code Conventions (In Progress)

**File Naming**: Going with PascalCase for components
**State Management**: Using Zustand for now, may revisit
**Supabase Queries**: Still figuring out the pattern
```

As you build, update these to reflect what you actually do.

### Should I document *how* to do things or just *what* we do?

**Both!**

**What we do** (principles):
- "We use React Query for all server state"
- "We keep components small and focused"

**How to do it** (patterns):
```typescript
// Our standard React Query pattern:
const { data, isLoading } = useQuery({
  queryKey: ['resource', id],
  queryFn: () => fetchResource(id)
})
```

The "how" examples help AI assistants match your exact patterns.

### What if my project has inconsistencies?

**Document the direction you want to go**:

```markdown
## File Naming

**Current state**: Mix of PascalCase and camelCase
**Going forward**: All new components should use PascalCase.tsx
**TODO**: Gradually migrate old files during refactors
```

This helps push toward consistency over time.

### Can I use this for non-Vite/Supabase projects?

**Absolutely!** This template is Vite + Supabase focused, but the concept works for any stack:

- Next.js + Firebase
- Django + PostgreSQL
- Rails + MySQL
- Express + MongoDB
- Flutter + AWS
- Whatever you're building!

Just adapt the sections to your stack.

---

## Team Questions

### How do we keep this in sync with multiple developers?

**Treat it like any other documentation**:

1. **PR Reviews**: Check that major changes are documented
2. **PR Template**: Add checkbox "Updated claude.md if needed"
3. **Quarterly review**: Schedule a review session every few months
4. **Make it easy**: Lower the barrier - quick updates are fine

**Anti-pattern**: Making it so formal that no one updates it

### What if team members disagree on conventions?

**Use this as a forcing function!**

When filling out claude.md, you'll discover disagreements:
- Person A uses default exports
- Person B uses named exports

**Resolution**: Have a quick discussion, pick one, document it, move on.

The act of documenting forces alignment.

### Should junior developers edit this?

**YES!** In fact, juniors often write the best context docs because they:
- Ask questions seniors assume are obvious
- Document gotchas they discover
- Write in beginner-friendly language

Encourage everyone to contribute.

### How do we prevent it from getting stale?

**Make it part of your workflow**:

**When opening a PR**:
- "Did this change introduce new patterns?"
- "Did I add a new table or integration?"
- "Did I discover a gotcha?"

If yes → update claude.md in the same PR

**Monthly check**:
- Skim through claude.md
- Remove outdated sections
- Add anything you've been meaning to document

**Keep it useful**:
If a section is always outdated, remove it. Better to have less that's accurate than more that's wrong.

---

## ROI Questions

### How much time does this actually save?

Hard to quantify, but here's what users report:

**Before**:
- 5-10 back-and-forth questions per task
- AI makes assumptions that don't match your stack
- Repetitive explanations of the same patterns

**After**:
- AI gets it right on first try (mostly)
- Fewer clarifying questions
- Consistent code that matches your style

**Rough estimate**: If you use AI for coding, this probably saves 20-30% of your interaction time.

**Time to create**: 5 minutes minimum, 1-2 hours for comprehensive

**Break-even**: After 5-10 AI coding sessions

### Does this help with onboarding new team members?

**Bonus benefit!** While designed for AI, humans love it too:

- New developers read it to understand the codebase
- Serves as supplementary onboarding material
- Answers common "how do we..." questions
- Points to where things are located

Some teams make it required reading on day 1.

### Can this replace other documentation?

**No, it's complementary**:

- **README**: User-facing, how to use/install
- **claude.md**: Developer-facing, how to work on it
- **API docs**: Endpoint specifications
- **Design docs**: Architecture decisions
- **Comments**: Code-level explanations

They all serve different purposes.

---

## Troubleshooting

### AI isn't following my claude.md guidelines

**Possible reasons**:

1. **File not in project root** - AI can't find it
2. **Too vague** - Make rules more specific with examples
3. **AI wasn't prompted to read it** - Some tools need explicit instruction
4. **File is too long** - AI may not read all of it

**Solutions**:
- Ensure file is at project root
- Add concrete examples, not just abstract principles
- Start conversations with "Read claude.md first"
- Keep it focused and concise

### My team isn't updating it

**Common causes**:

1. **Too formal** - Make updates casual and quick
2. **Not in workflow** - Add to PR template/checklist
3. **Not obviously valuable** - Share success stories
4. **Don't know what to add** - Provide examples

**Try**:
- "Updated claude.md" as PR checklist item
- Lead by example - update it yourself
- Share wins: "Claude got it right because of claude.md!"

### The file is getting too long

**Solutions**:

1. **Split by domain** - Frontend, backend, infrastructure
2. **Archive old sections** - Move outdated stuff to `claude-archive.md`
3. **Remove obvious things** - Don't document what's self-evident
4. **Use links** - Reference external docs instead of duplicating

**Example**:
```markdown
## Authentication

We use Supabase Auth. See [Supabase Auth Docs](https://supabase.com/docs/guides/auth) for basics.

**Our specific patterns**:
- Session stored in localStorage (Supabase default)
- Check auth status with useAuth() hook
- Protected routes use RequireAuth component
```

---

## Advanced Questions

### Can I auto-generate parts of this?

**Some parts yes, some no**:

**Can auto-generate**:
- Database schema (from migrations)
- API endpoints (from route files)
- Environment variables (from .env.example)
- Dependencies (from package.json)

**Can't auto-generate**:
- Why you made decisions
- Business logic and rules
- Gotchas and workarounds
- Team conventions

**Best approach**: Mix of auto + manual
- Script to extract database schema
- Manually add the context and "why"

### Should I have different claude.md for different AI tools?

**Usually no** - one file works for all AI tools.

**Exception**: If you use a tool with specific features:
- `claude.md` - General context
- `.cursorrules` - Cursor-specific settings
- `.github/copilot-instructions.md` - Copilot-specific

But the core context should be in one place.

### Can I make this private even in a public repo?

If you want to open-source your code but keep some context private:

**Option 1**: Keep sensitive context in a private doc
```markdown
## Internal Context

See internal wiki: [link to private docs]
```

**Option 2**: Two versions
- `claude.md` - Public, safe to share
- `claude-internal.md` - Private, in .gitignore

**Option 3**: Just don't include sensitive stuff
Most context is fine to share publicly!

---

## Still Have Questions?

**Open an issue**: [GitHub Issues](https://github.com/[your-repo]/issues)
**Start a discussion**: [GitHub Discussions](https://github.com/[your-repo]/discussions)
**Real-time help**: [Discord/Slack community]

We're here to help!
