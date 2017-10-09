---
title: aaaConnect tooAzure SQL Data Warehouse sqlcmd | Documents Microsoft
description: "Utilisez [sqlcmd] [sqlcmd] utilitaire de ligne de commande tooconnect tooand requête un entrepôt de données SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 6e2b69e5-4806-4e91-9ea1-e2b63bf28c46
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 0334df7b969da1966ba29c97f835a2dc9e383e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sqlcmd"></a>Se connecter tooSQL l’entrepôt de données avec sqlcmd
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Utilisez [sqlcmd] [ sqlcmd] tooand de tooconnect d’utilitaire de ligne de commande de requête un entrepôt de données SQL Azure.  

## <a name="1-connect"></a>1. Connecter
tooget main [sqlcmd][sqlcmd], ouvrez l’invite de commandes hello et entrez **sqlcmd** suivi d’une chaîne de connexion hello pour votre base de données SQL Data Warehouse. chaîne de connexion Hello nécessite hello paramètres suivants :

* **Serveur (-S) :** serveur sous forme de hello `<`nom du serveur`>`. database.windows.net
* **Base de données (-d) :** nom de la base de données.
* **Activer les identificateurs entre guillemets (-I) :** identificateurs entre guillemets doivent être l’instance de SQL Data Warehouse tooa tooconnect activé.

toouse l’authentification SQL Server, vous devez disposer de paramètres de nom d’utilisateur/mot de passe tooadd hello :

* **Utilisateur (-U) :** utilisateur du serveur sous forme de hello `<`utilisateur`>`
* **Mot de passe (-P) :** mot de passe associé à utilisateur de hello.

Par exemple, votre chaîne de connexion peut se présenter comme hello suivantes :

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

toouse de l’authentification intégrée à Active Directory de Azure, vous devez disposer de paramètres d’Azure Active Directory tooadd hello :

* **Authentification Azure Active Directory (-G) :** utilisez Azure Active Directory pour l’authentification

Par exemple, votre chaîne de connexion peut se présenter comme hello suivantes :

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> Vous devez trop[activer l’authentification Azure Active Directory](sql-data-warehouse-authentication.md) tooauthenticate à l’aide d’Active Directory.
> 
> 

## <a name="2-query"></a>2. Interroger
Une fois la connexion, vous pouvez émettre les instructions Transact-SQL prises en charge par rapport à l’instance de hello.  Dans cet exemple, les requêtes sont soumises en mode interactif.

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

Les exemples suivants indiquent comment vous pouvez exécuter vos requêtes en mode de traitement par lots à l’aide hello Q - option ou en transférant votre toosqlcmd SQL.

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a>Étapes suivantes
Consultez [documentation sqlcmd] [ sqlcmd] pour plus d’informations sur les détails sur les options de hello disponibles dans sqlcmd.

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->