# Arqui-Software---Proyecto-1
# Proyecto de Diseño de Software – Corte Uno

## 🧠 Presentación del Problema

Muchas personas que entrenan en el gimnasio no llevan un registro organizado de sus rutinas, repeticiones, peso y progreso. Esto genera pérdida de motivación, estancamiento y dificultad para medir resultados.
El proyecto busca resolver este problema mediante una aplicación móvil que permita registrar entrenamientos de forma diaria, ofrecer rutinas predeterminadas con videos explicativos y mostrar el progreso del usuario.
Los principales beneficiados son:

- Usuarios principiantes: obtienen orientación con rutinas básicas y videos.

- Usuarios intermedios y avanzados: pueden llevar un seguimiento detallado de su progreso.

- Entrenadores personales: tendrán una herramienta digital para recomendar rutinas y evaluar avances.

## 🎨 Creatividad en la Presentación

(https://www.canva.com/design/DAGwe2s2f3g/X2C_D6cZoTVPqrhfewGJmA/edit?utm_content=DAGwe2s2f3g&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton)

## 🧱 Fundamentos de Ingeniería de Software

Los atributos de calidad priorizados son:

- Usabilidad: interfaz intuitiva y clara para registrar entrenamientos en pocos clics.

- Escalabilidad: posibilidad de agregar nuevas rutinas, métricas o integración con dispositivos wearables.

- Mantenibilidad: código estructurado en capas con aplicación de principios SOLID para facilitar cambios futuros.

- Portabilidad: aplicación pensada para Android inicialmente, pero con arquitectura adaptable a otros entornos móviles.

## 🧩 Diseño de Software

**Principios SOLID aplicados**

1. **Principio de Responsabilidad Única (SRP)** Cada clase tiene un único propósito. Las Activities se encargan solo de la interfaz de usuario, los Managers gestionan la lógica de negocio (por ejemplo, registrar progresos o manejar notificaciones), los Repositories se dedican exclusivamente al acceso a datos, y AppNavigator controla la navegación. Esto asegura claridad y evita sobrecarga en las clases.

2. **Principio Abierto/Cerrado (OCP)** La aplicación permite extender funcionalidades sin necesidad de modificar código existente. Por ejemplo, al añadir una nueva rutina o pantalla, se crea un nuevo método en AppNavigator o una nueva clase que implemente la lógica, sin alterar las clases ya probadas. De esta forma, se minimiza el riesgo de errores y se facilita la escalabilidad.

3. **Principio de Inversión de Dependencias (DIP)** Las clases de alto nivel (Activities y Managers) dependen de abstracciones (interfaces) y no de implementaciones concretas. Un ejemplo es la interfaz ProgressRepository, que abstrae la lógica de almacenamiento de datos. Esto permite cambiar Firebase por otra base de datos, como SQLite o Room, sin afectar el resto de la aplicación.

**Patrones de diseño utilizados**

1. **Patrón Creacional: Singleton** Implementé el patrón Singleton para la gestión de datos estáticos y repositorios. En Kotlin, este patrón se consigue de forma nativa mediante la palabra clave _object_, la cual utilicé para clases como _DatosQuizzes_ y _ContentData_.

**Justificación Técnica:** El uso de Singleton para estas clases es óptimo, ya que los datos de contenido (preguntas, títulos de videos, etc.) son constantes a lo largo del ciclo de vida de la aplicación. Este patrón asegura que exista una única instancia de estos datos en memoria, evitando la sobrecarga innecesaria que supondría crear nuevos objetos repetidamente. Esto no solo optimiza el uso de recursos, sino que también proporciona un punto de acceso global y consistente a esta información desde cualquier componente de la aplicación, como las Activities _Entrenate_ o _Favoritos_.

2. **Patrón de Comportamiento: Strategy** Para la capa de acceso a datos, implementé el patrón Strategy. Este patrón se materializa a través de la interfaz _ProgressRepository_ y su implementación concreta, _FirebaseProgressRepository_.

**Justificación Técnica:** La interfaz _ProgressRepository_ define un "contrato" o una estrategia abstracta para las operaciones de persistencia de datos (ej. _getWeeklyProgress_, _resetAllProgress_). Los módulos de alto nivel, como el _ProgressManager_, dependen de esta abstracción y no de la implementación específica de Firebase.

Esta estructura me permite que el algoritmo de persistencia sea intercambiable. Si en el futuro se requiriera un modo offline, podría crear una nueva clase _SQLiteProgressRepository_ que implemente la misma interfaz. De este modo, sería posible cambiar la estrategia de guardado de datos (por ejemplo, entre online y offline) sin necesidad de modificar el _ProgressManager_ o las Activities, que son los clientes de esta estrategia. Esto desacopla la lógica de negocio de los detalles de la implementación de datos, aumentando la flexibilidad y mantenibilidad del sistema.

### UML
![Image_Alt](https://github.com/lopezito52/Arqui-Software---Proyecto-1/blob/c3ec64c0d3fc8c06da9d3f630420874fa2fb6d1c/uml.jpeg)

**Justificación**

La elección de estos principios y patrones responde a la necesidad de construir una aplicación mantenible, escalable y adaptable.

- **SOLID** garantiza que las clases estén bien organizadas, con responsabilidades claras, y que la lógica de negocio no dependa de detalles técnicos como la base de datos.
- **Factory Method** permite ofrecer flexibilidad al generar rutinas dinámicas según el perfil del usuario.
- **Observer** asegura comunicación fluida y reactiva, fundamental en una aplicación que busca motivar al usuario en tiempo real.

## 💻 Implementación

La estructura del código seguirá un modelo en capas:

- Capa de presentación: interfaz gráfica para que el usuario interactúe.

- Capa de lógica: contiene la gestión de rutinas, registros y notificaciones.

- Capa de datos: conexión con la base de datos (local o en la nube).

## 🔍 Análisis Técnico

El sistema se diseñó priorizando la alta cohesión y el bajo acoplamiento mediante la aplicación de principios SOLID y patrones de diseño adecuados. Cada clase cumple un rol específico (gestión de usuarios, rutinas, registros, notificaciones), lo que facilita la mantenibilidad y reduce la complejidad. El uso de interfaces y el patrón Observer permiten desacoplar la lógica central de los servicios externos, garantizando flexibilidad y escalabilidad en futuras extensiones, como la integración con dispositivos de monitoreo o nuevas rutinas de entrenamiento. Con esta arquitectura, el sistema cumple con los atributos de calidad definidos: es usable, mantenible, escalable y adaptable a diferentes contextos de uso.

## 👥 Créditos y Roles

- Juan Pablo Parrado Morales - Desarrolador App e Implementación de patrones de diseño.
- Gabriela sofia Fuentes Cordoba - Diseño UML y lógica de negocio.
- Samuel Esteban Lopez Huertas - Creatividad y video de presentación.
