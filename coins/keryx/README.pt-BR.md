# Keryx

[English](README.md) · **Português (Brasil)** · [Todas as moedas](../../README.pt-BR.md)

Como minerar Keryx com o fear-miner. Algoritmo: `keryxhash`.

> [!WARNING]
> **O hard fork H16** ativa no DAA 147.000.000 (07/11/2026, por volta das 11:00 de Brasília). A
> partir daí, versões anteriores à 1.6.0 são inválidas: a rede rejeita os shares e blocos delas.
> Quem minera solo precisa do keryx-node 1.6.7 ou mais novo.

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
| 8-11 GB | 0 | ~6,7 GB |
| 12 GB | 1 | ~8,5 GB |
| 16-20 GB | 2 | ~10 GB |
| 24 GB | 3 | ~17 GB |
| 32 GB ou mais | 4 | ~30 GB |

Cada resposta de IA também fica guardada no disco por 12 horas, dezenas de MB por resposta, então
deixe alguns GB livres além do modelo num rig que responde muitos pedidos.

Com monitor ligado, o que o desktop ocupa não conta, e uma placa no limite pode minerar um tier
abaixo.

## Configurações

Instale o pacote pelo guia da sua plataforma e use estes valores.

### Flight sheet do HiveOS

| Campo | Valor |
| --- | --- |
| Miner name | `fear-miner` |
| Installation URL | `https://github.com/fearke85/fear-miner/releases/download/v1.6.5/fear-miner-1.6.5.tar.gz` |
| Hash algorithm | `keryxhash` |
| Wallet and worker template | Pool: `%WAL%.%WORKER_NAME%`. Solo: `%WAL%` |
| Pool URL | Pool: `stratum+tcp://krx.suprnova.cc:4404`, ou `stratum+ssl://krx.cryo-pool.com:5555`. Solo: `grpc://IP:PORTA` do seu node |
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

### Pools

| Pool | Endereço | Transporte |
| --- | --- | --- |
| Suprnova | `krx.suprnova.cc:4404` (UE), `stratum-us.suprnova.cc:4404` (EUA) | simples; `stratum+ssl://krx.suprnova.cc:4405` também funciona |
| Cryo Pool | `krx.cryo-pool.com:5555` | só criptografado: `stratum+ssl://krx.cryo-pool.com:5555` |

O `-pool` aceita `host:porta` ou uma URL stratum; `stratum+ssl://` (ou `stratum+tls://`) conecta
com TLS. O miner confere o certificado da pool, então um endereço sem certificado válido não
conecta. A mesma carteira e o mesmo worker valem nas duas pools; cada uma tem o seu painel. No
HiveOS, coloque a URL completa no campo Pool URL.

Guias de instalação: [Linux](../../docs/pt-BR/linux.md) · [Windows](../../docs/pt-BR/windows.md).

## Pedidos de IA

O Keryx manda pedidos de IA aos mineradores de cada tier, e todo minerador daquele tier precisa
responder a tempo. O miner responde sozinho enquanto minera. Um pedido que a sua rig não responde
conta como strike contra o seu endereço de pagamento: mantenha o miner rodando e as placas
estáveis, e confira o `log.txt`. Mais em [solução de problemas](docs/pt-BR/troubleshooting.md).

Desde o H15 a rede dá bem menos tempo para responder. Um pedido que chega com o modelo
descarregado pode ser respondido com atraso.

A tela do miner mostra **AI processed**, as respostas que o seu pool ou nó aceitou, e no solo
**AI paid**, as recompensas de IA que a rede pagou à sua carteira e o valor em KRX. Uma recompensa
chega cerca de 12 horas depois da resposta; a que chega com o miner parado é paga, mas não entra
na contagem. As duas contagens ficam guardadas por carteira entre reinícios. Rigs que mineram para
a mesma carteira contam, cada uma, todas as recompensas dessa carteira.

## Mais

- [Mineração solo](docs/pt-BR/solo.md)
- [Opções do Keryx](docs/pt-BR/options.md) (depois de `--`)
- [Problemas do Keryx](docs/pt-BR/troubleshooting.md)
- [Opções do miner e problemas gerais](../../docs/pt-BR/options.md)
