# Advanced claude.md Techniques

Once you have the basics down, these advanced sections can make AI assistance even more powerful.

## 🔌 Third-Party Integrations

### Why Document This
AI assistants need to know how you integrate with external services to avoid conflicts and follow your patterns.

### Template

```markdown
## Third-Party Integrations

### Stripe (Payments)
- **What we use**: Stripe Checkout for subscriptions
- **Where**: `lib/stripe.ts` handles all Stripe logic
- **Webhooks**: `/api/webhooks/stripe` endpoint
- **Important**:
  - Always use test mode keys in development
  - Webhook secret must be configured in .env
  - Don't create checkout sessions client-side

**Pattern**:
```typescript
// Create checkout on server, redirect on client
const session = await createCheckoutSession(priceId)
window.location.href = session.url
```

### SendGrid (Email)
- **What we use**: Transactional emails only (no marketing)
- **Where**: `lib/email.ts` with templates in `email-templates/`
- **Important**:
  - All emails must have unsubscribe link
  - Use dynamic templates (not HTML in code)
  - Never send to unverified emails

### Sentry (Error Tracking)
- **What we use**: Error and performance monitoring
- **Where**: Initialized in `main.tsx`
- **Important**:
  - Don't log PII (emails, names, etc.)
  - Use custom contexts for user feedback
  - Set environment tags (dev/staging/prod)
```

---

## 📊 Observability & Monitoring

```markdown
## Monitoring & Observability

### Error Tracking
- **Tool**: Sentry
- **What we track**: All uncaught errors, failed API calls, performance issues
- **What we DON'T track**: User PII, authentication tokens
- **Custom events**: Payment failures, upload failures

### Analytics
- **Tool**: PostHog (self-hosted)
- **Events we track**:
  - User sign up
  - Recipe created/published/deleted
  - Recipe saved/unsaved
  - Image uploaded
- **Privacy**: IP anonymization enabled, no personal data

### Performance
- **Tool**: Vercel Analytics + Web Vitals
- **Budgets**:
  - First Contentful Paint: < 1.8s
  - Largest Contentful Paint: < 2.5s
  - Total Blocking Time: < 200ms
  - Cumulative Layout Shift: < 0.1

### Logging
- **Development**: Console logs are fine
- **Production**: Use Sentry for errors, PostHog for events
- **Never log**: Passwords, tokens, API keys, PII
```

---

## 🌍 Internationalization (i18n)

```markdown
## Internationalization

### Current Status
- [ ] Not implemented yet
- [x] Planned for Q2 2025
- [ ] Fully implemented

### Approach (when we implement)
- **Library**: react-i18next
- **Languages**: English (default), Spanish, French
- **Where translations live**: `public/locales/{lang}/translation.json`
- **Date/number formatting**: Use native Intl API

### Important Rules
- All user-facing text must be in translation files (no hardcoded strings)
- Use keys like `recipe.title` not generic `title`
- Include context comments in translation files
- Right-to-left (RTL) support: Not yet, maybe future

**Example**:
```typescript
// Good
t('recipe.delete.confirm')

// Bad (hardcoded)
'Are you sure you want to delete this recipe?'
```
```

---

## 🎯 Feature Flags

```markdown
## Feature Flags

### Why We Use Them
- Test features with small user groups
- Roll out changes gradually
- Quick rollback if issues arise

### Tool
- **Current**: Environment variables (simple on/off)
- **Future**: PostHog feature flags (percentage rollouts)

### Active Flags

**ENABLE_AI_RECIPE_GENERATION**
- What: AI-powered recipe generation feature
- Status: Beta, 10% of users
- Location: Check in `lib/features.ts`
- Plan: Full rollout in March 2025

**ENABLE_RECIPE_COLLECTIONS_V2**
- What: New collections UI with drag-and-drop
- Status: Development, disabled in production
- Location: `features/collections/v2/`
- Plan: Testing in staging

### Pattern
```typescript
import { isFeatureEnabled } from '@/lib/features'

if (isFeatureEnabled('ENABLE_AI_RECIPE_GENERATION')) {
  // Show AI generation UI
}
```

### Important
- Never remove a flag without checking all code references
- Document why each flag exists
- Set removal dates for old flags
```

---

## 📱 Mobile Considerations

```markdown
## Mobile Support

### Responsive Design
- **Approach**: Mobile-first design with Tailwind breakpoints
- **Breakpoints**: sm (640px), md (768px), lg (1024px), xl (1280px)
- **Testing**: Chrome DevTools + real devices (iPhone 12, Pixel 5)

### Progressive Web App (PWA)
- **Status**: Planned, not implemented
- **Features**:
  - [ ] Offline recipe viewing
  - [ ] Add to home screen
  - [ ] Push notifications for saved recipes

### Mobile-Specific Rules
- All touch targets minimum 44x44px
- No hover-only interactions
- Image optimization critical (slow connections)
- Test on slow 3G network throttling

### Known Mobile Issues
- Image upload on iOS Safari sometimes fails (investigating)
- Landscape mode on tablets has layout issues
- Recipe scaling UI cramped on small screens
```

---

## 🔐 Security Policies

```markdown
## Security Policies

### Authentication
- **Method**: Supabase Auth (email + OAuth)
- **Session storage**: LocalStorage (auto-managed by Supabase)
- **Session duration**: 7 days
- **Refresh token rotation**: Enabled

### Authorization
- **Approach**: Row Level Security (RLS) on all tables
- **Never**: Check permissions client-side only
- **Always**: Rely on RLS policies for data access control

### Data Protection

**PII (Personally Identifiable Information)**:
- Email addresses: Stored in auth.users (encrypted by Supabase)
- Display names: Stored in profiles table
- User-generated content: Recipes, collections

**What we NEVER do**:
- ❌ Store passwords (Supabase handles this)
- ❌ Log authentication tokens
- ❌ Expose service_role key client-side
- ❌ Send PII to analytics services
- ❌ Store credit card data (Stripe handles this)

**Rate Limiting**:
- Supabase built-in rate limiting (60 requests/min per IP)
- Custom: Image uploads (5 per minute per user)

### Content Security Policy (CSP)
```javascript
// vite.config.ts
headers: {
  'Content-Security-Policy':
    "default-src 'self'; img-src 'self' https://*.supabase.co data:; ..."
}
```

### Vulnerability Scanning
- **Tool**: Dependabot (GitHub)
- **Frequency**: Weekly
- **Action**: Review and update dependencies monthly
```

---

## 🎨 Design System

```markdown
## Design System

### Component Library
- **Base**: shadcn/ui (Radix UI primitives)
- **Custom components**: `src/components/recipes/`
- **Icons**: Lucide React

### Design Tokens

**Colors**:
```javascript
// tailwind.config.js
colors: {
  primary: colors.orange,
  secondary: colors.slate,
  success: colors.green[500],
  error: colors.red[500],
  warning: colors.yellow[500],
}
```

**Typography**:
- Font family: Inter (from Google Fonts)
- Headings: font-bold, tracking-tight
- Body: font-normal, leading-relaxed

**Spacing**:
- Use Tailwind spacing scale
- Component internal padding: p-4 or p-6
- Section spacing: space-y-8 or space-y-12

### Component Checklist

When creating new components, ensure:
- [ ] Accessible (ARIA labels, keyboard navigation)
- [ ] Responsive (works on mobile, tablet, desktop)
- [ ] Dark mode support
- [ ] Loading states
- [ ] Error states
- [ ] Empty states

### Accessibility Standards
- **Target**: WCAG 2.1 Level AA
- **Color contrast**: Minimum 4.5:1 for text
- **Focus indicators**: Visible on all interactive elements
- **Screen reader**: Test with VoiceOver (Mac) or NVDA (Windows)
```

---

## 🔄 Background Jobs & Scheduled Tasks

```markdown
## Background Jobs

### What We Use
- **Tool**: Supabase Edge Functions + pg_cron
- **Location**: `supabase/functions/`

### Active Jobs

**Job**: Daily recipe engagement digest
- **Schedule**: Every day at 8am UTC
- **What**: Sends email to users with new recipes from followed creators
- **Function**: `supabase/functions/daily-digest/`
- **Important**: Respects user email preferences

**Job**: Cleanup abandoned uploads
- **Schedule**: Every hour
- **What**: Deletes images uploaded but not attached to recipes after 24h
- **Function**: SQL function called by pg_cron

**Job**: Update recipe trending scores
- **Schedule**: Every 15 minutes
- **What**: Recalculates trending score based on views/saves/recency
- **Implementation**: Database function

### Pattern for Adding New Jobs

1. Create Edge Function in `supabase/functions/`
2. Add cron schedule in migration:
```sql
SELECT cron.schedule(
  'job-name',
  '0 8 * * *',  -- cron schedule
  $$SELECT net.http_post(
    url := 'https://yourproject.supabase.co/functions/v1/your-function',
    headers := '{"Authorization": "Bearer ' || current_setting('app.service_role_key') || '"}'
  ) AS request_id;$$
);
```
3. Document it in this section
```

---

## 🔗 Webhooks

```markdown
## Webhooks

### Incoming Webhooks (We Receive)

**Stripe**:
- **Endpoint**: `/api/webhooks/stripe`
- **Events**:
  - `checkout.session.completed` → Create subscription
  - `customer.subscription.deleted` → Cancel subscription
- **Verification**: Stripe signature verification required
- **Important**: Always acknowledge webhook quickly (< 5s), process async

**Supabase Auth**:
- **Endpoint**: `/api/webhooks/auth`
- **Events**:
  - `user.created` → Create profile record
  - `user.deleted` → Cleanup user data
- **Verification**: Supabase JWT signature

### Outgoing Webhooks (We Send)

**Recipe Published**:
- **When**: User publishes a recipe
- **Payload**: `{ event: 'recipe.published', recipe_id, user_id, published_at }`
- **Who receives**: Integrations that user has connected (Zapier, etc.)

### Webhook Security
- Always verify signatures
- Use HTTPS only
- Retry failed webhooks (3x with exponential backoff)
- Log all webhook attempts
```

---

## 📧 Email Templates

```markdown
## Email System

### Email Provider
- **Service**: SendGrid
- **Templates**: Dynamic templates in SendGrid dashboard
- **Location of template IDs**: `lib/email-templates.ts`

### Email Types

**Transactional** (always sent):
- Welcome email (template: `d-abc123`)
- Email verification (Supabase default)
- Password reset (Supabase default)
- Recipe published confirmation (template: `d-def456`)

**Marketing** (opt-in):
- Weekly recipe digest (template: `d-ghi789`)
- New followers notification (template: `d-jkl012`)

### Email Rules
- All marketing emails must have one-click unsubscribe
- Never send more than 1 marketing email per day per user
- Check user preferences before sending: `profiles.email_preferences`
- All emails must render well on mobile

### Testing Emails
```bash
# Development: Use Ethereal (fake SMTP)
# Staging: Send to @company.com addresses only
# Production: Real emails
```

### Email Preferences Schema
```sql
-- In profiles table
email_preferences jsonb DEFAULT '{
  "weekly_digest": true,
  "new_followers": true,
  "recipe_comments": true
}'
```
```

---

## 🧪 Testing Strategy (Advanced)

```markdown
## Advanced Testing

### Test Coverage Goals
- **Utilities**: 90%+ coverage
- **Components**: 70%+ coverage
- **E2E critical flows**: 100% (sign up, publish recipe, payments)

### Testing Pyramid
```
     /\
    /E2E\      ← Few (5-10 tests, critical flows)
   /------\
  /  Integ \   ← Some (20-30 tests, feature flows)
 /----------\
/   Unit     \ ← Many (100+ tests, utilities/hooks)
--------------
```

### What We Mock

**Always mock**:
- Supabase client (use msw)
- External API calls (Stripe, SendGrid)
- File uploads
- Environment variables

**Never mock**:
- Utility functions
- React hooks (test real behavior)
- Component logic

### E2E Testing (Playwright)

**Critical flows we test**:
1. User sign up → verify email → complete profile → create first recipe
2. User saves recipe → adds to collection → removes from collection
3. User upgrades to paid → publishes recipe → cancels subscription

**Test data**:
- Use separate test database (not production!)
- Reset database before each test run
- Seed with predictable test data

### Visual Regression Testing
- **Tool**: Percy (plan to add)
- **What**: Screenshot key pages, detect unintended visual changes
- **When**: On every PR

### Performance Testing
```bash
# Lighthouse CI runs on every deploy
npm run lighthouse:ci

# Budgets in lighthouserc.json:
# - Performance: 90+
# - Accessibility: 95+
# - Best Practices: 90+
# - SEO: 90+
```
```

---

## 🎛️ Environment-Specific Configs

```markdown
## Environments

### Development (Local)
- **Supabase**: Local instance via `supabase start`
- **Database**: Seeded with fake data
- **Emails**: Ethereal (fake SMTP, view at ethereal.email)
- **Payments**: Stripe test mode
- **Analytics**: Disabled
- **Error tracking**: Console only

**URL**: http://localhost:5173

### Staging
- **Supabase**: Dedicated staging project
- **Database**: Copy of production (anonymized)
- **Emails**: Only to @company.com addresses
- **Payments**: Stripe test mode
- **Analytics**: PostHog test project
- **Error tracking**: Sentry (staging environment)

**URL**: https://staging.recipeapp.com

### Production
- **Supabase**: Production project
- **Database**: Live data with RLS enforced
- **Emails**: Real emails via SendGrid
- **Payments**: Stripe live mode
- **Analytics**: PostHog production
- **Error tracking**: Sentry (production environment)

**URL**: https://recipeapp.com

### Environment Variables by Environment

| Variable | Dev | Staging | Production |
|----------|-----|---------|------------|
| VITE_SUPABASE_URL | localhost:54321 | staging.supabase.co | prod.supabase.co |
| VITE_ENABLE_ANALYTICS | false | true | true |
| VITE_STRIPE_KEY | pk_test_... | pk_test_... | pk_live_... |
```

---

## When to Use These Advanced Sections

**Add them when**:
- ✅ You actually implement the feature (not before)
- ✅ The complexity justifies documentation
- ✅ It would save AI assistants (or humans) from making mistakes
- ✅ Multiple people need to understand it

**Don't add them if**:
- ❌ You're just planning (document when you build)
- ❌ It's obvious from the code
- ❌ It's standard practice (no need to document "we use git")

Keep your claude.md practical and current!
