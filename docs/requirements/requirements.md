
# Requisitos do Sistema - EcoDenúncia

## Requisitos Funcionais (RF)

*   **RF001:** O sistema deve permitir o cadastro e login de usuários (cidadãos).
*   **RF002:** O sistema deve permitir o cadastro e login de administradores/gestores (prefeitura/ONG).
*   **RF003:** O sistema deve permitir que o usuário (cidadão) tire uma foto ou selecione uma imagem da galeria para a denúncia.
*   **RF004:** O sistema deve capturar automaticamente a localização geográfica (latitude e longitude) da denúncia via GPS.
*   **RF005:** O sistema deve permitir que o usuário (cidadão) adicione uma descrição textual à denúncia.
*   **RF006:** O sistema deve permitir que o usuário (cidadão) envie a denúncia para o servidor.
*   **RF007:** O sistema deve exibir o histórico de denúncias enviadas pelo usuário (cidadão).
*   **RF008:** O sistema deve permitir que o usuário (cidadão) visualize o status de suas denúncias (e.g., "Recebida", "Em Análise", "Resolvida").
*   **RF009:** O sistema deve exibir todas as denúncias em um mapa interativo para administradores/gestores.
*   **RF010:** O sistema deve permitir que administradores/gestores filtrem denúncias por status, data, localização e tipo.
*   **RF011:** O sistema deve permitir que administradores/gestores atualizem o status de uma denúncia.
*   **RF012:** O sistema deve permitir que administradores/gestores atribuam denúncias a equipes de campo.
*   **RF013:** O sistema deve gerar relatórios sobre a quantidade de denúncias, status e áreas críticas.

## Requisitos Não-Funcionais (RNF)

*   **RNF001 (Performance):** O tempo de carregamento das denúncias no mapa não deve exceder 3 segundos para até 1000 denúncias.
*   **RNF002 (Segurança):** Todas as comunicações entre cliente e servidor devem ser criptografadas (HTTPS).
*   **RNF003 (Segurança):** O sistema deve implementar autenticação baseada em tokens (JWT) para acesso à API.
*   **RNF004 (Usabilidade):** A interface do usuário deve ser intuitiva e fácil de usar para cidadãos de diferentes níveis de familiaridade com tecnologia.
*   **RNF005 (Disponibilidade):** O sistema deve estar disponível 99,5% do tempo.
*   **RNF006 (Escalabilidade):** A arquitetura deve ser capaz de suportar um aumento de 50% no número de usuários e denúncias sem degradação significativa de performance.
*   **RNF007 (Compatibilidade):** O aplicativo mobile deve ser compatível com as últimas duas versões dos sistemas operacionais iOS e Android.
*   **RNF008 (Manutenibilidade):** O código-fonte deve ser modular, bem documentado e seguir padrões de codificação.

## Regras de Negócio

*   **RN001:** Uma denúncia deve conter obrigatoriamente uma foto e a localização geográfica.
*   **RN002:** Apenas administradores/gestores podem alterar o status de uma denúncia.
*   **RN003:** O status inicial de uma denúncia é "Recebida".
*   **RN004:** Denúncias resolvidas não podem ter seu status alterado novamente para "Em Análise" ou "Recebida".

## Histórias de Usuário ou Casos de Uso

*   **História de Usuário 1: Registrar Denúncia**
    *   **Como:** Um cidadão
    *   **Quero:** Registrar uma denúncia de lixo irregular com foto e localização
    *   **Para que:** A prefeitura possa tomar providências.
    *   **Critérios de Aceitação:**
        *   Consigo tirar uma foto ou selecionar da galeria.
        *   A localização é automaticamente preenchida.
        *   Consigo adicionar uma descrição.
        *   A denúncia é enviada com sucesso e aparece no meu histórico.
*   **História de Usuário 2: Acompanhar Status da Denúncia**
    *   **Como:** Um cidadão
    *   **Quero:** Ver o status das minhas denúncias enviadas
    *   **Para que:** Eu saiba se a prefeitura está agindo.
    *   **Critérios de Aceitação:**
        *   Consigo acessar uma lista das minhas denúncias.
        *   Cada denúncia exibe seu status atual.
*   **História de Usuário 3: Visualizar Denúncias no Mapa**
    *   **Como:** Um gestor da prefeitura
    *   **Quero:** Visualizar todas as denúncias em um mapa
    *   **Para que:** Eu possa identificar os pontos críticos e planejar a coleta.
    *   **Critérios de Aceitação:**
        *   O mapa exibe marcadores para cada denúncia.
        *   Ao clicar em um marcador, vejo detalhes da denúncia (foto, descrição, status).
        *   Consigo filtrar as denúncias exibidas no mapa.
*   **História de Usuário 4: Atualizar Status da Denúncia**
    *   **Como:** Um gestor da prefeitura
    *   **Quero:** Alterar o status de uma denúncia
    *   **Para que:** Eu possa indicar o progresso da resolução do problema.
    *   **Critérios de Aceitação:**
        *   Consigo selecionar uma denúncia e escolher um novo status (e.g., "Em Análise", "Resolvida").
        *   A alteração de status é registrada e visível para o cidadão.

## Perfis de Usuários

*   **Cidadão:**
    *   **Objetivo:** Denunciar lixo irregular e acompanhar o status.
    *   **Habilidades:** Usuário básico de smartphone, não requer conhecimento técnico.
    *   **Acesso:** Aplicativo mobile.
*   **Gestor/Administrador (Prefeitura/ONG):**
    *   **Objetivo:** Gerenciar denúncias, monitorar pontos críticos, planejar ações.
    *   **Habilidades:** Conhecimento básico de uso de sistemas web, capacidade de análise de dados.
    *   **Acesso:** Plataforma web.