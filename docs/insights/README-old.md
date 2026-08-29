CERTIFIQUE-SE que Laravel é instalável
DOCS: melhorar estrutura, deixar mais clean
DOCS: criar uma seção "Casos de uso", que fale quais tecnologias são utilizadas para cada matéria, justificando cada inclusão (tanto para power users quanto users)
Maintainability: evitar updates no disco imutável. Como?:
+ Dotfiles guardados em version control, startup script dá git pull (botar numa branch chamada stable para evitar mudanças que quebram)
+ Docker compose dentro desses dotfiles; fazer compose up e compose stop em startup (se possível uma solução que não cause esse atraso de startup seria melhor; idealmente isso ocorre em um TUI bonito pro usuário interromper se quiser, pois pode requerer o pull de novas imagens)

### REQUISITOS

- Listar matérias e o que elas farão (Sistemas Operacionais tem Packet Tracer com internet bloqurada, banco de dados tem OraclrXE 21g)

## Maquina Geral

- **Base:** Debian
- **Desktop Environment 1:** Cinnamon
- **Desktop Environment 2:** i3 + Rofi + Polybar
- **Display Manager:** LightDM + lightdm-slick-greeter
- **Tema padrão:** Adwaita Dark (GTK), Breeze (Qt)
- **Virtual Disk Image:** Immutable

### Consideração X11

- Base Debian é estável e muda pouco, algo ideal para a VM marcada como imutável
- X11 utiliza menos da GPU, o que resolve um considerável bottle-neck no VirtualBox.

### Aplicações

- ufw
- Git
- Git Credential Manager
- neovim¹, xclip, ripgrep
- lxappearance
- stow (manage configs)
- firejail (previne apps de quebrar o sistema)
- DistroBox
- Firefox
- Chrome
- GIMP
- Inkscape
- clangd
- Openjdk-25-jdk
- Eclipse
- IntelliJ + JUnit
- Android Studio
- Cisco Packet Tracer (`firejail --net=0 --appimage` allows for loginless usage)
- Wireshark
- VsCode
  - Global: Prettier, editorconfig
  - PHP: Intelephense
  - Java: RedHat Java
  - C++: clangd, cmake extensions, makefile
- python3
- php8.3
- composer
- node (24 LTS)
- dotnet
- clangd
- gdb
- Docker⁴
  - postgres:18.3
  - dpage/pgadmin4:9.14.0
  - mysql:8.4
  - webdevops/php-apache
  - phpmyadmin:5.2.3-apache
  - gvenzl/oracle-xe:11-slim
- Simple Container Manager
- DbDesigner Fork (via Wine)
- Oracle Data Modeler (distrobox Fedora)
- React Native & Expo
- Django

### Configurações

- Certificar funcionamento de `openssh-client` para git
- Certificar funcionamento de `curl wget ca-certificates`
- Adicionar usuário 'fatec' ao grupo `docker`

#### Configurações PHP

- phpmyadmin: localhost/phpmyadmin
- PHP: curl, PDO mysql PDO postgres, PDO oracle, ...

#### Configurações MySQL

- Usuário: admin
- Senha: 

- Usuário: root
- Senha: N/A (sudo)

#### Configurações i3

- Executar gnome-polkit para autenticação root de aplicativos GUI
- Instalar pacotes `adwaita-qt qt5-ct qt6-ct` e definir `QT_QPA_PLATFORMTHEME=qt5ct` em bashrc
- Executar `feh --bg-fill <caminho-wallpaper>`
- Executar `dbus-update-activation-environment --systemd DISPLAY`
- Configurar Polybar e Rofi

#### Scripts

  - git-ssh-reset.sh
  - .local/bin/launch-oracle-xe -> docker exec -it ...

### Footnotes

1. Build Neovim from source (as dependências são úteis)
2. Docker deverá ter os containers instanciados mas parados. O projeto `eduardosaraujo1/simple-container-manager` (xampp-like container manager in QT and C++) será utilizado para gerenciar a ativação e desativação desses containers.
