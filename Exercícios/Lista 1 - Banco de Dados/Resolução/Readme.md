# Resolução: Banco de Dados

**1 -**<br>
Resultado esperado:<br>
**Database → Schema → Tabelas e demais objetos**

**2 -** 
Resultado esperado:<br>
**a)**<br>
create table cadastros.tb_produto(<br>
id int not null primary key,<br>
descrição varchar(500) not null,<br>
preco_custo numeric(12,2),<br>
preco_venda numeric(12,2)<br>
);<br>
**b)**<br>
alter table cadastros.tb_produto add categoria varchar(100);<br>
**c)**<br>
drop table cadastros.tb_produto;

**3 -** <br>
Resultado esperado:<br>
**a)**<br>
insert into tb_produto<br>
(id, descrição, preco_custo, preco_venda)<br>
values<br>
(4, ‘mesa’, 149.00, 259.99);<br>
**b)**<br>
update tb_produto set preco_custo = 2249.00 where id = 3;<br>
**c)**<br>
delete from tb_produto Where preco_venda < 1000.00;

**4 -** <br>
Resultado esperado:<br>
A chave primária define o identificador único de cada tabela. Este identificador pode ser
simples (apenas uma coluna) ou composto (mais de uma coluna).

**5 -** <br>
Resultado esperado:<br>
*Create tablet b_cliente (<br>
codigo int not null,<br>
razao_social varchar(200),<br>
nome_fantasia varchar(200),<br>
numero_cnpj varchar(14),<br>
valor_capital_social numeric(12,2),<br>
primary key (código, numero_cnpj)<br>
);*

**6 -**<br>
Resultado esperado:<br>
*ALTER TABLE tb_contato<br>
ADD FOREIGN KEY (fornecedor_id)<br>
REFERENCES tb_fornecedor (codigo)<br>
ON UPDATE NO ACTION ON DELETE NO ACTION;*

**7 -** <br>
Resultado esperado:<br>
*select<br>
a.codigo, a.razao_social, count(*)<br>
from tb_fornecedor a<br>
join tb_contato b on (a.codigo = b.fornecedor_id)<br>
group by a.codigo, a.razao_social;*

**8 -** <br>
Resultado esperado:<br>
*select<br>
a.codigo, a.razao_social, b.id<br>
from tb_fornecedor a<br>
left join tb_contato b on (a.codigo = b.fornecedor_id)<br>
where b.id IS NULL;*

**9 -** <br>
Resultado esperado:<br>
*create table tb_dados_cadastro(<br>
codigo int8 generated always as identity primary key,<br>
nome_completo varchar(50),<br>
data_nascimento date,<br>
possui_filhos varchar(1) default 'N'<br>
);<br>
insert into tb_dados_cadastro<br>
(nome_completo, data_nascimento, possui_filhos)<br>
values<br>
('João da Silva', '1985-05-06', 'N'),<br>
('Maria Maria', '1990-05-08', 'S'),<br>
('Antonio Santos', '2000-10-29', 'N'),<br>
('Antonio Santos Jr', '2007-01-31', 'N'),<br>
('André Silva', '1970-10-29', 'N');<br>
delete from tb_dados_cadastro where codigo = 3;<br>
drop table tb_dados_cadastro;*

**10 -** <br><br>

**11 -** <br>
Resultado esperado:<br>
Normalização é a aplicação de regras em todas as tabelas do banco de dados, com o
objetivo a diminuição de falhas no projeto.<br>
1ª Forma Normal: Todos os atributos de uma tabela devem ser atômicos;<br>
2ª Forma Normal: Todos os atributos não chaves de uma tabela devem depender
unicamente da chave da tabela.<br>
3ª Forma Normal: Atributos não chave de uma tabela deve ser mutuamente independente
e dependentes unicamente e exclusivamente da chave primária.

**12 -** <br>
Resultado esperado:<br>
*select<br>
b.id_produto, c.descricao, SUM(b.quantidade)<br>
from tb_nota_fiscal a<br>
join tb_nota_fiscal_item b on (a.numero = b.id_nota_fiscal)<br>
join tb_produto c on (b.id_produto = [c.id](http://c.id/))<br>
where data_emissao >= '2017-01-01'<br>
group by b.id_produto, c.descricao<br>
order by SUM(b.quantidade)*

**13 -** <br>
Resultado esperado:<br>
*select<br>
a.numero, a.data_emissao, d.razao_social, b.id_produto,<br>
c.descricao, b.valor_unitario, b.quantidade,<br>
(b.quantidade * b.valor_unitario) as valor_total<br>
from tb_nota_fiscal a<br>
join tb_nota_fiscal_item b on (a.numero = b.id_nota_fiscal)<br>
join tb_produto c on (b.id_produto = c.id)<br>
join tb_cliente d on (a.id_cliente = d.id)<br>
where c.descricao = 'escritorio';*

**14 -** <br>
Resultado esperado:<br>
O comando não será executado com sucesso, uma vez que existe chave estrangeira
ligando as duas tabelas, é preciso deletar todos os registros “filhos” antes de deletar o
registro “pai”

**15 -** <br>
Resultado esperado:<br>
*select*<br>
*d.id, d.razao_social, d.nome_fantasia,<br>
AVG(b.quantidade * b.valor_unitario) as valor_total<br>
from tb_nota_fiscal a<br>
join tb_nota_fiscal_item b on (a.numero = b.id_nota_fiscal)<br>
join tb_produto c on (b.id_produto = c.id)<br>
join tb_cliente d on (a.id_cliente = d.id)<br>
group by d.id, d.razao_social, d.nome_fantasia;*
