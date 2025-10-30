# 🚀 Bootcamp Santander Code Girls 2025

Este repositório reúne o andamento das atividades realizadas durante o **Bootcamp Santander Code Girls 2025**.  
O objetivo é registrar aprendizados, atividades práticas e anotações pessoais ao longo do curso.  

---

## 📂 Estrutura do Repositório

Por enquanto:
- `README.md` → Documento principal com progresso, resumo dos módulos e links.  

Futuramente:
- Pastas organizadas por módulos/atividades 
- Scripts, códigos, exercícios resolvidos

---

## ✅ Progresso dos Módulos

| Status | Módulo | Tópicos |
|--------|--------|---------|
| ✅ | [Introdução à AWS e Conceitos Básicos](#-introdução-à-aws-e-conceitos-básicos) | - Introdução à AWS e ao Universo da Computação em Nuvem <br> - Fundamentos de Infraestrutura AWS <br> - Configurando a Conta AWS: Segurança e Eficiência <br> - Acesso seguro e controle de custos |
| ✅ | [Computação na Nuvem com EC2](#-computação-na-nuvem-com-ec2) | - Instâncias EC2 e Otimização de Recursos AWS <br> - Gerenciando Instâncias EC2 AWS |
| ✅ | [Criando Recursos na AWS](#-criando-recursos-na-aws) | - Formas de acesso à AWS <br> - Criando uma instância EC2 <br> - Criando Bucket no Amazon S3 <br> - Criando Função com Amazon Lambda |
| ✅ | [Redes na AWS](#-redes-na-aws) | - Amazon VPC (Virtual Private Cloud) <br> - Amazon Subnet <br> - Amazon Security Group <br> - Amazon Route 53 <br> - Amazon CloudFront <br> - Amazon Elastic Load Balancer (ELB) |
| ⬜ | [Banco de Dados na AWS](#-banco-de-dados-na-aws) | — |
| ⬜ | [Serviços de Armazenamento e CDN](#-serviços-de-armazenamento-e-cdn) | — |
| ⬜ | [Serviços Intermediários e Avançados](#-serviços-intermediários-e-avançados) | — |
| ⬜ | [Gerenciamento e Governança na AWS](#-gerenciamento-e-governança-na-aws) | — |
| ⬜ | [Segurança na AWS](#-segurança-na-aws) | — |
| ⬜ | [Desenvolvimento e Ferramenta](#-desenvolvimento-e-ferramenta) | — |
| ⬜ | [Automação e DevOps na AWS](#-automação-e-devops-na-aws) | — |

---

## 📘 Detalhes dos Módulos

## 🌐 Introdução à AWS e Conceitos Básicos

---

## 💻 Computação na Nuvem com EC2

### 🔹 Amazon EC2 (Elastic Compute Cloud)
- Máquinas virtuais (servidores) na AWS, com Windows ou Linux.  
- Compostas por: CPU, memória, disco, rede e sistema operacional.  
- Modelo **IaaS** → AWS cuida da infraestrutura física (energia, cabeamento, hardware) e da segurança básica, mas a **configuração e uso são responsabilidade do cliente**.  
  - AWS protege a infraestrutura e oferece firewall (grupos de segurança, portas, IPs, protocolos).  
  - Cliente deve configurar corretamente o acesso (evitar exposição pública desnecessária). 
- É possível **upgrade/downgrade** de instância conforme necessidade.    

#### Escolha de Instância
- Sempre considerando **custo x necessidade real**.  
- Exemplos:  
  - Web app simples → não precisa de GPU ou RAM muito alta.  
  - Jump server (acesso a rede privada) → instância pequena e econômica.  
- Avaliar se é possível **desligar em horários ociosos** (fim de expediente/finais de semana).  

#### Famílias de Instâncias (tipos principais)
- **General Purpose (A1, T2, M4):** uso geral, pequenas aplicações e servidores web.  
- **Compute Optimized (C4):** processamento intensivo em CPU.  
- **Memory Optimized (R4, X1, z1d):** aplicações que exigem muita RAM (ex.: SAP, Spark).  
- **Accelerated Computing (P2, G3, F1):** aprendizado de máquina, gráficos, aceleração por hardware.  
- **Storage Optimized (H1, I3, D2):** grande volume de dados, NoSQL, data warehousing.  

#### Tipos de Contratação
- **On-Demand:** uso sob demanda, pagamento por hora/segundo.  
- **Spot:** instâncias ociosas da AWS com desconto (interrompíveis).  
- **Reserved:** contratadas por longo prazo (1 ou 3 anos), mais baratas.  


### 📦 Armazenamento com EBS e S3

#### Amazon EBS (Elastic Block Store)
- Armazenamento em blocos altamente confiável e expansível.  
- Funciona como um **HD externo** para as instâncias **EC2**.  
- Cada instância já possui um volume (para o SO), mas é possível anexar novos volumes EBS.  
- Permite **upgrade/downgrade** rápido e tem alta disponibilidade.  

##### Exemplos de uso:  
- Bancos de dados (MySQL, PostgreSQL, Oracle): Volume raiz → O EBS pode ser usado como o volume raiz para a instância EC2 que executa o servidor do banco de dados, garantindo que o sistema operacional e as configurações do banco de dados sejam persistentes. É a principal forma de armazenar os arquivos de dados, logs e tabelas do MySQL. Isso garante que os dados permaneçam mesmo se a instância EC2 for encerrada. 
- Pode criar **snapshots** para backup e restaurar em outras regiões. Os snapshots do EBS criam backups incrementais ponto a ponto dos volumes, armazenando-os de forma durável no Amazon S3. Em caso de falha, um novo volume EBS pode ser restaurado a partir de um snapshot, permitindo a recuperação rápida do banco de dados. Funcionam como uma foto de um disco rígido em um momento específico. **Armazenados no S3, em uma matriz separada do EBS.** Possível configurar frequência de snapshots para backup automático. Usados em estratégias de Disaster Recovery (DR) → podem ser armazenados em regiões remotas.   
- Backup de ambientes de produção (homologação às vezes, testes normalmente não). 

##### Volumes SSD
Para bancos de dados que exigem alta performance de E/S, é importante considerar volumes SSD como:
  - gp3 (SSD de uso geral): Oferece um bom equilíbrio entre preço e performance para a maioria das cargas de trabalho.
  - io2 Block Express (SSD de IOPS provisionadas): Recomendado para bancos de dados de missão crítica que precisam de latência muito baixa e alta performance sustentada.

#### Amazon S3 (Simple Storage Service)
Serviço de **armazenamento de objetos** em nuvem, seguro e escalável. O S3 funciona como uma **caixa (bucket)** onde você guarda arquivos (objetos).    
- Ideal para armazenar e recuperar grandes volumes de dados.  
- Muito usado em pipelines de processamento, exportação/importação de arquivos e integração com outros serviços (ex.: Lambda, EC2).  
- **Custo:** pagar pelo armazenamento + leitura/download dos dados.  
- Permite configurar **lifecycle policies** para mover objetos automaticamente entre classes de armazenamento.  
- Disponibilidade: **99,999999999% (11 9’s)** de durabilidade.  

Cada bucket pode ter **regras, triggers e permissões** específicas, e costuma ser usado em fluxos de automação de processamento de dados, como:
- Entrada de arquivos (pasta “input” ou “entrada”)  
- Processamento automático via **Lambda Functions**  
- Movimentação de arquivos para pastas de “processado”  
- Envio de resultados para outros serviços (ex: DynamoDB, SQS)

##### Exemplo de uso:
Uma empresa (como redes de pagamento ou fast food) que exporta arquivos posicionais (arquivos com cabeçalho, rodapé e colunas fixas, comuns em sistemas bancários). Esses arquivos são enviados periodicamente via **AWS CLI** para uma **pasta de entrada** no S3, e assim que chegam, um **Lambda Function** (em Node.js ou Python) é acionado automaticamente para processá-los, validar o conteúdo e enviá-los para uma fila do **Amazon SQS**. Posteriormente, outro Lambda lê essa fila e grava as informações processadas em um banco de dados **DynamoDB**.
Esse tipo de arquitetura serverless é bastante comum em pipelines de dados e automação de sistemas corporativos.

##### Principais Classes de Armazenamento
- **S3 Standard:** acesso frequente, baixa latência, alta disponibilidade.  
- **S3 Standard-IA (Infrequent Access):** acesso esporádico, custo menor.  
- **S3 One Zone-IA:** acesso esporádico, armazenado em uma única zona de disponibilidade (mais barato).  
- **S3 Glacier:** baixo custo para arquivamento, recuperação mais lenta.  
- **S3 Glacier Deep Archive:** ainda mais barato, para retenção de longo prazo (anos).  
- **S3 Intelligent-Tiering:** alterna automaticamente entre classes conforme o padrão de acesso.  

##### Boas Práticas
- Armazenar logs pouco acessados em classes IA ou Glacier para reduzir custos.  
- Criar alertas para acessos relevantes em vez de ler logs constantemente.  
- Usar lifecycle para mover dados antigos automaticamente.  

### ⚙️ Gerenciamento de Instâncias EC2
Os conceitos relacionados ao EBS e S3 foram retomados nesse módulo do curso devido a alta conexão com a existência e usabilidade do EC2, mas as principais informações sobre esses serviços já estão descritas em [📦 Armazenamento com EBS e S3](#-armazenamento-com-ebs-e-s3).

#### Criação e Uso de Imagens AMI

Uma **AMI (Amazon Machine Image)** é uma imagem de máquina pré-configurada, com:  
- Sistema Operacional.  
- Servidores e aplicações instaladas.  
- Configurações específicas do ambiente.  

Permite replicar e escalar ambientes de forma consistente.  

##### Principais pontos  
- **Criação:** AMIs podem ser criadas a partir de instâncias em execução ou paradas.  
- **AMIs públicas e privadas:** AWS oferece diversas AMIs públicas prontas para uso, mas também é possível criar AMIs privadas personalizadas.  
- **Personalização:** instalar softwares, ajustar configurações, e depois salvar como AMI.  
- **Lançamento de instâncias:** para criar novas EC2 basta escolher uma AMI → ela fornece os volumes raiz e permissões de inicialização.  
- **Tipos de AMIs:** Amazon Linux, Windows, entre outros.  

##### Exemplo de uso
Um sistema de backoffice utilizado por vários funcionários.  
- Cria-se uma instância, configura tudo (sistema, apps).  
- Gera-se uma AMI e replica-se para múltiplas instâncias idênticas.

##### Diferença entre AMI e Snapshots 
- **AMI (Amazon Machine Image):** backup completo de um servidor inteiro, incluindo todos os volumes EBS anexados.  
- **Snapshot EBS:** backup pontual de um único volume específico.  

---

## 🛠️ Criando Recursos na AWS
### 🌐 Formas de Acesso à AWS

Há diversas maneiras de criar e gerenciar recursos dentro da AWS. As principais são:

- **AWS Management Console:** interface gráfica via navegador, também chamada de *AWS Console*, voltada para operações manuais.  
- **AWS CloudShell:** ambiente de terminal dentro do próprio navegador, baseado em Linux e com ferramentas da AWS pré-instaladas (como Python, AWS CLI e Git). Permite criar e gerenciar recursos via linha de comando, sem precisar instalar nada localmente.  
- **AWS CLI (Command Line Interface):** ferramenta de linha de comando instalada localmente, usada para executar comandos e automatizar tarefas. É indicada para **automação e scripts**, diferentemente do Console e do CloudShell, que são mais voltados para configurações manuais.

#### Criação de Usuários e Chaves de Acesso (IAM)

A criação de chaves de acesso permite autenticar e usar a AWS CLI ou SDKs com permissões específicas de um usuário IAM.
  Passos:
    1. Acesse **IAM → Users → [usuário desejado] → Security Credentials → Access Keys → Create Access Key**.  
    2. Copie a **Access Key ID** e a **Secret Access Key** geradas.  
    3. Configure a CLI no terminal com:

      ```bash
      aws configure
      ```

    4. Durante a configuração, informe:

      ```bash
      AWS Access Key ID [None]: <sua_access_key_id>
      AWS Secret Access Key [None]: <sua_secret_access_key>
      Default region name [None]: us-west-2
      Default output format [None]: json
      ```

    5. Verifique se a instalação e configuração foram concluídas corretamente:

      ```bash
      aws --version
      cat ~/.aws/credentials
      cat ~/.aws/config
      aws sts get-caller-identity
      aws configure list
      ```

    Esses comandos confirmam que as credenciais estão salvas e que a CLI consegue autenticar com a conta IAM configurada.

##### Boas práticas
- Sempre use usuários IAM (nunca a conta root).
- Conceda apenas as permissões necessárias.
- Para permitir que usuários alterem suas próprias senhas, associe a política IAMUserChangePassword aos grupos adequados.

#### 🖥️ Criando e Acessando uma instância EC2
O Amazon EC2 (Elastic Compute Cloud) permite criar máquinas virtuais na nuvem. A criação pode ser feita manualmente pelo Console da AWS ou de forma automatizada via CLI.

  Passos (via Console):
    1. Acesse o serviço EC2 no Console AWS e clique em Launch Instance.
    2. Defina:
      - **Nome** da instância.
      - **AMI (Amazon Machine Image):** selecione o sistema operacional (por exemplo, Amazon Linux 2023, Ubuntu, Windows Server).
      - **Tipo de instância:** escolha conforme o uso e orçamento (ex: t2.micro é elegível ao nível gratuito).
      - **Par de chaves (Key Pair):** crie ou selecione uma existente (usada para acesso SSH).
      - **Configuração de rede:** defina o grupo de segurança (portas e regras de acesso).
      - **Armazenamento:** defina o volume (geralmente 8 GiB padrão).

    3. Revise as configurações e clique em Launch Instance.

##### Acessando a Instância
Depois de criada, a instância aparecerá no painel Instances com status Running. Clique sobre ela para ver detalhes como IP público, tipo de instância, VPC, subnet e grupo de segurança.

  Para se conectar:
    1. Clique em **Connect**, dentro da página da instância.
    2. Escolha o método:
      - **EC2 Instance Connect:** acesso via navegador, sem precisar configurar SSH.
      - **SSH Client:** acesso via terminal (Linux/Mac) ou PuTTY (Windows).
      - **Session Manager:** acesso sem chaves SSH, utilizando permissões do IAM.

      **Exemplo de conexão SSH:**

        ```bash
        chmod 400 "minha_chave.pem"
        ssh -i "minha_chave.pem" ec2-user@ec2-xx-xx-xx-xx compute-1.amazonaws.com
        ```

      *Se a instância não tiver par de chaves associado, o acesso via SSH não será possível. Use o EC2 Instance Connect ou configure um perfil IAM com permissões do Systems Manager (como explicado no tópico anterior [Criação de Usuários e Chaves de Acesso (IAM)](#-criacao-de-usuarios-e-chaves-de-acesso)).

##### Verificando a Instância
Dentro da instância, é possível executar comandos como:

  ```bash
  top     # mostra processos e uso de CPU/memória
  pwd     # mostra o diretório atual
  curl google.com  # testa conectividade com a Internet
  ```

Esses comandos ajudam a verificar se a instância está operacional e conectada à rede.

### 🪣 Criando Bucket no Amazon S3

O **Amazon S3 (Simple Storage Service)** é um serviço de armazenamento de objetos na nuvem da AWS. Lembrando que, pode ser usado tanto para **armazenamento de arquivos estáticos** (como imagens, logs, backups, sites estáticos) quanto para **processamento de grandes volumes de dados** — especialmente quando combinado com outros serviços, como **AWS Lambda**, **SQS**, **SNS** e **DynamoDB**.

#### Formas de Enviar Arquivos ao S3

Os arquivos podem ser enviados para o S3 de várias formas:

- **Via AWS Console:** upload manual pelo navegador.  
- **Via AWS CLI:** com comandos de linha, como:

  ```bash
  aws s3 cp arquivo.txt s3://meu-bucket/entrada/
  ```

- **Via automação:** (ex: sistemas Java, Spring Batch, Python, Node.js) integrados à API da AWS.

#### Criando o Bucket

Para criar um bucket no Console da AWS:
  1. Acesse o serviço S3 → Create Bucket.
  2. Defina as opções principais:
    - **Bucket name:** precisa ser único globalmente (não pode haver dois com o mesmo nome em toda a AWS).
    - **Region:** buckets são regionais, ou seja, pertencem a uma região específica (ex: us-east-1).
    - **Bucket type:** escolha entre General Purpose (uso comum) ou Directory Bucket (acesso via namespace).
    - **Object Ownership:** define o controle de propriedade (ACLs podem ser habilitadas se necessário).
    - **Public access settings:** permite ou bloqueia acesso público.
    - **Versioning:** ativa controle de versões de objetos (útil para histórico de alterações).
    - **Tags:** adicione identificadores para organização e cobrança.
    - **Encryption:** escolha entre:
      - SSE-S3: chaves gerenciadas pelo S3.
      - SSE-KMS: chaves gerenciadas pelo KMS.
      - DSSE-KMS: dupla camada de criptografia.
      - Também é possível ativar Bucket Keys para reduzir custos de chamadas KMS.

Após configurar, clique em **Create Bucket**.

#### Armazenando e Gerenciando Objetos
Ao clicar dentro do bucket recém-criado, você pode:
  - Fazer upload de arquivos do seu computador para a nuvem.
  - Criar pastas internas, como /entrada e /processado.
  - Definir Storage Class para cada arquivo (Standard, Glacier, Deep Archive etc.).
  - Ativar versionamento individual para cada objeto.

Durante o upload, o destino será exibido como:

  ```bash
  s3://nome-do-bucket/nome-do-arquivo
  ```
Cada arquivo também terá:
  - Um ARN (Amazon Resource Name)
  - Uma S3 URI
  - Uma Object URL (caso pública)

Exemplo:

  ```bash
  S3 URI: s3://cursoawsfundamentals/DiagramasEC2.png
  Region: us-east-1
  ARN: arn:aws:s3:::cursoawsfundamentals/DiagramasEC2.png
  URL pública: https://cursoawsfundamentals.s3.amazonaws.com/DiagramasEC2.png
  ```

**Se, ao acessar a URL pública, aparecer uma mensagem de AccessDenied, isso significa que o bucket ou o objeto não é público.
Para resolver, ajuste as permissões em Permissions → Bucket Policy ou desative o bloqueio de acesso público.

#### Permissões e Acesso Público
Buckets e objetos podem ser configurados para permitir acesso público.
Porém, ao marcar a opção “Block all public access”, o conteúdo não poderá ser acessado via Internet, mesmo que haja uma bucket policy liberando o acesso.

Para hospedar um site estático no S3 (como uma página index.html):
  1. Crie o bucket.
  2. Faça upload dos arquivos do site (index.html, style.css, etc.).
  3. Vá em Properties → Static Website Hosting → Enable.
  4. Configure a página inicial (index.html) e a de erro (error.html).
  5. Ajuste as permissões para permitir acesso público ao conteúdo.

Assim, o site poderá ser acessado via:

  ```bash
  http://nome-do-bucket.s3-website-us-east-1.amazonaws.com
  ```

#### Access Points
O S3 também permite criar Access Points, que são endpoints nomeados para acessar o bucket de forma controlada e escalável.
Eles são úteis quando várias aplicações ou contas precisam interagir com o mesmo bucket, simplificando a política de acesso.

Cada access point tem:
  1. Um nome exclusivo (único em toda a AWS).
  2. Um ARN próprio.
  3. Configurações individuais de permissão e rede (por exemplo, restrito a uma VPC).

### ⚙️ Criando Função com Amazon Lambda
#### O que é Serveless
Serverless é um paradigma de computação em que o desenvolvedor não precisa gerenciar servidores. O provedor de nuvem (no caso, a AWS) é responsável por todo o provisionamento, escalonamento e manutenção da infraestrutura.
Isso não significa que não existem servidores, mas sim que o gerenciamento deles é totalmente automatizado. Com o modelo serverless, o foco passa a ser apenas o código e a lógica de negócio.

#### Serviços Serveless na AWS
A AWS oferece vários serviços baseados em arquitetura serverless:
  - Amazon S3: armazenamento de arquivos.
  - Amazon DynamoDB: banco de dados NoSQL totalmente gerenciado.
  - AWS Cognito: autenticação e gerenciamento de usuários.
  - AWS API Gateway: gerenciamento e proteção de APIs.
  - Amazon SNS / SQS: serviços de mensagens e filas.
  - AWS Kinesis: streaming e análise de logs em tempo real.
  - AWS Aurora Serverless: banco de dados relacional serverless.
  - **AWS Lambda: execução de código sob demanda.**

Esses serviços permitem construir soluções completas e escaláveis sem precisar subir um único servidor EC2.

#### Lambda
O Lambda pode ser usado para inúmeras finalidades:
  - Processar arquivos recém-enviados ao S3.
  - Ler e escrever dados em bancos DynamoDB.
  - Enviar mensagens via SNS ou SQS.
  - Executar tarefas agendadas (via EventBridge).
  - Criar APIs completas integradas ao API Gateway.

#### EC2 vs Lambda
| **Característica**     | **EC2**                    | **Lambda**                              |
|--------------------------|----------------------------|------------------------------------------|
| **Tipo**                | Servidor virtual           | Função sem servidor                      |
| **Gerenciamento**        | Manual                     | Automático                               |
| **Escalonamento**        | Configurado pelo usuário   | Automático                               |
| **Tempo de execução**    | Contínuo                   | Até 15 minutos por invocação             |
| **Cobrança**             | Por hora de uso            | Por requisição e tempo de execução       |
| **Linguagens**           | Todas                      | Todas (Node.js, Python, Java, Go, etc.)  |

O Lambda é ideal para tarefas pontuais e event-driven (executadas apenas quando algo acontece), enquanto o EC2 é mais indicado para processos contínuos ou sistemas que precisam estar sempre ativos.

#### Criando uma função Lambda
  1. Acesse o serviço Lambda → Create Function.
  2. Escolha uma das opções:
    - Author from scratch: cria uma função vazia, geralmente usada para testes como “Hello World”.
    - Use a blueprint: usa um modelo pré-configurado com código de exemplo.
    - Container image: usa uma imagem Docker como base.
  3. Preencha os campos:
    - Function name: nome descritivo da função.
    - Runtime: linguagem de programação (Node.js, Python, Java, etc.).
    - Architecture: escolha entre x86_64 ou arm64.
    - Execution role: crie uma nova role com permissões básicas de Lambda (AWSLambdaBasicExecutionRole).

#### Exemplo de uso
Após criar, pode-se testar o Lambda utilizando o código abaixo no editor de código que aparece:
  ```bash
  import json

  print('Loading function')

  def lambda_handler(event, context):
      print("value1 =", event['key1'])
      print("value2 =", event['key2'])
      print("value3 =", event['key3'])
      return event['key1']
  ```

Esse código lê três parâmetros (key1, key2, key3) do evento recebido e retorna o valor de key1.

Testando:
  1. Clique em Test → Configure Test Event.
  2. Escolha o template “hello-world” e defina um JSON de exemplo:

    ```bash
    {
      "key1": "Desafio AWS 01",
      "key2": "Desafio AWS 02",
      "key3": "Desafio AWS 03"
    }
    ```

  3. Execute o teste.
    A saída mostrará o retorno e os logs da execução:

    ```bash
    Response:
    "Desafio AWS 01"

    Function Logs:
    value1 = Desafio AWS 01
    value2 = Desafio AWS 02
    value3 = Desafio AWS 03
    REPORT RequestId: ...
    Duration: 1.17 ms  Memory Used: 30 MB
    ```

A cada modificação no código, basta clicar em Deploy para atualizar a função imediatamente.

---

## 🌐 Redes na AWS
### 🔹 Amazon VPC (Virtual Private Cloud)
A Amazon Virtual Private Cloud (VPC) é o serviço que permite criar uma rede virtual isolada dentro da infraestrutura da AWS.
Com ela, é possível controlar totalmente a configuração de rede, endereçamento IP, sub-redes, rotas, firewalls e acessos.

Em outras palavras, a VPC funciona como o ambiente de rede privado de uma empresa dentro da nuvem — semelhante a um datacenter próprio, mas com toda a escalabilidade, segurança e flexibilidade da AWS.

#### Propriedades
- Isolamento de rede: garante um ambiente seguro para hospedar aplicações e dados sensíveis.
- Controle de tráfego: define regras de entrada (inbound) e saída (outbound) usando Security Groups e ACLs (Access Control Lists).
- Sub-redes (Subnets): permite criar redes públicas (com acesso à internet) e privadas (somente comunicação interna).
- Controle de endereçamento IP: define intervalos de IP próprios (CIDR Blocks).
- Conectividade híbrida: permite integração com redes locais via VPN ou AWS Direct Connect, estendendo a infraestrutura on-premises para a nuvem.

#### Estrutura e Conectividade
- Cada VPC é criada dentro de uma única região AWS e não pode se estender para outras regiões. Contudo, é possível interligar VPCs em regiões diferentes utilizando:
  - VPC Peering: conexão direta ponto a ponto entre duas VPCs.
  - AWS Transit Gateway: gerencia múltiplas conexões entre várias VPCs e redes locais de forma centralizada.
- Serviços públicos (como S3) não precisam de VPC por padrão, mas serviços privados (como bancos de dados) exigem configuração dentro de uma.


### 🗄️ Amazon Subnet
Uma Subnet (sub-rede) é um bloco de endereços IP dentro de uma VPC.
Ela permite organizar e isolar recursos de acordo com a função ou nível de acesso que precisam ter.

#### Estrutura e Função
  - Cada Subnet reside em apenas uma Zona de Disponibilidade (AZ) — por exemplo, “São Paulo (sa-east-1a)” ou “Norte da Virgínia (us-east-1b)”.
  - Dentro das Subnets são aplicadas regras de segurança, protocolos e endereços IP que controlam:
    - Quais IPs e protocolos podem acessar seus recursos (inbound).
    - Para quais destinos esses recursos podem se comunicar (outbound).

#### Tipos de Subnets
  - Pública: conectada a um Internet Gateway, permitindo acesso externo (por exemplo, servidores web).
  - Privada: sem acesso direto à internet, usada para recursos internos (como bancos de dados ou sistemas de back-end).

#### Exemplo de uso:
Em um sistema corporativo:
  - Subnet pública → EC2 com servidor web.
  - Subnet privada → banco de dados relacional RDS.
Ambos se comunicam entre si, mas apenas o web server tem acesso direto à internet.

**Por que usar VPC e não apenas Subnets?**
As Subnets dependem da VPC — elas não podem existir isoladamente.
A VPC é quem fornece a base lógica de roteamento, firewall e conectividade, enquanto as Subnets apenas segmentam essa rede em zonas específicas.
Sem a VPC, não há controle global de tráfego, isolamento entre ambientes (dev, test, prod) nem integração com outros serviços da AWS.

#### Analogia
Imagine a VPC como um prédio:
  - O prédio (VPC) representa a rede principal.
  - Cada andar (Subnet) pode ser público ou privado.
  - Os apartamentos (IPs) são os endereços dos recursos, como instâncias EC2.

### 🔒 Amazon Security Group
Os Security Groups (SGs) funcionam como firewalls virtuais para controlar o tráfego de entrada e saída das instâncias EC2 e outros recursos da VPC.

Eles atuam no nível da interface de rede da instância, e cada instância pode ter um ou mais grupos de segurança associados.

#### Propriedades
- Controle de tráfego: define regras de inbound (entrada) e outbound (saída).
- Regras reflexivas: se você autoriza uma porta inbound, a resposta outbound já é automaticamente liberada.
- Reuso: um mesmo Security Group pode ser criado uma vez e associado a várias instâncias EC2.

#### Exemplos de regras:
  - Permitir acesso SSH (porta 22) apenas para um IP específico.
  - Habilitar RDP (porta 3389) para conexões administrativas.
  - Liberar apenas a porta 3306 para conexões ao banco de dados.

#### Integração com ambientes híbridos
Em um ambiente híbrido (parte on-premises e parte em cloud), o tráfego pode passar primeiro por um firewall físico local, antes de alcançar a VPC.
Nesse caso:
  - É preciso garantir que o firewall local (por exemplo, Palo Alto, Fortigate) permita o tráfego para a VPC.
  - O Security Group atua dentro da AWS, mas o firewall físico é a primeira “parede” de proteção antes da nuvem.
  - Assim, ambos precisam ter regras coerentes para garantir conectividade e segurança.

### ➡️ Amazon Route 53
O Amazon Route 53 é o serviço de DNS (Domain Name System) gerenciado da AWS.
Ele converte nomes de domínio (como meusite.com) em endereços IP, permitindo que usuários acessem recursos hospedados na nuvem.

#### Propriedades
  - Resolução DNS interna e externa: traduz nomes para IPs dentro da AWS (interno) ou para a internet (externo).
  - Gerenciamento de zonas hospedadas: controle completo de domínios registrados.
  - Balanceamento de tráfego baseado em geolocalização: redireciona o usuário para o recurso mais próximo.

#### Exemplo de uso:
Um domínio como empresa.com pode ser configurado para resolver internamente dentro da VPC e também estar disponível externamente para clientes — o Route 53 faz a ponte entre o mundo externo e a infraestrutura interna.

### ⏳ Amazon CloudFront
O Amazon CloudFront é o serviço de entrega de conteúdo (CDN) da AWS.
Ele distribui dados, vídeos, aplicações e APIs globalmente com baixa latência e alta velocidade de transferência.

#### Funcionamento
  - Quando um cliente faz uma requisição, o CloudFront entrega o conteúdo a partir de Edge Locations — servidores de cache espalhados pelo mundo.
  - O primeiro acesso armazena uma cópia local do conteúdo; acessos seguintes são entregues mais rapidamente.
  - Reduz latência e melhora a experiência do usuário final.

#### Exemplo de uso:
Serviços de streaming e portais web globais usam o CloudFront para garantir que usuários na Europa, Ásia ou América do Sul recebam o mesmo conteúdo com desempenho semelhante, independentemente da localização.

#### Integração com outros serviços
  - Pode distribuir conteúdo de buckets S3, instâncias EC2 ou Load Balancers.
  - Necessita que os serviços de origem estejam configurados para suportar acesso global.


### Amazon Elastic Load Balancer (ELB)
O Elastic Load Balancer (ELB) distribui automaticamente o tráfego de rede entre múltiplas instâncias ou serviços, melhorando desempenho e disponibilidade.

Ele atua como um balanceador de carga, direcionando requisições de forma inteligente entre servidores conforme a demanda.

#### Exemplo de uso:
Durante uma campanha com grande pico de acessos (como uma promoção de TV em horário nobre), o ELB distribui as requisições entre múltiplas instâncias EC2 para evitar sobrecarga e lentidão.

#### Tipos de Load Balancer
  - Application Load Balancer (ALB): gerencia tráfego HTTP/HTTPS, com regras baseadas em caminhos de URL ou cabeçalhos — ideal para aplicações web e microsserviços.
  - Network Load Balancer (NLB): balanceia tráfego TCP/UDP com baixa latência e alta performance — ideal para jogos online e sistemas financeiros.
  - Gateway Load Balancer (GLB): combina balanceamento com serviços de segurança de rede, como firewalls e inspeções de tráfego.
  - Classic Load Balancer (CLB): modelo mais antigo, ainda usado para compatibilidade com aplicações legadas.

#### Aplicações e Benefícios

- Aumenta a escalabilidade de ambientes híbridos.
- Pode equilibrar recursos locais e na AWS em uma única estrutura.
- Melhora a resiliência e a tolerância a falhas, redirecionando tráfego automaticamente em caso de instância inativa.
---

## 🗄️ Banco de Dados na AWS
*(a preencher conforme andamento)*  

---

## 📦 Serviços de Armazenamento e CDN
*(a preencher conforme andamento)*  

---

## ⚙️ Serviços Intermediários e Avançados
*(a preencher conforme andamento)*  

---

## 📊 Gerenciamento e Governança na AWS
*(a preencher conforme andamento)*  

---

## 🔒 Segurança na AWS
*(a preencher conforme andamento)*  

---

## 👩‍💻 Desenvolvimento e Ferramenta
*(a preencher conforme andamento)*  

---

## 🤖 Automação e DevOps na AWS
*(a preencher conforme andamento)*  

