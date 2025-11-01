# DESAFIO QA BEEDOO 2025

Este repositório contém a documentação completa, os artefatos de teste e a análise crítica para o Desafio de Analista de Qualidade Júnior da Beedoo, focado no módulo de cadastro de cursos.

A suíte de testes completa, com todos os 20+ cenários (Gherkin, passos e evidências) está disponível na planilha de Casos de Teste vinculada na Seção 4.

---

## 1. User Story (História de Usuário)

A História de Usuário abaixo foi criada com base na funcionalidade *existente* na aplicação fornecida para o teste (conforme CT-001).

> **Como um** Coordenador Pedagógico,
> **Eu quero** acessar um formulário para cadastrar novos cursos,
> **Para que** eles fiquem disponíveis na listagem da plataforma.

### Critérios de Aceite (AC)

* **AC1:** O usuário deve ser capaz de cadastrar um curso com todos os dados válidos (CT-001).
* **AC2:** O sistema **não** deve permitir o cadastro de um curso com campos obrigatórios vazios (CT-002, CT-006, CT-007, CT-008, CT-009, CT-010).
* **AC3:** O sistema **não** deve permitir o cadastro de um curso com um `Nome` já existente (CT-011).
* **AC4:** O sistema **não** deve permitir o cadastro de um curso com `Número de Vagas` negativo ou zero (CT-015, CT-016).
* **AC5:** O sistema **não** deve permitir o cadastro de um curso onde a `Data de fim` seja anterior à `Data de início` (CT-003).
* **AC6:** O sistema **não** deve aceitar um formato de `URL` inválido (CT-017).
* **AC7:** O campo "Link da aula" deve ser obrigatório se o tipo for "Online" (CT-005).
* **AC8:** O sistema **deve** permitir que um curso criado seja excluído da listagem (CT-018).

---

## 2. Metodologia e Relatório de Bugs

### Metodologia Utilizada

A metodologia de teste foi o **Teste Exploratório baseado em Cenários**.

* **Justificativa:** Sem uma documentação prévia, iniciei com um "caminho feliz" (CT-001) para entender o fluxo. Em seguida, usei técnicas de **Análise de Valor Limite** (testando "0" e "-5" em vagas) e **Partição de Equivalência** (testando campos vazios, dados inválidos, etc.) para "quebrar" sistematicamente cada campo do formulário e das funcionalidades da lista.

### Relatório Resumido de Bugs Críticos

A aplicação apresentou **falhas graves de validação e de funcionalidades básicas**. O formulário não valida regras de negócio no *back-end* e funcionalidades essenciais (como exclusão e lógica condicional) estão quebradas.

| ID do Teste | Bug Encontrado | Prioridade |
| :--- | :--- | :--- |
| **CT-015** | **DADO CORROMPIDO:** O sistema aceita vagas negativas (ex: "-5") e as exibe de forma corrompida na listagem como **"-5 ANOS"**. | **CRÍTICA** |
| **CT-018** | **FUNCIONALIDADE QUEBRADA:** O botão "EXCLUIR CURSO" não funciona. | **ALTA** |
| **CT-011** | **Duplicidade Permitida:** O sistema permite o cadastro de múltiplos cursos com o mesmo "Nome". | **ALTA** |
| **CT-006** | **Campo Obrigatório Ignorado:** "Nome do curso" vazio é aceito. | **ALTA** |
| **CT-007** | **Campo Obrigatório Ignorado:** "Descrição" vazia é aceita. | **ALTA** |
| **CT-008** | **Campo Obrigatório Ignorado:** "Instrutor" vazio é aceito. | **ALTA** |
| **CT-009** | **Campo Obrigatório Ignorado:** "URL da imagem" vazia é aceita. | **ALTA** |
| **CT-010** | **Campo Obrigatório Ignorado:** "Número de Vagas" vazio é aceito. | **ALTA** |
| **CT-005** | **Lógica Quebrada:** Permite cadastrar curso "Online" com "Link da aula" vazio. | **MÉDIA** |
| **CT-003** | **Lógica de Datas Ignorada:** Permite que a "Data de Fim" seja anterior à "Data de Início". | **MÉDIA** |
| **CT-017** | **Formato Inválido Ignorado:** Aceita "meu teste" como uma "URL da imagem" (exibe imagem em branco). | **MÉDIA** |

---

## 3. Sugestões de Melhoria e Análise Crítica

Durante os testes, foram identificadas funcionalidades ausentes e oportunidades de melhoria que não são bugs, mas sim falhas de requisito ou design.

### Melhoria 1: Funcionalidade "Editar Curso" Ausente (GAP-001)

* **Observação:** A aplicação está com o ciclo CRUD (Create, Read, Update, Delete) incompleto. O Criar (`C`) e o Ler (`R`) funcionam (embora `C` seja bugado), mas o **Excluir (`D`) está quebrado (Bug CT-018)** e o **Editar/Atualizar (`U`) é inexistente (GAP-001)**.
* **Sugestão:** Implementar a funcionalidade de "Editar" para permitir ao usuário corrigir dados do curso sem precisar excluí-lo e criá-lo novamente.

### Melhoria 2: Lógica de Negócio para "Vagas"

* **Observação:** O formulário pede "Número de Vagas" para todos os tipos de curso. Isso não faz sentido de negócio para um curso "Online", que (geralmente) tem vagas ilimitadas.
* **Sugestão:** Ocultar o campo "Número de Vagas" quando o "Tipo de curso" for "Online" para evitar confusão do usuário e dados desnecessários.

### Melhoria 3: Correção de UI/UX (CT-019)

* **Observação:** Os botões e links de navegação para o cadastro estão com o texto "Curso Cadastrar" (Substantivo + Verbo).
* **Sugestão:** Corrigir o texto para o padrão "Cadastrar Curso" (Verbo + Substantivo), melhorando a leitura e o profissionalismo da interface.

---

## 4. Artefatos do Teste (Links)

* **[➡️ Link para a Suíte de Testes Completa (Google Sheets)]**
    * `https://docs.google.com/spreadsheets/d/1VLxl_z2kX3LU-CFD4hr3aIymFkuK3F5rADGRscPjWzk/edit?gid=0#gid=0`

* **[➡️ Link para Evidências em Vídeo - MP4 (Google Drive)]**
    * ` `
