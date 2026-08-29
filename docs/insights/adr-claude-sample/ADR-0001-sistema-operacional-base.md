# ADR-0001: Sistema operacional base da imagem

**Status:** Aceito
**Data:** 2026-08-06

## Contexto

A imagem será construída uma única vez (ou por semestre) como um `.vdi`
imutável, distribuído para todos os desktops dos laboratórios via
VirtualBox. Isso muda o cálculo de risco em relação a um desktop Linux
tradicional: não há necessidade de o usuário final atualizar pacotes
livremente, mas há forte necessidade de que **todo** o software listado no
currículo (ver `inventario-software.md`) consiga ser instalado e builde/rode
sem gambiarra durante a fase de preparação da imagem.

A grade cobre um espectro muito amplo de exigências:
- Toolchains modernas (.NET, Node.js, Kotlin/Android, Python 3.14, PHP 8.3,
  OpenJDK 25) — algumas mais novas que o ciclo de uma distro *stable*.
- Aplicações legadas via Wine (DbDesigner Fork).
- Pacotes proprietários distribuídos como `.deb`/instaladores binários
  (Cisco Packet Tracer, Oracle Data Modeler, Oracle XE).
- Isolamento de rede via `firejail --net 0` (Packet Tracer).
- IDEs pesadas com plugins específicos (Eclipse, IntelliJ, Android Studio).

A equipe técnica sugeriu duas alternativas:
1. **Debian**, pelo ciclo de atualização mais espaçado (maior estabilidade
   para uma imagem "congelada"), com suporte a software ainda "relativamente
   rico".
2. Uma **distro imutável** (ex.: Fedora Silverblue, openSUSE MicroOS,
   VanillaOS), mas sem experiência prévia da equipe quanto a suporte de
   software nesse modelo.

## Decisão

Usar **Debian 12 (Bookworm)**, ramo *stable*, como base, com o repositório
`bookworm-backports` habilitado para os pacotes onde a versão do currículo
exige algo mais novo que o *stable* puro (ex.: Node.js LTS via NodeSource,
`docker-ce` via repositório oficial Docker, .NET SDK via repositório
Microsoft) — e não uma distro imutável no nível do SO.

## Justificativa

1. **A imutabilidade já é resolvida em outra camada.** O requisito de
   "imagem protegida contra alteração pelo aluno" será satisfeito marcando o
   `.vdi` como *immutable* no próprio VirtualBox (disco *immutable*/somente
   leitura reconstruído a cada boot). Não há necessidade de que o sistema de
   arquivos interno também seja *image-based* (OSTree/Btrfs snapshots
   read-only, `rpm-ostree`, etc.) — isso duplicaria a proteção e adicionaria
   complexidade sem benefício real dentro de uma VM já protegida por fora.

2. **Superfície de risco do modelo imutável não compensa.** Distribuições
   imutáveis tratam instalação de software fora do repositório curado (Wine,
   `.deb` avulso do Cisco Packet Tracer, Oracle XE, `firejail`) como caso de
   segunda classe — normalmente exigindo Flatpak/Toolbox/`rpm-ostree
   install` com *layering*, o que é mais uma fonte de atrito durante a
   *criação* da imagem (justamente a única fase em que instalamos software
   nesse projeto). Como a equipe reportou não ter experiência prévia nesse
   modelo, o risco de gastar o tempo de preparação resolvendo
   incompatibilidades de packaging é maior que o benefício.

3. **Debian cobre a maior parte da grade nativamente via APT**, com um
   repositório enorme e estável, e é a base mais testada para os cenários
   "difíceis" da lista: Wine é first-class no Debian, `firejail` está nos
   repositórios oficiais, e a imensa maioria dos instaladores proprietários
   third-party (Cisco, Oracle) publica primariamente para Debian/Ubuntu.

4. **Ciclo de atualização espaçado é uma vantagem real** para uma imagem que
   será congelada e distribuída — menos risco de uma atualização de sistema
   quebrar uma toolchain no meio do semestre, já que a imagem não fica
   recebendo atualizações de pacote em produção.

## Alternativas consideradas e descartadas

- **Fedora Silverblue / openSUSE MicroOS / VanillaOS (imutáveis):**
  descartadas por falta de experiência da equipe e maior atrito esperado
  com Wine, `.deb` avulsos e `firejail`, sem ganho real (ver justificativa
  1).
- **Ubuntu LTS:** candidata viável (mesma base Debian, mesmo suporte a
  software), mas descartada em favor do Debian puro por ter menos software
  pré-instalado por padrão (Snap, telemetria, GNOME "customizado") que
  precisaria ser removido/desabilitado manualmente para não conflitar com a
  decisão de ambiente gráfico (ver ADR-0002).
- **Arch/derivados:** descartada — ciclo rolling é o oposto do que se quer
  para uma imagem congelada e imutável.

## Consequências

- A equipe precisa manter uma lista de repositórios de terceiros
  (`backports`, NodeSource, Docker, Microsoft, etc.) documentada e versionada
  junto ao script/receita de build da imagem, para reprodutibilidade.
- Pacotes muito recentes (ex.: OpenJDK 25, Python 3.14) podem não estar nem
  em *stable* nem em *backports* no momento do build; nesses casos, a
  instalação será via tarball oficial do fornecedor ou repositório
  específico (ex.: `deb.nodesource.com`), documentada individualmente no
  inventário de software.
- Revisão desta decisão deve ocorrer se, no futuro, o ciclo de vida do
  Debian *stable* atrasar demais em relação às versões mínimas exigidas por
  alguma disciplina.
