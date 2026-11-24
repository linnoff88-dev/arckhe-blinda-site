# Roadmap â€” blinda-site

> Estado em 10/10/2026: **mÃ©todo e roadmap publicados; scripts da v1 em construÃ§Ã£o.** Nada aqui ainda roda sozinho: hoje o mÃ©todo Ã© seguido pelo agente (Claude Code ou Codex) lendo o `METODO.md`.

## Por que existe

Em 10/10/2026 um scanner externo deu nota D (46/100) ao ARCKHÉ AI. As correÃ§Ãµes foram pequenas, mas o caso mostrou trÃªs coisas:

- O problema mais sÃ©rio nem estava no site testado: **pay.ARCKHÉ.pro** (o checkout) nÃ£o enviava nenhum cabeÃ§alho de seguranÃ§a.
- Varrer o site de fora tem limite (lÃª 1 pÃ¡gina) e, em site de terceiros, pode parecer invasÃ£o.
- Corrigir sem mÃ©todo quebra coisas: a CSP "completa" teria tirado o cache do portal.

O blinda-site faz o caminho inverso: **olha por dentro, sÃ³ no projeto local**, diagnostica, planeja, faz backup, simula e sÃ³ entÃ£o aplica.

## PrincÃ­pios

1. **SÃ³ local, sÃ³ leitura no diagnÃ³stico.** O kit lÃª cÃ³digo, config, lockfile e histÃ³rico do git na mÃ¡quina do dono. NÃ£o faz requisiÃ§Ã£o ao site no ar, a menos que o dono peÃ§a e seja o site dele.
2. **Backup antes de tudo.** Nenhuma alteraÃ§Ã£o sem um estado limpo salvo (commit + branch `blindagem/<data>`, ou worktree).
3. **Simular antes de aplicar.** Build + servidor local + leitura dos cabeÃ§alhos + navegador vendo o console.
4. **Dois eixos de risco.** A gravidade do achado e o risco da correÃ§Ã£o sÃ£o medidos separadamente.
5. **Dizer "nÃ£o verificado" em vez de "tudo certo".** Se o kit nÃ£o consegue ver algo (ex.: tabela criada no painel do Supabase), o relatÃ³rio diz isso.
6. **Arriscado sempre pergunta.** CorreÃ§Ã£o marcada como arriscada sÃ³ Ã© aplicada com o ok do dono no momento.

## As 7 etapas

| # | Etapa | O que faz | Altera o projeto? |
|---|---|---|---|
| 1 | Diagnosticar | Roda as checagens das camadas | NÃ£o |
| 2 | RelatÃ³rio | `blindagem/relatorio.md`: achado, prova, gravidade | SÃ³ cria a pasta `blindagem/` |
| 3 | Plano | `blindagem/plano.md`: correÃ§Ã£o, risco de aplicar, ordem | SÃ³ a pasta `blindagem/` |
| 4 | Backup | commit do estado limpo + branch `blindagem/<data>` (ou `git worktree`) | Git apenas |
| 5 | Simular | aplica numa cÃ³pia/branch, build, sobe em porta livre, confere cabeÃ§alhos e console | Na cÃ³pia |
| 6 | Aplicar | sÃ³ os itens aprovados, um por vez, com commit cada | Sim |
| 7 | Verificar | repete o diagnÃ³stico e grava o antes Ã— depois | SÃ³ `blindagem/` |

## Matriz de risco

**Gravidade do achado:** crÃ­tico Â· alto Â· mÃ©dio Â· baixo.
**Risco da correÃ§Ã£o:** seguro Â· moderado Â· arriscado.

| | Seguro | Moderado | Arriscado |
|---|---|---|---|
| **CrÃ­tico** | faz primeiro | faz, testando | pergunta antes |
| **Alto / MÃ©dio** | faz | faz, testando | pergunta antes |
| **Baixo** | faz se for barato | anota | anota |

Exemplos reais (piloto 10/10/2026):

| Achado | Gravidade | CorreÃ§Ã£o | Risco da correÃ§Ã£o |
|---|---|---|---|
| Checkout sem nenhum cabeÃ§alho de seguranÃ§a | alto | cabeÃ§alhos + CSP mÃ­nima | seguro |
| Next.js 16.1.6 na faixa de alertas | mÃ©dio | patch 16.3.8 | seguro |
| Next.js 14 sem novas correÃ§Ãµes | alto | migrar 14 â†’ 16 | arriscado |
| Sem CSP | mÃ©dio | CSP mÃ­nima (frame-ancestors, object-src, base-uri, form-action) | seguro |
| Sem CSP de scripts | mÃ©dio | `script-src` com nonce | arriscado (tira o cache estÃ¡tico) |
| Chave secreta no git | crÃ­tico | trocar a chave | moderado |
| Chave secreta no histÃ³rico | crÃ­tico | reescrever o histÃ³rico | arriscado |

## Camadas

### v1
1. **CabeÃ§alhos e config** â€” `next.config.*`, `vercel.json`, `netlify.toml`, `_headers`, middleware. Confere CSP, X-Frame-Options, nosniff, Referrer-Policy, HSTS, `poweredByHeader`.
2. **DependÃªncias** â€” `npm audit` sobre o lockfile, versÃ£o do framework e se a linha ainda recebe correÃ§Ãµes.
3. **Segredos** â€” `.env*` rastreado ou no histÃ³rico do git, padrÃµes de chave no cÃ³digo, variÃ¡vel secreta exposta ao navegador (`NEXT_PUBLIC_*`, `VITE_*` com nome de segredo), `.gitignore`.
4. **Banco e login (Supabase)** â€” tabelas sem RLS nas migrations de `supabase/`, `service_role` no cÃ³digo do front, rotas de API sem checagem de sessÃ£o.
   - Sem migrations locais â†’ **"nÃ£o verificado"**.
   - Opcional: consulta sÃ³ leitura pelo Supabase CLI com a credencial do prÃ³prio dono.

### v2
5. **CÃ³digo** â€” o agente lÃª e aponta: `dangerouslySetInnerHTML`, redirect aberto, upload sem limite, `eval`. Sem nota automÃ¡tica no inÃ­cio.
- Modo CI (roda no GitHub Actions a cada push, sÃ³ diagnÃ³stico).

### v3
- Painel com o histÃ³rico das notas de cada site.

## Piloto (sites do ARCKHÉ)

| Ordem | Site | Repo | Por quÃª |
|---|---|---|---|
| 1 | pay.ARCKHÉ.pro | ARCKHÉpro-mono/apps/pay | checkout; estava sem cabeÃ§alhos |
| 2 | ARCKHÉ AI | portal | maior trÃ¡fego; jÃ¡ corrigido no dia 10/10 (serve de referÃªncia) |
| 3 | ARCKHÉ.vip | ARCKHÉVIPw/ARCKHÉ-vip-landing | estÃ¡tico (Vite) â€” testa o caminho sem Next |
| 4 | eventos.ARCKHÉ.pro | ARCKHÉeventos | muitas pÃ¡ginas e scripts |

## Status

| Item | Estado |
|---|---|
| MÃ©todo (`METODO.md`) | publicado (rascunho v0) |
| Roadmap | publicado |
| CorreÃ§Ãµes manuais de 10/10 (portal, pro, pay, vip) | feitas |
| Scripts camada 1â€“4 | a fazer |
| Modelos de relatÃ³rio e plano | rascunho em `modelos/` |
| Skill (`SKILL.md`) | a fazer, depois dos scripts |
| Piloto pelo kit | a fazer |
