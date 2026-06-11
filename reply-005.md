Email Reply #005 — Fatal Error: call_user_func_array()
Subject: Re: Fatal error — call_user_func_array() sanitize_comment_cookies not found
Hi,
I can see why this is frustrating — you've already tried the usual fixes and nothing has worked. The good news is the error message actually tells us exactly what's wrong.
The function sanitize_comment_cookies is part of WordPress core. The error means WordPress is trying to call this function but it can't find it — which tells us that your WordPress core files are most likely corrupted or incomplete. This is why disabling plugins and changing PHP versions didn't help — the problem is in the core files themselves, not your plugins or PHP.
Here's how to fix it:
Step 1 — Re-upload WordPress core files
Go to wordpress.org/download and download the latest WordPress zip file.
Extract it on your computer.
Connect to your server via FTP (FileZilla is free and works well).
Upload ONLY these — do not touch wp-content:
The wp-admin folder (replace entirely)
The wp-includes folder (replace entirely)
All .php files in the root (wp-login.php, wp-settings.php, index.php etc.)
Your wp-content folder stays untouched — all your themes, plugins and uploads are safe.
Step 2 — Check wp-config.php
Open your wp-config.php file via FTP and make sure there are no extra characters or broken lines at the top or bottom of the file.
Step 3 — Clear cache
Delete everything inside wp-content/cache/ via FTP.
Then test your site in an incognito browser window.
What most likely happened: A WordPress auto-update partially failed, leaving some core files incomplete. This is more common on shared hosting where file write permissions are restricted during updates.
After re-uploading the core files, your site should load normally. This fix works in the large majority of cases like this.
Let me know how it goes — if the error is still showing after the re-upload, share the updated error message and we can dig deeper!
Best,
Akshay Jhorar
WordPress Support Specialist