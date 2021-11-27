# Born2beRoot

### Overview

#### Como funciona uma VM ?

Uma máquina virtual (VM) é um ambiente virtual que funciona como um sistema de computação com sua própria CPU, memória, interface de rede e armazenamento. Esse sistema virtual é criado a partir de um sistema de hardware físico localizado on-premise ou não. Um software chamado de hipervisor separa do hardware os recursos utilizados pela máquina virtual e os provisiona adequadamente.

A máquina física, onde o hipervisor, como a Máquina virtual baseada em kernel (KVM), está instalado é chamada de host. AS VMs que usam os recursos da máquina host é chamadas de guest. O hipervisor trata os recursos de computação (por exemplo, CPU, memória e armazenamento) como um pool que pode ser realocado com facilidade entre os guests existentes ou para novas máquinas virtuais.

A tecnologia de virtualização permite compartilhar um sistema com muitos ambientes virtuais. O hipervisor gerencia o hardware e separa os recursos físicos dos ambientes virtuais. Os recursos são particionados, conforme a necessidade, a partir do ambiente físico para as máquinas virtuais.

Quando a máquina virtual está sendo executada e um usuário ou programa emite uma instrução que exige recursos adicionais do ambiente físico, o hipervisor programa essa solicitação. Assim, as aplicações e o sistema operacional da máquina virtual podem acessar o pool compartilhado de recursos físicos.

#### CentOS vs Linux

![centosxlinux](https://cdn.educba.com/academy/wp-content/uploads/2018/09/CentOS-vs-Debian-1.jpg.webp)

#### Por que usar máquinas virtuais?

apt-get e aptitude são interfaces de gerenciamento de pacotes linha de comando no Debian.

O principal motivo para usar máquinas virtuais é a consolidação do servidor. A maioria das implantações de aplicações e sistemas operacionais utiliza somente uma pequena parcela dos recursos físicos disponíveis quando executadas em bare-metal. Ao virtualizar as máquinas, é possível colocar vários servidores virtuais em cada servidor físico para otimizar o uso do hardware. 

Isso diminui a necessidade de adquirir mais recursos físicos, como discos rígidos, assim como de usar mais energia, espaço e poder de resfriamento no datacenter. As máquinas virtuais oferecem mais opções de recuperação de desastres, pois permitem implementar failover e redundância. Antes isso só era possível apenas com o uso de hardwares adicionais.

As máquinas virtuais fornecem um ambiente que é isolado do resto do sistema. Então, independentemente do que estiver sendo executado na máquina virtual, não haverá interferência alguma no que estiver sendo executado no hardware host.

Como proporcionam isolamento, as máquinas virtuais são uma boa opção para testar novas aplicações ou configurar um ambiente de produção. Também é possível executar uma máquina virtual de uma única finalidade para dar suporte a um processo específico.

### apt vs aptitude

A diferença mais óbvia é que aptitudefornece uma interface de menu de terminal (semelhante ao Synaptic em um terminal), enquanto apt-getnão fornece.

Considerando apenas as interfaces de linha de comando de cada uma, elas são bastante semelhantes e, na maioria das vezes, realmente não importa qual delas você usar. As versões recentes de ambos rastrearão quais pacotes foram instalados manualmente e quais foram instalados como dependências (e, portanto, elegíveis para remoção automática). De fato, acredito que, ainda mais recentemente, as duas ferramentas foram atualizadas para compartilhar o mesmo banco de dados de pacotes instalados manualmente ou automaticamente, portanto, os casos em que você instala algo com o apt-get e depois o aptitude deseja desinstalá-lo são principalmente uma coisa do o passado.

Existem algumas pequenas diferenças:

O aptitude removerá automaticamente pacotes elegíveis, enquanto o apt-get requer um comando separado para fazer isso
Os comandos para atualização vs. dist-upgrade ter sido renomeado na aptidão para os nomes provavelmente mais precisos seguro à atualização e à atualização completa , respectivamente.
O aptitude realmente executa as funções não apenas do apt-get, mas também de algumas de suas ferramentas complementares, como apt-cache e apt-mark.
O aptitude possui uma sintaxe de consulta ligeiramente diferente para pesquisa (em comparação com o apt-cache)
O aptitude possui os comandos por que e por que não para lhe dizer quais pacotes instalados manualmente estão impedindo uma ação que você pode querer executar.
Se as ações (instalação, remoção, atualização de pacotes) que você deseja executar causam conflitos, o aptitude pode sugerir várias possíveis soluções. O apt-get dirá "Sinto muito, Dave, não posso permitir que você faça isso".

#### APPArmor

O Apparmor é um sistema de controle de acesso obrigatório (ou MAC). Ele usa aprimoramentos do kernel LSM para restringir os programas a determinados recursos. O AppArmor faz isso com perfis carregados no kernel quando o sistema é iniciado. O Apparmor tem dois tipos de modos de perfil: imposição e reclamação. Os perfis no modo de imposição aplicam as regras desse perfil e relatam tentativas de violação em syslogou auditd. Os perfis no modo de reclamação não impõem nenhuma regra de perfil, apenas tentativas de violação de log.

### Setup

#### UFW

```sh
sudo ufw status
```

#### SSH

```sh
sudo service ssh status
```

#### Check OS

```sh
sudo cat /etc/os-release
```

### User

#### Check user groups

```sh
groups vcordeir
```

#### Password Policy

1. Configurações de Senha

Arquivo de configuração `/etc/login.defs`. Alterar:

- PASS_MAX_DAYS 30
- PASS_MIN_DAYS 2
- PASS_WARN_AGE 7

2.  Política de Senhas Forte - `lib-pwquality`

Verificar instalação: `dpkg -l | grep libpam-pwquality`

Alterar o arquivo: `/etc/pam.d/common-password`

| Comando          | Significado                                               |
|------------------|-----------------------------------------------------------|
| retry=3          | número máximo de tentativas                               |
| minlen=10        | tamanho mínimo de caracteres da senha                     |
| ucredit=-1       | pelo menos uma letra maiúscula                            |
| dcredit=-1       | pelo menos um número                                      |
| maxrepeat=3      | não pode ter mais que 3 caracteres idênticos consecutivos |
| reject_username  | não pode incluir o nome do usuário                        |
| difok=7          | não pode repetir 7 dos caracteres da senha anterior       |
| enforce_for_root | o root deve obedecer os mesmos critérios                  |

#### User

```sh
adduser <username>
```

```sh
deluser <username>
```

```sh
getent passwd <username>
```

```sh
chage -l <username>
```

#### Groups

```sh
addgroup <group_name>
```

```sh
delgroup <group_name>
```

```sh
cat etc/group
```

```sh
gpasswd -a <username> <group_name>
```

```sh
getent group user42
```

### Hostname

```sh
hostnamectl
```

```sh
sudo hostname NEW_HOSTNAME
```

### Partitions

```sh
lsblk
```

### Sudo

Criar o diretório:

```sh
sudo mkdir /var/log/sudo
```

Arquivo de configuração:

```sh
sudo visudo
```

- Limitar a 3 tentativas: `Defaults passwd_tries = 3`

- Mensagem de erro:   `Defaults badpass_message`

- Salvar todos os acessos via sudo: 

```sh
Defaults logfile="/var/log/sudo/sudo.log"

Defaults log_input, log_output

Defaults iolog_dir="/var/log/sudo"
```

- Para solicitar TTY: `Defaults requiretty`

- Definir local do sudo: `Defaults secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"`

### UFW

UFW, or uncomplicated firewall, is a frontend for managing firewall rules in Arch Linux, Debian, or Ubuntu.

```sh
dpkg -l | grep ufw
```

Verificar o status: `ufw status numbered`

Permitir conexões na porta 8080: `ufw allow 8080`

Deletar conexão: `ufw delete (that number, for example 5 or 6)`

### SSH

```sh
dpkg -l | grep ssh
```

```sh
service ssh status
```

### Script monitoring.sh

Need these to run on 30-sec boundaries, keep commands in sync.

```sh
* * * * *              /path/to/executable param1 param2
* * * * * ( sleep 30 ; /path/to/executable param1 param2 )
```

### Links

- [VM](https://www.redhat.com/pt-br/topics/virtualization/what-is-a-virtual-machine)

- [CentOS vs Linux](https://www.educba.com/centos-vs-debian/)

- [apt vs aptitude](https://qastack.com.br/unix/767/what-is-the-real-difference-between-apt-get-and-aptitude-how-about-wajig)

- [APPArmor](https://qastack.com.br/ubuntu/236381/what-is-apparmor)