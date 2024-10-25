### Dom Rock
2° Semestre - 02/2022

Parceiro Acadêmico: Pro4Tech
<p align="center"><img src="./pro4tech-logo.png" widht="20%"></img>

## Empresa parceira

A Pro4tech é uma empresa que visa a transformação digital como um de seus pilares. Seu produto está voltado para criação de soluções digitais, ágeis e inovadoras por meio do desenvolvimento de pessoas. A empresa possui seu portifólio de serviços voltados para soluções em Aplicações Transacionais (Web/App), Aplicações Analíticas (BI/Analytics), Redesenho de Processos de Negócio, Inteligência Artificial (IA), Robotização de Processos (RPA) e Internet das Coisas (IoT).


## 💻 Nossa proposta

A Pro4tech está abrindo varias vagas para contratação de novos funcionários, com isso sentiu a necessidade de ter um software onde pudesse registrar e ter todo o controle das vagas que estão ofertando no mercado.

### Solução para o problema
A solução para essa demanda será a criação de um sistema desktop onde será possível cadastrar vagas, excluir vagas, editar vagas, cadastrar usuários, aplicação da vaga pelo usuário e extrair relatórios.

## Modelagem do Banco

<p align="center"><img src="./modelagem.jpg" widht="20%"></img>
<p align="center"><img src="./modelo-.png" widht="20%"></img>

## Contribuições Individuais
 
<details>
  <summary><b>TelaLogin: Interface de Login</b></summary>
  <br>
  <p>O código acima implementa a classe `TelaLogin`, que representa a interface de login do sistema. Aqui está uma explicação detalhada do que acontece no código:</p>
  
```java
package ClassesConexao;

import java.awt.EventQueue;

import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.border.EmptyBorder;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import java.awt.Font;
import javax.swing.JTextField;
import javax.swing.JPasswordField;
import javax.swing.JButton;
import java.awt.event.ActionListener;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.awt.event.ActionEvent;
import java.awt.Color;
import javax.swing.SwingConstants;
import javax.swing.ImageIcon;

public class TelaLogin extends JFrame {

    private static final long serialVersionUID = 1L;
    private JPanel contentPane;
    private JTextField tfUsuario;
    private JPasswordField pfSenha;
    private JButton btnCadastrar;
    private JButton btnEntrar;
    private JLabel lblAquiTemUma;
    private JLabel lblOlSejaBemvindo;
    private JLabel lblFaaSeuLogin_1;
    private JLabel lblNewLabel_1;

    public static void main(String[] args) {
        EventQueue.invokeLater(new Runnable() {
            public void run() {
                try {
                    TelaLogin frame = new TelaLogin();
                    frame.setVisible(true);
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        });
    }

    public TelaLogin() {
        btnEntrar = new JButton("ENTRAR");
        btnEntrar.setBackground(new Color(255, 140, 0));
        btnEntrar.setForeground(Color.BLACK);
        btnEntrar.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                try {
                    Connection con = Conexao.faz_conexao();
                    String sql = "select *from cadastro_usuario where email=? and senha= ?";
                    PreparedStatement stmt = con.prepareStatement(sql);
                    stmt.setString(1, tfUsuario.getText());
                    stmt.setString(2, new String(pfSenha.getPassword()));
                    ResultSet rs = stmt.executeQuery();
                    if (rs.next()) {
                        JOptionPane.showMessageDialog(null, "Entrando!");
                        Singleton.getInstance().nomeUsuario = rs.getString("nome");
                        Singleton.getInstance().cpfUsuario = rs.getString("cpf");
                        System.out.println(Singleton.getInstance().nomeUsuario);
                        TelaOpcoes exibir = new TelaOpcoes();
                        exibir.setVisible(true);
                        setVisible(false);
                    } else {
                        try {
                            String sql1 = "select * from cadastro_funcionario where email=? and senha= ?";
                            PreparedStatement stmt1 = con.prepareStatement(sql1);
                            stmt1.setString(1, tfUsuario.getText());
                            stmt1.setString(2, new String(pfSenha.getPassword()));
                            ResultSet rs1 = stmt1.executeQuery();
                            if (rs1.next()) {
                                JOptionPane.showMessageDialog(null, "Entrando!");
                                Singleton.getInstance().nomeFuncionario = rs1.getString("nome");
                                TelaOpcoesFuncionario exibir = new TelaOpcoesFuncionario();
                                exibir.setVisible(true);
                                setVisible(false);
                            } else {
                                try {
                                    String sql2 = "select * from cadastro_admin where email = ? and senha= ?";
                                    PreparedStatement stmt2 = con.prepareStatement(sql2);
                                    stmt2.setString(1, tfUsuario.getText());
                                    stmt2.setString(2, new String(pfSenha.getPassword()));
                                    ResultSet rs2 = stmt2.executeQuery();
                                    if (rs2.next()) {
                                        JOptionPane.showMessageDialog(null, "Entrando!");
                                        Singleton.getInstance().nomeFuncionario = "vitoria";
                                        TelaMenuRH exibir = new TelaMenuRH();
                                        exibir.setVisible(true);
                                        setVisible(false);
                                    } else {
                                        message.setText("E-mail ou senha incorreta!!");
                                    }
                                    stmt2.close();
                                    con.close();
                                } catch (Exception e2) {
                                    e2.printStackTrace();
                                }
                            }
                            stmt1.close();
                            con.close();
                        } catch (SQLException e1) {
                            e1.printStackTrace();
                        }
                    }
                    stmt.close();
                    con.close();
                } catch (SQLException e1) {
                    e1.printStackTrace();
                }
            }
        });

```
  <p>A classe `TelaLogin` representa a tela de login do sistema. Ela possui campos para inserção do e-mail e senha do usuário, botões para entrar e cadastrar, além de mensagens de erro e informações para orientar o usuário.</p>
</details>

<details>
 <summary><b>Tela Cadastro: Interface de Cadastro de Usuario</b></summary>
  <br>
  <p>O código implementa a classe `TelaCadastro', que representa a interface de cadastro de usuario. Aqui está uma explicação detalhada do que acontece no código:</p>
  
```java
       package ClassesConexao;

        import java.util.Date;

        import javax.swing.text.DefaultFormatterFactory;
        import javax.swing.text.MaskFormatter;

        public class CadastroUsuario<Interger> {
            private String email;
            private String senha;
            private String nome;
            private String cpf;
            private Date data_nasc;
            private String formaçao_acad;
            private String pretensao_salarial;
            private String cargo_interesse;
            private String experiencia_profissional;
            private String telefone;
            private String quemsoueu;
            private String cep;
            private String endereco;
            private String bairro;
            private String cidade;
            private String uf;
            private String numero;
            private static final String Formato = "###.###.###-##";
            
            public CadastroUsuario() {
            }
                
            public CadastroUsuario(String email, String senha, String nome, String cpf, Date data_nasc, String formaçao_acad, String pretensao_salarial,
                String cargo_interesse, String experiencia_profissional, String telefone, String quemsoueu, String cep, String endereco, String bairro, String cidade, String uf, String numero, Boolean isCPF) {
                this.email = email;
                this.senha = senha;
                this.nome = nome;
                this.cpf = cpf;
                this.data_nasc = data_nasc;
                this.formaçao_acad = formaçao_acad;
                this.pretensao_salarial = pretensao_salarial;
                this.cargo_interesse = cargo_interesse;
                this.experiencia_profissional = experiencia_profissional;
                this.telefone = telefone;
                this.quemsoueu = quemsoueu;
                this.cep = cep;
                this.endereco = endereco;
                this.bairro = bairro;
                this.cidade = cidade;
                this.uf = uf;
                this.numero = numero;
            }
                
            
            public String getEmail() {
                return email;
            }
            
            public void setEmail(String email) {
                this.email = email;
            }
            
            public String getSenha() {
                return senha;
            }
            
            public void setSenha(String senha) {
                this.senha = senha;
            }
            
            public String getNome() {
                return nome;
            }
            
            public void setNome(String nome) {
                this.nome = nome;
            }
            
            public String getCpf() {
                return cpf;
            }
            
            public void setCpf(String C) {
                this.cpf = this.Format(C, false);
            }
            
            public Date getData_nasc() {
                return data_nasc;
            }
            
            public void setData_nasc(Date data_nasc) {
                this.data_nasc = data_nasc;
            }
            
            public String getFormaçao_acad() {
                return formaçao_acad;
            }
            
            public void setFormaçao_acad(String formaçao_acad) {
                this.formaçao_acad = formaçao_acad;
            }
            
            public String getPretensao_salarial() {
                return pretensao_salarial;
            }
            
            public void setPretensao_salarial(String pretensao_salarial) {
                this.pretensao_salarial = pretensao_salarial;
            }
            
            public String getCargo_interesse() {
                return cargo_interesse;
            }
            
            public void setCargo_interesse(String cargo_interesse) {
                this.cargo_interesse = cargo_interesse;
            }
            
            public String getExperiencia_profissional() {
                return experiencia_profissional;
            }
            
            public void setExperiencia_profissional(String experiencia_profissional) {
                this.experiencia_profissional = experiencia_profissional;
            }
            
            public String getTelefone() {
                return this.telefone;
            }
            
            public void setTelefone(String telefone) {
                this.telefone = telefone;
            }
            public String getQuemsoueu() {
                return this.quemsoueu;
            }
            
            public void setQuemsoueu(String quemsoueu) {
                this.quemsoueu = quemsoueu;
            }
            public String getCep() {
                return this.cep;
            }
            
            public void setCep(String cep) {
                this.cep= cep;
            }
            public String getEndereco() {
                return this.endereco;
            }
            
            public void setEndereco(String endereco) {
                this.endereco = endereco;
            }
            public String getBairro() {
                return this.bairro;
            }
            
            public void setBairro(String bairro) {
                this.bairro = bairro;
            }
            public String getCidade() {
                return this.cidade;
            }
            
            public void setCidade(String cidade) {
                this.cidade = cidade;
            
            }
            public String getUf() {
                return this.uf;
            }
            
            public void setUf(String uf) {
                this.uf = uf;
            }
            public String getNumero() {
                return this.numero;
            }
            
            public void setNumero(String numero) {
                this.numero = numero;
            }

            
            public boolean isCPF(){
                    
                    if (this.cpf.equals("00000000000") || 
                        this.cpf.equals("11111111111") || 
                        this.cpf.equals("22222222222") || 
                        this.cpf.equals("33333333333") ||
                        this.cpf.equals("44444444444") ||
                        this.cpf.equals("55555555555") ||
                        this.cpf.equals("66666666666") ||
                        this.cpf.equals("77777777777") ||
                        this.cpf.equals("88888888888") ||
                        this.cpf.equals("99999999999") ||
                        this.cpf.length() != 11)
                        return(false);
                    
                    char dig10, dig11; 
                    int sm, i, r, num, peso; 
                    try { 
                        sm = 0; 
                        peso = 10; 
                        for (i=0; i<9; i++) { 
                            num = (int)(this.cpf.charAt(i) - 48); 
                            sm = sm + (num * peso); 
                            peso = peso - 1;
                        } 
                        r = 11 - (sm % 11); 
                        if ((r == 10) || (r == 11)) 
                            dig10 = '0'; 
                        else 
                            dig10 = (char)(r + 48); 
            
                        sm = 0; 
                        peso = 11; 
                        for(i=0; i<10; i++) { 
                            num = (int)(this.cpf.charAt(i) - 48);
                            sm = sm + (num * peso); 
                            peso = peso - 1;
                        } 
                        r = 11 - (sm % 11); 
                        if ((r == 10) || (r == 11)) 
                            dig11 = '0'; 
                        else 
                            dig11 = (char)(r + 48); 
            
                        if ((dig10 == this.cpf.charAt(9)) && (dig11 == this.cpf.charAt(10))) 
                            return(true); 
                        else return(false);
                    } catch(Exception e) { 
                        return(false); 
                    } 
                }
                
            private String Format(String C, boolean Mascara){
                    if(Mascara){
                        return(C.substring(0, 3) + "." + C.substring(3, 6) + "." +
                        C.substring(6, 9) + "-" + C.substring(9, 11));
                    }else{
                        C = C.replace(".","");
                        C = C.replace("-","");
                        return C;
                    }
                }
                
                
                public static DefaultFormatterFactory getFormat(){
                    try {
                        return new DefaultFormatterFactory(new MaskFormatter(Formato));
                    } catch (Exception e) {
                        return null;
                    }
                }
        }
```
<p>A classe 'TelaCadastro' representa a tela de cadastro de usuario. Ela possuí campos para inserção de dados do usuario, botoão para salvar os dados no campo e mascarás nos campos</p>
</details>


## Tecnologias Utilizadas
Java: Linguagem de programação utilizada para o desenvolvimento do sistema.

Java Swing: Biblioteca gráfica utilizada para criar a interface de usuário.

JDBC (Java Database Connectivity): API do Java para conexão e interação com bancos de dados relacionais.

MySQL: Sistema de gerenciamento de banco de dados relacional utilizado para armazenar informações sobre usuários e autenticação.

Figma: utilizado para o desenvolvimento e prototipação das wireframes.

## Lições Aprendidas

<p align="justify"></p>

<h3>Hard Skills</h3>
<details>
  <summary><b>Clique para ver a lista de hard skills</b></summary>
<p1>Desenvolvimento de Interface Gráfica: Aprendi a criar interfaces gráficas de usuário utilizando Java Swing, desenvolvendo habilidades em design de interfaces.</p1>

<p1>Conexão com Banco de Dados: Adquiri conhecimentos sobre conexão e manipulação de dados em um banco de dados MySQL utilizando JDBC.</p1>

</details>
<h3>Soft Skills</h3>
<details>
  <summary><b>Clique para ver a lista de soft skills</b></summary>
<p1>Resolução de Problemas: Enfrentou desafios relacionados à implementação de funcionalidades complexas e buscou soluções eficazes para problemas encontrados durante o desenvolvimento do sistema.</p1>

<p1>Trabalho em Equipe: Colaborou com outros membros da equipe no desenvolvimento do projeto, demonstrando habilidades de trabalho em equipe e colaboração para alcançar os objetivos do projeto.</p1>

</details>


## Meus Projetos
## Semestres

- [Semestre 3](../Semestre03/Semestre03.md)
- [Semestre 4](../Semestre04/Semestre04.md)
- [Semestre 5](../Semestre06/Semestre05.md)
- [Semestre 6](../Semestre05/Semestre06.md)