---
name: RPP Planning Improvements
about: Track AOI polygon, concern sorting, RPP eligibility, and existing-practice model updates
labels: enhancement, planning, rpp
assignees: ''
---

## Summary
Implement planning workflow improvements so users can see what acres are being assessed, get cleaner concern ranking, and only receive valid RPP practice options.

## Problem Statement
Current behavior has five gaps:
- Land use polygons and planned-practice polygons are not consistently created after AOI confirmation.
- Resource concerns are not consistently ordered by priority.
- Low and None concerns add unnecessary scrolling noise.
- RPP mode still suggests practices for non-RPP land uses.
- Existing practices are not loaded into the model before planning.

## Scope
### 1) AOI and land use polygon creation
- After land use is confirmed and AOI analysis runs, create and display land use polygons.
- Show acres for each polygon and a total for assessed area.
- When a new practice is planned, create a practice polygon linked to the source land use polygon.

### 2) Concern ordering and visibility
- Sort concerns in this exact order: High, Moderate, Low, None.
- Keep ordering stable within each priority band.
- Hide Low and None by default.
- Add a toggle to show Low and None when needed.

### 3) RPP eligibility filtering
- When RPP flag is on, filter recommended practices to land-use eligible options only.
- Do not show practices for land uses that are not in RPP eligibility rules.
- Apply the same eligibility rule in both recommendations and manual practice search.

### 4) Existing practices in model
- Load existing practices before generating recommendations.
- Existing practices must influence concern scoring and recommendation ranking.
- Prevent duplicate recommendations where an existing practice already addresses a concern.

## Business Rules
- Priority order is fixed: High > Moderate > Low > None.
- Default UI should optimize for actionability: show High and Moderate first, hide Low and None initially.
- In RPP mode, eligibility rules are mandatory and must be enforced for all recommendation paths.
- Practice planning should be spatially explicit: every planned practice should have a linked shape.

## Data and API Notes
- AOI analysis output must include polygon geometry and acre calculations.
- Practice planning output must store geometry and relationship to land use polygon id.
- RPP eligibility should reference a single source of truth table or service.
- Existing-practice inputs must be ingested before recommendation scoring is executed.

## Acceptance Criteria
- [ ] Running AOI analysis after land use confirmation creates visible land use polygons with acre totals.
- [ ] Planning a practice creates a visible practice polygon tied to a land use polygon.
- [ ] Concerns are sorted High, Moderate, Low, None in all concern views.
- [ ] Low and None are hidden by default and visible only when toggle is enabled.
- [ ] With RPP flag on, ineligible land uses return no RPP practice options.
- [ ] Recommendation list and manual search both honor the same RPP filter.
- [ ] Existing practices are loaded before scoring and change recommendation output.
- [ ] Duplicate recommendations are prevented when existing practices already address a concern.

## Test Cases
### Functional
- Confirm land use, run AOI, verify polygons and acres display.
- Plan one practice and verify shape creation plus linkage metadata.
- Verify concern ordering across multiple farms and mixed priority sets.
- Toggle Low and None visibility on and off.
- Enable RPP and verify water land use does not receive non-eligible suggestions.
- Add existing practices and verify recommendation list changes.

### Regression
- Non-RPP mode still returns full eligible practice set for the selected land use.
- Export/reporting paths still include the same concern and practice records.
- Existing geometry drawing and editing behavior remains intact.

## Definition of Done
- [ ] Feature behavior matches acceptance criteria.
- [ ] Unit and integration tests added or updated.
- [ ] QA checklist executed with at least one RPP-on and one RPP-off scenario.
- [ ] Documentation updated for concern filters, RPP rules, and existing-practice loading order.
- [ ] Product owner validation completed on a real sample AOI.

## Implementation Notes
Add links to design docs, PRs, and API contracts here.
