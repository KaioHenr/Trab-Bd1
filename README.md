# TRABALHO 01:  Título do Trabalho
Trabalho desenvolvido durante a disciplina de BD1

# Sumário

### 1. COMPONENTES<br>
Integrantes do grupo<br>
Adriano Lemos Bandeira: adriano.lemos1997@gmail.com<br>
Daniel Martins Patricio: daniel011298@hotmail.com<br>
Isadora Laurindo Brandão: isabrandao13@gmail.com<br>
Kaio Henrique Arantes Andre Nheri: kaiohenrrique50@gmail.com<br> 


### 2.MINI-MUNDO<br>

O sistema proposto para “Quero viajar”, conterá as informações aqui detalhadas. Dos usuários, são necessários as informações pessoais, como nome, e-mail, seus interesses e senha. Sobre os locais deve-se saber o nome, descrição, foto, categoria e endereço. Os clientes podem deixar avaliações nos locais, datas, comentários e fotos caso queiram. Sendo que este sistema tem de permitir que um usuário possa “seguir” outros, para aumentar a relevância de seus comentários. O sistema tem de permitir a visualização dos estabelecimentos, de um endereço específico escolhido pelo usuário, podendo personalizar esta busca, filtrando por distância, tipo de estabelecimento e avaliação.

Entidades
  Usuário: nome, e-mail e senha;
  Locais: nome, descrição e endereço;
  Entretenimento: tipo e descrição;
  Foto: url;
  Avaliação: avaliação e descrição.

Relacionamento
  Usuário/usuário: Um usuário pode seguir nenhum ou vários usuários e um usuário pode ser seguido por nenhum ou vários usuários;
  Usuário/Locais: Um usuário pode avaliar nenhum ou mais locais e um local pode ser avaliado por nenhum ou vários usuários;
  Locais/Entretenimento: Um local tem um ou vários tipos de entretenimento, um tipo de entretenimento pode pertencer a um ou vários locais.
  Usuário/Entretenimento: Um usuário pode ter um ou mais entretenimentos e entretenimento pode estar relacionado com um ou mais usuários.
  Foto/Local: Uma foto representa um único local e um local pode ter nenhuma ou múltiplas fotos.
  Foto/Avaliação: Uma foto é registrada em uma única avaliação e uma avaliação pode ter nenhuma ou várias fotos.


### 3.PERGUNTAS A SEREM RESPONDIDAS<br>
#### 3.1 QUAIS PERGUNTAS PODEM SER RESPONDIDAS COM O SISTEMA PROPOSTO?
  O grupo Quero Viajar precisa dos seguintes relatórios:
    Relatório que mostre locais utilizando filtros escolhidos pelo usuário;
    Relatório que mostre os locais dentro de um raio definido pelo usuário;
    Relatório que mostre o nome e os interesses de todos os usuários;
    Relatório que mostre o nome e a descrição de todos os locais;
    Relatório que mostre os locais que cada usuário comentou.


    
### 5.MODELO CONCEITUAL<br>
      A) Utilizar a Notação adequada (Preferencialmente utilizar o BR Modelo 3)
      B) O mínimo de entidades do modelo conceitual pare este trabalho será igual a 3 e o Máximo 5.
          * informe quais são as 3 principais entidades do sistema em densenvolvimento<br>(se houverem mais de 3 entidades, pense na importância da entidade para o sistema)       
      C) Principais fluxos de informação/entidades do sistema (mínimo 3). <br>Dica: normalmente estes fluxos estão associados as tabelas que conterão maior quantidade de dados 
      D) Qualidade e Clareza
          Garantir que a semântica dos atributos seja clara no esquema (nomes coerentes com os dados).
          Criar o esquema de forma a garantir a redução de informação redundante, possibilidade de valores null, 
          e tuplas falsas (Aplicar os conceitos de normalização abordados).   
          
  ![Alt text](https://github.com/discipbd1/trab01/blob/master/images/concept_sample.png?raw=true "Modelo Conceitual")
    
    
#### 5.1 Validação do Modelo Conceitual
  Grupo avaliado: Adriano Lemos Bandeira, Daniel Martins Patricio, Isadora Laurindo Brandão, Kaio Henrique Arantes Andre Nheri.
  
  Grupo avaliador: [Nomes dos que participaram na avaliação]


#### 5.2 Descrição dos dados 
  Usuário: Tabela que armazena as informações relativas ao usuário;
  Entretenimento: Tabela que armazena tipos possíveis de interesse de usuários e entretenimento disponíveis nos locais;
  Local: Tabela que armazena as informações relativas ao local;
  Foto: tabela que armazena fotos que podem pertencer a um local ou avaliação;
  Complemento: tabela que armazena o complemento do endereço dos locais;
  Avaliação: tabela que armazena as avaliações feitas pelos usuários sobre os locais.

### 6	MODELO LÓGICO<br>
        a) inclusão do esquema lógico do banco de dados
        b) verificação de correspondencia com o modelo conceitual 
        (não serão aceitos modelos que não estejam em conformidade)

### 7	MODELO FÍSICO<br>
CREATE TABLE USUARIO (
	id serial PRIMARY KEY,
	nome varchar(50),
	email varchar(30),
	senha varchar(30)
);

CREATE TABLE LOCAL (
	id serial PRIMARY KEY,
	nome varchar(50),
	descricao varchar(200),
	tipo_logradouro varchar(10),
	nome_logradouro varchar(100),
	cep integer,
	estado varchar(2),
	cidade varchar(25),
	bairro varchar(25),
	numero varchar(10),
	latitude varchar(15),
	longitude varchar(15)
);

CREATE TABLE COMPLEMENTO(
	id serial PRIMARY KEY,
	complemento varchar(200)
);

CREATE TABLE ENTRETENIMENTO (
	id serial PRIMARY KEY,
	tipo varchar(30),
	descricao varchar(200)
);

CREATE TABLE _Avaliacao (
	id serial PRIMARY KEY,
	fk_usuario_id integer,
	fk_local_id integer,
	comentario varchar(200),
	avaliacao smallint
);

CREATE TABLE FOTO (
	id serial PRIMARY KEY,
	data date,
	url_foto varchar(400)
);

CREATE TABLE LOCAL_COMPLEMENTO (
	fk_local_id integer,
	fk_complemento_id integer
);

CREATE TABLE USUARIO_USUARIO (
	fk_usuario_id_seguido integer,
	fk_usuario_id_seguidor integer
);

CREATE TABLE ENTRETENIMENTO_LOCAL (
	fk_entretenimento_id integer,
	fk_local_id integer
);

CREATE TABLE USUARIO_ENTRETENIMENTO (
	fk_usuario_id integer,
	fk_entretenimento_id integer
);

CREATE TABLE FOTO_ESTABELECIMENTO (
	fk_local_id integer,
	fk_foto_id integer
);

CREATE TABLE AVALIACAO_FOTO (
	fk__avaliacao_id integer,
	fk_foto_id integer
);

ALTER TABLE LOCAL_COMPLEMENTO ADD CONSTRAINT FK_LOCAL_COMPLEMENTO_1
	FOREIGN KEY (fk_local_id)
	REFERENCES LOCAL (id);

ALTER TABLE LOCAL_COMPLEMENTO ADD CONSTRAINT FK_LOCAL_COMPLEMENTO_2
	FOREIGN KEY (fk_complemento_id)
	REFERENCES COMPLEMENTO (id);
 
ALTER TABLE _Avaliacao ADD CONSTRAINT FK__Avaliacao_2
	FOREIGN KEY (fk_usuario_id)
	REFERENCES USUARIO (id);
 
ALTER TABLE _Avaliacao ADD CONSTRAINT FK__Avaliacao_3
	FOREIGN KEY (fk_local_id)
	REFERENCES LOCAL (id);
 
ALTER TABLE USUARIO_USUARIO ADD CONSTRAINT FK_USUARIO_USUARIO_1
	FOREIGN KEY (fk_usuario_id_seguido)
	REFERENCES USUARIO (id)
	ON DELETE CASCADE;
 
ALTER TABLE USUARIO_USUARIO ADD CONSTRAINT FK_USUARIO_USUARIO_2
	FOREIGN KEY (fk_usuario_id_seguidor)
	REFERENCES USUARIO (id)
	ON DELETE CASCADE;
 
ALTER TABLE ENTRETENIMENTO_LOCAL ADD CONSTRAINT FK_ENTRETENIMENTO_LOCAL_1
	FOREIGN KEY (fk_entretenimento_id)
	REFERENCES ENTRETENIMENTO (id)
	ON DELETE RESTRICT;
 
ALTER TABLE ENTRETENIMENTO_LOCAL ADD CONSTRAINT FK_ENTRETENIMENTO_LOCAL_2
	FOREIGN KEY (fk_local_id)
	REFERENCES LOCAL (id)
	ON DELETE RESTRICT;
 
ALTER TABLE USUARIO_ENTRETENIMENTO ADD CONSTRAINT FK_USUARIO_ENTRETENIMENTO_1
	FOREIGN KEY (fk_usuario_id)
	REFERENCES USUARIO (id)
	ON DELETE RESTRICT;
 
ALTER TABLE USUARIO_ENTRETENIMENTO ADD CONSTRAINT FK_USUARIO_ENTRETENIMENTO_2
	FOREIGN KEY (fk_entretenimento_id)
	REFERENCES ENTRETENIMENTO (id)
	ON DELETE RESTRICT;
 
ALTER TABLE FOTO_ESTABELECIMENTO ADD CONSTRAINT FK_FOTO_ESTABELECIMENTO_1
	FOREIGN KEY (fk_local_id)
	REFERENCES LOCAL (id)
	ON DELETE SET NULL;
 
ALTER TABLE FOTO_ESTABELECIMENTO ADD CONSTRAINT FK_FOTO_ESTABELECIMENTO_2
	FOREIGN KEY (fk_foto_id)
	REFERENCES FOTO (id)
	ON DELETE RESTRICT;
 
ALTER TABLE AVALIACAO_FOTO ADD CONSTRAINT FK_AVALIACAO_FOTO_1
	FOREIGN KEY (fk__avaliacao_id)
	REFERENCES _Avaliacao (id)
	ON DELETE SET NULL;
 
ALTER TABLE AVALIACAO_FOTO ADD CONSTRAINT FK_AVALIACAO_FOTO_2
	FOREIGN KEY (fk_foto_id)
	REFERENCES FOTO (id)
	ON DELETE SET NULL;
      
### 8	INSERT APLICADO NAS TABELAS DO BANCO DE DADOS<br>
  INSERT INTO USUARIO (nome, email, senha) 
    VALUES ('Kaio', ‘kaiomaromba123@gmail.com’, ‘batatinhafrita123’), 
            ('Adriano', ‘OAdriano.depresso@gmail.com’, ‘queroMorre!’),
            ('Daniel', ‘danielSuperonze@gmail.com', ‘EndouMelhorGoleiro!’),
            ('Isadora', ‘isa@gmail.com', ‘narutoPikachu2’);

INSERT INTO LOCAL (nome, descricao,  tipo_logradouro, nome_logradouro, cep, estado, cidade, bairro, numero, latitude, longitude)
    VALUES (‘Pizzaria bangalo’, ‘vendemos pizzas e temos espaço para recreação infantil’, ‘Av’, ’Alegria’, 52435552, ‘ES’, ‘Viana’, ‘Universal’, ‘666D’, ‘-20.383935’, ‘-40.466370’),
            (‘Flamengo artigos para festa’, ‘equipamentos para pesca’, ‘Rua’, ‘Dante Michelini’, 22222222, ‘PA’, ‘Gurigica’, ‘castanheira’, ‘35F’, ‘-20.272874’, ‘-40.279709’),
            (‘Casa de show Adriano’, ‘LOCAL PARA VC TRAZER TODA A SUA FAMILIA AMIGOS E FAMILIARESES PARA UM DIA REVIGORANTE PARA UM JANTAR EM PLENA LUZ D SOL COM ÓTIMOS PETISCOS PETISCOS PARA SEU PET SOMOS AMIGAVEIS COM NOT PET FRIENDLY!!’, ‘Avenida’, ‘Emancipacao’, 13184654, ‘SP’, ‘Hortolândia’, ‘Jardim Amanda’, ‘5000’, ‘-22.883950’, ‘-47.224187’),
            (‘Buerger Buergi’, ’O hambúrguer mais saboroso, com carnes suculentas, vários flavours de drinks clássicos da mixologia internacional (caipirinha, c* de burro). Ambiente bonito e climatizado.’, ‘Beco’, ‘Diagonal’, 12345678, ‘AM’, ‘Manaus’, ‘Oliveira Acre’, ‘2345MEIA78’, ‘-3.048206’, ‘-59.995185’);

INSERT INTO COMPLEMENTO(complemento)
    VALUES (‘proximo ao posto ipiranga’),
            (‘proximo a banca do seu ze’),
            (‘tocar campainha e subir pro segundo andar’),
            (‘NAO TEM’);

INSERT INTO ENTRETENIMENTO (tipo, descricao)
    VALUES (‘Boate’, ‘Boates, casas de festas’),
            (‘Parque’, ‘Parques de diversões, parques ao ar livre, parques para cachorros’),
            (‘Comida’, ‘Pizzaria, Hamburgueria, Fast foods, etc.’),
            (‘Pesca’, ‘Pesque e pague, Pesque e solte’);

INSERT INTO _Avaliacao(fk_usuario_id, fk_local_id, comentario, avaliacao)
    VALUES (1, 1, ‘pizza mt boa, recomendo’, 5),
            (1, 4, ‘um lixo’, 1),
            (2, 3, ‘Melhor casa de shows que tem’, 5),
            (3, 2, ‘Não existe lugar melhor que uma boa loja do flamengo com equipamentos para pesca. GABIGOL MEU HEROI’, 3);

INSERT INTO FOTO (data, url_foto)
    VALUES (‘24/03/2023’, ‘https://media-cdn.tripadvisor.com/media/photo-s/1a/f9/e2/8a/pizzaria-hermon.jpg’),
(‘01/01/2023’, ‘https://www.pescapinheiros.com.br/produtos/original/pinheiros-93252.jpg’),
            (‘30/05/2023’, ‘https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT6gV3x9a4XDZywzMrqr8WCzhQBigDLUc4jDVywMdAib5gEoWHJ-Nys_YooNC9I0haJaUs&usqp=CAU’),
            (‘16/09/2023’, ‘https://www.guiadasemana.com.br/contentFiles/image/opt_w840h0/villa-country-casa-de-shows.jpg’),
            (‘22/06/2023’, ‘https://conteudo.imguol.com.br/c/esporte/fe/2023/07/26/gabigol-comemora-gol-do-flamengo-sobre-o-gremio-em-partida-da-copa-do-brasil-1690420734992_v2_1920x1280.jpg’),
(‘01/02/2023’, ‘https://respostas.sebrae.com.br/wp-content/uploads/2022/02/set-hamburger-beer-french-fries-standard-set-drinks-food-pub-beer-snacks-dark-background-fast-food-traditional-american-food-scaled.jpg’),
(‘02/03/2022’, ‘https://assets.pokemon.com/assets/cms2/img/pokedex/full/025.png’),
(‘23/10/2019’, ‘https://gkpb.com.br/wp-content/uploads/2023/02/novo-capitao-pikachu-e1677251557266.jpg’);

INSERT INTO LOCAL_COMPLEMENTO (fk_local_id, fk_complemento_id)
    VALUES (1, 2),
            (2, 1),
            (3, 4),
            (4, 3);

INSERT INTO USUARIO_USUARIO(fk_usuario_id_seguido, fk_usuario_id_seguidor)
    VALUES (1, 2),
            (1, 3),
            (2, 1),
            (3, 4);

INSERT INTO ENTRETENIMENTO_LOCAL(fk_entretenimento_id, fk_local_id)
    VALUES (1, 3),
            (3, 1),
            (3, 4),
            (4, 3);

INSERT INTO USUARIO_ENTRETENIMENTO(fk_usuario_id, fk_entretenimento_id)
    VALUES (1, 2),
            (2, 3),
            (2, 2),
            (3, 1),
            (4, 1);

INSERT INTO FOTO_ESTABELECIMENTO(fk_local_id, fk_foto_id)
    VALUES (1, 1),
            (2, 2),
            (3, 4),
            (4, 6);

INSERT INTO AVALIACAO_FOTO(fk__avaliacao_id, fk_foto_id)
    VALUES (1, 7),
            (2, 3),
            (3, 8),
            (4, 5);


### 9	TABELAS E PRINCIPAIS CONSULTAS<br>
    OBS: Usa template da disciplina disponibilizado no Colab.<br>
#### 9.1	CONSULTAS DAS TABELAS COM TODOS OS DADOS INSERIDOS (Todas) <br>

#### 9.2	CONSULTAS DAS TABELAS COM FILTROS WHERE (Mínimo 4)<br>

#### 9.3	CONSULTAS QUE USAM OPERADORES LÓGICOS, ARITMÉTICOS E TABELAS OU CAMPOS RENOMEADOS (Mínimo 11)
    a) Criar 5 consultas que envolvam os operadores lógicos AND, OR e Not
    b) Criar no mínimo 3 consultas com operadores aritméticos 
    c) Criar no mínimo 3 consultas com operação de renomear nomes de campos ou tabelas

#### 9.4	CONSULTAS QUE USAM OPERADORES LIKE E DATAS (Mínimo 12) <br>
    a) Criar outras 5 consultas que envolvam like ou ilike
    b) Criar uma consulta para cada tipo de função data apresentada.

># Marco de Entrega 02: Do item 6. até o item 9.1 (5 PTS) <br>

#### 9.5	INSTRUÇÕES APLICANDO ATUALIZAÇÃO E EXCLUSÃO DE DADOS (Mínimo 6)<br>
    a) Criar minimo 3 de exclusão
    b) Criar minimo 3 de atualização

#### 9.6	CONSULTAS COM INNER JOIN E ORDER BY (Mínimo 6)<br>
    a) Uma junção que envolva todas as tabelas possuindo no mínimo 2 registros no resultado
    b) Outras junções que o grupo considere como sendo as de principal importância para o trabalho

#### 9.7	CONSULTAS COM GROUP BY E FUNÇÕES DE AGRUPAMENTO (Mínimo 6)<br>
    a) Criar minimo 2 envolvendo algum tipo de junção

#### 9.8	CONSULTAS COM LEFT, RIGHT E FULL JOIN (Mínimo 4)<br>
    a) Criar minimo 1 de cada tipo

#### 9.9	CONSULTAS COM SELF JOIN E VIEW (Mínimo 6)<br>
        a) Uma junção que envolva Self Join (caso não ocorra na base justificar e substituir por uma view)
        b) Outras junções com views que o grupo considere como sendo de relevante importância para o trabalho

#### 9.10	SUBCONSULTAS (Mínimo 4)<br>
     a) Criar minimo 1 envolvendo GROUP BY
     b) Criar minimo 1 envolvendo algum tipo de junção

># Marco de Entrega 03: Do item 9.2 até o ítem 9.10 (10 PTS)<br>

### 10 RELATÓRIOS E GRÁFICOS

#### a) análises e resultados provenientes do banco de dados desenvolvido (usar modelo disponível)
#### b) link com exemplo de relatórios será disponiblizado pelo professor no AVA
#### OBS: Esta é uma atividade de grande relevância no contexto do trabalho. Mantenha o foco nos 5 principais relatórios/resultados visando obter o melhor resultado possível.

    

### 11	AJUSTES DA DOCUMENTAÇÃO, CRIAÇÃO DOS SLIDES E VÍDEO PARA APRESENTAÇAO FINAL <br>

#### a) Modelo (pecha kucha)<br>
#### b) Tempo de apresentação 6:40 

># Marco de Entrega 04: Itens 10 e 11 (20 PTS) <br>
<br>
<br>




### 12 FORMATACAO NO GIT:<br> 
https://help.github.com/articles/basic-writing-and-formatting-syntax/
<comentario no git>
    
##### About Formatting
    https://help.github.com/articles/about-writing-and-formatting-on-github/
    
##### Basic Formatting in Git
    
    https://help.github.com/articles/basic-writing-and-formatting-syntax/#referencing-issues-and-pull-requests
    
    
##### Working with advanced formatting
    https://help.github.com/articles/working-with-advanced-formatting/
#### Mastering Markdown
    https://guides.github.com/features/mastering-markdown/

    
### OBSERVAÇÕES IMPORTANTES

#### Todos os arquivos que fazem parte do projeto (Imagens, pdfs, arquivos fonte, etc..), devem estar presentes no GIT. Os arquivos do projeto vigente não devem ser armazenados em quaisquer outras plataformas.
1. <strong>Caso existam arquivos com conteúdos sigilosos<strong>, comunicar o professor que definirá em conjunto com o grupo a melhor forma de armazenamento do arquivo.

#### Todos os grupos deverão fazer Fork deste repositório e dar permissões administrativas ao usuário do git "profmoisesomena", para acompanhamento do trabalho.

#### Os usuários criados no GIT devem possuir o nome de identificação do aluno (não serão aceitos nomes como Eu123, meuprojeto, pro456, etc). Em caso de dúvida comunicar o professor.


Link para BrModelo:<br>
http://www.sis4.com/brModelo/download.html
<br>


Link para curso de GIT<br>
![https://www.youtube.com/curso_git](https://www.youtube.com/playlist?list=PLo7sFyCeiGUdIyEmHdfbuD2eR4XPDqnN2?raw=true "Title")

