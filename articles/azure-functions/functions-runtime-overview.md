---
title: "Vue d’ensemble du runtime d’Azure Functions | Microsoft Docs"
description: "Vue d’ensemble du runtime d’Azure Functions en version préliminaire"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/28/2017
ms.author: anwestg
ms.openlocfilehash: 557f071e2cd8d4f639c881274e6e74a8fb745859
ms.sourcegitcommit: a48e503fce6d51c7915dd23b4de14a91dd0337d8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2017
---
# <a name="azure-functions-runtime-overview"></a>Vue d’ensemble du runtime d’Azure Functions

Le runtime d’Azure Functions vous fournit une nouvelle façon de tirer parti de la simplicité et de la flexibilité du modèle de programmation Azure Functions sur site. Basé sur les mêmes racines open source qu’Azure Functions, le runtime d’Azure Functions est déployé sur site pour fournir une expérience de développement quasiment identique à celle du service cloud.

![Portail du runtime d’Azure Functions en version préliminaire][1]

Le runtime d’Azure Functions vous permet de découvrir Azure Functions avant même d’adopter le cloud. De cette façon, les ressources de code que vous créez peuvent ensuite être dirigées sur le cloud lors de la migration.  Le runtime vous donne également accès à de nouvelles options, comme l’utilisation de la puissance de calcul de secours de vos ordinateurs locaux pour exécuter des traitements par lots pendant la nuit. Vous pouvez également utiliser des appareils au sein de votre organisation pour envoyer de manière conditionnelle des données à d’autres systèmes, sur site et sur le cloud.

Le runtime d’Azure Functions se compose de deux éléments :

* Rôle de gestion du runtime d’Azure Functions
* Rôle de travail du runtime d’Azure Functions

## <a name="azure-functions-management-role"></a>Rôle de gestion d’Azure Functions

Le rôle de gestion d’Azure Functions fournit un hôte pour la gestion de vos fonctions sur site. Ce rôle effectue les tâches suivantes :

* Hébergement du portail de gestion Azure Functions, qui est identique à celui que vous voyez dans le [portail Azure](https://portal.azure.com). Ce portail offre une expérience uniforme qui vous permet de développer vos fonctions de la même manière que vous le feriez dans le portail Azure.
* Répartition des fonctions entre plusieurs Workers Functions.
* Mise à disposition d’un point de terminaison de publication pour vous permettre de publier vos fonctions directement à partir de Microsoft Visual Studio, en téléchargeant et en important le profil de publication.

## <a name="azure-functions-worker-role"></a>Rôle de travail d’Azure Functions

Les rôles de travail d’Azure Functions sont déployés dans des conteneurs Windows et se trouvent là où le code de votre fonction s’exécute.  Vous pouvez déployer plusieurs rôles de travail au sein de votre organisation, cette option représente un excellent moyen par le biais duquel les clients peuvent utiliser la puissance de calcul inutilisée.  Un exemple où l’on trouve cette réserve de calcul dans de nombreuses entreprises sont les ordinateurs mis sous tension en permanence et qui demeurent inutilisés pendant de longues périodes.

## <a name="minimum-requirements"></a>Configuration minimale requise

Pour bien démarrer avec le runtime Azure Functions, vous devez disposer d’une machine Windows Server 2016 ou Windows 10 Creators Update avec accès à une instance SQL Server.

## <a name="next-steps"></a>Étapes suivantes

Installer la [préversion du runtime d’Azure Functions](https://aka.ms/azafrdoc)

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
