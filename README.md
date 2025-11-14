# Sistema de Gestión de Campañas de WhatsApp

Una plataforma integral de mensajería WhatsApp construida con Laravel y Node.js, que incluye gestión avanzada de campañas, seguimiento de mensajes en tiempo real y manejo automatizado de respuestas.

## 🚀 Funcionalidades

### Gestión de Campañas
- **Crear y Editar Campañas**: Operaciones CRUD completas para campañas de marketing
- **Mensajería Masiva**: Envío de mensajes a múltiples destinatarios simultáneamente
- **Reinicio de Campaña**: Reiniciar campañas completadas y reiniciar estadísticas
- **Plantillas de Mensajes**: Soporte tanto para mensajes de texto como para plantillas
- **Gestión de Números**: Añadir/eliminar destinatarios dinámicamente

### Seguimiento en Tiempo Real
- **Estado del Mensaje**: Seguimiento de enviado, entregado y leído
- **Seguimiento de Respuestas**: Captura automática y vinculación de respuestas de clientes
- **Estadísticas en Vivo**: Métricas y analíticas de campaña en tiempo real
- **Integración por Webhooks**: Integración fluida con la API de WhatsApp Business

### Análisis e Informes
- **Estadísticas de Campaña**: Tasas de entrega, lectura y respuesta
- **Gestión de Respuestas**: Ver y gestionar las respuestas de los clientes
- **Exportar Resultados**: Exportar resultados de campañas a CSV
- **Métricas de Rendimiento**: Seguimiento completo del rendimiento de campañas

## 🛠 Stack Tecnológico

- **Backend**: Laravel 10+ (PHP 8.1+)
- **Frontend**: Livewire, TailwindCSS, Alpine.js
- **Motor WhatsApp**: Node.js con la librería Baileys
- **Base de Datos**: MySQL/PostgreSQL
- **Tiempo Real**: Integración por WebSocket
- **Colas**: Colas de Laravel para procesamiento de mensajes

## 📋 Requisitos

- PHP 8.1 o superior
- Composer
- Node.js 16+ y npm
- Base de datos MySQL/PostgreSQL
- Cuenta de WhatsApp Business

## ⚡ Inicio Rápido

### 1. Clonar e Instalar
```bash
git clone <repository-url>
cd laravel-whatsapp-saas
composer install
npm install
```

### 2. Configurar el Entorno
```bash
cp .env.example .env
php artisan key:generate
```

### 3. Configuración de la Base de Datos
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=whatsapp_saas
DB_USERNAME=tu_usuario
DB_PASSWORD=tu_contraseña
```

### 4. Ejecutar Migraciones
```bash
php artisan migrate
```

### 5. Compilar Assets
```bash
npm run build
```

### 6. Iniciar Servicios
```bash
# Terminal 1: Aplicación Laravel
php artisan serve

# Terminal 2: Motor de WhatsApp
cd whatsapp-engine
npm install
npm start
```

## 🔧 Configuración del Motor de WhatsApp

### 1. Instalar Dependencias
```bash
cd whatsapp-engine
npm install
```

### 2. Configurar el Entorno
```bash
# Crear archivo .env en el directorio whatsapp-engine
WHATSAPP_ENGINE_PORT=3000
APP_URL=http://localhost:8000
WEBHOOK_URL=http://localhost:8000/webhook/whatsapp
NODE_ENV=development
```

### 3. Iniciar el Motor y Conectar WhatsApp
```bash
npm start
# Visita http://localhost:3000/status
# Escanea el código QR con tu WhatsApp
```

## 📱 Guía de Uso

### Crear Campañas
1. Navega a la sección **Campaigns**
2. Haz clic en **"New Campaign"**
3. Rellena los detalles de la campaña:
   - Nombre y descripción de la campaña
   - Contenido del mensaje
   - Números de teléfono (uno por línea)
4. Haz clic en **"Create Campaign"**

### Gestionar Campañas
- **Start**: Iniciar el envío de mensajes
- **Pause**: Pausar temporalmente la campaña
- **Edit**: Modificar contenido o destinatarios (incluso campañas completadas)
- **Restart**: Reiniciar y volver a enviar campañas completadas
- **View Details**: Ver estadísticas detalladas y respuestas

### Monitoreo de Respuestas
- **Seguimiento en Tiempo Real**: Las respuestas aparecen automáticamente
- **Gestión de Respuestas**: Ver todas las respuestas en una sección dedicada
- **Exportar Datos**: Descargar resultados de la campaña con respuestas

## 🔌 Endpoints de la API

### Gestión de Campañas
```bash
# Obtener estado de una campaña
GET /api/campaigns/{id}

# Crear campaña
POST /api/campaigns

# Actualizar campaña
PUT /api/campaigns/{id}
```

### Operaciones de Mensajes
```bash
# Enviar un mensaje único
POST /api/messages
{
    "phone_number": "+1234567890",
    "message": "¡Hola Mundo!"
}

# Obtener estado de un mensaje
GET /api/messages/{id}/status
```

### Endpoints de Webhook
```bash
# Webhook de WhatsApp (configurado automáticamente)
POST /webhook/whatsapp

# Verificación de webhook
GET /webhook/whatsapp
```

## 🔄 Integración por Webhooks

El sistema maneja automáticamente los webhooks de WhatsApp para:
- **Mensaje Enviado**: Confirma el envío a WhatsApp
- **Mensaje Entregado**: Actualiza el estado de entrega
- **Mensaje Leído**: Registra los recibos de lectura
- **Mensajes Entrantes**: Captura y vincula respuestas de clientes

## 📊 Estadísticas de Campaña

### Métricas Disponibles
- **Total de Destinatarios**: Número de destinatarios objetivo
- **Enviados**: Mensajes enviados con éxito
- **Entregados**: Mensajes entregados a los dispositivos
- **Leídos**: Mensajes abiertos por los destinatarios
- **Respuestas**: Respuestas recibidas de clientes
- **Fallidos**: Intentos de envío fallidos

### Tasas Calculadas
- **Tasa de Éxito**: (Entregados / Enviados) × 100
- **Tasa de Lectura**: (Leídos / Entregados) × 100
- **Tasa de Respuesta**: (Respuestas / Entregados) × 100

## 🛡 Características de Seguridad

- **Protección CSRF**: Endpoints de webhook asegurados correctamente
- **Validación de Entradas**: Todas las entradas de usuario validadas
- **Limitación de Tasa**: Endpoints de la API con rate limiting
- **Autenticación**: Acceso autenticado requerido
- **Saneamiento de Datos**: Números de teléfono y contenido sanitizados

## 🧪 Pruebas

### Ejecutar Tests de Laravel
```bash
php artisan test
```

### Pruebas Manuales
1. Crea una campaña de prueba
2. Envía mensajes mediante el Motor de WhatsApp
3. Responde desde tu teléfono
4. Verifica que las estadísticas se actualizan en tiempo real

## 🔧 Desarrollo

### Estilo de Código
```bash
./vendor/bin/pint
```

### Desarrollo Frontend
```bash
npm run dev
```

### Seed de Base de Datos
```bash
php artisan db:seed
```

## 📁 Estructura del Proyecto

```
├── app/
│   ├── Http/Controllers/     # Controladores de API y Webhook
│   ├── Livewire/            # Componentes frontend
│   ├── Models/              # Modelos de la base de datos
│   └── Services/            # Lógica de negocio
├── whatsapp-engine/         # Integración de WhatsApp en Node.js
├── resources/views/         # Plantillas Blade
├── database/migrations/     # Esquema de la base de datos
└── routes/                  # Rutas de la aplicación
```

## 🤝 Contribuir

1. Haz fork del repositorio
2. Crea una rama de función (`git checkout -b feature/amazing-feature`)
3. Haz commit de tus cambios (`git commit -m 'Add amazing feature'`)
4. Sube la rama (`git push origin feature/amazing-feature`)
5. Abre un Pull Request

## 📄 Licencia

Este proyecto está bajo la licencia MIT - consulta el archivo [LICENSE](LICENSE) para más detalles.

## 🆘 Soporte

- **Issues**: Reporta bugs mediante GitHub Issues
- **Documentación**: Revisa la wiki para guías detalladas
- **Comunidad**: Únete a nuestro servidor de Discord para soporte

## 🙏 Agradecimientos

- Construido con [Laravel](https://laravel.com/)
- Integración de WhatsApp mediante [Baileys](https://github.com/WhiskeySockets/Baileys)
- Componentes UI con [TailwindCSS](https://tailwindcss.com/)
- Funcionalidades en tiempo real con [Livewire](https://laravel-livewire.com/)
