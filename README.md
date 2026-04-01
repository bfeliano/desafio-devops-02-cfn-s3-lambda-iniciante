# 🧩 Desafio DevOps #02 — S3 + Lambda com CloudFormation (Nível Iniciante)

Este é o segundo desafio da série **Desafios DevOps**, criado para ajudar iniciantes a praticar conceitos fundamentais de **Infraestrutura como Código (IaC)** utilizando **AWS CloudFormation**.

Neste desafio, você criará um fluxo serverless simples composto por:

*   Um **S3 Bucket**
*   Uma **função Lambda**
*   Uma **IAM Role** básica para execução da Lambda
*   Uma **notificação de eventos do S3**, acionando a Lambda sempre que um arquivo for enviado ao bucket
*   Logs da execução no **CloudWatch Logs**

A proposta deste repositório é oferecer um ambiente prático para estudo.  
👉 a pasta **desafio/** contém os arquivos para você implementar  
👉 a pasta **solucao/** contém a implementação final

## 🤝 Participe da Comunidade

Tem dúvidas sobre o desafio ou quer compartilhar sua solução?  
Entre no nosso Discord oficial:

[![Discord](https://img.shields.io/badge/Discord-Desafios%20DevOps-5865F2?style=flat&logo=discord&logoColor=white)](https://discord.gg/RgcC7YytVZ)

Lá você encontrará fóruns por desafio, ajuda da comunidade e novidades sobre próximos desafios DevOps.

Divirta-se aprendendo DevOps com CloudFormation! ☁️💻🔥

## 📁 Estrutura do Repositório

```
desafio-devops-02-cfn-s3-lambda-iniciante/
│
├── desafio/       → Onde você deve escrever seu template CloudFormation
├── solucao/       → Solução completa e funcional
└── README.md      → Este arquivo
```

## 📌 Como completar o seu desafio?

Todo o desenvolvimento do seu código deve ser feito dentro da pasta:

```
/desafio
```
Nela você encontrará um README com instruções detalhadas, dicas e, quando necessário, arquivos auxiliares para te orientar na construção da solução.

Quando terminar ou quiser comparar a sua abordagem, a solução final está disponível em:

```
/solucao
```

## 🛠️ Pré-requisitos

Antes de começar, certifique-se de ter:

- **AWS CLI** configurado (`aws configure`)  
  Instalação: https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html  
  Configuração: https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html

- **Conta AWS** com permissões básicas de:
  * CloudFormation
  * S3
  * Lambda
  * IAM
  * CloudWatch Logs

## 🔜 Próximos Passos

Este desafio faz parte de uma trilha contínua de aprendizado DevOps.

Depois de concluir este nível, você poderá avançar para:

➡️ **Desafio DevOps #02 — Nível Intermediário** *(em breve)*  
Nele você irá aprimorar esta mesma infraestrutura adicionando **Parameters**, **Mappings**, **Conditions**, IAM mais detalhado e boas práticas avançadas de CloudFormation.

## 🤝 Contribuições

Pull requests com melhorias em documentação, estrutura ou sugestões para novos desafios são bem-vindos!

## 📄 Licença

Este projeto está sob a licença MIT. Consulte o arquivo `LICENSE` para mais detalhes.
