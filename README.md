# The Literary Dove — GitHub Pages + Decap CMS

## Before uploading
1. Back up your current repository (download a ZIP or create a branch).
2. Upload all project files and folders to the **root** of your existing GitHub repository, replacing the old index.html.
3. Edit `_config.yml`: set `baseurl` to `/your-repository-name` (or `""` for a root-domain site). Edit `admin/config.yml`: replace `REPLACE_USERNAME/REPLACE_REPOSITORY` with your actual `owner/repo`.
4. Configure a trusted Decap-compatible GitHub OAuth provider. Set `base_url` to its HTTPS origin (no trailing slash), and set `auth_endpoint` to the path it documents (often `auth`). This is **not** a working login until OAuth is configured.
5. Keep GitHub Pages publishing from `main` / root; allow a few minutes for Jekyll to build.
6. Visit your actual Pages URL followed by `/admin/` (e.g. `https://owner.github.io/repo/admin/`). Sign in with your GitHub account.

## Authentication
GitHub Pages cannot host a server-side OAuth callback. Decap's GitHub backend requires an OAuth provider such as a properly configured Cloudflare Worker implementation, or a managed provider such as Decap Turbo (which uses a different backend config). Register the GitHub OAuth app with the callback URL specified by your chosen provider. Store the client secret ONLY in that provider's secret settings, never in this repository. Do not use `open_authoring: true` if you want only repository writers to edit.

## Content
Create or edit an article in `/admin/`. Published articles become files in `_posts/`; uploaded images are committed to `images/uploads/`. GitHub Pages builds the homepage and article URLs automatically.

## Important image-path note
The CMS `public_folder` is relative (`images/uploads`) so article cover image URLs work under a GitHub Pages project subpath. In Markdown article bodies, inserted images may be relative to the article permalink and fail. Prefer inserting images via Markdown using `{{ site.baseurl }}/images/uploads/filename.jpg` in source (Jekyll Liquid), or set a full public URL to the uploaded image. For a production CMS with frequent inline images, customize the media handling further.

## Safety and publishing
A publicly reachable `/admin/` page is not itself a security problem: GitHub write permissions control publishing. Enable 2FA on your GitHub account, do not grant collaborators write access, and follow your school's publication/privacy policies. Never commit OAuth client secrets.

## Notes
- This is a new Jekyll-based version; old article objects inside your previous `index.html` are NOT imported.
- If your repository uses a custom domain or is a user/organisation root site, update `_config.yml` as appropriate. Set `baseurl` to match your project URL path exactly.
- The search field filters headlines and article summaries on the homepage; it is not full-text search.
