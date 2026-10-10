# fear-miner

[English](README.md) · **Português (Brasil)**

Miner de GPU NVIDIA para Keryx (keryxhash). Pacotes para HiveOS, Linux e Windows.

[![release](https://img.shields.io/badge/release-0.0.31-2b7bd6)](https://github.com/fearke85/fear-miner/releases/tag/v0.0.31)
![HiveOS](https://img.shields.io/badge/HiveOS-jammy-3a9a3a)
![Linux](https://img.shields.io/badge/Linux-glibc%202.35%2B-3a9a3a)
![Windows](https://img.shields.io/badge/Windows-10%20%2F%2011-3a9a3a)
[![Discord](https://img.shields.io/badge/chat-Discord-5865f2)](https://discord.gg/uK93NPAhbd)

> [!WARNING]
> **O hard fork H14 está ativo** (DAA 121.985.000, 09/10/2026). Versões anteriores à 0.0.22 são
> inválidas: a rede rejeita os shares e blocos delas. Quem minera solo precisa do keryx-node 1.6.4
> ou mais novo.

## Download: 0.0.31 (2026-10-09)

| Plataforma | Arquivo | Guia |
| --- | --- | --- |
| HiveOS | [fear-miner-0.0.31.tar.gz](https://github.com/fearke85/fear-miner/releases/download/v0.0.31/fear-miner-0.0.31.tar.gz) | [docs/pt-BR/hiveos.md](docs/pt-BR/hiveos.md) |
| Linux | [fear-miner-linux-0.0.31.tar.gz](https://github.com/fearke85/fear-miner/releases/download/v0.0.31/fear-miner-linux-0.0.31.tar.gz) | [docs/pt-BR/linux.md](docs/pt-BR/linux.md) |
| Windows | [fear-miner-windows-0.0.31.zip](https://github.com/fearke85/fear-miner/releases/download/v0.0.31/fear-miner-windows-0.0.31.zip) | [docs/pt-BR/windows.md](docs/pt-BR/windows.md) |

O que mudou: [notas da release](https://github.com/fearke85/fear-miner/releases/tag/v0.0.31) ·
[CHANGELOG](CHANGELOG.md) (em inglês). Os checksums estão na página da release.

## Começo rápido

<details open>
<summary><b>HiveOS</b></summary>

Crie um flight sheet com o miner **Custom**:

| Campo | Valor |
| --- | --- |
| Miner name | `fear-miner` |
| Installation URL | `https://github.com/fearke85/fear-miner/releases/download/v0.0.31/fear-miner-0.0.31.tar.gz` |
| Wallet and worker template | `%WAL%.%WORKER_NAME%` (carteira `keryx:SEU_ENDERECO`) |
| Pool URL | `stratum+tcp://krx.suprnova.cc:4404`, ou `grpc://IP:PORTA` do seu node para minerar solo |
| Password | `x` |

Para atualizar depois, troque a versão na Installation URL. O resto do flight sheet continua igual.
Guia completo: [docs/pt-BR/hiveos.md](docs/pt-BR/hiveos.md).
</details>

<details>
<summary><b>Linux</b></summary>

```
tar -xzf fear-miner-linux-0.0.31.tar.gz
cd fear-miner
nano run.sh     # preencha WALLET, WORKER e POOL (ou NODE para solo)
./run.sh
```

Guia completo: [docs/pt-BR/linux.md](docs/pt-BR/linux.md).
</details>

<details>
<summary><b>Windows</b></summary>

Extraia `fear-miner-windows-0.0.31.zip`, abra o `start.bat` no Bloco de Notas, preencha
`WALLET`, `WORKER` e `POOL` (ou `NODE` para solo), salve e dê dois cliques nele.

Guia completo: [docs/pt-BR/windows.md](docs/pt-BR/windows.md).
</details>

## Requisitos

- NVIDIA Turing ou mais nova (RTX 20xx, 30xx, 40xx, 50xx) com 8 GB ou mais. Placas de 6 GB
  mineram o tier 0 ao lado de outra placa. Pascal (GTX 10xx, P104/P106) e anteriores não são
  suportadas.
- Driver NVIDIA 580 ou mais novo (CUDA 13.2). Os pacotes trazem as bibliotecas CUDA, não o driver.
- Espaço em disco para o modelo de cada tier minerado (tabela abaixo). Ele é baixado na primeira
  execução.
- HiveOS: imagem Ubuntu 22.04 (jammy). A imagem 20.04 não é suportada.

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

## Está funcionando?

- Hashrate e shares: `curl 127.0.0.1:4060/stats` na rig. No HiveOS aparecem no painel.
- Avisos, pedidos de IA perdidos e relatórios de crash vão para o `log.txt`:
  `/var/lib/fear-miner/log.txt` no HiveOS, ao lado do miner no Linux e no Windows.

## Ajuda

- [Solução de problemas](docs/pt-BR/troubleshooting.md)
- [Mineração solo](docs/pt-BR/solo.md) · [Todas as opções](docs/pt-BR/configuration.md)
- [Discord](https://discord.gg/uK93NPAhbd)
- [Abra uma issue](https://github.com/fearke85/fear-miner/issues/new/choose) e anexe o `log.txt`

## Licença

O fear-miner é proprietário. A [LICENSE](LICENSE) permite apenas o uso do software sem
modificações. Modificação, extração e tentativas de quebrar a codificação protegida são proibidas.
Os componentes de terceiros do pacote estão listados no [NOTICE](NOTICE). Este repositório publica
os pacotes das releases e a documentação. Ele não publica código-fonte.
