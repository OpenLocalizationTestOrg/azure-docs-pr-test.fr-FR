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
# <a name="connect-toosql-data-warehouse-with-sqlcmd"></a><span data-ttu-id="95428-103">Se connecter tooSQL l’entrepôt de données avec sqlcmd</span><span class="sxs-lookup"><span data-stu-id="95428-103">Connect tooSQL Data Warehouse with sqlcmd</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="95428-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="95428-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="95428-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="95428-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="95428-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="95428-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="95428-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="95428-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="95428-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="95428-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="95428-109">Utilisez [sqlcmd] [ sqlcmd] tooand de tooconnect d’utilitaire de ligne de commande de requête un entrepôt de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="95428-109">Use [sqlcmd][sqlcmd] command-line utility tooconnect tooand query an Azure SQL Data Warehouse.</span></span>  

## <a name="1-connect"></a><span data-ttu-id="95428-110">1. Connecter</span><span class="sxs-lookup"><span data-stu-id="95428-110">1. Connect</span></span>
<span data-ttu-id="95428-111">tooget main [sqlcmd][sqlcmd], ouvrez l’invite de commandes hello et entrez **sqlcmd** suivi d’une chaîne de connexion hello pour votre base de données SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="95428-111">tooget started with [sqlcmd][sqlcmd], open hello command prompt and enter **sqlcmd** followed by hello connection string for your SQL Data Warehouse database.</span></span> <span data-ttu-id="95428-112">chaîne de connexion Hello nécessite hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="95428-112">hello connection string requires hello following parameters:</span></span>

* <span data-ttu-id="95428-113">**Serveur (-S) :** serveur sous forme de hello `<`nom du serveur`>`. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="95428-113">**Server (-S):** Server in hello form `<`Server Name`>`.database.windows.net</span></span>
* <span data-ttu-id="95428-114">**Base de données (-d) :** nom de la base de données.</span><span class="sxs-lookup"><span data-stu-id="95428-114">**Database (-d):** Database name.</span></span>
* <span data-ttu-id="95428-115">**Activer les identificateurs entre guillemets (-I) :** identificateurs entre guillemets doivent être l’instance de SQL Data Warehouse tooa tooconnect activé.</span><span class="sxs-lookup"><span data-stu-id="95428-115">**Enable Quoted Identifiers (-I):** Quoted identifiers must be enabled tooconnect tooa SQL Data Warehouse instance.</span></span>

<span data-ttu-id="95428-116">toouse l’authentification SQL Server, vous devez disposer de paramètres de nom d’utilisateur/mot de passe tooadd hello :</span><span class="sxs-lookup"><span data-stu-id="95428-116">toouse SQL Server Authentication, you need tooadd hello username/password parameters:</span></span>

* <span data-ttu-id="95428-117">**Utilisateur (-U) :** utilisateur du serveur sous forme de hello `<`utilisateur`>`</span><span class="sxs-lookup"><span data-stu-id="95428-117">**User (-U):** Server user in hello form `<`User`>`</span></span>
* <span data-ttu-id="95428-118">**Mot de passe (-P) :** mot de passe associé à utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="95428-118">**Password (-P):** Password associated with hello user.</span></span>

<span data-ttu-id="95428-119">Par exemple, votre chaîne de connexion peut se présenter comme hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="95428-119">For example, your connection string might look like hello following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

<span data-ttu-id="95428-120">toouse de l’authentification intégrée à Active Directory de Azure, vous devez disposer de paramètres d’Azure Active Directory tooadd hello :</span><span class="sxs-lookup"><span data-stu-id="95428-120">toouse Azure Active Directory Integrated authentication, you need tooadd hello Azure Active Directory parameters:</span></span>

* <span data-ttu-id="95428-121">**Authentification Azure Active Directory (-G) :** utilisez Azure Active Directory pour l’authentification</span><span class="sxs-lookup"><span data-stu-id="95428-121">**Azure Active Directory Authentication (-G):** use Azure Active Directory for authentication</span></span>

<span data-ttu-id="95428-122">Par exemple, votre chaîne de connexion peut se présenter comme hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="95428-122">For example, your connection string might look like hello following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> <span data-ttu-id="95428-123">Vous devez trop[activer l’authentification Azure Active Directory](sql-data-warehouse-authentication.md) tooauthenticate à l’aide d’Active Directory.</span><span class="sxs-lookup"><span data-stu-id="95428-123">You need too[enable Azure Active Directory Authentication](sql-data-warehouse-authentication.md) tooauthenticate using Active Directory.</span></span>
> 
> 

## <a name="2-query"></a><span data-ttu-id="95428-124">2. Interroger</span><span class="sxs-lookup"><span data-stu-id="95428-124">2. Query</span></span>
<span data-ttu-id="95428-125">Une fois la connexion, vous pouvez émettre les instructions Transact-SQL prises en charge par rapport à l’instance de hello.</span><span class="sxs-lookup"><span data-stu-id="95428-125">After connection, you can issue any supported Transact-SQL statements against hello instance.</span></span>  <span data-ttu-id="95428-126">Dans cet exemple, les requêtes sont soumises en mode interactif.</span><span class="sxs-lookup"><span data-stu-id="95428-126">In this example, queries are submitted in interactive mode.</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

<span data-ttu-id="95428-127">Les exemples suivants indiquent comment vous pouvez exécuter vos requêtes en mode de traitement par lots à l’aide hello Q - option ou en transférant votre toosqlcmd SQL.</span><span class="sxs-lookup"><span data-stu-id="95428-127">These next examples show how you can run your queries in batch mode using hello -Q option or piping your SQL toosqlcmd.</span></span>

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a><span data-ttu-id="95428-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="95428-128">Next steps</span></span>
<span data-ttu-id="95428-129">Consultez [documentation sqlcmd] [ sqlcmd] pour plus d’informations sur les détails sur les options de hello disponibles dans sqlcmd.</span><span class="sxs-lookup"><span data-stu-id="95428-129">See [sqlcmd documentation][sqlcmd] for more about details about hello options available in sqlcmd.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
