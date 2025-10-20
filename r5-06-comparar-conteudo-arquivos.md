:pushpin: Título do Roteiro

:point_right: Descrição do(s) cenário(s) em que este roteiro pode ser aplicado

:compass: Palavras-chave para facilitar a indexação das buscas

:book: Detalhamento dos procedimentos, entradas necessárias e resultados esperados

:globe_with_meridians: Referências técnicas

--------------

:pushpin: Comparar conteúdo de dois arquivos

:point_right: O poder computacional do SORT/DFSORT, que disponibiliza o utilitário multi propósito chamado ICETOOL, permite trabalhar com grandes volumes de dados, sejam em arquivos únicos ou vários arquivos. 

Neste roteiro utilizaremos a característica de batimento ou balanced line de arquivos. Este processo utiliza um campo chave que possui conteúdo comum entre os dois arquivos. 

:compass: copiar, arquivo, ICETOOL, DFSORT

:book: O job a seguir compara dois arquivos em busca dos registros que possuem a mesma chave, gerando um arquivo de saída com os dados que são comuns aos dois registros (joinkeys).

JCL:
```jcl
//STEP01 EXEC PGM=SORT
//SORTJNF1 DD DSN=ARQUIVO1,DISP=SHR
//SORTJNF2 DD DSN=ARQUIVO2,DISP=SHR
//SORTOUT DD DSN=ARQ1.ARQ2.OUT,DISP=(NEW,CATLG,DELETE)
//SYSOUT DD SYSOUT=*
//SYSIN DD *
JOINKEYS FILE=F1,FIELDS=(1,10,A)  * chave nas primeiras 10 posicoes do arquivo1
JOINKEYS FILE=F2,FIELDS=(1,10,A)  * chave nas primeiras 10 posicoes do arquivo2
REFORMAT FIELDS=(F1:1,10,F2:1,80) * a chave do arquivo1 e os dados do arquivo 2 até a posicao 80.
```

:globe_with_meridians: https://www.ibm.com/docs/en/zos/3.1.0?topic=statements-joining-records
