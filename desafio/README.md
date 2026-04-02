# 🧩 Desafio DevOps #02 — S3 + Lambda com CloudFormation (Nível Iniciante)

Bem-vindo(a) ao segundo desafio da série **Desafios DevOps**!  
Aqui você irá praticar conceitos essenciais de **Infraestrutura como Código (IaC)** utilizando **AWS CloudFormation** para criar um fluxo simples de processamento de arquivos com **S3 → Lambda**.

Este desafio é ideal para quem está começando com CloudFormation ou quer reforçar como eventos e permissões funcionam em arquiteturas serverless.

## 🎯 Objetivo

Dentro desta pasta (`/desafio`), você deve criar um **template CloudFormation** chamado:

```
template.yaml
```

O objetivo é implementar uma solução composta por:

1. Um **bucket S3**
2. Uma **função Lambda** (código python fornecido abaixo)
3. Uma **IAM Role** mínima para a Lambda
4. Uma **notificação de eventos S3** que dispare a Lambda quando um arquivo for enviado
5. Outputs úteis (ex.: ARN da Lambda, nome do bucket)

# 💬 Dicas importantes para te ajudar

## 💡 1. Como começar um template CloudFormation?
Você pode aprender a declarar a estrutura básica aqui:

📘 **Documentação — Estrutura básica do template**  
https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-formats.html

Seu template deve começar com algo assim:

```yaml
AWSTemplateFormatVersion: 2010-09-09
Description: Desafio DevOps 02 — CloudFormation Iniciante
Resources:
  # Seus recursos vão aqui
```

## 💡 2. Onde encontrar a documentação de cada recurso?

- [**S3 Bucket**](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-s3-bucket.html)
- [**S3 Bucket Notifications**](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-s3-bucket-notificationconfig.html)
- [**AWS Lambda Function**](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html)
- [**IAM Role para Lambda**](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-iam-role.html)
- [**Permissão para S3 invocar Lambda**](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-permission.html)

Use essas páginas como referência enquanto constrói seu template.

## 💡 3. Função Lambda pronta (copie e cole)

Salve a função inline dentro do recurso Lambda no campo `Code → ZipFile`.

```python
import json
import urllib.parse
import boto3

s3 = boto3.client('s3')

def lambda_handler(event, context):
    print("Evento recebido:")
    print(json.dumps(event))

    # Pega o bucket e o arquivo enviado
    record = event['Records'][0]
    bucket = record['s3']['bucket']['name']
    key = urllib.parse.unquote_plus(record['s3']['object']['key'])

    print(f"Arquivo recebido: {key} no bucket {bucket}")

    return {
        'statusCode': 200,
        'body': json.dumps(f"Processado com sucesso: {key}")
    }
```

Essa Lambda não precisa fazer nada complexo — o objetivo é ver os logs no CloudWatch.

## 💡 4. Ordem sugerida para construir o template

Para facilitar:

1.  Declare o **bucket S3**
2.  Declare a **IAM Role** usada pela Lambda
3.  Declare a **Lambda Function**
4.  Declare a **Lambda Permission**  
    Para permitir que o S3 invoque a Lambda
5.  Configure o **NotificationConfiguration** do S3 apontando para a Lambda
6.  Adicione **Outputs**
7.  Faça deploy e teste com:
    ```bash
    aws s3 cp arquivo.txt s3://<bucket-name>
    ```

# ▶️ Como testar seu template

1.  Valide:

```bash
aws cloudformation validate-template --template-body file://template.yaml
```

2.  Faça o deploy:

```bash
aws cloudformation deploy \
  --template-file template.yaml \
  --stack-name desafio-devops-02 \
  --capabilities CAPABILITY_NAMED_IAM
```

3. Envie um arquivo para o bucket:

```bash
aws s3 cp arquivo.txt s3://desafio-devops-02-<ACCOUNT_ID>-<REGION>/
```

4.  Veja os logs da Lambda:

```bash
aws logs tail /aws/lambda/desafio-devops-02-lambda-<ACCOUNT_ID>-<REGION> --follow
```

# 🧹 Como destruir a infraestrutura

```bash
aws cloudformation delete-stack --stack-name desafio-devops-02
```

# ❗ Quando consultar a solução?

Apenas depois que você tentar resolver sozinho(a).  
A solução completa está na pasta solucao.


Boa sorte e divirta-se aprendendo DevOps na prática! 🚀🔥