# Repository Guidelines

## Project Structure & Content Flow
- Published posts live in `entries/<blog-domain>/entry/YYYYMMDD/<entryid>.md`; drafts belong in the mirrored `draft_entries` tree until merged.
- Each markdown file starts with YAML front matter (`Title`, `Category`, `Date`, `URL` or `Draft`, `EditURL`/`PreviewURL`, optional `CustomPath`). Keep lists indented with two spaces.
- Templates: `.github/PULL_REQUEST_TEMPLATE/draft.md` injects edit/preview URLs; `draft.template` can seed new drafts if you prefer copying locally.
- Automation: `.github/workflows` handles pulling, pushing, and publishing via hatenablog-workflows; update those with `bash scripts/download_boilerplate_workflows.sh`.
- Blog configuration lives in `blogsync.yaml`; do not commit secrets or personal API keys.

## Build, Sync, and Development Commands
- `blogsync pull yoshiyoshifujii.hatenablog.com` — fetch latest posts from Hatena into `entries` (requires configured `blogsync` and API key).
- `blogsync push yoshiyoshifujii.hatenablog.com` — push local changes back to Hatena; use only after review/approval.
- `bash scripts/download_boilerplate_workflows.sh` — refresh reusable GitHub Actions definitions from upstream.
- GitHub Actions: trigger `create draft`, `pull draft from hatenablog`, or `pull from hatenablog` in the Actions tab instead of manual CLI if you prefer the hosted flow.

## Content Style & Naming Conventions
- File naming: keep date folders and numeric entry IDs from Hatena; for new drafts, follow `draft_entries/<domain>/entry/YYYYMMDD/<slug>.md`.
- Writing: use Markdown, prefer `#`/`##` headings, code fences for snippets, and keep front matter minimal—avoid deleting `EditURL`/`PreviewURL`.
- Categories: maintain existing Japanese taxonomy; add new tags sparingly and in Japanese when aligning with current entries.

## Testing and Validation
- No automated tests; validate by rendering Markdown locally and checking internal links.
- For drafts, confirm `Draft: true` stays set until publish; before merging, remove it and ensure `CustomPath` (if set) matches intended URL.
- After syncing or pushing, spot-check one or two changed entries to confirm dates and URLs remain untouched.

## Commit and Pull Request Guidelines
- Use short, imperative commit subjects (e.g., `Add draft on <topic>`, `Fix category for 20100724 entry`), mirroring existing history.
- PRs: include summary of affected entries, paste preview URLs (template provides them), and note whether the change is draft-only or publishes content.
- Link related issues if any; screenshots are optional, but add if formatting is novel or includes embedded media.

## Security & Configuration Tips
- Keep `OWNER_API_KEY` secret and `BLOG_DOMAIN` variable scoped in GitHub settings; avoid echoing secrets in logs.
- Changes to `blogsync.yaml` affect sync targets—coordinate before switching domains or local roots.
