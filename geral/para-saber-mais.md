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
