# ROADMAP - open_source_ai

## MVP

Rede da casa com um agente, um Nó MAIN e um chat. Detalhe em [`MVP.md`](MVP.md).

## ~metade

- Vários agentes na LAN.
- O mesmo modelo em mais de uma máquina, cada uma como instância própria.
- Auto no MAIN por regras: código, documento, conversa.
- Fila quando não há slot, e a conversa permanece na instância enquanto está ativa.
- A interface mostra a máquina e o modelo que atenderam.

## completo

- Projeto marcado como aberto.
- Voluntário escolhe em quais projetos cede recurso.
- Subagente viaja como objeto novo (texto, hash do modelo, id do projeto), não como cópia do chat.
- Filtro de forma conhecida de segredo. Se achar, a tarefa fica na origem.
- Arquivo só sai se foi marcado como exportável.
- A máquina de origem é quem aplica o resultado em banco ou serviço interno.
