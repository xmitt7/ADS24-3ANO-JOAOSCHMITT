Parte pratica

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
  `valor_total` decimal(10,2) DEFAULT NULL,
  `data_pedido` datetime DEFAULT current_timestamp()
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Despejando dados para a tabela `pedidos`
--

INSERT INTO `pedidos` (`id_pedido`, `id_cliente`, `valor_total`, `data_pedido`) VALUES
(4, 3, 100.00, '2026-04-23 14:29:03'),
(5, 3, 200.00, '2026-04-23 14:29:03'),
(6, 2, 150.00, '2026-04-23 14:29:03'),
(7, 3, 999.99, '2026-04-23 14:29:03');

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

comandos usados

CREATE TABLE clientes ( id_cliente INT AUTO_INCREMENT PRIMARY KEY, nome VARCHAR(100) );
INSERT INTO clientes (nome) VALUES ('João'), ('Maria');
SELECT id_cliente, nome, CONCAT(nome, '_', id_cliente) AS identificador FROM clientes;
DROP TABLE `livros`
DROP TABLE `autores`
SELECT * FROM `clientes`
SELECT nome, SUBSTRING(nome, 1, 3) AS inicio_nome FROM produtos;
SELECT nome, UPPER(nome) AS nome_maiusculo FROM clientes;
SELECT * FROM `pedidos`
SELECT * FROM `pedido_produto`
SELECT * FROM `perfil`
SELECT * FROM `produtos`
SELECT * FROM `clientes`
SELECT DATE_FORMAT(NOW(), '%d/%m/%Y %H:%i:%s') AS data_hora_formatada;
ALTER TABLE pedidos ADD COLUMN data_pedido DATETIME DEFAULT CURRENT_TIMESTAMP;
SELECT id_pedido, data_pedido, DATEDIFF(NOW(), data_pedido) AS dias_passados FROM pedidos;
SELECT nome, preco, ROUND(preco, 2) AS preco_arredondado FROM produtos;
SELECT * FROM `pedidos`
SELECT id_pedido, valor_total, FLOOR(valor_total) AS arredondado_para_baixo, CEIL(valor_total) AS arredondado_para_cima FROM pedidos;
SELECT * FROM `pedidos`
SELECT * FROM `pedido_produto`
SELECT * FROM `pedidos`
SELECT * FROM `clientes`
SELECT * FROM `pedidos`
SELECT * FROM `pedido_produto`
SELECT * FROM `perfil`
SELECT * FROM `produtos`
SELECT * FROM `pedidos`
SELECT * FROM `pedidos`
SELECT * FROM `pedidos`
DROP PROCEDURE IF EXISTS inserir_pedido;
DROP PROCEDURE IF EXISTS inserir_pedido;


Parte Teóricas

Resposta 1:
Funções no MySQL são comandos que retornam valores a partir de dados. Os tipos mais comuns são funções de string, data/hora e numéricas.

Resposta 2:
A função CONCAT junta valores, sendo usada em relatórios para combinar dados como nome e sobrenome ou criar identificadores.

Resposta 3:
NOW retorna data e hora atual. CURDATE retorna apenas a data. NOW é usado quando precisa de horário, CURDATE quando só a data importa.

Resposta 4:
ROUND arredonda normalmente, FLOOR arredonda para baixo e CEIL para cima. ROUND é usado para valores comuns, FLOOR para limites mínimos e CEIL para limites máximos.

Resposta 5:
Procedimentos armazenados melhoram desempenho, organizam o código e aumentam a segurança do banco.

Resposta 6:
IN recebe valor, OUT retorna valor e INOUT faz os dois ao mesmo tempo.

Resposta 7:
O comando é CALL, usado para executar o procedimento passando os parâmetros necessários.

Resposta 8:
UDFs são funções criadas pelo usuário que retornam valores. Diferem dos procedimentos porque podem ser usadas dentro de SELECT.

Resposta 9:
Uma função personalizada é útil quando se precisa repetir um cálculo, como aplicar desconto em vários pedidos.

Resposta 10:
Funções retornam um valor e podem ser usadas em consultas. Procedimentos não retornam diretamente valores e são usados para executar ações.