# Projeto MariaDB – AWS

**Recursos utilizados na aplicação:**

1. Placa CPU EMBFLEX ESP32;
2. Máquina virtual EC2 - aws;
3. Mqtt Broker instalado na EC2;
4. Técnica de link de broker IoT com DB;

### Banco de dados MariaDB:

Para a criação de um banco de dados MariaDB em cloud, deve-se primeiro ter uma conta em um cloud web servisse, nesse caso foi utilizado a AWS.
Como o MariaDB é um banco de dados relacional, foi utilizado o serviço RDS da AWS, especializado em banco de dados relacionais, dentro desse serviço são determinadas configurações como, nome do banco de dados, VPC, security groups que determina permissão e negação de acessos externos, pode ser configurado uma role IAM (conjunto de regras, grupos, usuários e politicas para a própria segurança do banco, segurança interna), memória do banco, acesso público e backup dos dados. Para esse banco em fase de testes, foram configurados:

- Storage: 20GiB;
- Security groups:
- Type | port range | Source
- SSH | 22 | 0.0.0.0/0
- Mysql | 5432 | sg-046c41689d9e6969a - launch-wizard-1
- Mysql | 5432 | MyIP
- Zona: North Virginia (pode ser usada qualquer uma);
- VPC: padrão;
- Public accessibility: sim;
- Class: db.t3.micro;
- vCPU: 2;
- RAM: 1GB;

A aplicação é similar a do PostgreSQL, o modo de criação e as configurações são as mesmas, o diferencial está no banco em si e na manipulação dos dados.

## Acessando o banco e criando tabelas

- Primeiro instale o xampp de 'start' em MySQL
- Abra o shell e digite:

```js
mysql -u root -p -h (ip do banco)
```

O processo de criação do banco é bem parecido com o PostgreSQL

```js
CREATE DATABASE mqtt;
```

```js
USE mqtt;
```

Ao entrar no banco digite:

```js
CREATE TABLE temperature(
id INT primary key AUTO_INCREMENT,
temp FLOAT(4,2),
dh TIMESTAMP);
```

A tabela foi criada!

## Conclusão da pesquisa MariaDB

Essa foi a primeira pesquisa de banco para armzenar dados IoT realizada, nessa pesquisa foi constatado a eficiência do banco, facilidade de criação e implementação em nuvem e utilização de banco de dados raclacionais.
Ao fazer a conexão do MQTT Broker, através de um código de ligação, com o banco de dados MariaDB a fase final de testes foi bem sucedida.

## Referências bibliográficas

[https://aws.amazon.com/pt/rds/mariadb/](https://aws.amazon.com/pt/rds/mariadb/)  
[https://docs.aws.amazon.com/pt_br/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.MariaDB.html](https://docs.aws.amazon.com/pt_br/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.MariaDB.html)
