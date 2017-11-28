---
title: "Guide pratique pour vider et restaurer une base de données Azure pour PostgreSQL | Microsoft Docs"
description: "Décrit comment extraire une base de données PostgreSQL dans un fichier de vidage et restaurer la base de données PostgreSQL à partir d’un fichier d’archive créé par la commande pg_dump dans la base de données Azure pour PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 190373c4980b67e16b58700e4b7e65658545c615
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a><span data-ttu-id="76bc7-103">Migration de votre base de données PostgreSQL par vidage et restauration</span><span class="sxs-lookup"><span data-stu-id="76bc7-103">Migrate your PostgreSQL database using dump and restore</span></span>
<span data-ttu-id="76bc7-104">Vous pouvez utiliser la commande [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) pour extraire une base de données PostgreSQL vers un fichier de vidage, et la commande [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) pour restaurer la base de données PostgreSQL à partir d’un fichier d’archive créé par pg_dump.</span><span class="sxs-lookup"><span data-stu-id="76bc7-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) to extract a PostgreSQL database into a dump file and [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) to restore the PostgreSQL database from an archive file created by pg_dump.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76bc7-105">Prérequis</span><span class="sxs-lookup"><span data-stu-id="76bc7-105">Prerequisites</span></span>
<span data-ttu-id="76bc7-106">Pour parcourir ce guide pratique, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="76bc7-106">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="76bc7-107">Un [serveur Azure Database pour PostgreSQL](quickstart-create-server-database-portal.md) avec des règles de pare-feu autorisant l’accès et la base de données sous-jacente.</span><span class="sxs-lookup"><span data-stu-id="76bc7-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules to allow access and database under it.</span></span>
- <span data-ttu-id="76bc7-108">Utilitaires de ligne de commande [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) et [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) installés</span><span class="sxs-lookup"><span data-stu-id="76bc7-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) and [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) command-line utilities installed</span></span>

<span data-ttu-id="76bc7-109">Suivez les étapes ci-dessous pour vider et restaurer votre base de données PostgreSQL :</span><span class="sxs-lookup"><span data-stu-id="76bc7-109">Follow these steps to dump and restore your PostgreSQL database:</span></span>

## <a name="create-a-dump-file-using-pgdump-that-contains-the-data-to-be-loaded"></a><span data-ttu-id="76bc7-110">Création d’un fichier de vidage à l’aide de pg_dump qui contient les données à charger</span><span class="sxs-lookup"><span data-stu-id="76bc7-110">Create a dump file using pg_dump that contains the data to be loaded</span></span>
<span data-ttu-id="76bc7-111">Pour sauvegarder une base de données PostgreSQL existante en local ou sur une machine virtuelle, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="76bc7-111">To back up an existing PostgreSQL database on-premises or in a VM, run the following command:</span></span>
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
<span data-ttu-id="76bc7-112">Par exemple, si vous avez un serveur local contenant une base de données appelée **testdb**</span><span class="sxs-lookup"><span data-stu-id="76bc7-112">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-the-data-into-the-target-azure-database-for-postrgesql-using-pgrestore"></a><span data-ttu-id="76bc7-113">Restauration des données dans la base de données cible pour PostrgeSQL à l’aide de pg_restore</span><span class="sxs-lookup"><span data-stu-id="76bc7-113">Restore the data into the target Azure Database for PostrgeSQL using pg_restore</span></span>
<span data-ttu-id="76bc7-114">Une fois que vous avez créé la base de données cible, vous pouvez utiliser la commande pg_restore et le paramètre -d, --dbname pour restaurer les données dans la base de données cible à partir du fichier de vidage.</span><span class="sxs-lookup"><span data-stu-id="76bc7-114">Once you have created the target database, you can use the pg_restore command and the -d, --dbname parameter to restore the data into the target database from the dump file.</span></span>
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
<span data-ttu-id="76bc7-115">Dans cet exemple, restaurez les données à partir du fichier de vidage **testdb.dump** dans la base de données **mypgsqldb** sur le serveur cible **mypgserver-20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="76bc7-115">In this example, restore the data from the dump file **testdb.dump** into the database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a><span data-ttu-id="76bc7-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="76bc7-116">Next steps</span></span>
- <span data-ttu-id="76bc7-117">Pour migrer une base de données PostgreSQL par exportation et importation, consultez la rubrique [Migration de votre base de données PostgreSQL par exportation et importation](howto-migrate-using-export-and-import.md)</span><span class="sxs-lookup"><span data-stu-id="76bc7-117">To migrate a PostgreSQL database using export and import, see [Migrate your PostgreSQL database using export and import](howto-migrate-using-export-and-import.md)</span></span>