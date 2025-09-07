:pushpin: Copiar Arquivos utilizando Icetool

:point_right: O poder computacional do DFSORT, que disponibiliza o utilitário multi propósito chamado ICETOOL, permite trabalhar com grandes volumes de dados, sejam em arquivos únicos ou vários arquivos. Neste roteiro utilizaremos a característica de copiar arquivos. No link das referências é possível encontar mais detalhes sobre seu funcionamento e outros exemplos.

:compass: copiar, arquivo, ICETOOL, DFSORT

:book: O job a seguir recebe como entrada um arquivo INPUT e cataloga um arquivo OUTPUT contendo as mesmas informações do arquivo de entrada. Se os parâmetros de alocação não corresponderem ao LRECL do arquivo de entrada, os dados serão truncados, nenhuma informação de erro será gerada, terminando com OPERATION RETURN CODE:  00, mas indicando a diferença na quantidade de bytes por registro com a seguinte mensagem:

**SORTOUT LRECL OF Y IS DIFFERENT FROM SORTIN(NN) LRECL OF X - RC=0** 
```jcl
//JOBNAME JOB (ACCT),'USER',MSGCLASS=X,CLASS=A
//STEP1 EXEC PGM=ICETOOL
//TOOLMSG DD SYSOUT=*
//DFSMSG DD SYSOUT=*
//ALL DD DSN=YOUR.INPUT.DATASET,DISP=SHR
//D1 DD DSN=YOUR.OUTPUT.DATASET.COPY1,DISP=(NEW,CATLG,DELETE),
//       DCB=(RECFM=FB,LRECL=80,BLKSIZE=0),SPACE=(CYL,(1,1))
//TOOLIN DD *
  COPY FROM(ALL) TO(D1)
/*
```

:globe_with_meridians: https://www.ibm.com/docs/en/zos/2.4.0?topic=icetool-overview
