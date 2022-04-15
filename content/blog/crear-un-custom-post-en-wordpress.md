---
title: Crear Custom Post en Wordpress
published: true
description: Función Php para crear y definir un Custom Post Type personalizado en Wordress
tags:
  - php
  - wordpress
ctime: "2013-10-20 15:10:00"
---

Crear un <strong>Custom Post</strong> por en Wordpress es relativamente sencillo con un poco de conocimiento de PHP. Voy a mostrar los pasos necesarios para poder tener un tipo de <strong>Post personalizado (Custom Post)</strong> en Wordpress, sin usar Plugins.

Actualmente Wordpress trae dos tipos: las <code>paginas</code> y las <code>entradas</code>.

Necesitaremos <strong>modificar</strong> el archivo <code>funtions.php</code> y crear un nuevo archivo php para mostrar el contenido del Custom Post.

Editar archivo <code>funtions.php</code>:

```php
function cp_portfolio() {
	$labels = array(
		'name'               => __( 'Portfolios' ),
		'singular_name'      => __( 'Portfolio' ),
		'add_new'            => __( 'Añadir nuevo' ),
		'add_new_item'       => __( 'Añadir nuevo item),
		'edit_item'          => __( 'Editar Portfolio' ),
		'new_item'           => __( 'Nuevo Portfolio' ),
		'all_items'          => __( 'Todos los Portfolios' ),
		'view_item'          => __( 'Ver Portfolios' ),
		'search_items'       => __( 'Buscar Portfolios' ),
		'not_found'          => __( 'No se encontraron portfolios' ),
		'not_found_in_trash' => __( 'No se encontraron portfolios en la paperlera' ), 
		'parent_item_colon'  => '',
		'menu_name'          => 'Portfolios'
	);
	$args = array(
		'labels'        => $labels,
		'description'   => 'Post para publicarlos trabajos realizados',
		'public'        => true,
		'menu_position' => 4,
		'supports'      => array( 'title', 'editor', 'thumbnail' ),
		'has_archive'   => true,
	);
	register_post_type( 'portfolio', $args );	
}
add_action( 'init', 'cp_portfolio' );
```

Crearemos un nuevo archivo php para mostrar las entradas que pertenecen al nuevo tipo llamado porfolio. El nombre debe seguir unas condiciones. Mi tipo de archivo, como se ve en la línea 26, se llama portfolio.

```php
register_post_type( 'portfolio', $args );
```

Nuestro archivo tiene que llamarse: <code>single-nombreelegido.php</code> (hay otra opción: <code>archive-nombreelegido.php</code>).

Nuestro archivo se llamará <code>single-portfolio.php</code>

<figure>
	<img alt="Schema Wordpress Rest Api" loading="lazy" src="/images/blog/crear-un-custom-post-en-wordpress/01.jpg">
</figure>

<figure>
	<img alt="Schema Wordpress Rest Api" loading="lazy" src="/images/blog/crear-un-custom-post-en-wordpress/02.jpg">
</figure>

<figure>
	<img alt="Schema Wordpress Rest Api" loading="lazy" src="/images/blog/crear-un-custom-post-en-wordpress/03.jpg">
</figure>

<figure>
	<img alt="Schema Wordpress Rest Api" loading="lazy" src="/images/blog/crear-un-custom-post-en-wordpress/04.jpg">
</figure>