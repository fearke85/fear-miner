# Windows

[English](../en/windows.md) · **Português (Brasil)** · [Voltar ao README](../../README.pt-BR.md)

Como instalar o fear-miner no Windows, para qualquer moeda. Os valores da sua moeda estão na página
dela: [Keryx](../../coins/keryx/README.pt-BR.md#runsh-linux-e-startbat-windows).

## Antes de começar

- Windows 10 ou 11, 64 bits.
- Driver NVIDIA 580 ou mais novo, do site da NVIDIA ou do NVIDIA app. O pacote traz as
  bibliotecas CUDA.
- Uma placa que a sua moeda suporte, e o espaço em disco que a página da moeda pede, ao lado do
  miner.

## Instalar

1. Baixe o `fear-miner-windows-1.1.0.zip` na
   [página da release](https://github.com/fearke85/fear-miner/releases/tag/v1.1.0).
2. Extraia numa pasta só dele, por exemplo `C:\fear-miner`.
3. Clique com o botão direito no `start.bat` e escolha **Editar** (ou abra no Bloco de Notas).

## Configurações no start.bat

`WALLET`, `POOL`, `NODE` e qualquer linha que a sua moeda acrescente usam os valores da página da
moeda.

| Linha | O que colocar |
| --- | --- |
| `WALLET` | Seu endereço de pagamento |
| `WORKER` | Um nome para este PC na pool |
| `POOL` | A pool, `stratum+tcp://host:porta` |
| `NODE` | Só solo: `grpc://IP:PORTA` do seu node. Deixe `POOL=` vazio |
| `DEVICES` | `all`, ou as placas que vão minerar, por exemplo `0,2,5` |
| `EXTRA` | Opções da moeda |
| `STATS` | Endereço da API de stats. `0.0.0.0:4060` abre para a sua rede |

Opções do miner: [options.md](options.md).

## Rodar

Salve o `start.bat` e dê dois cliques nele. Deixe a janela aberta: fechar a janela para o miner.

## Atualizar para uma versão nova

Extraia o zip novo por cima da pasta antiga e copie suas configurações para o `start.bat` novo. O
que o miner guarda fica em `data` e é mantido.

## Onde fica cada coisa

| O quê | Onde |
| --- | --- |
| Log com avisos, erros e relatórios de crash | `log.txt` ao lado do `fear-miner.exe` |
| Dados que o miner guarda | `data`. Defina `FEAR_DATA_DIR` para mudar o local |
| Hashrate e shares | `http://127.0.0.1:4060/stats` no navegador |
