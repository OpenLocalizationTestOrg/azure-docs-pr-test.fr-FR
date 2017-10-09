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
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a><span data-ttu-id="05f56-103">Configuration d'un pare-feu d'applications Web (WAF) pour un environnement App Service</span><span class="sxs-lookup"><span data-stu-id="05f56-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="05f56-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="05f56-104">Overview</span></span>
<span data-ttu-id="05f56-105">Web pare-feux de l’application comme hello [WAF Barracuda pour Azure](https://www.barracuda.com/programs/azure) qui est disponible sur hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) vous aide à sécuriser vos applications web en examinant tooblock de trafic web entrant SQL injections, scripts entre sites, des téléchargements de programmes malveillants & application DDoS et autres attaques.</span><span class="sxs-lookup"><span data-stu-id="05f56-105">Web application firewalls like hello [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that is available on hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helps secure your web applications by inspecting inbound web traffic tooblock SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span></span> <span data-ttu-id="05f56-106">Il examine également réponses hello à partir de serveurs web principal de hello pour Data Loss Prevention (DLP).</span><span class="sxs-lookup"><span data-stu-id="05f56-106">It also inspects hello responses from hello back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="05f56-107">Combiné avec l’isolation de hello et la mise à l’échelle supplémentaire fournie par les environnements App Service, cela fournit un environnement idéal toohost métier critiques web applications nécessitant les requêtes malveillantes toowithstand et volume de trafic élevé.</span><span class="sxs-lookup"><span data-stu-id="05f56-107">Combined with hello isolation and additional scaling provided by App Service Environments, this provides an ideal environment toohost business critical web applications that need toowithstand malicious requests and high volume traffic.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a><span data-ttu-id="05f56-108">Paramétrage</span><span class="sxs-lookup"><span data-stu-id="05f56-108">Setup</span></span>
<span data-ttu-id="05f56-109">Pour ce document, nous allons configurer notre environnement App Service derrière la charge de plusieurs équilibrée des instances de Barracuda WAF afin que seul le trafic à partir de hello WAF peut atteindre hello environnement App Service et il ne sera pas accessible à partir de hello réseau de périmètre.</span><span class="sxs-lookup"><span data-stu-id="05f56-109">For this document we will configure our App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from hello WAF can reach hello App Service Environment and it will not be accessible from hello DMZ.</span></span> <span data-ttu-id="05f56-110">Il nous faudra également Azure Traffic Manager devant notre solde de tooload Barracuda WAF instances entre les centres de données Azure et les régions.</span><span class="sxs-lookup"><span data-stu-id="05f56-110">We will also have Azure Traffic Manager in front of our Barracuda WAF instances tooload balance across Azure data centers and regions.</span></span> <span data-ttu-id="05f56-111">Un diagramme de haut niveau de l’installation de hello ressemble à ce qui est indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="05f56-111">A high level diagram of hello setup would look like what is shown below.</span></span>

![Architecture][Architecture] 

> <span data-ttu-id="05f56-113">Remarque : avec l’introduction de hello de [prennent en charge de l’équilibrage de charge interne pour l’environnement App Service](app-service-environment-with-internal-load-balancer.md), vous pouvez configurer toobe hello ASE inaccessible à partir de hello réseau de périmètre et être uniquement le réseau privé de toohello disponibles.</span><span class="sxs-lookup"><span data-stu-id="05f56-113">Note: With hello introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure hello ASE toobe inaccessible from hello DMZ and only be available toohello private network.</span></span> 
> 
> 

## <a name="configuring-your-app-service-environment"></a><span data-ttu-id="05f56-114">Configuration de votre environnement App Service</span><span class="sxs-lookup"><span data-stu-id="05f56-114">Configuring your App Service Environment</span></span>
<span data-ttu-id="05f56-115">tooconfigure un environnement App Service font référence trop[notre documentation](app-service-web-how-to-create-an-app-service-environment.md) sur le sujet de hello.</span><span class="sxs-lookup"><span data-stu-id="05f56-115">tooconfigure an App Service Environment refer too[our documentation](app-service-web-how-to-create-an-app-service-environment.md) on hello subject.</span></span> <span data-ttu-id="05f56-116">Une fois que vous avez un environnement App Service créé, vous pouvez créer [Web Apps](app-service-web-overview.md), [applications API](../app-service-api/app-service-api-apps-why-best-platform.md) et [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) dans cet environnement qui sera être protégé derrière hello WAF nous configurer dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="05f56-116">Once you have an App Service Environment created, you can create [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind hello WAF we configure in hello next section.</span></span>

## <a name="configuring-your-barracuda-waf-cloud-service"></a><span data-ttu-id="05f56-117">Configuration de votre service cloud WAF Barracuda</span><span class="sxs-lookup"><span data-stu-id="05f56-117">Configuring your Barracuda WAF Cloud Service</span></span>
<span data-ttu-id="05f56-118">Barracuda propose un [article détaillé](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) sur le déploiement de son WAF sur une machine virtuelle dans Azure.</span><span class="sxs-lookup"><span data-stu-id="05f56-118">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span></span> <span data-ttu-id="05f56-119">Mais étant donné que la redondance et nous pas introduire un point de défaillance unique, instance de WAF toodeploy au moins 2 machines virtuelles dans hello même Service Cloud lorsque suivant ces instructions.</span><span class="sxs-lookup"><span data-stu-id="05f56-119">But because we want redundancy and not introduce a single point of failure, you want toodeploy at least 2 WAF instance VMs into hello same Cloud Service when following these instructions.</span></span>

### <a name="adding-endpoints-toocloud-service"></a><span data-ttu-id="05f56-120">Ajout de points de terminaison tooCloud Service</span><span class="sxs-lookup"><span data-stu-id="05f56-120">Adding Endpoints tooCloud Service</span></span>
<span data-ttu-id="05f56-121">Une fois que vous avez 2 ou plus WAF VM instances dans votre Service Cloud, vous pouvez utiliser hello [portail Azure](https://portal.azure.com/) tooadd HTTP et HTTPS points de terminaison qui sont utilisées par votre application, comme indiqué dans l’image hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="05f56-121">Once you have 2 or more WAF VM instances in your Cloud Service you can use hello [Azure portal](https://portal.azure.com/) tooadd HTTP and HTTPS endpoints that are used by your application as shown in hello image below.</span></span>

![Configurer le point de terminaison][ConfigureEndpoint]

<span data-ttu-id="05f56-123">Si vos applications utilisent les autres points de terminaison, assurez-vous que tooadd ces liste toothis ainsi.</span><span class="sxs-lookup"><span data-stu-id="05f56-123">If your applications use other endpoints, make sure tooadd those toothis list as well.</span></span> 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a><span data-ttu-id="05f56-124">Configuration du WAF Barracuda avec son portail de gestion</span><span class="sxs-lookup"><span data-stu-id="05f56-124">Configuring Barracuda WAF through its Management Portal</span></span>
<span data-ttu-id="05f56-125">Le WAF Barracuda utilise le port TCP 8000 pour sa configuration avec le portail de gestion.</span><span class="sxs-lookup"><span data-stu-id="05f56-125">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span></span> <span data-ttu-id="05f56-126">Comme il y a plusieurs instances de machines virtuelles de hello WAF vous aurez besoin des étapes hello toorepeat pour chaque instance de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="05f56-126">Since we have multiple instances of hello WAF VMs you will need toorepeat hello steps here for each VM instance.</span></span> 

> <span data-ttu-id="05f56-127">Remarque : Une fois que vous avez terminé avec une configuration WAF, supprimez point de terminaison TCP/8000 hello de tous les tookeep de vos machines virtuelles de WAF votre WAF sécurisé.</span><span class="sxs-lookup"><span data-stu-id="05f56-127">Note: Once you are done with WAF configuration, remove hello TCP/8000 endpoint from all your WAF VMs tookeep your WAF secure.</span></span>
> 
> 

<span data-ttu-id="05f56-128">Ajouter un point de terminaison de gestion de hello comme indiqué dans l’image hello ci-dessous tooconfigure votre WAF Barracuda.</span><span class="sxs-lookup"><span data-stu-id="05f56-128">Add hello management endpoint as shown in hello image below tooconfigure your Barracuda WAF.</span></span>

![Ajouter un point de terminaison de gestion][AddManagementEndpoint]

<span data-ttu-id="05f56-130">Utilisez un point de terminaison de la gestion de toohello de navigateur toobrowse sur votre Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="05f56-130">Use a browser toobrowse toohello management endpoint on your Cloud Service.</span></span> <span data-ttu-id="05f56-131">Si votre Service Cloud est appelé test.cloudapp.net, vous pouvez accéder à ce point de terminaison en parcourant toohttp://test.cloudapp.net:8000.</span><span class="sxs-lookup"><span data-stu-id="05f56-131">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing toohttp://test.cloudapp.net:8000.</span></span> <span data-ttu-id="05f56-132">Vous devez voir une page de connexion comme ci-dessous, que vous pouvez vous connecter à l’aide des informations d’identification que vous avez spécifié dans la phase d’installation hello WAF machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="05f56-132">You should see a login page like below that you can login using credentials you specified in hello WAF VM setup phase.</span></span>

![Page de connexion à la gestion][ManagementLoginPage]

<span data-ttu-id="05f56-134">Une fois connexion vous devez normalement voir un tableau de bord hello une image hello ci-dessous, qui présente des statistiques de base sur la protection de WAF de hello.</span><span class="sxs-lookup"><span data-stu-id="05f56-134">Once you login you should see a dashboard as hello one in hello image below that will present basic statistics about hello WAF protection.</span></span>

![Tableau de bord de gestion][ManagementDashboard]

<span data-ttu-id="05f56-136">En cliquant sur l’onglet Services de hello vous permettent de configurer votre WAF pour les services qu’il protège.</span><span class="sxs-lookup"><span data-stu-id="05f56-136">Clicking on hello Services tab will let you configure your WAF for services it is protecting.</span></span> <span data-ttu-id="05f56-137">Pour plus d’informations sur la configuration de votre WAF Barracuda, consultez [la documentation appropriée](https://techlib.barracuda.com/waf/getstarted1).</span><span class="sxs-lookup"><span data-stu-id="05f56-137">For more details on configuring your Barracuda WAF you can consult [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span></span> <span data-ttu-id="05f56-138">Dans l’exemple hello ci-dessous, une application Web Azure desservant le trafic sur HTTP et HTTPS a été configuré.</span><span class="sxs-lookup"><span data-stu-id="05f56-138">In hello example below an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span></span>

![Ajouter des services de gestion][ManagementAddServices]

> <span data-ttu-id="05f56-140">Remarque : Selon la façon dont vos applications sont configurées et les fonctionnalités qui sont utilisées dans votre environnement App Service, vous devrez tooforward trafic pour des ports TCP autre que 80 et 443, par exemple, si vous avez le programme d’installation de IP SSL pour une application Web.</span><span class="sxs-lookup"><span data-stu-id="05f56-140">Note: Depending on how your applications are configured and what features are being used in your App Service Environment, you will need tooforward traffic for TCP ports other than 80 and 443, e.g. if you have IP SSL setup for a Web App.</span></span> <span data-ttu-id="05f56-141">Pour obtenir la liste des ports réseau utilisé dans des environnements de Service d’application, consultez trop[la documentation du trafic entrant de contrôle](app-service-app-service-environment-control-inbound-traffic.md) section Ports de réseau.</span><span class="sxs-lookup"><span data-stu-id="05f56-141">For a list of network ports used in App Service Environments, please refer too[Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span></span>
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a><span data-ttu-id="05f56-142">Configuration de Microsoft Azure Traffic Manager (FACULTATIF)</span><span class="sxs-lookup"><span data-stu-id="05f56-142">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span></span>
<span data-ttu-id="05f56-143">Si votre application est disponible dans plusieurs régions, vous souhaiteriez solde de tooload leur derrière [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="05f56-143">If your application is available in multiple regions, then you would want tooload balance them behind [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span></span> <span data-ttu-id="05f56-144">toodo afin que vous pouvez ajouter un point de terminaison Bonjour [portail Azure classic](https://manage.azure.com) à l’aide de nom du Service Cloud pour votre WAF hello dans le profil Traffic Manager hello comme indiqué dans l’image hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="05f56-144">toodo so you can add an endpoint in hello [Azure classic portal](https://manage.azure.com) using hello Cloud Service name for your WAF in hello Traffic Manager profile as shown in hello image below.</span></span> 

![Point de terminaison Traffic Manager][TrafficManagerEndpoint]

<span data-ttu-id="05f56-146">Si votre application requiert une authentification, assurez-vous de qu'avoir certaines ressources qui ne nécessite pas d’authentification pour tooping Traffic Manager pour la disponibilité hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="05f56-146">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager tooping for hello availability of your application.</span></span> <span data-ttu-id="05f56-147">Vous pouvez configurer des URL hello sous la section de configuration de hello sur hello [portail Azure classic](https://manage.azure.com) comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="05f56-147">You can configure hello URL under hello Configure section on hello [Azure classic portal](https://manage.azure.com) as shown below.</span></span>

![Configuration de Traffic Manager][ConfigureTrafficManager]

<span data-ttu-id="05f56-149">tooforward hello Traffic Manager les tests ping à partir de votre application de tooyour WAF, vous devez les traductions du site Web toosetup dans votre Barracuda WAF tooforward trafic tooyour l’application comme indiqué dans l’exemple hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="05f56-149">tooforward hello Traffic Manager pings from your WAF tooyour application, you need toosetup Website Translations on your Barracuda WAF tooforward traffic tooyour application as shown in hello example below.</span></span>

![Traductions de site Web][WebsiteTranslations]

## <a name="securing-traffic-tooapp-service-environment-using-network-security-groups-nsg"></a><span data-ttu-id="05f56-151">Sécuriser le trafic tooApp Service environnement à l’aide de réseau sécurité groupes (NSG)</span><span class="sxs-lookup"><span data-stu-id="05f56-151">Securing Traffic tooApp Service Environment Using Network Security Groups (NSG)</span></span>
<span data-ttu-id="05f56-152">Suivez hello [documentation de trafic entrant de contrôle](app-service-app-service-environment-control-inbound-traffic.md) pour plus d’informations sur la limitation du trafic tooyour environnement App Service à partir de hello WAF uniquement à l’aide d’adresse hello adresse IP virtuelle de votre Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="05f56-152">Follow hello [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic tooyour App Service Environment from hello WAF only by using hello VIP address of your Cloud Service.</span></span> <span data-ttu-id="05f56-153">Voici un exemple de commande Powershell pour effectuer cette tâche pour le port TCP 80.</span><span class="sxs-lookup"><span data-stu-id="05f56-153">Here's a sample Powershell command for performing this task for TCP port 80.</span></span>

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

<span data-ttu-id="05f56-154">Remplacez hello SourceAddressPrefix hello adresse IP virtuelle (VIP) du Service de Cloud de votre WAF.</span><span class="sxs-lookup"><span data-stu-id="05f56-154">Replace hello SourceAddressPrefix with hello Virtual IP Address (VIP) of your WAF's Cloud Service.</span></span>

> <span data-ttu-id="05f56-155">Remarque : hello adresse IP virtuelle de votre Service Cloud changent lorsque vous supprimez et recréez hello Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="05f56-155">Note: hello VIP of your Cloud Service will change when you delete and re-create hello Cloud Service.</span></span> <span data-ttu-id="05f56-156">Assurez-vous que tooupdate hello adresse du groupe de ressources de réseau de hello après cette opération.</span><span class="sxs-lookup"><span data-stu-id="05f56-156">Make sure tooupdate hello IP address in hello Network Resource group once you do so.</span></span> 
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
