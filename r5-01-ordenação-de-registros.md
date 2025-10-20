:pushpin: Título do Roteiro

:point_right: Descrição do(s) cenário(s) em que este roteiro pode ser aplicadado

:compass: Palavras-chave para facilitar a indexação das buscas

:book: Detalhamento dos procedimentos, entradas necessárias e resultados esperados

:globe_with_meridians: Referências técnicas

--------------

:pushpin: ordenação de registros utilizando uma determinada chave

:point_right: O poder computacional do SORT/DFSORT, que disponibiliza o utilitário multi propósito chamado ICETOOL, permite trabalhar com grandes volumes de dados, sejam em arquivos únicos ou vários arquivos. 
Neste roteiro utilizaremos a característica de ordenar os registros de um arquivo por determinado campo/chave. 
Mais detalhes sobre seu funcionamento e outros exemplos podem ser encontrados no link das referências.

:compass: copiar, arquivo, ICETOOL, DFSORT

:book: O job a seguir recebe como entrada um arquivo INPUT e cataloga um arquivo OUTPUT contendo as mesmas informações do arquivo de entrada com a diferença de estar com os registros em ordem alfabética pelo campo indicado:

JCL:
```jcl
//ORDENA JOB (ACCT),'ORDENAR',CLASS=A,MSGCLASS=X
//STEP01 EXEC PGM=SORT
//SYSOUT DD SYSOUT=*
//SORTIN DD DSN=MEU.ARQUIVO.INPUT,DISP=SHR
//SORTOUT DD DSN=MEU.ARQUIVO.OUTPUT,DISP=(NEW,CATLG,DELETE),
// SPACE=(TRK,(5,2)),UNIT=SYSDA
//SYSIN DD *
 SORT FIELDS=(1,10,CH,A) /* Ordena pela posição 1-10, CH=formato alfanumérico, A=ascendente
```

:globe_with_meridians: https://www.ibm.com/docs/en/zos/2.4.0?topic=operator-sort-examples
