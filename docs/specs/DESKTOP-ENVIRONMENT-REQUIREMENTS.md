# Requisitos do Ambiente de Desktop

## Objetivo

O ambiente de desktop da máquina virtual deve proporcionar uma experiência de uso geral comparável à de um computador pessoal convencional, especialmente à experiência que um usuário acostumado ao Windows espera encontrar.

A máquina virtual não deve ser limitada às necessidades específicas das disciplinas ou das ferramentas de desenvolvimento. Ela deve também fornecer as funcionalidades básicas que normalmente seriam esperadas de um computador de uso geral, evitando que o usuário precise descobrir posteriormente que uma função cotidiana não está disponível.

Como princípio geral:

> **Se uma instalação convencional do Windows fornece uma capacidade básica ao usuário sem exigir que ele procure e instale um programa adicional, a máquina virtual deve, sempre que tecnicamente viável, fornecer uma capacidade equivalente.**

Isso não significa reproduzir o conjunto exato de aplicativos do Windows, mas garantir as mesmas capacidades de uso.

A referência utilizada para definir essas capacidades é a experiência de uso geral do Windows 10/11, considerando principalmente as funcionalidades disponíveis ao usuário final no Explorador de Arquivos, Configurações, área de trabalho e aplicativos utilitários integrados.

---

# 1. Área de trabalho

O ambiente deve fornecer uma área de trabalho gráfica completa, incluindo:

- Área de trabalho (desktop).
- Menu principal de aplicativos.
- Barra de tarefas ou mecanismo equivalente.
- Área de notificação.
- Relógio e calendário.
- Indicadores de rede, áudio e energia quando aplicáveis.
- Lançamento de aplicativos.
- Pesquisa de aplicativos e arquivos, quando disponível.
- Menus de contexto.
- Atalhos na área de trabalho.
- Fixação de aplicativos no menu/barra de tarefas.
- Gerenciamento de múltiplas janelas.
- Minimização, maximização, restauração e fechamento de janelas.
- Redimensionamento e movimentação de janelas.
- Alternância entre aplicativos.
- Múltiplas áreas de trabalho virtuais.
- Bloqueio de tela.
- Logout.
- Reinicialização e desligamento.

O usuário deve conseguir utilizar o sistema exclusivamente pela interface gráfica para tarefas comuns, sem que o uso do terminal seja obrigatório.

---

# 2. Gerenciamento de arquivos

O sistema deve fornecer um gerenciador de arquivos completo, equivalente em função ao Explorador de Arquivos do Windows.

Deve ser possível:

- Navegar pela estrutura de diretórios.
- Criar, excluir e renomear arquivos e diretórios.
- Copiar e mover arquivos.
- Recortar e colar.
- Selecionar múltiplos arquivos.
- Arrastar e soltar.
- Abrir arquivos com o aplicativo associado.
- Alterar associações de arquivos.
- Exibir propriedades de arquivos e diretórios.
- Exibir tamanho, tipo e datas dos arquivos.
- Pesquisar arquivos.
- Exibir arquivos ocultos.
- Exibir extensões de arquivos.
- Acessar dispositivos e volumes montados.
- Acessar mídias removíveis.
- Utilizar a lixeira.
- Restaurar arquivos da lixeira.
- Esvaziar a lixeira.
- Criar atalhos ou equivalentes.
- Fixar locais frequentemente utilizados.
- Trabalhar com arquivos compactados.

O Windows considera o gerenciamento, organização e localização de arquivos e pastas uma função central do Explorador de Arquivos.

---

# 3. Arquivos compactados

O usuário deve conseguir trabalhar com os formatos de compactação mais comuns sem precisar utilizar o terminal.

No mínimo:

- `.zip`

Preferencialmente também:

- `.tar`
- `.tar.gz`
- `.tar.bz2`
- `.tar.xz`
- `.7z`
- `.rar`, quando tecnicamente e legalmente apropriado.

Deve ser possível:

- Criar arquivos ZIP.
- Extrair arquivos ZIP.
- Abrir arquivos compactados.
- Extrair arquivos para um diretório escolhido.
- Compactar arquivos através do menu de contexto do gerenciador de arquivos.

---

# 4. Visualização e manipulação de imagens

O sistema deve permitir o uso cotidiano de imagens.

Deve incluir:

- Visualizador de imagens.
- Visualização de miniaturas no gerenciador de arquivos.
- Abertura de formatos comuns de imagem.
- Rotação de imagens.
- Redimensionamento ou alguma ferramenta equivalente para manipulação básica.
- Recorte de imagens.
- Exportação para formatos comuns.

Também deve existir uma ferramenta simples de edição de imagens equivalente ao conceito do Paint.

Não é necessário fornecer um editor profissional como GIMP por padrão.

O objetivo é permitir operações ocasionais como:

- Cortar uma imagem.
- Redimensionar.
- Adicionar texto.
- Fazer desenhos/anotações simples.
- Salvar em outro formato.
- Fazer pequenas correções.

---

# 5. Capturas de tela

O sistema deve possuir uma ferramenta gráfica para captura de tela.

Deve ser possível capturar:

- Tela inteira.
- Uma janela.
- Uma região selecionada.

Preferencialmente também:

- Copiar a captura diretamente para a área de transferência.
- Salvar a captura em arquivo.
- Fazer anotações simples.
- Definir um atraso antes da captura.

A existência dessa funcionalidade é considerada parte da experiência básica de desktop. O Windows, por exemplo, fornece a Ferramenta de Captura para capturas de tela inteira, janelas e regiões selecionadas, além de edição, salvamento e compartilhamento.

---

# 6. Documentos e PDF

O sistema deve fornecer suporte básico para documentos comuns.

Deve incluir:

- Visualizador de PDF.
- Associação automática de arquivos PDF ao visualizador.
- Impressão de documentos.
- Visualização e manipulação básica de documentos de texto.

Um usuário deve conseguir receber um PDF, clicar duas vezes sobre ele e visualizá-lo sem precisar descobrir qual aplicativo instalar.

Ferramentas de edição avançada de documentos, como suítes de escritório completas, são tratadas separadamente e não constituem requisito do ambiente desktop básico.

---

# 7. Editor de texto

Deve existir um editor de texto gráfico simples para:

- Criar arquivos de texto.
- Editar arquivos de texto.
- Salvar e abrir arquivos.
- Trabalhar com texto simples.

O editor não precisa substituir uma IDE ou editor de código.

Editores destinados ao desenvolvimento, como VS Code, pertencem à camada de desenvolvimento.

---

# 8. Calculadora e utilitários simples

O ambiente deve fornecer uma calculadora gráfica.

Idealmente deve permitir:

- Operações aritméticas básicas.
- Operações científicas.
- Histórico de cálculos.
- Conversões de unidades comuns.

O Windows atualmente oferece, além da aritmética básica, modos científico, gráfico e programador, cálculo de datas e diversos conversores.

Não é necessário reproduzir todas essas funcionalidades, mas uma calculadora simples deve estar disponível por padrão.

---

# 9. Áudio e vídeo

O sistema deve permitir o consumo de conteúdo multimídia sem configuração adicional significativa.

Deve ser possível:

- Reproduzir arquivos de áudio comuns.
- Reproduzir arquivos de vídeo comuns.
- Controlar volume.
- Selecionar dispositivo de saída.
- Selecionar dispositivo de entrada.
- Silenciar o sistema.
- Controlar volume individualmente por aplicativo, quando suportado.
- Reproduzir mídia através do navegador.

Formatos adicionais podem ser fornecidos conforme as necessidades de compatibilidade e licenciamento.

---

# 10. Áudio, microfone e dispositivos de entrada

O usuário deve conseguir configurar graficamente:

- Volume principal.
- Dispositivo de saída.
- Dispositivo de entrada.
- Microfone.
- Volume do microfone.
- Dispositivos de áudio conectados.
- Fones de ouvido.
- Alto-falantes.

Quando houver múltiplos dispositivos, deve ser possível escolher qual utilizar.

---

# 11. Rede

O ambiente deve fornecer uma interface gráfica para gerenciamento da conexão de rede.

Deve ser possível:

- Visualizar o estado da conexão.
- Conectar e desconectar redes.
- Configurar redes disponíveis.
- Configurar DNS quando necessário.
- Configurar conexões com e sem fio quando suportadas pelo hardware virtual.
- Configurar VPNs quando necessário.
- Visualizar informações básicas da conexão.

A infraestrutura de rede atualmente funcional na instalação não deve ser substituída apenas para adicionar uma interface gráfica. A ferramenta gráfica deve integrar-se à infraestrutura existente.

---

# 12. Dispositivos externos

O ambiente deve fornecer suporte gráfico para dispositivos externos normalmente utilizados por um computador pessoal.

Incluindo, quando aplicável:

- Pendrives.
- Discos externos.
- Dispositivos USB.
- Teclados.
- Mouses.
- Microfones.
- ~~Fones de ouvido~~ (gerenciado pelo host).
- ~~Webcams~~.
- ~~Impressoras~~.
- ~~Dispositivos Bluetooth~~.

O Windows disponibiliza uma área própria para gerenciamento de dispositivos conectados, incluindo periféricos Bluetooth, mouse, teclado, áudio e outros dispositivos.

---

# 13. Monitores e vídeo

O ambiente deve fornecer configuração gráfica de vídeo.

Deve ser possível:

- Alterar resolução.
- Configurar orientação.
- Configurar múltiplos monitores.
- Escolher monitor principal.
- Ajustar escala quando suportado.
- Configurar taxa de atualização quando suportada.
- Espelhar ou estender a área de trabalho.

Para a máquina virtual, a resolução inicial deve ser escolhida de maneira razoável para a utilização em uma janela de VM.

---

# 14. Teclado, mouse e entrada

Deve ser possível configurar:

- Layout do teclado.
- Idioma de entrada.
- Teclas de atalho.
- Velocidade do mouse.
- Sensibilidade do touchpad, quando aplicável.
- Ações de botões.
- Velocidade de repetição do teclado.
- Atraso de repetição.

O ambiente deve fornecer suporte adequado tanto à interação por mouse quanto por teclado.

---

# 15. Área de transferência

O sistema deve possuir uma área de transferência funcional para:

- Texto.
- Imagens.
- Arquivos.

Deve ser possível utilizar copiar/colar entre aplicativos.

Quando suportado pela virtualização, deve existir integração entre a área de transferência do sistema convidado e a máquina hospedeira.

A área de transferência é explicitamente tratada como uma funcionalidade configurável do Windows.

---

# 16. Associações de arquivos

O ambiente deve possuir um mecanismo para definir o aplicativo padrão para tipos de arquivo.

Exemplos:

- `.pdf` → visualizador de PDF.
- `.png` → visualizador de imagens.
- `.txt` → editor de texto.
- `.html` → navegador.
- `.zip` → gerenciador de arquivos compactados.

O usuário deve conseguir alterar essas associações através da interface gráfica.

---

# 17. Gerenciamento de aplicativos

O usuário deve conseguir:

- Localizar aplicativos instalados.
- Iniciar aplicativos.
- Desinstalar aplicativos quando apropriado.
- Definir aplicativos padrão.
- Visualizar informações básicas sobre aplicativos.

A instalação de software pode ocorrer através de APT, Nix ou outros mecanismos definidos pela especificação da máquina virtual; isso não constitui uma exigência do ambiente gráfico em si.:w

---

# 18. Gerenciamento de energia

O ambiente deve possuir configurações básicas de energia, incluindo quando aplicável:

- Suspensão.
- Bloqueio automático.
- Tempo para desligamento da tela.
- Comportamento ao fechar a tampa, quando aplicável.
- Estado de bateria, quando aplicável.

Recursos específicos de notebooks físicos não são necessários quando não existem no hardware virtualizado.

---

# 19. Relógio, calendário e notificações

O ambiente deve fornecer:

- Relógio.
- Data.
- Calendário.
- Notificações de aplicativos.
- Indicadores de notificações.
- Controle básico de notificações.

Também deve ser possível configurar:

- Fuso horário.
- Formato de data/hora.
- Idioma/região.

---

# 20. Pesquisa

Deve existir algum mecanismo razoavelmente acessível para encontrar:

- Aplicativos.
- Arquivos.
- Configurações.

A pesquisa não precisa reproduzir o Windows Search, mas o usuário não deve depender exclusivamente da navegação manual pelos menus para localizar um aplicativo instalado.

---

# 21. Configurações do sistema

O ambiente deve disponibilizar uma interface gráfica centralizada para configurações comuns.

No mínimo:

- Aparência.
- Tela.
- Teclado.
- Mouse.
- Áudio.
- Rede.
- Bluetooth.
- Data e hora.
- Idioma.
- Usuários.
- Aplicativos padrão.
- Energia.
- Notificações.
- Acessibilidade.

---

# 22. Acessibilidade

O ambiente deve fornecer os recursos básicos de acessibilidade disponíveis no desktop, incluindo, quando suportados:

- Aumento de tamanho de texto.
- Escala da interface.
- Ajuste do cursor.
- Alto contraste.
- Temas de contraste.
- Leitor de tela.
- Lupa.
- Teclado virtual.
- Recursos de acessibilidade do teclado.
- Recursos de acessibilidade do mouse.

O Windows organiza seus recursos de acessibilidade em categorias relacionadas à visão, audição, mobilidade/destreza e foco, incluindo lupa, contraste, leitor de tela, teclado virtual e recursos para entrada alternativa.

Não é necessário instalar ferramentas de acessibilidade especializadas por padrão quando a funcionalidade básica já estiver disponível no ambiente.

---

# 23. Segurança básica do desktop

O ambiente deve permitir:

- Bloqueio de tela.
- Autenticação de usuário.
- Logout.
- Gerenciamento básico de usuários.
- Firewall.
- Atualizações do sistema.
- Visualização de dispositivos e serviços relevantes.

O usuário não deve precisar utilizar o terminal para executar tarefas de segurança comuns.
