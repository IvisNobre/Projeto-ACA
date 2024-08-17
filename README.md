# Projeto de  Análise Computacional da Aprendizagem

# Base de dados

A base de dados que apresenta registros acadêmicos dos estudantes da UFRN, ano 2021 do 1° semestre, contendo informações sobre suas notas, faltas e status final em um curso específico.
A base utilizada se encontra disponível no link: https://dados.ufrn.br/dataset/matriculas-componentes/resource/ffd73a99-325b-4835-9338-036be30fdec8

### Estrutura da Base de Dados:
id_turma: Identificador da turma na qual o estudante está matriculado.
discente: Identificador único do estudante (provavelmente anonimizado).
id_curso: Identificador do curso que o estudante está cursando.
unidade: Unidade do curso ou avaliação (pode ser 1, 2, 3, etc., sugerindo diferentes avaliações ou períodos).
notas: Nota obtida pelo estudante em uma unidade específica.
reposicao: Indica se o estudante realizou uma prova de reposição (valores booleanos: true ou false).
faltas_unidade: Número de faltas em uma unidade específica.
medias_finais: Média final do estudante no curso, considerando todas as unidades.
numero_total_faltas: Total de faltas acumuladas pelo estudante ao longo do curso.
descricao: Status final do estudante no curso (ex.: "APROVADO", "REPROVADO", "TRANCADO", "INDEFERIDO").

# Reclassificação

### Principais Condições para Previsão:
Faltas: Um dos primeiros critérios utilizados na árvore é o número total de faltas. Alunos com um número elevado de faltas tendem a ser classificados como "REPROVADO" ou "TRANCADO", dependendo de outros fatores.
Média Final: Alunos com médias mais altas têm maior probabilidade de serem classificados como "APROVADO". Por exemplo, médias >= 7 tendem a ser associadas à aprovação.

### Resultados da Previsão:
Aprovado: Geralmente, alunos com poucas ou nenhuma falta e uma média final alta (acima de 7, por exemplo) são classificados como "APROVADO".
Reprovado: Alunos com muitas faltas ou médias finais baixas (abaixo de 5) tendem a ser classificados como "REPROVADO".
Aprovado por nota: Geralmente, alunos com médias finais entre 5 e 7 e com poucas faltas.
Reprovado por falta: Alunos que independente das notas e média final tiveram muitas faltas.
Trancado: A classificação como "TRANCADO" ocorre em casos onde a árvore detecta que o aluno não completou as avaliações ou que há registros indicando um trancamento formal do curso.

### Resumo
A árvore de decisão utiliza variáveis como faltas, médias finais, e unidades para segmentar os alunos em categorias específicas. Condições como um número elevado de faltas e médias baixas geralmente resultam em reprovação, enquanto médias altas e faltas mínimas levam à aprovação. Casos de trancamento ou indeferimento são identificados com base em registros específicos no conjunto de dados.

### Árvore

![a](https://github.com/user-attachments/assets/97315998-f45a-4d75-b423-3e100fc342a4)


# Regressão

Correlação entre numero_total_de_faltas e medias_finais:
Coeficiente de correlação de Pearson: -0.49 (negativa)

Eixo x = media final do aluno com intervalo de 0.0 a 10.0
Eixo y = numero total de faltas do aluno.

![gráfico de dispersao](https://github.com/user-attachments/assets/cc121881-069c-42d2-8282-8bf83ff47792)


target: medias_finais.

O modelo de regressão sugere que um aumento no numero total de faltas do aluno está associado a uma diminuição da média final do mesmo.

# Associação
# Agrupamento
