# EcoDenúncia: Plataforma Multiplataforma para Denúncia e Gestão de Descarte Irregular de Lixo

## Objetivo do Projeto

O principal objetivo do sistema **EcoDenúncia** é **facilitar e agilizar o processo de denúncia de descarte irregular de lixo** por parte dos cidadãos, ao mesmo tempo em que **otimiza a gestão e a resposta dos órgãos públicos e ONGs** responsáveis pela limpeza urbana e fiscalização ambiental. Busca-se, assim, contribuir para a construção de **cidades mais limpas, sustentáveis e com maior engajamento cívico**.

## Descrição Funcional da Solução Planejada

O EcoDenúncia é uma aplicação multiplataforma (web e mobile) que visa empoderar cidadãos a reportar pontos de descarte irregular de lixo em suas comunidades. A plataforma permitirá que usuários tirem fotos, marquem a localização e enviem denúncias de forma rápida e intuitiva. Órgãos públicos (como prefeituras) e ONGs poderão acompanhar esses pontos críticos, gerenciar as denúncias, planejar e monitorar as ações de coleta e limpeza, contribuindo para cidades mais limpas e sustentáveis.

## Problema Abordado e Justificativa

*   **Problema Abordado:** O descarte irregular de lixo é um problema ambiental e de saúde pública significativo em muitas cidades, incluindo Fortaleza. Ele contribui para a proliferação de pragas, enchentes, poluição do solo e da água, e degradação da paisagem urbana. A falta de um canal eficiente e acessível para a população denunciar esses pontos dificulta a ação rápida e coordenada dos órgãos responsáveis.
*   **Justificativa:** Uma plataforma como o EcoDenúncia oferece uma solução tecnológica direta para este problema, facilitando a comunicação entre cidadãos e autoridades. Ao centralizar as denúncias e permitir o monitoramento em tempo real, a aplicação otimiza a gestão de resíduos, promove a participação cívica e contribui diretamente para a melhoria da qualidade de vida e do meio ambiente urbano.

## Objetivos do Sistema

*   **Objetivo Geral:** Desenvolver uma plataforma multiplataforma que facilite a denúncia de descarte irregular de lixo por cidadãos e o gerenciamento dessas denúncias por órgãos públicos e ONGs, visando a melhoria da gestão ambiental urbana.
*   **Objetivos Específicos:**
    *   Permitir que usuários registrem denúncias de lixo irregular com fotos e localização geográfica.
    *   Fornecer um painel de controle para prefeituras e ONGs visualizarem, gerenciarem e atualizarem o status das denúncias.
    *   Mapear os pontos críticos de descarte irregular de lixo.
    *   Facilitar a comunicação entre denunciantes e órgãos responsáveis.
    *   Contribuir para a conscientização ambiental da população.

## Escopo do Projeto

*   **Funcionalidades Principais:**
    *   **Para Cidadãos (Mobile e Web):**
        *   Cadastro e login de usuário.
        *   Registro de denúncia com foto (galeria ou câmera no mobile; upload de arquivo no web).
        *   Marcação automática da localização via GPS (no mobile) ou seleção/busca no mapa (no web).
        *   Adição de descrição textual à denúncia.
        *   Visualização do histórico de denúncias enviadas.
        *   Acompanhamento do status da denúncia (recebida, em análise, resolvida).

    *   **Para Órgãos Públicos/ONGs (Web):**
        *   Cadastro e login de administradores/gestores.
        *   Visualização de todas as denúncias em um mapa interativo.
        *   Filtro e busca de denúncias por status, localização, data.
        *   Atualização do status da denúncia.
        *   Atribuição de denúncias a equipes de campo.
        *   Geração de relatórios sobre pontos críticos e ações realizadas.
*   **Não Escopo:**
    *   Sistema de gamificação para usuários.
    *   Integração direta com sistemas de logística de coleta de lixo existentes (pode ser uma fase futura).
    *   Módulo financeiro para gestão de custos de coleta.

## Visão Geral da Arquitetura com Diagrama

A arquitetura proposta será baseada em um modelo cliente-servidor, com uma API RESTful como intermediário.

*   **Frontend:**
    *   **Mobile:** Aplicativo nativo ou híbrido (React Native/Flutter) para iOS e Android.
    *   **Web:** Aplicação web (React/Angular/Vue.js) para o painel de gestão.
*   **Backend:**
    *   API RESTful para comunicação entre o frontend e o banco de dados.
    *   Linguagem de programação: Node.js (Express.js) ou Python (Django/Flask).
    *   Serviços de geolocalização (Google Maps API, OpenStreetMap).
    *   Serviço de armazenamento de imagens (Cloudinary, AWS S3).
*   **Banco de Dados:**
    *   Relacional (PostgreSQL/MySQL) para dados estruturados (usuários, denúncias, status).
    *   Não relacional (MongoDB) para armazenamento de metadados de imagens ou logs (opcional).

```mermaid
graph TD;
    A[Usuário Mobile] --> B[API RESTful];
    C[Gestor Web] --> B;
    B --> D[Banco de Dados (PostgreSQL)];
    B --> E[Serviço de Armazenamento de Imagens (AWS S3)];
    B --> F[Serviço de Mapas (Google Maps API)];
```
## Lista de Tecnologias Propostas

*   **Frontend Mobile:** React Native ou Flutter (para desenvolvimento multiplataforma eficiente).
*   **Frontend Web:** React.js ou Vue.js (para interfaces de usuário dinâmicas).
*   **Backend:** Node.js com Express.js (para API RESTful escalável).
*   **Banco de Dados:** PostgreSQL (para robustez e integridade dos dados).
*   **Armazenamento de Imagens:** AWS S3 ou Cloudinary.
*   **Mapas:** Google Maps API ou Mapbox.
*   **Controle de Versão:** Git/GitHub.
*   **Ferramentas de Prototipagem:** Figma.
*   **Ferramentas de Diagramação:** Draw.io.

## Cronograma de Desenvolvimento para a Etapa 2 (N708)

Este cronograma é uma estimativa e pode ser ajustado.

*   **Mês 1: Desenvolvimento do Backend e API**
    *   Sprints 1-2: Configuração do ambiente, modelagem de dados inicial, implementação de autenticação e autorização.
    *   Sprints 3-4: Desenvolvimento dos endpoints da API para denúncias (criação, leitura, atualização de status), usuários e gestão.
*   **Mês 2: Desenvolvimento do Frontend Mobile**
    *   Sprints 5-6: Configuração do ambiente mobile, desenvolvimento das telas de login/cadastro, tela de denúncia (foto, localização, descrição).
    *   Sprints 7-8: Implementação da visualização do histórico de denúncias, integração com a API.
*   **Mês 3: Desenvolvimento do Frontend Web e Testes**
    *   Sprints 9-10: Desenvolvimento do painel de gestão web (mapa, listagem de denúncias, filtros, atualização de status).
    *   Sprints 11-12: Testes de integração, testes de usabilidade, correção de bugs, preparação para deploy.

# Integrantes da Equipe e Seus Papéis

- **André Silva De Oliveira**: Líder do Projeto / Arquiteto de Software  
- **André Silva De Oliveira**: Desenvolvedor Backend  
- **Natan Aguiné Holanda**: Desenvolvedor Frontend Mobile  
- **Henrique Correia De Lima**: Desenvolvedor Frontend Web  
- **Thayná Stephanie Da Silva**: Especialista em UX/UI / Prototipagem  
- **Thayná Stephanie Da Silva**: Analista de Requisitos / Documentador  


## Relação com o ODS 11: Cidades e Comunidades Sustentáveis

O projeto EcoDenúncia se alinha diretamente com o Objetivo de Desenvolvimento Sustentável (ODS) 11, que visa tornar as cidades e os assentamentos humanos inclusivos, seguros, resilientes e sustentáveis. Ao fornecer uma ferramenta para a gestão eficiente do descarte de resíduos, a plataforma contribui para:

*   **Redução do Impacto Ambiental Negativo:** O mapeamento e a rápida remoção de lixo irregular diminuem a poluição do solo, da água e do ar, além de prevenir enchentes e a proliferação de doenças.
*   **Melhoria da Qualidade de Vida Urbana:** Cidades mais limpas são mais agradáveis, seguras e saudáveis para seus habitantes.
*   **Participação Cidadã:** A plataforma empodera os cidadãos a serem agentes ativos na construção de suas comunidades, promovendo a governança participativa e a responsabilidade compartilhada.
*   **Infraestrutura Resiliente:** Ao identificar e resolver problemas de descarte, a cidade se torna mais resiliente a eventos climáticos extremos e a problemas de saúde pública.

A arquitetura proposta, com sua capacidade de coletar dados georreferenciados e fornecer um painel de gestão para autoridades, é fundamental para a criação de cidades mais inteligentes e sustentáveis, permitindo uma resposta ágil e baseada em dados aos desafios ambientais urbanos.
