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
| ✅ | [Computação na Nuvem com EC2](#-computação-na-nuvem-com-ec2) | - Instâncias EC2 e Otimização de Recursos AWS <br> - Armazenamento com EBS e S3 <br> - Gerenciando Instâncias EC2 AWS |
| ⬜ | [Criando Recursos na AWS](#-criando-recursos-na-aws) | — |
| ⬜ | [Redes na AWS](#-redes-na-aws) | — |
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
*(Aqui você escreve o resumo do que aprendeu, reflexões ou insights pessoais sobre este módulo.)*  

---

## 💻 Computação na Nuvem com EC2

### 🔹 Amazon EC2 (Elastic Compute Cloud)
- Máquinas virtuais (servidores) na AWS, com Windows ou Linux.  
- Compostas por: CPU, memória, disco, rede e sistema operacional.  
- Modelo **IaaS** → AWS cuida da infraestrutura física (energia, cabeamento, hardware) e da segurança básica, mas a **configuração e uso são responsabilidade do cliente**.  

##### Responsabilidades e Segurança
- AWS protege a infraestrutura e oferece firewall (grupos de segurança, portas, IPs, protocolos).  
- Cliente deve configurar corretamente o acesso (evitar exposição pública desnecessária).  

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

#### Flexibilidade
- É possível **upgrade/downgrade** de instância conforme necessidade.  
- Escolha correta → garante **eficiência operacional e economia**.   


### 📦 Armazenamento com EBS e S3

#### Amazon EBS (Elastic Block Store)
- Armazenamento em blocos altamente confiável e expansível.  
- Funciona como um **HD externo** para as instâncias **EC2**.  
- Cada instância já possui um volume (para o SO), mas é possível anexar novos volumes EBS.  
- Permite **upgrade/downgrade** rápido e tem alta disponibilidade.  
- Exemplos de uso:  
  - Bancos de dados (MySQL, PostgreSQL, Oracle).  
  - Dados de aplicativos web e logs de sistema.  
- Pode criar **snapshots** para backup e restaurar em outras regiões.  


#### Amazon S3 (Simple Storage Service)
- Serviço de **armazenamento de objetos** em nuvem, seguro e escalável.  
- Ideal para armazenar e recuperar grandes volumes de dados.  
- Muito usado em pipelines de processamento, exportação/importação de arquivos e integração com outros serviços (ex.: Lambda, EC2).  
- **Custo:** pagar pelo armazenamento + leitura/download dos dados.  
- Permite configurar **lifecycle policies** para mover objetos automaticamente entre classes de armazenamento.  
- Disponibilidade: **99,999999999% (11 9’s)** de durabilidade.  

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

#### Snapshots EBS

- Serviço de backup nativo da AWS que faz cópias pontuais de volumes EBS.  
- Funcionam como uma foto de um disco rígido em um momento específico.  
- Armazenados no S3, em uma matriz separada do EBS.  
- Possível configurar frequência de snapshots para backup automático.  
- Usados em estratégias de Disaster Recovery (DR) → podem ser armazenados em regiões remotas.  
- Otimização: é possível usar volumes SSD para operações com alta demanda de I/O.  

##### Exemplos de uso 
- Backup de ambientes de produção (homologação às vezes, testes normalmente não).  
- Recuperação de ambientes críticos em caso de falhas.  


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

### 🛠️ Criando Recursos na AWS
*(a preencher conforme andamento)*  

---

### 🌐 Redes na AWS
*(a preencher conforme andamento)*  

---

### 🗄️ Banco de Dados na AWS
*(a preencher conforme andamento)*  

---

### 📦 Serviços de Armazenamento e CDN
*(a preencher conforme andamento)*  

---

### ⚙️ Serviços Intermediários e Avançados
*(a preencher conforme andamento)*  

---

### 📊 Gerenciamento e Governança na AWS
*(a preencher conforme andamento)*  

---

### 🔒 Segurança na AWS
*(a preencher conforme andamento)*  

---

### 👩‍💻 Desenvolvimento e Ferramenta
*(a preencher conforme andamento)*  

---

### 🤖 Automação e DevOps na AWS
*(a preencher conforme andamento)*  

