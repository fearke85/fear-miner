# fear-miner

[English](README.md) · **Português (Brasil)**

Miner multi-algoritmo para GPUs NVIDIA. Pacotes para HiveOS, Linux e Windows.

[![release](https://img.shields.io/badge/release-1.3.1-2b7bd6)](https://github.com/fearke85/fear-miner/releases/tag/v1.3.1)
![HiveOS](https://img.shields.io/badge/HiveOS-jammy-3a9a3a)
![Linux](https://img.shields.io/badge/Linux-glibc%202.35%2B-3a9a3a)
![Windows](https://img.shields.io/badge/Windows-10%20%2F%2011-3a9a3a)
[![Discord](https://img.shields.io/badge/chat-Discord-5865f2)](https://discord.gg/uK93NPAhbd)

## Moedas

Escolha a sua moeda. A página dela tem as configurações de pool e carteira, as placas suportadas e
as opções próprias.

| Moeda | Algoritmo | Placas | Docs |
| --- | --- | --- | --- |
| Keryx | `keryxhash` | NVIDIA Turing ou mais nova, 8 GB ou mais | [coins/keryx](coins/keryx/README.pt-BR.md) |
| Vela | `vela` | NVIDIA Turing ou mais nova | [coins/vela](coins/vela/README.pt-BR.md) |

> [!WARNING]
> **Keryx:** o hard fork H14 está ativo. Versões anteriores à 0.0.22 são inválidas.
> Veja [coins/keryx](coins/keryx/README.pt-BR.md).

## Download: 1.3.1 (2026-10-20)

Um pacote por plataforma. Ele minera todas as moedas da tabela acima.

| Plataforma | Arquivo | Guia de instalação |
| --- | --- | --- |
| HiveOS | [fear-miner-1.3.1.tar.gz](https://github.com/fearke85/fear-miner/releases/download/v1.3.1/fear-miner-1.3.1.tar.gz) | [docs/pt-BR/hiveos.md](docs/pt-BR/hiveos.md) |
| Linux | [fear-miner-linux-1.3.1.tar.gz](https://github.com/fearke85/fear-miner/releases/download/v1.3.1/fear-miner-linux-1.3.1.tar.gz) | [docs/pt-BR/linux.md](docs/pt-BR/linux.md) |
| Windows | [fear-miner-windows-1.3.1.zip](https://github.com/fearke85/fear-miner/releases/download/v1.3.1/fear-miner-windows-1.3.1.zip) | [docs/pt-BR/windows.md](docs/pt-BR/windows.md) |

O que mudou: [notas da release](https://github.com/fearke85/fear-miner/releases/tag/v1.3.1) ·
[CHANGELOG](CHANGELOG.md) (em inglês). Os checksums estão na página da release.

## Como começar

1. Escolha a sua moeda na tabela acima e anote as configurações de pool, carteira e algoritmo.
2. Instale o pacote da sua plataforma seguindo o guia: [HiveOS](docs/pt-BR/hiveos.md),
   [Linux](docs/pt-BR/linux.md) ou [Windows](docs/pt-BR/windows.md).
3. Confira se está minerando: no painel do HiveOS, ou com `curl 127.0.0.1:4060/stats` na rig.

## Requisitos para todas as moedas

- Uma placa NVIDIA que a moeda suporte (veja a página dela).
- Driver NVIDIA 580 ou mais novo (CUDA 13.2). Os pacotes trazem as bibliotecas CUDA, não o driver.
- HiveOS com a imagem Ubuntu 22.04 (jammy), Linux com glibc 2.35 ou mais nova, ou Windows 10 / 11.

## Documentação

| Assunto | Para todas as moedas | Keryx | Vela |
| --- | --- | --- | --- |
| Instalação | [HiveOS](docs/pt-BR/hiveos.md) · [Linux](docs/pt-BR/linux.md) · [Windows](docs/pt-BR/windows.md) | [Configurações por plataforma](coins/keryx/README.pt-BR.md#configurações) | [Configuração por plataforma](coins/vela/README.pt-BR.md#configuração) |
| Opções | [Opções do miner](docs/pt-BR/options.md) | [Opções do Keryx](coins/keryx/docs/pt-BR/options.md) | [Opções do Vela](coins/vela/README.pt-BR.md#opções-do-vela) |
| Problemas | [Solução de problemas](docs/pt-BR/troubleshooting.md) | [Problemas do Keryx](coins/keryx/docs/pt-BR/troubleshooting.md) | [Problemas do Vela](coins/vela/README.pt-BR.md#problemas) |
| Mineração solo | | [Keryx solo](coins/keryx/docs/pt-BR/solo.md) | |

## Ferramentas da comunidade

O site do [Juliano Caju](https://www.julianocaju.com.br/calculadora/) tem ferramentas para várias
moedas, em português e inglês:

- [Tabela de overclocks](https://www.julianocaju.com.br/overclocks/) por placa e moeda
- [Calculadora de mineração](https://www.julianocaju.com.br/calculadora/)
- [Rentabilidade por placa](https://www.julianocaju.com.br/rentabilidade/)

## Ajuda

- [Discord](https://discord.gg/uK93NPAhbd)
- [Abra uma issue](https://github.com/fearke85/fear-miner/issues/new/choose) e anexe o `log.txt`

## Licença

O fear-miner é proprietário. A [LICENSE](LICENSE) permite apenas o uso do software sem
modificações. Modificação, extração e tentativas de quebrar a codificação protegida são proibidas.
Os componentes de terceiros do pacote estão listados no [NOTICE](NOTICE). Este repositório publica
os pacotes das releases e a documentação. Ele não publica código-fonte.
