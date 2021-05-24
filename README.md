# Projeto `<Correlação de dados de imagens de RM e dados clínicos em paciente com Esclerose Lateral Amiotrófica (ELA)>`
# Project `<MR Imaging and Clinical Data Correlation on Amyotrophic Lateral Sclerosis (ALS) Patients>`

## ToDo List

> - [x] Cookiecutter DS (Ler instruções)
> - [x] Github
> - [x] Tabela Nome/RA
> - [ ] Organizar Notebooks
> - [ ] Organizar Artigos
> - [x] Vídeo de apresentação

---------

> - [x] Apresentação
> - [x] Descrição
> - [x] Perguntas de Pesquisa
> - [x] Base de Dados
> - [x] Metodologia
> - [x] Ferramenta
> - [X] Cronograma

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
| Pedro Lelis | 233896 | Ciência da Computação |
| Renata Prôa | 224637 | Matemática |


## 2. Descrição do Projeto

A Esclerose Lateral Amiotrófica (ELA) é uma doença neurodegenerativa que afeta o sistema motor dos pacientes. Alterações progressivas e cumulativas na musculatura de todo corpo leva na maioria dos casos a uma eventual morte por complicações respiratórias de 3 a 5 anos após começarem tais sintomas. Do ponto de vista genético 90% dos casos de ELA são esporádicos (ELAs) e apenas 10% dos casos são familiares (ELAf), porém aproximadamente 70% dos casos de ELAf já possuem um gene candidato, contra apenas 10% dos casos de ELAs. Os genes mais frequentes encontrados tanto em casos de ELAf quanto em casos de ELAs são C9orf72, FUS, TARDBP e SOD1.

Apesar de diversas técnicas serem empregadas na identificação da ELA, o tempo médio que um paciente leva para receber o diagnóstico correto é de 12 a 18 meses.Na prática os pacientes com ELA são submetidos a Ressonância Magnética (RM) apenas com a finalidade de se excluir outras patologias, mas talvez seja possível extrair informações dessas imagens que possam não somente classificar os casos de ELA, como também identificar os substratos anatômicos cerebrais que subdividem os pacientes, tendo em vista essa variabilidade genética.

Sendo assim, nosso grupo prõpoe analisar divergências anatômicas do cortéx cerebral (matéria cinzenta) aplicando a técnica de morfometria baseada em "voxel" (pixel 3D) selecionando os dados sobre o volume e a espessura cortical e analisar dados de estruturas axonais (matéria branca) a partir da técnica de imagem de tensor de difusão "DTI" em controles e pacientes diagnosticados com ELAs e ELAf atendidos regularmente no HC Unicamp. Do grupo dos ELAf foram selecionados aqueles que possuíam maior representatividade (Casos de C9orf72 e VAPB) e também foram utilizadas informações sobre a idade, sexo dos pacientes e controles.

> Um breve vídeo de apresentação do projeto está disponível no Google Drive pelo link a seguir: [Vídeo de Apresentação](https://drive.google.com/file/d/14wwlC784iaPo-pFCyMjoqUAnqoewHfpT/view?usp=sharing)

## 3. Perguntas de Pesquisa

* A partir de informações sobre o Volume, Expessura média e indíces de difusão de substratos anatômicos cerebrais, é possível diferenciar os subtipos de ELA?

## 4. Bases de Dados

Imagens de RM
* Fonte: Ambulatório de Neurologia do HC da Unicamp
* Conteúdo: 91 RM de pacientes diagnosticados com ELA e controles pareados por sexo e idade.
> 
Dados Genéticos
* Fonte: Dados genéticos obtidos através do pipeline de análise empregado no diagnóstico genético e molecular dos pacientes do Ambulatório de Neurologia do HC da Unicamp.
* Conteúdo: Informações sobre os subtipos genéticos de ELA.

## 5. Metodologia

> Subdividir os grupos de pacientes e controles. O grupo dos pacientes conterá os subgrupos, sals (ELAs), vap (VAPB) e c9o (C9orf72)

> Realizar análise exploratória dos dados para compreender as diversas variáveis e estruturas dos dados, possivelmente identificando vieses e padrões claros.

> Divisão dos dataset em dois grupos: treino e teste. Utilizar visão computacional - Keras, TensorFlow e Transfer Learning - para identificar e extrair features referentes aos substratos anatômicos cerebrais.

> Classificação e predição dos diferentes tipos genéticos a partir dos substratos anatômicos.

## 6. Ferramentas

* Jupyter Notebooks/Colab
* Python
* Scikit-Learn
* Keras API
* TensorFlow

## 7. Cronograma
> A primeira etapa seria a etapa de análise das imagens. Dado que ainda não tivemos contato com as imagens é difícil estimar quanto tempo levará. Mas achamos que levaremos em torno de 8 semanas para realizar isso.
> A correlação com os dados clínicos pode levar em torno de 4 semanas caso haja necessidade de tabularmos.
> A escrita do projeto final e ocorrerá concomitantemente.

## 8. Estrutura de Diretórios

```shell
ds4h
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
