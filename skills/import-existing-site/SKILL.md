---
name: import-existing-site
description: Import a website the user already has, such as HTML, CSS and JS, a zip, or a site built with Lovable, Bolt or v0, into a new UiChemy project and prepare it for WordPress, Elementor or Gutenberg. Use when the user wants to bring an existing static site or AI-generated site into UiChemy.
---

Use this skill when the user supplies site code or a zip and wants it in UiChemy.

Steps:
1. Call `uichemy_import_spec` once. Follow what it says the importer accepts and how to verify an import. Do not guess the format.
2. Choose the path:
   - Files the user pasted or you wrote in this chat: `uichemy_import_files`.
   - A zip at an https URL the user gave: `uichemy_import_zip` with `zipUrl`.
   - A zip the user attached: `uichemy_import_zip` with `zipData` only if the file is small enough to pass directly; otherwise ask for a URL.
3. Tell the user a new project is being created in their UiChemy account, then run the import.
4. Verify with `uichemy_get_project` and `uichemy_validate`. If the import spec lists a known failure signature that matches, apply its fix. Otherwise report the problem and what you tried.
5. Run `uichemy_check_responsive` on each page and report overflow or unreadable text.
6. When the user wants builder-ready output, call `uichemy_sync_builders` for the project and report the result.

Rules:
- Import only code the user owns or has the right to use. If the user asks you to copy a third-party site they do not control, decline.
- Do not fetch or scrape sites yourself. Work only from what the user supplied.
- Never include credentials, API keys or personal data from the source files in your replies.
