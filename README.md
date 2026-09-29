# bc-pd-cdn

Storefront files of **Product Part Diagram by PapaThemes** (BigCommerce app), served by jsDelivr.

## URLs

Every release is a git tag `v<version>` (the version in the app's `client/scripts/manifest.json`), and stores
load the widget from that tag only:

```
https://cdn.jsdelivr.net/gh/tvlgiao/bc-pd-cdn@v<version>/productpartdiagram.js
https://cdn.jsdelivr.net/gh/tvlgiao/bc-pd-cdn@v<version>/productpartdiagram.css
https://cdn.jsdelivr.net/gh/tvlgiao/bc-pd-cdn@v<version>/viewer3d/…      (3D viewer, workers, Basis transcoder)
```

- A tagged URL never changes content, so browsers and jsDelivr may cache it for as long as they like. The
  widget loads the 3D files of its own tag, with SRI.
- `@latest` and branch URLs are **not** used by any store.
- A store moves to a new version when the merchant opens the app (the app compares the store's Script
  Manager entry with the version its server release pins and reinstalls it), or when the app reinstalls its
  script. Rolling a store back means pinning the previous tag in the server release.

## Rules

- Written only by the app's `s3-deploy-client` workflow: it commits the new build (widget at the repository
  root, 3D files under `viewer3d/`) and creates the tag.
- A tag is never moved or deleted. Publishing a version whose tag already exists fails unless the files are
  identical; ship changes under a new version.
