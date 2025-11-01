# DESAFIO QA BEEDOO 2025

Este repositório contém a documentação completa, os artefatos de teste e a análise crítica para o Desafio de Analista de Qualidade Júnior da Beedoo, focado no módulo de cadastro de cursos.

A suíte de testes completa, com todos os 20+ cenários (Gherkin, passos e evidências) está disponível na planilha de Casos de Teste vinculada na Seção 4.

---
## 📝 História de Usuário

**Como um** Coordenador Pedagógico,
**Eu quero** ter acesso a um sistema com abas para cadastro e visualização de cursos,
**Para que** eu possa facilmente gerenciar (cadastrar, visualizar e excluir) os cursos oferecidos pela instituição.

### 🎯 Critérios de Aceitação

#### 1. Navegação e Estrutura Geral

* **AC1.1:** O sistema deve ter duas abas principais: **"Cadastro de Cursos"** e **"Lista de Cursos"**.
* **AC1.2:** A aba **"Cadastro de Cursos"** deve exibir o formulário de cadastro.
* **AC1.3:** A aba **"Lista de Cursos"** deve exibir todos os cursos cadastrados em formato de **Card**, contendo um **botão de exclusão** para cada um.

#### 2. Formulário de Cadastro (Aba "Cadastro de Cursos")

| Campo | Requisito de Validação | Tipo de Dado/Entrada |
| :--- | :--- | :--- |
| **Nome do Curso** | Aceita todos os caracteres (letras, números, símbolos). | Texto (Obrigatório) |
| **Descrição do Curso** | Sem limite de caracteres. | Área de Texto (Obrigatório) |
| **Instrutor** | Padrão de texto. | Texto (Obrigatório) |
| **URL de Imagem de Capa** | Deve aceitar apenas um formato de link (URL válida). | Link/URL (Obrigatório) |
| **Data de Início** | Seleção via calendário, permitindo datas **a partir da data atual** (futuro). | Seletor de Data (Obrigatório) |
| **Data de Fim** | Seleção via calendário, permitindo datas **a partir da data atual** e **posterior à Data de Início**. | Seletor de Data (Obrigatório) |
| **Número de Vagas** | Deve aceitar **apenas números inteiros maiores que 0** ($>0$). | Número (Obrigatório) |
| **Tipo de Curso** | Lista de seleção (Dropdown) com opções: **Presencial** e **Online**. | Seleção (Obrigatório) |

* **AC2.1: Lógica Condicional (Tipo de Curso):**
    * Se for selecionado **"Presencial"**, deve abrir um campo adicional de texto para **"Endereço"**.
    * Se for selecionado **"Online"**, deve abrir um campo adicional **"Link do Curso"** que aceita **apenas formato de link (URL válida)**.
* **AC2.2: Botão "Cadastrar Curso":** O botão deve estar **desabilitado** por padrão e só deve ser **habilitado** após o **preenchimento válido de todos os campos obrigatórios**, incluindo os campos condicionais.
* **AC2.3: Fluxo de Cadastro:** Ao clicar no botão **"Cadastrar Curso"** (habilitado), as informações devem ser salvas com sucesso, um card do novo curso deve ser criado na lista, e o usuário deve ser **redirecionado automaticamente** para a aba **"Lista de Cursos"**.

#### 3. Visualização e Exclusão (Aba "Lista de Cursos")

* **AC3.1: Detalhes do Card:** Cada Card na lista deve exibir **todas as informações** preenchidas no formulário de cadastro.
* **AC3.2: Exclusão:** Cada Card deve ter um **botão de exclusão** que, ao ser acionado, remove o curso da lista permanentemente (após confirmação, se necessário - *a ser definido*).
* **AC3.3: Visualização Detalhada (Modal):** Ao clicar em qualquer parte do Card (exceto o botão de exclusão), deve ser aberto um **Modal** que exibe as informações detalhadas do curso.
* **AC3.4: Link Clicável (Online):** Se o curso for do tipo **Online**, o Modal de visualização deve exibir o campo **"Link do Curso"** como um **link clicável** para a sala/plataforma.

* ## 2. Metodologia e Relatório de Bugs

### Metodologia Utilizada

A metodologia de teste foi o **Teste Exploratório baseado em Cenários**.

* **Justificativa:** Sem uma documentação prévia, iniciei com um "caminho feliz" (CT-001) para entender o fluxo. Em seguida, usei técnicas de **Análise de Valor Limite** (testando "0" e "-5" em vagas) e **Partição de Equivalência** (testando campos vazios, dados inválidos, etc.) para "quebrar" sistematicamente cada campo do formulário e das funcionalidades da lista.

## 🚀 Sugestões de Melhorias Futuras

### 1. Funcionalidades de Gerenciamento Avançado (CRUD)

* **Editar Curso**
    * **Objetivo:** Adicionar um botão "Editar" ao Card ou Modal de visualização para permitir que o Coordenador Pedagógico atualize as informações de um curso existente, em vez de excluí-lo e recadastrá-lo.

* **Duplicar Curso**
    * **Objetivo:** Adicionar um botão para duplicar um curso. Útil para cursos recorrentes que só mudam a data e o número de vagas.

* **Arquivamento/Status**
    * **Objetivo:** Incluir um campo de status (`Ativo`, `Inativo`, `Concluído`) e uma opção de "Arquivar Curso" em vez de apenas "Excluir", mantendo o histórico.

* **Notificação de Vagas Baixas**
    * **Objetivo:** Implementar um alerta visual no Card quando o `Número de Vagas` restante atingir um limite baixo (ex: $< 5$).

* **Filtros e Pesquisa na Lista**
    * **Objetivo:** Adicionar filtros por `Tipo de Curso` (Presencial/Online), `Instrutor` e uma barra de pesquisa por `Nome do Curso` ou `Descrição` na aba "Lista de Cursos".

* **Ordenação da Lista**
    * **Objetivo:** Opção para ordenar a lista por `Data de Início` (próximo ou mais distante) ou `Nome do Curso`.

* **Preview da URL da Imagem**
    * **Objetivo:** No formulário de cadastro, exibir uma pré-visualização da imagem de capa após o Coordenador Pedagógico inserir a `URL de Imagem de Capa`, para validar se o link está correto.

* **UX na Exclusão**
    * **Objetivo:** Adicionar uma etapa de confirmação (**Modal de Confirmação**) antes de excluir permanentemente um curso, minimizando erros.

* **Seleção de Instrutores**
    * **Objetivo:** Mudar o campo `Instrutor` (atualmente texto livre) para uma **lista de seleção** que puxe dados de um cadastro de instrutores preexistente. Isso garante consistência nos nomes.

* **Integração com Calendário**
    * **Objetivo:** Oferecer a opção de sincronizar a `Data de Início` e `Data de Fim` com um calendário externo (Google Calendar, Outlook) ou do próprio sistema.

* **Upload de Arquivo (Imagem)**
    * **Objetivo:** Permitir o `upload de arquivo` para a Imagem de Capa, em vez de apenas aceitar uma URL, tornando a criação mais prática e menos dependente de links externos.


* **Autenticação e Permissões**
    * **Objetivo:** Se a aplicação for usada por mais pessoas, implementar controle de acesso para garantir que **somente** o Coordenador Pedagógico possa usar a aba de cadastro e exclusão.

* **Performance da Lista**
    * **Objetivo:** Garantir que a lista de cursos carregue rapidamente (em menos de 2 segundos), mesmo após o cadastro de centenas de cursos (teste de volume).

---

## ⚠️ Vulnerabilidades Potenciais da Aplicação Inicial

### 1. Injeção de Código (XSS e SQL Injection)

#### Cross-Site Scripting (XSS)
* **Onde Ocorre:** Campos de Texto Livre: `Nome do Curso`, `Descrição do Curso`, `Instrutor`, `Endereço`.
* **Detalhes:** O Coordenador pode inserir código malicioso (`<script>alert('hack');</script>`) nesses campos. Quando outro usuário (ou ele mesmo) visualiza o Card ou o Modal, o navegador executa o script, o que pode levar a roubo de cookies ou sessões.

#### SQL Injection (SQLi)
* **Onde Ocorre:** Formulário de Cadastro e Exclusão.
* **Detalhes:** Se a aplicação não higienizar as entradas do formulário (`Nome do Curso`, etc.) antes de construir a *query* de banco de dados, um atacante pode injetar comandos SQL que alteram, deletam ou roubam dados.

---

### 2. Validação e Manipulação de Entradas Críticas

#### Injeção de URL Maliciosa
* **Onde Ocorre:** Campos de Link/URL: `URL de Imagem de Capa`, `Link do Curso`.
* **Detalhes:** Se a validação for superficial (apenas verifica se contém "http"), um atacante pode inserir links para sites de *phishing* ou conteúdo malicioso.

#### Bypass de Validação de Números
* **Onde Ocorre:** Campo: `Número de Vagas`.
* **Detalhes:** A validação é feita no *front-end*. Um atacante pode usar ferramentas de *proxy* para enviar um valor não numérico ou um número negativo/zero diretamente para o *back-end*, causando erros ou inconsistência de dados. **A validação deve ser repetida no *back-end***.

#### Injeção de Caminho de Arquivo (Path Traversal)
* **Onde Ocorre:** `URL de Imagem de Capa`.
* **Detalhes:** Se o servidor processa a URL de forma insegura, um atacante pode tentar usar sequências como `../` na URL para acessar arquivos confidenciais no sistema operacional do servidor.

---

### 3. Falta de Controle de Acesso e Autorização

#### Quebra de Controle de Acesso (Insecure Direct Object Reference - IDOR)
* **Onde Ocorre:** Exclusão de Curso (Botão de Excluir).
* **Detalhes:** Se o ID do curso a ser excluído for facilmente previsível e enviado diretamente na requisição (ex: `DELETE /cursos/123`), um atacante não autorizado pode tentar excluir outros cursos modificando esse ID.

#### Ausência de Autenticação/Autorização
* **Onde Ocorre:** Em toda a aplicação.
* **Detalhes:** Se a aplicação não exige autenticação robusta e garante que **apenas** o Coordenador Pedagógico tem permissão, qualquer pessoa com o link do site pode manipular os cursos.

---

### 4. Vulnerabilidades de Confidencialidade e Dados

#### Exposição de Dados Sensíveis
* **Onde Ocorre:** Transmissão de Dados.
* **Detalhes:** Se a comunicação entre o navegador e o servidor não usar **HTTPS**, as informações cadastradas (nomes, links, endereços) podem ser interceptadas.

---

### ✅ Medidas Mitigadoras Recomendadas

* **Sempre Valide no *Back-end***: Nunca confie apenas nas validações de *front-end* (JavaScript). Repita todas as validações (datas, números, links) no servidor.
* **Codificação de Saída (Output Encoding)**: Use funções de *encoding* antes de renderizar dados fornecidos pelo usuário (como `Nome do Curso`) no HTML. Isso impede a execução de scripts XSS.
* **Consultas Parametrizadas**: Use *Prepared Statements* ou ORMs para todas as interações com o banco de dados para evitar SQL Injection.
* **Implementar Autenticação e Autorização**: Garanta que todas as rotas críticas (Cadastro e Exclusão) só possam ser acessadas por um usuário autenticado com a permissão correta (Coordenador Pedagógico).

---

## 4. Artefatos do Teste (Links)

* **[➡️ Link para a Suíte de Testes Completa (Google Sheets)]**
    * `https://docs.google.com/spreadsheets/d/1VLxl_z2kX3LU-CFD4hr3aIymFkuK3F5rADGRscPjWzk/edit?gid=0#gid=0`

* **[➡️ Link para Evidências em Vídeo - MP4 (Google Drive)]**
    * ` `
