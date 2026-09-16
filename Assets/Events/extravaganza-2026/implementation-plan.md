# Fellowship event-gallery implementation plan

This is an integration specification, not a replacement Fellowship page. Only events.html was attached to the referenced conversation; no Fellowship HTML was available. Its existing markup, navigation and styles have not been inferred.

## Asset location and data

Place this event directory under `assets/events/extravaganza-2026/`. Keep `full/`, `thumbs/`, `featured/` and `gallery.json` together. Review documents and checksums are handoff records and do not need to be deployed. Keep the original JPG archive separately, outside public website assets.

Use `gallery.json` as the source of truth for order, alt text and intrinsic image dimensions. Asset paths are relative to this event directory. Reuse the same gallery component for future events by providing another manifest, title and unique section ID.

## Page composition

1. Add a section with the unique anchor `extravaganza-2026`, headed “Extravaganza 2026”. Suggested introduction: “Food, fellowship and memories from the Arrid Club Extravaganza.”
2. Show photo 04 as the featured image at its natural 4:3 ratio, up to 960 CSS pixels wide. Use the 960- and 1440-pixel featured files and the 2048-pixel full file as responsive srcset candidates. Sizes should reflect the actual Fellowship content width. Keep title and text outside the photograph.
3. Follow with the remaining 17 photos in manifest order. The feature belongs to the same 18-image browsing sequence; do not repeat its thumbnail.
4. Use a responsive grid: one column on very narrow screens, two from roughly 360px, three from 700px, four from 1000px, bounded by the actual page container. Use 12–16px gaps. Display thumbnail images within consistent 4:3 cells using object-fit: contain and a neutral background. This preserves the full portrait image without cutting off faces.
5. Each image is a genuine link to its full WebP, progressively enhanced to open the lightbox. This preserves basic viewing when JavaScript fails. Give each image its supplied alt text and provide an accessible link name such as “Open photo 2 of 18: [description]”.

## Loading and image quality

Thumbnails have a maximum 480px long edge, quality 78. Full images retain the original 2048px long edge at quality 76. Cover derivatives are 960px and 1440px at quality 84. Do not stretch full images beyond their native resolution for default viewing. Preserve portrait orientation and use object-fit: contain in the viewer.

Set image width and height attributes from the manifest to reserve layout space; use decoding="async". Lazy-load thumbnails. If the feature is above the fold, load it eagerly with high fetch priority; if the section is lower on the existing Fellowship page, lazy-load it too. Full images should not be fetched until opened. Optionally preload only the next image after the active image loads, avoiding speculative loading on constrained connections. No slideshow or autoplay.

## Lightbox behavior and accessibility

Use a native modal dialog filling the viewport, with a dark background, a contained image, visible Previous/Next/Close buttons, caption, and “Photo N of 18” counter. This is a full-viewport overlay; browser Fullscreen API is unnecessary.

Opening stores the triggering link and moves focus to Close. Modal behavior must keep keyboard focus in the dialog and make the page behind it inactive. Escape closes; Left/Right browse; visible buttons provide equivalent touch and keyboard operation. Wrap last-to-first and first-to-last consistently. Restore focus to the initiating link on close and restore the prior page scroll position. Lock background scrolling only while open.

Use at least 44px touch controls with clear focus indicators. Allow ordinary pinch zoom: do not disable browser scaling or apply touch-action: none. Optional horizontal swipe navigation must ignore multi-touch gestures and vertical scrolling; buttons remain available without gestures. Respect reduced-motion preferences and avoid animation by default.

Keep the current descriptive alt text on the displayed image. Announce the counter and caption through a polite live region when navigation changes, without moving keyboard focus. Provide a loading state, readable error message, Retry control and direct full-image link if an image fails to load. Guard against stale loads when navigation is rapid.

## Integration and acceptance checks

Once the actual Fellowship HTML is supplied, match its type, colors, container width and spacing; scope component styles so other page galleries are unaffected. Resolve its real URL before changing the Events card to “View Photos” linking to that page's #extravaganza-2026 anchor. No existing page was edited for this handoff.

Before publication, verify the following in the integrated page:

- All 18 image links resolve; manifest order and cover match the review.
- No horizontal overflow at 320px, 390px, tablet and desktop widths, or at 200% text zoom.
- Portrait photos remain complete; cover faces are not cropped.
- Keyboard opening, focus containment, Escape, arrow navigation and focus restoration work.
- Screen-reader labels, counter announcements and image alt text are meaningful.
- iOS Safari and Android Chrome can open, browse, close, rotate the device and pinch zoom.
- Only the responsive cover and nearby thumbnails load initially; full images load on demand.
- Direct links work without JavaScript; failed image requests produce usable recovery controls.

This specification has not been implemented or browser-tested against Fellowship HTML. Asset decoding, output dimensions and original byte checksums were verified independently. The video is outside this deliverable.

