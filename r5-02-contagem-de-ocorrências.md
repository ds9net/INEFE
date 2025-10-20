:pushpin: Título do Roteiro

:point_right: Descrição do(s) cenário(s) em que este roteiro pode ser aplicado

:compass: Palavras-chave para facilitar a indexação das buscas

:book: Detalhamento dos procedimentos, entradas necessárias e resultados esperados

:globe_with_meridians: Referências técnicas

--------------

:pushpin: Contagem de ocorrências de um campo ou chave em um arquivo

:point_right: O poder computacional do SORT/DFSORT, que disponibiliza o utilitário multi propósito chamado ICETOOL, permite trabalhar com grandes volumes de dados, sejam em arquivos únicos ou vários arquivos. 

Neste roteiro utilizaremos a característica de contagem de registros que possuem a mesma informação, gerando um arquivo com os totais de ocorrências de cada uma. 

Outros exemplos de contagem de ocorrências podem ser encontrados no link das referências.

:compass: copiar, arquivo, ICETOOL, DFSORT

:book: Este job conta ordena o arquivo de entrada pela chave indicada, acrescenta um trailer em cada registro contendo a quantidade de ocorrências. 

Se compararmos com instrução SQL, seria o equivalente a:
```sql
Select campo-1a12, count(*)
groyp by campo-1a12;
```

JCL:
```jcl
//CONTAR JOB (ACCT),'SORT SUM',CLASS=A,MSGCLASS=X
//SORT01 EXEC PGM=SORT
//SYSOUT DD SYSOUT=*
//SORTIN DD DSN=MEU.ARQUIVO.INPUT,DISP=SHR
//SORTOUT DD DSN=MEU.ARQUIVO.OUTPUT,DISP=(NEW,CATLG,DELETE),
//           SPACE=(TRK,(5,2)),UNIT=SYSDA
//SYSIN DD *
   SORT FIELDS=(1,12,CH,A) /* Ordena o campo chave que ocupa as posições 1-12
   OUTFIL REMOVECC,NODETAIL,                         
   SECTIONS=(1,12,TRAILER3=(1,12,X,COUNT=(M11,LENGTH=8)))
```

:globe_with_meridians: https://www.ibm.com/docs/en/zos/3.1.0?topic=fields-editing-numeric
