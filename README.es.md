# ðŸ›¡ï¸ blinda-site

**ðŸ‡§ðŸ‡· [PortuguÃªs](README.md) Â· ðŸ‡ºðŸ‡¸ [English](README.en.md) Â· ðŸ‡ªðŸ‡¸ [EspaÃ±ol](README.es.md)**

[![blinda-site](guia/assets/banner-es.jpg)](https://linnoff88-dev.github.io/

## QuÃ© es

blinda-site es un mÃ©todo para que tu agente de IA (Claude Code o Codex) proteja un sitio sin tocar el sitio que estÃ¡ en lÃ­nea. Lee el cÃ³digo y la configuraciÃ³n del proyecto en tu mÃ¡quina, encuentra lo que estÃ¡ expuesto y arma un plan de correcciones. Cada correcciÃ³n viene con dos niveles de riesgo: quÃ© tan grave es el problema y quÃ© tanto puede romper algo el cambio. Antes de tocar nada, el mÃ©todo exige un respaldo y una simulaciÃ³n local. Para usarlo, basta con tener el proyecto del sitio en tu computadora y un agente abierto en su carpeta.

> **Estado (10/10/2026):** mÃ©todo y roadmap publicados; scripts automÃ¡ticos de la v1 en construcciÃ³n. El guion ya funciona con el agente haciendo las verificaciones.

## ðŸ“– GuÃ­a de uso

GuÃ­a completa (landing + paso a paso): **https://linnoff88-dev.github.io/

## CÃ³mo usarlo hoy

1. Clona el kit: `git clone https://github.com/linnoff88-dev/blinda-site ~/projetos/blinda-site`
2. Abre Claude Code o Codex en la carpeta de **tu sitio** y pide:
   > Sigue ~/projetos/blinda-site/METODO.md, etapas 1 a 3. Solo lectura: no modifiques nada fuera de la carpeta blindagem/. Guarda blindagem/relatorio.md y blindagem/plano.md.
3. Lee el informe y el plan, aprueba los Ã­tems y pide las etapas 4 (respaldo) y 5 (simulaciÃ³n).
4. Con la simulaciÃ³n aprobada, pide las etapas 6 (aplicar) y 7 (verificar).

## Las 7 etapas

Diagnosticar â†’ Informe â†’ Plan â†’ Respaldo â†’ Simular â†’ Aplicar â†’ Verificar. Las tres primeras solo leen.

## Capas

| v | Capa | QuÃ© revisa |
|---|---|---|
| 1 | Encabezados y configuraciÃ³n | CSP, X-Frame-Options, nosniff, Referrer-Policy, HSTS |
| 1 | Dependencias | `npm audit`, versiÃ³n del framework, lÃ­nea aÃºn con soporte |
| 1 | Secretos | `.env` en git/historial, clave en el cÃ³digo, secreto expuesto al navegador |
| 1 | Base de datos y login | Supabase: RLS, `service_role` en el front, API sin sesiÃ³n |
| 2 | CÃ³digo | HTML inyectado, redirect abierto, subida de archivos sin lÃ­mite |

## Archivos

- [`METODO.md`](METODO.md) (en portuguÃ©s) â€” guion que sigue el agente
- [`ROADMAP.md`](ROADMAP.md) (en portuguÃ©s) â€” principios, matriz de riesgo, piloto y estado
- [`modelos/`](modelos/) â€” modelos de informe y plan

## Licencia

MIT. Gratuito y abierto â€” [ARCKHÉ AI](https://ARCKHÉ AI).
