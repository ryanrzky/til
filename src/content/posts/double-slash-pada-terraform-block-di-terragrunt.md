---
title: Double Slash Pada terraform Block di Terragrunt
pubDate: '2026-01-03'
---

# Overview
Terragrunt memanggil Terraform module menggunakan dalam `terraform` block menggunakan doubel slash `//` untuk:
1. Memisahkan antara main repository / main dirktori dengan sub direktori.
2. Memastikan relative path berjalan dengan benar.

# Contoh

## Local Module
`vpc` ada di dalam direktori `modules/aws/vpc`. Idealnya untuk memanggil module `vpc` kita perlu menambahkan `//` sebelum `vpc`.
```hcl
terraform {
    source = "../..//modules/aws/vpc"
}
```

Tujuanya adalah untuk mencegah Terragrunt hanya mengunduh module `vpc` saja. Jika module `vpc` begantung pada module lain, maka terragrunt akan error.

## Remote Module
```hcl
terraform {
    source = "git::https://github.com/org/repo.git//modules/aws/vpc"
}
```

Terragrunt akan meng-clone seluruh `repo.git` kemudian masuk ke sub direktori `modules/aws/vpc`.