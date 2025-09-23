![[Pasted image 20250102003305.png]]
**Rutas Estáticas:** Son rutas cuyos paths o URL son definidos de manera estática. Esto significa que el contenido asociado a estas rutas se genera durante la fase de compilación y no cambia después de que la aplicación ha sido construida y desplegada.

- En Next.js, las rutas estáticas son típicamente creadas en el directorio `pages` de tu proyecto. Cada archivo en `pages` se convierte en una ruta estática.
```sh
pages/
├── index.js        // Ruta estática: /
├── about.js        // Ruta estática: /about
├── contact.js      // Ruta estática: /contact
```

En este ejemplo, `/`, `/about`, y `/contact` son rutas estáticas porque sus paths son definidos de manera fija y no cambian durante la ejecución de la aplicación.

**Rutas Dinámicas:** Son rutas que pueden cambiar dinámicamente en función de parámetros específicos que se incluyen en la URL. Esto permite crear páginas que pueden manejar diferentes contenidos según los valores de los parámetros.

- En Next.js, puedes lograr rutas dinámicas utilizando corchetes `[]` en los nombres de los archivos en el directorio `pages`.
```sh
pages/
├── posts/
│   ├── [id].js     // Ruta dinámica: /posts/[id]
│   ├── latest.js   // Ruta estática: /posts/latest
```
En este ejemplo, `/posts/[id]` es una ruta dinámica porque `[id]` es un marcador de posición para un parámetro que puede variar en cada solicitud. Puedes tener URLs como `/posts/1`, `/posts/2`, etc., y el valor de `id` se utiliza para personalizar el contenido de la página.

En resumen, las rutas estáticas se definen con paths fijos y su contenido se genera durante la compilación, mientras que las rutas dinámicas permiten manejar parámetros que pueden cambiar en función de la URL solicitada. Next.js ofrece una forma conveniente de trabajar con ambos tipos de rutas y proporciona una gran flexibilidad para desarrollar aplicaciones web. (Créditos a chatgpt).

----
Atomizar componentes se refiere a dividir una aplicación en componentes más pequeños y reutilizables. En el contexto de Next.js, esto permite crear estructuras más limpias y mantenibles. Al hacerlo, cada componente puede encargarse de una parte específica de la funcionalidad o presentación, lo que mejora la organización del código y la eficiencia en el rendimiento. Además, facilita la prueba y la reutilización de cada parte de la aplicación. Esta práctica es esencial para desarrollar aplicaciones escalables y de alto rendimiento.
