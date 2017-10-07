---
title: aaaGet en main de test en production pour les applications Web
description: "Découvrez hello Test dans la fonctionnalité de Production (TiP) dans Azure App Service Web Apps."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 4623468d-886e-4203-8012-8f86deb2790b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: cephalin
ms.openlocfilehash: 2ddbd532ffe2a4f3e07fd386d9741a3fde3639ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-test-in-production-for-web-apps"></a>Prise en main de la fonction de test en production pour les applications web
Le test en production, ou test en direct de votre application web à l’aide du trafic client en direct, est une stratégie de test que les développeurs d’applications intègrent de plus en plus à leur méthodologie de [développement agile](https://en.wikipedia.org/wiki/Agile_software_development) . Il vous permet de qualité de hello tootest de vos applications avec le trafic des utilisateurs en direct dans votre environnement de production, en tant que données toosynthesized exécutée dans un environnement de test. En exposant des nouveaux utilisateurs tooreal application, être informé sur les problèmes réels hello que votre application peut être confronté à une fois qu’il est déployé. Vous pouvez vérifier la valeur de vos mises à jour de l’application sur le volume de hello, de rapidité et diverses du trafic utilisateur réel que vous pouvez rapprocher jamais dans un environnement de test, les performances et les fonctionnalités de hello.

## <a name="traffic-routing-in-app-service-web-apps"></a>Routage du trafic dans App Service Web Apps
Avec le routage du trafic de hello fonctionnalité dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), vous pouvez diriger une partie de tooone du trafic utilisateur dynamique ou de plusieurs [les emplacements de déploiement](web-sites-staged-publishing.md), puis d’analyser votre application avec [Application Azure Insights](/services/application-insights/) ou [Azure HDInsight](/services/hdinsight/), ou un outil tiers comme [New Relic](/marketplace/partners/newrelic/newrelic/) toovalidate votre modification. Par exemple, vous pouvez implémenter hello du Service d’applications dans les scénarios suivants :

* Découvrir les bogues fonctionnelles ou d’identifier les goulots d’étranglement de performances de votre déploiement de toosite à l’échelle préalable des mises à jour
* Effectuer des « test contrôlé vols » de vos modifications en mesurant les métriques d’utilisation sur l’application de bêta hello
* Progressivement rampe tooa nouvelle mise à jour et en douceur sauvegarder la version actuelle de toohello si une erreur se produit. 
* Optimiser les résultats commerciaux de votre application en exécutant des [tests A/B](https://en.wikipedia.org/wiki/A/B_testing) ou des [tests multivariables](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing) dans plusieurs emplacements de déploiement

### <a name="requirements-for-using-traffic-routing-in-web-apps"></a>Configuration requise pour utiliser le routage du trafic dans Web Apps
* Votre application web doit s’exécuter au niveau **Standard** ou **Premium**, requis pour les emplacements de déploiement multiples.
* Dans l’ordre toowork correctement, le routage du trafic nécessite toobe cookies activé dans le navigateur des utilisateurs hello. Routage de trafic utilise les cookies toopin un emplacement de déploiement de client navigateur tooa session du client hello vie hello.
* Le routage du trafic prend en charge des scénarios avancés de test en production via les applets de commande Azure PowerShell.

## <a name="route-traffic-segment-tooa-deployment-slot"></a>Emplacement de déploiement de router le trafic segment tooa
Au niveau de base hello dans chaque scénario d’info-bulle, vous acheminer un pourcentage prédéfini de votre emplacement de déploiement de production non tooa le trafic dynamique. toodo, suit hello suivantes :

> [!NOTE]
> Hello étapes ici suppose que vous avez déjà un [emplacement de déploiement de production non](web-sites-staged-publishing.md) et ce hello souhaité de contenu de l’application web est déjà [déployé](web-sites-deploy.md) tooit.
> 
> 

1. Ouvrez une session sur hello [Azure Portal](https://portal.azure.com/).
2. Dans le panneau de votre application web, cliquez sur **Paramètres** > **Routage du trafic**.
   ![](./media/app-service-web-test-in-production/01-traffic-routing.png)
3. Emplacement de hello SELECT que vous souhaitez tooroute trafic tooand hello pourcentage du trafic total de hello vous le souhaitez, puis cliquez sur **enregistrer**.
   
    ![](./media/app-service-web-test-in-production/02-select-slot.png)
4. Accédez à panneau de l’emplacement de déploiement toohello. Vous devez maintenant voir le trafic dynamique qui est routé tooit.
   
    ![](./media/app-service-web-test-in-production/03-traffic-routed.png)

Une fois que le routage du trafic est configuré, hello spécifié, pourcentage de clients sera l’emplacement de production non tooyour routés de façon aléatoire. Toutefois, il est important toonote qu’une fois qu’un client est un emplacement spécifique de tooa routé automatiquement, elle sera emplacement toothat « épinglé » pour la durée de vie hello de cette session client. Cela est fait à l’aide d’une session utilisateur de cookie toopin hello. Si vous Inspectez les requêtes hello HTTP, vous trouverez une `TipMix` cookie dans toutes les requêtes suivantes.

![](./media/app-service-web-test-in-production/04-tip-cookie.png)

## <a name="force-client-requests-tooa-specific-slot"></a>Forcer l’emplacement spécifique du tooa demandes client
Dans le routage du trafic tooautomatic addition, du Service d’applications est emplacement spécifique du tooa tooroute en mesure de demandes. Cela est utile lorsque vous souhaitez que votre tooopt en mesure des utilisateurs toobe-dans ou annulations de votre application de la version bêta. toodo, vous utilisez hello `x-ms-routing-name` paramètre de requête.

à l’aide de tooreroute utilisateurs tooa emplacement spécifique `x-ms-routing-name`, vous devez vous assurer que cet emplacement hello est déjà ajouté la liste de routage du trafic toohello. Étant donné que vous souhaitez explicitement tooroute tooa emplacement, peu importe pourcentage réel routage hello que vous définissez. Si vous le souhaitez, vous pouvez créer un lien de bêta » « que les utilisateurs peuvent cliquer tooaccess hello bêta application.

![](./media/app-service-web-test-in-production/06-enable-x-ms-routing-name.png)

### <a name="opt-users-out-of-beta-app"></a>Utilisateurs refusant l’application bêta
les utilisateurs toolet refuser de votre application de la version bêta, par exemple, vous pouvez placer ce lien dans votre page web :

    <a href="<webappname>.azurewebsites.net/?x-ms-routing-name=self">Go back tooproduction app</a>

Hello chaîne `x-ms-routing-name=self` Spécifie l’emplacement de production hello. Une fois hello lien de hello accès client navigateur, non seulement il redirigé toohello l’emplacement de production, mais que chaque demande ultérieure contiendra hello `x-ms-routing-name=self` cookie qui épingle l’emplacement de production toohello hello session.

![](./media/app-service-web-test-in-production/05-access-production-slot.png)

### <a name="opt-users-in-toobeta-app"></a>Choisir les utilisateurs de l’application de toobeta
s’abonner aux utilisateurs de toolet tooyour bêta app, jeu hello même interroger toohello nom du paramètre d’emplacement de production non hello, par exemple :

        <webappname>.azurewebsites.net/?x-ms-routing-name=staging

## <a name="more-resources"></a>Autres ressources
* [Configurer des environnements intermédiaires pour les applications web dans Azure App Service](web-sites-staged-publishing.md)
* [Déployer une application complexe de manière prévisible dans Microsoft Azure](app-service-deploy-complex-application-predictably.md)
* [Développement logiciel agile avec Azure App Service](app-service-agile-software-development.md)
* [Utiliser efficacement les environnements DevOps pour vos applications web](app-service-web-staged-publishing-realworld-scenarios.md)

