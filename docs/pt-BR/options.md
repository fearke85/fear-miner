# Opções do miner

[English](../en/options.md) · **Português (Brasil)** · [Voltar ao README](../../README.pt-BR.md)

Opções que funcionam igual para todas as moedas. As opções de cada moeda estão na página dela:
[Keryx](../../coins/keryx/docs/pt-BR/options.md), [Vela](../../coins/vela/README.pt-BR.md#opções-do-vela).

## Onde colocar as opções

| Plataforma | Onde |
| --- | --- |
| HiveOS | Flight sheet, **Extra config arguments** |
| Linux | Na linha do `start-<moeda>.sh` da moeda |
| Windows | Na linha do `start-<moeda>.bat` da moeda |

Flags do miner levam um hífen. Flags da moeda levam dois. A ordem não importa: tudo fica na
mesma linha. Um `--` solto de uma linha antiga ainda é aceito e ignorado.

```
-device 1,6 -stats 0.0.0.0:4060 --tier 2
└──── flags do miner ──────────┘ └ moeda ┘
```

Caminhos são uma palavra só, sem aspas.

## Opções

| Opção | O que faz | Padrão |
| --- | --- | --- |
| `-coin keryxhash` | Moeda a minerar: `keryxhash` ou `vela`. Igual ao positional `keryxhash`; os dois juntos, vale `-coin` | obrigatório |
| `-device 0,2,5` | Minera só nessas placas, pelos números que o miner mostra | `all` |
| `-pool host:porta` | Pool onde minerar: `host:porta`, `stratum+tcp://host:porta` (simples) ou `stratum+ssl://host:porta` (criptografado) | definido pelo lançador |
| `-node grpc://IP:PORTA` | Seu node, para minerar solo | definido pelo lançador |
| `-wallet ENDERECO` | Endereço de pagamento. `-address` é o mesmo campo; vale o último | definido pelo lançador |
| `-worker NOME` | Nome da rig. Substitui o trecho da carteira depois do primeiro `.` | |
| `-user ENDERECO.WORKER` | Usuário completo da pool. Prefira `-wallet` e `-worker` | definido pelo lançador |
| `-password x` | Senha da pool | `x` |
| `-stats ENDERECO:PORTA` | Endereço da API de stats (`GET /stats`) | `127.0.0.1:4060` |
| `-log-file CAMINHO` | Onde gravar o `log.txt` | ao lado do miner |

Dois hífens ainda funcionam nestas flags (`--pool`, `--device`). Flags da moeda não: `--escrow-dir`
é flag da moeda, `-escrow-dir` é recusado.

A API de stats não tem senha. `0.0.0.0:4060` abre para qualquer máquina que alcance a rig, então
mantenha ela só na sua rede local.

## Overclock

O miner ajusta clocks e ventoinhas por conta própria, no Linux e no Windows, pelo driver da
NVIDIA (NVML).

| Opção | O que faz |
| --- | --- |
| `-cclock 275` | Offset do clock do core em MHz. Negativo diminui: `-cclock -100` |
| `-mclock 1000` | Offset do clock da memória em MHz. Negativo diminui: `-mclock -500`. O clock de memória que o miner mostra muda metade do valor |
| `-lock-cclock 2610` | Trava o clock do core nesse MHz |
| `-lock-mclock 810` | Trava o clock da memória nesse MHz (RTX 30 em diante) |
| `-fan 75` | Velocidade da ventoinha em %, todas as ventoinhas da placa |

Um valor só vale para todas as placas. Placas diferentes recebem uma lista, um valor por placa,
na ordem do `-device`; `*` deixa aquela placa como está:

```
-device 0,1,2 -cclock 275,250,* -lock-cclock 2610,1350,1350 -fan 75
```

Aqui a placa 0 recebe +275 e 2610 MHz, a placa 1 +250 e 1350 MHz, a placa 2 mantém o offset e
recebe 1350 MHz, e todas as ventoinhas ficam em 75%. Sem `-device`, a lista segue os números de
placa que o miner mostra: 0, 1, 2…

- Uma lista com a quantidade errada de valores não muda nada em nenhuma placa, e o log avisa.
  Se uma placa cair do barramento, os números mudam; aí o miner minera no stock em vez de
  colocar o clock de uma placa em outra.
- No Linux precisa de root ([com sudo](linux.md#com-sudo)) e no Windows de **Executar como
  administrador**. O HiveOS já roda o miner como root.
- Ao sair (Ctrl+C, ou fechando a tela), o miner desfaz o que mudou: offsets 0, clocks
  destravados, ventoinhas no automático. Se o processo for morto, os ajustes ficam até o
  próximo start.
- No HiveOS, use estas flags ou a página de OC para uma placa, não as duas: a saída do miner
  desfaz o lock e a ventoinha do Hive até o Hive aplicar o perfil de novo.

## Overclock automático

Por enquanto só no Keryx; as outras moedas mineram com o clock que a placa já tem.

| Opção | O que faz |
| --- | --- |
| `-auto-oc` | O miner encontra o clock do core, o undervolt, a memória e a ventoinha de cada placa, e guarda |
| `-eco` | Com `-auto-oc`, o padrão: o melhor hashrate por watt, placas a no máximo 70 °C |
| `-boost` | Com `-auto-oc`: mais hashrate enquanto a energia extra compensa, placas a no máximo 75 °C |
| `-retune` | Com `-auto-oc`: ajusta todas as placas de novo. `-retune 1,3` só as placas 1 e 3 |

```
-auto-oc              eco em todas as placas
-auto-oc -boost       boost em todas as placas
-auto-oc -retune 2    eco, e ajusta a placa 2 de novo
```

- Todas as placas são ajustadas ao mesmo tempo; a rig inteira leva uns 30 a 45 minutos. O
  hashrate varia enquanto isso; a TUI mostra `AUTO OC eco · tuning 4 of 4` (placas ainda em
  ajuste) e um `~` ao lado do hashrate de cada placa em medição. Deixe a rig minerando até o
  cabeçalho mostrar `tuned`.
- O resultado fica salvo por placa na pasta de dados da moeda (`keryx/auto-oc.json`), e o
  próximo start já usa. Uma placa nova ou um driver novo é ajustado de novo sozinho.
- O miner controla a ventoinha. Com `-fan`, a placa fica na sua ventoinha e o ajuste trabalha
  com ela. Acima do limite de temperatura a ventoinha sobe primeiro; só com ela no máximo o
  clock desce.
- Um ajuste que derrubou o miner ou devolveu resultados errados nunca é tentado de novo. O
  ajuste pode reiniciar o miner algumas vezes; é esperado.
- Uma placa com `-cclock`, `-mclock`, `-lock-cclock` ou `-lock-mclock` fica por sua conta e
  aparece como `manual`; as outras são ajustadas.
- Enquanto uma placa responde a um pedido de IA, ela roda nos clocks do driver; assim que volta
  a minerar, o overclock (seu ou do `-auto-oc`) volta. Só os clocks que o miner definiu são
  trocados; uma placa só com `-fan`, ou com OC do Hive, fica como está.
- Isso vale também para `-boost` e clocks manuais: um overclock agressivo pode derrubar a
  geração de tokens, então os clocks do driver são a base segura para toda resposta.
- Tire o `-retune` quando o ajuste terminar: com ele, todo start ajusta de novo.
- As mesmas permissões das flags acima: root no Linux, **Executar como administrador** no
  Windows.
- **HiveOS:** com `-auto-oc`, deixe o OC e o autofan da rig vazios no Hive. Os dois mexeriam
  nos mesmos clocks e ventoinhas, e vale o último aplicado.

## Variáveis de ambiente

| Variável | O que faz |
| --- | --- |
| `FEAR_DATA_DIR` | Linux e Windows: pasta dos dados que o miner guarda. Padrão `keryx` (Vela: `vela`) ao lado do miner |
| `FEAR_SYNC=block` | Keryx: menos uso de CPU em rigs com muitas GPUs e poucos núcleos, com cerca de 0,1% a menos de hashrate |
| `FEAR_SYNC=spin` | Keryx: um núcleo inteiro de CPU por GPU. O Vela não lê `FEAR_SYNC` |

## Exemplos

| Objetivo | Extra config no HiveOS | `start-<moeda>.sh` / `start-<moeda>.bat` |
| --- | --- | --- |
| Só as placas 0 e 1 | `-device 0,1` | `-device 0,1` na linha de start |
| Stats na rede local | `-stats 0.0.0.0:4060` | `-stats 0.0.0.0:4060` na linha de start |
| Dados em outro disco | | `FEAR_DATA_DIR=/data/fear-miner` |
| Overclock igual em todas as placas | `-cclock 275 -lock-cclock 2610 -lock-mclock 810 -fan 75` | o mesmo, na linha de start |
