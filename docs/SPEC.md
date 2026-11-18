# SPEC - open_source_ai

## Problema

Rodar modelos abertos na própria rede, em uma ou várias máquinas, com uma interface única. A máquina que só serve modelo não tem UI. Quem conversa fala com um Nó MAIN, e o MAIN escolhe onde a geração acontece.

O dono da máquina que executa vê o que chega nela. O desenho parte dessa premissa.

## O que é

Gerenciador local de modelos. Três peças:

| Peça | Onde fica | Função |
| --- | --- | --- |
| Interface | PC de quem conversa | Chat. Só conhece o Nó MAIN. |
| Nó MAIN | Uma máquina da rede da casa | Cadastro, fila, Auto, histórico, montagem do pacote. |
| Agente | Cada Ubuntu, ou PC virado em servidor | Sobe e derruba instância, mede memória, anuncia modelos e slots livres. Sem UI. |

Não é fork do Jan. O produto não fala com API comercial de chat. O motor local é um processo de modelo GGUF sob o agente.

## Conceitos

| Nome | O que é |
| --- | --- |
| Modelo | Identidade dos pesos, o arquivo. Um modelo pode ter N instâncias. |
| Instância | Processo com esses pesos carregados na memória. Os chats compartilham os pesos. |
| Slot | Contexto vivo dentro da instância. Uma instância tem N slots. N sai da memória livre e do tamanho do contexto, medido pelo agente. Não é fixo em 1. |
| Chat | Histórico guardado no Nó MAIN. Enquanto a resposta sai, ocupa um slot. |

A instância não guarda um contexto extra além dos slots. O contexto do chat em geração é o slot. Quando a resposta fecha, o slot pode ser liberado. O histórico continua no MAIN. Na mensagem seguinte, o histórico volta para um slot livre. Se não houver slot, o chat espera na fila. Quem já está gerando não é interrompido.

O MAIN gruda a conversa na instância enquanto ela está ativa. Mudar de máquina no meio do chat é possível: a outra instância relê o histórico.

## Rede da casa

- A interface só abre conexão com o Nó MAIN.
- O agente não recebe conexão vinda do navegador.
- O agente anuncia: hash dos modelos no disco, instâncias carregadas, slots livres, memória.
- O MAIN só manda geração para instância que já tem aquele modelo e tem slot livre.
- O mesmo modelo em duas máquinas são duas instâncias. Dois chats podem gerar ao mesmo tempo, um em cada uma.
- Uma GPU com um modelo grande tende a um slot. Máquina com muita memória unificada pode ter várias instâncias e vários slots. Quem informa o número é o agente, não uma constante no MAIN.
- Trocar o modelo carregado numa GPU derruba a instância atual e carrega a outra. A primeira resposta dessa troca espera o carregamento.

## Auto

O Auto mora no Nó MAIN. Ele olha a tarefa e escolhe o tipo de modelo (código, documento, conversa) e uma instância desse tipo com slot livre. Se todas estiverem ocupadas, a tarefa entra na fila.

No MVP o Auto pode ser regra fixa. Escolha por outro modelo fica fora do MVP.

## Rede de voluntários

Horizonte completo, não MVP.

A mesma peça do agente, com outra regra de entrada. Quem instala marca os projetos que podem usar a máquina. Um instituto publica trabalho com o identificador do projeto.

A execução principal fica na máquina de origem. Um subagente é uma tarefa nova, não uma cópia da conversa. O voluntário devolve o resultado fechado. Não é cada token da mesma frase viajando entre países.

Quem cede a máquina lê o que executa. Trabalho que não pode ser lido fica nas máquinas do próprio instituto. Trabalho aberto só vai para agente que aderiu àquele projeto.

O agente de fora não abre porta na rede de quem pediu. A conexão nasce de dentro para fora. Ele não alcança banco, disco nem serviço interno de quem pediu.

## Pacote que pode sair

O modelo em execução não monta o pacote. O Nó MAIN monta.

Por padrão a tarefa fica nas máquinas da casa. Para ir a um voluntário, as duas coisas são verdade ao mesmo tempo: o projeto está marcado como aberto, e a tarefa nasceu como objeto novo.

Campos do objeto: texto do pedido, hash do modelo, identificador do projeto.

Não entram: ambiente, senha, string de conexão, lista de ferramentas da rede de origem, histórico inteiro do chat.

Arquivo só entra se foi marcado como exportável, um a um.

Antes de enviar, o MAIN recusa o pacote se achar forma conhecida de segredo: IP privado, URL com usuário e senha, chave, token, arquivo de credencial. A tarefa permanece na origem e a interface mostra o motivo.

Segredo escrito como frase comum, sem formato reconhecível, não é pego pelo filtro. Texto liberado para sair é tratado como público.

Quem aplica resultado em banco, arquivo ou API interna é a máquina de origem, depois que a resposta volta.

## Modelos nas máquinas

O peso não viaja dentro da tarefa. O agente anuncia o hash do arquivo que já tem. O MAIN só entrega tarefa para quem tem esse hash e tem slot livre.

Na rede da casa, os modelos são instalados nas máquinas escolhidas. Na rede de voluntários, cada um guarda os modelos públicos que aceitou baixar, uma vez. Fine-tune privado não entra na lista que o voluntário recebe.

## Isolamento

Cada tarefa roda em processo separado, sem o disco pessoal do dono e sem rota para a casa de quem pediu. O contexto fica na RAM do slot e some quando a resposta fecha. O agente não grava o prompt em log.

Isso separa uma tarefa da outra. Não esconde o conteúdo do administrador daquela máquina.

## Fora deste produto

- API comercial de chat
- Fork do Jan
- Esconder o prompt do administrador da máquina que executa
- Partir um único token entre máquinas na internet
- Commitar GGUF, `.env` real ou contexto de conversa
