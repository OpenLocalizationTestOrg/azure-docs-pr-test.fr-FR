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
# <a name="migrate-your-postgresql-database-using-export-and-import"></a>Migration de votre base de données PostgreSQL par exportation et importation
Vous pouvez utiliser [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract une base de données PostgreSQL dans un fichier de script et [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport les données de salutation dans la base de données cible hello à partir de ce fichier.

## <a name="prerequisites"></a>Composants requis
toostep via ce tooguide de procédure, vous devez :
- Un [Azure de base de données PostgreSQL serveur](quickstart-create-server-database-portal.md) avec tooallow accès aux règles de pare-feu et de la base de données dans cette section.
- Utilitaire de ligne de commande [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) installé
- Utilitaire de ligne de commande [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) installé

Suivez ces étapes tooexport et importer votre base de données PostgreSQL.

## <a name="create-a-script-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a>Créer un fichier de script à l’aide de pg_dump contenant hello toobe de données chargé
tooexport votre PostgreSQL existant de la base de données locale ou dans un fichier de script sql de machine virtuelle tooa, exécutez hello suivant de commande dans votre environnement existant :
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
Par exemple, si vous avez un serveur local contenant une base de données appelée **testdb**
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-hello-data-on-target-azure-database-for-postrgesql"></a>Importer des données sur la cible de la base de données Azure pour PostrgeSQL hello
Vous pouvez utiliser la ligne de commande psql hello et hello -d, données de hello--dbname paramètre tooimport dans la base de données Azure pour PostrgeSQL, nous avons créé et charger des données à partir du fichier sql de hello.
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
Cet exemple utilise psql utilitaire et un fichier de script nommé **testdb.sql** à partir des données de tooimport étape précédente dans la base de données hello **mypgsqldb** sur le serveur cible  **mypgserver-20170401.postgres.database.azure.com**.
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a>Étapes suivantes
- une base de données PostgreSQL à l’aide de vidage et la restauration, reportez-vous à toomigrate [migrer votre base de données PostgreSQL à l’aide de vidage et restauration](howto-migrate-using-dump-and-restore.md)
