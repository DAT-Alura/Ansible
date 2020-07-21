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
