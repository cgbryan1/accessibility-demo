# Accessibility demo: bad vs. good

This repo contains a deliberately bad and a deliberately good version of the same sign-up page. The goal is to show how nearly identical visual design can still create very different keyboard and assistive-technology experiences.

## Files

- `bad.html` — intentionally inaccessible version
- `good.html` — accessible version with the same layout and styling

## Local deployment strategies

Use any of the following from the repo root:

1. Python static server
   ```bash
   cd /Users/carolinebryan/code/accessibility-demo
   python3 -m http.server 8000
   ```
   Open:
   - `http://localhost:8000/bad.html`
   - `http://localhost:8000/good.html`

2. Node static server
   ```bash
   cd /Users/carolinebryan/code/accessibility-demo
   npx serve . -l 8000
   ```

3. Lightweight HTTP server via npm
   ```bash
   cd /Users/carolinebryan/code/accessibility-demo
   npx http-server . -p 8000
   ```

4. VS Code / browser preview
   - Open the HTML files directly in a browser, or
   - Use the Live Server extension in VS Code to serve the folder.

## Suggested walkthrough (5 minutes)

### 1) Keyboard only (about 1.5 minutes)

Open the bad version first:

- Tab through the page.
- Notice that the visual focus indicator is missing.
- The navigation items are `div` elements instead of links or buttons, so they are skipped in the tab order.
- The modal trigger appears clickable but is not reliable with keyboard navigation.
- Once the modal opens, focus may trap or be lost, and the close control is not clearly exposed to assistive tech.

Then open the good version:

- Tab through the same flow.
- Focus is visible, and the tab order is logical.
- Links and buttons are real interactive elements.
- The modal opens with a clear accessible dialog pattern and focus moves into the dialog.
- Press `Tab` and `Shift+Tab` to confirm the focus stays inside the dialog until it closes.

### 2) Browser accessibility tree (about 1.5 minutes)

Open Chrome DevTools and inspect the page with the Accessibility panel:

- Compare the names, roles, and states for the nav controls, form fields, and dialog.
- In the bad version, some controls are unlabeled, announced as generic elements, or missing state information.
- In the good version, the form fields have labels, the buttons have accessible names, and the dialog exposes a proper role and state.

Look for examples such as:

- link/button semantics
- field labels
- input state (`disabled`, `checked`, etc.)
- dialog name and modal state (`aria-modal="true"`)

### 3) Lighthouse and axe (about 1 minute)

Run Lighthouse and axe on both pages.

Typical result:

- bad version: roughly 40-60
- good version: roughly 90-100

The score gap is dramatic, but automated tools are not the whole story. They do not always catch:

- whether the tab order is intuitive
- whether focus styles are visible to the sighted keyboard user
- whether a focus trap is confusing in practice
- whether a component is actually understandable to a screen-reader user in context

This is why accessibility must be checked with keyboard testing, accessibility-tree inspection, and real user flows—not only with tools.

## WCAG 2.1 themes highlighted

This demo focuses on the kinds of failures that often map to WCAG 2.1 success criteria, including:

- 2.1.1 Keyboard
- 2.4.7 Focus Visible
- 4.1.2 Name, Role, Value
- 2.4.3 Focus Order
- 2.4.11 Focus Not Obscured

## Teaching tip

Keep the visual design almost identical in both versions so the audience can see that the accessibility differences are not obvious to a sighted mouse user—but they are highly visible to keyboard and assistive-tech users.
