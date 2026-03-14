# Sistema Embebido Multi-Núcleo para Análisis Espectral 802.11 y Control Optoelectrónico Asíncrono

##  Descripción del Proyecto
Este repositorio contiene el código fuente y la documentación de un firmware desarrollado en C++ nativo para la arquitectura de doble núcleo **ESP32-S3**. El sistema está diseñado para operar de forma 100% autónoma, prescindiendo de servidores web o conexiones a dispositivos móviles, y orquesta la ejecución concurrente de una interfaz humano-máquina (HMI) avanzada y un analizador de protocolos de red inalámbricos.

##  Objetivo General
Desarrollar un firmware en C++ nativo que orqueste la ejecución concurrente de un motor gráfico táctil y un analizador de protocolos de red inalámbricos. El sistema se despliega sobre una arquitectura de doble núcleo (ESP32-S3), utilizando un Sistema Operativo de Tiempo Real (FreeRTOS) para aislar las cargas de procesamiento de radiofrecuencia de la interfaz humano-máquina (HMI).

##  Objetivos Específicos

A partir de las competencias técnicas y la arquitectura del sistema, los objetivos específicos del proyecto se dividen en los siguientes puntos clave:

### 1. Gestión Avanzada de Memoria y Punteros
* Implementar asignación dinámica de memoria en la **PSRAM externa** para alojar los *buffers* de renderizado del motor gráfico (LVGL) y los arreglos masivos de estructuras de datos (direcciones MAC y tramas 802.11).
* Mantener la **SRAM interna** libre y optimizada para las operaciones críticas del procesador.

### 2. Concurrencia Estricta mediante RTOS
* Establecer un aislamiento asimétrico de tareas garantizando la concurrencia a través de **FreeRTOS**.
* Implementar Comunicación Inter-Procesos (IPC) utilizando colas de mensajes (`xQueue`) y semáforos.
* Garantizar que la inyección de paquetes de red y el refresco de pantalla operen simultáneamente sin generar condiciones de carrera (*race conditions*) ni provocar interbloqueos en el *Watchdog Timer*.

### 3. Manipulación de Hardware a Bajo Nivel
* Abstraer el hardware físico mediante el uso de Acceso Directo a Memoria (**DMA**) y el periférico **RMT** del procesador.
* Generar señales de temporización estricta para la matriz optoelectrónica externa sin consumir ciclos de reloj de la CPU.

### 4. Implementación de Arquitectura de Ejecución Aislada (Dual-Core)
El sistema divide sus operaciones en dos bloques de ejecución completamente aislados:

**Core 0 (Módulo de Radiofrecuencia):**
* Configurar el silicio de la antena en modo promiscuo.
* Capturar y disecar *Probe Requests* en crudo mediante aritmética de punteros.
* Ensamblar e inyectar tramas de desautenticación en el espectro 802.11.

**Core 1 (Motor HMI y Actuadores):**
* Gestionar el bucle de eventos gráficos manteniendo una tasa de refresco constante de 60 FPS.
* Procesar las interrupciones de hardware generadas por el panel capacitivo a través del bus I2C.
* Traducir los estados lógicos a señales de potencia direccionables para el control optoelectrónico (control LED).
