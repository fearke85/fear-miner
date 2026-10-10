# Linux

[English](../en/linux.md) · **Português (Brasil)** · [Voltar ao README](../../README.pt-BR.md)

Para uma máquina Linux comum, fora do HiveOS.

## Antes de começar

- Linux x86-64 com glibc 2.35 ou mais nova (Ubuntu 22.04, Debian 12 ou mais novos).
- Driver NVIDIA 580 ou mais novo. Confira com `nvidia-smi`. O pacote traz as bibliotecas CUDA.
- Placas: Turing ou mais novas. Veja [qual tier sua placa minera](../../README.pt-BR.md#qual-tier-minha-placa-minera).
- Espaço em disco ao lado do miner para o modelo de cada tier minerado.

## Instalar

```
wget https://github.com/fearke85/fear-miner/releases/download/v0.0.31/fear-miner-linux-0.0.31.tar.gz
tar -xzf fear-miner-linux-0.0.31.tar.gz
cd fear-miner
nano run.sh
```

## Configurações no run.sh

Edite as linhas do topo do `run.sh` e salve:

| Linha | O que colocar |
| --- | --- |
| `WALLET` | Seu endereço Keryx, `keryx:...` |
| `WORKER` | Um nome para esta rig na pool |
| `POOL` | A pool, por exemplo `stratum+tcp://krx.suprnova.cc:4404` |
| `NODE` | Só solo: `grpc://IP:PORTA` do seu node. Deixe `POOL=""` |
| `ESCROW_CERT` | Só solo, primeira execução: os 128 caracteres hex da sua carteira. Veja [solo.md](solo.md) |
| `DEVICES` | `all`, ou as placas que vão minerar, por exemplo `0,2,5` |
| `EXTRA` | Outras opções, por exemplo `(--tier 0)` ou `(--headless)` |
| `STATS` | Endereço da API de stats. `0.0.0.0:4060` abre para a sua rede |

Numa máquina sem monitor, adicione `--headless` ao `EXTRA`: placas de 10 e 12 GB passam a minerar
um tier maior. Todas as opções estão em [configuration.md](configuration.md).

## Rodar

```
./run.sh
```

A primeira execução baixa o modelo, o que leva alguns minutos. Para o miner continuar rodando
depois que você sair, inicie dentro do `screen` ou do `tmux`, ou como serviço do systemd.

## Atualizar para uma versão nova

Extraia o pacote novo por cima da pasta antiga e copie suas configurações para o `run.sh` novo.
Modelos e arquivos de escrow ficam em `./data` e são mantidos.

## Onde fica cada coisa

| O quê | Onde |
| --- | --- |
| Log com avisos, pedidos perdidos e relatórios de crash | `log.txt` ao lado do miner |
| Modelos, arquivos de escrow | `./data`. Defina `FEAR_DATA_DIR` para mudar o local |
| Hashrate e shares | `curl 127.0.0.1:4060/stats` |
