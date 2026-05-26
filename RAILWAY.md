# Deploy en Railway

## Opción 1: Desde GitHub (Recomendado)

1. Haz fork de este repo a tu cuenta de GitHub
2. En [Railway](https://railway.app), crea un nuevo proyecto → **Add → GitHub Repo**
3. Selecciona tu fork del repo
4. Railway detecta automáticamente el `Dockerfile` y hace build
5. La imagen incluye la SQLite con ~145k registros de SEPOMEX

## Opción 2: Deploy con Railway CLI

```bash
# Instalar CLI si no la tienes
npm i -g @railway/cli

# Login
railway login

# Inicializar proyecto
railway init

# Deploy
railway up
```

## Variables de entorno (opcionales)

Railway inyecta automáticamente `PORT`, pero puedes ajustar:

| Variable | Valor | Descripción |
|---|---|---|
| `RAILS_FORCE_SSL` | `no` | Railway maneja SSL en el edge |
| `RAILS_MAX_THREADS` | `5` | Threads de Puma |

## Después del deploy

La API estará disponible en la URL que Railway te asigna:

```
https://tu-proyecto.railway.app/api/v1/zip_codes
https://tu-proyecto.railway.app/api/v1/states
https://tu-proyecto.railway.app/api/v1/municipalities
https://tu-proyecto.railway.app/api/v1/cities
```

## Notas

- La base de datos SQLite se construye **dentro de la imagen Docker** durante el build
- Los ~145k registros ya vienen del CSV incluido en `lib/sepomex_db.csv`
- No necesitas descargar ni configurar nada adicional
- La API es read-only, no hay writes en runtime
