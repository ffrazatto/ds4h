# Projeto `<Correlação de Imagens e Fatores Clinicos em Paciente com Esclerose Lateral Amiotrófica (ELA)>`
# Project `<MR Imaging and Clinical Factors Correlation on Amyotrophic Lateral Sclerosis (ALS) Patients>`

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

A Esclerose Lateral Amiotrófica (ELA) é uma doença neurodegenerativa que afeta o sistema motor dos pacientes. Alterações progressivas e cumulativas na musculatura de todo corpo leva na maioria dos casos a uma eventual morte por complicações respiratórias de 3 a 5 anos após começarem tais sintomas. Apesar de diversas técnicas serem empregadas na identificação da ELA, o tempo médio que um paciente leva para receber o diagnóstico correto é de 12 a 18 meses. Um campo que ainda tem espaço para crescer e ainda está se consolidando nesse contexto da ELA, é o da aquisição e o processamento de imagens afim de se emitir um diagnóstico preciso ou obter biomarcadores da progressão e/ou aparecimento dos sintomas. Atualmente, técnincas baseadas na Ressonância Magnética (RM) são utilizadas apenas para excluir outras patologias. Além disso, há poucos estudos que fazem uso do "data mining" para obtenção de características relevantes nas imagens, ou que comparam dados de mais de uma técnica como por exemplo RM, DTI e MRS.

Sendo assim, nosso grupo prõpoe analisar dados de imagens de RM obtidos de pacientes com ELA atendidos regularmente no HC Unicamp. Concluída essa etapa, tentaremos correlacionar os dados clínicos disponíveis, se atentando à algumas características como aparecimento dos sintomas, progressão dos sintomas e sobrevida dos pacientes. Tais dados serão usados como "timelines" que se possível, pretendemos correlacionar com as imagens para gerar novos biomarcadores para cada período relatado.
> 
Um breve vídeo de apresentação do projeto está disponível no Google Drive pelo link a seguir: [Vídeo de Apresentação](https://drive.google.com/file/d/14wwlC784iaPo-pFCyMjoqUAnqoewHfpT/view?usp=sharing)

## 3. Perguntas de Pesquisa

* Existe correlação entre a evolução de sintomas de um paciente diagnosticado com ELA e estruturas cerebrais?
* Existem biomarcadores que possam ser identificados com diferentes técnicas de imageamento (MRI, DTI)?
* A partir de micro e macro estruturas cerebrais, é possível analisar e predizer a sobrevida de um paciente, fornecendo um prognóstico?

## 4. Bases de Dados

Imagens de RM
* Fonte: Ambulatório de Neurologia do HC da Unicamp
* Conteúdo: Mais de 400 imagens de DTI e MRI de pacientes diagnosticados com ELA e um numero correspondente de imagens de controle
> 
Dados Clinicos
* Fonte: Dados clínicos obtidos através de consultas com pacientes acompanhados regularmente no Ambulatório de Neurologia do HC da Unicamp
* Conteúdo: Nessa projeto utilizaremos dados de início de sintomas e sobrevida dos pacientes.

## 5. Metodologia

> Realizar análise exploratória dos dados para compreender as diversas variáveis e estruturas dos dados, possivelmente identificando vieses e padrões claros.

> Divisão dos dataset em dois grupos: treino e teste. Utilizar visão computacional - Keras, TensorFlow e Transfer Learning - para identificar e extrair features referentes a micro e macro estruturas cerebrais.

> Correlacionar o conjunto de imagens e suas features com seus respectivos dados clínicos, visando a identificação de padrões.

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
