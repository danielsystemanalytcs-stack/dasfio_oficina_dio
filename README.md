# ⚙️ Modelo de Dados para Gestão de Oficina Mecânica (Ordem de Serviço - OS)

Este repositório contém o **Modelo Lógico de Banco de Dados** projetado para o controle e gerenciamento completo de Ordens de Serviço (OS) em uma oficina mecânica. O modelo garante a rastreabilidade de clientes, veículos, equipes de mecânicos e todos os custos associados a peças e serviços.

---

## 🎯 Objetivo do Modelo

O principal objetivo deste esquema é suportar a execução e o faturamento de Ordens de Serviço, com as seguintes funcionalidades chave:

1.  **Rastreamento de Veículos:** Ligar o histórico de serviços diretamente ao veículo e ao cliente.
2.  **Gestão de Equipes:** Designar cada OS a uma **Equipe de Mecânicos** e gerenciar a composição dessas equipes.
3.  **Cálculo da OS:** Separar e somar corretamente os custos de **Mão de Obra (Serviços)** e **Materiais (Peças)**, registrando o valor transacional de cada item.

---

## 🏗️ Diagrama do Modelo Lógico (DER)

*(Insira aqui a imagem do seu diagrama final, **Oficina_3.png**)*

![Diagrama do Modelo de Dados da Oficina Mecânica](https://github.com/danielsystemanalytcs-stack/dasfio_oficina_dio/blob/main/Oficina.png)

### Resumo das Entidades

O modelo é composto por 10 tabelas, incluindo 3 tabelas associativas para resolver os relacionamentos complexos.

| Tabela | Tipo | Função |
| :--- | :--- | :--- |
| **CLIENTE** | Forte | Informações básicas do cliente. |
| **VEÍCULO** | Forte | Informações do carro; ligado ao `CLIENTE`. |
| **MECÂNICO** | Forte | Cadastro dos profissionais e suas especialidades. |
| **EQUIPE** | Forte | Agrupamento de mecânicos. |
| **SERVIÇO** | Forte | Catálogo de mão de obra e seus valores de referência. |
| **PEÇA** | Forte | Estoque de peças e seus valores de referência. |
| **ORDEM\_DE\_SERVIÇO (OS)** | Central | O documento que centraliza a transação, ligado a Veículo e Equipe. |
| **EQUIPE\_MECÂNICO** | Associativa | Liga **Mecânico** a **Equipe** (N:M). |
| **OS\_SERVIÇO** | Associativa | Liga **OS** a **Serviço** (N:M). Armazena horas e valor final do serviço. |
| **OS\_PEÇA** | Associativa | Liga **OS** a **Peça** (N:M). Armazena quantidade e valor final da peça. |

---

## 🔑 Resolução de Relacionamentos N:M

Os relacionamentos de Muitos-para-Muitos (N:M) são cruciais e foram resolvidos da seguinte forma:

| Relacionamento | Solução (Tabela Associativa) | Chaves Estrangeiras (FKs) | Detalhes Transacionais |
| :--- | :--- | :--- | :--- |
| **Mecânicos na Equipe** | `EQUIPE_MECÂNICO` | `fk_idEquipe`, `fk_idMecanico` | Define a composição de cada equipe. |
| **Serviços na OS** | `OS_SERVIÇO` | `fk_numero_OS`, `fk_idServiço` | Permite registrar a **quantidade de horas** e o **valor final** cobrado. |
| **Peças na OS** | `OS_PEÇA` | `fk_numero_OS`, `fk_idPeça` | Permite registrar a **quantidade** de peças usadas e o **valor unitário** no momento da OS. |

---

## ⚙️ Tecnologias

* **Modelagem:** MySQL Workbench / Modelo Entidade-Relacionamento (DER)

---

## 🤝 Contribuições

Sinta-se à vontade para propor melhorias neste modelo, como adicionar entidades para `Fornecedores` ou `Agendamento`!

1.  Faça um `fork` do projeto.
2.  Crie sua branch (`git checkout -b feature/sua-sugestao`).
3.  Faça o `commit` das suas alterações.
4.  Abra um **Pull Request**.

---
Modelo desenvolvido por **[Daniel Silva / github.com/danielsystemanalystc-stack]**
