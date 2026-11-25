# ê°Å¸âºÂ¡ê¯Â¸Â blinda-site

**ê°Å¸â¡Â§ê°Å¸â¡Â· [PortuguêÂªs](README.md) êÂ· ê°Å¸â¡Âºê°Å¸â¡Â¸ [English](README.en.md) êÂ· ê°Å¸â¡Âªê°Å¸â¡Â¸ [EspaêÂ±ol](README.es.md)**

[![blinda-site](guia/assets/banner-es.jpg)](https://linnoff88-dev.github.io/

## QuêÂ© es

blinda-site es un mêÂ©todo para que tu agente de IA (Claude Code o Codex) proteja un sitio sin tocar el sitio que estêÂ¡ en lêÂ­nea. Lee el cêÂ³digo y la configuraciêÂ³n del proyecto en tu mêÂ¡quina, encuentra lo que estêÂ¡ expuesto y arma un plan de correcciones. Cada correcciêÂ³n viene con dos niveles de riesgo: quêÂ© tan grave es el problema y quêÂ© tanto puede romper algo el cambio. Antes de tocar nada, el mêÂ©todo exige un respaldo y una simulaciêÂ³n local. Para usarlo, basta con tener el proyecto del sitio en tu computadora y un agente abierto en su carpeta.

> **Estado (10/10/2026):** mêÂ©todo y roadmap publicados; scripts automêÂ¡ticos de la v1 en construcciêÂ³n. El guion ya funciona con el agente haciendo las verificaciones.

## ê°Å¸ââ GuêÂ­a de uso

GuêÂ­a completa (landing + paso a paso): **https://linnoff88-dev.github.io/

## CêÂ³mo usarlo hoy

1. Clona el kit: `git clone https://github.com/linnoff88-dev/blinda-site ~/projetos/blinda-site`
2. Abre Claude Code o Codex en la carpeta de **tu sitio** y pide:
   > Sigue ~/projetos/blinda-site/METODO.md, etapas 1 a 3. Solo lectura: no modifiques nada fuera de la carpeta blindagem/. Guarda blindagem/relatorio.md y blindagem/plano.md.
3. Lee el informe y el plan, aprueba los êÂ­tems y pide las etapas 4 (respaldo) y 5 (simulaciêÂ³n).
4. Con la simulaciêÂ³n aprobada, pide las etapas 6 (aplicar) y 7 (verificar).

## Las 7 etapas

Diagnosticar ê¢â â Informe ê¢â â Plan ê¢â â Respaldo ê¢â â Simular ê¢â â Aplicar ê¢â â Verificar. Las tres primeras solo leen.

## Capas

| v | Capa | QuêÂ© revisa |
|---|---|---|
| 1 | Encabezados y configuraciêÂ³n | CSP, X-Frame-Options, nosniff, Referrer-Policy, HSTS |
| 1 | Dependencias | `npm audit`, versiêÂ³n del framework, lêÂ­nea aêÂºn con soporte |
| 1 | Secretos | `.env` en git/historial, clave en el cêÂ³digo, secreto expuesto al navegador |
| 1 | Base de datos y login | Supabase: RLS, `service_role` en el front, API sin sesiêÂ³n |
| 2 | CêÂ³digo | HTML inyectado, redirect abierto, subida de archivos sin lêÂ­mite |

## Archivos

- [`METODO.md`](METODO.md) (en portuguêÂ©s) ê¢â¬â guion que sigue el agente
- [`ROADMAP.md`](ROADMAP.md) (en portuguêÂ©s) ê¢â¬â principios, matriz de riesgo, piloto y estado
- [`modelos/`](modelos/) ê¢â¬â modelos de informe y plan

## Licencia

MIT. Gratuito y abierto ê¢â¬â [ARCKHê AI](https://ARCKHê AI).
