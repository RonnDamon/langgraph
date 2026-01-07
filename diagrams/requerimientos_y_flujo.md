# Requerimientos del proyecto 

## Alcance y canales
- Canales soportados: Contact Center/IVR (migracion), WhatsApp Business, Chatbot embebido en Portal.
- Integracion de canales mediante APIs y reutilizacion de mecanismos existentes del Portal.
- Operacion 24x7.

## Arquitectura de agentes
- Agente Orquestador Central (Gatekeeper/IVR inteligente).
- Agentes Especializados modulares por dominio:
  - Pago y Subsidio.
  - Siniestro y Documentacion.
  - Soporte Web y Acceso.
  - Capacitacion y Diplomas.
  - Adhesion y Asesoria.
  - Movilizacion.
- Agente Evaluador Externo para control de calidad por metricas. Si un agente no cumple con las metricas de respuesta requerida, vuelve a solicitar una respuesta.
- Agente Notificador para salida multicanal.
- Escalamiento humano para casos complejos o excepciones.

## Funciones del Orquestador
- Identificacion y autenticacion (RUT y serie de cedula; para empresas RUT, usuario y contrasena).
- Clasificacion de rol (trabajador vs empresa).
- Deteccion de intencion y ruteo al agente adecuado.
- Derivacion y control de flujo conversacional.

## Funciones por agente especializado
- Pago y Subsidio: consultas de pagos de licencias, confirmacion de fechas (quincena/fin de mes), manejo de "no hay pagos".
- Siniestro y Documentacion: ingreso/seguimiento de denuncias, verificacion de documentos faltantes, extensiones de licencia.
- Soporte Web y Acceso: reseteo de claves, credenciales invalidas, acceso a sucursal virtual y cursos.
- Capacitacion y Diplomas: inscripcion a cursos, cambios de datos, envio de diplomas/certificados.
- Adhesion y Asesoria: entrega numero de adhesion, pasos de renuncia y nueva adhesion.
- Movilizacion: consultas de traslado, confirmacion de locomocion, coordinacion de transporte.

## Evaluacion de respuestas
- Metricas minimas: calidad, completitud, exactitud, tono.
- Umbral de aprobacion configurable.
- Si no cumple metricas: reintentar con el mismo agente especializado.
- Si cumple metricas: avanzar a notificacion y respuesta al usuario.

## Integraciones backend
- APIs para pagos/licencias, siniestros, documentos, credenciales, LMS/cursos, transporte.
- Validaciones cruzadas cuando existan inconsistencias entre lo informado y el sistema.
- Envio de enlaces por correo/SMS cuando falten documentos.

## Notificacion y respuesta
- Respuesta por el canal original.
- Notificaciones por SMS/Email/Push cuando aplique.

## Seguridad y cumplimiento
- Proteccion de datos personales (RUT, credenciales).
- Control de acceso, trazabilidad y auditoria.

## KPIs esperados
- Tasa de resolucion automatica.
- Reduccion de llamadas y tiempos de espera.
- Tasa de reintento por calidad.
- Escalamiento humano y causas.
- Satisfaccion de usuario.

