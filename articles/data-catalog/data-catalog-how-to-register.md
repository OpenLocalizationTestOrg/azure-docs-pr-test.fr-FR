---
title: "sources de données aaaRegister dans Azure Data Catalog | Documents Microsoft"
description: "Cet article présente comment tooregister les sources de données dans Azure Data Catalog, y compris les champs de métadonnées hello extraites lors de l’inscription."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: bab89906-186f-4d35-9ffd-61b1d903905d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: efc8a852ddc9fb4bbacc7b0280477bd47814936f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="register-data-sources-in-azure-data-catalog"></a>Inscrire des sources de données dans Azure Data Catalog
## <a name="introduction"></a>Introduction
Azure Data Catalog est un service cloud entièrement géré qui permet d’inscrire et de détecter les sources de données d’entreprise. En d’autres termes, Data Catalog aide les utilisateurs à détecter, comprendre et utiliser les sources de données, et permet aux organisations de mieux exploiter leurs données existantes. première étape toomaking une source de données de Hello détectable via le catalogue de données est tooregister à cette source de données.

## <a name="register-data-sources"></a>Inscription des sources de données
Inscription consiste hello extraction des métadonnées à partir de la source de données hello et la copie de ce service de catalogue de données de toohello données. Hello données demeurent dans lequel il réside actuellement et reste sous contrôle hello des administrateurs de hello et les stratégies du système en cours de hello.

tooregister une source de données, procédez comme hello suivant :
1. Dans le portail Azure Data Catalog hello, démarrez l’outil d’inscription de hello catalogue de données données source. 
2. Connectez-vous avec votre compte professionnel ou scolaire avec hello, mêmes informations d’identification Azure Active Directory que vous utilisez toosign dans toohello portal.
3. Sélectionnez hello source de données tooregister.

Pour plus d’informations détaillées, consultez hello [prise en main Azure Data Catalog](data-catalog-get-started.md) didacticiel.

Une fois que vous avez enregistré la source de données hello, catalogue de hello effectue le suivi de son emplacement et ses métadonnées d’index. Les utilisateurs peuvent rechercher, parcourir et détecter la source de données hello et ensuite utiliser son tooit de tooconnect d’emplacement à l’aide d’application hello ou outil de leur choix.

## <a name="supported-data-sources"></a>Sources de données prises en charge
Pour obtenir la liste des sources de données prises en charge, consultez [Sources de données prises en charge par Azure Data Catalog](data-catalog-dsr.md).

## <a name="structural-metadata"></a>Métadonnée structurelle
Lorsque vous enregistrez une source de données, outil d’inscription de hello extrait des informations sur la structure hello d’objets hello que vous sélectionnez. Ces informations sont les métadonnées structurelles tooas référencé.

Pour tous les objets, ces métadonnées structurelles incluent l’emplacement de l’objet hello, afin que les utilisateurs de découvrir les données hello peuvent utiliser cet objet de toohello tooconnect plus d’informations dans les outils clients hello de leur choix. Parmi les autres métadonnées structurelles, on peut citer le nom et le type d’objet, le nom d’attribut/colonne et le type de données.

## <a name="descriptive-metadata"></a>Métadonnée descriptive
En outre toohello base structurelle métadonnées extraites à partir de la source de données hello, outil de l’enregistrement de source de données hello extrait des métadonnées descriptives. Pour SQL Server Analysis Services et SQL Server Reporting Services, ces métadonnées sont extraite des propriétés de Description hello exposées par ces services. Pour SQL Server, les valeurs fournies à l’aide de hello ms\_description de propriété étendue est extraite. Pour la base de données Oracle, hello source de données d’inscription outil extraits hello commentaires colonne à partir de tous les hello\_onglet\_affichage des commentaires.

Dans Ajout toohello métadonnées descriptives qui sont extraites de la source de données hello, les utilisateurs peuvent entrer des métadonnées descriptives en utilisant l’outil de l’enregistrement de source de données hello. Les utilisateurs peuvent ajouter des balises, et ils peuvent identifier les experts pour les objets hello en cours d’inscription. Toutes les métadonnées de cette description sont copié toohello service de catalogue de données, ainsi que les métadonnées structurelles hello.

## <a name="include-previews"></a>Inclure des aperçus
Par défaut, seules les métadonnées sont extraites de sources de données et copié toohello service de catalogue de données, mais comprendre qu'une source de données est souvent facilitée lorsque vous pouvez afficher un échantillon des données hello qu’il contient.

En utilisant l’outil d’inscription de hello source de données de catalogue de données, vous pouvez inclure un aperçu instantané de données de hello dans chaque table et la vue qui est inscrit. Si vous choisissez les aperçus tooinclude pendant l’inscription, outil d’inscription de hello inclut les enregistrements too20 à partir de chaque table et vue. Cet instantané est ensuite copié catalogue toohello, ainsi que les métadonnées structurelles et descriptif hello.

> [!NOTE]
> Il se peut que l’aperçu des tableaux larges (c’est-à-dire comportant un grand nombre de colonnes) contienne moins de 20 enregistrements.
>
>

## <a name="include-data-profiles"></a>Inclure des profils de données
Tout comme les versions préliminaires, y compris peuvent fournir le contexte précieuse pour les utilisateurs de rechercher des sources de données dans le catalogue de données, y compris un profil des données peut rendre plus facilement des sources de données toounderstand découverts.

En utilisant l’outil d’inscription de hello source de données de catalogue de données, vous pouvez inclure un profil des données pour chaque table et la vue qui est inscrit. Si vous choisissez tooinclude un profil des données pendant l’inscription, outil d’inscription de hello inclut des statistiques sur les données de salutation dans chaque table et vue, y compris :

* nombre de Hello de lignes et de la taille des données hello dans l’objet de hello.
* date de Hello pour hello dernière mise à jour les données de salutation et le schéma d’objet hello.
* nombre de Hello de valeurs distinctes pour les colonnes et les enregistrements null.
* valeurs minimum, maximum, moyenne et écart type Hello pour les colonnes.

Ces statistiques sont ensuite copiés catalogue toohello, ainsi que les métadonnées structurelles et descriptif hello.

> [!NOTE]
> Les colonnes de texte et de date n’incluent pas de statistiques de valeurs moyennes ou d’écart type dans leur profil de données.
>
>

## <a name="update-registrations"></a>Mettre à jour les inscriptions
Inscription d’une source de données rend détectables dans le catalogue de données lorsque vous utilisez les métadonnées hello et facultatif preview extraites lors de l’inscription. Si source de données hello doit toobe mis à jour dans le catalogue (par exemple, si hello le schéma d’un objet a changé, les tables à l’origine exclues doivent être inclus, ou vous souhaitez que les données de hello tooupdate qui sont incluses dans les versions préliminaires de hello) de hello, outil de l’enregistrement de source de données hello peut être réexécutée.

La réinscription d’une source de données déjà inscrite aboutit à une opération de fusion de type « upsert » : les objets existants sont actualisés, tandis que les nouveaux objets sont créés. Toutes les métadonnées fournies par les utilisateurs via le portail de catalogue de données hello sont conservés.

## <a name="summary"></a>Résumé
Puisqu’il copie les métadonnées structurelles et descriptive à partir d’un service de catalogue de source de données toohello, l’inscription de la source de données hello dans le catalogue de données rend toodiscover plus facile de données hello et comprendre. Une fois que vous avez enregistré la source de données hello, vous pouvez annoter, gérer et en le détectant à l’aide du portail de catalogue de données hello.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’inscription des sources de données, consultez hello [prise en main Azure Data Catalog](data-catalog-get-started.md) didacticiel.
