# Sweetie's Wish — Version 0.7

Final mobile + sharing polish pass after V0.6.

- Keeps the seven games, effects, sounds, bloom atmosphere, and existing multilingual content architecture intact.
- Adds the real build version (`0.7`) everywhere the website exposes its version, including Settings and the home/footer version note.
- Fixes mobile viewport/safe-area handling for the create-wish sheet so fields, headings, buttons, and share panels stay inside the phone viewport and remain scrollable.
- Keeps the keyboard behaviour and saved-form draft system intact.
- Makes the Hinglish recipient-facing wording respectful (`aap/aapke/aapka`) without changing the other language systems.
- Hardens shareable links by URL-encoding the wish payload and keeps the full `WB2-...` offline token format compatible with the existing opener.
- Adds a clipboard fallback so Copy Token / Copy Link still works when `navigator.clipboard` is unavailable.
- Keeps native Share behaviour and the existing static/no-database architecture.

This build is intended as the final polish before packaging/deployment.
