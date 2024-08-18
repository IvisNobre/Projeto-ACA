# Projeto de  Análise Computacional da Aprendizagem

# Base de dados

A base de dados que apresenta registros acadêmicos dos estudantes da UFRN, ano 2021 do 1° semestre, contendo informações sobre suas notas, faltas e status final em um curso específico. 

A base utilizada se encontra disponível no link: https://dados.ufrn.br/dataset/matriculas-componentes/resource/ffd73a99-325b-4835-9338-036be30fdec8

### Estrutura da Base de Dados:

- id_turma: Identificador da turma na qual o estudante está matriculado.

- discente: Identificador único do estudante (provavelmente anonimizado).

- id_curso: Identificador do curso que o estudante está cursando.

- unidade: Unidade do curso ou avaliação (pode ser 1, 2, 3, etc., sugerindo diferentes avaliações ou períodos).

- notas: Nota obtida pelo estudante em uma unidade específica.

- reposicao: Indica se o estudante realizou uma prova de reposição (valores booleanos: true ou false).

- faltas_unidade: Número de faltas em uma unidade específica.

- medias_finais: Média final do estudante no curso, considerando todas as unidades.

- numero_total_faltas: Total de faltas acumuladas pelo estudante ao longo do curso.

- descricao: Status final do estudante no curso (ex.: "APROVADO", "REPROVADO", "TRANCADO", "INDEFERIDO").

# Reclassificação

### Principais Condições para Previsão:
- Faltas: Um dos primeiros critérios utilizados na árvore é o número total de faltas. Alunos com um número elevado de faltas tendem a ser classificados como "REPROVADO" ou "TRANCADO", dependendo de outros fatores.
- Média Final: Alunos com médias mais altas têm maior probabilidade de serem classificados como "APROVADO". Por exemplo, médias >= 7 tendem a ser associadas à aprovação.


### Resultados da Previsão:
- Aprovado: Geralmente, alunos com poucas ou nenhuma falta e uma média final alta (acima de 7, por exemplo) são classificados como "APROVADO".
- Reprovado: Alunos com muitas faltas ou médias finais baixas (abaixo de 5) tendem a ser classificados como "REPROVADO".
- Aprovado por nota: Geralmente, alunos com médias finais entre 5 e 7 e com poucas faltas.
- Reprovado por falta: Alunos que independente das notas e média final tiveram muitas faltas.


### Resumo

A árvore de decisão utiliza variáveis como faltas, médias finais, e unidades para segmentar os alunos em categorias específicas. Condições como um número elevado de faltas e médias baixas geralmente resultam em reprovação, enquanto médias altas e faltas mínimas levam à aprovação. Casos de trancamento ou indeferimento são identificados com base em registros específicos no conjunto de dados.

### Árvore

![Arvore](https://github.com/user-attachments/assets/d9350a31-1a38-40e3-9d0c-83f679dbd4d0)


### Avaliação modelo árvore

![image](https://github.com/user-attachments/assets/c4815cf8-661c-47f7-97e1-d23c62c2500c)

Acurácia: A acurácia é muito alta, indicando boas previsões.

Precisão: A precisão é boa, mas inferior à acurácia. Ou seja, embora a maioria das previsões positivas estejam corretas, pode haver alguns casos em que o modelo faça previsões positivas incorretas.

Revocação: A revocação é boa, indicando que o modelo identifica quase todos os casos positivos verdadeiros.

O modelo é bem equilibrado, com alta acurácia, precisão e revocação.

### Matriz de Confusão do modelo árvore

![image](https://github.com/user-attachments/assets/b483b88a-4d92-4d80-b9e6-4aea3045c5c0)



# Regressão

Correlação entre numero_total_de_faltas e medias_finais:
Coeficiente de correlação de Pearson: -0.49 (negativa)

Eixo x = media final do aluno com intervalo de 0.0 a 10.0
Eixo y = numero total de faltas do aluno.

![gráfico de dispersao](https://github.com/user-attachments/assets/cc121881-069c-42d2-8282-8bf83ff47792)


target: medias_finais.

O modelo de regressão sugere que um aumento no numero total de faltas do aluno está associado a uma diminuição da média final do mesmo.

# Associação

### Regras de Associação:

- _Regra 1:_ Se media final >= 7, então a reposição será falsa. Com suporte de 0.664 e confiança de 0.995
- _Regra 2:_ Se reposição = false, então a media final >= 7. Com suporte de 0.664 e  confiança de 0.736
- _Regra 3:_ Se número total de faltas <= 9, então a reposição = false. Com suporte de 0.797 e confiança de 0.950
- _Regra 4:_ Se reposição = false, então numero total de faltas <= 9. Com suporte de 0.797 e confiança de 0.884
- _Regra 5:_ Se numero total de faltas <= 9, então a media final será >= 7. Com suporte de 0.634 e confiança de 0.756
- _Regra 6:_ Se media final >= 7, então numero total de faltas <= 9. Com suporte de 0.634 e confiança de 0.951
- _Regra 7:_ Se numero total de faltas <= 9 e media final >= 7, então a reposição = false. Com suporte de 0.632 e confiança de 0.792
- _Regra 8:_ Se reposição = false e numero total de faltas < = 9, então a media final >= 7. Com suporte de 0.632 e confiança de 0.792.
- _Regra 9:_ Se numero total de faltas <= 9, então reposição = false e media final >=7 . Com suporte de 0.632 e confiança de 0.753
- _Regra 10:_ Se reposição = false, então numero total de faltas <= 9 e media final >=7. Com suporte de 0.632 e confiança de 0.700
- _Regra 11:_ Se reposição = false e media final >= 7, então numero total de faltas < = 9. Com suporte de 0.632 e confiança de 0.951
- _Regra 12:_ Se media final >= 7, então reposição = false e numero total de faltas < = 9. Com suporte de 0.632 e confiança de 0.947
  

![image](https://github.com/user-attachments/assets/a0723b18-77e8-496b-a00c-068f4238eec3)


### Resumo da Análise de Regras de Associação:

**Média Final e Reposição:** A Regra 1 e a Regra 2 indicam uma forte relação entre a média final e a necessidade de reposição. Se a média final for maior ou igual a 7, é quase certo (confiança de 99,5%) que o aluno não precisará de reposição.
O contrário também é válido, se a reposição é falsa, a média final tende a ser maior ou igual a 7 com confiança de 73,6%.

**Faltas e Reposição:** As Regras 3 e 4 mostram que os alunos com menos de 9 faltas têm uma alta probabilidade de não precisarem de reposição, com confiança de 95% e 88,4% respectivamente.

**Faltas e Média Final:** A Regra 5 e a Regra 6 associam o número de faltas com a média final. Se o aluno tem menos de 9 faltas, há uma boa chance (confiança de 75,6%) de que sua média final seja maior ou igual a 7. Se a média final for maior ou igual a 7, também é muito provável (confiança de 95,1%) que o aluno tenha menos de 9 faltas.

**Faltas, Média Final e Reposição:** As Regras 7 até a 12 combinam múltiplas condições, reforçando as associações anteriores. Por exemplo, se o aluno tem menos de 9 faltas e média final maior ou igual a 7, ele quase certamente não precisará de reposição. Essas regras apresentam suportes consistentes ao redor de 0.632 e confiança >= 0.700.

**Resumo:** Essas regras indicam que a frequência e o desempenho acadêmico estão fortemente correlacionados com a necessidade de reposição. Alunos que mantêm uma média final alta e têm poucas faltas quase certamente não precisam de reposição, sugerindo que o controle de faltas e o bom desempenho são cruciais para evitar a reposição.


# Agrupamento
