# Opções do Keryx

[English](../en/options.md) · **Português (Brasil)** · [Voltar ao Keryx](../../README.pt-BR.md)

Opções que só o Keryx tem. Elas vão depois de `--`. As opções de todas as moedas (`--device`,
`--stats` e outras) estão em [opções do miner](../../../../docs/pt-BR/options.md).

| Plataforma | Onde |
| --- | --- |
| HiveOS | Extra config arguments, depois de `--`: `-- --tier 2` |
| Linux | `EXTRA=(--tier 2)` no `run.sh` |
| Windows | `set "EXTRA=--tier 2"` no `start.bat` |

## Opções

| Opção | O que faz |
| --- | --- |
| `--tier 2` | Força um tier em todas as placas que mineram. Não é preciso: o miner escolhe sozinho o maior tier |
| `--tier 2,0,2` | Força um tier por placa, na ordem do `--device` |
| `--headless` | Rig sem monitor: placas de 10 e 12 GB mineram um tier maior. Já vem ligado no HiveOS |
| `--inference-gpu N` | Número da placa que responde todos os pedidos de IA. `auto` escolhe por você |
| `--escrow-cert HEX` | Solo, primeira execução: o escrow cert da sua carteira ([mineração solo](solo.md)) |
| `--escrow-claim grpc://IP:PORTA` | Rig de pool: resgata o escrow maduro por este node |
| `--escrow-dir CAMINHO` | Pasta dos arquivos de escrow |
| `--models-dir CAMINHO` | Pasta dos modelos |

Um tier forçado acima do que a placa consegue minerar pode baixar muito o hashrate dela, ou deixar
a placa parada se nenhuma placa da rig consegue responder os pedidos de IA desse tier. O log diz o
motivo.

## Exemplos

| Objetivo | Extra config no HiveOS | `run.sh` / `start.bat` |
| --- | --- | --- |
| Tier 0 em todas as placas | `-- --tier 0` | `EXTRA=(--tier 0)` / `set "EXTRA=--tier 0"` |
| Placas 1 e 6, tier 3 nas duas | `--device 1,6 -- --tier 3,3` | `DEVICES="1,6"` e `EXTRA=(--tier 3,3)` |
| Modelos em outro disco | `-- --models-dir /data/models` | `EXTRA=(--models-dir /data/models)` |
| Rig Linux sem monitor | já vem ligado | `EXTRA=(--headless)` |
