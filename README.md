# Go!Go!BOOO! browser preview

This repository hosts only a packaged Godot browser export and the small deployment workflow needed to serve it. It does not contain the private development repository or its history.

Play: https://lys20001205.github.io/gogobooo-play/godot/

Source build revision: `a7563b65fe8d85f2fe401e163ba47caacc107425`  
Godot: `4.7.2.stable.official.ed1daf0bf`  
Renderer: WebGL 2, single-threaded

The complete `godot/` export, including its loader and metadata, is copied byte-for-byte from the successful source CI artifact. Only the independent root redirect and repository transport packaging are added.

## Publishing

GitHub Pages uses the GitHub Actions publishing source. The workflow verifies `UPLOADS.sha256`, reconstructs the static site from the three export archives, verifies `SITE.sha256`, and deploys that site. It does not fetch a private repository or need a cross-repository token.

- `godot-engine.wasm.gz`: exported engine runtime
- `game-data.pck.gz`: exported game resources and compiled scripts
- `web-shell.zip`: browser loader, root redirect, build metadata, and third-party license notices

Compression is only for repository upload. The deployed game requests ordinary `godot/index.wasm` and `godot/index.pck` files. Relative paths support the `/gogobooo-play/` GitHub Pages base path.

## Notes

The preview needs a browser with WebGL 2. It has no offline service worker or installable PWA manifest. Browser saves are stored locally in the exported game's own storage namespace; saves from a different website origin are not transferred automatically.

A public playable export is downloadable and its runtime resources can be inspected or extracted. Keeping the development repository private does not make the exported assets or compiled scripts secret.

Third-party notices are included in `godot/GODOT_LICENSE.txt`, `godot/GODOT_COPYRIGHT.txt`, and `godot/FONT_OFL.txt` after unpacking. Those notices apply to their respective components.
