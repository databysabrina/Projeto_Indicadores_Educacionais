## 📄 Regras de Negócio e Definições Métricas

### 1. Definição da População e Faixa Etária
Para garantir que a análise reflita a realidade do ensino médio (1º ano), foram aplicadas as seguintes premissas:
* **Público-alvo:** Estudantes regularmente matriculados.
* **Regra de Idade:** A faixa etária padrão foi definida entre **14 e 17 anos**.
    * *Ação Técnica:* Alunos identificados fora dessa faixa (ex: ID 3 com 25 anos) foram tratados como inconsistências de cadastro e ajustados para a idade média da turma (15 anos) após validação.

### 2. Critérios de Proficiência e Aproveitamento
A métrica de "Status de Aproveitamento" não é apenas um número, mas uma classificação baseada no desempenho acadêmico:
* **Cálculo da Porcentagem de Acerto:** $\frac{\text{Acertos}}{\text{Total de Questões}} \times 100$
* **Classificação de Status de Aproveitamento:** baseado na porcentagem de acertos
    * **Crítico:** Aproveitamento abaixo de 40%.
    * **Insuficiente:** Aproveitamento entre 40% e 59%.
    * **Suficiente:** Aproveitamento entre 60% e 79%.
    * **Excelente:** Aproveitamento igual ou superior a 80%.
* **Nota:** A escolha de cada classificação e porcentagem (de forma pedagógica e analítica)

### 3. Matriz de Coerência (Auditoria de Dados)
Para garantir a confiabilidade dos dados lançados, criamos uma regra de **Cruzamento de Inconsistência** entre a nota objetiva (Acertos) e a classificação de proficiência da avaliação externa (ID_Proficiência):
* **Inconsistência Tipo A:** Estudante com alto acerto ($\geq$ 60%) mas com ID de proficiência baixo (1 ou 2).
* **Inconsistência Tipo B:** Estudante com baixo acerto ($\leq$ 40%) mas com ID de proficiência alto (3 ou 4).
* *Objetivo:* Isolar erros de lançamento manual que poderiam distorcer a média das turmas.
* **Risco de Dados:** Quando a linha é sinalizada como "Analisar Inconsistência".


### 4. Definição de "Alunos em Risco" (Métrica Composta)
A regra mais importante do dashboard. Um aluno é sinalizado como "Em Risco" se atender a **pelo menos um** dos critérios abaixo:
* **Risco Etário:** Estudante com 17 anos ou mais (risco de evasão/distorção idade-série).
* **Risco Acadêmico:** Proficiência classificada nos níveis 1 ou 2 (Abaixo do Básico/Básico).
* **Risco de Aproveitamento:** Status "Crítico" ou "Insuficiente".
* **Sem Risco:**

### 5. Lógica de Ranking de Turmas
Para comparar a performance entre as turmas (1A, 1B, 1C), o ranking foi estabelecido com base na **Média de Acertos**.
* *Mecânica:* Utilização da função `RANK()` no SQL para ordenar as turmas de forma decrescente, onde a maior média ocupa a 1ª posição.
