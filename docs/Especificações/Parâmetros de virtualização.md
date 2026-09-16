# Especificações de Virtualização

Este documento especifica os requisitos e as configurações recomendadas para a execução da máquina virtual do projeto.

A máquina virtual foi desenvolvida e validada utilizando o **Oracle VM VirtualBox**. As configurações apresentadas abaixo correspondem ao ambiente utilizado durante os testes e devem ser consideradas a configuração de referência. Alguns parâmetros podem ser ajustados de acordo com as características do computador hospedeiro, desde que os requisitos funcionais da máquina virtual sejam preservados.

## Configurações Gerais

A configuração de referência da máquina virtual utiliza:

- **Software de virtualização:** Oracle VM VirtualBox
- **Firmware:** UEFI
- **Memória RAM:** 8192 MB
- **CPU:** 2 cores
- **Aceleração de hardware:** habilitada
- **Memória de vídeo:** 64 MB
- **Controlador gráfico:** VMSVGA
- **Rede:** NAT
- **Controladora USB:** USB 3.0
- **Armazenamento:** dois discos virtuais, sendo um imutável e um persistente

A quantidade de CPU, RAM e memória de vídeo pode ser ajustada conforme os recursos disponíveis no computador hospedeiro, desde que seja suficiente para a execução dos softwares instalados na VM.

## Discos Virtuais

A máquina virtual utiliza dois discos virtuais com finalidades distintas:

1. **Disco do sistema:** contém o sistema operacional e os componentes que definem o ambiente da VM. É distribuído no formato **VDI** e configurado como **imutável**.
2. **Disco de dados:** contém os arquivos que devem sobreviver ao ciclo de utilização da VM. É mantido como um disco virtual **mutável**, não estando sujeito ao mecanismo de restauração do disco imutável.

A separação entre os discos permite combinar duas características importantes do ambiente: a possibilidade de restaurar o sistema a um estado conhecido e a persistência seletiva dos arquivos produzidos pelo usuário.

Para informações relacionadas à implementação lógica do uso desses dois discos, veja [Configuração do Sistema Operacional](./Configuração\ do\ Sistema\ Operacional.md).

## Integração VirtualBox

A VM foi projetada tendo o **VirtualBox** como plataforma de virtualização de referência. Para fornecer integração com o hospedeiro, a instalação inclui os componentes do **VirtualBox Guest Additions** disponibilizados pelo gerenciador de pacotes do sistema operacional convidado.

Os Guest Additions são utilizados principalmente para fornecer suporte a pastas compartilhadas, área de trabalho compartilhada, escalonamento de resolução e demais recursos de integração disponibilizados pelo VirtualBox.

No entanto, a VM não depende de recursos exclusivos dos Guest Additions para sua execução básica. Caso seja executada em outro hipervisor, como VMware ou QEMU/KVM, os componentes específicos do VirtualBox permanecem instalados sem necessariamente interferir na execução do sistema, mas os recursos de integração fornecidos por eles não estarão disponíveis.

## USB Passthrough

O uso de dispositivos USB conectados ao computador hospedeiro foi considerado um requisito do ambiente.

Por esse motivo, a configuração de referência utiliza **USB 3.0**, permitindo que dispositivos compatíveis, como pendrives e smartphones, possam ser encaminhados para a máquina virtual através do mecanismo de USB passthrough do VirtualBox.

A disponibilidade efetiva do dispositivo dentro da VM depende da configuração do hospedeiro e das permissões necessárias para que o VirtualBox acesse o dispositivo USB.

Dito isso, o sistema operacional é robusto o bastante para funcionar de modo normal sem essa configuração, embora a funcionalidade prática de inserir dispositivos removíveis diretamente na máquina não está mais disponível.

## Pastas Compartilhadas

A VM utiliza uma pasta compartilhada para facilitar a transferência de arquivos entre o sistema convidado e o computador hospedeiro.

Uma pasta denominada **`Compartilhado`** será disponibilizada na área de trabalho do sistema operacional. Essa pasta corresponde a uma pasta localizada no computador hospedeiro e é montada dentro do sistema convidado através do mecanismo de **Shared Folders** do VirtualBox.

Embora possa ser montada em qualquer lugar, durante os testes a pasta do hospedeiro foi configurada em `%LOCALAPPDATA%\LabVM\Compartilhado` a fim de previnir exclusões acidentais por parte de outros usuários do computador.

O caminho no hospedeiro não é considerado um requisito fixo da VM e pode ser alterado conforme a organização utilizada no computador onde a VM for executada.

Vale ressaltar que durante os testes, por ser conveniente, atalhos para a pasta podem ser disponibilizados na **Área de Trabalho** e em **Documentos** do hospedeiro, facilitando seu acesso pelo usuário.
