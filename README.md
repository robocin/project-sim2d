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
Para começar a desenvolver na categoria são necessárias algumas ferramentas que dão suporte a categoria, ao ambiente e que são utilizadas constantemente na execução de partidas e desenvolvimento do código.

- Ubuntu e pré-requisitos:
  - Antes de tudo, é bem importante que o sistema operacional para a instalação das demais ferramentas seja o **Ubuntu 18.04 ou superior**. Recomendamos fortemente o Ubuntu 20.04 e é o que utilizamos atualmente no laboratório. É importante ressaltar que o ambiente **não** executa em windows
  - Além do Ubuntu, é preciso que o sistema possua as devidas dependências:
    - Compilador de C++:  g++ (que suporte C++ >=  14)
    - autoconf
    - automake
    - flex
    - bison
    - boost >= 1.44
    - libtool
    
  - Em caso de Ubuntu 18.04, 20.04 ou 22.04:
    - O seguinte comando poderá resolver todos pré-requisitos:
      ```bash
      sudo apt-get update
      sudo apt install build-essential automake cmake autoconf libtool flex bison libboost-all-dev
      ```
    
    - Para verificar se o ambiente tem g++, teste com:
      ```bash
      g++ -v
      ```
      
    - Para verificar se o flex ou bison foi instalado, teste com:
      ```bash
      which flex
      which bison
      ```
      
- Robocup Soccer Simulation Server (rcssserver)
  - Utilize o link abaixo para fazer o download do **.tar** da release 17.0.1 do servidor.
  
    [Releases · rcsoccersim/rcssserver](https://github.com/rcsoccersim/rcssserver/releases)

    - Após obter o arquivo compactado, extraia e instale.
      ```bash
      # extrair o arquivo baixado
      tar xzvfp rcssserver-x.x.x.tar.gz

      # Entre no diretório
      cd rcssserver-x.x.x

      # Instale
      sudo ./configure
      sudo make
      sudo make install
      ```

- Robocup Soccer Simulation Monitor (rcssmonitor)
  - Utilize o link abaixo para fazer o download do **.tar** da release mais recente do monitor.
    
    [Release rcssmonitor-17.0.0 · rcsoccersim/rcssmonitor](https://github.com/rcsoccersim/rcssmonitor/releases/tag/rcssmonitor-17.0.0)

  - Após obter o arquivo compactado, extraia e instale.
    ```bash
    # extrair o arquivo baixado
    tar xzvfp rcssmonitor-x.x.x.tar.gz

    # Entre no diretório
    cd rcssmonitor-x.x.x

    # Instale
    sudo ./configure
    sudo make
    sudo make install
    ```

    - *Troubleshooting:* 
      - Em caso de "Qt5Core could not be found". Rode:
        ```bash
        sudo apt-get install qtbase5-dev qtchooser qt5-qmake qtbase5-dev-tools
        ```

- Formation Edit (FEdit):
  - O FEdit é uma ferramenta que serve para editar formações conforme o desenvolvedor queira. Útil para modificações pontuais nas formações ou até mesmo criar uma formação única. Para realizar a instalção é necessária a instalação da libRCSC, portanto, siga o passo a passo do **setup do ambiente** antes de instalar.

  - Faça o downloand da versão mais atualizada do fedit neste [Link](https://github.com/helios-base/fedit2)
    - *Troubleshooting:* 
      - É importante que a linguagem e região do seu Ubuntu esteja em EN-US
      - Em caso de erro de cast na instalção, altere o seguinte arquivo:
        - fedit2/tool/average_formation.cpp e modificar a linha 98 para ter o cast de bool 
        - ``` return (bool) M_target_formation; ```

## Setup do ambiente
### Instalação da biblioteca LibRCSC:
Faça o download da release mais recente da StarterLibRCSC nesse [Link](https://github.com/naderzare/StarterLibRCSC/releases)
  ```bash
  cd StarterLibRCSCPath
  ./configure
  make  
  sudo make install
  ```  

### Como usar o StarterAgent2D
O código que se encontra nesse repositório é o StarterAgent2D, basta clonar e seguir os próximos passos.

#### Pela primeira vez
  ```bash
  cd StarterAgent2DPath
  ./configure
  make  
  ```
  
#### Depois de qualquer mudança, recompile
  ```bash
  cd StarterAgent2DPath/src
  make
  ```
  
#### Executar o time
  ```bash
  cd src
  ./start.sh -t teamname
  ```

### Como rodar uma partida entre dois times
- Para cada comando será necessário um novo terminal.
#### Certifique-se de que a instalação da StarterLibRCSC foi feita sem erros.
#### Primeiramente, em qualquer diretório, execute o servidor:
  ``` rcssserver ```

#### Para visualizar a partida, em qualquer diretório, execute o monitor:
  ``` rcssmonitor ```

#### Com o servidor e o monitor rodando, no diretório do starterAgent, inicialize o primeiro time:
  ```bash
  cd src
  ./start.sh -t teamname1
  ```
  
#### Inicialize o segundo time, no diretório do starterAgent, em outro terminal:
  ```bash
  cd src
  ./start.sh -t teamname2
  ```
  
#### Por fim, você verá os dois times inicializados no monitor, basta dar o kick-off na partida.  
