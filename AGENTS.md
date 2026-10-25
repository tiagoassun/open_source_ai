# AGENTS.md - open_source_ai

## Contexto

- **Lateral** (fora do ranking 1-12): não compete com backlog de produto nem com slots A/B/C.
- Path: `/d/Docs Locais/Git/open_source_ai`
- Intenção: `/d/Docs Locais/Git/__Confg-Projetos/projetos/18-open_source_ai/`
- Gerenciador local de modelos. Interface só no Nó MAIN. Agente headless nas máquinas que cedem recurso.
- Não é fork do Jan. Sem API comercial de chat.
- Agents Window pode implementar com pedido explícito, sem roubar OSDP.

## Leitura obrigatória

1. `/d/Docs Locais/Git/__Confg-Projetos/PRIORIDADE.md` + `WIP.md` + `CONVENCOES.md`
2. `/d/Docs Locais/Git/__Confg-Projetos/LINGUA-PT-BR.md` + `FAZER-CERTO-PRIMEIRA-VEZ.md`
3. Pasta do meta `projetos/18-open_source_ai/`: `AGENTS.md`, `NEXT-AGENT.md`, `SPEC.md`, `MVP.md`, `ROADMAP.md`
4. Neste repo: `NEXT-AGENT.md` (ponte) e `README.md`

## Git

```text
feature/<descricao-kebab> -> dev -> hml -> main
```

- Trabalho novo em `feature/...` a partir de `dev`.
- Preview via PR para `dev` (Agents OK). Homologação via PR `dev` -> `hml` (só humano).
- Estável via PR `hml` -> `main` (só humano).
- Conventional commits.
- **Proibido** `workflow_run` disparado a partir de `main` para encadear deploy.
- Não commitar GGUF, `.env` real, secrets nem contexto de conversa.

## Homologação

- O MVP fala na LAN. Não depende de stack no Portainer para nascer.
- Se um dia houver URL de lab: DEV `{slug}-dev.tiagoassun.com.br`, HML `{slug}-hml.tiagoassun.com.br`, PRD `{slug}.tiagoassun.com.br`.
- Host de lab, quando existir: **Servidor Pessoal** / **Notebook Servidor**. Nunca só "notebook".

## Notas do produto

- Sem lote na feature e no Cloud.
- Trabalhar **só** na branch designada e **não** criar outras branches.
- Premissa: o administrador da máquina que executa vê contexto, tarefa e resposta.
- Slot não é constante. O agente mede memória livre e informa o N.

## Ambiente DEV (Agents Window / Cloud Agent)

- Fluxo: `feature/*` -> PR -> `dev` (Agents podem abrir/aprovar/mergear) -> PR -> `hml` / `main` (**só humano**).
- Na `feature/*` e no Cloud da missão: editar, testar, commit, push e PR/merge para `dev` **sem** pedir lote a cada passo (brief/pedido da missão já autoriza). Ver `__Confg-Projetos/AGENTS.md`.
- Branch **designada**: trabalhar **somente** na `feature/...` nomeada na missão / `NEXT-AGENT.md`. Se não existir, criar **apenas essa** a partir de `origin/dev`. **Proibido** criar outras branches. Sem nome no brief: pedir ao humano.
- **Proibido** para Agents: merge em `hml` ou `main`.
