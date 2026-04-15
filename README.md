# 📂 Laboratorio: Recuperación Forense de Datos (CLI & Forensics)

Este proyecto documenta el procedimiento técnico para recuperar información crítica tras un fallo lógico o error humano (formateo/borrado de partición) utilizando herramientas de línea de comandos y escaneo de firmas.

## 🎯 Escenario de Prueba
1. **Unidad Objetivo:** Disco secundario de 5GB inicializado en GPT.
2. **Acción del "Usuario":** Borrado accidental de archivos y posterior ejecución del comando `clean` en Diskpart (destrucción de la tabla de particiones).
3. **Estado del Disco:** "No inicializado" / Espacio no asignado.

---

## 🛠️ Fase 1: Preparación y Fallo Simulado
Para garantizar una práctica real, se utilizó la herramienta `diskpart` para gestionar el almacenamiento desde la terminal.

### Configuración del Disco:
```cmd
diskpart
select disk 1
clean
convert gpt
create partition primary
format fs=ntfs quick label="EVICENCIA"
assign letter=E
```
Se procedió a cargar archivos de prueba (JPG, TXT, PDF) en la unidad E: antes de ejecutar un segundo comando clean para simular la pérdida total de acceso.
## Fase 2:Analisis y Recuperacion con PhotoRec
Al desaparecer la unidad lógica, se utilizó PhotoRec para realizar una recuperación basada en firmas (Signature-based recovery).

## **Procedimiento Tecnico:**
1. **Selección del Origen:** Identificación del disco físico de 5GB (Harddisk 1).
2.**Tipo de Escaneo:** Se seleccionó `[Whole Disk]` para buscar fragmentos de archivos en sectores que el sistema operativo ya no reconoce como particionados.
3.**Filtro de Archivos:** Configuración de `File Opt` para buscar específicamente cabeceras:
<p align="center">
<img src="./screenshots/photorec_scan.png" height="350" alt="Escaneo de PhotoRec en progreso">
</p>
##Conceptos tecnicos Aprendidos:
