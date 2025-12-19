# 🗺️ LocalSpot - Red Social de Recomendaciones Locales

Plataforma web donde usuarios pueden compartir y descubrir lugares locales (restaurantes, cafés, bares, parques, tiendas) con reviews, fotos y ubicación en mapa interactivo.

---

## 🎯 Objetivo del Proyecto

Crear una red social enfocada en recomendaciones de lugares locales, permitiendo a los usuarios:
- Descubrir nuevos lugares cerca de su ubicación
- Compartir sus experiencias y recomendaciones
- Ver opiniones de otros usuarios
- Explorar lugares en un mapa interactivo
- Guardar sus lugares favoritos

---

## 🛠️ Stack Tecnológico

### Frontend
- **React** con **Vite**
- **Tailwind CSS** para estilos
- **React Router** para navegación
- **React Hook Form** para manejo de formularios
- **Axios** para peticiones HTTP
- **React Leaflet** o **Google Maps React** para mapas interactivos
- **Zustand** o **Context API** para gestión de estado

### Backend
- **Express.js**
- **MongoDB** con **Mongoose**
- **JWT** para autenticación
- **bcrypt** para encriptación de contraseñas
- **Multer** para carga de archivos
- **express-validator** para validaciones

### APIs Externas
- **Google Maps Platform:**
  - Places API (autocompletado de direcciones)
  - Maps JavaScript API (mapa interactivo)
  - Geocoding API (conversión de direcciones a coordenadas)
  - Geolocation API (ubicación del usuario)
- **Cloudinary** para almacenamiento y optimización de imágenes
- **SendGrid** o **Nodemailer** para envío de emails (opcional)
- **WhatsApp Business API** o **Web Share API** para compartir lugares

---

## ⚡ Funcionalidades Principales

### 1. Autenticación y Perfiles 👤
- Sistema de registro y login con JWT
- Perfil de usuario personalizable:
  - Foto de perfil
  - Biografía
  - Ubicación/ciudad
  - Lugares favoritos
  - Historial de recomendaciones publicadas
- Sistema de seguir a otros usuarios (opcional)

### 2. CRUD de Lugares 📍
**Crear lugar:**
- Nombre del establecimiento
- Categoría (restaurante, café, bar, parque, museo, tienda, etc.)
- Descripción detallada
- Dirección con autocompletado (Google Places API)
- Coordenadas geográficas (automáticas)
- Galería de fotos (múltiples imágenes vía Cloudinary)
- Rango de precio ($, $$, $$$)
- Tags/etiquetas personalizadas (ej: "terraza", "pet-friendly", "wifi gratis")
- Horarios de atención (opcional)

**Ver lugar:**
- Información completa del lugar
- Galería de fotos en grid
- Ubicación en mapa interactivo
- Lista de reviews de usuarios
- Puntuación promedio con estrellas
- Botón para guardar en favoritos
- Opciones para compartir en redes sociales

**Editar/Eliminar:**
- Solo el creador del lugar puede editarlo o eliminarlo
- Validación de permisos en backend

### 3. Sistema de Reviews y Ratings ⭐
- Calificación de 1 a 5 estrellas
- Comentario escrito descriptivo
- Posibilidad de adjuntar fotos adicionales
- Fecha de la visita
- Sistema de votos "Útil" en reviews
- Editar o eliminar tu propio review
- Un usuario solo puede hacer un review por lugar

### 4. Búsqueda y Filtros 🔍
**Búsqueda por:**
- Nombre del lugar
- Categoría específica
- Ciudad o ubicación
- Tags/etiquetas
- Rango de precio

**Ordenamiento:**
- Más recientes
- Mejor calificados
- Mayor cantidad de reviews
- Distancia (cerca de mi ubicación)

**Filtros adicionales:**
- Solo mostrar favoritos
- Por usuario específico
- Por rango de calificación

### 5. Mapa Interactivo 🗺️
- Visualización de todos los lugares con markers personalizados
- Click en marker abre popup con información básica
- Filtros aplicables directamente en el mapa
- Botón "Cerca de mí" con geolocalización
- Opción de ver ruta desde tu ubicación
- Agrupación de markers cuando hay muchos cercanos (clusters)

### 6. Sistema de Favoritos ❤️
- Guardar lugares en favoritos con un click
- Crear listas personalizadas (ej: "Para visitar", "Mejores cafés")
- Ver todos tus favoritos en una página dedicada
- Compartir tus listas con otros usuarios

### 7. Features Sociales 🌐
**Feed/Timeline:**
- Nuevos lugares agregados recientemente
- Reviews recientes de la comunidad
- Actividad de usuarios que sigues (opcional)

**Notificaciones:**
- Alguien comenta en un lugar que creaste
- Nuevo seguidor en tu perfil
- Tu lugar fue guardado como favorito

**Compartir:**
- WhatsApp (usando Web Share API o enlace directo)
- Twitter, Facebook (Social Share APIs)
- Copiar enlace al portapapeles

### 8. Dashboard y Estadísticas (Opcional) 📊
- Lugares más populares del mes
- Categorías más activas
- Mapa de calor de zonas con más lugares
- Usuarios más activos de la comunidad
- Tus estadísticas personales:
  - Lugares creados
  - Reviews escritos
  - Lugares guardados
  - Seguidores

---

## 🗄️ Estructura de Base de Datos

### Colección: Users
```
- _id (ObjectId)
- username (String, único)
- email (String, único)
- password (String, hasheado)
- avatar (String, URL de Cloudinary)
- bio (String)
- location (String)
- favorites (Array de Place IDs)
- followers (Array de User IDs)
- following (Array de User IDs)
- createdAt (Date)
```

### Colección: Places
```
- _id (ObjectId)
- name (String)
- category (String)
- description (String)
- address (String)
- coordinates (Object: {lat: Number, lng: Number})
- photos (Array de Strings - URLs de Cloudinary)
- priceRange (String: $, $$, $$$)
- tags (Array de Strings)
- hours (String)
- createdBy (User ID)
- averageRating (Number)
- totalReviews (Number)
- createdAt (Date)
- updatedAt (Date)
```

### Colección: Reviews
```
- _id (ObjectId)
- placeId (Place ID)
- userId (User ID)
- rating (Number, 1-5)
- comment (String)
- photos (Array de Strings)
- visitDate (Date)
- helpfulCount (Number)
- createdAt (Date)
- updatedAt (Date)
```

---

## 📱 Páginas Principales (Frontend)

1. **Home/Feed** - Timeline con lugares recientes y actividad
2. **Explorar/Mapa** - Mapa interactivo con todos los lugares
3. **Detalle de Lugar** - Información completa, fotos, reviews y mapa
4. **Perfil de Usuario** - Tus lugares, reviews y favoritos
5. **Crear/Editar Lugar** - Formulario para agregar nuevos lugares
6. **Búsqueda** - Página de búsqueda con filtros avanzados
7. **Favoritos** - Lista de lugares guardados
8. **Login/Register** - Autenticación de usuarios
9. **Configuración** - Editar perfil y preferencias

---

## 🚀 Plan de Desarrollo por Fases

> **IMPORTANTE:** Este proyecto está diseñado para desarrollarse en fases incrementales. NO intentes hacer todo de una vez. Completa cada fase antes de pasar a la siguiente.

---

### **FASE 1: Fundamentos (MVP Básico)** ✅
**Objetivo:** Tener un sistema funcional básico de usuarios y lugares.

**Backend:**
- [ ] Configurar proyecto Express
- [ ] Conectar MongoDB con Mongoose
- [ ] Crear modelos de User y Place
- [ ] Implementar autenticación (registro, login, JWT)
- [ ] Crear rutas CRUD para Places
- [ ] Validaciones básicas con express-validator
- [ ] Middleware de autenticación

**Frontend:**
- [ ] Configurar proyecto React + Vite + Tailwind
- [ ] Crear estructura de carpetas
- [ ] Páginas de Login y Register
- [ ] Configurar React Router
- [ ] Página de creación de lugar (sin imágenes aún)
- [ ] Página de lista de lugares (vista simple)
- [ ] Página de detalle de lugar
- [ ] Sistema de autenticación en frontend (tokens)

**Funcionalidades de esta fase:**
- Usuarios pueden registrarse e iniciar sesión
- Usuarios pueden crear lugares (solo con texto, sin fotos)
- Ver lista de lugares
- Ver detalle de un lugar específico

---

### **FASE 2: Reviews y Sistema de Calificación** ⭐
**Objetivo:** Agregar sistema de reviews y ratings.

**Backend:**
- [ ] Crear modelo de Reviews
- [ ] Rutas CRUD para reviews
- [ ] Lógica para calcular promedio de ratings
- [ ] Validar que un usuario solo pueda hacer 1 review por lugar
- [ ] Actualizar contador de reviews en Places

**Frontend:**
- [ ] Componente de rating con estrellas
- [ ] Formulario para crear review
- [ ] Mostrar reviews en detalle de lugar
- [ ] Sistema de paginación o scroll infinito para reviews
- [ ] Editar/eliminar tu propio review

**Funcionalidades de esta fase:**
- Usuarios pueden calificar y comentar lugares
- Ver promedio de calificaciones
- Ver todas las reviews de un lugar
- Editar o eliminar tu review

---

### **FASE 3: Integración de Imágenes (Cloudinary)** 📸
**Objetivo:** Agregar soporte para subir y mostrar imágenes.

**Backend:**
- [ ] Configurar Cloudinary SDK
- [ ] Instalar y configurar Multer
- [ ] Ruta para subir fotos de lugares
- [ ] Ruta para subir foto de perfil
- [ ] Optimización de imágenes (resize, formato)
- [ ] Eliminar imágenes de Cloudinary al borrar lugares

**Frontend:**
- [ ] Componente de upload de imágenes (drag & drop)
- [ ] Preview de imágenes antes de subir
- [ ] Galería de fotos en detalle de lugar
- [ ] Selector de foto de perfil
- [ ] Lightbox para ver imágenes en grande

**Funcionalidades de esta fase:**
- Subir múltiples fotos al crear lugares
- Galería de fotos en cada lugar
- Foto de perfil personalizada
- Preview y crop de imágenes

---

### **FASE 4: Mapa Interactivo (Google Maps)** 🗺️
**Objetivo:** Integrar Google Maps para visualizar lugares.

**Backend:**
- [ ] Integrar Google Geocoding API
- [ ] Endpoint para convertir direcciones a coordenadas
- [ ] Endpoint para buscar lugares cercanos por radio
- [ ] Guardar coordenadas al crear lugar

**Frontend:**
- [ ] Configurar Google Maps API o React Leaflet
- [ ] Página de exploración con mapa
- [ ] Markers personalizados para lugares
- [ ] Popup al hacer click en marker
- [ ] Autocompletado de direcciones (Google Places)
- [ ] Mapa en detalle de lugar
- [ ] Botón "Cerca de mí" con geolocalización

**Funcionalidades de esta fase:**
- Ver todos los lugares en un mapa interactivo
- Buscar lugares por ubicación
- Autocompletado al escribir direcciones
- Ver ubicación exacta de cada lugar
- Encontrar lugares cerca de ti

---

### **FASE 5: Búsqueda y Filtros Avanzados** 🔍
**Objetivo:** Sistema completo de búsqueda y filtros.

**Backend:**
- [ ] Implementar búsqueda por texto (nombre, descripción, tags)
- [ ] Filtros por categoría
- [ ] Filtros por rango de precio
- [ ] Filtros por calificación mínima
- [ ] Ordenamiento (recientes, mejor calificados, más reviews)
- [ ] Búsqueda por proximidad geográfica
- [ ] Paginación de resultados

**Frontend:**
- [ ] Barra de búsqueda global
- [ ] Página de resultados de búsqueda
- [ ] Sidebar con filtros
- [ ] Chips/tags para filtros activos
- [ ] Botones de ordenamiento
- [ ] Limpiar todos los filtros
- [ ] Aplicar filtros en mapa también

**Funcionalidades de esta fase:**
- Buscar lugares por nombre o descripción
- Filtrar por múltiples criterios simultáneamente
- Ordenar resultados de diferentes formas
- Ver resultados en lista o mapa

---

### **FASE 6: Sistema de Favoritos y Perfil** ❤️
**Objetivo:** Guardar lugares favoritos y perfil completo.

**Backend:**
- [ ] Endpoint para agregar/quitar favoritos
- [ ] Endpoint para obtener favoritos del usuario
- [ ] Endpoint para editar perfil
- [ ] Endpoint para ver perfil de otros usuarios
- [ ] Estadísticas del usuario (lugares creados, reviews)

**Frontend:**
- [ ] Botón de favorito (corazón) en cada lugar
- [ ] Página de favoritos del usuario
- [ ] Página de perfil completo
- [ ] Formulario para editar perfil
- [ ] Ver perfil de otros usuarios
- [ ] Tabs en perfil (lugares, reviews, favoritos)
- [ ] Dashboard con estadísticas personales

**Funcionalidades de esta fase:**
- Guardar lugares como favoritos
- Ver todos tus favoritos en una página
- Editar tu perfil (bio, ubicación, foto)
- Ver perfiles de otros usuarios
- Estadísticas personales

---

### **FASE 7: Features Sociales** 🌐
**Objetivo:** Agregar interacción entre usuarios.

**Backend:**
- [ ] Sistema de seguir/dejar de seguir usuarios
- [ ] Feed personalizado con actividad
- [ ] Sistema de notificaciones
- [ ] Endpoint para obtener seguidores/seguidos
- [ ] Actividad reciente (nuevos lugares, reviews)

**Frontend:**
- [ ] Botón de seguir/dejar de seguir
- [ ] Feed/Timeline en home
- [ ] Centro de notificaciones
- [ ] Indicador de notificaciones sin leer
- [ ] Lista de seguidores y seguidos
- [ ] Compartir lugares (Web Share API, WhatsApp)
- [ ] Botones de compartir en redes sociales

**Funcionalidades de esta fase:**
- Seguir a otros usuarios
- Ver feed con actividad de usuarios que sigues
- Recibir notificaciones de interacciones
- Compartir lugares por WhatsApp o redes sociales

---

### **FASE 8: Optimizaciones y Pulido** 🎨
**Objetivo:** Mejorar rendimiento y experiencia de usuario.

**Backend:**
- [ ] Implementar caché (Redis opcional)
- [ ] Optimizar queries de MongoDB (índices)
- [ ] Rate limiting
- [ ] Compresión de respuestas (gzip)
- [ ] Logging de errores
- [ ] Variables de entorno bien configuradas

**Frontend:**
- [ ] Lazy loading de imágenes
- [ ] Skeleton loaders
- [ ] Manejo de errores con toast notifications
- [ ] Modo oscuro/claro
- [ ] Responsive design completo
- [ ] Optimización de bundle (code splitting)
- [ ] PWA (opcional)
- [ ] Animaciones y transiciones suaves

**Funcionalidades de esta fase:**
- Aplicación más rápida y fluida
- Mejor experiencia de usuario
- Manejo elegante de errores
- Diseño responsive perfecto
- Modo oscuro

---

### **FASE 9 (Opcional): Features Avanzados** 🚀
**Objetivo:** Agregar funcionalidades premium.

- [ ] Sistema de listas personalizadas de lugares
- [ ] Modo offline (PWA)
- [ ] Chat entre usuarios
- [ ] Sistema de reportes/moderación
- [ ] Verificación de lugares (badge)
- [ ] Integración con redes sociales (login con Google)
- [ ] Recomendaciones personalizadas (ML básico)
- [ ] Dashboard de analytics global
- [ ] Exportar datos personales
- [ ] API pública para desarrolladores

---

## 📋 Checklist General de Cada Fase

Antes de pasar a la siguiente fase, asegúrate de:
- [ ] Todas las funcionalidades están implementadas
- [ ] Código está limpio y comentado
- [ ] No hay errores en consola
- [ ] Validaciones funcionan correctamente
- [ ] Responsive en móvil y desktop
- [ ] Manejo de errores implementado
- [ ] Testing básico realizado
- [ ] Git commit con mensaje descriptivo

---

## 🎨 Consideraciones de Diseño

- **Mobile First:** Diseña primero para móvil
- **UX Intuitiva:** Navegación clara y simple
- **Feedback Visual:** Loading states, confirmaciones
- **Accesibilidad:** Contraste, alt text, keyboard navigation
- **Performance:** Lazy loading, optimización de imágenes
- **Consistencia:** Mantén un sistema de diseño coherente

---

## 🔒 Consideraciones de Seguridad

- Hashear contraseñas con bcrypt
- Validar y sanitizar TODAS las entradas
- Rate limiting en endpoints sensibles
- CORS configurado correctamente
- Variables sensibles en .env (nunca en código)
- Validación de tokens JWT
- Protección contra XSS y SQL injection
- HTTPS en producción

---

## 📝 Notas Importantes

> ⚠️ **REGLA #1:** NO uses IA para generar código. Este proyecto es para practicar tus habilidades.

> 📚 **REGLA #2:** Consulta documentación oficial cuando tengas dudas.

> 🐛 **REGLA #3:** Debug paso a paso. No copies y pegues soluciones sin entenderlas.

> ⏰ **REGLA #4:** Tómate tu tiempo. Es mejor hacer poco bien que mucho mal.

> 🎯 **REGLA #5:** Completa cada fase antes de pasar a la siguiente.

---

## 🔗 Recursos Útiles

- [React Docs](https://react.dev)
- [Express Docs](https://expressjs.com)
- [MongoDB Docs](https://docs.mongodb.com)
- [Tailwind CSS](https://tailwindcss.com/docs)
- [Google Maps Platform](https://developers.google.com/maps)
- [Cloudinary Docs](https://cloudinary.com/documentation)
- [JWT.io](https://jwt.io)
- [MDN Web Docs](https://developer.mozilla.org)

---

## 📊 Progreso del Proyecto

**Fase actual:** Fase 1 - Fundamentos

**Completado:**
- [ ] Fase 1: Fundamentos
- [ ] Fase 2: Reviews
- [ ] Fase 3: Imágenes
- [ ] Fase 4: Mapa
- [ ] Fase 5: Búsqueda
- [ ] Fase 6: Favoritos
- [ ] Fase 7: Social
- [ ] Fase 8: Optimizaciones

---

## 🎉 ¡Buena Suerte!

Recuerda: El objetivo no es terminar rápido, sino **aprender y mejorar tus habilidades**. Tómate el tiempo necesario para entender cada concepto y disfruta el proceso de crear algo desde cero.

**¡Nos vemos cuando las RAM bajen de precio!** 💾