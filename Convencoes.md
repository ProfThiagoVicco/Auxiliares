# 📌 Guia de Convenções de Desenvolvimento C#

Este documento define os padrões de nomenclatura, estilo e design de código para garantir a manutenibilidade e a qualidade técnica do projeto.

---

## 1. Nomenclatura (Naming Conventions)

Seguimos as diretrizes oficiais da Microsoft para o ecossistema .NET:

| Elemento | Padrão | Exemplo |
| :--- | :--- | :--- |
| **Classes, Records e Enums** | `PascalCase` | `MovieProfile`, `UserRole` |
| **Interfaces** | `IPascalCase` (Prefixo I) | `IRecommendationEngine` |
| **Métodos** | `PascalCase` | `CalculateAffinity()`, `AddRating()` |
| **Propriedades Públicas** | `PascalCase` | `public Guid Id { get; }` |
| **Variáveis Locais** | `camelCase` | `var movieTotal = 0;` |
| **Parâmetros de Métodos** | `camelCase` | `(string title, int releaseYear)` |
| **Campos Privados (Fields)** | `_camelCase` (Underscore) | `private readonly List<Rating> _ratings;` |

---

## 2. Padrões de Identificação

* **Tipo de Dado:** Uso obrigatório de `Guid` (Globally Unique Identifier) para chaves primárias.
* **Atribuição:** Os identificadores devem ser imutáveis após a criação e gerados preferencialmente no construtor da entidade ou classe base.
* **Formato:** `public Guid Id { get; private set; } = Guid.NewGuid();`

---

## 3. Programação Orientada a Objetos (POO)

O código deve seguir o paradigma de **Domain Models Ricos**, evitando o antipadrão de Classes Anêmicas.

### Encapsulamento e Proteção de Estado
* **Acesso Restrito:** Propriedades devem utilizar `private set` ou `init` para impedir modificações externas acidentais.
* **Validação de Invariantes:** O estado do objeto deve ser validado no momento da criação (construtor) e em métodos de alteração. Se um dado for inválido, o código deve lançar uma exceção imediatamente.
* **Tell, Don't Ask:** Não extraia dados do objeto para realizar lógica externa. O objeto deve conter o comportamento (métodos) para processar seus próprios dados.

### Implementação dos Pilares
1.  **Abstração:** Uso de classes `abstract` para modelos de base que não devem ser instanciados sozinhos.
2.  **Herança:** Especialização de classes para compartilhar atributos e comportamentos comuns (ex: `BaseEntity`).
3.  **Encapsulamento:** Exposição apenas do necessário através de modificadores de acesso (`public`, `private`, `protected`).
4.  **Polimorfismo:** Implementação de interfaces e sobrescrita de métodos (`override`) para comportamentos dinâmicos.

---

## 4. Padronização de WebAPI (REST)

* **Recursos (URIs):** Substantivos no plural e em letras minúsculas (ex: `/movies`, `/users`).
* **Verbos HTTP:**
    * `GET`: Leitura e consulta (sem efeitos colaterais).
    * `POST`: Criação de novos recursos ou execução de lógicas de negócio complexas.
* **Responsabilidade:** Controllers devem atuar apenas como orquestradores, delegando a lógica de negócio para as classes de domínio.

---

## 5. Boas Práticas de Código (Clean Code)

* **Single Responsibility (SRP):** Cada classe e método deve ter uma única responsabilidade clara.
* **Nomes Semânticos:** Evite abreviações. Nomes de classes e métodos devem ser verbais e descrever exatamente o que fazem.
* **DRY (Don't Repeat Yourself):** Centralize lógicas comuns em classes base ou serviços utilitários.
