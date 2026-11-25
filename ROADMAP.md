# Roadmap ê¢â¬â blinda-site

> Estado em 10/10/2026: **mêÂ©todo e roadmap publicados; scripts da v1 em construêÂ§êÂ£o.** Nada aqui ainda roda sozinho: hoje o mêÂ©todo êÂ© seguido pelo agente (Claude Code ou Codex) lendo o `METODO.md`.

## Por que existe

Em 10/10/2026 um scanner externo deu nota D (46/100) ao ARCKHê AI. As correêÂ§êÂµes foram pequenas, mas o caso mostrou trêÂªs coisas:

- O problema mais sêÂ©rio nem estava no site testado: **pay.ARCKHê.pro** (o checkout) nêÂ£o enviava nenhum cabeêÂ§alho de seguranêÂ§a.
- Varrer o site de fora tem limite (lêÂª 1 pêÂ¡gina) e, em site de terceiros, pode parecer invasêÂ£o.
- Corrigir sem mêÂ©todo quebra coisas: a CSP "completa" teria tirado o cache do portal.

O blinda-site faz o caminho inverso: **olha por dentro, sêÂ³ no projeto local**, diagnostica, planeja, faz backup, simula e sêÂ³ entêÂ£o aplica.

## PrincêÂ­pios

1. **SêÂ³ local, sêÂ³ leitura no diagnêÂ³stico.** O kit lêÂª cêÂ³digo, config, lockfile e histêÂ³rico do git na mêÂ¡quina do dono. NêÂ£o faz requisiêÂ§êÂ£o ao site no ar, a menos que o dono peêÂ§a e seja o site dele.
2. **Backup antes de tudo.** Nenhuma alteraêÂ§êÂ£o sem um estado limpo salvo (commit + branch `blindagem/<data>`, ou worktree).
3. **Simular antes de aplicar.** Build + servidor local + leitura dos cabeêÂ§alhos + navegador vendo o console.
4. **Dois eixos de risco.** A gravidade do achado e o risco da correêÂ§êÂ£o sêÂ£o medidos separadamente.
5. **Dizer "nêÂ£o verificado" em vez de "tudo certo".** Se o kit nêÂ£o consegue ver algo (ex.: tabela criada no painel do Supabase), o relatêÂ³rio diz isso.
6. **Arriscado sempre pergunta.** CorreêÂ§êÂ£o marcada como arriscada sêÂ³ êÂ© aplicada com o ok do dono no momento.

## As 7 etapas

| # | Etapa | O que faz | Altera o projeto? |
|---|---|---|---|
| 1 | Diagnosticar | Roda as checagens das camadas | NêÂ£o |
| 2 | RelatêÂ³rio | `blindagem/relatorio.md`: achado, prova, gravidade | SêÂ³ cria a pasta `blindagem/` |
| 3 | Plano | `blindagem/plano.md`: correêÂ§êÂ£o, risco de aplicar, ordem | SêÂ³ a pasta `blindagem/` |
| 4 | Backup | commit do estado limpo + branch `blindagem/<data>` (ou `git worktree`) | Git apenas |
| 5 | Simular | aplica numa cêÂ³pia/branch, build, sobe em porta livre, confere cabeêÂ§alhos e console | Na cêÂ³pia |
| 6 | Aplicar | sêÂ³ os itens aprovados, um por vez, com commit cada | Sim |
| 7 | Verificar | repete o diagnêÂ³stico e grava o antes êâ depois | SêÂ³ `blindagem/` |

## Matriz de risco

**Gravidade do achado:** crêÂ­tico êÂ· alto êÂ· mêÂ©dio êÂ· baixo.
**Risco da correêÂ§êÂ£o:** seguro êÂ· moderado êÂ· arriscado.

| | Seguro | Moderado | Arriscado |
|---|---|---|---|
| **CrêÂ­tico** | faz primeiro | faz, testando | pergunta antes |
| **Alto / MêÂ©dio** | faz | faz, testando | pergunta antes |
| **Baixo** | faz se for barato | anota | anota |

Exemplos reais (piloto 10/10/2026):

| Achado | Gravidade | CorreêÂ§êÂ£o | Risco da correêÂ§êÂ£o |
|---|---|---|---|
| Checkout sem nenhum cabeêÂ§alho de seguranêÂ§a | alto | cabeêÂ§alhos + CSP mêÂ­nima | seguro |
| Next.js 16.1.6 na faixa de alertas | mêÂ©dio | patch 16.3.8 | seguro |
| Next.js 14 sem novas correêÂ§êÂµes | alto | migrar 14 ê¢â â 16 | arriscado |
| Sem CSP | mêÂ©dio | CSP mêÂ­nima (frame-ancestors, object-src, base-uri, form-action) | seguro |
| Sem CSP de scripts | mêÂ©dio | `script-src` com nonce | arriscado (tira o cache estêÂ¡tico) |
| Chave secreta no git | crêÂ­tico | trocar a chave | moderado |
| Chave secreta no histêÂ³rico | crêÂ­tico | reescrever o histêÂ³rico | arriscado |

## Camadas

### v1
1. **CabeêÂ§alhos e config** ê¢â¬â `next.config.*`, `vercel.json`, `netlify.toml`, `_headers`, middleware. Confere CSP, X-Frame-Options, nosniff, Referrer-Policy, HSTS, `poweredByHeader`.
2. **DependêÂªncias** ê¢â¬â `npm audit` sobre o lockfile, versêÂ£o do framework e se a linha ainda recebe correêÂ§êÂµes.
3. **Segredos** ê¢â¬â `.env*` rastreado ou no histêÂ³rico do git, padrêÂµes de chave no cêÂ³digo, variêÂ¡vel secreta exposta ao navegador (`NEXT_PUBLIC_*`, `VITE_*` com nome de segredo), `.gitignore`.
4. **Banco e login (Supabase)** ê¢â¬â tabelas sem RLS nas migrations de `supabase/`, `service_role` no cêÂ³digo do front, rotas de API sem checagem de sessêÂ£o.
   - Sem migrations locais ê¢â â **"nêÂ£o verificado"**.
   - Opcional: consulta sêÂ³ leitura pelo Supabase CLI com a credencial do prêÂ³prio dono.

### v2
5. **CêÂ³digo** ê¢â¬â o agente lêÂª e aponta: `dangerouslySetInnerHTML`, redirect aberto, upload sem limite, `eval`. Sem nota automêÂ¡tica no inêÂ­cio.
- Modo CI (roda no GitHub Actions a cada push, sêÂ³ diagnêÂ³stico).

### v3
- Painel com o histêÂ³rico das notas de cada site.

## Piloto (sites do ARCKHê)

| Ordem | Site | Repo | Por quêÂª |
|---|---|---|---|
| 1 | pay.ARCKHê.pro | ARCKHêpro-mono/apps/pay | checkout; estava sem cabeêÂ§alhos |
| 2 | ARCKHê AI | portal | maior trêÂ¡fego; jêÂ¡ corrigido no dia 10/10 (serve de referêÂªncia) |
| 3 | ARCKHê.vip | ARCKHêVIPw/ARCKHê-vip-landing | estêÂ¡tico (Vite) ê¢â¬â testa o caminho sem Next |
| 4 | eventos.ARCKHê.pro | ARCKHêeventos | muitas pêÂ¡ginas e scripts |

## Status

| Item | Estado |
|---|---|
| MêÂ©todo (`METODO.md`) | publicado (rascunho v0) |
| Roadmap | publicado |
| CorreêÂ§êÂµes manuais de 10/10 (portal, pro, pay, vip) | feitas |
| Scripts camada 1ê¢â¬â4 | a fazer |
| Modelos de relatêÂ³rio e plano | rascunho em `modelos/` |
| Skill (`SKILL.md`) | a fazer, depois dos scripts |
| Piloto pelo kit | a fazer |
