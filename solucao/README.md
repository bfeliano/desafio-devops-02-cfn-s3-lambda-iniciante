# ✅ Solução — Desafio DevOps #02 — S3 + Lambda com CloudFormation (Nível Iniciante)

Parabéns por chegar até aqui!  
Esta é a solução completa do **Desafio DevOps #02 — CloudFormation Iniciante**, onde o objetivo era criar um fluxo simples utilizando **S3 e Lambda** com template YAML.

A seguir você encontrará uma explicação clara sobre o que foi implementado, como testar, como remover os recursos e quais são os próximos passos na trilha DevOps.

## 🎯 O que foi implementado nesta solução?

Esta solução inclui todos os recursos solicitados no desafio:

### ✔ 1. **S3 Bucket**
Um bucket S3 é criado com nome estável, baseado no AccountId e na região.  
Ele está configurado para disparar notificações de evento sempre que um arquivo é criado (`s3:ObjectCreated:*`).

### ✔ 2. **Função Lambda (inline)**
A função Lambda foi criada diretamente dentro do template, usando `ZipFile`.  
Ela:

- Recebe o evento enviado pelo S3
- Extrai o nome do arquivo e do bucket
- Loga as informações no CloudWatch Logs
- Retorna uma mensagem indicando processamento

### ✔ 3. **IAM Role para a Lambda**
Uma IAM Role mínima foi configurada para permitir que a Lambda escreva logs no CloudWatch.

### ✔ 4. **Lambda Permission**
Recurso `AWS::Lambda::Permission` autorizando o S3 a invocar a função Lambda.

### ✔ 5. **Outputs**

- Nome do bucket S3
- ARN da função Lambda

Eles ajudam bastante durante testes e futuras evoluções do template.

## 📄 Arquivo principal desta solução

O template final está no arquivo:

```
template.yaml
```

Ele contém todos os recursos necessários para o funcionamento do fluxo **S3 → Lambda**.

## ▶️ Como executar esta solução

### 1. Valide o template

```bash
aws cloudformation validate-template --template-body file://template.yaml
```

### 2. Faça o deploy do stack

```bash
aws cloudformation deploy \
  --template-file template.yaml \
  --stack-name desafio-devops-02-iniciante \
  --capabilities CAPABILITY_NAMED_IAM
```

### 3. Suba um arquivo para testar o evento

```bash
aws s3 cp arquivo.txt s3://desafio-devops-02-<ACCOUNT_ID>-<REGION>/
```

### 4. Verifique os logs da Lambda

```bash
aws logs tail /aws/lambda/desafio-devops-02-lambda-<ACCOUNT_ID>-<REGION> --follow
```

Você deverá ver algo parecido com:

```bash
Evento recebido:
Arquivo recebido: template.yaml no bucket desafio-devops-02-123456789123-us-east-1
```

## 🧹 Como destruir a infraestrutura

Para apagar completamente a infraestrutura criada:

```bash
aws s3 rm s3://desafio-devops-02-<ACCOUNT_ID>-<REGION> --recursive
aws cloudformation delete-stack --stack-name desafio-devops-02-iniciante
```

## 📌 Observações importantes

- O bucket recebe **DeletionPolicy: Delete**, então ele será removido ao deletar a stack (somente se estiver vazio).  
- O nome do bucket depende do **AccountId** e da **região**, garantindo unicidade.  
- A Lambda usa **runtime Python 3.13**.  

## 🔜 Próximos Passos

Se você concluiu este desafio e revisou a solução, o próximo passo é avançar para:

➡️ [**Desafio DevOps #02 — Nível Intermediário**](https://github.com/bfeliano/desafio-devops-02-cfn-s3-lambda-intermediario)  

Neste próximo nível, você irá evoluir esta mesma infraestrutura, aplicando práticas mais avançadas de CloudFormation, incluindo:

- Parameters
- Mappings
- Variáveis de ambiente para a Lambda
- Políticas IAM mais refinadas
- Integração com SNS para envio de notificações

Se quiser discutir esta solução ou compartilhar sua própria implementação, participe da comunidade no Discord!  
Link: <https://discord.gg/RgcC7YytVZ>

Bom estudo e continue evoluindo na trilha DevOps! 🚀🔥