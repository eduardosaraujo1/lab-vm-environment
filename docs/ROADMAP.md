# Lista de Tarefas

1. [x] Documentar todas as tecnologias que serão utilizadas durante o curso em 2026/2
2. [ ] Escrever ADRs manualmente para prática
3. [ ] Consolidar com Claude essas disciplinas com o plano feito anteriormente (README_old.md + ADRs escritas manualmente)
4. [ ] Criar .vdi a partir das instruções, documentando qualquer desvio de plano em `implementation_deviations.md`
5. [ ] Escrever manual do usuário para o projeto e incluir no README.md principal usando \<details\>

# Scratchpad

You are now an operating systems professor tasked with helping your college institution to develop a Linux virtual environment for college desktops. Due to some technical limitations, this environment should work as a VirtualBox Linux Virtual Machine. The tech team has done some research as testing, and decided creating a .vdi file with the entire system, and then setting the disk to immutable is enough.

Your task is to analyze the curriculum, determine which applications each student needs, and document everything.

The first step is to decide how you will document this project. If possible, reference document standards that already exist.

Then, look at the disciplines ministered in the institution and decide what base system should be used. The tech team suggested Debian since its update cycles are less frequent, but still keeps a relatively rich software support. However, they also said an immutable distro could theoretically work but they have no experience on software support on those. The team also advised that Wayland-based environments are prone to screen tearing on VirtualBox, and Xorg is prefered. Lastly, the team suggested to use docker containers where possible, because those are easier to update and maintain even if an application is not directly compatible with the underlying OS.

Lastly, the documentation should be written in pt-BR. Here is the map of discipline and technologies used (so far):
(see docs/grade-2026.md)
