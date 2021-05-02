<img align="right" src="https://github.com/ada-school/module-template/blob/main/ada.png">

## Pruebas Unitarias en Spring Boot con Kotlin


**Objetivos de Aprendizaje**

- [ ] Implementar pruebas unitarias para los servicios en Spring Boot.
- [ ] Utilizar mocks para la creación de pruebas unitarias.
- [ ] Ejectura y verificar pruebas unitarias en Spring Boot.


**Temas Principales**
* Pruebas Unitarias.
* JUnit.
* Spring Boot.
* Mock.

## Codelab 🧪

🗣️ "Oigo y olvido. Veo y aprendo. Hago y entiendo." Confucio

### Parte 1: Configurando Entorno API Usuarios

1. Descarga e importa el [API de Usuarios](https://github.com/ada-school/users-api) en IntelliJ Idea.
2. Ejectuta los tests creados de ejemplo en la clase *UsersApplicationTests* y verifica que estas pasan.

### Parte 2: Creando Mocks y Probando Interacciones

1. Agrega la dependencia de Mockito al entorno de pruebas de tu proyecto tu proyecto:
  ```gradle
      	testImplementation("org.mockito:mockito-core")
  ```
2. Lee y comprende cómo usar y para que sirve Mockito en la [documentación oficial de Mockito](https://site.mockito.org/).
3. Crea un nuevo packete en el directiorio base de *test* llamado *service*
4. Crea una nueva clase llamada *UserServiceMongoDBTest*
5. 
