# Contributing to claude.md Template

Thanks for your interest in improving this template! This is a community-driven project, and we welcome contributions from everyone.

## Ways to Contribute

### 1. Share Your Experience
- ⭐ Star the repo if you find it useful
- 📢 Share it with your network
- 💬 Tell us how you're using it
- 📸 Share screenshots of your filled-out claude.md

### 2. Report Issues
- 🐛 Found a typo or error
- 🤔 Something confusing
- 💡 Have a suggestion
- 📝 Missing an important section

→ [Open an issue](https://github.com/[your-repo]/issues)

### 3. Improve the Template
- ✨ Add new sections
- 📚 Improve examples
- 🔧 Better explanations
- 🌍 Translations to other languages

→ Submit a Pull Request

### 4. Create Variations
- 🎨 Design for other stacks (Next.js, Django, etc.)
- 🏢 Industry-specific versions (SaaS, e-commerce, etc.)
- 🛠️ Tools (CLI generator, VS Code extension)

→ Share with the community

---

## Contributing Guidelines

### Before You Start

**Check existing issues/PRs**: Someone might already be working on it

**Open an issue first** (for major changes): Discuss the idea before spending time on it

**Small improvements**: Just submit a PR, no issue needed

### Making Changes

#### 1. Fork & Clone

```bash
# Fork the repo on GitHub, then:
git clone https://github.com/YOUR_USERNAME/claudemd.git
cd claudemd
```

#### 2. Create a Branch

```bash
git checkout -b feature/your-feature-name
# or
git checkout -b fix/issue-you-are-fixing
```

**Branch naming**:
- `feature/add-nextjs-section`
- `fix/typo-in-readme`
- `docs/improve-faq`
- `example/django-template`

#### 3. Make Your Changes

**When editing the template (`claude.md`)**:
- Keep it beginner-friendly
- Add concrete examples, not just placeholders
- Use clear, simple language
- Include `[brackets]` for things users should fill in
- Test that markdown renders correctly

**When editing docs (`README.md`, `FAQ.md`, etc.)**:
- Clear, concise writing
- Use examples to illustrate points
- Add links where helpful
- Keep tone friendly and encouraging

**When adding examples**:
- Use realistic project scenarios
- Fill it out as if it were a real project
- Show the right level of detail (not too much, not too little)
- Comment on what makes it a good example

#### 4. Test Your Changes

**For template changes**:
- [ ] Markdown renders correctly
- [ ] Examples are accurate
- [ ] No broken links
- [ ] Placeholders clearly marked with `[brackets]`
- [ ] Works for different tech stacks

**For documentation**:
- [ ] Links work
- [ ] Examples are clear
- [ ] No typos (use a spell checker)
- [ ] Formatting is consistent

#### 5. Commit Your Changes

```bash
git add .
git commit -m "Add clear, descriptive commit message"
```

**Good commit messages**:
- `Add PostgreSQL-specific database section`
- `Fix typos in FAQ.md`
- `Improve examples in Advanced.md`
- `Add Next.js variant of template`

**Bad commit messages**:
- `Update stuff`
- `Fix`
- `Changes`

#### 6. Push & Create PR

```bash
git push origin feature/your-feature-name
```

Then create a Pull Request on GitHub.

### Pull Request Guidelines

**PR Title**: Clear and descriptive
- ✅ "Add section for third-party API integrations"
- ✅ "Fix broken links in README"
- ❌ "Updates"
- ❌ "Changes to template"

**PR Description**: Explain what and why

```markdown
## What

Added a new section for documenting third-party API integrations (Stripe, SendGrid, etc.)

## Why

Many projects use external APIs, and AI assistants need to know how we integrate with them to avoid conflicts and suggest the right patterns.

## Changes

- Added "Third-Party Integrations" section to claude.md
- Added examples for Stripe, SendGrid, and Sentry
- Updated table of contents

## Testing

- Verified markdown renders correctly
- Checked examples are accurate
- Tested with real project to ensure it's useful
```

**Checklist** (included in PR template):
- [ ] Markdown renders correctly
- [ ] Examples are accurate and tested
- [ ] Documentation updated if needed
- [ ] No broken links
- [ ] Spellchecked

---

## Specific Contribution Types

### Adding a New Section to the Template

**Good new sections**:
- Solve a common need (many projects would use it)
- AI-relevant (helps AI assistants work better)
- Not too specific (avoid ultra-niche needs)
- Well-documented with examples

**Template for new section**:
```markdown
## [Section Name]

### Why Document This
[1-2 sentences explaining why this matters for AI assistance]

### Template

```markdown
[The actual template with examples and placeholders]
```

### When to Use This
[Guidance on when this section is relevant]
```

### Improving Existing Content

**Areas that always need improvement**:
- Clarity of explanations
- Quality of examples
- Removing outdated info
- Fixing typos/grammar
- Adding missing details

**How to improve**:
1. Identify what's confusing or unclear
2. Propose a better version
3. Explain why it's better in your PR

### Creating Stack-Specific Variants

Want to create a version for a different tech stack? Awesome!

**Popular requests**:
- Next.js + Firebase
- Django + PostgreSQL
- Rails + Hotwire
- Vue + Pinia
- Laravel + Inertia

**What to do**:
1. Copy `claude.md` as `claude-[stack].md`
2. Adapt for your stack
3. Update examples and patterns
4. Test with a real project
5. Submit PR or create a new repo

**If creating a new repo**:
- Link back to this original template
- Maintain the same spirit and structure
- Share it with us so we can link to it!

### Writing Better Examples

**What makes a good example**:
- ✅ Realistic (could be from a real project)
- ✅ Complete (enough context to understand)
- ✅ Not too complex (simple enough to grasp quickly)
- ✅ Demonstrates best practices

**Example of a good example**:
```typescript
// Good: Shows the full pattern with context
const { data, error } = await supabase
  .from('recipes')
  .select('id, title, user_id, created_at')
  .eq('user_id', userId)

if (error) {
  console.error('Failed to fetch recipes:', error)
  throw new Error('Could not load recipes')
}

return data
```

**Example of a bad example**:
```typescript
// Bad: Too vague, no context
const data = await fetch()
```

### Translating to Other Languages

Want to translate this to another language?

**Steps**:
1. Create `README.[language-code].md` (e.g., `README.es.md` for Spanish)
2. Translate all content
3. Keep code examples in English (universal)
4. Test that markdown renders correctly
5. Submit PR

**Languages we'd love**:
- Spanish (es)
- French (fr)
- German (de)
- Japanese (ja)
- Chinese (zh)
- Portuguese (pt)

---

## Code of Conduct

### Our Standards

**We encourage**:
- 🤝 Being welcoming and inclusive
- 💡 Sharing knowledge generously
- 🎯 Focusing on what's best for the community
- 👂 Listening to feedback with an open mind
- 🙏 Showing empathy toward others

**We don't tolerate**:
- ❌ Harassment or discriminatory language
- ❌ Trolling or insulting comments
- ❌ Spam or self-promotion
- ❌ Publishing others' private information

### Enforcement

Violations may result in:
1. Warning
2. Temporary ban
3. Permanent ban

Report violations to: [your email]

---

## Recognition

### Contributors

All contributors will be:
- Listed in CONTRIBUTORS.md
- Mentioned in release notes (for significant contributions)
- Given credit in the README

### Types of Contributions We Recognize

Not just code! We value:
- 📝 Documentation improvements
- 🐛 Bug reports
- 💡 Ideas and suggestions
- 🎨 Design improvements
- 📢 Spreading the word
- 🧪 Testing and feedback
- ❓ Answering questions in issues/discussions

---

## Development Setup

This is a documentation project (no code to run), but here's how to work on it:

### Prerequisites
- Git
- A markdown editor (VS Code recommended)
- GitHub account

### Recommended Tools

**VS Code Extensions**:
- `yzhang.markdown-all-in-one` - Markdown support
- `davidanson.vscode-markdownlint` - Linting
- `streetsidesoftware.code-spell-checker` - Spell checking

**Markdown Preview**:
```bash
# In VS Code: Cmd/Ctrl + Shift + V to preview
```

### File Structure

```
claudemd/
├── claude.md              # Main template
├── README.md              # Project documentation
├── FILL_OUT_GUIDE.md     # Quick start guide
├── MIGRATION_GUIDE.md    # For existing projects
├── ADVANCED.md           # Advanced sections
├── FAQ.md                # Frequently asked questions
├── CONTRIBUTING.md       # This file
├── example.claude.md     # Real-world example
├── .env.example          # Environment variables template
└── LICENSE               # MIT License
```

---

## Release Process

**Versioning**: We use semantic versioning
- Major: Breaking changes to template structure
- Minor: New sections or significant improvements
- Patch: Fixes, typos, small improvements

**Release Schedule**: As needed (no fixed schedule)

**How releases happen**:
1. Merge PRs into main
2. Update CHANGELOG.md
3. Create GitHub release
4. Announce in discussions

---

## Getting Help

**Questions about contributing?**
- 💬 Open a discussion: [Discussions](https://github.com/[your-repo]/discussions)
- 📧 Email: [your-email]
- 💡 Not sure what to work on? Check [Good First Issues](https://github.com/[your-repo]/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22)

**Want to help but don't know where to start?**

Easy wins:
- Fix typos
- Improve examples
- Add missing links
- Share your experience in discussions
- Test the template with your project and report feedback

---

## Thank You!

Every contribution, no matter how small, makes this template better for everyone. We appreciate you taking the time to improve this project.

**Special thanks** to all our contributors! 🎉

Want to see your name here? Make your first contribution today!

---

**Happy Contributing!** 🚀
