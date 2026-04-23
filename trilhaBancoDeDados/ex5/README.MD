
-- Banco de dados: `banco_de_dados`
--

-- --------------------------------------------------------

--
-- Estrutura para tabela `clientes`
--

CREATE TABLE `clientes` (
  `id_cliente` int(11) NOT NULL,
  `nome` varchar(100) DEFAULT NULL,
  `email` varchar(100) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Despejando dados para a tabela `clientes`
--

INSERT INTO `clientes` (`id_cliente`, `nome`, `email`) VALUES
(2, 'Maria', NULL),
(3, 'Pedro', NULL),
(4, 'Ana', NULL),
(5, 'Carlos', NULL),
(6, 'Fernanda', NULL),
(7, 'Lucas', NULL),
(8, 'Juliana', NULL),
(9, 'Rafael', NULL),
(10, 'Patricia', NULL),
(11, 'João', NULL),
(12, 'Maria', NULL);

-- --------------------------------------------------------

--
-- Estrutura para tabela `pedidos`
--

CREATE TABLE `pedidos` (
  `id_pedido` int(11) NOT NULL,
  `id_cliente` int(11) DEFAULT NULL,
  `valor_total` decimal(10,2) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Despejando dados para a tabela `pedidos`
--

INSERT INTO `pedidos` (`id_pedido`, `id_cliente`, `valor_total`) VALUES
(4, 3, 100.00),
(5, 3, 200.00),
(6, 2, 150.00),
(7, 3, 999.99);

-- --------------------------------------------------------

--
-- Estrutura para tabela `pedido_produto`
--

CREATE TABLE `pedido_produto` (
  `id_pedido` int(11) NOT NULL,
  `id_produto` int(11) NOT NULL,
  `quantidade` int(11) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Despejando dados para a tabela `pedido_produto`
--

INSERT INTO `pedido_produto` (`id_pedido`, `id_produto`, `quantidade`) VALUES
(4, 1, 1),
(5, 1, 1),
(6, 2, 2);

-- --------------------------------------------------------

--
-- Estrutura para tabela `perfil`
--

CREATE TABLE `perfil` (
  `id_perfil` int(11) NOT NULL,
  `id_cliente` int(11) DEFAULT NULL,
  `cpf` varchar(14) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Despejando dados para a tabela `perfil`
--

INSERT INTO `perfil` (`id_perfil`, `id_cliente`, `cpf`) VALUES
(3, 2, '222.222.222-22');

-- --------------------------------------------------------

--
-- Estrutura para tabela `produtos`
--

CREATE TABLE `produtos` (
  `id_produto` int(11) NOT NULL,
  `nome` varchar(100) NOT NULL,
  `preco` decimal(10,2) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Despejando dados para a tabela `produtos`
--

INSERT INTO `produtos` (`id_produto`, `nome`, `preco`) VALUES
(1, 'Pizza Calabresa', 50.00),
(2, 'Pizza Frango', 45.00),
(3, 'Refrigerante', 10.00),
(4, 'Suco', 8.00),
(5, 'Hamburguer', 25.00),
(6, 'Pizza', 50.00),
(7, 'Refrigerante', 10.00),
(8, 'Pizza', 50.00),
(9, 'Refrigerante', 10.00);

--
-- Índices para tabelas despejadas
--

--
-- Índices de tabela `clientes`
--
ALTER TABLE `clientes`
  ADD PRIMARY KEY (`id_cliente`);

--
-- Índices de tabela `pedidos`
--
ALTER TABLE `pedidos`
  ADD PRIMARY KEY (`id_pedido`),
  ADD KEY `id_cliente` (`id_cliente`);

--
-- Índices de tabela `pedido_produto`
--
ALTER TABLE `pedido_produto`
  ADD PRIMARY KEY (`id_pedido`,`id_produto`),
  ADD KEY `id_produto` (`id_produto`);

--
-- Índices de tabela `perfil`
--
ALTER TABLE `perfil`
  ADD PRIMARY KEY (`id_perfil`),
  ADD UNIQUE KEY `id_cliente` (`id_cliente`);

--
-- Índices de tabela `produtos`
--
ALTER TABLE `produtos`
  ADD PRIMARY KEY (`id_produto`);

--
-- AUTO_INCREMENT para tabelas despejadas
--

--
-- AUTO_INCREMENT de tabela `clientes`
--
ALTER TABLE `clientes`
  MODIFY `id_cliente` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=13;

--
-- AUTO_INCREMENT de tabela `pedidos`
--
ALTER TABLE `pedidos`
  MODIFY `id_pedido` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=8;

--
-- AUTO_INCREMENT de tabela `perfil`
--
ALTER TABLE `perfil`
  MODIFY `id_perfil` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=4;

--
-- AUTO_INCREMENT de tabela `produtos`
--
ALTER TABLE `produtos`
  MODIFY `id_produto` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=10;

--
-- Restrições para tabelas despejadas
--

--
-- Restrições para tabelas `pedidos`
--
ALTER TABLE `pedidos`
  ADD CONSTRAINT `pedidos_ibfk_1` FOREIGN KEY (`id_cliente`) REFERENCES `clientes` (`id_cliente`) ON DELETE CASCADE ON UPDATE CASCADE;

--
-- Restrições para tabelas `pedido_produto`
--
ALTER TABLE `pedido_produto`
  ADD CONSTRAINT `pedido_produto_ibfk_1` FOREIGN KEY (`id_pedido`) REFERENCES `pedidos` (`id_pedido`) ON DELETE CASCADE ON UPDATE CASCADE,
  ADD CONSTRAINT `pedido_produto_ibfk_2` FOREIGN KEY (`id_produto`) REFERENCES `produtos` (`id_produto`) ON DELETE CASCADE ON UPDATE CASCADE;

--
-- Restrições para tabelas `perfil`
--
ALTER TABLE `perfil`
  ADD CONSTRAINT `perfil_ibfk_1` FOREIGN KEY (`id_cliente`) REFERENCES `clientes` (`id_cliente`);
COMMIT;

COMANDOS 

SELECT clientes.nome, pedidos.valor_total FROM clientes INNER JOIN pedidos ON clientes.id_cliente = pedidos.id_cliente;
SELECT clientes.nome, pedidos.valor_total FROM clientes LEFT JOIN pedidos ON clientes.id_cliente = pedidos.id_cliente;
SELECT clientes.nome, pedidos.valor_total FROM clientes RIGHT JOIN pedidos ON clientes.id_cliente = pedidos.id_cliente;
SELECT clientes.nome, pedidos.valor_total FROM clientes LEFT JOIN pedidos ON clientes.id_cliente = pedidos.id_cliente UNION SELECT clientes.nome, pedidos.valor_total FROM clientes RIGHT JOIN pedidos ON clientes.id_cliente = pedidos.id_cliente;
SELECT nome FROM clientes WHERE id_cliente = ( SELECT id_cliente FROM pedidos WHERE valor_total = ( SELECT MAX(valor_total) FROM pedidos ) );
SELECT * FROM `pedidos`
SELECT * FROM `clientes`
SELECT * FROM `pedidos`
SELECT * FROM `pedido_produto`
SELECT * FROM `pedidos`
SELECT * FROM `clientes`
SELECT clientes.nome FROM clientes JOIN pedidos ON clientes.id_cliente = pedidos.id_cliente WHERE pedidos.valor_total = ( SELECT MAX(valor_total) FROM pedidos );
INSERT INTO pedidos (id_cliente, valor_total) SELECT clientes.id_cliente, 999.99 FROM clientes JOIN ( SELECT id_cliente FROM pedidos ORDER BY valor_total DESC LIMIT 1 ) AS maior_pedido ON clientes.id_cliente = maior_pedido.id_cliente;
SELECT * FROM `pedidos`
SELECT clientes.nome, ( SELECT SUM(pedidos.valor_total) FROM pedidos WHERE pedidos.id_cliente = clientes.id_cliente ) AS total_pedidos FROM clientes;
SELECT COUNT(*) AS total_pedidos FROM pedidos;
SELECT clientes.nome, SUM(pedidos.valor_total) AS total_vendido FROM clientes JOIN pedidos ON clientes.id_cliente = pedidos.id_cliente GROUP BY clientes.nome;
SELECT clientes.nome, SUM(pedidos.valor_total) AS total_vendido FROM clientes JOIN pedidos ON clientes.id_cliente = pedidos.id_cliente GROUP BY clientes.nome HAVING SUM(pedidos.valor_total) > 200;


parte teorica

Resposta 1:
INNER JOIN retorna apenas os registros que possuem correspondência nas duas tabelas. Exemplo: listar clientes que possuem pedidos.

Resposta 2:
LEFT JOIN traz todos os registros da tabela da esquerda e os relacionados da direita. RIGHT JOIN faz o contrário. Exemplo: LEFT mostra todos clientes mesmo sem pedido, RIGHT mostra todos pedidos mesmo sem cliente.

Resposta 3:
O FULL OUTER JOIN é feito usando UNION entre LEFT JOIN e RIGHT JOIN. Ele não é nativo no MySQL porque o banco não implementa diretamente esse tipo de junção.

Resposta 4:
Subconsulta simples é uma consulta dentro de outra. Exemplo: buscar o cliente com maior pedido usando SELECT dentro de outro SELECT.

Resposta 5:
Subconsulta simples roda independente. A correlacionada depende da consulta externa e executa para cada linha.

Resposta 6:
Funções de agregação fazem cálculos em vários dados. As mais usadas são COUNT, SUM, AVG, MAX e MIN.

Resposta 7:
GROUP BY agrupa dados iguais. É usado quando queremos fazer cálculos por grupo, como total por cliente.

Resposta 8:
HAVING filtra dados depois do GROUP BY. WHERE filtra antes.

Resposta 9:
Exemplo 1: total de vendas por cliente
Exemplo 2: quantidade de pedidos por produto

Resposta 10:
JOINs servem para relacionar tabelas. Eles evitam repetição de dados e deixam o banco mais organizado e eficiente