# ADR-0004: Persistência de dados sobre disco imutável

**Status:** Aceito
**Data:** 2026-08-06

## Contexto

A proposta original da equipe técnica é: construir um `.vdi` com o sistema
completo e marcá-lo como **imutável** no VirtualBox. No VirtualBox, um disco
*immutable* é reconstruído a partir do estado original a cada desligamento
da VM — qualquer escrita feita durante a sessão é descartada no próximo
boot (tecnicamente, as escritas vão para um disco diferencial temporário,
apagado ao encerrar).

Isso resolve bem o objetivo de "impedir que o aluno estrague a imagem
permanentemente", mas, se aplicado ao disco **inteiro**, também apaga:
- Projetos e código escrito pelo aluno durante a aula.
- Repositórios clonados e credenciais do Git Credential Manager.
- Bancos de dados criados em laboratórios (BD Relacional, Modelagem de BD).
- Volumes Docker de containers provisionados em aula (ex.: Oracle XE, stack
  Laravel do ADR-0003).
- Projetos Android Studio/React Native entre uma aula e a seguinte, em
  disciplinas que claramente pressupõem continuidade (Programação de
  Dispositivos Móveis I e II, Laboratório de Desenvolvimento Web).

Ou seja: imutabilidade total do disco, embora tecnicamente simples, quebra
o caso de uso pedagógico de qualquer disciplina que dependa de o aluno
continuar um projeto em sessões diferentes — o que descreve a maioria da
grade.

## Decisão

**Não** marcar o disco inteiro como imutável. Em vez disso, separar a VM em
dois discos virtuais:

1. **Disco do sistema (`sistema-base.vdi`)** — contém o SO, aplicações,
   toolchains e configuração padrão. Este sim é marcado como *immutable* no
   VirtualBox, garantindo que nenhuma alteração do aluno sobreviva a um
   reinício (proteção contra malware, configuração quebrada, etc.).
2. **Disco de dados do aluno (`dados-aluno.vdi`)**, montado em pontos como
   `/home`, `/var/lib/docker` e diretório de projetos — este disco é
   **normal** (não imutável), preservando trabalho entre sessões. Pode ser
   resetado manualmente pelo laboratório em cenários específicos (início de
   semestre, notebook público), mas não a cada boot.

## Justificativa

- Atende simultaneamente aos dois requisitos que pareciam conflitantes:
  proteção contra corrupção do sistema (o motivo original de se querer
  imutabilidade) e continuidade do trabalho do aluno entre aulas.
- Mantém a estratégia de contêineres do ADR-0003 viável: sem essa separação,
  qualquer container Docker criado em uma aula (Oracle XE, stack Laravel)
  desapareceria no boot seguinte, invalidando a escolha de usar Docker
  justamente para as disciplinas mais dependentes de estado persistente
  (banco de dados).
- É o mesmo padrão usado por laboratórios de TI em cenários análogos
  (ex.: *Deep Freeze*/*Windows Steady State* combinados com uma partição de
  dados separada, ou *live systems* Linux com *persistence partition*) —
  não é uma solução exótica, apenas adaptada à ferramenta já escolhida
  (VirtualBox *immutable disks*).

## Alternativas consideradas e descartadas

- **Disco único totalmente imutável, sem partição de dados:** rejeitado —
  inviabiliza qualquer disciplina que dependa de projeto contínuo (a
  maioria da grade), conforme listado no Contexto.
- **Disco único, não imutável, com backup/restauração manual pela equipe de
  TI:** rejeitado — depende de disciplina operacional humana constante
  (mais sujeita a falha) em vez de uma garantia estrutural da própria
  ferramenta.
- **Sincronização em nuvem por aluno (ex.: perfil de usuário remoto):**
  descartado por ora — adiciona dependência de rede constante e
  infraestrutura de backend fora do escopo desta fase do projeto; pode ser
  revisitado como evolução futura (relacionado às disciplinas de Computação
  em Nuvem I/II, hoje com tecnologia "a definir").

## Consequências

- O processo de build da imagem precisa gerar **dois** arquivos `.vdi`, e a
  documentação de setup do laboratório (fora do escopo deste documento, mas
  a ser criada) precisa instruir a equipe de TI sobre como anexar ambos os
  discos e marcar apenas o do sistema como *immutable*.
- Política de reset do disco de dados (quando e quem pode apagá-lo) precisa
  ser definida operacionalmente pela coordenação de laboratórios — sugerido
  como ADR futuro ou item de runbook operacional, não coberto aqui.
- `/home`, credenciais do Git Credential Manager e `/var/lib/docker` devem
  ser explicitamente montados no disco de dados durante a construção da
  imagem (checklist a ser incluído no script de provisionamento).
