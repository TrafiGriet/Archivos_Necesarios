# Ejercicios: ampliar la lista de blogs

Además de los ocho ejercicios en las secciones [React router](https://fullstackopen.com/es/part7/react_router[) y [custom hooks](https://fullstackopen.com/es/part7/hooks_personalizados) de esta séptima parte del material del curso, hay 13 ejercicios que continúan nuestro trabajo en la aplicación BlogList en la que trabajamos en las partes cuatro y cinco del material del curso. Algunos de los siguientes ejercicios son "funcionalidades" que son independientes entre sí, lo que significa que no es necesario terminarlos en ningún orden en particular. Eres libre de saltarte una parte de los ejercicios si lo deseas. Muchos de ellos son acerca de aplicar la técnica de gestión avanzada de estado (Redux, React Query y context) cubierta en la [parte 6](https://fullstackopen.com/es/part6).  
Si no deseas utilizar tu propia aplicación BlogList, puedes utilizar el código de la solución modelo como punto de partida para estos ejercicios.

Muchos de los ejercicios de esta parte del material del curso requerirán la refactorización del código existente. Esta es una realidad común a la hora de extender aplicaciones existentes, lo que significa que la refactorización es una habilidad importante y necesaria incluso si a veces puede parecer difícil y desagradable.

Un buen consejo para refactorizar y escribir código nuevo es dar _pequeños pasos_. Perder la cordura está casi garantizado si dejas la aplicación en un estado completamente roto durante largos períodos de tiempo mientras refactorizas.

> [!NOTE]
>
> ### 🎯 Base del Código y Ejercicios (7.9 - 7.21)
>
> La base para la realización de los ejercicios **7.9 al 7.21** es el código que desarrollé previamente en los módulos **Backend (parte-4)** y **Frontend (parte-5)**, y no el código de la solución modelo del curso.
>
> ### 🗑️ Archivos Omitidos
>
> Se han **omitido intencionalmente** los siguientes archivos y carpetas, ya que no son necesarios para completar los ejercicios propuestos:
>
> **📦 Backend (`parte-4`)**
>
> - `controllers/testing.js`: Archivo de _endpoint_ utilizado exclusivamente durante las pruebas E2E.
> - `carpeta tests`: Contiene todos los _tests_ del backend (principalmente con la librería **Supertest**).
>
> **🎨 Frontend (`parte-5`)**
>
> - `carpeta bloglist-pruebas-e2e`: Contiene los _tests_ de la lista de blogs con **Playwright** (pruebas E2E).
> - `components/Blog.test.jsx`: Archivo de _tests_ para el componente `Blog` (con **@testing-library/react**).
> - `components/BlogFormulario.test.jsx`: Archivo de _tests_ para el formulario de blogs (con **@testing-library/react**).
> - `archivo configuracionTests.js`: Función para resetear el JSDOM en el entorno de pruebas.
>
> ### 🧹 Legibilidad del Código
>
> Por último, se aclara que los **comentarios de código** del backend y frontend han sido eliminados en esta versión. Esto se hizo para mejorar la legibilidad y evitar redundancias, ya que los comentarios detallados se encuentran disponibles en las carpetas originales (`parte-4` y `parte-5`).
