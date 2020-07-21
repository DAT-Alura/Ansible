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
