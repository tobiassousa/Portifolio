### Tacsus
5° Semestre - 01/2024

Parceiro Acadêmico: Tecsus

## Empresa parceira

A Tecsus é uma startup que desenvolve dispositivos, aplicativos e sistemas para a transmissão e recepção de dados, controle de equipamentos remotos e gestão de faturas. Aplicados nos setores de abastecimento de água, distribuição de eletricidade e gás natural.


## 💻 Nossa proposta


A Tecsus realiza a coleta e processamento de contas de energia, água e gás para diversas empresas dos setores do atacado e varejo. Cada conta coletada precisa ter todos os seus campos digitados e salvos em banco de dados para eventuais consultas e análises técnicas/financeiras que podem trazer ao cliente oportunidades de redução de custos e alteração de contratos. Cada unidade do cliente pode possuir vários contratos (água, energia ou gás), cada contrato pode possuir uma ou mais contas (faturas de água, energia ou gás) por mês. Todos esses contratos estão ligados a uma concessionária de abastecimento. A Tecsus possuem uma base de dados de unidades, contratos, contas e concessionárias desestruturada em arquivo texto, a empresa tem interesse em aplicar técnicas de ETL e utilizar ferramentas de visualização de dados do mercado.


### Solução para o problema
Com isso sugerimos a criação de um sistema aonde possuí o acesso a todos esses dados facilmente e é possível inserir esses dados, juntamente com a criação de Dashboards pelos dados inseridos.

## Projeto:
https://github.com/Data-Team23/Tecsus


## Modelagem do Banco

### <p align="center">DER</p>
<p align="center"><img src="./modelo_logico_tecsus.png" widht="20%"></img>

## Contribuições Individuais
<details>
 <summary><b>Modelagem do Banco</b></summary>
  <br>
<p align="center"><img src="./modelo_logico_tecsus_energia.png" widht="20%"></img>
  <p>A modelagem foi utilizada por todo projeto para montar a estrutura do sistema</p>
  

<p>Foi necessario realizar a criação da modelagem seguindo o modelo estrela. Visto a proporção das planilhas e dados foi realizado um estudo encima dos dados para realizar o melhor relacionamento</p>
</details>

<details>
 <summary><b>Deploy</b></summary>
  <br>
<p>Foi realizado a estrutura do deploy antes da criação do código.</p>
<p align="center"><img src="./Deploy.png" widht="20%"></img>
<p align="center"><img src="./Deploy2.png" widht="20%"></img>

```java
name: Deploy Tecsus

on:
  pull_request:
    branches:
      - main
    types:
      - closed

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: 3.9

      - name: Log in to Docker Hub
        uses: docker/login-action@v2
        with:
            username: ${{ secrets.DOCKER_USERNAME }}
            password: ${{ secrets.DOCKER_PASSWORD }}
      
      - name: Build Docker Image
        run: docker build -t datateam23/tecsus-backend .
        working-directory: tecsus

      - name: Push Docker Image
        run: docker push datateam23/tecsus-backend
        working-directory: tecsus
       
       
  deploy:
          needs: build
          runs-on: self-hosted
          steps:
              - name: Pull image from docker hub
                run: sudo docker pull datateam23/tecsus-backend:latest
              - name: Remove docker container
                run: sudo docker rm -f tecsus-backend
              - name: Run docker container
                run: sudo docker run -d -p 8000:8000 -e DATABASE_USERNAME=${{secrets.DATABASE_USER}} -e DATABASE_PASSWORD='${{secrets.DATABASE_PASSWORD}}' -e DATABASE_URL=${{secrets.DATABASE_URL}} --name tecsus-backend  datateam23/tecsus-backend
```

<p>Foi realizado o código do deploy pensando na segurança, na agilidade de atualização e automoção.
O código coleta todas as alterações inseridas na main, realiza a criação da imagem docker e insere a imagem, após isso realiza as inserções dentro da VM inserida na AWS com a nova atualização do código. Para mantermos em segurança as chaves de acesso e usuario estão criptografados pelo git e assim utilizamos apenas um parametro para chamar essas chaves de acesso.</p>
</details>


## Tecnologias Utilizadas

- Python
- JavaScript
- Vue
- HTML
- CSS
- Oracle SQL
- AWS

## Lições Aprendidas

<p align="justify"></p>

<h3>Hard Skills</h3>
<details>
  <summary><b>Clique para ver a lista de hard skills</b></summary>
<p1>Desenvolvimento do modelo estrela: Aprendi a realizar a analise e compreender as relações necessarias para o modelo estrela</p1>

<p1>Deploy: Aprendi a realizar a criação do arquivo '.yml' o qual é utilizado para realizar a configuração do Deploy, aprendi também a configurar a maquina utilizada.</p1>

</details>
<h3>Soft Skills</h3>
<details>
  <summary><b>Clique para ver a lista de soft skills</b></summary>
<p1>Organização: Foi necessario organizar as tarefas e entregas pois tinhamos que coordenar as entregas do DevOps para gerar um fluxo.</p1>

<p1>Comunicação: Foi necessaria a comunicação para conseguir compreender melhor as tabelas encaminhadas para nós e também para organização das entregas.<p1>

</details>


## Meus Projetos
## Semestres

- [Semestre 1 - BETA](../Semestre01/Semestre01.md)
- [Semestre 2 - Pro4Tech](../Semestre02/Semestre02.md)
- [Semestre 3 - Dom Rock](../Semestre03/Semestre03.md)
- [Semestre 4 - Jaia](../Semestre04/Semestre04.md)
- [Semestre 6 - SPC Grafeno](../Semestre06/Semestre06.md)

