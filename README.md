# mongodb
Atividade prática de MongoDB da pós de Data Science

Exercício 1 - Aquecendo com ospets

- 1.Adicione outro Peixe e um Hamster com nome Frodo
  - <code> db.pets.insert({name:"Frodo",species:"Peixe"})
db.pets.insert({name:"Frodo",species:"Hamster"})</code>

- 2.Faça uma contagem dos pets na coleção
  - <code> db.pets.count() </code>
  - Resultado: 8

- 3.Retorne apenas um elemento o método prático possível
  - <code> db.pets.findOne() </code>

- 4.Identifique o ID para o Gato Kilha.
  - <code> db.pets.find({name: "Kilha", species: "Gato"}) </code>
  - Resultado: ObjectId("5e7926348a63a9d3dc37b91a")

- 5.Faça uma busca pelo ID e traga o Hamster Mike
  - <code> db.pets.find("5e79261e8a63a9d3dc37b918") </code>
  - Resultado: { "_id" : ObjectId("5e79261e8a63a9d3dc37b918"), "name" : "Mike", "species" : "Hamster" }

- 6.Use o find para trazer todos os Hamsters
  - <code> db.pets.find({species: "Hamster"}) </code>
  - Resultado: { "_id" : ObjectId("5e79261e8a63a9d3dc37b918"), "name" : "Mike", "species" : "Hamster" }
{ "_id" : ObjectId("5e7926a68a63a9d3dc37b91f"), "name" : "Frodo", "species" : "Hamster" }

- 7.Use o find para listar todos os pets com nome Mike
  - <code> db.pets.find({name: "Mike"}) </code>
  - Resultado: { "_id" : ObjectId("5e79261e8a63a9d3dc37b918"), "name" : "Mike", "species" : "Hamster" }
{ "_id" : ObjectId("5e79263b8a63a9d3dc37b91b"), "name" : "Mike", "species" : "Cachorro" }

- 8.Liste apenas o documento que é um Cachorro chamado Mike
  - <code> db.pets.find({name: "Mike", species: "Cachorro"}) </code>
  - Resultado: { "_id" : ObjectId("5e79263b8a63a9d3dc37b91b"), "name" : "Mike", "species" : "Cachorro" }
