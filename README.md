# 1. Gestão de Usuários e Perfis de Acesso

## 1.1 Cadastro de Usuários

- Registro e manutenção dos perfis de usuário, abrangendo os seguintes níveis:
  - **Admin**
  - **Gerente de Suporte**
  - **Usuário**
  - **Analista de Suporte**
- Implementação de mecanismos de autenticação (login/senha) e recuperação de senha.

## 1.2 Controle de Acesso

- **Admin:** Acesso total ao sistema, incluindo gerenciamento de todos os usuários, configurações globais e auditoria das ações realizadas.
- **Gerente de Suporte:** Responsável pela auditoria do sistema e pelo gerenciamento de relatórios, como indicadores de SLA e demais métricas de desempenho dos chamados.
- **Analista de Suporte:** Tem acesso para gerenciar, atender e resolver os chamados designados, atualizando o status e registrando as soluções implementadas.
- **Usuário:** Permite a criação de novos chamados de suporte e o acompanhamento dos chamados abertos por ele.

---

# 2. Registro e Cadastro de Chamados

## 2.1 Formulário de Criação de Chamados

- **Campos obrigatórios:**
  - **Título:** Campo para identificar resumidamente o problema.
  - **Descrição Detalhada:** Espaço destinado para que o usuário descreva de forma completa e clara o problema enfrentado.
  - **Categoria:**
    - O campo não será preenchido manualmente pelo usuário.
    - As categorias serão pré-definidas pelo Admin, permitindo a personalização do sistema de acordo com as necessidades de cada empresa.
    - O usuário deverá selecionar uma opção da lista disponibilizada.
  - **Impacto e Alcance:**
    - Esses campos serão utilizados para definir a prioridade do chamado por meio de uma matriz.
    - **Impacto:** Opções pré-definidas (Baixo, Médio, Alto, Crítico).
    - **Alcance:** Opções que indicam a abrangência do problema: "Somente a mim", "Meu setor", "Vários setores" ou "A empresa inteira".
    - A combinação escolhida alimentará a matriz Impacto X Alcance, que determinará automaticamente o nível de prioridade do chamado.
  - **Anexar Arquivos:** Permite que o usuário envie documentos, imagens ou outros arquivos que possam auxiliar na análise e resolução do problema.
  - **Contato:**
    - Embora os dados de contato possam ser carregados a partir das informações do usuário, esse campo será mantido para que o próprio usuário informe a melhor forma de ser contatado (telefone pessoal, corporativo ou ramal), considerando situações onde possa haver problemas de acesso a outros sistemas.

## 2.2 Validação e Consistência dos Dados

- O sistema deverá validar o preenchimento de todos os campos obrigatórios.
- A matriz Impacto X Alcance deverá processar as escolhas dos campos "Impacto" e "Alcance" para atribuir automaticamente um nível de prioridade ao chamado, sem que o usuário precise indicar essa prioridade diretamente.

---

# 3. Fluxo de Encaminhamento e Gestão do Chamado

## 3.1 Aprovação de Chamados

- Chamados criados por usuários devem ser submetidos à aprovação do gestor responsável.
- Disponibilizar uma tela ou painel para que o Gestor visualize os chamados pendentes de aprovação, com as seguintes opções:
  - Aprovar o chamado para que siga para o atendimento.
  - Rejeitar o chamado, informando o motivo, evitando assim a abertura de chamados desnecessários.

## 3.2 Encaminhamento Automático e Triagem por IA

- **Encaminhamento Pós-Aprovação:** Após a aprovação do chamado, o sistema encaminhará o registro para a IA de triagem.
- **Análise pela IA:** A IA de triagem analisará os seguintes parâmetros para determinar o melhor encaminhamento:
  - Categoria do problema.
  - Complexidade do problema.
  - Histórico de chamados do usuário.
- **Direcionamento:** Com base nessa análise, a IA poderá:
  - Direcionar o chamado para um agente de IA especializado, que fornecerá respostas automáticas para problemas conhecidos.
  - Ou encaminhar o chamado para um Analista de Suporte.

## 3.3 Intervenção do Analista de Suporte

- **Opções do Analista:**
  - Tratar o chamado e marcá-lo como **encerrado** caso o problema seja resolvido.
  - Escalar o chamado para um analista mais qualificado se a complexidade do problema for maior do que a capacidade de resolução do analista inicialmente designado.

## 3.4 Estado do Chamado

- **Status do Chamado:** O chamado deverá transitar pelos seguintes status no sistema:
  - **Aberto:** Chamado recém-criado.
  - **Aprovado:** Chamado que passou pela análise inicial e foi aprovado para encaminhamento.
  - **Aguardando Resposta:** Status exclusivo para chamados encaminhados para a IA de respostas a problemas conhecidos.
  - **Com Analista:** Chamado em tratamento por um Analista de Suporte.
  - **Resolvido:** Chamado cujo problema foi solucionado.
  - **Fechado:** Chamado encerrado após confirmação da resolução.
- **Reabertura:** O sistema deverá permitir a reabertura de um chamado caso o problema persista.
- **Reincidência:** Em casos de reincidência, um novo chamado deverá ser aberto para manter um histórico detalhado e preciso.

---

# 4. IA de Triagem de Chamados

## 4.1 Análise e Classificação

- A IA de triagem analisará a descrição detalhada fornecida pelo usuário.
- Utilizará critérios objetivos para classificar o chamado com base na seguinte hierarquia:
  1. **Categoria:** Selecionada a partir das opções pré-definidas pelo Admin.
  2. **Índice da Matriz Impacto X Alcance:** Calculado com base nas escolhas do usuário nos campos de Impacto e Alcance.
  3. **Complexidade:** Avaliada a partir da descrição e demais parâmetros associados ao chamado.
  4. **Histórico do Usuário:** Considera a quantidade e natureza dos chamados anteriores.

## 4.2 Direcionamento do Chamado

- Com base na análise dos parâmetros acima, a IA de triagem definirá o encaminhamento do chamado, adotando um dos dois caminhos:
  - Encaminhar para um dos **Agentes IA de Resolução**, se o problema se enquadrar como conhecido e possuir uma solução previamente treinada.
  - Encaminhar para um **Analista de Suporte**, caso o problema exija intervenção humana ou não corresponda aos critérios para resolução automática.

---

# 5. Agentes IA de Resolução

## 5.1 Especialização dos Agentes

- O sistema poderá contar com diversos Agentes IA especializados, cada um treinado para tratar tipos específicos de problemas, por exemplo:
  - Agente especializado em **Microsoft Office**.
  - Agente para questões relacionadas a **Sistema Operacional**.
  - Agente treinado para problemas envolvendo **SAP**.
  - Agente especializado em uma **linguagem de programação** utilizada internamente pela empresa.

## 5.2 Processo de Resolução

- Cada Agente IA de Resolução receberá os dados do chamado e, com base nas informações fornecidas, deverá:
  - Gerar uma resposta em texto com a resolução proposta para o problema.
  - Solicitar ao usuário uma confirmação sobre a eficácia da solução aplicada.

---

# 6. Acompanhamento e Monitoramento de Chamados

## 6.1 Dashboard do Usuário

- Visualização em tempo real do status dos chamados (Aberto, Aprovado, Aguardando Resposta, Com Analista, Resolvido, Fechado).
- Histórico completo de chamados, contendo detalhes das ações realizadas e prazos cumpridos.

## 6.2 Painel para Gestores e Admin

- Geração de relatórios e métricas sobre:
  - Volume de chamados.
  - Tempo de resolução.
  - Índices de aprovação/rejeição.
  - Desempenho dos Analistas de Suporte.
