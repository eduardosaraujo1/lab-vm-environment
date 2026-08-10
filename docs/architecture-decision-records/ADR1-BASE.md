# ADR1 - Escolha de sistema operacional base

**Status**: Pendente

## Contexto

O projeto requer um sistema operacional que se encaixe nos seguintes critérios:

- pouco uso de armazenamento em disco;
- desempenho rasoável em hardware limitado;
- baixa frequência de atualizações;
- compatibilidade para instalação com todas as tecnologias utilizadas durante o curso;
- fácil usabilidade por pessoas acostumadas com o ambiente Windows

## Decisão

Com base nos requisitos, foi escolhido a seguinte _stack_ de sistema operacional:

- Distro: [Debian 13](https://www.debian.org/News/2026/20260711)
- Display Manager: [LightDM](https://wiki.archlinux.org/title/LightDM)
- Display Server: [X11](https://wiki.archlinux.org/title/Xorg)
- Desktop Environment 1: [Cinnamon](https://wiki.archlinux.org/title/Cinnamon)
- Desktop Environment 2:
    - [i3 Tiling Window Manager](https://wiki.archlinux.org/title/I3)
    - [Rofi](https://wiki.archlinux.org/title/Rofi)
    - [Polybar](https://wiki.archlinux.org/title/Polybar)

## Justificativa

### Alternativas consideradas
