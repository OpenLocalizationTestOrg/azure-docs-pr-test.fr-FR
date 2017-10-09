---
title: "aaaOverview d’Azure Data Lake Store | Documents Microsoft"
description: "Comprendre ce qui est la valeur Azure Data Lake Store et hello fournie sur d’autres banques de données"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: b3475057-9427-4492-a3af-25a802a23a79
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 5a60a6b86a51c44647cf4ee168fb333d1c37b1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-data-lake-store"></a>Présentation d'Azure Data Lake Store
Azure Data Lake Store est un référentiel d'entreprise à très grande échelle pour les charges de travail d'analyse du Big Data. Azure Data Lake vous permet de toocapture les données de n’importe quelle vitesse de taille, de type et de réception dans un emplacement unique pour l’analytique opérationnelle et exploratoire.

> [!TIP]
> Hello d’utilisation [Data Lake Store cursus](https://azure.microsoft.com/documentation/learning-paths/data-lake-store-self-guided-training/) toostart Explorer le service d’Azure Data Lake Store hello.
> 
> 

Azure Data Lake Store est accessible à partir de Hadoop (disponible dans le cluster HDInsight) à l’aide de hello WebHDFS compatibles REST API. Il est spécifiquement conçu tooenable analytique sur les données stockée hello et est réglé pour des performances pour les scénarios de données analytique. En dehors de la zone de hello, elle inclut toutes les fonctions de niveau professionnel hello : sécurité, de facilité de gestion, de l’évolutivité, de fiabilité et de disponibilité, essentielles pour les cas d’usage entreprise réel.

![Azure Data Lake](./media/data-lake-store-overview/data-lake-store-concept.png)

Certaines des fonctionnalités clés de hello de hello Azure Data Lake hello suivants.

### <a name="built-for-hadoop"></a>Conçu pour Hadoop
magasin d’Azure Data Lake Hello est un système de fichiers Apache Hadoop compatible avec Hadoop Distributed fichier système (HDFS) et fonctionne avec l’écosystème de Hadoop hello.  Votre HDInsight applications ou les services qui utilisent hello WebHDFS API existantes peuvent s’intégrer facilement avec Data Lake Store. Data Lake Store offre également une interface REST compatible WebHDFS pour les applications

Les données stockées dans Data Lake Store peuvent être facilement analysées avec les infrastructures d'analyse Hadoop, comme MapReduce ou Hive. Clusters Microsoft Azure HDInsight peuvent être configurés et configuré toodirectly accéder aux données stockées dans Data Lake Store.

### <a name="unlimited-storage-petabyte-files"></a>Stockage illimité, fichiers de l´'ordre du pétaoctet
Azure Data Lake Store offre un stockage illimité et est approprié pour le stockage d'une grande variété de données à des fins d'analyse. Il n’impose aucune limite sur les tailles de compte, les tailles de fichier ou hello montant de données qui peuvent être stockées dans un lac de données. Les fichiers individuels peuvent s’échelonner de toopetabytes kilo-octets taille rend un toostore conseillés n’importe quel type de données. Données sont stockées de façon durable en effectuant des copies multiples et il n’existe aucune limite de durée hello pour le hello les données peuvent être stockées dans un lac de données hello.

### <a name="performance-tuned-for-big-data-analytics"></a>Performances optimisées pour l'analyse du Big Data
Azure Data Lake Store est conçu pour exécutant des systèmes d’analyse qui nécessitent un débit massive tooquery et analyser de grandes quantités de données à grande échelle. lac de données Hello répartit les parties d’un fichier sur un nombre de serveurs de stockage individuel. Cela améliore hello débit de lecture lors de la lecture du fichier hello en parallèle pour effectuer l’analytique des données.

### <a name="enterprise-ready-highly-available-and-secure"></a>Prêt à l'emploi : hautement disponible et sécurisé
Azure Data Lake Store offre une fiabilité et une disponibilité aux normes industrielles. Vos ressources de données sont stockés durablement en effectuant des copies redondantes des tooguard contre les défaillances inattendues. Les entreprises peuvent utiliser Azure Data Lake dans leurs solutions et l'intégrer à leur plateforme de données existante.

Data Lake Store fournit également une sécurité de niveau entreprise pour les données stockée hello. Pour plus d'informations, consultez [Sécurisation des données dans Azure Data Lake Store](#DataLakeStoreSecurity).

### <a name="all-data"></a>Toutes les données
Azure Data Lake Store peut stocker des données dans leur format natif, en l'état, sans nécessiter de transformations préalables. Data Lake Store ne nécessitent un toobe schéma définie avant le chargement de données de hello, laissant les données de hello toointerpret toohello framework analytiques individuels et définir un schéma au moment de l’analyse de hello hello. En cours de fichiers toostore en mesure de tailles arbitraires et les formats rend possible pour toohandle de Data Lake Store structurée, semi-structurées et non structurées les données.

Les conteneurs Azure Data Lake Store pour données sont essentiellement des dossiers et des fichiers. Vous utiliser hello stockée les données à l’aide de kits de développement logiciel, le portail d’Azure et Azure Powershell. Tant que vous placez vos données dans le magasin de hello à l’aide de ces interfaces et les conteneurs appropriés hello, vous pouvez stocker n’importe quel type de données. Data Lake Store n’effectue aucun traitement spécial des données en fonction de type hello de données qu’elle contient.

## <a name="DataLakeStoreSecurity"></a>Sécurisation des données dans Azure Data Lake Store
Azure Data Lake Store utilise Azure Active Directory pour l’authentification et la liste de contrôle d’accès (ACL) toomanage accéder à des données tooyour.

| Fonctionnalité | Description |
| --- | --- |
| Authentification |Azure Data Lake Store s’intègre avec Azure Active Directory (AAD) pour la gestion des identités et des accès pour toutes les données hello stockées dans Azure Data Lake Store. Suite à l’intégration de hello, avantages d’Azure Data Lake à partir de toutes les fonctionnalités AAD, y compris l’authentification multifacteur, l’accès conditionnel, contrôle d’accès basé sur un rôle, surveillance de l’utilisation d’application, sécurité analyse et d’alerte, etc. Azure Data Lake Store prend en charge hello protocole OAuth 2.0 pour l’authentification avec dans l’interface REST hello. |
| Contrôle d’accès |Azure Data Lake Store fournit le contrôle d’accès en prenant en charge les autorisations de POSIX-style exposées par hello WebHDFS protocole. Bonjour Data Lake Store Public Preview (version actuelle de hello), les ACL peuvent être activées sur le dossier racine de hello, dans les sous-dossiers et sur des fichiers individuels. Pour plus d’informations sur le fonctionnement des ACL dans le contexte de Data Lake Store, consultez [Contrôle d’accès dans Data Lake Store](data-lake-store-access-control.md). |
| Chiffrement |Data Lake Store fournit également le chiffrement de données qui sont stockés dans le compte de hello. Vous spécifiez des paramètres de chiffrement hello lors de la création d’un compte Data Lake Store. Vous pouvez choisir toohave vos données chiffrées ou optez pour aucun chiffrement. Pour plus d’informations sur la façon de configuration relatives au chiffrement de tooprovide, consultez [prise en main Azure Data Lake Store à l’aide de hello Azure Portal](data-lake-store-get-started-portal.md). |

Choix toolearn plus d’informations sur la sécurisation des données dans Data Lake Store. Suivez les liens hello ci-dessous.

* Pour obtenir des instructions sur la façon de toosecure les données dans Data Lake Store, consultez [sécurisation des données dans Azure Data Lake Store](data-lake-store-secure-data.md).
* Vous préférez visualiser des vidéos ? [Regardez cette vidéo](https://mix.office.com/watch/1q2mgzh9nn5lx) sur la façon dont les données de toosecure stockées dans Data Lake Store.

## <a name="applications-compatible-with-azure-data-lake-store"></a>Applications compatibles avec Azure Data Lake Store
Azure Data Lake Store est compatible avec les composants source plus ouverts dans l’écosystème de Hadoop hello. Par ailleurs, il s’intègre facilement avec d’autres services Azure. Cela fait du Data Lake Store la solution idéale pour vos besoins de stockage de données. Suivez les liens hello ci-dessous toolearn plus en détail comment Data Lake Store peut être utilisé avec les composants open source ainsi que d’autres services Azure.

* Consultez [Applications et services compatibles avec Azure Data Lake](data-lake-store-compatible-oss-other-applications.md) pour obtenir une liste des applications open source interopérables avec Data Lake Store.
* Consultez [intégration avec d’autres services Azure](data-lake-store-integrate-with-other-services.md) toounderstand comment Data Lake Store peuvent être utilisée avec autres Azure services tooenable un éventail plus large de scénarios.
* Consultez [scénarios d’utilisation de Data Lake Store](data-lake-store-data-scenarios.md) toolearn comment toouse Data Lake stocker dans des scénarios tels que la réception de données, le traitement des données, de téléchargement des données et de visualisation des données.

## <a name="what-is-azure-data-lake-store-file-system-adl"></a>Présentation du système de fichiers Azure Data Lake Store (adl://)
Data Lake Store est accessible via le nouveau système de fichiers hello, hello AzureDataLakeFilesystem (adl : / /), dans les environnements Hadoop (disponibles dans le cluster HDInsight). Applications et services qui utilisent adl : / / sont parti tootake en mesure de davantage d’optimisation des performances qui ne sont pas actuellement disponibles dans WebHDFS. Par conséquent, donne Data Lake Store hello de flexibilité tooeither bénéficier des performances optimales hello avec hello recommandé d’utiliser adl : / / ou conserver le code existant par la poursuite de l’opération toouse hello WebHDFS API directement. Azure HDInsight tire pleinement parti hello AzureDataLakeFilesystem tooprovide hello des performances optimales sur Data Lake Store.

Vous pouvez accéder à vos données à l’aide de Data Lake Store hello `adl://<data_lake_store_name>.azuredatalakestore.net`. Pour plus d’informations sur la façon dont tooaccess hello données Bonjour Data Lake Store, consultez [afficher les propriétés de hello les données stockées.](data-lake-store-get-started-portal.md#properties)

## <a name="how-do-i-start-using-azure-data-lake-store"></a>Comment commencer à utiliser Azure Data Lake Store ?
Consultez [prise en main à l’aide de Data Lake Store hello Azure Portal](data-lake-store-get-started-portal.md), sur comment tooprovision un à l’aide de Data Lake Store hello portail Azure. Une fois que vous avez configuré Azure Data Lake, vous pouvez apprendre comment toouse les offres de données volumineuses telles qu’Analytique de LAC de données Azure ou Azure HDInsight avec Data Lake Store. Vous pouvez également créer un toocreate d’application .NET à un compte Azure Data Lake Store et effectuer des opérations telles que les données de téléchargement, les données de transfert, etc..

* [Prise en main d'Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Utiliser Azure HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Prise en main d'Azure Data Lake Store avec le Kit de développement logiciel (SDK) .NET](data-lake-store-get-started-net-sdk.md)

## <a name="data-lake-store-videos"></a>Vidéos Data Lake Store
Si vous préférez regarder des vidéos toolearn, Data Lake Store fournit des vidéos sur une gamme de fonctionnalités.

* [Create an Azure Data Lake Store Account (Créer un compte Azure Data Lake Store)](https://mix.office.com/watch/1k1cycy4l4gen)
* [Utilisez hello Explorateur de données tooManage données dans Azure Data Lake Store](https://mix.office.com/watch/icletrxrh6pc)
* [Se connecter Analytique de LAC de données Azure tooAzure Data Lake Store](https://mix.office.com/watch/qwji0dc9rx9k)
* [Access Azure Data Lake Store via Data Lake Analytics](https://mix.office.com/watch/1n0s45up381a8)
* [Se connecter à Azure HDInsight tooAzure Data Lake Store](https://mix.office.com/watch/l93xri2yhtp2)
* [Access Azure Data Lake Store via Hive and Pig (Accéder à Azure Data Lake Store via Hive et Pig)](https://mix.office.com/watch/1n9g5w0fiqv1q)
* [Utilisez tooand de données toocopy DistCp (Hadoop Distributed copie) à partir d’Azure Data Lake Store](https://mix.office.com/watch/1liuojvdx6sie)
* [Utiliser des données de toomove Apache Sqoop entre sources relationnelles et Azure Data Lake Store](https://mix.office.com/watch/1butcdjxmu114)
* [Data Orchestration using Azure Data Factory for Azure Data Lake Store (Orchestration de données pour Azure Data Lake Store à l’aide d’Azure Data Factory)](https://mix.office.com/watch/1oa7le7t2u4ka)
* [Sécurisation des données Bonjour Azure Data Lake Store](https://mix.office.com/watch/1q2mgzh9nn5lx)

