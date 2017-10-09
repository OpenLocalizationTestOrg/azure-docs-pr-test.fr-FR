---
title: "les zones DNS aaaCreate et jeux d’enregistrements à l’aide d’Azure DNS hello .NET SDK | Documents Microsoft"
description: "Comment les zones DNS toocreate et enregistrement définit dans Azure DNS à l’aide de hello du SDK .NET."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: eed99b87-f4d4-4fbf-a926-263f7e30b884
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/19/2016
ms.author: jonatul
ms.openlocfilehash: e3bab98b13b787427219acb7ec55e53490512fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-zones-and-record-sets-using-hello-net-sdk"></a><span data-ttu-id="2288a-103">Créer des zones DNS et des jeux d’enregistrements à l’aide de hello .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2288a-103">Create DNS zones and record sets using hello .NET SDK</span></span>

<span data-ttu-id="2288a-104">Vous pouvez automatiser les opérations toocreate, supprimer ou mettre à jour les zones DNS, jeux d’enregistrements et les enregistrements à l’aide de DNS SDK avec la bibliothèque de gestion DNS de .NET.</span><span class="sxs-lookup"><span data-stu-id="2288a-104">You can automate operations toocreate, delete, or update DNS zones, record sets, and records by using DNS SDK with .NET DNS Management library.</span></span> <span data-ttu-id="2288a-105">Un projet Visual Studio complet est disponible [ici.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span><span class="sxs-lookup"><span data-stu-id="2288a-105">A full Visual Studio project is available [here.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span></span>

## <a name="create-a-service-principal-account"></a><span data-ttu-id="2288a-106">Créer un compte de principal du service</span><span class="sxs-lookup"><span data-stu-id="2288a-106">Create a service principal account</span></span>

<span data-ttu-id="2288a-107">En règle générale, les ressources tooAzure de l’accès par programme est accordé via un compte dédié, au lieu de vos propres informations d’identification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2288a-107">Typically, programmatic access tooAzure resources is granted via a dedicated account rather than your own user credentials.</span></span> <span data-ttu-id="2288a-108">Ces comptes dédiés sont appelés comptes de « principal du service ».</span><span class="sxs-lookup"><span data-stu-id="2288a-108">These dedicated accounts are called 'service principal' accounts.</span></span> <span data-ttu-id="2288a-109">toouse hello Azure SDK DNS exemple de projet, vous devez toocreate un compte de principal du service et lui attribuer les autorisations correctes de hello.</span><span class="sxs-lookup"><span data-stu-id="2288a-109">toouse hello Azure DNS SDK sample project, you first need toocreate a service principal account and assign it hello correct permissions.</span></span>

1. <span data-ttu-id="2288a-110">Suivez [ces instructions](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate un compte de principal du service (exemple de projet de kit de développement logiciel Azure DNS hello suppose l’authentification basée sur mot de passe).</span><span class="sxs-lookup"><span data-stu-id="2288a-110">Follow [these instructions](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate a service principal account (hello Azure DNS SDK sample project assumes password-based authentication.)</span></span>
2. <span data-ttu-id="2288a-111">Créez un groupe de ressources ([procédure](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span><span class="sxs-lookup"><span data-stu-id="2288a-111">Create a resource group ([here's how](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span></span>
3. <span data-ttu-id="2288a-112">Utilisez Azure RBAC toogrant hello principal groupe comptes de service « Collaborateur de Zone DNS » autorisations toohello ressource ([Voici comment](../active-directory/role-based-access-control-configure.md).)</span><span class="sxs-lookup"><span data-stu-id="2288a-112">Use Azure RBAC toogrant hello service principal account 'DNS Zone Contributor' permissions toohello resource group ([here's how](../active-directory/role-based-access-control-configure.md).)</span></span>
4. <span data-ttu-id="2288a-113">Si l’exemple de projet de kit de développement logiciel Azure DNS hello, modifiez fichier de « program.cs » hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2288a-113">If using hello Azure DNS SDK sample project, edit hello 'program.cs' file as follows:</span></span>

   * <span data-ttu-id="2288a-114">Insérer des valeurs correctes de hello pour hello tenantId, clientId (également appelé ID de compte), le secret (mot de passe de compte de principal du service) et ID d’abonnement utilisé à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="2288a-114">Insert hello correct values for hello tenantId, clientId (also known as account ID), secret (service principal account password) and subscriptionId as used in step 1.</span></span>
   * <span data-ttu-id="2288a-115">Entrez le nom de groupe de ressources hello choisi à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="2288a-115">Enter hello resource group name chosen in step 2.</span></span>
   * <span data-ttu-id="2288a-116">Entrez le nom de zone DNS de votre choix.</span><span class="sxs-lookup"><span data-stu-id="2288a-116">Enter a DNS zone name of your choice.</span></span>

## <a name="nuget-packages-and-namespace-declarations"></a><span data-ttu-id="2288a-117">Packages NuGet et déclaration des espaces de noms</span><span class="sxs-lookup"><span data-stu-id="2288a-117">NuGet packages and namespace declarations</span></span>

<span data-ttu-id="2288a-118">toouse hello DNS Azure .NET SDK, vous devez tooinstall hello **bibliothèque de gestion Azure DNS** package NuGet et autres requises des packages Azure.</span><span class="sxs-lookup"><span data-stu-id="2288a-118">toouse hello Azure DNS .NET SDK, you need tooinstall hello **Azure DNS Management Library** NuGet package and other required Azure packages.</span></span>

1. <span data-ttu-id="2288a-119">Dans **Visual Studio**, ouvrez un projet existant ou un nouveau projet.</span><span class="sxs-lookup"><span data-stu-id="2288a-119">In **Visual Studio**, open a project or new project.</span></span>
2. <span data-ttu-id="2288a-120">Accédez trop**outils**  **>**  **Gestionnaire de Package NuGet**  **>**  **gérer les Packages NuGet pour Solution...** .</span><span class="sxs-lookup"><span data-stu-id="2288a-120">Go too**Tools** **>** **NuGet Package Manager** **>** **Manage NuGet Packages for Solution...**.</span></span>
3. <span data-ttu-id="2288a-121">Cliquez sur **Parcourir**, activer hello **inclure la version préliminaire** case à cocher et le type **Microsoft.Azure.Management.Dns** dans la zone de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="2288a-121">Click **Browse**, enable hello **Include prerelease** checkbox, and type **Microsoft.Azure.Management.Dns** in hello search box.</span></span>
4. <span data-ttu-id="2288a-122">Sélectionnez un package hello et cliquez sur **installer** tooadd il projet de Visual Studio tooyour.</span><span class="sxs-lookup"><span data-stu-id="2288a-122">Select hello package and click **Install** tooadd it tooyour Visual Studio project.</span></span>
5. <span data-ttu-id="2288a-123">Répétez les processus hello ci-dessus hello d’installation tooalso suivant des packages : **Microsoft.Rest.ClientRuntime.Azure.Authentication** et **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="2288a-123">Repeat hello process above tooalso install hello following packages: **Microsoft.Rest.ClientRuntime.Azure.Authentication** and **Microsoft.Azure.Management.ResourceManager**.</span></span>

## <a name="add-namespace-declarations"></a><span data-ttu-id="2288a-124">Ajout de déclarations d'espaces de noms</span><span class="sxs-lookup"><span data-stu-id="2288a-124">Add namespace declarations</span></span>

<span data-ttu-id="2288a-125">Ajouter hello suivant des déclarations d’espace de noms</span><span class="sxs-lookup"><span data-stu-id="2288a-125">Add hello following namespace declarations</span></span>

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-hello-dns-management-client"></a><span data-ttu-id="2288a-126">Initialiser le client de gestion DNS hello</span><span class="sxs-lookup"><span data-stu-id="2288a-126">Initialize hello DNS management client</span></span>

<span data-ttu-id="2288a-127">Hello *DnsManagementClient* contient les méthodes de hello et les propriétés nécessaires pour la gestion des zones DNS et les jeux d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="2288a-127">hello *DnsManagementClient* contains hello methods and properties necessary for managing DNS zones and recordsets.</span></span>  <span data-ttu-id="2288a-128">Bonjour de code suivant enregistre dans le compte de principal du service toohello et crée un objet DnsManagementClient.</span><span class="sxs-lookup"><span data-stu-id="2288a-128">hello following code logs in toohello service principal account and creates a DnsManagementClient object.</span></span>

```cs
// Build hello service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a><span data-ttu-id="2288a-129">Créer ou mettre à jour une zone DNS</span><span class="sxs-lookup"><span data-stu-id="2288a-129">Create or update a DNS zone</span></span>

<span data-ttu-id="2288a-130">toocreate une zone DNS, tout d’abord un objet de la « Zone » est créé les paramètres de zone DNS toocontain hello.</span><span class="sxs-lookup"><span data-stu-id="2288a-130">toocreate a DNS zone, first a "Zone" object is created toocontain hello DNS zone parameters.</span></span> <span data-ttu-id="2288a-131">Étant donné que les zones DNS ne sont pas liés tooa une région spécifique, emplacement de hello a la valeur too'global'.</span><span class="sxs-lookup"><span data-stu-id="2288a-131">Because DNS zones are not linked tooa specific region, hello location is set too'global'.</span></span> <span data-ttu-id="2288a-132">Dans cet exemple, un [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) est également ajouté toohello zone.</span><span class="sxs-lookup"><span data-stu-id="2288a-132">In this example, an [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) is also added toohello zone.</span></span>

<span data-ttu-id="2288a-133">tooactually créer ou de mise à jour hello zone DNS Azure, objet de fuseau hello qui contient les paramètres de zone hello est passé toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* (méthode).</span><span class="sxs-lookup"><span data-stu-id="2288a-133">tooactually create or update hello zone in Azure DNS, hello zone object containing hello zone parameters is passed toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* method.</span></span>

> [!NOTE]
> <span data-ttu-id="2288a-134">DnsManagementClient prend en charge trois modes de fonctionnement : synchrone (« CreateOrUpdate »), asynchrone ('CreateOrUpdateAsync'), ou asynchrone avec la réponse de toohello HTTP d’accès (« CreateOrUpdateWithHttpMessagesAsync »).</span><span class="sxs-lookup"><span data-stu-id="2288a-134">DnsManagementClient supports three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access toohello HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>  <span data-ttu-id="2288a-135">Vous pouvez choisir l’un de ces modes, selon les besoins de votre application.</span><span class="sxs-lookup"><span data-stu-id="2288a-135">You can choose any of these modes, depending on your application needs.</span></span>

<span data-ttu-id="2288a-136">Azure DNS prend en charge l’accès simultané optimiste, appelé [ETags](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="2288a-136">Azure DNS supports optimistic concurrency, called [Etags](dns-getstarted-create-dnszone.md).</span></span> <span data-ttu-id="2288a-137">Dans cet exemple, en spécifiant « * » pour les en-tête hello 'If-None-Match' indique à Azure DNS toocreate une zone DNS s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="2288a-137">In this example, specifying "*" for hello 'If-None-Match' header tells Azure DNS toocreate a DNS zone if one does not already exist.</span></span>  <span data-ttu-id="2288a-138">appel de Hello échoue si une zone avec le nom donné de hello existe déjà dans hello groupe de ressources donné.</span><span class="sxs-lookup"><span data-stu-id="2288a-138">hello call fails if a zone with hello given name already exists in hello given resource group.</span></span>

```cs
// Create zone parameters
var dnsZoneParams = new Zone("global"); // All DNS zones must have location = "global"

// Create a Azure Resource Manager 'tag'.  This is optional.  You can add multiple tags
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");

// Create hello actual zone.
// Note: Uses 'If-None-Match *' ETAG check, so will fail if hello zone exists already.
// Note: For non-async usage, call dnsClient.Zones.CreateOrUpdate(resourceGroupName, zoneName, dnsZoneParams, null, "*")
// Note: For getting hello http response, call dnsClient.Zones.CreateOrUpdateWithHttpMessagesAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*")
var dnsZone = await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

## <a name="create-dns-record-sets-and-records"></a><span data-ttu-id="2288a-139">Créer des jeux d’enregistrements et d’enregistrements DNS</span><span class="sxs-lookup"><span data-stu-id="2288a-139">Create DNS record sets and records</span></span>

<span data-ttu-id="2288a-140">Les enregistrements DNS sont gérés en tant que jeu d'enregistrements.</span><span class="sxs-lookup"><span data-stu-id="2288a-140">DNS records are managed as a record set.</span></span> <span data-ttu-id="2288a-141">Un jeu d’enregistrements est un ensemble d’enregistrements par hello même nommer et enregistrer le type dans une zone.</span><span class="sxs-lookup"><span data-stu-id="2288a-141">A record set is a set of records with hello same name and record type within a zone.</span></span>  <span data-ttu-id="2288a-142">nom du jeu d’enregistrements Hello est le nom de la zone toohello relatif, ne Hello pas de nom DNS complet.</span><span class="sxs-lookup"><span data-stu-id="2288a-142">hello record set name is relative toohello zone name, not hello fully qualified DNS name.</span></span>

<span data-ttu-id="2288a-143">toocreate ou mise à jour un jeu d’enregistrements, un objet de paramètres de « RecordSet » est créé et passe trop*DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span><span class="sxs-lookup"><span data-stu-id="2288a-143">toocreate or update a record set, a "RecordSet" parameters object is created and passed too*DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span></span> <span data-ttu-id="2288a-144">Comme avec les zones DNS, il existe trois modes d’opération : synchrone (« CreateOrUpdate »), asynchrone ('CreateOrUpdateAsync'), ou asynchrone avec la réponse de toohello HTTP d’accès (« CreateOrUpdateWithHttpMessagesAsync »).</span><span class="sxs-lookup"><span data-stu-id="2288a-144">As with DNS zones, there are three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access toohello HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>

<span data-ttu-id="2288a-145">Comme avec les zones DNS, les opérations sur les jeux d’enregistrements prennent en charge l’accès concurrentiel optimiste.</span><span class="sxs-lookup"><span data-stu-id="2288a-145">As with DNS zones, operations on record sets include support for optimistic concurrency.</span></span>  <span data-ttu-id="2288a-146">Dans cet exemple, étant donné que ni 'If-Match' ni 'If-None-Match' est spécifiées, jeu d’enregistrements hello est toujours créé.</span><span class="sxs-lookup"><span data-stu-id="2288a-146">In this example, since neither 'If-Match' nor 'If-None-Match' are specified, hello record set is always created.</span></span>  <span data-ttu-id="2288a-147">Cet appel remplace tout enregistrement existant avec hello même nommer et enregistrer le type de cette zone DNS.</span><span class="sxs-lookup"><span data-stu-id="2288a-147">This call overwrites any existing record set with hello same name and record type in this DNS zone.</span></span>

```cs
// Create record set parameters
var recordSetParams = new RecordSet();
recordSetParams.TTL = 3600;

// Add records toohello record set parameter object.  In this case, we'll add a record of type 'A'
recordSetParams.ARecords = new List<ARecord>();
recordSetParams.ARecords.Add(new ARecord("1.2.3.4"));

// Add metadata toohello record set.  Similar tooAzure Resource Manager tags, this is optional and you can add multiple metadata name/value pairs
recordSetParams.Metadata = new Dictionary<string, string>();
recordSetParams.Metadata.Add("user", "Mary");

// Create hello actual record set in Azure DNS
// Note: no ETAG checks specified, will overwrite existing record set if one exists
var recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSetParams);
```

## <a name="get-zones-and-record-sets"></a><span data-ttu-id="2288a-148">Obtenir des zones et des jeux d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="2288a-148">Get zones and record sets</span></span>

<span data-ttu-id="2288a-149">Hello *DnsManagementClient.Zones.Get* et *DnsManagementClient.RecordSets.Get* méthodes récupèrent les zones individuelles et des jeux d’enregistrements, respectivement.</span><span class="sxs-lookup"><span data-stu-id="2288a-149">hello *DnsManagementClient.Zones.Get* and *DnsManagementClient.RecordSets.Get* methods retrieve individual zones and record sets, respectively.</span></span> <span data-ttu-id="2288a-150">Jeux d’enregistrements est identifiés par leur type, le nom et le groupe de zone et de ressources hello dans qu'elles existent.</span><span class="sxs-lookup"><span data-stu-id="2288a-150">RecordSets are identified by their type, name, and hello zone and resource group they exist in.</span></span> <span data-ttu-id="2288a-151">Les zones sont identifiées par leur groupe de ressources de nom et hello dans qu'elles existent.</span><span class="sxs-lookup"><span data-stu-id="2288a-151">Zones are identified by their name and hello resource group they exist in.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a><span data-ttu-id="2288a-152">Mettre à jour un jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="2288a-152">Update an existing record set</span></span>

<span data-ttu-id="2288a-153">tooupdate un enregistrement DNS existant défini, tout d’abord extraire jeu d’enregistrements hello, enregistrement hello de mise à jour le contenu du jeu, puis soumettez hello modification.</span><span class="sxs-lookup"><span data-stu-id="2288a-153">tooupdate an existing DNS record set, first retrieve hello record set, then update hello record set contents, then submit hello change.</span></span>  <span data-ttu-id="2288a-154">Dans cet exemple, nous spécifions hello 'Etag' à partir de hello récupérées ensemble d’enregistrements d’un paramètre de 'If-Match' hello.</span><span class="sxs-lookup"><span data-stu-id="2288a-154">In this example, we specify hello 'Etag' from hello retrieved record set in hello 'If-Match' parameter.</span></span> <span data-ttu-id="2288a-155">appel de Hello échoue si une opération simultanée a modifié hello ensemble d’enregistrements d’hello entre-temps.</span><span class="sxs-lookup"><span data-stu-id="2288a-155">hello call fails if a concurrent operation has modified hello record set in hello meantime.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record toohello local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update hello record set in Azure DNS
// Note: ETAG check specified, update will be rejected if hello record set has changed in hello meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a><span data-ttu-id="2288a-156">Répertorier les zones et les jeux d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="2288a-156">List zones and record sets</span></span>

<span data-ttu-id="2288a-157">les zones toolist, utilisez hello *DnsManagementClient.Zones.List...*  utilisent des méthodes qui prennent en charge la liste de toutes les zones d’un groupe de ressources donné ou toutes les zones d’un jeux d’enregistrements toolist abonnement Azure donné (sur les groupes de ressources.), *DnsManagementClient.RecordSets.List...*  méthodes qui prennent en charge de l’affichage de la liste tous les jeux d’enregistrements dans une zone donnée ou uniquement les jeux d’enregistrements d’un type spécifique.</span><span class="sxs-lookup"><span data-stu-id="2288a-157">toolist zones, use hello *DnsManagementClient.Zones.List...* methods, which support listing either all zones in a given resource group or all zones in a given Azure subscription (across resource groups.) toolist record sets, use *DnsManagementClient.RecordSets.List...* methods, which support either listing all record sets in a given zone or only those record sets of a specific type.</span></span>

<span data-ttu-id="2288a-158">Notez que les résultats peuvent être paginés lors du répertoriage des zones et des jeux d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="2288a-158">Note when listing zones and record sets that results may be paginated.</span></span>  <span data-ttu-id="2288a-159">Hello suivant montre l’exemple de comment tooiterate via les pages hello de résultats.</span><span class="sxs-lookup"><span data-stu-id="2288a-159">hello following example shows how tooiterate through hello pages of results.</span></span> <span data-ttu-id="2288a-160">(Une taille de page artificiellement small de '2' est utilisé tooforce pagination ; dans la pratique, ce paramètre doit être omis et hello de taille de page par défaut utilisée).</span><span class="sxs-lookup"><span data-stu-id="2288a-160">(An artificially small page size of '2' is used tooforce paging; in practice this parameter should be omitted and hello default page size used.)</span></span>

```cs
// Note: in this demo, we'll use a very small page size (2 record sets) toodemonstrate paging
// In practice, tooimprove performance you would use a large page size or just use hello system default
int recordSets = 0;
var page = await dnsClient.RecordSets.ListAllInResourceGroupAsync(resourceGroupName, zoneName, "2");
recordSets += page.Count();

while (page.NextPageLink != null)
{
    page = await dnsClient.RecordSets.ListAllInResourceGroupNextAsync(page.NextPageLink);
    recordSets += page.Count();
}
```

## <a name="next-steps"></a><span data-ttu-id="2288a-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2288a-161">Next steps</span></span>

<span data-ttu-id="2288a-162">Télécharger hello [exemple de projet Azure DNS .NET SDK](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), qui inclut d’autres exemples de la façon dont toouse hello Azure DNS .NET SDK, y compris des exemples pour les autres types d’enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="2288a-162">Download hello [Azure DNS .NET SDK sample project](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), which includes further examples of how toouse hello Azure DNS .NET SDK, including examples for other DNS record types.</span></span>
