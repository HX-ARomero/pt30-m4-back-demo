# TESTING

[Volver a Inicio](../../README.md)

> El testing es un proceso fundamental para asegurar que las aplicaciones funcionen correctamente, permitiendo verificar el comportamiento de los componentes de manera aislada y asegurando la calidad del código. NestJS facilita la realización de pruebas utilizando Jest como framework de testing por defecto, pero puede integrarse con otros frameworks de pruebas si se desea.

## A. Tipos de Testing según la automatización

- Manual: Una persona realiza las pruebas siguiendo un plan.
- Automatizado: Scripts y herramientas ejecutan las pruebas.
  - Herramientas web comunes: Jest, Mocha, Cypress, Playwright, Selenium.

## B. Tipos de Testing según el alcance

### 1. Unit Testing (Pruebas Unitarias):

Se enfocan en probar unidades de código individuales, como controladores o servicios, en aislamiento.
En NestJS, puedes utilizar Mocks y Stubs para simular dependencias y concentrarte en la lógica de la unidad que estás probando.
Se realizan utilizando las clases reales o mediante el uso de inyecciones falsas para reemplazar dependencias.

### 2. Integration Testing (Pruebas de Integración):

Estas pruebas verifican cómo interactúan varios módulos o componentes entre sí.
En NestJS, se utiliza un test module para simular el entorno del módulo real y se prueban las interacciones entre diferentes dependencias (por ejemplo, servicios y controladores).
A menudo se configuran con bases de datos en memoria como SQLite o MongoDB in-memory para pruebas más rápidas y realistas.

### 3. End-to-End Testing (E2E):

Este tipo de pruebas se enfoca en probar el sistema completo, emulando la interacción del usuario con la API.
Se utiliza una instancia real del servidor NestJS, para verificar que todo el flujo de la aplicación funciona correctamente.
Se emplea supertest junto con Jest para hacer peticiones HTTP y verificar las respuestas.

### 4. Aceptación / Usuario Final (Tests Manuales / De uso)

El cliente o usuarios validan si cumple con lo acordado.

---

## HERRAMIENTAS DE TESTING EN NestJS

- Jest: Framework por defecto para realizar pruebas en NestJS. Es potente, flexible y ampliamente utilizado en el ecosistema de Node.js.
- Supertest: Utilizado en pruebas de integración y E2E para realizar peticiones HTTP y validar respuestas.
- Test Utilities de NestJS: La función Test.createTestingModule() permite crear un entorno de prueba que emula los módulos de la aplicación real para pruebas unitarias e integradas.

<div style="text-align: center;">
  <img src="./assets/10-02.png" style="width: 700px;" alt="Tipos de Testing">
</div>

### Beneficios del Testing en NestJS

- Confiabilidad: Garantiza que los componentes funcionen como se espera a lo largo del tiempo.
- Mantenimiento: Facilita la identificación y corrección de errores, permitiendo que el código sea más fácil de mantener.
- Documentación: Las pruebas sirven como documentación viviente del comportamiento de la aplicación.
- Prevención de Regresiones: Ayuda a evitar que nuevas actualizaciones o cambios en el código introduzcan errores no deseados.

---

## 🚀 Secuencia de arranque en NestJS

### 1️⃣ main.ts — Punto de entrada

- Se crea la aplicación
- Se pasa el AppModule como módulo raíz

```ts
async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

### 2️⃣ NestFactory.create(AppModule)

Aquí comienza el proceso interno:

- Se crea el contenedor de dependencias (IoC Container)
  - Nest analiza:
    - @Module()
    - providers
    - controllers
    - imports
    - exports

### 3️⃣ Resolución de módulos (Dependency Graph)

Nest crea el Dependency Injection Container:

- Lee AppModule
- Carga módulos importados
- Resuelve dependencias
- Construye el árbol completo de inyección

### 4️⃣ Instanciación de Providers

Se crean:

- Services
- Repositories
- Guards
- Pipes
- Interceptors

### 5️⃣ Instanciación de Controllers

Una vez que los servicios existen, Nest crea los controllers e inyecta dependencias.

### 6️⃣ Registro del sistema HTTP

Por defecto:

- Usa Express (Puede usar Fastify si se configura)
- Aquí se:
  - Registran rutas
  - Vinculan controllers con endpoints
  - Configuran middlewares globales

### 7️⃣ Aplicación de configuración global

Se registran ahora pipes, guards interceptors y filters si se declararon en main.ts:

- app.useGlobalPipes(...)
- app.useGlobalGuards(...)
- app.useGlobalInterceptors(...)
- app.useGlobalFilters(...)

### 8️⃣ app.listen()

Aquí:

- Se abre el puerto
- Se inicia el servidor HTTP
- La app queda escuchando requests

<div style="text-align: center;">
  <img src="./assets/10-NestJS.png" style="width: 700px;" alt="Tipos de Testing">
</div>

### 🧠 Qué es lo más importante entender

Nest es:

- Modular
- Basado en Dependency Injection
- Orientado a metadata (decoradores)
- Basado en un contenedor IoC
- Primero construye estructura interna
- Después arranca el servidor

---

[Volver a Inicio](../../README.md)
