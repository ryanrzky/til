---
title: IRSA, Karpenter NodePool and EC2Nodeclass
pubDate: '2026-01-01'
---

Konteks dari konten ini adalah [Karpenter](https://karpenter.sh)

# IRSA (IAM Role for Service Account)
IAM Role yang digunakan oleh pod (dalam EKS Cluster) agar bisa berkomunikasi dengan AWS resources.

# NodePool
Sederhananya, ini adalah kumuplan aturan node yang akan dibuat oleh Karpenter dan yang akan dipakai oleh pod.

Contoh:
```yaml
    requirements:
        - key: "karpenter.k8s.aws/instance-category"
          operator: In
          values: ["c", "m", "r"]
```

# EC2NodeClass
Jika NodePool adalah yang menentukan aturan node apa yang dibutuhkan, EC2NodeClass adalah yang menentukan bagaiman dari sisi AWSnya yang harus disiapkan.

Contoh:
- `amiFamily` -> menentukan OS
- `subnetSelectorTerms` -> menentukan di VPC mana dan subnet mana ec2 instance akan dibuat
- `securityGroupSelectorTerms` -> menentukan security group yang akan dipakai
- `role` -> menentukan IAM role yang akan di pakai ec2