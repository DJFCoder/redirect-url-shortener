# URL Shortener Redirect API

## Overview

This project implements a serverless API for URL shortening using AWS Lambda and S3. It allows redirecting users from short URLs to the original URLs, with support for link expiration.

## Features

- Redirection from short URLs to original URLs
- URL expiration verification
- Data storage in S3 bucket
- Response with appropriate HTTP status codes

## Architecture

The application consists of:

1. **AWS Lambda Function**: Processes HTTP requests and performs the redirection
2. **Amazon S3**: Stores the mapping data between short URLs and original ones
3. **Data Model**: Representation of URL data with expiration time

## How It Works

1. User accesses a short URL (e.g., `https://yourdomain.com/abc123`)
2. The Lambda function is invoked and extracts the short URL code from the request path
3. The function fetches the corresponding JSON file from the S3 bucket (`abc123.json`)
4. If the file is found, the function verifies if the URL has expired
5. If the URL is valid, the API returns an HTTP 302 redirect to the original URL
6. If the URL has expired, the API returns an HTTP 410 status (Gone)

## File Structure

- `Main.java`: Main class that implements the Lambda function handler
- `UrlData.java`: Model class for URL data

## Storage Format

Data is stored in S3 as JSON files with the following format:

```json
{
    "originalUrl": "https://full-original-url.com/path",
    "expirationTime": 1640995200
}
```

Where `expirationTime` is the Unix timestamp (in seconds) that defines when the URL expires.

## Technologies Used

- Java
- AWS Lambda
- Amazon S3
- Jackson (for JSON processing)
- Lombok (for boilerplate reduction)
- AWS SDK for Java v2

## Requirements

- JDK 11 or higher
- Maven
- AWS CLI configured with appropriate credentials
- S3 bucket configured for data storage

## Configuration

To use this application, you need to:

1. Create an S3 bucket named `url-shortener-devjf` (or change the name in the code)
2. Configure Lambda to be triggered by HTTP requests via API Gateway
3. Set up the necessary permissions for Lambda to access the S3 bucket

## Limitations

- Does not include the functionality to create short URLs (only redirection)
- Does not include authentication or authorization mechanisms
- Does not have access metrics or analytics system

- ---

# Redirecionamento de URL Encurtada (pt-br)

## Visão Geral

Este projeto implementa uma API serverless para encurtamento de URLs utilizando AWS Lambda e S3. Ele permite redirecionar usuários de URLs curtas para as URLs originais, com suporte para expiração de links.

## Funcionalidades

- Redirecionamento de URLs curtas para URLs originais
- Verificação de expiração de URLs
- Armazenamento de dados em bucket S3
- Resposta com status HTTP apropriados

## Arquitetura

A aplicação é composta por:

1. **AWS Lambda Function**: Processa as requisições HTTP e realiza o redirecionamento
2. **Amazon S3**: Armazena os dados de mapeamento entre URLs curtas e originais
3. **Modelo de dados**: Representação dos dados de URL com tempo de expiração

## Como Funciona

1. O usuário acessa uma URL curta (ex: `https://seudominio.com/abc123`)
2. A função Lambda é invocada e extrai o código da URL curta do caminho da requisição
3. A função busca o arquivo JSON correspondente no bucket S3 (`abc123.json`)
4. Se o arquivo for encontrado, a função verifica se a URL expirou
5. Se a URL for válida, a API retorna um redirecionamento HTTP 302 para a URL original
6. Se a URL estiver expirada, a API retorna um status HTTP 410 (Gone)

## Estrutura de Arquivos

- `Main.java`: Classe principal que implementa o handler da função Lambda
- `UrlData.java`: Classe de modelo para os dados da URL

## Formato de Armazenamento

Os dados são armazenados no S3 como arquivos JSON com o seguinte formato:

```json
{
    "originalUrl": "https://url-original-completa.com/caminho",
    "expirationTime": 1640995200
}
```

Onde `expirationTime` é o timestamp Unix (em segundos) que define quando a URL expira.

## Tecnologias Utilizadas

- Java
- AWS Lambda
- Amazon S3
- Jackson (para processamento JSON)
- Lombok (para redução de boilerplate)
- AWS SDK para Java v2

## Requisitos

- JDK 11 ou superior
- Maven
- AWS CLI configurado com credenciais apropriadas
- Bucket S3 configurado para armazenamento dos dados

## Configuração

Para utilizar esta aplicação, você precisa:

1. Criar um bucket S3 chamado `url-shortener-devjf` (ou alterar o nome no código)
2. Configurar o Lambda para ser acionado por requisições HTTP via API Gateway
3. Configurar as permissões necessárias para o Lambda acessar o bucket S3

## Limitações

- Não inclui a funcionalidade de criação de URLs curtas (apenas o redirecionamento)
- Não inclui mecanismos de autenticação ou autorização
- Não possui sistema de métricas ou analytics de acesso
