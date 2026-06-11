Email Reply #001 — iPad Dropdown Navigation Issue
Subject: Re: Dropdown menus not working on iPad after WordPress 7.0 upgrade
Hi,
Thanks for the detailed report — testing across multiple browsers really helped narrow this down quickly.
The good news is this is a known issue with WordPress 7.0 and the Twenty Twenty-Two theme on iOS devices. It's not related to your plugins at all, which is why disabling them didn't help.
Here's what's happening: WordPress 7.0 updated its navigation code in a way that doesn't play well with touch screens on iOS 26. Desktop browsers work fine because they use mouse hover — but iPads use touch, and that's where it breaks.
Here's the fix — try these in order:
Step 1 — Quick CSS fix
Go to: Appearance → Customize → Additional CSS
Paste this code and click Publish:
Code 
.wp-block-navigation__responsive-container
.wp-block-navigation-item__content {
  pointer-events: auto !important;
  touch-action: manipulation !important;
}
Then test your menus on iPad in a private browsing window.
Step 2 — If that doesn't work
Switch your theme temporarily to Twenty Twenty-Four (Appearance → Themes). If your menus work there, it confirms the issue is in Twenty Twenty-Two specifically.
Step 3 — Permanent workaround
Install the free "Classic Widgets" plugin and rebuild your navigation using the classic menu. This bypasses the problematic code entirely.
The CSS fix in Step 1 works for most people. Give it a try and let me know how it goes!
Best,
Akshay Jhorar
WordPress Support Specialist