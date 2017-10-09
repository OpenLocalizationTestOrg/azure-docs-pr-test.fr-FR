---
title: "vue d’ensemble des applications aaaWeb | Documents Microsoft"
description: "Découvrez comment Azure App Service vous aide à développer et héberger des applications web."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 94af2caf-a2ec-4415-a097-f60694b860b3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 01/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: ce27519bddd62a7fca6ba1fb23c763d0fc378c2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="web-apps-overview"></a>Vue d'ensemble de Web Apps
*App Service Web Apps* est une plateforme de calcul entièrement gérée, optimisée pour l’hébergement de sites et d’applications web. Cela [platform-as-a-service](https://en.wikipedia.org/wiki/Platform_as_a_service) offre (PaaS) de Microsoft Azure vous permet de vous concentrer sur votre logique métier, tandis que Azure s’occupe de hello infrastructure toorun et faire évoluer vos applications.

Hello après 5 minutes vidéo présente Azure App Service Web Apps.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Web-Apps-with-Yochay-Kiriaty/player]
>
>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

## <a name="what-is-a-web-app-in-app-service"></a>Qu’est-ce qu’une application web dans App Service ?
Dans le Service d’application, un *application web* est hello des ressources de calcul Azure fournit pour l’hébergement d’une site Web ou une application web.  

ressources de calcul Hello peut-être sur partagé ou dédiés virtuels (VM), en fonction de hello tarification que vous choisissez. Le code de votre application s’exécute sur une machine virtuelle isolée des autres clients.

Votre code peut être écrit dans n’importe quel langage ou infrastructure pris en charge par [Azure App Service](../app-service/app-service-value-prop-what-is.md), tels que ASP.NET, Node.js, Java, PHP ou Python. Vous pouvez également exécuter des scripts utilisant [PowerShell et d’autres langages de script](web-sites-create-web-jobs.md#acceptablefiles) dans une application web.

Pour obtenir des exemples de scénarios d’application standard que vous pouvez utiliser des applications Web pour voir [Web des scénarios d’application](https://azure.microsoft.com/documentation/scenarios/web-app/) et hello **recommandations et scénarios** section de [du Service d’applications Azure, Virtual Comparaison des ordinateurs et des Services de Cloud Service Fabric](choose-web-site-cloud-service-vm.md#scenarios).

## <a name="why-use-web-apps"></a>Pourquoi utiliser Web Apps ?
Voici certaines fonctionnalités clés du Service d’application qui s’appliquent aux tooWeb :

* **Plusieurs langages et infrastructures** : App Service offre une excellente prise en charge d’ASP.NET, Node.js, Java, PHP et Python. Vous pouvez également exécuter [PowerShell et d’autres scripts ou exécutables](web-sites-create-web-jobs.md) sur les machines virtuelles App Service.
* **Optimisation DevOps** : configurez [l’intégration et le déploiement continus](app-service-continuous-deployment.md) avec Visual Studio Team Services, GitHub ou BitBucket. Assurez la promotion des mises à jour par le biais des [environnements de test et intermédiaires](web-sites-staged-publishing.md). Effectuez des [tests A/B](app-service-web-test-in-production-get-start.md). Gérer vos applications dans le Service d’applications à l’aide de [Azure PowerShell](/powershell/azureps-cmdlets-docs) ou hello [(CLI) d’une interface de ligne inter-plateformes](../cli-install-nodejs.md).
* **Mise à l’échelle globale avec une haute disponibilité** : effectuez des [montées en puissance](web-sites-scale.md) ou [augmentez la taille des instances](../monitoring-and-diagnostics/insights-how-to-scale.md) manuellement ou automatiquement. Hébergez vos applications n’importe où dans l’infrastructure de centre de données globaux de Microsoft et hello du Service d’applications [SLA](https://azure.microsoft.com/support/legal/sla/app-service/) promet de haute disponibilité.
* **Données des plateformes et locales tooSaaS connexions** -choisir parmi plus de 50 [connecteurs](../connectors/apis-list.md) pour les systèmes d’entreprise (par exemple, SAP, Siebel et Oracle), les services SaaS (par exemple, Salesforce et Office 365) et internet Services (tels que Facebook et Twitter). Accédez aux données locales à l’aide de [connexions hybrides](../biztalk-services/integration-hybrid-connection-overview.md) et de [réseaux virtuels Azure](web-sites-integrate-with-vnet.md).
* **Sécurité et conformité** : App Service est [conforme aux normes ISO, SOC et PCI](https://www.microsoft.com/TrustCenter/).
* **Modèles d’application** -Choisissez parmi une liste complète des modèles d’application Bonjour [Azure Marketplace](https://azure.microsoft.com/marketplace/) qui vous permettent d’utiliser un Assistant tooinstall open source répandus telles que WordPress, Joomla et Drupal.
* **Intégration de Visual Studio** -outils dédiés dans Visual Studio rationalisent travail hello de création, de déploiement et de débogage.

En outre, une application web peut tirer parti des fonctionnalités offertes par [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) (comme la prise en charge de CORS) et [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) (comme les notifications Push). Pour plus d’informations sur les types d’application dans App Service, consultez l’article [Qu’est-ce qu’Azure App Service ?](../app-service/app-service-value-prop-what-is.md)

En plus des applications web dans App Service, Azure offre d’autres services qui peuvent être utilisés pour l’hébergement de sites et d’applications web. La plupart des scénarios, les applications Web est hello meilleur choix.  Pour l’architecture de microservice, envisagez [Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric)et si vous avez besoin de davantage de contrôle sur hello machines virtuelles qui s’exécute votre code, [des Machines virtuelles Azure](https://azure.microsoft.com/documentation/services/virtual-machines/). Pour plus d’informations sur la façon toochoose entre ces services Azure, consultez [comparaison du Service d’applications Azure, les ordinateurs virtuels, les Service Fabric et les Services de cloud computing](choose-web-site-cloud-service-vm.md).

## <a name="getting-started"></a>Prise en main
tooget démarré en déployant exemple code tooa nouvelle application web dans le Service d’application, suivez un des didacticiels hello Bonjour après la zone de liste déroulante. Vous devrez créer un compte Azure gratuit

> [!div class="op_single_selector"]
> * [Déploiement de votre première application tooAzure ASP.NET web des 5 dernières minutes](app-service-web-get-started-dotnet.md)
> * [Déploiement de votre première application tooAzure PHP web des 5 dernières minutes](app-service-web-get-started-php.md)
> * [Déploiement de votre première application tooAzure de Node.js web des 5 dernières minutes](app-service-web-get-started-nodejs.md)
> * [Déploiement de votre première application tooAzure de Java web des 5 dernières minutes](app-service-web-get-started-java.md)
> * [Déploiement de votre première application tooAzure de Python web des 5 dernières minutes](app-service-web-get-started-python.md)
> * [Déployer votre premier tooAzure de site HTML 5 dernières minutes](app-service-web-get-started-html.md)
> 
> 

> [!NOTE]
> Vous pouvez [essayer App Service](https://azure.microsoft.com/try/app-service/) sans compte Azure. Créer une application de démarrage et de le manipuler pour les horaires de tooan--aucune carte de crédit requis, aucune des engagements.
> 
> 
