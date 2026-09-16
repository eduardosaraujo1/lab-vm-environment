# Documentação — Imagem Padrão de Laboratório (VirtualBox)
### Curso: Desenvolvimento de Software Multiplataforma — 2026/2

Este diretório documenta o projeto de construção da máquina virtual Linux
padronizada (`.vdi`) que será distribuída nos laboratórios/desktops da
instituição, com disco marcado como imutável no VirtualBox.

## 1. Por que documentar assim

Em vez de um único relatório monolítico, optei por separar a documentação em
dois tipos de artefato, cada um seguindo um padrão já consolidado no mercado
de TI — isso facilita revisão por outros professores/técnicos e a manutenção
da imagem em semestres futuros, quando o mapa de disciplinas mudar.

### 1.1. Registros de Decisão de Arquitetura (ADR)

Para toda decisão técnica relevante (sistema base, servidor gráfico,
estratégia de contêineres, política de persistência), uso o formato **ADR —
Architecture Decision Record**, popularizado por Michael Nygard e hoje padrão
de facto em times de engenharia/infra. Cada ADR responde: qual era o
contexto, o que foi decidido, quais alternativas foram descartadas e por quê,
e quais as consequências (inclusive as negativas). Isso cria um histórico
rastreável — se um técnico futuro quiser reabrir a discussão "por que não
usamos Wayland?", a resposta já está registrada, com as premissas que a
motivaram, em vez de se perder em conversa de corredor.

Arquivos: `ADR-000X-titulo.md`, numerados em ordem cronológica e nunca
reescritos — se uma decisão muda, cria-se um novo ADR marcando o antigo como
"Substituído por ADR-000Y", preservando o histórico (mesma prática usada em
`adr.github.io` / ferramentas como `adr-tools`).

### 1.2. Inventário de Software

Para o mapeamento disciplina → aplicação → forma de instalação, uso uma
tabela estruturada inspirada nos princípios de um **SBOM (Software Bill of
Materials — cf. formatos CycloneDX/SPDX)**: todo componente instalado na
imagem precisa ter proveniência e método de instalação declarados, o que
facilita auditoria de licenças (ex.: Oracle, Cisco Packet Tracer têm EULAs
específicas), atualização e resposta a vulnerabilidades. Não uso as
ferramentas formais de SBOM (não fariam sentido para uma imagem de
laboratório), mas mantenho a mesma disciplina de "nada entra na imagem sem
estar documentado".

Arquivo: `inventario-software.md`.

## 2. Índice de documentos

| Documento | Conteúdo |
|---|---|
| `ADR-0001-sistema-operacional-base.md` | Escolha da distribuição base |
| `ADR-0002-ambiente-grafico.md` | Xorg vs. Wayland e ambiente de desktop |
| `ADR-0003-estrategia-containers.md` | O que vai em Docker e o que fica nativo |
| `ADR-0004-persistencia-imagem-imutavel.md` | Risco de imutabilidade total do disco |
| `inventario-software.md` | Mapa completo disciplina → software → instalação |

## 3. Processo de manutenção

A cada novo semestre, o coordenador de curso deve fornecer a grade
atualizada. As disciplinas hoje marcadas como `-*` (tecnologia não definida)
devem ser revisadas com o professor responsável **antes** do fechamento da
imagem do semestre; a entrada correspondente no inventário deve sair de
"a definir" para uma decisão registrada (mesmo que seja "nenhum software
adicional necessário"). Mudanças de sistema base, ambiente gráfico ou
estratégia de contêiner exigem um novo ADR, não uma edição silenciosa.
