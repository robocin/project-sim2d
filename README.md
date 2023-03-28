# project-sim2d 🤖🔵 🇧🇷

Esse repositório tem como objetivo discorrer um pouco sobre a categoria de Simulação 2D de forma introdutória, bem como disponibilizar e demonstrar o setup da base [StarterAgent2D](https://github.com/naderzare/StarterAgent2D/) e também da [StarterLibRCSC](https://github.com/naderzare/StarterLibRCSC) utilizados para a categoria de Simulação 2D no processo seletivo do RobôCIn.

## Um pouco sobre a categoria
...

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
