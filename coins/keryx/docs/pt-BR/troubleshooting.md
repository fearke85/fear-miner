# Problemas do Keryx

[English](../en/troubleshooting.md) · **Português (Brasil)** · [Voltar ao Keryx](../../README.pt-BR.md)

Problemas específicos do Keryx. Os que podem acontecer com qualquer moeda (versão antiga no
HiveOS, "no CUDA device", risers, crashes por overclock) estão na
[solução de problemas geral](../../../../docs/pt-BR/troubleshooting.md).

## Shares rejeitados desde 30/10/2026

Versões anteriores à 1.5.0 são inválidas desde o hard fork H15. Instale a
[versão atual](../../../../README.pt-BR.md). Solo: atualize o seu node para o keryx-node 1.6.6 ou
mais novo.

## "no device fits a tier"

A mensagem lista a memória de cada placa e o que o menor tier precisa.

- Placas com menos de 8 GB não são suportadas.
- Pascal (GTX 10xx, P104/P106) e anteriores não são suportadas.
- No Linux ou no Windows, o monitor e os programas abertos ocupam memória da placa. Feche-os, ou
  use uma rig sem monitor com `--headless`.
- Tire um `--tier` que peça mais do que as placas conseguem.

## Falta espaço em disco

O miner confere o disco antes de baixar o modelo e diz quanto precisa, por exemplo
`it needs 10.1 GB free in /var/lib/fear-miner/models/..., 4.1 GB available`. Libere espaço, ou mude
os modelos de lugar com `--models-dir`. Os tamanhos por tier estão na
[página do Keryx](../../README.pt-BR.md#qual-tier-minha-placa-minera). Um download interrompido
continua de onde parou.

## Strikes ou linhas `MISSED`

Cada pedido de IA tem uma linha no `log.txt`, e uma linha `MISSED` diz em qual etapa o pedido estava
quando o tempo acabou. Causas comuns: uma placa que travou, disco lento ou pouca RAM, uma rig
reiniciada no meio de um pedido. Se os strikes continuarem, mande o log no
[Discord](https://discord.gg/uK93NPAhbd).

Nos primeiros dias depois do H15, se a sua rig levar um strike, pare o miner e mande o `log.txt` no
[Discord](https://discord.gg/uK93NPAhbd), para a causa ser encontrada antes de se repetir.

Uma placa que trava enquanto responde pedidos de IA continua minerando, mas fica um tempo sem pegar
pedidos de IA, e as outras placas respondem por ela. O relatório de crash no `log.txt` cita a placa.

## Hashrate baixo numa placa

- Compare com outras placas do mesmo modelo no [Discord](https://discord.gg/uK93NPAhbd).
