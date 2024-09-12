# Modelo Dimensional - Análise de Professores

## Visão Geral
Este repositório contém o modelo dimensional desenvolvido para análise dos dados de professores de uma instituição de ensino. O modelo foi criado utilizando um esquema estrela para facilitar consultas analíticas e gerar relatórios em ferramentas de **Business Intelligence (BI)**.

## Índice
- [Objetivo](#objetivo)
- [Estrutura do Modelo](#estrutura-do-modelo)
- [Diagrama Entidade-Relacionamento (DER)](#diagrama-entidade-relacionamento-der)
- [Como Utilizar o Modelo](#como-utilizar-o-modelo)
- [Próximos Passos](#próximos-passos)
- [Contribuições](#contribuições)
- [Licença](#licença)

## Objetivo
Este modelo dimensional foi criado para responder a perguntas como:
- Qual a **carga horária média** dos professores por departamento?
- Quais **cursos** são mais populares entre os professores?
- Qual a **evolução** das ofertas de disciplinas ao longo do tempo?

## Estrutura do Modelo

### **Tabela Fato: Professor**
- **Atributos:**
  - `ProfessorID` (PK)
  - `DepartamentoID` (FK)
  - `CursoID` (FK)
  - `DisciplinaID` (FK)
  - `DataOferta`
  - `CargaHoraria`

### **Dimensões:**
1. **Departamento**
   - Atributos: `DepartamentoID` (PK), `Nome`, `Campus`
2. **Curso**
   - Atributos: `CursoID` (PK), `Nome`, `Descrição`, `Nível`
3. **Disciplina**
   - Atributos: `DisciplinaID` (PK), `Nome`, `Ementa`
4. **Tempo**
   - Atributos: `DataID` (PK), `Data`, `Ano`, `Mês`, `DiaSemana`

## Diagrama Entidade-Relacionamento (DER)

```mermaid
erDiagram
  Professor {
    int ProfessorID PK
    string Nome
    int DepartamentoID
    int CursoID
    int DisciplinaID
    date DataOferta
    int CargaHoraria
  }

  Departamento {
    int DepartamentoID PK
    string Nome
    string Campus
  }

  Curso {
    int CursoID PK
    string Nome
    string Descricao
    string Nivel
  }

  Disciplina {
    int DisciplinaID PK
    string Nome
    string Ementa
  }

  Tempo {
    int DataID PK
    date Data
    int Ano
    string Mes
    string DiaSemana
  }

  Departamento ||--o{ Professor : "pertence a"
  Curso ||--o{ Professor : "ministra"
  Disciplina ||--o{ Professor : "leciona"
  Tempo ||--o{ Professor : "oferta em"
