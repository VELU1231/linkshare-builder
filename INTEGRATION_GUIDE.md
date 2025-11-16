# LinkShare - Firebase & Stripe Integration Guide

## Phase 3: Backend Integration Setup

This guide explains how to set up Firebase authentication, Firestore database, and Stripe payment integration for LinkShare.

## Prerequisites

- Node.js 16+ installed
- GitHub account with VELU1231/linkshare-builder repo access
- futureai2077@gmail.com Google account (for Firebase)
- futureai2077@gmail.com Stripe account

## Step 1: Firebase Project Setup

### 1.1 Create Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com)
2. Login with futureai2077@gmail.com
3. Click "Create project" or "Add project"
4. Enter project name: `linkshare-gen-z`
5. Enable Google Analytics (recommended)
6. Click "Create project"

### 1.2 Enable Authentication

1. In Firebase Console, go to Authentication > Sign-in method
2. Enable: **Email/Password**
3. Enable: **Google** (OAuth)
4. Add authorized domains:
   - localhost:3000 (development)
   - localhost:5173 (Vite development)
   - linkshare.web.app (production)

### 1.3 Create Firestore Database

1. Go to Firestore Database
2. Click "Create database"
3. Choose "Start in test mode" (development)
4. Select region: us-central1
5. Click "Create"

### 1.4 Create Firestore Collections

Create these collections in Firestore:

**Collection: users**
```
Document ID: uid (from Firebase Auth)
{
  email: string
  displayName: string
  created_at: timestamp
  updated_at: timestamp
  subscription_tier: 'free' | 'pro' | 'creator'
  stripe_customer_id: string
  sites_created: number
}
```

**Collection: sites**
```
Document ID: auto-generated
{
  user_id: string (reference to users)
  title: string
  slug: string
  template: string
  html_content: string
  css_content: string
  is_published: boolean
  is_public: boolean
  view_count: number
  created_at: timestamp
  updated_at: timestamp
  published_at: timestamp
}
```

**Collection: subscriptions**
```
Document ID: auto-generated
{
  user_id: string
  stripe_subscription_id: string
  tier: 'pro' | 'creator'
  status: 'active' | 'cancelled' | 'past_due'
  price_id: string
  current_period_start: timestamp
  current_period_end: timestamp
  cancel_at_period_end: boolean
  created_at: timestamp
  updated_at: timestamp
}
```

### 1.5 Get Firebase Config

1. Go to Project Settings (gear icon)
2. Go to "Your apps" section
3. Click "</> Web"
4. Copy the Firebase config object
5. Create `.env.local` file in project root
6. Add credentials (see Step 3)

## Step 2: Stripe Account Setup

### 2.1 Create Stripe Account

1. Go to [Stripe Dashboard](https://dashboard.stripe.com)
2. Login with futureai2077@gmail.com
3. Complete account setup
4. Switch to **Test Mode** (toggle in top-right)

### 2.2 Create Products and Prices

**Product: Pro Plan**
- Name: "Pro - 10 Sites"
- Price: $4.99/month
- Billing cycle: Monthly
- Copy Price ID (starts with `price_`)

**Product: Creator Plan**
- Name: "Creator - Unlimited Sites"
- Price: $14.99/month
- Billing cycle: Monthly
- Copy Price ID (starts with `price_`)

### 2.3 Get Stripe Keys

1. Go to Developers > API Keys
2. Copy **Publishable key** (starts with `pk_test_`)
3. Copy **Secret key** (starts with `sk_test_`)
4. Add to `.env.local` (see Step 3)

## Step 3: Configure Environment Variables

Create `.env.local` file in project root:

```env
# Firebase Configuration
VITE_FIREBASE_API_KEY=your_firebase_api_key
VITE_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your_project_id
VITE_FIREBASE_STORAGE_BUCKET=your_project.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
VITE_FIREBASE_APP_ID=your_app_id

# Stripe Configuration (Test Mode)
VITE_STRIPE_PUBLISHABLE_KEY=pk_test_your_key_here

# Backend Secret (for API calls)
VITE_STRIPE_SECRET_KEY=sk_test_your_key_here
```

## Step 4: Local Development

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# The app will be available at http://localhost:5173
```

## Step 5: Test Authentication Flow

1. Click "Sign Up" or "Sign In"
2. Test Email/Password registration
3. Test Google OAuth
4. Verify user appears in Firebase Authentication console
5. Verify user document created in Firestore

## Step 6: Test Payment Flow

1. Upgrade to Pro or Creator plan
2. Enter Stripe test card: `4242 4242 4242 4242`
3. Any future date and CVC
4. Verify subscription created in Firestore
5. Verify charge appears in Stripe Test Mode dashboard

### Test Cards

- **Success**: 4242 4242 4242 4242
- **Declined**: 4000 0000 0000 0002
- **3D Secure**: 4000 0025 0000 3155

## Step 7: Deploy to Firebase Hosting

```bash
# Install Firebase CLI (if not already installed)
npm install -g firebase-tools

# Login to Firebase
firebase login

# Build app
npm run build

# Deploy
firebase deploy

# Your app will be available at: https://linkshare-gen-z.web.app
```

## Firestore Security Rules (Production)

Update Firestore rules to:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read, write: if request.auth.uid == userId;
    }
    match /sites/{siteId} {
      allow read: if resource.data.is_public == true;
      allow create: if request.auth != null;
      allow update, delete: if request.auth.uid == resource.data.user_id;
    }
    match /subscriptions/{subscriptionId} {
      allow read, write: if request.auth.uid == resource.data.user_id;
    }
  }
}
```

## Troubleshooting

### Firebase Auth Not Working
- Ensure localhost:5173 is in authorized domains
- Check API key in .env.local is correct
- Clear browser cookies and try again

### Stripe Payment Fails
- Ensure Publishable Key is for Test Mode (pk_test_)
- Check .env.local has correct Stripe key
- Verify product prices exist in Stripe dashboard

### Firestore Write Fails
- Check Security Rules allow your user
- Ensure user document exists in /users/{uid}
- Check Firestore is in Test Mode for development

## Next Steps

1. Set up GitHub Actions CI/CD pipeline
2. Add email notifications for new subscriptions
3. Implement analytics dashboard
4. Add refund processing
5. Set up monitoring and error tracking

## Resources

- [Firebase Docs](https://firebase.google.com/docs)
- [Stripe Docs](https://stripe.com/docs)
- [React Fire](https://github.com/FirebaseExtended/react-fire)
- [Stripe React](https://stripe.com/docs/stripe-js/react)
