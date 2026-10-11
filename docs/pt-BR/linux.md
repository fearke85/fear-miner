# Linux

[English](../en/linux.md) · **Português (Brasil)** · [Voltar ao README](../../README.pt-BR.md)

Como instalar o fear-miner numa máquina Linux comum, fora do HiveOS, para qualquer moeda. Os
valores da sua moeda estão na página dela: [Keryx](../../coins/keryx/README.pt-BR.md#runsh-linux-e-startbat-windows).

## Antes de começar

- Linux x86-64 com glibc 2.35 ou mais nova (Ubuntu 22.04, Debian 12 ou mais novos).
- Driver NVIDIA 580 ou mais novo. Confira com `nvidia-smi`. O pacote traz as bibliotecas CUDA.
- Uma placa que a sua moeda suporte, e o espaço em disco que a página da moeda pede, ao lado do
  miner.

## Instalar

```
wget https://github.com/fearke85/fear-miner/releases/download/v0.0.32/fear-miner-linux-0.0.32.tar.gz
tar -xzf fear-miner-linux-0.0.32.tar.gz
cd fear-miner
nano run.sh
```

## Configurações no run.sh

Edite as linhas do topo do `run.sh` e salve. `WALLET`, `POOL`, `NODE` e qualquer linha que a sua
moeda acrescente usam os valores da página da moeda.

| Linha | O que colocar |
| --- | --- |
| `WALLET` | Seu endereço de pagamento |
| `WORKER` | Um nome para esta rig na pool |
| `POOL` | A pool, `stratum+tcp://host:porta` |
| `NODE` | Só solo: `grpc://IP:PORTA` do seu node. Deixe `POOL=""` |
| `DEVICES` | `all`, ou as placas que vão minerar, por exemplo `0,2,5` |
| `EXTRA` | Opções da moeda, por exemplo `(--headless)` |
| `STATS` | Endereço da API de stats. `0.0.0.0:4060` abre para a sua rede |

Opções do miner: [options.md](options.md).

## Rodar

```
./run.sh
```

Para o miner continuar rodando depois que você sair, inicie dentro do `screen` ou do `tmux`, ou
como serviço do systemd.

## Atualizar para uma versão nova

Extraia o pacote novo por cima da pasta antiga e copie suas configurações para o `run.sh` novo. O
que o miner guarda fica em `./data` e é mantido.

## Onde fica cada coisa

| O quê | Onde |
| --- | --- |
| Log com avisos, erros e relatórios de crash | `log.txt` ao lado do miner |
| Dados que o miner guarda | `./data`. Defina `FEAR_DATA_DIR` para mudar o local |
| Hashrate e shares | `curl 127.0.0.1:4060/stats` |
