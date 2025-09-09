# Especificação da API - EcoDenúncia

## Endpoints Previstos

A API será RESTful, utilizando verbos HTTP padrão e URLs descritivas.

*   **Autenticação:**
    *   `POST /api/auth/register` - Registrar novo usuário.
    *   `POST /api/auth/login` - Autenticar usuário e retornar token.
*   **Usuários:**
    *   `GET /api/users/me` - Obter dados do usuário logado. (Requer autenticação)
*   **Denúncias:**
    *   `POST /api/denuncias` - Criar uma nova denúncia. (Requer autenticação)
    *   `GET /api/denuncias` - Listar todas as denúncias (para gestores) ou denúncias do usuário (para cidadãos). (Requer autenticação)
    *   `GET /api/denuncias/:id` - Obter detalhes de uma denúncia específica. (Requer autenticação)
    *   `PUT /api/denuncias/:id/status` - Atualizar o status de uma denúncia. (Requer autenticação, apenas para gestores)
    *   `GET /api/denuncias/map` - Obter denúncias para exibição no mapa, com filtros opcionais. (Requer autenticação)
*   **Upload de Arquivos:**
    *   `POST /api/upload/image` - Fazer upload de uma imagem e retornar sua URL. (Requer autenticação)

## Parâmetros de Requisição

*   **`POST /api/auth/register`**
    *   **Body:** `{"nome": "string", "email": "string", "senha": "string", "tipo_usuario": "string"}`
*   **`POST /api/auth/login`**
    *   **Body:** `{"email": "string", "senha": "string"}`
*   **`POST /api/denuncias`**
    *   **Body:** `{"titulo": "string (opcional)", "descricao": "string", "url_foto": "string", "latitude": "number", "longitude": "number", "data_ocorrencia": "string (ISO 8601, opcional)"}`
*   **`GET /api/denuncias`**
    *   **Query Params (para gestores):** `?status=string&startDate=string&endDate=string&limit=number&offset=number`
*   **`PUT /api/denuncias/:id/status`**
    *   **Body:** `{"id_status": "number"}`
*   **`POST /api/upload/image`**
    *   **Body:** `multipart/form-data` contendo o arquivo de imagem.

## Formatos de Resposta

*   **Sucesso (2xx):**
    *   `200 OK`: Para GET, PUT, DELETE bem-sucedidos.
    *   `201 Created`: Para POST bem-sucedidos.
    *   **Body:** `{ "success": true, "data": { ... } }` ou `{ "success": true, "message": "..." }`
*   **Erro (4xx/5xx):**
    *   `400 Bad Request`: Requisição malformada.
    *   `401 Unauthorized`: Falha de autenticação.
    *   `403 Forbidden`: Sem permissão para acessar o recurso.
    *   `404 Not Found`: Recurso não encontrado.
    *   `500 Internal Server Error`: Erro no servidor.
    *   **Body:** `{ "success": false, "error": "string", "details": { ... } }`

## Autenticação e Autorização

*   **Autenticação:** Baseada em JSON Web Tokens (JWT). Após o login, o servidor emitirá um token que deverá ser incluído no cabeçalho `Authorization` (como `Bearer Token`) de todas as requisições subsequentes que exigem autenticação.
*   **Autorização:** Implementada no backend, verificando o `tipo_usuario` (cidadão ou gestor) e as permissões associadas a cada rota. Por exemplo, apenas usuários com `tipo_usuario: 'gestor'` poderão acessar o endpoint `PUT /api/denuncias/:id/status`.

## Exemplos de Chamadas e Respostas

*   **Exemplo 1: Registro de Usuário (Cidadão)**
    *   **Requisição:**
        ```http
        POST /api/auth/register
        Content-Type: application/json

        {
            "nome": "Maria Silva",
            "email": "maria.silva@example.com",
            "senha": "senhaSegura123",
            "tipo_usuario": "cidadao"
        }
        ```
    *   **Resposta (201 Created):**
        ```json
        {
            "success": true,
            "message": "Usuário registrado com sucesso!",
            "data": {
                "id": "a1b2c3d4-e5f6-7890-1234-567890abcdef",
                "email": "maria.silva@example.com"
            }
        }
        ```
*   **Exemplo 2: Criação de Denúncia**
    *   **Requisição:**
        ```http
        POST /api/denuncias
        Content-Type: application/json
        Authorization: Bearer <seu_jwt_token>

        {
            "descricao": "Lixo acumulado na esquina da Rua X com a Rua Y, próximo à praça.",
            "url_foto": "https://s3.amazonaws.com/ecodenuncia/foto_lixo_123.jpg",
            "latitude": -3.731861,
            "longitude": -38.526667,
            "data_ocorrencia": "2025-09-20T10:30:00Z"
        }
        ```
    *   **Resposta (201 Created):**
        ```json
        {
            "success": true,
            "message": "Denúncia criada com sucesso!",
            "data": {
                "id": "f1e2d3c4-b5a6-9876-5432-10fedcba9876",
                "descricao": "Lixo acumulado na esquina da Rua X com a Rua Y, próximo à praça.",
                "url_foto": "https://s3.amazonaws.com/ecodenuncia/foto_lixo_123.jpg",
                "latitude": -3.731861,
                "longitude": -38.526667,
                "data_criacao": "2025-09-20T11:00:00Z",
                "status": "Recebida"
            }
        }
        ```
*   **Exemplo 3: Atualização de Status da Denúncia (por Gestor)**
    *   **Requisição:**
        ```http
        PUT /api/denuncias/f1e2d3c4-b5a6-9876-5432-10fedcba9876/status
        Content-Type: application/json
        Authorization: Bearer <jwt_token_gestor>

        {
            "id_status": 2 // ID para "Em Análise"
        }
        ```
    *   **Resposta (200 OK):**
        ```json
        {
            "success": true,
            "message": "Status da denúncia atualizado com sucesso!",
            "data": {
                "id": "f1e2d3c4-b5a6-9876-5432-10fedcba9876",
                "novo_status": "Em Análise"
            }
        }
        ```