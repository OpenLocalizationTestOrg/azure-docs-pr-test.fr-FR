---
title: "Créer des zones et des jeux d’enregistrements DNS dans Azure DNS à l’aide du Kit SDK .NET | Microsoft Docs"
description: "Comment créer des zones et des jeux d’enregistrements DNS dans Azure DNS à l’aide du SDK .NET."
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
ms.openlocfilehash: c0fb0be8da1c0ca48a4d43ea027d30a0bc17fe30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-dns-zones-and-record-sets-using-the-net-sdk"></a><span data-ttu-id="59f14-103">Créer des zones et des jeux d’enregistrements DNS à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="59f14-103">Create DNS zones and record sets using the .NET SDK</span></span>

<span data-ttu-id="59f14-104">Vous pouvez automatiser les opérations de création, de suppression ou de mise à jour des zones , des jeux d’enregistrements et des enregistrements DNS à l’aide du Kit SDK DNS avec la bibliothèque de gestion DNS de .NET.</span><span class="sxs-lookup"><span data-stu-id="59f14-104">You can automate operations to create, delete, or update DNS zones, record sets, and records by using DNS SDK with .NET DNS Management library.</span></span> <span data-ttu-id="59f14-105">Un projet Visual Studio complet est disponible [ici.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span><span class="sxs-lookup"><span data-stu-id="59f14-105">A full Visual Studio project is available [here.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span></span>

## <a name="create-a-service-principal-account"></a><span data-ttu-id="59f14-106">Créer un compte de principal du service</span><span class="sxs-lookup"><span data-stu-id="59f14-106">Create a service principal account</span></span>

<span data-ttu-id="59f14-107">En règle générale, l’accès par programme aux ressources Azure est accordé via un compte dédié au lieu de vos propres informations d’identification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="59f14-107">Typically, programmatic access to Azure resources is granted via a dedicated account rather than your own user credentials.</span></span> <span data-ttu-id="59f14-108">Ces comptes dédiés sont appelés comptes de « principal du service ».</span><span class="sxs-lookup"><span data-stu-id="59f14-108">These dedicated accounts are called 'service principal' accounts.</span></span> <span data-ttu-id="59f14-109">Pour utiliser l’exemple de projet de kit de développement logiciel Azure DNS, vous devez d’abord créer un compte de principal du service et lui attribuer les autorisations appropriées.</span><span class="sxs-lookup"><span data-stu-id="59f14-109">To use the Azure DNS SDK sample project, you first need to create a service principal account and assign it the correct permissions.</span></span>

1. <span data-ttu-id="59f14-110">Suivez [ces instructions](../azure-resource-manager/resource-group-authenticate-service-principal.md) pour créer un compte de principal du service (l’exemple de projet de kit de développement logiciel Azure DNS part du principe qu’il s’agit d’une authentification par mot de passe).</span><span class="sxs-lookup"><span data-stu-id="59f14-110">Follow [these instructions](../azure-resource-manager/resource-group-authenticate-service-principal.md) to create a service principal account (the Azure DNS SDK sample project assumes password-based authentication.)</span></span>
2. <span data-ttu-id="59f14-111">Créez un groupe de ressources ([procédure](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span><span class="sxs-lookup"><span data-stu-id="59f14-111">Create a resource group ([here's how](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span></span>
3. <span data-ttu-id="59f14-112">Utilisez Azure RBAC pour accorder une autorisation « Collaborateur de zone DNS » au groupe de ressources ([procédure](../active-directory/role-based-access-control-configure.md)).</span><span class="sxs-lookup"><span data-stu-id="59f14-112">Use Azure RBAC to grant the service principal account 'DNS Zone Contributor' permissions to the resource group ([here's how](../active-directory/role-based-access-control-configure.md).)</span></span>
4. <span data-ttu-id="59f14-113">Si vous utilisez l’exemple de projet de kit de développement logiciel Azure DNS, modifiez le fichier program.cs comme suit :</span><span class="sxs-lookup"><span data-stu-id="59f14-113">If using the Azure DNS SDK sample project, edit the 'program.cs' file as follows:</span></span>

   * <span data-ttu-id="59f14-114">Insérez les valeurs correctes pour tenantId, clientId (également appelé ID de compte), secret (mot de passe du compte du principal du service) et subscriptionId tels qu’utilisés à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="59f14-114">Insert the correct values for the tenantId, clientId (also known as account ID), secret (service principal account password) and subscriptionId as used in step 1.</span></span>
   * <span data-ttu-id="59f14-115">Entrez le nom du groupe de ressources choisi à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="59f14-115">Enter the resource group name chosen in step 2.</span></span>
   * <span data-ttu-id="59f14-116">Entrez le nom de zone DNS de votre choix.</span><span class="sxs-lookup"><span data-stu-id="59f14-116">Enter a DNS zone name of your choice.</span></span>

## <a name="nuget-packages-and-namespace-declarations"></a><span data-ttu-id="59f14-117">Packages NuGet et déclaration des espaces de noms</span><span class="sxs-lookup"><span data-stu-id="59f14-117">NuGet packages and namespace declarations</span></span>

<span data-ttu-id="59f14-118">Pour utiliser le Kit de développement logiciel .NET d’Azure DNS, vous devez installer le package NuGet de la **bibliothèque de gestion Azure DNS** et les autres packages Azure requis.</span><span class="sxs-lookup"><span data-stu-id="59f14-118">To use the Azure DNS .NET SDK, you need to install the **Azure DNS Management Library** NuGet package and other required Azure packages.</span></span>

1. <span data-ttu-id="59f14-119">Dans **Visual Studio**, ouvrez un projet existant ou un nouveau projet.</span><span class="sxs-lookup"><span data-stu-id="59f14-119">In **Visual Studio**, open a project or new project.</span></span>
2. <span data-ttu-id="59f14-120">Accédez à **Outils** **>** **Gestionnaire de package NuGet** **>** **Gérer les packages NuGet pour la solution**.</span><span class="sxs-lookup"><span data-stu-id="59f14-120">Go to **Tools** **>** **NuGet Package Manager** **>** **Manage NuGet Packages for Solution...**.</span></span>
3. <span data-ttu-id="59f14-121">Cliquez sur **Parcourir**, cochez la case **Inclure la version préliminaire** et tapez **Microsoft.Azure.Management.Dns** dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="59f14-121">Click **Browse**, enable the **Include prerelease** checkbox, and type **Microsoft.Azure.Management.Dns** in the search box.</span></span>
4. <span data-ttu-id="59f14-122">Sélectionnez le package et cliquez sur **Installer** pour l’ajouter à votre projet Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="59f14-122">Select the package and click **Install** to add it to your Visual Studio project.</span></span>
5. <span data-ttu-id="59f14-123">Répétez la procédure ci-dessus pour installer les packages suivants : **Microsoft.Rest.ClientRuntime.Azure.Authentication** et **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="59f14-123">Repeat the process above to also install the following packages: **Microsoft.Rest.ClientRuntime.Azure.Authentication** and **Microsoft.Azure.Management.ResourceManager**.</span></span>

## <a name="add-namespace-declarations"></a><span data-ttu-id="59f14-124">Ajout de déclarations d'espaces de noms</span><span class="sxs-lookup"><span data-stu-id="59f14-124">Add namespace declarations</span></span>

<span data-ttu-id="59f14-125">Ajoutez les déclarations d’espace de noms suivantes :</span><span class="sxs-lookup"><span data-stu-id="59f14-125">Add the following namespace declarations</span></span>

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-the-dns-management-client"></a><span data-ttu-id="59f14-126">Initialiser le client de gestion DNS</span><span class="sxs-lookup"><span data-stu-id="59f14-126">Initialize the DNS management client</span></span>

<span data-ttu-id="59f14-127">Le *DnsManagementClient* contient les méthodes et les propriétés nécessaires à la gestion des zones et des jeux d’enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="59f14-127">The *DnsManagementClient* contains the methods and properties necessary for managing DNS zones and recordsets.</span></span>  <span data-ttu-id="59f14-128">Le code suivant ouvre une session du compte de principal du service et crée un objet DnsManagementClient.</span><span class="sxs-lookup"><span data-stu-id="59f14-128">The following code logs in to the service principal account and creates a DnsManagementClient object.</span></span>

```cs
// Build the service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a><span data-ttu-id="59f14-129">Créer ou mettre à jour une zone DNS</span><span class="sxs-lookup"><span data-stu-id="59f14-129">Create or update a DNS zone</span></span>

<span data-ttu-id="59f14-130">Pour créer une zone DNS, un objet « Zone » est d’abord créé pour contenir les paramètres de la zone DNS.</span><span class="sxs-lookup"><span data-stu-id="59f14-130">To create a DNS zone, first a "Zone" object is created to contain the DNS zone parameters.</span></span> <span data-ttu-id="59f14-131">Comme les zones DNS ne sont pas liées à une région spécifique, l’emplacement est défini sur « global ».</span><span class="sxs-lookup"><span data-stu-id="59f14-131">Because DNS zones are not linked to a specific region, the location is set to 'global'.</span></span> <span data-ttu-id="59f14-132">Dans cet exemple, une [« balise » Azure Resource Manager](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) est également ajoutée à la zone.</span><span class="sxs-lookup"><span data-stu-id="59f14-132">In this example, an [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) is also added to the zone.</span></span>

<span data-ttu-id="59f14-133">Pour créer ou mettre à jour la zone dans Azure DNS, l’objet de zone qui contient les paramètres de zone est transmis à la méthode *DnsManagementClient.Zones.CreateOrUpdateAsyc* .</span><span class="sxs-lookup"><span data-stu-id="59f14-133">To actually create or update the zone in Azure DNS, the zone object containing the zone parameters is passed to the *DnsManagementClient.Zones.CreateOrUpdateAsyc* method.</span></span>

> [!NOTE]
> <span data-ttu-id="59f14-134">DnsManagementClient prend en charge trois modes de fonctionnement : synchrone (CreateOrUpdate), asynchrone (CreateOrUpdateAsync) ou asynchrone avec accès à la réponse HTTP (CreateOrUpdateWithHttpMessagesAsync).</span><span class="sxs-lookup"><span data-stu-id="59f14-134">DnsManagementClient supports three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access to the HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>  <span data-ttu-id="59f14-135">Vous pouvez choisir l’un de ces modes, selon les besoins de votre application.</span><span class="sxs-lookup"><span data-stu-id="59f14-135">You can choose any of these modes, depending on your application needs.</span></span>

<span data-ttu-id="59f14-136">Azure DNS prend en charge l’accès simultané optimiste, appelé [ETags](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="59f14-136">Azure DNS supports optimistic concurrency, called [Etags](dns-getstarted-create-dnszone.md).</span></span> <span data-ttu-id="59f14-137">Dans cet exemple, le fait de spécifier « * » pour l’en-tête « If-None-Match » indique à Azure DNS de créer une zone DNS si celle-ci n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="59f14-137">In this example, specifying "*" for the 'If-None-Match' header tells Azure DNS to create a DNS zone if one does not already exist.</span></span>  <span data-ttu-id="59f14-138">L’appel échoue si une zone portant le nom spécifié existe déjà dans le groupe de ressources donné.</span><span class="sxs-lookup"><span data-stu-id="59f14-138">The call fails if a zone with the given name already exists in the given resource group.</span></span>

```cs
// Create zone parameters
var dnsZoneParams = new Zone("global"); // All DNS zones must have location = "global"

// Create a Azure Resource Manager 'tag'.  This is optional.  You can add multiple tags
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");

// Create the actual zone.
// Note: Uses 'If-None-Match *' ETAG check, so will fail if the zone exists already.
// Note: For non-async usage, call dnsClient.Zones.CreateOrUpdate(resourceGroupName, zoneName, dnsZoneParams, null, "*")
// Note: For getting the http response, call dnsClient.Zones.CreateOrUpdateWithHttpMessagesAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*")
var dnsZone = await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

## <a name="create-dns-record-sets-and-records"></a><span data-ttu-id="59f14-139">Créer des jeux d’enregistrements et d’enregistrements DNS</span><span class="sxs-lookup"><span data-stu-id="59f14-139">Create DNS record sets and records</span></span>

<span data-ttu-id="59f14-140">Les enregistrements DNS sont gérés en tant que jeu d'enregistrements.</span><span class="sxs-lookup"><span data-stu-id="59f14-140">DNS records are managed as a record set.</span></span> <span data-ttu-id="59f14-141">Un jeu d’enregistrements est un ensemble d’enregistrements ayant le même nom et le même type d’enregistrement au sein d’une zone.</span><span class="sxs-lookup"><span data-stu-id="59f14-141">A record set is a set of records with the same name and record type within a zone.</span></span>  <span data-ttu-id="59f14-142">Le nom du jeu d’enregistrements est relatif au nom de zone, et pas au nom DNS.</span><span class="sxs-lookup"><span data-stu-id="59f14-142">The record set name is relative to the zone name, not the fully qualified DNS name.</span></span>

<span data-ttu-id="59f14-143">Pour créer ou mettre à jour un jeu d’enregistrements, un objet « RecordSet » est créé et transmis à la méthode *DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span><span class="sxs-lookup"><span data-stu-id="59f14-143">To create or update a record set, a "RecordSet" parameters object is created and passed to *DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span></span> <span data-ttu-id="59f14-144">Comme avec les zones DNS, il existe trois modes de fonctionnement : synchrone (CreateOrUpdate), asynchrone (CreateOrUpdateAsync) ou asynchrone avec accès à la réponse HTTP (CreateOrUpdateWithHttpMessagesAsync).</span><span class="sxs-lookup"><span data-stu-id="59f14-144">As with DNS zones, there are three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access to the HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>

<span data-ttu-id="59f14-145">Comme avec les zones DNS, les opérations sur les jeux d’enregistrements prennent en charge l’accès concurrentiel optimiste.</span><span class="sxs-lookup"><span data-stu-id="59f14-145">As with DNS zones, operations on record sets include support for optimistic concurrency.</span></span>  <span data-ttu-id="59f14-146">Dans cet exemple, étant donné que ni « If-Match » ni « If-None-Match » n’est spécifié, le jeu d’enregistrements est toujours créé.</span><span class="sxs-lookup"><span data-stu-id="59f14-146">In this example, since neither 'If-Match' nor 'If-None-Match' are specified, the record set is always created.</span></span>  <span data-ttu-id="59f14-147">Cet appel remplace tout jeu d’enregistrements existant portant le même nom et le même type d’enregistrement dans cette zone DNS.</span><span class="sxs-lookup"><span data-stu-id="59f14-147">This call overwrites any existing record set with the same name and record type in this DNS zone.</span></span>

```cs
// Create record set parameters
var recordSetParams = new RecordSet();
recordSetParams.TTL = 3600;

// Add records to the record set parameter object.  In this case, we'll add a record of type 'A'
recordSetParams.ARecords = new List<ARecord>();
recordSetParams.ARecords.Add(new ARecord("1.2.3.4"));

// Add metadata to the record set.  Similar to Azure Resource Manager tags, this is optional and you can add multiple metadata name/value pairs
recordSetParams.Metadata = new Dictionary<string, string>();
recordSetParams.Metadata.Add("user", "Mary");

// Create the actual record set in Azure DNS
// Note: no ETAG checks specified, will overwrite existing record set if one exists
var recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSetParams);
```

## <a name="get-zones-and-record-sets"></a><span data-ttu-id="59f14-148">Obtenir des zones et des jeux d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="59f14-148">Get zones and record sets</span></span>

<span data-ttu-id="59f14-149">Les méthodes *DnsManagementClient.Zones.Get* et *DnsManagementClient.RecordSets.Get* récupèrent respectivement les zones et les jeux d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="59f14-149">The *DnsManagementClient.Zones.Get* and *DnsManagementClient.RecordSets.Get* methods retrieve individual zones and record sets, respectively.</span></span> <span data-ttu-id="59f14-150">Les jeux d’enregistrements sont identifiés par leur type et leur nom, ainsi que la zone et le groupe de ressources où ils sont présents.</span><span class="sxs-lookup"><span data-stu-id="59f14-150">RecordSets are identified by their type, name, and the zone and resource group they exist in.</span></span> <span data-ttu-id="59f14-151">Les zones sont identifiées par leur nom et le groupe de ressources dans lequel elles sont présentes.</span><span class="sxs-lookup"><span data-stu-id="59f14-151">Zones are identified by their name and the resource group they exist in.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a><span data-ttu-id="59f14-152">Mettre à jour un jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="59f14-152">Update an existing record set</span></span>

<span data-ttu-id="59f14-153">Pour mettre à jour un jeu d’enregistrements DNS, récupérez d’abord le jeu d’enregistrements, puis mettez à jour son contenu et soumettez la modification.</span><span class="sxs-lookup"><span data-stu-id="59f14-153">To update an existing DNS record set, first retrieve the record set, then update the record set contents, then submit the change.</span></span>  <span data-ttu-id="59f14-154">Dans cet exemple, nous spécifions l’Etag du jeu d’enregistrements récupéré dans le paramètre If-Match.</span><span class="sxs-lookup"><span data-stu-id="59f14-154">In this example, we specify the 'Etag' from the retrieved record set in the 'If-Match' parameter.</span></span> <span data-ttu-id="59f14-155">L’appel échoue si une opération simultanée a modifié le jeu d’enregistrements entre-temps.</span><span class="sxs-lookup"><span data-stu-id="59f14-155">The call fails if a concurrent operation has modified the record set in the meantime.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record to the local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update the record set in Azure DNS
// Note: ETAG check specified, update will be rejected if the record set has changed in the meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a><span data-ttu-id="59f14-156">Répertorier les zones et les jeux d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="59f14-156">List zones and record sets</span></span>

<span data-ttu-id="59f14-157">Pour répertorier les zones, utilisez les méthodes *DnsManagementClient.Zones.List...*, qui prennent en charge l’énumération de toutes les zones d’un groupe de ressources donné ou toutes les zones d’un abonnement Azure donné (parmi les groupes de ressources). Pour répertorier les jeux d’enregistrements, utilisez les méthodes *DnsManagementClient.RecordSets.List...*, qui prennent en charge l’énumération de tous les jeux d’enregistrements d’une zone donnée ou uniquement les jeux d’enregistrements d’un type spécifique.</span><span class="sxs-lookup"><span data-stu-id="59f14-157">To list zones, use the *DnsManagementClient.Zones.List...* methods, which support listing either all zones in a given resource group or all zones in a given Azure subscription (across resource groups.) To list record sets, use *DnsManagementClient.RecordSets.List...* methods, which support either listing all record sets in a given zone or only those record sets of a specific type.</span></span>

<span data-ttu-id="59f14-158">Notez que les résultats peuvent être paginés lors du répertoriage des zones et des jeux d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="59f14-158">Note when listing zones and record sets that results may be paginated.</span></span>  <span data-ttu-id="59f14-159">L’exemple suivant montre comment effectuer une itération dans les pages de résultats.</span><span class="sxs-lookup"><span data-stu-id="59f14-159">The following example shows how to iterate through the pages of results.</span></span> <span data-ttu-id="59f14-160">(Une taille de page artificiellement petite de « 2 » est utilisée pour forcer la pagination. Dans la pratique, ce paramètre doit être omis et la taille de page par défaut doit être utilisée.)</span><span class="sxs-lookup"><span data-stu-id="59f14-160">(An artificially small page size of '2' is used to force paging; in practice this parameter should be omitted and the default page size used.)</span></span>

```cs
// Note: in this demo, we'll use a very small page size (2 record sets) to demonstrate paging
// In practice, to improve performance you would use a large page size or just use the system default
int recordSets = 0;
var page = await dnsClient.RecordSets.ListAllInResourceGroupAsync(resourceGroupName, zoneName, "2");
recordSets += page.Count();

while (page.NextPageLink != null)
{
    page = await dnsClient.RecordSets.ListAllInResourceGroupNextAsync(page.NextPageLink);
    recordSets += page.Count();
}
```

## <a name="next-steps"></a><span data-ttu-id="59f14-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="59f14-161">Next steps</span></span>

<span data-ttu-id="59f14-162">Téléchargez l’[exemple de projet de SDK Azure .NET DNS](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), qui inclut d’autres exemples d’utilisation du SDK Azure DNS .NET, notamment des exemples d’autres types d’enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="59f14-162">Download the [Azure DNS .NET SDK sample project](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), which includes further examples of how to use the Azure DNS .NET SDK, including examples for other DNS record types.</span></span>
