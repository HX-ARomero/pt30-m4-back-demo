# Ejercicios Tipo

## 1. Filtros
- Get de Usuario por país Query Params
- Controller => GET /users?page=1&limit=5&country=colombia
- Array => filter en array

## 2. Ordenamientos
- Get de Usuario por país Query Params
- Controller => GET /users?page=1&limit=5&order=asc
- Array => sort en array

## 3. GET /category/:id

## 4. Borrado Lógico
- isActive
- Filtrar los isActive: false en los GET

## 5. Agregar un nuevo campo en Users (birthdate)
- Entity
- Dto

## 6. Auth
- Crear el rol de superAdmin
  - Entity: default => false
  - Dto: isEmpty()
  - Agregar al Payload del Token: authService
  - Validar en el Token Recibido: RoleGuard

## 7. Estandarizar respuestas
```js
{
  success: true,
  status: 200,
  message: 'Categorías cargadas',
  response: [ {...}, {...} ],
  error: {...},
  timestamp: Date
}
```

## 8. Manejo de Errores
- Error Layer de NestJS

## 9. Middlewares, Interceptor, Pipe, Guardián
- Interceptor: Filtrar el password de usuarios (GET /users)

## 10. Simulacro de Defensa | EJERCICIO
Baneo de Usuarios por parte del Administrador
 1. Crear nuevo atributo en el Modelo Users de la Base de Datos
	- Llamarlo "isBlocked" y cuyo tipo sea "boolean"
	- Darle valor "false" por defecto
	- Impedir que el valor pueda ser enviado en el Body
2. Crear una ruta "PUT /users/blocked/:id"
	- Esta ruta cambia el valor de "isBlocked" al usuario cuyo ID se recibe por params
	- Proteger la ruta para que solo sea accesible por Administradores
3. Agregar este atributo al Payload del Token
	- Restringir el acceso a todo usuario bloqueado