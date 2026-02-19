# Laboratório Executado na Escola da Núvem. AWS Lab: Troubleshooting de Permissões e Segurança (IAM) 🚀

Este repositório documenta a resolução de problemas reais de acesso encontrados durante laboratórios práticos na AWS (Escola da Nuvem), focando no Princípio do Menor Privilégio.

## 📋 Cenário do Laboratório
O objetivo era realizar o upload de um certificado de segurança em um bucket S3 e configurar uma instância EC2. Durante o processo, diversos erros de "Access Denied" foram disparados, permitindo uma análise profunda de políticas de IAM.

## 🛠️ Problemas Identificados e Resoluções

### 1. Falha no Upload para o S3 (Erro de Permissão)
Ao tentar fazer upload do arquivo `Certificado JavaScript.pdf`, o sistema retornará **Acesso Negado**.
- **Causa:** O usuário IAM não possuía permissão `s3:PutObject` no bucket de destino.
- **Resolução** Ajuste da política inline para permitir a ação apenas no bucket específico, mantendo a segurança.

---

### 2. Erro de Visualização de VPCs na EC2
Na tentativa de lançar uma instância (Console EC2), a mensagem de erro foi:
`User is not authorized to perform: ec2:DescribeVpcs`
- **Análise:** Sem essa permissão, o console da AWS não consegue listar as redes disponíveis para alocar a máquina virtual.
- **Impacto FinOps:** Erros de configuração de rede podem levar ao provisionamento em regiões ou sub-redes mais caras se não houver visibilidade.

## 🖼️ Evidências (Prints do Console)

| Erro de Acesso Negado (S3) | Erro de Autorização (EC2) |
| :---: | :---: |
| <img src="https://github.com/user-attachments/assets/76b03830-4a14-4dde-b17d-1e00d6e751a0" width="400"> | <img src="https://github.com/user-attachments/assets/c15a799f-fff1-4dca-bd8b-c3ec288d1394" width="400"> |
| *Tentativa de upload negada* | *Falha ao descrever VPCs* |

---

### Falha de Autorização na EC2
Abaixo, o erro que impedia a visualização de VPCs para a criação da instância:
<img width="800" alt="Erro ec2:DescribeVpcs" src="https://github.com/user-attachments/assets/c15a799f-fff1-4dca-bd8b-c3ec288d1394" />


---

## 💡 Habilidades Técnicas
1. **Troubleshooting:** Aprendi a ler e interpretar mensagens de erro JSON e XML retornadas pela API da AWS.
2. **Segurança:** A importância de conceder permissões granulares em vez de `AdministratorAccess`.
3. **IAM Policy Simulator:** Utilizei para validar quais permissões faltavam para o usuário `analista-s3`.
