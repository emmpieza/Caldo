# Caldo
API de Creación de Videos con Django y Docker
https://img.shields.io/badge/Licencia-Privada-blue.svg

Aplicación para generar videos automáticos con IA, incluyendo música, imágenes, voces en español y subtítulos, todo dentro de un contenedor Docker.

🚀 Características
🎵 Generador de música a partir de prompts de texto

🖼️ Creación de imágenes con modelos de IA

🔊 Síntesis de voz en español a partir de texto

🎬 Composición automática de videos con subtítulos

📦 Empaquetado en Docker para fácil despliegue

🔌 API REST con dos endpoints simples

📡 Endpoints de la API
1. Iniciar creación de video
Método: POST http://host.docker.internal:8000/start_video_creation/

Parámetros (JSON):

json
{  
    "texto": "El texto que aparecerá en el video y se convertirá en voz",  
    "music_prompt": "Ej: 'música épica para un viaje al espacio'"  
}  
Respuesta:

json
{  
    "task_id": "ID_UNICO",  
    "status": "processing"  
}  
2. Consultar estado del video
Método: GET http://host.docker.internal:8000/video_status/<task_id>/

Respuesta:

json
{  
    "status": "completed|processing|failed",  
    "video_url": "ruta/video_final_12345.mp4 (si está listo)"  
}  
🐳 Configuración con Docker
Requisitos previos
Docker instalado

Docker Compose instalado

🛠️ Instalación
Clona el repositorio

Construye la imagen Docker:

bash
docker-compose build  
Inicia el contenedor:

bash
docker-compose up -d  
La API estará disponible en: http://host.docker.internal:8000/

📂 Estructura de archivos
text
.  
├── Dockerfile                # Configuración de Docker  
├── docker-compose.yml        # Definición de servicios  
├── app/                      # Aplicación Django  
│   ├── modelos_ia/           # Modelos de IA  
│   ├── media/                # Archivos generados  
│   │   └── video_final_*.mp4 # Videos finales  
│   └── ...                   # Otros archivos Django  
└── requirements.txt          # Dependencias Python  
📜 Licencia
Este software es propietario y está bajo licencia de emmpieza.com.

Prohibido su uso, distribución o modificación sin autorización expresa.

© 2023 emmpieza.com - Todos los derechos reservados.

💡 Ejemplo de Uso
Solicitar creación:

bash
curl -X POST http://localhost:8000/start_video_creation/ \  
     -H "Content-Type: application/json" \  
     -d '{"texto":"Un tutorial sobre Django","music_prompt":"música relajante para programar"}'  
Verificar progreso:

bash
curl http://localhost:8000/video_status/ID_RECIBIDO/  
Descargar video: (Cuando status = "completed")

bash
wget http://localhost:8000/media/video_final_12345.mp4  
