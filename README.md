# ê°Å¸âºÂ¡ê¯Â¸Â blinda-site

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


**ê°Å¸â¡Â§ê°Å¸â¡Â· [PortuguêÂªs](README.md) êÂ· ê°Å¸â¡Âºê°Å¸â¡Â¸ [English](README.en.md) êÂ· ê°Å¸â¡Âªê°Å¸â¡Â¸ [EspaêÂ±ol](README.es.md)**

[![blinda-site](guia/assets/banner.jpg)](https://linnoff88-dev.github.io/

## O que êÂ©

O blinda-site êÂ© um mêÂ©todo para o seu agente de IA (Claude Code ou Codex) proteger um site sem tocar no site que estêÂ¡ no ar. Ele lêÂª o cêÂ³digo e as configuraêÂ§êÂµes do projeto na sua mêÂ¡quina, encontra o que estêÂ¡ exposto e monta um plano de correêÂ§êÂµes. Cada correêÂ§êÂ£o vem com dois nêÂ­veis de risco: o quanto o problema êÂ© grave e o quanto a mudanêÂ§a pode quebrar algo. Antes de mexer, o mêÂ©todo exige backup e uma simulaêÂ§êÂ£o local. Para usar, basta ter o projeto do site no computador e um agente aberto na pasta dele.

> **Estado (10/10/2026):** mêÂ©todo e roadmap publicados; scripts automêÂ¡ticos da v1 em construêÂ§êÂ£o. O roteiro jêÂ¡ funciona com o agente fazendo as checagens.

## ê°Å¸ââ Guia de uso

Guia completo (landing + passo a passo): **https://linnoff88-dev.github.io/

## Como usar hoje

1. Clone o kit: `git clone https://github.com/linnoff88-dev/blinda-site ~/projetos/blinda-site`
2. Abra o Claude Code ou o Codex na pasta do **seu site** e peêÂ§a:
   > Siga ~/projetos/blinda-site/METODO.md, etapas 1 a 3. SêÂ³ leitura: nêÂ£o altere nada fora da pasta blindagem/. Grave blindagem/relatorio.md e blindagem/plano.md.
3. Leia o relatêÂ³rio e o plano, aprove os itens e peêÂ§a as etapas 4 (backup) e 5 (simulaêÂ§êÂ£o).
4. Com a simulaêÂ§êÂ£o aprovada, peêÂ§a as etapas 6 (aplicar) e 7 (verificar).

## As 7 etapas

Diagnosticar ê¢â â RelatêÂ³rio ê¢â â Plano ê¢â â Backup ê¢â â Simular ê¢â â Aplicar ê¢â â Verificar. As trêÂªs primeiras sêÂ³ leem.

## Camadas

| v | Camada | O que olha |
|---|---|---|
| 1 | CabeêÂ§alhos e config | CSP, X-Frame-Options, nosniff, Referrer-Policy, HSTS |
| 1 | DependêÂªncias | `npm audit`, versêÂ£o do framework, linha ainda suportada |
| 1 | Segredos | `.env` no git/histêÂ³rico, chave no cêÂ³digo, segredo exposto ao navegador |
| 1 | Banco e login | Supabase: RLS, `service_role` no front, API sem sessêÂ£o |
| 2 | CêÂ³digo | HTML injetado, redirect aberto, upload sem limite |

## Arquivos

- [`METODO.md`](METODO.md) ê¢â¬â roteiro que o agente segue
- [`ROADMAP.md`](ROADMAP.md) ê¢â¬â princêÂ­pios, matriz de risco, piloto e status
- [`modelos/`](modelos/) ê¢â¬â modelos de relatêÂ³rio e plano

## LicenêÂ§a

MIT. Gratuito e aberto ê¢â¬â [ARCKHê AI](https://ARCKHê AI).

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>