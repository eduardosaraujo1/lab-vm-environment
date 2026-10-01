# Configuração do Sistema Operacional

> **Status da página:** 🚧 Em progresso. Partes marcadas como _stub_ ainda estão em processo de descobrimento (spike) e serão preenchidas conforme as decisões forem tomadas.

## Objetivo

Esta página responde à pergunta: **"Como o ambiente definido cumpre os papéis que um sistema operacional deve cumprir?"**

Os papéis esperados estão definidos em [Requisitos do Ambiente de Desktop](requisitos-sistemas-operacionais.md). O princípio que os orienta é: se uma instalação convencional do Windows fornece uma capacidade básica sem exigir a instalação de um programa adicional, a máquina virtual deve fornecer uma capacidade equivalente, sempre que tecnicamente viável.

Esta página documenta **o que foi decidido**. As alternativas descartadas e seus motivos estão registrados no [ADR 1 - Escolha do Sistema Operacional](ADR1-sistema-operacional.md).

---

## Informações básicas do sistema operacional

A stack definida é:

| Camada                                     | Escolha                                                                                                                                            |
| ------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| Sistema Operacional                        | [Debian 13](https://www.debian.org/News/2026/20260711)                                                                                             |
| Display Manager                            | [LightDM](https://wiki.archlinux.org/title/LightDM)                                                                                                |
| Display Server                             | X11 (nas duas sessões gráficas)                                                                                                                    |
| Ambiente desktop (sessão padrão)           | [Cinnamon](https://wiki.archlinux.org/title/Cinnamon)                                                                                              |
| Tiling Window Manager (sessão alternativa) | [i3](https://wiki.archlinux.org/title/I3), com [Rofi](https://wiki.archlinux.org/title/Rofi) e [Polybar](https://wiki.archlinux.org/title/Polybar) |

O que cada decisão significa na prática:

- **Debian 13** fornece a base estável, com ampla compatibilidade com softwares Linux, baixa frequência de atualizações disruptivas e instalação apenas dos componentes necessários, mantendo o consumo de armazenamento sob controle.
- **Cinnamon** é o ambiente principal por oferecer uma experiência próxima à do Windows, reduzindo a curva de adaptação. Nos testes, consumiu menos armazenamento que o KDE Plasma.
- **LightDM** permite manter o Cinnamon como sessão padrão e oferecer o i3 como alternativa, sem instalações ou configurações separadas para cada usuário.
- **i3 + Rofi + Polybar** formam uma introdução simples a Tiling Window Managers para alunos interessados, sem substituir a experiência tradicional do Cinnamon.
- **X11** é adotado como base das sessões gráficas. Usar o mesmo display server nas duas sessões reduz configurações específicas e problemas na troca de ambiente. O suporte a Wayland poderá ser reavaliado em versões futuras.

---

## Cobertura dos requisitos

A tabela resume como cada grupo de requisitos será atendido. A coluna **Origem** indica de onde vem a capacidade. Os detalhes de pacotes estão nas seções seguintes.

| #     | Requisito                               | Origem prevista                      | Status       |
| ----- | --------------------------------------- | ------------------------------------ | ------------ |
| 1     | Área de trabalho                        | Cinnamon                             | 🔎 A validar |
| 2     | Gerenciamento de arquivos               | Cinnamon                             | 🔎 A validar |
| 3     | Arquivos compactados                    | Pacote suplementar                   | 🚧 Stub      |
| 4     | Imagens (visualização e edição simples) | Pacote suplementar                   | 🚧 Stub      |
| 5     | Capturas de tela                        | Pacote suplementar                   | 🚧 Stub      |
| 6     | Documentos e PDF                        | Pacote suplementar                   | 🚧 Stub      |
| 7     | Editor de texto                         | Pacote suplementar                   | 🚧 Stub      |
| 8     | Calculadora e utilitários               | Pacote suplementar                   | 🚧 Stub      |
| 9, 10 | Áudio e vídeo; áudio e microfone        | Pacote suplementar                   | 🚧 Stub      |
| 11    | Rede                                    | NetworkManager + ferramenta gráfica  | 🚧 Stub      |
| 12    | Dispositivos externos                   | Cinnamon + Guest Additions           | 🚧 Stub      |
| 13    | Monitores e vídeo                       | Cinnamon + Guest Additions           | 🚧 Stub      |
| 14    | Teclado, mouse e entrada                | Cinnamon                             | 🔎 A validar |
| 15    | Área de transferência                   | Guest Additions                      | 🚧 Stub      |
| 16    | Associações de arquivos                 | Cinnamon                             | 🔎 A validar |
| 17    | Gerenciamento de aplicativos            | Cinnamon + APT/Nix                   | 🔎 A validar |
| 18    | Gerenciamento de energia                | Cinnamon                             | 🔎 A validar |
| 19    | Relógio, calendário e notificações      | Cinnamon                             | 🔎 A validar |
| 20    | Pesquisa                                | Cinnamon (menu) / Rofi (i3)          | 🔎 A validar |
| 21    | Configurações do sistema                | Cinnamon                             | 🔎 A validar |
| 22    | Acessibilidade                          | Cinnamon                             | 🔎 A validar |
| 23    | Segurança básica                        | Cinnamon + serviços de inicialização | 🚧 Stub      |
| 24    | Fontes                                  | Pacote suplementar                   | 🚧 Stub      |

**Legenda:** 🔎 _A validar_: espera-se que o Cinnamon atenda, mas isso ainda não foi verificado item a item. 🚧 _Stub_: depende de decisão ainda não tomada.

---

## Configurações suplementares para o ambiente desktop Cinnamon

> 🚧 **Em progresso (spike/discovering).** Esta seção ainda não está concluída.

O pacote [cinnamon-desktop-environment](https://packages.debian.org/sid/cinnamon-desktop-environment) do Debian possui diversas recomendações de pacotes. Quais delas serão mantidas ainda não foi decidido. A tabela abaixo é um _stub_ a ser preenchido no formato `Necessidade | Pacote resolutivo`.

| Necessidade                                                  | Pacote resolutivo |
| ------------------------------------------------------------ | ----------------- |
| Compactação e extração de arquivos (`.zip`, `.tar.*`, `.7z`) | _A definir_       |
| Visualizador de imagens                                      | _A definir_       |
| Edição simples de imagens (equivalente ao Paint)             | _A definir_       |
| Captura de tela                                              | _A definir_       |
| Visualizador de PDF                                          | _A definir_       |
| Editor de texto gráfico                                      | _A definir_       |
| Calculadora                                                  | _A definir_       |
| Reprodutor de áudio e vídeo                                  | _A definir_       |
| Controle de volume e dispositivos de áudio                   | _A definir_       |
| Interface gráfica de rede (integrada ao NetworkManager)      | _A definir_       |
| Impressão de documentos                                      | _A definir_       |
| Fontes Microsoft TrueType                                    | _A definir_       |
| Fontes Noto (emojis e Unicode)                               | _A definir_       |
| Fontes Liberation                                            | _A definir_       |
| Nerd Fonts                                                   | _A definir_       |

### Alterações fora do padrão

Alterações que fogem do padrão do Cinnamon serão registradas aqui (por exemplo, tema diferente ou mudança de atalho de teclado).

| Alteração   | Motivo      | Status          |
| ----------- | ----------- | --------------- |
| _A definir_ | _A definir_ | 🚧 Em progresso |

---

## Configurações suplementares para o ambiente i3

> 🚧 **Em progresso (spike/discovering).** Esta seção ainda não está concluída.

Por ser um Tiling Window Manager, o i3 exige uma quantidade extensa de configurações suplementares para fornecer o que o Cinnamon já oferece. O que já se sabe que será necessário:

| Necessidade                                                                              | Solução     | Status                              |
| ---------------------------------------------------------------------------------------- | ----------- | ----------------------------------- |
| Agente de autenticação (polkit)                                                          | _A definir_ | 🚧 Stub                             |
| Variável `DISPLAY` disponível no `systemd --user`                                        | _A definir_ | 🚧 Stub                             |
| Variável `DISPLAY` disponível no `dbus`                                                  | _A definir_ | 🚧 Stub                             |
| Lançador de aplicativos                                                                  | Rofi        | ✅ Decidido (configuração pendente) |
| Barra de status                                                                          | Polybar     | ✅ Decidido (configuração pendente) |
| Capacidades do desktop ausentes no i3 (rede, áudio, notificações, bloqueio de tela etc.) | _A definir_ | 🚧 Stub                             |

---

## Integração com ambiente virtualizado

Os componentes **Guest Additions** do VirtualBox são instalados pelo gerenciador de pacotes, e não manualmente a partir da imagem fornecida pelo VirtualBox. Isso mantém a instalação integrada ao sistema operacional convidado e facilita sua manutenção.

O sistema **não depende** dos recursos exclusivos do Guest Additions para sua execução básica. Em outro hipervisor (VMware, QEMU/KVM), os componentes do VirtualBox permanecem instalados sem necessariamente interferir, mas os recursos de integração que eles fornecem não estarão disponíveis.

| Recurso de integração                                        | Status               |
| ------------------------------------------------------------ | -------------------- |
| Pasta compartilhada                                          | ✅ Definido (abaixo) |
| Integração da área de transferência (requisito 15)           | 🚧 Stub              |
| Resolução inicial adequada a uma janela de VM (requisito 13) | 🚧 Stub              |
| Redimensionamento dinâmico da tela                           | 🚧 Stub              |

### Pasta compartilhada

A VM usa uma pasta compartilhada para transferir arquivos entre o sistema convidado e o computador hospedeiro.

- Uma pasta chamada **`Compartilhado`** é disponibilizada na área de trabalho. Ela corresponde a uma pasta do hospedeiro, montada no convidado pelo mecanismo de **Shared Folders** do VirtualBox.
- O usuário da VM tem permissão de leitura e escrita. Para isso, ele pertence ao grupo `vboxsf`, que o VirtualBox usa para controlar o acesso.
- O caminho no hospedeiro **não é um requisito fixo** e pode seguir a organização de cada computador. Nos testes, foi usado `%LOCALAPPDATA%\LabVM\Compartilhado`.
- Use esta pasta para arquivos que precisem passar entre hospedeiro e VM, especialmente porque o disco principal da VM é imutável.
- Quando conveniente, atalhos para a pasta podem ser colocados na **Área de Trabalho** e em **Documentos**.

---

## Disco imutável e disco persistente

A VM usa **dois discos virtuais**:

| Disco            | Tipo           | Função                                                                           |
| ---------------- | -------------- | -------------------------------------------------------------------------------- |
| Disco do sistema | Imutável (VDI) | Sistema operacional e configurações. Volta ao estado original ao ser restaurado. |
| Disco de dados   | Mutável        | Dados que devem sobreviver à restauração.                                        |

O objetivo é tornar o ambiente **descartável**: alterações acidentais ou indesejadas no sistema, nas configurações e nos aplicativos não permanecem entre ciclos de uso.

### Persistência seletiva

Apenas pastas específicas são montadas no disco de dados, por meio do `/etc/fstab`:

- `Downloads`
- `Desktop`
- `Documents`
- `/var/cache/apt/archives`

O diretório pessoal **não** é persistente por completo. Configurações de shell, de editores e de aplicativos, além de caches não listados acima, ficam no disco imutável e são descartados na restauração.

> 🚧 A lista acima reflete o que está definido até agora e pode ser ajustada.

### Ausência do disco persistente

O disco de dados **não é necessário** para a inicialização. Se ele estiver ausente, os pontos de montagem não são montados e os diretórios continuam existindo no disco imutável. Eles podem ser usados normalmente na sessão, mas o que for gravado ali será perdido na restauração. Se o disco voltar a estar disponível, será montado na inicialização seguinte e os dados persistentes voltam a aparecer.

Essa degradação é intencional. Nenhum mecanismo adicional é necessário para bloquear o uso desses diretórios quando o disco está ausente.

### Cache de pacotes

O cache do APT em `/var/cache/apt/archives` fica no disco persistente para reaproveitar arquivos `.deb` já baixados e reduzir downloads. Isso **não** persiste um `apt update` nem atualizações do sistema: metadados e estado dos pacotes ficam no disco imutável. Atualizações e mudanças no conjunto de pacotes continuam sendo alterações do disco imutável, e novas versões do ambiente são distribuídas gerando uma nova imagem.

Caches persistentes devem se limitar a dados cuja persistência traga benefício claro.

> 🚧 **A confirmar:** registrar aqui que o Firefox não armazena histórico entre sessões, e como isso é garantido.

---

## Serviços de inicialização automática

> 🚧 **Em progresso.** Texto gerado com auxílio de IA e sujeito a muitas alterações.

As rotinas executadas na inicialização são divididas em **serviços `systemd` independentes**. Dependências e ordem de execução são declaradas nas próprias unidades, sem um script de inicialização monolítico.

**Princípio:** cada serviço possui apenas as dependências necessárias. A inicialização não deve depender do armazenamento persistente nem da Internet quando isso não for necessário ao funcionamento básico.

### Sincronização Remota

1. Aguarda o NetworkManager inicializar a conectividade.
2. Verifica se há acesso efetivo à Internet. Se não houver, encerra sem falhar o sistema.
3. Sincroniza o repositório de configuração com a branch configurada (`git pull --rebase` ou equivalente).

A VM deve continuar funcional sem o segundo `.vdi` ou mesmo se o disco do sistema não estiver em estado imutável.

### Verificação de Integridade do Nix

Serviço independente que verifica a integridade do `/nix/store` persistente, para que corrupção ou alteração não autorizada seja detectada antes do uso do conteúdo.

- **Não roda a cada inicialização.** Um arquivo no Nix Store (ou mecanismo do próprio Nix, se existir) registra quando foi feita a última verificação.
- Uma nova verificação só ocorre após um período arbitrário, de forma **não disruptiva**: o sistema segue utilizável, apesar do maior uso de CPU para o cálculo de checksums.
- 🚧 A estratégia de reparo de um store corrompido será definida posteriormente.
- 🚧 A lista de pastas persistentes acima não inclui `/nix/store`. É preciso definir onde ele reside.

### Aplicação de Patches

Executa `patches.sh`. Depende da conclusão bem-sucedida da **Sincronização Remota**, garantindo que os patches rodem sobre a versão mais recente da configuração.

### Redefinição de Credenciais

Remove, durante a inicialização e antes de o ambiente do usuário ser disponibilizado, credenciais e identificadores pessoais deixados pelo usuário anterior. No mínimo:

- Credenciais do Git Credential Manager ou de outros mecanismos de credenciais do Git.
- Identidade global do Git (`user.name`, `user.email` e equivalentes).
- Chaves privadas e demais credenciais SSH do usuário.
- Chaves e credenciais GPG do usuário.
- Configurações de autenticação relacionadas que permitam reaproveitar uma sessão anterior.

Credenciais e configurações da infraestrutura da própria VM não fazem parte da limpeza. O serviço é **idempotente**: executá-lo sem credenciais armazenadas é normal e não impede a inicialização.
