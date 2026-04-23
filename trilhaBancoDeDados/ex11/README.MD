
-- Banco de dados: `loja`
--

-- --------------------------------------------------------

--
-- Estrutura para tabela `clientes`
--

CREATE TABLE `clientes` (
  `id_cliente` int(11) NOT NULL,
  `nome` varchar(100) NOT NULL,
  `email` varchar(100) DEFAULT NULL,
  `telefone` varchar(20) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- --------------------------------------------------------

--
-- Estrutura para tabela `pedidos`
--

CREATE TABLE `pedidos` (
  `id_pedido` int(11) NOT NULL,
  `id_cliente` int(11) NOT NULL,
  `data_pedido` date DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- --------------------------------------------------------

--
-- Estrutura para tabela `pedido_produto`
--

CREATE TABLE `pedido_produto` (
  `id_pedido` int(11) NOT NULL,
  `id_produto` int(11) NOT NULL,
  `quantidade` int(11) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- --------------------------------------------------------

--
-- Estrutura para tabela `produtos`
--

CREATE TABLE `produtos` (
  `id_produto` int(11) NOT NULL,
  `nome` varchar(100) NOT NULL,
  `preco` decimal(10,2) NOT NULL,
  `estoque` int(11) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

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
  ADD KEY `idx_cliente` (`id_cliente`);

--
-- Índices de tabela `pedido_produto`
--
ALTER TABLE `pedido_produto`
  ADD PRIMARY KEY (`id_pedido`,`id_produto`),
  ADD KEY `idx_produto` (`id_produto`),
  ADD KEY `idx_pedido` (`id_pedido`);

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
  MODIFY `id_cliente` int(11) NOT NULL AUTO_INCREMENT;

--
-- AUTO_INCREMENT de tabela `pedidos`
--
ALTER TABLE `pedidos`
  MODIFY `id_pedido` int(11) NOT NULL AUTO_INCREMENT;

--
-- AUTO_INCREMENT de tabela `produtos`
--
ALTER TABLE `produtos`
  MODIFY `id_produto` int(11) NOT NULL AUTO_INCREMENT;

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
  ADD CONSTRAINT `pedido_produto_ibfk_2` FOREIGN KEY (`id_produto`) REFERENCES `produtos` (`id_produto`) ON UPDATE CASCADE;
COMMIT;

comandos 

SELECT * FROM `pedidos`
Expandir Repetir consulta Editar Banco de dados : Tempo de execução da consulta : 16:5:45
INSERT INTO pedido_produto (id_pedido, id_produto, quantidade) VALUES (1, 1, 2), (1, 3, 2), (2, 2, 1);
SELECT * FROM `pedidos`
drop database loja;
CREATE TABLE pedido_produto ( id_pedido INT, id_produto INT, quantidade INT NOT NULL, PRIMARY KEY (id_pedido, id_produto), FOREIGN KEY (id_pedido) REFERENCES pedidos(id_pedido) ON DELETE CASCADE ON UPDATE CASCADE, FOREIGN KEY (id_produto) REFERENCES produtos(id_produto) ON DELETE RESTRICT ON UPDATE CASCADE );
SELECT p.id_pedido, c.nome AS cliente, p.data_pedido, pr.nome AS produto, pp.quantidade, pr.preco FROM pedidos p JOIN clientes c ON p.id_cliente = c.id_cliente JOIN pedido_produto pp ON p.id_pedido = pp.id_pedido JOIN produtos pr ON pp.id_produto = pr.id_produto;
SELECT pr.nome, SUM(pp.quantidade) AS total_vendido FROM produtos pr JOIN pedido_produto pp ON pr.id_produto = pp.id_produto GROUP BY pr.nome ORDER BY total_vendido DESC;
SELECT c.nome, SUM(pp.quantidade * pr.preco) AS total_gasto FROM clientes c JOIN pedidos p ON c.id_cliente = p.id_cliente JOIN pedido_produto pp ON p.id_pedido = pp.id_pedido JOIN produtos pr ON pp.id_produto = pr.id_produto GROUP BY c.nome;
CREATE INDEX idx_pedido ON pedido_produto(id_pedido);
EXPLAIN SELECT * FROM pedidos WHERE id_cliente = 1;

