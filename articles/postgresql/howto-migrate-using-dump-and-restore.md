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
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a>Migration de votre base de données PostgreSQL par vidage et restauration
Vous pouvez utiliser [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract une base de données PostgreSQL dans un fichier de vidage et [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) base de données PostgreSQL hello toorestore à partir d’un fichier d’archive créé par pg_dump.

## <a name="prerequisites"></a>Composants requis
toostep via ce tooguide de procédure, vous devez :
- Un [Azure de base de données PostgreSQL serveur](quickstart-create-server-database-portal.md) avec tooallow accès aux règles de pare-feu et de la base de données dans cette section.
- Utilitaires de ligne de commande [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) et [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) installés

Suivez ces étapes toodump et restaurer votre base de données PostgreSQL :

## <a name="create-a-dump-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a>Créer un fichier dump à l’aide de pg_dump contenant hello toobe de données chargé
tooback d’un PostgreSQL existant de la base de données locale ou dans une machine virtuelle, exécutez hello de commande suivante :
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
Par exemple, si vous avez un serveur local contenant une base de données appelée **testdb**
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-hello-data-into-hello-target-azure-database-for-postrgesql-using-pgrestore"></a>Restaurer des données de hello dans la cible de hello de base de données Azure pour PostrgeSQL à l’aide de pg_restore
Une fois que vous avez créé la base de données cible hello, vous pouvez utiliser la commande de pg_restore hello et hello -d, données de salutation--dbname paramètre toorestore dans la base de données cible hello à partir du fichier de vidage hello.
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
Dans cet exemple, restaurer les données de hello à partir du fichier de vidage hello **testdb.dump** dans la base de données hello **mypgsqldb** sur le serveur cible **mypgserver-20170401.postgres.database.azure.com**.
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a>Étapes suivantes
- consultez d’une base de données PostgreSQL à l’aide d’exportation et importation, toomigrate [migrer votre base de données PostgreSQL exporter et importer](howto-migrate-using-export-and-import.md)
