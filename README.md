# Proyecto-Final_Grupo4
## 1. Descripción del sistema
[cite_start]Este sistema es una solución de visión artificial ligera diseñada para la inspección automatizada de **Maíz Peto**[cite: 108, 195]. [cite_start]Utiliza el análisis estadístico en el espacio de color LAB para identificar impurezas o anomalías en tiempo real sobre una banda transportadora[cite: 122, 153, 195]. [cite_start]Al detectar un elemento defectuoso, el sistema detiene automáticamente la banda y acciona un pistón para descartar el producto[cite: 123, 124, 210].

## 2. Arquitectura
[cite_start]El sistema se compone de dos módulos principales coordinados mediante una máquina de estados no bloqueante[cite: 133, 134]:
* [cite_start]**Módulo de Visión (IA):** Captura video mediante `Picamera2`, procesa los frames con OpenCV y calcula la distancia de Mahalanobis para evaluar píxeles anómalos respecto a un modelo calibrado[cite: 108, 155, 175].
* [cite_start]**Módulo de Actuación (Hardware):** Controla dos motores DC mediante Puentes H (la banda transportadora y el pistón de rechazo) utilizando la librería `gpiozero` con soporte PWM para regular la velocidad[cite: 108, 122, 123].

### Flujo de Trabajo ante una Alerta
1. [cite_start]Alerta detectada por porcentaje de anomalías o área mínima[cite: 183].
2. [cite_start]Conteo del tiempo de retardo para que el producto llegue al punto de descarte[cite: 123, 133, 209].
3. [cite_start]Detención de la banda transportadora[cite: 123, 134].
4. [cite_start]Extensión del motor del pistón[cite: 124, 134].
5. [cite_start]Pausa breve de impacto y posterior retracción del pistón[cite: 124, 135, 136].
6. [cite_start]Rearme del sistema y reanudación del movimiento de la banda[cite: 124, 138, 139].

## 3. Requisitos e instalación

### Requisitos de Hardware
* [cite_start]Raspberry Pi (compatible con el manejo de comandos `lgpio`)[cite: 110].
* [cite_start]Módulo de Cámara Raspberry Pi (compatible con `Picamera2`).
* [cite_start]Dos controladores de motor Puente H[cite: 108, 122].
* [cite_start]Motor DC para la banda y Actuador/Motor DC para el pistón[cite: 122, 123].

### Requisitos de Software e Instalación
[cite_start]Para preparar el entorno en tu Raspberry Pi OS, ejecuta los siguientes comandos en la terminal[cite: 110, 111]:

```bash
# Actualizar el sistema e instalar dependencias de GPIO y gráficos
sudo apt update
sudo apt install python3-gpiozero python3-lgpio python3-opencv -y
