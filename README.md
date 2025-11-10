# Sistema de Captura de Movimiento Inercial de Bajo Costo

![Estado del Proyecto](https://img.shields.io/badge/Estado-Fin%20del%20Ciclo%202-yellowgreen.svg)
![Tecnologías](https://img.shields.io/badge/Tecnolog%C3%ADa-Arduino%20%7C%20Blender%20%7C%20Python-blue.svg)
![Licencia](https://img.shields.io/badge/Licencia-MIT-lightgrey.svg)

Proyecto de código abierto para el diseño y construcción de un sistema de captura de movimiento corporal (MoCap) asequible, utilizando sensores inerciales MPU6050 y visualización en tiempo real con Blender. Este repositorio documenta el progreso hasta el final del Ciclo 2 de desarrollo.

---

## Sobre el Proyecto

Este repositorio contiene el firmware y software desarrollados para un prototipo de captura de movimiento. El objetivo es crear una alternativa de bajo costo a las soluciones comerciales, ideal para estudiantes, investigadores y desarrolladores independientes.

El desarrollo sigue un Modelo en Espiral, donde cada ciclo añade funcionalidades y robustez al sistema.

## Estado Actual: Fin del Ciclo 2

El prototipo es actualmente funcional y ha validado los siguientes hitos técnicos:

✅ **Fusión Sensorial en Hardware:** Se utiliza el Procesador de Movimiento Digital (DMP) del MPU6050, reduciendo la carga de la CPU del microcontrolador en más de un 90%.

✅ **Representación con Cuaterniones:** La orientación se maneja mediante cuaterniones, eliminando por completo el riesgo de Gimbal Lock.

✅ **Soporte Multi-Sensor:** El sistema maneja dos sensores MPU6050 simultáneamente en el mismo bus I²C mediante direccionamiento por pin AD0.

✅ **Cinemática Directa:** Se ha validado la lógica de cinemática directa en Blender, aplicando las rotaciones a una jerarquía de huesos padre-hijo para simular una articulación.

✅ **Firmware Robusto:** El firmware es estable, no se congela y envía datos a un ritmo constante y suave (~100 Hz).

## Estructura del Repositorio

*   `/firmware`: Código fuente para la placa Arduino Nano.
    *   `ciclo_2_dmp_dos_sensores/`: Firmware final y robusto para la lectura de dos sensores MPU6050 con DMP.
*   `/software`: Scripts de Python para ser ejecutados en Blender.
    *   `ciclo_2_dos_sensores_cuaternion/`: Script que recibe los cuaterniones, implementa la calibración de pose de referencia y aplica el movimiento a un esqueleto de dos huesos.
*   `/documentacion/imagenes`: Imágenes y diagramas utilizados en la documentación del proyecto.

## Cómo Usar el Prototipo del Ciclo 2

### 1. Hardware Requerido

*   1 x Arduino Nano
*   2 x Sensores MPU6050
*   Protoboard y cables de conexión

### 2. Software Requerido

*   **Arduino IDE:** Para subir el firmware.
*   **Blender:** (v3.0 o superior) Para la visualización.
*   **Librería `pyserial` para Python:** Blender la necesita. Para instalarla, abre CMD y ejecuta: `C:\Program Files\Blender Foundation\Blender 3.x\3.x\python\bin\python.exe -m pip install pyserial` (ajusta la ruta a tu versión de Blender).

### 3. Instrucciones de Puesta en Marcha

1.  **Montaje:** Conecta los dos sensores MPU6050 al Arduino Nano vía I²C (SDA a A4, SCL a A5). Conecta el pin AD0 de un sensor a GND (dirección 0x68) y el del otro a 3.3V (dirección 0x69).
2.  **Firmware:**
    *   Abre el archivo `firmware/ciclo_2_dmp_dos_sensores/ciclo_2_dmp_dos_sensores.ino` en el Arduino IDE.
    *   **IMPORTANTE:** Coloca ambos sensores sobre una superficie plana y estable.
    *   Sube el código al Arduino. No muevas los sensores hasta que la calibración termine.
3.  **Blender:**
    *   Abre Blender y prepara una escena con un `Armature` que contenga dos huesos: `UpperArm` (padre) y `LowerArm` (hijo).
    *   Abre el script `software/ciclo_2_dos_sensores_cuaternion/script_blender_ciclo2.py` en el Editor de Texto.
    *   Modifica la línea `SERIAL_PORT` para que coincida con el puerto COM de tu Arduino.
    *   Presiona "Run Script" (icono de play). La captura comenzará automáticamente y se calibrará con la primera lectura.
    *   Para detener, presiona `ESC` en la ventana 3D.

## Próximos Pasos (Ciclo 3)

*   Migración del hardware a un microcontrolador ESP32.
*   Implementación de la comunicación inalámbrica vía WiFi.
*   Diseño de una arquitectura de hardware y firmware escalable para 14+ sensores.

## Licencia

Este proyecto está distribuido bajo la Licencia MIT.
