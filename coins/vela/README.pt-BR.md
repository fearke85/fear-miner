# Vela

[English](README.md) · **Português (Brasil)** · [Todas as moedas](../../README.pt-BR.md)

Como minerar Vela com o fear-miner. Algoritmo: `vela`. Mineração em pool na
[suprnova](https://vela.suprnova.cc) ou na [AriaPool](https://pool.ariabrain.com/vela.html), e
mineração solo no seu próprio node Vela.

Vela é uma moeda de prova por inferência: cada tentativa é uma inferência de um modelo de imagem,
então o minerador mostra a velocidade em **inferências por segundo** (`inf/s`) e a eficiência em
**inferências por joule** (`inf/J`). A HiveOS só conhece unidades de hash e mostra o mesmo número
como H/s.

## Placas

- NVIDIA Turing ou mais nova (RTX 20xx, 30xx, 40xx, 50xx).
- Pascal (GTX 10xx) e anteriores não são suportadas.

Medido com o fear-miner num rig HiveOS, com o overclock que esse rig usa para o Keryx (power limit
padrão, fans a 75-85%). Os watts são o consumo da placa minerando. Onde o rig tem duas placas do
mesmo modelo, a faixa cobre as duas.

| Placa | inf/s | Watts | inf/J | Core travado | Offset de core | Offset de memória |
| --- | --- | --- | --- | --- | --- | --- |
| RTX 3060 | 13,6-13,7 | 78-83 | 0,166-0,173 | 1350 MHz | +200 / +255 | -1000 |
| RTX 3070 | 20,9 | 123 | 0,170 | 1250 MHz | +250 | +1000 |
| RTX 3080 | 27,6 | 190-193 | 0,143-0,145 | 1100 MHz | +250 | -2000 |
| RTX 5070 Ti | 57,8-57,9 | 197-211 | 0,274-0,294 | 2300 MHz | +450 | 0 |

O fear-miner 1.3.2 é cerca de 3% mais rápido que essas taxas no mesmo overclock, e um pouco mais
eficiente (inf/J maior).

A velocidade do Vela acompanha o clock de core: um core travado mais alto dá mais inf/s e consome
mais watts.
O Vela deixa a placa em carga total. Fique de olho na temperatura: uma RTX 5070 Ti sem overclock
chegou a 84 °C num rig aberto. Um power limit ou um core travado mais baixo deixa a placa mais fria.

## Disco

O modelo (1,2 GB) é baixado na primeira execução e conferido antes do uso. Ele fica para as
próximas execuções e atualizações:

| Plataforma | Pasta do modelo |
| --- | --- |
| HiveOS | `/var/lib/fear-miner/vela/models` |
| Linux e Windows | `vela/models` ao lado do minerador, ou dentro de `FEAR_DATA_DIR` |

## Configuração

Instale o pacote com o guia da sua plataforma e use estes valores.

### Pools

| Pool | `-pool` no Linux e no Windows | Pool URL na HiveOS |
| --- | --- | --- |
| [suprnova](https://vela.suprnova.cc) | `vela.suprnova.cc:7601` | `stratum+tcp://vela.suprnova.cc:7601` |
| [AriaPool](https://pool.ariabrain.com/vela.html) | `http://159.69.194.46:3349` | `http://159.69.194.46:3349` |

O login é o mesmo nas duas: seu endereço Vela e um nome de worker, senha `x`. As tabelas abaixo
usam a suprnova; para a AriaPool, troque só a pool.

### Flight sheet na HiveOS

| Campo | Valor |
| --- | --- |
| Miner name | `fear-miner` |
| Installation URL | `https://github.com/fearke85/fear-miner/releases/download/v1.4.0/fear-miner-1.4.0.tar.gz` |
| Hash algorithm | `poi`, ou qualquer um da lista (veja abaixo) |
| Wallet and worker template | `%WAL%.%WORKER_NAME%` |
| Pool URL | `stratum+tcp://vela.suprnova.cc:7601` |
| Password | `x` |
| Extra config arguments | `-coin vela` |

A HiveOS não tem `vela` na lista de Hash algorithm. Para o miner, `poi` é Vela. Com qualquer outro
algoritmo, coloque `-coin vela` em Extra config arguments: ele substitui o Hash algorithm e o miner
minera Vela. As
opções do Vela vão na mesma linha, depois dele: `-coin vela --batch 4 --lanes 1`.

A carteira é o seu endereço Vela, `vela1...`. Guia de instalação: [HiveOS](../../docs/pt-BR/hiveos.md).

### start-vela.sh (Linux) e start-vela.bat (Windows)

A linha da pool já vem preenchida. Coloque o seu endereço em `-wallet`.

| O quê | Valor |
| --- | --- |
| `-wallet` | Seu endereço Vela, `vela1...` |
| `-worker` | Um nome para este rig na pool |
| `-pool` | `vela.suprnova.cc:7601` |

Guias de instalação: [Linux](../../docs/pt-BR/linux.md) · [Windows](../../docs/pt-BR/windows.md).

### Solo no seu próprio node

A mineração solo precisa de um node Vela sincronizado, com o servidor RPC ligado. A recompensa do
bloco vai para `-wallet`.

```
./fear-miner -coin vela -node http://RPCUSER:RPCPASSWORD@127.0.0.1:18743 -wallet vela1...
```

Use o `rpcuser`, o `rpcpassword` e o `rpcport` da configuração do seu node. Na HiveOS, coloque
`-coin vela -node http://RPCUSER:RPCPASSWORD@IP_DO_NODE:18743` em Extra config arguments: o
`-node` toma o lugar da Pool URL.

## Opções do Vela

Opções da moeda usam dois hífens. Na HiveOS elas vão em Extra config arguments.

| Opção | O que faz |
| --- | --- |
| `--batch N` | Inferências por lançamento, de 1 a 16. O minerador escolhe pela memória da placa. |
| `--lanes N` | Fluxos paralelos por placa, de 1 a 4. O minerador escolhe pela memória da placa. |
| `--suggest-diff D` | Pede à pool a dificuldade de share `D` (só na suprnova). |
| `--models-dir PASTA` | Guarda o modelo em `PASTA`. |
| `--model ARQUIVO` | Usa este arquivo de modelo onde ele está, sem baixar. |

A escolha automática é a mais rápida em todas as placas que medimos. Numa RTX 5070 Ti,
`--batch 4 --lanes 1` é 5% mais lento e 3% mais eficiente (inf/J).

## Ainda não

- A porta TLS da suprnova.

## Problemas

| O que aparece | O que fazer |
| --- | --- |
| `not enough disk for ...` na primeira execução | Libere 1,2 GB onde fica a pasta do modelo, ou aponte `--models-dir` para outro lugar. |
| `model hash ... does not match` | O arquivo do modelo está corrompido ou é outro. Apague; o minerador baixa de novo. |
| `... is too little for ...` | A placa tem pouca memória livre. Feche o que estiver usando, ou passe `--batch 1 --lanes 1`. |
| Shares rejeitados como stale | Verifique a rede do rig; um link lento faz shares chegarem atrasados. |

Problemas gerais: [problemas](../../docs/pt-BR/troubleshooting.md).

## Ajuda

- [Discord](https://discord.gg/uK93NPAhbd)
- [Abra uma issue](https://github.com/fearke85/fear-miner/issues/new/choose) e anexe o `log.txt`
