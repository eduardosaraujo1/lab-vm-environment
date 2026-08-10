# ADR1 - Escolha de sistema operacional base

**Status**: Pendente

## Contexto

O projeto requer um sistema operacional que se encaixe nos seguintes critérios:

- pouco uso de armazenamento em disco;
- desempenho rasoável em hardware limitado;
- baixa frequência de atualizações;
- compatibilidade para instalação com todas as tecnologias utilizadas durante o curso;
- fácil usabilidade por pessoas acostumadas com o ambiente Windows
- confortável para introdução de Tiling Window Managers para alunos interessados
- maleável para execução de scripts definidos remotamente via GitHub

## Decisão

Com base nos requisitos, foi escolhido a seguinte _stack_ de sistema operacional:

- Distro: [Debian 13](https://www.debian.org/News/2026/20260711)
- Display Server: [X11](https://wiki.archlinux.org/title/Xorg)
- Display Manager: [LightDM](https://wiki.archlinux.org/title/LightDM)
- Desktop Environment 1: [Cinnamon](https://wiki.archlinux.org/title/Cinnamon)
- Desktop Environment 2:
    - [i3 Tiling Window Manager](https://wiki.archlinux.org/title/I3)
    - [Rofi](https://wiki.archlinux.org/title/Rofi)
    - [Polybar](https://wiki.archlinux.org/title/Polybar)

## Justificativa

## Alternativas consideradas

Como distribuição Linux, foram considerados e descartados:

- [Ubuntu 24.04 LTS](https://releases.ubuntu.com/noble/), [Fedora Workstation](): Embora boas escolhas, essas distribuições vêm com _Desktop Environemnts_ diferentes dos especificados na documentação, além de dificultar a customizabilidade
- [Fedora Kionite](https://fedoraproject.org/pt-br/atomic-desktops/kinoite/): Distribuições atômicas ou imutáveis geram fricção com o requisito de maleabilidade do sistema base para criação de patches em deploys existentes.
- [Vanilla OS](https://vanillaos.org/): Distribuições atômicas ou imutáveis geram fricção com o requisito de maleabilidade do sistema base para criação de patches em deploys existentes.
- [Arch Linux](https://archlinux.org/): ESCREVER JUSTIFICATIVA

Para display server, foi considerado:

- [Wayland](https://wiki.archlinux.org/title/Wayland): Experiências com tecnologias baseadas em Wayland (distro Ubuntu, DE Gnome, e TWM Sway) revelaram _screen tearing_, congelamentos e dificuldades para sua utilização.

Para Desktop Environment, foram considerados:

- [Hyprland](): ESCREVER JUSTIFICATIVA
- [GNOME](): ESCREVER JUSTIFICATIVA
- [KDE Plasma](): ESCREVER JUSTIFICATIVA
- [XFCE](): ESCREVER JUSTIFICATIVA (testes anteriores revelaram UX ruim)
- [LXQt](): ESCREVER JUSTIFICATIVA (testes anteriores revelaram UX ruim)
