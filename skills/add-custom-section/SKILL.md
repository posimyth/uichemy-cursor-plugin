---
name: add-custom-section
description: Add or rewrite one custom section on a UiChemy page from code you write, in UiChemy, React or plain HTML/CSS/JS, for example a pricing table, a gallery, an animated hero or an embed. Use when the user asks for a custom section, a section the library does not have, a code block on a page, or to change the code of a section.
---

Use this skill when the library layouts do not cover what the user wants, and a section needs to be written as code.

Steps:
1. Identify the project and page. Use `uichemy_get_project` if needed. Say that a new section will be added to that page.
2. Call `uichemy_section_spec` once and follow it exactly if you will use the `uichemy` format. Do not guess its limits.
3. Pick the `format` for `uichemy_add_code_section`:
   - `uichemy`: JSX written to the spec. Best choice, because every design control drives it and it exports as native builder widgets.
   - `react`: any React component, converted onto the design system.
   - `html`: one root element with its own CSS and JS, kept as written. Images must be absolute https URLs.
4. Call `uichemy_add_code_section` with `projectId`, `pageName`, `code`, `format`, `kind` and `name`, and `index` if the position matters. It only appends one section and never replaces an existing one. If the call is refused, read the reasons it returns, fix the code and try again.
5. To change a section that already exists, call `uichemy_get_section_code` first so the copy the user edited on the canvas is not lost, then `uichemy_update_code_section`. That call OVERWRITES the section, so tell the user and wait for a clear yes before rewriting a section they have edited.
6. Run `uichemy_check_responsive` and `uichemy_validate`, then `uichemy_open_preview`.

Rules:
- Write copy from the user's brief only. Do not invent statistics, testimonials, prices or awards.
- Do not load scripts or styles from a source the user did not ask for. Use an external script or stylesheet URL only when the section needs it (for example a font or animation library) and name it to the user.
- Do not put keys, tokens or personal data into section code.
