# [GitHub Pages](https://pages.github.com/)

Free web hosting for static sites.
Will default to `username.github.io` with optional `/repo_name/` at the end, but also supports hosting for a custom domain that you have bought elsewhere.

# EECS User Hosting

These instructions will serve a website from `https://www.cs.tufts.edu/~EECS_username/`.

1. SSH into `linux.eecs.tufts.edu` with your EECS username and password.
2. In your home directory run `mkdir public_html; chmod 775 public_html`.
3. Place website files into `public_html` and apply `chmod 644` on all files you want to be publicly available.
4. Wait a minute before testing the site so changes have time to take effect.
5. Visit https://www.cs.tufts.edu/~EECS_username/ or https://www.eecs.tufts.edu/~EECS_username/ to view the website. This will load `index.html` but you can view other files by adding the appropriate path to the end of the URL.
