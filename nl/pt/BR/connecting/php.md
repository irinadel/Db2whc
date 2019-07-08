---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

keywords:

subcollection: Db2whc

---

<!-- Attribute definitions --> 
{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}

# Conectando programaticamente com o PHP
{: #con_prog_php}

Defina uma conexão entre um aplicativo PHP e um banco de dados {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

## Pré-requisitos
{: #prereq101}

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) necessários.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedimento
{: #proc101}

### Cenário 1: Conectando-se de fora  {{site.data.keyword.Bluemix_notm}}:
{: #scen1}

1. Faça download do [pacote de drivers do Db2](/docs/services/Db2whc?topic=Db2whc-dr_pkg#dr_pkg) por meio do console da web e, em seguida, instale o pacote de drivers na máquina em que seu aplicativo PHP será executado.
                
2. Use a função [`odbc_connect`](http://php.net/manual/en/function.odbc-connect.php){:external} para conexão com o banco de dados BLUDB.
    
   Exemplo de código PHP:

   ```
   <?php
   $database = "BLUDB";        # Get these database details from
   $hostname = "<Host-name>";  # the web console
   $user     = "<User-ID >";   #
   $password = "<Password>";   #
   $port     = 50000;          #
   $ssl_port = 50001;          #
   # Build the connection string
   #
   $driver  = "DRIVER={IBM DB2 ODBC DRIVER};";
   $dsn     = "DATABASE=$database; " .
              "HOSTNAME=$hostname;" .
              "PORT=$port;" .
              "PROTOCOL=TCPIP;" .
              "UID=$user;" .
              "PWD=$password;";
   $ssl_dsn = "DATABASE=$database; " .
              "HOSTNAME=$hostname;" .
              "PORT = $ssl_port;".
              "PROTOCOL=TCPIP;" .
              "UID=$user;" .
              "PWD = $password;".
              "SECURITY=SSL;";
   $conn_string = $driver . $dsn;     # Non-SSL
   $conn_string = $driver . $ssl_dsn; # SSL
   # Connect
   #
   $conn = odbc_connect( $conn_string, "", "" );
   if( $conn )
   {
       echo "Conexão bem-sucedida.";
       # Disconnect
       #
       odbc_close( $conn );
   }
   else
   {
       echo "Connection failed.";
   }
   ?>
   ```

   O salvamento desse exemplo de código PHP em um arquivo de script chamado `C:\sample.php` e, em seguida, a execução do script por meio de uma linha de comandos produzem a saída a seguir:

   ```
   C:\> php -f sample.php

   Conexão bem-sucedida.
   ```

### Cenário 2: Conectando-se por meio de um app da web PHP no {{site.data.keyword.Bluemix_notm}}
{: #scen2}

1. No catálogo do {{site.data.keyword.Bluemix_notm}}, crie um novo App PHP.
        
2. Na seção "Introdução" do novo App PHP no painel do {{site.data.keyword.Bluemix_notm}}, faça download do código de início do App no diretório de trabalho local.
        
3. No painel do {{site.data.keyword.Bluemix_notm}}, crie uma nova conexão do serviço do Db2 com o novo App PHP. (A criação dessa Conexão no {{site.data.keyword.Bluemix_notm}} disponibiliza a variável de ambiente `VCAP_SERVICES` para seu App PHP. A variável de ambiente `VCAP_SERVICES` contém detalhes do banco de dados para o serviço do Db2. O uso de `VCAP_SERVICES` é mais conveniente do que codificar permanentemente os detalhes do banco de dados no App PHP.)
        
4. Em seu diretório ativo local, atualize o arquivo `index.php` para conexão com o banco de dados BLUDB usando a função [`db2_connect`](http://php.net/manual/en/function.db2-connect.php){:external}.
        
   Exemplo:

   ```
   <!DOCTYPE html>
   <html>
   <head>
       <title>Aplicativo Iniciador PHP</title>
       <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
       <link rel="stylesheet" href="style.css" />
   </head>
   <body>
   <?php
   if( getenv( "VCAP_SERVICES" ) )
   {
       # Get database details from the VCAP_SERVICES environment variable
       #
       # *This can only work if you have used the Bluemix dashboard to 
       # create a connection from your dashDB service to your PHP App.
       #
       $details  = json_decode( getenv( "VCAP_SERVICES" ), true );
       $dsn      = $details [ "dashDB" ][0][ "credentials" ][ "dsn" ];
       $ssl_dsn  = $details [ "dashDB" ][0][ "credentials" ][ "ssldsn" ];
       # Build the connection string
       #
       $driver = "DRIVER={IBM DB2 ODBC DRIVER};";
       $conn_string = $driver . $dsn;     # Non-SSL
       $conn_string = $driver . $ssl_dsn; # SSL
       $conn = db2_connect( $conn_string, "", "" );
       if( $conn )
       {
           eco "<p>Conexão bem-sucedida.</p>";
           db2_close( $conn );
       }
       else
       {
           eco "<p>A conexão falhou.</p>";
       }
   } else {
       eco "<p>Nenhuma credencial.</p>";
   }
   ?>
   </body>
   </html>
   ```

5. No diretório ativo local, envie por push as atualizações para o {{site.data.keyword.Bluemix_notm}} seguindo as instruções na seção "Introdução" do App PHP no painel do {{site.data.keyword.Bluemix_notm}}. Em seguida, reinicie o App no {{site.data.keyword.Bluemix_notm}} e visualize-o em um navegador.


