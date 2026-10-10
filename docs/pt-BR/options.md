# Opções do miner

[English](../en/options.md) · **Português (Brasil)** · [Voltar ao README](../../README.pt-BR.md)

Opções que funcionam igual para todas as moedas. As opções de cada moeda estão na página dela:
[Keryx](../../coins/keryx/docs/pt-BR/options.md).

## Onde colocar as opções

| Plataforma | Onde |
| --- | --- |
| HiveOS | Flight sheet, **Extra config arguments** |
| Linux | `run.sh`: `DEVICES`, `STATS` e `EXTRA`, ou depois de `./run.sh` na linha de comando |
| Windows | `start.bat`: `DEVICES`, `STATS` e `EXTRA` |

**Opções do miner** vêm primeiro. **Opções da moeda** vêm depois de `--`. No HiveOS você mesmo
escreve o `--`. No `run.sh` e no `start.bat` ele já está lá, então o `EXTRA` leva só opções da
moeda.

```
--device 1,6 --stats 0.0.0.0:4060 -- <opções da moeda>
└──── opções do miner ───────────┘
```

Caminhos são uma palavra só, sem aspas.

## Opções

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

## Variáveis de ambiente

| Variável | O que faz |
| --- | --- |
| `FEAR_DATA_DIR` | Linux e Windows: pasta dos dados que o miner guarda. Padrão `data` ao lado do miner |
| `FEAR_SYNC=block` | Menos uso de CPU em rigs com muitas GPUs e poucos núcleos, com cerca de 0,1% a menos de hashrate |
| `FEAR_SYNC=spin` | Um núcleo inteiro de CPU por GPU |

## Exemplos

| Objetivo | Extra config no HiveOS | `run.sh` / `start.bat` |
| --- | --- | --- |
| Só as placas 0 e 1 | `--device 0,1` | `DEVICES="0,1"` |
| Stats na rede local | `--stats 0.0.0.0:4060` | `STATS="0.0.0.0:4060"` |
| Dados em outro disco | | `FEAR_DATA_DIR=/data/fear-miner` |
