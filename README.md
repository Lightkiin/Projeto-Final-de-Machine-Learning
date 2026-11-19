# Projeto Final — K-means para janelas prováveis de recompra

## Entrega reproduzida com a base integral

A entrada **online+retail.zip**, fornecida pelo usuário, contém **Online Retail.xlsx** com **541.909 linhas e 8 colunas**. O notebook importa todas elas (sem amostragem) e documenta a exclusão de operações inválidas/anônimas. O modelo K-means final é ajustado com **todas as 6.535 fotografias temporais de treino**; a amostra de até 2.500 fotografias é utilizada **apenas para estimar silhueta** durante a seleção de K.

Resultado após a limpeza: **392.692 linhas**, **4.338 clientes**, **18.532 faturas válidas**. Houve 12.926 fotografias cliente-data, divididas cronologicamente em 6.535 de treino, 1.890 de validação e 4.501 de teste.

## Arquivos

- `online+retail.zip`: dados públicos originais da UCI, ZIP preservado.
- `Projeto_Final_Kmeans_Recompra.ipynb`: código-fonte para executar a partir do início.
- `Projeto_Final_Kmeans_Recompra_EXECUTADO.ipynb`: mesmo notebook **executado**, com saídas e gráficos incorporados.
- `Relatorio_Final_Kmeans_Base_Completa.docx` e `.pdf`: relatório com resultados reais e referências.
- `Apresentacao_Final_Kmeans_Base_Completa.pptx`: defesa com 14 slides e resultados reais.
- `resultados_projeto/`: 10 gráficos PNG e CSVs de auditoria, fotografias, métricas, previsão para cada observação de teste, taxas por mês e recomendações retrospectivas.
- `requirements.txt`: dependências de Python.

## Como reproduzir

1. Extraia **todo** o pacote ZIP em uma pasta, mantendo `online+retail.zip` ao lado dos `.ipynb`. Não é necessário descompactar o dataset.
2. Abra um terminal nessa pasta. Instale Python 3.10 ou superior e as dependências: `python -m pip install -r requirements.txt`.
3. Execute `jupyter notebook` e abra `Projeto_Final_Kmeans_Recompra.ipynb`.
4. Clique em **Run All / Executar tudo**, de cima para baixo. O notebook lê preferencialmente o ZIP local original. Uma nova pasta `resultados_projeto/` será preenchida.
5. Para consultar os valores sem reexecutar o estudo, abra `Projeto_Final_Kmeans_Recompra_EXECUTADO.ipynb` e o relatório completo.

A execução validada ocorreu em Python 3.13.5 / pandas 2.2.3 / scikit-learn 1.8.0 com semente 42. A reprodução pode ter pequenas diferenças entre versões de bibliotecas. Computador com pelo menos 4 GB de RAM recomendado para a leitura do arquivo XLSX. A primeira instalação de dependências exige acesso ao repositório de pacotes; **a base de dados já está incluída**.

## Métricas verificadas no teste (outubro–novembro/2011)

| Modelo | Precisão | Recall | F1 | Acurácia |
|---|---:|---:|---:|---:|
| K-means + taxa histórica por grupo | 0,4561 | 0,8638 | **0,5970** | 0,5281 |
| Árvore de decisão | 0,5631 | 0,6129 | 0,5869 | **0,6510** |
| Sempre recomendar recompra | 0,4046 | 1,0000 | 0,5761 | 0,4046 |
| Classe majoritária | 0,0000 | 0,0000 | 0,0000 | 0,5954 |

K-means: três grupos, silhueta amostral 0,241, limiar de recomendação selecionado em validação = 0,20. Taxas de recompra de treino dos três grupos: 0,69; 0,19; 0,32. ROC-AUC do K-means = 0,6645, da árvore = 0,7002.

## Interpretação correta

O projeto avalia **nova compra registrada em até 30 dias** em uma loja histórica, não prevê o **dia mais barato** nem qual SKU será comprado. Os resultados são retrospectivos e NÃO se referem à data presente. Não foram geradas operações sintéticas. Há imputação apenas de atributos derivados quando necessário, com mediana ajustada no treino.

## Referências publicadas

- CHEN, D.; SAIN, S. L.; GUO, K. (2012). *Data mining for the online retail industry: A case study of RFM model-based customer segmentation using data mining*. Journal of Database Marketing & Customer Strategy Management, 19(3), 197–208. https://doi.org/10.1057/dbm.2012.17
- FADER, P. S.; HARDIE, B. G. S.; LEE, K. L. (2005). *“Counting Your Customers” the Easy Way: An Alternative to the Pareto/NBD Model*. Marketing Science, 24(2), 275–284. https://doi.org/10.1287/mksc.1040.0098
- UCI Machine Learning Repository. *Online Retail*. https://archive.ics.uci.edu/dataset/352/online+retail (CC BY 4.0).
