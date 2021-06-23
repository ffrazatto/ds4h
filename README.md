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
| Pedro Lelis | 233896 | Ciência da Computação |
| Renata Prôa | 224637 | Matemática |


## 2. Descrição do Projeto

A Esclerose Lateral Amiotrófica (ELA) é uma doença neurodegenerativa que afeta o sistema motor dos pacientes. Alterações progressivas e cumulativas na musculatura de todo corpo leva na maioria dos casos a uma eventual morte por complicações respiratórias de 3 a 5 anos após começarem tais sintomas. Do ponto de vista genético 90% dos casos de ELA são esporádicos (ELAs) e apenas 10% dos casos são familiares (ELAf), porém aproximadamente 70% dos casos de ELAf já possuem um gene candidato, contra apenas 10% dos casos de ELAs. Os genes mais frequentes encontrados tanto em casos de ELAf quanto em casos de ELAs são C9orf72, FUS, TARDBP e SOD1.

Apesar de diversas técnicas serem empregadas na identificação da ELA, o tempo médio que um paciente leva para receber o diagnóstico correto é de 12 a 18 meses. Na prática os pacientes com ELA são submetidos a Ressonância Magnética (RM) apenas com a finalidade de se excluir outras patologias, mas talvez seja possível extrair informações dessas imagens que possam não somente classificar os casos de ELA, como também identificar os substratos anatômicos cerebrais que subdividem os pacientes, tendo em vista essa variabilidade genética.

Sendo assim, nosso grupo prõpoe analisar divergências anatômicas do cortéx cerebral (matéria cinzenta) aplicando a técnica de morfometria baseada em "voxel" (pixel 3D) selecionando os dados sobre o volume e a espessura cortical e analisar dados de estruturas axonais (matéria branca) a partir da técnica de imagem de tensor de difusão "DTI" em controles e pacientes diagnosticados com ELAs e ELAf atendidos regularmente no HC Unicamp. Do grupo dos ELAf foram selecionados aqueles que possuíam maior representatividade (Casos de C9orf72 e VAPB) e também foram utilizadas informações sobre a idade, sexo dos pacientes e controles.

> Um breve vídeo de apresentação do projeto está disponível no Google Drive pelo link a seguir: [Vídeo de Apresentação](https://drive.google.com/file/d/14wwlC784iaPo-pFCyMjoqUAnqoewHfpT/view?usp=sharing)

## 3. Perguntas de Pesquisa

* A partir de informações sobre o volume, expessura média, medidas de difusão e a anisotropia fracionada dos diversos substratos anatômicos cerebrais, é possível diferenciar os subtipos de ELA?

## 4. Bases de Dados

### Imagens de RM
* Fonte: Ambulatório de Neurologia do HC da Unicamp
* Conteúdo: 91 RM de pacientes diagnosticados com ELA e controles pareados por sexo e idade.
* Para a extração de features de volume e expressura foram utilizadas todas as 91 amostras, porém apenas 88 delas foram utilizadas para extração de informações difisuvidade média (MD) e anisotropia fracionada (FA).


Em um primeiro momento, as imágens de ressonância foram segmentadas, ou seja, cada estrutura cerebral é identificada, e em seguida para cada região são calculadas diversas metricas, dentre elas o volume, rugosidade, profundidade de sulcos etc.

> A base de dados utilizada é uma tabela composta por três tabelas (.xlsx) conténdo diversas quantidades de volume (mm^3) e espessura (mm) das diversas estruturas cerebrais separadas por hemisférios.

- Volume: volumes de diversas regiões e estruturas
- Gyri+SulciLH: espessura cortical de estruturas no hemisfério esquerdo
- Gyri+SulciRH: espessura cortical de estruturas no hemisfério direito

### Dados Genéticos
* Fonte: Dados genéticos obtidos através do pipeline de análise empregado no diagnóstico genético e molecular dos pacientes do Ambulatório de Neurologia do HC da Unicamp.
* Conteúdo: Informações sobre os subtipos genéticos de ELA.

### Integração entre Bases e Análise Exploratória

Cada tabela foi importada e suas dimensões verificadas. Cada tabela possui 2 colunas (Unnamed 1 e 2) que são compostas apenas por dados faltantes de nomes e datas, que não serão necessários para esse projeto, sendo então completamente excluídas. A tabela 1 mostra a quantidade de linhas, colunas e quantidade de dados faltantes para cada conjunto de dados.

Table 1: Sumário da dimensionalidade dos dados.
| Data | Rows | Columns | Missing |
|---|---|---|---|
| Volume | 91 | 26 | 0 |
| Gyri+Sulci LH | 91 | 75 | 0 |
| Gyri+Sulci RH | 91 | 75 | 0 |

Nota-se um grande problema de dimensionalidade, ou seja, poucas linhas e muitas colunas.

Em seguida, a primeira coluna (Unnamed 0), é renomeada para "subject" e apartir do código utilizado para nomear cada paciente (ctl, sals, c9o e vap) são criadas outras duas colunas:

- "als": se o individuo possui (1) ou não (0) ELA.
- "group": qual tipo de ELA o individuo possui. Controle = 0, ELAs = 1, C9orf72 = 2 e VAPB = 3.

Sendo agora possível discriminar individuios do grupo de controle e diagnosticados, foram traçados os histogramas das figuras 1 a 3 das diversas variáveis com o induito de indentificar uma possível discrepância entre as duas populações. 


[Figura 1: Histograma de cada variável do dataset Volume.](assets/histVolume.png)

[Figura 2: Histograma de cada variável do dataset Gyri+SulciLH.](assets/histGSLH.png)

[Figura 3: Histograma de cada variável do dataset Gyri+SulciRH.](assets/histGSRH.png)


Nas três figuras, os dados estão agrupados em com (1) e sem ELA (0).
    
Através dessas três figuras, é possível notar que para algumas variáveis, existem diferenças entre as distribuições de pacientes com ELA, de qualquer tipo, e do grupo de controle. Para evidenciar quantizar essas diferenças, foi realizado um Teste T de Student para cada variável, cujas hipóteses são:
       
* H0: Não há diferença significativa entre as médias das populações de pacientes com ELA e controle
* H1: Há diferença significativa entre as médias das populações de pacientes com ELA e controle
    
Foi utilizado alpha = 0.05, significando que para todos os testes cujo pvalor for menor que alpha, rejeita-se a hipótese nula (H0) em favor da alternativa (H1). Portanto, a seguir são apresentadas as tabelas 2 a 4 contendo as feature que possuiem pvalores menor que alpha para cada dataset.

Tabela 2: Resultados do dataset Volume. Todas as Features que rejeitaram a hipótese nula.
|feature | pvalue | tstat |
|---|---|---|
|Brain-Stem | 2.263276e-03 | 3.144256|
|Left-Amygdala | 7.768082e-03 | 2.723759|
|Left-Caudate | 4.504153e-02 | 2.032907|
|Left-Hippocampus | 3.017448e-03 | 3.049686|
|Left-Putamen | 1.281947e-02 | 2.540013|
|Left-Thalamus-Proper | 8.218072e-03 | 2.703528|
|Left-VentralDC | 1.147013e-03 | 3.360653|
|Right-Amygdala | 4.401790e-03 | 2.922471|
|Right-Hippocampus | 2.868997e-03 | 3.066415|
|Right-Putamen | 1.583725e-02 | 2.459725|
|Right-Thalamus-Proper | 3.177435e-03 | 3.032492|
|Right-VentralDC | 2.715175e-03 | 3.084619|

Tabela 3: Resultados do dataset Gyri+SulciLH. Todas as Features que rejeitaram a hipótese nula.
|feature | pvalue | tstat |
|---|---|---|
| G&S_cingul-Ant | 0.000745 | 3.493471 |
| G&S_cingul-Mid-Post | 0.002188 | 3.155263 |
| G_cingul-Post-dorsal | 0.020414 | 2.360901 |
| G_cingul-Post-ventral | 0.005556 | 2.842116 |
| G_front_middle | 0.031206 | 2.189111 |
| G_insular_short | 0.016624 | 2.441054 |
| G_oc-temp_med-Lingual | 0.018476 | 2.400056 |
| G_subcallosal | 0.027091 | 2.247324 |
| G_temp_sup-Plan_tempo | 0.009874 | 2.636848 |
| G_temporal_inf | 0.008626 | 2.686032 |
| G_temporal_middle | 0.044824 | 2.035017 |
| Lat_Fis-post | 0.010700 | 2.607305 |
| S_circular_insula_sup | 0.013737 | 2.513950 |
| S_front_sup | 0.020480 | 2.359628 |
| S_oc-temp_med&Lingual | 0.018902 | 2.391153 |
| S_orbital-H_Shaped | 0.000951 | 3.418706 |
| S_precentral-inf-part | 0.032513 | 2.172025 |
| S_precentral-sup-part | 0.019934 | 2.370273 |
| S_temporal_sup | 0.008444 | 2.693741 |


Tabela 4: Resultados do dataset Gyri+SulciRH. Todas as Features que rejeitaram a hipótese nula.
|feature | pvalue | tstat |
|---|---|---|
| G&S_cingul-Mid-Ant | 0.004737 | 2.897282 |
| G&S_cingul-Mid-Post | 0.001211 | 3.343762 |
| G_cingul-Post-dorsal | 0.020027 | 2.368439 |
| G_front_inf-Opercular | 0.022769 | 2.317535 |
| G_front_middle | 0.016157 | 2.452031 |
| G_oc-temp_med-Lingual | 0.010179 | 2.625706 |
| G_oc-temp_med-Parahip | 0.006706 | 2.776123 |
| G_pariet_inf-Supramar | 0.036646 | 2.121660 |
| G_precentral | 0.020529 | 2.358689 |
| G_rectus | 0.013671 | 2.515779 |
| G_temporal_inf | 0.004761 | 2.895550 |
| G_temporal_middle | 0.003627 | 2.988167 |
| S_circular_insula_inf | 0.009561 | 2.648650 |
| S_circular_insula_sup | 0.003703 | 2.981165 |
| S_front_middle | 0.040235 | 2.081766 |
| S_oc-temp_lat | 0.015342 | 2.471904 |
| S_oc-temp_med&Lingual | 0.020603 | 2.357264 |
| S_precentral-inf-part | 0.007715 | 2.726205 |
| S_precentral-sup-part | 0.000480 | 3.625313 |
| S_temporal_inf | 0.000088 | 4.110700 |
| S_temporal_sup | 0.012058 | 2.562936 |
| S_temporal_transverse | 0.024444 | 2.289029 |

Portanto, é possível notar que existem diferenças significativas entre as populações com e sem ELA. 

Em seguida, a mesma análise é realizada comparando os diferentes tipos de ELA. As tabelas 5 a 13 evidenciam os resultados.

Tabela 5: Resultados do dataset Volume comparando ELAs e C9orf72. Todas as Features que rejeitaram a hipótese nula.
| feature | pvalue | tstat |
| --- | --- | --- |
| G&S_transv_frontopol | 0.000263 | 3.984912 |
| G_cingul-Post-dorsal | 0.000392 | 3.853952 |
| G_front_inf-Orbital | 0.000967 | 3.549258 |
| G_front_sup | 0.000164 | 4.139043 |
| G_oc-temp_lat-fusifor | 0.000827 | 3.602657 |
| G_occipital_sup | 0.001817 | 3.329818 |
| G_parietal_sup | 0.000000 | -inf |

Tabela 6: Resultados do dataset Gyri+SulciLH comparando ELAs e C9orf72. Todas as Features que rejeitaram a hipótese nula.
| feature | pvalue | tstat |
| --- | --- | --- |
| G&S_cingul-Mid-Ant | 0.000000 | -inf |
| G&S_cingul-Mid-Post | 0.000000 | -inf |
| G_front_inf-Opercular | 0.000000 | -inf |
| G_front_middle | 0.000000 | -inf |
| G_oc-temp_med-Lingual | 0.000000 | -inf |
| G_occipital_sup | 0.000000 | -inf |
| G_pariet_inf-Angular | 0.000000 | -inf |
| G_parietal_sup | 0.000000 | -inf |
| G_precuneus | 0.000000 | -inf |
| G_temporal_middle | 0.000000 | -inf |
| S_circular_insula_ant | 0.000000 | -inf |
| S_circular_insula_sup | 0.000000 | -inf |
| S_collat_transv_ant | 0.000000 | -inf |
| S_front_inf | 0.000000 | -inf |
| S_intrapariet&P_trans | 0.000000 | -inf |
| S_oc-temp_lat | 0.000000 | -inf |
| S_oc_sup&transversal | 0.000000 | -inf |
| S_orbital-H_Shaped | 0.000000 | -inf |
| S_postcentral | 0.000000 | -inf |
| S_precentral-inf-part | 0.000000 | -inf |
| S_subparietal | 0.000000 | -inf |
| S_temporal_sup | 0.000000 | -inf |

Tabela 7: Resultados do dataset Gyri+SulciRH comparando ELAs e C9orf72. Todas as Features que rejeitaram a hipótese nula.
| feature | pvalue | tstat |
| --- | --- | --- |
| G&S_cingul-Mid-Post | 0.000000 | -inf |
| G&S_subcentral | 0.000000 | -inf |
| G_front_inf-Opercular | 0.000000 | -inf |
| G_pariet_inf-Angular | 0.000000 | -inf |
| G_parietal_sup | 0.000000 | -inf |
| G_precuneus | 0.000000 | -inf |
| G_temporal_inf | 0.000000 | -inf |
| G_temporal_middle | 0.000000 | -inf |
| Lat_Fis-ant-Vertical | 0.000000 | -inf |
| Lat_Fis-post | 0.000000 | -inf |
| S_cingul-Marginalis | 0.000000 | -inf |
| S_circular_insula_sup | 0.000000 | -inf |
| S_interm_prim-Jensen | 0.000000 | -inf |
| S_oc-temp_lat | 0.000000 | -inf |
| S_orbital-H_Shaped | 0.000000 | -inf |
| S_precentral-inf-part | 0.000000 | -inf |
| S_subparietal | 0.000000 | -inf |
| S_temporal_sup | 0.000000 | -inf |

Tabela 8: Resultados do dataset Volume comparando ELAs e VAPB. Todas as Features que rejeitaram a hipótese nula.
| feature | pvalue | tstat |
| --- | --- | --- |
| G_front_inf-Orbital | 0.039936 | -2.105254 |
| G_front_middle | 0.034395 | 2.170370 |
| G_parietal_sup | 0.000000 | -inf |

Tabela 9: Resultados do dataset Gyri+SulciLH comparando ELAs e VAPB. Todas as Features que rejeitaram a hipótese nula.
| feature | pvalue | tstat |
| --- | --- | --- |
| S_central | 0.000000 | -inf |
| S_oc-temp_med&Lingual | 0.000000 | -inf |
| S_oc_middle&Lunatus | 0.000000 | -inf |
| S_oc_sup&transversal | 0.000000 | -inf |

Tabela 10: Resultados do dataset Gyri+SulciRH comparando ELAs e VAPB. Todas as Features que rejeitaram a hipótese nula.
| feature | pvalue | tstat |
| --- | --- | --- |
| G_postcentral | 0.000000 | -inf |
| G_precentral | 0.000000 | -inf |
| G_temp_sup-Plan_polar | 0.000000 | -inf |
| S_circular_insula_inf | 0.000000 | -inf |

Tabela 11: Resultados do dataset Volume comparando C9orf72 e VAPB. Todas as Features que rejeitaram a hipótese nula.
| feature | pvalue | tstat |
| --- | --- | --- |
| G&S_paracentral | 0.044352 | -2.079679 |
| G&S_transv_frontopol | 0.000064 | -4.489778 |
| G_Ins_lg&S_cent_ins | 0.044236 | -2.080886 |
| G_cingul-Post-dorsal | 0.017932 | -2.474235 |
| G_cingul-Post-ventral | 0.009285 | -2.740935 |
| G_front_inf-Opercular | 0.016558 | -2.507323 |
| G_front_inf-Orbital | 0.000003 | -5.452097 |
| G_front_sup | 0.000308 | -3.970241 |
| G_oc-temp_lat-fusifor | 0.032265 | -2.222657 |
| G_oc-temp_med-Lingual | 0.002302 | -3.268099 |
| G_occipital_middle | 0.039590 | -2.131325 |
| G_occipital_sup | 0.000008 | -5.163438 |
| G_parietal_sup | 0.000000 | -inf |

Tabela 12: Resultados do dataset Gyri+SulciLH comparando C9orf72 e VAPB. Todas as Features que rejeitaram a hipótese nula.
| feature | pvalue | tstat |
| --- | --- | --- |
| G&S_cingul-Mid-Ant | 0.000000 | -inf |
| G&S_cingul-Mid-Post | 0.000000 | -inf |
| G&S_occipital_inf | 0.000000 | -inf |
| G&S_paracentral | 0.000000 | -inf |
| G&S_subcentral | 0.000000 | -inf |
| G_cingul-Post-dorsal | 0.000000 | -inf |
| G_cuneus | 0.000000 | -inf |
| G_front_inf-Opercular | 0.000000 | -inf |
| G_front_inf-Orbital | 0.000000 | -inf |
| G_front_inf-Triangul | 0.000000 | -inf |
| G_front_middle | 0.000000 | -inf |
| G_front_sup | 0.000000 | -inf |
| G_occipital_middle | 0.000000 | -inf |
| G_occipital_sup | 0.000000 | -inf |
| G_pariet_inf-Angular | 0.000000 | -inf |
| G_pariet_inf-Supramar | 0.000000 | -inf |
| G_parietal_sup | 0.000000 | -inf |
| G_postcentral | 0.000000 | -inf |
| G_precentral | 0.000000 | -inf |
| G_precuneus | 0.000000 | -inf |
| G_temp_sup-Lateral | 0.000000 | -inf |
| G_temp_sup-Plan_tempo | 0.000000 | -inf |
| G_temporal_inf | 0.000000 | -inf |
| G_temporal_middle | 0.000000 | -inf |
| Lat_Fis-ant-Vertical | 0.000000 | -inf |
| Lat_Fis-post | 0.000000 | -inf |
| S_calcarine | 0.000000 | -inf |
| S_central | 0.000000 | -inf |
| S_circular_insula_ant | 0.000000 | -inf |
| S_circular_insula_sup | 0.000000 | -inf |
| S_collat_transv_ant | 0.000000 | -inf |
| S_front_inf | 0.000000 | -inf |
| S_front_sup | 0.000000 | -inf |
| S_interm_prim-Jensen | 0.000000 | -inf |
| S_intrapariet&P_trans | 0.000000 | -inf |
| S_oc-temp_lat | 0.000000 | -inf |
| S_oc-temp_med&Lingual | 0.000000 | -inf |
| S_oc_middle&Lunatus | 0.000000 | -inf |
| S_oc_sup&transversal | 0.000000 | -inf |
| S_occipital_ant | 0.000000 | -inf |
| S_orbital_lateral | 0.000000 | -inf |
| S_parieto_occipital | 0.000000 | -inf |
| S_postcentral | 0.000000 | -inf |
| S_precentral-inf-part | 0.000000 | -inf |
| S_precentral-sup-part | 0.000000 | -inf |
| S_subparietal | 0.000000 | -inf |
| S_temporal_inf | 0.000000 | -inf |
| S_temporal_sup | 0.000000 | -inf |

Tabela 13: Resultados do dataset Gyri+SulciRH comparando C9orf72 e VAPB. Todas as Features que rejeitaram a hipótese nula.
| feature | pvalue | tstat |
| --- | --- | --- |
| G&S_cingul-Mid-Ant | 0.000000 | -inf |
| G&S_cingul-Mid-Post | 0.000000 | -inf |
| G&S_paracentral | 0.000000 | -inf |
| G&S_subcentral | 0.000000 | -inf |
| G_cuneus | 0.000000 | -inf |
| G_front_inf-Opercular | 0.000000 | -inf |
| G_front_inf-Orbital | 0.000000 | -inf |
| G_occipital_middle | 0.000000 | -inf |
| G_occipital_sup | 0.000000 | -inf |
| G_orbital | 0.000000 | -inf |
| G_pariet_inf-Angular | 0.000000 | -inf |
| G_pariet_inf-Supramar | 0.000000 | -inf |
| G_parietal_sup | 0.000000 | -inf |
| G_postcentral | 0.000000 | -inf |
| G_precentral | 0.000000 | -inf |
| G_precuneus | 0.000000 | -inf |
| G_temporal_inf | 0.000000 | -inf |
| G_temporal_middle | 0.000000 | -inf |
| Lat_Fis-ant-Vertical | 0.000000 | -inf |
| Lat_Fis-post | 0.000000 | -inf |
| Pole_occipital | 0.000000 | -inf |
| S_calcarine | 0.000000 | -inf |
| S_central | 0.000000 | -inf |
| S_cingul-Marginalis | 0.000000 | -inf |
| S_circular_insula_ant | 0.000000 | -inf |
| S_circular_insula_inf | 0.000000 | -inf |
| S_circular_insula_sup | 0.000000 | -inf |
| S_collat_transv_ant | 0.000000 | -inf |
| S_interm_prim-Jensen | 0.000000 | -inf |
| S_intrapariet&P_trans | 0.000000 | -inf |
| S_oc-temp_lat | 0.000000 | -inf |
| S_oc-temp_med&Lingual | 0.000000 | -inf |
| S_oc_middle&Lunatus | 0.000000 | -inf |
| S_oc_sup&transversal | 0.000000 | -inf |
| S_occipital_ant | 0.000000 | -inf |
| S_orbital-H_Shaped | 0.000000 | -inf |
| S_orbital_med-olfact | 0.000000 | -inf |
| S_parieto_occipital | 0.000000 | -inf |
| S_postcentral | 0.000000 | -inf |
| S_precentral-inf-part | 0.000000 | -inf |
| S_precentral-sup-part | 0.000000 | -inf |
| S_subparietal | 0.000000 | -inf |
| S_temporal_inf | 0.000000 | -inf |
| S_temporal_sup | 0.000000 | -inf |

É importante salientar que o Teste T de Student não pode ser utilizado como seleção de features, já que ele não leva em consideração interações entre as variáveis, sendo necessário utilizar outros métodos como PCA ou LASSO, no entanto, a quantidade de features que possuem diferenças significativas entre os grupos servem de forte indício que é possível discriminar os diversos grupos.

Por fim, os três datasets são unidos em um único para que seja utilizado mais facilmente tanto na seleção de "feature" quanto no treino e teste dos classificadores.
 
    
## 5. Metodologia

As imagens de T1 foram primeiramente convertidas do formato DICOM para o formato NIfTI com o software 'Dicom2Nii', e em seguida processadas com o software Freesurfer. O Freesurfer primeiramente faz o Skull Stripping, isto é, a remoção da caixa craniana, identifica as principais regiões do cérebro (Volumetric Labeling), normalização da intensidade e a segmentação da substância branca. Em seguida a imagem é registrada num espaço padrão e um atlas é aplicado para que possam ser identificados os giros (parcelamento). Como resultado deste processo de segmentação e percelamento automáticos, obtivemos as medidas de volume para todas as 113 regiões identificadas. 
Quanto às imagens de difusão, estas foram processadas com as ferramentas 'DTI Mapping' e 'DTI MultiAtlas Segmentation' do MRI Cloud (https://braingps.mricloud.org/dtimultiatlasseg). Para tal, as imagens DICOM foram primeiro convertidas em imagens 'Raw Image' (.raw) e arquivos 'Data Parameter File' (.dpf) com um conversor do'DTI Mapping'. As imagens de difusão foram então ajustadas para o modelo tensorial de DTI (Diffusion Tensor Imaging) pelo 'DTI Mapping' e salvas em formato High Dynamic Range (.hdr). Em seguida, as imagens de DTI foram registradas num espaço padrão (MNI) e um atlas foi aplicado utilizando o 'DTI MultiAtlas Segmentation' e foi calculada a soma dos autovalores principais em cada uma das regiões identificadas. A partir disto, calculamos as medidas de difusão médias nestas regiões, são elas: Anisotropia Fracional (FA), Difusividade Média (MD), Difusividade Axial (AD) e Difusividade Radial (RD). As métricas de difusão extraídas e as informações de volumetria foram utilizadas como features para treinar os modelos.

Para classificar os sujeitos entre saudáveis e pacientes de ELA, treinamos três diferentes tipos modelo para comparação, são eles: regressão logistica, Support Vector Machine (SVM) e Random Forest. De cada um dos tipos, treinamos três modelos, um utilizando apenas os dados de difusão, outro utilizando somente os dados de volumetria e o terceiro utilizando ambos os dados de difusão e volumetria. Para classifcar os pacientes de ELA entre os três subtipos (ELAs, VAPB e C9orf72), treinamos apenas um tipo de modelo (Random Forest), sendo três modelos utilizando os mesmos três conjuntos de dados (dados de difusão, dados de voumetria e dado de difusão mais volumetria).

Previamente ao treinamento dos modelos, as features tais que para ao menos um sujeito não havia dados foram removidas da análise. A escolha de remover tais features foi feita com base no fato de que dispunhamos de um excesso de features em comparação com o número de sujeitos (alta dimensionalidade). Também foi feita uma análise da variância das features e foram excluídas as features com variância muito próxima de zero (Near Zero Variance). Em seguida, foi feita uma Análise de Componentes Principais (PCA) e os dados foram divididos nos conjuntos de Treino, Validação e Teste (60%, 20% e 20% respectivamete). Por fim, foi feita uma normalização das features (método Standard Scaler da biblioteca Scikit-Learn do Python) e o treinamento dos três modelos. Nos modelos de regressão logistica foi feita regularização através de um LASSO (Least Absolute Shrinkage and Selection Operator). Para todos os modelos foi calculada a matriz de confusão, a acurácia e foi feito um K-Fold Cross Validation com K = 100.


## 6. Ferramentas

* Freesurfer
* Acapuco
* MRICloud
* Jupyter Notebooks/Colab
* Python
* Scikit-Learn

## 7. Cronograma
> A primeira etapa seria a etapa de análise das imagens. Dado que ainda não tivemos contato com as imagens é difícil estimar quanto tempo levará. Mas achamos que levaremos em torno de 8 semanas para realizar isso.
> A correlação com os dados clínicos pode levar em torno de 4 semanas caso haja necessidade de tabularmos.
> A escrita do projeto final e ocorrerá concomitantemente.

## 8. Estrutura de Diretórios

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
