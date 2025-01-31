# Dinâmica: Design Estratégico do Projeto

## Objetivo
Identificar os subdomínios do projeto, classificá-los (Core, Supporting, Generic) e desenhar os bounded contexts, incluindo suas interações. Esse exercício ajudará a criar uma visão clara e estratégica do domínio.

---

## 1. Nome do Projeto
Sistema de Zeladoria Urbana

---

## 2. Objetivo Principal do Projeto
Plataforma que permite aos cidadãos apontar problemas na sua comunidade, notifica-los aos gestores urbanos e acompanhar o status das mesmas.

---

## 3. Identificação dos Subdomínios
Liste os subdomínios do sistema e classifique-os como **Core Domain**, **Supporting Subdomain** ou **Generic Subdomain**.

| **Subdomínio**              | **Descrição**                                                                                      | **Tipo**         |
|-----------------------------|--------------------------------------------------------------------------------------------------|------------------|
| Gestão de Ordem de Serviço | Gerencia as OSs, encaminha para a empresas prestadora especifica daquele serviço e mostra o tracking | Core Domain      |
| Gestão de Mapas de Calor | Com base nos problemas relatados mostra disponibiliza vários mapas de calor para os gestores para auxiliar no planejamento das cidades | Core Domain      |
| Gestão de Usuários | Cadastra os usuários do tipo cidadãos, gestor e prestadores e Autenticação                                         | Generic          |
| Gestão de Empresas Prestadores| Cadastra de empresas prestadores de serviço                                            | Generic          |
| Serviços em Cloud AWS  | Servidores EC2, Bucket para imagens S3 e banco de dados RDS                               | Supporting       |

---

## 4. Desenho dos Bounded Contexts
Liste e descreva os bounded contexts identificados no projeto. Explique a responsabilidade de cada um.

| **Bounded Context**           | **Responsabilidade**                                                                                 | **Subdomínios Relacionados** |
|-------------------------------|-----------------------------------------------------------------------------------------------------|-----------------------------|
| Contexto de OSs | Gerencia as ordens de serviço. Encaminha as OSs para as empresas prestadoras e manda para o cidadão o tracking | Gestão de Ordem de Serviço   |
| Contexto de Analise    | Gera mapas de calor com base nos problemas identificados | Gestão de Mapas de Calor |
| Contexto de Usuário    | Cadastra todos os tipos de usuários e disponibiliza os acessos pertinentes a cada um | Gestão de Usuários |
| Contexto de Prestadores de Serviço    | Cadastra as empresas prestadoras e qual é o tipo da prestação do serviço | Contexto de Prestadores de Serviço |

---

## 5. Comunicação entre os Bounded Contexts
Explique como os bounded contexts vão se comunicar. Use os padrões de comunicação, como:
- **Mensageria/Eventos (desacoplado):** Ex.: O Contexto de Consultas emite um evento "Consulta Finalizada", consumido pelo Contexto de Pagamentos.
- **APIs (síncrono):** Ex.: O Contexto de Pagamentos consulta informações de preços no Contexto de Consultas.

| **De (Origem)**              | **Para (Destino)**          | **Forma de Comunicação**    | **Exemplo de Evento/Chamada**                  |
|------------------------------|-----------------------------|-----------------------------|-----------------------------------------------|
|Gestão de Usuários | Gestão de Ordem de Serviço | API  | Usuários tipo cidadão - Obtém OSs e seus status|
|Gestão de Usuários | Gestão de Ordem de Serviço | API  | Usuários tipo Prestador - Obtém as OSs pendentes de atendimento |
|Gestão de Usuários | Gestão de Ordem de Serviço | API  | Usuários tipo gestor - Visualiza todas as OSs de todos os prestadores e todos os cidadãos|
|Gestão de Ordem de Serviço | Gestão de Empresas Prestadores | Mensageria (Evento)  | Cria uma OSs na fila de atendimento desta empresa |
|Gestão de Usuários | Gestão de Mapas de Calor | API  | Obtém quais mapas podem ser vistos|
|Gestão de Mapas de Calor | Gestão de Ordem de Serviço | API  | Renderização dos mapas|


---

## 6. Definição da Linguagem Ubíqua
Liste os termos principais da Linguagem Ubíqua do projeto. Explique brevemente cada termo.

| **Termo**                    | **Descrição**                                                                                   |
|------------------------------|-----------------------------------------------------------------------------------------------|
| Cidadão                | É quem aponta os problemas.                                                       |
| Gestor                | Gestor público que monitora e cobra empresas prestadoras de serviço.                                                      |
| Prestador                 | A empresa que presta o serviço (Iluminação, Limpeza e etc).                                                 |
| OS                 | Ordem de serviço que contém a solicitação a ser atendida                                                 |

---

## 7. Estratégia de Desenvolvimento
Para cada tipo de subdomínio, explique a abordagem para implementação:
- **Core Domain:** Desenvolver internamente com foco total.
- **Supporting Subdomain:** Desenvolver internamente ou parcialmente terceirizar.
- **Generic Subdomain:** Usar ferramentas ou serviços de mercado.

| **Subdomínio**              | **Estratégia**                         | **Ferramentas ou Serviços (se aplicável)** |
|-----------------------------|---------------------------------------|-------------------------------------------|
| Gestão de Ordem de Serviço         | Desenvolvimento interno               |                                           |
| Gestão de Mapas de Calor          | Desenvolvimento interno               |                                           |
| Gestão de Usuários        | Interno com uso de Auth0 para login   | Auth0                                     |
| Gestão Empresas Prestadores           | Desenvolvimento interno               |                                           |

---

## 8. Diagrama Visual (Opcional, mas Recomendado)
Desenhe um diagrama que mostre:
- Os bounded contexts.
- Como eles se comunicam.
- A relação com os subdomínios.

Use ferramentas como **Miro**, **Lucidchart** ou mesmo papel e caneta para criar seu diagrama e adicionar ao projeto.

---

## Dicas para Apresentação
- Explique cada parte do design, focando no **Core Domain** (o coração do negócio).
- Justifique por que certos subdomínios foram classificados como Supporting ou Generic.
- Destaque como a comunicação entre bounded contexts foi pensada para ser escalável.

---

Boa sorte com a dinâmica! 🚀
