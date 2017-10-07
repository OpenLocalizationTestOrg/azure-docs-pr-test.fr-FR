---
title: "aaaCopy des données à partir d’objets BLOB de stockage Azure dans Data Lake Store | Documents Microsoft"
description: "Utiliser des données toocopy de l’outil AdlCopy à partir d’objets BLOB de stockage Azure tooData Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: dc273ef8-96ef-47a6-b831-98e8a777a5c1
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: a3d4172eaefe7395cdef2fff72691bd70f642b78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-from-azure-storage-blobs-toodata-lake-store"></a>Copier des données d’objets BLOB de stockage Azure tooData Lake Store
> [!div class="op_single_selector"]
> * [Utilisation de DistCp](data-lake-store-copy-data-wasb-distcp.md)
> * [Utilisation d’AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
>
>

Azure Data Lake Store fournit un outil de ligne de commande, [AdlCopy](http://aka.ms/downloadadlcopy), toocopy des données à partir de hello les sources suivantes :

* Depuis des objets blob Azure dans Data Lake Store. Vous ne pouvez pas utiliser les données toocopy AdlCopy Data Lake Store tooAzure stockage BLOB.
* Depuis deux comptes Azure Data Lake Store.

Également, vous pouvez utiliser l’outil de AdlCopy hello dans deux modes différents :

* **Autonome**, où les outil hello utilisant la tâche de Data Lake Store ressources tooperform hello.
* **À l’aide d’un compte Analytique lac de données**, où les unités hello tooyour Analytique lac de données compte attribuées sont opération de copie utilisé tooperform hello. Vous pourriez toouse cette option lorsque vous cherchez des tâches de copie tooperform hello de manière prévisible.

## <a name="prerequisites"></a>Composants requis
Avant de commencer cet article, vous devez disposer de hello :

* **Un abonnement Azure**. Consultez [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).
* **objets blob Azure Storage** avec quelques données.
* **Un compte Azure Data Lake Store**. Pour obtenir des instructions sur la façon de voir d’un seul, toocreate [prise en main Azure Data Lake Store](data-lake-store-get-started-portal.md)
* **Analytique de LAC de données Azure du compte (facultatif)** -consultez [prise en main Analytique de LAC de données Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md) pour obtenir des instructions sur la façon dont toocreate stocker un lac de données de compte.
* **Outil AdlCopy**. Installer l’outil hello AdlCopy [http://aka.ms/downloadadlcopy](http://aka.ms/downloadadlcopy).

## <a name="syntax-of-hello-adlcopy-tool"></a>Syntaxe de hello AdlCopy outil
Utilisez hello suivant toowork syntaxe avec l’outil de AdlCopy hello

    AdlCopy /Source <Blob or Data Lake Store source> /Dest <Data Lake Store destination> /SourceKey <Key for Blob account> /Account <Data Lake Analytics account> /Unit <Number of Analytics units> /Pattern

paramètres Hello dans la syntaxe de hello sont décrites ci-dessous :

| Option | Description |
| --- | --- |
| Source |Spécifie l’emplacement hello de source de données hello dans l’objet blob de stockage Azure hello. Hello source peut être un conteneur d’objets blob, un objet blob ou un autre compte Data Lake Store. |
| Dest |Spécifie les hello Data Lake Store destination toocopy à. |
| SourceKey |Spécifie la clé d’accès de stockage hello pour la source d’objets blob Azure storage hello. Cela est nécessaire uniquement si la source de hello est un conteneur d’objets blob ou un objet blob. |
| Compte |**Facultatif**. Utilisez-le si vous souhaitez que le travail de copie du compte toorun hello toouse Analytique de LAC de données Azure. Si vous utilisez l’option d’Account hello dans la syntaxe de hello mais que vous ne spécifiez pas un compte Analytique lac de données, AdlCopy utilise un travail de hello de toorun de compte par défaut. En outre, si vous utilisez cette option, vous devez ajouter la source de hello (objet Blob de stockage Azure) et de destination (Azure Data Lake Store) comme sources de données pour votre compte Analytique lac de données. |
| Units |Spécifie le nombre hello d’unités Analytique lac de données qui sera utilisé pour le travail de copie hello. Cette option est obligatoire si vous utilisez hello **/compte** option compte de toospecify hello Analytique lac de données. |
| Modèle |Spécifie un modèle d’expression régulière qui indique quel toocopy d’objets BLOB ou des fichiers. AdlCopy respecte la casse pour la mise en correspondance. modèle par défaut de Hello utilisé lorsqu’aucun modèle n’est spécifié est toocopy tous les éléments. La spécification de plusieurs modèles de fichiers n’est pas prise en charge. |

## <a name="use-adlcopy-as-standalone-toocopy-data-from-an-azure-storage-blob"></a>Utiliser des données de toocopy AdlCopy (comme autonome) à partir d’un objet blob de stockage Azure
1. Ouvrez une invite de commandes et accédez répertoire toohello où AdlCopy est installé, généralement `%HOMEPATH%\Documents\adlcopy`.
2. Exécutez hello suivant commande toocopy un blob spécifique de hello source conteneur tooa Data Lake Store :

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    Par exemple :

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

    >[AZURE.NOTE] syntaxe de Hello ci-dessus spécifie hello fichier toobe copiés tooa dossier dans le compte Data Lake Store de hello. Outil de AdlCopy crée un dossier si le nom de dossier spécifié hello n’existe pas.

    Vous serez invité à tooenter informations d’identification hello pour hello abonnement Azure sous lequel vous avez à votre compte Data Lake Store. Vous découvrez une sortie similaire toohello :

        Initializing Copy.
        Copy Started.
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.

1. Vous pouvez également copier tous les objets BLOB de hello à partir d’un seul conteneur toohello Data Lake Store compte hello de commande suivante :

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/ /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>        

    Par exemple :

        AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

### <a name="performance-considerations"></a>Considérations relatives aux performances

Si vous copiez à partir d’un compte de stockage d’objets Blob Azure, vous pouvez être limitée au cours de la copie sur le côté de stockage d’objets blob hello. Cela sera dégrader les performances de hello de votre travail de copie. toolearn savoir plus sur les limites de hello de stockage d’objets Blob Azure, consultez les limites de stockage Azure à [abonnement Azure et limites de service](../azure-subscription-service-limits.md).

## <a name="use-adlcopy-as-standalone-toocopy-data-from-another-data-lake-store-account"></a>Utiliser des données de toocopy AdlCopy (comme autonome) à partir d’un autre compte Data Lake Store
Vous pouvez également utiliser les données de toocopy AdlCopy entre deux comptes Data Lake Store.

1. Ouvrez une invite de commandes et accédez répertoire toohello où AdlCopy est installé, généralement `%HOMEPATH%\Documents\adlcopy`.
2. Exécutez hello suivant commande toocopy un fichier spécifique à partir d’un tooanother de compte Data Lake Store.

        AdlCopy /Source adl://<source_adls_account>.azuredatalakestore.net/<path_to_file> /dest adl://<dest_adls_account>.azuredatalakestore.net/<path>/

    Par exemple :

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/909f2b.log /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

   > [!NOTE]
   > syntaxe de Hello ci-dessus spécifie hello fichier toobe copiés tooa dossier dans le compte Data Lake Store de destination hello. Outil de AdlCopy crée un dossier si le nom de dossier spécifié hello n’existe pas.
   >
   >

    Vous serez invité à tooenter informations d’identification hello pour hello abonnement Azure sous lequel vous avez à votre compte Data Lake Store. Vous découvrez une sortie similaire toohello :

        Initializing Copy.
        Copy Started.|
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.
3. Hello commande suivante copie tous les fichiers à partir d’un dossier spécifique dans hello source Data Lake Store compte tooa dossier de destination de hello compte Data Lake Store.

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/ /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

### <a name="performance-considerations"></a>Considérations relatives aux performances

Lorsque vous utilisez AdlCopy comme outil autonome, copie de hello est exécutée sur partagé, Azure les ressources managées. performances Hello que vous risquez d’obtenir dans cet environnement dépend de la charge du système et des ressources disponibles. Ce mode est idéal pour les petits transferts sur une base ad hoc. Aucun paramètre ne devez toobe paramétré lors de l’utilisation de AdlCopy comme outil autonome.

## <a name="use-adlcopy-with-data-lake-analytics-account-toocopy-data"></a>Utiliser des données toocopy AdlCopy (avec le compte de l’Analytique lac de données)
Vous pouvez également utiliser votre Analytique lac de données compte toorun hello toocopy données de la tâche AdlCopy depuis le stockage Azure BLOB tooData Lake Store. Vous utiliserez généralement cette option lorsque hello toobe de données déplacée dans hello de gigaoctets et téraoctets, et vous souhaitez que le débit des performances améliorées et prévisibles.

toouse que votre compte Analytique lac de données avec toocopy AdlCopy provenant d’un Blob de stockage Azure, la source de hello (objet Blob de stockage Azure) doit être ajouté en tant que source de données pour votre compte Analytique lac de données. Pour obtenir des instructions sur l’ajout de compte d’Analytique lac de données de tooyour de sources de données supplémentaires, consultez [Analytique de LAC de données de gérer les sources de données de compte](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#manage-data-sources).

> [!NOTE]
> Si vous copiez à partir d’un compte Azure Data Lake Store en tant que source de hello à l’aide d’un compte Analytique lac de données, il est inutile tooassociate hello compte Data Lake Store avec hello compte d’Analytique lac de données. Hello exigence tooassociate hello source magasin avec hello compte d’Analytique lac de données est uniquement lorsque la source de hello est un compte de stockage Azure.
>
>

Exécutez hello suivant toocopy de commande à partir d’un compte de tooa de blob du stockage Azure Data Lake Store à l’aide du compte de l’Analytique lac de données :

    AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Account <data_lake_analytics_account> /Unit <number_of_data_lake_analytics_units_to_be_used>

Par exemple :

    AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Account mydatalakeanalyticaccount /Units 2

De même, exécutez hello suivant toocopy de commande à partir d’un compte de tooa de blob du stockage Azure Data Lake Store à l’aide du compte de l’Analytique lac de données :

    AdlCopy /Source adl://mysourcedatalakestore.azuredatalakestore.net/mynewfolder/ /dest adl://mydestdatastore.azuredatalakestore.net/mynewfolder/ /Account mydatalakeanalyticaccount /Units 2

### <a name="performance-considerations"></a>Considérations relatives aux performances

Lors de la copie des données dans la plage de hello de téraoctets, à l’aide de AdlCopy avec votre propre compte Analytique de LAC de données Azure fournit des performances améliorées et plus prévisible. paramètre Hello qui doit être réglée est nombre hello de toouse d’unités de Azure Data Lake Analytique pour le travail de copie hello. Augmentation du nombre hello d’unités améliore les performances de hello de votre travail de copie. Chaque toobe fichier copié peut utiliser une unité de maximale. En spécifiant plus d’unités que le nombre de hello de fichiers copiés pas améliore les performances.

## <a name="use-adlcopy-toocopy-data-using-pattern-matching"></a>Utiliser des données de toocopy AdlCopy à l’aide de critères spéciaux
Dans cette section, vous apprendrez comment toouse AdlCopy les données de toocopy d’une source (dans notre exemple ci-dessous nous utilisons objet Blob de stockage Azure) compte Data Lake Store de tooa destination à l’aide de critères spéciaux. Par exemple, vous pouvez utiliser les étapes de hello ci-dessous toocopy tous les fichiers avec l’extension .csv à partir de hello source blob toohello de destination.

1. Ouvrez une invite de commandes et accédez répertoire toohello où AdlCopy est installé, généralement `%HOMEPATH%\Documents\adlcopy`.
2. Exécuter hello suivant commande toocopy tous les fichiers portant l’extension de *.csv à partir d’un blob spécifique à partir de hello source conteneur tooa Data Lake Store :

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Pattern *.csv

    Par exemple :

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/FoodInspectionData/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Pattern *.csv

## <a name="billing"></a>Facturation
* Si vous utilisez l’outil de AdlCopy hello autonome, que vous serez facturé pour les frais de sortie pour le déplacement des données, si la source de hello compte de stockage Azure n’est pas en hello même région que hello Data Lake Store.
* Si vous utilisez l’outil de AdlCopy hello avec votre Analytique lac de données compte standard [Analytique lac de données de taux de facturation](https://azure.microsoft.com/pricing/details/data-lake-analytics/) s’applique.

## <a name="considerations-for-using-adlcopy"></a>Considérations sur l’utilisation d’AdlCopy
* AdlCopy (pour la version 1.0.5) prend en charge la copie de données à partir de sources qui contiennent collectivement plusieurs milliers de fichiers et dossiers. Toutefois, si vous rencontrez des problèmes de copie d’un jeu de données volumineux, vous pouvez distribuer des fichiers/dossiers de hello dans différents sous-dossiers et utilisez à la place des sous-dossiers toothose de chemin d’accès hello en tant que source de hello.

## <a name="performance-considerations-for-using-adlcopy"></a>Considérations de performances sur l’utilisation d’AdlCopy

AdlCopy prend en charge la copie de données contenant des milliers de fichiers et dossiers. Toutefois, si vous rencontrez des problèmes de copie d’un jeu de données volumineux, vous pouvez distribuer hello fichiers/dossiers dans des sous-dossiers plus petits. AdlCopy est conçu pour les copies ad hoc. Si vous essayez de données toocopy régulièrement, vous devez envisager d’utiliser [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) qui fournit la gestion complète autour des opérations de copie hello.

## <a name="release-notes"></a>Notes de publication
* 1.0.13 - si vous copiez des données toohello même compte Azure Data Lake Store entre adlcopy plusieurs commandes, vous n’avez pas besoin de tooreenter vos informations d’identification pour chaque plus exécuter. Adlcopy met alors en cache ces informations sur plusieurs exécutions.

## <a name="next-steps"></a>Étapes suivantes
* [Sécuriser les données dans Data Lake Store](data-lake-store-secure-data.md)
* [Utiliser Azure Data Lake Analytics avec Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Utiliser Azure HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
