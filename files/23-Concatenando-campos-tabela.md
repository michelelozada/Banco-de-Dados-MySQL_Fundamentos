> **Concatenando campos de uma tabela (função CONCAT)**    
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @michelelozada
&nbsp;
     
&nbsp;   
**FUNÇÃO CONCAT**  
* Concatena strings de campos diferentes da tabela, através de uma mesma query.
&nbsp;
     
&nbsp;
**A tabela para o exemplo:**   
| idCliente | nomeCliente | sobrenomeCliente | scoreCliente |
| :---      | :---	      | :---	         | :---         |
| 1         | Luana	      | Borba	         | 300          |
| 2	        | Mariana	  | Fernandes        | 710          |
| 3	        | Cátia	      | Marcondes	     | NULL         |
| 4	        | Marcos	  | Góes	         | NULL         |
| 5	        | Enzo	      | Marques	         | 500          |
| 6	        | Carla	      | Santana	         | 800          |
| 7	        | Sandra	  | de Paula	     | NULL         |
| 8	        | Paulo	      | Figueiredo       | NULL         |
| 9	        | Larissa	  | Torres	         | 520          |
| 10        | Vinícius    | Motta	         | NULL         |

&nbsp;

&nbsp;
**1. Utilizando a função CONCAT:**  
```mysql
SELECT CONCAT(nomeCliente, ' ',sobrenomeCliente) AS 'Nome do Cliente'
FROM tb_cliente
ORDER BY nomeCliente;
```
###### * Output:  

| Nome do Cliente   |
| :---              |
| Carla Santana     |
| Cátia Marcondes   |
| Enzo Marques      |
| Larissa Torres    |
| Luana Borba       |
| Marcos Góes       |
| Mariana Fernandes |
| Paulo Figueiredo  |
| Sandra de Paula   |
| Vinícius Motta    |

&nbsp;
&nbsp;  
**Nova consulta:**  
```mysql
SELECT CONCAT('Score do(a) cliente ', nomeCliente, ' ', sobrenomeCliente, ': ', scoreCliente, ' pontos') AS  'Consulta sobre clientes'
FROM tb_cliente
WHERE idCliente = '2';
```
###### * Output:  
| Consulta sobre clientes                            |
| :---                                               |
| Score do(a) cliente Mariana Fernandes: 710 pontos. |

&nbsp;
&nbsp;  
**Agora repare o que acontece ao se fazer a consulta à um registro que contém valor nulo:**  
```mysql
SELECT CONCAT('Score do(a) cliente ', nomeCliente, ' ', sobrenomeCliente, ': ', scoreCliente, ' pontos') AS  'Consulta sobre clientes'
FROM tb_cliente
WHERE idCliente = '10';
```
###### * Output:  
| Consulta sobre clientes |
| :---                    |
| NULL 					  |	

&nbsp;
&nbsp;  
**2. Utilizando a função IFNULL:**  
- Strings concatenadas com campos que contém valores nulos não serão exibidas: será apenas retornada linha com valor NULL, como visto acima.    
- Portanto, para evitar isto, deve-se utilizar a função `IFNULL`, que contém 2 argumentos: 
	- no primeiro argumento, é colocado o campo a ser concatenado (que pode ter valor NULL); 
	- e no segundo argumento, coloca-se a mensagem que se deseja que substitua o termo NULL, quando houver. 
```mysql
SELECT CONCAT('Score do(a) cliente ', nomeCliente, ' ', sobrenomeCliente, ': ', IFNULL(scoreCliente,'ainda não computado'),'.') AS  'Consulta sobre clientes'
FROM tb_cliente
WHERE idCliente = '10';
```
###### * Output:  
| Consulta sobre clientes 									|
| :---                    									|
| Score do(a) cliente Vinícius Motta: ainda não computado.  |