# Desarrollo Local

Guía para configurar y ejecutar el proyecto en tu máquina local.

## Requisitos Previos

- **Node.js** 18+ (recomendado: LTS)
- **npm** (incluido con Node.js)
- **Git**

## Instalación

```bash
# 1. Clonar el repositorio
git clone https://github.com/albertllonch/paisdepandereta.git
cd paisdepandereta

# 2. Instalar dependencias
npm install
```

## Comandos Disponibles

| Comando           | Descripción                       |
| ----------------- | --------------------------------- |
| `npm run dev`     | Iniciar servidor de desarrollo    |
| `npm run build`   | Compilar para producción          |
| `npm run preview` | Previsualizar build de producción |
| `npm run check`   | Verificar tipos y Svelte          |
| `npm run format`  | Formatear código con Prettier     |
| `npm run lint`    | Verificar estilo de código        |

## Ejecutar en Desarrollo

```bash
npm run dev
```

El servidor estará disponible en: **http://localhost:5173**

## Verificar Código

Antes de hacer commit, ejecuta:

```bash
# Verificar tipos y errores
npm run check

# Formatear código
npm run format

# Linter completo
npm run lint
```

## Estructura del Proyecto

```
paisdepandereta/
├── src/
│   ├── lib/
│   │   ├── components/    # Componentes Svelte
│   │   └── assets/       # Recursos estáticos
│   └── routes/           # Páginas y rutas
│       ├── +page.svelte  # Página principal
│       ├── blog/         # Blog
│       ├── herramientas/ # Herramientas
│       ├── datos/        # Datos
│       └── ...
├── static/               # Archivos estáticos públicos
└── data/                # Archivos de datos (CSV, JSON)
```

## Tecnologías

- **SvelteKit** - Framework web
- **Svelte 5** - Componentes
- **TailwindCSS 4** - Estilos
- **TypeScript** - Tipado estático
