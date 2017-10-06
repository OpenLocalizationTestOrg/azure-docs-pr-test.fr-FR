---
title: aaaHow tooScale une application dans un environnement App Service
description: "Mise à l'échelle d'une application dans un environnement App Service"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: jimbe
ms.assetid: 78eb1e49-4fcd-49e7-b3c7-f1906f0f22e3
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: ccompy
ms.openlocfilehash: 08916eac056c46bf8cb6edffbf96285317b32062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-apps-in-an-app-service-environment"></a>Mise à l'échelle des applications dans un environnement App Service
Bonjour Azure App Service, il existe généralement trois choses, que vous pouvez mettre à l’échelle :

* Plan de tarification
* Taille du travail 
* Nombre d'instances

Dans un environnement app service n’est aucun hello tooselect ou modification besoin de plan de tarification.  En termes de fonctionnalités, il est déjà au niveau de tarification Premium.  

En ce qui concerne les tailles tooworker, hello ASE admin permet d’affecter taille hello de toobe de ressources de calcul hello utilisé pour chaque pool de travail.  Cela signifie que vous pouvez avoir le pool de travaux 1 avec les ressources de calcul P4 et le pool de travaux 2 avec les ressources de calcul P1, si vous le souhaitez.  Ils n’ont pas de toobe dans l’ordre de taille.  Pour plus d’informations sur les tailles de hello et la tarification, consultez document hello ici [tarification d’Azure App Service][AppServicePricing].  Cela laisse hello mise à l’échelle des options pour les applications web et les Plans de Service d’application dans un environnement App Service de toobe :

* Sélection du pool de travaux
* Nombre d'instances

Modification de des éléments est effectuée via hello approprié à l’interface utilisateur pour votre ASE hébergé Plans de Service d’application.  

![][1]

Vous ne pouvez pas puissance votre ASP au-delà de nombre hello disponible des ressources de calcul dans le pool de travail hello figurant dans vos pages ASP.  Si vous avez besoin de ressources de calcul dans ce pool de travail vous devez tooget votre tooadd d’administrateur ASE les.  Pour lire les informations autour de reconfigurer votre ASE informations hello ici : [comment tooConfigure un environnement App Service][HowtoConfigureASE].  Vous pouvez également parti tootake Hello ASE échelle fonctionnalités tooadd la capacité en fonction de la planification ou les métriques.  tooget plus d’informations sur la configuration de mise à l’échelle pour l’environnement hello ASE lui-même consultez [la mise à l’échelle de tooconfigure pour un environnement App Service][ASEAutoscale].

Vous pouvez créer une application plusieurs plans de service à l’aide des ressources de calcul à partir des pools de travail différent, ou vous pouvez utiliser hello même pool de travail.  Pour exemple, si vous avez les ressources de calcul disponibles (10) dans le processus de travail Pool 1, vous pouvez choisir toocreate plan de service d’une application à l’aide des ressources de calcul (6), et un deuxième service application plan qui utilise les ressources de calcul (4).

### <a name="scaling-hello-number-of-instances"></a>Mise à l’échelle de nombre hello d’instances
Lorsque vous créez votre application web dans un environnement App Service, elle ne contient qu’1 instance.  Vous pouvez ensuite la montée en puissance parallèle tooadditional tooprovide d’instances supplémentaire de calcul ressources pour votre application.   

Si votre environnement Application Service a une capacité suffisante, l'opération est assez simple.  Vous allez tooyour Plan App Service contenant des sites hello vous le souhaitez tooscale haut et sélectionnez la mise à l’échelle.  Hello l’interface utilisateur où vous pouvez manuellement définir montée en puissance hello pour vos pages ASP ou configurer des règles de mise à l’échelle pour votre ASP s’ouvre.  mise à l’échelle toomanually votre application simplement définie ***l’échelle*** trop***un nombre d’instances que j’entre manuellement***.  À partir d’ici faites glisser quantity de toohello souhaité de curseur hello ou saisir dans le curseur de toohello suivant hello boîte.  

![][2] 

règles de mise à l’échelle Hello pour une page ASP dans un travail ASE hello identiques car ils ne normalement.  Vous pouvez sélectionner ***Pourcentage UC*** sous ***Mise à l'échelle selon*** et créer des règles de mise à l'échelle automatique de votre ASP basées sur le pourcentage UC ou vous pouvez créer des règles plus complexes à l'aide des ***règles de performances et de planification***.  toosee effectuer plus de détails sur la configuration de mise à l’échelle utilisez hello guide [l’échelle d’une application dans Azure App Service][AppScale]. 

### <a name="worker-pool-selection"></a>Sélection du pool de travaux
Comme indiqué précédemment, sélection de pool de travail hello est accessible à partir de hello ASP UI.  Ouvrez le panneau hello pour hello ASP que vous souhaitez tooscale et que vous sélectionnez le pool de travail.  Vous verrez tous les pools de travail hello dont vous avez configuré dans votre environnement App Service.  Si vous avez seulement un worker pool puis vous verrez seulement un seul pool hello répertorié.  toochange le travail du pool votre ASP dans, vous sélectionnez simplement le pool de travail hello vous souhaitez que votre toomove Plan App Service pour.  

![][3]

Avant de déplacer votre ASP à partir d’un seul worker pool tooanother, il est important toomake sûr de qu'avoir une capacité suffisante pour vos pages ASP.  Dans la liste de hello des pools de travail, non seulement est le nom de pool de travail de hello répertorié, mais vous pouvez également voir le nombre de threads de travail sont disponibles dans ce pool de travail.  Assurez-vous qu’il y a suffisamment toocontain disponible instances votre Plan App Service.  Si vous avez besoin des ressources dans le pool de travail hello de calcul plus vous souhaitez toomove pour, puis obtenir votre tooadd d’administrateur ASE les.  

> [!NOTE]
> Déplacement de qu'une page ASP à partir d’un travail du pool entraîne à froid démarre d’applications que ASP hello.  Cela peut entraîner des demandes toorun lentement que votre application est à froid démarré sur les nouvelles ressources de calcul hello.  Hello démarrage à froid peut être évitée à l’aide de hello [application préchauffage capacité] [ AppWarmup] dans Azure App Service.  module d’initialisation de l’Application Hello décrit dans l’article hello fonctionne également pour un démarrage à froid, car le processus d’initialisation hello est également appelé lorsque des applications sont à froid démarré sur les nouvelles ressources de calcul. 
> 
> 

## <a name="getting-started"></a>Prise en main
tooget démarré avec les environnements de Service d’application, consultez [comment tooCreate un environnement App Service][HowtoCreateASE]

Pour plus d’informations sur la plateforme Azure App Service de hello, consultez [Azure App Service][AzureAppService].

<!--Image references-->
[1]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-aspblade.png
[2]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-manualscale.png
[3]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-sizescale.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ScaleWebapp]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[CreateWebappinASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-a-web-app-in-an-ase/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[AppScale]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[AppWarmup]: http://ruslany.net/2015/09/how-to-warm-up-azure-web-app-during-deployment-slots-swap/
