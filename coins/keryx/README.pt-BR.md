# Keryx

[English](README.md) · **Português (Brasil)** · [Todas as moedas](../../README.pt-BR.md)

Como minerar Keryx com o fear-miner. Algoritmo: `keryxhash`.

> [!WARNING]
> **O hard fork H14 está ativo** (DAA 121.985.000, 09/10/2026). Versões anteriores à 0.0.22 são
> inválidas: a rede rejeita os shares e blocos delas. Quem minera solo precisa do keryx-node 1.6.4
> ou mais novo.

## Placas

- NVIDIA Turing ou mais nova (RTX 20xx, 30xx, 40xx, 50xx) com 8 GB ou mais.
- NVIDIA CMP 170HX, inclusive as desbloqueadas para 64 GB, que mineram o tier 4. Medido: ~3,2 MH/s
  por placa com power limit de 200 W.
- Placas com 6 GB ou menos não são suportadas.
- Pascal (GTX 10xx, P104/P106) e anteriores não são suportadas.

## Qual tier minha placa minera?

Cada placa minera o maior tier cujo modelo cabe na memória dela com espaço para responder os
pedidos de IA desse tier. Não é preciso usar `--tier`.

| Memória da placa | Tier | Disco livre para o modelo |
| --- | --- | --- |
| 8 GB | 0 | ~6,7 GB |
| 10-11 GB | 1 | ~8,5 GB |
| 12-16 GB | 2 | ~10 GB |
| 20-24 GB | 3 | ~17 GB |
| 32 GB ou mais | 4 | ~30 GB |

Com monitor ligado, o que o desktop ocupa não conta, e uma placa no limite pode minerar um tier
abaixo.

## Configurações

Instale o pacote pelo guia da sua plataforma e use estes valores.

### Flight sheet do HiveOS

| Campo | Valor |
| --- | --- |
| Miner name | `fear-miner` |
| Installation URL | `https://github.com/fearke85/fear-miner/releases/download/v1.4.3/fear-miner-1.4.3.tar.gz` |
| Hash algorithm | `keryxhash` |
| Wallet and worker template | Pool: `%WAL%.%WORKER_NAME%`. Solo: `%WAL%` |
| Pool URL | Pool: `stratum+tcp://krx.suprnova.cc:4404`. Solo: `grpc://IP:PORTA` do seu node |
| Password | `x`, ou a senha da pool |

A carteira é o seu endereço Keryx, `keryx:...`. Guia de instalação: [HiveOS](../../docs/pt-BR/hiveos.md).

### start-keryx.sh (Linux) e start-keryx.bat (Windows)

A linha da pool já vem preenchida. Coloque o seu endereço em `-wallet`. Para solo, comente a
linha da pool e tire o comentário da linha solo.

| O quê | Valor |
| --- | --- |
| `-wallet` | Seu endereço Keryx, `keryx:...` |
| `-worker` | Um nome para esta rig na pool |
| `-pool` | `krx.suprnova.cc:4404` |
| `-node` | Só solo: `grpc://IP:PORTA` do seu node |
| `--escrow-cert` | Só solo, primeira execução: veja [mineração solo](docs/pt-BR/solo.md) |

Guias de instalação: [Linux](../../docs/pt-BR/linux.md) · [Windows](../../docs/pt-BR/windows.md).

## Pedidos de IA

O Keryx manda pedidos de IA aos mineradores de cada tier, e todo minerador daquele tier precisa
responder a tempo. O miner responde sozinho enquanto minera. Um pedido que a sua rig não responde
conta como strike contra o seu endereço de pagamento: mantenha o miner rodando e as placas
estáveis, e confira o `log.txt`. Mais em [solução de problemas](docs/pt-BR/troubleshooting.md).

## Mais

- [Mineração solo](docs/pt-BR/solo.md)
- [Opções do Keryx](docs/pt-BR/options.md) (depois de `--`)
- [Problemas do Keryx](docs/pt-BR/troubleshooting.md)
- [Opções do miner e problemas gerais](../../docs/pt-BR/options.md)
