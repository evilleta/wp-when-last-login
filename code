add_action( 'wp_login', 'nimda_collect_login_timestamp', 20, 2 );
 
function nimda_collect_login_timestamp( $user_login, $user ) {
 
	update_user_meta( $user->ID, 'last_login', time() );
 
}
add_filter( 'manage_users_columns', 'nimda_add_last_login_column' );
add_filter( 'manage_users_custom_column', 'nimda_last_login_column', 10, 3 );
 
function nimda_user_last_login_column( $columns ) {
 
	$columns['last_login'] = 'Last Login'; // column ID / column Title
	return $columns;
 
}
 
function nimda_last_login_column( $output, $column_id, $user_id ){
 
	if( $column_id == 'last_login' ) {
 
		$last_login = get_user_meta( $user_id, 'last_login', true );
		$date_format = 'j M, Y';
 
		$output = $last_login ? date( $date_format, $last_login ) : '-';
 
	}
 
	return $output;
 
}
add_filter( 'manage_users_sortable_columns', 'nimda_sortable_columns' );
add_action( 'pre_get_users', 'nimda_sort_last_login_column' );
 
function nimda_sortable_columns( $columns ) {
 
	return wp_parse_args( array(
	 	'last_login' => 'last_login'
	), $columns );
 
}
 
function nimda_sort_last_login_column( $query ) {
 
	if( !is_admin() ) {
		return $query;
	}
 
	$screen = get_current_screen();
 
	if( isset( $screen->id ) && $screen->id !== 'users' ) {
		return $query;
	}
 
	if( isset( $_GET[ 'orderby' ] ) && $_GET[ 'orderby' ] == 'last_login' ) {
 
		$query->query_vars['meta_key'] = 'last_login';
		$query->query_vars['orderby'] = 'meta_value';
 
	}
 
	return $query;
 
}
