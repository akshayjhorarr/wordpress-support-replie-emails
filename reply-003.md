Email Reply #003 — Custom Classes in wp_nav_menu
Subject: Re: Adding dropdownitem, nav-dropdown and dropdown classes to wp_nav_menu
Hi,
Good news — this is very doable with a Custom Walker class. It sounds more complicated than it is, so let me walk you through it clearly.
WordPress builds navigation menus using something called a "Walker" — basically a blueprint for how menu HTML is generated. By creating a custom version, you can control exactly what classes get added and where.
Here's the complete solution — add this to your functions.php:

class Custom_Nav_Walker extends Walker_Nav_Menu {

    function start_el( &$output, $item, $depth = 0, $args = array(), $id = 0 ) {
        $classes = empty( $item->classes ) ? array() : (array) $item->classes;
        
        // Add dropdownitem class to parent menu items
        if ( in_array( 'menu-item-has-children', $classes ) ) {
            $classes[] = 'dropdownitem';
        }
        
        $class_names = 'item ' . join( ' ', array_filter( $classes ) );
        $output .= '<li class="' . esc_attr( $class_names ) . '">';
        
        // Add nav-dropdown class to parent links
        $link_class = in_array( 'menu-item-has-children', (array) $item->classes ) 
            ? ' class="nav-dropdown"' : '';
        
        $output .= '<a href="' . esc_attr( $item->url ) . '"' . $link_class . '>' 
            . $item->title . '</a>';
    }

    // Wrap sub-menus in dropdown div
    function start_lvl( &$output, $depth = 0, $args = array() ) {
        $output .= '<div class="dropdown"><ul>';
    }

    function end_lvl( &$output, $depth = 0, $args = array() ) {
        $output .= '</ul></div>';
    }
}


Then update your wp_nav_menu call:

wp_nav_menu( array(
    'theme_location' => 'primary',
    'menu_class'     => 'mnav m-lg-auto',
    'container'      => false,
    'walker'         => new Custom_Nav_Walker(),
) );


This will output exactly the HTML structure you showed. The dropdownitem class goes on the parent li, nav-dropdown goes on the parent link, and dropdown wraps the sub-menu.
If you share what theme you're using, I can also check if there's an existing walker you can extend instead of building from scratch.
Hope this helps — let me know how it goes!
Best,
Akshay Jhorar
WordPress Support Specialist



