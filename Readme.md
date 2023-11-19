Cenários de Solução de Problemas no Linux


É sempre crucial entender o problema. Deve haver a abordagem correta ou um
processo passo a passo a ser seguido para solucionar os problemas. Não importa se você é um
Desenvolvedor de Software, Engenheiro DevOps ou Arquiteto, o Unix/Linux é amplamente utilizado e você
deve estar ciente dos problemas e da abordagem correta para resolvê-los.
Vamos discutir alguns deles:


	Problema 1: Servidor não está acessível ou incapaz de se conectar

Abordagem / Solução:

•	Pingue o servidor pelo Nome de Host e Endereço IP
•	Nome de Host/Endereço IP é pingável
•	O problema pode estar no lado do cliente, já que o servidor é alcançável
•	Nome de Host não é pingável, mas o Endereço IP é pingável
•	Pode ser um problema de DNS
•	Verifique /etc/hosts
•	Verifique /etc/resolv.conf
•	Verifique /etc/nsswitch.conf
•	(Opcional) DNS também pode ser definido em /etc/sysconfig/network-scripts/ifcfg-<interface>
•	Nome de Host/Endereço IP não são pingáveis
•	Verifique outro servidor na mesma rede para ver se há um problema de acesso de rede ou algo ruim em geral
•	Falso: O problema não é geral na rede, mas sim com aquele host/servidor
•	Verdadeiro: Pode ser um problema geral na rede
•	Faça login no servidor pelo Console Virtual, se o servidor estiver ligado. Verifique o tempo de atividade
•	Verifique se o servidor possui o IP e se a interface de rede está UP
•	(Opcional) Verifique também informações relacionadas ao IP em /etc/sysconfig/network-scripts/ifcfg-<interface>
•	Pinge o gateway e verifique as rotas
•	Verifique o Selinux e as regras do firewall
•	Verifique a conexão física do cabo


	Problema 2: Incapaz de se conectar a um site ou aplicativo

•	Abordagem / Solução:

•	Pingue o servidor pelo Nome de Host e Endereço IP
•	Falso: Consulte o Diagrama de Solução de Problemas acima "Servidor não está acessível ou não pode se conectar"
•	Verdadeiro: Verifique a disponibilidade do serviço usando o comando telnet com a porta
•	Verdadeiro: O serviço está em execução
•	Falso: O serviço não está acessível ou em execução
•	Verifique o status do serviço usando systemctl ou outro comando
•	Verifique as regras de firewall/Selinux
•	Verifique a configuração do serviço


	Problema 3: Incapaz de fazer SSH como root ou outro usuário

•	Abordagem / Solução:

•	Pingue o servidor pelo Nome de Host e Endereço IP
•	Falso: Consulte o Diagrama de Solução de Problemas acima "Servidor não está acessível ou não pode se conectar"
•	Verdadeiro: Verifique a disponibilidade do serviço usando o comando telnet com a porta
•	Verdadeiro: O serviço está em execução
•	O problema pode estar no lado do cliente
•	O usuário pode estar desabilitado, usando um shell "nologin", com login de root desativado ou com outra configuração
•	Falso: O serviço não está acessível ou em execução
•	Verifique o status do serviço usando systemctl ou outro comando
•	Verifique as regras de firewall/Selinux
•	Verifique a configuração do serviço


	Problema 4: Espaço em disco está cheio ou precisa adicionar/estender o espaço em disco

•	Abordagem / Solução:

•	Detecção de degradação do desempenho do sistema
•	Aplicação fica lenta/não responde
•	Comandos não estão sendo executados (por exemplo, devido a espaço em disco cheio)
•	Não é possível fazer registro e outros
•	Analise o problema
•	Use o comando df para encontrar o problema no espaço do sistema de arquivos
•	Ação
•	Após encontrar o sistema de arquivos específico, use o comando du nesse sistema de arquivos para descobrir quais arquivos/diretórios são grandes
•	Comprima/elimine arquivos grandes
•	Mova os itens para outra partição/servidor
•	Verifique o estado de saúde dos discos usando o comando badblocks (por exemplo: #badblocks -v /dev/sda)
•	Verifique qual processo está vinculado à E/S (usando iostat)
•	Crie um link para um arquivo/diretório
•	Adição de novo disco
•	Partição simples
•	Adicione o disco à VM
•	Verifique o novo disco com os comandos df/lsblk
•	Use o comando fdisk para criar uma partição. É melhor usar uma partição LVM
•	Crie um sistema de arquivos e monte-o
•	Adicione uma entrada no fstab para persistência
•	Partição LVM
•	Adicione o disco à VM
•	Verifique o novo disco com os comandos df/lsblk
•	Use o comando fdisk para criar uma partição LVM
•	PV, VG, LV
•	Crie um sistema de arquivos e monte-o
•	Adicione uma entrada no fstab para persistência
•	Estenda a partição LVM
•	Adicione um disco e crie uma partição LVM
•	Adicione a partição LVM (PV) ao VG existente
•	Estenda o LV e redimensione o sistema de arquivos


	Problema 5: Sistema de arquivos corrompido

•	Abordagem / Solução:

•	Um dos erros que impedem o sistema de INICIAR
•	Verifique /var/log/messages, dmesg e outros arquivos de log
•	Se houver logs de setores defeituosos, você precisará executar o comando fsck
•	Verdadeiro:
•	Reinicie o sistema no modo de recuperação, inicializando-o a partir de um CD-ROM com a ISO aplicada
•	Prossiga com a opção 1, que monta o sistema de arquivos raiz original em /mnt/sysimage
•	Edite as entradas do fstab ou crie um novo arquivo com a ajuda de blkid e reinicie


	Problema 6: Arquivo fstab ausente ou entrada incorreta

•	Abordagem / Solução:

•	Um dos erros que impedem o sistema de INICIAR
•	Verifique /var/log/messages, dmesg e outros arquivos de log
•	Se houver logs de setores defeituosos, você precisará executar o comando fsck
•	Verdadeiro:
•	Reinicie o sistema no modo de recuperação, inicializando-o a partir de um CD-ROM com a ISO aplicada
•	Prossiga com a opção 1, que monta o sistema de arquivos raiz original em /mnt/sysimage
•	Edite as entradas do fstab ou crie um novo arquivo com a ajuda de blkid e reinicie


	Problema 7: Não é possível acessar um diretório, mesmo se o usuário tiver privilégios sudo

•	Abordagem / Solução:

•	Razões e Resolução
•	O diretório não existe
•	Conflito de caminho: caminho relativo versus absoluto
•	Permissão/propriedade do diretório pai
•	Não possui permissão de execução no diretório de destino
•	Diretório oculto


	Problema 8: Não é possível criar links

•	Abordagem / Solução:

•	Razões e Resolução
•	Diretório/Arquivo de destino não existe
•	Conflito de caminho: caminho relativo versus absoluto (deve ser um caminho completo)
•	Permissão/propriedade do diretório pai
•	Permissão/propriedade do arquivo de destino (deve ter permissão de leitura)
•	Diretório/arquivo oculto


	Problema 9: Falta de memória

•	Abordagem / Solução:

•	Tipos

•	Cache (L1, L2, L3)
•	RAM
•	Uso
•	#free -h
•	Total (Memória total atribuída)
•	Usado (Memória usada real)
•	Livre (Memória livre real)
•	Compartilhado (Memória compartilhada)
•	Buff/Cache (Memória de cache de páginas)
•	Disponível (Memória que pode ser liberada)
•	/proc/meminfo
•	Arquivo ativo
•	Arquivo inativo
•	Anônimo ativo
•	Anônimo inativo
•	Swap (Memória virtual)

•	Resolução

•	Identifique os processos que estão usando muita memória usando comandos como top, htop, ps, etc. Verifique o OOM nos logs e também verifique se há um comprometimento de memória no sysctl.conf
•	Mate ou reinicie o processo/serviço
•	Priorize o processo usando o comando nice
•	Adicione/estenda o espaço de troca
•	Adicione mais RAM física


	Problema 10: Adicionar/Estender o Espaço de Troca

•	Abordagem / Solução:

•	Devido à falta de memória, será necessário adicionar mais espaço de troca
•	Crie um arquivo com o comando #dd, pois ele reservará blocos de disco para o arquivo de troca
•	Defina as permissões como 600 e atribua a propriedade ao root
•	#mkswap
•	Agora ligue a troca com #swapon
•	Inclua uma entrada no fstab para torná-la persistente


	Problema 11: Não é possível executar determinados comandos

•	Abordagem / Solução:

•	Solução de Problemas e Resolução
•	Comando
•	Pode ser um comando relacionado ao sistema que o usuário não tem acesso
•	Pode ser um script/comando definido pelo usuário
•	Solução de Problemas
•	Permissão/propriedade do comando/script
•	Permissão do sudo
•	Caminho absoluto/relativo do comando/script
•	Não definido na variável de ambiente $PATH do usuário
•	Comando não está instalado
•	Biblioteca do comando está ausente ou foi excluída


	Problema 12: Sistema reiniciado inesperadamente e processos reiniciados?

•	Abordagem / Solução:

•	Solução de Problemas e Resolução
•	Motivos para reinício/falha do sistema
•	Estresse da CPU
•	Estresse de RAM
•	Falha do kernel
•	Falha de hardware
•	Reinicialização de processos
•	Reinicialização do sistema
•	Reinicialização automática
•	Aplicativo de watchdog
•	Para evitar alto estresse nos recursos do sistema
•	Se o aplicativo estiver causando estresse, ele será reiniciado ou encerrado
•	Solução de Problemas
•	Após fazer login, verifique o status usando comandos como uptime, top, dmesg, journalctl, iostat -xz 1
•	syslog.log, boot.log, dmesg, messages.log etc.
•	Caminho personalizado do log do aplicativo
•	Se não estiver completamente acessível, acesse o console virtual, como através do ILO, IDRAC, etc.
•	Abra um chamado e entre em contato com o fornecedor


	Problema 13: Não é possível obter um endereço IP

•	Abordagem / Solução:

•	Métodos de atribuição de IP
•	DHCP
•	Alocação fixa
•	Alocação dinâmica
•	Estático
•	Solução de Problemas
•	Verifique as configurações de rede no ambiente de virtualização, como VMware, VirtualBox, etc.
•	Verifique se o endereço IP foi atribuído ou não
•	Verifique o status da NIC do lado do host usando #lspci, #nmcli, etc.
•	Reinicie o serviço de rede


	Problema 14: Backup e Restauração das Permissões de Arquivo no Linux

•	Abordagem / Soluções:

•	Solução de Problemas
•	A melhor opção é criar o arquivo ACL de Diretórios/Arquivos antes de alterar as permissões em massa
•	Crie o arquivo ACL antes de alterar as permissões (ou faça backup das permissões do arquivo): ~$ getfacl -R <dir> > permissions.acl
•	Restaure as Permissões do Arquivo: ~$ setfacl --restore=permissions.acl
•	Restauração a partir do Snapshot da VM (mas nem sempre é uma boa opção para produção)
•	Recrie a VM (essa opção é segura para o futuro)
•	Dicas Úteis Relacionadas à Partição de Disco:

•	Dicas
•	Após adicionar/anexar um novo disco a uma VM, você pode verificar seu status com o comando lsblk fazendo ~$echo 1 > /sys/block/sda/device/rescan
•	Se você aumentar o tamanho de um disco existente, o espaço adicional será anexado ao disco existente sem afetar o sistema de arquivos e a partição já existentes
•	Você também pode recriar o sistema de arquivos no dispositivo de bloco, pois ele formatará automaticamente o antigo
•	Se você tiver um disco com uma partição/sistema de arquivos criados, você pode compartilhar o arquivo .vmdk com outra VM. Portanto, após montá-lo, você terá os mesmos dados que estavam no anterior.

Estou curtindo o curso !!!





Comandos GIT Github


Para configurar o user name:
root@ubuntu-bionic:/home/erick# git config --global user.name "Erick Chamizo"


Para configurar o e-mail:
root@ubuntu-bionic:/home/erick# git config --global user.email "erickchamizos@gmail.com"

Para cadastrar o editor de texto:
root@ubuntu-bionic:/home/erick#  git config --global core.editor vim


Para saber qual é o valor dos dados acima, exemplo do saber o user name e e-mail.
root@ubuntu-bionic:/home/erick# git config user.name
root@ubuntu-bionic:/home/erick# git config user.mail


Para saber varias informações referente ao meu Git:
root@ubuntu-bionic:/home/erick# git config --list
user.name=Erick Chamizo
user.mail=erickchamizos@gmail.com
core.editor=vim


Criar uma pasta guardar os projetos
root@ubuntu-bionic:/home/erick/curso-git# mkdir curso-git


Para inicializar o repositorio e ele se integrar ao git usar o comando abaixo, ele tem a função de inicializar o repositorio e enchergar as mudanças dentro do projeto.
root@ubuntu-bionic:/home/erick/curso-git# git init


Criando o primeiro arquivo:
vim Readme.md



#Comandos para verificar os logs:

git log
git log --decorate
git log --author="Erick Chamizo"
git shortlog
git log --graph
git Show (rash "0990d75230dd457f2e1e395d71a71585db68a507"

Com esse comando vc consegue visualizar a modificação antes de comitar.
# git diff
# git diff --name-only



#Descreva a File Status Lifecycle do GIT


O ciclo de vida do status de um arquivo no Git descreve as diferentes etapas pelas quais um arquivo passa ao ser gerenciado por esse sistema de controle de versão. Aqui estão as principais fases do ciclo de vida do status dos arquivos no Git:

#Untracked (Não Rastreado):
Um arquivo que ainda não foi adicionado ao repositório Git é considerado não rastreado.
O Git não monitora ou mantém o controle de alterações nesses arquivos.

#Staged (Preparado):
Um arquivo que foi marcado para ser incluído no próximo commit é considerado preparado ou "staged".
Isso é feito usando o comando git add [nome do arquivo] para adicionar alterações específicas ou git add . para adicionar todas as alterações.

#Unmodified (Não Modificado):
Após um commit, os arquivos entram no estado não modificado.
Isso significa que os arquivos no diretório de trabalho são iguais à versão do repositório.

#Modified (Modificado):
Quando você faz alterações em um arquivo que já está no repositório, ele entra no estado modificado.
O Git reconhece que o arquivo foi alterado, mas essas alterações ainda não foram marcadas para o próximo commit.

#Staged (Preparado):
Se você editar um arquivo modificado e o marcar novamente usando git add, ele volta ao estado preparado.
Isso significa que as alterações foram selecionadas para serem incluídas no próximo commit.

#Committed (Cometido):
Após executar git commit, as alterações preparadas são salvas no repositório como uma nova revisão.
O estado do arquivo volta a ser não modificado, e o ciclo recomeça.


Durante essas transições, você pode usar comandos como git status para verificar o estado atual dos seus arquivos e git diff para ver as diferenças entre as versões. Essas operações fazem parte do fluxo de trabalho do Git para rastrear e gerenciar as mudanças em seus projetos.
