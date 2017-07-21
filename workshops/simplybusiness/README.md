# Claims Dataset

## Policies

`policies.csv.gz` contains 4000 policies from 2010. Fields:

* policy_id: unique ID of the policy
* starting_date: date when the policy cover starts
* ending_date: date when the policy cover ends
* policy_type: type of the policy, possible values are shop, landlord and professional

## Claims

`claims.csv.gz` contains 164 claims of those 4000 policies. Fields:

* policy_id: ID of the policy that covers the claim
* reference: unique ID of the claim
* claim_carrier: name of the insurer that covers the claim
* peril: type of claim

## Claim Transactions

`claim_transactions.csv.gz` contains 2029 transactions that originated from those claims. Fields:

* transaction_id: unique ID of the transaction
* claim_reference: claim reference
* tx_date: date of the transaction
* payment_type: type of payment, possible values are reserve, payment and fee
* value: the value of the transaction, which can be positive or negative

