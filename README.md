# formacaoaws
Formacao AWS Henrylle Maia
# Desafio 3 — Migração para Amazon Aurora PostgreSQL Serverless
Mentoria **Desafio Labs 2.0 — Formação AWS**

> Objetivo: migrar um banco relacional **PostgreSQL** para **Amazon Aurora PostgreSQL Serverless**, automatizando as etapas com shell scripts e validando disponibilidade, persistência e custos.

---

## ✨ Resultado
- **Aurora PostgreSQL Serverless** criado e acessível.
- **Dump/Restore** do banco concluído com `pg_dump`/`pg_restore`.
- **Conectividade** via **EC2 + AWS Systems Manager (Session Manager)** (sem chave SSH).
- **Boas práticas**: IAM mínimo, SGs específicos, monitoração e *autopause* (se usar Serverless v1).
- **Evidências** em `/docs/evidencias/` (prints e logs).

---

## 🧭 Arquitetura (visão)
```mermaid
flowchart LR
    subgraph VPC
      EC2[Bastion EC2\nSession Manager]---|TCP 5432| AUR[Aurora PostgreSQL Serverless\nCluster (writer/reader)]
      S3[(S3)]<-->EC2
    end
    IAM[(IAM Roles/Policies)]-->EC2
    CloudWatch[(CloudWatch)]-->AUR
