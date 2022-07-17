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

Nessa demonstração construiremos uma aplicação para manter o hanking de avaliações de livros. Cada registro será composto do nome do livro, o autor e a avaliação.

| Título   |      Autor      |  Avaliação |
|----------|:-------------:|------:|
| O senhor dos Anéis |  J.R.R. Tolkien | 10 |
| A morte de Artur |    Thomas Malory   |   9 |


```kotlin
implementation("software.amazon.awssdk:dynamodb:2.17.209"
```

```kotlin
data class Book(val title: String, 
                val author: String, 
                val rating: Number)
```

```kotlin

@Value("\${aws.key}")
val key: String? = null
@Value("\${aws.secret}")
val secret: String? = null
@Value("\${aws.region}")
val region: String? = null
@Value("\${aws.endpoint}")
val endpoint: String? = null
```

```kotlin
@Bean
fun awsCredentials(): AwsBasicCredentials = AwsBasicCredentials.create(key, secret)
```

```kotlin
@Bean
fun dynamoDbAsyncClient(awsBasicCredentials: AwsBasicCredentials): DynamoDbAsyncClient = DynamoDbAsyncClient
    .builder()
    .credentialsProvider(StaticCredentialsProvider.create(awsBasicCredentials))
    .region(Region.of(region))
    .endpointOverride(URI.create(endpoint!!))
    .build()
}
```