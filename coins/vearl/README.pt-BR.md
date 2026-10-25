# Vearl

[English](README.md) · **Português (Brasil)** · [Todas as moedas](../../README.pt-BR.md)

Minerar Vearl (VRL) na testnet pública com o fear-miner. Algoritmo: `vearl`. Mineração em pool na
[AriaPool](https://pool.ariabrain.com/vrl.html), na [NurseryPool](https://vearl.nurserypool.com/)
ou na [pool do Vearl](https://pool.vearl.org/), e solo pela porta solo de qualquer uma delas.

As moedas da testnet não têm valor. O programa de recompensas conta pontos por bloco; as regras
e o cadastro estão em [vearl.org](https://vearl.org/participate/).

O minerador mostra a velocidade em **sigmas por segundo** (`sigma/s`), a unidade que as pools
mostram, e a eficiência em `sigma/J`. A HiveOS só conhece unidades de hash e mostra o mesmo número
como H/s. Um sigma são 4096 tentativas de tile, então o MH/s do minerador oficial é
sigma/s × 4096 / 1.000.000.

## Placas

- NVIDIA Ampere ou mais nova (RTX 30xx, 40xx, 50xx).
- Turing (RTX 20xx) e anteriores não são suportadas: o trabalho do Vearl usa instruções que elas
  não têm.

Medido com o fear-miner no overclock de cada rig (RTX 30 numa rig HiveOS, RTX 40 em outra,
RTX 5070 Ti num desktop no clock de fábrica):

| Placa | sigma/s | MH/s do minerador oficial |
| --- | --- | --- |
| RTX 3060 | 22.300 | 91 |
| RTX 3070 | 35.300 | 145 |
| RTX 3080 | 45.900 | 188 |
| RTX 4060 Ti | 31.400 | 129 |
| RTX 4070 SUPER | 40.400 | 166 |
| RTX 5070 Ti | 108.100 | 443 |

## Configuração

Instale o pacote pelo guia da sua plataforma e use estes valores.

### Pools

| Pool | Modo | `-pool` no Linux e no Windows | Pool URL na HiveOS |
| --- | --- | --- | --- |
| [AriaPool](https://pool.ariabrain.com/vrl.html) | compartilhado (PPLNS, 2%) | `vrl.ariabrain.com:3354` | `vrl.ariabrain.com:3354` |
| AriaPool | solo (0%) | `vrl.ariabrain.com:3355` | `vrl.ariabrain.com:3355` |
| [NurseryPool](https://vearl.nurserypool.com/) | compartilhado (PPLNS, 2%) | `vearl.nurserypool.com:3367` | `vearl.nurserypool.com:3367` |
| NurseryPool | solo (0%) | `vearl.nurserypool.com:3366` | `vearl.nurserypool.com:3366` |
| [Pool do Vearl](https://pool.vearl.org/) | compartilhado (PPLNS, 1%) | `pool.vearl.org:3333` | `pool.vearl.org:3333` |
| Pool do Vearl | solo (1%) | `pool.vearl.org:3366` | `pool.vearl.org:3366` |

A carteira é o seu endereço Vearl (`vrl1...`). As pools não pedem cadastro nem senha.

### Flight sheet da HiveOS

| Campo | Valor |
| --- | --- |
| Miner name | `fear-miner` |
| Installation URL | `https://github.com/fearke85/fear-miner/releases/download/v1.4.2/fear-miner-1.4.2.tar.gz` |
| Hash algorithm | `vearl` |
| Wallet and worker template | `%WAL%.%WORKER_NAME%` |
| Pool URL | `vrl.ariabrain.com:3354` |
| Password | `x` |
| Extra config arguments | vazio |

Guia de instalação: [HiveOS](../../docs/pt-BR/hiveos.md).

### start-vearl.sh (Linux) e start-vearl.bat (Windows)

A linha da pool já vem preenchida. Coloque seu endereço em `-wallet`.

| O quê | Valor |
| --- | --- |
| `-wallet` | Seu endereço Vearl (`vrl1...`) |
| `-worker` | Um nome para esta rig na pool: de 1 a 32 letras, dígitos, `.`, `_` ou `-` |
| `-pool` | `vrl.ariabrain.com:3354` |

Guias de instalação: [Linux](../../docs/pt-BR/linux.md) · [Windows](../../docs/pt-BR/windows.md).

### Solo

Aponte o `-pool` (na HiveOS, o Pool URL) para a porta solo de uma pool: `vrl.ariabrain.com:3355`,
`vearl.nurserypool.com:3366` ou `pool.vearl.org:3366`. Um bloco que você encontrar é pago inteiro ao seu endereço, e
os pontos da testnet dele são seus. Um bloco solo é raro numa rig só; a porta compartilhada paga
com regularidade.

Solo no seu próprio node Vearl não está disponível: o node minera sozinho e não aceita
minerador de fora. O `-node` é recusado com uma mensagem que indica as portas solo.

### Seus pontos da testnet

As pools assinam recibos do seu trabalho a cada minuto. O fear-miner confere cada um e guarda em
`vearl/receipts.jsonl` ao lado do minerador (na HiveOS, `/var/lib/fear-miner/vearl/receipts.jsonl`).
Guarde esse arquivo: ele é a sua prova se uma pool creditar menos do que assinou. A página da
pool mostra os pontos do seu endereço, e o minerador mostra na tela.

## Opções do Vearl

Opções da moeda levam dois hífens. Na HiveOS, vão em Extra config arguments.

| Opção | O que faz |
| --- | --- |
| `--receipts ARQUIVO` | Guarda os recibos da pool neste arquivo em vez do padrão. |

## Problemas

| O que aparece | O que fazer |
| --- | --- |
| `no NVIDIA GPU of compute capability 8.0 or newer` | A placa é anterior à RTX 30. O Vearl não consegue usá-la. |
| Erros de `payout address` | A carteira precisa ser um endereço `vrl1...`, com `.worker` depois se quiser nome de worker. |
| Shares contadas como stale logo depois de um bloco | Normal: um bloco novo deixa atrasadas as shares do anterior. |

Problemas gerais: [solução de problemas](../../docs/pt-BR/troubleshooting.md).

## Ajuda

- [Discord](https://discord.gg/uK93NPAhbd)
- [Abra uma issue](https://github.com/fearke85/fear-miner/issues/new/choose) e anexe o `log.txt`
