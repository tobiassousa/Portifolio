### Jaia
4° Semestre - 02/2023

Parceiro Acadêmico: Jaia

## 💻 Nossa proposta

Jaia Software Em um cenário onde a paisagem urbana se compõe de uma mistura de edifícios modernos e históricos, a empresa Jaia, apresentou um desafio significativo. A condução de inspeções prediais estava provando ser uma tarefa morosa e suscetível a imprecisões. Diante desse cenário, a Jaia buscou soluções inovadoras para otimizar esse processo crucial. A visão estratégica da empresa contemplou o desenvolvimento de um software de inspeção predial, projetado para revolucionar a abordagem atual. A plataforma concebida promete oferecer uma experiência intuitiva, capacitando os inspetores a documentar minuciosamente detalhes relevantes e capturar evidências visuais de forma eficaz. Adicionalmente, a geração instantânea de relatórios abastecerá a tomada de decisões embasadas. A Jaia, reconhecendo a necessidade de aprimorar a qualidade e eficiência das inspeções, direcionou seus esforços para o desenvolvimento desse software inovador. O resultado obtido transcendeu as expectativas iniciais, beneficiando não somente a empresa, mas também elevando o padrão das inspeções prediais na esfera urbana, contribuindo, assim, para uma maior segurança e excelência nas estruturas urbanas.


## Projeto:
https://github.com/Data-Team23/Jaia



## Contribuições Individuais
<details>
<summary><b>Modelagem: Realização da modelagem de dados</b></summary>
<br>
<p>Realizei a modelagem e a criação das tabelas, foi necessario realizar a criação das tabelas com a necessidade do cliente pois não possuíamos uma base pronta.
Com isso foi necessario entender o produto e já realizar uma analise de quais tabelas seriam necessarias.</p>

### <p align="center">DER</p>
<p align="center"><img src="./model-der.png" widht="30%"></img>

### <p align="center">Mer</p>
<p align="center"><img src="./model-mer.png" widht="20%"></img>
</details>

<details>
<summary><b>AuthController: Controle de Autenticação</b></summary>
<br>
<p>Realizei a criação do envio de emails para o cliente, foi necessario realizar a criação do corpo do email e também da logica para realizar o envio do email quando a ordem do serviço for registrada.</p>

```java
package com.dataTeam.jaia.jaia.service.Email;

import java.security.SecureRandom;
import java.time.LocalDateTime;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.mail.javamail.JavaMailSender;
import org.springframework.mail.javamail.MimeMessageHelper;
import org.springframework.stereotype.Service;

import com.dataTeam.jaia.jaia.model.Checklist;
import com.dataTeam.jaia.jaia.model.Cliente;
import com.dataTeam.jaia.jaia.model.Funcionario;
import com.dataTeam.jaia.jaia.model.OrdemServico;
import com.dataTeam.jaia.jaia.model.Requisicao;
import com.dataTeam.jaia.jaia.repository.ClienteRepository;

import jakarta.mail.MessagingException;
 private String generateRandomPassword(int length) {

    return password.toString();
    }



    public void enviarOrdemServico(OrdemServico ordemServico, Requisicao requisicao, Cliente cliente, Funcionario funcionario, Checklist checklist, String assunto) throws MessagingException {


        MimeMessage mail = mailSender.createMimeMessage();

        MimeMessageHelper mensagem = new MimeMessageHelper(mail, true);
        mensagem.setSubject(assunto);
        mensagem.setTo(cliente.getEmail());
        mensagem.setFrom(supportMail);

        String conteudoDoEmail = getContentMailCertificate(ordemServico , requisicao, cliente, funcionario, checklist );

        mensagem.setText(conteudoDoEmail, true);

        mailSender.send(mail);


    }

    public String getContentMailCertificate(OrdemServico ordemServico, Requisicao requisicao, Cliente cliente, Funcionario funcionario, Checklist checklist) {
    String nomecli = cliente.getNome();    
    String nomeOrdem = ordemServico.getNome_ordem();
    String statusOrdem = ordemServico.getStatus_ordem();
    LocalDateTime dataAbertura = requisicao.getData_abertura();
    String descricao = requisicao.getDescricao();
    String cnpj = cliente.getCnpj();
    String inspecao = ordemServico.getTipo_inspecao();
    Funcionario responsasvel = funcionario.getSupervisor();
    String checklistname = checklist.getNome();

        // Customize the email content based on the data from OrdemServico
        String content = "<p>Olá, " + nomecli + "! Bem-vindo(a) ao Predial!</p>" +
                    "<p>&nbsp;</p>" +
                    "<p>Sua Ordem de Seriço está disponível abaixo:<br /></p>" +
                    "<p>Nome: " + nomeOrdem + "Status da Requisição:" +"</p>" +
                    "<p>Data da Abertura: " + dataAbertura + "Descrição:" + descricao + "</p>" +
                    "<p>CNPJ:" + cnpj + "Status da Ordem de Seriço:" + statusOrdem + "</p>"+
                    "<p>Inspeção:" + inspecao + "Responsável" + responsasvel +  "</p>" +
                    "<p>Data da Prestação do Serviço:"  + "Checklist:" + checklistname + "</p>"+
                    "<p>*Não responda este E-mail*</p>";

        return content;

    } 

}
```
<p>O código realiza a verificação da etapa da ordem e após a ordem chamar a função de 'enviarOrdemServico' ele irá pegar as informações do cliente e irá montar o email para realizar o envio.</p>
</details>


## Tecnologias Utilizadas
Spring Boot: Framework utilizado para desenvolver o Back-End do software.

Vue.js: Framework JavaScript utilizado para construir a interface interativa da página.

Oracle SQL: Sistema de gerenciamento de banco de dados relacional utilizado para armazenar informações sobre usuários e autenticação.

## Lições Aprendidas

<p align="justify"></p>

<h3>Hard Skills</h3>
<details>
  <p1>Oracle Sql: Foi necessario buscar o conhesimento sobre o Oracle SQL o qual foi disponibilizado uma chave para nós do PL/SQL com isso aprendi a realizar a conexão do banco de dados na nuvem com o nosso códgio.</p1>


  <p1>Java: Utilizei o Java para criar as funções e requisiçõs da tela de envio de email, e foi necessario compreender como os emails aceitavam o acesso de um codigo externo a eles.</p1>
</details>

<h3>Soft Skills</h3>
<details>
  <p1>Trabalho em Equipe: Foi necessario trabalhar com os colegas para compreender o sistema e entender o produto. Com isso tive auxilio para montar a modelagem.</p1>


  <p1>Organização: Aprendi a realizar a organização de tarefas pessoais e tarefas corporativas para conseguir entregar todas as tarefas a tempo.</p1>
</details>

## Meus Projetos
## Semestres

- [Semestre 1 - BETA](./Semestre01/Semestre01.md)
- [Semestre 2 - Pro4Tech](./Semestre02/Semestre02.md)
- [Semestre 3 - Dom Rock](./Semestre03/Semestre03.md)
- [Semestre 5 - Tecsus](./Semestre05/Semestre05.md)
- [Semestre 6 - SPC Grafeno](./Semestre06/Semestre06.md)
