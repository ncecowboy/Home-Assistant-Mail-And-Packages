# API Integration Options for Mail and Packages

## Overview

This document addresses the question: **Are there APIs available to integrate USPS, UPS, FedEx, and Amazon rather than using an IMAP email integration?**

**Short Answer:** Yes, all major shipping carriers offer official APIs. However, they require registration, API credentials, and in some cases have usage limits or costs. The current IMAP email-based approach works without requiring API credentials and is free to use.

## Official Carrier APIs

### 1. USPS (United States Postal Service)

**API Availability:** ✅ Yes

- **Platform:** USPS Developer Portal
- **Status:** New modernized API launched in 2026 (old Web Tools APIs retired January 25, 2026)
- **Capabilities:**
  - Package tracking with real-time updates
  - Delivery status and estimated delivery dates
  - Push webhook notifications for tracking events
  - Informed Delivery integration
- **Access Requirements:**
  - Register at [USPS Developer Portal](https://developer.usps.com/)
  - Obtain API credentials (API Key)
  - Free tier available with usage limits
- **API Documentation:** [Tracking 3.2 API](https://developers.usps.com/trackingv3r2)
- **Authentication:** API Key required
- **Cost:** Free tier available; commercial use may have fees

### 2. UPS (United Parcel Service)

**API Availability:** ✅ Yes

- **Platform:** UPS Developer Portal
- **Capabilities:**
  - Real-time package tracking
  - Shipment status and event notifications
  - Delivery time estimates
  - Exception handling
- **Access Requirements:**
  - Register at [UPS Developer Portal](https://developer.ups.com/)
  - Obtain API credentials (Client ID, Secret)
  - Agree to terms of service
- **API Documentation:** [UPS APIs](https://developer.ups.com/api/reference)
- **Authentication:** OAuth 2.0
- **Cost:** Free for development; production use may require business account

### 3. FedEx

**API Availability:** ✅ Yes

- **Platform:** FedEx Developer Portal
- **Capabilities:**
  - Track shipment status and history
  - Access estimated delivery dates
  - Receive exception notifications
  - Delivery confirmations
- **Access Requirements:**
  - Register at [FedEx Developer Portal](https://developer.fedex.com/)
  - Obtain API credentials (API Key, Secret Key)
  - FedEx account recommended
- **API Documentation:** [FedEx Track API](https://developer.fedex.com/api/en-us/catalog/track/v1/docs.html)
- **Authentication:** OAuth 2.0
- **Cost:** Free for registered FedEx customers; commercial use terms apply

### 4. Amazon

**API Availability:** ⚠️ Limited

- **Platform:** Amazon Shipping API (for merchants/partners only)
- **Capabilities:**
  - Real-time tracking for Amazon shipments
  - Delivery notifications
  - Proof-of-delivery (photo/GPS when available)
  - Order status updates
- **Access Requirements:**
  - Must be enrolled as Amazon Shipping customer or Selling Partner
  - Requires Amazon Seller/Partner credentials
  - **Not available for individual consumers**
- **API Documentation:** [Amazon Shipping API](https://shipping.amazon.com/api-integration)
- **Authentication:** Amazon MWS/SP-API credentials
- **Cost:** Requires Amazon business account
- **Limitation:** Amazon does not provide a public tracking API for general consumer use. Most integrations rely on:
  - Tracking emails (current approach)
  - Amazon order scraping (against TOS)
  - Third-party tracking services

## Third-Party Multi-Carrier APIs

For unified tracking across multiple carriers, consider third-party services:

### TrackingMore
- **Support:** 1,500+ carriers including USPS, UPS, FedEx, DHL
- **Features:** Auto-carrier detection, standardized responses, webhooks
- **Cost:** Freemium model (limited free tier, paid plans for production)
- **Website:** [TrackingMore API](https://www.trackingmore.com/tracking-api)

### AfterShip
- **Support:** 1,000+ carriers worldwide
- **Features:** Unified API, webhook notifications, branded tracking pages
- **Cost:** Paid service with various tiers

### EasyPost
- **Support:** Multi-carrier tracking and shipping APIs
- **Features:** Unified interface for multiple carriers
- **Cost:** Pay-per-use pricing model

### Ship24
- **Support:** Multiple carriers worldwide
- **Features:** Real-time tracking API, universal tracking
- **Cost:** Freemium model

## Comparison: API vs. IMAP Email Integration

### Current IMAP Approach (Used by This Integration)

**Advantages:**
- ✅ **Free:** No API costs or registration required
- ✅ **No rate limits:** Email parsing has no API quotas
- ✅ **Universal:** Works with any carrier that sends email notifications
- ✅ **Privacy:** All processing done locally, no data sent to third parties
- ✅ **Easy setup:** Only requires email credentials
- ✅ **Includes Amazon:** Works with Amazon delivery emails
- ✅ **Historical data:** Can access past emails
- ✅ **Informed Delivery images:** Can extract USPS mail preview images

**Disadvantages:**
- ❌ **Delay:** Updates depend on email delivery (usually minutes)
- ❌ **Email dependency:** Requires carrier notification emails to be enabled
- ❌ **Email parsing:** Subject line changes by carriers can break detection
- ❌ **Limited data:** Only information included in email notifications
- ❌ **No real-time:** Not suitable for real-time tracking updates

### API-Based Approach

**Advantages:**
- ✅ **Real-time:** Immediate tracking updates
- ✅ **Structured data:** Consistent, machine-readable format
- ✅ **More details:** Access to full tracking history and metadata
- ✅ **Reliable:** Less prone to parsing errors
- ✅ **Webhooks:** Push notifications for status changes
- ✅ **Professional:** Better for commercial/production use

**Disadvantages:**
- ❌ **Cost:** Many APIs have usage fees for production
- ❌ **Registration:** Requires account setup with each carrier
- ❌ **Rate limits:** API quotas and throttling
- ❌ **Credentials:** Need to manage multiple API keys/secrets
- ❌ **Amazon limitation:** No public consumer API available
- ❌ **Maintenance:** API changes require code updates
- ❌ **Privacy concerns:** Data sent to carrier APIs
- ❌ **Complexity:** More complex to implement and maintain

## Feasibility for This Integration

### Recommended Approach

For a Home Assistant integration targeting individual home users, the **current IMAP email-based approach is more appropriate** because:

1. **Target Audience:** Individual homeowners don't need business-level APIs
2. **Zero Cost:** No API fees for users
3. **Privacy First:** Aligns with Home Assistant's local-first philosophy
4. **Universal Support:** Works with all carriers, including Amazon
5. **Simple Setup:** Users only need to enable email notifications (which most already have)
6. **No Rate Limits:** Email parsing has no quotas

### When API Integration Makes Sense

API integration would be beneficial if:

- Building a commercial package tracking service
- Requiring real-time updates (seconds, not minutes)
- Needing detailed tracking history beyond email content
- Managing high volumes of shipments
- Integration with shipping/fulfillment systems
- Willing to pay for API access and maintain credentials

### Hybrid Approach Possibility

A potential future enhancement could offer both options:

1. **Default:** IMAP email integration (current approach)
2. **Optional:** API integration for users who have credentials
   - Users with UPS/FedEx/USPS business accounts could optionally configure API access
   - Would provide more detailed tracking information
   - Email integration would remain as fallback

**Implementation Complexity:** High
- Requires supporting two completely different data sources
- Managing API credentials securely
- Handling rate limits and errors
- Testing with multiple carriers
- Maintaining both code paths

## Conclusion

**Yes, APIs are available** for USPS, UPS, and FedEx, but **Amazon's API is not publicly accessible** for general consumer use.

**However, the current IMAP email integration approach is more suitable** for this Home Assistant integration because:

1. It's free and accessible to all users
2. It works with all carriers including Amazon
3. It's privacy-focused and requires no external API calls
4. It's simple to set up and maintain
5. Email updates are sufficiently timely for home use cases

API integration could be considered as a **future optional enhancement** for users who have business accounts and need real-time tracking, but should not replace the email-based approach which serves the majority of users well.

## Resources

### Official API Documentation
- [USPS Developer Portal](https://developer.usps.com/)
- [UPS Developer Portal](https://developer.ups.com/)
- [FedEx Developer Portal](https://developer.fedex.com/)
- [Amazon Shipping API](https://shipping.amazon.com/api-integration) (merchants only)

### Third-Party APIs
- [TrackingMore](https://www.trackingmore.com/tracking-api)
- [AfterShip](https://www.aftership.com/)
- [EasyPost](https://www.easypost.com/)
- [Ship24](https://www.ship24.com/)

### Open Source Projects
- [ts-shipment-tracking](https://github.com/0xA-10/ts-shipment-tracking) - Unified wrapper for FedEx, UPS, USPS APIs

---

**Last Updated:** February 2026
**Status:** Current as of USPS API migration to new platform
