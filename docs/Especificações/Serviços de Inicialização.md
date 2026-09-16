# Serviços de Inicialização

Este documento ainda está em fase de prototipagem. No futuro, considero colocar esse documento junto com o restante das especificações de 

## Stub: Serviços de inicialização automática
(gerado com auxílio de Inteligência Artifical)

O sistema terá rotinas a serem executadas durante a inicialização do sistema. Essas rotinas (scripts) serão divididos em serviços `systemd` independentes. Os serviços documentados até agora são:

### Sincronização Remota

Serviço responsável por:

1. Aguardar a inicialização da conectividade de rede pelo NetworkManager.
2. Verificar se há acesso efetivo à Internet; caso contrário, encerrar a execução sem falhar o sistema.
3. Sincronizar o repositório de configuração com a branch atualmente configurada (`git pull --rebase` ou equivalente).

A presença do disco persistente **não deve ser tratada como requisito para inicialização**. A VM deve continuar funcional mesmo sem o segundo `.vdi` ou mesmo caso o disco do sistema não esteja em estado imutável.

### Verificação de Integridade do Nix

Serviço independente responsável por verificar a integridade do `/nix/store` persistente.

Deve ser executado durante a inicialização, antes que o ambiente seja considerado pronto para uso, de forma que uma corrupção ou alteração não autorizada do Nix Store seja detectada antes de seu conteúdo ser utilizado.

A estratégia de reparo de store corrompido será definida posteriormente.

### Aplicação de Patches

Serviço responsável por executar `patches.sh`.

Deve depender da conclusão bem-sucedida do serviço de **Sincronização Remota**, garantindo que os patches sejam executados sobre a versão mais recente da configuração.

As dependências e a ordem de execução serão declaradas diretamente nas unidades `systemd`, evitando a necessidade de controlar manualmente a ordem através de um script de inicialização monolítico.

### Princípio

Os serviços devem ser independentes e possuir apenas as dependências necessárias entre si. A inicialização da VM não deve depender da disponibilidade do armazenamento persistente ou da Internet quando essas dependências não forem necessárias para o funcionamento básico do sistema.
