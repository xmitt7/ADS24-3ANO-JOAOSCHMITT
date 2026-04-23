
-- Banco de dados: `banco_de_dados`
--

-- --------------------------------------------------------

--
-- Estrutura para tabela `clientes`
--

CREATE TABLE `clientes` (
  `id_cliente` int(11) NOT NULL,
  `nome` varchar(100) DEFAULT NULL,
  `email` varchar(100) DEFAULT NULL,
  `cidade` varchar(100) DEFAULT 'Não Informado'
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Despejando dados para a tabela `clientes`
--

INSERT INTO `clientes` (`id_cliente`, `nome`, `email`, `cidade`) VALUES
(2, 'Maria', NULL, 'Não Informado'),
(3, 'Pedro', NULL, 'Não Informado'),
(4, 'Ana', NULL, 'Não Informado'),
(5, 'Carlos', NULL, 'Não Informado'),
(6, 'Fernanda', NULL, 'Não Informado'),
(7, 'Lucas', NULL, 'Não Informado'),
(8, 'Juliana', NULL, 'Não Informado'),
(9, 'Rafael', NULL, 'Não Informado'),
(10, 'Patricia', NULL, 'Não Informado'),
(11, 'João', NULL, 'Não Informado'),
(12, 'Maria', NULL, 'Não Informado');

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
  `preco` decimal(10,2) NOT NULL,
  `categoria` varchar(100) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Despejando dados para a tabela `produtos`
--

INSERT INTO `produtos` (`id_produto`, `nome`, `preco`, `categoria`) VALUES
(1, 'Pizza Calabresa', 50.00, NULL),
(2, 'Pizza Frango', 45.00, NULL),
(3, 'Refrigerante', 10.00, NULL),
(4, 'Suco', 8.00, NULL),
(5, 'Hamburguer', 25.00, NULL),
(6, 'Pizza', 50.00, NULL),
(7, 'Refrigerante', 10.00, NULL),
(8, 'Pizza', 50.00, NULL),
(9, 'Refrigerante', 10.00, NULL);

--
-- Índices para tabelas despejadas
--

--
-- Índices de tabela `clientes`
--
ALTER TABLE `clientes`
  ADD PRIMARY KEY (`id_cliente`),
  ADD UNIQUE KEY `idx_email_clientes` (`email`),
  ADD KEY `idx_nome_clientes` (`nome`),
  ADD KEY `idx_nome_cidade` (`nome`,`cidade`);

--
-- Índices de tabela `pedidos`
--
ALTER TABLE `pedidos`
  ADD PRIMARY KEY (`id_pedido`),
  ADD KEY `idx_pedidos_cliente` (`id_cliente`);

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
  ADD PRIMARY KEY (`id_produto`),
  ADD KEY `idx_produtos_categoria` (`categoria`),
  ADD KEY `idx_produtos_preco` (`preco`);

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


comandos 

CREATE INDEX idx_nome_clientes ON clientes(nome);
CREATE UNIQUE INDEX idx_email_clientes ON clientes(email);
ALTER TABLE clientes ADD cidade VARCHAR(100) DEFAULT 'Não Informado';
CREATE INDEX idx_nome_cidade ON clientes(nome, cidade);
EXPLAIN SELECT clientes.nome, pedidos.valor_total FROM clientes JOIN pedidos ON clientes.id_cliente = pedidos.id_cliente;
CREATE INDEX idx_pedidos_cliente ON pedidos(id_cliente);
Expandir Repetir consulta Editar Banco de dados : Tempo de execução da consulta : 9:35:33
SHOW INDEX FROM clientes;
EXPLAIN SELECT * FROM clientes WHERE nome = 'João';
EXPLAIN SELECT * FROM clientes WHERE nome = 'João';
SELECT * FROM clientes ORDER BY nome LIMIT 5;
SELECT * FROM clientes WHERE nome = 'João';
ALTER TABLE produtos ADD categoria VARCHAR(100);
CREATE INDEX idx_produtos_preco ON produtos(preco);
EXPLAIN SELECT clientes.nome, SUM(produtos.preco * pedido_produto.quantidade) AS total FROM clientes JOIN pedidos ON clientes.id_cliente = pedidos.id_cliente JOIN pedido_produto ON pedidos.id_pedido = pedido_produto.id_pedido JOIN produtos ON pedido_produto.id_produto = produtos.id_produto
WHERE produtos.preco > 50
GROUP BY clientes.nome;


parte teorica

Resposta 1:
Índices são estruturas que ajudam o banco a encontrar dados mais rápido. Eles são importantes porque melhoram a performance em tabelas grandes.

Resposta 2:
Índice básico melhora busca. Índice único não permite valores repetidos. Exemplo: nome pode repetir, email não.

Resposta 3:
Índice composto usa mais de uma coluna. Ele é útil quando a consulta usa várias condições, como nome e cidade juntos.

Resposta 4:
Índices podem deixar INSERT, UPDATE e DELETE mais lentos, porque o banco precisa atualizar o índice também.

Resposta 5:
EXPLAIN mostra como a consulta será executada. Ele mostra informações como tipo de acesso, índice usado e quantidade de linhas.

Resposta 6:
Full Table Scan é quando o banco lê toda a tabela. Isso é ruim porque deixa a consulta lenta. Pode ser evitado com índices.

Resposta 7:
LIMIT reduz a quantidade de dados retornados, melhorando a performance. Exemplo: mostrar apenas os 5 primeiros registros.

Resposta 8:
Índices ajudam nos JOINs porque aceleram a busca dos dados relacionados entre tabelas.

Resposta 9:
Evitar SELECT *
Usar WHERE para filtrar
Criar índices nas colunas usadas em consultas

Resposta 10:
Funções de agregação podem deixar a consulta mais lenta porque processam muitos dados. Pode melhorar usando índices e filtros antes do GROUP BY.