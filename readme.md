# WordPress Customizer Radio Image Control

A radio control using images for the WordPress Customizer

![Animation. Two icons. One is 3 stacked rectangles representing a list. The other 6 boxes in two rowns of 3 representing a grid.](https://user-images.githubusercontent.com/507025/136675766-d1370616-a9e4-4c94-b0b6-154e5d773086.gif)

## Installation

Add the following to your `composer.json` file and run `composer update`

```
"repositories": [
{
    "type": "git",
    "url": "https://github.com/helgatheviking/kia-customizer-radio-image-control.git"
}
],
"require": {
"helgatheviking/kia-customizer-radio-image-control": "dev-main"
},
"extra": {
"installer-paths": {
    "includes/{$name}": [
        "helgatheviking/kia-customizer-radio-image-control"
    ]
}
```

## Adding the control

```php

/**
 * Add range slider to Customizer.
 *
 * @param  obj     $wp_customize
 */
function kia_customizer( $wp_customize ) {
    // Include the class
    require_once dirname( __FILE__ ) . '/includes/kia-customizer-radio-image-control/class-kia-customizer-radio-image-control.php';

    // Register the control types that we're using as JavaScript controls.
	$wp_customize->register_control_type( 'KIA_Customizer_Radio_Image_Control' );

    $wp_customize->add_setting(
        'my_setting',
        array(
            'default'              => 'tabular',
            'type'                 => 'option',
            'capability'           => 'edit_themes',
            'sanitize_callback'    => array( 'KIA_Customizer_Radio_Image_Control', 'sanitize' ),
            'sanitize_js_callback' => array( 'KIA_Customizer_Radio_Image_Control', 'sanitize' ),
        )
    );

	$wp_customize->add_control(
		new KIA_Customizer_Radio_Image_Control(
			$wp_customize,
			'my_setting',
			array(
				'label'       => __( 'Layout', 'your-textdomain' ),
				'section'  => 'my_section',
				'settings' => 'my_setting',
				'choices'     => array(
					'tabular' 	=> array(
						'label' => esc_html__( 'List', 'your-textdomain' ),
						'img'   => 'assets/images/th-list.svg', // URL to image.
					),
					'grid'		=> array(
						'label' => esc_html__( 'Grid', 'your-textdomain' ),
						'img'   => 'assets/images/th-grid.svg', // URL to image.
					),
				),
			),
		)
	);

}
add_action( 'customize_register', 'kia_customizer' );
```

## Credits

Huge props to Rich Tabor's [Login Designer](https://github.com/thatplugincompany/login-designer).