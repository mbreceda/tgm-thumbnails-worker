# TGM · worker público de miniaturas

Worker de GitHub Actions para generar miniaturas sin gastar minutos del repo
privado.

**No imprime nombres de archivo.** El worker loguea UUIDs y conteos. La salida
del workflow no lista nombres.

## Secretos

En `Settings → Secrets and variables → Actions`:

| Secreto | Para qué |
|---|---|
| `TGM_DEPLOY_KEY` | Deploy key de solo lectura del repo privado |
| `TGM_WORKER_TOKEN` | Mismo `WORKER_TOKEN` del backend |
| `TGM_BACKEND_URL` | `https://tgm-media-server.onrender.com` |
| `R2_ENDPOINT` | Endpoint S3 del bucket |
| `R2_BUCKET` | Bucket de miniaturas |
| `R2_ACCESS_KEY_ID` | Credencial R2 |
| `R2_SECRET_ACCESS_KEY` | Credencial R2 |

`TGM_DEPLOY_KEY` es de solo lectura. No darle escritura. Rotarla si se filtra.

## Uso

- Cron cada 10 minutos.
- Manual: `Actions → thumbnails → Run workflow`.
- Encola hasta 40 faltantes y procesa 40 turnos.
- Solo reclama `thumbnail.generate`.
- No usa MTProto desde el runner.

## Seguridad

- El repo es público; los secretos no.
- No ejecutar workflows de `pull_request`.
- No imprimir payloads ni nombres.
- El código privado se descarga en el runner y se borra al terminar.
