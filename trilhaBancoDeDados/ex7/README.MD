parte pratica

comandos 

Resposta 1: Criação de usuários

CREATE USER 'usuario_local'@'localhost'
IDENTIFIED BY 'senha123';

CREATE USER 'usuario_remoto'@'%'
IDENTIFIED BY 'senha123';

Resposta 2: Alteração de senha

ALTER USER 'usuario_local'@'localhost'
IDENTIFIED BY 'Senha@Forte123';

Resposta 3: Exclusão de usuário

DROP USER 'usuario_remoto'@'%';

Resposta 4: Concessão de permissões

GRANT SELECT ON banco_de_dados.clientes
TO 'usuario_local'@'localhost';

CREATE USER 'admin_user'@'%'
IDENTIFIED BY 'admin123';

GRANT ALL PRIVILEGES ON loja.*
TO 'admin_user'@'%';

Resposta 5: Revogação de permissões

REVOKE SELECT ON banco_de_dados.clientes
FROM 'usuario_local'@'localhost';

Resposta 6: Usuário com acesso apenas local

CREATE USER 'usuario_servidor'@'localhost'
IDENTIFIED BY 'senha123';

Resposta 7: Princípio do menor privilégio

CREATE USER 'relatorio_user'@'%'
IDENTIFIED BY 'senha123';

GRANT SELECT ON banco_de_dados.relatorios
TO 'relatorio_user'@'%';

Resposta 8: Auditoria de usuários

SELECT user, host FROM mysql.user;

SHOW GRANTS FOR 'usuario_local'@'localhost';

Resposta 9: Política de senhas fortes

INSTALL PLUGIN validate_password SONAME 'validate_password.so';

SET GLOBAL validate_password.policy = STRONG;

Resposta 10: Configuração para produção

Usuário somente leitura:

CREATE USER 'leitura_user'@'%'
IDENTIFIED BY 'senha123';

GRANT SELECT ON producao.*
TO 'leitura_user'@'%';

Usuário com permissões de escrita:

CREATE USER 'escrita_user'@'%'
IDENTIFIED BY 'senha123';

GRANT INSERT, UPDATE, DELETE ON producao.*
TO 'escrita_user'@'%';
parte teorica

Resposta 1:
GRANT serve para dar permissões a um usuário. REVOKE serve para remover essas permissões. Exemplo: GRANT SELECT para permitir leitura e REVOKE SELECT para retirar.

Resposta 2:
Princípio do menor privilégio significa dar ao usuário apenas o acesso necessário. Isso é importante para evitar erros e aumentar a segurança.

Resposta 3:
Senhas fortes evitam invasões. Uma senha segura tem letras maiúsculas, minúsculas, números e símbolos.

Resposta 4:
Usuários compartilhados dificultam identificar quem fez alterações. Isso reduz a segurança e controle.

Resposta 5:
Permissões desnecessárias podem permitir exclusão ou alteração indevida de dados. Para evitar isso, dar apenas o acesso necessário.

Resposta 6:
Restrição por host limita de onde o usuário pode acessar. Isso aumenta a segurança impedindo acessos externos.

Resposta 7:
SELECT lê dados
INSERT insere dados
UPDATE altera dados
DELETE remove dados

Resposta 8:
Auditoria é verificar usuários e permissões. É importante para garantir segurança e controle.

Resposta 9:
Dar apenas permissões necessárias
Evitar usuários compartilhados
Revisar permissões regularmente

Resposta 10:
Desenvolvedores podem ter acesso limitado para alterar dados. Administradores têm acesso completo para gerenciar o banco.