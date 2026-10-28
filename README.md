# Controles ISO/IEC 27001:2022 para la confidencialidad en la administración de Oracle

Universidad Nacional de Costa Rica, Escuela de Informática.
Curso: Administración de Bases de Datos, II Ciclo 2026. Profesor: Johnny Villalobos Murillo.
Estudiante: Jostin Jiménez Alfaro

## Qué contiene

- `scripts/scripts_utilizados.txt`: los tres scripts SQL ejecutados (verificación de la línea base, mejoras de la fase 1 y datos de prueba con enmascaramiento de la fase 2A) y la prueba manual como usuario sin privilegios.
- `evidencia/`: salidas reales de las ejecuciones en Oracle XE 21c.
  - `evidencia_linea_base.txt`: línea base medida con el script de verificación.
  - `evidencia_fase1_despues.txt`: resultado de la fase 1 (perfil de contraseñas y revocación a PUBLIC).
- El informe en PDF, con riesgos, tareas del DBA, mapeo de controles, matriz de evaluación, batería de pruebas, marco teórico y tabla de uso de IA, se entrega junto con este repositorio.

## Entorno

Oracle Database 21c Express Edition (21.3.0.0.0), PDB `XEPDB1`, SQL*Plus.

## Cómo ejecutar los scripts

1. Conectarse como SYS: `sqlplus / as sysdba`.
2. Cambiar a la PDB: `ALTER SESSION SET CONTAINER = XEPDB1;`
3. Guardar cada bloque de `scripts_utilizados.txt` en su propio archivo `.sql` y ejecutarlo con `@archivo.sql`, en este orden: verificación, fase 1 y fase 2A.
4. La fase 2A recibe las claves de los usuarios de prueba como argumentos (`@mejora_fase2a_datos_prueba.sql <clave_RRHH> <clave_APP_CONSULTA>`); no se guardan en ningún archivo.

## Alcance y limitaciones

- Ejecutado: línea base, fase 1 (perfil de contraseñas, revocación de `EXECUTE` a `PUBLIC` sobre `UTL_FILE`, `UTL_HTTP`, `UTL_SMTP` y `UTL_TCP`) y fase 2A (clasificación de columnas y enmascaramiento con Data Redaction sobre una tabla de prueba).
- Solo diseño, no ejecutado: TDE, backup cifrado y auditoría sobre datos sensibles.
- La línea base se midió en una primera máquina; la fase 1 se repitió y la fase 2A se ejecutó en una segunda máquina (ver el Anexo A del informe).

## Uso de IA

Declarado en la tabla de uso de IA del informe, con su declaración jurada.

## Aviso

Los datos de la tabla `RRHH.EMPLEADOS` son ficticios. Este repositorio no contiene contraseñas.
