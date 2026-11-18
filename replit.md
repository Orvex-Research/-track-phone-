# TrackDown

## Overview

TrackDown is a location tracking tool that generates shareable links to collect visitor information (IP address, timestamp, and geolocation data) and sends this data to the user via a Telegram bot. The application serves disguised web pages that capture visitor details when accessed, then redirects users to a specified URL while reporting the collected data back through Telegram.

This project is built on Express.js and integrates with the Telegram Bot API for real-time notifications. It uses EJS templating for rendering tracking pages and is designed to be deployed on Replit.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Backend Architecture
- **Framework**: Express.js handles all HTTP routing and middleware
- **Templating**: EJS renders dynamic tracking pages (webview, cloudflare templates)
- **Bot Integration**: node-telegram-bot-api library manages Telegram bot communication with polling mode

### Core Tracking Flow
1. User generates a tracking link through the Telegram bot
2. Link contains encoded destination URL and unique identifier in the path
3. When target visits the link, the server captures IP and timestamp
4. EJS template renders a page that collects additional browser/location data
5. Data is sent back to the server and forwarded to the user via Telegram

### Route Structure
- `/w/:path/:uri` - Webview tracking page
- `/c/:path/:uri` - Cloudflare-styled tracking page
- Path parameters contain user ID and base64-encoded redirect URL

### Environment Configuration
- `bot` - Telegram Bot API token (required, case-sensitive)
- `REPL_SLUG` and `REPL_OWNER` - Auto-populated by Replit for dynamic URL generation

### URL Generation
The host URL is dynamically constructed using Replit environment variables (`REPL_SLUG.REPL_OWNER.repl.co`). There's also an optional URL shortener toggle (`use1pt`).

## External Dependencies

### Third-Party Services
- **Telegram Bot API**: Primary interface for user interaction and data delivery. Requires a bot token from BotFather.

### NPM Packages
- `express` - Web server framework
- `node-telegram-bot-api` - Telegram bot integration
- `ejs` - Server-side templating
- `body-parser` - Request body parsing (JSON and URL-encoded)
- `cors` - Cross-origin resource sharing
- `dotenv` - Environment variable management
- `node-fetch` - HTTP client for external API calls
- `base64-to-image` - Image processing utility

### Deployment
- Designed for Replit deployment with dynamic URL construction based on Replit environment variables