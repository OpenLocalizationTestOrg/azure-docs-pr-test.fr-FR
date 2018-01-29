---
title: "Présentation des plans Azure App Service | Microsoft Docs"
description: "Découvrez comment fonctionnent les plans Azure App Service et comment ils peuvent améliorer votre gestion."
keywords: "app service, azure app service, mise à l’échelle, évolutif, scalabilité, plan app service, coût d’app service"
services: app-service
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/09/2017
ms.author: cephalin
ms.openlocfilehash: 268844eae8dc06937529e79d52515cad2f6da3f4
ms.sourcegitcommit: 7edfa9fbed0f9e274209cec6456bf4a689a4c1a6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/17/2018
---
# <a name="azure-app-service-plan-overview"></a>Présentation des plans d’Azure App Service

Dans App Service, une application s’exécute dans un _plan App Service_. Un plan App Service définit un ensemble de ressources de calcul nécessaires à l’exécution d’une application web. Ces ressources de calcul sont analogues à la [_batterie de serveurs_](https://wikipedia.org/wiki/Server_farm) dans l’hébergement web classique. Une ou plusieurs applications peuvent être configurées pour s’exécuter sur les mêmes ressources informatiques (ou dans le même plan App Service).

Quand vous créez un plan App Service dans une région (par exemple, Europe de l’Ouest), un ensemble de ressources de calcul est créé pour ce plan dans cette région. Toutes les applications que vous placez dans ce plan App Service s’exécutent sur ces ressources de calcul telles que définies par votre plan App Service. Chaque plan App Service définit les éléments suivants :

- Région (ouest des États-Unis, est des États-Unis, etc.)
- Nombre d’instances de machine virtuelle
- Taille des instances de machine virtuelle (petite, moyenne ou grande)
- Niveau tarifaire (Gratuit, Partagé, De base, Standard, Premium, PremiumV2, Isolé, Consommation)

Le _niveau tarifaire_ d’un plan App Service détermine les fonctionnalités App Service que vous obtenez et combien vous payez pour le plan. Il existe plusieurs catégories de niveaux tarifaires :

- **Calcul partagé**: les deux niveaux de base, **Gratuit** et **Partagé**, exécutent une application sur la même machine virtuelle Azure que les autres applications App Service, y compris les applications d’autres clients. Ces niveaux allouent des quotas d’UC à chaque application qui s’exécute sur les ressources partagées, et les ressources ne peuvent pas être mises à l’échelle.
- **Calcul dédié** : les niveaux **De base**, **Standard**, **Premium** et **PremiumV2** exécutent les applications sur des machines virtuelles Azure dédiées. Seules les applications qui se trouvent dans un même plan App Service partagent les mêmes ressources de calcul. Plus le niveau est élevé, plus vous disposez d’instances de machine virtuelle pour une mises à l’échelle.
- **Isolé** : ce niveau exécute les machines virtuelles Azure dédiées sur des réseaux virtuels Azure dédiés, doublant l’isolement de calcul de vos applications d’un isolement réseau. Il fournit les fonctionnalités de mises à l’échelle maximales.
- **Consommation** : ce niveau n’est disponible que pour les [applications de fonction](../azure-functions/functions-overview.md). Il met à l’échelle les fonctions de manière dynamique en fonction de la charge de travail. Pour plus d’informations, consultez [Comparaison des plans d’hébergement Azure Functions](../azure-functions/functions-scale.md).

[!INCLUDE [app-service-dev-test-note](../../includes/app-service-dev-test-note.md)]

En outre, chaque niveau fournit un sous-ensemble spécifique de fonctionnalités App Service. Ces fonctionnalités comprennent, entre autres, les domaines personnalisés et les certificats SSL, la mise à l’échelle automatique, les emplacements de déploiement, les sauvegardes et l’intégration de Traffic Manager. Plus le niveau est élevé, plus de fonctionnalités sont disponibles. Pour savoir quelles fonctionnalités sont prises en charge dans chaque niveau tarifaire, consultez les [détails des plans App Service](https://azure.microsoft.com/pricing/details/app-service/plans/).

<a name="new-pricing-tier-premiumv2"></a>

> [!NOTE]
> Le nouveau niveau tarifaire **PremiumV2** fournit des [machines virtuelles Dv2](../virtual-machines/windows/sizes-general.md#dv2-series) dotées de processeurs plus rapides, d’un stockage SSD et d’un ratio mémoire-cœur deux fois plus élevé que celui du niveau **Standard**. **PremiumV2** offre également une évolutivité supérieure grâce à un plus grand nombre d’instances tout en fournissant toutes les fonctionnalités avancées du plan Standard. Toutes les fonctionnalités disponibles dans le niveau **Premium** existant sont incluses dans **PremiumV2**.
>
> Comme pour les autres niveaux dédiés, trois tailles de machine virtuelle sont disponibles pour ce niveau :
>
> - Petite (un seul cœur d’UC, 3,5 Gio de mémoire) 
> - Moyenne (deux cœurs d’UC, 7 Gio de mémoire) 
> - Grande (quatre cœurs d’UC, 14 Gio de mémoire)  
>
> Pour obtenir les informations tarifaires concernant **PremiumV2**, consultez [Tarification d’App Service](https://azure.microsoft.com/pricing/details/app-service/).
>
> Pour démarrer avec le nouveau niveau tarifaire **PremiumV2**, consultez [Configurer le niveau PremiumV2 pour App Service](app-service-configure-premium-tier.md).

## <a name="how-does-my-app-run-and-scale"></a>Comment mon application s’exécute-t-elle et se met-elle à l’échelle ?

Dans les niveaux **Gratuit** et **Partagé**, une application reçoit des minutes d’UC sur une instance de machine virtuelle partagée et ne peut pas être mise à l’échelle. Dans les autres niveaux, une application s’exécute et se met à l’échelle comme suit.

Quand vous créez une application dans App Service, elle est placée dans un plan App Service. Quand l’application s’exécute, elle s’exécute sur toutes les instances de machine virtuelle configurées dans le plan App Service. Si plusieurs applications sont dans le même plan App Service, elles partagent toutes les mêmes instances de machine virtuelle. Si vous avez plusieurs emplacements de déploiement pour une application, tous les emplacements de déploiement s’exécutent également sur les mêmes instances de machine virtuelle. Si vous activez les journaux de diagnostic, effectuez des sauvegardes ou exécutez des tâches web, ils utilisent également des cycles d’UC et de la mémoire sur ces instances de machine virtuelle.

Ainsi, le plan App Service est l’unité d’échelle des applications App Service. Si le plan est configuré pour exécuter cinq instances de machine virtuelle, toutes les applications dans le plan s’exécutent sur les cinq instances. Si le plan est configuré pour une mise à l’échelle automatique, toutes les applications dans le plan sont mises à l’échelle ensemble en fonction des paramètres de mise à l’échelle.

Pour plus d’informations la mise à l’échelle d’une application, consultez [Mise à l’échelle manuelle ou automatique du nombre d’instances](../monitoring-and-diagnostics/insights-how-to-scale.md).

<a name="cost"></a>

## <a name="how-much-does-my-app-service-plan-cost"></a>Combien coûte mon plan App Service ?

Cette section décrit la façon dont les applications App Service sont facturées. Pour obtenir des informations détaillées propres aux régions, consultez [Tarification d’App Service](https://azure.microsoft.com/pricing/details/app-service/).

À l’exception du niveau **Gratuit**, un plan App Service comporte une facturation horaire des ressources de calcul qu’il utilise.

- Dans le niveau **Partagé**, chaque application reçoit un quota de minutes d’UC ; ainsi, _chaque application_ est facturée toutes les heures pour le quota d’UC.
- Dans les niveaux de calcul dédié (**De base**, **Standard**, **Premium**, **PremiumV2**), le plan App Service définit le nombre d’instances de machines virtuelles auquel les applications sont mises à l’échelle ; ainsi, _chaque instance de machine virtuelle_ dans le plan App Service fait l’objet d’une facturation horaire. Ces instances de machine virtuelle sont facturées dans les mêmes proportions, quel que soit le nombre d’applications en cours d’exécution sur ces instances. Pour éviter des frais inattendus, consultez [Nettoyer un plan App Service](app-service-plan-manage.md#delete).
- Dans le niveau **Isolé**, l’environnement App Service définit le nombre de workers isolés qui exécutent vos applications, et _chaque worker_ est facturé toutes les heures. En outre, l’exécution de l’environnement App Service donne lieu à des frais horaires de base. 
- (Azure Functions uniquement) Le niveau **Consommation** alloue dynamiquement des instances de machine virtuelle pour gérer la charge de travail d’une application de fonction et est facturé dynamiquement par seconde par Azure. Pour plus d’informations, consultez [Tarification d’Azure Functions](https://azure.microsoft.com/pricing/details/functions/).

Vous ne payez pas pour l’utilisation des fonctionnalités App Service dont vous disposez (configuration de domaines personnalisés, certificats SSL, emplacements de déploiement, sauvegardes, etc.). Les exceptions sont les suivantes :

- Domaines App Service : vous payez quand vous en achetez un dans Azure et quand vous le renouvelez chaque année.
- Certificats App Service : vous payez quand vous en achetez un dans Azure et quand vous le renouvelez chaque année.
- Connexions SSL basées sur IP : il existe un tarif horaire pour chaque connexion SSL basée sur IP, mais certains niveaux (**Standard** ou supérieur) vous octroient gratuitement une connexion SSL basée sur IP. Les connexions SSL basées sur SNI sont gratuites.

> [!NOTE]
> Si vous intégrez App Service à un autre service Azure, vous devrez peut-être prendre en compte les frais liés à ce service. Par exemple, si vous utilisez Azure Traffic Manager pour mettre à l’échelle votre application géographiquement, Azure Traffic Manager facture votre utilisation en sus. Pour estimer le coût global des services dans Azure, consultez [Calculatrice de prix](https://azure.microsoft.com/pricing/calculator/). 
>
>

## <a name="what-if-my-app-needs-more-capabilities-or-features"></a>Que se passe-t-il si mon application a besoin de fonctions ou fonctionnalités supplémentaires ?

Votre plan App Service peut être mis à l’échelle à tout moment. C’est aussi simple que de changer le niveau tarifaire du plan. Vous pouvez choisir un niveau tarifaire inférieur dans un premier temps, puis monter en puissance ultérieurement quand vous avez besoin de davantage de fonctionnalités App Service.

Par exemple, vous pouvez commencer par tester votre application web dans un plan App Service **Gratuit**, et ainsi ne rien payer. Quand vous souhaitez ajouter votre [nom DNS personnalisé](app-service-web-tutorial-custom-domain.md) à l’application web, portez simplement votre plan au niveau **Partagé**. Ensuite, quand vous souhaitez ajouter un [certificat SSL personnalisé](app-service-web-tutorial-custom-ssl.md), portez votre plan au niveau **De base**. Quand vous souhaitez avoir des [environnements de préproduction](web-sites-staged-publishing.md), passez au niveau **Standard**. Quand vous avez besoin de cœurs, de mémoire ou de stockage supplémentaires, passez à une taille de machine virtuelle supérieure dans le même niveau.

Il en va de même dans l’autre sens. Quand vous estimez que vous n’avez plus besoin des fonctions ou fonctionnalités d’un niveau supérieur, vous pouvez passer à un niveau inférieur et économiser ainsi de l’argent.

Pour en savoir plus sur la mise à l’échelle du plan App Service, consultez [Mise à l’échelle d’une application web dans Microsoft Azure App Service](web-sites-scale.md).

Si votre application est dans le même plan App Service que d’autres applications, vous souhaiterez probablement améliorer le niveau de performance de l’application en isolant les ressources de calcul. Pour ce faire, vous pouvez déplacer l’application vers un plan App Service distinct. Pour plus d’informations, consultez [Déplacer une application vers un autre plan App Service](app-service-plan-manage.md#move).

## <a name="should-i-put-an-app-in-a-new-plan-or-an-existing-plan"></a>Dois-je mettre une application dans un nouveau plan ou dans un plan existant ?

Étant donné que vous payez pour les ressources informatiques qu’alloue votre plan App Service (consultez [Combien coûte mon plan App Service ?](#cost)), vous pouvez faire des économies en plaçant plusieurs applications dans le même plan App Service. Vous pouvez continuer à ajouter des applications à un plan existant tant que le plan a suffisamment de ressources pour gérer la charge. Toutefois, gardez à l’esprit que les applications qui se trouvent dans un même plan App Service partagent toutes les mêmes ressources de calcul. Pour déterminer si la nouvelle application a les ressources nécessaires, vous devez comprendre la capacité du plan App Service existant et la charge prévue pour la nouvelle application. Surcharger un plan App Service peut entraîner un temps d’arrêt pour vos applications nouvelles et existantes.

Isolez votre application dans un nouveau plan App Service si :

- L’application consomme beaucoup de ressources.
- Vous souhaitez mettre à l’échelle l’application indépendamment des autres applications dans le plan existant.
- L’application a besoin de ressources dans une région géographique différente.

De cette façon, vous pouvez allouer un nouveau jeu de ressources pour votre application et mieux contrôler vos applications.

## <a name="manage-an-app-service-plan"></a>Gérer un plan App Service

> [!div class="nextstepaction"]
> [Gérer un plan App Service](app-service-plan-manage.md)
