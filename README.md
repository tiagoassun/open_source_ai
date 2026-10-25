# open_source_ai

Gerenciador local de modelos. A interface fala só com um Nó MAIN. Cada máquina que cede GPU ou RAM roda um agente sem UI.

- **Tipo:** lateral (software). Não compete com o ranking 1-12 nem com os slots A/B/C.
- **Repo:** [tiagoassun/open_source_ai](https://github.com/tiagoassun/open_source_ai)
- **Intenção (meta-repo):** `/d/Docs Locais/Git/__Confg-Projetos/projetos/18-open_source_ai/`

## Para quê serve

Uma ou várias máquinas da casa servem modelos abertos. O MAIN escolhe a instância com slot livre, guarda o histórico e devolve a resposta na interface. Não há API comercial de chat.

O dono da máquina que executa vê o que chega nela. Segredo não viaja. Voluntário e projeto aberto ficam no horizonte completo, descritos no SPEC do meta-repo.

## O que já existe

Intenção e contrato (`AGENTS.md`, ponte `NEXT-AGENT.md`). Ainda não há processo de agente nem de MAIN.

## Regras rápidas

- Prosa em pt-BR.
- Sem GGUF, `.env` real ou contexto de conversa no git.
- Não chamar o host de serviço só de notebook. Use Servidor Pessoal ou Notebook Servidor quando for o lab; aqui o agente também pode ser um PC virado em servidor.
