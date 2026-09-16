Utilizando as informações disponibilizadas abaixo, escreva a página de documentação denominada "Configuração do Sistema Opreacional". Essa página tem o objetivo de responder ao leitor "Como o ambiente definido cumpre os papeis que um sistema operacional deve cumprir?". Esses papeis foram definidos no documento "Requisitos do Sistema Operacional.md".

# Stub: Informações básicas do sistema operacional
(colocar dados do ADR para ca)


# Stub: Configurações suplementares para o ambiente desktop Cinnamon

O pacote para instalar o ambiente desktop Cinnamon na distribuição Debian, chamado [cinnamon-desktop-environment](https://packages.debian.org/sid/cinnamon-desktop-environment), possui diversas recomendações para .

Como as recomendações escolhidas ainda não foram decididas (spike/discovering), simplesmente aplique um _stub_, ou seja, uma tabela que pode ser preenchida com o formato `| Dependência | Pacote resolutivo |`

Por fim, alterações fora do padrão serão também serão inclusas aqui (ex: uso de um tema diferente, mudança de um atalho de teclado e afins). Assim como acima, por estarmos em processo de descobrimento esse trecho não deve concluida ainda, mas sim apenas colocado como "em progresso"

# Stub: Configurações suplementares para o ambiente i3

Por ser um Tiling Window Manager, a quantidade de configurações suplementares será extensa. Além de correções para funcionamento básico (polkit, definir variável DISPLAY no `systemd --user` e `dbus`). Essa parte da documentação ainda está em processo de descobrimenot

# Stub: Intregração com ambiente virtualizado

A instalação dos componentes \[Guest Util Additions\] pelo gerenciador de pacotes, em vez da instalação manual a partir da imagem fornecida pelo VirtualBox, é preferível para manter a instalação integrada ao sistema operacional convidado e facilitar sua manutenção.

No entanto, o sistema não depende de recursos exclusivos oferecidos pelo Guest Additions para sua execução básica. Caso seja executada em outro hipervisor, como VMware ou QEMU/KVM, os componentes específicos do VirtualBox permanecem instalados sem necessariamente interferir na execução do sistema, mas os recursos de integração fornecidos por eles não estarão disponíveis.

## Subsection: Pasta compartilhada

A VM utiliza uma pasta compartilhada para facilitar a transferência de arquivos entre o sistema convidado e o computador hospedeiro.

Uma pasta denominada **`Compartilhado`** será disponibilizada na área de trabalho do sistema operacional. Essa pasta corresponde a uma pasta localizada no computador hospedeiro e é montada dentro do sistema convidado através do mecanismo de **Shared Folders** do VirtualBox.

Embora possa ser montada em qualquer lugar, durante os testes a pasta do hospedeiro foi configurada em`%LOCALAPPDATA%\LabVM\Compartilhado`

O caminho no hospedeiro não é considerado um requisito fixo da VM e pode ser alterado conforme a organização utilizada no computador onde a VM for executada.

O usuário da VM possui permissões de leitura e escrita na pasta compartilhada. Para isso, seu usuário é associado ao grupo `vboxsf`, utilizado pelo VirtualBox para controlar o acesso às pastas compartilhadas.

A pasta `Compartilhado` deve ser utilizada para arquivos que precisem ser transferidos entre o hospedeiro e a VM, especialmente porque o disco principal da VM é imutável.

Quando conveniente, atalhos para a pasta podem ser disponibilizados na **Área de Trabalho** e em **Documentos**, facilitando seu acesso pelo usuário.

# Stub: informações do disco imutável

Esse trecho originalmente havia sido colocado na documentação de "Parâmetros de virtualização". Além de ser extremamente redundante com a introdução já dada previamente, o trecho inclui algumas. O objetivo é reduzir esse trecho de modo que transmita a mensagem de modo conciso e coeso:

- Existem dois discos: um considerado "imutável" e outro considerado "mutável".
- O sistema operacional alocará pastas específicas (Downloads, Desktop, Documents, /var/cache/apt/archives) através do FSTAB

### Disco do Sistema Imutável

O disco principal da máquina virtual é distribuído no formato **VDI**, próprio do VirtualBox, e configurado como **imutável**.

O objetivo dessa configuração é garantir que a VM distribuída mantenha seu estado original. Alterações realizadas durante a utilização da máquina virtual não devem modificar permanentemente a imagem distribuída.

Dessa forma, alterações no sistema, instalações adicionais, modificações de configurações e arquivos gravados nas partes do sistema que não sejam destinadas à persistência são descartados quando a VM é restaurada ao estado original, conforme o mecanismo de discos imutáveis do VirtualBox.

Essa característica é utilizada deliberadamente para tornar o ambiente de execução **descartável**. Modificações acidentais ou indesejadas realizadas pelo usuário, inclusive alterações em arquivos de configuração e configurações de aplicativos, não devem permanecer entre ciclos de utilização da VM.

A definição de quais diretórios do sistema convidado pertencem ao disco imutável e quais são associados ao disco persistente é especificada no documento de **Sistema Operacional**.

### Disco de Dados Persistente

O segundo disco virtual é utilizado para armazenar dados que devem sobreviver à restauração do disco do sistema.

Esse disco permanece **mutável** e não é configurado como um disco imutável do VirtualBox. Diretórios selecionados do sistema convidado são montados sobre esse disco, de modo que os arquivos armazenados nesses diretórios não façam parte do estado descartável do sistema.

A persistência é, portanto, **seletiva**. O diretório pessoal do usuário não é considerado persistente por completo. Arquivos de configuração, caches e demais dados que não tenham sido explicitamente destinados à persistência continuam armazenados no disco do sistema e são restaurados ao estado original.

A relação dos diretórios montados no disco persistente será definida no documento de **Sistema Operacional**.

Essa abordagem permite, por exemplo, que alterações em arquivos como configurações de shell, configurações de editores e configurações de aplicativos sejam descartadas após a restauração da VM, enquanto documentos e outros arquivos de trabalho selecionados permanecem disponíveis.

### Ausência do Disco Persistente

A disponibilidade do disco de dados não deve ser necessária para a inicialização básica do sistema operacional.

Caso o disco persistente não esteja disponível, os pontos de montagem destinados a ele não serão montados. Os diretórios correspondentes continuarão existindo no sistema de arquivos do disco imutável e poderão ser utilizados normalmente durante aquela sessão.

Nesse cenário, os arquivos gravados nesses diretórios serão temporários e serão perdidos quando o sistema imutável for restaurado.

Essa degradação é intencional: a ausência do disco de dados não deve impedir a execução da VM. Caso o disco seja posteriormente disponibilizado novamente, seus diretórios serão montados durante a inicialização seguinte e os dados persistentes voltarão a estar disponíveis.

Não é necessário implementar um mecanismo adicional para impedir a utilização dos diretórios quando o disco persistente estiver indisponível.

### Considerações sobre o Cache de Pacotes

O disco persistente pode ser utilizado para armazenar caches de arquivos baixados, quando isso trouxer benefício ao funcionamento da VM.

O cache de pacotes do APT, localizado em `/var/cache/apt/archives`, é independente dos metadados utilizados pelo APT para determinar quais pacotes estão disponíveis. Com isso, a persistência do cache de arquivos `.deb` não implica na persistência de um `apt update`.

Os metadados e o estado de gerenciamento de pacotes permanecem no disco do sistema e, portanto, são restaurados juntamente com ele.

A persistência do cache pode permitir que arquivos `.deb` previamente baixados sejam reutilizados em sessões posteriores, reduzindo downloads desnecessários. Entretanto, essa persistência não deve ser interpretada como uma forma de persistir atualizações do sistema.

Atualizações do sistema operacional e alterações no conjunto de pacotes instalados continuam sendo consideradas alterações do disco imutável. Quando uma nova versão do ambiente precisar ser distribuída, o procedimento esperado é atualizar a imagem do sistema e gerar uma nova versão do disco imutável.

O uso de caches persistentes deve permanecer limitado a dados cuja persistência ofereça benefício claro, evitando tornar o estado do sistema parcialmente persistente de maneira desnecessária.

# Stub: Serviços de inicialização automática
(gerado com auxílio de Inteligência Artifical. Sujeito á inúmeras alterações)

O sistema terá rotinas a serem executadas durante a inicialização do sistema. Essas rotinas (scripts) serão divididos em serviços `systemd` independentes. Os serviços documentados até agora são:

## Sincronização Remota

Serviço responsável por:

1. Aguardar a inicialização da conectividade de rede pelo NetworkManager.
2. Verificar se há acesso efetivo à Internet; caso contrário, encerrar a execução sem falhar o sistema.
3. Sincronizar o repositório de configuração com a branch atualmente configurada (`git pull --rebase` ou equivalente).

A presença do disco persistente **não deve ser tratada como requisito para inicialização**. A VM deve continuar funcional mesmo sem o segundo `.vdi` ou mesmo caso o disco do sistema não esteja em estado imutável.

## Verificação de Integridade do Nix

Serviço independente responsável por verificar a integridade do `/nix/store` persistente.

Deve ser executado durante a inicialização, antes que o ambiente seja considerado pronto para uso, de forma que uma corrupção ou alteração não autorizada do Nix Store seja detectada antes de seu conteúdo ser utilizado.

Adicionar: Essa verificação de integridade não deve ocorrer a todo startup. Para isso, um arquivo localizado na nix store (ou solução do próprio Nix se houver) será utilizado para controlar quando a ultima verificação foi realizada. Apenas após um período arbitrário de tempo outra verificação de integridade deve ser realizada de modo não disruptivo (o sistema segue funcionando, apesar do uso de CPU aumentado para a verificação de checksums)

A estratégia de reparo de store corrompido será definida posteriormente.

## Aplicação de Patches

Serviço responsável por executar `patches.sh`.

Deve depender da conclusão bem-sucedida do serviço de **Sincronização Remota**, garantindo que os patches sejam executados sobre a versão mais recente da configuração.

As dependências e a ordem de execução serão declaradas diretamente nas unidades `systemd`, evitando a necessidade de controlar manualmente a ordem através de um script de inicialização monolítico.

## Redefinição de Credenciais

A máquina virtual deve remover, durante a inicialização, credenciais e identificadores pessoais que possam ter sido deixados pelo usuário anterior.

O serviço deve limpar, no mínimo:

* Credenciais armazenadas pelo Git Credential Manager ou por outros mecanismos de credenciais do Git.
* Configurações globais de identidade do Git (`user.name`, `user.email` e equivalentes).
* Chaves privadas e demais credenciais SSH pertencentes ao usuário.
* Chaves e credenciais GPG pertencentes ao usuário.
* Configurações de autenticação relacionadas a essas ferramentas que possam permitir a reutilização de uma sessão anterior.

A limpeza deve ocorrer antes que o ambiente do usuário seja disponibilizado.

Credenciais e configurações pertencentes à infraestrutura da própria máquina virtual, quando existentes, não fazem parte dessa limpeza.

O serviço deve ser idempotente: executá-lo quando não houver credenciais armazenadas deve ser considerado uma operação normal e não deve impedir a inicialização da máquina.

## Princípio

Os serviços devem ser independentes e possuir apenas as dependências necessárias entre si. A inicialização da VM não deve depender da disponibilidade do armazenamento persistente ou da Internet quando essas dependências não forem necessárias para o funcionamento básico do sistema.

Ideia: em algum lugar citar que Firefox não armazena histórico
Ideia: adicionar serviço de redefinir credenciais armazenadas
