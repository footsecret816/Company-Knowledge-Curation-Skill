# Example — Business Conversation Patch

## Candidate
During ordinary business work, the operator says:
> Our partner factory has just added a new long-term production line for Product X, and this capability will be available for future projects.

The host Agent flags this as `COMPANY_UPDATE_CANDIDATE` and the operator approves review.

## Curation
1. Determine whether the capability is factory-specific or company-general.
2. Ask for/record the factory identity or approved source if needed.
3. Resolve the current company Pack through `company-data/REGISTRY.yaml`.
4. Compare with the current Pack.
5. If only one factory is confirmed, write under factory/product scope; do not claim every supplier can do it.
6. Update source/version metadata.
7. Formalize only after operator approval.
8. Patch the relevant files under `company-data/packs/<company-id>/`.
9. Update the Registry entry if version/status/update date changed.

## Counterexample
> For Customer A, the boss approved 30-day payment terms this time.

This is normally `CUSTOMER_SPECIFIC` + one-off approval → `EXCLUDED` from Company Pack and must not be published into the shared `company-data/packs/` knowledge source.
