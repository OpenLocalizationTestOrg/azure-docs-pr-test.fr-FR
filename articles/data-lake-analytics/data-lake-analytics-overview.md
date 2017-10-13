---
title: Vue d'ensemble de Microsoft Azure Data Lake Analytics | Microsoft Docs
description: "Data Lake Analytics est un service de Big Data Azure qui vous permet de gérer votre entreprise en exploitant les informations issues de vos données dans le cloud, quels que soient leur taille ou leur emplacement."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 1e1d443a-48a2-47fb-bc00-bf88274222de
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/23/2017
ms.author: saveenr
ms.openlocfilehash: 8817b511d779029421491194b50120d51ec9dbad
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="overview-of-microsoft-azure-data-lake-analytics"></a>Vue d'ensemble de Microsoft Azure Data Lake Analytics
## <a name="what-is-azure-data-lake-analytics"></a>Définition d'Azure Data Lake Analytics
Azure Data Lake Analytics est un service de travaux d’analyse à la demande, qui simplifie l’analyse du Big Data. Vous pouvez vous concentrer sur l’écriture, l’exécution et la gestion des travaux, plutôt que sur le fonctionnement de l’infrastructure distribuée. Au lieu de déployer, de configurer et d’optimiser le matériel, vous écrivez des requêtes pour transformer vos données et en extraire des informations pertinentes. Le service d’analyse peut traiter les travaux instantanément, quelle qu’en soit l’échelle, en définissant le compteur sur la puissance requise. Vous payez les travaux uniquement lorsque ceux-ci sont exécutés, ce qui rend le service économique. Le service d’analyse prend en charge Azure Active Directory, ce qui vous permet de gérer les accès et les rôles et de bénéficier d’une intégration à votre système d’identité local. Il inclut également U-SQL, un langage qui associe les avantages de SQL avec la puissance d'expression du code utilisateur. Le runtime distribué et évolutif d’U-SQL vous permet d’analyser efficacement les données situées dans le magasin et sur les serveurs SQL Server dans Azure, Azure SQL Database et Azure SQL Data Warehouse.

## <a name="key-capabilities"></a>Fonctionnalités clés
* **Mise à l'échelle dynamique**
  
    Data Lake Analytics a été conçu pour fournir des performances et une mise à l’échelle dans le cloud.  Il approvisionne dynamiquement les ressources et vous permet d'analyser plusieurs téraoctets voire exaoctets de données. Lorsque le travail est terminé, le service ralentit automatiquement les ressources et vous payez uniquement la puissance de traitement utilisée. Il n’est pas nécessaire de réécrire le code à mesure que vous augmentez ou diminuez la taille des données stockées ou le volume des ressources de calcul utilisé. Vous pouvez vous concentrer uniquement sur votre logique métier, et non sur la manière dont vous traitez et stockez les jeux de données volumineux.
* **Développez plus rapidement, déboguez et optimisez de manière plus intelligente à l’aide d’outils familiers**
  
    L’étroite intégration de Data Lake Analytics avec Visual Studio vous permet d’utiliser des outils familiers pour exécuter, déboguer et optimiser votre code. Les visualisations de vos travaux U-SQL vous permettent de voir la façon dont votre code est exécuté à l'échelle. Vous pouvez ainsi facilement identifier les goulots d'étranglement en matière de performances et optimiser les coûts.
* **U-SQL : simple et familier, puissant et extensible**
  
    Data Lake Analytics inclut U-SQL, un langage de requête qui étend la nature connue, simple, déclarative de SQL avec la puissance d'expression de C#. Le langage U-SQL est basé sur le runtime distribué qui alimente les systèmes Big Data au sein de Microsoft. Des millions de développeurs SQL et .NET peuvent désormais traiter et analyser leurs données avec les compétences dont ils disposent.
* **S'intègre de façon transparente avec vos investissements informatiques**
  
    Data Lake Analytics peut utiliser vos investissements informatiques existants pour l'identité, la gestion, la sécurité et l'entreposage des données. Cette approche simplifie la gouvernance des données et facilite l’extension de vos applications de données actuelles. Data Lake Analytics est intégré à Active Directory pour les autorisations et la gestion des utilisateurs. Il est fourni avec des capacités de surveillance et d’audit intégrées.
* **Abordable et économique**
  
    Data Lake Analytics est une solution économique permettant d'exécuter vos charges de travail Big Data. Vous payez pour chaque travail au cours duquel des données sont traitées. Aucun matériel, aucune licence ni aucun contrat de support technique propre au service ne sont requis. Le système est mis à l’échelle automatiquement au démarrage du travail puis à la fin de son exécution de sorte que vous ne payez que ce dont vous avez réellement besoin.
* **Fonctionne avec toutes vos données Azure**
  
    Data Lake Analytics a été optimisé pour fonctionner avec Azure Data Lake, offrant ainsi un niveau de performances, de débit et de parallélisation optimal pour vos charges de travail de Big Data.  Data Lake Analytics est également utilisable avec le stockage Blob Azure et Azure SQL Database.

## <a name="next-steps"></a>Étapes suivantes
 
  * Prise en main de Data Lake Analytics à l’aide du [portail Azure](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI](data-lake-analytics-get-started-cli2.md)
  * Gérer Data Lake Analytics à l’aide du [portail Azure](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md) | [Kit de développement logiciel (SDK) Azure .NET](data-lake-analytics-manage-use-dotnet-sdk.md) | [Node.js](data-lake-analytics-manage-use-nodejs.md)
  * [Surveiller et résoudre les problèmes des tâches Azure Data Lake Analytics à l’aide du portail Azure](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md) 
