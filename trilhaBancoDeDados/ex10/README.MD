Parte pratica

NAO NENHUM COMANDO COM TRIGGER DEU CERTO

Parte teórica
Resposta 1:
Triggers são ações automáticas executadas pelo banco quando ocorre INSERT, UPDATE ou DELETE. Vantagens: automatização e integridade dos dados.
Resposta 2:
BEFORE executa antes da ação, AFTER depois. BEFORE é usado para validação, AFTER para atualizar dados relacionados.
Resposta 3:
Eventos são internos ao MySQL, não dependem do sistema operacional e são mais fáceis de gerenciar dentro do banco.
Resposta 4:
Um trigger pode impedir inserções inválidas, como bloquear um pedido com estoque insuficiente antes de salvar.
Resposta 5:
Evitar triggers complexos e pesados, pois podem deixar o sistema lento. Sempre manter simples e objetivo.
Resposta 6:
Eventos automatizam tarefas como limpeza de logs ou geração de relatórios sem intervenção manual.
Resposta 7:
Pode estar desativado por segurança ou configuração. Ativa com SET GLOBAL event_scheduler = ON.
Resposta 8:
DROP TRIGGER nome_trigger. Os dados não são afetados, apenas a automação deixa de existir.
Resposta 9:
Manter triggers simples, documentar e evitar excesso. Isso facilita manutenção e evita erros.
Resposta 10:
Planejar evita execuções erradas ou em horários críticos, como eventos que podem sobrecarregar o banco.