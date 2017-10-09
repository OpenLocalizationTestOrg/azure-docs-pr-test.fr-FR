---
title: "aaaAzure vue d’ensemble de fonctions Runtime | Documents Microsoft"
description: "Vue d’ensemble de hello Azure en version préliminaire fonctions Runtime"
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
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 8ce3e5037731d499c330b395c89c90109d18d65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-runtime-overview"></a>Vue d’ensemble du runtime d’Azure Functions

Bonjour Azure fonctions Runtime fournit un moyen de nouveau pour vous tootake parti de hello simplicité et souplesse de fonctions d’Azure hello local de modèle de programmation. Reposant sur hello même ouvrir des racines de la source comme fonctions d’Azure, Azure fonctions Runtime est tooprovide déployés localement un développement quasiment identique expérience en tant que service de cloud computing hello.

![Portail du runtime d’Azure Functions en version préliminaire][1]

Bonjour Azure fonctions Runtime fournit un moyen pour vous tooexperience Azure fonctions avant de les valider toohello cloud. De cette façon, les ressources de code hello que vous créez peuvent être utilisées avec le cloud de toohello vous lorsque vous migrez.  Hello runtime ouvre également de nouvelles options, telles que l’utilisation de puissance de calcul de rechange hello de vos processus de lot local ordinateurs toorun pendant la nuit. Vous pouvez également utiliser des périphériques au sein de votre organisation tooconditionally envoi données tooother les systèmes, à la fois localement et dans le cloud de hello.

Bonjour Azure fonctions Runtime comprend deux parties :
* Rôle de gestion du runtime d’Azure Functions
* Rôle de travail du runtime d’Azure Functions

## <a name="azure-functions-management-role"></a>Rôle de gestion d’Azure Functions

Hello rôle de fonctions de gestion Azure fournit un hôte pour la gestion de vos fonctions localement hello. Ce rôle effectue hello tâches suivantes :

* Hébergement de hello fonctions portail de gestion, qui est hello hello identique à celle présentée dans hello [portail Azure](https://portal.azure.com). Ce vous permet de développer de vos fonctions dans hello même façon que vous le feriez dans hello portail Azure.
* Répartition des fonctions entre plusieurs Workers Functions.
* Mise à disposition d’un point de terminaison de publication pour vous permettre de publier vos fonctions directement à partir de Microsoft Visual Studio.

## <a name="azure-functions-worker-role"></a>Rôle de travail d’Azure Functions

Rôles de travail de fonctions Azure Hello sont déployés dans les conteneurs Windows et Voici où s’exécute votre code de fonction.  Vous pouvez déployer plusieurs rôles de travail au sein de votre organisation. Il s’agit là d’une solution clé grâce à laquelle les clients peuvent utiliser la puissance de calcul de secours.

## <a name="minimum-requirements"></a>Configuration minimale requise

tooget main hello Azure fonctions Runtime, vous devez disposer d’un ordinateur avec **Windows Server 2016 ou mise à jour de Windows 10 créateurs** avec accès tooa **SQL Server** instance.

## <a name="next-steps"></a>Étapes suivantes

Installer hello [aperçu de l’exécution de fonctions Azure](https://aka.ms/azafr)

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
