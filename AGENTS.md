# AGENTS.md - Guía para Agentes de IA

Este archivo es la guía principal para que los agentes de IA de codificación comprendan, naveguen y contribuyan a este proyecto de manera eficiente.

## 🎯 ¿Qué es ShipFree?

ShipFree es una **alternativa open-source a ShipFast**, un boilerplate para lanzar aplicaciones web completas rápidamente. Está construido con:

- **Frontend**: Next.js 14 (App Router) + TailwindCSS + shadcn/ui
- **Auth**: Supabase Auth
- **Base de datos**: Supabase (PostgreSQL) o MongoDB
- **Pagos**: Stripe / LemonSqueezy
- **Email**: Mailgun
- **Deployment**: Vercel (recomendado) o Docker

---

## 📖 Documentación

Toda la documentación detallada está en la carpeta `docs/`. Consulta `docs/AGENTS.md` para una guía específica de navegación dentro de esa carpeta.

| Tema | Archivo | Cuándo leerlo |
|------|---------|---------------|
| **Inicio rápido** | `docs/geting-started.md` | Para entender el proyecto por primera vez |
| **Despliegue** | `docs/deployment.md` | Antes de hacer deploy a Vercel |
| **Extras** | `docs/extras.md` | Favicons, logos, Open Graph |
| **Auth** | `docs/features/auth.md` | Cambios en autenticación |
| **Pagos (Stripe)** | `docs/features/stripe.md` | Integración de pagos Stripe |
| **Pagos (Lemon)** | `docs/features/lemon-squeezy.md` | Integración LemonSqueezy |
| **Emails** | `docs/features/emails.md` | Configuración de Mailgun |
| **SEO** | `docs/features/SEO.md` | Metadatos, sitemap, Open Graph |
| **Componentes UI** | `docs/components/*.md` | Modificar componentes visuales |

---

## 🗂️ Estructura del Repositorio

```
ShipFree/
├── src/                        # Código fuente principal
│   ├── app/                    # Next.js App Router
│   │   ├── (site)/             # Páginas públicas del sitio
│   │   ├── api/                # API Routes (Stripe, webhooks, etc.)
│   │   ├── auth/               # Páginas de autenticación
│   │   ├── dashboard/          # Dashboard de usuario
│   │   ├── privacy-policy/     # Página de privacidad
│   │   ├── tos/                # Términos de servicio
│   │   ├── layout.tsx          # Layout principal
│   │   ├── page.tsx            # Landing page
│   │   └── globals.css         # Estilos globales
│   ├── components/             # Componentes React reutilizables
│   │   ├── ui/                 # Componentes base shadcn/ui
│   │   ├── CheckoutButton.tsx  # Botón de pago Stripe
│   │   ├── lemon-button.tsx    # Botón de pago LemonSqueezy
│   │   ├── pricing.tsx         # Componente de precios
│   │   └── *-form.tsx          # Formularios de auth
│   ├── lib/                    # Utilidades y configuraciones
│   │   ├── supabase/           # Cliente y servidor Supabase
│   │   ├── mailgun.ts          # Configuración de Mailgun
│   │   └── utils.ts            # Utilidades generales
│   ├── db/                     # Esquemas de base de datos (Drizzle)
│   ├── types/                  # Definiciones de tipos TypeScript
│   ├── utils/                  # Funciones auxiliares
│   └── config.ts               # Configuración global de la app
├── docs/                       # Documentación del proyecto
│   ├── AGENTS.md               # Guía de navegación de docs
│   ├── features/               # Docs de funcionalidades
│   └── components/             # Docs de componentes UI
├── docker/                     # Configuración Docker
│   ├── dev/                    # Desarrollo (watch mode)
│   └── prod/                   # Producción (optimizado)
├── public/                     # Assets estáticos
├── .env.example                # Variables de entorno de ejemplo
├── package.json                # Dependencias npm
├── tailwind.config.ts          # Configuración TailwindCSS
├── drizzle.config.ts           # Configuración Drizzle ORM
└── next.config.ts              # Configuración Next.js
```

---

## ⚡ Comandos Rápidos

```bash
# Desarrollo local
pnpm dev

# Build de producción
pnpm build

# Docker (desarrollo)
docker-compose -f docker/dev/docker-compose.yml up --build

# Docker (producción)
docker-compose -f docker/prod/docker-compose.yml up --build -d
```

---

## 🤖 Instrucciones para Agentes

### Antes de empezar cualquier tarea:
1. **Lee `docs/geting-started.md`** si es tu primera vez con el proyecto.
2. **Consulta la documentación relevante** según la tarea (ver tabla arriba).
3. **Revisa `src/config.ts`** para entender la configuración global.

### Al modificar código:
1. **Ubicación correcta**: Respeta la estructura del directorio. Componentes en `components/`, rutas en `app/`, utilidades en `lib/` o `utils/`.
2. **Tipos**: Añade tipos TypeScript en `src/types/` si creas nuevas interfaces.
3. **Componentes UI**: Usa los componentes de `components/ui/` (shadcn) como base.
4. **Estilos**: Usa TailwindCSS. Estilos globales van en `globals.css`.

### Al añadir nuevas funcionalidades:
1. **Documenta**: Actualiza o crea documentación en `docs/`.
2. **Variables de entorno**: Añádelas también en `.env.example`.
3. **API Routes**: Colócalas en `src/app/api/`.

### Integración con servicios externos:
- **Supabase**: Configuración en `src/lib/supabase/`
- **Stripe**: Ver `docs/features/stripe.md` y `src/app/api/`
- **LemonSqueezy**: Ver `docs/features/lemon-squeezy.md`
- **Mailgun**: Ver `docs/features/emails.md` y `src/lib/mailgun.ts`

---

## 🔑 Variables de Entorno Clave

Consulta `.env.example` para la lista completa. Las principales son:

| Variable | Descripción |
|----------|-------------|
| `NEXT_PUBLIC_SUPABASE_URL` | URL de tu proyecto Supabase |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Clave anónima de Supabase |
| `SUPABASE_SERVICE_ROLE_KEY` | Clave de servicio (backend) |
| `STRIPE_SECRET_KEY` | Clave secreta de Stripe |
| `MAILGUN_API_KEY` | API Key de Mailgun |
| `MAILGUN_DOMAIN` | Dominio de Mailgun |

---

*Este archivo está diseñado para ser leído por agentes de IA. Última actualización: Diciembre 2024.*
