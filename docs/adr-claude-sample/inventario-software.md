# Inventário de Software — Imagem Base 2026/2

Base: Debian 12 (Bookworm) + backports · Xorg + XFCE · ver ADR-0001 a
ADR-0004 para as decisões que fundamentam as colunas "Instalação" abaixo.

Legenda da coluna **Instalação**:
- `APT` — pacote do repositório Debian *stable* ou `backports`.
- `Repo 3º` — repositório de terceiros oficial adicionado ao APT (ex.:
  NodeSource, Docker, Microsoft).
- `Bin/Tarball` — instalador binário oficial do fornecedor, fora de
  repositório APT.
- `Wine` — aplicação Windows rodando via Wine nativo (não em Docker; ver
  ADR-0003).
- `Docker` — provisionado via container (Docker/`simple-container-manager`;
  ver ADR-0003).
- `Firejail` — executado sob sandbox de rede conforme especificado na grade.
- `A definir` — disciplina marcada `-*`; tecnologia não conhecida ainda,
  ver seção 4.

## 1. Pacote "Geral" (toda a imagem, independente de disciplina)

| Aplicação | Instalação | Observações |
|---|---|---|
| Neovim 12.x | APT/backports | Confirmar se a versão exata está em backports no momento do build; senão, PPA/tarball oficial. |
| Git + Git Credential Manager | APT + Bin | GCM não tem pacote Debian oficial; instalar `.deb` publicado no GitHub do GCM. |
| Nala (front-end do APT) | APT/Repo 3º | Repositório oficial do projeto (`volitank/nala`). |
| Docker (Engine + Compose) | Repo 3º | Repositório oficial Docker para Debian. |
| simple-container-manager | Bin/Tarball | Instalar a partir do repositório GitHub indicado na grade. |
| Toolkit C++ (CMake, gdb, Ninja, clangd) | APT | Extensões correspondentes do VS Code pré-instaladas/pré-configuradas na imagem. |
| Toolkit Java (VS Code) | APT + extensão VS Code | JDK específico entra por disciplina (ver TEC. PROG I/II abaixo). |
| Google Chrome | Repo 3º | Repositório oficial Google, necessário para DES. WEB I e testes de front-end em geral. |
| LibreOffice (Calc etc.) | APT | Cobre MAT. COMP e ALG. LINEAR nativamente; alternativa self-service a Excel/Google Sheets. |

## 2. 1º Semestre

| Disciplina | Aplicação | Instalação |
|---|---|---|
| ALG. PROG V | .NET SDK (C# Console App) | Repo 3º (repositório Microsoft) |
| DES. DIGITAL V | Inkscape | APT |
| DES. DIGITAL V | GIMP | APT |
| DES. WEB I V | Visual Studio Code | Repo 3º (repositório Microsoft) |
| DES. WEB I V | Node.js | Repo 3º (NodeSource, versão LTS vigente) |
| DES. WEB I V | prettier, eslint | npm (via Node.js acima) |
| DES. WEB I V | Chrome | Repo 3º (ver pacote Geral) |
| ENG. SOFT. I V | — | Nenhuma aplicação prevista (ver nota da grade) |
| MOD. BD V | DbDesigner Fork | **Wine** |
| MOD. BD V | Oracle Data Modeler | Bin/Tarball (instalador Oracle oficial) |
| SIST. OP. REDES COMP. V | Cisco Packet Tracer | Bin/Tarball + **Firejail** (`firejail --net 0`, conforme grade) |
| SIST. OP. REDES COMP. V | Wireshark | APT (ver ADR-0003 — mantido nativo por precisar de acesso direto à interface de rede) |

## 3. 2º Semestre

| Disciplina | Aplicação | Instalação |
|---|---|---|
| BD RELACIONAL V | Oracle XE 11g | **Docker** (imagem oficial Oracle; ver ADR-0003) |
| DES. WEB II V | PHP 8.3 | **Docker** via `simple-container-manager` mascarado como "XAMPP" (requisito explícito da grade) |
| DES. WEB II V | Apache Server | **Docker** (mesmo stack acima) |
| DES. WEB II V | Laravel tooling | **Docker** (mesmo stack) + Composer disponível no host se necessário |
| DES. WEB II V | VS Code + Intelephense | APT/Repo 3º (VS Code) + extensão |
| ENG. SOFT. II V | — | Nenhuma aplicação prevista |
| EST. DADOS V | VS Code + Toolkit C++ | Reaproveita pacote Geral |
| MAT. COMP V | Excel/Sheets/Calc | LibreOffice Calc nativo (pacote Geral); Excel/Sheets são web/cloud, sem instalação |
| TEC. PROG I V | Eclipse | Bin/Tarball (instalador oficial Eclipse) |
| TEC. PROG I V | OpenJDK 25 | APT/backports (confirmar disponibilidade; senão tarball Adoptium/Temurin) |

## 4. 3º Semestre

| Disciplina | Aplicação | Instalação |
|---|---|---|
| ALG. LINEAR V | Excel/Sheets/Calc | LibreOffice Calc nativo (pacote Geral) |
| BD NAO RELACIONAL V | — | A definir junto ao professor (grade marca `-`, sem tecnologia nomeada ainda) |
| DES. WEB III V | Python 3.14 | APT/backports (confirmar versão; senão `deadsnakes`-like/tarball oficial) |
| DES. WEB III V | Django | pip/venv sobre o Python instalado (nativo — ver ADR-0003, não containerizado) |
| GEST. AGIL PROJ. SOFT. V | — | **A definir** (`-*`) |
| Inglês I V | — | **A definir** (`-*`) — provavelmente sem app dedicado |
| INT. HUM. COMP. V | Visual Studio Code | Reaproveita pacote Geral |
| TEC. PROG II V | IntelliJ IDEA | Bin/Tarball (instalador oficial JetBrains) |
| TEC. PROG II V | Maven, Gradle | APT ou Bin/Tarball (versão mais recente costuma sair primeiro como tarball oficial) |
| TEC. PROG II V | OpenJDK 25 | Mesma entrada de TEC. PROG I |

## 5. 4º Semestre

| Disciplina | Aplicação | Instalação |
|---|---|---|
| Estatística Aplicada V | — | **A definir** (`-*`) |
| EXP. USUARIO V | — | **A definir** (`-*`) |
| Inglês II V | — | **A definir** (`-*`) |
| INT. COISAS APLIC. V | — | **A definir** (`-*`) — possível necessidade de ferramentas de firmware/serial; revisar antes do semestre |
| INTEG. ENT. CONT. V | — | **A definir** (`-*`) — nome sugere CI/CD; possivelmente coberto por Git/Docker já presentes no pacote Geral |
| LAB. DES. WEB V | — | **A definir** (`-*`) — provável reaproveitamento de DES. WEB I/II/III |
| PROG. DISP. MOVEIS I V | Android Studio | Bin/Tarball (instalador oficial Google) — **nativo**, ver ADR-0003 sobre virtualização aninhada |
| PROG. DISP. MOVEIS I V | Emulador Android 16 | Incluso no Android Studio; nativo |
| PROG. DISP. MOVEIS I V | Kotlin Toolkit | Plugin/SDK via Android Studio |
| PROG. DISP. MOVEIS I V | Jetpack Compose | Biblioteca de projeto (via Gradle), sem instalação de sistema adicional |

## 6. 5º Semestre

| Disciplina | Aplicação | Instalação |
|---|---|---|
| APREN. MAQUINA V | — | **A definir** (`-*`) — provável Python/Jupyter; reaproveitaria Python já instalado em DES. WEB III |
| COMP. NUVEM I V | — | **A definir** (`-*`) — possivelmente apenas contas web/cloud, sem instalação local |
| FUND. REDAC. TEC V | — | **A definir** (`-*`) — provável apenas LibreOffice Writer, já coberto se pacote Geral incluir suíte completa |
| Inglês III V | — | **A definir** (`-*`) |
| LAB. DES. DISP. MOVEIS V | — | **A definir** (`-*`) — provável reaproveitamento de Android Studio/React Native |
| PRO. DISP. MOVEIS II V | React Native | npm/Node.js (reaproveita Node.js do pacote Geral) |
| PRO. DISP. MOVEIS II V | Expo | npm/Node.js (idem) |
| SEGURANÇA EM DESENV. DE APLIC. V | — | **A definir** (`-*`) |

## 7. 6º Semestre

| Disciplina | Aplicação | Instalação |
|---|---|---|
| COMP. NUVEM II V | — | **A definir** (`-*`) |
| ETI. PROF. PAT V | — | **A definir** (`-*`) — provavelmente sem app dedicado |
| Inglês IV V | — | **A definir** (`-*`) |
| LAB. DES. MULTI V | — | **A definir** (`-*`) — projeto integrador, tecnologia depende do tema escolhido |
| MIN. DADOS V | — | **A definir** (`-*`) — provável Python/ferramentas de dados |
| PROC. LING. NATURAL V | — | **A definir** (`-*`) — provável Python |
| QUAL. TESTES SOFT. V | IntelliJ IDEA | Reaproveita instalação de TEC. PROG II |
| QUAL. TESTES SOFT. V | JUnit | Biblioteca de projeto (via Maven/Gradle), sem instalação de sistema adicional |

## 8. Itens pendentes de decisão (`-*`)

As disciplinas abaixo estão marcadas na grade original como tecnologia
desconhecida pelo autor do levantamento. Nenhuma delas deve ser
interpretada como "ficará de fora da imagem" — cada uma precisa ser
confirmada com o professor responsável antes do fechamento da imagem do
semestre correspondente, conforme processo descrito em `README.md`, seção
3:

Gestão Ágil de Projetos de Software, Inglês I–IV, Experiência do Usuário,
Internet das Coisas Aplicada, Integração Entrega Contínua, Laboratório de
Desenvolvimento Web, Aprendizagem de Máquina, Computação em Nuvem I e II,
Fundamentos de Redação Técnica, Laboratório de Desenvolvimento de
Dispositivos Móveis, Segurança em Desenvolvimento de Aplicações, Ética
Profissional e Patrimonial, Laboratório de Desenvolvimento Multiplataforma,
Mineração de Dados, Processamento de Linguagem Natural, Banco de Dados Não
Relacional.

Muitas dessas provavelmente se enquadram no caso 2 da observação original da
grade (tecnologia web/cloud sem instalação local) ou caso 1 (nenhuma
tecnologia), mas isso precisa ser confirmado, não presumido — em especial
Internet das Coisas Aplicada (pode exigir ferramentas de porta
serial/firmware, o que teria implicação direta de driver USB *passthrough*
no VirtualBox) e Banco de Dados Não Relacional (pode exigir outro container
Docker, análogo ao Oracle XE).
