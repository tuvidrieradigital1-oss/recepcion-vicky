# Vicky · Recepcionista virtual para consultorios dentales

React + Vite + Tailwind en el frontend. Cloudflare Pages Functions (carpeta `functions/`) como backend. Supabase como base de datos. Claude (Anthropic) como cerebro de Vicky.

## 1. Supabase
1. Creá un proyecto nuevo en https://supabase.com (el tuyo, no el de Lovable).
2. SQL Editor → pegá el contenido de `supabase/migrations/0001_init.sql` → Run.
3. Project Settings → API: copiá **Project URL** y la clave **service_role** (secreta, nunca en el frontend).

## 2. GitHub
```bash
git init
git add .
git commit -m "Vicky dental"
git branch -M main
git remote add origin https://github.com/TU-USUARIO/vicky-dental.git
git push -u origin main
```

## 3. Cloudflare Pages
Workers & Pages → Create → Pages → Connect to Git → elegí el repo.
- Framework preset: None
- Build command: `npm run build`
- Build output directory: `dist`

Settings → Variables and Secrets (Production), tipo Secret:
| Nombre | Valor |
|---|---|
| `ANTHROPIC_API_KEY` | tu clave de https://console.anthropic.com |
| `SUPABASE_URL` | Project URL de Supabase |
| `SUPABASE_SERVICE_ROLE_KEY` | clave service_role |
| `PANEL_PIN` | el PIN que quieras para el panel |
| `ANTHROPIC_MODEL` | (opcional) por defecto `claude-haiku-5-5` |

Después de cargar las variables, hacé un nuevo deploy (Deployments → Retry).

## 4. Personalizar para cada cliente
Editá solo `src/lib/clinic.ts` (nombre, doctor, dirección, WhatsApp, horarios, servicios, obras sociales).

## Probar en local
```bash
npm install
cp .dev.vars.example .dev.vars   # completá los valores
npm run build
npx wrangler pages dev dist
```
