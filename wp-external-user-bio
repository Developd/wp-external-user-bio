<?php if ( ! defined( 'ABSPATH' ) ) exit;

/*
 * Plugin Name: External User Bio
 * Plugin URI: http://kylebjohnson.me
 * Description: Get a User Bio from another WordPress website.
 * Version: 0.1.0
 * Author: Kyle B. Johnson
 */

final class KBJ_ExternalUserBio
{
    public function __construct()
    {
        // Hijack Page Output
        if (isset( $_GET['kbj_user_bio'] )) {
            add_action('template_include', array( $this, 'external_user_bio' ) );
        }

        // Shortcode for Displaying Bio
        add_shortcode( 'user_bio', array( $this, 'user_bio') );
        add_shortcode( 'user_bio_external', array( $this, 'user_bio_external') );
    }

    function external_user_bio()
    {
        $user_id = $_GET['kbj_user_bio'];
        echo get_the_author_meta( 'description', $user_id );
        die();
    }

    function user_bio( $atts = array() )
    {
        return wpautop( get_the_author_meta( 'description', $atts['user_id'] ) );
    }

    function user_bio_external( $atts = array() )
    {
        $user_id = $atts['user_id'];
        $user_url = get_the_author_meta( 'user_url', $user_id );
        return wpautop( wp_remote_fopen( $user_url . '?kbj_user_bio=' . $user_id ) );
    }

}

new KBJ_ExternalUserBio();
