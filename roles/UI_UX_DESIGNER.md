# Role: UI/UX Designer

**Companion to:** PRD-0001 Driver Hiring Application (v2.0)
**Reports to / Coordinates with:** Product Manager, Mobile Developer (handoff)
**Primary PRD Sections:** §7–9, §15–18

---

## 1. Mission

Design the customer, driver, and admin experiences so that every product rule in the PRD is discoverable and unambiguous to the end user — particularly the verification status of drivers and vehicles (§9, §13), the booking state a customer/driver is in at any moment (§14), and the confirmation-code/QR trip-start step (§15.5), which must feel like a natural, low-friction safety step rather than a chore.

## 2. Core Responsibilities

- Design the **onboarding flows** (§7 driver, §8 customer) as genuinely simple, small steps with a clear progress indicator — this is a stated Core Principle (§4), not just a nice-to-have.
- Design clear, distinct visual treatment for **verification badge states**: Pending, Correction Requested, Verified, Rejected (§13) — each needs to be instantly recognizable and carry the specific reason/note when relevant.
- Design the **saved vs. ad-hoc vehicle** selection experience (§9) so the distinction is obvious to a customer at booking time, and so a driver can clearly see "Verified" vs. "Unverified" vehicle status before deciding to accept a booking.
- Design both booking entry points (§15.1): a direct search-and-browse-drivers flow, and a broadcast-request flow with a clear "finding a driver" waiting state and appropriate messaging if the request is re-routed or expires.
- Design the **driver accept/reject interaction**, including the message from the customer and (where useful) an indication of the response time window.
- Design the **confirmation code/QR screen** (§15.5) for both customer and driver — this is a safety-critical UI moment and should be simple, hard to bypass accidentally, and clear about why it exists.
- Design the **chat interface** (§15.3) and the **phone-number-exchange opt-in prompt** (§15.4) as a clearly two-sided, consentful interaction — not implied or automatic.
- Design the **admin screens** (§18): pending queue with filters, submission detail view, and the Approve / Reject / Request Re-upload actions — with reject and request-re-upload both requiring a reason to be entered before confirming.
- Design the **notification center** and individual notification treatments for every notification type in §19.
- Ensure designs do not imply features that are explicitly out of Phase 1 scope (§21) — e.g. no live map/tracking UI, no wallet/payment UI, no Aadhaar/AI-verification UI elements.



## 3. Key Design Deliverables (Non-Exhaustive)


| Deliverable                                                  | PRD Reference |
| ------------------------------------------------------------ | ------------- |
| Driver onboarding flow (9 screens)                           | §7            |
| Customer onboarding flow                                     | §8            |
| Verification badge component set (all states)                | §13           |
| Saved vehicle list + ad-hoc entry form                       | §9            |
| Direct-book and broadcast-request booking flows              | §15.1         |
| Booking detail screen with state-appropriate actions         | §14, §16, §17 |
| Confirmation code/QR screen                                  | §15.5         |
| Admin verification queue + submission detail + action modals | §12, §18      |
| Notification center                                          | §19           |




## 4. Inputs Needed From Others

- Product Manager: confirmed product rules and scope boundaries, resolution of open questions affecting UX (e.g. §22.4 Correction Requested vs. Rejected policy affects how many distinct visual states are needed).
- Solution Architect / Backend Developer: any technical constraint on what state info can realistically be shown in real time.



## 5. Outputs Delivered To Others

- Finalized screen designs and component specs — to Mobile Developer for implementation.
- Design rationale tied to PRD sections — to Product Manager for validation against product rules.



## 6. Out of Scope

- Implementation (Mobile Developer's role)
- Product rule decisions (Product Manager's role — UX flags friction, doesn't unilaterally change rules)
- Web application design (future phase per §4)

