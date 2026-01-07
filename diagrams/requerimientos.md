# Requerimientos - Implementacion LangGraph con datos en SAP

## Resumen ejecutivo
Se propone implementar un sistema de agentes con LangGraph para refraccionar atenciones del Contact Center hacia canales digitales. La empresa posee sus datos en SAP, por lo que la integracion debe realizarse mediante interfaces oficiales (OData/RFC/IDoc/CPI). El resto de la solucion se implementa internamente: orquestacion, agentes especializados, evaluacion externa, canales, notificaciones y operacion.

## Requerimientos funcionales
### Canales
- Contact Center/IVR (migracion gradual).
- WhatsApp Business (fase inicial).
- Chatbot embebido en Portal.

### Orquestador
- Identificacion y autenticacion (RUT y serie de cedula; empresas con usuario y contrasena).
- Clasificacion de rol (trabajador vs empresa).
- Deteccion de intencion y ruteo.
- Derivacion al agente especializado.
- Operacion 24x7.

### Agentes especializados
- Pago y Subsidio: pagos de licencias, fechas de pago, historial de subsidios.
- Siniestro y Documentacion: ingreso/seguimiento de denuncias, documentos faltantes, extensiones.
- Soporte Web y Acceso: reseteo de claves, acceso a sucursal virtual y cursos.
- Capacitacion y Diplomas: inscripcion, cambios de datos, envio de diplomas/certificados.
- Adhesion y Asesoria: numero de adhesion, renuncia y nueva adhesion.
- Movilizacion: traslados, confirmacion de locomocion, coordinacion de transporte.

### Evaluacion externa
- Metricas: calidad, completitud, exactitud, tono.
- Umbral configurable.
- Reintento automatico con el mismo agente si no cumple.

### Notificacion y escalamiento
- Notificaciones por SMS/Email/Push cuando aplique.
- Escalamiento humano para excepciones o casos complejos.

## Requerimientos no funcionales
- Seguridad y cumplimiento: cifrado, auditoria, control de accesos.
- Trazabilidad completa por conversacion y transaccion.
- Disponibilidad 24x7 y tolerancia a fallas.

## Flujo general
1) Usuario entra por canal (IVR, WhatsApp, Portal).
2) Orquestador autentica, clasifica rol e intencion.
3) Ruteo al agente especializado.
4) Agente genera respuesta con datos SAP.
5) Evaluador externo valida metricas.
   - Si cumple: continua.
   - Si no cumple: reintenta el mismo agente.
6) Notificador envia SMS/Email/Push si aplica.
7) Respuesta por canal original.
8) Escalamiento humano si corresponde.

## Integracion con SAP (obligatoria)
### Interfaces recomendadas
- OData/REST via SAP Gateway (S/4HANA o ECC con Gateway).
- RFC/BAPI (SAP NetWeaver).
- IDoc/ALE para procesos asincronos.
- SAP BTP Integration Suite (CPI) o PI/PO si existe en el cliente.

### Opciones de conexion (si aun no se define el canal tecnico)
1) API intermedia del cliente.
2) API intermedia propia (Data Access Service).
3) Conexion directa al motor (ultima opcion).
4) Replica read-only.
5) CDC/streaming.
6) Batch ETL/ELT.
7) Archivos seguros (SFTP/S3/Blob).
8) Data virtualization.
9) Clean room.

### Informacion minima requerida del cliente
- Sistema SAP y version (ECC o S/4HANA).
- Interfaces disponibles (OData, RFC/BAPI, IDoc, CPI/PI/PO).
- Diccionario de datos o servicios expuestos.
- Metodo de acceso (VPN/API/private link).
- Volumen y criticidad de datos.
- Politicas de seguridad, auditoria y retencion.

## Componentes a implementar (ademas de LangGraph)
### Orquestacion y agentes
- Definicion de flujos, prompts, herramientas y manejo de estado.
- Validaciones de entrada/salida con reglas de negocio.

### Canales (inicio en WhatsApp)
- Integracion con WhatsApp Business API.
- Webhook receptor, validacion de firmas y rate limits.
- Mapeo de mensajes a sesiones LangGraph y persistencia.

### Integraciones backend
- Servicios para pagos, siniestros, documentos, LMS, credenciales, transporte.
- Normalizacion de identidad (RUT/empresa) y reglas de negocio.
- Manejo de inconsistencias entre lo informado y SAP.

### Observabilidad
- Logs, trazas, metricas y dashboards.
- Alertas operativas y de calidad.

### Infra y despliegue
- Contenedores Docker y CI/CD.
- Entornos dev/qa/prod y control de cambios.
- API gateway y proteccion perimetral.

## Fase 1 recomendada: WhatsApp
- Habilitar numero y plantilla de WhatsApp Business.
- Implementar webhook + validacion + almacenamiento de contexto.
- Conectar Orquestador -> Agentes -> Evaluador -> Respuesta.
- Pruebas end-to-end con casos reales.
