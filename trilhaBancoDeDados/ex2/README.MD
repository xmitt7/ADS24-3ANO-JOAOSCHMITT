parte pratica
-- Banco de dados: `banco_dados`
--

-- --------------------------------------------------------

--
-- Estrutura para tabela `produto`
--

CREATE TABLE `produto` (
  `id` int NOT NULL,
  `nome` varchar(100) NOT NULL,
  `preco` decimal(8,2) DEFAULT NULL,
  `data_cadastro` datetime DEFAULT CURRENT_TIMESTAMP,
  `descricao` varchar(1000) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

--
-- Índices para tabelas despejadas
--

--
-- Índices de tabela `produto`
--
ALTER TABLE `produto`
  ADD PRIMARY KEY (`id`);

--
-- AUTO_INCREMENT para tabelas despejadas
--

--
-- AUTO_INCREMENT de tabela `produto`
--
ALTER TABLE `produto`
  MODIFY `id` int NOT NULL AUTO_INCREMENT;
COMMIT;
-- 
DROP TABLE `produto`

parte teorica

Resposta 1:
A normalização é um processo utilizado em bancos de dados para organizar as informações de forma eficiente, evitando a repetição de dados e reduzindo erros. Ela divide os dados em tabelas menores e relacionadas, garantindo maior integridade e organização.

Resposta 2:
As formas normais são regras que ajudam a organizar o banco de dados. A 1ª forma normal (1NF) exige que cada campo tenha apenas um valor, sem listas. A 2ª forma normal (2NF) exige que a tabela esteja na 1NF e que todos os dados dependam da chave primária completa. A 3ª forma normal (3NF) exige que a tabela esteja na 2NF e que não existam dependências entre campos que não sejam a chave. A BCNF é uma versão mais rigorosa da 3NF, onde todo determinante deve ser uma chave candidata.

Resposta 3:
Um exemplo de normalização começa com uma tabela que possui dados repetidos, como pedido, cliente, cidade e produto na mesma tabela. Nesse caso, o nome do cliente e a cidade se repetem várias vezes. Para normalizar, primeiro garante-se que os dados sejam atômicos (1NF). Depois, separa-se as informações em tabelas diferentes, como cliente, produto e pedido (2NF). Por fim, remove-se dependências indevidas, como cidade ligada a outro campo, criando uma tabela separada para cidade (3NF). O resultado é um banco de dados organizado, sem repetições e mais fácil de manter.