---
title: "Vue d’ensemble d’App Service : Azure Stack | Microsoft Docs"
description: "Vue d’ensemble d’App Service sur Azure Stack"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: anwestg
ms.openlocfilehash: 1d763f592212b3a2dcc2f03ebe317eed84e9e2de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-on-azure-stack-overview"></a>Vue d’ensemble d’App Service sur Azure Stack

Service d’applications Azure sur la pile de Azure est hello Azure offre de remise tooAzure pile. Hello du Service d’applications sur le programme d’installation de la pile de Azure crée hello ensemble d’instances de rôle suivant :

*  Controller
*  Gestion (deux instances sont créées)
*  FrontEnd
*  Éditeur
*  Worker (en mode Partagé)

En outre, hello du Service d’applications sur le programme d’installation de la pile de Azure crée un serveur de fichiers.
    
## <a name="whats-new-in-hello-first-release-candidate-of-app-service-on-azure-stack"></a>Quelles sont les nouveautés dans hello première version finale du Service d’application sur la pile de Azure ?
![Service d’applications dans le portail d’Azure pile hello][1]

Hello première version finale du Service d’application sur Azure pile s’appuie sur une version préliminaire de tiers hello et apporte des améliorations et nouvelles fonctionnalités :

* Environnements Azure Functions dans Azure Stack basés sur AD FS 
* L’authentification unique prend en charge pour le portail de fonctions hello et hello des outils de développement avancées (Kudu)
* Prise en charge de Java pour les applications web, mobiles et d’API
* Gestion des niveaux de workers à l’échelle de machines virtuelles définit les fonctionnalités de montée en puissance parallèle tooimprove aux administrateurs de service
* Localisation de l’expérience de l’administrateur hello
* Stabilité accrue du service de hello
* Mises à jour de l’expérience du portail du locataire et mises à jour du processus d’installation

## <a name="limitations-of-hello-technical-preview"></a>Limitations de la version d’évaluation technique hello

Il n’existe aucune prise en charge pour hello du Service d’applications sur des versions préliminaires de Azure pile, bien que nous surveillez hello Forum MSDN de pile Azure. Ne placez aucune charge de travail de production dans cette préversion. Il n’existe également aucune mise à niveau entre les préversions App Service sur Azure Stack. Hello principal à des fins de ces versions préliminaires sont tooshow que nous fournissons et tooobtain commentaires. 

## <a name="what-is-an-app-service-plan"></a>Qu’est-ce qu’un plan App Service ?

Hello fournisseur de ressources du Service d’applications utilise hello même code que le Service d’applications Azure utilise. Par conséquent, il peut être utile de décrire certains concepts communs. Dans le Service d’application, hello tarification conteneur pour les applications est appelée hello plan App Service. Il représente le jeu hello d’utiliser des machines virtuelles dédiées toohold vos applications. Vous pouvez avoir plusieurs plans App Service dans un abonnement donné. 

Dans Azure, il existe des Workers partagés et dédiés. Un Worker partagé prend en charge l’hébergement d’applications mutualisées à densité élevée et il n'existe qu’un seul ensemble de Workers partagés. Les serveurs dédiés sont utilisés par un seul locataire et se présentent dans trois tailles : petit, moyen et grand. besoins Hello de clients de locale ne peut pas toujours être décrits à l’aide de ces termes. Dans le Service d’application sur la pile d’Azure, administrateurs de fournisseur de ressources peuvent définir les niveaux de workers hello qu’ils souhaitent toomake disponible. Les administrateurs peuvent définir plusieurs jeux de Workers partagés ou des jeux différents de Workers dédiés selon leurs besoins d’hébergements uniques. À l’aide de ces définitions de niveau Worker, ils peuvent ensuite définir leurs propres références de tarification.

## <a name="portal-features"></a>Fonctionnalités du portail

Service d’applications sur Azure pile utilise hello même interface utilisateur qui utilise Azure App Service, même avec hello back end. Certaines fonctionnalités sont désactivées et ne sont pas fonctionnelles dans Azure Stack. Hello des exigences spécifiques de Azure ou services qui requièrent de ces fonctionnalités ne sont pas encore disponibles dans la pile de Azure. 

## <a name="next-steps"></a>Étapes suivantes

- [Avant de commencer avec App Service sur Azure Stack](azure-stack-app-service-before-you-get-started.md)
- [Installer hello fournisseur de ressources du Service d’applications](azure-stack-app-service-deploy.md)

Vous pouvez également essayer l’autre [plateforme en tant que service (PaaS) services](azure-stack-tools-paas-services.md), comme hello [fournisseur de ressources SQL Server](azure-stack-sql-resource-provider-deploy.md) et hello [fournisseur de ressources MySQL](azure-stack-mysql-resource-provider-deploy.md).

<!--Image references-->
[1]: ./media/azure-stack-app-service-overview/AppService_Portal.png
