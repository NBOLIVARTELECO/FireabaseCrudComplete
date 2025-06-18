# Firebase CRUD - Proyecto Java

## 📋 Descripción

Este proyecto implementa operaciones CRUD (Create, Read, Update, Delete) utilizando Firebase Realtime Database en Java. Es una aplicación de escritorio desarrollada con Java Swing que permite gestionar objetos de tipo `Item` con propiedades como ID, nombre y precio.

## 🏗️ Arquitectura del Proyecto

### Estructura de Directorios
```
FireabaseCrudComplete/
├── src/
│   ├── modelView/
│   │   ├── Item.java                    # Modelo de datos
│   │   ├── FirebasePushObject.java      # Operaciones de inserción con push()
│   │   ├── FirebaseSaveObject.java      # Operaciones CRUD básicas
│   │   ├── NewJFrame.java               # Interfaz gráfica principal
│   │   └── NewJFrame.form               # Archivo de diseño de formulario
│   └── view/
│       └── ventana.java                 # Clase de ventana adicional
├── lib/                                 # Dependencias JAR
├── nbproject/                           # Configuración de NetBeans
├── build.xml                            # Script de construcción Ant
└── manifest.mf                          # Archivo de manifiesto
```

## 🎯 Funcionalidades

### Operaciones CRUD Implementadas

1. **Create (Crear)**
   - `save()`: Guarda un objeto Item en Firebase
   - `saveUsingPush()`: Inserta un objeto usando push() para generar ID automático

2. **Read (Leer)**
   - `recover()`: Recupera datos desde Firebase Realtime Database

3. **Delete (Eliminar)**
   - `remove()`: Elimina registros de Firebase

### Modelo de Datos

```java
public class Item {
    private Long id;
    private String name;
    private Double price;
    // Getters y Setters
}
```

## 🔧 Configuración y Dependencias

### Dependencias Requeridas
- **firebase-server-sdk-3.0.1.jar**: SDK oficial de Firebase para Java
- **google-api-client-1.22.0.jar**: Cliente de API de Google
- **google-http-client-1.21.0.jar**: Cliente HTTP de Google
- **google-http-client-gson-1.22.0.jar**: Integración GSON para HTTP
- **google-oauth-client-1.21.0.jar**: Cliente OAuth de Google
- **gson-2.1.jar**: Biblioteca para serialización JSON
- **jackson-all-1.9.0.jar**: Biblioteca Jackson para JSON
- **java-json.jar**: Utilidades JSON para Java
- **mysql-connector-java-5.1.48-bin.jar**: Conector MySQL (no utilizado en este proyecto)

### Configuración de Firebase

El proyecto requiere configuración de Firebase con:

1. **URL de la base de datos**: Configurada en `initFirebase()`
2. **Archivo de credenciales**: Archivo JSON de service account
3. **Reglas de seguridad**: Configuradas en Firebase Console

### Configuración Actual
```java
FirebaseOptions firebaseOptions = new FirebaseOptions.Builder()
    .setDatabaseUrl("https://testvscode-5996d-default-rtdb.firebaseio.com/")
    .setServiceAccount(new FileInputStream(new File("path/to/service-account.json")))
    .build();
```

## 🚀 Instalación y Uso

### Prerrequisitos
- Java JDK 8 o superior
- NetBeans IDE (recomendado)
- Proyecto Firebase configurado
- Archivo de credenciales de service account

### Pasos de Instalación

1. **Clonar o descargar el proyecto**
   ```bash
   git clone [URL_DEL_REPOSITORIO]
   cd FireabaseCrudComplete
   ```

2. **Configurar Firebase**
   - Crear proyecto en [Firebase Console](https://console.firebase.google.com/)
   - Habilitar Realtime Database
   - Descargar archivo de service account
   - Actualizar rutas en el código

3. **Configurar dependencias**
   - Asegurar que todos los archivos JAR estén en el directorio raíz
   - Configurar classpath en NetBeans

4. **Compilar y ejecutar**
   ```bash
   ant build
   ant run
   ```

### Ejecución desde NetBeans
1. Abrir proyecto en NetBeans
2. Configurar main class (FirebasePushObject o FirebaseSaveObject)
3. Ejecutar proyecto (F6)

## 📝 Ejemplos de Uso

### Crear un Item
```java
Item item = new Item();
item.setId(1L);
item.setName("iPhone");
item.setPrice(999.99);

FirebasePushObject firebase = new FirebasePushObject();
firebase.saveUsingPush(item);
```

### Recuperar Datos
```java
FirebaseSaveObject firebase = new FirebaseSaveObject();
firebase.recover();
```

## 🔍 Características Técnicas

### Patrones de Diseño
- **Model-View-Controller (MVC)**: Separación de lógica de negocio y presentación
- **Singleton**: Para conexión a Firebase
- **Observer**: Para eventos de Firebase

### Manejo de Concurrencia
- Uso de `CountDownLatch` para operaciones asíncronas
- Manejo de threads daemon de Firebase

### Gestión de Errores
- Try-catch para excepciones de archivo
- Manejo de errores de conexión
- Logging de errores

## 🛠️ Desarrollo

### Estructura de Clases Principales

#### FirebasePushObject
- **Propósito**: Operaciones de inserción con push()
- **Métodos principales**:
  - `initFirebase()`: Inicialización de conexión
  - `saveUsingPush()`: Guardar con ID automático
  - `recover()`: Recuperar datos

#### FirebaseSaveObject
- **Propósito**: Operaciones CRUD básicas
- **Métodos principales**:
  - `save()`: Guardar objeto
  - `remove()`: Eliminar objeto
  - `recover()`: Recuperar datos

#### Item
- **Propósito**: Modelo de datos
- **Propiedades**: id, name, price
- **Patrón**: JavaBean con getters/setters

## 🔒 Seguridad

### Consideraciones de Seguridad
- Archivo de credenciales debe mantenerse seguro
- No incluir credenciales en control de versiones
- Configurar reglas de seguridad en Firebase Console
- Validar datos de entrada

### Configuración de Reglas Firebase
```json
{
  "rules": {
    ".read": "auth != null",
    ".write": "auth != null"
  }
}
```

## 🐛 Solución de Problemas

### Errores Comunes

1. **FileNotFoundException**
   - Verificar ruta del archivo de credenciales
   - Asegurar que el archivo existe

2. **RuntimeException**
   - Verificar configuración de Firebase
   - Comprobar conectividad a internet

3. **InterruptedException**
   - Problemas con CountDownLatch
   - Verificar manejo de threads

### Debugging
- Habilitar logging detallado
- Verificar conexión a Firebase
- Revisar reglas de seguridad

## 📚 Recursos Adicionales

### Documentación
- [Firebase Java SDK Documentation](https://firebase.google.com/docs/admin/setup)
- [Firebase Realtime Database Guide](https://firebase.google.com/docs/database)
- [Google API Client Library](https://developers.google.com/api-client-library/java)

### Herramientas
- [Firebase Console](https://console.firebase.google.com/)
- [NetBeans IDE](https://netbeans.apache.org/)

## 👥 Contribución

### Cómo Contribuir
1. Fork del proyecto
2. Crear rama para feature (`git checkout -b feature/nueva-funcionalidad`)
3. Commit de cambios (`git commit -am 'Agregar nueva funcionalidad'`)
4. Push a la rama (`git push origin feature/nueva-funcionalidad`)
5. Crear Pull Request

### Estándares de Código
- Seguir convenciones de Java
- Documentar métodos públicos
- Incluir manejo de errores
- Escribir pruebas unitarias

## 📄 Licencia

Este proyecto está bajo la licencia [MIT](LICENSE).

## 👨‍💻 Autor

**locon** - Universidad Nacional de Colombia

---

## 🔄 Historial de Versiones

- **v1.0.0**: Implementación inicial de operaciones CRUD básicas
- **v1.1.0**: Agregado soporte para operaciones push()
- **v1.2.0**: Mejoras en manejo de errores y logging

---

*Última actualización: Diciembre 2024* 