# Sentry Setup Guide

This guide provides a quick overview of how to set up Sentry for error tracking in our application.

## 1. Create a Sentry Account & Project
1. Go to [sentry.io](https://sentry.io) and sign up/log in.
2. Create a new Project.
3. Select the platform/framework for your application (e.g., React, Node.js, Python).
4. Sentry will provide you with a **DSN** (Data Source Name). Keep this handy.

## 2. Install Sentry SDK
Install the appropriate Sentry SDK for your platform.

For example, for a JavaScript/TypeScript project (e.g., React or Next.js):
```bash
npm install @sentry/browser @sentry/tracing
# or for Node.js
npm install @sentry/node
```

## 3. Initialize Sentry
Initialize Sentry as early as possible in your application's lifecycle (e.g., `index.js`, `App.js`, or `main.ts`).

```javascript
import * as Sentry from "@sentry/browser";
import { BrowserTracing } from "@sentry/tracing";

Sentry.init({
  dsn: "YOUR_DSN_HERE",
  integrations: [new BrowserTracing()],

  // Set tracesSampleRate to 1.0 to capture 100%
  // of transactions for performance monitoring.
  // We recommend adjusting this value in production
  tracesSampleRate: 1.0,
});
```
*Note: Replace `"YOUR_DSN_HERE"` with the actual DSN from your Sentry project.*

## 4. Test the Setup
Trigger a deliberate error to ensure Sentry is capturing it correctly.

```javascript
// Example test error
myUndefinedFunction();
```
Check your Sentry dashboard to confirm the error was logged.

## 5. User Feedback (Optional)
Sentry allows you to collect user feedback when an error occurs. You can trigger the feedback dialog programmatically:

```javascript
Sentry.showReportDialog({ eventId });
```

---
**References:**
- [Sentry Documentation](https://docs.sentry.io/)
