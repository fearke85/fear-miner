# Linux

[English](../en/linux.md) · **Português (Brasil)** · [Voltar ao README](../../README.pt-BR.md)

Como instalar o fear-miner numa máquina Linux comum, fora do HiveOS, para qualquer moeda. Os
valores da sua moeda estão na página dela: [Keryx](../../coins/keryx/README.pt-BR.md#start-keryxsh-linux-e-start-keryxbat-windows).

## Antes de começar

- Linux x86-64 com glibc 2.35 ou mais nova (Ubuntu 22.04, Debian 12 ou mais novos).
- Driver NVIDIA 580 ou mais novo. Confira com `nvidia-smi`. O pacote traz as bibliotecas CUDA.
- Uma placa que a sua moeda suporte, e o espaço em disco que a página da moeda pede, ao lado do
  miner.

## Instalar

```
wget https://github.com/fearke85/fear-miner/releases/download/v1.2.0/fear-miner-linux-1.2.0.tar.gz
tar -xzf fear-miner-linux-1.2.0.tar.gz
cd fear-miner
nano start-keryx.sh
```

## Configurações no script de start

Cada moeda tem o seu script. Para o Keryx, edite o `start-keryx.sh`. Deixe uma linha sem
comentário, a da pool ou a do solo, e coloque o seu endereço em `-wallet`. A pool, o node e os
outros valores estão na página da moeda.

As outras opções vão nessa mesma linha. Opções do miner: [options.md](options.md).

## Rodar

```
./start-keryx.sh
```

Para o miner continuar rodando depois que você sair, inicie dentro do `screen` ou do `tmux`, ou
como serviço do systemd.

## Atualizar para uma versão nova

Extraia o pacote novo por cima da pasta antiga e copie a sua linha para o `start-keryx.sh` novo.
O que o miner guarda fica em `./keryx` e é mantido. Um `./data` antigo é aproveitado de lá.

## Onde fica cada coisa

| O quê | Onde |
| --- | --- |
| Log com avisos, erros e relatórios de crash | `log.txt` ao lado do miner |
| Dados que o miner guarda | `./keryx` (`models/`, e `escrow/<carteira>/`). Defina `FEAR_DATA_DIR` para mudar o local |
| Hashrate e shares | `curl 127.0.0.1:4060/stats` |
