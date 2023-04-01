# project-sim2d 🤖🔵 🇧🇷

Esse repositório tem como objetivo discorrer um pouco sobre a categoria de Simulação 2D de forma introdutória, bem como disponibilizar e demonstrar o setup da base [StarterAgent2D](https://github.com/naderzare/StarterAgent2D/) e também da [StarterLibRCSC](https://github.com/naderzare/StarterLibRCSC) utilizados para a categoria de Simulação 2D no processo seletivo do RobôCIn.

## Um pouco sobre a categoria
A categoria de simulação 2D no RobôCIn surgiu no ano de 2018 e é uma das categorias da maior competição de robótica de futebol do mundo, a RoboCup. Dentre as categorias da competição, simulação 2D tem a melhor aplicabilidade para algoritmos de aprendizado de máquina e inteligência artificial. Diante disso, você pode se perguntar como é o funcionamento dessa categoria. Bom, apesar de não ser muito claro, vamos tentar esclarecer alguns pontos sobre a sim2D.

A simulação consiste em um jogo de futebol entre dois times, cada um com 11 jogadores e 1 treinador, compostos completamente por agentes autônomos, que possuem fatores heterogêneos em suas características e têm uma visão limitada do mundo simulado.

Existem cinco componentes principais responsáveis pelo funcionamento do ambiente de simulação 2D.
- Servidor (rcssserver)
- Cliente (rcssclient)
- Biblioteca básica (librcsc)
- Monitor (rcssmonitor)
- Editor de formações (FEdit)

A figura abaixo mostra o funcionamento do ambiente durante a execução de uma partida.
![rcss2d_diagram](https://user-images.githubusercontent.com/53492989/229315795-ce733e0c-f12c-4cc0-acb8-364aeb2e7d12.png)

O código que temos nesse repositório é a implementação dos agentes autônomos. Estes agentes implementam o Player Client e o Coach, que não está na imagem acima. O cliente é como um único jogador, para fazer um time completo, 11 clientes são iniciados e também um coach. Eles conseguem se comunicar via UDP com o rcssserver trocando mensagens de posição, velocidade, ações, etc. A forma e a quantidade dessas mensagens são definidas no manual da categoria que está disponibilizado no edital do projeto.

Todas as bases de código para agentes de 2D utilizam uma biblioteca comum para a implementação dos agentes, a librcsc. Para a nossa base, como já visto acima, iremos utilizar a [StarterLibRCSC](https://github.com/naderzare/StarterLibRCSC). As libs são responsáveis por implementar a interface de rede UDP com o servidor, a transmissão das mensagens no formato que o servidor entende, a tradução das mensagens nos clientes, entre outras responsabilidades de infraestrutura de rede e comportamento dos agentes que são necessárias para o seu funcionamento.

![2Dbox_diagram](https://user-images.githubusercontent.com/53492989/229316010-cb6164b1-2cdd-46d2-a398-148d941f1d66.png)


## Ferramentas necessárias
...

## Setup
### Instalação da biblioteca LibRCSC:
Download last release of StarterLibRCSC from this [Link](https://github.com/naderzare/StarterLibRCSC/releases)
```bash
cd StarterLibRCSCPath
./configure
make  
sudo make install
```  

### How To Use StarterAgent2D
#### First Time
```bash
cd StarterAgent2DPath
./configure
make  
```
#### After Any Change
```bash
cd StarterAgent2DPath/src
make
```
#### Run
```bash
cd src
./start.sh -t teamname
```
