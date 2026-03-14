# Cronograma de Proyecto: Sistema Embebido Multinúcleo
**Proyecto:** Análisis Espectral 802.11 y Control Optoelectrónico Asincrónico  
**Periodo:** 10 de marzo - 31 de julio de 2026

---

##  Planificación por Fases

| Fase / Mes | Semanas | Actividad Principal | Entregable / Hito | Estado |
| :--- | :---: | :--- | :--- | :---: |
| **I. Arquitectura** (Marzo) | 1 - 3 | Selección de hardware (SDR/MCU) y diseño de la partición de tareas entre núcleos. | Documento de Arquitectura | 🟡 En curso |
| **II. Procesamiento** (Abril) | 4 - 7 | Implementación de algoritmos FFT y captura de paquetes 802.11. | Módulo de Análisis Espectral | ⚪ Pendiente |
| **III. Control** (Mayo) | 8 - 11 | Desarrollo del control optoelectrónico asincrónico y diseño de drivers. | Driver de Control Opto-aislado | ⚪ Pendiente |
| **IV. Integración** (Junio) | 12 - 15 | Sincronización Inter-Core (IPC), manejo de semáforos y memoria compartida. | Prototipo Alfa Integrado | ⚪ Pendiente |
| **V. Optimización** (Julio) | 16 - 19 | Pruebas de latencia, reducción de ruido RF/Óptico y depuración final. | Reporte de Rendimiento | ⚪ Pendiente |
| **VI. Cierre** (Julio) | 20 | Preparación de documentación técnica y presentación final. | **ENTREGA FINAL (31/07)** | ⚪ Pendiente |

---

##  Stack Tecnológico Sugerido
* **Lenguaje:** C / C++ (para bajo nivel y manejo de núcleos).
* **Hardware:** ESP32-S3 (Dual Core), STM32H7 (Dual Core) o FPGA con Soft-cores.
* **Herramientas:** Wireshark (para validar 802.11), Osciloscopio (para señales opto).

---
> **Nota técnica:** Dado el carácter asincrónico del control optoelectrónico, se recomienda usar colas de mensajes (Queues) para evitar condiciones de carrera entre los núcleos.
