# Fact Rules

## Canonical states

### CONFIRMED
Directly supported by a source or explicit operator confirmation.

### TO_CONFIRM
Source exists but one or more critical dimensions are unclear: scope, freshness, meaning, holder, product coverage, current validity, etc.

### INFERRED
A model conclusion or plausible interpretation not explicitly supported. Never formalize as Company fact.

### CONFLICT
Two or more claims cannot both be treated as active at the same scope/time and precedence is unresolved.

### SUPERSEDED
A previously valid fact that has been explicitly replaced by a newer confirmed fact.

### EXCLUDED
Information that may be true but belongs outside long-term Company Knowledge.

## Source precedence
There is no universal ranking that makes every conflict disappear. Use these factors together:

1. explicit operator correction;
2. source freshness/effective date;
3. source authority (official certificate, approved internal source, supplier note, marketing copy, etc.);
4. exact scope match;
5. consistency with other confirmed evidence.

If these do not resolve the conflict reliably, keep `CONFLICT`.

## Freshness
Never assume newest file = newest truth if the file itself is copied/archived/undated.

Use actual effective dates when available.

## Supersession
When a new confirmed fact replaces an old fact:
- keep enough history to know the old fact was superseded;
- update the active Pack wording;
- add source/date where possible;
- avoid retaining both old and new statements as if active simultaneously.

## Negative facts / withdrawn capability
Treat explicit removal as important Company Knowledge when long-term.

Examples:
- a product line discontinued;
- a certification expired and not renewed;
- a factory capability no longer available.

Do not simply delete history without trace if downstream decisions could otherwise reuse stale assumptions.

## Numbers
Preserve exact numbers only when they are stable/reusable and supported.

Examples that may belong:
- stable facility size from approved company source;
- long-term capacity for a specific factory if scope is preserved.

Examples that usually do not belong:
- one quote price;
- one project's MOQ;
- one temporary lead time.

## Marketing language
Convert marketing copy into factual operational language only when the factual basis is supported.

`We are a world-leading supplier` → do not preserve as fact unless there is meaningful evidence and need.

`We have more than 20 years of industry experience` → may be admitted if supported by approved company source.

## Missing information
Do not “complete” a Company Pack by guessing missing fields.

An incomplete but truthful Pack is better than a complete-looking fabricated one.