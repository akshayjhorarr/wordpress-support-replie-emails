Email Reply #002 — fetchpriority="high" Being Removed
Subject: Re: fetchpriority="high" getting stripped from featured image
Hi,
Great question — and you've already done excellent troubleshooting by ruling out Astra Pro and WP Rocket. That actually points us straight to the real cause.
This is a WordPress core behavior introduced in version 6.3. WordPress has its own system for managing the fetchpriority attribute on images, and it intentionally overrides values set through the wp_get_attachment_image_attributes filter. That's why loading="eager" and data-test="YES" work fine — but fetchpriority gets removed every time.
The fix is to use a different filter that runs after WordPress finishes its own processing:
Add this to your functions.php:

add_filter( 'wp_get_attachment_image', function( $html, $attachment_id ) {
    if ( has_post_thumbnail() && get_post_thumbnail_id() === $attachment_id ) {
        if ( strpos( $html, 'fetchpriority' ) === false ) {
            $html = str_replace( '<img ', '<img fetchpriority="high" ', $html );
        } else {
            $html = str_replace( 'fetchpriority="low"', 'fetchpriority="high"', $html );
        }
    }
    return $html;
}, 10, 2 );
After adding this, clear your WP Rocket cache and check the image in browser DevTools (right-click → Inspect → find your featured image tag). You should see fetchpriority="high" in the HTML.
This approach works reliably because it modifies the final HTML string after WordPress has finished its own optimization pass.
Let me know if you'd like me to walk through any part of this in more detail!
Best,
Akshay Jhorar
WordPress Support Specialist