TODO: documentar como atualizações remotas serão feitas:

- pasta [stow](/stow) para definições de configurações de arquivos
- pasta [docker](/docker) para definição de contâiners Docker instalados e em execução (Dockerfiles, php.ini, etc)
- arquivo [patches.sh](/patches.sh) para instalação de pacotes e serviços durante inicialização do sistema caso o disco seja imutável
- arquivo [autostart.sh](/autostart.sh) para definição de script de inicialização (git pull, execução de patches)
- quando o disco for regenerado (para reduzir o tamanho de patches.sh), uma nova branch será criada. Dessa forma a versão antiga (para máquinas que não foram regeneradas/tiveram o disco atualizado) continuarem funcionando
