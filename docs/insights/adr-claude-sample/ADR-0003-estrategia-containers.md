# ADR-0003: Critério de uso de contêineres Docker

**Status:** Aceito
**Data:** 2026-08-06

## Contexto

A equipe técnica indicou preferência por Docker sempre que possível, por
facilidade de atualização/manutenção mesmo quando uma aplicação não é
diretamente compatível com o SO base — o que se aplica bem a serviços de
backend/banco de dados, mas não é universalmente verdadeiro para todo tipo
de software da grade (há IDEs gráficas, apps Wine, e até um emulador Android
que depende de virtualização aninhada).

O currículo já nomeia explicitamente duas ferramentas de orquestração leve:
`docker` puro e o
[`simple-container-manager`](https://github.com/eduardosaraujo1/simple-container-manager/),
citado especificamente em **DES. WEB II** para "mascarar" um ambiente
Docker como se fosse um XAMPP tradicional — ou seja, o objetivo pedagógico
ali é dar ao aluno uma experiência de "clique e use" equivalente ao XAMPP,
escondendo a complexidade de containers.

## Decisão

Adotar contêineres Docker (geridos via `simple-container-manager` quando a
disciplina pedir uma experiência "tipo XAMPP", ou via `docker compose` puro
nos demais casos) **apenas** para software de **backend/serviço** com
requisitos de versão sensíveis ou historicamente frágeis de instalar/
desinstalar. Manter **instalação nativa** para IDEs, ferramentas gráficas de
desktop, e qualquer aplicação que dependa de acesso direto a
GPU/virtualização aninhada.

### Vai para Docker

| Aplicação | Disciplina | Motivo |
|---|---|---|
| Oracle XE (11g e a versão mais atual usada em BD Relacional) | MOD. BD, BD RELACIONAL | Instalador Oracle é notoriamente frágil para instalar/remover de forma limpa em Debian; Oracle publica imagens oficiais de container, tornando o Docker o caminho *mais* suportado, não uma alternativa de segunda linha. |
| PHP 8.3 + Apache + Laravel tooling ("XAMPP" via `simple-container-manager`) | DES. WEB II | Requisito explícito da grade; permite trocar versão de PHP/Apache por semestre sem reinstalar nada no sistema base. |

### Fica nativo (fora de container)

| Aplicação | Motivo de não containerizar |
|---|---|
| Android Studio + emulador Android 16 | Emulação de hardware Android dentro de um contêiner, dentro de uma VM VirtualBox, empilha *virtualização aninhada* — geralmente indisponível/instável em laboratórios sem VT-x/AMD-V exposto de forma aninhada ao convidado. Melhor mantido nativo, com aceleração via software se necessário. |
| Eclipse, IntelliJ, VS Code, Android Studio (as IDEs em si) | Aplicações gráficas de desktop; containerizar GUI exige X11 forwarding extra sem ganho real, já que a "imutabilidade"/reprodutibilidade já vem da imagem `.vdi` como um todo. |
| GIMP, Inkscape | Idem — apps gráficas de desktop, sem vantagem de isolamento aqui. |
| DbDesigner Fork (via Wine), Oracle Data Modeler | Rodar Wine dentro de um contêiner Docker adiciona uma segunda camada de compatibilidade sobre a primeira (Wine já é uma camada de compatibilidade); sem necessidade, pois o app já roda isolado o suficiente via Wine no sistema imutável. |
| Cisco Packet Tracer | Já roda sob isolamento próprio (`firejail --net 0`, conforme especificado pela grade); Docker adicionaria uma segunda camada de rede virtual sem necessidade, e potencialmente conflitando com o isolamento de rede pedido pela disciplina. |
| Node.js/toolchain de DES. WEB I, Python/Django de DES. WEB III | Ferramentas de desenvolvimento onde o aluno edita arquivos localmente e espera *live reload*/depuração direta na IDE;versionamento de runtime aqui é melhor resolvido com gerenciador de versão nativo (`nvm`, `venv`/`pyenv`) do que container, evitando a complexidade extra de montar volumes para todo projeto de aula. |
| Wireshark | Precisa de acesso direto à interface de rede da VM para captura; rodar em container complicaria permissões de rede sem benefício. |

## Justificativa geral do critério

O critério de decisão não é "Docker sempre que possível", mas sim: **Docker
quando o ganho de isolamento/versionamento supera o custo de indireção**,
especificamente para serviços de backend com histórico de instalação
problemática (Oracle) ou onde a própria disciplina pede a abstração
(XAMPP). Para ferramentas de desktop e depuração local, a indireção de um
contêiner atrapalha mais do que ajuda, e a "facilidade de manutenção" já é
garantida pela própria natureza da imagem `.vdi` versionada por semestre.

## Consequências

- `docker` e `simple-container-manager` devem estar pré-instalados e
  pré-configurados na imagem base (ver seção "Geral" do inventário), mesmo
  que os containers específicos (Oracle XE, stack Laravel) sejam
  provisionados sob demanda pelo aluno/professor, não pré-embutidos na
  imagem — reduz o tamanho do `.vdi` final.
- Ver ADR-0004 quanto ao risco de volumes Docker (`/var/lib/docker`) não
  persistirem se o disco for 100% imutável — isso é tratado como uma
  decisão separada de persistência, não de containerização.
