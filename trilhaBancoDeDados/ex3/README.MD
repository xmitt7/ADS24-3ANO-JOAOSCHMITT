 parte pratica
 Banco de dados: `banco_dados`
--

-- ------------------------------------------------------
-- Estrutura para tabela `funcionarios`

CREATE TABLE `funcionarios` (
  `id` int NOT NULL,
  `nome` varchar(100) NOT NULL,
  `email` varchar(100) NOT NULL,
  `cargo` varchar(100) NOT NULL,
  `cidade` varchar(100) DEFAULT 'não informado'
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

--
-- Despejando dados para a tabela `funcionarios`
--

INSERT INTO `funcionarios` (`id`, `nome`, `email`, `cargo`, `cidade`) VALUES
(1, 'João', 'joão@gmail.com', 'coordenador', 'não informado'),
(2, 'maria', 'mariadb@gmail.com', 'ajudante do bolsonario', 'não informado'),
(3, 'João Silva', 'joao.silva@email.com', 'Gerente', 'não informado'),
(4, 'Maria Souza', 'maria.souza@email.com', 'Vendedora', 'não informado'),
(6, 'Ana Costa', 'ana.costa@email.com', 'Assistente', 'não informado'),
(7, 'Lucas Pereira', 'lucas.pereira@email.com', 'Supervisor', 'não informado'),
(8, 'pedrao', 'pepeca@gmail.com', 'batedor de lage', 'não informado');

--
-- Índices para tabelas despejadas
--

--
-- Índices de tabela `funcionarios`
--
ALTER TABLE `funcionarios`
  ADD PRIMARY KEY (`id`);

--
-- AUTO_INCREMENT para tabelas despejadas
--

--
-- AUTO_INCREMENT de tabela `funcionarios`
--
ALTER TABLE `funcionarios`
  MODIFY `id` int NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=9;
COMMIT;

comandos:

SELECT * FROM `pedido`
SELECT * FROM `pedido_itens`
SELECT * FROM `funcionarios`
INSERT INTO `funcionarios`( `nome`, `email`, `cargo`) VALUES ('pedrao','pepeca@gmail.com','batedor de lage');
SELECT * FROM `funcionarios`
select * FROM funcionarios WHERE cargo = 'analista';
SELECT * FROM `funcionarios` ORDER BY nome ASC;
SELECT * FROM `funcionarios` ORDER BY nome ASC LIMIT 3;
SELECT DISTINCT cidade from funcionarios;
SELECT * FROM `funcionarios`
SELECT * FROM `funcionarios`
SELECT cargo, COUNT(*)AS total_cargos FROM funcionarios GROUP BY cargo;
UPDATE funcionarios SET cargo = 'coordenador' WHERE nome='joao';
SELECT * FROM `funcionarios`
DELETE FROM funcionarios where cargo = 'analista';
Expandir Repetir consulta Editar Demonstrar SQL Perfil Banco de dados : banco_dados Tempo de execução da consulta : 20:22:59
SELECT * FROM `funcionarios`
SELECT * FROM `funcionarios`
SELECT * FROM `funcionarios`
SELECT * FROM `funcionarios`

parte teorica 

Resposta 1:
O comando INSERT INTO é usado para inserir novos registros em uma tabela. Já o UPDATE é utilizado para alterar dados que já existem. O INSERT é usado quando você quer adicionar informações novas, enquanto o UPDATE é usado quando precisa corrigir ou modificar dados existentes.

Resposta 2:
O comando DELETE remove registros específicos de uma tabela, podendo usar condições com WHERE. Já o TRUNCATE apaga todos os dados da tabela de forma mais rápida, sem possibilidade de filtro. O DELETE é mais controlado, enquanto o TRUNCATE é mais bruto e limpa tudo.

Resposta 3:
A cláusula WHERE é importante porque define quais registros serão afetados. Sem ela, comandos como UPDATE e DELETE irão modificar ou apagar todos os dados da tabela, o que pode causar perda total de informações.

Resposta 4:
A cláusula ORDER BY serve para ordenar os resultados de uma consulta. Ela pode organizar os dados de forma crescente (ASC) ou decrescente (DESC), por exemplo, ordenar produtos pelo preço ou nome.

Resposta 5:
A palavra-chave DEFAULT define um valor padrão para uma coluna quando nenhum valor é informado na inserção. Exemplo: uma coluna cidade pode ter DEFAULT 'Não Informado', então se não for preenchida, esse valor será usado automaticamente.

Resposta 6:
A cláusula DISTINCT serve para retornar apenas valores únicos, eliminando duplicados. É útil quando você quer listar, por exemplo, apenas cidades diferentes cadastradas, sem repetir.

Resposta 7:
A cláusula GROUP BY agrupa registros que possuem valores iguais em uma ou mais colunas, geralmente usada com funções como COUNT, SUM, AVG. Exemplo: contar quantos pedidos cada cliente fez agrupando pelo nome do cliente.

Resposta 8:
Sem índices, o banco de dados precisa percorrer todos os registros da tabela para encontrar os dados (varredura completa), o que deixa as consultas mais lentas, principalmente em tabelas grandes.

Resposta 9:
Operadores de comparação:
= (igual) → verifica se dois valores são iguais

> (maior que) → verifica se um valor é maior que outro

Operadores lógicos:
AND = retorna verdadeiro se todas as condições forem verdadeiras
OR = retorna verdadeiro se pelo menos uma condição for verdadeira

Resposta 10:
A cláusula WHERE filtra dados antes do agrupamento, enquanto o HAVING filtra depois do GROUP BY. O HAVING é usado com GROUP BY porque permite aplicar condições em dados já agrupados, como filtrar grupos que tenham uma soma maior que determinado valor.
