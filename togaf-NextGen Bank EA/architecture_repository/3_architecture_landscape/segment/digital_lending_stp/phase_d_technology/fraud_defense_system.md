# Phase D: Technology Architecture - Fraud Defense System

This document specifies the real-time security safeguards, device telemetry capture, biometric liveness specifications, and API rate-limiting rules used to mitigate cyber-fraud and credit risk.

---

## 1. Mobile Device Fingerprinting Telemetry

To detect emulators, automated bot scripts, and compromised operating systems (rooted/jailbroken), the native Android/iOS SDKs collect device parameters before submitting any loan application.

### Telemetry Payload Schema (JSON)
```json
{
  "deviceTelemetry": {
    "os": "Android",
    "osVersion": "13.0.0",
    "sdkVersion": "33",
    "brand": "Samsung",
    "model": "SM-G998B",
    "fingerprint": "samsung/o1s/o1s:13/TP1A.220624.014/G998BXXU5DVK3:user/release-keys",
    "isRootedOrJailbroken": false,
    "isEmulator": false,
    "developerOptionsEnabled": false,
    "bootloaderUnlocked": false,
    "appIntegrityToken": "eyJhbGciOiJSUzI1NiIsImt5...[Google Play Integrity Attestation Token]",
    "network": {
      "carrier": "Jio",
      "ipAddress": "49.36.12.84",
      "macAddressHash": "f8d8b9821817bb8eeea217b18cbcf98492ae4c18",
      "vpnDetected": false,
      "torDetected": false
    },
    "hardware": {
      "screenResolution": "1440x3200",
      "screenBrightness": 0.65,
      "batteryLevel": 0.88,
      "freeDiskSpaceBytes": 42949672960
    }
  }
}
```

---

## 2. Biometric Liveness Verification Standards

During customer onboarding, identity verification is conducted using face matching and interactive liveness checks to prevent spoofing (e.g. photos, pre-recorded videos, synthetic deepfakes).

```
   [Camera Feed Capture] ──► [Passive Liveness Check] ──► [Active Gesture Challenge] 
                                                                    │
   [Target Matching] ◄────── [Face Feature Extraction] ◄────────────┘
         │
    (Aadhaar/PAN Database Photo)
```

* **Passive Liveness Detection:** Employs deep convolutional neural networks (CNNs) to analyze skin texture, depth parameters, and edge reflections without requiring user movement.
* **Active Gesture Challenge:** Prompt users to execute randomized micro-actions (e.g., blink twice, nod, tilt head 15 degrees right) to verify live response.
* **Threshold Match Metrics:**
  * **Liveness Confidence Score:** Must exceed `98.5%` to pass.
  * **Face Matching Threshold:** Comparing extracted face vector representations from the selfie to the identity document (PAN/Aadhaar) using Cosine Similarity:
    $$\text{Cosine Similarity} = \frac{A \cdot B}{\|A\| \|B\|} \ge 0.82 \quad (\text{equivalent to } 99\\% \text{ confidence accuracy}).$$

---

## 3. Redis Rate Limit Velocity Configurations

Rate limiting protects APIs against denial-of-service (DoS) attacks and brute-force testing. We implement the **Sliding Window Log** algorithm using Redis.

### Rate Limit Matrix
| Target Endpoint | Limit Rules | Storage Key Pattern | Action on Threshold Exceeded |
| :--- | :--- | :--- | :--- |
| **OTP Send Request** | Max 5 requests / hour | `rate:otp:send:<mobile>` | HTTP 429, block OTP generation for 30 minutes. |
| **Login Attempts** | Max 10 attempts / 5 mins | `rate:login:ip:<ip_hash>` | HTTP 429, force CAPTCHA verification. |
| **Loan Submission** | Max 3 attempts / month | `rate:loan:sub:<cust_id>` | HTTP 403, flag application for manual underwriting review. |

### Redis Lua Script for Sliding Window Rate Limiting
```lua
-- KEYS[1]: Rate limit identifier (e.g. 'rate:otp:send:+919999999999')
-- ARGV[1]: Current UNIX timestamp (seconds)
-- ARGV[2]: Window size (seconds)
-- ARGV[3]: Maximum capacity inside the window

local window_start = tonumber(ARGV[1]) - tonumber(ARGV[2])
local key = KEYS[1]

-- Remove timestamps older than the current window start
redis.call('ZREMRANGEBYSCORE', key, '-inf', window_start)

-- Count entries currently inside the window
local current_requests = redis.call('ZCARD', key)

if current_requests < tonumber(ARGV[3]) then
    -- Add the current request timestamp
    redis.call('ZADD', key, ARGV[1], ARGV[1])
    -- Set TTL to ensure key cleans up if inactive
    redis.call('EXPIRE', key, tonumber(ARGV[2]))
    return 1 -- Allowed
else
    return 0 -- Rejected
end
```

---

## 4. Geo-Blocking and Proxy Defense (MaxMind Rules)

The system integrates MaxMind GeoIP2 databases inside the Kong API Gateway layer to enforce geography-based access controls:
* **Allow-list Country Code:** `IN` (India). Requests from all other countries are blocked with `HTTP 403 Forbidden` unless the source IP matches authenticated corporate VPN networks.
* **Anonymous IP / Proxy Protection:** Requests from known proxy services, hosting providers (AWS, Azure, GCP, DigitalOcean), Tor exit nodes, and VPN ranges are automatically blocked at the load balancer.

---

## 5. Mule Account Checking Strategy

To prevent money laundering and funds diversion to disposable "mule" bank accounts:
1. **Name Match Verification:** Performs a "penny drop" verification check (sending ₹1 via IMPS) to query the beneficiary account holder name. The returned name must match the onboarding name with a minimum Levenshtein Distance similarity score of `0.85`.
2. **Account Age and Velocity Checks:** Queries bank APIs for account age where available. Newly created accounts (less than 30 days old) or accounts experiencing recent high-velocity, high-volume transactions without corresponding balance growth are flagged.
3. **Blacklist Reference Database:** Cross-references the bank account number and IFSC against NPCI/RBI blacklists of reported mule accounts.
