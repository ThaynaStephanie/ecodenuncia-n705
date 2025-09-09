# Arquitetura do Sistema - EcoDenúncia

## Descrição da Arquitetura

A arquitetura do EcoDenúncia será baseada em um modelo de microsserviços (ou uma arquitetura monolítica bem modularizada, dependendo da complexidade inicial e da equipe), com uma API RESTful como ponto central de comunicação. O sistema será dividido em três camadas principais:

1.  **Camada de Apresentação (Frontend):** Responsável pela interface do usuário.
    *   **Mobile App:** Para cidadãos, desenvolvido com React Native/Flutter para compatibilidade iOS e Android.
    *   **Web Dashboard:** Para gestores, desenvolvido com React.js/Vue.js.
2.  **Camada de Lógica de Negócio (Backend/API):** Responsável por processar as requisições, aplicar as regras de negócio e interagir com o banco de dados e serviços externos.
    *   Desenvolvido com Node.js (Express.js).
    *   Contém módulos para autenticação, gestão de usuários, gestão de denúncias, integração com serviços de geolocalização e armazenamento de arquivos.
3.  **Camada de Dados:** Responsável pelo armazenamento e recuperação de informações.
    *   **Banco de Dados Relacional:** PostgreSQL para dados estruturados e transacionais.
    *   **Serviço de Armazenamento de Objetos:** AWS S3 ou Cloudinary para armazenamento de imagens das denúncias.

## Componentes do Sistema

*   **Mobile Application:**
    *   Módulo de Autenticação (Login/Cadastro)
    *   Módulo de Denúncia (Câmera/Galeria, Geolocalização, Descrição)
    *   Módulo de Histórico de Denúncias
*   **Web Dashboard:**
    *   Módulo de Autenticação (Login)
    *   Módulo de Visualização de Mapa de Denúncias
    *   Módulo de Gestão de Denúncias (Filtros, Atualização de Status)
    *   Módulo de Relatórios
*   **API Gateway (Backend):**
    *   Serviço de Autenticação e Autorização
    *   Serviço de Usuários
    *   Serviço de Denúncias
    *   Serviço de Upload de Arquivos
*   **Database:**
    *   Tabelas para Usuários, Denúncias, Status de Denúncias.
*   **External Services:**
    *   Google Maps API / Mapbox (para mapas e geolocalização).
    *   AWS S3 / Cloudinary (para armazenamento de imagens).

## Padrões Arquiteturais Utilizados

*   **Cliente-Servidor:** Separação clara entre a interface do usuário e a lógica de negócio/dados.
*   **API RESTful:** Para comunicação padronizada e sem estado entre o frontend e o backend.
*   **MVC (Model-View-Controller) ou MVVM (Model-View-ViewModel):** Para organização do código no frontend e backend, promovendo a separação de responsabilidades.
*   **Camadas (Layered Architecture):** Divisão do sistema em camadas lógicas (apresentação, lógica de negócio, dados) para modularidade e manutenibilidade.

## Diagrama de Arquitetura

```mermaid
graph TD

    subgraph Frontend
        A[Mobile App (React Native/Flutter)]
        B[Web Dashboard (React.js/Vue.js)]
    end

    subgraph Backend (Node.js/Express.js)
        C(API Gateway)
        D(Serviço de Autenticação)
        E(Serviço de Usuários)
        F(Serviço de Denúncias)
        G(Serviço de Upload de Arquivos)
    end

    subgraph Data Layer
        H[PostgreSQL Database]
        I[AWS S3 / Cloudinary]
    end

    subgraph External Services
        J[Google Maps API / Mapbox]
    end

    A -- HTTP/S Requests --> C
    B -- HTTP/S Requests --> C

    C -- Calls --> D
    C -- Calls --> E
    C -- Calls --> F
    C -- Calls --> G

    F -- Reads/Writes --> H
    G -- Stores/Retrieves --> I
    F -- Uses --> J