# Especificações de Virtualização

Este documento especifica os requisitos e as configurações recomendadas para a execução da máquina virtual do projeto.

A máquina virtual foi desenvolvida e validada utilizando o **Oracle VM VirtualBox**. As configurações apresentadas abaixo correspondem ao ambiente utilizado durante os testes e devem ser consideradas a configuração de referência. Alguns parâmetros podem ser ajustados de acordo com as características do computador hospedeiro, desde que os requisitos funcionais da máquina virtual sejam preservados.

## Configurações Gerais

A configuração de referência da máquina virtual utiliza:

- **Software de virtualização:** Oracle VM VirtualBox
- **Firmware:** UEFI
- **Memória RAM:** 8192 MB
- **CPU:** 2 Cores
- **Aceleração de hardware:** habilitada
- **Memória de vídeo:** 64 MBV
- **Controlador gráfico:** VMSVGA
- **Rede:** NAT
- **USB:** USB 3.0

A quantidade de CPU, RAM e memória de vídeo pode ser ajustada conforme os recursos disponíveis no computador hospedeiro, desde que seja suficiente para a execução dos softwares instalados na VM.

## Disco Virtual Imutável

O disco principal da máquina virtual é distribuído no formato **VDI**, próprio do VirtualBox, e configurado como **imutável**.

O objetivo dessa configuração é garantir que a VM distribuída mantenha seu estado original. Alterações realizadas durante a utilização da máquina virtual não devem modificar permanentemente a imagem distribuída.

Dessa forma, a VM pode ser utilizada como um ambiente descartável: alterações no sistema, instalações adicionais e outros arquivos gravados no disco virtual são perdidos quando o disco é restaurado ao seu estado original, conforme o mecanismo de discos imutáveis do VirtualBox.

Arquivos que precisem sobreviver ao ciclo de utilização da VM devem, portanto, ser armazenados fora do disco imutável, utilizando os mecanismos de compartilhamento descritos neste documento.

## Integração com o VirtualBox

A VM foi projetada tendo o **VirtualBox** como plataforma de virtualização de referência. Para fornecer integração com o hospedeiro, a instalação inclui os componentes do **VirtualBox Guest Additions** disponibilizados pelo gerenciador de pacotes do sistema operacional convidado.

Os Guest Additions são utilizados principalmente para fornecer:

- suporte a pastas compartilhadas;
- integração entre o sistema convidado e o hospedeiro;
- suporte aos recursos de integração disponibilizados pelo VirtualBox.

A instalação dos componentes pelo gerenciador de pacotes, em vez da instalação manual a partir da imagem fornecida pelo VirtualBox, é preferível para manter a instalação integrada ao sistema operacional convidado e facilitar sua manutenção.

A VM não deve, entretanto, depender de recursos exclusivos dos Guest Additions para sua execução básica. Caso seja executada em outro hipervisor, como VMware ou QEMU/KVM, os componentes específicos do VirtualBox podem permanecer instalados sem necessariamente interferir na execução do sistema, mas os recursos de integração fornecidos por eles não estarão disponíveis.

## USB Passthrough

O uso de dispositivos USB conectados ao computador hospedeiro foi considerado um requisito do ambiente.

Por esse motivo, a configuração de referência utiliza **USB 3.0**, permitindo que dispositivos compatíveis, como pendrives e smartphones, possam ser encaminhados para a máquina virtual através do mecanismo de USB passthrough do VirtualBox.

A disponibilidade efetiva do dispositivo dentro da VM depende da configuração do hospedeiro e das permissões necessárias para que o VirtualBox acesse o dispositivo USB.

## Pastas Compartilhadas

A VM utiliza uma pasta compartilhada para facilitar a transferência de arquivos entre o sistema convidado e o computador hospedeiro.

Uma pasta denominada **`Compartilhado`** será disponibilizada na área de trabalho da VM. Essa pasta corresponde a uma pasta localizada no computador hospedeiro e é montada dentro do sistema convidado através do mecanismo de **Shared Folders** do VirtualBox.

Durante os testes, a pasta do hospedeiro foi configurada em:

`%LOCALAPPDATA%\LabVM\Compartilhado`

O caminho no hospedeiro não é considerado um requisito fixo da VM e pode ser alterado conforme a organização utilizada no computador onde a VM for executada.

O usuário da VM possui permissões de leitura e escrita na pasta compartilhada. Para isso, seu usuário é associado ao grupo `vboxsf`, utilizado pelo VirtualBox para controlar o acesso às pastas compartilhadas.

A pasta `Compartilhado` deve ser utilizada para arquivos que precisem ser transferidos entre o hospedeiro e a VM, especialmente porque o disco principal da VM é imutável.

Quando conveniente, atalhos para a pasta podem ser disponibilizados na **Área de Trabalho** e em **Documentos**, facilitando seu acesso pelo usuário.

## Requisitos para o Hospedeiro

Para utilizar integralmente os recursos de integração descritos neste documento, o computador hospedeiro deve possuir:

- Oracle VM VirtualBox instalado;
- suporte à virtualização por hardware habilitado;
- recursos de CPU, memória e armazenamento suficientes para executar a VM;
- suporte a USB, quando o passthrough de dispositivos for necessário;
- uma pasta do hospedeiro configurada como Shared Folder, quando o compartilhamento de arquivos for necessário.

O uso das pastas compartilhadas e de outros recursos de integração com o hospedeiro depende do VirtualBox e dos respectivos Guest Additions. A execução do sistema operacional convidado, por outro lado, deve permanecer independente desses recursos sempre que possível.
