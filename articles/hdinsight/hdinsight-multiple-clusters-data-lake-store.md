---
title: aaaUse HDInsight plusieurs clusters avec un compte Azure Data Lake Store - Azure | Documents Microsoft
description: "Découvrez comment toouse plus d’un HDInsight cluster avec un seul compte Data Lake Store"
keywords: "stockage hdinsight, hdfs, données structurées, données non structurées, data lake store"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: nitinme
ms.openlocfilehash: 3a125b91fcc1e436270a1bd349f7a2d8f27e06fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-multiple-hdinsight-clusters-with-an-azure-data-lake-store-account"></a>Utiliser plusieurs clusters HDInsight avec un compte Azure Data Lake Store

À partir de HDInsight version 3.5, vous pouvez créer des clusters HDInsight avec des comptes Azure Data Lake Store comme système de fichiers par défaut hello.
Data Lake Store prend en charge le stockage illimité qui le rend idéal non seulement pour héberger de grandes quantités de données, mais également pour héberger plusieurs clusters HDInsight qui partagent un même compte Data Lake Store. Pour instructionson comment toocreate un HDInsight de cluster avec Data Lake Store en tant que stockage de hello, consultez [HDInsight de créer des clusters avec Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

Cet article fournit un administrateur du magasin de recommandations toohello lac de données pour la configuration d’un seul et partagées compte Data Lake stocker qui peut être utilisé sur plusieurs **active** clusters HDInsight. Ces recommandations s’appliquent toohosting Hadoop de sécurisé mais aussi non sécurisées plusieurs clusters sur un compte de magasin Data Lake partagé.


## <a name="data-lake-store-file-and-folder-level-acls"></a>ACL de niveau fichier et dossier Data Lake Store

Hello reste de cet article suppose que vous avez une bonne connaissance du niveau de fichier et dossier ACL dans Azure Data Lake Store est décrit en détail à [contrôle d’accès dans Azure Data Lake Store](../data-lake-store/data-lake-store-access-control.md).

## <a name="data-lake-store-setup-for-multiple-hdinsight-clusters"></a>Configuration de Data Lake Store pour plusieurs clusters HDInsight
Faites-nous prendre une hiérarchie de dossiers de deux niveaux de recommandations de hello tooexplain pour l’utilisation des clusters HDInsight de dépendants avec un compte Data Lake Store. Envisagez d’avoir un compte Data Lake Store avec la structure de dossiers hello **/clusters/finance**. Avec cette structure, tous les clusters hello requis par l’organisation de Finance hello peuvent utiliser /clusters/finance comme emplacement de stockage hello. Dans le futur, si une autre organisation, par exemple Marketing, souhaite que les clusters HDInsight toocreate à l’aide de hello même compte Data Lake Store, Impossible de créer des /clusters/marketing de hello. Pour l’instant, nous allons simplement utiliser **/clusters/finance**.

tooenable cette toobe de structure de dossier utilisé efficacement par les clusters HDInsight, administrateur de Data Lake Store hello doit attribuer les autorisations appropriées, comme décrit dans la table de hello. Hello indiqué dans la table de hello correspondent tooAccess-ACL et pas par défaut-ACL. 


|Dossier  |Autorisations  |utilisateur propriétaire  |groupe propriétaire  | Utilisateur nommé | Autorisations de l’utilisateur nommé | Groupe nommé | Autorisations du groupe nommé |
|---------|---------|---------|---------|---------|---------|---------|---------|
|/ | rwxr-x--x  |admin |admin  |Principal du service |--x  |FINGRP   |r-x         |
|/clusters | rwxr-x--x |admin |admin |Principal du service |--x  |FINGRP |r-x         |
|/clusters/finance | rwxr-x--t |admin |FINGRP  |Principal du service |rwx  |-  |-     |

Dans la table de hello,

- **administrateur** est le créateur de hello et administrateur de hello compte Data Lake Store.
- **Principal du service** est hello Azure Active Directory (AAD) principal de service associé au compte de hello.
- **FINGRP** est un groupe d’utilisateurs créé dans AAD qui contient des utilisateurs hello financier.

Pour plus d’informations sur comment toocreate une application AAD (qui crée également un Principal de Service), consultez [créer une application AAD](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application). Pour obtenir des instructions sur la façon dont toocreate un groupe d’utilisateurs dans AAD, consultez [la gestion des groupes dans Azure Active Directory](../active-directory/active-directory-accessmanagement-manage-groups.md).

Tooconsider de certains points clés.

- structure de dossiers de niveau Hello deux (**/clusters/finance/**) doit être créé et configuré avec les autorisations appropriées à hello Data Lake Store admin **avant** à l’aide du compte de stockage hello pour les clusters. Cette structure n’est pas créée automatiquement lors de la création des clusters.
- exemple Hello ci-dessus recommande le paramètre hello propriétaire de groupe de **/clusters/finance** en tant que **FINGRP** et autorisant **r-x** accéder à la hiérarchie de dossiers entière tooFINGRP toohello démarrage à partir de la racine de hello. Cela garantit que les membres de hello de FINGRP peuvent parcourir la structure de dossier hello en commençant à partir de la racine.
- Dans les cas de hello lorsque des principaux de Service AAD différents peuvent créer des clusters sous **/clusters/finance**, hello rémanentes bits (lorsque la valeur sur hello **finance** dossier) permet de s’assurer que les dossiers créés par un Service Principal ne peut pas être supprimé par hello autres.
- Une fois la structure de dossiers hello et les autorisations sont en place, les processus de création du cluster HDInsight crée une loaction de stockage de cluster spécifiques sous **/clusters/finance/**. Par exemple, stockage hello pour un cluster avec hello nom fincluster01 peut être **/clusters/finance/fincluster01**. Hello propriétaire et les autorisations pour les dossiers de hello créés par le cluster HDInsight est indiqué dans la table hello ici.

    |Dossier  |Autorisations  |utilisateur propriétaire  |groupe propriétaire  | Utilisateur nommé | Autorisations de l’utilisateur nommé | Groupe nommé | Autorisations du groupe nommé |
    |---------|---------|---------|---------|---------|---------|---------|---------|
    |/clusters/finance/fincluster01 | rwxr-x---  |Principal de service |FINGRP  |- |-  |-   |-  | 
   


## <a name="recommendations-for-job-input-and-output-data"></a>Recommandations pour les données d’entrée et de sortie de tâche

Nous recommandons d’entrée de travail tooa des données et hello sorties à partir d’un travail d’être stockés dans un dossier en dehors de **/clusters**. Cela garantit que même si le dossier cluster hello est supprimé tooreclaim certains espace de stockage, les entrées du travail hello et les sorties sont toujours disponibles pour une utilisation ultérieure. Dans ce cas, vérifiez que la fonction arborescence des dossiers pour le stockage des entrées et sorties hello travail hello permet un niveau approprié de l’accès pour hello Principal du Service.

## <a name="limit-on-clusters-sharing-a-single-storage-account"></a>Limite sur les clusters partageant un même compte de stockage

Hello hello nombre limite de clusters qui peuvent partager un seul compte Data Lake Store dépend de la charge de travail hello en cours d’exécution sur ces clusters. Avoir trop de clusters ou des charges de travail très importantes sur les clusters hello qui partagent un compte de stockage peut entraîner des tooget d’entrées/sorties du compte de stockage hello limitée.

## <a name="support-for-default-acls"></a>Prise en charge des ACL par défaut

Lorsque vous créez un Principal de Service avec un accès utilisateur nommé (comme indiqué dans le tableau hello ci-dessus), nous vous recommandons de **pas** Ajout hello-utilisateur nommé avec une ACL par défaut. Configuration des accès utilisateur nommé à l’aide des résultats de l’ACL de la valeur par défaut dans l’attribution de 770 autorisations hello pour l’utilisateur propriétaire, groupe propriétaire et d’autres. Bien que la valeur par défaut de 770 ne retire pas les autorisations de l’utilisateur propriétaire (7) ou du groupe propriétaire (7), elle retire les autorisations des autres (0). Cela entraîne un problème connu avec un particulier en cas d’utilisation qui est décrite en détail dans hello [problèmes connus et solutions de contournement](#known-issues-and-workarounds) section.

## <a name="known-issues-and-workarounds"></a>Problèmes connus et solutions de contournement

Cette section répertorie les problèmes connus relatifs à l’aide de HDInsight avec Data Lake Store et leurs solutions de contournement de hello.

### <a name="publicly-visible-localized-yarn-resources"></a>Ressources YARN localisées visibles publiquement

Lorsqu’un compte Azure Data Lake store est créé, répertoire racine de hello est automatiquement configuré avec accès autorisation bits ensemble too770. dossier racine de Hello propriétaire utilisateur est ensemble toohello que hello compte (administrateur de Data Lake Store hello) a été créé et le groupe propriétaire de hello a la valeur toohello de groupe principal de l’utilisateur hello hello compte a été créé. Aucun accès n’est fourni pour les « autres ».

Ces paramètres sont connus tooaffect un spécifique HDInsight-cas capturé dans [fils 247](https://hwxmonarch.atlassian.net/browse/YARN-247). Les soumissions de travail peut échouer avec un toothis similaire de message erreur :

    Resource XXXX is not publicly accessible and as such cannot be part of hello public cache.

Comme indiqué dans hello que fils JIRA lié précédemment, lors de la localisation des ressources publiques, hello localisateur valide que tous les hello ressources demandées sont en effet publics en recherchant dans leurs autorisations sur hello-système de fichiers distant. Les éléments LocalResource qui ne correspondent pas à cette condition sont rejetés pour la localisation. Bonjour de vérification des autorisations, inclut les fichiers toohello d’accès en lecture pour les « autres ». Ce scénario ne fonctionne pas out of box lors de l’hébergement des clusters HDInsight sur Azure Data Lake, étant donné que Azure Data Lake refuse l’accès de tous les « autres » au niveau du dossier racine.

#### <a name="workaround"></a>Solution de contournement
Jeu en lecture-les autorisations d’exécution **d’autres** via la hiérarchie de hello, par exemple, sur  **/** , **/clusters** et   **/clusters/finance**  comme indiqué dans le tableau hello ci-dessus.

## <a name="see-also"></a>Voir aussi

* [Créer un cluster HDInsight avec Data Lake Store comme stockage.](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)


