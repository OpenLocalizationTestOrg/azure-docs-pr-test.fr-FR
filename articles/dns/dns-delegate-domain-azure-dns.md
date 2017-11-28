---
title: "Délégation de votre domaine à Azure DNS | Microsoft Docs"
description: "Découvrez comment modifier la délégation de domaine et les serveurs de noms Azure DNS pour fournir l’hébergement d’un domaine."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: 33b3ec24432ff1268860b9a2e9d5098600a8dedc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="delegate-a-domain-to-azure-dns"></a><span data-ttu-id="34948-103">Délégation de domaine à Azure DNS</span><span class="sxs-lookup"><span data-stu-id="34948-103">Delegate a domain to Azure DNS</span></span>

<span data-ttu-id="34948-104">Azure DNS vous permet d’héberger une zone DNS et de gérer les enregistrements DNS pour un domaine dans Azure.</span><span class="sxs-lookup"><span data-stu-id="34948-104">Azure DNS allows you to host a DNS zone and manage the DNS records for a domain in Azure.</span></span> <span data-ttu-id="34948-105">Pour que les requêtes DNS d’un domaine atteignent Azure DNS, le domaine doit être délégué à Azure DNS à partir du domaine parent.</span><span class="sxs-lookup"><span data-stu-id="34948-105">In order for DNS queries for a domain to reach Azure DNS, the domain has to be delegated to Azure DNS from the parent domain.</span></span> <span data-ttu-id="34948-106">GardeN’oubliez pas qu’Azure DNS n’est pas le bureau d’enregistrement de domaines.</span><span class="sxs-lookup"><span data-stu-id="34948-106">Keep in mind Azure DNS is not the domain registrar.</span></span> <span data-ttu-id="34948-107">Cet article explique comment déléguer votre domaine à Azure DNS</span><span class="sxs-lookup"><span data-stu-id="34948-107">This article explains how to delegate your domain to Azure DNS.</span></span>

<span data-ttu-id="34948-108">Pour les domaines achetés auprès d’un bureau d’enregistrement de domaines, ce dernier offre la possibilité de définir ces enregistrements NS.</span><span class="sxs-lookup"><span data-stu-id="34948-108">For domains purchased from a registrar, your registrar offers the option to set up these NS records.</span></span> <span data-ttu-id="34948-109">Pour créer une zone DNS avec un nom de domaine dans le DNS Azure, vous ne devez pas nécessairement être propriétaire de ce domaine.</span><span class="sxs-lookup"><span data-stu-id="34948-109">You do not have to own a domain to create a DNS zone with that domain name in Azure DNS.</span></span> <span data-ttu-id="34948-110">Toutefois, vous avez besoin de posséder le domaine pour configurer la délégation à Azure DNS dans le bureau d’enregistrement de domaines.</span><span class="sxs-lookup"><span data-stu-id="34948-110">However, you do need to own the domain to set up the delegation to Azure DNS with the registrar.</span></span>

<span data-ttu-id="34948-111">Par exemple, supposons que vous achetez le domaine « contoso.net » et que vous créez une zone avec le nom « contoso.net » dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="34948-111">For example, suppose you purchase the domain 'contoso.net' and create a zone with the name 'contoso.net' in Azure DNS.</span></span> <span data-ttu-id="34948-112">En tant que propriétaire du domaine, votre bureau d’enregistrement vous permet de configurer les adresses de serveur de noms (par exemple, les enregistrements NS) pour votre domaine.</span><span class="sxs-lookup"><span data-stu-id="34948-112">As the owner of the domain, your registrar offers you the option to configure the name server addresses (that is, the NS records) for your domain.</span></span> <span data-ttu-id="34948-113">Le bureau d’enregistrement stocke ces enregistrements NS dans le domaine parent, dans ce cas « .net ».</span><span class="sxs-lookup"><span data-stu-id="34948-113">The registrar stores these NS records in the parent domain, in this case '.net'.</span></span> <span data-ttu-id="34948-114">Les clients du monde entier peuvent ensuite être redirigés vers votre domaine dans la zone Azure DNS lors de la tentative de résolution des enregistrements DNS dans « contoso.net ».</span><span class="sxs-lookup"><span data-stu-id="34948-114">Clients around the world can then be directed to your domain in Azure DNS zone when trying to resolve DNS records in 'contoso.net'.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="34948-115">Création d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="34948-115">Create a DNS zone</span></span>

1. <span data-ttu-id="34948-116">Connectez-vous au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="34948-116">Sign in to the Azure portal</span></span>
1. <span data-ttu-id="34948-117">Dans le menu Hub, cliquez sur **Nouveau > Mise en réseau >**, puis cliquez sur **Zone DNS** pour ouvrir le panneau Créer une zone DNS.</span><span class="sxs-lookup"><span data-stu-id="34948-117">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![Zone DNS](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="34948-119">Dans le panneau **Créer une zone DNS**, entrez les valeurs suivantes, puis cliquez sur **Créer** :</span><span class="sxs-lookup"><span data-stu-id="34948-119">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>

   | <span data-ttu-id="34948-120">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="34948-120">**Setting**</span></span> | <span data-ttu-id="34948-121">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="34948-121">**Value**</span></span> | <span data-ttu-id="34948-122">**Détails**</span><span class="sxs-lookup"><span data-stu-id="34948-122">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="34948-123">**Name**</span><span class="sxs-lookup"><span data-stu-id="34948-123">**Name**</span></span>|<span data-ttu-id="34948-124">contoso.net</span><span class="sxs-lookup"><span data-stu-id="34948-124">contoso.net</span></span>|<span data-ttu-id="34948-125">Nom de la zone DNS</span><span class="sxs-lookup"><span data-stu-id="34948-125">The name of the DNS zone</span></span>|
   |<span data-ttu-id="34948-126">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="34948-126">**Subscription**</span></span>|<span data-ttu-id="34948-127">[Votre abonnement]</span><span class="sxs-lookup"><span data-stu-id="34948-127">[Your subscription]</span></span>|<span data-ttu-id="34948-128">Sélectionnez l’abonnement dans lequel créer la passerelle de l’application.</span><span class="sxs-lookup"><span data-stu-id="34948-128">Select a subscription to create the application gateway in.</span></span>|
   |<span data-ttu-id="34948-129">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="34948-129">**Resource group**</span></span>|<span data-ttu-id="34948-130">**Créer :** contosoRG</span><span class="sxs-lookup"><span data-stu-id="34948-130">**Create new:** contosoRG</span></span>|<span data-ttu-id="34948-131">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="34948-131">Create a resource group.</span></span> <span data-ttu-id="34948-132">Le nom du groupe de ressources doit être unique au sein de l’abonnement sélectionné.</span><span class="sxs-lookup"><span data-stu-id="34948-132">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="34948-133">Pour plus d’informations sur les groupes de ressources, consultez l’article [Présentation de Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="34948-133">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="34948-134">**Emplacement**</span><span class="sxs-lookup"><span data-stu-id="34948-134">**Location**</span></span>|<span data-ttu-id="34948-135">Ouest des États-Unis</span><span class="sxs-lookup"><span data-stu-id="34948-135">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="34948-136">Le groupe de ressources fait référence à l’emplacement du groupe de ressources et n’a aucun impact sur la zone DNS.</span><span class="sxs-lookup"><span data-stu-id="34948-136">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="34948-137">L’emplacement de la zone DNS est toujours « global » et n’est pas affiché.</span><span class="sxs-lookup"><span data-stu-id="34948-137">The DNS zone location is always "global", and is not shown.</span></span>

## <a name="retrieve-name-servers"></a><span data-ttu-id="34948-138">Récupérer les serveurs de noms</span><span class="sxs-lookup"><span data-stu-id="34948-138">Retrieve name servers</span></span>

<span data-ttu-id="34948-139">Avant de pouvoir déléguer votre zone DNS à Azure DNS, vous devez d’abord connaître les noms de serveur de noms correspondant à votre zone.</span><span class="sxs-lookup"><span data-stu-id="34948-139">Before you can delegate your DNS zone to Azure DNS, you first need to know the name server names for your zone.</span></span> <span data-ttu-id="34948-140">Azure DNS alloue des serveurs de noms à partir d’un pool chaque fois qu’une zone est créée.</span><span class="sxs-lookup"><span data-stu-id="34948-140">Azure DNS allocates name servers from a pool each time a zone is created.</span></span>

1. <span data-ttu-id="34948-141">Une fois la zone DNS créée, allez dans le panneau **Favoris** du portail Azure, puis cliquez sur **Toutes les ressources**.</span><span class="sxs-lookup"><span data-stu-id="34948-141">With the DNS zone created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="34948-142">Cliquez sur la zone DNS **contoso.net** dans le panneau **Toutes les ressources**.</span><span class="sxs-lookup"><span data-stu-id="34948-142">Click the **contoso.net** DNS zone in the **All resources** blade.</span></span> <span data-ttu-id="34948-143">Si l’abonnement que vous avez déjà sélectionné comporte plusieurs ressources, vous pouvez saisir **contoso.net** dans la case Filtrer par nom…</span><span class="sxs-lookup"><span data-stu-id="34948-143">If the subscription you selected already has several resources in it, you can enter **contoso.net** in the Filter by name…</span></span> <span data-ttu-id="34948-144">pour accéder facilement à la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="34948-144">box to easily access the application gateway.</span></span> 

1. <span data-ttu-id="34948-145">Récupérez les serveurs de noms à partir du panneau de zone DNS.</span><span class="sxs-lookup"><span data-stu-id="34948-145">Retrieve the name servers from the DNS zone blade.</span></span> <span data-ttu-id="34948-146">Dans cet exemple, la zone « contoso.net » a été attribuée aux serveurs de noms « ns1-01.azure-dns.com », « ns2-01.azure-dns.net », « ns3-01.azure-dns.org » et « ns4-01.azure-dns.info » :</span><span class="sxs-lookup"><span data-stu-id="34948-146">In this example, the zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="34948-148">Azure DNS crée automatiquement des enregistrements NS faisant autorité dans une zone qui contient les serveurs de noms attribués.</span><span class="sxs-lookup"><span data-stu-id="34948-148">Azure DNS automatically creates authoritative NS records in your zone containing the assigned name servers.</span></span>  <span data-ttu-id="34948-149">Pour afficher les noms de serveur de noms via Azure PowerShell ou l’interface de ligne de commande Azure, vous devez simplement récupérer ces enregistrements.</span><span class="sxs-lookup"><span data-stu-id="34948-149">To see the name server names via Azure PowerShell or Azure CLI, you simply need to retrieve these records.</span></span>

<span data-ttu-id="34948-150">Les exemples suivants présentent également les étapes permettant de récupérer les serveurs de noms d’une zone Azure DNS avec PowerShell et Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="34948-150">The following examples also provide the steps to retrieve the name servers for a zone in Azure DNS with PowerShell and Azure CLI.</span></span>

### <a name="powershell"></a><span data-ttu-id="34948-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="34948-151">PowerShell</span></span>

```powershell
# The record name "@" is used to refer to records at the top of the zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

<span data-ttu-id="34948-152">L’exemple suivant est la réponse.</span><span class="sxs-lookup"><span data-stu-id="34948-152">The following example is the response.</span></span>

```
Name              : @
ZoneName          : contoso.net
ResourceGroupName : contosorg
Ttl               : 172800
Etag              : 03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5
RecordType        : NS
Records           : {ns1-07.azure-dns.com., ns2-07.azure-dns.net., ns3-07.azure-dns.org.,
                    ns4-07.azure-dns.info.}
Metadata          :
```

### <a name="azure-cli"></a><span data-ttu-id="34948-153">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="34948-153">Azure CLI</span></span>

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

<span data-ttu-id="34948-154">L’exemple suivant est la réponse.</span><span class="sxs-lookup"><span data-stu-id="34948-154">The following example is the response.</span></span>

```json
{
  "etag": "03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosoRG/providers/Microsoft.Network/dnszones/contoso.net/NS/@",
  "metadata": null,
  "name": "@",
  "nsRecords": [
    {
      "nsdname": "ns1-07.azure-dns.com."
    },
    {
      "nsdname": "ns2-07.azure-dns.net."
    },
    {
      "nsdname": "ns3-07.azure-dns.org."
    },
    {
      "nsdname": "ns4-07.azure-dns.info."
    }
  ],
  "resourceGroup": "contosoRG",
  "ttl": 172800,
  "type": "Microsoft.Network/dnszones/NS"
}
```

## <a name="delegate-the-domain"></a><span data-ttu-id="34948-155">Déléguer le domaine</span><span class="sxs-lookup"><span data-stu-id="34948-155">Delegate the domain</span></span>

<span data-ttu-id="34948-156">Maintenant que la zone DNS est créée et que vous disposez des serveurs de noms, le domaine parent doit être mis à jour avec les serveurs de noms Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="34948-156">Now that the DNS zone is created and you have the name servers, the parent domain needs to be updated with the Azure DNS name servers.</span></span> <span data-ttu-id="34948-157">Chaque bureau d’enregistrement a ses propres outils de gestion DNS pour modifier les enregistrements de serveur de noms pour un domaine.</span><span class="sxs-lookup"><span data-stu-id="34948-157">Each registrar has their own DNS management tools to change the name server records for a domain.</span></span> <span data-ttu-id="34948-158">Dans la page de gestion du bureau d’enregistrement DNS, modifiez les enregistrements NS et remplacez-les par ceux créés par Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="34948-158">In the registrar's DNS management page, edit the NS records and replace the NS records with the ones Azure DNS created.</span></span>

<span data-ttu-id="34948-159">Lors de la délégation d’un domaine à Azure DNS, vous devez utiliser les noms de serveur de noms fournis par Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="34948-159">When delegating a domain to Azure DNS, you must use the name server names provided by Azure DNS.</span></span> <span data-ttu-id="34948-160">Nous vous recommandons d’utiliser les quatre noms de serveur de noms, quel que soit le nom de votre domaine.</span><span class="sxs-lookup"><span data-stu-id="34948-160">It is recommended to use all four name server names, regardless of the name of your domain.</span></span> <span data-ttu-id="34948-161">La délégation de domaine ne requiert pas que le nom du serveur de noms utilise le même domaine de premier niveau que votre domaine.</span><span class="sxs-lookup"><span data-stu-id="34948-161">Domain delegation does not require the name server name to use the same top-level domain as your domain.</span></span>

<span data-ttu-id="34948-162">Vous ne devez pas utiliser d’enregistrements de type glue pour pointer vers les adresses IP de serveur de noms Azure DNS, car ces adresses IP peuvent changer ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="34948-162">You should not use 'glue records' to point to the Azure DNS name server IP addresses, since these IP addresses may change in future.</span></span> <span data-ttu-id="34948-163">Les délégations utilisant les noms de serveurs de noms dans votre propre zone (parfois appelés « serveurs de noms de redirection vers un microsite ») ne sont actuellement pas prises en charge dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="34948-163">Delegations using name server names in your own zone, sometimes called 'vanity name servers', are not currently supported in Azure DNS.</span></span>

## <a name="verify-name-resolution-is-working"></a><span data-ttu-id="34948-164">Vérifier le fonctionnement de la résolution de noms</span><span class="sxs-lookup"><span data-stu-id="34948-164">Verify name resolution is working</span></span>

<span data-ttu-id="34948-165">Une fois la délégation effectuée, vous pouvez vérifier que la résolution de noms fonctionne à l’aide d’un outil tel que « nslookup » pour interroger l’enregistrement SOA de votre zone (qui est créé automatiquement en même temps que la zone).</span><span class="sxs-lookup"><span data-stu-id="34948-165">After completing the delegation, you can verify that name resolution is working by using a tool such as 'nslookup' to query the SOA record for your zone (which is also automatically created when the zone is created).</span></span>

<span data-ttu-id="34948-166">Vous n’êtes pas obligé de spécifier les serveurs de noms Azure DNS ; si la délégation a été correctement configurée, le processus de résolution DNS normal trouve les serveurs de noms automatiquement.</span><span class="sxs-lookup"><span data-stu-id="34948-166">You do not have to specify the Azure DNS name servers, if the delegation has been set up correctly, the normal DNS resolution process finds the name servers automatically.</span></span>

```
nslookup -type=SOA contoso.com
```

<span data-ttu-id="34948-167">Voici un exemple de réponse à partir de la commande précédente :</span><span class="sxs-lookup"><span data-stu-id="34948-167">The following is an example response from the preceding command:</span></span>

```
Server: ns1-04.azure-dns.com
Address: 208.76.47.4

contoso.com
primary name server = ns1-04.azure-dns.com
responsible mail addr = msnhst.microsoft.com
serial = 1
refresh = 900 (15 mins)
retry = 300 (5 mins)
expire = 604800 (7 days)
default TTL = 300 (5 mins)
```

## <a name="delegate-sub-domains-in-azure-dns"></a><span data-ttu-id="34948-168">Déléguer les sous-domaines dans Azure DNS</span><span class="sxs-lookup"><span data-stu-id="34948-168">Delegate sub-domains in Azure DNS</span></span>

<span data-ttu-id="34948-169">Si vous souhaitez configurer une zone enfant distincte, vous pouvez déléguer un sous-domaine dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="34948-169">If you want to set up a separate child zone, you can delegate a sub-domain in Azure DNS.</span></span> <span data-ttu-id="34948-170">Par exemple, vous avez configuré et délégué « contoso.net » dans Azure DNS. Supposons que vous voulez configurer une zone enfant distincte, « partners.contoso.net ».</span><span class="sxs-lookup"><span data-stu-id="34948-170">For example, having set up and delegated 'contoso.net' in Azure DNS, suppose you would like to set up a separate child zone, 'partners.contoso.net'.</span></span>

1. <span data-ttu-id="34948-171">Créez la zone enfant « partners.contoso.net » dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="34948-171">Create the child zone 'partners.contoso.net' in Azure DNS.</span></span>
2. <span data-ttu-id="34948-172">Recherchez les enregistrements NS faisant autorité dans la zone enfant pour obtenir les serveurs de noms qui hébergent la zone enfant dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="34948-172">Look up the authoritative NS records in the child zone to obtain the name servers hosting the child zone in Azure DNS.</span></span>
3. <span data-ttu-id="34948-173">Déléguez la zone enfant en configurant les enregistrements NS de la zone parent pour qu'ils pointent vers la zone enfant.</span><span class="sxs-lookup"><span data-stu-id="34948-173">Delegate the child zone by configuring NS records in the parent zone pointing to the child zone.</span></span>

### <a name="create-a-dns-zone"></a><span data-ttu-id="34948-174">Création d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="34948-174">Create a DNS zone</span></span>

1. <span data-ttu-id="34948-175">Connectez-vous au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="34948-175">Sign in to the Azure portal</span></span>
1. <span data-ttu-id="34948-176">Dans le menu Hub, cliquez sur **Nouveau > Mise en réseau >**, puis cliquez sur **Zone DNS** pour ouvrir le panneau Créer une zone DNS.</span><span class="sxs-lookup"><span data-stu-id="34948-176">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![Zone DNS](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="34948-178">Dans le panneau **Créer une zone DNS**, entrez les valeurs suivantes, puis cliquez sur **Créer** :</span><span class="sxs-lookup"><span data-stu-id="34948-178">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>

   | <span data-ttu-id="34948-179">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="34948-179">**Setting**</span></span> | <span data-ttu-id="34948-180">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="34948-180">**Value**</span></span> | <span data-ttu-id="34948-181">**Détails**</span><span class="sxs-lookup"><span data-stu-id="34948-181">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="34948-182">**Name**</span><span class="sxs-lookup"><span data-stu-id="34948-182">**Name**</span></span>|<span data-ttu-id="34948-183">partners.contoso.net</span><span class="sxs-lookup"><span data-stu-id="34948-183">partners.contoso.net</span></span>|<span data-ttu-id="34948-184">Nom de la zone DNS</span><span class="sxs-lookup"><span data-stu-id="34948-184">The name of the DNS zone</span></span>|
   |<span data-ttu-id="34948-185">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="34948-185">**Subscription**</span></span>|<span data-ttu-id="34948-186">[Votre abonnement]</span><span class="sxs-lookup"><span data-stu-id="34948-186">[Your subscription]</span></span>|<span data-ttu-id="34948-187">Sélectionnez l’abonnement dans lequel créer la passerelle de l’application.</span><span class="sxs-lookup"><span data-stu-id="34948-187">Select a subscription to create the application gateway in.</span></span>|
   |<span data-ttu-id="34948-188">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="34948-188">**Resource group**</span></span>|<span data-ttu-id="34948-189">**Use Existing :** (Utiliser existant) contosoRG</span><span class="sxs-lookup"><span data-stu-id="34948-189">**Use Existing:** contosoRG</span></span>|<span data-ttu-id="34948-190">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="34948-190">Create a resource group.</span></span> <span data-ttu-id="34948-191">Le nom du groupe de ressources doit être unique au sein de l’abonnement sélectionné.</span><span class="sxs-lookup"><span data-stu-id="34948-191">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="34948-192">Pour plus d’informations sur les groupes de ressources, consultez l’article [Présentation de Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="34948-192">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="34948-193">**Emplacement**</span><span class="sxs-lookup"><span data-stu-id="34948-193">**Location**</span></span>|<span data-ttu-id="34948-194">Ouest des États-Unis</span><span class="sxs-lookup"><span data-stu-id="34948-194">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="34948-195">Le groupe de ressources fait référence à l’emplacement du groupe de ressources et n’a aucun impact sur la zone DNS.</span><span class="sxs-lookup"><span data-stu-id="34948-195">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="34948-196">L’emplacement de la zone DNS est toujours « global » et n’est pas affiché.</span><span class="sxs-lookup"><span data-stu-id="34948-196">The DNS zone location is always "global", and is not shown.</span></span>

### <a name="retrieve-name-servers"></a><span data-ttu-id="34948-197">Récupérer les serveurs de noms</span><span class="sxs-lookup"><span data-stu-id="34948-197">Retrieve name servers</span></span>

1. <span data-ttu-id="34948-198">Une fois la zone DNS créée, allez dans le panneau **Favoris** du portail Azure, puis cliquez sur **Toutes les ressources**.</span><span class="sxs-lookup"><span data-stu-id="34948-198">With the DNS zone created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="34948-199">Cliquez sur la zone DNS **partners.contoso.net** dans le panneau **Toutes les ressources**.</span><span class="sxs-lookup"><span data-stu-id="34948-199">Click the **partners.contoso.net** DNS zone in the **All resources** blade.</span></span> <span data-ttu-id="34948-200">Si l’abonnement que vous avez déjà sélectionné comporte plusieurs ressources, vous pouvez saisir **partners.contoso.net** dans la case Filtrer par nom…</span><span class="sxs-lookup"><span data-stu-id="34948-200">If the subscription you selected already has several resources in it, you can enter **partners.contoso.net** in the Filter by name…</span></span> <span data-ttu-id="34948-201">pour accéder facilement à la zone DNS.</span><span class="sxs-lookup"><span data-stu-id="34948-201">box to easily access the DNS zone.</span></span>

1. <span data-ttu-id="34948-202">Récupérez les serveurs de noms à partir du panneau de zone DNS.</span><span class="sxs-lookup"><span data-stu-id="34948-202">Retrieve the name servers from the DNS zone blade.</span></span> <span data-ttu-id="34948-203">Dans cet exemple, la zone « contoso.net » a été attribuée aux serveurs de noms « ns1-01.azure-dns.com », « ns2-01.azure-dns.net », « ns3-01.azure-dns.org » et « ns4-01.azure-dns.info » :</span><span class="sxs-lookup"><span data-stu-id="34948-203">In this example, the zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="34948-205">Azure DNS crée automatiquement des enregistrements NS faisant autorité dans une zone qui contient les serveurs de noms attribués.</span><span class="sxs-lookup"><span data-stu-id="34948-205">Azure DNS automatically creates authoritative NS records in your zone containing the assigned name servers.</span></span>  <span data-ttu-id="34948-206">Pour afficher les noms de serveur de noms via Azure PowerShell ou l’interface de ligne de commande Azure, vous devez simplement récupérer ces enregistrements.</span><span class="sxs-lookup"><span data-stu-id="34948-206">To see the name server names via Azure PowerShell or Azure CLI, you simply need to retrieve these records.</span></span>

### <a name="create-name-server-record-in-parent-zone"></a><span data-ttu-id="34948-207">Créer un enregistrement de serveur de noms dans la zone parente</span><span class="sxs-lookup"><span data-stu-id="34948-207">Create name server record in parent zone</span></span>

1. <span data-ttu-id="34948-208">Accédez à la zone DNS **contoso.net** dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="34948-208">Navigate to the **contoso.net** DNS zone in the Azure portal.</span></span>
1. <span data-ttu-id="34948-209">Cliquez sur **+ Jeu d’enregistrements**.</span><span class="sxs-lookup"><span data-stu-id="34948-209">Click **+ Record set**</span></span>
1. <span data-ttu-id="34948-210">Dans le panneau **Ajouter un jeu d’enregistrements**, entrez les valeurs suivantes, puis cliquez sur **OK** :</span><span class="sxs-lookup"><span data-stu-id="34948-210">On the **Add record set** blade, enter the following values, then click **OK**:</span></span>

   | <span data-ttu-id="34948-211">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="34948-211">**Setting**</span></span> | <span data-ttu-id="34948-212">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="34948-212">**Value**</span></span> | <span data-ttu-id="34948-213">**Détails**</span><span class="sxs-lookup"><span data-stu-id="34948-213">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="34948-214">**Name**</span><span class="sxs-lookup"><span data-stu-id="34948-214">**Name**</span></span>|<span data-ttu-id="34948-215">partenaires</span><span class="sxs-lookup"><span data-stu-id="34948-215">partners</span></span>|<span data-ttu-id="34948-216">Nom de la zone DNS enfant</span><span class="sxs-lookup"><span data-stu-id="34948-216">The name of the child DNS zone</span></span>|
   |<span data-ttu-id="34948-217">**Type**</span><span class="sxs-lookup"><span data-stu-id="34948-217">**Type**</span></span>|<span data-ttu-id="34948-218">NS</span><span class="sxs-lookup"><span data-stu-id="34948-218">NS</span></span>|<span data-ttu-id="34948-219">Utilisez NS pour les enregistrements de serveur de noms.</span><span class="sxs-lookup"><span data-stu-id="34948-219">Use NS for name server records.</span></span>|
   |<span data-ttu-id="34948-220">**TTL**</span><span class="sxs-lookup"><span data-stu-id="34948-220">**TTL**</span></span>|<span data-ttu-id="34948-221">1</span><span class="sxs-lookup"><span data-stu-id="34948-221">1</span></span>|<span data-ttu-id="34948-222">Durée de vie.</span><span class="sxs-lookup"><span data-stu-id="34948-222">Time to live.</span></span>|
   |<span data-ttu-id="34948-223">**Unité de durée de vie**</span><span class="sxs-lookup"><span data-stu-id="34948-223">**TTL unit**</span></span>|<span data-ttu-id="34948-224">Heures</span><span class="sxs-lookup"><span data-stu-id="34948-224">Hours</span></span>|<span data-ttu-id="34948-225">définit l’heure pour un affichage en direct (heures)</span><span class="sxs-lookup"><span data-stu-id="34948-225">sets time to live unit to hours</span></span>|
   |<span data-ttu-id="34948-226">**SERVEUR DE NOMS**</span><span class="sxs-lookup"><span data-stu-id="34948-226">**NAME SERVER**</span></span>|<span data-ttu-id="34948-227">{serveurs de noms à partir de la zone partners.contoso.net}</span><span class="sxs-lookup"><span data-stu-id="34948-227">{name servers from partners.contoso.net zone}</span></span>|<span data-ttu-id="34948-228">Entrez les 4 serveurs de noms à partir de la zone de partners.contoso.net.</span><span class="sxs-lookup"><span data-stu-id="34948-228">Enter all 4 of the name servers from partners.contoso.net zone.</span></span> |

   ![Dns-nameserver](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a><span data-ttu-id="34948-230">Déléguer des sous-domaines dans Azure DNS avec d’autres outils</span><span class="sxs-lookup"><span data-stu-id="34948-230">Delegating sub-domains in Azure DNS with other tools</span></span>

<span data-ttu-id="34948-231">Les exemples suivants présentent les étapes permettant de déléguer des sous-domaines dans Azure DNS avec PowerShell et CLI :</span><span class="sxs-lookup"><span data-stu-id="34948-231">The following examples provide the steps to delegate sub-domains in Azure DNS with PowerShell and CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="34948-232">PowerShell</span><span class="sxs-lookup"><span data-stu-id="34948-232">PowerShell</span></span>

<span data-ttu-id="34948-233">L’exemple PowerShell suivant illustre cette procédure.</span><span class="sxs-lookup"><span data-stu-id="34948-233">The following PowerShell example demonstrates how this works.</span></span> <span data-ttu-id="34948-234">Vous pouvez exécuter les mêmes étapes à l’aide du portail Azure ou de la version interplateforme d’Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="34948-234">The same steps can be executed via the Azure portal, or via the cross-platform Azure CLI.</span></span>

```powershell
# Create the parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve the authoritative NS records from the child zone as shown in the next example. This contains the name servers assigned to the child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create the corresponding NS record set in the parent zone to complete the delegation. The record set name in the parent zone matches the child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

<span data-ttu-id="34948-235">Utilisez `nslookup` pour vérifier que tout est correctement configuré en recherchant l’enregistrement SOA de la zone enfant.</span><span class="sxs-lookup"><span data-stu-id="34948-235">Use `nslookup` to verify that everything is set up correctly by looking up the SOA record of the child zone.</span></span>

```
nslookup -type=SOA partners.contoso.com
```

```
Server: ns1-08.azure-dns.com
Address: 208.76.47.8

partners.contoso.com
    primary name server = ns1-08.azure-dns.com
    responsible mail addr = msnhst.microsoft.com
    serial = 1
    refresh = 900 (15 mins)
    retry = 300 (5 mins)
    expire = 604800 (7 days)
    default TTL = 300 (5 mins)
```

#### <a name="azure-cli"></a><span data-ttu-id="34948-236">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="34948-236">Azure CLI</span></span>

```azurecli
#!/bin/bash

# Create the parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

<span data-ttu-id="34948-237">Récupérez les serveurs de noms de la zone `partners.contoso.net` à partir de la sortie.</span><span class="sxs-lookup"><span data-stu-id="34948-237">Retrieve the name servers for the `partners.contoso.net` zone from the output.</span></span>

```
{
  "etag": "00000003-0000-0000-418f-250de2b2d201",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosorg/providers/Microsoft.Network/dnszones/partners.contoso.net",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "partners.contoso.net",
  "nameServers": [
    "ns1-09.azure-dns.com.",
    "ns2-09.azure-dns.net.",
    "ns3-09.azure-dns.org.",
    "ns4-09.azure-dns.info."
  ],
  "numberOfRecordSets": 2,
  "resourceGroup": "contosorg",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="34948-238">Créez le jeu d’enregistrements et les enregistrements NS pour chaque serveur de noms.</span><span class="sxs-lookup"><span data-stu-id="34948-238">Create the record set and NS records for each name server.</span></span>

```azurecli
#!/bin/bash

# Create the record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a><span data-ttu-id="34948-239">Supprimer toutes les ressources</span><span class="sxs-lookup"><span data-stu-id="34948-239">Delete all resources</span></span>

<span data-ttu-id="34948-240">Pour supprimer toutes les ressources créées dans cet article, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="34948-240">To delete all resources created in this article, complete the following steps:</span></span>

1. <span data-ttu-id="34948-241">Allez dans le panneau **Favoris** du portail Azure, puis cliquez sur **Toutes les ressources**.</span><span class="sxs-lookup"><span data-stu-id="34948-241">In the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="34948-242">Cliquez sur le groupe de ressources **contosorg** dans le panneau Toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="34948-242">Click the **contosorg** resource group in the All resources blade.</span></span> <span data-ttu-id="34948-243">Si l’abonnement que vous avez déjà sélectionné comporte plusieurs ressources, vous pouvez saisir **contosorg** dans la case **Filtrer par nom...**</span><span class="sxs-lookup"><span data-stu-id="34948-243">If the subscription you selected already has several resources in it, you can enter **contosorg** in the **Filter by name…**</span></span> <span data-ttu-id="34948-244">pour accéder facilement au groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="34948-244">box to easily access the resource group.</span></span>
1. <span data-ttu-id="34948-245">Dans le panneau **contosorg**, cliquez sur le bouton **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="34948-245">In the **contosorg** blade, click the **Delete** button.</span></span>
1. <span data-ttu-id="34948-246">Le portail nécessite que vous saisissiez le nom du groupe de ressources pour confirmer la suppression.</span><span class="sxs-lookup"><span data-stu-id="34948-246">The portal requires you to type the name of the resource group to confirm that you want to delete it.</span></span> <span data-ttu-id="34948-247">Tapez *contosorg* comme nom du groupe de ressources, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="34948-247">Type *contosorg* for the resource group name, then click **Delete**.</span></span> <span data-ttu-id="34948-248">La suppression d’un groupe de ressources supprime toutes les ressources qu’il contient. Veuillez donc toujours vérifier le contenu d’un groupe de ressources avant de le supprimer.</span><span class="sxs-lookup"><span data-stu-id="34948-248">Deleting a resource group deletes all resources within the resource group, so always be sure to confirm the contents of a resource group before deleting it.</span></span> <span data-ttu-id="34948-249">Le portail supprime toutes les ressources contenues dans le groupe de ressources, puis supprime le groupe de ressources lui-même.</span><span class="sxs-lookup"><span data-stu-id="34948-249">The portal deletes all resources contained within the resource group, then deletes the resource group itself.</span></span> <span data-ttu-id="34948-250">Cette opération prend plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="34948-250">This process takes several minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34948-251">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="34948-251">Next steps</span></span>

[<span data-ttu-id="34948-252">Gestion des zones DNS</span><span class="sxs-lookup"><span data-stu-id="34948-252">Manage DNS zones</span></span>](dns-operations-dnszones.md)

[<span data-ttu-id="34948-253">Gestion des enregistrements DNS</span><span class="sxs-lookup"><span data-stu-id="34948-253">Manage DNS records</span></span>](dns-operations-recordsets.md)
