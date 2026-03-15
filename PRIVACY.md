# Privacy Policy

**Effective Date:** March 14, 2026
**Last Updated:** March 14, 2026

Loggerhead Instruments ("we", "us", "our") operates Weft, a desktop application for bioacoustic data analysis and acoustic classifier training. This Privacy Policy describes how we collect, use, and protect your information when you use Weft.

## 1. Information We Collect

### 1.1 Account Information

When you sign up for Weft, we collect your email address for account authentication and communication about the service.

### 1.2 Telemetry Data

Weft collects anonymous usage telemetry to help us improve the application. This includes:

- **Feature usage** — which features and workspaces you use (e.g., training, processing, analysis)
- **Performance metrics** — app startup time, processing duration, error rates
- **System information** — operating system, app version, screen resolution
- **Crash reports** — stack traces and error messages when the app encounters problems

Telemetry data is sent to our cloud servers and is used solely for improving Weft. It does **not** include:

- Your audio files or recordings
- Your detection data, analysis results, or project contents
- File names or file paths
- GPS coordinates or location data from your projects
- Haikubox API keys or account credentials

### 1.3 Haikubox Integration

If you connect a Haikubox account to Weft, your Haikubox API key is stored locally on your machine at `~/.weft/haikubox.json`. API keys are never transmitted to Loggerhead Instruments servers — they are sent only to the Haikubox API (`weft.haikubox.com`) to authenticate your requests.

## 2. How We Use Your Information

We use the information we collect to:

- Provide and maintain the Weft application
- Improve app performance, stability, and features
- Diagnose and fix bugs
- Communicate important updates about the service
- Understand usage patterns to prioritize development

## 3. Data Storage and Security

### 3.1 Local-First Architecture

Weft is a local-first application. Your project data, audio files, analysis results, and databases are stored on your local machine by default. Trained models can optionally be uploaded to and downloaded from our cloud storage for sharing across devices or with other users. Uploaded models are stored on Supabase infrastructure (see below).

### 3.2 Third-Party Services

Weft connects to the following third-party services:

| Service | Purpose | Data Sent |
|---------|---------|-----------|
| **Visual Crossing** | Weather and air quality enrichment | GPS coordinates and date ranges from your project |
| **NOAA CO-OPS** | Tidal data enrichment | GPS coordinates and date ranges from your project |
| **NOAA ERDDAP** | Ocean data enrichment (SST, chlorophyll-a) | GPS coordinates and date ranges from your project |
| **Anthropic Claude API** | AI Advisor for data analysis | Table metadata, summary statistics, and conversation messages from your project |
| **Supabase** | Account auth, telemetry, and cloud model storage | Email address, telemetry events, and trained model files you choose to upload |
| **Haikubox API** | Detection sync and audio streaming (optional) | Your Haikubox API key and query parameters |

These connections are initiated only when you explicitly request the corresponding feature (e.g., clicking "Compute" on weather enrichment or "Sync" on Haikubox data).

### 3.3 Security

We use industry-standard practices to protect your information. Telemetry data is transmitted over HTTPS. Local credentials (such as Haikubox API keys) are stored in plain text on your local filesystem — protect access to your machine accordingly.

## 4. Data Retention

- **Telemetry data** is retained indefinitely to support long-term product improvement.
- **Account information** is retained for as long as your account is active.
- **Local data** is under your control — delete it from your machine at any time.

## 5. Children's Privacy

Weft is not directed at children under 13. We do not knowingly collect personal information from children under 13.

## 6. Free Beta

Weft is currently in free beta. During the beta period, features and data collection practices may change. We will update this Privacy Policy to reflect any material changes and notify users via the app or email.

## 7. Your Rights

You may:

- **Request deletion** of your account and associated telemetry data by contacting us
- **Opt out** of telemetry by disabling it in Settings (when available)
- **Delete local data** at any time by removing project folders from your machine

## 8. Changes to This Policy

We may update this Privacy Policy from time to time. Changes will be posted to this page with an updated "Last Updated" date. Continued use of Weft after changes constitutes acceptance of the updated policy.

## 9. Contact Us

If you have questions about this Privacy Policy, contact us at:

**Loggerhead Instruments**
Email: info@loggerhead.com
Website: [loggerhead.com](https://loggerhead.com)
