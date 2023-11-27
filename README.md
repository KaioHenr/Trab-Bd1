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
  ![Alt text](https://github.com/KaioHenr/Trab-Bd1/blob/main/conceito.png)
    
    
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
  ![Alt text](https://github.com/KaioHenr/Trab-Bd1/blob/main/logico.png)

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
    fk_local_id integer,
    complemento varchar(200)
);

CREATE TABLE ENTRETENIMENTO (
    id serial PRIMARY KEY,
    tipo varchar(30),
    descricao varchar(200)
);

CREATE TABLE Avaliacao (
    id serial PRIMARY KEY,
    fk_usuario_id integer,
    fk_local_id integer,
    comentario varchar(200),
    avaliacao smallint,
    	data date
);

CREATE TABLE FOTO (
    id serial PRIMARY KEY,
    data date,
    url_foto varchar(400)
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
    fk_Avaliacao_id integer,
    fk_foto_id integer
);

ALTER TABLE COMPLEMENTO ADD CONSTRAINT FK_COMPLEMENTO_1
    FOREIGN KEY (fk_local_id)
    REFERENCES LOCAL (id);
 
ALTER TABLE Avaliacao ADD CONSTRAINT FKAvaliacao_2
    FOREIGN KEY (fk_usuario_id)
    REFERENCES USUARIO (id);
 
ALTER TABLE Avaliacao ADD CONSTRAINT FKAvaliacao_3
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
 
ALTER TABLE AVALIACAO_FOTO ADD CONSTRAINT FKAvaliacao_FOTO_1
    FOREIGN KEY (fk_Avaliacao_id)
    REFERENCES Avaliacao (id)
    ON DELETE SET NULL;
 
ALTER TABLE AVALIACAO_FOTO ADD CONSTRAINT FKAvaliacao_FOTO_2
    FOREIGN KEY (fk_foto_id)
    REFERENCES FOTO (id)
    ON DELETE SET NULL;

      
### 8	INSERT APLICADO NAS TABELAS DO BANCO DE DADOS<br>
INSERT INTO USUARIO (nome, email, senha) VALUES ('Kaio', 'kaiomaromba123@gmail.com', 'batatinhafrita123'), ('Adriano', 'OAdriano.depresso@gmail.com', 'queroMorre!'), ('Daniel', 'danielSuperonze@gmail.com', 'EndouMelhorGoleiro!'), ('Isadora', 'isa@gmail.com', 'narutoPikachu2');

INSERT INTO USUARIO (nome, email, senha) VALUES
    ('Kaio', 'kaiomaromba123@gmail.com', 'batatinhafrita123'),
    ('Adriano', 'OAdriano.depresso@gmail.com', 'queroMorre!'),
    ('Daniel', 'danielSuperonze@gmail.com', 'EndouMelhorGoleiro!'),
    ('Isadora', 'isa@gmail.com', 'narutoPikachu2'),
    ('Lucas', 'lucas@gmail.com', 'senha123'),   
    ('Amanda', 'amanda@yahoo.com', 'amandaSenha'),   
    ('Rafael', 'rafael@hotmail.com', 'rafaelPass'),   
    ('Fernanda', 'fernanda@gmail.com', 'senhaFer123'),   
    ('Pedro', 'pedro@gmail.com', 'pedroPass'),   
    ('Cristina', 'cristina@gmail.com', 'senhaCris567'),   
    ('Eduardo', 'eduardo@yahoo.com', 'senhaEdu789'),   
    ('Mariana', 'mariana@hotmail.com', 'marianaPass'),   
    ('Carlos', 'carlos@gmail.com', 'senhaCarlos12'),   
    ('Ana', 'ana@yahoo.com', 'anaSenha'),   
    ('Gabriel', 'gabriel@hotmail.com', 'senhaGabi345'),   
    ('Juliana', 'juliana@gmail.com', 'julianaPass'),   
    ('Rodrigo', 'rodrigo@yahoo.com', 'rodrigoSenha'),   
    ('Patricia', 'patricia@gmail.com', 'patriciaPass'),   
    ('Hugo', 'hugo@hotmail.com', 'senhaHugo678');

INSERT INTO LOCAL (nome, descricao, tipo_logradouro, nome_logradouro, cep, estado, cidade, bairro, numero, latitude, longitude) VALUES
    ('Pizzaria bangalo', 'vendemos pizzas e temos espaço para recreação infantil', 'Av', 'Alegria', 52435552, 'ES', 'Viana', 'Universal', '666D', '-20.383935', '-40.466370'),
    ('Flamengo artigos para festa', 'equipamentos para pesca', 'Rua', 'Dante Michelini', 22222222, 'PA', 'Gurigica', 'castanheira', '35F', '-20.272874', '-40.279709'),
    ('Casa de show Adriano', 'LOCAL PARA VC TRAZER TODA A SUA FAMILIA AMIGOS E FAMILIARESES PARA UM DIA REVIGORANTE PARA UM JANTAR EM PLENA LUZ D SOL COM ÓTIMOS PETISCOS PETISCOS PARA SEU PET SOMOS AMIGAVEIS COM NOT PET FRIENDLY!!', 'Avenida', 'Emancipacao', 13184654, 'SP', 'Hortolândia', 'Jardim Amanda', '5000', '-22.883950', '-47.224187'),
    ('Buerger Buergi', 'O hambúrguer mais saboroso, com carnes suculentas, vários flavours de drinks clássicos da mixologia internacional (caipirinha, c* de burro). Ambiente bonito e climatizado.', 'Beco', 'Diagonal', 12345678, 'AM', 'Manaus', 'Oliveira Acre', '2345MEIA78', '-3.048206', '-59.995185'),
      ('Teatro Municipal', 'Espaço cultural para apresentações artísticas', 'Rua', 'São João', 12345678, 'SP', 'São Paulo', 'Centro', '123', '-23.550520', '-46.633308'),
      ('Biblioteca Municipal', 'Local para leitura e estudos', 'Avenida', 'Cultural', 98765432, 'RJ', 'Rio de Janeiro', 'Copacabana', '456', '-22.967739', '-43.186005'),
      ('Parque da Cidade', 'Área verde com trilhas e áreas de lazer', 'Parque', 'Aeroporto', 54321098, 'DF', 'Brasília', 'Asa Sul', '789', '-15.794157', '-47.882529'),
      ('Museu de Arte Contemporânea', 'Exposições de arte moderna', 'Rua', 'Oscar Niemeyer', 13579246, 'RJ', 'Niterói', 'Icaraí', '246', '-22.902520', '-43.124682'),
      ('Cinema Paradiso', 'Cinema com exibições de filmes clássicos e independentes', 'Rua', 'Cineasta', 45678901, 'SP', 'São Paulo', 'Vila Madalena', '789A', '-23.553687', '-46.681102'),
      ('Praia do Futuro', 'Praia com barracas e opções de lazer', 'Avenida', 'Dioguinho', 98765432, 'CE', 'Fortaleza', 'Praia do Futuro', '1020', '-3.724034', '-38.477009'),
      ('Planetário Municipal', 'Observatório astronômico e projeções sobre o universo', 'Avenida', 'Galáxia', 14725836, 'RS', 'Porto Alegre', 'Jardim Botânico', '3030', '-30.035151', '-51.214697'),
      ('Zoológico Nacional', 'Parque com variedade de animais', 'Estrada', 'Dos Animais', 36985214, 'MG', 'Belo Horizonte', 'Pampulha', '123', '-19.854808', '-43.971797'),
      ('Arena Esportiva', 'Local para eventos esportivos e shows', 'Rodovia', 'Esportiva', 95175384, 'SC', 'Florianópolis', 'Centro', '456', '-27.595378', '-48.548050'),
      ('Galeria de Arte Moderna', 'Exposições de artistas contemporâneos', 'Rua', 'Das Artes', 78945612, 'BA', 'Salvador', 'Barra', '789B', '-12.979161', '-38.503327'),
      ('Aquário Nacional', 'Exposição de vida marinha e aquática', 'Avenida', 'Dos Peixes', 36914725, 'PE', 'Recife', 'Boa Viagem', '987', '-8.107506', '-34.893511'),
      ('Centro de Convenções', 'Local para eventos e convenções', 'Avenida', 'Das Convenções', 25836914, 'PR', 'Curitiba', 'Centro', '654', '-25.429568', '-49.266214'),
      ('Estádio Municipal', 'Campo de futebol e palco de eventos esportivos', 'Rua', 'Do Esporte', 14796385, 'GO', 'Goiânia', 'Setor Bueno', '321', '-16.680904', '-49.256966'),
      ('Jardim Botânico', 'Área verde com espécies botânicas diversas', 'Avenida', 'Botânico', 75315928, 'AM', 'Manaus', 'Parque 10', '1010', '-3.113844', '-60.023756'),
      ('Casa de Cultura', 'Espaço dedicado à promoção cultural', 'Praça', 'Cultural', 36914725, 'RN', 'Natal', 'Cidade Alta', '456', '-5.794477', '-35.210013');

INSERT INTO COMPLEMENTO(fk_local_id, complemento) VALUES
    (1, 'proximo ao posto ipiranga'),
    (2, 'proximo a banca do seu ze'),
    (3, 'tocar campainha e subir pro segundo andar'),
    (4, 'NAO TEM'),
    (5, 'Bloco A, Apt 302'),
    (6, 'Próximo à Praça Principal'),
    (7, 'Fundos do edifício'),
    (8, 'Atrás da árvore grande'),
    (9, 'Perto da entrada principal'),
    (11, 'Ao lado da escola estadual'),
    (13, 'Piso superior, Sala 15');

INSERT INTO ENTRETENIMENTO (tipo, descricao) VALUES
    ('Boate', 'Boates, casas de festas'),
    ('Parque', 'Parques de diversões, parques ao ar livre, parques para cachorros'),
    ('Comida', 'Pizzaria, Hamburgueria, Fast foods, etc.'),
    ('Pesca', 'Pesque e pague, Pesque e solte'),
    ('Boate', 'Boa pista de dança e excelente seleção musical'),
    ('Parque de Diversões', 'Atrações emocionantes para todas as idades'),
    ('Restaurante Temático', 'Ambiente temático com menu exclusivo'),
    ('Casa de Shows', 'Apresentações ao vivo e ótima atmosfera'),
    ('Clube Noturno', 'Música ao vivo e área VIP disponível'),
    ('Teatro', 'Produções teatrais de alta qualidade'),
    ('Lounge de Jazz', 'Ambiente sofisticado com música jazz ao vivo');

INSERT INTO Avaliacao(fk_usuario_id, fk_local_id, comentario, avaliacao, data) VALUES
	(1, 1, 'pizza mt boa, recomendo', 5, '2022/10/01'),
	(1, 4, 'um lixo', 1, '1958/10/01'),
	(2, 3, 'Melhor casa de shows que tem', 5, '2000/05/01'),
	(3, 2, 'Não existe lugar melhor que uma boa loja do flamengo com equipamentos para pesca. GABIGOL MEU HEROI', 3, '2022/02/19'),
	(5, 6, 'Ambiente agradável e comida deliciosa', 4, '2014/08/17'),
	(2, 9, 'Excelente atendimento, recomendo!', 5, '2016/11/23'),
	(7, 14, 'Show de bola! Recomendo a todos', 4, '2012/10/11'),
	(8, 11, 'Lugar muito bonito, mas a comida poderia ser melhor', 3, '2022/12/15'),
	(12, 16, 'Atendimento rápido e eficiente', 5, '2020/05/11'),
	(13, 18, 'Ótima opção para um passeio em família', 4, '2018/06/24'),
	(10, 3, 'Muito bom, principalmente para quem gosta de esportes', 5, '2017/07/19'),
	(9, 4, 'Adorei a exposição de arte contemporânea', 4, '2021/09/26'),
	(6, 7, 'Aquário incrível, muitas espécies diferentes', 5, '2020/07/30'),
	(14, 2, 'Bom lugar para eventos e convenções', 3, '2016/09/18'),
	(15, 1, 'Participar de um jogo no estádio é uma experiência única', 4, '2020/05/15'),
	(16, 5, 'Jardim Botânico bem cuidado e com plantas variadas', 5, '2022/10/09'),
	(17, 8, 'Casa de Cultura promove eventos culturais interessantes', 4, '2012/10/01'),
	(18, 9, 'Estádio bem localizado e de fácil acesso', 3, '2022/10/16'),
	(19, 12, 'Zoológico com muita diversidade de animais', 5, '2022/09/01'),
	(1, 15, 'Boate com boa música e ambiente animado', 2, '2020/10/01'),
	(2, 14, 'Parque com brinquedos emocionantes', 3, '2022/10/16'),
	(3, 18, 'Hamburgueria com opções deliciosas', 4, '2022/12/01'),
	(4, 1, 'Ótimo lugar para a prática da pesca esportiva', 3, '2016/10/01'),
	(5, 16, 'Boate com ambiente descontraído', 5, '2022/10/16'),
	(6, 12, 'Parque com áreas verdes e trilhas', 2, '2022/08/01'),
	(7, 3, 'Pizzaria com sabores incríveis', 4, '2022/10/13'),
	(8, 6, 'Cinema com ótima seleção de filmes', 3, '2022/03/01'),
	(9, 8, 'Praia com estrutura e opções de lazer', 5, '2022/01/01'),
	(10, 13, 'Planetário com projeções impressionantes', 4, '2022/02/01'),
	(11, 4, 'Zoológico com animais encantadores', 2, '2013/10/01'),
	(12, 2, 'Arena esportiva para grandes eventos', 3, '2022/08/01'),
	(13, 11, 'Galeria de Arte Moderna com exposições inspiradoras', 4, '2022/10/08'),
	(14, 7, 'Aquário com variedade de peixes e animais aquáticos', 5, '2022/06/01'),
	(15, 18, 'Centro de Convenções para eventos diversos', 2, '2017/10/01'),
	(16, 5, 'Estádio com atmosfera vibrante', 4, '2022/10/11'),
	(17, 9, 'Jardim Botânico com paisagens exuberantes', 5, '2019/10/01'),
	(18, 15, 'Casa de Cultura com programação cultural rica', 3, '2013/10/01'),
	(19, 1, 'Estádio com infraestrutura moderna', 5, '2022/05/01'),
	(1, 3, 'Ótimo atendimento, recomendo!', 5, '2022/10/13'),
	(2, 6, 'Local agradável para eventos esportivos', 4, '2022/10/19'),
	(3, 9, 'Adorei a exposição de arte contemporânea', 5, '2021/10/01'),
	(4, 12, 'Excelente cinema, ótima seleção de filmes', 4, '2022/10/16'),
	(5, 15, 'Pizza deliciosa, ambiente familiar', 5, '2010/10/01'),
	(6, 18, 'Praia movimentada, ótimas barracas', 3, '2009/10/01'),
	(7, 2, 'Observatório incrível, recomendo a visita', 5, '2000/10/01'),
	(8, 5, 'Zoológico bem cuidado, muitas opções de animais', 4, '2002/10/01'),
	(9, 10, 'Arena esportiva moderna, show de eventos', 5, '2003/10/01'),
	(10, 11, 'Galeria com obras incríveis, artistas talentosos', 4, '2009/10/01'),
	(11, 14, 'Aquário com variedade de peixes, boa infraestrutura', 4, '2006/10/01'),
	(12, 17, 'Centro de convenções espaçoso e bem equipado', 3, '2007/10/01');

INSERT INTO FOTO (data, url_foto) VALUES
	('2023/03/24', 'https://media-cdn.tripadvisor.com/media/photo-s/1a/f9/e2/8a/pizzaria-hermon.jpg'),
	('2023/01/01', 'https://www.pescapinheiros.com.br/produtos/original/pinheiros-93252.jpg'),
	('2023/05/30', 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT6gV3x9a4XDZywzMrqr8WCzhQBigDLUc4jDVywMdAib5gEoWHJ-Nys_YooNC9I0haJaUs&usqp=CAU'),
	('2023/09/16', 'https://www.guiadasemana.com.br/contentFiles/image/opt_w840h0/villa-country-casa-de-shows.jpg'),
	('2023/06/22', 'https://conteudo.imguol.com.br/c/esporte/fe/2023/07/26/gabigol-comemora-gol-do-flamengo-sobre-o-gremio-em-partida-da-copa-do-brasil-1690420734992_v2_1920x1280.jpg'),
	('2023/01/02', 'https://respostas.sebrae.com.br/wp-content/uploads/2022/02/set-hamburger-beer-french-fries-standard-set-drinks-food-pub-beer-snacks-dark-background-fast-food-traditional-american-food-scaled.jpg'),
	('2022/02/03', 'https://assets.pokemon.com/assets/cms2/img/pokedex/full/025.png'),
	('2019/10/23', 'https://gkpb.com.br/wp-content/uploads/2023/02/novo-capitao-pikachu-e1677251557266.jpg'),
	('2021/03/19', 'https://ddragon.leagueoflegends.com/cdn/img/champion/splash/Kindred_0.jpg'),
	('1999/01/10', 'https://img.freepik.com/vetores-gratis/fundo-a-tecnologia-moderna_1035-4314.jpg?size=626&ext=jpg&ga=GA1.1.921908989.1700334646&semt=sph'),
	('2010/10/10', 'https://img.freepik.com/fotos-gratis/um-homem-em-um-terno-de-neon-esta-sentado-em-uma-cadeira-com-um-letreiro-de-neon-que-diz-a-palavra_188544-27011.jpg?size=626&ext=jpg&uid=R88527489&ga=GA1.1.921908989.1700334646&semt=ais'),
	('2001/04/15',  'https://img.freepik.com/fotos-gratis/figura-triangular-geometrica-legal-em-uma-luz-de-laser-neon-otima-para-fundos-e-papeis-de-parede_181624-9331.jpg?size=626&ext=jpg&uid=R88527489&ga=GA1.1.921908989.1700334646&semt=ais'),
	('1657/12/14', 'https://img.freepik.com/fotos-gratis/figura-triangular-geometrica-fantastica-em-uma-luz-de-laser-neon-otima-para-fundos_181624-11068.jpg?size=626&ext=jpg&uid=R88527489&ga=GA1.1.921908989.1700334646&semt=ais'),
	('2014/08/13', 'https://img.freepik.com/fotos-gratis/figura-triangular-geometrica-fantastica-em-uma-luz-de-laser-neon-otima-para-fundos_181624-11068.jpg?size=626&ext=jpg&uid=R88527489&ga=GA1.1.921908989.1700334646&semt=ais'),
	('2015/10/14', 'https://img.freepik.com/fotos-gratis/a-ascensao-dos-humanoides-com-ia-generativa-de-capacetes-avancados_8829-2877.jpg?size=626&ext=jpg&uid=R88527489&ga=GA1.1.921908989.1700334646&semt=ais'),
	('2013/09/20', 'https://img.freepik.com/fotos-gratis/vista-lateral-mulher-feliz-vencendo-no-videogame_23-2149349981.jpg?size=626&ext=jpg&uid=R88527489&ga=GA1.1.921908989.1700334646&semt=ais'),
	('2022/07/15', 'https://example.com/photo31.jpg'),
	('2022/12/05', 'https://example.com/photo32.jpg'),
	('2023/04/02', 'https://example.com/photo33.jpg'),
	('2021/08/20', 'https://example.com/photo34.jpg'),
	('2022/11/18', 'https://example.com/photo35.jpg'),
	('2023/02/14', 'https://example.com/photo36.jpg'),
	('2021/06/30', 'https://example.com/photo37.jpg'),
	('2023/01/20', 'https://example.com/photo38.jpg'),
	('2022/09/08', 'https://example.com/photo39.jpg'),
	('2022/03/12', 'https://example.com/photo40.jpg'),
	('2023/08/25', 'https://example.com/photo41.jpg'),
	('2022/05/10', 'https://example.com/photo42.jpg'),
	('2023/11/05', 'https://example.com/photo43.jpg'),
	('2021/09/28', 'https://example.com/photo44.jpg');




INSERT INTO USUARIO_USUARIO(fk_usuario_id_seguido, fk_usuario_id_seguidor) VALUES
    (1, 2),
    (1, 3),
    (2, 1),
    (3, 4),
    (5, 6),
    (7, 8),
    (9, 10),
    (11, 12),
    (13, 14),
    (15, 16),
    (17, 18),
    (19, 1),
    (2, 4),
    (5, 7),
    (8, 10),
    (12, 14),
    (16, 18),
    (19, 3),
    (1, 5),
    (6, 8),
    (10, 12),
    (14, 16),
    (18, 2),
    (3, 1),
    (7, 9),
    (11, 13),
    (15, 17),
    (19, 4),
    (2, 6),
    (8, 12),
    (10, 14),
    (16, 3),
    (18, 5),
    (1, 7),
    (9, 11),
    (13, 15),
    (17, 19),
    (4, 2),
    (6, 10),
    (12, 15),
    (16, 8),
    (19, 11),
    (3, 5),
    (7, 10),
    (11, 15),
    (15, 9),
    (2, 4),
    (6, 18),
    (4, 5),
    (4, 14);

INSERT INTO ENTRETENIMENTO_LOCAL(fk_entretenimento_id, fk_local_id) VALUES
    	(1, 3),
    	(3, 1),
    	(3, 4),
	(4, 3),
	(2, 3),
	(5, 7),
	(11, 15),
	(4, 2),
	(8, 6),
	(1, 10),
	(10, 19);

INSERT INTO USUARIO_ENTRETENIMENTO(fk_usuario_id, fk_entretenimento_id) VALUES
	(1, 2),
	(2, 3),
	(2, 2),
	(3, 1),
	(4, 1),
	(1, 5),
	(3, 5),
	(7, 11),
	(2, 4),
	(6, 8),
	(10, 1),
	(15, 10);

INSERT INTO FOTO_ESTABELECIMENTO(fk_local_id, fk_foto_id) VALUES
	(1, 1),
	(2, 2),
	(3, 3),
	(4, 4),
	(5, 5),
	(6, 6),
	(7, 7),
	(8, 8),
	(9, 9),
	(10, 10),
	(11, 11),
	(12, 12),
	(13, 13),
	(14, 14),
	(15, 15);

INSERT INTO AVALIACAO_FOTO(fk_Avaliacao_id, fk_foto_id) VALUES
    (1, 16),
    (2, 17),
    (3, 18),
    (4, 19),
    (9, 20),
    (10, 21),
    (11, 22),
    (15, 23),
    (16, 24),
    (22, 25),
    (24, 26),
    (29, 27),
    (30, 28),
    (33, 29),
    (39, 30);

