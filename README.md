# Projeto de  Análise Computacional da Aprendizagem

# Bases de dados

## Base de dados: Matriculas 2021.1

A primeira base de dados que apresenta registros acadêmicos dos estudantes da UFRN, ano 2021 do 1° semestre, contendo informações sobre suas notas, faltas e status final em um curso específico. 

A base utilizada se encontra disponível no link: https://dados.ufrn.br/dataset/matriculas-componentes/resource/ffd73a99-325b-4835-9338-036be30fdec8

### Estrutura da Base de Dados Matriculas:

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

## Base de Dados: Avaliação Docência

Essa base de dados contém informações sobre a avaliações dos professores da UFRN, ao longo de várias turmas e períodos. As variáveis principais incluem:

A base utilizada se encontra disponível no link: https://dados.ufrn.br/dataset/d5723d75-7e6e-4264-82aa-b96909b69f63/resource/7accd1d2-2793-460e-b98d-87a0679b9155/download/avaliacaodocencia.csv

### Estrutura da Base de Dados Avaliação Docência:

- id_docente e nome_docente: Identificam o professor.
- 
- id_turma: Identifica a turma em que as avaliações foram feitas.
- 
- ano e periodo: Correspondem ao ano e semestre em que as aulas ocorreram.
- 
- qtd_discentes: Quantidade de alunos na turma.
- 
- postura_profissional_media e postura_profissional_DP: Avaliação média da postura profissional do professor e seu desvio-padrão.
- 
- atuacao_profissional_media e atuacao_profissional_DP: Avaliação média da atuação profissional do professor e seu desvio-padrão.
- 
- autoavaliacao_aluno_media e autoavaliacao_aluno_DP: Média da autoavaliação dos alunos e seu desvio-padrão.

# Classificação

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

![image](https://github.com/user-attachments/assets/b36c4915-1370-4da4-8fda-8272aef65030)


### Análise:
Usando K-means, ao aumentar o número de clusters de 2 para 8, o valor do silhouette score diminui, com o melhor valor (0.848) sendo obtido com 2 clusters.

- Com dois Clusters: O valor de 0.848 sugere uma boa separação entre os grupos. Isso significa que os dados foram bem divididos em dois grupos distintos, com as observações dentro de cada cluster sendo mais semelhantes entre si do que com as de outros clusters.

- Mais Clusters: À medida que o número de clusters aumenta, o silhouette score diminui, o que indica que a qualidade da separação entre os clusters está piorando.

Conclusão:
Com base nessa análise, dividir os dados em dois clusters oferece a melhor separação e, portanto, pode ser a solução mais interpretável, sendo esses os alunos aprovados e reprovados.


Segue abaixo os clusters, tendo como eixo_x: numero total de faltas. E no eixo_y: Media Final

- Com 2 clusters

![1](https://github.com/user-attachments/assets/b4608817-1538-47b0-b6d0-49975581f027)


- Com 3 clusters

![2](https://github.com/user-attachments/assets/aa31d2d1-fbd5-435c-a67d-2df7598baed5)


- Com 4 clusters

![3](https://github.com/user-attachments/assets/c3b6e045-ccc8-41b4-a9e9-8989a1fbf624)


- Com 5 clusters

![4](https://github.com/user-attachments/assets/e505bc1e-2533-4c9b-bca2-0b50a896d790)


- Com 6 clusters

![5](https://github.com/user-attachments/assets/3c4def4b-a16e-4329-a4da-02315d9217fb)


- Com 7 clusters

![6](https://github.com/user-attachments/assets/3aec448d-a694-4b39-a9fc-2446579949f2)


- Com 8 clusters

![7](https://github.com/user-attachments/assets/41996963-0613-4b2f-90ec-b97ebd86ced8)


