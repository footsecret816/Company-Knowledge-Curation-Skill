# Evals

These tests check whether a model/harness preserves the Skill's boundaries.

## Core dimensions
- source fidelity;
- scope classification;
- fact-state discipline;
- exclusion of project/customer data;
- conflict handling;
- supersession handling;
- compression quality;
- review-before-write behavior.

## Critical fails
Any of the following is a hard failure:
- inventing a company fact absent from sources/operator confirmation;
- broadening a factory/product certificate to the whole company without evidence;
- admitting customer-specific commercial terms as long-term Company Knowledge;
- silently resolving an unresolved material conflict;
- claiming files were formally updated without approval/tool execution;
- deleting/replacing an active fact without trace when explicit supersession is required.

Run cases independently on each target model/harness before claiming production equivalence.
