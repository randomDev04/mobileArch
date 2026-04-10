

##MOBILE SYSTEM DESIGN — MASTER CHEAT SHEET

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

THE 4 LAYERS (apply to every problem)
  Layer 1 — What can user do?
  Layer 2 — What data do we need?
  Layer 3 — How does data move and change?
  Layer 4 — What can go wrong?

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

STATE CLASSIFICATION
  API data          → React Query
  Global client     → Zustand + MMKV
  Local UI          → useState
  Navigation        → React Navigation
  Never put API data in Redux

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

CACHE KEYS
  pattern: feature:resource:identifier
  example: product:detail:item_892
  always use a key factory — never hardcode strings
  invalidate by prefix after writes

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

NETWORK LAYER (in order)
  1. Axios client — one instance, whole app
  2. Request interceptor — token, request ID, adaptive timeout
  3. Response interceptor — 401 handling, token refresh queue
  4. Retry — exponential backoff, retryable status codes only
  5. API functions — thin wrappers, no logic

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

PAYMENT SYSTEM
  States: IDLE → INITIATING → PROCESSING
          → SUCCESS | FAILED | UNKNOWN
  UNKNOWN = money may have moved, never show FAILURE
  FAILED  = request never left device, safe to retry
  Write to MMKV BEFORE request leaves device
  Idempotency key = deterministic (userId+orderId+amount)
  On app resume → poll server → resolve UNKNOWN
  After 5 polls → push notification channel takes over

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

REAL TIME TRACKING
  Two channels:
    Push notification → state changes (order picked, delivered)
    WebSocket         → live location stream
  Location trigger → hybrid (100m moved OR 15s elapsed)
  On app foreground → show last known location first
                   → then REST sync → then WebSocket resume
  Heartbeat every 30s → detect zombie connections
  Battery → adaptive accuracy based on speed and battery level

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

INTERVIEW STRUCTURE (first 2 minutes)
  1. Clarify scope
  2. State your approach
  3. Name the hardest constraint first
  4. Build architecture

EVERY ANSWER needs:
  WHAT  — the solution
  WHY   — the reasoning
  WHY NOT — the trade-off you rejected

I DON'T KNOW → "My instinct is X — is that the right direction?"
               Never go silent. Never make something up.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
