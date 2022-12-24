> **Restrições (Constraints)**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @michelelozada
&nbsp;
     
&nbsp;     
**RESTRIÇÕES**    

* Regras ou condições que são vinculadas a uma coluna, a respeito dos valores que serão aceitos no banco de dados.
* P. ex.: valores que não podem se repetir, validações de dados inseridos, identificações de registros, etc.  
&nbsp;
     
&nbsp;      
**1 . PRIMARY KEY (aka Chave Primária)**  
Define o atributo (ou conjunto de atributos) que indentificará de forma única cada registro/linha de uma tabela de um banco de dados.  
* Só pode haver uma chave primária por tabela.
* Quando aplicada, não podem ocorer valores duplicados.
* Necessário ser declarada em conjunto com a cláusula `NOT NULL`, já que chaves primárias não podem receber valores nulos.
```mysql
CREATE TABLE tb_aluno(
    idAluno int(11) AUTO_INCREMENT NOT NULL,
    nomeAluno varchar(40),
    PRIMARY KEY (idAluno)
);
```
&nbsp;
     
&nbsp;    
**2. FOREIGN KEY (aka Chave Estrangeira)**  
Campo de uma tabela que aponta para o campo primário de uma outra tabela que contém a chave primária.  
* Imaginando uma tabela chamada Contrato, cujo campo idAluno estará vinculado ao campo primário da tabela Aluno, seria assim criada uma chave estrangeira:
```mysql
CREATE TABLE tb_contrato(
    idContrato int(11) PRIMARY KEY NOT NULL,
    idAluno_fk int(11),
    CONSTRAINT idAluno FOREIGN KEY (idAluno_fk) 
    REFERENCES tb_aluno(idAluno)
);
```
* Alteração para aplicar a chave estrangeira numa tabela já criada:
```mysql
ALTER TABLE tb_contrato 
ADD CONSTRAINT idAluno FOREIGN KEY (idAluno_fk) 
REFERENCES tb_aluno(idAluno);
```
* Exclusão de uma chave estrangeira:
```mysql
ALTER TABLE tb_contrato 
DROP CONSTRAINT idAluno;
```
&nbsp;
     
&nbsp;    
**3. UNIQUE**  
Define que valores em uma dada coluna não poderão se repetir.
```mysql
CREATE TABLE tb_aluno(
    idAluno int(11),
    cpfAluno varchar(15) UNIQUE
);
```	
&nbsp;
     
&nbsp;          
**4. NOT NULL**  
Define que não serão admitidos valores nulos/dados vazios na coluna (lembrando que o valor default é `NULL`).
```mysql
CREATE TABLE tb_aluno(
    idAluno int(11) AUTO_INCREMENT NOT NULL,
    nomeAluno varchar(40),
    PRIMARY KEY(idAluno)
);
```
* Caso a restrição não tenha sido definida no momento da criação da tabela:
```mysql
ALTER TABLE tb_aluno 
MODIFY nomeAluno varchar(40) NOT NULL;
```
* Caso seja necessária a reversão:
```mysql
ALTER TABLE tb_aluno 
MODIFY nomeAluno varchar(40) NULL;
```
&nbsp;
     
&nbsp;     
**5. DEFAULT**  
Define que - caso não seja especificado um valor pelo usuário - será associado um valor pré-definido à coluna a que se aplicou esta restrição.
```mysql
CREATE TABLE tb_aluno(
    idAluno int(11),
    cidadeAluno varchar(40) DEFAULT 'Curitiba',
    estadoAluno char(2) DEFAULT 'PR'
);
```
* Caso a restrição não tenha sido definida no momento da criação da tabela:
```mysql
ALTER TABLE tb_aluno 
ALTER cidadeAluno 
SET DEFAULT 'Curitiba';
```
&nbsp;
     
&nbsp;         
**6. CHECK**  
Define a validação dos dados inseridos em uma coluna, através da especificação de uma condição.  
Portanto: apenas dados, cujo resultado da avaliação da condição seja verdadeiro, serão aceitos.
```mysql
CREATE TABLE tb_aluno(
    idAluno int(11),
    idadeAluno int(2) NOT NULL CHECK(idadeAluno >= 0 AND idadeAluno <= 99)
);
```

&nbsp;    

<div align="center">
<a href="https://github.com/michelelozada/Banco-de-Dados-MySQL-Fundamentos">Voltar à tela inicial do repositório</a>
</div>