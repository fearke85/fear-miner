# HiveOS

[English](../en/hiveos.md) · **Português (Brasil)** · [Voltar ao README](../../README.pt-BR.md)

Como instalar o fear-miner no HiveOS, para qualquer moeda. Os valores da sua moeda (algoritmo,
template da carteira, Pool URL) estão na página dela: [Keryx](../../coins/keryx/README.pt-BR.md#flight-sheet-do-hiveos).

## Antes de começar

- HiveOS com a imagem Ubuntu 22.04 (jammy). A imagem 20.04 não é suportada.
- Driver NVIDIA 580 ou mais novo. Atualize pelo painel do HiveOS ou com `nvidia-driver-update`.
- Uma placa que a sua moeda suporte, e o espaço em disco que a página da moeda pede.

## Flight sheet

Crie um flight sheet com o miner **Custom**:

| Campo | Valor |
| --- | --- |
| Miner name | `fear-miner` |
| Installation URL | `https://github.com/fearke85/fear-miner/releases/download/v1.0.0/fear-miner-1.0.0.tar.gz` |
| Hash algorithm | da página da sua moeda |
| Wallet and worker template | da página da sua moeda |
| Pool URL | da página da sua moeda |
| Password | `x`, ou a senha da pool |
| Extra config arguments | Deixe vazio, ou veja abaixo |

A Pool URL precisa do prefixo: `stratum+tcp://` para pool, `grpc://` para node. Um `host:porta` sem
prefixo ou com `http://` é recusado.

Aplique o flight sheet. O painel mostra o hashrate quando as placas começam a minerar.

## Instalar pelo console da rig

```
/hive/miners/custom/custom-get https://github.com/fearke85/fear-miner/releases/download/v1.0.0/fear-miner-1.0.0.tar.gz
```

Adicione `-f` para reinstalar.

## Atualizar para uma versão nova

Troque a versão na Installation URL, nos dois lugares: em `v1.0.0` e em
`fear-miner-1.0.0.tar.gz`. O resto do flight sheet continua igual. Com a URL antiga, a rig
continua instalando a versão antiga.

Tudo o que o miner guarda (modelos, chaves, o log) fica em `/var/lib/fear-miner` entre
atualizações e reinstalações.

## Extra config arguments

Opções do miner vão antes de `--`, opções da moeda depois:

```
--device 0,2 --stats 0.0.0.0:4060 -- <opções da moeda>
```

| O quê | Extra config arguments |
| --- | --- |
| Minerar só nas placas 0 e 2 | `--device 0,2` |
| Abrir a API de stats para a rede local | `--stats 0.0.0.0:4060` |

O pacote já roda em modo headless. Opções do miner: [options.md](options.md). Opções da moeda: a
página dela ([Keryx](../../coins/keryx/docs/pt-BR/options.md)).

## Onde fica cada coisa

| O quê | Onde |
| --- | --- |
| Log com avisos, erros e relatórios de crash | `/var/lib/fear-miner/log.txt` |
| Dados que o miner guarda | `/var/lib/fear-miner` |
| Console do miner | `miner` no shell da rig, ou o log do miner no painel |

## Uso de CPU em rigs com poucos núcleos

Numa rig com muitas GPUs e CPU fraca, defina `FEAR_SYNC=block` no ambiente do flight sheet para
usar menos CPU, com cerca de 0,1% a menos de hashrate. `FEAR_SYNC=spin` usa um núcleo inteiro por
GPU.
