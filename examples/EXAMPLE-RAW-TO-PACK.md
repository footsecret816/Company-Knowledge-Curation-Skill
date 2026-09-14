# Example — Raw Materials to Company Pack

## Raw inputs
Assume the operator supplies:
- one company profile PPT;
- one product catalogue;
- a factory audit certificate;
- a spreadsheet containing customer-specific quotes;
- a sales note saying a new product line is now offered long-term.

## Correct curation behavior

### Confirmed Company Knowledge
- stable company identity from approved profile;
- supported product families from catalogue;
- long-term new product line if operator confirms it;
- factory audit only at the actual holder/factory scope.

### TO_CONFIRM
- any certificate where validity/holder/product coverage is unclear;
- marketing claims with no supporting basis;
- inconsistent capacity figures across sources.

### Excluded
- customer-specific quote rows;
- one customer's payment terms;
- temporary delivery dates.

## Review Draft
The Skill should show what it proposes to write into each Pack file, plus `TO_CONFIRM`, conflicts and excluded items.

It should **not** immediately create a polished company profile that silently mixes all source content together.
