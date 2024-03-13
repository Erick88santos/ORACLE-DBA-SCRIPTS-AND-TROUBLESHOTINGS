# ORACLE-DBA-SCRIPTS-AND-TROUBLESHOTINGS

##**Configurar o Statspack no Oracle Database**

Para configurar o Statspack no Oracle Database, siga estas etapas:
1.	**Conectar-se como DBA:** Utilize um cliente SQL ou a linha de comando para se conectar ao Oracle Database como um usuário com privilégios de DBA (Database Administrator).
2.	**Criar a Tabela de Estatísticas:** Execute o script spcreate.sql, localizado no diretório $ORACLE_HOME/rdbms/admin, para criar a tabela de estatísticas do Statspack. Este script cria a tabela STATSPACK no schema selecionado.

``@?/rdbms/admin/spcreate.sql``

3. **Configurar o Schema de Coleta de Estatísticas:** Defina o schema onde as estatísticas do Statspack serão armazenadas. Isso é feito alterando a variável de ambiente STATSOWN para o nome do schema desejado. Por exemplo, para definir o schema como **STATPACK:**

``ALTER SESSION SET EVENTS '10401 TRACE NAME CONTEXT FOREVER, LEVEL 1';``

``ALTER SYSTEM SET STATISTICS_LEVEL = TYPICAL SCOPE = BOTH;``

4. **Executar a Coleta de Estatísticas:** Para iniciar a coleta de estatísticas, execute o procedimento statspack.snap especificando o intervalo de coleta desejado. Por exemplo, para coletar estatísticas a cada hora:

``EXEC statspack.snap;``

5. **Gerar Relatórios de Desempenho:** Para gerar um relatório de desempenho com base nas estatísticas coletadas, execute o procedimento *statspack.report.* Por exemplo, para gerar um relatório para o último snapshot:

``SET LONG 1000000``
``SET PAGESIZE 1000``
``SET LINESIZE 200``
``SELECT * FROM TABLE(statspack.snap);``

6. **Automatizar a Coleta de Estatísticas (Opcional):** Você pode configurar um job no Oracle Scheduler para executar o procedimento statspack.snap periodicamente e automatizar a coleta de estatísticas.

Lembre-se de revisar a documentação do Oracle Database e adaptar essas instruções de acordo com a sua versão específica do banco de dados e requisitos do seu ambiente.
