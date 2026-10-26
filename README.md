# Catálogo de productos con Astro

Prototipo de catálogo para una tienda. Los productos no están escritos a mano en el código: se piden a una API pública cuando Astro genera la página, y cada uno se dibuja con un componente reutilizable. Arriba hay un buscador que filtra las tarjetas por nombre sin recargar.

## API utilizada

DummyJSON, endpoint `https://dummyjson.com/products?limit=12`. Entrega datos de mentira para practicar, no pide cuenta ni clave. De cada producto uso `title`, `price`, `category`, `rating` y `thumbnail`.

## Cómo ejecutarlo

Necesitas Node 18.20 o superior.

```bash
npm install
npm run dev      # http://localhost:4321
npm run build    # genera la carpeta dist/
npm run preview  # sirve el resultado de build
```

## Estructura

```
src/
├── components/ProductoCard.astro   # una tarjeta, recibe todo por props
├── layouts/Layout.astro            # html, head y slot comunes
├── pages/index.astro               # fetch, map() y script del buscador
└── styles/global.css               # estilos y CSS Grid
```

## Cómo funciona

- El `fetch()` está en el frontmatter de `index.astro`, así que corre cuando se genera la página (en el servidor con `npm run dev`, al compilar con `npm run build`). Se revisa `respuesta.ok` y se toma `datos.products`.
- Si la API falla o devuelve una lista vacía, la página muestra un mensaje en vez de romperse.
- `productos.map()` crea un `<ProductoCard />` por producto. La página trae los datos y el componente solo los presenta.
- Las tarjetas van en un CSS Grid con `repeat(auto-fit, minmax(220px, 1fr))`, por eso se acomodan solas en pantallas chicas y no hay scroll horizontal.
- El buscador es un `<script>` que corre en el navegador. Cada vez que se escribe, compara el texto con el atributo `data-title` de cada tarjeta y le pone `hidden` a las que no coinciden. Si no queda ninguna visible, aparece un aviso.

## Limitación

El buscador solo filtra los 12 productos que se descargaron, no todo el catálogo de DummyJSON.

## Captura

![Captura del sitio](./captura.png)

_(Agregar aquí la captura del sitio funcionando antes de subir el repositorio.)_
# catalogo-api
