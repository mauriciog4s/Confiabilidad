Documentación de Cambios: Branch-Dev vs. main
Resumen General
La versión actual en la rama main introduce varias mejoras significativas en comparación con el código original de Branch-Dev. Los cambios se centran en cuatro áreas principales:

Trazabilidad del Usuario: Se corrige un error que impedía saber qué usuario realizaba una carga masiva.
Calidad de Datos: Se añaden validaciones estrictas al campo "Identificación".
Reglas de Negocio: Se implementan nuevas reglas para la selección de servicios.
Experiencia de Usuario: Se permite la actualización de datos en tiempo real sin recargar la página.
Cambios Detallados por Funcionalidad
A continuación se desglosa cada nueva funcionalidad:

1. Trazabilidad de Usuario en Carga Masiva (Bulk Upload)

Funcionalidad Anterior (Branch-Dev):

Cuando se creaba una solicitud desde el formulario, el email del usuario quedaba guardado.
Sin embargo, cuando un usuario subía un archivo masivo (.csv), su email no se almacenaba, dejando un registro incompleto.
Funcionalidad Actual (main):

Se modificó el backend para que, durante el procesamiento de la carga masiva, también se capture y guarde el email del usuario que realiza la operación.
Diferencias y Mejoras:

Mejora: Se garantiza la trazabilidad y auditoría completa de todas las solicitudes, sin importar si fueron creadas individualmente o en masa.
Diferencia: El comportamiento ahora es consistente en ambos métodos de creación de solicitudes.
2. Validación del Campo "Identificación"

Funcionalidad Anterior (Branch-Dev):

El campo "Identificación" en el formulario de nueva solicitud era un campo de texto libre, sin ninguna validación de formato o longitud.
Funcionalidad Actual (main):

Se han añadido validaciones estrictas en el formulario (frontend):
Formato: Solo se permiten letras y números (alfanumérico).
Caracteres no permitidos: No se admiten espacios, guiones, puntos ni ningún otro carácter especial.
Longitud: El valor debe tener entre 5 y 15 caracteres.
Se muestra un texto de ayuda debajo del campo para guiar al usuario.
Diferencias y Mejoras:

Mejora: Se asegura una mayor calidad e integridad de los datos desde el momento de su ingreso.
Diferencia: Se previene el ingreso de datos incorrectos y se estandariza el formato de las identificaciones, lo que facilita futuras búsquedas y reportes.
3. Nuevas Reglas de Negocio para Selección de Servicios

Funcionalidad Anterior (Branch-Dev):

El usuario podía crear una solicitud sin seleccionar ningún servicio.
No existían reglas que impidieran combinar ciertos servicios.
Funcionalidad Actual (main):

Validación de Servicio Mínimo: Ahora es obligatorio seleccionar al menos un servicio para poder enviar el formulario. Si no se selecciona ninguno, el sistema muestra un error y no permite crear la solicitud. Esta validación se aplica tanto en el frontend como en el backend para máxima seguridad.
Regla de Exclusión: Se implementó una nueva regla:
Si el servicio "Visita Domiciliaria" está seleccionado, el servicio "Referencia Personal" se deshabilita y no puede ser elegido.
Si el usuario intenta seleccionar "Referencia Personal" mientras "Visita Domiciliaria" ya está activo, se muestra una advertencia.
Diferencias y Mejoras:

Mejora: Se evitan solicitudes "vacías" que no tienen ningún servicio que procesar.
Diferencia: Se aplican lógicas de negocio específicas que previenen combinaciones de servicios incompatibles, reduciendo errores operativos.
4. Actualización de Clientes Asignados en Tiempo Real

Funcionalidad Anterior (Branch-Dev):

Si un administrador asignaba un nuevo cliente a un usuario, este último debía recargar toda la página o cerrar y abrir sesión para poder ver el nuevo cliente en su lista.
Funcionalidad Actual (main):

En la pantalla de Configuración, se ha añadido un nuevo botón llamado "Actualizar" en la sección "Clientes Asignados".
Al hacer clic en este botón, el sistema refresca únicamente la lista de clientes del usuario, sin necesidad de recargar toda la aplicación.
Diferencias y Mejoras:

Mejora: La experiencia de usuario (UX) es mucho más fluida y eficiente.
Diferencia: Se elimina un paso manual y molesto, permitiendo a los usuarios ver sus cambios de asignación de forma instantánea.
Archivos Modificados
Code.gs: Contiene los cambios del backend (trazabilidad en carga masiva, validación de servicio mínimo y el nuevo endpoint para refrescar clientes).
Index.html: Contiene todos los cambios del frontend (nuevas validaciones en el formulario, la regla de exclusión de servicios y el nuevo botón de actualizar clientes).
