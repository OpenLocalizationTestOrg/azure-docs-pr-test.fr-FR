---
title: "aaaMigrate un à l’aide de la base de données d’importation et d’exportation dans la base de données Azure pour PostgreSQL | Documents Microsoft"
description: "Décrit comment extraire une base de données PostgreSQL dans un fichier de script et importer des données de hello dans base de données cible hello à partir de ce fichier."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 5ca4650782b02e1067c5a8a3710f2dfbc8c76063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-postgresql-database-using-export-and-import"></a><span data-ttu-id="563de-103">Migration de votre base de données PostgreSQL par exportation et importation</span><span class="sxs-lookup"><span data-stu-id="563de-103">Migrate your PostgreSQL database using export and import</span></span>
<span data-ttu-id="563de-104">Vous pouvez utiliser [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract une base de données PostgreSQL dans un fichier de script et [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport les données de salutation dans la base de données cible hello à partir de ce fichier.</span><span class="sxs-lookup"><span data-stu-id="563de-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract a PostgreSQL database into a script file and [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport hello data into hello target database from that file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="563de-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="563de-105">Prerequisites</span></span>
<span data-ttu-id="563de-106">toostep via ce tooguide de procédure, vous devez :</span><span class="sxs-lookup"><span data-stu-id="563de-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="563de-107">Un [Azure de base de données PostgreSQL serveur](quickstart-create-server-database-portal.md) avec tooallow accès aux règles de pare-feu et de la base de données dans cette section.</span><span class="sxs-lookup"><span data-stu-id="563de-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules tooallow access and database under it.</span></span>
- <span data-ttu-id="563de-108">Utilitaire de ligne de commande [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) installé</span><span class="sxs-lookup"><span data-stu-id="563de-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) command-line utility installed</span></span>
- <span data-ttu-id="563de-109">Utilitaire de ligne de commande [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) installé</span><span class="sxs-lookup"><span data-stu-id="563de-109">[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) command-line utility installed</span></span>

<span data-ttu-id="563de-110">Suivez ces étapes tooexport et importer votre base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="563de-110">Follow these steps tooexport and import your PostgreSQL database.</span></span>

## <a name="create-a-script-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a><span data-ttu-id="563de-111">Créer un fichier de script à l’aide de pg_dump contenant hello toobe de données chargé</span><span class="sxs-lookup"><span data-stu-id="563de-111">Create a script file using pg_dump that contains hello data toobe loaded</span></span>
<span data-ttu-id="563de-112">tooexport votre PostgreSQL existant de la base de données locale ou dans un fichier de script sql de machine virtuelle tooa, exécutez hello suivant de commande dans votre environnement existant :</span><span class="sxs-lookup"><span data-stu-id="563de-112">tooexport your existing PostgreSQL database on-premises or in a VM tooa sql script file, run hello following command in your existing environment:</span></span>
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
<span data-ttu-id="563de-113">Par exemple, si vous avez un serveur local contenant une base de données appelée **testdb**</span><span class="sxs-lookup"><span data-stu-id="563de-113">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-hello-data-on-target-azure-database-for-postrgesql"></a><span data-ttu-id="563de-114">Importer des données sur la cible de la base de données Azure pour PostrgeSQL hello</span><span class="sxs-lookup"><span data-stu-id="563de-114">Import hello data on target Azure Database for PostrgeSQL</span></span>
<span data-ttu-id="563de-115">Vous pouvez utiliser la ligne de commande psql hello et hello -d, données de hello--dbname paramètre tooimport dans la base de données Azure pour PostrgeSQL, nous avons créé et charger des données à partir du fichier sql de hello.</span><span class="sxs-lookup"><span data-stu-id="563de-115">You can use hello psql command line and hello -d, --dbname parameter tooimport hello data into Azure Database for PostrgeSQL we created and load data from hello sql file.</span></span>
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
<span data-ttu-id="563de-116">Cet exemple utilise psql utilitaire et un fichier de script nommé **testdb.sql** à partir des données de tooimport étape précédente dans la base de données hello **mypgsqldb** sur le serveur cible  **mypgserver-20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="563de-116">This example uses psql utility and a script file named **testdb.sql** from previous step tooimport data into hello database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a><span data-ttu-id="563de-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="563de-117">Next steps</span></span>
- <span data-ttu-id="563de-118">une base de données PostgreSQL à l’aide de vidage et la restauration, reportez-vous à toomigrate [migrer votre base de données PostgreSQL à l’aide de vidage et restauration](howto-migrate-using-dump-and-restore.md)</span><span class="sxs-lookup"><span data-stu-id="563de-118">toomigrate a PostgreSQL database using dump and restore, see [Migrate your PostgreSQL database using dump and restore](howto-migrate-using-dump-and-restore.md)</span></span>
