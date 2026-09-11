# 🛒 Sistema de Gestión de Productos Cloud

Sistema web de gestión de inventario y productos para un supermercado, desarrollado como proyecto para la asignatura **Computación en la Nube** del **Instituto Profesional Santo Tomás**.

## 🚀 Funcionalidades

- **CRUD Completo:** Creación, lectura, actualización y eliminación de productos.
- **Tiempo Real:** Los datos se sincronizan instantáneamente gracias a los WebSockets de Firebase.
- **Gestión de Stock:** Control estricto de unidades y precios.
- **Filtros de Búsqueda:** Búsqueda dinámica por nombre, categoría o proveedor.
- **Validaciones:** Prevención de envío de formularios incompletos o con datos corruptos.

## ☁️ Arquitectura y Explicación Cloud

Este proyecto marca la transición de un almacenamiento tradicional y local a una arquitectura basada en la Nube:

### Diferencia con `localStorage`
En versiones o proyectos anteriores se solía utilizar `localStorage`, lo que significaba que los datos vivían **únicamente en el navegador del usuario**. Si el usuario cambiaba de dispositivo o limpiaba su caché, los datos se perdían. Al migrar a la nube (Cloud Computing), la información está centralizada en un servidor externo, permitiendo que **múltiples dispositivos accedan y modifiquen la misma información en tiempo real**, garantizando persistencia y disponibilidad.

### Componentes Cloud Utilizados
1. **Hosting (GitHub Pages):** Se encarga de servir los archivos estáticos (HTML, CSS y JS). Aprovecha la escalabilidad automática de la infraestructura de GitHub para soportar altos volúmenes de tráfico sin requerir la configuración de servidores dedicados (arquitectura Serverless para el frontend).
2. **Base de Datos (Firebase Firestore):** Base de datos NoSQL alojada en la nube de Google. Provee un servicio de Base de Datos como Servicio (DBaaS). Gestiona automáticamente la persistencia, escalabilidad y sincronización en tiempo real con los clientes conectados.

### Flujo de la Aplicación
1. El usuario accede a la URL pública. El navegador descarga el frontend desde GitHub Pages.
2. Al ingresar al sistema, el código JavaScript inicializa el SDK de Firebase y establece una conexión segura con Firestore.
3. Se crea una suscripción en tiempo real (`onSnapshot`) a la colección de `productos`. 
4. Cualquier cambio (crear, editar, eliminar) se envía directamente a los servidores de Firebase, los cuales procesan la operación y notifican automáticamente a todos los clientes conectados para que refresquen su interfaz.

## 🛠️ Instalación y Uso (Desarrollo Local)

Dado que es una aplicación Serverless puramente frontend, no requiere instalación de dependencias de servidor.

1. Clona este repositorio:
   ```bash
   git clone https://github.com/ManzanoDeAbril/ManzanoDeAbril.github.io.git
   ```
2. Abre el archivo `index.html` en tu navegador web de preferencia, o utiliza una extensión como Live Server en VSCode.
3. Para ver el proyecto en producción, visita el enlace público generado por GitHub Pages.

## ⚠️ Notas de Seguridad

- **Reglas de Firestore:** Actualmente, las reglas de Firestore están en modo de pruebas (`allow read, write: if true;`) para facilitar la corrección y evaluación académica. En un entorno de producción real, esto se restringiría implementando Firebase Authentication.
