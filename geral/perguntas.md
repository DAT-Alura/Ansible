# Perguntas

## Aula 1

1 - Temos as seguintes afirmativas sobre Ansible e Infraestrutura sobre código:

A) Infraestrutura como código é a base da cultura DevOps, encurtando assim o ciclo de feedback entre os times de desenvolvimento e os de infraestrutura.

B) É a partir da máquina de controle com o Ansible instalado que gerenciamos outras máquinas.

C) As máquinas gerenciadas pelo Ansible só precisam do Python e de um servidor SSH instalados.

Podemos afirmar que:

- Apenas a afirmativa C é falsa.
- __Todas as afirmativas são verdadeiras.__

> Realmente todas as afirmativas são verdadeiras. Animado para aprender mais sobre Ansible?

- Apenas a afirmativa A é falsa.

2 - Temos as seguintes afirmativas a respeito do Ansible

A) O Ansible é uma ferramenta que auxilia no processo de infraestrutura como código.

B) Arquivo de inventário: arquivo com as "receitas de bolo" do que queremos fazer.

C) Playbook: é aquele que lista todas as máquinas que serão utilizadas.

Podemos afirmar que:

- __As afirmativas B e C são falsas.__

> Alternativa correta! O arquivo de inventário é aquele que lista todas as máquinas que serão configuradas e o Playbook é o arquivo com as "receitas de bolo" do que queremos fazer.

- Apenas a afirmativa B é falsa.
- As afirmativas A e B são falsas.

3 - Ricardo está começando a estudar Ansible. Ele já subiu a sua máquina com o Vagrant, criou o arquivo de inventário hosts com o grupo groupA, com o IP 10.0.0.1, e resolveu fazer um teste, imprimindo o famoso Hello, World, através do seguinte comando:

```ansible groupA -u vagrant -i hosts -m shell -a 'echo Hello, World'```

Esse comando irá funcionar?

- Sim, o comando irá executar com sucesso e imprimirá uma saída semelhante a esta:  
```10.0.0.1 | SUCCESS | rc=0 >> Hello, World```
- Sim, o comando irá executar, mas não imprimirá nenhuma saída.
- __Não, pois o Ansible não conseguirá fazer a autenticação para executar um comando na máquina.__

> Alternativa correta! Para fazer a autenticação, uma chave precisa ser passada, que o próprio Vagrant cria:  
> ```ansible wordpress -u vagrant --private-key .vagrant/machines/wordpress/virtualbox/private_key -i hosts -m shell -a 'echo Hello, World'```

- Não, pois o IP da máquina não foi passado para o comando.

## Aula 2

1 - A Ana quer criar um Playbook que gere um arquivo txt com o seu nome dentro do arquivo /vagrant/nome.txt. A tarefa deve funcionar para todos os hosts configurados. Como deverá ficar esse Playbook?

- __A__

``` yml
---
- hosts: all
  tasks:
    - shell: "echo Ana > /vagrant/nome.txt"
```

> Alternativa correta! A primeira linha do Playbook são três hífens, o primeiro elemento são os hosts que o Ansible vai trabalhar e após isso são escritos os comandos a serem executados, que são uma lista de tasks. Para escrever o nome em um arquivo, utilizamos o módulo shell, executando o comando echo em seguida.

- B

``` yml
- hosts: all
  tasks:
    - shell: "echo Ana > /vagrant/nome.txt"
```

- C

``` yml
---
- hosts: all
    - shell: "echo Ana > /vagrant/nome.txt"
```

- D

``` yml
- hosts: all
  tasks:
    - echo: "Frederico > /vagrant/nome.txt"
```

2 - Tendo como referência o Playbook abaixo, podemos dizer:

``` yml
---
- hosts: all
    - name: 'Instala o PHP5'
        name: php5
        state: latest
      become: yes
```

- O arquivo possui 3 erros.
- O arquivo possui 1 erro.
- O arquivo está correto.
- __O arquivo possui 2 erros.__

> Alternativa correta! O arquivo possui 2 erros: faltou colocar a dependência na lista de tasks e declarar o módulo a ser utilizado, o apt. O arquivo correto seria:
>
> ``` yml
> ---
> - hosts: all
>   tasks:
>     - name: 'Instala o PHP5'
>       apt:
>         name: php5
>         state: latest
>       become: yes
> ```

3 - Abaixo estão algumas palavras-chave do Ansible e os seus usos. Mas há um uso incorreto, qual?

- hosts: Indica para qual grupo ou host do arquivo de inventário o Ansible vai aplicar as tarefas.
- __become: É um booleano e indica se a task será executada antes das outras tasks.__

> Alternativa correta! O uso do become está incorreto, pois ele é um booleano e indica se a task será executada com ou sem privilégios administrativos.

- tasks: Lista principal de comandos a serem executados nos hosts selecionados.

## Aula 3

1 - Temos as seguintes afirmativas sobre with_items:

A) O parâmetro with_items fica no nível da task, ou seja, não faz parte da task.

B) Em with_items, passamos o nome (name) dos pacotes das tasks que desejamos que ele contenha.

C) Acabamos escrevendo mais com with_items.

Podemos afirmar que:

- __Apenas as afirmativas A e B são verdadeiras__

> Alternativa correta! A afirmativa C é falsa, pois acabamos escrevendo menos com with_items.

- Apenas as afirmativas B e C são verdadeiras
- Apenas as afirmativas A e C são verdadeiras

2 - No último vídeo aprendemos sobre a variável especial item. Qual das afirmações abaixo é verdadeira?

- __Ela é uma palavra reservada do Ansible e com ela conseguimos fazer uma referência a todos os elementos inclusos em uma lista.__

> Alternativa correta! Ela é uma palavra reservada do Ansible e serve para fazer uma referência aos objetos inclusos na nossa lista de dependências.

- Não tem utilidade real, já que é muito mais fácil utilizar diversas tasks diferentes.
- Ela é meramente semântica e com ela conseguimos fazer uma referência a um o elemento de uma lista.

## Aula 4

1 - Aprendemos no último vídeo como podemos usar o Ansible para criar e deletar bancos de dados. Qual das opções abaixo realiza a opção de criação de uma base de dados MySQL chamada bancoteste?

- A

``` yml
- name: 'Cria o banco do MySQL'
  mysql_db:
    name: bancoteste
    login_user: root
    state: create
```

- B

``` yml
- name: 'Cria o banco do MySQL'
  mysql_db:
    name: bancoteste
    login_user: root
    state: new
```

- __C__

``` yml
- name: 'Cria o banco do MySQL'
  mysql_db:
    name: bancoteste
    login_user: root
    state: present
```

> Alternativa correta! Com essa sintaxe e com o state present, a base de dados MySQL bancoteste é criada.

- D

``` yml
- name: 'Cria o banco do MySQL'
  mysql_db:
    name: bancoteste
    login_user: root
    state: absent
```

2 - O usuário do MySQL também possui alguns privilégios, que são configurados no parâmetro priv. Como seria a permissão para o usuário poder fazer todas as operações comuns em todas as tabelas da base de dados alura_ansible?

- priv: '*.*:ALL'
- __priv: 'alura_ansible.*:ALL'__

> Alternativa correta! O formato da string de privilégio é: base_de_dados.tabela:privilegio. A base de dados é alura_ansible, as tabelas são todas (logo, utiliza-se *) e para o usuário poder fazer todas as operações comuns no banco de dados, usa-se ALL.

- priv: 'ALL.*:alura_ansible'

3 - Tendo como referência a task abaixo de criação de um usuário do MySQL, podemos dizer:

``` yml
- name: 'Cria o usuário do MySQL'
  mysql_user:
    login: root
    alias: wordpress_user
    pass: 12345
    priv: 'wordpress_db.*:ALL'
    state: present
```

- Ela possui 1 erro.
- Ela está correta.
- __Ela possui 3 erros.__

> Alternativa correta! A task possui 3 erros: o usuário que será utilizado para fazer a autenticação não é passado no parâmetro login, e sim no parâmetro login_user; o usuário a ser criado não é passado no parâmetro alias, e sim no parâmetro name; e por fim, a senha do usuário não é passada no parâmetro pass, e sim no parâmetro password. O três parâmetros incorretos sequer existem.

- Ela possui 2 erros.

## Aula 5

1 - Temos o seguinte código:

``` yml
- name: 'x'
  get_url:
    url: 'https://endereco.com/x.zip'
    dest: '/tmp/y.zip'
```

Podemos afirmar que:

- __O Ansible baixará o arquivo da URL definida na propriedade url, gravando-o na pasta indicada na propriedade dest, com o nome que definirmos.__

> Alternativa correta! Na propriedade ```url```, é definida a URL que o Ansible utilizará para baixar o arquivo, que será gravado na pasta indicada na propriedade ```dest```, com o nome que definirmos.

- É um código inválido.
- O Ansible baixará o arquivo da URL definida na propriedade url, gravando-o na pasta indicada na propriedade dest, com o mesmo nome do arquivo baixado.

2 - Temos o seguinte trecho de código do Playbook:

``` yml
- copy:
    src: '/var/www/wordpress/wp-config-sample.php'
    dist: '/var/www/wordpress/wp-config.php'
    remote_src: yes
  become: yes
```

Quantos erros há no trecho de código acima?

- Nenhum erro
- __1 erro__

> Alternativa correta! Há apenas um erro: a propriedade não é dist, é dest.

- 3 erros
- 2 erros

3 - Tendo como referência o handler abaixo para reiniciar o Apache2, podemos dizer:

``` yml
handlers:
  - name: restart apache
      name: apache2
      state: restarted
    become: yes
```

- Ele possui 3 erros.
- Ele possui 2 erros.
- __Ele possui 1 erro.__

> Alternativa correta! Ele possui um erro: faltou a declaração do serviço, através de service. O correto seria:
>
> ``` yml
> handlers:
>   - name: restart apache
>    service:
>       name: apache2
>       state: restarted
>     become: yes
> ```

- Ele está correto.

## Aula 6

1 - Segue uma parte do provisioning.yml com a configuração do handler que reinicia o Apache2:

``` yml
- hosts: wordpress
  handlers:
    - name: restart apache
      service:
        name: apache2
        state: restarted
      become: yes
...
```

Como garantimos que esse handler realmente será chamado após execução de uma tarefa?

- Handlers serão chamados automaticamente após a execução das tasks.

- __No final da task, usando:__

``` yml
notify:
  - restart apache
```

> Alternativa correta! Através do notify podemos "avisar" o handler.

- Criando uma task específica:

``` yml
tasks:
  - name: restart apache
```

2 - O Ansible nos permite executar comandos contra uma lista arbitrária de hosts remotos através do arquivo de inventário, que podem estar divididos em diferentes grupos. Dito isso, dado o arquivo de inventário abaixo, qual seria o retorno do comando ```ansible groupA -i hosts -m ping```?

``` txt
[groupA]
10.0.0.1
10.0.0.2

[groupB]
10.0.0.3
10.0.0.4

[groupC]
10.0.0.5
10.0.0.6
```

- A

``` yml
10.0.0.1 | SUCCESS => {
    "changed": false,
    "failed": false,
    "ping": "pong"
}
10.0.0.2 | SUCCESS => {
    "changed": false,
    "failed": false,
    "ping": "pong"
}
10.0.0.3 | SUCCESS => {
    "changed": false,
    "failed": false,
    "ping": "pong"
}
10.0.0.4 | SUCCESS => {
    "changed": false,
    "failed": false,
    "ping": "pong"
}
10.0.0.5 | SUCCESS => {
    "changed": false,
    "failed": false,
    "ping": "pong"
}
10.0.0.6 | SUCCESS => {
    "changed": false,
    "failed": false,
    "ping": "pong"
}
```

- B

``` yml
10.0.0.3 | SUCCESS => {
    "changed": false,
    "failed": false,
    "ping": "pong"
}
10.0.0.4 | SUCCESS => {
    "changed": false,
    "failed": false,
    "ping": "pong"
}
10.0.0.5 | SUCCESS => {
    "changed": false,
    "failed": false,
    "ping": "pong"
}
10.0.0.6 | SUCCESS => {
    "changed": false,
    "failed": false,
    "ping": "pong"
}
```

- __C__

``` yml
10.0.0.1 | SUCCESS => {
    "changed": false,
    "failed": false,
    "ping": "pong"
}

10.0.0.2 | SUCCESS => {
    "changed": false,
    "failed": false,
    "ping": "pong"
}
```

> Alternativa correta! O comando informado recebeu os seguintes parâmetros : ```<grupo> -i <inventário> -m <módulo>```.
> O grupo informado foi o groupA, que de acordo com o arquivo de inventário fornecido é formado pelos hosts 10.0.0.1 e 10.0.0.2. Dessa forma, quando rodamos o comando ansible informando o grupo groupA, o módulo solicitado será executado apenas contra os hosts desse grupo.
> Para maiores detalhes, você pode ler a documentação [aqui](https://docs.ansible.com/ansible/2.4/intro_patterns.html).

- D

``` yml
localhost | SUCCESS => {
    "changed": false,
    "failed": false,
    "ping": "pong"
}
```
