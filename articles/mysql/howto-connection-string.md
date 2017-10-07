---
title: "applications d’aaaConnect tooAzure base de données MySQL | Documents Microsoft"
description: "Ce document répertorie les chaînes de connexion hello actuellement pris en charge pour les applications tooconnect avec la base de données Azure pour MySQL, y compris ADO.NET (c#), JDBC, Node.js, ODBC, PHP, Python et Ruby."
services: mysql
author: mswutao
ms.author: wuta
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 06/12/2017
ms.openlocfilehash: bbcb2c0ddb4f8e5c225ebef53781e073f5c7b1a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-applications-tooazure-database-for-mysql"></a>Comment tooconnect applications tooAzure de base de données MySQL
Ce document répertorie les types de chaîne de connexion de hello sont pris en charge par la base de données Azure pour MySQL, ainsi que des modèles et des exemples. Vous pouvez avoir des paramètres et des réglages différents dans votre chaîne de connexion.

- certificat de hello tooobtain, consultez [comment tooconfigure SSL](./howto-configure-ssl.md).
- {votre_hôte} = <servername>.mysql.database.azure.com
- {votre_utilisateur}@{nomserveur} = format ID utilisateur pour une authentification correcte.  L’utilisation de simplement hello userID entraîne hello authentification toofail.

## <a name="adonet"></a>ADO.NET
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

Dans cet exemple, le nom du serveur hello est `myserver4demo`, nom de la base de données est `wpdb`, nom d’utilisateur est `WPAdmin`, et le mot de passe est `mypassword!2`. Ensuite, la chaîne de connexion hello doit être :

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a>JDBC
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a>Node.js
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a>ODBC
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a>PHP
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a>Python
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a>Ruby
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-hello-connection-string-details-from-hello-azure-portal"></a>Obtenir des détails de la chaîne de connexion de hello de hello portail Azure
Bonjour [portail Azure](https://portal.azure.com), accédez tooyour base de données Azure pour le serveur MySQL, puis cliquez sur **les chaînes de connexion** tooget votre chaîne de liste de l’instance : ![volet de chaînes de connexion hello Bonjour Portail Azure](./media/howto-connection-strings/connection-strings-on-portal.png)

chaîne de Hello fournit des détails tels que les pilotes de hello, serveur et autres paramètres de connexion de base de données. Modifiez ces exemples en utilisant vos propres paramètres, tels que le nom de la base de données, le mot de passe, etc. Vous pouvez ensuite utiliser ce serveur de toohello tooconnect chaîne à partir de votre code et les applications.

## <a name="next-steps"></a>Étapes suivantes
- Pour plus d’informations sur les bibliothèques de connexions, consultez [Concepts - Bibliothèques de connexions](./concepts-connection-libraries.md).
