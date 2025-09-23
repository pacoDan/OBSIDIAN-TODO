https://nextjs.org/docs/pages/api-reference/cli/create-next-app

creación del proyecto ejemplo:
```sh
╰─❯ npx create-next-app@latest --ts
Need to install the following packages:
create-next-app@15.1.3
Ok to proceed? (y) y

✔ What is your project named? … example-next-js
✔ Would you like to use ESLint? … No / Yes
✔ Would you like to use Tailwind CSS? … No / Yes
✔ Would you like your code inside a `src/` directory? … No / Yes
✔ Would you like to use App Router? (recommended) … No / Yes
✔ Would you like to use Turbopack for `next dev`? … No / Yes
✔ Would you like to customize the import alias (`@/*` by default)? … No / Yes
✔ What import alias would you like configured? … app/*
Creating a new Next.js app in /home/daniel_wsl/PROYECTOS/demo-next-js/example-next-js.

Using npm.

Initializing project with template: app-tw
```
import alias Yes tambien 

#### **###🚀 App Router vs Pages Router**

Next.js tiene dos enrutadores diferentes: App Router y Pages Router. **App Router** es un enrutador más nuevo que le permite utilizar las funciones más recientes de React, como Server Components. Pages Router es el enrutador Next.js original, que le permitió a crear aplicaciones React renderizadas en el servidor utilizando `getStaticProps` y `getServerSideProps` y continúa siendo compatible con aplicaciones Next.js más antiguas.

.

Ten esto presente porque hay mucha información sobre Pages Router (ya que estuvo varios años en funcionamiento). Puedes revisar la documentación de Next.js para que veas las diferencias [https://nextjs.org/docs](https://nextjs.org/docs), hay menú desplegable que muestra “Using App router” o “Using Pages router”.

---
## TOP Levels Folders

Son usadas para organizar nuestra aplicacion y recuros estaticos:
app App Router
pages Pages Router
public Static assets to be served
src Optional application source folder

## TOP LEVELS FILES

Son usadas para configurar nuestra aplicacion, manejar dependencias, correr middleware, integrar herramientas de monitoreo y definir variables de entorno.
next.config.js Configuration file for Next.js
package.json Project dependencies and scripts
instrumentation.ts OpenTelemetry and Instrumentation file
middleware.ts Next.js request middleware
.env Environment variables
.env.local Local environment variables
.env.production Production environment variables
.env.development Development environment variables
.eslintrc.json Configuration file for ESLint
.gitignore Git files and folders to ignore
next-env.d.ts TypeScript declaration file for Next.js
tsconfig.json Configuration file for TypeScript
jsconfig.json Configuration file for JavaScript

# APP ROUTING CONVENTIONS

Dentro del App router pueden existir estos archivos:
layout Layout
page Page
loading Loading UI
not-found Not found UI
error Error UI
global-error Global error UI
route endpoint
template Re-rendered layout
default Parallel route fallback page

- Pero adicionalmente ofrece otros features como:
  [x] Nested Routes
  [x] Dynamic Routes
  [x] Route Groups and Private Folders
  [x] Parallel and Intercepted Routes
  [x] Metadata File Conventions
  [x] Open Graph and Twitter Images
  [x] SEO

```
Ref: \[Next.js Project Structure]\(<u>https://nextjs.org/docs/getting-started/project-structure</u>)
```


