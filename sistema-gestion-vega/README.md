# Sistema de Gestión de Pedidos - La Vega

Sistema web para procesar exportaciones de Shopify y generar listas de compras y armado de pedidos.

## 🚀 Instalación Rápida

### Opción 1: Local (para pruebas)

```bash
# 1. Instalar dependencias
pip install -r requirements.txt

# 2. Ejecutar
python app.py

# 3. Abrir en navegador
# http://localhost:8000
```

### Opción 2: Railway (recomendado para producción)

1. Crear cuenta en [Railway](https://railway.app)
2. Nuevo proyecto → "Deploy from GitHub" o subir archivos
3. Railway detectará automáticamente Python y desplegará
4. Agregar variable de entorno si es necesario: `PORT=8000`

### Opción 3: Render

1. Crear cuenta en [Render](https://render.com)
2. Nuevo Web Service → subir repositorio
3. Build command: `pip install -r requirements.txt`
4. Start command: `uvicorn app:app --host 0.0.0.0 --port $PORT`

---

## 📖 Guía de Uso

### 1. Importar Pedidos

1. Exportar pedidos desde Shopify Admin (Pedidos → Exportar → CSV)
2. En el sistema, hacer clic en "Seleccionar archivo CSV"
3. Clic en "Importar"
4. El sistema detectará automáticamente:
   - Pedidos nuevos
   - Pedidos duplicados (se ignoran)
   - Pedidos sin fecha de entrega

### 2. Asignar Categorías

Los productos nuevos aparecerán en "Productos sin asignar". Para cada uno:

1. Clic en "Asignar"
2. Seleccionar la categoría correspondiente
3. Guardar

Esto permite que la lista de compras se agrupe correctamente.

### 3. Descargar Reportes

Para cada fecha con pedidos pendientes, puedes descargar:

- **🛒 Compras**: Excel con lista de compras agrupada por categoría
- **📦 Armado**: Excel con detalle de cada pedido para armar los paquetes

### 4. Marcar Pedidos Completados

1. Clic en "👁️ Ver" para una fecha
2. Ver el detalle de cada pedido
3. Clic en "✅ Completado" cuando el pedido esté armado y entregado

---

## 📊 Estructura de Datos

### Categorías por defecto
- Frutas
- Verduras
- Congelados
- Abarrotes
- Lácteos
- Carnes
- Otros

Puedes agregar más categorías desde la interfaz.

### Campos importados desde Shopify
- Número de orden
- Email
- Comuna de entrega (desde Note Attributes)
- Fecha de entrega (desde Note Attributes)
- Nombre del cliente
- Dirección
- Productos y cantidades

---

## 🗂️ Archivos del Sistema

```
vega-system/
├── app.py              # Aplicación principal (FastAPI)
├── requirements.txt    # Dependencias Python
├── vega.db            # Base de datos SQLite (se crea automáticamente)
├── outputs/           # Archivos Excel generados
├── static/
│   └── style.css      # Estilos
└── templates/
    └── index.html     # Interfaz web
```

---

## 🔧 Configuración Avanzada

### Agregar más categorías por defecto

En `app.py`, busca `categorias_default` y agrega:

```python
categorias_default = [
    ('Frutas', 1),
    ('Verduras', 2),
    # ... agregar más aquí
    ('Mi Nueva Categoría', 10),
]
```

### Cambiar puerto

```bash
uvicorn app:app --host 0.0.0.0 --port 3000
```

---

## 📱 Compatibilidad

- ✅ Desktop (Chrome, Firefox, Safari, Edge)
- ✅ Tablet
- ✅ Móvil (responsive)

---

## 🆘 Soporte

Para modificaciones o soporte técnico, contactar a FlipIt.
