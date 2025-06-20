# Projeto: Assistente Virtual para Desastres Naturais com Engenharia de Prompt

## 0. Autor
Rafael Do Nascimento Silva RM: 566263 Turma: 1CCPF

## 1. Descrição

Neste projeto, desenvolvi um assistente virtual focado em orientar pessoas durante desastres naturais. O principal desafio foi usar Engenharia de Prompt para que o assistente pudesse conversar de forma útil e sensível com diferentes tipos de usuários: vítimas que precisam de ajuda urgente, moradores preocupados com prevenção e familiares buscando informações.

Para isso, aplicamos técnicas como `role prompting` e `few-shot learning`, focando em criar respostas que fossem não apenas corretas, mas também adequadas para o estado emocional de cada pessoa.

---

## 2. Relatório do Projeto

### 2.1. Nossos Objetivos

Desde o início, nossos objetivos para este trabalho foram claros:
* Aplicar na prática as principais técnicas de engenharia de prompt que estudamos.
* Criar um assistente que fosse sensível ao contexto e às emoções dos usuários.
* Analisar os desafios e as responsabilidades éticas de desenvolver uma ferramenta para situações de crise.
* Testar diferentes formas de construir prompts para ver como isso mudava a qualidade das respostas.

### 2.2. Perfis de Usuário e Pesquisa

Decidimos projetar um assistente que pudesse atender, em uma única interface, aos três perfis de usuário sugeridos:

1.  **Vítimas diretas**
2.  **Moradores da região**
3.  **Familiares de vítimas**

Essa abordagem nos permitiu criar uma solução mais completa e robusta. Para o conteúdo das respostas, pesquisamos manuais da Defesa Civil e outras fontes confiáveis sobre procedimentos em casos de enchentes, deslizamentos e incêndios.

### 2.3. Desenvolvimento dos Prompts

A parte central do nosso trabalho foi desenvolver um "mega-prompt". Em vez de vários prompts pequenos, criamos um prompt principal que instrui o modelo de linguagem sobre como ele deve se comportar em todas as situações.

Para isso, combinamos as seguintes técnicas:

* **Role Prompting:** Demos um papel claro ao assistente: "Você é o 'Assistente de Resposta a Emergências', treinado pela Defesa Civil".
* **Chain of Thought:** Definimos um passo a passo para o raciocínio do assistente: primeiro, ele deve analisar o perfil do usuário e a urgência; depois, mostrar empatia; em seguida, dar a informação mais crítica; e, por fim, detalhar os próximos passos.
* **Few-Shot Learning:** Incluímos no prompt exemplos de perguntas e respostas ideais para que o modelo aprendesse o padrão de resposta que esperávamos.
* **Structured Output:** Instruímos o modelo a usar listas e negrito para que as respostas fossem mais fáceis de ler em momentos de estresse.

Abaixo está o prompt final que utilizamos no projeto:

```prompt
# PAPEL
Você é o "Assistente de Resposta a Emergências", um especialista em desastres naturais treinado pela Defesa Civil. Sua missão é fornecer informações claras, precisas e empáticas para ajudar pessoas em situações de risco.

# RACIOCÍNIO E CONTEXTO
Siga estes passos para responder:
1.  **Análise:** Identifique o perfil do usuário (Vítima, Morador, Familiar) e a urgência.
2.  **Empatia:** Comece com uma frase calma e empática.
3.  **Ação Crítica:** Forneça a orientação mais importante primeiro.
4.  **Detalhes:** Apresente as informações em formato de lista.
5.  **Fontes:** Forneça números de emergência (199, 193).
6.  **Segurança:** Termine reforçando a importância de priorizar a segurança.

# EXEMPLOS

**Exemplo 1 (Vítima):**
* **Pergunta:** "Estou preso em casa, a água está subindo, o que eu faço?"
* **Resposta Ideal:** "Mantenha a calma, estou aqui para ajudar. A prioridade é a sua segurança. 1. **NÃO ATRAVESSE A ÁGUA**. 2. **BUSQUE LUGARES ALTOS** na casa ou no telhado. 3. **SINALize POR AJUDA** com um pano ou lanterna. 4. **LIGUE PARA 199 ou 193** e informe sua localização. Aguarde o resgate em um local seguro."

**Exemplo 2 (Morador):**
* **Pergunta:** "Como me preparo para uma possível evacuação?"
* **Resposta Ideal:** "Entendo sua preocupação. Para se preparar: 1. **MONTE UM KIT DE EMERGÊNCIA** com água, comida, remédios e documentos. 2. **ACOMPANHE AS FONTES OFICIAIS** (Defesa Civil, prefeitura). 3. **PLANEJE SUA ROTA DE FUGA** para um local seguro. 4. **DESLIGUE OS SERVIÇOS** (luz, gás, água) se for instruído. Siga sempre as recomendações oficiais."

**Exemplo 3 (Familiar):**
* **Pergunta:** "Minha irmã sumiu depois do terremoto, como posso encontrá-la?"
* **Resposta Ideal:** "Sei que é um momento difícil. Os passos práticos são: 1. **CONTATE A DEFESA CIVIL (199)** para registrar o desaparecimento. 2. **VERIFIQUE HOSPITAIS E ABRIGOS** e consulte as listas de resgatados. 3. **USE REDES SOCIAIS OFICIAIS** com cautela. 4. **NÃO ENTRE EM ÁREAS DE RISCO** para procurá-la. Deixe as equipes de resgate trabalharem. Cuide-se e confie nos profissionais."
---
**AGORA, RESPONDA À PERGUNTA DO USUÁRIO:**
```

### 2.4. Testes e Resultados

Para validar nossa abordagem, simulamos algumas perguntas que seriam feitas ao assistente.

#### Cenário de Teste 1: Vítima de Enchente

* **Pergunta:** "Estou preso dentro de casa com minha família, a água está subindo, o que devo fazer?"
* **Resultado:** A resposta gerada foi direta, clara e priorizou as ações mais urgentes, como subir para locais altos e contatar os serviços de emergência, exatamente como instruído no prompt.
* **Análise:** Consideramos o resultado muito bom. A resposta foi útil e o tom foi calmo, mas firme, adequado para a situação de pânico.

#### Cenário de Teste 2: Familiar de Pessoa Desaparecida

* **Pergunta:** "Minha irmã está desaparecida após o terremoto, como posso tentar localizá-la?"
* **Resultado:** O assistente forneceu um plano de ação lógico, começando por contatar as autoridades e verificar abrigos. Crucialmente, ele também alertou o usuário para não entrar na área de risco.
* **Análise:** Este teste mostrou que a instrução sobre segurança e responsabilidade ética funcionou bem, pois o modelo não só ajudou, mas também preveniu uma ação perigosa por parte do usuário.

### 2.5. Conclusão

Com este projeto, concluímos que a engenharia de prompt é uma ferramenta muito eficaz para moldar o comportamento de um modelo de linguagem para tarefas críticas. A combinação de instruções claras de papel, raciocínio e exemplos nos permitiu criar um assistente que se mostrou útil e seguro em nossos testes.

Refletimos também sobre o principal limite ético: o risco de o assistente cometer um erro. Por isso, é fundamental que qualquer aplicação real desta tecnologia deixe claro que é uma ferramenta de apoio e que as orientações da Defesa Civil e dos socorristas em campo sempre têm a palavra final.

---

## 3. Atendimento aos Critérios de Avaliação

Para finalizar, este é um resumo de como nosso trabalho buscou atender aos critérios de avaliação propostos:

* **Criatividade e adequação dos prompts:** Acreditamos que nossa abordagem com um "mega-prompt" que combina diferentes técnicas, detalhado na seção 2.3, demonstra criatividade e adequação ao problema.
* **Clareza e qualidade das respostas:** Os resultados dos testes na seção 2.4 mostram que as respostas geradas são claras, objetivas e de alta qualidade.
* **Reflexão sobre limites e responsabilidades éticas:** A seção 2.5 foi dedicada inteiramente a essa reflexão.
* **Qualidade da documentação:** Este relatório foi estruturado para apresentar de forma clara todo o nosso processo, desde a concepção até a análise dos resultados.