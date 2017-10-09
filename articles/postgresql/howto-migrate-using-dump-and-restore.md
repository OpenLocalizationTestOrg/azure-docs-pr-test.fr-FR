---
title: "aaaHow tooDump et la restauration dans la base de données Azure pour PostgreSQL | Documents Microsoft"
description: "Décrit comment tooextract un PostgreSQL de base de données dans un fichier de vidage et de la base de données PostgreSQL hello restauration à partir d’un fichier d’archive créé par pg_dump dans la base de données Azure pour PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 9ad28e9dec3927b0f80b5e6bab6423cc944f5156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a><span data-ttu-id="0daf3-103">Migration de votre base de données PostgreSQL par vidage et restauration</span><span class="sxs-lookup"><span data-stu-id="0daf3-103">Migrate your PostgreSQL database using dump and restore</span></span>
<span data-ttu-id="0daf3-104">Vous pouvez utiliser [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract une base de données PostgreSQL dans un fichier de vidage et [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) base de données PostgreSQL hello toorestore à partir d’un fichier d’archive créé par pg_dump.</span><span class="sxs-lookup"><span data-stu-id="0daf3-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract a PostgreSQL database into a dump file and [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) toorestore hello PostgreSQL database from an archive file created by pg_dump.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0daf3-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0daf3-105">Prerequisites</span></span>
<span data-ttu-id="0daf3-106">toostep via ce tooguide de procédure, vous devez :</span><span class="sxs-lookup"><span data-stu-id="0daf3-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="0daf3-107">Un [Azure de base de données PostgreSQL serveur](quickstart-create-server-database-portal.md) avec tooallow accès aux règles de pare-feu et de la base de données dans cette section.</span><span class="sxs-lookup"><span data-stu-id="0daf3-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules tooallow access and database under it.</span></span>
- <span data-ttu-id="0daf3-108">Utilitaires de ligne de commande [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) et [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) installés</span><span class="sxs-lookup"><span data-stu-id="0daf3-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) and [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) command-line utilities installed</span></span>

<span data-ttu-id="0daf3-109">Suivez ces étapes toodump et restaurer votre base de données PostgreSQL :</span><span class="sxs-lookup"><span data-stu-id="0daf3-109">Follow these steps toodump and restore your PostgreSQL database:</span></span>

## <a name="create-a-dump-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a><span data-ttu-id="0daf3-110">Créer un fichier dump à l’aide de pg_dump contenant hello toobe de données chargé</span><span class="sxs-lookup"><span data-stu-id="0daf3-110">Create a dump file using pg_dump that contains hello data toobe loaded</span></span>
<span data-ttu-id="0daf3-111">tooback d’un PostgreSQL existant de la base de données locale ou dans une machine virtuelle, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0daf3-111">tooback up an existing PostgreSQL database on-premises or in a VM, run hello following command:</span></span>
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
<span data-ttu-id="0daf3-112">Par exemple, si vous avez un serveur local contenant une base de données appelée **testdb**</span><span class="sxs-lookup"><span data-stu-id="0daf3-112">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-hello-data-into-hello-target-azure-database-for-postrgesql-using-pgrestore"></a><span data-ttu-id="0daf3-113">Restaurer des données de hello dans la cible de hello de base de données Azure pour PostrgeSQL à l’aide de pg_restore</span><span class="sxs-lookup"><span data-stu-id="0daf3-113">Restore hello data into hello target Azure Database for PostrgeSQL using pg_restore</span></span>
<span data-ttu-id="0daf3-114">Une fois que vous avez créé la base de données cible hello, vous pouvez utiliser la commande de pg_restore hello et hello -d, données de salutation--dbname paramètre toorestore dans la base de données cible hello à partir du fichier de vidage hello.</span><span class="sxs-lookup"><span data-stu-id="0daf3-114">Once you have created hello target database, you can use hello pg_restore command and hello -d, --dbname parameter toorestore hello data into hello target database from hello dump file.</span></span>
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
<span data-ttu-id="0daf3-115">Dans cet exemple, restaurer les données de hello à partir du fichier de vidage hello **testdb.dump** dans la base de données hello **mypgsqldb** sur le serveur cible **mypgserver-20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="0daf3-115">In this example, restore hello data from hello dump file **testdb.dump** into hello database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a><span data-ttu-id="0daf3-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0daf3-116">Next steps</span></span>
- <span data-ttu-id="0daf3-117">consultez d’une base de données PostgreSQL à l’aide d’exportation et importation, toomigrate [migrer votre base de données PostgreSQL exporter et importer](howto-migrate-using-export-and-import.md)</span><span class="sxs-lookup"><span data-stu-id="0daf3-117">toomigrate a PostgreSQL database using export and import, see [Migrate your PostgreSQL database using export and import](howto-migrate-using-export-and-import.md)</span></span>
