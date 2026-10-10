# Configuração

[English](../en/configuration.md) · **Português (Brasil)** · [Voltar ao README](../../README.pt-BR.md)

## Onde colocar as opções

| Plataforma | Onde |
| --- | --- |
| HiveOS | Flight sheet, **Extra config arguments** |
| Linux | `EXTRA=( ... )` no `run.sh`, ou depois de `./run.sh` na linha de comando |
| Windows | `set "EXTRA=..."` no `start.bat` |

As opções têm dois grupos. **Opções do miner** vêm primeiro. **Opções do Keryx** vêm depois de
`--`. No HiveOS você mesmo escreve o `--`. No `run.sh` e no `start.bat` ele já está lá, então o
`EXTRA` leva só opções do Keryx.

```
--device 1,6 --stats 0.0.0.0:4060 -- --tier 3,3
└──── opções do miner ───────────┘    └ Keryx ┘
```

Caminhos são uma palavra só, sem aspas.

## Opções do miner

| Opção | O que faz | Padrão |
| --- | --- | --- |
| `--device 0,2,5` | Minera só nessas placas, pelos números que o miner mostra | `all` |
| `--pool host:porta` | Pool onde minerar | definido pelo lançador |
| `--node grpc://IP:PORTA` | Seu node, para minerar solo | definido pelo lançador |
| `--user ENDERECO.WORKER` | Usuário da pool, ou o endereço de pagamento no solo | definido pelo lançador |
| `--password x` | Senha da pool | `x` |
| `--stats ENDERECO:PORTA` | Endereço da API de stats (`GET /stats`) | `127.0.0.1:4060` |
| `--log-file CAMINHO` | Onde gravar o `log.txt` | ao lado do miner |

A API de stats não tem senha. `0.0.0.0:4060` abre para qualquer máquina que alcance a rig, então
mantenha ela só na sua rede local.

## Opções do Keryx (depois de `--`)

| Opção | O que faz |
| --- | --- |
| `--tier 2` | Força um tier em todas as placas que mineram |
| `--tier 2,0,2` | Força um tier por placa, na ordem do `--device` |
| `--headless` | Rig sem monitor: placas de 10 e 12 GB mineram um tier maior. Já vem ligado no HiveOS |
| `--inference-gpu N` | Número da placa que responde todos os pedidos de IA. `auto` escolhe por você |
| `--escrow-cert HEX` | Solo, primeira execução: o escrow cert da sua carteira ([solo.md](solo.md)) |
| `--escrow-claim grpc://IP:PORTA` | Rig de pool: resgata o escrow maduro por este node |
| `--no-inference` | Só solo: minera sem responder pedidos de IA. Outra rig no mesmo endereço de pagamento precisa responder os tiers desta, senão o endereço leva strikes |
| `--escrow-dir CAMINHO` | Pasta dos arquivos de escrow |
| `--models-dir CAMINHO` | Pasta dos modelos |

Um tier forçado acima do que a placa consegue minerar pode baixar muito o hashrate dela, ou deixar
a placa parada se nenhuma placa da rig consegue responder os pedidos de IA desse tier. O log diz o
motivo.

## Variáveis de ambiente

| Variável | O que faz |
| --- | --- |
| `FEAR_DATA_DIR` | Linux e Windows: pasta dos modelos e arquivos de escrow. Padrão `data` ao lado do miner |
| `FEAR_SYNC=block` | Menos uso de CPU em rigs com muitas GPUs e poucos núcleos, com cerca de 0,1% a menos de hashrate |
| `FEAR_SYNC=spin` | Um núcleo inteiro de CPU por GPU |

## Exemplos

| Objetivo | Extra config no HiveOS | `run.sh` / `start.bat` |
| --- | --- | --- |
| Só as placas 0 e 1 | `--device 0,1` | `DEVICES="0,1"` |
| Tier 0 em todas as placas | `-- --tier 0` | `EXTRA=(--tier 0)` / `set "EXTRA=--tier 0"` |
| Stats na rede local | `--stats 0.0.0.0:4060` | `STATS="0.0.0.0:4060"` |
| Modelos em outro disco | `-- --models-dir /data/models` | `FEAR_DATA_DIR=/data/fear-miner` |
