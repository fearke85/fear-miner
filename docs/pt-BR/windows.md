# Windows

[English](../en/windows.md) · **Português (Brasil)** · [Voltar ao README](../../README.pt-BR.md)

## Antes de começar

- Windows 10 ou 11, 64 bits.
- Driver NVIDIA 580 ou mais novo, do site da NVIDIA ou do NVIDIA app. O pacote traz as
  bibliotecas CUDA.
- Placas: Turing ou mais novas. Veja [qual tier sua placa minera](../../README.pt-BR.md#qual-tier-minha-placa-minera).
- Espaço em disco ao lado do miner para o modelo de cada tier minerado.

## Instalar

1. Baixe o `fear-miner-windows-0.0.31.zip` na
   [página da release](https://github.com/fearke85/fear-miner/releases/tag/v0.0.31).
2. Extraia numa pasta só dele, por exemplo `C:\fear-miner`.
3. Clique com o botão direito no `start.bat` e escolha **Editar** (ou abra no Bloco de Notas).

## Configurações no start.bat

| Linha | O que colocar |
| --- | --- |
| `WALLET` | Seu endereço Keryx, `keryx:...` |
| `WORKER` | Um nome para este PC na pool |
| `POOL` | A pool, por exemplo `stratum+tcp://krx.suprnova.cc:4404` |
| `NODE` | Só solo: `grpc://IP:PORTA` do seu node. Deixe `POOL=` vazio |
| `ESCROW_CERT` | Só solo, primeira execução: os 128 caracteres hex da sua carteira. Veja [solo.md](solo.md) |
| `DEVICES` | `all`, ou as placas que vão minerar, por exemplo `0,2,5` |
| `EXTRA` | Outras opções, por exemplo `--tier 0` |
| `STATS` | Endereço da API de stats. `0.0.0.0:4060` abre para a sua rede |

Todas as opções estão em [configuration.md](configuration.md).

## Rodar

Salve o `start.bat` e dê dois cliques nele. A primeira execução baixa o modelo, o que leva alguns
minutos. Deixe a janela aberta: fechar a janela para o miner.

## Atualizar para uma versão nova

Extraia o zip novo por cima da pasta antiga e copie suas configurações para o `start.bat` novo.
Modelos e arquivos de escrow ficam em `data` e são mantidos.

## Onde fica cada coisa

| O quê | Onde |
| --- | --- |
| Log com avisos, pedidos perdidos e relatórios de crash | `log.txt` ao lado do `fear-miner.exe` |
| Modelos, arquivos de escrow | `data`. Defina `FEAR_DATA_DIR` para mudar o local |
| Hashrate e shares | `http://127.0.0.1:4060/stats` no navegador |
