---
title: "AAA » Azure Analysis Services Adventure Works didacticiel | Documents Microsoft »"
description: "Présente le didacticiel d’Adventure Works hello pour Azure Analysis Services"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: 2df8b3ab4e8c4ffbe0086418d60fd2e2abd35e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-analysis-services---adventure-works-tutorial"></a>Azure Analysis Services - Didacticiel Adventure Works

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Ce didacticiel inclut des leçons sur la façon de toocreate et déployer un modèle tabulaire au niveau de compatibilité hello 1400 à l’aide de [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  

Si vous êtes nouveaux Services tooAnalysis et modélisation tabulaire, ils auront terminé ce didacticiel est toolearn moyen le plus rapide de hello comment toocreate et déployer un modèle tabulaire de base. Une fois que vous disposez des prérequis de hello sur place, il doit prendre entre deux toocomplete d’heures toothree.  
  
## <a name="what-you-learn"></a>Contenu   
  
-   Comment toocreate un nouveau modèle tabulaire de projet à hello **le niveau de compatibilité 1400** dans SSDT.
  
-   Comment tooimport des données à partir d’une base de données relationnelle dans un projet de modèle tabulaire.  
  
-   Comment toocreate et gérer les relations entre les tables dans le modèle de hello.  
  
-   Mode toocreate de calcul des colonnes, mesures et indicateurs de Performance clés qui aideront les utilisateurs analyser des métriques commerciales critiques.  
  
-   Comment toocreate et gérer des perspectives et des hiérarchies qui aideront les utilisateurs plus facilement parcourir les données de modèle en fournissant l’entreprise et les points de vue spécifiques à l’application.  
  
-   Comment toocreate les partitions qui divisent les données de table en parties logiques plus petites qui peuvent être traitées indépendamment des autres partitions.  
  
-   Comment toosecure modèle des objets et des données en créant des rôles avec des membres de l’utilisateur.  
  
-   Comment toodeploy un modèle tabulaire de tooan **Azure Analysis Services** serveur ou un serveur de SQL Server 2017 Analysis Services local.  
  
## <a name="prerequisites"></a>Composants requis  
toocomplete ce didacticiel, vous devez :  
  
-   Un Azure Analysis Services ou SQL Server 2017 Analysis Services instance toodeploy votre modèle. Inscrivez-vous pour bénéficier d’un [essai gratuit d’Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) et [créez un serveur](../analysis-services-create-server.md). Ou inscrivez-vous et téléchargez [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp). 

-   Un entrepôt de données SQL Server ou d’un entrepôt de données SQL Azure avec hello [base de données exemple AdventureWorksDW2014](http://go.microsoft.com/fwlink/?LinkID=335807). Cette base de données exemple inclut toocomplete nécessaires des données de hello ce didacticiel. Téléchargez les [éditions gratuites de SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads). Ou inscrivez-vous pour obtenir un [essai gratuit d’Azure SQL Database](https://azure.microsoft.com/services/sql-database/). 

    **Important :** si vous installez la base de données exemple hello sur un ordinateur local SQL Server et de déploiement de votre serveur Azure Analysis Services de tooan de modèle, un [passerelle de données locale](../analysis-services-gateway.md) est requis.

-   version la plus récente de Hello [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

-   version la plus récente de Hello [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).    

-   Une application cliente telle que [Power BI Desktop](https://powerbi.microsoft.com/desktop/) ou Excel. 

## <a name="scenario"></a>Scénario  
Ce didacticiel repose sur la société fictive Adventure Works Cycles. Adventure Works est une société de fabrication volumineuse, multinationale qui produit et distribue des bicyclettes, les parties et les marchés de toocommercial accessoires en Amérique du Nord, Europe et Asie. société de Hello emploie des 500 travailleurs. Par ailleurs, Adventure Works emploie plusieurs équipes commerciales régionales pour couvrir son marché. Votre projet est toocreate un modèle tabulaire pour les utilisateurs ventes et marketing tooanalyze données des ventes Internet dans la base de données AdventureWorksDW hello.  
  
didacticiel de hello toocomplete, vous devez effectuer plusieurs leçons. Chaque leçon comprend des tâches. Chaque tâche dans l’ordre est nécessaire pour terminer la leçon de hello. Une leçon peut comporter plusieurs tâches qui aboutissent au même résultat, mais la façon d’exécuter chaque tâche diffère légèrement. Cette affiche de méthode, il existe souvent plus d’une façon toocomplete une tâche et toochallenge vous à l’aide de compétences vous avez appris dans les tâches et les leçons précédentes.  
  
Hello vise les leçons hello tooguide vous guide dans la création d’un modèle tabulaire de base à l’aide de nombreuses fonctionnalités de hello inclus dans SSDT. Étant donné que chaque leçon repose sur la leçon précédente de hello, vous devez effectuer les leçons hello dans l’ordre.
  
Ce didacticiel ne fournit pas les données de modèle d’application toobrowse leçons sur la gestion d’un serveur dans le portail Azure, la gestion d’un serveur ou une base de données à l’aide de SSMS, ou à l’aide d’un client. 


## <a name="lessons"></a>Leçons  
Ce didacticiel inclut hello suivant leçons :  
  
|Leçon|Durée estimée toocomplete|  
|----------|------------------------------|  
|[1 - Créer un nouveau projet de modèle tabulaire](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)|10 minutes|  
|[2 - Obtenir des données](../tutorials/aas-lesson-2-get-data.md)|10 minutes|  
|[3 - Marquer en tant que Table de dates](../tutorials/aas-lesson-3-mark-as-date-table.md)|3 minutes|  
|[4 - créer des relations](../tutorials/aas-lesson-4-create-relationships.md)|10 minutes|  
|[5 - Créer des colonnes calculées](../tutorials/aas-lesson-5-create-calculated-columns.md)|15 minutes|
|[6 - Créer des mesures](../tutorials/aas-lesson-6-create-measures.md)|30 minutes|  
|[7 - Créer des indicateurs de performance clés (KPI)](../tutorials/aas-lesson-7-create-key-performance-indicators.md)|15 minutes|  
|[8 - Créer des perspectives](../tutorials/aas-lesson-8-create-perspectives.md)|5 minutes|  
|[9 - Créer des hiérarchies](../tutorials/aas-lesson-9-create-hierarchies.md)|20 minutes|  
|[10 - Créer des partitions](../tutorials/aas-lesson-10-create-partitions.md)|15 minutes|  
|[11 - Créer des rôles](../tutorials/aas-lesson-11-create-roles.md)|15 minutes|  
|[12 - Analyser dans Excel](../tutorials/aas-lesson-12-analyze-in-excel.md)|5 minutes| 
|[13 - Déployer](../tutorials/aas-lesson-13-deploy.md)|5 minutes|  
  
## <a name="supplemental-lessons"></a>Leçons supplémentaires  
Ces leçons ne sont pas didacticiel de hello toocomplete requis, mais il peuvent être utiles pour une meilleure compréhension modèle tabulaire avancé fonctionnalités de création.  
  
|Leçon|Durée estimée toocomplete|  
|----------|------------------------------|  
|[Lignes de détails](../tutorials/aas-supplemental-lesson-detail-rows.md)|10 minutes|
|[Sécurité dynamique](../tutorials/aas-supplemental-lesson-dynamic-security.md)|30 minutes|
|[Hiérarchies déséquilibrées](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)|20 minutes| 

  
## <a name="next-steps"></a>Étapes suivantes  
tooget démarré, consultez [leçon 1 : créer un projet de modèle tabulaire](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).  
  
  
  

