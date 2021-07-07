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



## Pronto más secciones...
- Estoy trabajando en los próximos videos...

<div>
    <img :src="$withBase('/img/trabajar.gif')">
</div>