
# 🌐 Estratégia de Publicação de Aplicações Mendix – Resumo Executivo

## 🎯 Objetivo
Definir as opções para publicar e operar apps Mendix com foco em complexidade, custo e uso ideal.  
> ✅ Toda solução envolve **publicar o app** e **provisionar um banco de dados funcional**.

---

## 🚀 Opções de Publicação

### 🐳 Docker Local – POC/Dev
- 📦 App em contêiner local + 🗄️ DB local  
- Zero SRE, rápido para validar ideias  
- Não indicado para produção  
- [Doc](https://docs.mendix.com/howto/deploy/run-mendix-on-docker/)

```
[Dev] -> [Docker] -> [Mendix App] -> [Local DB]
```

---

### ☁️ Mendix Cloud – SaaS Gerenciado
- 📦 App publicado direto no portal  
- 🗄️ Banco gerenciado incluído  
- Sem operação de infraestrutura  
- Menos controle de rede e serviços  
- [Doc](https://docs.mendix.com/developerportal/deploy/mendix-cloud-deploy/)

```
[Usuário] -> [Mendix Cloud] -> [Runtime + Managed DB]
```

---

### ☸️ Azure Kubernetes (AKS) – Produção Corporativa
- 📦 App em pods + 🗄️ PostgreSQL gerenciado  
- Total controle de rede, segurança e CI/CD  
- Requer equipe SRE mínima  
- [Doc AKS](https://learn.microsoft.com/azure/aks/) | [Mendix K8s](https://docs.mendix.com/developerportal/deploy/kubernetes-deploy/)

```
[Usuário] -> [Ingress] -> [AKS Cluster] -> [PostgreSQL Gerenciado]
```

---

### ☸️ Kubernetes (EKS/GKE/On-Prem) – Multicloud
- 📦 App em pods + 🗄️ DB gerenciado (RDS/Cloud SQL)  
- Mesma estrutura do AKS em outros provedores  
- Maior controle e responsabilidade  
- [EKS](https://docs.aws.amazon.com/eks/) | [GKE](https://cloud.google.com/kubernetes-engine/docs)

```
[Usuário] -> [Ingress] -> [K8s Cluster] -> [Managed DB]
```

---

## 💰 Estimativas de Custo (App + DB)

| Cenário | HA | USD/mês | BRL/mês |
|--------|----|----------|-----------|
| 🐳 Docker Local | ❌ | 0–50 | 0–300 |
| ☁️ Mendix Cloud | ✅ | 300–800 | 1.800–4.400 |
| ☸️ AKS Azure | ❌ | 400–600 | 2.200–3.300 |
| ☸️ AKS Azure | ✅ | 600–1.000 | 3.500–5.500 |
| ☸️ EKS/GKE | ✅ | 600–1.000 | 3.500–5.500 |

---

## 🧭 Recomendação Estratégica
- 🐳 **POC/Dev:** Docker  
- ☁️ **Entrega rápida e sem SRE:** Mendix Cloud  
- ☸️ **Produção corporativa:** AKS  
- ☸️ **Multicloud / on-prem:** EKS / GKE

---

## ✅ Conclusão
- Toda solução exige **app publicado + banco funcional**.  
- **Rápido e simples:** Mendix Cloud  
- **Escalável e corporativo:** Kubernetes  
- **Exploração:** Docker
