# Changelog

## Versão 3.4-alpha – Fase 1.8A – Infraestrutura de Parâmetros de Atualização (29/07/2026)

### Adicionado
- Criada a infraestrutura inicial da **Guia 5 – Atualização**.
- Criada tela administrativa oculta para gerenciamento de parâmetros de atualização.
- Implementado acesso à tela administrativa por atalho:
  `CTRL + SHIFT + E`.
- Implementado módulo `js/admin-encadeamentos.js`.
- Implementada criação de JSONs independentes de parâmetros de atualização.
- Implementado suporte à criação de parâmetros de:
  - Correção monetária;
  - Juros de mora.
- Implementada seleção do tipo de parâmetro na tela administrativa:
  - `correcao_monetaria`;
  - `juros_mora`;
  - `selic` reservado para fase futura;
  - `taxa_legal` reservado para fase futura.
- Implementada tela administrativa com:
  - Nome do encadeamento;
  - Descrição;
  - Tipo do parâmetro;
  - Tabela de períodos;
  - Índice;
  - Data inicial;
  - Data final;
  - Adição e remoção de linhas;
  - Validação do encadeamento;
  - Exportação de JSON;
  - Importação de JSON.
- Implementado carregamento de JSON de correção monetária na Guia 5.
- Implementado carregamento de JSON de juros de mora na Guia 5.
- Implementada exibição, na Guia 5, dos dados do parâmetro carregado:
  - Nome;
  - Descrição;
  - Índices utilizados;
  - Quantidade de períodos.
- Criadas variáveis globais para uso futuro:
  - `window.parametrosCorrecaoAtual`;
  - `window.parametrosJurosAtual`;
  - `window.parametrosSelicAtual`.
- Criada função preparatória `coletarDiferencasParaAtualizacao()`, destinada à futura integração da Guia 5 com a Guia 4.
- Implementada sincronização inicial entre os campos da Guia 1 e da Guia 5:
  - Data de Atualização;
  - Início dos Juros.

### Alterado
- Reestruturada a apresentação inicial da **Guia 5 – Atualização**.
- Substituídos os antigos campos visuais de critério de correção e critério de juros por botões de carregamento de JSON:
  - **Carregar JSON de Correção**;
  - **Carregar JSON de Juros**.
- Mantidos os campos `criterioCorrecao` e `criterioJuros` como campos ocultos para preservar compatibilidade com a exportação/importação do JSON do caso.
- Ajustado o layout da Guia 5 para separar:
  - Datas de referência;
  - Parâmetros de correção monetária;
  - Parâmetros de juros de mora;
  - Aviso de módulo em construção.
- Padronizada a largura dos botões de carregamento de JSON na Guia 5.
- Adicionado estilo para exibição dos status de parâmetros carregados:
  - `#statusCorrecao`;
  - `#statusJuros`.

### Corrigido
- Corrigida incompatibilidade causada pela remoção dos antigos campos `criterioCorrecao` e `criterioJuros`, que eram utilizados por `js/json.js`.
- Eliminado erro na importação de JSON do caso:
  `Cannot set properties of null (setting 'value')`.
- Restaurado o funcionamento do botão **Exportar Dados do Caso** após inclusão dos campos ocultos de compatibilidade.
- Corrigido o carregamento dos botões da Guia 5:
  - `btnCarregarCorrecao`;
  - `btnCarregarJuros`.
- Corrigida a abertura da tela administrativa via `CTRL + SHIFT + E`.
- Corrigida a criação dinâmica do modal administrativo.
- Corrigido conflito potencial com função existente na Guia 4, evitando recriação global de `converterCompetenciaParaNumero`.
- Criada função própria `adminCompetenciaParaNumero()` para uso exclusivo da administração de encadeamentos.
- Corrigido o parse de valores brasileiros na função preparatória `coletarDiferencasParaAtualizacao()`.
- Corrigida a validação de períodos para impedir sobreposição.
- Corrigida a validação de períodos abertos, permitindo no máximo um período sem data final.
- Corrigida a coleta de linhas da tabela administrativa para não ignorar linhas incompletas.
- Evitada duplicação de eventos ao abrir e fechar o modal administrativo repetidas vezes.

### Homologação

Testes aprovados:

- Importação de JSON do caso sem erro.
- Exportação de JSON do caso funcionando.
- Guia 5 aberta corretamente.
- Botão **Carregar JSON de Correção** funcionando.
- Botão **Carregar JSON de Juros** funcionando.
- Tela administrativa aberta por `CTRL + SHIFT + E`.
- Criação de encadeamento de correção monetária pela tela administrativa.
- Validação de sobreposição entre períodos.
- Rejeição de período sobreposto:
  - Exemplo: `IPCAE 01/2000 a 12/2025` com `INPC 01/2025 aberto`.
- Validação positiva de períodos encadeados:
  - Exemplo: `IPCAE 01/2000 a 12/2025` e `INPC 01/2026 aberto`.
- Exportação de JSON de correção monetária.
- Carregamento de JSON de correção monetária na Guia 5.
- Exibição correta do parâmetro de correção carregado:
  - Nome;
  - Descrição;
  - Índices;
  - Quantidade de períodos.
- Rejeição de JSON de juros quando carregado no campo de correção.
- Rejeição de JSON de correção quando carregado no campo de juros.
- Exportação de JSON de juros de mora.
- Carregamento de JSON de juros de mora na Guia 5.
- Preservação da Guia 4.
- Preservação do motor de evolução previdenciária.
- Nenhum cálculo financeiro implementado nesta fase.

### Observação Técnica
Esta fase implementa apenas a infraestrutura de parâmetros da atualização monetária e dos juros de mora.  
A Guia 5 ainda não realiza cálculo de correção monetária, juros, SELIC ou taxa legal.  
O cálculo financeiro será implementado em fase posterior, a partir dos parâmetros carregados e das diferenças apuradas na Guia 4.

---

## Versão 3.3 – Fase 1.7D2 (28/07/2026)

### Adicionado
- Implementado cálculo do Abono Anual (13º) na Guia 4.
- Inclusão automática de competências no formato `13º/AAAA`.
- Implementada função de cálculo de avos com regra dos 15 dias.
- Implementado suporte ao primeiro 13º de benefícios previdenciários comuns.
- Implementado suporte ao cálculo de 13º para benefícios baseados em salário mínimo.
- Adicionada opção **"Incluir 13º proporcional no ano final aberto"** na Guia 1.
- Implementada persistência da opção em exportação/importação JSON.
- Implementado cálculo individualizado do 13º para benefício devido e benefícios recebidos.

### Alterado
- Guia 4 passou a calcular o 13º utilizando a mesma base exibida nas competências da tabela (`obterValorIntegral()`).
- Reestruturada a lógica de geração da linha `13º/AAAA` para o ano final.
- Ajustada a memória da Guia 3 para exibir apenas a evolução mensal do benefício recebido.
- Re-renderização da memória da Guia 3 após recálculo.
- Ajustado o destaque visual das linhas de 13º para um modelo mais discreto e uniforme entre Chrome e Edge.
- Removido destaque visual excessivo (fundo azul e bordas fortes) da linha de 13º.
- Mantido apenas o texto da competência em azul/negrito.

### Corrigido
- Corrigido o cálculo do primeiro 13º quando a memória do benefício possuía apenas competências de reajuste.
- Corrigida a obtenção da base de cálculo do 13º para memórias resumidas.
- Corrigido o comportamento do ano final aberto.
- Corrigido o cálculo proporcional do 13º do benefício devido até a Data Final.
- Corrigido o cálculo do 13º dos benefícios recebidos com DCB dentro do período.
- Corrigida a limitação do 13º dos recebidos quando a DCB ocorre após a Data Final.
- Impedido que a DIP do benefício devido seja interpretada como DCB.
- Corrigida a restauração de competências de 13º na Central de Alterações Manuais.
- Corrigida a funcionalidade "Restaurar Todas".
- Corrigida recursão infinita em `relatorios.js`.
- Eliminado erro:
  `Maximum call stack size exceeded`.
- Restaurada a exibição da Central de Competências Modificadas após edição manual.
- Corrigida compatibilidade da importação JSON após inclusão do módulo de 13º.

### Homologação
Testes aprovados:

- Ano final aberto sem DCB e opção desmarcada.
- Ano final aberto com opção marcada.
- Benefício recebido com DCB dentro do período.
- Benefício recebido com DCB posterior à Data Final.
- Ano final completo em dezembro.
- DIP do devido sem efeito de DCB.
- Edição e restauração de competências.
- Importação e exportação JSON.
- Compatibilidade visual entre Chrome e Edge.
