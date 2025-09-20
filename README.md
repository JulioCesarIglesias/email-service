# 📧 Email Service - Uber Challenge

[![Java](https://img.shields.io/badge/Java-21-blue)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5.5-green)](https://spring.io/projects/spring-boot)
[![Build](https://img.shields.io/badge/Build-Maven-orange)](https://maven.apache.org/)
[![License](https://img.shields.io/badge/License-MIT-lightgrey)](LICENSE)

Este projeto é um **serviço de backend para envio de e-mails**, desenvolvido como solução para o desafio de codificação da Uber, **"Email Service"**. O desenvolvimento foi baseado em uma videoaula da **Fernanda Kipper** ([link do vídeo](https://www.youtube.com/watch?v=eFgeO9M9lLw&list=PLNCSWIsR6ADKaT1cO6XUJkRy0_v9p-h0Z)), que demonstra a solução para o desafio original ([link do desafio](https://github.com/uber-archive/coding-challenge-tools/blob/master/coding_challenge.md)).

A arquitetura do projeto segue o padrão de **Clean Architecture**, dividindo a aplicação em camadas distintas para garantir **modularidade, testabilidade e separação de responsabilidades**. O serviço utiliza o **Amazon Simple Email Service (SES)** para envio de e-mails, integrando-se com a AWS para um gerenciamento eficiente e escalável das comunicações por e-mail.

## 🛠 Tecnologias Utilizadas
- **Java 21**
- **Spring Boot 3.5.5**
- **Amazon Web Services (AWS)**: serviço SES para envio de e-mails
- **Maven**: gerenciamento de dependências e build do projeto
- **Lombok**: para reduzir boilerplate de código
- **Spring Boot DevTools**: para facilitar o desenvolvimento
- **Spring Boot Starter Test**: testes unitários

## 📂 Estrutura do Projeto
O projeto segue a **Clean Architecture**, com as seguintes camadas:
- **adapters**: interfaces de gateway que conectam a aplicação à infraestrutura
- **application**: lógica de negócio do serviço
- **core**: entidades de negócio e casos de uso
- **controllers**: manipulação das requisições HTTP
- **infra**: detalhes de infraestrutura, como integração com AWS SES

## ⚙️ Configuração e Instalação
**Pré-requisitos**: JDK 21 ou superior, Maven, conta AWS com SES configurado, chave de acesso e chave secreta da AWS

1. Clone o repositório:
```bash
git clone https://github.com/JulioCesarIglesias/email-service.git
cd email-service
```  

2. Configure as credenciais da AWS no arquivo `src/main/resources/application.properties`:
```properties
spring.application.name=email-service
aws.accessKey=SEU_ACCESS_KEY
aws.secretKey=SEU_SECRET_KEY
aws.region=SUA_REGIAO
```
> Certifique-se de que a região corresponde à região onde o SES está habilitado.

3. Configure o endereço de e-mail de origem no arquivo `src/main/java/com/jci/email_service/infra/ses/SesEmailSender.java`:
```java
SendEmailRequest request = new SendEmailRequest()
    .withSource("seu-email-verificado@exemplo.com")
```
> O e-mail de origem deve ser verificado no AWS SES.

## 🏃 Execução do Projeto
1. Construa o projeto:
```bash
mvn clean install
```  
2. Execute a aplicação:
```bash
mvn spring-boot:run
```  
O serviço será iniciado na porta padrão do Spring Boot (**8080**).

## 📬 Como Utilizar a API
**Endpoint:** `POST /api/email`

**Corpo da requisição (JSON):**
```json
{
  "to": "destinatario@exemplo.com",
  "subject": "Assunto do E-mail",
  "body": "Conteúdo do corpo do e-mail."
}
```

**Exemplo usando curl:**
```bash
curl -X POST http://localhost:8080/api/email \
-H 'Content-Type: application/json' \
-d '{
  "to": "destinatario@exemplo.com",
  "subject": "E-mail de Teste",
  "body": "Olá, este é um e-mail de teste enviado pelo meu serviço!"
}'
```

**Resposta em caso de sucesso:**
- Status: 200 OK
- Body: "Email sent successfully"

**Resposta em caso de erro:**
- Status: 500 INTERNAL SERVER ERROR
- Body: "Error while sending email"

## 🤝 Contribuição
Sinta-se à vontade para **abrir issues** ou **enviar pull requests** para melhorar este projeto.

**Autor:** Júlio César Iglesias – Estudante e entusiasta de **backend com Spring**  
[LinkedIn](https://www.linkedin.com/in/juliocesariglesiasdev/) | [GitHub](https://github.com/JulioCesarIglesias)
