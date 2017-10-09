---
title: aaaDelegate votre tooAzure de domaine DNS | Documents Microsoft
description: "Comprendre comment délégation de domaine toochange et Azure DNS d’utiliser le nom de serveurs tooprovide domaine héberge."
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
ms.openlocfilehash: f780bdaa416150e5e3afe6c6845dc75ba54b6203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-a-domain-tooazure-dns"></a><span data-ttu-id="173a6-103">Déléguer un tooAzure de domaine DNS</span><span class="sxs-lookup"><span data-stu-id="173a6-103">Delegate a domain tooAzure DNS</span></span>

<span data-ttu-id="173a6-104">DNS Azure vous permet de toohost une zone DNS et gérer les enregistrements DNS de hello pour un domaine dans Azure.</span><span class="sxs-lookup"><span data-stu-id="173a6-104">Azure DNS allows you toohost a DNS zone and manage hello DNS records for a domain in Azure.</span></span> <span data-ttu-id="173a6-105">Dans l’ordre pour les requêtes DNS pour un tooreach de domaine DNS d’Azure, domaine de hello a toobe déléguée tooAzure DNS dans le domaine parent hello.</span><span class="sxs-lookup"><span data-stu-id="173a6-105">In order for DNS queries for a domain tooreach Azure DNS, hello domain has toobe delegated tooAzure DNS from hello parent domain.</span></span> <span data-ttu-id="173a6-106">N’oubliez pas d’Azure DNS n’est pas de domaines hello.</span><span class="sxs-lookup"><span data-stu-id="173a6-106">Keep in mind Azure DNS is not hello domain registrar.</span></span> <span data-ttu-id="173a6-107">Cet article explique comment toodelegate votre tooAzure de domaine DNS.</span><span class="sxs-lookup"><span data-stu-id="173a6-107">This article explains how toodelegate your domain tooAzure DNS.</span></span>

<span data-ttu-id="173a6-108">Pour les domaines achetés à partir d’un bureau d’enregistrement, votre bureau d’enregistrement offre tooset d’option hello ces enregistrements NS.</span><span class="sxs-lookup"><span data-stu-id="173a6-108">For domains purchased from a registrar, your registrar offers hello option tooset up these NS records.</span></span> <span data-ttu-id="173a6-109">Il est inutile tooown un toocreate domaine une zone DNS avec ce nom de domaine dans le système DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="173a6-109">You do not have tooown a domain toocreate a DNS zone with that domain name in Azure DNS.</span></span> <span data-ttu-id="173a6-110">Toutefois, vous n’avez pas besoin de tooown hello domaine tooset des hello tooAzure de délégation DNS avec le bureau d’enregistrement hello.</span><span class="sxs-lookup"><span data-stu-id="173a6-110">However, you do need tooown hello domain tooset up hello delegation tooAzure DNS with hello registrar.</span></span>

<span data-ttu-id="173a6-111">Par exemple, supposons que vous achetez le domaine hello 'contoso.net' et créez une zone avec le nom hello 'contoso.net' dans le système DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="173a6-111">For example, suppose you purchase hello domain 'contoso.net' and create a zone with hello name 'contoso.net' in Azure DNS.</span></span> <span data-ttu-id="173a6-112">En tant que propriétaire hello du domaine de hello, votre bureau d’enregistrement offre que Hello d’adresses de serveur de noms option tooconfigure hello (autrement dit, les enregistrements hello NS) pour votre domaine.</span><span class="sxs-lookup"><span data-stu-id="173a6-112">As hello owner of hello domain, your registrar offers you hello option tooconfigure hello name server addresses (that is, hello NS records) for your domain.</span></span> <span data-ttu-id="173a6-113">bureau d’enregistrement Hello stocke ces enregistrements NS dans le domaine parent hello, dans ce cas, « .net ».</span><span class="sxs-lookup"><span data-stu-id="173a6-113">hello registrar stores these NS records in hello parent domain, in this case '.net'.</span></span> <span data-ttu-id="173a6-114">Les clients monde hello peuvent ensuite être domaine tooyour suggérés dans la zone DNS de Azure lors de la tentative d’enregistrements DNS tooresolve 'contoso.net'.</span><span class="sxs-lookup"><span data-stu-id="173a6-114">Clients around hello world can then be directed tooyour domain in Azure DNS zone when trying tooresolve DNS records in 'contoso.net'.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="173a6-115">Création d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="173a6-115">Create a DNS zone</span></span>

1. <span data-ttu-id="173a6-116">Se connecter toohello portail Azure</span><span class="sxs-lookup"><span data-stu-id="173a6-116">Sign in toohello Azure portal</span></span>
1. <span data-ttu-id="173a6-117">Dans le menu du Hub hello, cliquez sur, puis cliquez sur **Nouveau > mise en réseau >** puis cliquez sur **zone DNS** Panneau de zone DNS de créer tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="173a6-117">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![Zone DNS](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="173a6-119">Sur hello **zone DNS de créer** panneau hello valeurs suivantes, puis entrez **créer**:</span><span class="sxs-lookup"><span data-stu-id="173a6-119">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>

   | <span data-ttu-id="173a6-120">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="173a6-120">**Setting**</span></span> | <span data-ttu-id="173a6-121">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="173a6-121">**Value**</span></span> | <span data-ttu-id="173a6-122">**Détails**</span><span class="sxs-lookup"><span data-stu-id="173a6-122">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="173a6-123">**Name**</span><span class="sxs-lookup"><span data-stu-id="173a6-123">**Name**</span></span>|<span data-ttu-id="173a6-124">contoso.net</span><span class="sxs-lookup"><span data-stu-id="173a6-124">contoso.net</span></span>|<span data-ttu-id="173a6-125">nom Hello de zone DNS de hello</span><span class="sxs-lookup"><span data-stu-id="173a6-125">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="173a6-126">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="173a6-126">**Subscription**</span></span>|<span data-ttu-id="173a6-127">[Votre abonnement]</span><span class="sxs-lookup"><span data-stu-id="173a6-127">[Your subscription]</span></span>|<span data-ttu-id="173a6-128">Sélectionnez une passerelle d’application abonnement toocreate hello dans.</span><span class="sxs-lookup"><span data-stu-id="173a6-128">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="173a6-129">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="173a6-129">**Resource group**</span></span>|<span data-ttu-id="173a6-130">**Créer :** contosoRG</span><span class="sxs-lookup"><span data-stu-id="173a6-130">**Create new:** contosoRG</span></span>|<span data-ttu-id="173a6-131">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="173a6-131">Create a resource group.</span></span> <span data-ttu-id="173a6-132">nom de groupe de ressources Hello doit être unique au sein de l’abonnement hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="173a6-132">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="173a6-133">toolearn plus d’informations sur les groupes de ressources, lire hello [le Gestionnaire de ressources](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) l’article de vue d’ensemble.</span><span class="sxs-lookup"><span data-stu-id="173a6-133">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="173a6-134">**Emplacement**</span><span class="sxs-lookup"><span data-stu-id="173a6-134">**Location**</span></span>|<span data-ttu-id="173a6-135">Ouest des États-Unis</span><span class="sxs-lookup"><span data-stu-id="173a6-135">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="173a6-136">groupe de ressources Hello fait référence emplacement toohello hello du groupe de ressources et n’a aucun impact sur la zone DNS de hello.</span><span class="sxs-lookup"><span data-stu-id="173a6-136">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="173a6-137">emplacement des zones DNS Hello est toujours « globaux » et n’est pas affiché.</span><span class="sxs-lookup"><span data-stu-id="173a6-137">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="retrieve-name-servers"></a><span data-ttu-id="173a6-138">Récupérer les serveurs de noms</span><span class="sxs-lookup"><span data-stu-id="173a6-138">Retrieve name servers</span></span>

<span data-ttu-id="173a6-139">Vous pouvez déléguer votre tooAzure de zone DNS DNS, vous devez tout d’abord tooknow hello server nom de votre zone.</span><span class="sxs-lookup"><span data-stu-id="173a6-139">Before you can delegate your DNS zone tooAzure DNS, you first need tooknow hello name server names for your zone.</span></span> <span data-ttu-id="173a6-140">Azure DNS alloue des serveurs de noms à partir d’un pool chaque fois qu’une zone est créée.</span><span class="sxs-lookup"><span data-stu-id="173a6-140">Azure DNS allocates name servers from a pool each time a zone is created.</span></span>

1. <span data-ttu-id="173a6-141">Avec zone DNS de hello créé, Bonjour Azure portal **favoris** volet, cliquez sur **toutes les ressources**.</span><span class="sxs-lookup"><span data-stu-id="173a6-141">With hello DNS zone created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="173a6-142">Cliquez sur hello **contoso.net** zone DNS Bonjour **toutes les ressources** panneau.</span><span class="sxs-lookup"><span data-stu-id="173a6-142">Click hello **contoso.net** DNS zone in hello **All resources** blade.</span></span> <span data-ttu-id="173a6-143">Si l’abonnement hello déjà sélectionné comporte plusieurs ressources, vous pouvez entrer **contoso.net** Bonjour filtre par nom...</span><span class="sxs-lookup"><span data-stu-id="173a6-143">If hello subscription you selected already has several resources in it, you can enter **contoso.net** in hello Filter by name…</span></span> <span data-ttu-id="173a6-144">passerelle d’application hello boîte tooeasily accès.</span><span class="sxs-lookup"><span data-stu-id="173a6-144">box tooeasily access hello application gateway.</span></span> 

1. <span data-ttu-id="173a6-145">Récupérer des serveurs de noms hello à partir du Panneau de zone DNS hello.</span><span class="sxs-lookup"><span data-stu-id="173a6-145">Retrieve hello name servers from hello DNS zone blade.</span></span> <span data-ttu-id="173a6-146">Dans cet exemple, la zone de hello 'contoso.net' a été affectée à des serveurs de nom ' ns1-01.azure-dns.com', 'ns2-01.azure-dns .net', ' ns3-01.azure-dns.org », et « ns4-01.azure-dns.info':</span><span class="sxs-lookup"><span data-stu-id="173a6-146">In this example, hello zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="173a6-148">DNS Azure crée automatiquement les enregistrements NS faisant autoritées dans votre zone contenant hello affecté des serveurs de noms.</span><span class="sxs-lookup"><span data-stu-id="173a6-148">Azure DNS automatically creates authoritative NS records in your zone containing hello assigned name servers.</span></span>  <span data-ttu-id="173a6-149">noms de serveur de noms toosee hello via Azure PowerShell ou CLI d’Azure, vous devez simplement tooretrieve ces enregistrements.</span><span class="sxs-lookup"><span data-stu-id="173a6-149">toosee hello name server names via Azure PowerShell or Azure CLI, you simply need tooretrieve these records.</span></span>

<span data-ttu-id="173a6-150">Hello exemples suivants fournissent également des étapes de hello serveurs de noms tooretrieve hello pour une zone DNS Azure avec PowerShell et CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="173a6-150">hello following examples also provide hello steps tooretrieve hello name servers for a zone in Azure DNS with PowerShell and Azure CLI.</span></span>

### <a name="powershell"></a><span data-ttu-id="173a6-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="173a6-151">PowerShell</span></span>

```powershell
# hello record name "@" is used toorefer toorecords at hello top of hello zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

<span data-ttu-id="173a6-152">Hello, l’exemple suivant est la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="173a6-152">hello following example is hello response.</span></span>

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

### <a name="azure-cli"></a><span data-ttu-id="173a6-153">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="173a6-153">Azure CLI</span></span>

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

<span data-ttu-id="173a6-154">Hello, l’exemple suivant est la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="173a6-154">hello following example is hello response.</span></span>

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

## <a name="delegate-hello-domain"></a><span data-ttu-id="173a6-155">Domaine de hello délégué</span><span class="sxs-lookup"><span data-stu-id="173a6-155">Delegate hello domain</span></span>

<span data-ttu-id="173a6-156">Maintenant que la zone DNS de hello est créé et que les serveurs de noms hello, le domaine parent hello doit toobe mis à jour avec les serveurs DNS de Azure hello.</span><span class="sxs-lookup"><span data-stu-id="173a6-156">Now that hello DNS zone is created and you have hello name servers, hello parent domain needs toobe updated with hello Azure DNS name servers.</span></span> <span data-ttu-id="173a6-157">Chaque bureau d’enregistrement a leurs propres enregistrements DNS management tools toochange hello name server pour un domaine.</span><span class="sxs-lookup"><span data-stu-id="173a6-157">Each registrar has their own DNS management tools toochange hello name server records for a domain.</span></span> <span data-ttu-id="173a6-158">Dans la page de gestion hello du bureau d’enregistrement DNS, modifier les enregistrements NS hello et remplacer les enregistrements NS hello hello ceux créé par le système DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="173a6-158">In hello registrar's DNS management page, edit hello NS records and replace hello NS records with hello ones Azure DNS created.</span></span>

<span data-ttu-id="173a6-159">Lors de la délégation un tooAzure de domaine DNS, vous devez utiliser des noms de serveur de nom de hello fournies par le système DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="173a6-159">When delegating a domain tooAzure DNS, you must use hello name server names provided by Azure DNS.</span></span> <span data-ttu-id="173a6-160">Il est recommandé de toouse toutes les quatre noms des noms de serveur, quel que soit le nom hello de votre domaine.</span><span class="sxs-lookup"><span data-stu-id="173a6-160">It is recommended toouse all four name server names, regardless of hello name of your domain.</span></span> <span data-ttu-id="173a6-161">Délégation de domaine ne nécessite pas de toouse de nom de serveur de nom hello hello du même domaine de niveau supérieur que votre domaine.</span><span class="sxs-lookup"><span data-stu-id="173a6-161">Domain delegation does not require hello name server name toouse hello same top-level domain as your domain.</span></span>

<span data-ttu-id="173a6-162">Vous ne devez pas utiliser « enregistrements glue » toopoint toohello Azure DNS nom adresses IP de serveur, étant donné que ces adresses IP peuvent changer dans les futures.</span><span class="sxs-lookup"><span data-stu-id="173a6-162">You should not use 'glue records' toopoint toohello Azure DNS name server IP addresses, since these IP addresses may change in future.</span></span> <span data-ttu-id="173a6-163">Les délégations utilisant les noms de serveurs de noms dans votre propre zone (parfois appelés « serveurs de noms de redirection vers un microsite ») ne sont actuellement pas prises en charge dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="173a6-163">Delegations using name server names in your own zone, sometimes called 'vanity name servers', are not currently supported in Azure DNS.</span></span>

## <a name="verify-name-resolution-is-working"></a><span data-ttu-id="173a6-164">Vérifier le fonctionnement de la résolution de noms</span><span class="sxs-lookup"><span data-stu-id="173a6-164">Verify name resolution is working</span></span>

<span data-ttu-id="173a6-165">Après avoir effectué la délégation de hello, vous pouvez vérifier que la résolution de noms fonctionne à l’aide d’un outil tel que « nslookup » tooquery hello enregistrement SOA de votre zone (qui est créé automatiquement lors de la création de la zone de hello).</span><span class="sxs-lookup"><span data-stu-id="173a6-165">After completing hello delegation, you can verify that name resolution is working by using a tool such as 'nslookup' tooquery hello SOA record for your zone (which is also automatically created when hello zone is created).</span></span>

<span data-ttu-id="173a6-166">Vous n’avez pas de serveurs de noms DNS Azure toospecify hello, si la délégation contrainte hello a été configurée correctement, hello DNS résolution processus normal détecte automatiquement les serveurs de noms hello.</span><span class="sxs-lookup"><span data-stu-id="173a6-166">You do not have toospecify hello Azure DNS name servers, if hello delegation has been set up correctly, hello normal DNS resolution process finds hello name servers automatically.</span></span>

```
nslookup -type=SOA contoso.com
```

<span data-ttu-id="173a6-167">Hello Voici un exemple de réponse à partir de hello précédant la commande :</span><span class="sxs-lookup"><span data-stu-id="173a6-167">hello following is an example response from hello preceding command:</span></span>

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

## <a name="delegate-sub-domains-in-azure-dns"></a><span data-ttu-id="173a6-168">Déléguer les sous-domaines dans Azure DNS</span><span class="sxs-lookup"><span data-stu-id="173a6-168">Delegate sub-domains in Azure DNS</span></span>

<span data-ttu-id="173a6-169">Si vous souhaitez tooset d’une zone enfant distincte, vous pouvez déléguer un sous-domaine dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="173a6-169">If you want tooset up a separate child zone, you can delegate a sub-domain in Azure DNS.</span></span> <span data-ttu-id="173a6-170">Par exemple, avoir défini et délégués 'contoso.net' dans le système DNS Azure, supposons que vous aimeriez tooset d’une zone enfant distincte, 'partners.contoso.net'.</span><span class="sxs-lookup"><span data-stu-id="173a6-170">For example, having set up and delegated 'contoso.net' in Azure DNS, suppose you would like tooset up a separate child zone, 'partners.contoso.net'.</span></span>

1. <span data-ttu-id="173a6-171">Créer hello enfant zone 'partners.contoso.net' dans le système DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="173a6-171">Create hello child zone 'partners.contoso.net' in Azure DNS.</span></span>
2. <span data-ttu-id="173a6-172">Recherchez les enregistrements NS faisant autoritées hello dans hello enfant zone tooobtain hello serveurs de noms hébergeant la zone enfant de hello dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="173a6-172">Look up hello authoritative NS records in hello child zone tooobtain hello name servers hosting hello child zone in Azure DNS.</span></span>
3. <span data-ttu-id="173a6-173">Déléguer hello enfant en configurant les enregistrements NS dans la zone parente de hello pointant vers la zone enfant de toohello.</span><span class="sxs-lookup"><span data-stu-id="173a6-173">Delegate hello child zone by configuring NS records in hello parent zone pointing toohello child zone.</span></span>

### <a name="create-a-dns-zone"></a><span data-ttu-id="173a6-174">Création d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="173a6-174">Create a DNS zone</span></span>

1. <span data-ttu-id="173a6-175">Se connecter toohello portail Azure</span><span class="sxs-lookup"><span data-stu-id="173a6-175">Sign in toohello Azure portal</span></span>
1. <span data-ttu-id="173a6-176">Dans le menu du Hub hello, cliquez sur, puis cliquez sur **Nouveau > mise en réseau >** puis cliquez sur **zone DNS** Panneau de zone DNS de créer tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="173a6-176">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![Zone DNS](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="173a6-178">Sur hello **zone DNS de créer** panneau hello valeurs suivantes, puis entrez **créer**:</span><span class="sxs-lookup"><span data-stu-id="173a6-178">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>

   | <span data-ttu-id="173a6-179">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="173a6-179">**Setting**</span></span> | <span data-ttu-id="173a6-180">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="173a6-180">**Value**</span></span> | <span data-ttu-id="173a6-181">**Détails**</span><span class="sxs-lookup"><span data-stu-id="173a6-181">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="173a6-182">**Name**</span><span class="sxs-lookup"><span data-stu-id="173a6-182">**Name**</span></span>|<span data-ttu-id="173a6-183">partners.contoso.net</span><span class="sxs-lookup"><span data-stu-id="173a6-183">partners.contoso.net</span></span>|<span data-ttu-id="173a6-184">nom Hello de zone DNS de hello</span><span class="sxs-lookup"><span data-stu-id="173a6-184">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="173a6-185">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="173a6-185">**Subscription**</span></span>|<span data-ttu-id="173a6-186">[Votre abonnement]</span><span class="sxs-lookup"><span data-stu-id="173a6-186">[Your subscription]</span></span>|<span data-ttu-id="173a6-187">Sélectionnez une passerelle d’application abonnement toocreate hello dans.</span><span class="sxs-lookup"><span data-stu-id="173a6-187">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="173a6-188">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="173a6-188">**Resource group**</span></span>|<span data-ttu-id="173a6-189">**Use Existing :** (Utiliser existant) contosoRG</span><span class="sxs-lookup"><span data-stu-id="173a6-189">**Use Existing:** contosoRG</span></span>|<span data-ttu-id="173a6-190">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="173a6-190">Create a resource group.</span></span> <span data-ttu-id="173a6-191">nom de groupe de ressources Hello doit être unique au sein de l’abonnement hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="173a6-191">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="173a6-192">toolearn plus d’informations sur les groupes de ressources, lire hello [le Gestionnaire de ressources](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) l’article de vue d’ensemble.</span><span class="sxs-lookup"><span data-stu-id="173a6-192">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="173a6-193">**Emplacement**</span><span class="sxs-lookup"><span data-stu-id="173a6-193">**Location**</span></span>|<span data-ttu-id="173a6-194">Ouest des États-Unis</span><span class="sxs-lookup"><span data-stu-id="173a6-194">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="173a6-195">groupe de ressources Hello fait référence emplacement toohello hello du groupe de ressources et n’a aucun impact sur la zone DNS de hello.</span><span class="sxs-lookup"><span data-stu-id="173a6-195">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="173a6-196">emplacement des zones DNS Hello est toujours « globaux » et n’est pas affiché.</span><span class="sxs-lookup"><span data-stu-id="173a6-196">hello DNS zone location is always "global", and is not shown.</span></span>

### <a name="retrieve-name-servers"></a><span data-ttu-id="173a6-197">Récupérer les serveurs de noms</span><span class="sxs-lookup"><span data-stu-id="173a6-197">Retrieve name servers</span></span>

1. <span data-ttu-id="173a6-198">Avec zone DNS de hello créé, Bonjour Azure portal **favoris** volet, cliquez sur **toutes les ressources**.</span><span class="sxs-lookup"><span data-stu-id="173a6-198">With hello DNS zone created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="173a6-199">Cliquez sur hello **partners.contoso.net** zone DNS Bonjour **toutes les ressources** panneau.</span><span class="sxs-lookup"><span data-stu-id="173a6-199">Click hello **partners.contoso.net** DNS zone in hello **All resources** blade.</span></span> <span data-ttu-id="173a6-200">Si l’abonnement hello déjà sélectionné comporte plusieurs ressources, vous pouvez entrer **partners.contoso.net** Bonjour filtre par nom...</span><span class="sxs-lookup"><span data-stu-id="173a6-200">If hello subscription you selected already has several resources in it, you can enter **partners.contoso.net** in hello Filter by name…</span></span> <span data-ttu-id="173a6-201">zone DNS zone tooeasily accès hello.</span><span class="sxs-lookup"><span data-stu-id="173a6-201">box tooeasily access hello DNS zone.</span></span>

1. <span data-ttu-id="173a6-202">Récupérer des serveurs de noms hello à partir du Panneau de zone DNS hello.</span><span class="sxs-lookup"><span data-stu-id="173a6-202">Retrieve hello name servers from hello DNS zone blade.</span></span> <span data-ttu-id="173a6-203">Dans cet exemple, la zone de hello 'contoso.net' a été affectée à des serveurs de nom ' ns1-01.azure-dns.com', 'ns2-01.azure-dns .net', ' ns3-01.azure-dns.org », et « ns4-01.azure-dns.info':</span><span class="sxs-lookup"><span data-stu-id="173a6-203">In this example, hello zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="173a6-205">DNS Azure crée automatiquement les enregistrements NS faisant autoritées dans votre zone contenant hello affecté des serveurs de noms.</span><span class="sxs-lookup"><span data-stu-id="173a6-205">Azure DNS automatically creates authoritative NS records in your zone containing hello assigned name servers.</span></span>  <span data-ttu-id="173a6-206">noms de serveur de noms toosee hello via Azure PowerShell ou CLI d’Azure, vous devez simplement tooretrieve ces enregistrements.</span><span class="sxs-lookup"><span data-stu-id="173a6-206">toosee hello name server names via Azure PowerShell or Azure CLI, you simply need tooretrieve these records.</span></span>

### <a name="create-name-server-record-in-parent-zone"></a><span data-ttu-id="173a6-207">Créer un enregistrement de serveur de noms dans la zone parente</span><span class="sxs-lookup"><span data-stu-id="173a6-207">Create name server record in parent zone</span></span>

1. <span data-ttu-id="173a6-208">Accédez toohello **contoso.net** zone DNS Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="173a6-208">Navigate toohello **contoso.net** DNS zone in hello Azure portal.</span></span>
1. <span data-ttu-id="173a6-209">Cliquez sur **+ Jeu d’enregistrements**.</span><span class="sxs-lookup"><span data-stu-id="173a6-209">Click **+ Record set**</span></span>
1. <span data-ttu-id="173a6-210">Sur hello **ajouter le jeu d’enregistrements** panneau, entrez hello valeurs suivantes, puis cliquez sur **OK**:</span><span class="sxs-lookup"><span data-stu-id="173a6-210">On hello **Add record set** blade, enter hello following values, then click **OK**:</span></span>

   | <span data-ttu-id="173a6-211">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="173a6-211">**Setting**</span></span> | <span data-ttu-id="173a6-212">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="173a6-212">**Value**</span></span> | <span data-ttu-id="173a6-213">**Détails**</span><span class="sxs-lookup"><span data-stu-id="173a6-213">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="173a6-214">**Name**</span><span class="sxs-lookup"><span data-stu-id="173a6-214">**Name**</span></span>|<span data-ttu-id="173a6-215">partenaires</span><span class="sxs-lookup"><span data-stu-id="173a6-215">partners</span></span>|<span data-ttu-id="173a6-216">nom de Hello de zone DNS d’enfant hello</span><span class="sxs-lookup"><span data-stu-id="173a6-216">hello name of hello child DNS zone</span></span>|
   |<span data-ttu-id="173a6-217">**Type**</span><span class="sxs-lookup"><span data-stu-id="173a6-217">**Type**</span></span>|<span data-ttu-id="173a6-218">NS</span><span class="sxs-lookup"><span data-stu-id="173a6-218">NS</span></span>|<span data-ttu-id="173a6-219">Utilisez NS pour les enregistrements de serveur de noms.</span><span class="sxs-lookup"><span data-stu-id="173a6-219">Use NS for name server records.</span></span>|
   |<span data-ttu-id="173a6-220">**TTL**</span><span class="sxs-lookup"><span data-stu-id="173a6-220">**TTL**</span></span>|<span data-ttu-id="173a6-221">1</span><span class="sxs-lookup"><span data-stu-id="173a6-221">1</span></span>|<span data-ttu-id="173a6-222">Heure toolive.</span><span class="sxs-lookup"><span data-stu-id="173a6-222">Time toolive.</span></span>|
   |<span data-ttu-id="173a6-223">**Unité de durée de vie**</span><span class="sxs-lookup"><span data-stu-id="173a6-223">**TTL unit**</span></span>|<span data-ttu-id="173a6-224">Heures</span><span class="sxs-lookup"><span data-stu-id="173a6-224">Hours</span></span>|<span data-ttu-id="173a6-225">définit les toohours toolive unité de temps</span><span class="sxs-lookup"><span data-stu-id="173a6-225">sets time toolive unit toohours</span></span>|
   |<span data-ttu-id="173a6-226">**SERVEUR DE NOMS**</span><span class="sxs-lookup"><span data-stu-id="173a6-226">**NAME SERVER**</span></span>|<span data-ttu-id="173a6-227">{serveurs de noms à partir de la zone partners.contoso.net}</span><span class="sxs-lookup"><span data-stu-id="173a6-227">{name servers from partners.contoso.net zone}</span></span>|<span data-ttu-id="173a6-228">Entrez les 4 hello de serveurs de noms à partir de la zone de partners.contoso.net.</span><span class="sxs-lookup"><span data-stu-id="173a6-228">Enter all 4 of hello name servers from partners.contoso.net zone.</span></span> |

   ![Dns-nameserver](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a><span data-ttu-id="173a6-230">Déléguer des sous-domaines dans Azure DNS avec d’autres outils</span><span class="sxs-lookup"><span data-stu-id="173a6-230">Delegating sub-domains in Azure DNS with other tools</span></span>

<span data-ttu-id="173a6-231">Hello suivants fournit des exemples des étapes de hello toodelegate des sous-domaines dans DNS Azure avec PowerShell et l’interface CLI :</span><span class="sxs-lookup"><span data-stu-id="173a6-231">hello following examples provide hello steps toodelegate sub-domains in Azure DNS with PowerShell and CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="173a6-232">PowerShell</span><span class="sxs-lookup"><span data-stu-id="173a6-232">PowerShell</span></span>

<span data-ttu-id="173a6-233">Hello PowerShell l’exemple suivant montre comment cela fonctionne.</span><span class="sxs-lookup"><span data-stu-id="173a6-233">hello following PowerShell example demonstrates how this works.</span></span> <span data-ttu-id="173a6-234">Hello mêmes étapes peuvent être exécutées via hello portail Azure ou via hello CLI d’Azure inter-plateformes.</span><span class="sxs-lookup"><span data-stu-id="173a6-234">hello same steps can be executed via hello Azure portal, or via hello cross-platform Azure CLI.</span></span>

```powershell
# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve hello authoritative NS records from hello child zone as shown in hello next example. This contains hello name servers assigned toohello child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create hello corresponding NS record set in hello parent zone toocomplete hello delegation. hello record set name in hello parent zone matches hello child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

<span data-ttu-id="173a6-235">Utilisez `nslookup` tooverify que tout est configuré correctement en recherchant hello enregistrement SOA de zone enfant de hello.</span><span class="sxs-lookup"><span data-stu-id="173a6-235">Use `nslookup` tooverify that everything is set up correctly by looking up hello SOA record of hello child zone.</span></span>

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

#### <a name="azure-cli"></a><span data-ttu-id="173a6-236">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="173a6-236">Azure CLI</span></span>

```azurecli
#!/bin/bash

# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

<span data-ttu-id="173a6-237">Récupérer les serveurs nom hello hello `partners.contoso.net` zone à partir de la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="173a6-237">Retrieve hello name servers for hello `partners.contoso.net` zone from hello output.</span></span>

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

<span data-ttu-id="173a6-238">Créer le jeu d’enregistrements hello et les enregistrements NS pour chaque serveur de noms.</span><span class="sxs-lookup"><span data-stu-id="173a6-238">Create hello record set and NS records for each name server.</span></span>

```azurecli
#!/bin/bash

# Create hello record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a><span data-ttu-id="173a6-239">Supprimer toutes les ressources</span><span class="sxs-lookup"><span data-stu-id="173a6-239">Delete all resources</span></span>

<span data-ttu-id="173a6-240">toodelete toutes les ressources créées dans cet article, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="173a6-240">toodelete all resources created in this article, complete hello following steps:</span></span>

1. <span data-ttu-id="173a6-241">Bonjour Azure portal **favoris** volet, cliquez sur **toutes les ressources**.</span><span class="sxs-lookup"><span data-stu-id="173a6-241">In hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="173a6-242">Cliquez sur hello **contosorg** groupe de ressources Bonjour toutes les lames de ressources.</span><span class="sxs-lookup"><span data-stu-id="173a6-242">Click hello **contosorg** resource group in hello All resources blade.</span></span> <span data-ttu-id="173a6-243">Si l’abonnement hello déjà sélectionné comporte plusieurs ressources, vous pouvez entrer **contosorg** Bonjour **filtrer par nom...**</span><span class="sxs-lookup"><span data-stu-id="173a6-243">If hello subscription you selected already has several resources in it, you can enter **contosorg** in hello **Filter by name…**</span></span> <span data-ttu-id="173a6-244">groupe de ressources boîte tooeasily accès hello.</span><span class="sxs-lookup"><span data-stu-id="173a6-244">box tooeasily access hello resource group.</span></span>
1. <span data-ttu-id="173a6-245">Bonjour **contosorg** panneau, cliquez sur hello **supprimer** bouton.</span><span class="sxs-lookup"><span data-stu-id="173a6-245">In hello **contosorg** blade, click hello **Delete** button.</span></span>
1. <span data-ttu-id="173a6-246">Hello portail requiert vous tootype hello nom du tooconfirm de groupe de ressources hello que vous souhaitez toodelete il.</span><span class="sxs-lookup"><span data-stu-id="173a6-246">hello portal requires you tootype hello name of hello resource group tooconfirm that you want toodelete it.</span></span> <span data-ttu-id="173a6-247">Type *contosorg* pour le nom du groupe de ressources de hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="173a6-247">Type *contosorg* for hello resource group name, then click **Delete**.</span></span> <span data-ttu-id="173a6-248">La suppression d’un groupe de ressources supprime toutes les ressources dans le groupe de ressources hello, toujours que tooconfirm contenu hello d’un groupe de ressources avant de le supprimer.</span><span class="sxs-lookup"><span data-stu-id="173a6-248">Deleting a resource group deletes all resources within hello resource group, so always be sure tooconfirm hello contents of a resource group before deleting it.</span></span> <span data-ttu-id="173a6-249">portail de Hello supprime toutes les ressources contenues dans le groupe de ressources hello, puis supprime le groupe de ressources hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="173a6-249">hello portal deletes all resources contained within hello resource group, then deletes hello resource group itself.</span></span> <span data-ttu-id="173a6-250">Cette opération prend plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="173a6-250">This process takes several minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="173a6-251">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="173a6-251">Next steps</span></span>

[<span data-ttu-id="173a6-252">Gestion des zones DNS</span><span class="sxs-lookup"><span data-stu-id="173a6-252">Manage DNS zones</span></span>](dns-operations-dnszones.md)

[<span data-ttu-id="173a6-253">Gestion des enregistrements DNS</span><span class="sxs-lookup"><span data-stu-id="173a6-253">Manage DNS records</span></span>](dns-operations-recordsets.md)
