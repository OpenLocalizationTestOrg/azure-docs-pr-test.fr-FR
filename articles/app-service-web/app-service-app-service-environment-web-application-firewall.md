---
title: "aaaConfiguring un pare-feu d’applications Web (WAF) pour l’environnement App Service"
description: "Découvrez comment tooconfigure une application web de pare-feu devant votre environnement App Service."
services: app-service\web
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: a2101291-83ba-4169-98a2-2c0ed9a65e8d
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: naziml
ms.openlocfilehash: 0fcf62aea871751c9d4f294d2d24df2186fc0e7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a>Configuration d'un pare-feu d'applications Web (WAF) pour un environnement App Service
## <a name="overview"></a>Vue d'ensemble
Web pare-feux de l’application comme hello [WAF Barracuda pour Azure](https://www.barracuda.com/programs/azure) qui est disponible sur hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) vous aide à sécuriser vos applications web en examinant tooblock de trafic web entrant SQL injections, scripts entre sites, des téléchargements de programmes malveillants & application DDoS et autres attaques. Il examine également réponses hello à partir de serveurs web principal de hello pour Data Loss Prevention (DLP). Combiné avec l’isolation de hello et la mise à l’échelle supplémentaire fournie par les environnements App Service, cela fournit un environnement idéal toohost métier critiques web applications nécessitant les requêtes malveillantes toowithstand et volume de trafic élevé.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a>Paramétrage
Pour ce document, nous allons configurer notre environnement App Service derrière la charge de plusieurs équilibrée des instances de Barracuda WAF afin que seul le trafic à partir de hello WAF peut atteindre hello environnement App Service et il ne sera pas accessible à partir de hello réseau de périmètre. Il nous faudra également Azure Traffic Manager devant notre solde de tooload Barracuda WAF instances entre les centres de données Azure et les régions. Un diagramme de haut niveau de l’installation de hello ressemble à ce qui est indiqué ci-dessous.

![Architecture][Architecture] 

> Remarque : avec l’introduction de hello de [prennent en charge de l’équilibrage de charge interne pour l’environnement App Service](app-service-environment-with-internal-load-balancer.md), vous pouvez configurer toobe hello ASE inaccessible à partir de hello réseau de périmètre et être uniquement le réseau privé de toohello disponibles. 
> 
> 

## <a name="configuring-your-app-service-environment"></a>Configuration de votre environnement App Service
tooconfigure un environnement App Service font référence trop[notre documentation](app-service-web-how-to-create-an-app-service-environment.md) sur le sujet de hello. Une fois que vous avez un environnement App Service créé, vous pouvez créer [Web Apps](app-service-web-overview.md), [applications API](../app-service-api/app-service-api-apps-why-best-platform.md) et [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) dans cet environnement qui sera être protégé derrière hello WAF nous configurer dans la section suivante de hello.

## <a name="configuring-your-barracuda-waf-cloud-service"></a>Configuration de votre service cloud WAF Barracuda
Barracuda propose un [article détaillé](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) sur le déploiement de son WAF sur une machine virtuelle dans Azure. Mais étant donné que la redondance et nous pas introduire un point de défaillance unique, instance de WAF toodeploy au moins 2 machines virtuelles dans hello même Service Cloud lorsque suivant ces instructions.

### <a name="adding-endpoints-toocloud-service"></a>Ajout de points de terminaison tooCloud Service
Une fois que vous avez 2 ou plus WAF VM instances dans votre Service Cloud, vous pouvez utiliser hello [portail Azure](https://portal.azure.com/) tooadd HTTP et HTTPS points de terminaison qui sont utilisées par votre application, comme indiqué dans l’image hello ci-dessous.

![Configurer le point de terminaison][ConfigureEndpoint]

Si vos applications utilisent les autres points de terminaison, assurez-vous que tooadd ces liste toothis ainsi. 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a>Configuration du WAF Barracuda avec son portail de gestion
Le WAF Barracuda utilise le port TCP 8000 pour sa configuration avec le portail de gestion. Comme il y a plusieurs instances de machines virtuelles de hello WAF vous aurez besoin des étapes hello toorepeat pour chaque instance de machine virtuelle. 

> Remarque : Une fois que vous avez terminé avec une configuration WAF, supprimez point de terminaison TCP/8000 hello de tous les tookeep de vos machines virtuelles de WAF votre WAF sécurisé.
> 
> 

Ajouter un point de terminaison de gestion de hello comme indiqué dans l’image hello ci-dessous tooconfigure votre WAF Barracuda.

![Ajouter un point de terminaison de gestion][AddManagementEndpoint]

Utilisez un point de terminaison de la gestion de toohello de navigateur toobrowse sur votre Service Cloud. Si votre Service Cloud est appelé test.cloudapp.net, vous pouvez accéder à ce point de terminaison en parcourant toohttp://test.cloudapp.net:8000. Vous devez voir une page de connexion comme ci-dessous, que vous pouvez vous connecter à l’aide des informations d’identification que vous avez spécifié dans la phase d’installation hello WAF machine virtuelle.

![Page de connexion à la gestion][ManagementLoginPage]

Une fois connexion vous devez normalement voir un tableau de bord hello une image hello ci-dessous, qui présente des statistiques de base sur la protection de WAF de hello.

![Tableau de bord de gestion][ManagementDashboard]

En cliquant sur l’onglet Services de hello vous permettent de configurer votre WAF pour les services qu’il protège. Pour plus d’informations sur la configuration de votre WAF Barracuda, consultez [la documentation appropriée](https://techlib.barracuda.com/waf/getstarted1). Dans l’exemple hello ci-dessous, une application Web Azure desservant le trafic sur HTTP et HTTPS a été configuré.

![Ajouter des services de gestion][ManagementAddServices]

> Remarque : Selon la façon dont vos applications sont configurées et les fonctionnalités qui sont utilisées dans votre environnement App Service, vous devrez tooforward trafic pour des ports TCP autre que 80 et 443, par exemple, si vous avez le programme d’installation de IP SSL pour une application Web. Pour obtenir la liste des ports réseau utilisé dans des environnements de Service d’application, consultez trop[la documentation du trafic entrant de contrôle](app-service-app-service-environment-control-inbound-traffic.md) section Ports de réseau.
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a>Configuration de Microsoft Azure Traffic Manager (FACULTATIF)
Si votre application est disponible dans plusieurs régions, vous souhaiteriez solde de tooload leur derrière [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md). toodo afin que vous pouvez ajouter un point de terminaison Bonjour [portail Azure classic](https://manage.azure.com) à l’aide de nom du Service Cloud pour votre WAF hello dans le profil Traffic Manager hello comme indiqué dans l’image hello ci-dessous. 

![Point de terminaison Traffic Manager][TrafficManagerEndpoint]

Si votre application requiert une authentification, assurez-vous de qu'avoir certaines ressources qui ne nécessite pas d’authentification pour tooping Traffic Manager pour la disponibilité hello de votre application. Vous pouvez configurer des URL hello sous la section de configuration de hello sur hello [portail Azure classic](https://manage.azure.com) comme indiqué ci-dessous.

![Configuration de Traffic Manager][ConfigureTrafficManager]

tooforward hello Traffic Manager les tests ping à partir de votre application de tooyour WAF, vous devez les traductions du site Web toosetup dans votre Barracuda WAF tooforward trafic tooyour l’application comme indiqué dans l’exemple hello ci-dessous.

![Traductions de site Web][WebsiteTranslations]

## <a name="securing-traffic-tooapp-service-environment-using-network-security-groups-nsg"></a>Sécuriser le trafic tooApp Service environnement à l’aide de réseau sécurité groupes (NSG)
Suivez hello [documentation de trafic entrant de contrôle](app-service-app-service-environment-control-inbound-traffic.md) pour plus d’informations sur la limitation du trafic tooyour environnement App Service à partir de hello WAF uniquement à l’aide d’adresse hello adresse IP virtuelle de votre Service Cloud. Voici un exemple de commande Powershell pour effectuer cette tâche pour le port TCP 80.

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

Remplacez hello SourceAddressPrefix hello adresse IP virtuelle (VIP) du Service de Cloud de votre WAF.

> Remarque : hello adresse IP virtuelle de votre Service Cloud changent lorsque vous supprimez et recréez hello Service Cloud. Assurez-vous que tooupdate hello adresse du groupe de ressources de réseau de hello après cette opération. 
> 
> 

<!-- IMAGES -->
[Architecture]: ./media/app-service-app-service-environment-web-application-firewall/Architecture.png
[ConfigureEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureEndpoint.png
[AddManagementEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/AddManagementEndpoint.png
[ManagementAddServices]: ./media/app-service-app-service-environment-web-application-firewall/ManagementAddServices.png
[ManagementDashboard]: ./media/app-service-app-service-environment-web-application-firewall/ManagementDashboard.png
[ManagementLoginPage]: ./media/app-service-app-service-environment-web-application-firewall/ManagementLoginPage.png
[TrafficManagerEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/TrafficManagerEndpoint.png
[ConfigureTrafficManager]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureTrafficManager.png
[WebsiteTranslations]: ./media/app-service-app-service-environment-web-application-firewall/WebsiteTranslations.png
