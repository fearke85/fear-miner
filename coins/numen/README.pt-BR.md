# Numen

[English](README.md) · **Português (Brasil)** · [Todas as moedas](../../README.pt-BR.md)

Como minerar Numen (NUMN) com o fear-miner. Algoritmo: `numen` (a HiveOS chama de `poscan`).
Mineração em pool na [rplant](https://pool.rplant.xyz), na [ninjaraider](https://ninjaraider.com) ou na
[Nitopool](https://pool.nitopool.online/), solo pela rplant ou pela Nitopool e solo no seu próprio
node Numen.

O minerador mostra a velocidade em MH/s.

## Placas

- NVIDIA Turing ou mais nova (RTX 20xx, 30xx, 40xx, 50xx).
- Pascal (GTX 10xx) e anteriores não são suportadas.

Medido com o fear-miner num rig HiveOS, no core lock que esse rig usa (RTX 30 a 1500 MHz, RTX
5070 Ti a 2300 MHz):

| Placa | MH/s |
| --- | --- |
| RTX 3060 | 0,34 |
| RTX 3070 | 0,55 |
| RTX 3080 | 0,81 |
| RTX 5070 Ti | 1,30 |

A velocidade do Numen acompanha o clock do core: um core lock maior dá mais MH/s e consome mais
watts.

## Configuração

Instale o pacote com o guia da sua plataforma e use estes valores.

### Pools

| Pool | `-pool` no Linux e no Windows | Pool URL na HiveOS |
| --- | --- | --- |
| [rplant](https://pool.rplant.xyz), Europa | `eu.rplant.xyz:7189` | `stratum+tcp://eu.rplant.xyz:7189` |
| rplant, América do Norte | `na.rplant.xyz:7189` | `stratum+tcp://na.rplant.xyz:7189` |
| rplant, Ásia | `asia.rplant.xyz:7189` | `stratum+tcp://asia.rplant.xyz:7189` |
| [ninjaraider](https://ninjaraider.com) | `numen.ninjaraider.com:44960` | `stratum+tcp://numen.ninjaraider.com:44960` |
| [Nitopool](https://pool.nitopool.online/) | `numn.stratum.nitopool.online:3028` | `stratum+tcp://numn.stratum.nitopool.online:3028` |
| Nitopool, farms | `numn.stratum.nitopool.online:3029` | `stratum+tcp://numn.stratum.nitopool.online:3029` |

Escolha a região da rplant mais perto do rig: um link lento transforma shares atrasadas em stale.
O modo compartilhado da Nitopool é PPLNS com taxa de 0,9%; a porta de farm começa com uma
dificuldade de share oito vezes maior, para rigs com muitas placas.

### Flight sheet na HiveOS

| Campo | Valor |
| --- | --- |
| Miner name | `fear-miner` |
| Installation URL | `https://github.com/fearke85/fear-miner/releases/download/v1.4.2/fear-miner-1.4.2.tar.gz` |
| Hash algorithm | `poscan` |
| Wallet and worker template | `%WAL%.%WORKER_NAME%` |
| Pool URL | `stratum+tcp://eu.rplant.xyz:7189` |
| Password | `x` (ou `m=solo`, veja abaixo) |
| Extra config arguments | vazio |

A carteira é o seu endereço Numen. Guia de instalação: [HiveOS](../../docs/pt-BR/hiveos.md).

### start-numen.sh (Linux) e start-numen.bat (Windows)

A linha da pool já vem preenchida. Coloque o seu endereço em `-wallet`.

| O quê | Valor |
| --- | --- |
| `-wallet` | Seu endereço Numen |
| `-worker` | Um nome para este rig na pool |
| `-pool` | `eu.rplant.xyz:7189` |

Guias de instalação: [Linux](../../docs/pt-BR/linux.md) · [Windows](../../docs/pt-BR/windows.md).

### Solo pela rplant

A rplant minera solo no mesmo stratum: coloque `m=solo` na senha. Um bloco que você achar é pago
inteiro para você, com a taxa solo da rplant (2%, contra 1% no modo compartilhado).

| Onde | Valor |
| --- | --- |
| Linux e Windows | `-password m=solo` |
| HiveOS | Campo Password: `m=solo` |

As outras opções de senha da rplant vão na mesma linha, separadas por vírgula: `m=solo,d=200000`
fixa a dificuldade de share.

### Solo pela Nitopool

A Nitopool minera solo em portas próprias: `numn.stratum.nitopool.online:3024`, ou `numn.stratum.nitopool.online:3026` para uma farm. Um bloco que
você achar é pago inteiro para você, com a taxa de 0,9% da Nitopool. Na HiveOS, coloque
`stratum+tcp://numn.stratum.nitopool.online:3024` na Pool URL; a senha continua `x`.

### Solo no seu próprio node

```
./fear-miner -coin numen -node ws://127.0.0.1:9944
```

O node paga o bloco para a conta de mineração configurada nele, não para `-wallet`. O `-node`
toma o lugar do `-pool`; não passe os dois. Na HiveOS, coloque o node na Pool URL:
`ws://IP_DO_NODE:9944`.

## Opções do Numen

Opções da moeda usam dois hífens. Na HiveOS elas vão em Extra config arguments.

| Opção | O que faz |
| --- | --- |
| `--block 128` ou `--block 256` | Pula a escolha entre os dois na primeira partida e usa este. |
| `--kernel exact` | Uma varredura muito mais lenta, para conferir resultados. A padrão, `fast`, é a de minerar. |

A primeira partida mede a placa por alguns segundos e guarda o resultado.

## Ainda não

- A porta TLS da rplant.

## Problemas

| O que aparece | O que fazer |
| --- | --- |
| Shares rejeitadas como `stale share` | Algumas são normais: os jobs mudam a cada poucos segundos. Muitas indicam um link lento; escolha uma região da rplant mais perto. |
| Shares rejeitadas como `invalid PoScan work` na Nitopool | Algumas são normais: é assim que a Nitopool responde a uma share que chegou depois de o job mudar. Muitas indicam um link lento até a pool. |
| `pass -pool or -node, not both` | Deixe só um dos dois. |

Problemas gerais: [problemas](../../docs/pt-BR/troubleshooting.md).

## Ajuda

- [Discord](https://discord.gg/uK93NPAhbd)
- [Abra uma issue](https://github.com/fearke85/fear-miner/issues/new/choose) e anexe o `log.txt`
