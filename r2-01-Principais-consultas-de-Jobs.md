:pushpin: Título do Roteiro

:point_right: Descrição do(s) cenário(s) em que este roteiro pode ser aplicado

:compass: Palavras-chave para facilitar a indexação das buscas

:book: Detalhamento dos procedimentos, entradas necessárias e resultados esperados

:globe_with_meridians: Referências técnicas

--------------

:pushpin: Principais consultas de Jobs: SDSF, JESMSGLG/JESYSMSG/JOBLOG.

:point_right: As execuções dos jobs no Mainframe IBM geram um conjunto de logs específicos, detalhando o status de cada step (JESMSGLG), o status de interação com o sistema operacional (JESYSMSGLG) e as mensagens de geradas pela execução do job (JOBLOG). Todos estes detalhes estão disponíveis para consulta e interação via SDSF (System Display and Search Facility). 

Este roteiro detalhará os seguintes tópicos:
1. [Consultas Principais de Jobs](#consultas-principais-de-jobs)
2. [JESMSGLG / JESYSMSG / JOBLOG](#jesmsgl)
3. [Checklist de Diagnóstico](#checklist-de-diagnóstico)
4. [Etapas para Diagnóstico](#etapas-para-diagnóstico)

:compass: SDSF, JES, JESMSGLB, JESYSMSG, datasets, jcl, fila DA, fila ST, fila H.

:book: A seguir estão as principais funcionalidades que permitem analisar a execução de um job, diagnosticando eventuais falhas na escrita do JCL, chamada de utilitários ou utilização dos recursos do ambiente (storage, etc).

### 1. Consultas Principais de Jobs

    * SDSF (System Display and Search Facility) - ferramenta utilizada para visualizar e gerenciar jobs no JES (Job Entry Subsystem).
    * Comandos úteis:
       - ST – Visualiza o status dos jobs ativos;
       - DA – Lista os datasets alocados;
       - LOG – Exibe o log do sistema;
       - HASPLOG – Mostra mensagens do JES. 
    
### 2. JESMSGLG / JESYSMSG / JOBLOG
    * Esses logs são essenciais para entender o comportamento do job:
      - JESMSGLG: Mensagens do JES sobre o job (início, término, alocação de recursos);
      - JESYSMSG: Mensagens do sistema operacional (erros, alocações, chamadas de sistema);
      - JOBLOG: Saída geral do job, incluindo mensagens de erro, retornos e prints.

<img width="1462" height="664" alt="image" src="https://github.com/user-attachments/assets/93137bcc-bfc6-40d9-bf19-0d5a8f7ceb4f" />
<img width="1439" height="291" alt="image" src="https://github.com/user-attachments/assets/230de142-22e6-4d8c-88bb-1663fad800e2" />


### 3. Checklist de Diagnóstico para Jobs com retorno diferente de zero (RC ≠ 0)
   
|RC-Return Code|Significado|Ação Recomendada|
|--------------|-----------|----------------|
|RC 04|Warning – O job foi executado, mas houve alertas.|Revisar a lógica do JCL ou programa. Verificar mensagens de advertência no JOBLOG. Pode indicar uso de parâmetros não ideais ou condições não críticas.|
|RC 08 / RC 12|Erro esperado de aplicação – O job falhou por erro de lógica ou dados.|Verificar mensagens de erro no JESYSMSG e JOBLOG. Validar parâmetros de entrada, arquivos utilizados, e lógica do programa. Pode ser necessário ajustar o código ou os dados.|
|RC 16 / RC 20+|Falha estrutural ou de ambiente – Erros graves.|Investigar alocação de recursos, permissões, ausência de datasets, problemas de compilação. Verificar mensagens no JESMSGLG e JESYSMSG. Pode indicar falhas no ambiente ou infraestrutura.|

### 4. Etapas para Diagnóstico
1. Identificar o Job: Localize o job via SDSF (ST ou H) e anote o Job ID. 
2. Verificar Logs: Acesse JESMSGLG, JESYSMSG e JOBLOG para entender o fluxo e identificar mensagens de erro.
3. Analisar RC: Verifique o código de retorno (RC) e aplique o checklist acima.
4. Validar Recursos: Confirme se os datasets estão corretamente alocados (DA) e se há permissões adequadas. 
5. Consultar Histórico: Verifique execuções anteriores para identificar padrões de falha.
6. Documentar Ações: Registre os passos tomados e os ajustes realizados para futuras referências. 
   
:globe_with_meridians: https://www.ibm.com/docs/en/zos-basic-skills?topic=sdsf-what-is-system-display-search-facility

:globe_with_meridians: https://www.ibm.com/docs/en/zos/3.1.0?topic=punches-jes2-system-data-sets

:globe_with_meridians: https://www.ibm.com/docs/en/zos-basic-skills?topic=jobs-job-flow-through-system

:globe_with_meridians: https://www.ibm.com/docs/en/zdmf/3.4.1?topic=return-codes
