# mongodb
Atividade prática de MongoDB da pós de Data Science

Exercício 1 - Aquecendo com ospets

- 1.Adicione outro Peixe e um Hamster com nome Frodo
  - <code> db.pets.insert({name:"Frodo",species:"Peixe"})
db.pets.insert({name:"Frodo",species:"Hamster"})</code>

- 2.Faça uma contagem dos pets na coleção
  - <code> db.pets.count() </code>

- 3.Retorne apenas um elemento o método prático possível
  - <code> db.pets.findOne() </code>

- 4.Identifique o ID para o Gato Kilha.
  - <code> db.pets.find({name: "Kilha", species: "Gato"}) </code>

- 5.Faça uma busca pelo ID e traga o Hamster Mike
  - <code> db.pets.find("5e79261e8a63a9d3dc37b918") </code>

- 6.Use o find para trazer todos os Hamsters
  - <code> db.pets.find({species: "Hamster"}) </code>

- 7.Use o find para listar todos os pets com nome Mike
  - <code> db.pets.find({name: "Mike"}) </code>

- 8.Liste apenas o documento que é um Cachorro chamado Mike
  - <code> db.pets.find({name: "Mike", species: "Cachorro"}) </code>
  
  Exercício2–Mama mia!
  
- 1.Liste/Conte todas as pessoas que tem exatamente 99 anos. Você pode usar um count para indicar a quantidade.
  - <code> db.italians.find({age: 99}).count() </code>
  
- 2.Identifique quantas pessoas são elegíveis atendimento prioritário (pessoas com mais de 65 anos)
  - <code> db.italians.find({age: {"$gt":65}}).count() </code>
 
- 3.Identifique todos os jovens (pessoas entre 12 a 18 anos).
  - <code> db.italians.find({age: {"$gte":12, "$lte": 18}}).count() </code>

- 4.Identifique quantas pessoas tem gatos, quantas tem cachorro e quantas não tem nenhum dos dois
  - <code> db.italians.find({cat:{$exists:true}}).count() </code>
  - <code> db.italians.find({dog:{$exists:true}}).count() </code>
  - <code> db.italians.find({"$and":[{cat:{$exists:false}},{dog:{$exists:false}}]}).count() </code>

- 5.Liste/Conte todas as pessoas acima de 60 anos que tenham gato
  - <code> db.italians.find({"$and":[{age: {"$gt":60}}, {cat:{$exists:true}}]}).count() </code>

- 6.Liste/Conte todos os jovens com cachorro
  - <code> db.italians.find({"$and":[{age: {"$gte":12, "$lte": 18}}, {dog:{$exists:true}}]}).count() </code>

- 7.Utilizando o $where, liste todas as pessoas que tem gato e cachorro
  - <code> db.italians.find({$where: "this.cat && this.dog"}).count() </code>

- 8.Liste todas as pessoas mais novas que seus respectivos gatos.
  - <code> db.italians.find({ $and: [{ cat: { $exists: true }}, { $where: "this.age < this.cat.age" }]}).count() </code>

- 9.Liste as pessoas que tem o mesmo nome que seu bichano (gatou ou cachorro)
  - <code> db.italians.find ({$or: [{ $where: "this.cat && this.firstname == this.cat.name" }, { $where: "this.dog && this.firstname == this.dog.name" }]}).count() </code>

- 10.Projete apenas o nome e sobrenomedas pessoas com tipo de sangue de fator RH negativo
  - <code> db.italians.find({bloodType:/-/},{firstname:1,surname:1,_id:0}) </code>

- 11.Projete apenas os animais dos italianos. Devem ser listados os animais com nome e idade. Não mostre o identificado do mongo (ObjectId)
  - <code>  </code>

- 12.Quais são as 5 pessoas mais velhas com sobrenome Rossi?
  - <code>  </code>

- 13.Crie um italiano que tenha um leão como animal de estimação. Associe um nome e idade ao bichano
  - <code>  </code>

- 14.Infelizmente o Leão comeu o italiano. Remova essa pessoa usando o Id.
  - <code>  </code>

- 15.Passou um ano. Atualize a idade de todos os italianos e dos bichanos em 1.
  - <code>  </code>

- 16.O Corona Vírus chegou na Itália e misteriosamente atingiu pessoas somente com gatos e de 66 anos. Remova esses italianos.
  - <code>  </code>

- 17.Utilizando o framework agregate, liste apenas as pessoas com nomes iguais a sua respectiva mãe e que tenha gato ou cachorro.
  - <code>  </code>

- 18.Utilizando aggregate framework, faça uma lista de nomes única de nomes. Faça isso usando apenas o primeiro nome
  - <code>  </code>

- 19.Agora faça a mesma lista do item acima, considerando nome completo.
  - <code>  </code>

- 20.Procure pessoas que gosta de Banana ou Maçã, tenham cachorro ou gato, mais de 20 e menos de 60 anos.
  - <code>  </code>
