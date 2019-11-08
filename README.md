#Iniciando o projeto 

   #Instalando as dependecias.
   
   1-yarn init -yarn
   
   2-yarn add express pg pg-hstore sequelize
   
   3-yarn add sequelize-cli -D 
   
       obs:yarn sequelize -h ver todos os comando do sequelize
   
   #Abre a pasta onde estalou o projeto.
   
     code.
	 
   # Dentro do projeto estala a dependecias nodemon.
   
     1-yarn add nodemon -D
	 
   #Dentro do package.js ensira o sequinto codigo

     "script":{
       "dev": "nodemon src/server.js"
              },
			  
    #Criar uma pasta no projeto src dentro um arquivo server.js
	
	#Dentro do arquivo server.js
	 
	  const express = require('express');
	  
	  const app = express();
	  
	  app.listen(3333);
	  
	#Criar um arquivo routes.js dentro da pasta src.
         dentro desse aquivo coloca o codigo.

          const express = require('express');

          const routes = express.Router();

          routes.get('/', (req, res) => {
             return res.json({hello:'whord'});
		  })

      module.exports = routes;

    #Volta no arquevo server.js para importar a rotas.
       código a ser ensarido:
        
        const routes = require('./routes');

        app.use(routes);
        app.use(express.json());
		
		ver se esta tudo ok execulta yarn dev entra na localhost:3333:

    #Cria uma  pasta no scr com nome config dentro um arguivo database.js
	  coloca o código dentro:
	  
	  module.export={
		  dialect:,
		  host,
		  username,
		  database,
		  define:{
			  timestamps: true,
			  underscored: true,
		  },
	  };
	  
	  
    #Cria uma pasta no src com o nome database e dentro um arquivo index.		
       coloca o código dentro:
	   
	   const Sequelize = require('sequelize');
	   
	   const dbConfig = require('../config/database');
	   
	   const connection = new Sequelize(dbConfig);
	   
	   module.export = connection;
	   
	   #Cria um arquilo na raiz do projeto .sequelizerc
	     obs: tem que tranformar a limguagem desse arquivo para javascript.
		   dentro coloca o seguinte codigo:
		   
		   const path = require('path');
		   
		   module.export = {
			   config : path.resolve(__Disname, 'src', 'config', 'database.js'),
			   
		   };
		   
		   
		   #Desntro da pasta database criar uma pasta chamada migrations
		   
		   #Dentro do arquivo .sequelizerc acresenta o sequinte código.
		   
		      'migrations-path': path.resolve(__Disname, 'scr', 'database', 'migrations'),
			  
		  #Criando o arquivo de migrations para a pasta migrations.
             execulta o comando: yarn sequelize migration:create --name = create-Users

           
    #Criando a migração no banco de dados.
      entra na pasta migrations que foi criada dentro da pasta database 
  
         dentro tem um código altera conforme os dados da sua tabela de usuários.

          'use script';

         module.export={
           
           up:(queryInterface, Sequelize)=>{
			   return queryInterface.CreateTable('users',{          
              id:{
                 type: Sequelize.STRING,
                 primaryKey: true,
                 autoIncrement: true,
                 allowNull: false,
                 
			  },
              name:{
                 type: Sequelize.STRING,
                 allowNull: false,
              },
              
              email:{
                 type: Sequelize.STRING,
                 allowNull: false,
			  },
 
              created_at:{
                 type: Sequelize.DATE,
                 allowNull:false,
			  },
   
               updated_at:{
                  type: Sequelize.DATE,
                  allowNull: false,
			   },				  
			   
		   });
		   },
		   
		   #Execulta o comando no cmd para criação da tabela no banco de dados.
		   
		              yarn sequelize db:create 
		              yarn sequelize db:migrate 
					  
			#Trabalhando com migration 
              1°Para desfazer a ultima migration faça o comando.
                 yarn sequelize db:migrate: undo

               2°Para fazer alterção em uma migration ja criada no banco seque esse passos
                  cria outra maigrations : yarn sequelize db:miration
                   dentro coloca o sequinte codigo:

                  'use script'

              module.export ={
            up(queryInterface, Sequelize)=>{

                'users'; "obs: esse e o nome da tabela a qual quer mudar o campo"
                'Age'; "obs: esse e o nome da coluna da tabela a ser acresentado ou substituido"
			},
			  };

           #No comando dows(queryInterface, Sequelize)=>{
		 return queryInterface.removeColumn('User';'age';);}} serve para deletar a coluna da tabela 

          #Execulta o comando para fazer a alteração no banco de dados colocando a coluna noca.
              yarn sequelize db:migrate
              yarn sequelize db:migrate:undo
     
          #Cria dentro do diretorio scr uma pasta chamada models dentro um arquivo User.js         
            
              coloca dentro o código:
     
              const {Model, Data_Types} = require('sequelize');

              class User externds Model {
                 static init(sequelize){
                  super.init({
                     name:DataTypes.STRING,
                     email:DataTypes.STRING,
				  }, 
				  { sequelize
				  })
				 }
			  }

             module.export = User;

          #Dentro do arquivo index da pasta database import o models 
        
             const User = require('../models/User');

            depois do comando new connection insira o seguinte codigo 
   
             User.Init(connection);

 
          # Cria uma pasta controllers dentro cria uma arquivo UserController.js
  
              ensira o sequinte codigo:
       
               const User = require('../models/User');

             module.export ={
               async store(req, res){
                 const {name, email} = req.body;
 
             const user = await User.Create({name,email});

              return res.json(user);
			   }
			 };

          #Vai para o arquivo routes e importa o controller User.

              const UserController = require('./controller/UserController');
			  
			  routes.post('/users, UserController.store);
			  
			  

           obs: Import dentro do arquivo server.js a connect com o banco de dados
                  require('./database');

            # depois execulta o comando dentro do insomnia o usuario a ser cadastrado.			
   
  