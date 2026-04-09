# 📨 Facebook Messenger API (v23) — Send Text, Image & Video

![Facebook Graph API](https://img.shields.io/badge/Graph_API-v23.0-1877F2?style=for-the-badge&logo=facebook&logoColor=white)
![Method](https://img.shields.io/badge/Method-cURL-black?style=for-the-badge)
![Messages](https://img.shields.io/badge/Supports-Text%20%7C%20Image%20%7C%20Video-green?style=for-the-badge)

A developer reference for sending outbound messages to Facebook users via the Messenger Platform using **Graph API v23.0** and cURL.

---

## 🔑 Prerequisites

Before running any request, make sure you have:

- A Facebook Page with **`pages_messaging`** permission granted
- A valid **Page Access Token** for that Page
- The recipient's **PSID** — the user must have initiated a conversation with your Page first

---

## 📋 Placeholder Reference

Replace these values in every request below:

| Placeholder | Description |
|---|---|
| `<PAGE_ID>` | Your Facebook Page's unique ID |
| `<PAGE_ACCESS_TOKEN>` | Long-lived or short-lived Page Access Token |
| `<USER_ID>` | Recipient's Page-Scoped ID (PSID) |
| `<IMAGE_URL>` | Publicly accessible direct image URL |
| `<VIDEO_URL>` | Publicly accessible direct video URL |

> ⚠️ All media URLs must be publicly hosted and reachable — private or localhost URLs will fail.

---

## 1️⃣ Send a Text Message

Delivers a plain-text message to the specified recipient.

```bash
curl -X POST "https://graph.facebook.com/v23.0/<PAGE_ID>/messages" \
  -H "Authorization: Bearer <PAGE_ACCESS_TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{
    "messaging_type": "RESPONSE",
    "recipient": { "id": "<USER_ID>" },
    "message": { "text": "Hello from Graph API v23!" }
  }'
```

---

## 2️⃣ Send an Image Message

Sends an image attachment using a direct URL. Setting `is_reusable: true` caches the asset on Facebook's servers so it can be reused in future requests without re-uploading.

```bash
curl -X POST "https://graph.facebook.com/v23.0/<PAGE_ID>/messages" \
  -H "Authorization: Bearer <PAGE_ACCESS_TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{
    "recipient": { "id": "<USER_ID>" },
    "message": {
      "attachment": {
        "type": "image",
        "payload": {
          "url": "<IMAGE_URL>",
          "is_reusable": true
        }
      }
    }
  }'
```

---

## 3️⃣ Send a Video Message

Sends a video attachment via URL. The same `is_reusable` flag applies — recommended for any asset you expect to send more than once.

```bash
curl -X POST "https://graph.facebook.com/v23.0/<PAGE_ID>/messages" \
  -H "Authorization: Bearer <PAGE_ACCESS_TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{
    "recipient": { "id": "<USER_ID>" },
    "message": {
      "attachment": {
        "type": "video",
        "payload": {
          "url": "<VIDEO_URL>",
          "is_reusable": true
        }
      }
    }
  }'
```

---

## 📌 Key Constraints

| Constraint | Detail |
|---|---|
| **Permission required** | Page must have `pages_messaging` approved |
| **24-hour window** | Outside the standard window, only approved message tags are permitted |
| **User-initiated only** | The recipient must have messaged your Page first before you can reach them |
| **Media hosting** | All image and video assets must be served over a public HTTPS URL |
| **API version** | These examples target **Graph API v23.0** specifically |

---

*For the full Messenger Platform documentation, visit [developers.facebook.com/docs/messenger-platform](https://developers.facebook.com/docs/messenger-platform).*
