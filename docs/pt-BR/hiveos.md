# HiveOS

[English](../en/hiveos.md) · **Português (Brasil)** · [Voltar ao README](../../README.pt-BR.md)

## Antes de começar

- HiveOS com a imagem Ubuntu 22.04 (jammy). A imagem 20.04 não é suportada.
- Driver NVIDIA 580 ou mais novo. Atualize pelo painel do HiveOS ou com `nvidia-driver-update`.
- Placas: Turing ou mais novas. Veja [qual tier sua placa minera](../../README.pt-BR.md#qual-tier-minha-placa-minera).
- Espaço em disco para o modelo de cada tier minerado. Um pendrive de 32 GB comporta o tier 2.

## Flight sheet

Crie um flight sheet com o miner **Custom** e preencha:

| Campo | Valor |
| --- | --- |
| Miner name | `fear-miner` |
| Installation URL | `https://github.com/fearke85/fear-miner/releases/download/v0.0.31/fear-miner-0.0.31.tar.gz` |
| Hash algorithm | `keryxhash` |
| Wallet and worker template | Pool: `%WAL%.%WORKER_NAME%`. Solo: `%WAL%` |
| Pool URL | Pool: `stratum+tcp://krx.suprnova.cc:4404`. Solo: `grpc://IP:PORTA` do seu node |
| Password | `x`, ou a senha da pool |
| Extra config arguments | Deixe vazio, ou veja abaixo |

A carteira é o seu endereço Keryx, `keryx:...`. A Pool URL precisa do prefixo: `stratum+tcp://`
para pool, `grpc://` para node. Um `host:porta` sem prefixo ou com `http://` é recusado.

Aplique o flight sheet. A primeira execução baixa o modelo, o que leva alguns minutos. O painel
mostra o hashrate quando as placas começam a minerar.

Para minerar solo, leia antes o [solo.md](solo.md): a primeira execução pede um passo na carteira.

## Instalar pelo console da rig

```
/hive/miners/custom/custom-get https://github.com/fearke85/fear-miner/releases/download/v0.0.31/fear-miner-0.0.31.tar.gz
```

Adicione `-f` para reinstalar.

## Atualizar para uma versão nova

Troque a versão na Installation URL, nos dois lugares: em `v0.0.31` e em
`fear-miner-0.0.31.tar.gz`. O resto do flight sheet continua igual. Com a URL antiga, a rig
continua instalando a versão antiga.

Modelos, arquivos de escrow e o log ficam em `/var/lib/fear-miner` entre atualizações e
reinstalações.

## Extra config arguments

Opções do miner vão antes de `--`, opções do Keryx depois. Exemplos comuns:

| O quê | Extra config arguments |
| --- | --- |
| Minerar só nas placas 0 e 2 | `--device 0,2` |
| Forçar tier 2 em todas as placas | `-- --tier 2` |
| Placas 1 e 6, tier 3 nas duas | `--device 1,6 -- --tier 3,3` |
| Abrir a API de stats para a rede local | `--stats 0.0.0.0:4060` |
| Solo: primeira execução com o escrow cert | `-- --escrow-cert COLE_OS_128_CARACTERES_HEX` |
| Guardar os modelos em outro disco | `-- --models-dir /data/models` |

O pacote já roda em modo headless. Não adicione `--headless`. Todas as opções estão em
[configuration.md](configuration.md).

## Onde fica cada coisa

| O quê | Onde |
| --- | --- |
| Log com avisos, pedidos perdidos e relatórios de crash | `/var/lib/fear-miner/log.txt` |
| Modelos | `/var/lib/fear-miner/models` |
| Chave, cert e estado do escrow | `/var/lib/fear-miner` |
| Console do miner | `miner` no shell da rig, ou o log do miner no painel |

Um modelo que outro miner da rig já baixou (por exemplo, o `/hive/miners/custom/models` do miner
da Suprnova) é verificado e reaproveitado, sem segunda cópia no disco.

## Uso de CPU em rigs com poucos núcleos

Numa rig com muitas GPUs e CPU fraca, defina `FEAR_SYNC=block` no ambiente do flight sheet para
usar menos CPU, com cerca de 0,1% a menos de hashrate. `FEAR_SYNC=spin` usa um núcleo inteiro por
GPU.
