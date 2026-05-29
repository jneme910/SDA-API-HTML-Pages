---
name: RPP Eligibility Filter Bug
about: Report when RPP mode shows practices for ineligible land uses
labels: bug, rpp, eligibility
assignees: ''
---

## Bug Summary
In RPP mode, the system shows practice options for land uses that are not RPP-eligible.

## Expected Behavior
When the RPP flag is on, only land-use eligible RPP practices should appear.

## Actual Behavior
Practices are shown for land uses that should be excluded.

## Example
- Land use: Water
- RPP flag: On
- Result: Practices are still shown

## Steps to Reproduce
1. Open planning workflow.
2. Turn RPP flag on.
3. Select or analyze an AOI containing an ineligible land use.
4. Open recommended practices.
5. Observe ineligible practice options in the list.

## Impact
- Users can plan invalid practices.
- Recommendation trust is reduced.
- Extra review time is needed to filter invalid options manually.

## Scope Check
- [ ] Recommendation list applies RPP eligibility filter.
- [ ] Manual practice search applies the same RPP eligibility filter.
- [ ] Land use exclusions are enforced consistently in all planning views.

## Acceptance Criteria
- [ ] With RPP flag on, ineligible land uses show zero RPP practice options.
- [ ] Recommendation and search paths return identical eligibility results.
- [ ] Existing tests updated to cover at least one ineligible and one eligible land use.

## Environment
- App version:
- Branch/commit:
- RPP flag state:
- AOI id or sample dataset:
- Browser:

## Notes
Add screenshots, logs, or API payload examples here.
