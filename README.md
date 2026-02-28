# Ultimate claude.md Template

**Make AI assistants 10x more effective on your project in 5 minutes.**

This is a battle-tested template for creating a `claude.md` file that teaches AI assistants (like Claude) everything about your Vite + Supabase project. The more context you provide, the better the assistance you get.

## Why You Need This

Without a `claude.md` file, AI assistants:
- Don't know your project conventions
- Can't follow your patterns
- Make assumptions that don't match your setup
- Suggest solutions that don't fit your architecture
- Repeatedly ask the same questions

With this file, AI assistants:
- ✅ Know your tech stack and preferences
- ✅ Follow your established patterns
- ✅ Understand your database schema
- ✅ Respect your code style
- ✅ Make context-aware suggestions
- ✅ Work more autonomously

## Quick Start

### 1. Copy the template

```bash
# Download claude.md from this repo
curl -O https://raw.githubusercontent.com/[your-username]/claudemd/main/claude.md

# Or just copy/paste the content into your project root
```

### 2. Fill out the Quick Start section (5 minutes)

Open `claude.md` and fill out just the first section:
- What your app does
- Your tech stack choices
- Your database tables
- Your dev commands

That's it! You're already getting value.

### 3. Fill in more as you go

As your project grows, update sections:
- When you add a new database table → update Database Information
- When you make an architectural decision → add it to the file
- When you discover a gotcha → document it in Known Issues
- When you establish a pattern → add it to Code Conventions

## What Makes This Template Special

### 1. Progressive Disclosure
You don't need to fill everything out at once. Start with the basics, expand as needed.

### 2. Examples Everywhere
Not just `[placeholders]` - real examples show you exactly what to write.

### 3. User-Friendly Format
- Clear sections with emoji headers
- Checklists you can tick off
- "Delete what you don't use" approach
- Multiple choice options

### 4. AI-Optimized
Specifically designed for how AI assistants read and use context:
- Clear do's and don'ts
- Progressive complexity guide
- Code pattern examples
- Decision-making frameworks

### 5. Vite + Supabase Focused
Tailored for the popular Vite + Supabase stack with specific:
- Supabase query patterns
- RLS policy examples
- Migration workflows
- Real-time subscription guidance

## Real Impact

**Before claude.md**:
```
You: "Add a user profile page"
Claude: "Should I use Redux or Context for state?"
You: "We use Zustand"
Claude: "How should I structure the Supabase query?"
You: "Same pattern as the other queries"
Claude: "Where do components go?"
You: "In src/components"
```

**After claude.md**:
```
You: "Add a user profile page"
Claude: *Creates ProfilePage.tsx in src/pages/ with proper Zustand
        integration and Supabase error handling matching your patterns*
```

## What's Included

### Core Sections
- **Quick Start** - Fill this first (5 min)
- **Technology Stack** - Your tools and frameworks
- **Code Conventions** - How you write code
- **Database Info** - Schema and RLS patterns
- **Development Workflow** - Commands and processes
- **AI Guidelines** - How Claude should help you

### Advanced Sections
- **Design Guidelines** - UI patterns and components
- **Business Logic** - Domain-specific rules
- **Testing Strategy** - When you add tests
- **Deployment** - When you're ready to ship
- **Known Issues** - Gotchas and workarounds

## Usage Tips

### Start Small
Don't try to fill out everything on day one. Just do the Quick Start section.

### Update As You Go
Treat this as a living document:
- Made a decision? → Document it
- Fixed a tricky bug? → Add it to Known Issues
- Established a pattern? → Add it to conventions

### Delete Sections You Don't Need
Not using TypeScript? Delete those parts.
No tests yet? Remove the testing section until you add them.

### Customize Freely
This is YOUR file. Add sections that make sense for your project:
- Third-party API integrations
- Payment processing notes
- Email template locations
- Whatever helps Claude understand your project

## Examples of Good Entries

**Good Database Entry**:
```
**Table**: `posts`
- Purpose: User-created blog posts
- Key columns: id, user_id, title, content, published_at
- Access: Users can CRUD their own posts, read all published posts
- RLS: auth.uid() = user_id for mutations
```

**Good Business Logic Entry**:
```
**Post Publishing**:
- Users can save unlimited drafts
- Free users can publish max 3 posts
- Published posts can't be unpublished (only deleted)
- Deleting a post is soft-delete (sets deleted_at)
```

**Good Known Issue Entry**:
```
**Real-time subscriptions memory leak**:
- Issue: Subscriptions not cleaned up on component unmount
- Workaround: Always unsubscribe in useEffect cleanup
- Fix planned: Create useRealtimeSubscription hook
```

## Advanced: Multiple Environments

If you have different setups for dev/staging/prod, add a section:

```markdown
## Environments

**Development** (local):
- Uses local Supabase (supabase start)
- Seed data automatically loaded
- All RLS policies disabled for easier testing

**Staging** (staging.yourapp.com):
- Connected to staging Supabase project
- Anonymized production data
- Stripe test mode

**Production** (yourapp.com):
- Production Supabase project
- Stripe live mode
- RLS strictly enforced
```

## Integration with AI Tools

### Claude Desktop / API
Just have `claude.md` in your project root. Claude will automatically read it.

### GitHub Copilot
While Copilot doesn't read claude.md directly, the standardized patterns help Copilot suggestions align better.

### Cursor / Windsurf
These tools will pick up claude.md and use it for context.

## 📚 Full Documentation

This project includes comprehensive guides for every use case:

### Getting Started
- **[START_HERE.md](START_HERE.md)** - Choose your path based on what you need
- **[FILL_OUT_GUIDE.md](FILL_OUT_GUIDE.md)** - 5-minute step-by-step fill-out guide
- **[MIGRATION_GUIDE.md](MIGRATION_GUIDE.md)** - Add claude.md to existing projects
- **[example.claude.md](example.claude.md)** - Real-world example (recipe app)

### Reference
- **[QUICK_REFERENCE.md](QUICK_REFERENCE.md)** - Bookmark this! Cheat sheet for ongoing use
- **[FAQ.md](FAQ.md)** - Frequently asked questions
- **[ADVANCED.md](ADVANCED.md)** - Advanced sections (integrations, monitoring, etc.)

### Project Info
- **[CONTRIBUTING.md](CONTRIBUTING.md)** - How to contribute improvements
- **[CHANGELOG.md](CHANGELOG.md)** - Version history
- **[LICENSE](LICENSE)** - MIT License

**Not sure where to start?** Open [START_HERE.md](START_HERE.md) - it will guide you to the right place.

## Contributing

This template is open-source and community-driven.

**Found it useful?** Star the repo!

**Have improvements?**
- Read [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines
- Check [existing issues](https://github.com/[your-repo]/issues)
- Submit a PR with your improvements

**Ideas for future versions**:
- [ ] Stack-specific variants (Next.js, Django, Rails, etc.)
- [ ] CLI tool to generate customized templates
- [ ] VS Code extension for easy updates
- [ ] More real-world examples from popular open-source projects
- [ ] Video walkthrough series
- [ ] Community showcase

## License

MIT - Use freely, modify, share, sell, do whatever you want with it.

## Credits

Created for the developer community to make working with AI assistants more effective.

**Version**: 2.0 - User-Friendly Edition
**Stack**: Vite + Supabase
**Maintained by**: [Your name/team]

---

**Questions?** Open an issue or discussion.
**Success story?** Share it! We'd love to hear how this helped your project.

---

Made with ❤️ for developers building with AI
