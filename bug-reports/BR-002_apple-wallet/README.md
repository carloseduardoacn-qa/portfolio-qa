# BR-002 — Apple Wallet: "Enter Password" button does not respond

| Field | Details |
|---|---|
| **Bug ID** | BR-002 |
| **Title** | Apple Wallet "Enter Password" button does not respond |
| **Severity** | Medium |
| **Priority** | Medium |
| **Environment** | iPhone 13 — iOS 26.5.2 |
| **Application** | Apple Wallet |
| **Language** | English |
| **Connection** | Wi-Fi |

---

## Description

The **"Enter Password"** button displayed on the Apple Wallet verification screen does not respond when tapped.

The issue was observed after the iPhone had previously been placed in **Lost Mode** and subsequently removed from Lost Mode.

---

## Preconditions

- Payment cards are already added to Apple Wallet.
- The device was previously placed in Lost Mode.
- The device has subsequently exited Lost Mode.
- Apple Wallet displays the **"Apple Account Verification Required"** screen.

---

## Steps to Reproduce

1. Open **Apple Wallet**.
2. Wait for the **"Apple Account Verification Required"** screen to appear.
3. Tap **"Enter Password"**.
4. Observe the behavior.

---

## Expected Result

The **"Enter Password"** button should respond to the tap and initiate the Apple Account authentication flow.

---

## Actual Result

The **"Enter Password"** button does not respond when tapped.

- No authentication screen is displayed.
- No error message is shown.
- No visual feedback indicates that the button was activated.

---

## Reproducibility

**100%** under the observed conditions.

---

## Impact

The user cannot proceed with the Apple Account verification flow through the provided **"Enter Password"** action, potentially preventing normal access to Apple Wallet functionality.

---

## Evidence

- **Video:** [Loom](LOOM_LINK)
- **Screenshots:** Included in the repository

---

## Additional Notes

The issue was first observed after the device exited **Lost Mode**.

The relationship between Lost Mode and the observed behavior has not been established as the root cause.

---

## Portfolio Context

Bug report developed as part of a practical **QA portfolio**, based on exploratory testing performed on a real device.
