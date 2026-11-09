# 2026-11-09 · Release 0.14, parte 6: config publicado (`nube/cepillado-v2` → `main`)

**Autorización:** «autorizado por Xavi: merge a main, 9-nov-2026 13:43». **Créditos: 0** (ni ElevenLabs ni fal). Sin
correos, redes, consolas ni pagos. Solo `don-bigotes-config`; de `don-bigotes` (`feature/cepillado-2`) solo he leído.

## Resumen

- **Fusión `4d651ad`** (`--no-ff`, 2.º padre `32ef504`): push `c08584b..4d651ad` a las **12:46:55 UTC (13:46:55 Madrid)**.
  `main` no tenía nada que no tuviera la rama. El árbol de la fusión es **idéntico** al de `32ef504`.
- **Producción sirve lo nuevo desde las 12:48:11 UTC (13:48:11 Madrid)**: `last-modified` 12:48:04 GMT, 1 min 16 s
  tras el push. Antes, la caché de Fastly daba el viejo (HIT, `age` 55-97 s). `cache-control: max-age=600`: algún nodo
  que guardara el viejo justo antes puede servirlo hasta las **~12:58 UTC (13:58 Madrid)** como mucho. Ojo: `?nc=` no
  salta la caché (Fastly devolvía el mismo HIT).
- **config.json de producción = el de la rama, byte a byte** (sha256 `8edbdf55…502d8098`, 1.489 B).
- **198 de 198 bien en producción**: 85 manifests y 113 ficheros, todos **HTTP 200**, con los mismos bytes y sha256 que la
  rama y que su manifest (156.194.427 B sin contar los manifests). Lista completa en `2026-11-09-config-publicado.tsv`.

## Punto 2, antes de fusionar (todo bien)

- `cepillado_es` / `cepillado_419`: version 2, enabled true, min_build 37, min_build_ios 22. Su v2 lleva `cancion.m4a`
  (la que lee la 0.13), con el mismo sha256 que en la v1 (`21bf1241…` es, `7e219ab3…` 419).
- `nam_es` / `nam_419`: version 1, enabled true, min_build 38, min_build_ios 23.
- `nombres_es`: version 3 (27/13). Hay 80 zips (5 contextos × 16). Contra la v2 cambian **los 16 del vídeo**, y están
  todos en la rama. Huella de la v3 = `298081a9…a24d961`, la del commit `32ef504`, reproducida con `find | sort | sha256sum`.
- `dedicatoria-v1.m4a` está donde dice el informe de la parte 3: en `cepillado_es/2` y `cepillado_419/2`, 20.012 B,
  sha256 `3c3f0572…5ae49` en los dos manifests.
- Las 9 entradas de `audio_paquetes` llevan `enabled` explícito (regla 30). En local, 113 ficheros contra su manifest: 0 fallos.
- La 0.14 (`feature/cepillado-2`) tiene `versionNombresDedicatoria = 3`, así que la dedicatoria espera justo la v3 que sale ahora.

## Punto 4 · producción (HTTP y bytes)

- `cepillado_es/2`: manifest 200 996 · cancion-34-3D.m4a 200 1.607.354 · cancion-79-7B.m4a 200 2.348.654 ·
  cancion.json 200 478 · cancion.m4a 200 2.442.049 · canciones.json 200 1.939 · dedicatoria-v1.m4a 200 20.012
- `cepillado_419/2`: manifest 200 997 · cancion-34-3D.m4a 200 1.607.354 · cancion-79-7B.m4a 200 2.348.654 ·
  cancion.json 200 483 · cancion.m4a 200 2.441.123 · canciones.json 200 1.944 · dedicatoria-v1.m4a 200 20.012
- `nam_es/1`: manifest 200 1.560 · nam-es-v2.m4a 200 3.095.538 · nam.json 200 2.051 · nam-1a…8a.webp 200
  (198.728 · 203.062 · 183.712 · 204.212 · 200.744 · 193.144 · 200.526 · 190.578)
- `nam_419/1`: manifest 200 1.562 · nam-419-v2.m4a 200 3.121.526 · nam.json 200 2.051 · las 8 webp 200, mismos bytes que en es
- `nombres/es/3`: índice (manifest 200 218 · indice.json 200 3.443) y 80 zips con su manifest, todos 200:
  m1 30.270.410 B · m2 39.821.344 · m3 25.354.436 · cumple 22.459.660 · vídeo 16.074.500. Los 16 del vídeo:
  00 1.294.868 · 01 949.435 · 02 748.966 · 03 916.526 · 04 622.866 · 05 1.475.986 · 06 835.277 · 07 1.082.818 ·
  08 869.207 · 09 825.372 · 10 871.026 · 11 1.240.110 · 12 899.740 · 13 1.250.431 · 14 1.147.009 · 15 1.044.863

## Qué falta

- Lo que sigue en el orden de la parte 4: la **política** (`web/privacidad-32-eventos`) antes de enviar a revisión, y la
  **página de la canción** (`web/cancion-014`) cuando la 0.14 / 1.0.17 esté a la venta. Sus URL de audio v2 ya dan 200.
- Builds y subidas de la 0.14.0 (38) / 1.0.17 (23): en el Mac. Hasta entonces, nadie en tienda ve Ñam (min_build 38/23).
- La rama `nube/cepillado-v2` queda en origin tal cual (ya fusionada). Nada me ha bloqueado.
