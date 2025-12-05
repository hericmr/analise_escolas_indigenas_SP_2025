# Documentação Metodológica: Visualizações Gráficas

Este documento detalha a metodologia, fontes de dados e processamento utilizado para a geração das visualizações gráficas sobre as Escolas Estaduais Indígenas de São Paulo (SEDUC 2025).

## 1. Alunos por Escola Indígena (Com Total)
- **Arquivo de Saída**: `output/alunos_por_escola_com_total.png`
- **Script Gerador**: `scripts/plotting/plot_alunos.py`
- **Fonte de Dados**: `base_de_dados/escolas.csv`
- **Variáveis Utilizadas**:
    - `Nome` (Nome da Escola)
    - `Tipo` (Filtro: deve ser 'EEI - INDIGENA')
    - `Total_Alunos` (Quantidade numérica de alunos)
- **Processamento**:
    - Filtragem apenas por escolas do tipo 'EEI - INDIGENA'.
    - Conversão da coluna `Total_Alunos` para numérico (erros tratados como 0).
    - Ordenação decrescente pelo número de alunos.
- **Visualização**:
    - **Tipo**: Gráfico de Barras Vertical.
    - **Eixo X**: Nome da Escola.
    - **Eixo Y**: Número de Alunos.
    - **Detalhes**: Rótulos com o valor exato no topo de cada barra.

## 2. Relação Alunos vs. Docentes
- **Arquivo de Saída**: `output/alunos_vs_docentes.png`
- **Script Gerador**: `scripts/plotting/plot_alunos_vs_docentes.py`
- **Fonte de Dados**:
    - `base_de_dados/escolas.csv`
    - `base_de_dados/docentes.csv`
- **Processamento**:
    - **Cálculo de Docentes**: Agrupamento da tabela `docentes.csv` por escola (`CIE_Escola`), contando professores únicos (distintos por nome).
    - **Unificação**: Junção (merge) com a tabela `escolas.csv` através do código da escola (`CIE` / `CIE_Escola`).
    - Tratamento de valores nulos (substituídos por 0) e conversão para numérico.
- **Visualização**:
    - **Tipo**: Gráfico de Dispersão (Scatter Plot).
    - **Eixo X**: Número Total de Alunos.
    - **Eixo Y**: Número Total de Docentes.
    - **Objetivo**: Visualizar a correlação entre o tamanho do corpo discente e docente.

## 3. Distribuição de Escolas por Faixa de Alunos
- **Arquivo de Saída**: `output/distribuicao_alunos_final_posicionado_v2.png`
- **Script Gerador**: `scripts/plotting/plot_distribuicao.py`
- **Fonte de Dados**: `base_de_dados/escolas.csv`
- **Processamento**:
    - Categorização ("Binning") do número de alunos nas seguintes faixas:
        - Até 10 alunos
        - 11 a 25 alunos
        - 26 a 50 alunos
        - 51 a 100 alunos
        - Mais de 100 alunos
    - Contagem de escolas em cada faixa.
- **Visualização**:
    - **Tipo**: Gráfico de Pizza (Pie Chart).
    - **Detalhes**: Fatias "explodidas" (separadas do centro) para destaque. Percentual e valor absoluto exibidos nas fatias relevantes. Uso da paleta de cores 'viridis'.

## 4. Distribuição de Equipamentos
- **Arquivo de Saída**: `output/equipamentos_distribuicao.png`
- **Script Gerador**: `scripts/plotting/plot_equipamentos_distribuicao.py`
- **Fonte de Dados**: `base_de_dados/equipamentos.csv`
- **Processamento**:
    - Agrupamento por `Equipamento` e soma da coluna `Quantidade`.
    - Ordenação ascendente por quantidade total.
- **Visualização**:
    - **Tipo**: Gráfico de Barras Horizontal.
    - **Eixo X**: Quantidade Total.
    - **Eixo Y**: Tipo de Equipamento.
    - **Detalhes**: Quantidade exata exibida ao lado de cada barra.

## 5. Escolas por Diretoria de Ensino
- **Arquivo de Saída**: `output/escolas_por_diretoria.png`
- **Script Gerador**: `scripts/plotting/plot_escolas_por_diretoria.py`
- **Fonte de Dados**: `base_de_dados/escolas.csv`
- **Processamento**:
    - Contagem de ocorrências únicas por `Diretoria`.
    - Ordenação ascendente.
- **Visualização**:
    - **Tipo**: Gráfico de Barras Horizontal.
    - **Eixo X**: Número de Escolas.
    - **Eixo Y**: Diretoria de Ensino.
    - **Objetivo**: Mostrar a concentração regional/administrativa das escolas indígenas.

## 6. Tipos de Ensino Oferecidos
- **Arquivo de Saída**: `output/tipos_ensino.png`
- **Script Gerador**: `scripts/plotting/plot_tipos_ensino.py`
- **Fonte de Dados**: `base_de_dados/turmas_por_tipo.csv`
- **Variáveis Analisadas**:
    - Anos Iniciais, Anos Finais, EJA (Anos Iniciais/Finais/Médio), Ensino Infantil.
- **Processamento**:
    - Verificação coluna a coluna: Conta-se, para cada tipo de ensino, quantas escolas possuem valor > 0 (ou seja, oferecem aquela modalidade).
- **Visualização**:
    - **Tipo**: Gráfico de Barras Vertical.
    - **Eixo X**: Tipo de Ensino (ex: Anos Iniciais, Ensino Infantil).
    - **Eixo Y**: Número de Escolas que oferecem.
    - **Detalhes**: Rótulos inclinados 45 graus para legibilidade.
