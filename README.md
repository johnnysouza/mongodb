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
  - <code> db.italians.find({bloodType:/-/},{firstname:1, surname:1, _id:0}) </code>

- 11.Projete apenas os animais dos italianos. Devem ser listados os animais com nome e idade. Não mostre o identificado do mongo (ObjectId)
  - <code> db.italians.find({$where: "this.cat && this.dog"}, {"cat.name":1, "cat.age":1, "dog.name":1, "dog.age":1, _id:0}) </code>

- 12.Quais são as 5 pessoas mais velhas com sobrenome Rossi?
  - <code> db.italians.find({surname:"Rossi"}).sort({age:-1}).limit(5) </code>

- 13.Crie um italiano que tenha um leão como animal de estimação. Associe um nome e idade ao bichano
  - <code> db.italians.insert({
    firstname:"Pedro",
    surname:"Di Paula",
    username:"lasanha123",
    age:37,
    lion:{name:"simba", age:7}
    }) </code>

- 14.Infelizmente o Leão comeu o italiano. Remova essa pessoa usando o Id.
  - <code> db.italians.find({"lion": {$exists: true})
    db.italians.remove("5e7a8797b59d369ea00ba376") </code>

- 15.Passou um ano. Atualize a idade de todos os italianos e dos bichanos em 1.
  - <code> db.italians.update({}, {"$inc": {"age": 1}}, {multi: true}) 
    db.italians.update({cat: {$exists: true}}, {$inc: {"cat.age": 1}}, {multi: true})
    db.italians.update({dog: {$exists: true}}, {$inc: {"dog.age": 1}}, {multi: true})
  </code>

- 16.O Corona Vírus chegou na Itália e misteriosamente atingiu pessoas somente com gatos e de 66 anos. Remova esses italianos.
  - <code> db.italians.remove({$and:[{cat: {$exists: true}}, {age: 66}]}) </code>

- 17.Utilizando o framework agregate, liste apenas as pessoas com nomes iguais a sua respectiva mãe e que tenha gato ou cachorro.
  - <code> db.italians.aggregate([    
  {$match: { mother: { $exists: 1}}},     
  {$match: { $or: [{ cat: { $exists: true }}, { dog: { $exists: true }}]}},     
  {$project: { firstname:1, _id:0, sameNameWithMom: {$eq: ["$firstname","$mother.firstname"]}}},    
  {$match: {sameNameWithMom: true}} ]) </code>

- 18.Utilizando aggregate framework, faça uma lista de nomes única de nomes. Faça isso usando apenas o primeiro nome
  - <code> db.italians.aggregate([{$group: { _id: "$firstname"}}]) </code>

- 19.Agora faça a mesma lista do item acima, considerando nome completo.
  - <code> db.italians.aggregate([{"$group": { "_id": { firstname: "$firstname", surname: "$surname" }}}]) </code>

- 20.Procure pessoas que gosta de Banana ou Maçã, tenham cachorro ou gato, mais de 20 e menos de 60 anos.
  - <code> db.italians.aggregate([    
{$match: { favFruits: {$all:["Banana", "Maçã"]}}},  
{$match: { $or: [{ cat: { $exists: true }}, { dog: { $exists: true }}]}},
{$match: { age: {$gt:20, $lt: 60}}},
{$project: {firstname:1, _id:0}}
]) </code>

Exercício3-Stockbrokers

- 1.Liste as ações com profit acima de 0.5 (limite a 10 o resultado)
  <code> db.stocks.find({"Profit Margin": {$gt: 0.5}}, {_id: 0, Ticker: 1, "Profit Margin": 1, "Company": 1}).limit(10) </code>
  
- 2.Liste as ações com perdas (limite a 10 novamente)
  <code> db.stocks.find({"Profit Margin": {$lt: 0}}, {_id: 0, Ticker: 1, "Profit Margin": 1, "Company": 1}).limit(10) </code>
  
- 3.Liste as 10 ações mais rentáveis 
  <code> db.stocks.find({"Profit Margin": {$exists: true}}, {_id: 0, Ticker: 1, "Profit Margin": 1, "Company": 1}).sort({"Profit Margin": -1}).limit(10) </code>
  
- 4.Qual foi o setor mais rentável?
  <code> db.stocks.aggregate([{$group: {_id: "$Sector", "Total profits": {$sum: "$Profit Margin"} }}, {$sort: {"Total profits": -1}}]) </code>
  
- 5.Ordene as ações pelo profit e usando um cursor, liste as ações.
  <code> var bigger_profit = db.stocks.find({"Profit Margin": {$exists: true}}, {_id: 0, Ticker: 1, "Profit Margin": 1, "Company": 1}) </code>
  <code> bigger_profit = bigger_profit.sort({"Profit Margin": -1}) </code>
  
- 6.Renomeie o campo “Profit Margin” para apenas “profit”.
  <code> db.stocks.update({"Profit Margin": { $exists: true }}, { $rename: {"Profit Margin": "Profit"}}, {multi: true}) </code>
  
- 7.Agora liste apenas a empresa e seu respectivo resultado
  <code> db.stocks.find({"Profit": {$exists: true}}, {_id: 0, "Company": 1, "Profit": 1}) </code>
  
- 8.Analise as ações. É uma bola de cristal na sua mão... Quais as três ações você investiria?
  - Escolhi as com melhores margem, desde que não estejam endividas demais hehe
  <code> db.stocks.find({$and: [{"Profit": {$exists: true}}, {"Total Debt/Equity": {$lt: 3}}]}, {_id: 0, Ticker: 1, "Profit": 1, "Company": 1, "Total Debt/Equity": 1}).sort({"Profit": -1}).limit(3) </code>
  
- 9.Liste as ações agrupadas por setor
  <code> db.stocks.aggregate([ {$group: {_id: "$Sector", items: { $addToSet: {Company: "$Company", Profit: "$Profit"}}}}]) </code>
 
Exercício3 –FraudenaEnron!

1.Liste as pessoas que enviaram e-mails (de forma distinta, ou seja, sem repetir). Quantas pessoas são?
  - <code> var senders = db.enron.distinct("sender") </code>
  - <code> senders.length </code>
  
2.Contabilize quantos e-mails tem a palavra “fraud”
  - <code> db.enron.find({text: { $regex: ".fraud."}}).count() </code>
