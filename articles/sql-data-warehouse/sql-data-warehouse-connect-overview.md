---
title: "Se connecter à Azure SQL Data Warehouse | Microsoft Docs"
description: "Comment trouver le nom de serveur et la chaîne de connexion pour Azure SQL Data Warehouse"
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
ms.openlocfilehash: 72c2b404e66611da421eca0dc30aa71e18c6d120
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-azure-sql-data-warehouse"></a><span data-ttu-id="5ef66-103">Se connecter à Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5ef66-103">Connect to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="5ef66-104">Cet article vous aidera à établir votre première connexion à SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5ef66-104">This article helps you get connected to SQL Data Warehouse for the first time.</span></span>

## <a name="find-your-server-name"></a><span data-ttu-id="5ef66-105">Recherche du nom de serveur</span><span class="sxs-lookup"><span data-stu-id="5ef66-105">Find your server name</span></span>
<span data-ttu-id="5ef66-106">La première étape de connexion à SQL Data Warehouse consiste à déterminer le nom de votre serveur.</span><span class="sxs-lookup"><span data-stu-id="5ef66-106">The first step to connecting to SQL Data Warehouse is knowing how to find your server name.</span></span>  <span data-ttu-id="5ef66-107">Dans l’exemple suivant, le nom du serveur est sample.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="5ef66-107">For example, the server name in the following example is sample.database.windows.net.</span></span> <span data-ttu-id="5ef66-108">Pour rechercher le nom complet du serveur :</span><span class="sxs-lookup"><span data-stu-id="5ef66-108">To find the fully qualified server name:</span></span>

1. <span data-ttu-id="5ef66-109">Accédez au [portail Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="5ef66-109">Go to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="5ef66-110">Cliquez sur **Bases de données SQL**</span><span class="sxs-lookup"><span data-stu-id="5ef66-110">Click on **SQL databases**</span></span> 
3. <span data-ttu-id="5ef66-111">Cliquez sur la base de données à laquelle vous souhaitez vous connecter.</span><span class="sxs-lookup"><span data-stu-id="5ef66-111">Click on the database you want to connect to.</span></span>
4. <span data-ttu-id="5ef66-112">Recherchez le nom complet du serveur.</span><span class="sxs-lookup"><span data-stu-id="5ef66-112">Locate the full server name.</span></span>
   
    ![Nom complet du serveur][1]

## <a name="supported-drivers-and-connection-strings"></a><span data-ttu-id="5ef66-114">Chaînes de connexion et pilotes pris en charge</span><span class="sxs-lookup"><span data-stu-id="5ef66-114">Supported drivers and connection strings</span></span>
<span data-ttu-id="5ef66-115">Azure SQL Data Warehouse prend en charge [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP] et [JDBC][JDBC].</span><span class="sxs-lookup"><span data-stu-id="5ef66-115">Azure SQL Data Warehouse supports [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP], and [JDBC][JDBC].</span></span> <span data-ttu-id="5ef66-116">Cliquez sur l’un des pilotes ci-dessus pour rechercher la dernière version et accéder à la documentation connexe.</span><span class="sxs-lookup"><span data-stu-id="5ef66-116">Click on one of the preceding drivers to find the latest version and documentation.</span></span> <span data-ttu-id="5ef66-117">Pour générer automatiquement la chaîne de connexion pour le pilote que vous utilisez à partir du portail Azure, vous pouvez cliquer sur l’option **Afficher les chaînes de connexion de la base de données** dans l’exemple précédent.</span><span class="sxs-lookup"><span data-stu-id="5ef66-117">To automatically generate the connection string for the driver that you are using from the Azure portal, you can click on the **Show database connection strings** from the preceding example.</span></span>  <span data-ttu-id="5ef66-118">Voici également quelques exemples montrant à quoi ressemble une chaîne de connexion pour chaque pilote.</span><span class="sxs-lookup"><span data-stu-id="5ef66-118">Following are also some examples of what a connection string looks like for each driver.</span></span>

> [!NOTE]
> <span data-ttu-id="5ef66-119">Vous pouvez définir le délai de connexion à 300 secondes pour permettre à votre connexion de résister à des courtes périodes d’indisponibilité.</span><span class="sxs-lookup"><span data-stu-id="5ef66-119">Consider setting the connection timeout to 300 seconds to allow your connection to survive short periods of unavailability.</span></span>
> 
> 

### <a name="adonet-connection-string-example"></a><span data-ttu-id="5ef66-120">Exemple de chaîne de connexion ADO.NET</span><span class="sxs-lookup"><span data-stu-id="5ef66-120">ADO.NET connection string example</span></span>
```C#
Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};User ID={your_user_name};Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

### <a name="odbc-connection-string-example"></a><span data-ttu-id="5ef66-121">Exemple de chaîne de connexion ODBC</span><span class="sxs-lookup"><span data-stu-id="5ef66-121">ODBC connection string example</span></span>
```C#
Driver={SQL Server Native Client 11.0};Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};Uid={your_user_name};Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
```

### <a name="php-connection-string-example"></a><span data-ttu-id="5ef66-122">Exemple de chaîne de connexion PHP</span><span class="sxs-lookup"><span data-stu-id="5ef66-122">PHP connection string example</span></span>
```PHP
Server: {your_server}.database.windows.net,1433 \r\nSQL Database: {your_database}\r\nUser Name: {your_user_name}\r\n\r\nPHP Data Objects(PDO) Sample Code:\r\n\r\ntry {\r\n   $conn = new PDO ( \"sqlsrv:server = tcp:{your_server}.database.windows.net,1433; Database = {your_database}\", \"{your_user_name}\", \"{your_password_here}\");\r\n    $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );\r\n}\r\ncatch ( PDOException $e ) {\r\n   print( \"Error connecting to SQL Server.\" );\r\n   die(print_r($e));\r\n}\r\n\rSQL Server Extension Sample Code:\r\n\r\n$connectionInfo = array(\"UID\" => \"{your_user_name}\", \"pwd\" => \"{your_password_here}\", \"Database\" => \"{your_database}\", \"LoginTimeout\" => 30, \"Encrypt\" => 1, \"TrustServerCertificate\" => 0);\r\n$serverName = \"tcp:{your_server}.database.windows.net,1433\";\r\n$conn = sqlsrv_connect($serverName, $connectionInfo);
```

### <a name="jdbc-connection-string-example"></a><span data-ttu-id="5ef66-123">Exemple de chaîne de connexion JDBC</span><span class="sxs-lookup"><span data-stu-id="5ef66-123">JDBC connection string example</span></span>
```Java
jdbc:sqlserver://yourserver.database.windows.net:1433;database=yourdatabase;user={your_user_name};password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

## <a name="connection-settings"></a><span data-ttu-id="5ef66-124">Paramètres de connexion</span><span class="sxs-lookup"><span data-stu-id="5ef66-124">Connection settings</span></span>
<span data-ttu-id="5ef66-125">SQL Data Warehouse standardise certains paramètres pendant la connexion et la création d’objets.</span><span class="sxs-lookup"><span data-stu-id="5ef66-125">SQL Data Warehouse standardizes some settings during connection and object creation.</span></span> <span data-ttu-id="5ef66-126">Ces paramètres, qui ne peuvent pas être remplacés, comprennent notamment :</span><span class="sxs-lookup"><span data-stu-id="5ef66-126">These settings cannot be overridden and include:</span></span>

| <span data-ttu-id="5ef66-127">Paramètre de base de données</span><span class="sxs-lookup"><span data-stu-id="5ef66-127">Database Setting</span></span> | <span data-ttu-id="5ef66-128">Valeur</span><span class="sxs-lookup"><span data-stu-id="5ef66-128">Value</span></span> |
|:--- |:--- |
| <span data-ttu-id="5ef66-129">[ANSI_NULLS][ANSI_NULLS]</span><span class="sxs-lookup"><span data-stu-id="5ef66-129">[ANSI_NULLS][ANSI_NULLS]</span></span> |<span data-ttu-id="5ef66-130">ACTIVÉ</span><span class="sxs-lookup"><span data-stu-id="5ef66-130">ON</span></span> |
| <span data-ttu-id="5ef66-131">[QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS]</span><span class="sxs-lookup"><span data-stu-id="5ef66-131">[QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS]</span></span> |<span data-ttu-id="5ef66-132">ACTIVÉ</span><span class="sxs-lookup"><span data-stu-id="5ef66-132">ON</span></span> |
| <span data-ttu-id="5ef66-133">[DATEFORMAT][DATEFORMAT]</span><span class="sxs-lookup"><span data-stu-id="5ef66-133">[DATEFORMAT][DATEFORMAT]</span></span> |<span data-ttu-id="5ef66-134">mdy</span><span class="sxs-lookup"><span data-stu-id="5ef66-134">mdy</span></span> |
| <span data-ttu-id="5ef66-135">[DATEFIRST][DATEFIRST]</span><span class="sxs-lookup"><span data-stu-id="5ef66-135">[DATEFIRST][DATEFIRST]</span></span> |<span data-ttu-id="5ef66-136">7</span><span class="sxs-lookup"><span data-stu-id="5ef66-136">7</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5ef66-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5ef66-137">Next steps</span></span>
<span data-ttu-id="5ef66-138">Pour vous connecter à Visual Studio et l’utiliser pour lancer des requêtes, consultez la page [Envoyer des requêtes avec Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="5ef66-138">To connect and query with Visual Studio, see [Query with Visual Studio][Query with Visual Studio].</span></span> <span data-ttu-id="5ef66-139">Pour en savoir plus sur les options d’authentification, consultez la page [Authentification sur Azure SQL Data Warehouse][Authentication to Azure SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="5ef66-139">To learn more about authentication options, see [Authentication to Azure SQL Data Warehouse][Authentication to Azure SQL Data Warehouse].</span></span>

<!--Articles-->
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[Authentication to Azure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md

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


