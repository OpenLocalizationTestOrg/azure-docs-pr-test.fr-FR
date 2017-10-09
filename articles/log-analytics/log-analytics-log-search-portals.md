---
title: "aaaPortals pour créer et modifier des requêtes de journal dans l’Analytique des journaux Azure | Documents Microsoft"
description: "Cet article décrit les portails hello que vous pouvez utiliser dans Azure journal Analytique toocreate et modifier des recherches de journal."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 7a2657574a132b2c4298511bb31259e68113ac91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="portals-for-creating-and-editing-log-queries-in-azure-log-analytics"></a>Portails servant à la création et la modification des requêtes de journal dans Azure Log Analytics

> [!NOTE]
> Cet article décrit les portails dans Azure Analytique de journal à l’aide du nouveau langage de requête hello.  Vous pouvez en savoir plus sur le nouveau langage de hello et obtenir hello procédure tooupgrade votre espace de travail à [mise à niveau de votre recherche de journal toonew espace de travail Analytique des journaux Azure](log-analytics-log-search-upgrade.md).  
>
> Si votre espace de travail n’a pas été mis à niveau toohello nouveau langage de requête, vous devez faire référence trop[trouver des données à l’aide de recherches de journal dans le journal Analytique](log-analytics-log-searches.md) pour plus d’informations sur la version actuelle de hello du portail de recherche de journal hello.

Vous utilisez des recherches de journaux dans plusieurs emplacements dans l’ensemble de données de tooretrieve Analytique de journal à partir de l’espace de travail hello.  Pour créer et modifier des requêtes de réellement en outre tooworking interactive avec a retourné des données via, vous avez deux options sont décrites ci-dessous.  

## <a name="log-search-portal"></a>Portail de recherche dans les journaux
portail de recherche de journal Hello est accessible à partir de hello portail Azure ou du portail OMS hello.  Il convient pour la création de requêtes de base pouvant être créées sur une seule ligne.  portail de recherche de journal Hello peut être utilisé sans lancer un portail externe, et vous pouvez l’utiliser tooperform diverses fonctions avec des recherches de journaux, y compris la création de règles d’alerte, la création de groupes d’ordinateurs et l’exportation des résultats de requête de hello hello.  

portail de recherche de journal Hello fournit plusieurs fonctionnalités pour la modification de requête de hello sans avoir une connaissance complète du langage de requête hello.  Vous pouvez obtenir un résumé de ces fonctionnalités dans [créer des recherches de journaux dans Azure Analytique de journal à l’aide du portail de recherche de journal hello](log-analytics-log-search-log-search-portal.md).


![Portail de recherche dans les journaux](media/log-analytics-log-search-portals/log-search-portal.png)

## <a name="advanced-analytics-portal"></a>Portail Analytics avancé
portail d’Analytique avancée Hello est un portail dédié qui fournit des fonctionnalités avancées non disponibles dans le portail de recherche de journal hello.  Fonctionnalités incluent la possibilité de hello tooedit une requête sur plusieurs lignes, exécuter une sélection de code, Intellisense sensible au contexte et Analytique actives.  portail d’Analytique de Advanced Hello se révèle particulièrement adaptée pour concevoir des requêtes complexes qui sont soit enregistrés sous la forme d’une recherche de journal ou copiées et collées dans les autres éléments de journal Analytique.  Vous lancez le portail d’Analytique de Advanced hello à partir d’un lien dans le portail de recherche de journal hello.

![Portail Analytics avancé](media/log-analytics-log-search-portals/advanced-analytics-portal.png)


En raison de ses fonctionnalités avancées, vous utiliserez généralement portal d’Analytique avancée hello comme votre principal outil de création et modification des requêtes.  Une fois que vous avez déterminé que les requête hello fonctionnent comme prévu, puis vous copiez et collez d’ailleurs tels que le portail de recherche de journal hello ou le Concepteur de vue.  Portail d’Analytique de Advanced hello prenant en charge des requêtes avec plusieurs lignes Cependant, vous devez tootake hello règles suivantes lors de la copie d’une requête à partir de ce portail.

- Commentaires doivent être supprimés à partir de la requête de hello avant est copié et collé dans un autre emplacement.  Vous pouvez commenter une ligne en la précédant de deux barres obliques (//).  Lorsque vous collez une requête de lignes multiples dans une seule ligne, les sauts de ligne sont supprimés.  Si les commentaires sont inclus, tous les caractères après le premier commentaire de hello sont considérées comme partie du commentaire de hello.


## <a name="next-steps"></a>Étapes suivantes

- Suivre un didacticiel sur l’utilisation de hello [portal de recherche de journal](log-analytics-log-search-log-search-portal.md) ou hello [portal d’Analytique de Advanced](https://go.microsoft.com/fwlink/?linkid=856587) toocreate requêtes.
- Extraire un [didacticiel sur l’écriture de requêtes](https://go.microsoft.com/fwlink/?linkid=856078) à l’aide du nouveau langage de requête hello.
