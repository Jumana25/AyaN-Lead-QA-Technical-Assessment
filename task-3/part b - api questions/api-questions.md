### 3.1 What are the highest-risk scenarios you would test on this endpoint?

| High-Risk Point                       | What to Validate                                                                                            |
|---------------------------------------|-------------------------------------------------------------------------------------------------------------|
| **Duplicate Transfers & Idempotency** | Retrying the same request must not create duplicate payments or debit the account twice.                    |
| **Insufficient Funds & Limits**       | Transfers exceeding available funds or transaction limits must be rejected without moving money.            |
| **Failure Handling (503 & Retries)**  | Retrying after a timeout or `503` must not duplicate a payment, even if the original request was processed. |

### 3.2 What is the Idempotency-Key for, how would you test that it works, and what should happen when a client retries after a network timeout or after receiving a 503?

* **Purpose:** Prevent the same payment from being executed more than once when a client retries a request.
* **Same key, same request:** Verify that repeated requests create only one payment and deduct the amount once.
* **Same key, different request:** Verify that reusing the key with different payment details is rejected.
* **Network timeout or 503:** Retry using the same key and verify that the payment is not duplicated, even if the original request was already processed.


### 3.3 How would you verify that the money actually moved — beyond checking that the API returned 201?

* Checking the status code alone is barely enough assertion.
* Use a GET API to verify the updated source account balance after deduction.
* Use another GET API to verify that the beneficiary's balance has been updated after receiving the money.
* Verify the transaction history on both accounts to confirm the correct amount, currency, reference, and transaction status.
* Verify that an account with a zero balance can successfully receive a payment and use the received funds in another transaction within a tight time frame.
* If manually tested, verify the database records as well, even if through tools.
