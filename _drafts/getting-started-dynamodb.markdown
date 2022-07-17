---
layout: post
title:  "Primeiros passos com DynamoDB"
date:   2022-08-01 18:00:00 -0300
categories: kotlin dynamodb
---

# Primeiros passos com DynamoDB

## Contextualização

A escolha de uma nova stack geralemte é feita considerando que trará um desempenho melhor do que a stack "padrão" ou mais utilizada pela equipe. Um fator importante para aplicações é o tempo de leitura de dado. Esse tempo pode variar bastante dependendo da tecnologia escolhida. Quando falamos de rapidez e escalabilidade para leitura de dados, podemos citar o DynamoDb. O DynamoDB é um banco de dados NoSQL oferecido pela AWS que promete desempenho e escalabilidade, asegurando que os dados são criptografados e os backups são automáticos.

## Projeto

Nessa demonstração criaremos uma aplicação para manter o hanking de avaliações de livros.

```kotlin
implementation("software.amazon.awssdk:dynamodb:2.17.209"
```

