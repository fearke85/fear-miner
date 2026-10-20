# Solução de problemas

[English](../en/troubleshooting.md) · **Português (Brasil)** · [Voltar ao README](../../README.pt-BR.md)

Problemas que podem acontecer com qualquer moeda. Os problemas de cada moeda estão na página dela:
[Keryx](../../coins/keryx/docs/pt-BR/troubleshooting.md).

Comece pelo `log.txt`: `/var/lib/fear-miner/log.txt` no HiveOS, ao lado do miner no Linux e no
Windows. Ele guarda avisos, erros, o motivo de o miner ter parado e um relatório depois de um
crash. Cada linha traz a versão do miner.

## O HiveOS continua rodando uma versão antiga

A versão está no nome do arquivo da Installation URL. Troque os dois lugares da URL (`v0.0.XX` e
`fear-miner-0.0.XX.tar.gz`) e aplique o flight sheet.

## "no CUDA device"

A mensagem diz qual é o caso:

- placas desativadas no HiveOS (desativadas nas configurações da rig, ou power limit 1 no perfil
  de OC);
- placas antigas demais para o driver ou para este miner;
- uma atualização de driver que pede reinicialização.

## Uma placa aparece como travada durante o carregamento

Uma linha do log cita a placa e o endereço PCI dela e termina com `Reseat or swap its riser`. As
outras placas continuam minerando. Reencaixe ou troque o riser ou o cabo dessa placa.

## O miner reiniciou depois de um crash

A próxima execução grava um relatório de crash no `log.txt`: a placa, os offsets de overclock,
temperatura, consumo, link PCIe, os erros de GPU que o sistema registrou e a causa mais provável. A
correção mais comum é baixar o overclock de memória ou de core dessa placa. A
[tabela de overclocks](https://www.julianocaju.com.br/overclocks/) do Juliano Caju traz valores por
placa e moeda.

No Windows, o `start-keryx.bat` inicia o miner de novo depois de um crash desses. Um
`start-keryx.bat` de uma versão antiga para em `Pressione qualquer tecla para continuar`: copie a sua
linha para o novo.

## "Permission denied" nos arquivos ou pastas do miner

- **Linux, arquivos com dono root:** um miner iniciado com `sudo` antes da 1.2.1 deixou `keryx`, a
  pasta de escrow e o `log.txt` com dono root. Inicie esta versão uma vez com `sudo` a partir do
  seu próprio login: ela devolve tudo ao dono da pasta do miner. Um serviço do systemd ou um login
  de root mantém os arquivos como root; rode `sudo chown -R "$USER": .` na pasta do miner. Mais em
  [Linux, com sudo](linux.md#com-sudo).
- **HiveOS ou outra execução como root, `Failed to create escrow key directory ... Permission
  denied`:** a 1.2.1 parava assim quando a pasta do miner pertencia a um usuário comum. Corrigido
  na 1.3.0: atualize o miner.

## Pedir ajuda

Pergunte no [Discord](https://discord.gg/uK93NPAhbd) ou
[abra uma issue](https://github.com/fearke85/fear-miner/issues/new/choose). Informe a versão do
miner, a plataforma, a moeda, suas placas, se é pool ou solo, e anexe o `log.txt`.
