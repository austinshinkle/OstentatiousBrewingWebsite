# Feature Specification: Brewery Production Stages

**Feature Branch**: `002-production-stages`  
**Created**: January 31, 2026  
**Status**: Draft  
**Input**: User description: "Create a specification for brewery production stages (on-tap, in-production, recipe-design, recipe-archive)"

## User Scenarios & Testing *(mandatory)*

<!--
  IMPORTANT: User stories should be PRIORITIZED as user journeys ordered by importance.
  Each user story/journey must be INDEPENDENTLY TESTABLE - meaning if you implement just ONE of them,
  you should still have a viable MVP (Minimum Viable Product) that delivers value.
  
  Assign priorities (P1, P2, P3, etc.) to each story, where P1 is the most critical.
  Think of each story as a standalone slice of functionality that can be:
  - Developed independently
  - Tested independently
  - Deployed independently
  - Demonstrated to users independently
-->

### User Story 1 - Browse Beers in Current Production Stages (Priority: P1)

Users should be able to view beers organized by their production stage: "On Tap" (ready to drink), "In Production" (currently being brewed), "Recipe Design" (in planning), and "Recipe Archive" (completed/historical). This helps users understand the brewing workflow and find beers they're interested in.

**Why this priority**: This is the core feature of the brewery section. Users need to see what's available now and what's coming next. It directly addresses the main use case of showcasing recipes and current activity.

**Independent Test**: Can be tested by navigating to each production stage page and verifying that beers appear correctly organized by their status, with proper filtering and display of beer information.

**Acceptance Scenarios**:

1. **Given** a user navigates to the "On Tap" page, **When** the page loads, **Then** only beers marked as "on_tap" status are displayed with their details (name, style, ABV, IBU, SRM)
2. **Given** a user navigates to the "In Production" page, **When** the page loads, **Then** beers marked as "in_production" status are shown with a clear indication they are currently being brewed and include the relevant target details
3. **Given** a user navigates to the "Recipe Archive" page, **When** the page loads, **Then** all past beers are displayed in reverse chronological order (newest first) with full recipe details visible
4. **Given** a beer has no assigned logo image, **When** the page renders, **Then** a default placeholder image is displayed instead of a broken image

---

### User Story 2 - Filter Recipe Archive by Beer Style (Priority: P2)

Users should be able to filter the recipe archive by beer style/group (IPA, Lager, Stout, etc.) to quickly find recipes they're interested in. This makes it easier to explore the brewery's work in a particular style.

**Why this priority**: Important for usability when the recipe archive grows large. Allows users to discover recipes in their favorite styles without scrolling through the entire archive.

**Independent Test**: Can be tested by navigating to the Recipe Archive, clicking filter buttons, and verifying that only beers matching the selected style are displayed.

**Acceptance Scenarios**:

1. **Given** the Recipe Archive page has beers from multiple beer groups, **When** filter buttons are displayed, **Then** an "All" button and buttons for each unique beer group are shown
2. **Given** a user clicks a filter button for a specific beer group, **When** the click is processed, **Then** only beers in that group are displayed and other beers are hidden
3. **Given** a user clicks the "All" button, **When** the filter is applied, **Then** all archive beers are displayed again
4. **Given** only one beer group exists in the archive, **When** the page loads, **Then** no filter buttons are shown

---

### User Story 3 - View Detailed Beer Recipe Information (Priority: P1)

Users should be able to click on any beer card to view the complete recipe details including ingredients (malts, hops, yeast), brew instructions, original and final gravity, alcohol content, and brewing notes.

**Why this priority**: This is essential for users who want to brew their own recipes or study the brewing process. It's the primary value proposition of the site.

**Independent Test**: Can be tested by clicking on a beer card and verifying that the detailed recipe page loads with all recipe data displayed correctly.

**Acceptance Scenarios**:

1. **Given** a user is viewing a beer card, **When** they click on the beer image or "View Details" link, **Then** they are taken to the detailed recipe page for that beer
2. **Given** a detailed recipe page is displayed, **When** the page loads, **Then** all recipe data is visible including malts, hops, yeast, brewing instructions, OG, FG, and ABV
3. **Given** a user is on a detailed beer page, **When** they click the back button, **Then** they return to the production stage page they came from

---

### User Story 4 - Empty State Messaging (Priority: P2)

When a production stage has no beers (e.g., nothing currently on tap or in production), users should see a friendly message explaining the situation rather than a blank page.

**Why this priority**: Improves user experience by providing context when lists are empty, preventing confusion about whether the page loaded correctly or if there's truly nothing to display.

**Independent Test**: Can be tested by checking pages that have no associated beers and verifying appropriate empty state messages appear.

**Acceptance Scenarios**:

1. **Given** the "On Tap" page has no beers, **When** the page loads, **Then** a message displays such as "The taps are empty. :( Check out what's in production."
2. **Given** the "In Production" page has no beers, **When** the page loads, **Then** a message indicates no beers are currently in production and suggests checking other pages

---

### Edge Cases

- What happens when a beer has incomplete recipe data (missing hops, yeast, or instructions)?
- How should beers be ordered if brew dates are missing or identical?
- What happens if a filter button label is very long or contains special characters?
- How does the system handle beers that could fit multiple groups or styles?

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST organize beers into four distinct production stages: "On Tap", "In Production", "Recipe Design", and "Recipe Archive" based on beer status
- **FR-002**: System MUST display beers on production stage pages as cards showing name, style, description, ABV, IBU, and SRM
- **FR-003**: System MUST sort beers in all production stages by brew date in reverse chronological order (newest first)
- **FR-004**: System MUST provide clickable beer cards that link to detailed recipe pages
- **FR-005**: System MUST display a default placeholder image if a beer's logo is missing
- **FR-006**: System MUST filter the Recipe Archive page by beer group/style when filter buttons are clicked
- **FR-007**: System MUST only display filter buttons on Recipe Archive if there are at least 2 different beer groups represented
- **FR-008**: System MUST display an empty state message when a production stage has no beers
- **FR-009**: System MUST show complete recipe details on beer detail pages including all ingredients and brewing instructions
- **FR-010**: System MUST provide a back navigation button on beer detail pages to return to the previous production stage page
- **FR-011**: System MUST ensure beer detail pages inherit the consistent base layout (header, footer, navigation)
- **FR-012**: System MUST display beer information that matches the current data structure (brew_date, ABV, IBU, SRM, etc.)

### Key Entities

- **Beer**: Represents a single recipe with properties including title, status, style, group, logo, ABV, IBU, SRM, brew_date, ingredients, and brewing instructions
- **Production Stage**: A category grouping beers by their current status (on_tap, in_production, in_design, past_beer)
- **Beer Group/Style**: A classification system for organizing beers (IPA, Lager, Stout, etc.) used for filtering

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: All beers are correctly categorized by production stage with 100% accuracy
- **SC-002**: Beer cards display all required information (name, style, ABV, IBU, SRM) with consistent formatting
- **SC-003**: Recipe Archive filtering reduces the displayed list by the correct number of beers when filters are applied (verified by comparing filtered count to expected count)
- **SC-004**: Beer detail pages load in under 1 second and display complete recipe information without errors
- **SC-005**: Empty state pages display appropriate messaging and are visually distinct from pages with beer listings
- **SC-006**: Filter functionality works on all device sizes (mobile, tablet, desktop) without layout breakage
- **SC-007**: All beer links maintain referential integrity - clicking a beer always shows the correct recipe
- **SC-008**: Back navigation successfully returns users to the previous page with scroll position maintained when possible

## Assumptions

- Each beer has a unique identifier (beer_key or similar) for reliable linking
- Beer status values are consistently managed in the beer data files
- The beer data structure remains stable with malts, hops, yeast, and brewing instructions organized as arrays or lists
- Beers in the Recipe Archive will grow over time, making filtering increasingly valuable
- Users primarily access these pages on desktop and mobile browsers, with Jekyll-generated static HTML
- Empty state scenarios are intentional design states, not error conditions

