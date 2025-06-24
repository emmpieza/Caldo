# Caldo
# API de Creación de Videos con Django y Docker

![Licencia](https://img.shields.io/badge/Licencia-Privada-blue.svg)
![Python](https://img.shields.io/badge/Python-3.8+-green.svg)
![Django](https://img.shields.io/badge/Django-4.0+-blue.svg)
![Docker](https://img.shields.io/badge/Docker-Ready-blue.svg)


https://github.com/emmpieza/Caldo/blob/main/video_final_1750719510.mp4

Aplicación para **generar videos automáticos** con IA, incluyendo música, imágenes, voces en español y subtítulos, todo dentro de un contenedor Docker.

## 🚀 Características

- 🎵 **Generador de música** a partir de prompts de texto
- 🖼️ **Creación de imágenes** con modelos de IA
- 🔊 **Síntesis de voz** en español a partir de texto
- 🎬 **Composición automática de videos** con subtítulos
- 📦 **Empaquetado en Docker** para fácil despliegue
- 🔌 **API REST** con dos endpoints simples

## 📡 Endpoints de la API

### 1. Iniciar creación de video

**Método**: `POST http://localhost:8000/start_video_creation/`

**Parámetros (JSON)**:
```json
{  
    "texto": "El texto que aparecerá en el video y se convertirá en voz",  
    "music_prompt": "Ej: 'música épica para un viaje al espacio'"  
}
```

**Respuesta**:
```json
{  
    "task_id": "ID_UNICO",  
    "status": "processing"  
}
```

### 2. Consultar estado del video

**Método**: `GET http://localhost:8000/video_status/<task_id>/`

**Respuesta**:
```json
{  
    "status": "completed|processing|failed",  
    "video_url": "ruta/video_final_12345.mp4 (si está listo)"  
}
```

## 🐳 Configuración con Docker

### Requisitos previos

- Docker instalado
- Docker Compose instalado

### 🛠️ Instalación

1. **Clona el repositorio**
   ```bash
   git clone [https://github.com/emmpieza/Caldo.git]
   cd video-api
   ```

2. **Construye la imagen Docker**:
   ```bash
   docker-compose build
   ```

3. **Inicia el contenedor**:
   ```bash
   docker-compose up -d
   ```

4. **Verifica que esté funcionando**:
   ```bash
   curl http://localhost:8000/
   ```

La API estará disponible en: `http://localhost:8000/`

## 📂 Estructura de archivos

```
.
├── Dockerfile                # Configuración de Docker
├── docker-compose.yml        # Definición de servicios
├── requirements.txt          # Dependencias Python
├── README.md                 # Este archivo
├── app/                      # Aplicación Django
│   ├── settings.py           # Configuración Django
│   ├── urls.py               # URLs de la API
│   ├── views.py              # Lógica de endpoints
│   ├── modelos_ia/           # Modelos de IA
│   ├── media/                # Archivos generados
│   │   └── video_final_*.mp4 # Videos finales
│   └── ...                   # Otros archivos Django
```

## 💡 Ejemplo de Uso

### 1. Solicitar creación de video

```bash
curl -X POST http://localhost:8000/start_video_creation/ \
     -H "Content-Type: application/json" \
     -d '{"texto":"Un tutorial sobre Django","music_prompt":"música relajante para programar"}'
```

**Respuesta esperada**:
```json
{
    "task_id": "abc123def456",
    "status": "processing"
}
```

### 2. Verificar progreso

```bash
curl http://localhost:8000/video_status/abc123def456/
```

**Respuestas posibles**:
```json
// Procesando
{
    "status": "processing"
}

// Completado
{
    "status": "completed",
    "video_url": "media/video_final_abc123def456.mp4"
}

// Error
{
    "status": "failed",
    "error": "Descripción del error"
}
```

### 3. Descargar video

Una vez que el status sea `"completed"`:

```bash
wget http://localhost:8000/media/video_final_abc123def456.mp4
```

## 🔧 Configuración avanzada

### Variables de entorno

Puedes personalizar la configuración creando un archivo `.env`:

```env
HF_HUB_DOWNLOAD_CHUNK_SIZE=262144
HF_HUB_DOWNLOAD_TIMEOUT=600
```

### Logs

Para ver los logs del contenedor:

```bash
docker-compose logs -f
```

## 🐛 Troubleshooting

### Puerto ocupado
Si el puerto 8000 está ocupado, cámbialo en `docker-compose.yml`:
```yaml
ports:
  - "8001:8000"  # Usar puerto 8001 en lugar de 8000
```

### Problemas de permisos
Si tienes problemas con permisos de archivos:
```bash
sudo chown -R $USER:$USER ./media/
```

### Reiniciar servicios
Para reiniciar completamente:
```bash
docker-compose down
docker-compose up -d --build
```

## 📊 Monitoreo

### Estado de la API
```bash
curl http://localhost:8000/health/
```

### Métricas básicas
```bash
curl http://localhost:8000/stats/
```

## 🤝 Contribución

Este es un proyecto privado. Para contribuir:

1. Contacta con el equipo de desarrollo
2. Solicita acceso al repositorio privado
3. Sigue las guías de desarrollo internas

## 📜 Licencia

Este software es **propietario** y está bajo licencia de emmpieza.com.

**Prohibido** su uso, distribución o modificación sin autorización expresa.

© 2024 emmpieza.com - Todos los derechos reservados.

## 📞 Soporte

Para soporte técnico o consultas:
- Email: emmpieza@gmail.com

---

**Desarrollado con ❤️ por el equipo de emmpieza.com
