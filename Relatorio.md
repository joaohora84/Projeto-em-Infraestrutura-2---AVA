# Instalação e configuração do Moodle no Ubuntu Server

### Objetivo
    
    Mostrar passo a passo como instalar e configurar o Moodle no Ubuntu Server.
    
### Download

  >wget https://download.moodle.org/stable38/moodle-latest-38.tgz
  
### Descompactar o arquivo dentro da pasta **/var/www**

  >tar -zxvf moodle-latest-38.tgz
  
### Acesso no navegador o endereço http://<ip_servidor>/moodle

   Você verá a primeira tela de Moodle. Selecione a linguagem e clique em avançar. O moodle irá fazer um verificação no sistema e mostrará um tela para definir
   se o é capaz de rodar o moodle.
   
   Se tudo estiver ok clique em próximo. Nesta tela também é mostrado o diretório onde será instalado o Moodle.
   
### Crie um diretório chamado moodledata dentro do /var e dê permissão total a ele, e reinicie o Apache.

    >mkdir /var/moodledata
    
    >chmod 777 moodledata
    
    >service apache2 restart
    
    
    Na tela de instação do Moodle clique em próximo.
    
A próxima tela mostrada é muito importante, aqui é referente ao banco de dados do Moodle. Antes de prosseguir vamos criar o banco.

### Vá no terminal e digite os comando para criar o banco, usuário, e dar privilégios ao mesmo.

    >mysql -u root -p
    
    >CREATE DATABASE moodle DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
    
    >CREATE USER 'moodle'@'localhost' IDENTIFIED WITH mysql_native_password BY 'SENHA';
    
    >GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,CREATE TEMPORARY TABLES, DROP, INDEX,ALTER ON moodle.* moodle@localhost;
    
    >quit;
    
 ### Na tela de instalão do Moodle informamos os dados do banco e clicamos em próximo.
 
 O Moodle fará uma varredura no sistema para saber se é compatível ou não.
 
 As seguintes linhas no arquivo config.php devem estar de acordo com essas, se não o Moodle vai informar o erro e sugerir que seja alterado o arquivo config.php.
 
 $CFG->dbtype = 'mysql'; // mysql or postgres7 (for now)
 
 $CFG->dbhost = 'localhost'; // eg localhost or db.isp.com
 
 $CFG->dbname = 'moodle'; // database name, eg moodle
 
 $CFG->dbuser = 'moodle'; // your database username
 
 $CFG->dbpass = 'moodle'; // your database password
 
 $CFG->prefix = 'mdl_'; // Prefix to use for all table names
 
 Verifique a linha $CFG->wwwroot = 'http://localhost/moodle';
 
 Verifique a linha $CFG->dirroot = '/var/www/moodle';
 
 Verifique a linha $CFG->dataroot = '/var/moodledata';
 
 Se tudo certo volte e continue a instação.
 
 ### Na próxima tela apresentada, você deve configurar os dados do usuário administrador para acesso à plataforma.
 
 Após inserir as informações solicitadas nesta tela, o Moodle estará pronto para ser acessado. Basta acessar o endereço referente e logar com o usuário e senha criados na 
 última tela.
 
 ### Referência
 
 [Moodle.org](https://docs.moodle.org/all/pt_br/Instala%C3%A7%C3%A3o_do_Moodle_no_Ubuntu)
 
 [Techexpert.tips](https://techexpert.tips/pt-br/moodle-pt-br/instalacao-de-moodle-no-ubuntu-linux/)
    
    

   
  



