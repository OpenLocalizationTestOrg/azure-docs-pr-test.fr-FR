---
title: application de conteneur DC/OS aaaEnable access tooAzure | Documents Microsoft
description: "Comment tooenable public accéder aux conteneurs tooDC/système d’exploitation dans le Service de conteneur Azure."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: Docker, conteneurs, micro-services, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 1ba251ba5a176a6a5e1c7831655164e380a62b27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-public-access-tooan-azure-container-service-application"></a><span data-ttu-id="31048-104">Activer l’application de Service de conteneur Azure tooan accès public</span><span class="sxs-lookup"><span data-stu-id="31048-104">Enable public access tooan Azure Container Service application</span></span>
<span data-ttu-id="31048-105">N’importe quel conteneur de contrôleur de domaine/système d’exploitation Bonjour ACS [pool d’agents publics](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) est exposé automatiquement toohello internet.</span><span class="sxs-lookup"><span data-stu-id="31048-105">Any DC/OS container in hello ACS [public agent pool](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) is automatically exposed toohello internet.</span></span> <span data-ttu-id="31048-106">Par défaut, les ports **80**, **443**, **8080** sont ouverts, et tous les conteneurs (publics) à l’écoute sur ces ports sont accessibles.</span><span class="sxs-lookup"><span data-stu-id="31048-106">By default, ports **80**, **443**, **8080** are opened, and any (public) container listening on those ports are accessible.</span></span> <span data-ttu-id="31048-107">Cet article vous explique comment tooopen ports plus pour vos applications dans le conteneur de Service Azure.</span><span class="sxs-lookup"><span data-stu-id="31048-107">This article shows you how tooopen more ports for your applications in Azure Container Service.</span></span>

## <a name="open-a-port-portal"></a><span data-ttu-id="31048-108">Ouvrir un port (portail)</span><span class="sxs-lookup"><span data-stu-id="31048-108">Open a port (portal)</span></span>
<span data-ttu-id="31048-109">Tout d’abord, nous avons besoin du port de hello tooopen que nous voulons.</span><span class="sxs-lookup"><span data-stu-id="31048-109">First, we need tooopen hello port we want.</span></span>

1. <span data-ttu-id="31048-110">Ouvrez une session dans toohello portal.</span><span class="sxs-lookup"><span data-stu-id="31048-110">Log in toohello portal.</span></span>
2. <span data-ttu-id="31048-111">Groupe de ressources hello recherche que vous avez déployé Bonjour Azure conteneur de Service.</span><span class="sxs-lookup"><span data-stu-id="31048-111">Find hello resource group that you deployed hello Azure Container Service to.</span></span>
3. <span data-ttu-id="31048-112">Sélectionnez l’équilibrage de charge de l’agent hello (qui est le même nom trop**XXXX-agent-lb-XXXX**).</span><span class="sxs-lookup"><span data-stu-id="31048-112">Select hello agent load balancer (which is named similar too**XXXX-agent-lb-XXXX**).</span></span>
   
    ![Équilibrage de charge dans Azure Container Service](./media/container-service-enable-public-access/agent-load-balancer.png)
4. <span data-ttu-id="31048-114">Cliquez sur **Sondes**, puis sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="31048-114">Click **Probes** and then **Add**.</span></span>
   
    ![Sondes d’équilibrage de charge dans Azure Container Service](./media/container-service-enable-public-access/add-probe.png)
5. <span data-ttu-id="31048-116">Remplissez le formulaire de sonde hello et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="31048-116">Fill out hello probe form and click **OK**.</span></span>
   
   | <span data-ttu-id="31048-117">Champ</span><span class="sxs-lookup"><span data-stu-id="31048-117">Field</span></span> | <span data-ttu-id="31048-118">Description</span><span class="sxs-lookup"><span data-stu-id="31048-118">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="31048-119">Nom</span><span class="sxs-lookup"><span data-stu-id="31048-119">Name</span></span> |<span data-ttu-id="31048-120">Un nom descriptif de sonde de hello.</span><span class="sxs-lookup"><span data-stu-id="31048-120">A descriptive name of hello probe.</span></span> |
   | <span data-ttu-id="31048-121">Port</span><span class="sxs-lookup"><span data-stu-id="31048-121">Port</span></span> |<span data-ttu-id="31048-122">port Hello hello conteneur tootest.</span><span class="sxs-lookup"><span data-stu-id="31048-122">hello port of hello container tootest.</span></span> |
   | <span data-ttu-id="31048-123">Chemin</span><span class="sxs-lookup"><span data-stu-id="31048-123">Path</span></span> |<span data-ttu-id="31048-124">(En mode HTTP) hello tooprobe de chemin d’accès relatif de site Web.</span><span class="sxs-lookup"><span data-stu-id="31048-124">(When in HTTP mode) hello relative website path tooprobe.</span></span> <span data-ttu-id="31048-125">HTTPS non pris en charge.</span><span class="sxs-lookup"><span data-stu-id="31048-125">HTTPS not supported.</span></span> |
   | <span data-ttu-id="31048-126">Intervalle</span><span class="sxs-lookup"><span data-stu-id="31048-126">Interval</span></span> |<span data-ttu-id="31048-127">Durée Hello entre sonde tentatives en secondes.</span><span class="sxs-lookup"><span data-stu-id="31048-127">hello amount of time between probe attempts, in seconds.</span></span> |
   | <span data-ttu-id="31048-128">Seuil de défaillance sur le plan de l’intégrité</span><span class="sxs-lookup"><span data-stu-id="31048-128">Unhealthy threshold</span></span> |<span data-ttu-id="31048-129">Nombre de sonde consécutifs tentatives avant de considérer le conteneur de hello défectueux.</span><span class="sxs-lookup"><span data-stu-id="31048-129">Number of consecutive probe attempts before considering hello container unhealthy.</span></span> |
6. <span data-ttu-id="31048-130">Retour sur les propriétés de hello d’équilibrage de charge de l’agent de hello, cliquez sur **règles d’équilibrage de charge** , puis **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="31048-130">Back at hello properties of hello agent load balancer, click **Load balancing rules** and then **Add**.</span></span>
   
    ![Règles d’équilibrage de charge dans Azure Container Service](./media/container-service-enable-public-access/add-balancer-rule.png)
7. <span data-ttu-id="31048-132">Remplissez le formulaire d’équilibrage de charge hello et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="31048-132">Fill out hello load balancer form and click **OK**.</span></span>
   
   | <span data-ttu-id="31048-133">Champ</span><span class="sxs-lookup"><span data-stu-id="31048-133">Field</span></span> | <span data-ttu-id="31048-134">Description</span><span class="sxs-lookup"><span data-stu-id="31048-134">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="31048-135">Nom</span><span class="sxs-lookup"><span data-stu-id="31048-135">Name</span></span> |<span data-ttu-id="31048-136">Un nom descriptif d’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="31048-136">A descriptive name of hello load balancer.</span></span> |
   | <span data-ttu-id="31048-137">Port</span><span class="sxs-lookup"><span data-stu-id="31048-137">Port</span></span> |<span data-ttu-id="31048-138">Hello publique le port entrant.</span><span class="sxs-lookup"><span data-stu-id="31048-138">hello public incoming port.</span></span> |
   | <span data-ttu-id="31048-139">Port principal</span><span class="sxs-lookup"><span data-stu-id="31048-139">Backend port</span></span> |<span data-ttu-id="31048-140">port public interne Hello hello conteneur tooroute le trafic.</span><span class="sxs-lookup"><span data-stu-id="31048-140">hello internal-public port of hello container tooroute traffic to.</span></span> |
   | <span data-ttu-id="31048-141">Pool principal</span><span class="sxs-lookup"><span data-stu-id="31048-141">Backend pool</span></span> |<span data-ttu-id="31048-142">conteneurs Hello dans ce pool seront cible hello pour cet équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="31048-142">hello containers in this pool will be hello target for this load balancer.</span></span> |
   | <span data-ttu-id="31048-143">Sonde</span><span class="sxs-lookup"><span data-stu-id="31048-143">Probe</span></span> |<span data-ttu-id="31048-144">Hello toodetermine de sonde utilisée si une cible Bonjour **pool principal** est sain.</span><span class="sxs-lookup"><span data-stu-id="31048-144">hello probe used toodetermine if a target in hello **Backend pool** is healthy.</span></span> |
   | <span data-ttu-id="31048-145">Persistance de session</span><span class="sxs-lookup"><span data-stu-id="31048-145">Session persistence</span></span> |<span data-ttu-id="31048-146">Détermine comment le trafic à partir d’un client doit être géré pour la durée de session de hello hello.</span><span class="sxs-lookup"><span data-stu-id="31048-146">Determines how traffic from a client should be handled for hello duration of hello session.</span></span><br><br><span data-ttu-id="31048-147">**Aucun**: les demandes successives d’hello même client peut être gérée par n’importe quel conteneur.</span><span class="sxs-lookup"><span data-stu-id="31048-147">**None**: Successive requests from hello same client can be handled by any container.</span></span><br><span data-ttu-id="31048-148">**Client IP**: les demandes successives d’hello même adresse IP du client sont gérées par hello même conteneur.</span><span class="sxs-lookup"><span data-stu-id="31048-148">**Client IP**: Successive requests from hello same client IP are handled by hello same container.</span></span><br><span data-ttu-id="31048-149">**Client IP et le protocole**: les demandes successives d’hello même combinaison d’adresse IP et le protocole du client sont gérées par hello même conteneur.</span><span class="sxs-lookup"><span data-stu-id="31048-149">**Client IP and protocol**: Successive requests from hello same client IP and protocol combination are handled by hello same container.</span></span> |
   | <span data-ttu-id="31048-150">Délai d’inactivité</span><span class="sxs-lookup"><span data-stu-id="31048-150">Idle timeout</span></span> |<span data-ttu-id="31048-151">TCP (uniquement) En quelques minutes, hello tookeep de temps un client TCP/HTTP ouvrir sans se baser sur *KeepAlive* messages.</span><span class="sxs-lookup"><span data-stu-id="31048-151">(TCP only) In minutes, hello time tookeep a TCP/HTTP client open without relying on *keep-alive* messages.</span></span> |

## <a name="add-a-security-rule-portal"></a><span data-ttu-id="31048-152">Ajouter une règle de sécurité (portail)</span><span class="sxs-lookup"><span data-stu-id="31048-152">Add a security rule (portal)</span></span>
<span data-ttu-id="31048-153">Ensuite, nous devons tooadd une règle de sécurité qui achemine le trafic à partir de notre port ouvert via le pare-feu hello.</span><span class="sxs-lookup"><span data-stu-id="31048-153">Next, we need tooadd a security rule that routes traffic from our opened port through hello firewall.</span></span>

1. <span data-ttu-id="31048-154">Ouvrez une session dans toohello portal.</span><span class="sxs-lookup"><span data-stu-id="31048-154">Log in toohello portal.</span></span>
2. <span data-ttu-id="31048-155">Groupe de ressources hello recherche que vous avez déployé Bonjour Azure conteneur de Service.</span><span class="sxs-lookup"><span data-stu-id="31048-155">Find hello resource group that you deployed hello Azure Container Service to.</span></span>
3. <span data-ttu-id="31048-156">Sélectionnez hello **public** groupe de sécurité de l’agent réseau (qui est le même nom trop**XXXX-agent-public-groupe de sécurité réseau-XXXX**).</span><span class="sxs-lookup"><span data-stu-id="31048-156">Select hello **public** agent network security group (which is named similar too**XXXX-agent-public-nsg-XXXX**).</span></span>
   
    ![Groupe de sécurité réseau Azure Container Service](./media/container-service-enable-public-access/agent-nsg.png)
4. <span data-ttu-id="31048-158">Sélectionnez les **règles de sécurité de trafic entrant**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="31048-158">Select **Inbound security rules** and then **Add**.</span></span>
   
    ![Règles du groupe de sécurité réseau Azure Container Service](./media/container-service-enable-public-access/add-firewall-rule.png)
5. <span data-ttu-id="31048-160">Entrez votre port public tooallow de règle de pare-feu hello et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="31048-160">Fill out hello firewall rule tooallow your public port and click **OK**.</span></span>
   
   | <span data-ttu-id="31048-161">Champ</span><span class="sxs-lookup"><span data-stu-id="31048-161">Field</span></span> | <span data-ttu-id="31048-162">Description</span><span class="sxs-lookup"><span data-stu-id="31048-162">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="31048-163">Nom</span><span class="sxs-lookup"><span data-stu-id="31048-163">Name</span></span> |<span data-ttu-id="31048-164">Un nom descriptif hello de règle de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="31048-164">A descriptive name of hello firewall rule.</span></span> |
   | <span data-ttu-id="31048-165">Priorité</span><span class="sxs-lookup"><span data-stu-id="31048-165">Priority</span></span> |<span data-ttu-id="31048-166">Rang de priorité pour la règle de hello.</span><span class="sxs-lookup"><span data-stu-id="31048-166">Priority rank for hello rule.</span></span> <span data-ttu-id="31048-167">Hello inférieur hello numéro hello hello prioritaires.</span><span class="sxs-lookup"><span data-stu-id="31048-167">hello lower hello number hello higher hello priority.</span></span> |
   | <span data-ttu-id="31048-168">Source</span><span class="sxs-lookup"><span data-stu-id="31048-168">Source</span></span> |<span data-ttu-id="31048-169">Restreindre hello entrants IP adresse plage toobe autorisé ou refusé par cette règle.</span><span class="sxs-lookup"><span data-stu-id="31048-169">Restrict hello incoming IP address range toobe allowed or denied by this rule.</span></span> <span data-ttu-id="31048-170">Utilisez **tout** toonot spécifient une restriction.</span><span class="sxs-lookup"><span data-stu-id="31048-170">Use **Any** toonot specify a restriction.</span></span> |
   | <span data-ttu-id="31048-171">Service</span><span class="sxs-lookup"><span data-stu-id="31048-171">Service</span></span> |<span data-ttu-id="31048-172">Sélectionner un ensemble de services prédéfinis concerné par cette règle de sécurité.</span><span class="sxs-lookup"><span data-stu-id="31048-172">Select a set of predefined services this security rule is for.</span></span> <span data-ttu-id="31048-173">Sinon, utilisez **personnalisé** toocreate votre propre.</span><span class="sxs-lookup"><span data-stu-id="31048-173">Otherwise use **Custom** toocreate your own.</span></span> |
   | <span data-ttu-id="31048-174">Protocole</span><span class="sxs-lookup"><span data-stu-id="31048-174">Protocol</span></span> |<span data-ttu-id="31048-175">Restreindre le trafic basé sur **TCP** ou **UDP**.</span><span class="sxs-lookup"><span data-stu-id="31048-175">Restrict traffic based on **TCP** or **UDP**.</span></span> <span data-ttu-id="31048-176">Utilisez **tout** toonot spécifient une restriction.</span><span class="sxs-lookup"><span data-stu-id="31048-176">Use **Any** toonot specify a restriction.</span></span> |
   | <span data-ttu-id="31048-177">Plage de ports</span><span class="sxs-lookup"><span data-stu-id="31048-177">Port range</span></span> |<span data-ttu-id="31048-178">Lorsque **Service** est **personnalisé**, spécifie la plage de hello de ports que cette règle affecte.</span><span class="sxs-lookup"><span data-stu-id="31048-178">When **Service** is **Custom**, specifies hello range of ports that this rule affects.</span></span> <span data-ttu-id="31048-179">Vous pouvez utiliser un port unique, tel que **80** ou une plage comme **1024-1500**.</span><span class="sxs-lookup"><span data-stu-id="31048-179">You can use a single port, such as **80**, or a range like **1024-1500**.</span></span> |
   | <span data-ttu-id="31048-180">Action</span><span class="sxs-lookup"><span data-stu-id="31048-180">Action</span></span> |<span data-ttu-id="31048-181">Autoriser ou refuser le trafic qui répond aux critères de hello.</span><span class="sxs-lookup"><span data-stu-id="31048-181">Allow or deny traffic that meets hello criteria.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="31048-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="31048-182">Next steps</span></span>
<span data-ttu-id="31048-183">En savoir plus sur la différence de hello [agents de contrôleur de domaine/système d’exploitation publiques et privées](container-service-dcos-agents.md).</span><span class="sxs-lookup"><span data-stu-id="31048-183">Learn about hello difference between [public and private DC/OS agents](container-service-dcos-agents.md).</span></span>

<span data-ttu-id="31048-184">En savoir plus sur la [gestion de vos conteneurs DC/OS](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="31048-184">Read more information about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

