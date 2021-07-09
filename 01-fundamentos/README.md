---
metaTitle: Fundamentos de Next.js Framework React.
meta:
  - name: description
    content: Aprendamos los conceptos claves de cómo trabajar con Next.js, aprenderás a crear tus primeros proyectos utilizando SSG y SSR.
lang: en-ES
---

# Fundamentos
Aprenderemos los fundamentos de Next.js

## Requisitos
- [Javascript Moderno](https://youtu.be/Z4TuS0HEJP8)
- [Node.js Fundamentos](https://youtu.be/mG4U9t5nWG8)
- [React Hooks Fundamentos](https://youtu.be/Di4eAxkPNp0)

::: tip CURSO EN UDEMY OFERTA!
Aprende desde cero a trabajar con <b>React.js y Firebase</b> aquí: [Inscríbete Aquí](http://curso-react-js-udemy.bluuweb.cl)
<b>Nos vemos en clases!</b>
:::

## ¿Qué es Next.js?
- [https://nextjs.org/](https://nextjs.org/)
- Framework de React para producción.
- Next.js le brinda la mejor experiencia de desarrollador con todas las funciones que necesita para la producción: SSR / server side rendering, Renderizado estático (SSG / static site generator), Router, compatibilidad con TypeScript, etc.
- No necesita configuración. 

## Aprender Next.js
En esta primera parte del curso nos basaremos en su potente guía de aprendizaje:

- [Guía aprendizaje](https://nextjs.org/learn/basics/create-nextjs-app)

## ¿SSG? ¿SSR? 
Anteriormente creamos aplicaciones SPA las cuales no tienen un pre-renderizado.

<img :src="$withBase('/img/spa.jpg')">

La carga se la lleva el navegador, ya que a través de Javascript nosotros "pintamos" todo nuestro sitio web.

### Pre-rendering
De forma predeterminada, Next.js procesa previamente cada página. Esto significa que Next.js genera HTML para cada página por adelantado , en lugar de hacerlo todo con JavaScript del lado del cliente. El renderizado previo puede resultar en un mejor rendimiento y SEO.

- [Ejemplo con next.js](https://next-learn-starter.vercel.app/)
- [Ejemplo create react app](https://create-react-app.now-examples.vercel.app/)

<img :src="$withBase('/img/ssr.jpg')">

### Dos formas de renderizado previo
Next.js tiene dos formas de renderizado previo: generación estática (SSG) y renderizado del lado del servidor (SSR). La diferencia está en cuando genera el HTML para una página.

<b>Static Generation</b> es el método de representación previa que genera el HTML en el momento de la <b>compilación</b>.

<b>La representación del lado del servidor</b> es el método de representación previa que genera el HTML en cada solicitud.

## Mi primer proyecto
Para craer un proyecto necesitamos configurar Webpack, babel, SEO, prerenderizar, etc, pero Next nos resuelve esto con su instalación sin configuraciones.

Requisitos
```sh
node -v
npm -v
```

Instalador
```sh
npx create-next-app nombre-proyecto

cd nombre-proyecto
npm run dev
```

## VSC
- [ES7 React](https://marketplace.visualstudio.com/items?itemName=dsznajder.es7-react-js-snippets)
- [Theme](https://marketplace.visualstudio.com/items?itemName=dbanksdesign.nu-disco)

```js
_rfc (snippet)

export default function about() {
    return (
        <div>
            soy la página de about
        </div>
    )
}
```

## Rutas
Exploremos cómo agregar más páginas a nuestra aplicación.

- ``pages/index.js`` está asociado con la ``/`` ruta.

Podemos crear páginas de diferentes formas:

- `pages/contacto.jsx`
- `pages/contacto/index.jsx`

Estas dos opciones llevarán a la misma ruta: "/contacto"

- `pages/blog/index.jsx`

```jsx
export default function Blog() {
  return (
    <div>
      <h1>Lista de Posts</h1>
    </div>
  );
}
```

- `pages/blog/articulo-uno.jsx`

```jsx
export default function ArticuloUno() {
  return (
    <div>
      <h1>Articulo 1</h1>
    </div>
  );
}
```

:::tip
El componente puede tener cualquier nombre, pero debe exportarlo como ``export default``.
:::

## Link

En Next.js `Link` se utiliza para envolver la etiqueta `<a>`

```jsx
import Link from "next/link";

export default function contacto() {
  return (
    <div>
      <h1>Contacto</h1>
      <button>
        <Link href="/">
          <a>Inicio</a>
        </Link>
      </button>
    </div>
  );
}
```
### Beneficios de Link
- Link es más rápido que la navegación nativa del navegador.
- Next.js divide el código automáticamente, por lo que cada página solo carga lo necesario para esa página. Eso significa que cuando se representa la página de inicio, el código de otras páginas no se sirve inicialmente.
- Si una página tiene errores queda aislada, por ende si no viaja a esa ruta su aplicación funcionará correctamente.
- [Link](https://nextjs.org/docs/api-reference/next/link)
- [Routing](https://nextjs.org/docs/routing/introduction)

## Image
Next.js proporciona un ``Image`` componente listo para usar para manejar esto por usted.

```
public/imagenes
```

- [picsum.photos](https://picsum.photos/)

- Las imágenes se cargan a medida que se desplazan hacia la ventana gráfica.
- Las imágenes siempre se representan de tal manera que se evite el cambio de diseño acumulativo, un elemento fundamental de la Web que Google utilizará en el ranking de búsqueda.
- [Optimización de imágenes](https://nextjs.org/docs/basic-features/image-optimization)


```jsx
import Image from "next/image";

export default function ArticuloUno() {
  return (
    <div>
      <h1>Articulo 1</h1>

      <Image
        src="/imagenes/perfil.jpg"
        height={400}
        width={400}
        alt="mi imagen de perfil"
      ></Image>
      
    </div>
  );
}
```

## Metadatos

```js
import Head from "next/head";
```

```jsx
<Head>
  <title>Create Next App</title>
  <link rel="icon" href="/favicon.ico" />
</Head>
```

pages/blog/index.jsx
```jsx
import Head from "next/head";

export default function index() {
  return (
    <>
      <Head>
        <title>Lista de Posts | Next.js</title>
        <meta name="description" content="Generated by create next app" />
      </Head>
      <h1>Lista de artículos</h1>
    </>
  );
}
```

## Layout (componente)
components/layout.jsx
```jsx
export default function Layout({ children }) {
  return <div>{children}</div>;
}
```

pages/blog/articulo-uno.jsx
```jsx
import Image from "next/image";
import Layout from "../../components/layout";

export default function ArticuloUno() {
  return (
    <Layout>
      <h1>Articulo 1</h1>

      <Image
        src="/imagenes/perfil.jpg"
        height={400}
        width={400}
        alt="mi imagen de perfil"
      ></Image>
    </Layout>
  );
}
```

styles/Layout.module.css
```css
.container {
    max-width: 36rem;
    padding: 0 1rem;
    margin: 3rem auto 6rem;
}
```

components/layout.jsx
```jsx
import styles from "../styles/Layout.module.css";

export default function Layout({ children }) {
  return <div className={styles.container}>{children}</div>;
}
```

Esto es lo que hacen los módulos CSS: genera automáticamente nombres de clase únicos . Siempre que use módulos CSS, no tiene que preocuparse por las colisiones de nombres de clases.

## Estilos Globales
Solo se manejan en el archivo ``_app.js``

```js
import '../styles/globals.css'

function MyApp({ Component, pageProps }) {
  return <Component {...pageProps} />
}

export default MyApp
```

## Layout (global)
Revisar estilos css en: [Tutorial css Next.js](https://nextjs.org/learn/basics/assets-metadata-css/polishing-layout)


```jsx
import styles from "../styles/Layout.module.css";
import utilStyles from "../styles/utils.module.css";

import Head from "next/head";
import Image from "next/image";
import Link from "next/link";

const name = "Bluuweb!";
export const siteTitle = "Mi sitio web con next.js";

export default function Layout({ children, home, title, description }) {
  return (
    <div className={styles.container}>
      <Head>
        <link rel="icon" href="/favicon.ico" />
        <title>{title}</title>
        <meta name="description" content={description} />
      </Head>
      <header className={styles.header}>
        {home ? (
          <>
            <Image
              priority
              src="/imagenes/perfil.jpg"
              className={utilStyles.borderCircle}
              height={144}
              width={144}
              alt={name}
            ></Image>
            <h1 className={utilStyles.heading2Xl}>{name}</h1>
          </>
        ) : (
          <>
            <Link href="/">
              <a>
                <Image
                  priority
                  src="/imagenes/perfil.jpg"
                  className={utilStyles.borderCircle}
                  height={108}
                  width={108}
                  alt={name}
                ></Image>
              </a>
            </Link>
            <h2 className={utilStyles.headingLg}>
              <Link href="/">
                <a className={utilStyles.colorInherit}>{name}</a>
              </Link>
            </h2>
          </>
        )}
        <nav>
          <Link href="/">
            <a>Inicio | </a>
          </Link>
          <Link href="/blog">
            <a>Blog | </a>
          </Link>
          <Link href="/contacto">
            <a>Contacto</a>
          </Link>
        </nav>
      </header>
      <main>{children}</main>
      {!home && (
        <div className={styles.backToHome}>
          <Link href="/">
            <a>← Back to home</a>
          </Link>
        </div>
      )}
    </div>
  );
}

Layout.defaultProps = {
  title: "Mi sitio web con Next",
  description: "Este es un sitio web para aprender con next.js",
};
```

### Ahora en las páginas:
```jsx
import Layout from "../components/layout";
import utilStyles from "../styles/utils.module.css";

export default function Home() {
  return (
    <Layout
      home
      title="Página de inicio"
      description="Descripción de la página de inicio"
    >
      <section className={utilStyles.headingMd}>
        <p>[Your Self Introduction]</p>
        <p>
          (This is a sample website - you’ll be building a site like this on{" "}
          <a href="https://nextjs.org/learn">our Next.js tutorial</a>.)
        </p>
      </section>
    </Layout>
  );
}
```

Separando el código:
components/Header.jsx
```jsx
import Image from "next/image";
import Link from "next/link";
import utilStyles from "../styles/utils.module.css";
import styles from "../styles/Layout.module.css";

const name = "bluuweb!";

export default function Header({ home }) {
  return (
    <header className={styles.header}>
      {home ? (
        <>
          <Image
            priority
            src="/imagenes/perfil.jpg"
            className={utilStyles.borderCircle}
            height={144}
            width={144}
            alt={name}
          ></Image>
          <h1 className={utilStyles.heading2Xl}>{name}</h1>
        </>
      ) : (
        <>
          <Link href="/">
            <a>
              <Image
                priority
                src="/imagenes/perfil.jpg"
                className={utilStyles.borderCircle}
                height={108}
                width={108}
                alt={name}
              ></Image>
            </a>
          </Link>
          <h2 className={utilStyles.headingLg}>
            <Link href="/">
              <a className={utilStyles.colorInherit}>{name}</a>
            </Link>
          </h2>
        </>
      )}
      <nav>
        <Link href="/">
          <a>Inicio | </a>
        </Link>
        <Link href="/blog">
          <a>Blog | </a>
        </Link>
        <Link href="/contacto">
          <a>Contacto</a>
        </Link>
      </nav>
    </header>
  );
}
```

components/Layout.jsx
```jsx
import styles from "../styles/Layout.module.css";
import Header from "./Header";

import Head from "next/head";
import Link from "next/link";

export default function Layout({ children, home, title, description }) {
  return (
    <div className={styles.container}>
      <Head>
        <link rel="icon" href="/favicon.ico" />
        <title>{title}</title>
        <meta name="description" content={description} />
      </Head>

      <Header home />

      <main>{children}</main>
      {!home && (
        <div className={styles.backToHome}>
          <Link href="/">
            <a>← Back to home</a>
          </Link>
        </div>
      )}
    </div>
  );
}

Layout.defaultProps = {
  title: "Mi sitio web con Next",
  description: "Este es un sitio web para aprender con next.js",
};
```

## Pronto más secciones...
- Estoy trabajando en los próximos videos...

<div>
    <img :src="$withBase('/img/trabajar.gif')">
</div>