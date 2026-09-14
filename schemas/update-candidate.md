# Company Update Candidate

Suggested fields:

```yaml
candidate_id: <id>
company_id: <company-id>
statement: <candidate fact>
source_type: conversation | document | operator-correction | other
source_reference: <reference>
detected_at: <timestamp/date>
proposed_scope: COMPANY_GENERAL | FACTORY_SPECIFIC | PRODUCT_SPECIFIC | MARKET_SPECIFIC | CERTIFICATE_HOLDER_SPECIFIC | PROJECT_SPECIFIC | CUSTOMER_SPECIFIC
evidence_state: CONFIRMED | TO_CONFIRM | INFERRED
operator_review_status: pending | approved-for-curation | rejected
notes: <optional>
```

A candidate is not formal Company Knowledge until curation and operator approval are complete.
