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
- Placas de 6 GB mineram o tier 0 ao lado de outra placa na mesma rig, com 2 GB de RAM livre na
  partida.
- Pascal (GTX 10xx, P104/P106) e anteriores não são suportadas.

## Qual tier minha placa minera?

O miner escolhe sozinho o maior tier que cada placa suporta. Não é preciso usar `--tier`.

Espaço livre em disco que cada tier precisa para baixar o modelo:

| Tier | Disco livre |
| --- | --- |
| 0 | ~6,7 GB |
| 1 | ~8,5 GB |
| 2 | ~10 GB |
| 3 | ~17 GB |
| 4 | ~30 GB |

## Configurações

Instale o pacote pelo guia da sua plataforma e use estes valores.

### Flight sheet do HiveOS

| Campo | Valor |
| --- | --- |
| Miner name | `fear-miner` |
| Installation URL | `https://github.com/fearke85/fear-miner/releases/download/v1.0.1/fear-miner-1.0.1.tar.gz` |
| Hash algorithm | `keryxhash` |
| Wallet and worker template | Pool: `%WAL%.%WORKER_NAME%`. Solo: `%WAL%` |
| Pool URL | Pool: `stratum+tcp://krx.suprnova.cc:4404`. Solo: `grpc://IP:PORTA` do seu node |
| Password | `x`, ou a senha da pool |

A carteira é o seu endereço Keryx, `keryx:...`. Guia de instalação: [HiveOS](../../docs/pt-BR/hiveos.md).

### run.sh (Linux) e start.bat (Windows)

| Linha | Valor |
| --- | --- |
| `WALLET` | Seu endereço Keryx, `keryx:...` |
| `WORKER` | Um nome para esta rig na pool |
| `POOL` | `stratum+tcp://krx.suprnova.cc:4404` |
| `NODE` | Só solo: `grpc://IP:PORTA` do seu node, com `POOL` vazio |
| `ESCROW_CERT` | Só solo, primeira execução: veja [mineração solo](docs/pt-BR/solo.md) |

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
