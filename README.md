### GitHub utilizado na Gestão do Conhecimento:  uma abordagem prática de documentação e recuperação da informação para monitoramento e diagnósitico de ocorrências no ambiente Mainframe IBM

**Aluno: Esmet Mustafá Ammar**

**Orientadora: Msc. Profa. Ana Cristina B.R. Silva** 


<img width="1476" height="781" alt="TN3270-Marist1" src="https://github.com/user-attachments/assets/89e7a9d9-305f-4aed-a682-d6d42a6f7687" />

Significado dos ícones encontrados nos textos a seguir:

   :pushpin: Título do Roteiro
   
   :point_right: Descrição do(s) cenário(s) em que este roteiro pode ser aplicado
   
   :compass: Palavras-chave para facilitar a indexação das buscas
   
   :book: Detalhamento dos procedimentos, entradas necessárias e resultados esperados
   
   :globe_with_meridians: Referências técnicas

>  Os roteiros a seguir tem o propósito de sintetizar o conhecimento adquirido em mais de 400 horas de treinamento. Em cada um são indicadas as referências aos sites oficiais da IBM que detalham as características e múltiplos parâmetros das ferramentas utilizadas. 
<img width="485" height="210" alt="TN3270-Marist2" src="https://github.com/user-attachments/assets/d6cc8918-324f-4232-8048-0a145ceab3f6" />

## 1) Coleta de Dados do sistema
- [SMF/RMF: registros de execução e performance (CPU, memória, I/O, workloads).](https://github.com/ds9net/INEFE/blob/Roteiros/r1-01-SMF-RMF-registros-de-execu%C3%A7%C3%A3o-performance.md)
    
## 2) Análise de Jobs

- [Principais consultas de Jobs: SDSF, JESMSGLG/JESYSMSG/JOBLOG.](https://github.com/ds9net/INEFE/blob/Roteiros/r2-01-Principais-consultas-de-Jobs.md)
    
- [Checklist de diagnóstico para jobs anormais (JCL errors, RC≠0)](https://github.com/ds9net/INEFE/blob/Roteiros/r2-01-Principais-consultas-de-Jobs.md#checklist-de-diagn%C3%B3stico)
    1. [RC 04 → Warning (revisar lógica)](https://github.com/ds9net/INEFE/blob/Roteiros/r2-01-Principais-consultas-de-Jobs.md#checklist-de-diagn%C3%B3stico);
    2. [RC 08/12 → Erro esperado de aplicação](https://github.com/ds9net/INEFE/blob/Roteiros/r2-01-Principais-consultas-de-Jobs.md#checklist-de-diagn%C3%B3stico);
    3. [RC 16/20+ → Falha estrutural ou de ambiente](https://github.com/ds9net/INEFE/blob/Roteiros/r2-01-Principais-consultas-de-Jobs.md#checklist-de-diagn%C3%B3stico).    
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
    1.  [ordenação de registros](https://github.com/ds9net/INEFE/blob/Roteiros/r5-01-ordena%C3%A7%C3%A3o-de-registros.md)
    2.  [contagem de ocorrências](https://github.com/ds9net/INEFE/blob/Roteiros/r5-02-contagem-de-ocorr%C3%AAncias.md)
    3.  [separar determinados registros em novos arquivos](https://github.com/ds9net/INEFE/blob/Roteiros/r5-03-separar-determinados-registros-em-novos-arquivos.md)    
    4.  [alocar/excluir arquivos](https://github.com/ds9net/INEFE/blob/Roteiros/r5-04-alocar-excluir-arquivos.md)
    5.  [copiar arquivos](https://github.com/ds9net/INEFE/blob/Roteiros/r5-05-copiar-arquivos.md)
    6.  [comparar conteúdo de arquivos](https://github.com/ds9net/INEFE/blob/Roteiros/r5-06-comparar-conteudo-arquivos.md)
