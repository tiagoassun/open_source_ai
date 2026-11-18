# MVP - open_source_ai

## Fatia

Rede da casa, uma máquina servindo modelo e um Nó MAIN. Um chat. Um modelo já instalado nessa máquina. Sem voluntário, sem projeto aberto, sem Auto entre vários tipos.

## Entregáveis

1. Agente headless: anuncia o hash do modelo no disco, sobe uma instância e informa quantos slots cabem agora.
2. Nó MAIN: guarda o histórico do chat, manda a geração para essa instância e libera o slot quando a resposta fecha.
3. Fila de um slot: o segundo envio espera o primeiro terminar, sem cortar a resposta em curso.
4. Interface mínima que só fala com o MAIN: uma conversa, a resposta voltando, e qual instância atendeu.
5. Sem caminho para API comercial de chat. Não existe tela nem cliente para isso.

## Critérios de aceite

- [ ] O agente sobe sem UI e o MAIN enxerga modelo, instância e slots livres.
- [ ] Um chat gera na instância e o histórico fica no MAIN depois que o slot libera.
- [ ] Com o único slot ocupado, o próximo envio espera.
- [ ] A interface não oferece provedor de nuvem.
- [ ] GGUF, `.env` real e texto de conversa não entram no git.

## Estimativa

Primeira fatia utilizável na LAN, antes de segunda máquina e antes de voluntário.
