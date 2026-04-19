# Dicionário de Dados  

## Convenção de Tipagem utilizada nesta documentação:
* **INT4:** Campos destinados a chaves primárias ou valores numéricos sem casas decimais (como quantidade de acertos ou idade).
* **VARCHAR(50):** Campos de texto alfanumérico limitados, ideais para nomes de turmas, nomes de alunos ou classificações (como "Básico", "Adequado"), garantindo a economia de armazenamento no banco.
* **NUMERIC:** Escolhido para campos de cálculo (como a Proficiência ou a Porcentagem de Acerto) por permitir casas decimais e garantir que não haja perda de precisão em operações matemáticas.

## Tabelas Originais
#### Tabela Dimensão: Turmas
OBS: Coluna ID_TURMA se conecta com coluna de mesmo nome na tabela AVALIA.
| Coluna | Tipo | Descrição | Observações/Domínio |
| :--- | :--- | :--- | :--- |
| ID_TURMA | Varchar (50)| Chave primária da turma | Única por turma. Utilizada para relacionamento (JOIN). |
| NOME_TURMA | Varchar (50) | Referência nominal da turma | Ex: Ailton Krenak, Lélia Gonzalez. |
| SÉRIE | Varchar (50) | Nível de Escolaridade | Domínio fixo: "1º Ano EM". |
| TURNO | Varchar (50) | Período em que frequentam as aulas | Manhã (1A, 1B) e Tarde (1C, 1D). |


#### Tabela Dimensão: Alunos
OBS: Coluna ID_ALUNO se conecta com coluna de mesmo nome na tabela AVALIA.
| Coluna | Tipo | Descrição | Observações/Domínio |
| :--- | :--- | :--- | :--- |
| ID_ALUNO | Int4 | Chave primária do aluno | Única por aluno |
| NOME | Varchar (50) | Nome cadastrado | Único por aluno |
| IDADE | Int4 | Idade cadastrada | Faixa etária entre 14 e 17 anos |


#### Tabela Dimensão: Proficiencia
Nota: A Proficiencia nas próximas tabelas se refere ao domínio dos estudantes na disciplina de matemática, em uma avaliação externa. A classificação considera pontuações de diferentes questões, tempo de prova, dentre outros critérios.

OBS: Coluna ID_PROFICIENCIA se conecta com coluna de mesmo nome na tabela AVALIA.
| Coluna | Tipo | Descrição | Observações/Domínio |
| :--- | :--- | :--- | :--- |
| ID_PROFICIENCIA | Int4| Chave primária da proficiência | Única por nível |
| FAIXA_DE_PROFICIENCIA | Varchar (50) | Nome cadastrado | ... |
| NÍVEL_ORDEM | Int4 | Idade cadastrada | Mostra qual está mais abaixo e qual está mais acima, dentre as FAIXAS DE PROFICIENCIA |
| DESCRIÇÃO | Varchar (50)  | Detalhamento do que ... | Detalha o que cada Faixa de Proficiencia indica sobre os estudantes |


#### Tabela Fato: Avalia
Nota: Cada questão da prova tem um peso diferente, o que leva a pontuações diferentes para o mesmo ID_PROFICIENCIA;

OBS: Colunas ID_ALUNO, ID_TURMA e ID_PROFICIENCIA se conecta com colunas de mesmo nome nas tabelas dimensão.
| Coluna | Tipo | Descrição | Observações/Domínio |
| :--- | :--- | :--- | :--- |
| ID_ALUNO | Int4| Chave primária do aluno | Única por aluno |
| ID_TURMA | Varchar (50) | Chave primária da turma | Única por turma |
| ACERTOS | Int4 | Qtd de itens respondidos corretamente | Intervalo de 0 a 32 |
| TOTAL_QUESTOES | Int4| Qtd de itens na avaliação externa | Por padrão, são 32 questões |
| PROFICIENCIA | Numeric| Pontuação de cada aluno | Critérios diversos de avaliação |
| ID_PROFICIENCIA | Int4| Chave primária da proficiência | Indica o nível de desempenho do aluno |

(ARRUMAR A PARTIR DAQUI)

| ACERTOS | Integer | Qtd de itens respondidos corretamente | Range: 0 a 32 |
| STATUS_APROVEITAMENTO| String | Classificação de rendimento | Calculado via DAX/SQL |
| ALUNOS_EM_RISCO | String | Identificador de alerta pedagógico | Baseado em critérios de proficiência e acertos |

## Novas Métricas
#### Tabela: Analise Geral
OBS: Coluna ID_TURMA se conecta com coluna de mesmo nome na tabela AVALIA.
| Coluna | Tipo | Descrição | Observações/Domínio |
| :--- | :--- | :--- | :--- |
| ID_TURMA | Integer (ARRUMAR DEPOIS, DBEAVER)| Chave primária da turma | Única por turma |
| NOME_TURMA | Integer | Referência nominal da turma | Único por turma |

#### Tabela: Analise Turmas
OBS: Coluna ID_TURMA se conecta com coluna de mesmo nome na tabela AVALIA.
| Coluna | Tipo | Descrição | Observações/Domínio |
| :--- | :--- | :--- | :--- |
| ID_TURMA | Integer (ARRUMAR DEPOIS, DBEAVER)| Chave primária da turma | Única por turma |
| NOME_TURMA | Integer | Referência nominal da turma | Único por turma |
