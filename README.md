# LinkShare - Build Your Online Presence in 30 Seconds 🚀

**No coding. No designers needed. Pure vibes.**

LinkShare is a lightning-fast, Gen Z-focused landing page builder powered by GrapesJS, Supabase, and Stripe.
Build beautiful link-in-bio pages, portfolios, resumes, and landing pages with drag-and-drop simplicity.

---

## 🎯 Why LinkShare?

- **30-Second Setup**: Pick a template, customize, and launch
- **Mobile-First Design**: Looks perfect on all devices  
- **Drag-and-Drop Editor**: No code required, total control
- **AI-Powered Templates**: Gen Z-optimized designs with gradients, animations, social widgets
- **One-Click Deploy**: Your site goes live instantly
- **Monetized**: Free tier with premium features ($4.99/mo & $14.99/mo)

---

## 📊 Market Validation

- **Landing page builder market**: $725M (2025) → $3.87B (2037) [14.6% CAGR]
- **Gen Z spending power**: $12 trillion in 5 years
- **36% of marketers now target Gen Z** (up from 34% in 2023)
- **Underserved niche**: No builder specifically designed for Gen Z creators

---

## ✨ Features

### 🎁 FREE TIER
- Drag-and-drop page builder (GrapesJS)
- 3 preset templates (link-in-bio, portfolio, resume)
- Mobile preview
- Export as HTML
- Basic analytics (view count)
- Share publicly

### ⭐ PAID TIER ($4.99/month)
- Custom domain support
- 50+ Gen Z templates (gradients, animations, social widgets)
- Premium analytics (traffic sources, device tracking)
- AI design suggestions
- Unlimited pages
- Priority support
- Remove "Made with LinkShare" branding

### 🚀 PREMIUM TIER ($14.99/month)
- Everything in Paid
- AI page generation ("Describe your vibe" feature)
- White-label builder
- Email integration (Mailchimp)
- Advanced SEO tools
- API access for agencies
- Custom CSS/JavaScript support

---

## 🏗️ Tech Stack

| Component | Technology | Why |
|-----------|-----------|-----|
| Frontend | React 18 + TypeScript + Tailwind CSS | Fast, modern, scalable |
| Builder Engine | GrapesJS | 25K+ GitHub stars, proven |
| Auth + Database | Supabase (PostgreSQL) | Free tier, open-source |
| Payments | Stripe | Industry standard |
| Hosting | Vercel | 100GB free bandwidth, CI/CD |
| CI/CD | GitHub Actions | 100% web-based, free |

---

## 🚀 Quick Start

### Prerequisites
- Node.js 18+
- Git
- Free accounts: Supabase, Stripe, Vercel

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/VELU1231/linkshare-builder.git
cd linkshare-builder

# 2. Install dependencies
npm install

# 3. Set up environment variables
cp .env.example .env.local
# Edit .env.local with your Supabase and Stripe keys

# 4. Start development server
npm run dev

# 5. Open http://localhost:5173
```

---

## 📁 Project Structure

```
linkshare-builder/
├── .github/
│   └── workflows/
│       └── deploy.yml          # GitHub Actions CI/CD
├── src/
│   ├── components/
│   │   ├── BuilderEditor.tsx    # GrapesJS wrapper
│   │   ├── TemplateGallery.tsx  # Gen Z templates
│   │   ├── PricingPlans.tsx     # Subscription plans
│   │   └── NavBar.tsx
│   ├── pages/
│   │   ├── Dashboard.tsx        # User dashboard
│   │   ├── Editor.tsx           # Main editor
│   │   ├── Preview.tsx          # Site preview
│   │   └── LandingPage.tsx      # Marketing landing page
│   ├── services/
│   │   ├── supabaseClient.ts    # Auth + DB
│   │   ├── stripeClient.ts      # Payments
│   │   └── builderService.ts    # GrapesJS utils
│   ├── styles/
│   │   └── grapesjs-genz.css    # Custom themes
│   ├── App.tsx
│   └── main.tsx
├── public/
├── package.json
├── vite.config.ts
├── tailwind.config.js
├── tsconfig.json
├── .env.example
└── README.md
```

---

## 🗄️ Database Schema (Supabase)

```sql
-- Users table
CREATE TABLE users (
  id UUID PRIMARY KEY,
  email TEXT UNIQUE NOT NULL,
  name TEXT,
  avatar_url TEXT,
  subscription_tier TEXT DEFAULT 'free', -- 'free', 'paid', 'premium'
  stripe_customer_id TEXT,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Sites table
CREATE TABLE sites (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  title TEXT NOT NULL,
  slug TEXT UNIQUE,
  template TEXT DEFAULT 'link-bio',
  html_content JSONB,
  is_published BOOLEAN DEFAULT FALSE,
  view_count INTEGER DEFAULT 0,
  custom_domain TEXT,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Analytics table
CREATE TABLE analytics (
  id UUID PRIMARY KEY,
  site_id UUID REFERENCES sites(id) ON DELETE CASCADE,
  views INTEGER DEFAULT 0,
  unique_visitors INTEGER DEFAULT 0,
  referrer TEXT,
  device TEXT, -- 'mobile', 'desktop', 'tablet'
  date DATE DEFAULT CURRENT_DATE,
  created_at TIMESTAMP DEFAULT NOW()
);
```

---

## 💰 Revenue Model

### Subscription Tiers
- **Free**: 0% revenue, but user acquisition
- **Paid** ($4.99/mo): 70% Stripe fee
- **Premium** ($14.99/mo): 70% Stripe fee

### Projected Revenue (Year 1)

| Month | Users | Paying Users | Revenue | Notes |
|-------|-------|--------------|---------|-------|
| 1-3 | 100 | 5-10 | $25-50 | Launch phase, viral potential |
| 4-6 | 1,000 | 50-100 | $250-500 | Growth phase |
| 7-12 | 10,000 | 500-1,000 | $2,500-5,000 | Scale phase |

### Year 2 Projection
- **50,000 users** → **5,000-10,000 paying subs**  
- **Revenue**: $25,000-50,000/month ($300k-600k/year)

---

## 📈 Go-to-Market Strategy

### Launch (Week 1-2)
- ✅ Product Hunt launch (offer free Pro for 30 days)
- ✅ Reddit: r/startups, r/webdev, r/entrepreneurship
- ✅ Indie Hackers
- ✅ Twitter threads + Hacker News

### Growth (Week 3-8)
- 📱 TikTok/Instagram Shorts: "Build your site in 30 seconds"
- 💬 Discord servers (freelance, creator economy)
- 🔄 Referral program (2 months free for 5 referrals)
- 🤝 Partnerships with creator/freelance communities

### Scale (Month 3+)
- 🎯 Influencer collaborations (micro-influencers)
- 📊 Content marketing (SEO blog posts)
- 🌍 Communities: Slack, Discord, Facebook Groups
- 💌 Email marketing to early users

---

## 🔧 Setup Guide

### 1. Supabase Setup (5 min)
1. Go to [supabase.com](https://supabase.com) → Create free project
2. Run the SQL migrations from `supabase/migrations/001_init.sql`
3. Copy your API keys to `.env.local`:
   ```
   VITE_SUPABASE_URL=your_url
   VITE_SUPABASE_ANON_KEY=your_anon_key
   ```

### 2. Stripe Setup (5 min)
1. Go to [stripe.com](https://stripe.com) → Sign up
2. Get your publishable and secret keys
3. Add to `.env.local`:
   ```
   VITE_STRIPE_PUBLISHABLE_KEY=your_key
   STRIPE_SECRET_KEY=your_secret
   ```

### 3. GitHub Actions CI/CD (5 min)
1. Add `.github/workflows/deploy.yml` (see below)
2. Add Vercel deployment secrets to GitHub
3. Every `git push` deploys automatically

### 4. Vercel Deployment (5 min)
1. Connect your GitHub repo to Vercel
2. Add environment variables
3. Deploy with one click

---

## 🤝 Contributing

We're building this together! Contributions welcome:

1. Fork the repo
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📝 License

MIT License - See LICENSE file for details

---

## 💬 Community

- **Discord**: [Join our Discord](https://discord.gg/linkshare)
- **Twitter**: [@LinkShareBuilder](https://twitter.com/linksharebuilder)
- **Reddit**: [r/LinkShare](https://reddit.com/r/linkshare)
- **Email**: support@linkshare.dev

---

## 🙏 Acknowledgments

- **GrapesJS**: 25K+ star open-source page builder framework
- **Supabase**: Open-source Firebase alternative
- **Vercel**: Best-in-class frontend deployment
- **Our Gen Z community**: For inspiring this vision

---

**Built with ❤️ for Gen Z creators** 🎨✨
