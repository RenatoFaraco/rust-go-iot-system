# 🦀 Sensor Simulator + Backend API (Rust + Go) 🐹

[![Rust](https://img.shields.io/badge/Rust-v1.70+-red)](https://www.rust-lang.org/)
[![Go](https://img.shields.io/badge/Go-v1.20+-blue)](https://go.dev/)

Um projeto integrado para simulação de sensores em **Rust** com processamento de sinais e backend em **Go**, ideal para aplicações IoT e sistemas embarcados.

## 📋 Sumário

- [Visão Geral](#-visão-geral)
- [Arquitetura](#-arquitetura)
- [Estrutura de Pastas](#-estrutura-de-pastas)
- [Configuração](#-configuração)
- [Como Executar](#-como-executar)
- [Exemplos de Código](#-exemplos-de-código)
- [Roadmap](#-roadmap)
- [Contribuição](#-contribuição)

## 🌐 Visão Geral

Este projeto demonstra:

- **Rust**: Simulação de sensores e implementação de filtros digitais (média móvel, Kalman)
- **Go**: API REST para coleta e armazenamento de dados (SQLite/PostgreSQL)
- **Integração**: Comunicação via HTTP entre os sistemas

## ⚙ Arquitetura

mermaid
flowchart LR
RUST[[Rust]] -->|HTTP POST| GO[[Go]]
GO --> DB[(Database)]
GO --> WEB[Dashboard]

## 📂 Estrutura de Pastas

.
├── rust_sensor/
│ ├── src/
│ │ ├── main.rs # Ponto de entrada
│ │ ├── sensor.rs # Lógica do sensor
│ │ ├── filters.rs # Implementação de filtros
│ │ └── lib.rs # Definições compartilhadas
│ ├── Cargo.toml
│ └── README.md
│
├── go_backend/
│ ├── main.go # API principal
│ ├── models/ # Modelos de dados
│ ├── handlers/ # Lógica dos endpoints
│ └── go.mod
│
└── README.md # Este arquivo

## ⚡ Como Executar

### Pré-requisitos

- Rust 1.70+
- Go 1.20+
- SQLite (ou PostgreSQL)

### Passo a Passo

1. **Backend (Go)**:
   bash
   cd go_backend
   go run main.go

2. **Sensor Simulator (Rust)**:
   bash
   cd rust_sensor
   cargo run --release

## 🦀 Exemplo Rust (filters.rs)

rust
/// Filtro de média móvel
pub fn moving_average(data: &[f32], window_size: usize) -> Vec<f32> {
data.windows(window_size)
.map(|window| window.iter().sum::<f32>() / window_size as f32)
.collect()
}

/// Simulação de sensor de temperatura
pub fn simulate*temperature(samples: usize) -> Vec<f32> {
(0..samples).map(|*| 25.0 + rand::random::<f32>() \* 10.0).collect()
}

## 🐹 Exemplo Go (main.go)

go
package main

import (
"log"
"net/http"
"github.com/gin-gonic/gin"
"gorm.io/gorm"
)

type SensorData struct {
gorm.Model
SensorID string json:"sensor_id" binding:"required"
Value float32 json:"value" binding:"required"
}

func main() {
router := gin.Default()
db := setupDatabase()
router.POST("/api/data", func(c \*gin.Context) {
var data SensorData
if err := c.ShouldBindJSON(&data); err != nil {
c.JSON(http.StatusBadRequest, gin.H{"error": err.Error()})
return
}
if result := db.Create(&data); result.Error != nil {
c.JSON(http.StatusInternalServerError, gin.H{"error": result.Error.Error()})
return
}
c.JSON(http.StatusOK, data)
})
log.Fatal(router.Run(":8080"))
}

## 🚧 Roadmap

- [ ] Simulação básica de sensores
- [ ] API REST em Go
- [ ] Adicionar autenticação JWT
- [ ] Implementar dashboard Grafana
- [ ] Dockerização completa

## 🤝 Contribuição

1. Faça um fork do projeto
2. Crie sua branch (`git checkout -b feature/awesome-feature`)
3. Commit suas mudanças (`git commit -m 'Add awesome feature'`)
4. Push para a branch (`git push origin feature/awesome-feature`)
5. Abra um Pull Request

## 📄 Licença

MIT © [Seu Nome]

---

> **Note**: Projeto desenvolvido como parte do portfólio técnico. Atualizado em `2025-03-27`
