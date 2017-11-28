---
title: "aaaHost plusieurs sites avec la passerelle d’Application Azure | Documents Microsoft"
description: "Cette page fournit des instructions tooconfigure une passerelle d’application Windows Azure existante pour l’hébergement de plusieurs applications web sur hello même passerelle avec hello portail Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 95f892f6-fa27-47ee-b980-7abf4f2c66a9
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 2172aa2c80720f6f1ab7dd91745b44654bcaee00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="fae25-103">Configurer une passerelle Application Gateway existante pour l’hébergement de plusieurs applications web</span><span class="sxs-lookup"><span data-stu-id="fae25-103">Configure an existing application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fae25-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="fae25-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="fae25-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fae25-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

<span data-ttu-id="fae25-106">Hébergement de plusieurs sites vous permet de toodeploy plus d’une application web sur hello même passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="fae25-106">Multiple site hosting allows you toodeploy more than one web application on hello same application gateway.</span></span> <span data-ttu-id="fae25-107">Il s’appuie sur la présence de l’en-tête d’hôte dans la requête HTTP entrante hello, toodetermine quels écouteur reçoit le trafic.</span><span class="sxs-lookup"><span data-stu-id="fae25-107">It relies on presence of host header in hello incoming HTTP request, toodetermine which listener would receive traffic.</span></span> <span data-ttu-id="fae25-108">écouteur de Hello dirige ensuite pool principal de tooappropriate trafic tel que configuré dans la définition des règles de passerelle de hello hello.</span><span class="sxs-lookup"><span data-stu-id="fae25-108">hello listener then directs traffic tooappropriate backend pool as configured in hello rules definition of hello gateway.</span></span> <span data-ttu-id="fae25-109">Dans les applications web SSL est activé, passerelle d’application s’appuie sur hello Indication de nom de serveur (SNI) extension toochoose hello correct écouteur pour le trafic web hello.</span><span class="sxs-lookup"><span data-stu-id="fae25-109">In SSL enabled web applications, application gateway relies on hello Server Name Indication (SNI) extension toochoose hello correct listener for hello web traffic.</span></span> <span data-ttu-id="fae25-110">Une utilisation courante pour l’hébergement de plusieurs sites est équilibrer les demandes de tooload pour les pools de serveur principal toodifferent web différents domaines.</span><span class="sxs-lookup"><span data-stu-id="fae25-110">A common use for multiple site hosting is tooload balance requests for different web domains toodifferent back-end server pools.</span></span> <span data-ttu-id="fae25-111">De même, plusieurs sous-domaines de hello même domaine racine peut également être hébergé sur hello même passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="fae25-111">Similarly multiple subdomains of hello same root domain could also be hosted on hello same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="fae25-112">Scénario</span><span class="sxs-lookup"><span data-stu-id="fae25-112">Scenario</span></span>

<span data-ttu-id="fae25-113">Dans l’exemple suivant de hello, passerelle d’application sert le trafic pour contoso.com et fabrikam.com avec deux pools de serveur principal : contoso pool de serveurs et de pool de serveurs de fabrikam.</span><span class="sxs-lookup"><span data-stu-id="fae25-113">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="fae25-114">Le programme d’installation similaire peut être sous-domaines toohost utilisés comme app.contoso.com et blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="fae25-114">Similar setup could be used toohost subdomains like app.contoso.com and blog.contoso.com.</span></span>

![scénario multisite][multisite]

## <a name="before-you-begin"></a><span data-ttu-id="fae25-116">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="fae25-116">Before you begin</span></span>

<span data-ttu-id="fae25-117">Ce scénario ajoute la prise en charge de plusieurs sites tooan une passerelle d’application existant.</span><span class="sxs-lookup"><span data-stu-id="fae25-117">This scenario adds multi-site support tooan existing application gateway.</span></span> <span data-ttu-id="fae25-118">toocomplete tooconfigure disponible de toobe a besoin de ce scénario, une passerelle d’application existant.</span><span class="sxs-lookup"><span data-stu-id="fae25-118">toocomplete this scenario, an existing application gateway needs toobe available tooconfigure.</span></span> <span data-ttu-id="fae25-119">Visitez [créer une passerelle d’application à l’aide du portail de hello](application-gateway-create-gateway-portal.md) toolearn comment toocreate une passerelle d’application de base dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="fae25-119">Visit [Create an application gateway by using hello portal](application-gateway-create-gateway-portal.md) toolearn how toocreate a basic application gateway in hello portal.</span></span>

<span data-ttu-id="fae25-120">Hello Voici les étapes de hello nécessaires passerelle d’application hello tooupdate :</span><span class="sxs-lookup"><span data-stu-id="fae25-120">hello following are hello steps needed tooupdate hello application gateway:</span></span>

1. <span data-ttu-id="fae25-121">Créer toouse pools du serveur principal pour chaque site.</span><span class="sxs-lookup"><span data-stu-id="fae25-121">Create back-end pools toouse for each site.</span></span>
2. <span data-ttu-id="fae25-122">Créez un écouteur pour chaque site que la passerelle Application Gateway prend en charge.</span><span class="sxs-lookup"><span data-stu-id="fae25-122">Create a listener for each site application gateway supports.</span></span>
3. <span data-ttu-id="fae25-123">Créer règles toomap chaque écouteur et hello approprié back-end.</span><span class="sxs-lookup"><span data-stu-id="fae25-123">Create rules toomap each listener with hello appropriate back-end.</span></span>

## <a name="requirements"></a><span data-ttu-id="fae25-124">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="fae25-124">Requirements</span></span>

* <span data-ttu-id="fae25-125">**Pool de serveur principal :** liste hello des adresses IP des serveurs principaux de hello.</span><span class="sxs-lookup"><span data-stu-id="fae25-125">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="fae25-126">adresses IP de Hello répertoriés doivent appartenir soit de sous-réseau de réseau virtuel toohello ou doivent être une adresse IP/VIP publique.</span><span class="sxs-lookup"><span data-stu-id="fae25-126">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="fae25-127">Le nom de domaine complet peut également être utilisé.</span><span class="sxs-lookup"><span data-stu-id="fae25-127">FQDN can also be used.</span></span>
* <span data-ttu-id="fae25-128">**Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies.</span><span class="sxs-lookup"><span data-stu-id="fae25-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="fae25-129">Ces paramètres sont lié tooa pool et sont des serveurs tooall appliqué dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="fae25-129">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="fae25-130">**Port frontal :** ce port est le port public hello qui est ouvert sur la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="fae25-130">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="fae25-131">Le trafic atteint ce port et obtient redirigés tooone de hello sur les serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="fae25-131">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="fae25-132">**Écouteur :** hello port d’écoute utilise un port frontal, un protocole (Http ou Https, ces valeurs respectent la casse) et le nom du certificat SSL hello (si le déchargement de la configuration de SSL).</span><span class="sxs-lookup"><span data-stu-id="fae25-132">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="fae25-133">Pour les passerelles Application Gateway activées pour plusieurs sites, le nom d’hôte et les indicateurs SNI sont également ajoutés.</span><span class="sxs-lookup"><span data-stu-id="fae25-133">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="fae25-134">**La règle :** règle de hello lie écouteur hello, pool de serveur principal hello et définit le trafic de hello de pool de serveur principal doit être dirigée toowhen il atteint un écouteur particulier.</span><span class="sxs-lookup"><span data-stu-id="fae25-134">**Rule:** hello rule binds hello listener, hello back-end server pool, and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="fae25-135">Les règles sont traitées dans l’ordre de hello qu’ils sont répertoriés, et le trafic est dirigé via hello première règle qui correspond, quelle que soit la spécificité.</span><span class="sxs-lookup"><span data-stu-id="fae25-135">Rules are processed in hello order they are listed, and traffic will be directed via hello first rule that matches regardless of specificity.</span></span> <span data-ttu-id="fae25-136">Par exemple, si vous disposez d’une règle à l’aide d’un écouteur de base et une règle à l’aide d’un écouteur de plusieurs site à la fois sur hello même règle de port, hello avec écouteur de plusieurs sites hello doit figurer avant les règle hello qu’un écouteur de base hello dans l’ordre pour toofunction de règle de plusieurs sites hello en tant que attendu.</span><span class="sxs-lookup"><span data-stu-id="fae25-136">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on hello same port, hello rule with hello multi-site listener must be listed before hello rule with hello basic listener in order for hello multi-site rule toofunction as expected.</span></span> 
* <span data-ttu-id="fae25-137">**Certificats :** chaque écouteur requiert un certificat unique, dans cet exemple, 2 écouteurs sont créés pour plusieurs sites.</span><span class="sxs-lookup"><span data-stu-id="fae25-137">**Certificates:** Each listener requires a unique certificate, in this example 2 listeners are created for multi-site.</span></span> <span data-ttu-id="fae25-138">Deux .pfx certificats et les mots de passe hello pour eux doivent toobe créé.</span><span class="sxs-lookup"><span data-stu-id="fae25-138">Two .pfx certificates and hello passwords for them need toobe created.</span></span>

## <a name="create-back-end-pools-for-each-site"></a><span data-ttu-id="fae25-139">Créer des pools principaux pour chaque site</span><span class="sxs-lookup"><span data-stu-id="fae25-139">Create back-end pools for each site</span></span>

<span data-ttu-id="fae25-140">Un pool principal pour chaque site que cette passerelle Application Gateway prend en charge est nécessaire, dans cet exemple, 2 sont créés : un pour contoso11.com et un fabrikam11.com.</span><span class="sxs-lookup"><span data-stu-id="fae25-140">A back-end pool for each site that application gateway supports is needed, in this case 2 are be created, one for contoso11.com and one for fabrikam11.com.</span></span>

### <a name="step-1"></a><span data-ttu-id="fae25-141">Étape 1</span><span class="sxs-lookup"><span data-stu-id="fae25-141">Step 1</span></span>

<span data-ttu-id="fae25-142">Accédez à passerelle d’application existant tooan Bonjour portail Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fae25-142">Navigate tooan existing application gateway in hello Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="fae25-143">Sélectionnez **Pools principaux** et cliquez sur **Ajouter**</span><span class="sxs-lookup"><span data-stu-id="fae25-143">Select **Backend pools** and click **Add**</span></span>

![ajouter des pools principaux][7]

### <a name="step-2"></a><span data-ttu-id="fae25-145">Étape 2</span><span class="sxs-lookup"><span data-stu-id="fae25-145">Step 2</span></span>

<span data-ttu-id="fae25-146">Renseignez les informations de hello pour le pool principal de hello **pool1**, en ajoutant des adresses ip hello ou des noms de domaine complets pour les serveurs principaux hello et cliquez sur **OK**</span><span class="sxs-lookup"><span data-stu-id="fae25-146">Fill in hello information for hello back-end pool **pool1**, adding hello ip addresses or FQDNs for hello back-end servers and click **OK**</span></span>

![paramètres du pool principal pool1][8]

### <a name="step-3"></a><span data-ttu-id="fae25-148">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="fae25-148">Step 3</span></span>

<span data-ttu-id="fae25-149">Panneau de pools de principaux hello sur **ajouter** tooadd un pool principal supplémentaire **pool2**, en ajoutant des adresses ip hello ou des noms de domaine complets pour les serveurs principaux hello et cliquez sur **OK**</span><span class="sxs-lookup"><span data-stu-id="fae25-149">On hello backend-pools blade click **Add** tooadd an additional back-end pool **pool2**, adding hello ip addresses or FQDNS for hello back-end servers and click **OK**</span></span>

![paramètres du pool principal pool2][9]

## <a name="create-listeners-for-each-back-end"></a><span data-ttu-id="fae25-151">Créer des écouteurs pour chaque serveur principal</span><span class="sxs-lookup"><span data-stu-id="fae25-151">Create listeners for each back-end</span></span>

<span data-ttu-id="fae25-152">Passerelle d’application s’appuie sur HTTP 1.1 hôte en-têtes toohost plus d’un site Web sur hello même adresse IP publique et le port.</span><span class="sxs-lookup"><span data-stu-id="fae25-152">Application Gateway relies on HTTP 1.1 host headers toohost more than one website on hello same public IP address and port.</span></span> <span data-ttu-id="fae25-153">écouteur de base Hello créé dans le portail de hello ne contient pas cette propriété.</span><span class="sxs-lookup"><span data-stu-id="fae25-153">hello basic listener created in hello portal does not contain this property.</span></span>

### <a name="step-1"></a><span data-ttu-id="fae25-154">Étape 1</span><span class="sxs-lookup"><span data-stu-id="fae25-154">Step 1</span></span>

<span data-ttu-id="fae25-155">Cliquez sur **écouteurs** hello passerelle d’application existant et cliquez sur **multisite** premier écouteur de tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="fae25-155">Click **Listeners** on hello existing application gateway and click **Multi-site** tooadd hello first listener.</span></span>

![panneau Vue d’ensemble des écouteurs][1]

### <a name="step-2"></a><span data-ttu-id="fae25-157">Étape 2</span><span class="sxs-lookup"><span data-stu-id="fae25-157">Step 2</span></span>

<span data-ttu-id="fae25-158">Complétez les informations de hello pour le port d’écoute hello.</span><span class="sxs-lookup"><span data-stu-id="fae25-158">Fill out hello information for hello listener.</span></span> <span data-ttu-id="fae25-159">Dans cet exemple la terminaison SSL est configurée, créez un nouveau port de serveur frontal.</span><span class="sxs-lookup"><span data-stu-id="fae25-159">In this example SSL termination is configured, create a new frontend port.</span></span> <span data-ttu-id="fae25-160">Téléchargez toobe de certificat .pfx hello utilisé pour la terminaison SSL.</span><span class="sxs-lookup"><span data-stu-id="fae25-160">Upload hello .pfx certificate toobe used for SSL termination.</span></span> <span data-ttu-id="fae25-161">Hello sur ce panneau d’écouteur de base standard de toohello panneau par rapport diffère uniquement nom d’hôte hello.</span><span class="sxs-lookup"><span data-stu-id="fae25-161">hello only difference on this blade compared toohello standard basic listener blade is hello hostname.</span></span>

![panneau Propriétés d’écouteur][2]

### <a name="step-3"></a><span data-ttu-id="fae25-163">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="fae25-163">Step 3</span></span>

<span data-ttu-id="fae25-164">Cliquez sur **multisite** et créer un autre écouteur comme décrit dans l’étape précédente de hello pour le site de deuxième hello.</span><span class="sxs-lookup"><span data-stu-id="fae25-164">Click **Multi-site** and create another listener as described in hello previous step for hello second site.</span></span> <span data-ttu-id="fae25-165">Assurez-vous que toouse un certificat différent pour l’écouteur de deuxième hello.</span><span class="sxs-lookup"><span data-stu-id="fae25-165">Make sure toouse a different certificate for hello second listener.</span></span> <span data-ttu-id="fae25-166">Hello sur ce panneau d’écouteur de base standard de toohello panneau par rapport diffère uniquement nom d’hôte hello.</span><span class="sxs-lookup"><span data-stu-id="fae25-166">hello only difference on this blade compared toohello standard basic listener blade is hello hostname.</span></span> <span data-ttu-id="fae25-167">Renseignez les informations hello pour le port d’écoute hello et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="fae25-167">Fill out hello information for hello listener and click **OK**.</span></span>

![panneau Propriétés d’écouteur][3]

> [!NOTE]
> <span data-ttu-id="fae25-169">La création d’écouteurs Bonjour portail Azure pour la passerelle d’application est une tâche de longue durée, peut prendre quelques hello toocreate de temps deux écouteurs dans ce scénario.</span><span class="sxs-lookup"><span data-stu-id="fae25-169">Creation of listeners in hello Azure portal for application gateway is a long running task, it may take some time toocreate hello two listeners in this scenario.</span></span> <span data-ttu-id="fae25-170">Lorsque les écouteurs hello complète affichent dans le portail de hello comme Bonjour suivant image :</span><span class="sxs-lookup"><span data-stu-id="fae25-170">When complete hello listeners show in hello portal as seen in hello following image:</span></span>

![vue d’ensemble de l’écouteur][4]

## <a name="create-rules-toomap-listeners-toobackend-pools"></a><span data-ttu-id="fae25-172">Créer des pools de toobackend toomap écouteurs de règles</span><span class="sxs-lookup"><span data-stu-id="fae25-172">Create rules toomap listeners toobackend pools</span></span>

### <a name="step-1"></a><span data-ttu-id="fae25-173">Étape 1</span><span class="sxs-lookup"><span data-stu-id="fae25-173">Step 1</span></span>

<span data-ttu-id="fae25-174">Accédez à passerelle d’application existant tooan Bonjour portail Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fae25-174">Navigate tooan existing application gateway in hello Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="fae25-175">Sélectionnez **règles** , sélectionnez une règle par défaut existant hello **rule1** et cliquez sur **modifier**.</span><span class="sxs-lookup"><span data-stu-id="fae25-175">Select **Rules** and choose hello existing default rule **rule1** and click **Edit**.</span></span>

### <a name="step-2"></a><span data-ttu-id="fae25-176">Étape 2</span><span class="sxs-lookup"><span data-stu-id="fae25-176">Step 2</span></span>

<span data-ttu-id="fae25-177">Remplir le panneau de règles hello comme Bonjour suivant l’image.</span><span class="sxs-lookup"><span data-stu-id="fae25-177">Fill out hello rules blade as seen in hello following image.</span></span> <span data-ttu-id="fae25-178">Choisissez le premier écouteur de hello et premier pool et sur **enregistrer** lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="fae25-178">Choosing hello first listener and first pool and clicking **Save** when complete.</span></span>

![modifier une règle existante][6]

### <a name="step-3"></a><span data-ttu-id="fae25-180">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="fae25-180">Step 3</span></span>

<span data-ttu-id="fae25-181">Cliquez sur **de règles de base** deuxième règle de toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="fae25-181">Click **Basic rule** toocreate hello second rule.</span></span> <span data-ttu-id="fae25-182">Rempliront hello avec hello deuxième port d’écoute et le second pool principal et cliquez sur **OK** toosave.</span><span class="sxs-lookup"><span data-stu-id="fae25-182">Fill out hello form with hello second listener and second backend pool and click **OK** toosave.</span></span>

![panneau ajouter une règle de base][10]

<span data-ttu-id="fae25-184">Ce scénario procède à la configuration d’une passerelle d’application existant avec prise en charge de plusieurs site via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fae25-184">This scenario completes configuring an existing application gateway with multi-site support through hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fae25-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fae25-185">Next steps</span></span>

<span data-ttu-id="fae25-186">Découvrez comment tooprotect vos sites Web avec [passerelle d’Application - pare-feu d’applications Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="fae25-186">Learn how tooprotect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

<!--Image references-->
[1]: ./media/application-gateway-create-multisite-portal/figure1.png
[2]: ./media/application-gateway-create-multisite-portal/figure2.png
[3]: ./media/application-gateway-create-multisite-portal/figure3.png
[4]: ./media/application-gateway-create-multisite-portal/figure4.png
[5]: ./media/application-gateway-create-multisite-portal/figure5.png
[6]: ./media/application-gateway-create-multisite-portal/figure6.png
[7]: ./media/application-gateway-create-multisite-portal/figure7.png
[8]: ./media/application-gateway-create-multisite-portal/figure8.png
[9]: ./media/application-gateway-create-multisite-portal/figure9.png
[10]: ./media/application-gateway-create-multisite-portal/figure10.png
[multisite]: ./media/application-gateway-create-multisite-portal/multisite.png
