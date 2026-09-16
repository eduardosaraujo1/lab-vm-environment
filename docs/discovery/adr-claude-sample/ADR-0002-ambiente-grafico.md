# ADR-0002: Servidor gráfico e ambiente de desktop

**Status:** Aceito
**Data:** 2026-08-06

## Contexto

A imagem roda dentro de uma VM VirtualBox em desktops de laboratório, não em
hardware bare-metal. A aceleração gráfica oferecida pelo Guest Additions do
VirtualBox (`vboxvideo`/3D via VMSVGA) é limitada frente a um driver GPU
nativo, e não implementa corretamente primitivas exigidas pelos
compositores Wayland modernos (ex.: *explicit sync*, certas extensões de
`wl_drm`). A equipe técnica já observou, em testes, tearing perceptível em
sessões Wayland dentro do VirtualBox, e recomendou usar Xorg.

Além do protocolo gráfico, é preciso escolher um ambiente de desktop (DE)
completo, considerando que a máquina será usada por alunos em disciplinas
que vão de IDEs pesadas (Android Studio, IntelliJ) a ferramentas gráficas
(GIMP, Inkscape) e terminal.

## Decisão

- Usar **Xorg (X11)** como servidor gráfico, não Wayland.
- Usar **XFCE** como ambiente de desktop padrão.

## Justificativa

**Xorg vs. Wayland:**
- Suporte maduro e estável de aceleração 2D/3D dentro do VirtualBox
  (VMSVGA 3D é desenhado pensando em X11/GLX; o caminho Wayland depende de
  DRM/KMS mais completo do que o dispositivo virtual oferece).
- Compatibilidade universal com ferramentas antigas/proprietárias da grade:
  Cisco Packet Tracer, Oracle Data Modeler e aplicações rodando sob Wine
  historicamente têm problemas ou exigem camadas extras (XWayland) em
  sessões Wayland — sob X11 nativo, funcionam sem camada de compatibilidade.
- Ferramentas de captura de tela/gravação usadas em disciplinas de
  documentação (ex.: Fundamentos de Redação Técnica) são mais previsíveis
  sob X11 dentro de uma VM.

**Escolha do DE (XFCE):**
- É um ambiente **X11 por padrão** (evita a pegadinha do GNOME moderno, que
  no Debian assume sessão Wayland por padrão em `gdm3`, exigindo forçar
  Xorg manualmente e revalidar isso a cada atualização de `gdm`/GNOME).
- Baixo consumo de RAM/CPU — relevante porque a VM concorre por recursos
  com o host físico do laboratório e com IDEs pesadas (Android Studio,
  IntelliJ) e emuladores rodando dentro do convidado.
- Integração estável e bem testada com `VBoxClient` (redimensionamento de
  tela, clipboard compartilhado, drag-and-drop) — recurso crítico para aulas
  que dependem de compartilhar arquivos entre host e convidado.
- Interface simples reduz a curva de adaptação de alunos que não têm
  familiaridade prévia com Linux (público de um curso de graduação em geral,
  não só de alunos avançados em SO).

## Alternativas consideradas e descartadas

- **GNOME:** descartado — sessão Wayland por padrão no Debian, exigindo
  contorno manual recorrente; maior consumo de recursos.
- **KDE Plasma (sessão X11):** viável tecnicamente, mas descartado por
  consumo de recursos maior que XFCE sem ganho funcional relevante para o
  caso de uso (laboratório, não estação de produtividade pessoal).
- **MATE / Cinnamon:** candidatos razoáveis (também X11-first), mas XFCE
  tem o menor *footprint* de recursos entre os três, o que pesa mais no
  cenário de VM compartilhando recursos com host.
- **Ambiente "headless" (sem DE, apenas WM leve tipo i3):** descartado — a
  grade inclui disciplinas de Design Digital (GIMP/Inkscape) e UX que se
  beneficiam de um DE completo com gerenciador de arquivos gráfico,
  não apenas um gerenciador de janelas minimalista.

## Consequências

- Ao instalar pacotes de outras DEs (ex.: dependências trazidas por
  Android Studio ou GIMP), a equipe deve garantir que nenhum instalador
  force `gdm3`/GNOME como *display manager* padrão, sobrescrevendo o XFCE.
  Recomenda-se `lightdm` como *display manager*.
- Caso alguma ferramenta específica exija Wayland no futuro (hoje não é o
  caso na grade), será necessário reabrir esta decisão com testes de
  desempenho dedicados dentro do VirtualBox.
