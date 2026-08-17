# ADR1 - Escolha de sistema operacional base

**Status**: Pendente

## Contexto

A escolha do sistema operacional base é relevante para o projeto porque influencia diretamente o consumo de recursos, a compatibilidade com as ferramentas utilizadas durante o curso, a facilidade de manutenção e a experiência dos usuários finais. Como o sistema será executado em hardware potencialmente limitado e deverá permanecer utilizável por diferentes alunos, a escolha da base deve equilibrar estabilidade, desempenho, compatibilidade e facilidade de uso.

O projeto requer um sistema operacional que atenda aos seguintes critérios:

- baixo uso de armazenamento em disco;
- desempenho razoável em hardware limitado;
- baixa frequência de atualizações disruptivas;
- compatibilidade com as tecnologias utilizadas durante o curso;
- fácil utilização por pessoas acostumadas com o ambiente Windows;
- suporte à introdução de Tiling Window Managers para alunos interessados;
- flexibilidade para execução de scripts definidos e distribuídos remotamente via GitHub.

## Decisão

Com base nos requisitos, foi escolhida a seguinte stack de sistema operacional:

- Distribuição: [Debian 13](https://www.debian.org/News/2026/20260711)
- Display Manager: [LightDM](https://wiki.archlinux.org/title/LightDM)
- Desktop Environment: [Cinnamon](https://wiki.archlinux.org/title/Cinnamon)
- Ambiente alternativo:
  - [i3 Tiling Window Manager](https://wiki.archlinux.org/title/I3)
  - [Rofi](https://wiki.archlinux.org/title/Rofi)
  - [Polybar](https://wiki.archlinux.org/title/Polybar)

A escolha prioriza uma base estável e de manutenção previsível, mantendo uma interface gráfica familiar para usuários provenientes do Windows e permitindo que usuários interessados utilizem um ambiente baseado em Tiling Window Manager sem substituir a instalação principal.

## Justificativa

O Debian foi escolhido por oferecer uma base estável, ampla compatibilidade com softwares disponíveis para Linux e um ciclo de manutenção adequado ao objetivo do projeto. A distribuição também permite instalar e configurar apenas os componentes necessários, contribuindo para manter o consumo de armazenamento sob controle.

O Cinnamon foi escolhido como ambiente principal por oferecer uma experiência de uso semelhante à de sistemas Windows, reduzindo a curva de adaptação para os usuários. Durante os testes, também apresentou menor consumo de armazenamento que o KDE Plasma mantendo os recursos necessários para o ambiente principal.

O LightDM foi escolhido como Display Manager por ser compatível com os ambientes selecionados e permitir a seleção do ambiente gráfico durante o login. Isso permite manter o Cinnamon como ambiente padrão e disponibilizar o i3 como alternativa sem exigir instalações ou configurações separadas para cada usuário.

O i3, acompanhado de Rofi e Polybar, foi escolhido como ambiente alternativo por oferecer uma introdução simples ao conceito de Tiling Window Manager, sem substituir a experiência tradicional fornecida pelo Cinnamon. Dessa forma, o mesmo sistema pode atender tanto usuários que preferem uma interface gráfica convencional quanto alunos interessados em experimentar um ambiente orientado a atalhos e gerenciamento automático de janelas.

## Alternativas consideradas

As alternativas foram avaliadas principalmente de acordo com os requisitos de compatibilidade, desempenho, estabilidade, facilidade de uso, consumo de armazenamento e maleabilidade do sistema.

### Sistemas operacionais não baseados em Linux

- [Windows](https://en.wikipedia.org/wiki/Microsoft_Windows) — Foi descartado devido ao maior consumo de recursos e armazenamento em comparação com as alternativas Linux consideradas, tornando-o menos adequado para o hardware limitado utilizado pelo projeto.

- [FreeBSD](https://www.freebsd.org/) — Foi descartado principalmente pela menor compatibilidade com as tecnologias e ferramentas utilizadas durante o curso. Embora seja adequado para diversos cenários de uso, a necessidade de compatibilidade ampla com o ecossistema Linux utilizado no projeto torna o custo de adaptação desnecessário.

### Distribuições Linux

- [NixOS](https://nixos.org/) — Foi descartado apesar de oferecer vantagens relevantes em reprodutibilidade e gerenciamento declarativo do sistema. A complexidade adicional e a curva de aprendizado do NixOS aumentariam o tempo necessário para desenvolver e manter o sistema, contrariando o objetivo de manter a solução simples de configurar e utilizar.

- [Ubuntu 24.04 LTS](https://releases.ubuntu.com/noble/) — Foi descartado porque, apesar da estabilidade e ampla compatibilidade, sua configuração padrão não corresponde à stack de ambiente gráfico definida para o projeto. A utilização de uma base diferente da escolhida também não apresentou benefícios suficientes para justificar a mudança.

- [Fedora Workstation](https://fedoraproject.org/workstation/) — Foi descartado pelos mesmos motivos gerais do Ubuntu: embora seja uma distribuição moderna e bem suportada, sua configuração padrão e ciclo de atualizações não se alinham tão bem aos requisitos de estabilidade e à stack definida para o projeto.

- [Linux Mint: Cinnamon](https://www.linuxmint.com/) — Foi utilizado em um protótipo do projeto e serviu como proof of concept para validar a abordagem adotada. Entretanto, sua base Ubuntu não atende aos requisitos definidos para este projeto. Além disso, a instalação padrão inclui pacotes que não são utilizados no ambiente imutável proposto, resultando em consumo adicional de armazenamento e componentes desnecessários.

- [Fedora Kinoite](https://fedoraproject.org/pt-br/atomic-desktops/kinoite/) — Foi descartado por utilizar uma abordagem atômica/imutável. Embora esse modelo ofereça vantagens de confiabilidade e recuperação, ele reduz a maleabilidade necessária para modificar diretamente o sistema base e aplicar patches ou ajustes durante o processo de implantação.

- [Vanilla OS](https://vanillaos.org/) — Foi descartado pelo mesmo motivo: seu modelo de sistema imutável introduz restrições e complexidade adicional para modificações diretas no sistema base, enquanto o projeto exige flexibilidade para scripts e ajustes realizados durante a implantação.

- [Arch Linux](https://archlinux.org/) — Foi descartado por priorizar um modelo de distribuição rolling release, que exige atualizações mais frequentes e maior acompanhamento de possíveis mudanças no sistema. Embora ofereça grande flexibilidade e acesso a versões recentes dos pacotes, essas características não são prioritárias para um sistema que deve permanecer estável e exigir pouca manutenção.

### Desktop Environments e Window Managers

- [Hyprland](https://hypr.land/) — Foi descartado como ambiente principal porque sua principal vantagem para este projeto seria a possibilidade de realizar uma customização extensa da experiência gráfica. Essa customização não é necessária para o objetivo do ambiente principal e adicionaria complexidade à configuração e manutenção.

- [GNOME](https://www.gnome.org/) — Foi descartado devido a problemas observados durante os testes, incluindo dificuldades relacionadas a screen tearing, além de uma experiência de uso menos próxima do modelo de interface ao qual os usuários-alvo estão acostumados.

- [KDE Plasma](https://kde.org/plasma-desktop/) — Foi considerado uma das alternativas mais próximas do perfil desejado, principalmente por oferecer uma experiência familiar aos usuários de Windows e grande capacidade de configuração. Entretanto, os testes realizados apresentaram consumo de armazenamento superior ao Cinnamon, fazendo com que este último fosse considerado mais adequado para o hardware e as restrições do projeto.

- [XFCE](https://xfce.org/) — Foi descartado devido a resultados insatisfatórios nos testes anteriores de experiência de uso. Embora seja leve e adequado para hardware limitado, a economia de recursos não compensou a experiência de usuário considerada inferior para os objetivos do projeto.

- [LXQt](https://lxqt-project.org/) — Foi descartado por razões semelhantes às do XFCE. Apesar do baixo consumo de recursos, os testes anteriores apresentaram uma experiência de uso menos adequada ao público-alvo.

### Display Server

Também foi considerada a utilização de ambientes baseados em [Wayland](https://wiki.archlinux.org/title/Wayland). Wayland é o protocolo de display utilizado por diversos ambientes gráficos modernos e possui suporte consolidado para uma grande parte das aplicações atuais, além de oferecer uma arquitetura diferente da tradicional baseada em X11.

Entretanto, os testes realizados com Cinnamon e KDE Plasma indicaram que a combinação Cinnamon + X11 apresentou o melhor equilíbrio entre consumo de recursos, compatibilidade e previsibilidade para este projeto. Como o Cinnamon ainda possui suporte a X11, essa combinação permite utilizar o ambiente escolhido sem introduzir uma camada adicional de compatibilidade.

Manter o mesmo display server nos ambientes principal e alternativo também reduz a quantidade de configurações específicas necessárias para cada sessão e, consequentemente, as possibilidades de problemas durante a troca de ambiente pelo usuário. Por esse motivo, o projeto utiliza X11 como base para as sessões gráficas, enquanto o suporte a Wayland poderá ser reavaliado em uma versão futura caso os requisitos ou o suporte dos ambientes utilizados mudem.
