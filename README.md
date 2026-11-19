# ðŸ›¡ï¸ blinda-site

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


**ðŸ‡§ðŸ‡· [PortuguÃªs](README.md) Â· ðŸ‡ºðŸ‡¸ [English](README.en.md) Â· ðŸ‡ªðŸ‡¸ [EspaÃ±ol](README.es.md)**

[![blinda-site](guia/assets/banner.jpg)](https://inematds.github.io/blinda-site/guia/)

## O que Ã©

O blinda-site Ã© um mÃ©todo para o seu agente de IA (Claude Code ou Codex) proteger um site sem tocar no site que estÃ¡ no ar. Ele lÃª o cÃ³digo e as configuraÃ§Ãµes do projeto na sua mÃ¡quina, encontra o que estÃ¡ exposto e monta um plano de correÃ§Ãµes. Cada correÃ§Ã£o vem com dois nÃ­veis de risco: o quanto o problema Ã© grave e o quanto a mudanÃ§a pode quebrar algo. Antes de mexer, o mÃ©todo exige backup e uma simulaÃ§Ã£o local. Para usar, basta ter o projeto do site no computador e um agente aberto na pasta dele.

> **Estado (10/10/2026):** mÃ©todo e roadmap publicados; scripts automÃ¡ticos da v1 em construÃ§Ã£o. O roteiro jÃ¡ funciona com o agente fazendo as checagens.

## ðŸ“– Guia de uso

Guia completo (landing + passo a passo): **https://inematds.github.io/blinda-site/guia/**

## Como usar hoje

1. Clone o kit: `git clone https://github.com/inematds/blinda-site ~/projetos/blinda-site`
2. Abra o Claude Code ou o Codex na pasta do **seu site** e peÃ§a:
   > Siga ~/projetos/blinda-site/METODO.md, etapas 1 a 3. SÃ³ leitura: nÃ£o altere nada fora da pasta blindagem/. Grave blindagem/relatorio.md e blindagem/plano.md.
3. Leia o relatÃ³rio e o plano, aprove os itens e peÃ§a as etapas 4 (backup) e 5 (simulaÃ§Ã£o).
4. Com a simulaÃ§Ã£o aprovada, peÃ§a as etapas 6 (aplicar) e 7 (verificar).

## As 7 etapas

Diagnosticar â†’ RelatÃ³rio â†’ Plano â†’ Backup â†’ Simular â†’ Aplicar â†’ Verificar. As trÃªs primeiras sÃ³ leem.

## Camadas

| v | Camada | O que olha |
|---|---|---|
| 1 | CabeÃ§alhos e config | CSP, X-Frame-Options, nosniff, Referrer-Policy, HSTS |
| 1 | DependÃªncias | `npm audit`, versÃ£o do framework, linha ainda suportada |
| 1 | Segredos | `.env` no git/histÃ³rico, chave no cÃ³digo, segredo exposto ao navegador |
| 1 | Banco e login | Supabase: RLS, `service_role` no front, API sem sessÃ£o |
| 2 | CÃ³digo | HTML injetado, redirect aberto, upload sem limite |

## Arquivos

- [`METODO.md`](METODO.md) â€” roteiro que o agente segue
- [`ROADMAP.md`](ROADMAP.md) â€” princÃ­pios, matriz de risco, piloto e status
- [`modelos/`](modelos/) â€” modelos de relatÃ³rio e plano

## LicenÃ§a

MIT. Gratuito e aberto â€” [INEMA.CLUB](https://inema.club).

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>