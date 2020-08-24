**RF (Requisitos Funcionais)**
-> São as funcionalidades que vamos ter dentro de Recuperação de Senha
ex: o usuário vai poder recuperar a senha informando o email dele
-> Nesse campo vamos descrever cada uma das funcionalidades para recuperar uma senha

**RNF (Requisitos não Funcionais)**
-> São coisas que não são ligadas diretamente com a regra de negócios da aplicação
ex: oenvio de email precisa ser feito utilizando a lib noadmailer
-> São requisitos mais voltados para a parte técnica e que foge um pouco
da questão de como o sistema vai funcionar.
-> É mais voltado para a questão de qual lib vamos utilizar, qual banco vamos usar,
etc.. coisas que não estão ligadas diretamente a funcionalidade e sim
com alguma coisa que escolhemos utilizar

obs: A regra de negócio sempre deve estar atrelada a um requisito funcional (caso
tenhamos alguma regra de negócio que não consigamos atrelar
a um requisito funcinal, alguma coisa está errada).


# Recuperação de senha

**RF (Requisitos Funcionais)**
-> O usuário deve poder recperar a sua senha informando o seu e-mail;
-> O usuário deve receber um e-mail com instruções de recuperação de senha;
-> O usuário deve poder resetar a sua senha.

**RNF (Requisitos não Funcionais)**
-> Utilizar o Mailtrap para testar envios em ambinete de desenvolvimento (o mailtrap
funciona como um serviço de e-mail fake);
-> Utilizar o Amazon SES para envios em produção;
-> O envio de e-mials deve acontecer em segundo plano (background job);
   - O envio de e-mail demora um pouco de acontecer, por isso devemos deixar
   ele rodando em segundo plano.
   - Vamos ter uma fila onde mandaremos ações para essa fila e ela vai processar
   conforme ela vai conseguindo.
   ex: 100 pessoas fazendo a recuperação de senha ao mesmo tempo. ao invés de
   enviarmos senha e e-mail ao mesmo tempo (pode gerar lentidão) vamos jogar
   tudo isso em uma fila, e esssa fila é processada em segundo plano, será processada
   aos poucos pela ferramenta que vamos utilizar e ai ele vai enviando os emails
   conforme der. (a recuperação de senha não é uma coisa que temos que fazer
   no mesmo segundo que o usuário requisitar).

**RN (Regras de Negócio)**
-> O link enviado por e-mail para resetar senha deve expirar em 2hs;
-> O usuário precisa confirmar a sua nova senha ao resetar sua senha;

# Atualização do perfil
**RF (Requisitos Funcionais)**
-> O usuário deve poder atualizar o seu perfil (nome, email e senha);

**RN (Regras de Negócio)**
-> O usuário não pode alterar seu e-mail para um e-mail já utilizado;
-> Para atualizar a sua senha o usuário deve informar a senha antiga;
-> Para atualizar a sua senha o usuário precisa confirmar a nova senha;

# Painel do prestador
**RF (Requisitos Funcionais)**
-> O usuário deve poder listar seus agendamentos de um dia específico;
-> O prestador deve receber um notificação sempre que tiver um novo agendamento;
-> O prestador deve poder visualizar as notificações não lidas;

**RNF (Requisitos não Funcionais)**
-> Os agendamentos do prestador no dia devem ser armazenados em cache;
-> As notificações do prestador devem ser armazenadas no MongoDB;
  - como as notificações são geralmente só texto (não precisam realizar
  relacionamentos).
  - Cada notificação pode ter um conteúdo diferente da outra (não precisamos
  de campos pré-definidos e estruturados para salvar as informações);
-> As notificações do prestador devem ser enviadas em tempo real utilizando o
Socket.io (lib para lhe dar com protocolo web socket que é um protocolo
assim como o http, porém nos permite transitar mensagens em tempo real, ou seja
consguimos cominicar o front com o back em tempo real);

**RN (Regras de Negócio)**
-> A notificação deve ter um status de lida ou não lida para que o prestador
possa controlar;


# Agendamento de serviços
**RF (Requisitos Funcionais)**
-> O usuário deve poder listar todos os prestadores de serviço cadastrados;
-> O usuário deve poder listar os dias de um mês com pelo menos um horário
disponível de um prestador;
-> O usuário deve poder listar horários disponíveisem um dia específico de um prestador;
-> O usuário deve poder realizar um novo agendamento com um prestador;

**RNF (Requisitos não Funcionais)**
-> A listagem de prestadores deve ser armazenada em cache;

**RN (Regras de Negócio)**
-> Cada agendamento deve durar exatamente 1h;
-> Os agendamentos devem estar disponíveis entre 8hs ás 18hrs (Primeiro ás 8hrs
e ultimo ás 17hrs);
-> O usuário não pode agendar em um horario já ocupado;
-> O usuário não pode agendar em um horário que já passou;
-> O usuário não pode agendar serviços com ele mesmo;




