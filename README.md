# Projeto Teste Raptor: Hello World com Zephyr OS

Este projeto demonstra o uso do **Zephyr OS** para exibir a mensagem **"Hello World! This is Raptor!"** em um ambiente de simulação utilizando o **QEMU**.

---

## Relatório Técnico

### Introdução
Este projeto tem como objetivo a implementação de um **Sistema Operacional de Tempo Real** (RTOS) para sistemas embarcados utilizando o **Zephyr OS**. A aplicação simula o funcionamento de um hardware virtualizado usando o **QEMU**, exibindo a mensagem `"Hello World! This is Raptor!"` no console.  

Para este projeto, utilizei minha máquina pessoal configurada com o sistema operacional **Arch Linux**.

### Configuração do Ambiente
Para configurar o ambiente de desenvolvimento, segui os seguintes passos:

- **Instalação de Dependências**: Ferramentas essenciais como **QEMU**, **CMake**, **Ninja** e pacotes Python.
- **Criação de um Ambiente Virtual**: Uso do **virtualenv** para isolar as dependências do projeto.
- **Uso do Zephyr SDK**: Utilização do **Zephyr SDK** para compilar e emular o código no QEMU.

### Implementação
O código principal (`src/main.c`) utiliza a função `printk()` para imprimir a mensagem no console.

### Desafios Enfrentados
- **Configuração Inicial**: Instalar e configurar o Zephyr SDK na minha máquina, incluindo as dependências do Python e do QEMU, foi um desafio, pois, sendo ferramentas novas para mim, precisei ler a documentação e realizar testes para entender seu funcionamento.
  
- **Refatoração e Organização do Código**: Melhorar e limpar o código base do exemplo foi desafiador devido à grande quantidade de arquivos e diretórios interligados. O objetivo era manter a estrutura modular para permitir futuras expansões do projeto.

### Melhorias Futuras
- **Execução em Hardware Físico**: Expandir o projeto para rodar em hardware embarcado real.
- **Integração com Sensores**: Implementar drivers para sensores e dispositivos externos.

### Conclusão
O projeto demonstra a implementação de um sistema de tempo real utilizando o Zephyr OS em um ambiente virtualizado com QEMU, exibindo a mensagem `"Hello World! This is Raptor!"` no console.

---

## Métodos que usei para a instalação e Execução no Arch Linux 

A seguir, estão os meus passos para configurar e executar o projeto.
> Use-os para auxiliar no teste do projeto

### 1. Instalar o Yay
O **yay** é um helper de AUR de minha preferencia utilizado para instalar pacotes no Arch.

```bash
sudo pacman -S yay
```
> Caso no seja do seu agrado substitua `yay` por `sudo pacman`: 


### 2. Instalar o QEMU
**QEMU** é necessário usado para emular o hardware.

```bash
yay -S qemu-full vde2
```
> Comando no **Debian**: 
> ```bash
> sudo apt install -y qemu-system-x86 qemu-utils vde2
> ```

### 3. Instalar Bibliotecas para o Zephyr
Instalei as bibliotecas essenciais para o desenvolvimento do Zephyr OS, conforme recomendado na documentação.

```bash
yay -S cmake ninja dtc
```
> Comando no **Debian**: 
> ```bash
> sudo apt install -y cmake ninja-build device-tree-compiler
> ```

### 4. Instalar os Pacotes Python
Instalei os pacotes Python necessários para o ambiente virtual do projeto.

```bash
yay -S python python-virtualenv python-pip python-pyelftools
```
> Comando no **Debian**: 
> ```bash
> sudo apt install -y python3 python3-venv python3-pip python3-pyelftools
> ```


### 5. Criar o Ambiente Virtual
Criei um diretório para o ambiente virtual.

```bash
sudo apt install -y qemu-system-x86 qemu-utils vde2
mkdir -p raptor-env
cd raptor-env
python -m venv .venv
source .venv/bin/activate
```

### 6. Instalar o West no Ambiente Virtual
**West** é o gerenciador de projetos oficial do Zephyr.

```bash
pip install west pyelftools
```

### 7. Clonar o Projeto Exemplo
Clonei o repositório do Zephyr com o projeto de exemplo para a minha máquina .

```bash
git clone https://github.com/zephyrproject-rtos/example-application.git
```

### 8. Inicializar o West
Inicializei os submódulos do West.

```bash
west init -l
west update
```

### 9. Modificar o Código para Exibir a Mensagem Desejada
Editei as variáveis do projeto e o arquivo `app/src/main.c` para exibir a mensagem personalizada:  
**"Hello World! This is Raptor!"**

### 10. Limpeza do Projeto
Analisei a estrutura do projeto e removi arquivos e diretórios desnecessários.

### 11. Compilar o Projeto

```bash
west build -b qemu_x86 app --pristine
```
> O parâmetro `--pristine` garante que a pasta de build seja completamente limpa antes da compilação.  
> Caso o comando `pristine` não funcione corretamente, exclua a pasta manualmente:
> ```bash
> rm -rf build
> ```

### 12. Executar o Projeto no QEMU
Para rodar o projeto no QEMU, utilize o comando:

```bash
west build -t run
```

