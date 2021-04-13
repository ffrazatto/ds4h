# Projeto `<Correlação de Imagens e Fatores Clinicos em Paciente com Esclerose Lateral Amiotrófica (ELA)>`
# Project `<MR Imaging and Clinical Factors Correlation on Amyotrophic Lateral Sclerosis (ALS) Patients>`

## ToDo List

- [ ] Cookiecutter DS (Ler instruções)
- [x] Github
- [x] Tabela Nome/RA
- [ ] Organizar Notebooks
- [ ] Organizar Artigos
- [ ] Vídeo de apresentação

---------

- [x] Apresentação
- [x] Descrição
- [ ] Perguntas de Pesquisa
- [ ] Base de Dados
- [ ] Metodologia
- [ ] Ferramenta
- [ ] Cronograma


# Apresentação

O presente projeto foi originado no contexto das atividades da disciplina de pós-graduação [*Ciência e Visualização de Dados em Saúde*](https://github.com/datasci4health/home), oferecida no primeiro semestre de 2021, na Unicamp.

> Incluir nome RA e foco de especialização de cada membro do grupo. Os grupos devem ter no máximo 5 integrantes e devem contar com pelo menos um aluno da área da saúde e um aluno de área afim à Computação (Ex.: Computação, Elétrica...)
> |Nome  | RA | Especialização|
> |--|--|--|
> | Felipe Frazatto  | 146001  | Engenharia Elétrica |
> | João Pedro N. Gonçalves | 227991  | Farmácia |
> | Pedro Lelis  | 233896 | Ciência da Computação |
> | Renata Prôa  | 224637  | Matemática |


# Descrição Resumida do Projeto
> A Esclerose Lateral Amiotrófica (ELA) é uma doença neurodegenerativa que afeta o sistema motor dos pacientes. Alterações progressivas e cumulativas na musculatura de todo corpo leva na maioria dos casos a uma eventual morte por complicações respiratórias de 3 a 5 anos após começarem tais sintomas. Apesar de diversas técnicas serem empregadas na identificação da ELA, o tempo médio que um paciente leva para receber o diagnóstico correto é de 12 a 18 meses. Um campo que ainda tem espaço para crescer e ainda está se consolidando nesse contexto da ELA, é o da aquisição e o processamento de imagens afim de se emitir um diagnóstico preciso ou obter biomarcadores da progressão e/ou aparecimento dos sintomas. Atualmente, técnincas baseadas na Ressonância Magnética (RM) são utilizadas apenas para excluir outras patologias. Além disso, há poucos estudos que fazem uso do "data mining" para obtenção de características relevantes nas imagens, ou que comparam dados de mais de uma técnica como por exemplo RM, DTI e MRS.
Sendo assim, nosso grupo prõpoe analisar e minerear dados de imagens, principalmente RM de pacientes com ELA, atendidos regularmente no HC Unicamp. Concluída essa etapa, tentaremos correlacionar os dados clínicos disponíveis, se atentando à algumas características como hipótese clínica de ELA, diagnóstico defeinitivo e aparecimento e progressão dos sintomas. Tais dados serão usados como "timelines" que se possível, pretendemos correlacionar com as imagens para gerar novos biomarcadores para cada período relatado.
> 
> Link para vídeo de apresentação da proposta do projeto (máximo 3 minutos).

# Perguntas de Pesquisa
> Existe correlação entre a evolução de sintomas de um paciente diagnosticado com ELA e estruturas cerebrais?
>
> Existem biomarcadores que possam ser identificados com diferentes técnicas de imageamento (MRI, DTI)?
>
> A partir de micro e macro estruturas cerebrais, é possível analisar e predizer a sobrevida de um paciente, fornecendo um prognóstico?

# Bases de Dados
> Imagens de MRI e DTI
> * Fonte: Ambulatório de Neurologia do HC da Unicamp
> * Conteúdo: Mais de 400 imagens de DTI e MRI de pacientes diagnosticados com ELA e um numero correspondente de imagens de controle
> 
> Dados Clinicos
> * Fonte: HC da Unicamp
> * Conteúdo: ?

# Metodologia
Realizar análise exploratória dos dados para compreender as diversas variáveis e estruturas dos dados, possivelmente identificando vieses e padrões claros.

Divisão dos dataset em dois grupos: treino (80%) e teste (20%). Utilizar visão computacional - Keras, TensorFlow e Transfer Learning - para identificar e extrair features referentes a micro e macro estruturas cerebrais.

Correlacionar o conjunto de imagens e suas features com seus respectivos dados clínicos, visando a identificação de padrões.

# Ferramentas
• Jupyter Notebooks/Colab
• Python
• Scikit-Learn
• Keras API
• TensorFlow

# Cronograma
> Proposta de cronograma. Procure estimar quantas semanas serão gastas para cada etapa do projeto.
