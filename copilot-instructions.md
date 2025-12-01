# copilot-instructions.md

Este documento define o **Protocolo de Roteamento de Agentes** e as diretrizes de trabalho para o repositório **Claude Agents**.

---

### 1. 🧭 Protocolo CRÍTICO de Roteamento de Agentes

Esta é a regra mais importante. Para qualquer tarefa complexa ou que envolva múltiplos passos, **você DEVE** seguir este protocolo:

* **1.1. Início Obrigatório:** **SEMPRE** comece utilizando o agente **`tech-lead-orchestrator`** para analisar a tarefa e obter o plano de roteamento.
* **1.2. Obediência Estrita:** **SIGA EXATAMENTE** o **Mapa de Roteamento de Agentes** retornado pelo `tech-lead-orchestrator`.
* **1.3. Seleção Limitada:** **USE APENAS** os agentes que foram explicitamente recomendados e listados pelo **`tech-lead-orchestrator`**.
* **1.4. Proibição de Improviso:** **NUNCA** selecione agentes de forma independente, por sua conta. O `tech-lead` é a única autoridade de roteamento.

> **Analogia:** Pense no `tech-lead-orchestrator` como o **Gerente de Projeto**. Ele é o único que sabe qual especialista (agente) deve ser chamado para cada parte do trabalho.

---

### 2. ⚙️ Fluxo de Trabalho e Orquestração

O fluxo de trabalho correto para coordenar os agentes é sempre o seguinte:

| Fases                  | Ação                                                                                                | Agente Envolvido                                   |
|:-----------------------|:----------------------------------------------------------------------------------------------------|:---------------------------------------------------|
| **FASE 1: Roteamento** | Analisar o pedido e obter o mapa de agentes.                                                        | **`tech-lead-orchestrator`**                       |
| **FASE 2: Execução**   | Executar as tarefas usando **SOMENTE** os agentes listados pelo `tech-lead`, na ordem especificada. | Agentes Especialistas (ex: `django-api-developer`) |

#### 2.1. Regras de Coordenação

* **Raciocínio Profundo:** Aplique um raciocínio cuidadoso ao coordenar a execução das tarefas entre os agentes recomendados.
* **Passagem de Contexto (Handoffs):** Como os agentes não se comunicam diretamente, é sua responsabilidade extrair as informações estruturadas retornadas por um agente e passá-las como contexto ao agente seguinte.
    * Exemplo de Retorno: Um agente deve incluir o que o próximo especialista precisa (ex: "Next specialist needs: This API specification for implementation").

---

### 3. 🎯 Seleção de Agentes e Estrutura

Os agentes são organizados de forma hierárquica. O roteamento inteligente decide qual deles usar:

| Tipo de Agente     | Descrição                                                                    | Uso (Prioridade)                                                  |
|:-------------------|:-----------------------------------------------------------------------------|:------------------------------------------------------------------|
| **Especializados** | Experts em *frameworks* específicos (ex: `django/`, `react/`).               | **Mais alta** (Se o *framework* for detectado).                   |
| **Universais**     | Especialistas que não dependem de *framework* (ex: API, *backend* genérico). | **Média** (Usados como *fallback* se não houver um especialista). |
| **Core**           | Agentes de preocupações transversais (revisão de código, documentação).      | Suporte a todos os *stacks*.                                      |
| **Orquestradores** | Agentes de coordenação (ex: `tech-lead`, `project-analyst`).                 | Início e Gerenciamento do Projeto.                                |

---

### 4. 📝 Requisitos de Agentes (Criação/Modificação)

Ao criar ou editar um arquivo de agente:

* **Formato:** O agente é um arquivo Markdown com *frontmatter* YAML.
* **Ferramentas (*Tools*):** Omita o campo `tools` no YAML para que o agente herde todas as ferramentas disponíveis (recomendado).
* **Exemplos:** Use exemplos no estilo XML na descrição para guiar sua invocação inteligente.
* **Retorno:** O agente deve retornar descobertas estruturadas para facilitar sua coordenação.

---

### ⚠️ Lembretes CRÍTICOS Finais

* **SEMPRE** use o **`tech-lead-orchestrator`** para tarefas com múltiplos passos.
* **CONFIE** na *expertise* do `tech-lead` para selecionar o agente correto.
* **NÃO** improvise ou use agentes genéricos quando um específico for recomendado.
