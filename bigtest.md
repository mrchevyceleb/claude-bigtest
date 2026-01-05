---
name: bigtest
description: Comprehensive application testing with Playwright MCP
version: 2.5
author: Matt Johnston
tags: [testing, qa, playwright, automation]
---

# /bigtest - Comprehensive Application Testing

**Version:** 2.5 (Phase 1 + Phase 2 features)

Automated comprehensive testing using Playwright MCP that tests UI, functionality, performance, accessibility, and catches visual regressions.

---

## Usage

```bash
/bigtest
/bigtest https://myapp.com
/bigtest --config path/to/bigtest-config.json
```

---

## What Gets Tested

### Phase 1: Core Testing (v2.0)
- ✅ UI/UX (20 points) - Layout, responsiveness, visual consistency
- ✅ Functionality (30 points) - Forms, buttons, features, data flow
- ✅ Console Errors (20 points) - JS errors with smart classification
- ✅ Network Errors (15 points) - API calls, 404s, 500s
- ✅ User Flows (15 points) - Complete user journeys

### Phase 2: Advanced Testing (v2.5 - NEW)
- ✅ Visual Regression - Screenshot comparison against baseline
- ✅ Accessibility - WCAG 2.1 AA compliance checks
- ✅ Performance - Load times, network requests, bundle size
- ✅ Data States - Empty, populated, and heavy data scenarios
- ✅ Smart Error Detection - Classify errors by severity

---

## Workflow

```
0. Load App-Specific Config (if exists)
1. Assessment - Map entire app structure
2. Setup - Navigate, check auth
3. Auth Testing - Login/logout flows
4. Desktop Testing - 1280x720 viewport
5. Mobile Testing - 375x667 viewport
6. Visual Regression - Compare screenshots
7. Accessibility Audit - A11y checks
8. Performance Audit - Speed + resource checks
9. Console/Network Audit - Error classification
10. Score Calculation - 0-100 with breakdown
11. Report Generation - Comprehensive findings
12. Fix Plan - Prioritized issue list
```

---

## App-Specific Configuration

Create `bigtest-config.json` in your project root for custom testing:

```json
{
  "appName": "My App",
  "appType": "dashboard",
  "url": "http://localhost:3000",

  "criticalFlows": [
    {
      "name": "User Login → Dashboard",
      "steps": [
        { "action": "navigate", "url": "/login" },
        { "action": "fill", "selector": "#email", "value": "test@example.com" },
        { "action": "fill", "selector": "#password", "value": "password123" },
        { "action": "click", "selector": "button[type=submit]" },
        { "action": "wait", "condition": "url", "value": "/dashboard" }
      ],
      "expectedOutcome": "Dashboard loads with user data"
    }
  ],

  "dataStates": {
    "empty": {
      "description": "New user with no data",
      "setup": "Clear database or use empty test account"
    },
    "populated": {
      "description": "Normal user with 10-20 items",
      "setup": "Seed database with sample data"
    },
    "heavy": {
      "description": "Power user with 1000+ items",
      "setup": "Load test with large dataset"
    }
  },

  "expectedBehaviors": {
    "forms": {
      "onSubmit": "clear",
      "validation": "inline",
      "errorDisplay": "below-field"
    },
    "modals": {
      "closeOn": ["escape", "clickOutside", "closeButton"],
      "backdrop": "blur"
    },
    "tables": {
      "sortable": true,
      "filterable": true,
      "pagination": true
    }
  },

  "performance": {
    "maxPageLoadTime": 3000,
    "maxNetworkRequests": 15,
    "maxBundleSize": 500,
    "maxTTI": 5000
  },

  "accessibility": {
    "level": "AA",
    "excludeRules": [],
    "reportOnly": false
  },

  "visualRegression": {
    "enabled": true,
    "baselineDir": "tests/baselines",
    "threshold": 0.1,
    "ignoreRegions": [
      { "selector": ".date-display", "reason": "Dynamic timestamps" },
      { "selector": ".live-chart", "reason": "Real-time data" }
    ]
  },

  "errorClassification": {
    "ignore": [
      "ResizeObserver loop limit exceeded",
      "Third-party script warning"
    ],
    "critical": [
      "TypeError",
      "ReferenceError",
      "Cannot read property"
    ]
  }
}
```

---

## Scoring Rubric (Updated for Phase 2)

| Category | Max Points | Criteria |
|----------|------------|----------|
| **Functionality** | 25 | Features work as specified |
| **UI Correctness** | 15 | Visual elements render correctly |
| **Console Errors** | 15 | No JS errors (classified by severity) |
| **Network Errors** | 10 | No failed API calls |
| **User Flows** | 10 | Critical journeys work |
| **Accessibility** | 10 | WCAG AA compliance |
| **Performance** | 10 | Meets speed budgets |
| **Visual Regression** | 5 | Matches baseline screenshots |
| **TOTAL** | **100** | |

### Error Classification (Smart Detection)

**CRITICAL (-5 points each)** - Must fix:
- TypeError, ReferenceError, RangeError
- "Cannot read property of undefined"
- Network 500 errors
- Authentication failures
- Data loss scenarios

**MAJOR (-3 points each)** - Should fix:
- Warning errors from core code
- Network 404 errors
- Slow page loads (>3s)
- Missing accessibility labels
- WCAG AA violations

**MINOR (-1 point each)** - Nice to fix:
- Third-party warnings
- Deprecation notices
- Console.log statements
- Minor visual inconsistencies

**IGNORED (0 points)** - Configured via config:
- Known third-party issues
- ResizeObserver limit exceeded
- Framework dev mode warnings

---

## Accessibility Checks (Phase 2)

Tests against WCAG 2.1 Level AA:

**Automated Checks:**
- [ ] All images have alt text
- [ ] Form inputs have labels
- [ ] Color contrast meets 4.5:1 ratio
- [ ] Heading hierarchy is logical
- [ ] ARIA roles used correctly
- [ ] Focus indicators visible
- [ ] Keyboard navigation works
- [ ] No keyboard traps
- [ ] Skip links present
- [ ] Link text is descriptive

**Scoring:**
- 10 points: 100% pass rate
- 8 points: 1-2 violations
- 6 points: 3-5 violations
- 3 points: 6-10 violations
- 0 points: 10+ violations

---

## Visual Regression Testing (Phase 2)

**How it works:**
1. First run: Capture baseline screenshots of all pages
2. Future runs: Compare current vs baseline
3. Flag differences above threshold (default 0.1%)
4. Generate visual diff overlays

**Baseline Management:**
```bash
/bigtest --update-baseline  # Update baseline screenshots
/bigtest --ignore-visual    # Skip visual regression checks
/bigtest --threshold 0.5    # Custom diff threshold (0.5%)
```

**Stored in:** `tests/bigtest/baselines/`

**Diff reports:** `tests/bigtest/diffs/`

---

## Performance Budgets (Phase 2)

**Default Budgets:**
- Max page load: 3000ms
- Max Time to Interactive (TTI): 5000ms
- Max network requests: 15 per page
- Max JavaScript bundle: 500kb
- Max total page size: 2MB

**Measured Metrics:**
- First Contentful Paint (FCP)
- Largest Contentful Paint (LCP)
- Time to Interactive (TTI)
- Total Blocking Time (TBT)
- Cumulative Layout Shift (CLS)

**Scoring:**
- All budgets met: 10 points
- 1 budget exceeded: 7 points
- 2-3 budgets exceeded: 4 points
- 4+ budgets exceeded: 0 points

---

## Data State Testing (Phase 2)

Tests app in different data scenarios:

**Empty State:**
- New user, no data
- Verify empty state UI shows
- Verify CTA works ("Add your first item")

**Normal State:**
- 10-20 items of data
- Verify list/table rendering
- Verify pagination if applicable

**Heavy State:**
- 1000+ items
- Verify performance doesn't degrade
- Verify virtualization/lazy loading
- Check for memory leaks

---

## Test Execution

### Phase 1: Core Testing

**Assessment Phase:**
```typescript
// Map entire app
const pages = await mapApplication(url);
const forms = await findAllForms(pages);
const buttons = await findAllButtons(pages);
const flows = await identifyCriticalFlows(pages);
```

**Testing Phase:**
```typescript
// Test at both viewports
for (const viewport of [DESKTOP, MOBILE]) {
  await browser.setViewport(viewport);

  // Test each page
  for (const page of pages) {
    await testPage(page);
    await captureScreenshot(page, viewport);
    await checkConsoleErrors();
    await checkNetworkErrors();
  }

  // Test each form
  for (const form of forms) {
    await testFormSubmit(form);
    await testFormValidation(form);
  }

  // Test each flow
  for (const flow of flows) {
    await executeFlow(flow);
    await verifyOutcome(flow);
  }
}
```

### Phase 2: Advanced Testing

**Accessibility Audit:**
```typescript
await browser.evaluate(async () => {
  const { default: axe } = await import('axe-core');
  const results = await axe.run();
  return results.violations;
});
```

**Performance Audit:**
```typescript
const metrics = await browser.evaluate(() => {
  return {
    fcp: performance.getEntriesByName('first-contentful-paint')[0],
    lcp: performance.getEntriesByType('largest-contentful-paint')[0],
    tti: performance.getEntriesByType('tti')[0],
    cls: performance.getEntriesByType('layout-shift')
  };
});
```

**Visual Regression:**
```typescript
const baseline = await loadBaseline(page.name, viewport);
const current = await browser.screenshot();
const diff = await compareImages(baseline, current);

if (diff.percentage > threshold) {
  await saveDiffImage(diff);
  issues.push({
    type: 'visual-regression',
    page: page.name,
    diff: diff.percentage
  });
}
```

---

## Report Output

### Comprehensive Report Structure

```markdown
# BigTest Report - [App Name]
**Date:** [Timestamp]
**URL:** [App URL]
**Score:** [X]/100
**Status:** [EXCELLENT/GOOD/FAIR/POOR/CRITICAL]

---

## Summary

- **Pages Tested:** X
- **Forms Tested:** X
- **Buttons Tested:** X
- **Flows Tested:** X
- **Viewports:** Desktop + Mobile

---

## Score Breakdown

| Category | Score | Max | Status |
|----------|-------|-----|--------|
| Functionality | X | 25 | ✅/⚠️/❌ |
| UI Correctness | X | 15 | ✅/⚠️/❌ |
| Console Errors | X | 15 | ✅/⚠️/❌ |
| Network Errors | X | 10 | ✅/⚠️/❌ |
| User Flows | X | 10 | ✅/⚠️/❌ |
| Accessibility | X | 10 | ✅/⚠️/❌ |
| Performance | X | 10 | ✅/⚠️/❌ |
| Visual Regression | X | 5 | ✅/⚠️/❌ |

---

## CRITICAL Issues (Must Fix)

1. **[Issue Title]**
   - Severity: CRITICAL
   - Category: [Category]
   - Page: [Page Name]
   - Description: [Details]
   - How to reproduce:
     1. [Step 1]
     2. [Step 2]
   - Expected: [What should happen]
   - Actual: [What happens]
   - Screenshot: [Link]

---

## MAJOR Issues (Should Fix)

[Same format]

---

## MINOR Issues (Polish)

[Same format]

---

## Accessibility Report

**WCAG AA Compliance:** [X]% pass rate

| Violation | Count | Impact | Pages |
|-----------|-------|--------|-------|
| Missing alt text | X | Critical | [pages] |
| Low contrast | X | Serious | [pages] |
| [etc] | X | [impact] | [pages] |

---

## Performance Report

| Metric | Value | Budget | Status |
|--------|-------|--------|--------|
| Page Load | Xms | 3000ms | ✅/❌ |
| TTI | Xms | 5000ms | ✅/❌ |
| Bundle Size | Xkb | 500kb | ✅/❌ |
| Network Requests | X | 15 | ✅/❌ |

---

## Visual Regression Report

| Page | Viewport | Diff % | Status |
|------|----------|--------|--------|
| Home | Desktop | 0.5% | ✅ |
| Login | Mobile | 5.2% | ❌ |

[Visual diff images saved to: tests/bigtest/diffs/]

---

## Console Error Log

**Total Errors:** X (Critical: X, Major: X, Minor: X)

### Critical Errors (X)
```
[Page] [Timestamp] TypeError: Cannot read property 'map' of undefined
  at Component.tsx:42
```

### Major Errors (X)
[Same format]

### Minor Errors (X)
[Same format]

---

## Network Error Log

**Total Failures:** X

| Request | Type | Status | Page |
|---------|------|--------|------|
| /api/users | GET | 404 | Dashboard |
| /api/quotes | POST | 500 | Quotes |

---

## User Flow Results

**Total Flows:** X | **Passed:** X | **Failed:** X

| Flow | Status | Issues |
|------|--------|--------|
| Login → Dashboard | ✅ PASS | None |
| Create Quote | ❌ FAIL | Form validation error |

---

## Recommendations

**Priority 1 (This Week):**
1. Fix [Critical Issue]
2. Fix [Critical Issue]

**Priority 2 (This Sprint):**
1. Fix [Major Issue]
2. Improve [Performance Issue]

**Priority 3 (Nice to Have):**
1. Polish [Minor Issue]
2. Add [Feature Enhancement]

---

## Next Steps

1. Review critical issues
2. Fix blocking bugs
3. Re-run /bigtest
4. Target score: 95+
```

---

## Score Interpretation

| Score | Status | Meaning |
|-------|--------|---------|
| **95-100** | EXCELLENT | Production ready, minor polish at most |
| **85-94** | GOOD | Solid, a few issues to address |
| **70-84** | FAIR | Usable but needs work |
| **50-69** | POOR | Significant issues, not ready |
| **<50** | CRITICAL | Major problems, needs rework |

---

## Playwright MCP Tools Used

### Core Navigation
- `mcp__playwright__browser_navigate`
- `mcp__playwright__browser_navigate_back`
- `mcp__playwright__browser_resize`

### Interaction
- `mcp__playwright__browser_click`
- `mcp__playwright__browser_type`
- `mcp__playwright__browser_press_key`
- `mcp__playwright__browser_fill_form`

### Inspection
- `mcp__playwright__browser_snapshot`
- `mcp__playwright__browser_take_screenshot`
- `mcp__playwright__browser_console_messages`
- `mcp__playwright__browser_network_requests`

### Execution
- `mcp__playwright__browser_evaluate`
- `mcp__playwright__browser_run_code`
- `mcp__playwright__browser_wait_for`

---

## Prerequisites

1. **Playwright MCP enabled** - Run `/mcp` to verify
2. **App running** - Dev server must be accessible
3. **Config file** (optional) - `bigtest-config.json` for custom tests

---

## Configuration Examples

### Dashboard App
```json
{
  "appType": "dashboard",
  "criticalFlows": [
    "Login → Dashboard → View Data",
    "Create Item → Save → Verify in List",
    "Edit Item → Update → Verify Changes"
  ],
  "performance": {
    "maxPageLoadTime": 2000,
    "maxTTI": 4000
  }
}
```

### E-commerce App
```json
{
  "appType": "ecommerce",
  "criticalFlows": [
    "Browse Products → Add to Cart → Checkout",
    "Search → Filter → View Product → Add to Cart",
    "Login → View Orders → Track Order"
  ],
  "dataStates": {
    "empty": "New user, empty cart",
    "populated": "Cart with 3-5 items",
    "heavy": "100+ products in category"
  }
}
```

---

## Tips for Best Results

1. **Create app config** - Defines expected behaviors and critical flows
2. **Update baselines** - After intentional UI changes
3. **Run regularly** - Catch regressions early
4. **Fix critical first** - Focus on must-fix issues
5. **Track scores** - Monitor quality over time

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Playwright not found | Run `/mcp` and enable playwright |
| High false positives | Tune error classification in config |
| Visual diffs failing | Update baseline or increase threshold |
| Slow tests | Reduce data state sizes, limit flows |
| A11y false positives | Add excluded rules to config |

---

## Related Commands

| Command | Description |
|---------|-------------|
| `/perfect` | Single task test-fix loop |
| `/test` | Run project test suite |
| `/commit` | Git commit changes |

---

## Changelog

### v2.5 (January 5, 2026) - Phase 2
- ✅ Added visual regression testing
- ✅ Added accessibility checks (WCAG AA)
- ✅ Added performance budgets
- ✅ Added data state testing
- ✅ Added smart error classification
- ✅ Added app-specific config support
- ✅ Improved scoring rubric (8 categories)

### v2.0 (January 5, 2026) - Phase 1
- ✅ Comprehensive functionality testing
- ✅ Scoring system (0-100)
- ✅ Severity classification
- ✅ Desktop + mobile viewports
- ✅ Console + network error tracking
- ✅ User flow testing

### v1.0 (January 4, 2026)
- Initial release (UI/UX only)

---

**Created:** January 4, 2026
**Updated:** January 5, 2026 (v2.5 - Phase 2 complete)
**Author:** Matt Johnston
**GitHub:** https://github.com/mrchevyceleb/claude-bigtest
