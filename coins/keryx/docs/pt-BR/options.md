# Opções do Keryx

[English](../en/options.md) · **Português (Brasil)** · [Voltar ao Keryx](../../README.pt-BR.md)

Opções que só o Keryx tem. Elas levam dois hífens. Flags do miner levam um (`-device`, `-stats`);
elas estão em [opções do miner](../../../../docs/pt-BR/options.md). Um `--` solto de uma linha
antiga ainda é aceito.

| Plataforma | Onde |
| --- | --- |
| HiveOS | Extra config arguments: `--tier 2` |
| Linux | Na linha do `start-keryx.sh`, por exemplo `--tier 2` |
| Windows | Na linha do `start-keryx.bat`, por exemplo `--tier 2` |

## Opções

| Opção | O que faz |
| --- | --- |
| `--tier 2` | Força um tier em todas as placas que mineram. Não é preciso: o miner escolhe sozinho o maior tier |
| `--tier 2,0,2` | Força um tier por placa, na ordem do `-device` |
| `--headless` | Rig sem monitor: placas de 10 GB mineram um tier maior. Já vem ligado no HiveOS |
| `--inference-gpu N` | Número da placa que responde todos os pedidos de IA. `auto` escolhe por você |
| `--escrow-cert HEX` | Solo, primeira execução: o escrow cert da sua carteira ([mineração solo](solo.md)) |
| `--escrow-claim grpc://IP:PORTA` | Rig de pool: resgata o escrow maduro por este node |
| `--escrow-dir CAMINHO` | Pasta com uma subpasta por carteira (`escrow.key`, `escrow.cert`, `escrow.state.json`) |
| `--models-dir CAMINHO` | Pasta dos modelos |

Uma placa forçada acima do tier dela só minera o tier forçado quando o modelo desse tier cabe na
memória dela; os pedidos de IA dela são respondidos por uma placa maior desse tier na rig, se
houver, ou mais devagar, se não houver. Senão, a placa minera o tier que a memória dela comporta.
O log diz qual tier cada placa minera e por quê.

## Exemplos

| Objetivo | Extra config no HiveOS | `start-keryx.sh` / `start-keryx.bat` |
| --- | --- | --- |
| Tier 0 em todas as placas | `--tier 0` | `--tier 0` na linha de start |
| Placas 1 e 6, tier 1 nas duas | `-device 1,6 --tier 1,1` | `-device 1,6 --tier 1,1` na linha de start |
| Modelos em outro disco | `--models-dir /data/models` | `--models-dir /data/models` na linha de start |
| Rig Linux sem monitor | já vem ligado | `--headless` na linha de start |
