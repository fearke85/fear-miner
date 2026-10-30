# Mineração solo

[English](../en/solo.md) · **Português (Brasil)** · [Voltar ao Keryx](../../README.pt-BR.md)

Na mineração solo, os blocos vão para o seu próprio node Keryx, em vez de uma pool.

## O que você precisa

- Um node Keryx sincronizado, **keryx-node 1.6.6 ou mais novo** (obrigatório desde o H15), com a
  porta gRPC acessível a partir da rig.
- Sua carteira, para autorizar a rig uma vez.

## Apontar o miner para o seu node

| Plataforma | Configuração |
| --- | --- |
| HiveOS | Pool URL `grpc://IP:PORTA`, wallet template `%WAL%` |
| Linux | Tire o comentário da linha solo no `start-keryx.sh` e defina `-node grpc://IP:PORTA` |
| Windows | Tire o comentário da linha solo no `start-keryx.bat` e defina `-node grpc://IP:PORTA` |

Exemplo: `grpc://192.168.1.20:22110`. Use `grpc://`, não `http://` nem um `IP:PORTA` sem prefixo.

## Autorizar a rig (só na primeira execução)

1. Inicie o miner. O log mostra `Escrow key to authorise in your wallet: ...`.
2. Na carteira, abra **Authorise a miner** e cole essa chave. A carteira devolve uma linha de 128
   caracteres hex: o escrow cert.
3. Passe o cert para o miner e inicie de novo:
   - HiveOS, Extra config arguments: `-- --escrow-cert COLE_OS_128_CARACTERES_HEX`
   - Linux: acrescente `--escrow-cert ...` na linha solo do `start-keryx.sh`
   - Windows: acrescente `--escrow-cert ...` na linha solo do `start-keryx.bat`

Essa execução salva o cert. As próximas carregam o arquivo, então você pode tirar o cert das
configurações.

O cert vale para um endereço de carteira e para a chave de escrow desta rig. Se trocar a carteira,
autorize a rig de novo. Guarde os arquivos de escrow ao reinstalar ou mudar o miner de lugar:

| Plataforma | Arquivos de escrow |
| --- | --- |
| HiveOS | `/var/lib/fear-miner/escrow/<carteira>/` |
| Linux, Windows | `keryx/escrow/<carteira>/` ao lado do miner |

`<carteira>` é o endereço de pagamento, com `:` escrito como `_`. Uma atualização copia um escrow
que estava solto para essa pasta e guarda os arquivos antigos ao lado, com o sufixo `.pre-layout`.

## Pedidos de IA e strikes

A rede manda pedidos de IA aos mineradores de cada tier, e todo minerador daquele tier precisa
responder a tempo. Um pedido que a sua rig não responde conta como strike contra o seu endereço de
pagamento. O miner responde sozinho. Mantenha ele rodando, mantenha as placas estáveis e confira o
`log.txt`: cada pedido tem uma linha lá, e uma linha `MISSED` diz por que um pedido atrasou.

Se você roda várias rigs no mesmo endereço de pagamento, cada tier que qualquer uma delas minera
precisa ser respondido por pelo menos uma delas.

## Rigs de pool e escrow

Uma rig de pool pode resgatar o escrow maduro por um node enquanto continua minerando na pool:
adicione `-- --escrow-claim grpc://IP:PORTA` (HiveOS) ou `--escrow-claim grpc://IP:PORTA` na
linha da pool.
