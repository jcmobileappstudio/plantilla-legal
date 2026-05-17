# Plantilla Privacy Notice

**Last updated: May 17, 2026**
**Effective date: May 17, 2026**

Plantilla is published by JC Mobile App Studio LLC ("we", "us", "the company"). This Privacy Notice explains what information the Plantilla iOS app collects, how it is used, and the choices you have. Plantilla is designed around a simple principle: your data stays on your device unless you explicitly choose to use a feature that requires sending it elsewhere.

This Notice applies to the Plantilla iOS app distributed through the Apple App Store. It does not apply to other apps, websites, or services that may be linked from within Plantilla.

For questions about this Notice, contact jcmappstudio@gmail.com.

## Summary

For people who want the quick version:

- **What stays on your phone**: pay stubs you scan, W-2s you scan, your document vault, your direct deposit forms, your PTO entries, your tip and overtime logs, your incident logs, your FMLA timeline, your settings preferences. None of this leaves your phone unless you export or share it yourself.
- **What we do send to our proxy server**: the OCR text from a W-2 or HR letter when you ask for an AI explanation, your question and the relevant context when you ask the AI assistant a question, and the OCR text from a benefits document when you upload one to ask questions about it. We send nothing else, and nothing is stored on the server after the request finishes.
- **What we never collect**: your Social Security number, bank account numbers, credit card numbers, biometric data, advertising identifiers, your contacts, your location, your photo library outside of pictures you explicitly upload to a scanner, or browsing activity outside the app.
- **We do not show ads, we do not sell your information, and we do not use your information to train AI models.**
- **You can delete everything at any time** by deleting the app or by using the in-app delete controls described below.

## Who can use Plantilla

Plantilla is intended for adults 18 years of age or older. We do not knowingly collect any information from children under 13. If you believe a child has used Plantilla, contact us and we will help remove any associated data.

## What information we collect, where it lives, and why

We have organized this section by feature so you can see exactly what each feature does.

### Pay stub scanner

When you scan a pay stub, the image is captured by your camera or chosen from your photos library. Apple Vision (a system framework that runs entirely on your device) reads the text from the image. Plantilla's local parser identifies the wages and deductions. The image, the recognized text, and the parsed fields are saved to encrypted storage on your device only. The pay stub does not leave your phone.

The W-2 scanner and direct deposit scanner work the same way at the OCR layer.

### W-2 scanner AI assist

After the on-device OCR runs, Plantilla offers to send the recognized text to our proxy server so an AI model can identify the boxes more accurately. The proxy is operated by us at a Cloudflare Worker endpoint. The proxy forwards the text to Anthropic's Claude API and returns a structured JSON response. The proxy strips any Social Security numbers from the response before returning it. We do not log the request body, we do not retain the text, and the response is not stored on the server. Anthropic processes the request under their own enterprise data terms and does not use the content to train models.

Sending the text to the proxy is automatic when you scan a W-2. You can avoid this entirely by not using the W-2 scanner.

### HR letter translator

You take a photo of an HR letter. Apple Vision OCRs it on device, then the recognized text is sent to our proxy (same flow as the W-2 AI assist). The proxy forwards to Claude with a translation prompt and returns a plain-language summary. The text does not stay on the server.

### Ask Plantilla AI assistant

When you type or speak a question to the AI assistant, your question, your selected language, and your selected work state (a two-letter state code) are sent to our proxy. The proxy forwards to Claude and returns an answer. The question is not stored. Your assistant chat history is kept only on your device.

### Benefits document AI

When you upload a benefits guide or memo, Apple Vision OCRs the pages on device. The recognized text is sent to our proxy in chunks so the AI can answer follow-up questions about it. The text is processed per question and not retained on the server. Your questions and the AI's answers are stored on your device only.

### Compliance digest

When the app fetches the quarterly compliance digest, it makes an anonymous GET request to our proxy. No user data is sent. The proxy returns the same digest content to every user.

### Document vault

Documents you save (work authorization, driver's license, SSN card image, certifications, vaccination records, etc.) are stored encrypted on your device. They are never uploaded anywhere automatically. You can export a document yourself using iOS share sheet, which sends it to whatever destination you pick.

### Workplace incident logger

Incident entries (timestamp, notes, photos, witnesses) are stored encrypted on your device. They are never synced or uploaded. You can export a PDF of your log yourself if you decide to file a complaint.

### Direct deposit forms, PTO tracker, tip and overtime tracker, FMLA timeline, scheduled stub history

All on device only. Never uploaded.

### Settings and language preferences

Your language choice, work state, notification preferences, and other settings are stored in iOS UserDefaults on your device.

### Rate limiting

Our proxy uses a randomly generated client identifier (a 16-character string created on your device the first time you use the AI assistant) to enforce per-day rate limits and prevent abuse. The identifier is not tied to your Apple ID, your name, your email, your phone number, or any other personal information. It is stored in the proxy's Cloudflare KV namespace for 24 hours and then deleted automatically.

## What we do NOT collect

Plantilla does not collect, request, or transmit any of the following:

- Social Security numbers (the W-2 AI parser is explicitly instructed not to return one, and the proxy redacts any SSN-shaped value before returning the response)
- Bank account or routing numbers (the direct deposit scanner stores these on device only)
- Credit card or payment information (we do not currently support in-app purchases; future Premium will go through Apple's standard purchase flow which never exposes your card details to us)
- Your full name, email, mailing address, phone number, or any contact information
- Your location, GPS coordinates, IP-based location, or geographic activity
- Your contacts, calendar, photos library outside of pictures you explicitly upload, or browsing history
- Biometric data (Face ID, Touch ID, or any other)
- Apple's advertising identifier (IDFA) or any other advertising or tracking ID
- Analytics about your usage patterns
- Crash reports with identifying information

## How we use information

The limited information sent to our proxy is used solely to provide the feature you requested at the moment you requested it. We do not use any of the information for any other purpose. Specifically, we do not:

- Sell or rent your information to anyone
- Share your information with advertisers, data brokers, or analytics companies
- Use your information to train AI models
- Combine your information with data from other sources
- Profile you for advertising, employment decisions, credit decisions, or any other purpose
- Provide your information to your employer or any third party except as required by law

## Third parties we use

Plantilla relies on the following service providers to operate the AI-powered features:

- **Apple Inc.** provides the iOS platform, on-device OCR (Vision framework), and the App Store. Plantilla uses standard iOS APIs only.
- **Cloudflare, Inc.** hosts our proxy server. Cloudflare receives the request body when you use an AI feature (so it can forward to Claude) and the temporary rate-limit identifier. Cloudflare's logs may temporarily contain request metadata (IP address, timestamp, response code) as part of normal operations.
- **Anthropic PBC** processes AI requests through the Claude API. Anthropic does not use API content to train models. See Anthropic's API privacy terms.

We do not use Google Analytics, Facebook Pixel, Mixpanel, Amplitude, Segment, or any other analytics or tracking service.

## Data retention and deletion

**On your device**: data stays until you delete it. You can delete an individual document, pay stub, W-2, or incident from inside the app at any time. You can delete everything by deleting the app from your iPhone (iOS will remove the app's container including all local storage).

**On our proxy**: nothing is stored permanently. Request bodies are processed in memory and discarded once the response is sent. The rate-limit identifier (a random string with no link to your identity) is auto-deleted after 24 hours.

**With Anthropic**: API requests are subject to Anthropic's API data retention policy. As of this writing, Anthropic does not retain content for training and discards prompts on a short rolling basis as documented in their privacy terms.

You do not need to file a request to delete your data. Deleting the app removes everything we have on your device. There is no account to close because we do not maintain user accounts.

## Your rights

Depending on where you live, you may have specific rights under your local privacy law:

- **California (CCPA/CPRA)**: right to know, delete, correct, opt out of sale or sharing (we do not sell or share), and limit use of sensitive personal information. Plantilla collects very little personal information at all, and you can exercise all of these rights yourself by deleting data through the app or deleting the app. To submit a formal request, email us.
- **European Union and UK (GDPR/UK GDPR)**: right to access, rectify, erase, restrict, port, and object. Same notes as above: most of this is achievable through the app itself. To make a formal request, email us. The legal bases we rely on are consent (for AI features you opt into by using them) and legitimate interests (for rate-limiting abuse prevention).
- **Other U.S. states with privacy laws** (Colorado, Connecticut, Virginia, Utah, Texas, Florida, Oregon, Montana, Tennessee, Indiana, Iowa, Delaware, New Hampshire, New Jersey, Maryland, Minnesota, Rhode Island, Kentucky, and others as enacted): similar rights apply and the same response paths work.

To exercise rights or ask questions about how we handle data, email jcmappstudio@gmail.com. We respond within 30 days.

## Security

We protect data with these specific measures:

- All local files are written with iOS `.completeFileProtection`, which uses hardware-backed encryption tied to your device passcode. Files are inaccessible when your phone is locked.
- All network requests to our proxy use HTTPS (TLS 1.2 or higher).
- Our proxy does not log request bodies and discards data after the response is sent.
- The W-2 AI parser system prompt explicitly forbids returning Social Security numbers, and the proxy applies a regex scrubber as a backup.
- Plantilla has no user accounts, no passwords, and no tokens to be stolen.

No system is perfectly secure. We commit to notify users of any material data breach affecting Plantilla within the timelines required by applicable law.

## International users

Plantilla is operated from the United States. If you use the app from outside the U.S., requests sent to our proxy may be processed in the United States. By using the AI features, you consent to this transfer. If you do not want your data transferred to the U.S., do not use the AI features. The on-device features work entirely offline and do not transfer any data internationally.

## Children

Plantilla is intended for adults 18 and older. We do not knowingly collect information from anyone under 18. If you are a parent or guardian and believe your child has used the app, contact us and we will help remove any associated data.

## Changes to this Notice

We may update this Notice from time to time. If we make material changes, we will post the updated Notice in the app and on github.com/jcmappstudio/plantilla-legal with a new "Last updated" date. Continued use of the app after the effective date constitutes acceptance of the updated Notice.

For non-material changes (typo fixes, clarifications that do not change what we do with data), we update the date and post the change without further notice.

## Contact

JC Mobile App Studio LLC
Email: jcmappstudio@gmail.com
Website: www.jcmobileappstudio.com

For privacy-specific inquiries, please use the subject line "Plantilla Privacy" so we route the message correctly.

---

This Notice is general information about how Plantilla handles data. It is not legal advice. If you need legal advice about your specific situation, consult a qualified attorney in your jurisdiction.
