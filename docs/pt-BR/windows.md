# Windows

[English](../en/windows.md) · **Português (Brasil)** · [Voltar ao README](../../README.pt-BR.md)

Como instalar o fear-miner no Windows, para qualquer moeda. Os valores da sua moeda estão na página
dela: [Keryx](../../coins/keryx/README.pt-BR.md#start-keryxsh-linux-e-start-keryxbat-windows).

## Antes de começar

- Windows 10 ou 11, 64 bits.
- Driver NVIDIA 580 ou mais novo, do site da NVIDIA ou do NVIDIA app. O pacote traz as
  bibliotecas CUDA.
- Uma placa que a sua moeda suporte, e o espaço em disco que a página da moeda pede, ao lado do
  miner.

## Instalar

1. Baixe o `fear-miner-windows-1.2.0.zip` na
   [página da release](https://github.com/fearke85/fear-miner/releases/tag/v1.2.0).
2. Extraia numa pasta só dele, por exemplo `C:\fear-miner`.
3. Clique com o botão direito no `start-keryx.bat` e escolha **Editar** (ou abra no Bloco de Notas).

## Configurações no script de start

Cada moeda tem o seu script. Para o Keryx, edite o `start-keryx.bat`. Deixe uma linha sem
comentário, a da pool ou a do solo, e coloque o seu endereço em `-wallet`. A pool, o node e os
outros valores estão na página da moeda.

As outras opções vão nessa mesma linha. Opções do miner: [options.md](options.md).

## Rodar

Salve o `start-keryx.bat` e dê dois cliques nele. Deixe a janela aberta: fechar a janela para o miner.
Quando o CUDA morre numa placa, o miner sai e o script inicia ele de novo depois de 3 segundos.

## Atualizar para uma versão nova

Extraia o zip novo por cima da pasta antiga e copie a sua linha para o `start-keryx.bat` novo. O
que o miner guarda fica em `keryx` e é mantido. Uma pasta `data` antiga é aproveitada de lá.

## Onde fica cada coisa

| O quê | Onde |
| --- | --- |
| Log com avisos, erros e relatórios de crash | `log.txt` ao lado do `fear-miner.exe` |
| Dados que o miner guarda | `keryx` (`models\`, e `escrow\<carteira>\`). Defina `FEAR_DATA_DIR` para mudar o local |
| Hashrate e shares | `http://127.0.0.1:4060/stats` no navegador |
