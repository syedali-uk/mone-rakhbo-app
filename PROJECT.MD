# Mone Rakhবো – Project Plan

**Domain:** monerakhbo.com
**Working name:** mone-rakhbo-app

A scheduled reminder and message-sending service, primarily for people in Bangladesh, focused on not forgetting important dates (birthdays, anniversaries, reminders), with a simple, mobile-first experience.

---

## 1. Product Summary

Mone Rakhবো allows users to schedule reminders or messages in advance. On the scheduled date, the system will either:

- Remind the sender, or
- Send a predefined or custom message (e.g. birthday wishes) to a recipient

**Primary goals:**

- Simple
- Reliable
- Mobile-first
- Friendly for non-technical users
- Culturally relevant to Bangladesh

---

## 2. Target Users

- Individuals in Bangladesh
- Primarily mobile users
  - Android (Chrome)
  - iOS (Mobile Safari)
- Desktop usable, but mobile is the priority
- Non-technical users
- People who frequently forget important dates

---

## 3. Core User Flow

### 3.1 Authentication

- Email + password
- Email verification required
- 2FA via email code when cookie is not present (limited initially to reduce friction)

### 3.2 Create Message

- Select message type:
  - Reminder to self
  - Message to recipient
- Choose template (optional)
- Add custom message (optional, template-dependent)
- Add recipient details:
  - Email (required for now)
  - Mobile number (future)

### 3.3 Message Configuration

- Option: "Send me a reminder" (this is a self-reminder feature, separate from e-card functionality)
- Optional recipient relationship (mum, dad, sister, brother, uncle, etc.)
- Optional recipient timezone

### 3.4 Scheduling

- Select date only (no time picker)
- Default send time:
  - 00:00 recipient timezone
  - If timezone not provided → UTC
- Clear warning/help text explaining this

### 3.5 Preview & Confirmation

- Final preview
- Confirm send

### 3.6 Dashboard

- List of all scheduled and sent messages
- Must be very easy to view on mobile
- Status indicators:
  - Scheduled
  - Sent
  - Failed
  - Opened (email only, with caveat: "where possible" due to Apple Mail Privacy Protection)

---

## 4. Features (Current Scope)

### 4.1 Messaging Channels

- Email (initial)
- SMS (future)
- WhatsApp (future)

### 4.2 Templates

- Predefined templates (birthdays, reminders, etc.)
- Templates may allow limited custom text
- Animated templates (email-safe only)
- Text/HTML initially (image templates in future)
- Must have: recipient name, sender name, and message where relevant
- Tokens: `{{name}}` and `{{message}}` where applicable

### 4.3 Language & Localisation

- Bangla + English together where possible
- English-only option
- Use UK English spelling if in doubt
- Bangladeshi tone and cultural relevance

### 4.4 UX / UI Principles

- Responsive (mobile + desktop)
- Clean, simple, uncluttered
- Fast load times
- Small page size
- Works reasonably with mobile data drops
- No heavy downloads
- Easy for non-technical users

### 4.5 Branding & Visual Identity

**Theme:** Pohela Boishakh (Bengali New Year) - festive, warm, culturally Bangladeshi

**Colour Palette:**

| Name | Hex | Usage |
|------|-----|-------|
| Red | `#D32F2F` | Primary accent, buttons, highlights |
| Red Dark | `#B71C1C` | Button hover, emphasis |
| Red Light | `#EF5350` | Subtle accents |
| Gold | `#D4A84B` | Secondary accent, logo, decorative |
| Gold Light | `#F0D78C` | Highlights, badges |
| Gold Dark | `#B8923A` | Shadows, depth |
| Cream | `#FFF8F0` | Background |
| White | `#FFFFFF` | Cards, content areas |
| Text Dark | `#2D2D2D` | Primary text |
| Text Muted | `#666666` | Secondary text |
| Border | `#F5E6E6` | Dividers, borders |

**Logo:**

- Gold bell with red accents (loop, clapper, sound waves)
- Symbolises reminders and notifications
- Files: `assets/logo-bell.svg`, `assets/favicon.svg`

**Typography:**

- Primary font: Hind Siliguri (supports Bengali + Latin)
- Weights: 400 (body), 500 (medium), 600 (semibold), 700 (bold)
- Source: Google Fonts

**Visual Elements:**

- Alpona-style corner decorations (traditional Bengali floor art patterns)
- Floating festive elements with subtle animation
- Red top band with gold dotted pattern
- Gradient borders (red → gold → red)
- Rounded corners (12-16px)

**SVG Guidelines (Cross-browser):**

- Always include `xmlns="http://www.w3.org/2000/svg"`
- Decorative SVGs: add `role="presentation" aria-hidden="true" focusable="false"`
- Logo/meaningful SVGs: add `role="img" aria-label="description"` and `<title>` element
- Use inline SVGs for critical UI elements (no external requests)
- Keep SVGs simple for mobile performance

---

## 5. Authentication & Security

- Email verification mandatory
- 2FA via email code when session cookie is missing
- Password reset via email
- No social login (initially)

---

## 6. Admin Features

- Admin dashboard
- Manage:
  - Templates
  - Message limits
  - Abuse / spam prevention
  - Users
- Individual users only (no teams)

---

## 7. Message Delivery Rules

- Invalid emails should be detected and not sent
- Failed sends should retry (basic retry logic needed)
- Sender receives notification when:
  - Message is sent
  - Message is opened (email only, where tracking is possible)
- Editing allowed unless within 12 hours of midnight in recipient timezone
- Yearly recurrence supported for birthdays/anniversaries (can be turned off)
- Account deletion cancels all pending messages

---

## 8. Help & Support

**Help section (static content):**

- Explain why time cannot be selected
- Explain timezone behaviour
- Explain open tracking limitations (Apple Mail Privacy Protection)

**Support form:**

- Logged-in users only
- Payment-related support only visible if user has paid
- General support option always available

---

## 9. Data & Privacy

**Users can:**

- Delete their data
- Export their data

**Privacy policy:**

- Not written yet
- Should align with:
  - Bangladesh norms
  - Basic international expectations
- Minimal data retention
- No analytics or insights in initial version

---

## 10. Payments & Pricing

### 10.1 Pricing Model

Pay-as-you-go (no subscriptions):

| Plan   | Messages     | Price            |
|--------|--------------|------------------|
| Free   | 3 / year     | Free             |
| Small  | 10           | 100 BDT / 1 USD  |
| Medium | 50           | 300 BDT / 3 USD  |

- Free tier: 3 free messages per year (resets on signup anniversary)
- Messages include both reminders and sent messages
- Unused credits never expire (trust signal)

### 10.2 Pricing Analysis

**Strengths:**

- Very low friction
- Easy to understand
- Works well for Bangladesh price sensitivity
- Pay-as-you-go fits reminder use-cases

**Risks:**

- Free tier may be too generous for email cost
- Users may never convert

---

## 11. Tech Stack

### 11.1 Development Standards

- **Git commits and branching:**
  - Branch naming: `feature/MRA-001`, `feature/MRA-002`, etc.
  - Commit naming: `feat: my commit message (MRA-001)`
  - Conventional commits
- **Testing:** Must have unit tests; execute regularly after likely affecting changes
- **Language:** TypeScript preferred
- **Monorepo:** Frontend + backend together

### 11.2 MVP Tech Stack (Cloudflare-first)

**Why Cloudflare:** Global edge, very low running cost, simple deployment, good for "mobile data drops", and built-in scheduling.

| Component | Choice | Notes |
|-----------|--------|-------|
| Frontend | Cloudflare Pages + React + Vite + TypeScript | Mobile-first |
| Backend/API | Cloudflare Workers (Hono + TypeScript) | Edge deployment |
| Database | Cloudflare D1 | SQLite-compatible; can migrate to Postgres later |
| Job scheduling | Cloudflare Workers Cron Triggers | Run every 5-10 minutes |
| Queue | Cloudflare Queues | Retries + smoothing bursts |
| File assets | Cloudflare R2 | For template images (future) |
| Auth | Email/password + httpOnly session cookies | + email verification + 2FA fallback |
| Email sending | Resend | Simple API, open/link tracking |
| Email auth | SPF + DKIM + DMARC | Critical for deliverability |

### 11.3 Payment Strategy: bKash First

**Phase 1 (MVP):** bKash Checkout (Tokenized) as primary payment method

- Lower fees (~1.5%) vs aggregators (~2-2.5%)
- Dominant payment method in Bangladesh
- Simpler single-provider integration
- Faster settlement

**Phase 2 (Post-launch):** Add SSLCommerz for additional options

- Nagad
- Local cards (Visa/Mastercard via local banks)
- Other mobile wallets

**bKash Integration Requirements:**

- Merchant account from bKash (requires business registration)
- Sandbox environment available for testing
- REST-based API
- Webhook for payment confirmation
- Onboarding timeline: 1-2 weeks

> **Note:** Start bKash merchant onboarding early as it can take time.

**International payments:** Stripe is not available for BD-based merchants. Consider Paddle or LemonSqueezy as merchant of record if needed.

### 11.4 Email Deliverability

- Use subdomain for sending (e.g., `send.monerakhbo.com`)
- Rotate subdomain monthly to isolate reputation
- SPF + DKIM + DMARC required

### 11.5 Deployment Flow

```
GitHub → Cloudflare Pages build + deploy
Workers API deployed via Wrangler
Environments: dev + prod
```

---

## 12. Data Model (MVP)

### 12.1 Core Entities

**users**

| Field | Type |
|-------|------|
| id | pk, uuid |
| email | unique, lowercase |
| password_hash | string |
| email_verified_at | nullable datetime |
| preferred_language | enum: en, bn, both |
| created_at | datetime |
| updated_at | datetime |
| is_admin | bool |

**sessions**

| Field | Type |
|-------|------|
| id | pk |
| user_id | fk users |
| session_token_hash | string |
| expires_at | datetime |
| created_at | datetime |
| last_seen_at | datetime |

**email_verification_tokens**

| Field | Type |
|-------|------|
| id | pk |
| user_id | fk users |
| token_hash | string |
| expires_at | datetime |
| used_at | nullable datetime |

**two_factor_codes**

| Field | Type |
|-------|------|
| id | pk |
| user_id | fk users |
| code_hash | string |
| expires_at | datetime |
| used_at | nullable datetime |
| created_at | datetime |
| ip_hash | optional string |

### 12.2 Messaging & Scheduling

**recipients**

Store recipients once, reuse across messages.

| Field | Type |
|-------|------|
| id | pk |
| user_id | fk users |
| display_name | optional string |
| relationship | enum: mum, dad, sister, brother, uncle, etc. |
| email | nullable string |
| phone_e164 | nullable string |
| timezone | nullable string (if null, use UTC + show warning) |
| created_at | datetime |
| updated_at | datetime |

**templates**

Admin-managed; localised.

| Field | Type |
|-------|------|
| id | pk |
| key | unique slug (e.g., `birthday_basic_01`) |
| category | enum: birthday, anniversary, reminder, etc. |
| language | enum: en, bn, both |
| subject_template | string with tokens like `{{name}}` |
| body_template_html | text |
| body_template_text | text |
| allows_custom_message | bool |
| is_active | bool |
| created_at | datetime |
| updated_at | datetime |

**scheduled_messages**

A "user intent" record.

| Field | Type |
|-------|------|
| id | pk |
| user_id | fk users |
| type | enum: reminder_to_self, send_to_recipient |
| template_id | nullable fk templates |
| recipient_id | nullable fk recipients (required for send_to_recipient) |
| custom_message | nullable text |
| send_date | date (ISO format) |
| recipient_timezone | nullable string (snapshot from recipient at creation) |
| send_at_utc | datetime (computed: send_date 00:00 in recipient TZ → UTC) |
| status | enum: scheduled, paused, cancelled |
| is_recurring | bool |
| preview_snapshot_json | optional json |
| created_at | datetime |
| updated_at | datetime |

**message_deliveries**

One row per actual send attempt.

| Field | Type |
|-------|------|
| id | pk |
| scheduled_message_id | fk scheduled_messages |
| channel | enum: email, sms, whatsapp |
| to_address | string (email or phone snapshot) |
| subject_rendered | string |
| body_html_rendered | text |
| body_text_rendered | text |
| provider | enum: resend, postmark, ses, etc. |
| provider_message_id | nullable string |
| status | enum: queued, sent, failed, bounced, invalid |
| attempt_count | int |
| next_retry_at | nullable datetime |
| last_error_code | nullable string |
| last_error_message | nullable text |
| sent_at | nullable datetime |
| created_at | datetime |
| updated_at | datetime |

**message_events**

Track delivery events without building analytics dashboards.

| Field | Type |
|-------|------|
| id | pk |
| message_delivery_id | fk message_deliveries |
| event_type | enum: delivered, opened, clicked, bounced, complained |
| event_at | datetime |
| metadata_json | json (user-agent, ip hash, etc.) |

### 12.3 Credits & Payments

**credit_wallets**

One per user.

| Field | Type |
|-------|------|
| user_id | pk, fk users |
| balance_messages | int |
| free_anniversary_month | int (month of signup) |
| free_anniversary_day | int (day of signup) |
| free_remaining | int (set to 3 at signup anniversary) |
| updated_at | datetime |

**credit_ledger**

Immutable ledger.

| Field | Type |
|-------|------|
| id | pk |
| user_id | fk users |
| type | enum: grant_free_yearly, purchase, consume, refund, admin_adjust |
| delta_messages | int (e.g., +50, -1) |
| reference_type | enum: scheduled_message, payment, admin |
| reference_id | string |
| created_at | datetime |
| notes | nullable text |

**payments**

| Field | Type |
|-------|------|
| id | pk |
| user_id | fk users |
| provider | enum: bkash, sslcommerz |
| provider_payment_id | string |
| currency | enum: BDT, USD |
| amount | decimal |
| status | enum: initiated, paid, failed, refunded |
| package | enum: 10_messages, 50_messages |
| created_at | datetime |
| paid_at | nullable datetime |

### 12.4 Admin & Safety

**rate_limits** (optional)

| Field | Type |
|-------|------|
| user_id | fk users |
| date | date (YYYY-MM-DD) |
| messages_created_count | int |
| messages_sent_count | int |
| updated_at | datetime |

**audit_log** (optional but useful)

| Field | Type |
|-------|------|
| id | pk |
| actor_user_id | fk users |
| action | string (e.g., TEMPLATE_UPDATED, USER_DISABLED) |
| target_type | string |
| target_id | string |
| metadata_json | json |
| created_at | datetime |

---

## 13. Backend Jobs (MVP)

### 13.1 Scheduler Job (Cron every 5-10 minutes)

1. Query `scheduled_messages` where `status=scheduled` and `send_at_utc <= now`
2. For each:
   - Validate destination (email format)
   - Consume 1 credit (free first, then paid)
   - Create `message_deliveries` with status `queued`
   - Send via provider
   - Mark delivery `sent` or `failed`
   - If failed and retryable: set `next_retry_at` with backoff

Uses Cloudflare Cron Triggers.

### 13.2 Webhook Receiver (Email Provider)

- Receive events (delivered/opened/bounced)
- Write to `message_events`
- Update `message_deliveries.status` accordingly

Resend supports open tracking and has an API-focused workflow.

---

## 14. Growth & Discovery

### 14.1 Initial Growth Loop

1. Recipient receives a message
2. Email footer: "Sent via Mone Rakhবো – don't forget important dates"
3. Recipient encouraged to sign up and send their own

### 14.2 Future Viral Ideas (Not MVP)

- "Remind me next year" button in emails
- Shareable reminder links
- Cultural reminder packs (Eid, anniversaries, etc.)

---

## 15. Explicit Non-Goals (Initial Version)

- No SMS / WhatsApp
- No analytics dashboard
- No images, video, or voice (text/HTML templates only)
- No team accounts
- No advanced scheduling
- No social login

---

## 16. What Makes This Service Unique

To avoid being "just another reminder app":

- Emotional + cultural focus (Bangladesh-first)
- Message-sending, not just notifications
- Extremely low friction
- No subscription pressure
- Trust-first pricing
- Clean, respectful emails (not marketing-style)

---

## 17. Open Questions & Decisions

### 17.1 Resolved Decisions

| Question | Decision |
|----------|----------|
| Free tier reset timing | Signup anniversary (month/day) |
| Number of free messages | 3 per year |
| Recurring reminders | Yes, with option to turn off |
| Editing scheduled messages | Allowed unless within 12 hours of midnight in recipient timezone |
| Account deletion with pending messages | Cancel all pending messages |
| DST handling for recipients abroad | Use recipient's selected timezone |
| Cron precision (up to 10 min late) | Acceptable |
| D1 storage limit (500MB free) | Review later |
| Open tracking reliability | De-emphasise; show "where possible" with explanation |
| "Send me a reminder" feature | Self-reminder functionality, separate from e-card |
| Template customisation | Name + message tokens; text/HTML initially |
| Monorepo vs separate repos | Monorepo |

### 17.2 Still Open

**Abuse / Trust:**

- Max messages per day per user? 30
- Max messages per user 500 per month
- Max credits per user $50 per month
- CAPTCHA on signup? Yes
- Template approval process? No, these will be predefined by admin

**Legal / Compliance:**

- Simple consent language for sending emails to others
- Opt-out language in email footer

---

## 18. Estimated Monthly Costs (MVP)

| Service | Cost |
|---------|------|
| Cloudflare (Workers, D1, Pages) | Free tier |
| Resend | Free up to 3k emails/month |
| bKash | Transaction fees only |
| Domain | ~$12/year |
| **Total** | **~$1-5/month** until scale |
