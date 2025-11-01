# DESAFIO QA BEEDOO 2025

Este repositório contém a documentação completa, os artefatos de teste e a análise crítica para o Desafio de Analista de Qualidade Júnior da Beedoo, focado no módulo de cadastro de cursos.

---

## 1. User Story (História de Usuário)

A História de Usuário abaixo foi criada com base na funcionalidade *existente* na aplicação fornecida para o teste.

> **Como um** Coordenador Pedagógico,
> **Eu quero** acessar um formulário para cadastrar novos cursos,
> **Para que** eles fiquem disponíveis na listagem da plataforma.

### Critérios de Aceite (AC)

* **AC1:** O formulário deve conter os campos: `Nome do curso`, `Descrição do curso`, `Instrutor`, `URL da imagem de capa`, `Data de início`, `Data de fim`, `Número de` (vagas) e `Tipo de curso`.
* **AC2:** Ao preencher todos os campos com dados válidos e clicar em "CURSO CADASTRAR", o curso deve ser criado e aparecer na tela de "Listar Cursos".
* **AC3:** O sistema **não** deve permitir o cadastro de um curso com campos obrigatórios vazios (Ex: Nome, Descrição, Instrutor, etc.).
* **AC4:** O sistema **não** deve permitir o cadastro de um curso com um `Nome` já existente.
* **AC5:** O sistema **não** deve permitir o cadastro de um curso com `Número de Vagas` negativo ou zero.
* **AC6:** O sistema **não** deve permitir o cadastro de um curso onde a `Data de fim` seja anterior à `Data de início`.
* **AC7:** O sistema **não** deve aceitar um formato de `URL` inválido (ex: um texto simples).

### Decisões Tomadas para a User Story

A User Story foi criada através de "engenharia reversa" da aplicação de teste. As decisões foram:

1.  **Escopo Simples:** A US foca apenas no "Cadastro", que é o núcleo da funcionalidade testada.
2.  **Foco em Validação:** Os Critérios de Aceite (ACs) foram escritos para cobrir as regras de negócio mais críticas que uma aplicação robusta *deveria* ter (obrigatoriedade, duplicidade, lógica de datas e valores). Estes ACs se tornaram a base para os cenários de teste de erro.

---

## 2. Metodologia e Relatório de Bugs

### Metodologia Utilizada

A metodologia de teste foi o **Teste Exploratório baseado em Cenários**.

* **Justificativa:** Sem uma documentação prévia, iniciei com um "caminho feliz" (CT-001) para entender o fluxo. Em seguida, usei técnicas de **Análise de Valor Limite** (testando "0" e "-5" em vagas) e **Partição de Equivalência** (testando campos vazios, dados inválidos, etc.) para "quebrar" sistematicamente cada campo do formulário.

### Relatório Resumido de Bugs Críticos

A aplicação apresentou **falhas graves de validação de *back-end* e de regras de negócio**. O formulário bloqueia apenas a digitação de letras em campos numéricos, mas permite a submissão de dados inválidos.

| ID do Teste | Bug Encontrado | Prioridade |
| :--- | :--- | :--- |
| **CT-007** | **Campo Obrigatório Ignorado:** O sistema permite o cadastro de curso com a "Descrição" vazia. | **ALTA** |
| **CT-008** | **Campo Obrigatório Ignorado:** O sistema permite o cadastro de curso com o "Instrutor" vazio. | **ALTA** |
| **CT-011** | **Duplicidade Permitida:** O sistema permite o cadastro de múltiplos cursos com o mesmo "Nome". | **CRÍTICA** |
| **CT-017** | **Lógica de Negócio Ignorada:** O sistema permite o cadastro de um curso com vagas negativas (ex: "-5"). | **ALTA** |
| **CT-018** | **Lógica de Negócio Ignorada:** O sistema permite o cadastro de um curso com "0" vagas. | **MÉDIA** |
| **CT-019** | **Lógica de Datas Ignorada:** O sistema permite que a "Data de Fim" seja anterior à "Data de Início". | **ALTA** |
| **CT-021** | **Formato Inválido Ignorado:** O sistema aceita "texto simples" como uma "URL da imagem", quebrando a exibição. | **MÉDIA** |

---

## 3. Sugestões de Melhoria e Análise Crítica

Durante os testes, além dos bugs de validação, foram identificadas oportunidades de melhoria funcional e de regras de negócio que aumentariam a qualidade e a robustez da aplicação, demonstrando criatividade e visão de produto.

### Melhoria 1: Funcionalidade "Editar Curso" (CRUD Incompleto)

* **Observação:** A aplicação atual permite Criar (`C`), Listar (`R`) e Excluir (`D`) cursos. No entanto, ela não possui a funcionalidade de **Editar/Atualizar (`U`)** um curso.
* **Sugestão:** Implementar um botão "Editar" em cada card de curso na listagem. Ao clicar, o usuário seria levado de volta ao formulário de cadastro, pré-preenchido com os dados do curso, permitindo a correção de informações sem a necessidade de excluir e cadastrar novamente.

### Melhoria 2: Lógica Condicional para "Tipo de Curso"

* **Observação:** O formulário possui um campo `Tipo de curso` (Online/Presencial), mas ele não tem impacto funcional. A aplicação cadastra o tipo, mas não solicita os dados específicos de cada modalidade.
* **Sugestão:** Implementar lógica condicional (campos dinâmicos), assim como foi imaginado na História de Usuário ideal:
    * **Se** `Tipo de curso` = **`Online`**, exibir um novo campo obrigatório: **`Link da Aula`** (para o Zoom, Meet, etc.).
    * **Se** `Tipo de curso` = **`Presencial`** , exibir um novo campo obrigatório: **`Endereço`** (com campos de rua, número, cidade, etc.).

### Melhoria 3: Validação Proativa de Valores Numéricos

* **Observação:** Como identificado nos bugs (CT-017, CT-018), o sistema aceita valores negativos e "0" para o `Número de vagas`.
* **Sugestão:** Além de corrigir o bug no back-end, implementar uma validação proativa no front-end, definindo o atributo `min="1"` no campo de input (`<input type="number" min="1">`). Isso impediria o usuário de submeter valores inválidos, melhorando a usabilidade.

---

## 4. Artefatos do Teste (Links)

* **[➡️ Link para a Suíte de Testes Completa (Google Sheets)]**
    * `[COLOQUE SEU LINK DO GOOGLE SHEETS AQUI]`

* **[➡️ Link para Evidências em Vídeo - MP4 (Google Drive)]**
    * `[COLOQUE SEU LINK DO GOOGLE DRIVE AQUI]`
