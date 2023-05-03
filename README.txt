# churn_analysis

- Linguagem:
	- Python 3.8.2
		-Pandas 2.0.1
		- Numpy 1.24.3

-Elaboradas funções: 
	- obj_to_datetime(col): Leitura de datas no formato datetime, para padronização '%m/%d/%y %H:%M %p'
		-col: array pandas		
		-finalidade
	- diferenca_datas(series_final, series_inicial, periodo): calcula diferença entre datas
		- series_final: series NumPy declarada como data final
		- series_inicial: series NumPy declarada como data inicial
		- periodo: Y: ano; M: mês; D: dias
	- corrige_idade(array1): Uma vez que, de acordo com os padrões POSIX e ISO C, inteiros menores do que 69 são mapeados como sendo anos do século XXI, necessário adequar a idade de nascidos no século XX.
		- array1: array Pandas

-Transformações:
	-Tabela por usuário
		-conversão das datas de string para datetime;
		-cálculo de tempo de clientela (em meses)
		-cálculo de idade dos clientes, além de segmentação por faixa etária
		-binarização de status: "paused" e "active" convertidos para 1 e "canceled" para 0
	-Tabela por datas
		-Conta quantas contas foram criadas no mês, segmentando por estado
		-Conta quantas contas foram excluídas no mês, também segmentando por estado, em outra tabela
		-une ambas tabelas criadas
		-realização de soma acumulada de contas criadas por mês em determinado estado
		-realizaçao de soma acumulada de contas excluídas por mês em determinado estado
		-subtrai duas colunas anteriores para saber quantas cotas estavam ativas no fim do mês
		-soma contas ativas no fim do mês com excluídas ao longo do mês, para saber quantas estavam ativas no início do mês
		-calcula churn dividindo contas excluídas no mês com contas ativas no início do mês, multiplicando por 100


Tabelas finais:
	user_data:
		-id
		-usuario_criado: data de criação de usuário
		-usuario_excluido: data de esclusão de usuário
		-meses_assinatura: tempo de assinatura até a exclusão (-1 se conta ativa ou pausada)
		-intervalo de inatividade: tempo entre a data atual e a última compra (se ativo) ou entre a exclusão e a última compra (se excluído)
		-idade: idade
		-faixa_idade_05: segmentação de idade em grupos de cinco anos
		-faixa_idade_10: segmentação de idade em grupos de dez anos
		-ativo: 1 ativo, 0 inativo
		-versao: versão de quando da assinatura
		-cidade: cidade
		-estado: estado
		-gasto_medio: gasto médio do cliente
		-media_de_itens: media de itens adquiridos pelo cliente - pela quantidade de compras
		-gasto_total: gasto total do cliente
		-total_de_pedidos: total de pedidos realizados pelo cliente
		-canal_marketing: canal de captação
	calculo_churn:
		-estado: estado da federação
		-ano_mes: YYYYMM
		-contas_criadas: quantidade de contas criadas no mês - por estado
		-contas excluídas: quantidade de contas excluídas no mês - por estado
		-contas_criadas_acumuladas: soma acumulada de contas criadas de todo o período - por estado
		-contas_excluidas_acumuladas: soma acumulada de contas excluídas em todo o período - por estado
		-contas_ativas_fim_mes: contas ativas ao fim de cada mês - por estado
		-contas_ativas_comeco_mes: contas ativas no começo do mês - por estado
		-churn: índice de churn de um determinado mês - por estado



