:pushpin: Título do Roteiro

:point_right: Descrição do(s) cenário(s) em que este roteiro pode ser aplicado

:compass: Palavras-chave para facilitar a indexação das buscas

:book: Detalhamento dos procedimentos, entradas necessárias e resultados esperados

:globe_with_meridians: Referências técnicas

--------------

:pushpin: SMF/RMF: registros de execução e performance (CPU, memória, I/O, workloads).

:point_right: O SMF - System Management Facility - é um produto IBM, componente do z/OS, responsável pela captura e
armazenamento de informações diversas sobre o funcionamento e uso de
diversos outros produtos, inclusive do próprio sistema operacional.
O SMF possui diversos tipos de registros, para diferentes finalidades, que
podem ser processados, através de softwares de terceiros, ou até mesmo pelo
RMF - Resource Measurement Facilty, para gerar os mais diversos tipos de relatórios, seja sobre acessos a
determinados DATASETs, seja sobre informações de performance, entre outras
finalidades. 



<img width="1179" height="737" alt="image" src="https://github.com/user-attachments/assets/cdce38af-fa17-4d51-9683-6c863d394ef3" />

<img width="1259" height="681" alt="image" src="https://github.com/user-attachments/assets/917965fc-91b0-41d1-a3b5-1fd40bc686dc" />

<img width="1231" height="763" alt="image" src="https://github.com/user-attachments/assets/0da717f5-bedc-4a4b-b7fe-5baa3b1780ef" />

<img width="1174" height="727" alt="image" src="https://github.com/user-attachments/assets/37ec4ccb-ed02-4717-84e4-104dee9695bc" />

<img width="1165" height="825" alt="image" src="https://github.com/user-attachments/assets/ac52794e-3c0d-49b7-9f51-6f144e1e73d9" />


:compass: SMF, RMF, CPU, MEMÓRIA, I/O, WORKLOAD.

:book: A seguir estão os detalhes de como extrair os dados dos datasets que armazenam as informações do SMF e como são formatados para análise. Observar que o HLQ (High Level Qualifier) do arquivo SYS1.MAN pode ser ajustado conforme o padrão corporativo. Este job pode ser schedulado/automatizado para executar em intervalos periódicos, exportando-se o arquivo final para um dashboard de monitoramento para visualização gráfica ou sumarização dos dados extraídos (CPU, MEM, I/O):
  
    . STEP1 (IFASMFDP)
       Extrai registros SMF dos datasets ativos (SYS1.MANx).
       Filtra tipos 30 (execução) e 70-79 (performance CPU, memória, I/O).



    . STEP2 (IDCAMS REPRO)
       Converte o arquivo VBS para VB, facilitando processamento posterior.



    . STEP3 (IEBGENER)
       Grava os dados em um arquivo sequencial com RECFM=FB, ideal para relatórios ou exportação.
 

JCL:
```jcl
//EXTRSMF  JOB (INEFE),'EXTRACAO SMF',CLASS=A,MSGCLASS=X,NOTIFY=&SYSUID
//*---------------------------------------------------------------*
//*  PASSO 1: EXTRAIR REGISTROS SMF (TIPOS 30, 70-79)            *
//*---------------------------------------------------------------*
//STEP1    EXEC PGM=IFASMFDP
//SYSPRINT DD SYSOUT=*
//DUMPIN   DD DSN=SYS1.MAN1,DISP=SHR
//DUMPOUT  DD DSN=HLQ.SMF.DUMP,DISP=(NEW,CATLG,DELETE),
//         UNIT=SYSDA,SPACE=(CYL,(50,10)),
//         DCB=(RECFM=VBS,LRECL=32756,BLKSIZE=32760)
//SYSIN    DD *
  INDD(DUMPIN,OPTIONS(DUMP))
  OUTDD(DUMPOUT,TYPE(30,70:79))
/*
//*----------------------------------------------------------------*
//*  PASSO 2: CONVERTER PARA FORMATO VB USANDO IDCAMS REPRO       *
//*----------------------------------------------------------------*
//STEP2    EXEC PGM=IDCAMS
//SYSPRINT DD SYSOUT=*
//SYSIN    DD *
  REPRO INFILE(DUMPOUT) OUTFILE(WORKSMF)
/*
//DUMPOUT  DD DSN=HLQ.SMF.DUMP,DISP=SHR
//WORKSMF  DD DSN=HLQ.SMF.WORK,DISP=(NEW,CATLG,DELETE),
//         UNIT=SYSDA,SPACE=(CYL,(50,10)),
//         DCB=(RECFM=VB,LRECL=32756,BLKSIZE=32760)
//*----------------------------------------------------------------*
//*  PASSO 3: GRAVAR EM ARQUIVO SEQUENCIAL PARA RELATÓRIO         *
//*----------------------------------------------------------------*
//STEP3    EXEC PGM=IEBGENER
//SYSUT1   DD DSN=HLQ.SMF.WORK,DISP=SHR
//SYSUT2   DD DSN=HLQ.SMF.REPORT,DISP=(NEW,CATLG,DELETE),
//         UNIT=SYSDA,SPACE=(CYL,(10,5)),
//         DCB=(RECFM=FB,LRECL=200,BLKSIZE=0)
//SYSPRINT DD SYSOUT=*
//SYSIN    DD DUMMY
```

:globe_with_meridians: https://www.ibm.com/docs/en/z-decision-support/1.9.0?topic=performance-using-rmf-smf-data
:globe_with_meridians: https://www.ibm.com/docs/en/z-backup-resiliency/1.2.0?topic=smf-data-extraction
