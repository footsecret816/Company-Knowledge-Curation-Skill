# Scope Rules

Correct scope is one of the most important protections in Company Knowledge.

## Scope levels

### COMPANY_GENERAL
A relatively stable fact describing the company overall.

Examples:
- company identity and location;
- core business model;
- long-term product families;
- general target customer types;
- reusable company SOP.

A company-general fact does **not** prove every factory/product/project shares that capability.

### FACTORY_SPECIFIC
A fact true for a named or identifiable factory/supplier only.

Examples:
- one factory's certification;
- one factory's machine/equipment capability;
- one factory's daily capacity;
- one factory's material process.

Do not convert into `COMPANY_GENERAL` unless evidence supports that broader statement.

### PRODUCT_SPECIFIC
A fact applying to one product, product family, material, construction or model.

Examples:
- a material option available for one category;
- a test report tied to one product;
- a tooling method used for a specific product line.

### MARKET_SPECIFIC
A fact limited by geography/channel/market.

Examples:
- packaging requirements used for one market;
- a distribution/channel strength in one region;
- market-specific compliance experience.

### CERTIFICATE_HOLDER_SPECIFIC
Use when the legal entity/factory/product covered by a certificate matters.

Record at minimum when known:
- holder/entity;
- issuing body;
- certificate type;
- validity period;
- covered facility/product/scope.

### PROJECT_SPECIFIC
A fact true only for one active/historical project.

Examples:
- project MOQ;
- current quote;
- approved lead time;
- specific sample deviation;
- one project test result.

Usually belongs in Project Memory, not Company Pack.

### CUSTOMER_SPECIFIC
A fact tied to one customer/account.

Examples:
- negotiated price;
- payment history;
- bespoke agreement;
- special packaging;
- customer-specific exception.

Belongs in Customer/Project Memory, not Company Pack.

## Promotion rule
Never promote a narrow fact to a broader scope merely because it sounds useful.

`FACTORY_SPECIFIC → COMPANY_GENERAL` requires evidence that the company can reliably provide that capability across relevant operations, not just one supplier instance.

`PRODUCT_SPECIFIC → COMPANY_GENERAL` requires evidence that the statement describes a general product-family capability rather than a single model.

`PROJECT_SPECIFIC → COMPANY_GENERAL` requires explicit confirmation that the project fact establishes a long-term rule/capability.

## Mixed statement rule
Split compound source sentences when they contain multiple scopes.

Example source:
> We have FDA documents from Factory A and can support private label projects.

Possible extraction:
- `FACTORY_SPECIFIC`: Factory A has the specified FDA-related document — exact document/scope `TO_CONFIRM` if unclear.
- `COMPANY_GENERAL`: company supports private-label projects — only if source/operator confirms this generally.

## Scope uncertainty
If a source says “we have CE/FDA/BSCI” without identifying holder/product/factory, do not automatically write a broad certification claim. Mark `TO_CONFIRM` and request actual scope.

## Downstream-use note
The Company Pack should preserve narrow scope even if downstream Agents later summarize it. This prevents a general business reply from accidentally becoming an unsupported project commitment.