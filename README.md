![GitHub](https://img.shields.io/github/license/ncecowboy/Home-Assistant-Mail-And-Packages)
![GitHub Repo stars](https://img.shields.io/github/stars/ncecowboy/Home-Assistant-Mail-And-Packages)
![GitHub release (latest by date)](https://img.shields.io/github/v/release/ncecowboy/Home-Assistant-Mail-And-Packages)
[![hacs_badge](https://img.shields.io/badge/HACS-Default-orange.svg)](https://github.com/hacs/integration)
![Pytest](https://github.com/ncecowboy/Home-Assistant-Mail-And-Packages/workflows/Pytest/badge.svg?branch=master)
![CodeQL](https://github.com/ncecowboy/Home-Assistant-Mail-And-Packages/workflows/CodeQL/badge.svg?branch=master)
![Validate with hassfest](https://github.com/ncecowboy/Home-Assistant-Mail-And-Packages/workflows/Validate%20with%20hassfest/badge.svg?branch=master)

![GitHub contributors](https://img.shields.io/github/contributors/ncecowboy/Home-Assistant-Mail-And-Packages)
![Maintenance](https://img.shields.io/maintenance/yes/2026)
![GitHub commit activity](https://img.shields.io/github/commit-activity/y/ncecowboy/Home-Assistant-Mail-And-Packages)
![GitHub commits since tagged version](https://img.shields.io/github/commits-since/ncecowboy/Home-Assistant-Mail-And-Packages/0.3.3-2/dev)
![GitHub last commit](https://img.shields.io/github/last-commit/ncecowboy/Home-Assistant-Mail-And-Packages/dev)
![Codecov branch](https://img.shields.io/codecov/c/github/ncecowboy/Home-Assistant-Mail-And-Packages/master)

## About Mail and Packages integration

The [Mail and Packages integration](https://github.com/ncecowboy/Home-Assistant-Mail-And-Packages) creates sensors for [supported shippers](https://github.com/ncecowboy/Home-Assistant-Mail-And-Packages/wiki/Supported-Shipper-Requirements) to show a snapshot of mail and **packages that are scheduled to be delivered the current day**. For the packages that are scheduled for delivery the current day a count of in transit and delivered packages will be provided. It also generates the number of USPS mail pieces and provides a rotating GIF of the USPS provided images of the mail, if available, for the current day.

### Key Features
- **📦 13 Supported Shippers** - USPS, UPS, FedEx, Amazon, DHL, Canada Post, Royal Mail, Australia Post, Hermes, Poczta Polska, InPost, DPD Poland, and GLS
- **📸 USPS Informed Delivery Images** - Automatic download and GIF/MP4 creation from daily mail images
- **🏪 Amazon Hub Locker Support** - Detects pickup codes and provides dedicated tracking
- **🌍 Multi-Language Support** - Recognizes notifications in English, Italian, Polish, and German
- **🔒 Privacy First** - All processing done locally, no external services or data sharing
- **📊 50+ Sensors** - Comprehensive tracking of delivered, in-transit, and exception packages per shipper
- **📷 2 Cameras** - USPS mail images and Amazon delivery photos
- **🔔 Custom Services** - On-demand camera refresh and more

## Credits:

- Huge contributions from [@firstof9](https://github.com/firstof9) moving the project forward and keeping it active!
  <br/>

## How it works

From your instance of HASS, the [Mail and Packages integration](https://github.com/ncecowboy/Home-Assistant-Mail-And-Packages) connects to the email account you supply where your shipment notifications are sent. It reviews at the subject lines of the current day's emails from the [supported shippers](https://github.com/ncecowboy/Home-Assistant-Mail-And-Packages/wiki/Supported-Shipper-Requirements) and counts the subject lines that match known language from the [supported shippers](https://github.com/ncecowboy/Home-Assistant-Mail-And-Packages/wiki/Supported-Shipper-Requirements) about their transit status. For USPS Informed delivery emails, it also downloads the mail images to combine them into a rotating GIF. 
See the WIKI [information on how this works](https://github.com/ncecowboy/Home-Assistant-Mail-And-Packages/wiki).

_**The email can not be deleted until the next day**_. You can have your email filtered into a folder and have the integration watch that folder.

The image will revert back to the no mail graphic after the first email check after midnight, local time.

* **All procedures are done locally on your machine.**
* **No external services are used to process your email.**
* **No data is sent outside of your local instance of Home Assistant**

##### *Privacy / Security Note
Please note that files stored in the `www` Home Assistant folder are [publicly accessible](https://www.home-assistant.io/integrations/http/#hosting-files) unless you have taken security measures outside of Home Assistant to secure it. For increased security and simplicity the USPS Informed Delivery image name is random by default and no longer has the option to turn it on/off. Two new sensors have been created that provide the local file path or a web accessible url for use in displaying or sending in various Home Assistant notification methods.

* `sensor.mail_image_system_path`
* `sensor.mail_image_url` - Requires that either `External_URL` or `Internal_URL` is defined in the general configuration options in Home Assistant.

## Installation

### HACS (Recommended)

1. Open HACS in your Home Assistant instance
2. Go to "Integrations"
3. Search for "Mail and Packages"
4. Click "Download"
5. Restart Home Assistant
6. Go to Settings → Devices & Services → Add Integration
7. Search for "Mail and Packages" and follow the configuration steps

### Manual Installation

1. Download the latest release from [GitHub releases](https://github.com/ncecowboy/Home-Assistant-Mail-And-Packages/releases)
2. Extract the `mail_and_packages` folder to your `custom_components` directory
3. Restart Home Assistant
4. Go to Settings → Devices & Services → Add Integration
5. Search for "Mail and Packages" and follow the configuration steps

## Requirements

- **Email Account** - A dedicated email account (Gmail, Outlook, etc.) where shipping notifications are sent
- **IMAP Access** - IMAP must be enabled on your email account
- **USPS Informed Delivery** (Optional) - Register at [USPS Informed Delivery](https://informeddelivery.usps.com/) for mail image features
- **Shipping Notifications** - Sign up for delivery notifications with your preferred shippers:
  - [USPS Informed Delivery](https://informeddelivery.usps.com/)
  - [UPS My Choice](https://www.ups.com/us/en/services/tracking/mychoice.page)
  - [FedEx Delivery Manager](https://www.fedex.com/en-us/delivery-manager.html)
  - Amazon (already enabled for most accounts)
- **FFmpeg** (Optional) - Required only if you want MP4 video generation from mail images

## Supported Shippers

The integration currently supports **13 international shipping carriers**:

| Shipper | Delivered | In Transit | Exceptions | Tracking |
|---------|-----------|------------|------------|----------|
| **USPS** (USA) | ✅ | ✅ | ✅ | ✅ |
| **UPS** | ✅ | ✅ | ✅ | ✅ |
| **FedEx** | ✅ | ✅ | ❌ | ✅ |
| **Amazon** | ✅ | ✅ | ✅ | ✅ |
| **Canada Post** | ✅ | ❌ | ❌ | ❌ |
| **DHL** | ✅ | ✅ | ❌ | ✅ |
| **Hermes** (UK) | ✅ | ✅ | ❌ | ✅ |
| **Royal Mail** (UK) | ✅ | ✅ | ❌ | ✅ |
| **Australia Post** | ✅ | ✅ | ❌ | ✅ |
| **Poczta Polska** (Poland) | ❌ | ✅ | ❌ | ✅ |
| **InPost** (Poland) | ✅ | ✅ | ❌ | ✅ |
| **DPD** (Poland) | ✅ | ✅ | ❌ | ✅ |
| **GLS** | ✅ | ✅ | ❌ | ✅ |

See the [Wiki - Supported Shipper Requirements](https://github.com/ncecowboy/Home-Assistant-Mail-And-Packages/wiki/Supported-Shipper-Requirements) for email configuration details for each shipper.

## Configuration

The integration is configured through the Home Assistant UI. After installation, add it via:

**Settings → Devices & Services → Add Integration → Mail and Packages**

### Basic Configuration

| Setting | Required | Default | Description |
|---------|----------|---------|-------------|
| **Host** | Yes | - | Your email server address (e.g., `imap.gmail.com`) |
| **Port** | Yes | 993 | IMAP port (typically 993 for SSL) |
| **Username** | Yes | - | Your email address |
| **Password** | Yes | - | Your email password or app-specific password |
| **Folder** | No | INBOX | Email folder to monitor (use quotes for folders with spaces) |

### Advanced Options

| Setting | Default | Description |
|---------|---------|-------------|
| **Scan Interval** | 5 minutes | How often to check for new emails (minimum 5 minutes) |
| **IMAP Timeout** | 30 seconds | Timeout for IMAP connection (minimum 10 seconds) |
| **GIF Duration** | 5 seconds | Animation speed for mail image GIFs |
| **Image Security** | Enabled | Randomize image filenames for privacy |
| **Generate MP4** | Disabled | Create MP4 videos from mail images (requires FFmpeg) |
| **Amazon Forwards** | - | Comma-separated list of emails for forwarded Amazon notifications |
| **Amazon Days** | 3 | How many days back to look for Amazon packages |
| **Allow External Access** | Disabled | Allow images to be accessed externally |
| **Custom Image** | Disabled | Use a custom image when no mail is present |

For detailed configuration instructions, see [Wiki - Configuration and Email Settings](https://github.com/ncecowboy/Home-Assistant-Mail-And-Packages/wiki/Configuration-and-Email-Settings).

## Sensors

The integration creates comprehensive sensors for tracking your deliveries:

### Status Sensors
- `sensor.mail_updated` - Timestamp of last successful update

### Per-Shipper Sensors
Each supported shipper gets multiple sensors (where applicable):
- `sensor.mail_<shipper>_delivered` - Packages delivered today
- `sensor.mail_<shipper>_delivering` - Packages in transit for today
- `sensor.mail_<shipper>_exception` - Packages with delivery issues
- `sensor.mail_<shipper>_packages` - Total packages from this shipper

### USPS-Specific Sensors
- `sensor.mail_usps_mail` - Number of mail pieces (from Informed Delivery)
- `sensor.mail_image_system_path` - Local file path to mail images
- `sensor.mail_image_url` - Web-accessible URL for mail images

### Amazon-Specific Sensors
- `sensor.mail_amazon_hub` - Amazon Hub Locker packages with pickup code in attributes

### Aggregate Sensors
- `sensor.mail_packages_delivered` - Total packages delivered today (all shippers)
- `sensor.mail_packages_in_transit` - Total packages in transit (all shippers)

## Cameras

- **`camera.mail_usps_camera`** - Rotating GIF/MP4 of your USPS Informed Delivery mail images
- **`camera.mail_amazon_delivery_camera`** - Amazon package delivery photos

## Services

### `mail_and_packages.update_image`
Manually refresh the mail camera(s) to fetch the latest images.

**Parameters:**
- `entity_id` (optional): Specific camera entity to refresh (e.g., `camera.mail_usps_camera`). Leave blank to refresh all cameras.

**Example:**
```yaml
service: mail_and_packages.update_image
data:
  entity_id: camera.mail_usps_camera
```

## Support & Documentation

### Setup & Configuration
- [Configuration and Email Settings](https://github.com/ncecowboy/Home-Assistant-Mail-And-Packages/wiki/Configuration-and-Email-Settings)
- [Supported Shipper Requirements](https://github.com/ncecowboy/Home-Assistant-Mail-And-Packages/wiki/Supported-Shipper-Requirements)
- [Troubleshooting](https://github.com/ncecowboy/Home-Assistant-Mail-And-Packages/wiki/Troubleshooting)

### Templates & Examples
- [USPS Informed Delivery Image](https://github.com/ncecowboy/Home-Assistant-Mail-And-Packages/wiki/USPS-Informed-Delivery-Image)
- [Text Summary](https://github.com/ncecowboy/Home-Assistant-Mail-And-Packages/wiki/Mail-Summary-Message)
- [Notifications](https://github.com/ncecowboy/Home-Assistant-Mail-And-Packages/wiki/Notifications)

### Issues & Feature Requests
- [GitHub Issues](https://github.com/ncecowboy/Home-Assistant-Mail-And-Packages/issues)
- [GitHub Discussions](https://github.com/ncecowboy/Home-Assistant-Mail-And-Packages/discussions)
