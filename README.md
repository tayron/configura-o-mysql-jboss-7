# Configuração do drive MySQL no Jboss 7

Configuração para adicionar o drive do Mysql no Jboss7,

!) Adicionar dentro do diretório (diretório-jboss-7/modules/com/mysql/main) do Jboss 7 o diretório mysql que está no repositório.

2) Abra o arquivo standalone.xml que está em diretório-jboss-7/standalone/configuration/ e dentro da tag <datasources> adicione as seguintes configurações:

A) Adicione seu datasource:

                <datasource jndi-name="java:jboss/datasources/MySqlDS" pool-name="MySqlDS">
                    <connection-url>jdbc:mysql://localhost:3306/nome-do-seu-banco-de-dados-no-mysql</connection-url>
                    <driver>com.mysql</driver>
                    <transaction-isolation>TRANSACTION_READ_COMMITTED</transaction-isolation>
                    <pool>
                        <min-pool-size>10</min-pool-size>
                        <max-pool-size>100</max-pool-size>
                        <prefill>true</prefill>
                    </pool>
                    <security>
                        <user-name>usuario-do-mysql</user-name>
                        <password>senha-do-mysql</password>
                    </security>
                    <statement>
                        <prepared-statement-cache-size>32</prepared-statement-cache-size>
                        <share-prepared-statements>true</share-prepared-statements>
                    </statement>
                </datasource>

B) Adicione o drive do Mysql:

                <drivers>
                    <driver name="com.mysql" module="com.mysql">
                        <xa-datasource-class>com.mysql.jdbc.jdbc2.optional.MysqlXADataSource</xa-datasource-class>
                    </driver>
                </drivers>
                
No final sua configuração deverá ser semelhante ao exemplo abaixo:

        <subsystem xmlns="urn:jboss:domain:datasources:1.0">
            <datasources>
                <datasource jndi-name="java:jboss/datasources/ExampleDS" pool-name="ExampleDS" enabled="true" use-java-context="true">
                    <connection-url>jdbc:h2:mem:test;DB_CLOSE_DELAY=-1</connection-url>
                    <driver>h2</driver>
                    <security>
                        <user-name>sa</user-name>
                        <password>sa</password>
                    </security>
                </datasource>
                <datasource jndi-name="java:jboss/datasources/MySqlDS" pool-name="MySqlDS">
                    <connection-url>jdbc:mysql://localhost:3306/nome-do-seu-banco-de-dados-no-mysql</connection-url>
                    <driver>com.mysql</driver>
                    <transaction-isolation>TRANSACTION_READ_COMMITTED</transaction-isolation>
                    <pool>
                        <min-pool-size>10</min-pool-size>
                        <max-pool-size>100</max-pool-size>
                        <prefill>true</prefill>
                    </pool>
                    <security>
                        <user-name>usuario-do-mysql</user-name>
                        <password>senha-do-mysql</password>
                    </security>
                    <statement>
                        <prepared-statement-cache-size>32</prepared-statement-cache-size>
                        <share-prepared-statements>true</share-prepared-statements>
                    </statement>
                </datasource>
                <drivers>
                    <driver name="h2" module="com.h2database.h2">
                        <xa-datasource-class>org.h2.jdbcx.JdbcDataSource</xa-datasource-class>
                    </driver>
                    <driver name="com.mysql" module="com.mysql">
                        <xa-datasource-class>com.mysql.jdbc.jdbc2.optional.MysqlXADataSource</xa-datasource-class>
                    </driver>
                </drivers>
            </datasources>
        </subsystem>
