> **Alterando nome de tabelas e colunas existentes (comando RENAME)**  
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @michelelozada
&nbsp;
     
&nbsp;  
**RENAME**  
Para renomear tabelas ou colunas já existentes no banco de dados.
&nbsp;
     
&nbsp;   
**1 – Renomeando tabelas**  
```mysql
ALTER TABLE tb_alunos -- aqui o nome da tabela a ser alterado
RENAME Alunos; -- aqui o novo nome da tabela  
```
Ou alternativamente:
```mysql
RENAME TABLE tb_aluno TO Alunos;
```
Para alterar vários nomes de tabelas ao mesmo tempo:
```mysql
RENAME TABLE 
	tb_alunos TO Alunos, 
	tb_professores TO Professores, 
	tb_departamentos TO Departamentos; 
```
&nbsp;
     
&nbsp;  
**2 – Renomeando colunas**  
```mysql
ALTER TABLE tb_alunos 
RENAME COLUMN nomeAluno TO nome_aluno; 
-- antes, o nome da coluna a ser alterado; depois o novo nome da coluna
```
Ou alternativamente:
```mysql 
ALTER TABLE tb_alunos
CHANGE nomeAluno nome varchar(50);
```

&nbsp;

<div align="center">
<a href="https://github.com/michelelozada/Banco-de-Dados-MySQL-Fundamentos">[Voltar à tela inicial do repositório]</a>
</div>