:pushpin: Título do Roteiro

:point_right: Descrição do(s) cenário(s) em que este roteiro pode ser aplicado

:compass: Palavras-chave para facilitar a indexação das buscas

:book: Detalhamento dos procedimentos, entradas necessárias e resultados esperados

:globe_with_meridians: Referências técnicas

--------------

:pushpin: Separar determinados registros em novos arquivos

:point_right: O poder computacional do SORT/DFSORT, que disponibiliza o utilitário multi propósito chamado ICETOOL, permite trabalhar com grandes volumes de dados, sejam em arquivos únicos ou vários arquivos. 

Neste roteiro utilizaremos a característica de filtragem de registros para separar informações em arquivos diferentes.

Outros exemplos de contagem de ocorrências podem ser encontrados no link das referências.

:compass: copiar, arquivo, ICETOOL, DFSORT

:book: Este job identifica o conteúdo a ser filtrado no campo chave do arquivo Input e grava os registros que possuem este conteúdo em um arquivo chamado Chave e os demais registros no arquivo chamado Outros.

JCL:
```jcl
//STEP01 EXEC PGM=SORT
//SORTIN DD DSN=MEU.ARQUIVO.INPUT,DISP=SHR
//CHAVE  DD DSN=MEU.ARQUIVO.CHAVE,DISP=(NEW,CATLG,DELETE)
//OUTROS DD DSN=MEU.ARQUIVO.OUTROS,DISP=(NEW,CATLG,DELETE)
//SYSIN DD *
 SORT FIELDS=COPY
 OUTFIL FNAMES=CHAVE,INCLUDE=(01,12,CH,EQ,C'MINAS GERAIS') /* Observar a instrução EQ=equal
 OUTFIL FNAMES=OUTROS,INCLUDE=(01,12,CH,NE,C'MINAS GERAIS') /* Observar a instrucao NE=not equal
```

:globe_with_meridians: https://www.ibm.com/docs/en/zos/3.1.0?topic=reports-including-omitting-saving-discards
