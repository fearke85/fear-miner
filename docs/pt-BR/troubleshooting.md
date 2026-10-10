# Solução de problemas

[English](../en/troubleshooting.md) · **Português (Brasil)** · [Voltar ao README](../../README.pt-BR.md)

Comece pelo `log.txt`: `/var/lib/fear-miner/log.txt` no HiveOS, ao lado do miner no Linux e no
Windows. Ele guarda avisos, erros, o motivo de o miner ter parado, uma linha por pedido de IA e um
relatório depois de um crash. Cada linha traz a versão do miner.

## Shares rejeitados desde 09/10/2026

Versões anteriores à 0.0.22 são inválidas desde o hard fork H14. Instale a
[versão atual](../../README.pt-BR.md). Solo: atualize o seu node para o keryx-node 1.6.4 ou mais
novo.

## O HiveOS continua rodando uma versão antiga

A versão está no nome do arquivo da Installation URL. Troque os dois lugares da URL (`v0.0.XX` e
`fear-miner-0.0.XX.tar.gz`) e aplique o flight sheet.

## "no CUDA device"

A mensagem diz qual é o caso:

- placas desativadas no HiveOS (desativadas nas configurações da rig, ou power limit 1 no perfil
  de OC);
- placas antigas demais para o driver ou para este miner (Pascal e anteriores não são suportadas);
- uma atualização de driver que pede reinicialização.

## "no device fits a tier"

A mensagem lista a memória de cada placa e o que o menor tier precisa.

- Placas com menos de 8 GB precisam de outra placa na rig que responda o tier 0, e de 2 GB de RAM
  livre.
- No Linux ou no Windows, o monitor e os programas abertos ocupam memória da placa. Feche-os, ou
  use uma rig sem monitor com `--headless`.
- Tire um `--tier` que peça mais do que as placas conseguem.

## Falta espaço em disco

O miner confere o disco antes de baixar e diz quanto precisa, por exemplo
`it needs 10.1 GB free in /var/lib/fear-miner/models/..., 4.1 GB available`. Libere espaço, ou mude
os modelos de lugar com `--models-dir` (HiveOS) ou `FEAR_DATA_DIR` (Linux, Windows). Os tamanhos
por tier estão no [README](../../README.pt-BR.md#qual-tier-minha-placa-minera). Um download
interrompido continua de onde parou.

## Uma placa aparece como travada durante o carregamento

Uma linha do log cita a placa e o endereço PCI dela e termina com `Reseat or swap its riser`. As
outras placas continuam minerando. Reencaixe ou troque o riser ou o cabo dessa placa.

## O miner reiniciou depois de um crash

A próxima execução grava um relatório de crash no `log.txt`: a placa, os offsets de overclock,
temperatura, consumo, link PCIe, os erros de GPU que o sistema registrou e a causa mais provável. A
correção mais comum é baixar o overclock de memória ou de core dessa placa. Uma placa que trava
enquanto responde pedidos de IA continua minerando, mas fica um tempo sem pegar pedidos de IA, e as
outras placas respondem por ela.

## Strikes ou linhas `MISSED`

Cada pedido de IA tem uma linha no `log.txt`, e uma linha `MISSED` diz em qual etapa o pedido estava
quando o tempo acabou. Causas comuns: uma placa que travou, disco lento ou pouca RAM, uma rig
reiniciada no meio de um pedido. Se os strikes continuarem, mande o log no Discord.

## Hashrate baixo numa placa

- Uma placa num link PCIe estreito (riser x1) que minera um tier maior que a memória dela chega ao
  hashrate cerca de dois minutos depois da partida. Um link mais rápido dá mais hashrate.
- Compare com outras placas do mesmo modelo no [Discord](https://discord.gg/uK93NPAhbd).

## Pedir ajuda

Pergunte no [Discord](https://discord.gg/uK93NPAhbd) ou
[abra uma issue](https://github.com/fearke85/fear-miner/issues/new/choose). Informe a versão do
miner, a plataforma, suas placas, se é pool ou solo, e anexe o `log.txt`.
