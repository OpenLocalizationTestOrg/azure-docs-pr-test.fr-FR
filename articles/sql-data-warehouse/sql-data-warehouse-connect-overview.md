---
title: aaaConnect tooAzure SQL Data Warehouse | Documents Microsoft
description: "Comment chaîne de connexion et le nom du serveur toofind hello pour votre tooAzure SQL Data Warehouse"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: e52872ca-ae74-4e25-9c56-d49c85c8d0f0
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: f15e098026afb7c5efbbbfaf62b681e8cd7936bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-sql-data-warehouse"></a>Se connecter tooAzure SQL Data Warehouse
Cet article vous aidera à obtenir tooSQL connecté l’entrepôt de données pour hello première fois.

## <a name="find-your-server-name"></a>Recherche du nom de serveur
Hello tooSQL de tooconnecting première étape l’entrepôt de données est de savoir comment toofind votre nom de serveur.  Par exemple, le nom du serveur hello Bonjour l’exemple suivant est sample.database.windows.net. nom de serveur complet toofind hello :

1. Accédez toohello [portail Azure][Azure portal].
2. Cliquez sur **Bases de données SQL** 
3. Cliquez sur hello base de données tooconnect à.
4. Recherchez le nom de serveur complet hello.
   
    ![Nom complet du serveur][1]

## <a name="supported-drivers-and-connection-strings"></a>Chaînes de connexion et pilotes pris en charge
Azure SQL Data Warehouse prend en charge [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP] et [JDBC][JDBC]. Cliquez sur un des hello précédant la dernière version des pilotes toofind hello et la documentation. tooautomatically générer la chaîne de connexion de hello pour que vous utilisez le pilote hello de hello Azure portail, vous pouvez cliquer sur hello **afficher les chaînes de connexion de base de données** de hello précédent exemple.  Voici également quelques exemples montrant à quoi ressemble une chaîne de connexion pour chaque pilote.

> [!NOTE]
> Envisagez de définir hello connexion délai d’attente too300 secondes tooallow votre toosurvive connexion courtes périodes d’indisponibilité.
> 
> 

### <a name="adonet-connection-string-example"></a>Exemple de chaîne de connexion ADO.NET
```C#
Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};User ID={your_user_name};Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

### <a name="odbc-connection-string-example"></a>Exemple de chaîne de connexion ODBC
```C#
Driver={SQL Server Native Client 11.0};Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};Uid={your_user_name};Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
```

### <a name="php-connection-string-example"></a>Exemple de chaîne de connexion PHP
```PHP
Server: {your_server}.database.windows.net,1433 \r\nSQL Database: {your_database}\r\nUser Name: {your_user_name}\r\n\r\nPHP Data Objects(PDO) Sample Code:\r\n\r\ntry {\r\n   $conn = new PDO ( \"sqlsrv:server = tcp:{your_server}.database.windows.net,1433; Database = {your_database}\", \"{your_user_name}\", \"{your_password_here}\");\r\n    $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );\r\n}\r\ncatch ( PDOException $e ) {\r\n   print( \"Error connecting tooSQL Server.\" );\r\n   die(print_r($e));\r\n}\r\n\rSQL Server Extension Sample Code:\r\n\r\n$connectionInfo = array(\"UID\" => \"{your_user_name}\", \"pwd\" => \"{your_password_here}\", \"Database\" => \"{your_database}\", \"LoginTimeout\" => 30, \"Encrypt\" => 1, \"TrustServerCertificate\" => 0);\r\n$serverName = \"tcp:{your_server}.database.windows.net,1433\";\r\n$conn = sqlsrv_connect($serverName, $connectionInfo);
```

### <a name="jdbc-connection-string-example"></a>Exemple de chaîne de connexion JDBC
```Java
jdbc:sqlserver://yourserver.database.windows.net:1433;database=yourdatabase;user={your_user_name};password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

## <a name="connection-settings"></a>Paramètres de connexion
SQL Data Warehouse standardise certains paramètres pendant la connexion et la création d’objets. Ces paramètres, qui ne peuvent pas être remplacés, comprennent notamment :

| Paramètre de base de données | Valeur |
|:--- |:--- |
| [ANSI_NULLS][ANSI_NULLS] |ACTIVÉ |
| [QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS] |ACTIVÉ |
| [DATEFORMAT][DATEFORMAT] |mdy |
| [DATEFIRST][DATEFIRST] |7 |

## <a name="next-steps"></a>Étapes suivantes
tooconnect et requête avec Visual Studio, consultez [requête avec Visual Studio][Query with Visual Studio]. toolearn savoir plus sur les options d’authentification, consultez [tooAzure de l’authentification SQL Data Warehouse][Authentication tooAzure SQL Data Warehouse].

<!--Articles-->
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[Authentication tooAzure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[ADO.NET]: https://msdn.microsoft.com/library/e80y5yhx(v=vs.110).aspx
[ODBC]: https://msdn.microsoft.com/library/jj730314.aspx
[PHP]: https://msdn.microsoft.com/library/cc296172.aspx?f=255&MSPPError=-2147217396
[JDBC]: https://msdn.microsoft.com/library/mt484311(v=sql.110).aspx
[ANSI_NULLS]: https://msdn.microsoft.com/library/ms188048.aspx
[QUOTED_IDENTIFIERS]: https://msdn.microsoft.com/library/ms174393.aspx
[DATEFORMAT]: https://msdn.microsoft.com/library/ms189491.aspx
[DATEFIRST]: https://msdn.microsoft.com/library/ms181598.aspx

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->
[1]: media/sql-data-warehouse-connect-overview/get-server-name.png


