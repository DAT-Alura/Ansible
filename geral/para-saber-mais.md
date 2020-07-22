# Para saber mais

## Novo Loop

Na aula aprendemos como definir varias dependências no playbook através ```{{ item }}``` e ```with_items```.

Exemplo com ```with_items```:

``` yml
- name: 'Instala pacotes do sistema operacional'
  apt:
    name: '{{ item }}'
    state: latest
  become: yes
  with_items:
    - php5
    - apache2
    - libapache2-mod-php5
```

As versões mais recentes do Ansible descontinuaram (_deprecated_) essa forma de laço a favor de um nova sintaxe mais enxuta.

Abaixo o exemplo do mesmo laço mas agora listando os pacotes pelo ```name```:

``` yml
    - name: 'Instala pacotes do sistema operacional'
      apt:
        name:
        - php5
        - apache2
        - libapache2-mod-php5
        state: latest
      become: yes
```

Fique a vontade de testar a nova forma.

## Variáveis

Existem algumas regras que devemos considerar na hora de declarar uma varíavel (como em qualquer outra ferramenta ou linguagem de programação). Por exemplo, uma variável não deve ter um ponto, espaço ou hífen no nome. Todas as declarações abaixo são inválidas:

``` yml
foo-var: 'nao_pode_ter_hifen'
foo var: 'nem_ter_espaco'
foo.var: 'tambem_nao_pode_ter_ponto'
12foovar: 'nao_pode_ter_numero_no_inicio'
```

Todos os detalhes sobre as declarações e muito mais se encontra da documentação do Ansible: [Documentação sobre Variáveis](https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#what-makes-a-valid-variable-name).

## Jinja

No curso você já aprendeu como usar templates e qual é a sintaxe para declarar uma variável. Para trabalhar com os templates, o Ansible usa um outro framework que se chama Jinja.

Ele faz parte dos template engine's (ou template processor). Um template engine combina um template (HTML, XML, ou qualquer outro arquivo, configurações etc) com um modelo de dados para gerar um novo documento: [Template Engine Jinja](http://jinja.pocoo.org/).

Isso é muito utilizado no desenvolvimento web para gerar páginas HTML dinamicamente. Por isso o Jinja é o template engine padrão do Flask, um micro framework web também escrito em Python: [Python Flask Web Framework](https://flask.palletsprojects.com/en/1.1.x/)

Se tiver interessado em aprender Flask, na Alura também temos cursos dedicados. Vale conferir: [Cursos Flask na Alura](https://cursos.alura.com.br/search?query=flask).
