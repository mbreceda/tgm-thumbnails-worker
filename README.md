# TGM · worker público de miniaturas

Worker de GitHub Actions para generar miniaturas sin gastar minutos del repo
privado.

**No imprime nombres de archivo.** El worker loguea UUIDs y conteos. La salida
del workflow no lista nombres.

## Secretos

En `Settings → Secrets and variables → Actions`:

| Secreto | Para qué |
|---|---|
| `TGM_READ_TOKEN` | PAT fine-grained con `Contents: Read` sobre `mbreceda/tgm_media_server` |
| `TGM_WORKER_TOKEN` | Mismo `WORKER_TOKEN` del backend |
| `TGM_BACKEND_URL` | `https://tgm-media-server.onrender.com` |

`TGM_READ_TOKEN` es de solo lectura. No darle escritura. Rotarlo si se filtra.

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
