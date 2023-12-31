```c
function add_nn_to_existing_categories() {
    $args = array(
        'hide_empty' => false,
    );
    
    $categories = get_categories( $args );
    
    foreach ( $categories as $category ) {
        $original_slug = sanitize_title( $category->slug );
        $new_slug = 'nn-' . $original_slug;
        
        wp_update_term(
            $category->term_id,
            $category->taxonomy,
            array(
                'slug' => $new_slug,
            )
        );
    }
}

function add_nn_to_existing_posts() {
    $args = array(
        'post_type'      => 'series',
        'posts_per_page' => -1,
    );
    
    $posts = get_posts( $args );
    
    foreach ( $posts as $post ) {
        $original_slug = sanitize_title( $post->post_title );
        $new_slug = 'nn-' . $original_slug;
        
        wp_update_post(
            array(
                'ID'        => $post->ID,
                'post_name' => $new_slug,
            )
        );
    }
}

add_action( 'init', 'add_nn_to_existing_posts' );
```