parte pratica

-- Banco de dados: `biblioteca`
--

-- --------------------------------------------------------

--
-- Estrutura para tabela `autores`
--

CREATE TABLE `autores` (
  `id_autor` int(11) NOT NULL,
  `nome` varchar(100) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Despejando dados para a tabela `autores`
--

INSERT INTO `autores` (`id_autor`, `nome`) VALUES
(1, 'Autor 1'),
(2, 'Autor 2');

-- --------------------------------------------------------

--
-- Estrutura para tabela `clientes`
--

CREATE TABLE `clientes` (
  `id_cliente` int(11) NOT NULL,
  `nome` varchar(100) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Despejando dados para a tabela `clientes`
--

INSERT INTO `clientes` (`id_cliente`, `nome`) VALUES
(1, 'João'),
(2, 'Maria');

-- --------------------------------------------------------

--
-- Estrutura para tabela `livros`
--

CREATE TABLE `livros` (
  `id_livro` int(11) NOT NULL,
  `titulo` varchar(100) DEFAULT NULL,
  `id_autor` int(11) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Despejando dados para a tabela `livros`
--

INSERT INTO `livros` (`id_livro`, `titulo`, `id_autor`) VALUES
(1, 'Livro A', 1),
(2, 'Livro B', 2);

--
-- Índices para tabelas despejadas
--

--
-- Índices de tabela `autores`
--
ALTER TABLE `autores`
  ADD PRIMARY KEY (`id_autor`);

--
-- Índices de tabela `clientes`
--
ALTER TABLE `clientes`
  ADD PRIMARY KEY (`id_cliente`);

--
-- Índices de tabela `livros`
--
ALTER TABLE `livros`
  ADD PRIMARY KEY (`id_livro`),
  ADD KEY `id_autor` (`id_autor`);

--
-- AUTO_INCREMENT para tabelas despejadas
--

--
-- AUTO_INCREMENT de tabela `autores`
--
ALTER TABLE `autores`
  MODIFY `id_autor` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=3;

--
-- AUTO_INCREMENT de tabela `clientes`
--
ALTER TABLE `clientes`
  MODIFY `id_cliente` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=3;

--
-- AUTO_INCREMENT de tabela `livros`
--
ALTER TABLE `livros`
  MODIFY `id_livro` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=3;

--
-- Restrições para tabelas despejadas
--

--
-- Restrições para tabelas `livros`
--
ALTER TABLE `livros`
  ADD CONSTRAINT `livros_ibfk_1` FOREIGN KEY (`id_autor`) REFERENCES `autores` (`id_autor`);
COMMIT;

comando para backup

Backup completo do banco

mysqldump -u root -p biblioteca > biblioteca_backup.sql

Backup apenas das tabelas livros e autores

mysqldump -u root -p biblioteca livros autores > backup_parcial.sql

Backup de todos os bancos

mysqldump -u root -p --all-databases > backup_total.sql

Backup incremental (logs binários)

Ativar no MySQL (my.ini ou my.cnf):

log-bin=mysql-bin

Depois usar:

mysqlbinlog mysql-bin.000001 > incremental.sql

Explicação:

Logs binários guardam alterações (INSERT, UPDATE, DELETE)
Você usa eles para recuperar só mudanças recentes

Restaurar banco biblioteca

mysql -u root -p biblioteca < biblioteca_backup.sql

Restaurar todos os bancos

mysql -u root -p < backup_total.sql

Exportar para CSV

SELECT * 
FROM clientes
INTO OUTFILE 'C:/xampp/mysql/data/clientes.csv'
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n';

Importar CSV

LOAD DATA INFILE 'C:/xampp/mysql/data/clientes.csv'
INTO TABLE clientes
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n';

Automatizar backup (cron job - Linux)

0 2 * * * mysqldump -u root -p senha biblioteca > /backups/biblioteca_$(date +\%F).sql

Teste de restauração

Criar banco de teste:
CREATE DATABASE biblioteca_teste;

Restaurar:
mysql -u root -p biblioteca_teste < biblioteca_backup.sql

Verificar:
USE biblioteca_teste;
SELECT * FROM livros;
SELECT * FROM autores;



parte teorica

Resposta 1:

Backup é uma cópia dos dados para segurança. Ele é importante para evitar perda de dados em caso de erro, falha ou ataque.
Resposta 2:

mysqldump é usado para exportar banco de dados. Ele permite fazer backup completo ou parcial.
Resposta 3:

Backup completo copia tudo. Backup incremental copia apenas alterações. Completo é mais seguro, incremental é mais rápido.
Resposta 4:

Logs binários registram alterações no banco. Eles podem ser usados para recriar mudanças e fazer backup incremental.
Resposta 5:

LOAD DATA INFILE importa arquivos CSV para o banco. É preciso configurar separador, aspas e quebra de linha.
Resposta 6:

SELECT INTO OUTFILE exporta dados para arquivo. Pode configurar separadores e formato.
Resposta 7:

Fazer backups regularmente
Armazenar em locais seguros
Testar restauração
Resposta 8:

Testar restauração garante que o backup funciona. Pode identificar erros ou dados corrompidos.
Resposta 9:

CSV é usado porque é simples, leve e compatível com vários sistemas.
Resposta 10:

Automatizar backups economiza tempo e evita esquecimento. Deve garantir que os arquivos estão sendo gerados corretamente.