<img align="right" src="https://github.com/ada-school/module-template/blob/main/ada.png">

## Pruebas Unitarias en Spring Boot con Kotlin



**Objetivos de Aprendizaje**

- [ ] Implementar pruebas unitarias para los servicios en Spring Boot.
- [ ] Implementar Launcher Activity para verificación del token de autorización.
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
2. Lee y comprende para que sirve Mockito y cómo usarlo en la [documentación oficial de Mockito](https://site.mockito.org/).
3. Crea un nuevo packete en el directiorio base de *test* llamado *service*
4. Crea una nueva clase llamada *UserServiceMongoDbTest*
5. Anota la clase *UserServiceMongoDBTest* con *@SpringBootTest* y *@TestInstance(TestInstance.Lifecycle.PER_CLASS)*
  ```kotlin 
    @SpringBootTest
    @TestInstance(TestInstance.Lifecycle.PER_CLASS)
    class UserServiceMongoDBTest {}
  ```
6. Crea un mock para la clase *UserRepository* e instancialo en una función de configuración anotada con *@BeforeAll* que se ejecutara siempre antes de ejecutar las otras funciones:
  ```kotlin
    @SpringBootTest
    @TestInstance(TestInstance.Lifecycle.PER_CLASS)
    class UserServiceMongoDbTest {

        @Mock
        var userRepository: UserRepository? = null

        @BeforeAll
        fun setup() {
            MockitoAnnotations.openMocks(this)
        }

    }
  ```
7. Finalmente instancia el componente que realmente queremos probar *UserServiceMongoDb* y pasale el mock creado en 6. como parametro en el contructor:
  ```kotlin
      @Mock
      lateinit var userRepository: UserRepository

      lateinit var userServiceMongoDb: UserServiceMongoDb

      @BeforeAll
      fun setup() {
          MockitoAnnotations.openMocks(this)
          userServiceMongoDb = UserServiceMongoDb(userRepository)
      }
  ```
8. Crea la funcion *saveUsersSavesOnRepositoryTest* y anotala con *@Test*.
9. Implementa la función *saveUsersSavesOnRepositoryTest* creando un *UserDto*(puede ser un mock también), invocando al método save en la instancia del *UserServiceMongoDb* y verificando la interacción con el método *save* del mock del *UserRepository*:
  ```kotlin
      @Test
      fun saveUsersSavesOnRepositoryTest(){
          val userDto = UserDto("1", "Name","mail@mail.com", "password")
          `when`(userRepository.save(any())).thenReturn(User(userDto))
          userServiceMongoDb.save(userDto)
          verify(userRepository)!!.save(any())
      }
  ```
10. Implementa los Unit Test faltantes para el CRUD del *UserServiceMongoDb* teniendo en cuenta las siguientes recomendaciones:
  * Utilizar nombres claros y compuestos para cada función que vas a probar.
  * Implementa una función por cada prueba que vas a realizar.
  * Crea tantos unit test como sean necesarios dependiendo de los posibles comportamientos de las funciones(Ej si findById retorna null o si retorna un usuario)
  * Verifica que las interacciones con el mock del *UserRepository* son correctas.
  * Utiliza la funcion `when` para configurar el comportamiento que esperas del mock.
