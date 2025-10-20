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
//JOB04  JOB (ACCT),'ALOCA E DESALOCA',MSGCLASS=X,CLASS=A
//STEP01 EXEC PGM=IEFBR14
//NOVO   DD DSN=MEU.NOVO.ARQUIVO,DISP=(NEW,CATLG),VOL=SER=WORK02,
//          UNIT=3390,SPACE=(CYL,(3,1,25)
//APAGAR DD DSN=MEU.ANTIGO.ARQUIVO,DISP=(OLD,DELETE)
```

Se o job acima for executado duas vezes seguidas, ele vai retornar um código de erro devido a existência do arquivo NOVO, criado pela execução anterior, e devido ao arquivo APAGAR não existir mais no sistema. Uma sugestão para evitar estas ocorrências seria esta alteração:

```jcl
//JOB04  JOB (ACCT),'ALOCA E DESALOCA',MSGCLASS=X,CLASS=A
//STEP01 EXEC PGM=IEFBR14
//APAGAR DD DSN=MEU.NOVO.ARQUIVO,DISP=(MOD,DELETE),SPACE=(TRK,(1,1)),                 
//       UNIT=SYSDA                         
//NOVO   DD DSN=MEU.NOVO.ARQUIVO,DISP=(NEW,CATLG),VOL=SER=WORK02,
//       UNIT=3390,SPACE=(CYL,(3,1,25)
```
:globe_with_meridians: https://www.ibm.com/docs/en/zos-basic-skills?topic=utilities-iefbr14-utility-do-almost-nothing
