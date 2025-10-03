# 🌐 Estratégia de Publicação de Aplicações Mendix – Visão Executiva

## 1. Objetivo
Definir as opções viáveis de publicação e operação de aplicações Mendix, avaliando complexidade operacional, necessidade de SRE, custo e cenários ideais (POC vs Produção).

---

## 2. Opções de Publicação

### 🐳 1. Docker Local (POC e Desenvolvimento)
**Descrição:**  
Execução local via contêiner Docker, ideal para laboratórios, provas de conceito e desenvolvimento inicial.

**Características:**
- Zero dependência de SRE ou infraestrutura gerenciada.
- Rápido para subir ambientes em notebooks ou VMs locais.
- Limitado em escalabilidade, observabilidade e segurança.
- **Não recomendado para produção**.

**Quando usar:**  
- Testes iniciais de conceito.  
- Demonstrações internas e desenvolvimento isolado.

---

### ☁️ 2. Mendix Cloud (SaaS Gerenciado)
**Descrição:**  
Plataforma como serviço oferecida pela Mendix, totalmente gerenciada e hospedada em nuvem (AWS subjacente).

**Características:**
- Zero operação de cluster ou infraestrutura (sem SRE).
- Escalabilidade automática e segurança embutida.
- Ambientes de Dev/QA/Prod prontos para uso.
- Limitações de customização de rede e serviços gerenciados.

**Quando usar:**  
- Times pequenos e foco em entrega rápida.  
- Projetos sem exigência de VPC própria ou integração avançada com serviços nativos do CSP.

---

### ☸️ 3. Azure Kubernetes Service (AKS)
**Descrição:**  
Implantação em cluster Kubernetes no Azure, com suporte a observabilidade corporativa, RBAC, escalabilidade e compliance.

**Características:**
- Total controle de rede, segurança e arquitetura.  
- Integração nativa com serviços Azure (PostgreSQL, Redis, Storage, Monitor).  
- Suporte a pipelines CI/CD e GitOps.  
- Requer suporte de SRE ou equipe DevOps mínima.

**Quando usar:**  
- Ambientes de produção corporativos.  
- Exigência de VPC própria, auditoria, backup e integração com infraestrutura existente.  
- Cenários regulatórios ou de soberania de dados.

---

### ☸️ 4. Kubernetes em Outros CSPs (EKS – AWS / GKE – GCP / On-Prem)
**Descrição:**  
Mesma abordagem do AKS, porém executada em outro provedor ou infraestrutura on-premises.

**Características:**
- Equivalentes técnicos ao AKS, com pequenas diferenças de custo e ferramentas.  
- Pode usar serviços nativos do provedor para banco, cache e monitoramento.  
- Maior liberdade de escolha, porém mais responsabilidade operacional.

**Quando usar:**  
- Estratégia multicloud ou já existir cluster Kubernetes consolidado.  
- Cenários com requisitos específicos de conformidade ou soberania.

---

## 3. Estimativas de Custo (Mensal)

| Cenário | Infraestrutura | HA | Estimativa (USD) | Estimativa (BRL) |
|--------|------------------|----|------------------|------------------|
| 🐳 Docker Local | 1 nó local (POC) | ❌ | ~0 – 50 | ~R$ 0 – 300 |
| ☁️ Mendix Cloud (SaaS) | Ambientes gerenciados | ✅ | ~300 – 800 | ~R$ 1.800 – 4.400 |
| ☸️ AKS – Azure | 3 nós médios (4 vCPU / 16 GB), DB gerenciado, Redis, Storage, Monitoramento | ❌ | ~400 – 600 | ~R$ 2.200 – 3.300 |
| ☸️ AKS – Azure | 3+ nós, alta disponibilidade, backup e observabilidade corporativa | ✅ | ~600 – 1.000 | ~R$ 3.500 – 5.500 |
| ☸️ Kubernetes – Outros CSPs | Estrutura equivalente em EKS/GKE | ❌ | ~400 – 650 | ~R$ 2.200 – 3.600 |
| ☸️ Kubernetes – Outros CSPs | Estrutura com HA e monitoramento corporativo | ✅ | ~600 – 1.000 | ~R$ 3.500 – 5.500 |

> 💡 *Valores variam conforme região, reserva de instâncias, descontos contratuais e volume de tráfego.*

---

## 4. Recomendação Estratégica

- **Início de projeto / validação de hipótese:** 🐳 **Docker Local**  
- **Entrega rápida e sem operação:** ☁️ **Mendix Cloud**  
- **Produção corporativa com compliance e integração:** ☸️ **AKS no Azure**  
- **Cenários multicloud ou infraestrutura híbrida:** ☸️ **EKS / GKE / On-Prem**

---

## 5. Conclusão
A escolha ideal depende do estágio do projeto e dos requisitos de negócio.  
- **Sem SRE e rápido time-to-market:** Mendix Cloud.  
- **Controle total, integração e governança corporativa:** Kubernetes (AKS ou outros CSPs).  
- **Exploração e POC:** Docker local.

