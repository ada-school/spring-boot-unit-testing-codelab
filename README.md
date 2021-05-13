<img align="right" src="https://github.com/ada-school/module-template/blob/main/ada.png">

## Pruebas Unitarias en Spring Boot con Kotlin


**Objetivos de Aprendizaje**

- [ ] Implementar y configurar JWT Interceptor.
- [ ] Utilizar mocks para implementar pruebas unitarias.
- [ ] Implementar LocalStorage y almacenar el token JWT.


**Temas Principales**
* Interceptor.
* JWT.
* SharedPreferences.
* LauncherActivity.

## Codelab 🧪

🗣️ "Oigo y olvido. Veo y aprendo. Hago y entiendo." Confucio

### Parte 1: Implementando el LocalStorage

1. Lee y entiende la documentación oficial de Android del [SharedPreferences](https://developer.android.com/training/data-storage/shared-preferences).
2. Crea una implementación de la interfaz *Storage* llamada *LocalStorage* que por dentro utiliza el *SharedPreferences*:
  ```kotlin
      interface Storage {

          fun saveToken(token: String)

          fun getToken(): String

          fun clear()

      }
  ```
3.Configura el nuevo módulo de inyección de dependencias para que puedas inyectar tu *Storage* en cualquier lugar del proyecto e instancialo usando la implementación que hiciste en 2. *LocalStorage*.


### Parte 2: Implementando el LauncherActivity

1. Crea una nueva actividad llamada *LoginActiviy* e incluyela en el *AndroidManifest.xml*.
2. Crea una nueva actividad llamada *LauncherActivity*.
3. Modifica tu *AndroidManifest.xml* para que incluyas el *LauncherActivity* y que sea tu actividad principal y punto de entrada de tu app(Launcher).
4. Inyecta el *Storage* en el *LauncherActivity* y sobreescribe el método *onCreate(savedInstanceState: Bundle?)* para verificar si existe el token de usuario redireccionar al *MainActivity* en caso contrario al *LoginActivity*.


### Parte 3: Implementando el TokenInterceptor
1. Implementa la clase *TokenInterceptor*:
  ```kotlin
    class TokenInterceptor(private val storage: Storage) : Interceptor {
        override fun intercept(chain: Interceptor.Chain): Response {
            val request = chain.request().newBuilder()
            val token = storage.getToken()
            if (token.isNotEmpty()) {
                request.header("Authorization", "Bearer $token")
            }
            return chain.proceed(request.build())
        }
    }
  ```
2. Modifica la configuración de *Retrofit* agregando el *TokenInterceptor* al *OkHttpClient*:
  ```kotlin
    val okHttpClient = OkHttpClient.Builder()
            .addInterceptor(loggingInterceptor)
            .addInterceptor(TokenInterceptor(storage))
            .writeTimeout(0, TimeUnit.MILLISECONDS)
            .readTimeout(2, TimeUnit.MINUTES)
            .connectTimeout(1, TimeUnit.MINUTES).build()
  ```
3. Implementa alguno de los servicios de usuarios o tareas que están asegurados por el JWT y verifica que tu interceptor funciona correctamente.

