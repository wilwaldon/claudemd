# claude.md Quick Reference

**Bookmark this page for quick lookup while working on your project!**

---

## 🚀 When Starting a New Project

1. Copy `claude.md` to project root
2. Fill out Quick Start (5 min):
   - What your app does
   - Tech stack (delete what you don't use)
   - Database tables
   - Dev commands
3. Start coding, update as you go

---

## ✏️ What to Update & When

### ✅ Always Update For

| When you... | Update this section |
|-------------|---------------------|
| Add a database table | Database Information |
| Add a new dependency | Technology Stack |
| Make an architectural decision | Architecture & Design |
| Establish a code pattern | Code Conventions |
| Add a third-party integration | Third-Party Integrations |
| Discover a gotcha/workaround | Known Issues |
| Change deployment setup | Deployment |
| Add a business rule | Business Logic |
| Create a new environment | Environment Variables |

### ❌ Don't Update For

- Regular bug fixes
- Small code changes
- Typos in code
- Daily work
- Obvious things

**Rule of thumb**: Would you tell a new team member about this? If yes, add it.

---

## 📋 Copy-Paste Templates

### Database Table Entry
```markdown
**Table**: `table_name`
- Purpose: [what this stores]
- Key columns: [important columns]
- Access: [who can read/write]
- RLS: [your RLS rule]
```

### Feature Entry
```markdown
**Feature**: [Name]
- What it does: [brief description]
- How it works: [technical details]
- Important: [gotchas or special rules]
```

### Known Issue Entry
```markdown
**[Issue Title]**:
- Problem: [what's wrong]
- Impact: [how it affects users]
- Workaround: [temporary solution]
- Fix planned: [yes/no, when]
```

### Integration Entry
```markdown
### [Service Name]
- **What we use**: [specific feature]
- **Where**: [file location]
- **Important**:
  - [key point 1]
  - [key point 2]
```

### User Flow Entry
```markdown
**[Flow Name]**:
1. [Step 1]
2. [Step 2]
3. [Step 3]
Result: [outcome]
```

---

## 🎯 Sections Priority Guide

### Must Have (Fill First)
1. **Project Overview** - What your app does
2. **Technology Stack** - What you're building with
3. **Development Commands** - How to run it
4. **Database Tables** - What data you store
5. **One Important Rule** - Most critical thing to know

### Should Have (Add Soon)
6. **Code Conventions** - How you write code
7. **Known Issues** - Current gotchas
8. **Business Logic** - Key rules and constraints
9. **Environment Variables** - What's needed to run

### Nice to Have (Add When Relevant)
10. **User Flows** - How users navigate
11. **Testing Strategy** - How you test
12. **Deployment** - How you ship
13. **Third-Party Integrations** - External services
14. **Performance** - Optimization notes

### Advanced (Only If Needed)
15. Feature flags
16. Background jobs
17. Webhooks
18. Email templates
19. Monitoring setup
20. Security policies

---

## 🔍 Quick Checks

### Is My claude.md Good?

**Green flags** ✅:
- [ ] Can be read in < 5 minutes
- [ ] Has concrete examples (not just placeholders)
- [ ] Includes real code patterns
- [ ] Explains *why* not just *what*
- [ ] Updated in last month
- [ ] No secrets or API keys

**Red flags** ❌:
- [ ] All sections are `[TODO]` or `[Fill in]`
- [ ] No examples, just abstract rules
- [ ] Out of date (references old stack)
- [ ] Contains API keys or secrets
- [ ] Too long (10+ pages of fluff)
- [ ] Just restates what's obvious from code

### Is This Worth Adding?

Ask yourself:
1. **Would AI get this wrong without documentation?** → Yes = Add it
2. **Is this repeated across the codebase?** → Yes = Add it
3. **Is it a gotcha you keep forgetting?** → Yes = Add it
4. **Would a new teammate ask about this?** → Yes = Add it
5. **Is it obvious from the code?** → Yes = Skip it

---

## 💡 Quick Examples

### Good Entry (Specific & Useful)
```markdown
**Supabase Query Pattern**:
```typescript
const { data, error } = await supabase
  .from('recipes')
  .select('id, title, user_id')

if (error) {
  console.error('Error:', error)
  throw new Error('Failed to fetch recipes')
}

return data
```

Always check error, never ignore the error property.
```

### Bad Entry (Too Vague)
```markdown
**Database**: We use Supabase for data storage.
Handle errors properly.
```

### Good Entry (Actionable Context)
```markdown
**Image Uploads**:
- Max size: 5MB (enforced client-side in useUpload hook)
- Allowed types: jpg, png, webp
- Stored in 'recipe-images' bucket (public)
- Always compress before upload using compressImage() utility
- Never store as base64 in database
```

### Bad Entry (Not Helpful)
```markdown
**Images**: Use Supabase Storage for images.
```

---

## 🛠️ Maintenance Schedule

### Weekly
- [ ] Nothing! Don't overthink it.

### After Each Feature
- [ ] Quick check: Did I add a new pattern? → Document it

### Monthly
- [ ] Skim through claude.md (5 min)
- [ ] Remove outdated info
- [ ] Add anything you've been meaning to document

### Quarterly
- [ ] Team review session (30 min)
- [ ] Update technology stack if changed
- [ ] Verify examples still work
- [ ] Remove completed TODOs

### Yearly
- [ ] Full audit (1 hour)
- [ ] Major cleanup
- [ ] Reorganize if needed
- [ ] Archive old sections

---

## 🚨 Common Mistakes

### Mistake 1: Over-documenting
**Problem**: Every tiny detail is documented
**Fix**: Only document what's non-obvious or AI would get wrong

### Mistake 2: Under-documenting
**Problem**: Just has "TODO" everywhere
**Fix**: Spend 5 minutes filling Quick Start at minimum

### Mistake 3: Out of date
**Problem**: References old stack, deprecated patterns
**Fix**: Monthly quick review to keep current

### Mistake 4: Too abstract
**Problem**: "Write clean code" - no concrete examples
**Fix**: Show actual code patterns with examples

### Mistake 5: Contains secrets
**Problem**: Has API keys or database URLs
**Fix**: Never commit secrets! Use .env.example instead

---

## 🎓 Advanced Tips

### Tip 1: Use AI to Help Fill It Out
```
Prompt: "Look at my codebase and help me fill out the
'Code Conventions' section of my claude.md file.
Analyze my existing components and tell me what
patterns I'm using."
```

### Tip 2: Link to External Docs
```markdown
## Authentication

We use Supabase Auth - see [their docs](https://supabase.com/docs/guides/auth) for basics.

**Our specific approach**:
- Session in localStorage
- Check auth with useAuth() hook
- Protected routes use <RequireAuth> wrapper
```

### Tip 3: Version Control Gotchas
```markdown
## Known Issues

**Supabase real-time breaks on connection loss**
- Issue discovered: 2025-01-15
- Ticket: #234
- Workaround: Manual page refresh for now
- Fix planned: Implementing auto-reconnect in Q1
```

### Tip 4: Progressive Disclosure
Start simple, expand sections as project grows:

**Week 1**: Just Quick Start
**Month 1**: Add Code Conventions, Database Info
**Month 3**: Add Business Logic, User Flows
**Month 6**: Add Advanced sections as needed

### Tip 5: Team Ownership
Assign sections to experts:
- Backend lead → Database, API patterns
- Frontend lead → Component patterns, UI
- DevOps → Deployment, environments
- Product → Business logic, user flows

---

## 📚 Resources

**Main Docs**:
- [Full README](README.md) - Project overview
- [Fill-Out Guide](FILL_OUT_GUIDE.md) - Step-by-step
- [Migration Guide](MIGRATION_GUIDE.md) - For existing projects
- [Advanced Techniques](ADVANCED.md) - Power user features
- [FAQ](FAQ.md) - Common questions

**Examples**:
- [example.claude.md](example.claude.md) - Real-world recipe app

**Contributing**:
- [CONTRIBUTING.md](CONTRIBUTING.md) - How to contribute

---

## 🎯 TL;DR - Just Do This

**Absolute minimum** (5 minutes):
1. Copy claude.md to your project
2. Fill out "Quick Start" section
3. Update when you add tables/integrations/patterns
4. Done!

That's it. Don't overcomplicate it.

---

**Save this page**: You'll reference it often as you maintain your claude.md file!
