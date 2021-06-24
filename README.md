# Projeto `<Correlação de dados de imagens de RM e dados genéticos em paciente com Esclerose Lateral Amiotrófica (ELA)>`
# Project `<MRI Imaging and Genetic Data Correlation on Amyotrophic Lateral Sclerosis (ALS) Patients>`


## Indice

1. Apresentação
2. Descrição do Projeto
3. Perguntas de Pesquisa
4. Base de Dados
5. Metodologia
6. Ferramentas
7. Cronograma
8. Estrutura de Diretórios

## 1. Apresentação

O presente projeto foi originado no contexto das atividades da disciplina de pós-graduação [*Ciência e Visualização de Dados em Saúde*](https://github.com/datasci4health/home), oferecida no primeiro semestre de 2021, na Unicamp.

| Nome | RA | Especialização |
|--|--|--|
| Felipe Frazatto | 146001 | Engenharia Elétrica |
| João Pedro N. Gonçalves | 227991 | Farmácia |
| Renata Prôa | 224637 | Matemática |

> Um breve vídeo de apresentação do projeto está disponível no Google Drive pelo link a seguir: [Vídeo da Proposta](https://drive.google.com/file/d/14wwlC784iaPo-pFCyMjoqUAnqoewHfpT/view?usp=sharing)

## 2. Descrição do Projeto

A Esclerose Lateral Amiotrófica (ELA) é uma doença neurodegenerativa que afeta o sistema motor dos pacientes. Alterações progressivas e cumulativas na musculatura de todo corpo leva na maioria dos casos a uma eventual morte por complicações respiratórias de 3 a 5 anos após começarem tais sintomas. Do ponto de vista genético 90% dos casos de ELA são esporádicos (ELAs) e apenas 10% dos casos são familiares (ELAf), porém aproximadamente 70% dos casos de ELAf já possuem um gene candidato, contra apenas 10% dos casos de ELAs. Os genes mais frequentes encontrados tanto em casos de ELAf quanto em casos de ELAs são C9orf72, FUS, TARDBP e SOD1.

Apesar de diversas técnicas serem empregadas na identificação da ELA, o tempo médio que um paciente leva para receber o diagnóstico correto é de 12 a 18 meses. Na prática os pacientes com ELA são submetidos a Ressonância Magnética (RM) apenas com a finalidade de se excluir outras patologias, mas talvez seja possível extrair informações dessas imagens, "features", que possam não somente classificar os casos de ELA, como também identificar os substratos anatômicos cerebrais que subdividem os pacientes, tendo em vista essa variabilidade genética. Durante esse trabalho será tratado como features, todos números ou medidas obtidas das imagens de RM.

Sendo assim, nosso grupo prõpoe analisar divergências anatômicas do cortéx cerebral (matéria cinzenta) aplicando a técnica de morfometria baseada em "voxel" (pixel 3D) selecionando os dados sobre o volume e a espessura cortical obtidos a partir das imagens de T1 ponderadas e analisar dados de estruturas axonais (matéria branca) a partir da técnica de imagem de tensor de difusão "DTI" em controles e pacientes diagnosticados com ELAs e ELAf atendidos regularmente no HC Unicamp. Do grupo dos ELAf foram selecionados aqueles que possuíam maior representatividade (Casos de C9orf72 e VAPB) e também foram utilizadas informações sobre a idade, sexo dos pacientes e controles.

> A seguir está um link para um vídeo expositivo do projeto: [Vídeo da Apresentação Final](https://drive.google.com/file/d/1B7IrWRsjD3mj0n888kyfIzax0t_VchdH/view?usp=sharing)


## 3. Perguntas de Pesquisa

* A partir de informações sobre o volume, expessura média, medidas de difusão e a anisotropia fracionada dos diversos substratos anatômicos cerebrais, é possível diferenciar os subtipos de ELA?

## 4. Bases de Dados

### Imagens de RM
* Fonte: Ambulatório de Neurologia do HC da Unicamp
* Conteúdo: 91 RM de pacientes diagnosticados com ELA e controles pareados por sexo e idade.
* Para a extração de features de volume e expressura foram utilizadas todas as 91 amostras, porém apenas 87 delas foram utilizadas para extração de informações difisuvidade média (MD) e anisotropia fracionada (FA).

> Será utilizado das imagens de T1 as métricas de volume, rugosidade, profundidade de sulcos. Já para análise das imagens de DTI serão usadas as medidas de anisotropia Fracional (FA), difusividade média (MD), difusividade Axial (AD) e difusividade radial (RD).
> Os dados de análise de significância das regiões cerebrais conforme os parâmetros descritos acima, ou seja, quais features são releventes para construção do nosso classificador estão em data/processed desse repositório.

### Dados Genéticos
* Fonte: Dados genéticos obtidos através do pipeline de análise empregado no diagnóstico genético e molecular dos pacientes do Ambulatório de Neurologia do HC da Unicamp.
* Conteúdo: Informações sobre os subtipos genéticos de ELA.
   
## 5. Metodologia

As imagens de T1 foram primeiramente convertidas do formato DICOM para o formato NIfTI com o software 'Dicom2Nii', e em seguida processadas com o software Freesurfer. O Freesurfer primeiramente faz o Skull Stripping, isto é, a remoção da caixa craniana, identifica as principais regiões do cérebro (Volumetric Labeling), normalização da intensidade e a segmentação da substância branca. Em seguida a imagem é registrada num espaço padrão e um atlas é aplicado para que possam ser identificados os giros (parcelamento). Como resultado deste processo de segmentação e percelamento automáticos, obtivemos as medidas de volume para todas as 113 regiões identificadas. 

Quanto às imagens de difusão, estas foram processadas com as ferramentas 'DTI Mapping' e 'DTI MultiAtlas Segmentation' do MRI Cloud (https://braingps.mricloud.org/dtimultiatlasseg). Para tal, as imagens DICOM foram primeiro convertidas em imagens 'Raw Image' (.raw) e arquivos 'Data Parameter File' (.dpf) com um conversor do 'DTI Mapping'. As imagens de difusão foram então ajustadas para o modelo tensorial de DTI (Diffusion Tensor Imaging) pelo 'DTI Mapping' e salvas em formato High Dynamic Range (.hdr). Em seguida, as imagens de DTI foram registradas num espaço padrão (MNI) e um atlas foi aplicado utilizando o 'DTI MultiAtlas Segmentation' e foi calculada a soma dos autovalores principais em cada uma das regiões identificadas. A partir disto, calculamos as medidas de difusão médias nestas regiões, são elas: Anisotropia Fracional (FA), Difusividade Média (MD), Difusividade Axial (AD) e Difusividade Radial (RD). As métricas de difusão extraídas e as informações de volumetria foram utilizadas como features para treinar os modelos.

Para classificar os sujeitos entre saudáveis e pacientes de ELA, treinamos três diferentes tipos modelo para comparação, são eles: regressão logistica, Support Vector Machine (SVM) e Random Forest. De cada um dos tipos, treinamos três modelos, um utilizando apenas os dados de difusão, outro utilizando somente os dados de volumetria e o terceiro utilizando ambos os dados de difusão e volumetria. Para classifcar os pacientes de ELA entre os três subtipos (ELAs, VAPB e C9orf72), treinamos apenas um tipo de modelo (Random Forest), sendo três modelos utilizando os mesmos três conjuntos de dados (dados de difusão, dados de voumetria e dado de difusão mais volumetria).

Previamente ao treinamento dos modelos, as features tais que para ao menos um sujeito não havia dados foram removidas da análise. A escolha de remover tais features foi feita com base no fato de que dispunhamos de um excesso de features em comparação com o número de sujeitos (alta dimensionalidade). Também foi feita uma análise da variância das features e foram excluídas as features com variância muito próxima de zero (Near Zero Variance). Em seguida, foi feita uma Análise de Componentes Principais (PCA) e os dados foram divididos nos conjuntos de Treino, Validação e Teste (60%, 20% e 20% respectivamete). Por fim, foi feita uma normalização das features (método Standard Scaler da biblioteca Scikit-Learn do Python) e o treinamento dos três modelos. Nos modelos de regressão logistica foi feita regularização através de um LASSO (Least Absolute Shrinkage and Selection Operator). Para todos os modelos foi calculada a matriz de confusão, a acurácia e foi feito um K-Fold Cross Validation com K = 100.

## 6. Resultados

O nosso estudo mostrou que é possível a construção de um classificador de ELA numa causuística que incluia pacientes com dois tipos de ELAf, casos de ELAs e controles saudáveis. Também foi possível construir um classificar dos subtipos de ELA com certa acurácia.
> Para o classificador de ELA, o modelo que apresentou os melhores resultados foi o de regressão logística, com acurácia de 77% e cross validation score de 0.84.
> [Matriz de Confusão do Modelo de Regressão Logística DTI + T1](assets/1.png)
> Já o classificador de subtipos de ELA, que utiliza o algoritmo de random forest, obteve uma acurácia de 74% e cross validation score de 0.79.
> [Matriz de Confusão do Modelo Random Forest DTI + T1](assets/2.png)

Tabela 14: somatória das features que tiveram algum significado estatístico quando comparados incialmente pacientes com controles e quando comparamos os subtipos de ELA.

Comparação: Saudável vs ELA
| Dataset | numberFeatures |
| --- | --- |
| t1 | 55 |
| dti | 228 |
| all | 283 |


Comparação: Subtipos de ELA
| Dataset | Alvo1 | Alvo2 | numeroFeatures |
| --- | --- | --- | --- |
| t1 | ELAs | c90rf72 | 47 |
| t1 | ELAs | vapb | 11 |
| t1 | c9orf72 | vapb | 47 |
| dti | ELAs | c90rf72 | 304 |
| dti | ELAs | vapb | 185 |
| dti | c9orf72 | vapb | 304 |
| all | ELAs | c90rf72 | 351 |
| all | ELAs | vapb | 196 |
| all | c9orf72 | vapb | 351 |

## 7. Discussão

Apesar da alta sensibilidade dos dois modelos (92% e 100%) o primeiro modelo possui baixa especificidade (28%) e o segundo sofre com baixa acurácia de dois subtipos (82% esporadica, 67% c9orf72 e 57% vapb). Atribuímos isso a uma alta dimensionalidade do dados, que também impacta negativamente o treinamento dos modelos, causando overfitting na etapa de treinamento e baixissimas acurácias nos conjuntos de validaçao e teste.
É importante salientar que o Teste T de Student não pode ser utilizado como seleção de features, já que ele não leva em consideração interações entre as variáveis, sendo necessário utilizar outros métodos como PCA ou LASSO, no entanto, a quantidade de features que possuem diferenças significativas entre os grupos servem de forte indício que é possível discriminar os diversos grupos.
O uso da tecnicas de feature selection (como o near zero variance,  pca e LASSO) ajudam a minimizar esse problema, mas o numero baixo de obseravações, especialmente quando divididas em subtipos de ELA, ainda prejudicam a elaboração de modelos mais robustos.

## 8. Conclusão

Os resultados são promissores, porém ambos os modelos sofrem com a baixa quantidade de observações e alta dimensionalidade. Acreditamos que esse trabalho pode ser encarado como um pipeline para a elaboração de classificadores para ELA, podendo ser aprimorado conforme o banco de dados adquire novas entradas.
 
## 9. Ferramentas

* Freesurfer
* Acapuco
* MRICloud
* Jupyter Notebooks/Colab
* Python
* Scikit-Learn

## 10. Cronograma
> A primeira etapa seria a etapa de análise das imagens. Dado que ainda não tivemos contato com as imagens é difícil estimar quanto tempo levará. Mas achamos que levaremos em torno de 8 semanas para realizar isso.
> A correlação com os dados clínicos pode levar em torno de 4 semanas caso haja necessidade de tabularmos.
> A escrita do projeto final e ocorrerá concomitantemente.

## 11. Estrutura de Diretórios

```shell
ds4h
├── assets
├── data
│   ├── external
│   ├── interim
│   ├── processed
│   └── raw
├── models
├── notebooks
├── references
├── reports
│   └── figures
└── src
    ├── data
    ├── features
    ├── models
    └── visualization



```
