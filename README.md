# Configuração do drive MySQL no Jboss 7

Configuração para adicionar o drive do Mysql no Jboss7,

!) Adicionar dentro do diretório (diretório-jboss-7/modules/com/mysql/main) do Jboss 7 o diretório mysql que está no repositório.

2) Abra o arquivo standalone.xml que está em diretório-jboss-7/standalone/configuration/ e dentro da tag <datasources> adicione as seguintes configurações:

