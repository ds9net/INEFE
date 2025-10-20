:pushpin: Título do Roteiro

:point_right: Descrição do(s) cenário(s) em que este roteiro pode ser aplicado

:compass: Palavras-chave para facilitar a indexação das buscas

:book: Detalhamento dos procedimentos, entradas necessárias e resultados esperados

:globe_with_meridians: Referências técnicas

--------------

:pushpin: Alocar/excluir arquivos

:point_right: IEFBR14 é frequentemente utilizado como uma forma controlada de acionar serviços do sistema, como alocação ou exclusão de datasets, sem a necessidade de um programa complexo. Sua execução serve como gatilho para que componentes do sistema z/OS entrem em ação. É uma ferramenta clássica para operações diversas em modo batch.

:compass: IEFBR14, alocar, desalocar, arquivos, datasets, jcl

:book: O job a seguir ativa a verificação das instruções JCL quanto a erros de sintaxe, cria o arquivo definido por NOVO mantendo-o alocado ao final da execução do job, em seguida exclui o arquivo definido por APAGAR, desalocando-o ao término do job.

JCL:
```jcl
//JOB04   JOB (INEFE),'ALOCA E DESALOCA',CLASS=A,MSGLEVEL=(1,1),  
//        MSGCLASS=C,REGION=0M,NOTIFY=&SYSUID                     
//* -------------------------------------                         
//STEP01  EXEC PGM=IEFBR14                                        
//APAGAR  DD DSN=KC03BFF.ANTIGO.ARQUIVO,DISP=(OLD,DELETE), 
//        DCB=(RECFM=FB,LRECL=80,BLKSIZE=0),                      
//        SPACE=(TRK,(1,1))                                       
//NOVO    DD DSN=KC03BFF.NOVO.ARQUIVO,DISP=(NEW,CATLG),           
//        DCB=(RECFM=FB,LRECL=80,BLKSIZE=0),                      
//        SPACE=(TRK,(1,1))                                       ```
```

Se o job acima for executado duas vezes seguidas, ele vai retornar um código de erro devido a existência do arquivo NOVO, criado pela execução anterior, e devido ao arquivo APAGAR não existir mais no sistema. Seguem os erros e tela de execução:

ERRO: 
<img width="1453" height="450" alt="image" src="https://github.com/user-attachments/assets/6819bba0-eb7a-40a6-88c4-2c41c4e1440a" />

```jcl
IEFA107I JOB04 STEP01 APAGAR - DATA SET KC03BFF.ANTIGO.ARQUIVO NOT FOUND
```

O ajuste abaixo evita o erro ao deletar o arquivo Antigo:
```jcl
//JOB04   JOB (INEFE),'ALOCA E DESALOCA',CLASS=A,MSGLEVEL=(1,1),  
//        MSGCLASS=C,REGION=0M,NOTIFY=&SYSUID                     
//* -------------------------------------                         
//STEP01  EXEC PGM=IEFBR14                                        
//APAGAR  DD DSN=KC03BFF.ANTIGO.ARQUIVO,DISP=(MOD,DELETE,DELETE), 
//        DCB=(RECFM=FB,LRECL=80,BLKSIZE=0),                      
//        SPACE=(TRK,(1,1))                                       
//NOVO    DD DSN=KC03BFF.NOVO.ARQUIVO,DISP=(NEW,CATLG),           
//        DCB=(RECFM=FB,LRECL=80,BLKSIZE=0),                      
//        SPACE=(TRK,(1,1))                                       
```
Resultado:
```JCL
IGD105I KC03BFF.ANTIGO.ARQUIVO                       DELETED,   DDNAME=APAGAR
```
:globe_with_meridians: https://www.ibm.com/docs/en/zos-basic-skills?topic=utilities-iefbr14-utility-do-almost-nothing
