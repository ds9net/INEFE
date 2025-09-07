GitHub utilizado na Gestão do Conhecimento:  uma abordagem prática de documentação e recuperação da informação para monitoramento e diagnósitico de ocorrências no ambiente Mainframe IBM

**Aluno: Esmet Mustafá Ammar**

**Orientadora: Msc. Profa. Ana Cristina B.R. Silva** 

**Cada roteiro está padronizado com as seguintes sessões:**

   :pushpin: Título do Roteiro
   
   :point_right: Descrição do(s) cenário(s) em que este roteiro pode ser aplicadado
   
   :compass: Palavras-chave para facilitar a indexação das buscas
   
   :book: Detalhamento dos procedimentos, entradas necessárias e resultados esperados
   
   :globe_with_meridians: Referências técnicas

>  Os roteiros a seguir tem o propósito de sintetizar o conhecimento adquirido em mais de 400 horas de treinamento. Em cada um são indicadas as referências aos sites oficiais da IBM que detalham as características e múltiplos parâmetros das ferramentas utilizadas. 

## 1) Coleta de Dados do sistema
- SMF/RMF: registros de execução e performance (CPU, memória, I/O, workloads).
    
## 2) Análise de Jobs

- Principais consultas de Jobs: SDSF, JESMSGLG/JESYSMSG/JOBLOG.
    
- Checklist de diagnóstico para jobs anormais (JCL errors, RC≠0)
    1. RC 04 → Warning (revisar lógica);
    2. RC 08/12 → Erro esperado de aplicação;
    3. RC 16/20+ → Falha estrutural ou de ambiente.    
## 3) Diagnóstico de Subsistemas
- DB2:
    1. Analisar objetos inválidos, identificar deadlocks e locks.
- MQ:
    1. Alertas para canais stopped e filas com acúmulo.
- CICS:
    1. Logs que indicam gargalos;
    2. Programas loops, tasks long-running.
- RACF (Resource Access Control Facility):
    1. Usuarios, privilégios;
    2. Grupos de Acesso e Datasets.          
- Storage:
    1. LISTCAT para catálogos.
    2. Análise de volumes.
## 4) Monitoração automática
- Geração de relatórios automáticos para identificar:
    1. Jobs críticos falhados.
    2. Locks DB2.
    3. MQ depth anormal.
    4. CICS tasks suspensas.
    5. Utilização de storage acima de thresholds ou contenções.
## 5) Jobs reutilizáveis para tarefas rotineiras
- Exemplos de Jobs prontos para:
    1.  ordenação de registros
    2.  contagem de ocorrências
    3.  separar determinados registros em novos arquivos
    4.  copiar arquivos
    5.  alocar/excluir arquivos
    6.  extrair informações de um JCL (IEBEDIT)
    7.  comparar conteúdo de arquivos
