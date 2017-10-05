---
title: "Migration d’une base de données par importation et exportation dans Azure Database pour PostgreSQL | Microsoft Docs"
description: "Décrit comment extraire une base de données PostgreSQL dans un fichier de script et importer les données dans la base de données cible à partir de ce fichier."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 5e306d516d04789e4526bfd09bf99139b83573ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="migrate-your-postgresql-database-using-export-and-import"></a><span data-ttu-id="c1675-103">Migration de votre base de données PostgreSQL par exportation et importation</span><span class="sxs-lookup"><span data-stu-id="c1675-103">Migrate your PostgreSQL database using export and import</span></span>
<span data-ttu-id="c1675-104">Vous pouvez utiliser [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) pour extraire une base de données PostgreSQL dans un fichier de script et [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) pour importer les données dans la base de données cible à partir de ce fichier.</span><span class="sxs-lookup"><span data-stu-id="c1675-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) to extract a PostgreSQL database into a script file and [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) to import the data into the target database from that file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1675-105">Prérequis</span><span class="sxs-lookup"><span data-stu-id="c1675-105">Prerequisites</span></span>
<span data-ttu-id="c1675-106">Pour parcourir ce guide pratique, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c1675-106">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="c1675-107">Un [serveur Azure Database pour PostgreSQL](quickstart-create-server-database-portal.md) avec des règles de pare-feu autorisant l’accès et la base de données sous-jacente.</span><span class="sxs-lookup"><span data-stu-id="c1675-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules to allow access and database under it.</span></span>
- <span data-ttu-id="c1675-108">Utilitaire de ligne de commande [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) installé</span><span class="sxs-lookup"><span data-stu-id="c1675-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) command-line utility installed</span></span>
- <span data-ttu-id="c1675-109">Utilitaire de ligne de commande [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) installé</span><span class="sxs-lookup"><span data-stu-id="c1675-109">[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) command-line utility installed</span></span>

<span data-ttu-id="c1675-110">Suivez ces étapes pour exporter et importer votre base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="c1675-110">Follow these steps to export and import your PostgreSQL database.</span></span>

## <a name="create-a-script-file-using-pgdump-that-contains-the-data-to-be-loaded"></a><span data-ttu-id="c1675-111">Création d’un fichier de script à l’aide de pg_dump qui contient les données à charger</span><span class="sxs-lookup"><span data-stu-id="c1675-111">Create a script file using pg_dump that contains the data to be loaded</span></span>
<span data-ttu-id="c1675-112">Pour exporter votre base de données PostgreSQL existante en local ou dans une machine virtuelle vers un fichier de script sql, exécutez la commande suivante dans votre environnement existant :</span><span class="sxs-lookup"><span data-stu-id="c1675-112">To export your existing PostgreSQL database on-premises or in a VM to a sql script file, run the following command in your existing environment:</span></span>
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
<span data-ttu-id="c1675-113">Par exemple, si vous avez un serveur local contenant une base de données appelée **testdb**</span><span class="sxs-lookup"><span data-stu-id="c1675-113">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-the-data-on-target-azure-database-for-postrgesql"></a><span data-ttu-id="c1675-114">Importation des données dans la base de données Azure pour PostrgeSQL cible</span><span class="sxs-lookup"><span data-stu-id="c1675-114">Import the data on target Azure Database for PostrgeSQL</span></span>
<span data-ttu-id="c1675-115">Vous pouvez utiliser la ligne de commande psql et le paramètre -d, --dbname pour importer les données dans la base de données Azure pour PostrgeSQL que nous avons créée, puis charger les données à partir du fichier sql.</span><span class="sxs-lookup"><span data-stu-id="c1675-115">You can use the psql command line and the -d, --dbname parameter to import the data into Azure Database for PostrgeSQL we created and load data from the sql file.</span></span>
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
<span data-ttu-id="c1675-116">Cet exemple utilise l’utilitaire psql et un fichier de script nommé **testdb.sql** de l’étape précédente pour importer les données dans la base de données **mypgsqldb** sur le serveur cible **mypgserver-20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="c1675-116">This example uses psql utility and a script file named **testdb.sql** from previous step to import data into the database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a><span data-ttu-id="c1675-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c1675-117">Next steps</span></span>
- <span data-ttu-id="c1675-118">Pour migrer une base de données PostgreSQL par vidage et restauration, consultez la rubrique [Migration de votre base de données PostgreSQL par vidage et exportation](howto-migrate-using-dump-and-restore.md)</span><span class="sxs-lookup"><span data-stu-id="c1675-118">To migrate a PostgreSQL database using dump and restore, see [Migrate your PostgreSQL database using dump and restore](howto-migrate-using-dump-and-restore.md)</span></span>