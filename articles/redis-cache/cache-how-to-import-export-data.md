---
title: "aaaImport et exporter des données dans le Cache Redis Azure | Documents Microsoft"
description: "Découvrez comment tooimport et exportation tooand de données à partir du stockage d’objets blob avec vos instances de Cache Redis Azure premium"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 4a68ac38-87af-4075-adab-569d37d7cc9e
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: sdanie
ms.openlocfilehash: f17464b207f1c652952f4da63ca147473fee2759
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-data-in-azure-redis-cache"></a>Importer et exporter des données dans le Cache Redis Azure
Importation/exportation est une opération de gestion de données du Cache Redis Azure, qui vous permet de tooimport données dans le Cache Redis Azure ou exporter des données à partir du Cache Redis Azure par l’importation et exportation d’un instantané de base de données de Cache Redis (RDB) à partir d’un blob de tooa de cache premium dans Azure Compte de stockage. 

- **Exporter** -vous pouvez exporter votre tooa de captures instantanées Azure Redis Cache RDB objet Blob de pages.
- **Importation** : vous pouvez importer vos captures instantanées Redis Cache RDB à partir d’un objet blob de pages ou d’un objet blob de blocs.

Importation/exportation vous permet de toomigrate entre différentes instances de Cache Redis Azure ou remplir le cache de hello avec les données avant des utiliser.

Cet article fournit un guide pour l’importation et exportation de données avec le Cache Redis Azure et fournit des réponses hello toocommonly aux questions.

> [!IMPORTANT]
> Cette fonctionnalité est en version préliminaire et uniquement disponible pour les caches de [niveau Premium](cache-premium-tier-intro.md) .
>
>

## <a name="import"></a>Importer
Importation peut être des fichiers compatibles RDB toobring utilisé Redis à partir de n’importe quel serveur Redis en cours d’exécution dans n’importe quel cloud ou l’environnement, y compris Redis en cours d’exécution sur Linux, Windows ou n’importe quel fournisseur de cloud comme Amazon Web Services et d’autres. L’importation de données est un toocreate facilement un cache de données prédéfinis. Pendant le processus d’importation hello, le Cache Redis Azure charge les fichiers RDB hello depuis le stockage Azure en mémoire, puis insère les clés hello dans le cache de hello.

> [!NOTE]
> Avant de commencer l’opération d’importation hello, assurez-vous que votre base de données Redis (RDB) ou les fichiers sont téléchargés dans la page ou les objets BLOB de blocs dans le stockage Azure, hello même région et l’abonnement en tant que votre instance de Cache Redis Azure. Pour plus d’informations, consultez l’article [Prise en main du stockage d’objets blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Si vous avez exporté le fichier RDB à l’aide de hello [exportation d’Azure Redis Cache](#export) fonctionnalité, votre fichier RDB est déjà stocké dans un objet blob de pages et est prêt pour l’importation.
>
>

1. tooimport un ou plusieurs exporté des objets BLOB du cache, [parcourir le cache de tooyour](cache-configure.md#configure-redis-cache-settings) hello portail Azure et cliquez sur **importer des données** de hello **menu ressource**.

    ![Importer des données][cache-import-data]
2. Cliquez sur **choisir un étaient** et sélectionnez le compte de stockage hello contenant hello données tooimport.

    ![Sélection d'un compte de stockage][cache-import-choose-storage-account]
3. Cliquez sur le conteneur hello contenant hello données tooimport.

    ![Sélection d’un conteneur][cache-import-choose-container]
4. Sélectionnez un ou plusieurs tooimport d’objets BLOB en cliquant sur hello zone toohello gauche du nom d’objet blob hello, puis cliquez sur **sélectionnez**.

    ![Sélection d’objets blob][cache-import-choose-blobs]
5. Cliquez sur **importer** processus d’importation toobegin hello.

   > [!IMPORTANT]
   > cache de Hello n’est pas accessible par les clients de cache au cours du processus d’importation hello et toutes les données existantes dans le cache de hello sont supprimées.
   >
   >

    ![Importer][cache-import-blobs]

    Vous pouvez surveiller la progression hello d’opération d’importation hello en notifications hello suivantes à partir de hello portail Azure, ou en affichant les événements de hello Bonjour [journal d’audit](../azure-resource-manager/resource-group-audit.md).

    ![Progression de l’importation][cache-import-data-import-complete]

## <a name="export"></a>Exportation
Exportation vous permet des données de hello tooexport stockées dans le Cache Redis Azure tooRedis compatible RDB ou les fichiers. Vous pouvez utiliser ces données toomove de fonctionnalité à partir d’un Cache Redis Azure instance tooanother ou tooanother Redis server. Au cours du processus d’exportation hello, un fichier temporaire est créé sur hello VM que hôtes hello l’instance de serveur de Cache Redis Azure et hello fichier téléchargé toohello désigné du compte de stockage. Lors de l’opération d’exportation hello se termine avec l’état de réussite ou l’échec, le fichier temporaire de hello est supprimé.

1. contenu actuel de hello tooexport de hello cache toostorage, [Parcourir tooyour cache](cache-configure.md#configure-redis-cache-settings) hello portail Azure et cliquez sur **exporter des données** de hello **menu ressource**.

    ![Choisir un conteneur de stockage][cache-export-data-choose-storage-container]
2. Cliquez sur **choisir un conteneur de stockage** et sélectionnez le compte de stockage hello souhaité. compte de stockage Hello doit être Bonjour même abonnement et région que votre cache.

   > [!IMPORTANT]
   > La fonctionnalité Exportation fonctionne avec les objets blob de pages, qui sont pris en charge par les comptes de stockage Resource Manager et classiques, mais pas par les [comptes de stockage d’objets Blob](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts) pour l’instant.
   >
   >

    ![Compte de stockage][cache-export-data-choose-account]
3. Choisissez hello souhaité conteneur d’objets blob et cliquez sur **sélectionnez**. toouse un nouveau conteneur, cliquez sur **ajouter un conteneur** tooadd il premier, puis sélectionnez à partir de la liste de hello.

    ![Choisir un conteneur de stockage][cache-export-data-container]
4. Tapez un **préfixe de nom d’objet Blob** et cliquez sur **exporter** processus d’exportation toostart hello. préfixe de nom d’objet blob Hello est tooprefix utilisé hello les noms des fichiers générés par cette opération d’exportation.

    ![Exportation][cache-export-data]

    Vous pouvez surveiller la progression hello d’opération d’exportation hello en notifications hello suivantes à partir de hello portail Azure, ou en affichant les événements de hello Bonjour [journal d’audit](../azure-resource-manager/resource-group-audit.md).

    ![Exportation des données terminées][cache-export-data-export-complete]

    Caches restent disponibles pour une utilisation pendant le processus d’exportation hello.

## <a name="importexport-faq"></a>FAQ sur l’Importation/Exportation
Cette section contient des questions fréquemment posées sur la fonctionnalité d’importation/exportation hello.

* [Quels niveaux de tarification permettent d’utiliser l’Importation/Exportation ?](#what-pricing-tiers-can-use-importexport)
* [Puis-je importer des données à partir de n’importe quel serveur Redis ?](#can-i-import-data-from-any-redis-server)
* [Quelles versions RDB puis-je importer ?](#what-rdb-versions-can-i-import)
* [Mon cache est-il disponible pendant une opération d’Importation/Exportation ?](#is-my-cache-available-during-an-importexport-operation)
* [Puis-je utiliser l’Importation/Exportation avec le cluster Redis ?](#can-i-use-importexport-with-redis-cluster)
* [Comment l’importation/exportation fonctionne avec un paramètre de base de données personnalisé ?](#how-does-importexport-work-with-a-custom-databases-setting)
* [En quoi l’Importation/Exportation est-elle différente de la persistance Redis ?](#how-is-importexport-different-from-redis-persistence)
* [Puis-je automatiser l’Importation/Exportation à l’aide de PowerShell, de CLI ou d’autres clients de gestion ?](#can-i-automate-importexport-using-powershell-cli-or-other-management-clients)
* [J’ai reçu une erreur de délai d’attente pendant mon opération d’importation/exportation. Qu’est-ce que cela signifie ?](#i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean)
* [J’ai reçu une erreur lors de l’exportation de mon tooAzure données stockage d’objets Blob. Que s’est-il passé ?](#i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened)

### <a name="what-pricing-tiers-can-use-importexport"></a>Quels niveaux de tarification permettent d’utiliser l’Importation/Exportation ?
Importation/exportation est disponible uniquement dans le niveau tarifaire premium de hello.

### <a name="can-i-import-data-from-any-redis-server"></a>Puis-je importer des données à partir de n’importe quel serveur Redis ?
Oui, en outre tooimporting les données exportées à partir d’instances de Cache Redis Azure, vous pouvez importer les fichiers RDB à partir de n’importe quel serveur Redis en cours d’exécution dans n’importe quel cloud ou l’environnement, telles que les fournisseurs de cloud comme Amazon Web Services, Windows ou Linux. toodo ce téléchargement hello RDB fichier à partir du serveur de Redis hello souhaité dans un objet blob de blocs ou de pages dans un compte de stockage Azure, puis importez il dans votre instance de Cache Redis Azure premium. Par exemple, vous pouvez souhaitez que les données de salutation tooexport à partir de votre cache de production et l’importer dans un cache utilisé en tant que partie d’un environnement intermédiaire pour tester ou de migration.

> [!IMPORTANT]
> toosuccessfully importer des données exportées à partir des serveurs de Redis autre que le Cache Redis Azure lors de l’aide d’un objet blob de pages, la taille d’objet blob hello page doit être alignée sur une limite de 512 octets. Pour exemple code tooperform tous requis remplissage d’octet, consultez [exemple page blog pour télécharger](https://github.com/JimRoberts-MS/SamplePageBlobUpload).
> 
> 

### <a name="what-rdb-versions-can-i-import"></a>Quelles versions RDB puis-je importer ?

Cache Redis Azure prend en charge l’importation RDB via la version 7 de RDB.

### <a name="is-my-cache-available-during-an-importexport-operation"></a>Mon cache est-il disponible pendant une opération d’Importation/Exportation ?
* **Exporter** - Caches restent disponibles et vous pouvez continuer votre cache toouse pendant une opération d’exportation.
* **Importer** - Caches deviennent indisponibles lorsqu’une opération d’importation démarre et sont disponibles pour une utilisation lors de l’opération d’importation hello se termine.

### <a name="can-i-use-importexport-with-redis-cluster"></a>Puis-je utiliser l’Importation/Exportation avec le cluster Redis ?
Oui, et vous pouvez importer/exporter des données entre un cache en cluster et un cache hors cluster. Depuis que le cluster Redis [ne prend en charge que la base de données 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), toutes les données de bases de données différentes de 0 ne sont pas importées. Lors de l’importation de données en cluster du cache, les clés de hello sont redistribuées entre les partitions hello du cluster de hello.

### <a name="how-does-importexport-work-with-a-custom-databases-setting"></a>Comment l’importation/exportation fonctionne avec un paramètre de base de données personnalisé ?
Certains niveaux de tarification ont différents [limites des bases de données](cache-configure.md#databases), donc il existe certaines considérations lors de l’importation si vous avez configuré une valeur personnalisée pour hello `databases` paramètre lors de la création du cache.

* Lors de l’importation tooa tarification avec une faible `databases` limite à niveau hello à partir duquel vous avez exporté :
  * Si vous utilisez le nombre par défaut de hello de `databases`, qui est 16 pour tous les niveaux de tarification, aucune donnée n’est perdue.
  * Si vous utilisez un nombre de `databases` que se situe dans les limites de hello pour hello ne couche toowhich vous importez, aucune donnée n’est perdue.
  * Si vos données exportées contenaient des données dans une base de données dépasse les limites de hello du nouveau niveau de hello, données hello à partir de ces bases de données plus élevées ne sont pas importées.

### <a name="how-is-importexport-different-from-redis-persistence"></a>En quoi l’Importation/Exportation est-elle différente de la persistance Redis ?
Persistance de Cache Redis Azure vous permet de toopersist les données stockées dans Redis tooAzure stockage. Lors de la persistance est configurée, le Cache Redis Azure conserve un instantané du cache Redis de hello dans un toodisk de format binaire Redis selon une fréquence de sauvegarde peut être configurée. Si un événement catastrophique désactive hello principal et cache de réplica se produit, les données du cache de salutation sont restaurées automatiquement à l’aide d’instantané le plus récent hello. Pour plus d’informations, consultez [la persistance des données d’un Cache de Redis Azure Premium tooconfigure](cache-how-to-premium-persistence.md).

Importation / exportation vous permet de toobring importer ou exporter à partir du Cache Redis Azure. Elle ne configure pas la sauvegarde et restauration à l’aide de la persistance Redis.

### <a name="can-i-automate-importexport-using-powershell-cli-or-other-management-clients"></a>Puis-je automatiser l’Importation/Exportation à l’aide de PowerShell, de CLI ou d’autres clients de gestion ?
Oui, pour PowerShell instructions voir [tooimport un cache Redis](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) et [tooexport un cache Redis](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).

### <a name="i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean"></a>J’ai reçu une erreur de délai d’attente pendant mon opération d’Importation/Exportation. Qu’est-ce que cela signifie ?
Si vous restez sur hello **importer des données** ou **exporter des données** panneau pendant plus de 15 minutes avant de lancer l’opération de hello, vous recevez une erreur avec une erreur message similaire toohello l’exemple suivant :

    hello request tooimport data into cache 'contoso55' failed with status 'error' and error 'One of hello SAS URIs provided could not be used for hello following reason: hello SAS token end time (se) must be at least 1 hour from now and hello start time (st), if given, must be at least 15 minutes in hello past.

tooresolve, démarrer hello importation ou l’exportation avant 15 minutes se sont écoulées.

### <a name="i-got-an-error-when-exporting-my-data-tooazure-blob-storage-what-happened"></a>J’ai reçu une erreur lors de l’exportation de mon tooAzure données stockage d’objets Blob. Que s’est-il passé ?
L’exportation ne fonctionne qu’avec les fichiers RDB stockés sous la forme d’objets blob de pages. Les autres types d’objets blob ne sont pas pris en charge pour l’instant, y compris les comptes de stockage d’objets blob de niveaux chaud et froid. Pour plus d’informations, consultez [Comptes de stockage Blob](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).

## <a name="next-steps"></a>Étapes suivantes
Découvrez comment mettre en cache des fonctionnalités par toouse plus premium.

* [Couche de présentation toohello Azure Redis Cache Premium](cache-premium-tier-intro.md)    

<!-- IMAGES -->
[cache-settings-import-export-menu]: ./media/cache-how-to-import-export-data/cache-settings-import-export-menu.png
[cache-export-data-choose-account]: ./media/cache-how-to-import-export-data/cache-export-data-choose-account.png
[cache-export-data-choose-storage-container]: ./media/cache-how-to-import-export-data/cache-export-data-choose-storage-container.png
[cache-export-data-container]: ./media/cache-how-to-import-export-data/cache-export-data-container.png
[cache-export-data-export-complete]: ./media/cache-how-to-import-export-data/cache-export-data-export-complete.png
[cache-export-data]: ./media/cache-how-to-import-export-data/cache-export-data.png
[cache-import-data]: ./media/cache-how-to-import-export-data/cache-import-data.png
[cache-import-choose-storage-account]: ./media/cache-how-to-import-export-data/cache-import-choose-storage-account.png
[cache-import-choose-container]: ./media/cache-how-to-import-export-data/cache-import-choose-container.png
[cache-import-choose-blobs]: ./media/cache-how-to-import-export-data/cache-import-choose-blobs.png
[cache-import-blobs]: ./media/cache-how-to-import-export-data/cache-import-blobs.png
[cache-import-data-import-complete]: ./media/cache-how-to-import-export-data/cache-import-data-import-complete.png
