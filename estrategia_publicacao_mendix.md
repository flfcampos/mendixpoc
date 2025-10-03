
# 🌐 Aplicações Mendix  

## 1. Opções de Publicação

### 🐳 a. Docker Local (POC e Desenvolvimento)
**Descrição:**  
Execução local via contêiner Docker, ideal para laboratórios, provas de conceito e desenvolvimento inicial.

**Inclui:**  
- 📦 App Mendix rodando em contêiner local  
- 🗄️ Banco de dados local (PostgreSQL ou SQLite)

**Características:**
- Zero dependência de SRE ou infraestrutura gerenciada.
- Rápido para subir ambientes em notebooks ou VMs locais.
- Limitado em escalabilidade, observabilidade e segurança.
- **Não recomendado para produção**.

**Documentação:**  
- [Executando Mendix em Docker – Guia oficial](https://docs.mendix.com/howto/deploy/run-mendix-on-docker/)  
- [Docker Hub – Imagens Mendix](https://hub.docker.com/r/mendix/docker-mendix-buildpack)

**Diagrama ASCII (POC):**
```
[Dev Machine]
     |
 [Docker Engine]
     |
 [Mendix App Container] --(localhost volume)--> [Local PostgreSQL DB]
```

---

### ☁️ b. Mendix Cloud (SaaS Gerenciado)
**Descrição:**  
Plataforma como serviço oferecida pela Mendix, totalmente gerenciada e hospedada em nuvem (AWS subjacente).

**Inclui:**  
- 📦 Publicação automática do app via Portal Mendix  
- 🗄️ Banco de dados gerenciado e mantido pela plataforma  

**Características:**
- Zero operação de cluster ou infraestrutura (sem SRE).
- Escalabilidade automática e segurança embutida.
- Ambientes de Dev/QA/Prod prontos para uso.

**Documentação:**  
- [Mendix Cloud Overview](https://docs.mendix.com/developerportal/deploy/mendix-cloud-deploy/)  
- [Gerenciamento de Ambientes Mendix Cloud](https://docs.mendix.com/developerportal/deploy/environments/)

**Diagrama ASCII (SaaS):**
```
[Users/Frontends]
       |
    [HTTPS/WAF]
       |
   [Mendix Cloud]
     /      [Runtime] [Mgmt/CI]
     |          [Managed PostgreSQL DB]  [Logs/Monitoring]
```

---

### ☸️ c. Azure Kubernetes Service (AKS)
**Descrição:**  
Implantação em cluster Kubernetes no Azure, com suporte a observabilidade corporativa, RBAC, escalabilidade e compliance.

**Inclui:**  
- 📦 App Mendix em pods no cluster AKS  
- 🗄️ Banco de dados PostgreSQL gerenciado (Azure Database for PostgreSQL) ou externo  

**Características:**
- Total controle de rede, segurança e arquitetura.  
- Integração nativa com serviços Azure (PostgreSQL, Redis, Storage, Monitor).  
- Suporte a pipelines CI/CD e GitOps.  
- Requer suporte de SRE ou equipe DevOps mínima.

**Documentação:**  
- [Mendix Deployment em Kubernetes](https://docs.mendix.com/developerportal/deploy/kubernetes-deploy/)  
- [Mendix Operator – Kubernetes](https://github.com/mendix/mendix-k8s-operator)  
- [Azure Kubernetes Service – Documentação oficial](https://learn.microsoft.com/azure/aks/)  
- [PostgreSQL Gerenciado no Azure](https://learn.microsoft.com/azure/postgresql/flexible-server/)

**Diagrama ASCII (AKS – Prod):**
```
[Users] --HTTPS--> [Azure Front Door/WAF] --> [Ingress Controller]
                                                  |
                                             [AKS Cluster]
                                              /    |                                         [Mendix Pods] [HPA]  [Operator]
                                           |
                                  [Azure DB for PostgreSQL]
                                           |
                                      [Backups / PITR]
                                           |
                                   [Azure Monitor / Logs]
```

---

### ☸️ d. Kubernetes em Outros CSPs (EKS – AWS / GKE – GCP / On-Prem)
**Descrição:**  
Mesmo modelo do AKS, porém executado em outro provedor ou on-premises.

**Inclui:**  
- 📦 App Mendix em pods no cluster K8s  
- 🗄️ Banco de dados gerenciado (RDS, Cloud SQL) ou provisionado externamente  

**Documentação:**  
- [Mendix on Kubernetes – Visão geral](https://docs.mendix.com/developerportal/deploy/kubernetes-deploy/)  
- [Amazon EKS – Documentação oficial](https://docs.aws.amazon.com/eks/)  
- [Google GKE – Documentação oficial](https://cloud.google.com/kubernetes-engine/docs)

**Diagrama ASCII (EKS/GKE – Prod):**
```
[Users] -> [LB/WAF] -> [Ingress Controller] -> [K8s Cluster]
                                             |         |
                                         [Mendix Pods] [Operator]
                                             |
                                   [Managed DB (RDS / Cloud SQL)]
```

---

## 2. Estimativas de Custo (Mensal)

| Cenário | Inclui App + DB | HA | Estimativa (USD) | Estimativa (BRL) |
|--------|------------------|----|------------------|------------------|
| 🐳 Docker Local | ✅ | ❌ | ~0–50 | ~R$ 0–300 |
| ☁️ Mendix Cloud (SaaS) | ✅ | ✅ | ~300–800 | ~R$ 1.800–4.400 |
| ☸️ AKS – Azure | ✅ | ❌ | ~400–600 | ~R$ 2.200–3.300 |
| ☸️ AKS – Azure | ✅ | ✅ | ~600–1.000 | ~R$ 3.500–5.500 |
| ☸️ Kubernetes – Outros CSPs | ✅ | ❌ | ~400–650 | ~R$ 2.200–3.600 |
| ☸️ Kubernetes – Outros CSPs | ✅ | ✅ | ~600–1.000 | ~R$ 3.500–5.500 |

**Referências de preço:**  
- [Preços do Azure AKS](https://azure.microsoft.com/pricing/details/kubernetes-service/)  
- [Preços Mendix Cloud](https://www.mendix.com/pricing/)  
- [Preços Amazon EKS](https://aws.amazon.com/eks/pricing/)  
- [Preços Google GKE](https://cloud.google.com/kubernetes-engine/pricing)

---

## 3. Recomendação Estratégica
- **Exploração/POC:** 🐳 Docker Local.  
- **Entrega rápida e sem SRE:** ☁️ Mendix Cloud.  
- **Produção corporativa (compliance, VPC, observabilidade):** ☸️ AKS.  
- **Multicloud ou base pré-existente:** ☸️ EKS/GKE/On-Prem.

---

## 4. Conclusão
- Todas as opções envolvem a **publicação do app Mendix e a provisão de um banco de dados funcional**.  
- **Sem SRE e foco em velocidade:** Mendix Cloud.  
- **Controle total, integração e governança:** Kubernetes (AKS/EKS/GKE).  
- **POC e dev local:** Docker.
