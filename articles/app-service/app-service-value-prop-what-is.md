---
title: "aaaAzure du Service d’applications pour le web, mobiles et les applications de l’API | Documents Microsoft"
description: "Découvrez comment Azure App Service vous permet de développer, déployer et gérer des applications web et mobiles."
keywords: "app service, azure app service, coût de l’app service, mise à l’échelle, évolutif, déploiement d’applications, déploiement d’applications azure, paas, platform-as-a-service, siteweb, site web, azure mobile"
services: app-service
documentationcenter: 
author: omarkmsft
manager: erikre
editor: cephalin
ms.assetid: 979cafa8-eeb6-4d3b-87cf-764a821c3e4f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: 22f414c7d79092d87406a8d3538b946881fb4580
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-app-service"></a>Qu'est-ce qu'Azure App Service ?
*App Service* est une offre PaaS ( [platform-as-a-service](https://en.wikipedia.org/wiki/Platform_as_a_service) ) de Microsoft Azure. Créez des applications web et mobiles adaptées à toutes les plateformes et appareils. Intégrez vos applications avec des solutions SaaS, connectez-vous à des applications locales et automatisez vos processus d’entreprise. Azure exécute vos applications sur des machines virtuelles entièrement gérées, avec les ressources de machines virtuelles partagées ou les machines virtuelles dédiées de votre choix.

Service d’applications inclut web de hello et capacités que nous avons précédemment fourni séparément en tant que sites Web Azure et Azure Mobile Services. Il inclut également de nouvelles fonctionnalités d’automatisation des processus d’entreprise et d’hébergement d’API cloud. En tant que service intégré unique, App Service vous permet d’assembler différents éléments (sites web, serveurs principaux d’application mobile, API RESTful et processus d’entreprise) au sein d’une solution unique.

Hello vidéo 4 minutes suivante fournit une brève explication de la relation de Service d’application entre tooearlier Azure offres et quelles sont les nouveautés dans celui-ci.

> [!VIDEO https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/app-service-history-lesson/player]
> 
> 

## <a name="why-use-app-service"></a>Pourquoi utiliser App Service ?
Voici quelques fonctionnalités et capacités clés d’App Service :

* **Plusieurs langages et infrastructures** : App Service offre une excellente prise en charge d’ASP.NET, Node.js, Java, PHP et Python. Vous pouvez également exécuter [Windows PowerShell et d’autres scripts ou exécutables](../app-service-web/web-sites-create-web-jobs.md) sur les machines virtuelles App Service.
* **Optimisation DevOps** : configurez [l’intégration et le déploiement continus](../app-service-web/app-service-continuous-deployment.md) avec Visual Studio Team Services, GitHub ou BitBucket. Assurez la promotion des mises à jour par le biais des [environnements de test et intermédiaires](../app-service-web/web-sites-staged-publishing.md). Effectuez des [tests A/B](../app-service-web/app-service-web-test-in-production-get-start.md). Gérer vos applications dans le Service d’applications à l’aide de [Azure PowerShell](/powershell/azureps-cmdlets-docs) ou hello [(CLI) d’une interface de ligne inter-plateformes](../cli-install-nodejs.md).
* **Mise à l’échelle globale avec une haute disponibilité** : effectuez des [montées en puissance](../app-service-web/web-sites-scale.md) ou [augmentez la taille des instances](../monitoring-and-diagnostics/insights-how-to-scale.md) manuellement ou automatiquement. Hébergez vos applications n’importe où dans l’infrastructure de centre de données globaux de Microsoft et hello du Service d’applications [SLA](https://azure.microsoft.com/support/legal/sla/app-service/) promet de haute disponibilité.
* **Données des plateformes et locales tooSaaS connexions** -choisir parmi plus de 50 [connecteurs](../connectors/apis-list.md) pour les systèmes d’entreprise (par exemple, SAP, Siebel et Oracle), les services SaaS (par exemple, Salesforce et Office 365) et internet Services (tels que Facebook et Twitter). Accédez aux données locales à l’aide de [connexions hybrides](../biztalk-services/integration-hybrid-connection-overview.md) et de [réseaux virtuels Azure](../app-service-web/web-sites-integrate-with-vnet.md).
* **Sécurité et conformité** : App Service est [conforme aux normes ISO, SOC et PCI](https://www.microsoft.com/TrustCenter/).
* **Modèles d’application** -Choisissez parmi une liste complète des modèles Bonjour [Azure Marketplace](https://azure.microsoft.com/marketplace/) qui vous permettent d’utiliser un Assistant tooinstall open source répandus telles que WordPress, Joomla et Drupal.
* **Intégration de Visual Studio** -outils dédiés dans Visual Studio rationalisent travail hello de création, de déploiement et de débogage.

## <a name="app-types-in-app-service"></a>Types d’applications dans App Service
Service d’applications offre plusieurs *types d’application*, chaque dont est prévue toohost une charge de travail spécifique :

* [**Web Apps**](../app-service-web/app-service-web-overview.md) : pour l’hébergement de sites et d’applications web.
* [**Mobile Apps**](../app-service-mobile/app-service-mobile-value-prop.md) : pour l’hébergement de serveurs principaux d’application mobile.
* [**API Apps**](../app-service-api/app-service-api-apps-why-best-platform.md) : pour l’hébergement d’API RESTful.
* [**Logic Apps**](../logic-apps/logic-apps-what-are-logic-apps.md) - pour l’automatisation des processus d’entreprise et l’intégration de systèmes et de données dans des clouds sans écrire de code.

Hello word *application* fait ici référence toohello toorunning dédié de ressources une charge de travail d’hébergement. En prenant « application web », par exemple, vous êtes probablement habitués toothinking d’une application web, comme ce navigateur tooa de fonctionnalité ensemble remettre le code à la fois les ressources de calcul hello et application. Mais dans le Service d’applications un *application web* est hello des ressources de calcul Azure fournit pour l’hébergement de votre code d’application. 

Votre application peut être composée d’applications App Service de différents types. Par exemple, si votre application se compose d’un serveur web frontal et d’une API RESTful principale, vous pouvez :

- Déployer (front-end et api) tooa unique web app  
- Déployer votre application web de tooa code frontal et de votre application tooan API de code du serveur principal. 



## <a name="app-service-plans"></a>Plans App Service
[Plans de Service d’applications](azure-web-sites-web-hosting-plans-in-depth-overview.md) représentent collection hello de ressources physiques utilisées toohost vos applications.

Les plans App Service définissent :

- **Région** (ouest des États-Unis, est des États-Unis, etc.)
- **Comptage** (un, deux, trois instances, etc.)
- La **taille d’instance** (« Petit », « Moyen », « Grand »)
- **Référence (SKU)** (gratuit, partagé, basique, standard, premium)

Toutes les applications affectées tooan **plan App Service** partagent des ressources hello qu’elle vous permettant de coût de toosave lorsque plusieurs applications d’hébergement.

Votre **plan App Service** peut évoluer de **libre** et **Shared** références trop**base**, **Standard**, et **Premium** références (SKU), vous pouvez ainsi accéder aux ressources de la toomore et de fonctionnalités le long de hello moyen. Une fois que votre Plan App Service est défini trop**base** ou une version ultérieure, vous pouvez également contrôler hello **taille** et d’augmenter le nombre de machines virtuelles de hello.

Hello **référence (SKU)** et **échelle** Hello du Service d’applications plan détermine hello coût et hello pas le numéro d’applications qu’elle contient. 

Si vous avez besoin de plus d’évolutivité et d’isolement réseau, vous pouvez exécuter vos applications dans un [environnement App Service](../app-service-web/app-service-app-service-environment-intro.md).

## <a name="pricing"></a>Tarification
Pour plus d’informations sur le coût d’App Service, consultez la page [Tarification de App Service](https://azure.microsoft.com/pricing/details/app-service/).

## <a name="test-drive-app-service"></a>Tester App Service
[Créez un exemple d’application web, mobile ou logique](https://azure.microsoft.com/try/app-service/) et utilisez-la pendant une heure sans carte de crédit, sans aucun engagement et sans aucune contrainte.

Ou ouvrez un [compte Azure gratuit](https://azure.microsoft.com/pricing/free-trial/), puis essayez l’un de nos didacticiels dédiés à la prise en main :

* [Didacticiel : Créer une application web](../app-service-web/app-service-web-get-started.md)
* [Didacticiel : Créer une application mobile](../app-service-mobile/app-service-mobile-android-get-started.md)
* [Didacticiel : Créer une application API](../app-service-api/app-service-api-dotnet-get-started.md)
* [Didacticiel : Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md)

