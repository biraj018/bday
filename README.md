Birthday Surprises — responsive & accessibility updates

What I changed

- Responsive behavior: On small screens (max-width:520px) flip-cards convert to a stacked list. Tapping a card expands its back content in-flow (`.flip-card.expanded`) instead of performing a 3D rotate. Desktop retains the 3D flip.
- Performance: Heavy decorative visuals hidden on small screens; confetti is throttled or replaced with a lightweight burst when `prefers-reduced-motion`, `Save-Data` is enabled, or device memory is low. Particle count is reduced on narrow viewports.
- Accessibility: `role="button"`, `tabindex="0"`, and `aria-expanded` added to `.flip-card`. Keyboard activation via Enter/Space toggles cards. Escape collapses expanded/flipped cards and dismisses the modal/letter page.
- JS: `flipCard(i)` and `unflip(e,i)` updated to support the mobile stacked behavior and maintain progress counting. Confetti logic updated to respect user preferences and device capabilities.

Testing steps (quick)

1. Open `birthday_surprises.html` in a browser.
2. Desktop (wide): click cards — they should perform 3D flips, unlock progress, and when all revealed trigger confetti and the modal.
3. Mobile (or narrow your browser to <=520px): cards should stack; tapping a card expands its back content inline (no 3D flip). Progress updates should still count first-time reveals.
4. Keyboard: Tab to a card and press Enter or Space to toggle it. Press Escape to collapse or dismiss the modal.
5. Reduced-motion / low-power checks:
   - In Chrome devtools emulate `prefers-reduced-motion: reduce` (Rendering > Emulate CSS media features) — confetti should switch to a lightweight burst or be skipped.
   - In Network throttling, enabling `Save-Data` (if available) should also reduce confetti.

Notes / Next steps

- I implemented conservative defaults to maintain visual delight while avoiding jank on low-power devices. If you want confetti fully disabled on phones, I can make that stricter.
- If you want automated visual tests (e.g., Puppeteer screenshots at breakpoints), I can add a small test script.

— Changes applied directly to `birthday_surprises.html` on 