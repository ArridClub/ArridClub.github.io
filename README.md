# Arrid Club Website

Website: https://arridclub.com

## File organization

- Root HTML files: website pages and Google verification.
- `css/style.css`: shared website styles.
- `Assets/images/site/`: backgrounds and cinematic site photos.
- `Assets/images/meeting-spaces/`: meeting-room photos.
- `Assets/images/fellowship/sobriety-chips/`: sobriety-chip photos.
- `Assets/flyers/`: event flyers.
- `Assets/Events/extravaganza-2026/`: existing event gallery and supporting records.

Keep `CNAME`, `sitemap.xml`, and all HTML pages in the root.

## Making updates

1. Create a new branch from the latest `main`.
2. Place new images in the appropriate folder, preferably in WebP format.
3. Match filename and folder capitalization exactly.
4. When moving a file, update every reference in the same branch. Check image sources, links, responsive images, CSS backgrounds, social-sharing metadata, and structured data.
5. Review the pull request before merging into `main`.
6. After deployment finishes, check affected pages on wide and narrow screens, including enlarged images and galleries.
7. Delete the finished branch after confirming the site works.

Keep original source images backed up separately. Avoid uploading unrelated files during a small cleanup batch.
