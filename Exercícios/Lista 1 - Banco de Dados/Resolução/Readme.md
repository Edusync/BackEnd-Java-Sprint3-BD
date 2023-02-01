# Resolução: Banco de Dados

1 -
Resultado esperado:
**Database → Schema → Tabelas e demais objetos**

2 - 

Resultado esperado:
**a)**
create table cadastros.tb_produto(
id int not null primary key,
descrição varchar(500) not null,
preco_custo numeric(12,2),
preco_venda numeric(12,2)
);
**b)**
alter table cadastros.tb_produto add categoria varchar(100);
**c)**
drop table cadastros.tb_produto;

3 - 

Resultado esperado:
**a)**
insert into tb_produto
(id, descrição, preco_custo, preco_venda)
values
(4, ‘mesa’, 149.00, 259.99);
**b)**
update tb_produto set preco_custo = 2249.00 where id = 3;
**c)**
delete from tb_produto Where preco_venda < 1000.00;

4 - 
Resultado esperado:
A chave primária define o identificador único de cada tabela. Este identificador pode ser
simples (apenas uma coluna) ou composto (mais de uma coluna).

5 - 

Resultado esperado:
*Create tablet b_cliente (
codigo int not null,
razao_social varchar(200),
nome_fantasia varchar(200),
numero_cnpj varchar(14),
valor_capital_social numeric(12,2),
primary key (código, numero_cnpj)
);*

6 - 

Resultado esperado:
*ALTER TABLE tb_contato
ADD FOREIGN KEY (fornecedor_id)
REFERENCES tb_fornecedor (codigo)
ON UPDATE NO ACTION ON DELETE NO ACTION;*

7 - 

Resultado esperado:
*select
a.codigo, a.razao_social, count(*)
from tb_fornecedor a
join tb_contato b on (a.codigo = b.fornecedor_id)
group by a.codigo, a.razao_social;*

8 - 
Resultado esperado:
*select
a.codigo, a.razao_social, b.id
from tb_fornecedor a
left join tb_contato b on (a.codigo = b.fornecedor_id)
where b.id IS NULL;*

9 - 

Resultado esperado:
*create table tb_dados_cadastro(
codigo int8 generated always as identity primary key,
nome_completo varchar(50),
data_nascimento date,
possui_filhos varchar(1) default 'N'
);
insert into tb_dados_cadastro
(nome_completo, data_nascimento, possui_filhos)
values
('João da Silva', '1985-05-06', 'N'),
('Maria Maria', '1990-05-08', 'S'),
('Antonio Santos', '2000-10-29', 'N'),
('Antonio Santos Jr', '2007-01-31', 'N'),
('André Silva', '1970-10-29', 'N');
delete from tb_dados_cadastro where codigo = 3;
drop table tb_dados_cadastro;*

10 - 

11 - 
Resultado esperado:
Normalização é a aplicação de regras em todas as tabelas do banco de dados, com o
objetivo a diminuição de falhas no projeto.
1ª Forma Normal: Todos os atributos de uma tabela devem ser atômicos;
2ª Forma Normal: Todos os atributos não chaves de uma tabela devem depender
unicamente da chave da tabela.
3ª Forma Normal: Atributos não chave de uma tabela deve ser mutuamente independente
e dependentes unicamente e exclusivamente da chave primária.

12 - 

Resultado esperado:
*select
b.id_produto, c.descricao, SUM(b.quantidade)
from tb_nota_fiscal a
join tb_nota_fiscal_item b on (a.numero = b.id_nota_fiscal)
join tb_produto c on (b.id_produto = [c.id](http://c.id/))
where data_emissao >= '2017-01-01'
group by b.id_produto, c.descricao
order by SUM(b.quantidade)*

13 - 

Resultado esperado:
*select
a.numero, a.data_emissao, d.razao_social, b.id_produto,
c.descricao, b.valor_unitario, b.quantidade,
(b.quantidade * b.valor_unitario) as valor_total
from tb_nota_fiscal a
join tb_nota_fiscal_item b on (a.numero = b.id_nota_fiscal)
join tb_produto c on (b.id_produto = c.id)
join tb_cliente d on (a.id_cliente = d.id)
where c.descricao = 'escritorio';*

14 - 

Resultado esperado:
O comando não será executado com sucesso, uma vez que existe chave estrangeira
ligando as duas tabelas, é preciso deletar todos os registros “filhos” antes de deletar o
registro “pai”

15 - 

Resultado esperado:
*select*
*d.id, d.razao_social, d.nome_fantasia,
AVG(b.quantidade * b.valor_unitario) as valor_total
from tb_nota_fiscal a
join tb_nota_fiscal_item b on (a.numero = b.id_nota_fiscal)
join tb_produto c on (b.id_produto = c.id)
join tb_cliente d on (a.id_cliente = d.id)
group by d.id, d.razao_social, d.nome_fantasia;*