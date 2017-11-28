---
title: "Configuration d'un pare-feu d'applications Web (WAF) pour un environnement App Service"
description: "Apprenez à configurer un pare-feu d'applications Web devant votre environnement App Service."
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
ms.openlocfilehash: 3e9e9fa4ddab60a467e8aa793ec0ca269b0bc4e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a><span data-ttu-id="a50dd-103">Configuration d'un pare-feu d'applications Web (WAF) pour un environnement App Service</span><span class="sxs-lookup"><span data-stu-id="a50dd-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="a50dd-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="a50dd-104">Overview</span></span>
<span data-ttu-id="a50dd-105">Les pare-feu d’applications web comme le [WAF Barracuda pour Azure](https://www.barracuda.com/programs/azure) qui est disponible sur [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) permettent de sécuriser vos applications web en inspectant le trafic web entrant pour bloquer les injections SQL, l’exécution de scripts de site à site, les téléchargements de logiciels malveillants, les attaques DDoS d’application et d’autres attaques.</span><span class="sxs-lookup"><span data-stu-id="a50dd-105">Web application firewalls like the [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that is available on the [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helps secure your web applications by inspecting inbound web traffic to block SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span></span> <span data-ttu-id="a50dd-106">Ce type de pare-feu inspecte également les réponses des serveurs Web principaux pour prévention de perte de données (DLP).</span><span class="sxs-lookup"><span data-stu-id="a50dd-106">It also inspects the responses from the back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="a50dd-107">En association avec l'isolement et la mise à l'échelle supplémentaire fournis par les environnements App Service, ceci fournit un environnement idéal pour héberger des applications Web professionnelles critiques qui doivent résister aux requêtes malveillantes et à un volume de trafic élevé.</span><span class="sxs-lookup"><span data-stu-id="a50dd-107">Combined with the isolation and additional scaling provided by App Service Environments, this provides an ideal environment to host business critical web applications that need to withstand malicious requests and high volume traffic.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a><span data-ttu-id="a50dd-108">Paramétrage</span><span class="sxs-lookup"><span data-stu-id="a50dd-108">Setup</span></span>
<span data-ttu-id="a50dd-109">Pour ce document, nous allons configurer notre environnement App Service derrière plusieurs instances à charge équilibrée de WAF Barracuda, afin que seul le trafic provenant du WAF puisse atteindre l'environnement App Service. Il ne sera pas accessible depuis la zone DMZ.</span><span class="sxs-lookup"><span data-stu-id="a50dd-109">For this document we will configure our App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from the WAF can reach the App Service Environment and it will not be accessible from the DMZ.</span></span> <span data-ttu-id="a50dd-110">Nous aurons également Azure Traffic Manager devant nos instances WAF Barracuda pour équilibrer la charge entre les régions et les centres de données Azure.</span><span class="sxs-lookup"><span data-stu-id="a50dd-110">We will also have Azure Traffic Manager in front of our Barracuda WAF instances to load balance across Azure data centers and regions.</span></span> <span data-ttu-id="a50dd-111">Un diagramme de haut niveau de la configuration ressemblerait à ce qui est illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a50dd-111">A high level diagram of the setup would look like what is shown below.</span></span>

![Architecture][Architecture] 

> <span data-ttu-id="a50dd-113">Remarque : avec l’introduction de la [prise en charge de l’équilibreur de charge interne pour l’environnement App Service](app-service-environment-with-internal-load-balancer.md), vous pouvez configurer l’ASE de façon à ce qu’il soit inaccessible depuis le DMZ et uniquement disponible pour le réseau privé.</span><span class="sxs-lookup"><span data-stu-id="a50dd-113">Note: With the introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure the ASE to be inaccessible from the DMZ and only be available to the private network.</span></span> 
> 
> 

## <a name="configuring-your-app-service-environment"></a><span data-ttu-id="a50dd-114">Configuration de votre environnement App Service</span><span class="sxs-lookup"><span data-stu-id="a50dd-114">Configuring your App Service Environment</span></span>
<span data-ttu-id="a50dd-115">Pour configurer un environnement App Service, consultez [notre documentation](app-service-web-how-to-create-an-app-service-environment.md) sur le sujet.</span><span class="sxs-lookup"><span data-stu-id="a50dd-115">To configure an App Service Environment refer to [our documentation](app-service-web-how-to-create-an-app-service-environment.md) on the subject.</span></span> <span data-ttu-id="a50dd-116">Une fois qu’un environnement App Service est créé, vous pouvez créer des [Web Apps](app-service-web-overview.md), des [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) et des [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) dans cet environnement. Elles seront toutes protégées derrière le WAF que nous allons configurer dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="a50dd-116">Once you have an App Service Environment created, you can create [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind the WAF we configure in the next section.</span></span>

## <a name="configuring-your-barracuda-waf-cloud-service"></a><span data-ttu-id="a50dd-117">Configuration de votre service cloud WAF Barracuda</span><span class="sxs-lookup"><span data-stu-id="a50dd-117">Configuring your Barracuda WAF Cloud Service</span></span>
<span data-ttu-id="a50dd-118">Barracuda propose un [article détaillé](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) sur le déploiement de son WAF sur une machine virtuelle dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a50dd-118">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span></span> <span data-ttu-id="a50dd-119">Mais étant donné que nous voulons la redondance sans introduire aucun point de défaillance, vous devez déployer au moins 2 machines virtuelles d'instances WAF dans le même service cloud.</span><span class="sxs-lookup"><span data-stu-id="a50dd-119">But because we want redundancy and not introduce a single point of failure, you want to deploy at least 2 WAF instance VMs into the same Cloud Service when following these instructions.</span></span>

### <a name="adding-endpoints-to-cloud-service"></a><span data-ttu-id="a50dd-120">Ajout de points de terminaison au service cloud</span><span class="sxs-lookup"><span data-stu-id="a50dd-120">Adding Endpoints to Cloud Service</span></span>
<span data-ttu-id="a50dd-121">Du moment où vous disposez d’au moins deux instances de machines virtuelles WAF dans votre service cloud, vous pouvez utiliser le [portail Azure](https://portal.azure.com/) pour ajouter des points de terminaison HTTP et HTTPS utilisés par votre application, comme illustré dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a50dd-121">Once you have 2 or more WAF VM instances in your Cloud Service you can use the [Azure portal](https://portal.azure.com/) to add HTTP and HTTPS endpoints that are used by your application as shown in the image below.</span></span>

![Configurer le point de terminaison][ConfigureEndpoint]

<span data-ttu-id="a50dd-123">Si vos applications utilisent d'autres points de terminaison, veillez à les ajouter à cette liste également.</span><span class="sxs-lookup"><span data-stu-id="a50dd-123">If your applications use other endpoints, make sure to add those to this list as well.</span></span> 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a><span data-ttu-id="a50dd-124">Configuration du WAF Barracuda avec son portail de gestion</span><span class="sxs-lookup"><span data-stu-id="a50dd-124">Configuring Barracuda WAF through its Management Portal</span></span>
<span data-ttu-id="a50dd-125">Le WAF Barracuda utilise le port TCP 8000 pour sa configuration avec le portail de gestion.</span><span class="sxs-lookup"><span data-stu-id="a50dd-125">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span></span> <span data-ttu-id="a50dd-126">Puisque nous avons plusieurs instances de machines virtuelles WAF, vous devrez répéter ces étapes pour chaque instance de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a50dd-126">Since we have multiple instances of the WAF VMs you will need to repeat the steps here for each VM instance.</span></span> 

> <span data-ttu-id="a50dd-127">Remarque : lorsque la configuration WAF est terminée, supprimez le point de terminaison TCP/8000 de toutes les machines virtuelles WAF pour sécuriser votre WAF.</span><span class="sxs-lookup"><span data-stu-id="a50dd-127">Note: Once you are done with WAF configuration, remove the TCP/8000 endpoint from all your WAF VMs to keep your WAF secure.</span></span>
> 
> 

<span data-ttu-id="a50dd-128">Ajoutez le point de terminaison de gestion, comme illustré dans l'image ci-dessous, pour configurer votre WAF Barracuda.</span><span class="sxs-lookup"><span data-stu-id="a50dd-128">Add the management endpoint as shown in the image below to configure your Barracuda WAF.</span></span>

![Ajouter un point de terminaison de gestion][AddManagementEndpoint]

<span data-ttu-id="a50dd-130">Utilisez un navigateur pour accéder au point de terminaison de gestion sur votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="a50dd-130">Use a browser to browse to the management endpoint on your Cloud Service.</span></span> <span data-ttu-id="a50dd-131">Si votre service cloud se nomme test.cloudapp.net, vous atteignez ce point de terminaison en accédant à http://test.cloudapp.net:8000.</span><span class="sxs-lookup"><span data-stu-id="a50dd-131">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing to http://test.cloudapp.net:8000.</span></span> <span data-ttu-id="a50dd-132">Une page de connexion, comme celle illustrée ci-dessous, doit s'afficher. Vous pouvez vous connecter à l'aide des informations d'identification spécifiées durant la phase de configuration de la machine virtuelle WAF.</span><span class="sxs-lookup"><span data-stu-id="a50dd-132">You should see a login page like below that you can login using credentials you specified in the WAF VM setup phase.</span></span>

![Page de connexion à la gestion][ManagementLoginPage]

<span data-ttu-id="a50dd-134">Lorsque vous êtes connecté, un tableau de bord comme celui illustré dans l'image ci-dessous doit s'afficher. Il présente des statistiques de base sur la protection du WAF.</span><span class="sxs-lookup"><span data-stu-id="a50dd-134">Once you login you should see a dashboard as the one in the image below that will present basic statistics about the WAF protection.</span></span>

![Tableau de bord de gestion][ManagementDashboard]

<span data-ttu-id="a50dd-136">Cliquez sur l'onglet Services pour configurer votre WAF pour les services qu'il protège.</span><span class="sxs-lookup"><span data-stu-id="a50dd-136">Clicking on the Services tab will let you configure your WAF for services it is protecting.</span></span> <span data-ttu-id="a50dd-137">Pour plus d’informations sur la configuration de votre WAF Barracuda, consultez [la documentation appropriée](https://techlib.barracuda.com/waf/getstarted1).</span><span class="sxs-lookup"><span data-stu-id="a50dd-137">For more details on configuring your Barracuda WAF you can consult [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span></span> <span data-ttu-id="a50dd-138">Dans l'exemple ci-dessous, une application Web Azure desservant le trafic HTTP et HTTPS a été configurée.</span><span class="sxs-lookup"><span data-stu-id="a50dd-138">In the example below an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span></span>

![Ajouter des services de gestion][ManagementAddServices]

> <span data-ttu-id="a50dd-140">Remarque : selon la configuration de vos applications et les fonctionnalités utilisées dans votre environnement App Service, vous devrez transférer le trafic pour les ports TCP autres que 80 et 443 ; par exemple, si vous avez configuré SSL IP pour une application Web.</span><span class="sxs-lookup"><span data-stu-id="a50dd-140">Note: Depending on how your applications are configured and what features are being used in your App Service Environment, you will need to forward traffic for TCP ports other than 80 and 443, e.g. if you have IP SSL setup for a Web App.</span></span> <span data-ttu-id="a50dd-141">Pour obtenir la liste des ports réseau utilisés dans les environnements App Service, consultez la section Ports réseau de la [documentation relative au contrôle du trafic entrant](app-service-app-service-environment-control-inbound-traffic.md) .</span><span class="sxs-lookup"><span data-stu-id="a50dd-141">For a list of network ports used in App Service Environments, please refer to [Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span></span>
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a><span data-ttu-id="a50dd-142">Configuration de Microsoft Azure Traffic Manager (FACULTATIF)</span><span class="sxs-lookup"><span data-stu-id="a50dd-142">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span></span>
<span data-ttu-id="a50dd-143">Si votre application est disponible dans plusieurs régions, vous devez en équilibrer la charge derrière [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a50dd-143">If your application is available in multiple regions, then you would want to load balance them behind [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span></span> <span data-ttu-id="a50dd-144">Pour ce faire, vous pouvez ajouter un point de terminaison dans le [portail Azure Classic](https://manage.azure.com) en utilisant le nom du service cloud de votre WAF dans le profil Traffic Manager, comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a50dd-144">To do so you can add an endpoint in the [Azure classic portal](https://manage.azure.com) using the Cloud Service name for your WAF in the Traffic Manager profile as shown in the image below.</span></span> 

![Point de terminaison Traffic Manager][TrafficManagerEndpoint]

<span data-ttu-id="a50dd-146">Si votre application requiert une authentification, vérifiez que vous disposez d'une ressource qui ne nécessite pas d'authentification pour permettre à Traffic Manager d'exécuter la commande ping pour vérifier la disponibilité de votre application.</span><span class="sxs-lookup"><span data-stu-id="a50dd-146">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager to ping for the availability of your application.</span></span> <span data-ttu-id="a50dd-147">Vous pouvez configurer l’URL sous la section Configuration du [portail Azure Classic](https://manage.azure.com) , comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a50dd-147">You can configure the URL under the Configure section on the [Azure classic portal](https://manage.azure.com) as shown below.</span></span>

![Configuration de Traffic Manager][ConfigureTrafficManager]

<span data-ttu-id="a50dd-149">Pour transférer les exécutions de commande ping de Traffic Manager à partir de votre WAF à votre application, vous devez configurer des traductions de site Web sur votre WAF Barracuda pour transférer le trafic vers votre application, comme illustré dans l'exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a50dd-149">To forward the Traffic Manager pings from your WAF to your application, you need to setup Website Translations on your Barracuda WAF to forward traffic to your application as shown in the example below.</span></span>

![Traductions de site Web][WebsiteTranslations]

## <a name="securing-traffic-to-app-service-environment-using-network-security-groups-nsg"></a><span data-ttu-id="a50dd-151">Sécurisation du trafic vers un environnement App Service à l’aide de groupes de sécurité réseau (NSG)</span><span class="sxs-lookup"><span data-stu-id="a50dd-151">Securing Traffic to App Service Environment Using Network Security Groups (NSG)</span></span>
<span data-ttu-id="a50dd-152">Consultez la [documentation relative au contrôle du trafic entrant](app-service-app-service-environment-control-inbound-traffic.md) pour plus d’informations sur la restriction du trafic du WAF vers votre environnement App Service uniquement en utilisant l’adresse IP virtuelle de votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="a50dd-152">Follow the [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic to your App Service Environment from the WAF only by using the VIP address of your Cloud Service.</span></span> <span data-ttu-id="a50dd-153">Voici un exemple de commande Powershell pour effectuer cette tâche pour le port TCP 80.</span><span class="sxs-lookup"><span data-stu-id="a50dd-153">Here's a sample Powershell command for performing this task for TCP port 80.</span></span>

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

<span data-ttu-id="a50dd-154">Remplacez SourceAddressPrefix par l'adresse IP virtuelle (VIP) du service cloud de votre WAF.</span><span class="sxs-lookup"><span data-stu-id="a50dd-154">Replace the SourceAddressPrefix with the Virtual IP Address (VIP) of your WAF's Cloud Service.</span></span>

> <span data-ttu-id="a50dd-155">Remarque : l'adresse IP virtuelle de votre service cloud changera lorsque vous supprimerez et créerez de nouveau le service cloud.</span><span class="sxs-lookup"><span data-stu-id="a50dd-155">Note: The VIP of your Cloud Service will change when you delete and re-create the Cloud Service.</span></span> <span data-ttu-id="a50dd-156">Dans ce cas, veillez à mettre à jour l'adresse IP dans le groupe de ressources réseau.</span><span class="sxs-lookup"><span data-stu-id="a50dd-156">Make sure to update the IP address in the Network Resource group once you do so.</span></span> 
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
