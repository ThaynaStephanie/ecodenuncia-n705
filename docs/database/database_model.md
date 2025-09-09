# Modelo de Dados - EcoDenúncia

## Modelo de Dados

O modelo de dados será relacional, focado na integridade e consistência das informações. As principais entidades serão `Usuário`, `Denuncia` e `StatusDenuncia`.

## Descrição das Entidades e Relacionamentos

*   **Usuário:** Representa tanto os cidadãos que fazem as denúncias quanto os gestores da prefeitura/ONG.
    *   **Atributos:** `id` (PK), `nome`, `email` (UNIQUE), `senha_hash`, `tipo_usuario` (ENUM: 'cidadao', 'gestor'), `data_cadastro`.
*   **Denuncia:** Representa cada ocorrência de lixo irregular reportada.
    *   **Atributos:** `id` (PK), `titulo` (opcional), `descricao`, `url_foto`, `latitude`, `longitude`, `data_ocorrencia`, `data_criacao`, `id_usuario` (FK para Usuário), `id_status` (FK para StatusDenuncia).
*   **StatusDenuncia:** Tabela de lookup para os possíveis status de uma denúncia.
    *   **Atributos:** `id` (PK), `nome_status` (UNIQUE: 'Recebida', 'Em Análise', 'Resolvida', 'Rejeitada').

## Diagrama ER ou Similar

```mermaid
erDiagram
    USUARIO ||--o{ DENUNCIA : "faz"
    STATUS_DENUNCIA ||--o{ DENUNCIA : "tem"

    USUARIO {
        UUID id PK
        VARCHAR nome
        VARCHAR email UK
        VARCHAR senha_hash
        VARCHAR tipo_usuario ENUM("cidadao", "gestor")
        TIMESTAMP data_cadastro
    }

    DENUNCIA {
        UUID id PK
        VARCHAR titulo
        TEXT descricao
        VARCHAR url_foto
        DECIMAL latitude
        DECIMAL longitude
        TIMESTAMP data_ocorrencia
        TIMESTAMP data_criacao
        UUID id_usuario FK
        INT id_status FK
    }

    STATUS_DENUNCIA {
        INT id PK
        VARCHAR nome_status UK
    }

## Dicionário de Dados

### Tabela: Usuário
| Atributo | Tipo de Dado | Restrição | Descrição |
| :--- | :--- | :--- | :--- |
| id | UUID | Chave Primária | Identificador único do usuário. |
| nome | VARCHAR(255) | Obrigatório | Nome completo do usuário. |
| email | VARCHAR(255) | Único, Obrigatório | Endereço de e-mail do usuário para login. |
| senha_hash | VARCHAR(255) | Obrigatório | Hash da senha do usuário para segurança. |
| tipo_usuario | VARCHAR(10) | Obrigatório, ENUM | Tipo de usuário: 'cidadao' ou 'gestor'. |
| data_cadastro | TIMESTAMP | Obrigatório | Data e hora em que o usuário foi cadastrado. |

### Tabela: Denuncia
| Atributo | Tipo de Dado | Restrição | Descrição |
| :--- | :--- | :--- | :--- |
| id | UUID | Chave Primária | Identificador único da denúncia. |
| titulo | VARCHAR(255) | Opcional | Título opcional da denúncia. |
| descricao | TEXT | Opcional | Descrição detalhada do ponto de lixo irregular. |
| url_foto | VARCHAR(255) | Obrigatório | URL da foto da denúncia armazenada no serviço de objetos. |
| latitude | DECIMAL(10, 8) | Obrigatório | Coordenada de latitude do ponto da denúncia. |
| longitude | DECIMAL(11, 8) | Obrigatório | Coordenada de longitude do ponto da denúncia. |
| data_ocorrencia | TIMESTAMP | Obrigatório | Data e hora em que a denúncia foi realizada. |
| data_criacao | TIMESTAMP | Obrigatório | Data e hora de registro da denúncia no sistema. |
| id_usuario | UUID | Chave Estrangeira | Relacionamento com a tabela `Usuário`. |
| id_status | INT | Chave Estrangeira | Relacionamento com a tabela `StatusDenuncia`. |

### Tabela: StatusDenuncia
| Atributo | Tipo de Dado | Restrição | Descrição |
| :--- | :--- | :--- | :--- |
| id | INT | Chave Primária | Identificador único do status. |
| nome_status | VARCHAR(50) | Único, Obrigatório | Nome do status da denúncia (e.g., 'Recebida', 'Em Análise'). |
