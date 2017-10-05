---
title: "Héberger plusieurs sites sur la passerelle Azure Application Gateway | Microsoft Docs"
description: "Cette page fournit des instructions pour configurer une passerelle Application Gateway Azure pour l’hébergement de plusieurs applications web sur la même passerelle avec le portail Azure."
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
ms.openlocfilehash: 84bd62ae17b7f7ba4cd815ef1f9880679607ebce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="7fe18-103">Configurer une passerelle Application Gateway existante pour l’hébergement de plusieurs applications web</span><span class="sxs-lookup"><span data-stu-id="7fe18-103">Configure an existing application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7fe18-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="7fe18-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="7fe18-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7fe18-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

<span data-ttu-id="7fe18-106">L’hébergement de plusieurs sites vous permet de déployer plusieurs applications web sur la même passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7fe18-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span></span> <span data-ttu-id="7fe18-107">Il s’appuie sur la présence de l’en-tête de l’hôte dans la requête HTTP entrante pour déterminer l’écouteur qui doit recevoir le trafic.</span><span class="sxs-lookup"><span data-stu-id="7fe18-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span></span> <span data-ttu-id="7fe18-108">L’écouteur dirige ensuite le trafic vers le pool principal approprié tel que configuré dans la définition des règles de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="7fe18-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span></span> <span data-ttu-id="7fe18-109">Dans les applications web SSL, la passerelle Application Gateway s’appuie sur l’extension d’indication du nom du serveur (SNI) pour choisir l’écouteur approprié au trafic web.</span><span class="sxs-lookup"><span data-stu-id="7fe18-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span></span> <span data-ttu-id="7fe18-110">Une utilisation courante de l’hébergement de plusieurs sites consiste à équilibrer la charge des demandes pour différents domaines Web entre différents pools de serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="7fe18-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span></span> <span data-ttu-id="7fe18-111">De même, plusieurs sous-domaines du même domaine racine pourraient également être hébergés sur la même passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7fe18-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="7fe18-112">Scénario</span><span class="sxs-lookup"><span data-stu-id="7fe18-112">Scenario</span></span>

<span data-ttu-id="7fe18-113">Dans l’exemple suivant, la passerelle Application Gateway gère le trafic pour contoso.com et fabrikam.com avec deux pools de serveurs principaux : un pool de serveurs contoso et un pool de serveurs fabrikam.</span><span class="sxs-lookup"><span data-stu-id="7fe18-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="7fe18-114">Une configuration similaire pourrait servir à héberger des sous-domaines hôtes comme app.contoso.com et blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="7fe18-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span></span>

![scénario multisite][multisite]

## <a name="before-you-begin"></a><span data-ttu-id="7fe18-116">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="7fe18-116">Before you begin</span></span>

<span data-ttu-id="7fe18-117">Ce scénario ajoute la prise en charge de plusieurs sites à une passerelle Application Gateway existante.</span><span class="sxs-lookup"><span data-stu-id="7fe18-117">This scenario adds multi-site support to an existing application gateway.</span></span> <span data-ttu-id="7fe18-118">Pour ce scénario, une passerelle Application Gateway existante doit être disponible pour pouvoir procéder à la configuration.</span><span class="sxs-lookup"><span data-stu-id="7fe18-118">To complete this scenario, an existing application gateway needs to be available to configure.</span></span> <span data-ttu-id="7fe18-119">Consultez [Créer une passerelle Application Gateway à l’aide du portail](application-gateway-create-gateway-portal.md) pour apprendre à créer une passerelle Application Gateway de base dans le portail.</span><span class="sxs-lookup"><span data-stu-id="7fe18-119">Visit [Create an application gateway by using the portal](application-gateway-create-gateway-portal.md) to learn how to create a basic application gateway in the portal.</span></span>

<span data-ttu-id="7fe18-120">Procédez comme suit pour mettre à jour une passerelle Application Gateway :</span><span class="sxs-lookup"><span data-stu-id="7fe18-120">The following are the steps needed to update the application gateway:</span></span>

1. <span data-ttu-id="7fe18-121">Créez des pools principaux à utiliser pour chaque site.</span><span class="sxs-lookup"><span data-stu-id="7fe18-121">Create back-end pools to use for each site.</span></span>
2. <span data-ttu-id="7fe18-122">Créez un écouteur pour chaque site que la passerelle Application Gateway prend en charge.</span><span class="sxs-lookup"><span data-stu-id="7fe18-122">Create a listener for each site application gateway supports.</span></span>
3. <span data-ttu-id="7fe18-123">Créez des règles pour associer chaque écouteur au serveur principal approprié.</span><span class="sxs-lookup"><span data-stu-id="7fe18-123">Create rules to map each listener with the appropriate back-end.</span></span>

## <a name="requirements"></a><span data-ttu-id="7fe18-124">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="7fe18-124">Requirements</span></span>

* <span data-ttu-id="7fe18-125">**Pool de serveurs principaux :** liste des adresses IP des serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="7fe18-125">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="7fe18-126">Les adresses IP répertoriées doivent appartenir au sous-réseau de réseau virtuel ou doivent correspondre à une adresse IP/VIP publique.</span><span class="sxs-lookup"><span data-stu-id="7fe18-126">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="7fe18-127">Le nom de domaine complet peut également être utilisé.</span><span class="sxs-lookup"><span data-stu-id="7fe18-127">FQDN can also be used.</span></span>
* <span data-ttu-id="7fe18-128">**Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies.</span><span class="sxs-lookup"><span data-stu-id="7fe18-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="7fe18-129">Ces paramètres sont liés à un pool et sont appliqués à tous les serveurs du pool.</span><span class="sxs-lookup"><span data-stu-id="7fe18-129">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="7fe18-130">**Port frontal :** il s’agit du port public ouvert sur la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7fe18-130">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="7fe18-131">Le trafic atteint ce port, puis il est redirigé vers l’un des serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="7fe18-131">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="7fe18-132">**Écouteur :** l’écouteur a un port frontal, un protocole (Http ou Https, avec respect de la casse) et le nom du certificat SSL (en cas de configuration du déchargement SSL).</span><span class="sxs-lookup"><span data-stu-id="7fe18-132">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="7fe18-133">Pour les passerelles Application Gateway activées pour plusieurs sites, le nom d’hôte et les indicateurs SNI sont également ajoutés.</span><span class="sxs-lookup"><span data-stu-id="7fe18-133">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="7fe18-134">**Règle :** la règle lie l’écouteur et le pool de serveurs principaux, et définit vers quel pool de serveurs principaux le trafic doit être dirigé quand il atteint un écouteur spécifique.</span><span class="sxs-lookup"><span data-stu-id="7fe18-134">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="7fe18-135">Les règles sont traitées dans l’ordre où elles sont répertoriées, et le trafic est orienté selon la première règle correspondante, quelle que soit sa spécificité.</span><span class="sxs-lookup"><span data-stu-id="7fe18-135">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="7fe18-136">Par exemple, si une règle utilise un écouteur de base et qu’une autre utilise un écouteur multisite sur le même port, la règle avec l’écouteur multisite doit être répertoriée avant la règle avec l’écouteur de base pour que la règle multisite fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="7fe18-136">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span> 
* <span data-ttu-id="7fe18-137">**Certificats :** chaque écouteur requiert un certificat unique, dans cet exemple, 2 écouteurs sont créés pour plusieurs sites.</span><span class="sxs-lookup"><span data-stu-id="7fe18-137">**Certificates:** Each listener requires a unique certificate, in this example 2 listeners are created for multi-site.</span></span> <span data-ttu-id="7fe18-138">Deux certificats .pfx et leurs mots de passe doivent être créés.</span><span class="sxs-lookup"><span data-stu-id="7fe18-138">Two .pfx certificates and the passwords for them need to be created.</span></span>

## <a name="create-back-end-pools-for-each-site"></a><span data-ttu-id="7fe18-139">Créer des pools principaux pour chaque site</span><span class="sxs-lookup"><span data-stu-id="7fe18-139">Create back-end pools for each site</span></span>

<span data-ttu-id="7fe18-140">Un pool principal pour chaque site que cette passerelle Application Gateway prend en charge est nécessaire, dans cet exemple, 2 sont créés : un pour contoso11.com et un fabrikam11.com.</span><span class="sxs-lookup"><span data-stu-id="7fe18-140">A back-end pool for each site that application gateway supports is needed, in this case 2 are be created, one for contoso11.com and one for fabrikam11.com.</span></span>

### <a name="step-1"></a><span data-ttu-id="7fe18-141">Étape 1 :</span><span class="sxs-lookup"><span data-stu-id="7fe18-141">Step 1</span></span>

<span data-ttu-id="7fe18-142">Accédez à une passerelle Application Gateway existante dans le portail Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7fe18-142">Navigate to an existing application gateway in the Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="7fe18-143">Sélectionnez **Pools principaux** et cliquez sur **Ajouter**</span><span class="sxs-lookup"><span data-stu-id="7fe18-143">Select **Backend pools** and click **Add**</span></span>

![ajouter des pools principaux][7]

### <a name="step-2"></a><span data-ttu-id="7fe18-145">Étape 2</span><span class="sxs-lookup"><span data-stu-id="7fe18-145">Step 2</span></span>

<span data-ttu-id="7fe18-146">Fournissez les informations sur le pool principal **pool1**, en ajoutant les adresses IP ou les noms de domaine complets des serveurs principaux, puis cliquez sur **OK**</span><span class="sxs-lookup"><span data-stu-id="7fe18-146">Fill in the information for the back-end pool **pool1**, adding the ip addresses or FQDNs for the back-end servers and click **OK**</span></span>

![paramètres du pool principal pool1][8]

### <a name="step-3"></a><span data-ttu-id="7fe18-148">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="7fe18-148">Step 3</span></span>

<span data-ttu-id="7fe18-149">Dans le panneau des pools principals, cliquez sur **Ajouter** pour ajouter un autre pool principal, **pool2**, en ajoutant les adresses IP ou les noms de domaine complets des serveurs principaux, puis cliquez sur **OK**</span><span class="sxs-lookup"><span data-stu-id="7fe18-149">On the backend-pools blade click **Add** to add an additional back-end pool **pool2**, adding the ip addresses or FQDNS for the back-end servers and click **OK**</span></span>

![paramètres du pool principal pool2][9]

## <a name="create-listeners-for-each-back-end"></a><span data-ttu-id="7fe18-151">Créer des écouteurs pour chaque serveur principal</span><span class="sxs-lookup"><span data-stu-id="7fe18-151">Create listeners for each back-end</span></span>

<span data-ttu-id="7fe18-152">Application Gateway se base sur des en-têtes d’hôte HTTP 1.1 pour héberger plusieurs sites web sur les mêmes adresses IP et port.</span><span class="sxs-lookup"><span data-stu-id="7fe18-152">Application Gateway relies on HTTP 1.1 host headers to host more than one website on the same public IP address and port.</span></span> <span data-ttu-id="7fe18-153">L’écouteur de base créé dans le portail ne contient pas cette propriété.</span><span class="sxs-lookup"><span data-stu-id="7fe18-153">The basic listener created in the portal does not contain this property.</span></span>

### <a name="step-1"></a><span data-ttu-id="7fe18-154">Étape 1</span><span class="sxs-lookup"><span data-stu-id="7fe18-154">Step 1</span></span>

<span data-ttu-id="7fe18-155">Cliquez sur **Écouteurs** sur la passerelle Application Gateway existante et cliquez sur **Multisite** pour ajouter le premier écouteur.</span><span class="sxs-lookup"><span data-stu-id="7fe18-155">Click **Listeners** on the existing application gateway and click **Multi-site** to add the first listener.</span></span>

![panneau Vue d’ensemble des écouteurs][1]

### <a name="step-2"></a><span data-ttu-id="7fe18-157">Étape 2 :</span><span class="sxs-lookup"><span data-stu-id="7fe18-157">Step 2</span></span>

<span data-ttu-id="7fe18-158">Fournissez les informations sur l’écouteur.</span><span class="sxs-lookup"><span data-stu-id="7fe18-158">Fill out the information for the listener.</span></span> <span data-ttu-id="7fe18-159">Dans cet exemple la terminaison SSL est configurée, créez un nouveau port de serveur frontal.</span><span class="sxs-lookup"><span data-stu-id="7fe18-159">In this example SSL termination is configured, create a new frontend port.</span></span> <span data-ttu-id="7fe18-160">Téléchargez le certificat .pfx à utiliser pour la terminaison SSL.</span><span class="sxs-lookup"><span data-stu-id="7fe18-160">Upload the .pfx certificate to be used for SSL termination.</span></span> <span data-ttu-id="7fe18-161">La seule différence dans ce panneau par rapport au panneau d’écouteur de base standard est le nom d’hôte.</span><span class="sxs-lookup"><span data-stu-id="7fe18-161">The only difference on this blade compared to the standard basic listener blade is the hostname.</span></span>

![panneau Propriétés d’écouteur][2]

### <a name="step-3"></a><span data-ttu-id="7fe18-163">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="7fe18-163">Step 3</span></span>

<span data-ttu-id="7fe18-164">Cliquez sur **Multisite** et créez un autre écouteur comme décrit dans l’étape précédente pour le deuxième site.</span><span class="sxs-lookup"><span data-stu-id="7fe18-164">Click **Multi-site** and create another listener as described in the previous step for the second site.</span></span> <span data-ttu-id="7fe18-165">Veillez à utiliser un certificat différent pour le deuxième écouteur.</span><span class="sxs-lookup"><span data-stu-id="7fe18-165">Make sure to use a different certificate for the second listener.</span></span> <span data-ttu-id="7fe18-166">La seule différence dans ce panneau par rapport au panneau d’écouteur de base standard est le nom d’hôte.</span><span class="sxs-lookup"><span data-stu-id="7fe18-166">The only difference on this blade compared to the standard basic listener blade is the hostname.</span></span> <span data-ttu-id="7fe18-167">Fournissez les informations sur l’écouteur et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7fe18-167">Fill out the information for the listener and click **OK**.</span></span>

![panneau Propriétés d’écouteur][3]

> [!NOTE]
> <span data-ttu-id="7fe18-169">La création d’écouteurs dans le portail Azure pour la passerelle Application Gateway est une tâche longue. Un certain temps peut être nécessaire pour créer les deux écouteurs dans ce scénario.</span><span class="sxs-lookup"><span data-stu-id="7fe18-169">Creation of listeners in the Azure portal for application gateway is a long running task, it may take some time to create the two listeners in this scenario.</span></span> <span data-ttu-id="7fe18-170">Une fois la tâche terminée, les écouteurs s’affichent dans le portail comme indiqué dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="7fe18-170">When complete the listeners show in the portal as seen in the following image:</span></span>

![vue d’ensemble de l’écouteur][4]

## <a name="create-rules-to-map-listeners-to-backend-pools"></a><span data-ttu-id="7fe18-172">Créer des règles pour associer des écouteurs aux pools principaux</span><span class="sxs-lookup"><span data-stu-id="7fe18-172">Create rules to map listeners to backend pools</span></span>

### <a name="step-1"></a><span data-ttu-id="7fe18-173">Étape 1</span><span class="sxs-lookup"><span data-stu-id="7fe18-173">Step 1</span></span>

<span data-ttu-id="7fe18-174">Accédez à une passerelle Application Gateway existante dans le portail Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7fe18-174">Navigate to an existing application gateway in the Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="7fe18-175">Sélectionnez **Règles** et choisissez la règle existante par défaut **rule1**, puis cliquez sur **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="7fe18-175">Select **Rules** and choose the existing default rule **rule1** and click **Edit**.</span></span>

### <a name="step-2"></a><span data-ttu-id="7fe18-176">Étape 2</span><span class="sxs-lookup"><span data-stu-id="7fe18-176">Step 2</span></span>

<span data-ttu-id="7fe18-177">Renseignez le panneau des règles comme indiqué dans l’image suivante.</span><span class="sxs-lookup"><span data-stu-id="7fe18-177">Fill out the rules blade as seen in the following image.</span></span> <span data-ttu-id="7fe18-178">Choisissez le premier écouteur et le premier pool, puis cliquez sur **Enregistrer** lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="7fe18-178">Choosing the first listener and first pool and clicking **Save** when complete.</span></span>

![modifier une règle existante][6]

### <a name="step-3"></a><span data-ttu-id="7fe18-180">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="7fe18-180">Step 3</span></span>

<span data-ttu-id="7fe18-181">Cliquez sur **Règle de base** pour créer la deuxième règle.</span><span class="sxs-lookup"><span data-stu-id="7fe18-181">Click **Basic rule** to create the second rule.</span></span> <span data-ttu-id="7fe18-182">Remplissez le formulaire avec le deuxième écouteur et le deuxième pool principal, puis cliquez sur **OK** à enregistrer.</span><span class="sxs-lookup"><span data-stu-id="7fe18-182">Fill out the form with the second listener and second backend pool and click **OK** to save.</span></span>

![panneau ajouter une règle de base][10]

<span data-ttu-id="7fe18-184">La configuration d’une passerelle Application Gateway existante avec la prise en charge de plusieurs sites via le portail Azure est terminée par ce scénario.</span><span class="sxs-lookup"><span data-stu-id="7fe18-184">This scenario completes configuring an existing application gateway with multi-site support through the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fe18-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7fe18-185">Next steps</span></span>

<span data-ttu-id="7fe18-186">Découvrez comment protéger vos sites web grâce au [Pare-feu d’applications web sur Application Gateway](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7fe18-186">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

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
