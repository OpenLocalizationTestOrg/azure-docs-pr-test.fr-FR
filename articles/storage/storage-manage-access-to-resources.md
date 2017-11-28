---
title: "accès en lecture aaaEnable public pour les conteneurs et objets BLOB dans le stockage Blob Azure | Documents Microsoft"
description: "Découvrez comment toomake conteneurs et objets BLOB disponibles pour l’accès anonyme et comment tooaccess les par programme."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a2cffee6-3224-4f2a-8183-66ca23b2d2d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: marsma
ms.openlocfilehash: 0675b5dc4d32a3a0a34376ae4c049542b07ba03a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-anonymous-read-access-toocontainers-and-blobs"></a><span data-ttu-id="ae4aa-103">Gérer les objets BLOB et l’accès en lecture anonyme toocontainers</span><span class="sxs-lookup"><span data-stu-id="ae4aa-103">Manage anonymous read access toocontainers and blobs</span></span>
<span data-ttu-id="ae4aa-104">Vous pouvez activer un accès en lecture public anonyme tooa conteneur et ses objets BLOB dans le stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-104">You can enable anonymous, public read access tooa container and its blobs in Azure Blob storage.</span></span> <span data-ttu-id="ae4aa-105">En procédant ainsi, vous pouvez accorder des ressources de toothese accès en lecture seule sans partager votre clé de compte et sans nécessiter une signature d’accès partagé (SAS).</span><span class="sxs-lookup"><span data-stu-id="ae4aa-105">By doing so, you can grant read-only access toothese resources without sharing your account key, and without requiring a shared access signature (SAS).</span></span>

<span data-ttu-id="ae4aa-106">Accès en lecture public est idéal pour les scénarios où vous souhaitez que certains objets BLOB tooalways être disponibles pour l’accès en lecture anonyme.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-106">Public read access is best for scenarios where you want certain blobs tooalways be available for anonymous read access.</span></span> <span data-ttu-id="ae4aa-107">Pour un contrôle plus précis, vous pouvez créer une signature d’accès partagé.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-107">For more fine-grained control, you can create a shared access signature.</span></span> <span data-ttu-id="ae4aa-108">Signatures d’accès partagé activer tooprovide restreint l’accès à l’aide des autorisations différentes pour une période spécifique.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-108">Shared access signatures enable you tooprovide restricted access using different permissions, for a specific time period.</span></span> <span data-ttu-id="ae4aa-109">Pour plus d’informations sur la création de signatures d’accès partagé, consultez [Utilisation des signatures d’accès partagé (SAP) dans le Stockage Azure](storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="ae4aa-109">For more information about creating shared access signatures, see [Using shared access signatures (SAS) in Azure Storage](storage-dotnet-shared-access-signature-part-1.md).</span></span>

## <a name="grant-anonymous-users-permissions-toocontainers-and-blobs"></a><span data-ttu-id="ae4aa-110">Accorder aux utilisateurs anonymes des autorisations toocontainers et les objets BLOB</span><span class="sxs-lookup"><span data-stu-id="ae4aa-110">Grant anonymous users permissions toocontainers and blobs</span></span>
<span data-ttu-id="ae4aa-111">Par défaut, un conteneur et tous les objets BLOB qu’il contient sont accessibles uniquement par le propriétaire de hello hello du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-111">By default, a container and any blobs within it may be accessed only by hello owner of hello storage account.</span></span> <span data-ttu-id="ae4aa-112">conteneur de tooa toogive les utilisateurs anonymes des autorisations lecture et ses objets BLOB, vous pouvez définir des autorisations hello conteneur tooallow un accès public.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-112">toogive anonymous users read permissions tooa container and its blobs, you can set hello container permissions tooallow public access.</span></span> <span data-ttu-id="ae4aa-113">Utilisateurs anonymes peuvent lire des objets BLOB dans un conteneur accessible publiquement sans authentifier la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-113">Anonymous users can read blobs within a publicly accessible container without authenticating hello request.</span></span>

<span data-ttu-id="ae4aa-114">Vous pouvez configurer un conteneur avec hello les autorisations suivantes :</span><span class="sxs-lookup"><span data-stu-id="ae4aa-114">You can configure a container with hello following permissions:</span></span>

* <span data-ttu-id="ae4aa-115">**Accès en lecture sans public :** conteneur de hello et ses objets BLOB sont accessibles uniquement par le propriétaire du compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-115">**No public read access:** hello container and its blobs can be accessed only by hello storage account owner.</span></span> <span data-ttu-id="ae4aa-116">Il s’agit par défaut de hello pour tous les conteneurs de nouveau.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-116">This is hello default for all new containers.</span></span>
* <span data-ttu-id="ae4aa-117">**Pour les objets BLOB uniquement l’accès en lecture public :** BLOB conteneur hello peuvent être lus par une demande anonyme, mais les données de conteneur ne seront pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-117">**Public read access for blobs only:** Blobs within hello container can be read by anonymous request, but container data is not available.</span></span> <span data-ttu-id="ae4aa-118">Les clients anonymes ne peuvent pas énumérer les objets BLOB hello conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-118">Anonymous clients cannot enumerate hello blobs within hello container.</span></span>
* <span data-ttu-id="ae4aa-119">**Accès en lecture public total :** toutes les données du conteneur et des objets blob peuvent être lues par une demande anonyme.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-119">**Full public read access:** All container and blob data can be read by anonymous request.</span></span> <span data-ttu-id="ae4aa-120">Les clients peuvent énumérer les objets BLOB dans le conteneur de hello par une demande anonyme, mais ne peut pas énumérer des conteneurs dans le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-120">Clients can enumerate blobs within hello container by anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="ae4aa-121">Vous pouvez utiliser hello tooset conteneur autorisations suivantes :</span><span class="sxs-lookup"><span data-stu-id="ae4aa-121">You can use hello following tooset container permissions:</span></span>

* [<span data-ttu-id="ae4aa-122">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="ae4aa-122">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="ae4aa-123">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae4aa-123">Azure PowerShell</span></span>](storage-powershell-guide-full.md#how-to-manage-azure-blobs)
* [<span data-ttu-id="ae4aa-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ae4aa-124">Azure CLI 2.0</span></span>](storage-azure-cli.md#create-and-manage-blobs)
* <span data-ttu-id="ae4aa-125">Par programme, en utilisant l’une des bibliothèques clientes de stockage hello ou hello API REST</span><span class="sxs-lookup"><span data-stu-id="ae4aa-125">Programmatically, by using one of hello storage client libraries or hello REST API</span></span>

### <a name="set-container-permissions-in-hello-azure-portal"></a><span data-ttu-id="ae4aa-126">Définir les autorisations du conteneur dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="ae4aa-126">Set container permissions in hello Azure portal</span></span>
<span data-ttu-id="ae4aa-127">autorisations du conteneur tooset Bonjour [portail Azure](https://portal.azure.com), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ae4aa-127">tooset container permissions in hello [Azure portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="ae4aa-128">Ouvrez votre **compte de stockage** panneau dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-128">Open your **Storage account** blade in hello portal.</span></span> <span data-ttu-id="ae4aa-129">Vous pouvez trouver votre compte de stockage en sélectionnant **comptes de stockage** dans le panneau de menus du portail principal hello.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-129">You can find your storage account by selecting **Storage accounts** in hello main portal menu blade.</span></span>
1. <span data-ttu-id="ae4aa-130">Sous **SERVICE BLOB** dans le panneau de menu hello, sélectionnez **conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-130">Under **BLOB SERVICE** on hello menu blade, select **Containers**.</span></span>
1. <span data-ttu-id="ae4aa-131">Avec le bouton droit sur la ligne du conteneur hello ou du conteneur hello hello Sélectionnez points de suspension tooopen **menu contextuel**.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-131">Right-click on hello container row or select hello ellipsis tooopen hello container's **Context menu**.</span></span>
1. <span data-ttu-id="ae4aa-132">Sélectionnez **stratégie d’accès** dans le menu contextuel de hello.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-132">Select **Access policy** in hello context menu.</span></span>
1. <span data-ttu-id="ae4aa-133">Sélectionnez un **type d’accès** de hello menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-133">Select an **Access type** from hello drop down menu.</span></span>

    ![Boîte de dialogue Modifier les métadonnées du conteneur](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a><span data-ttu-id="ae4aa-135">Définir des autorisations de conteneur avec .NET</span><span class="sxs-lookup"><span data-stu-id="ae4aa-135">Set container permissions with .NET</span></span>
<span data-ttu-id="ae4aa-136">autorisations tooset pour un conteneur à l’aide de c# et hello bibliothèque cliente de stockage pour .NET, tout d’abord extraire les autorisations existantes du conteneur hello en appelant hello **GetPermissions** (méthode).</span><span class="sxs-lookup"><span data-stu-id="ae4aa-136">tooset permissions for a container using C# and hello Storage Client Library for .NET, first retrieve hello container's existing permissions by calling hello **GetPermissions** method.</span></span> <span data-ttu-id="ae4aa-137">Puis ensemble hello **PublicAccess** propriété hello **BlobContainerPermissions** objet qui est retourné par hello **GetPermissions** (méthode).</span><span class="sxs-lookup"><span data-stu-id="ae4aa-137">Then set hello **PublicAccess** property for hello **BlobContainerPermissions** object that is returned by hello **GetPermissions** method.</span></span> <span data-ttu-id="ae4aa-138">Enfin, appelez hello **SetPermissions** méthode avec hello mis à jour les autorisations.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-138">Finally, call hello **SetPermissions** method with hello updated permissions.</span></span>

<span data-ttu-id="ae4aa-139">Hello, l’exemple suivant définit les autorisations du conteneur hello toofull un accès en lecture public.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-139">hello following example sets hello container's permissions toofull public read access.</span></span> <span data-ttu-id="ae4aa-140">tooset autorisations toopublic l’accès en lecture pour les objets BLOB uniquement, définissez hello **PublicAccess** propriété trop**BlobContainerPublicAccessType.Blob**.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-140">tooset permissions toopublic read access for blobs only, set hello **PublicAccess** property too**BlobContainerPublicAccessType.Blob**.</span></span> <span data-ttu-id="ae4aa-141">valeur de toutes les autorisations pour les utilisateurs anonymes, tooremove hello propriété trop**BlobContainerPublicAccessType.Off**.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-141">tooremove all permissions for anonymous users, set hello property too**BlobContainerPublicAccessType.Off**.</span></span>

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a><span data-ttu-id="ae4aa-142">Accéder anonymement aux conteneurs et aux objets Blob</span><span class="sxs-lookup"><span data-stu-id="ae4aa-142">Access containers and blobs anonymously</span></span>
<span data-ttu-id="ae4aa-143">Un client ayant un accès anonyme aux conteneurs et aux objets Blob peut utiliser des constructeurs qui ne nécessitent pas d’informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-143">A client that accesses containers and blobs anonymously can use constructors that do not require credentials.</span></span> <span data-ttu-id="ae4aa-144">Hello suivant exemples montrent différentes manières de ressources du service Blob tooreference anonymement.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-144">hello following examples show a few different ways tooreference Blob service resources anonymously.</span></span>

### <a name="create-an-anonymous-client-object"></a><span data-ttu-id="ae4aa-145">Créer un objet de client anonyme</span><span class="sxs-lookup"><span data-stu-id="ae4aa-145">Create an anonymous client object</span></span>
<span data-ttu-id="ae4aa-146">Vous pouvez créer un nouvel objet de service client pour l’accès anonyme en fournissant un point de terminaison de service hello Blob pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-146">You can create a new service client object for anonymous access by providing hello Blob service endpoint for hello account.</span></span> <span data-ttu-id="ae4aa-147">Toutefois, vous devez également connaître nom hello d’un conteneur dans ce compte n’est disponible pour l’accès anonyme.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-147">However, you must also know hello name of a container in that account that's available for anonymous access.</span></span>

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create hello client object using hello Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read hello container's properties. Note this is only possible when hello container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a><span data-ttu-id="ae4aa-148">Référencer un conteneur de manière anonyme</span><span class="sxs-lookup"><span data-stu-id="ae4aa-148">Reference a container anonymously</span></span>
<span data-ttu-id="ae4aa-149">Si vous avez hello URL tooa conteneur qui est disponible de manière anonyme, vous pouvez utiliser il tooreference hello conteneur directement.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-149">If you have hello URL tooa container that is anonymously available, you can use it tooreference hello container directly.</span></span>

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in hello container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a><span data-ttu-id="ae4aa-150">Référencer un objet Blob de façon anonyme</span><span class="sxs-lookup"><span data-stu-id="ae4aa-150">Reference a blob anonymously</span></span>
<span data-ttu-id="ae4aa-151">Si vous avez hello URL tooa blob qui est disponible pour l’accès anonyme, vous pouvez référencer des blob hello directement à l’aide de cette URL :</span><span class="sxs-lookup"><span data-stu-id="ae4aa-151">If you have hello URL tooa blob that is available for anonymous access, you can reference hello blob directly using that URL:</span></span>

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-tooanonymous-users"></a><span data-ttu-id="ae4aa-152">Utilisateurs de fonctionnalités disponible tooanonymous</span><span class="sxs-lookup"><span data-stu-id="ae4aa-152">Features available tooanonymous users</span></span>
<span data-ttu-id="ae4aa-153">Hello tableau suivant montre les opérations pouvant être appelées par des utilisateurs anonymes lorsque les ACL d’un conteneur a tooallow un accès public.</span><span class="sxs-lookup"><span data-stu-id="ae4aa-153">hello following table shows which operations may be called by anonymous users when a container's ACL is set tooallow public access.</span></span>

| <span data-ttu-id="ae4aa-154">Opération REST</span><span class="sxs-lookup"><span data-stu-id="ae4aa-154">REST Operation</span></span> | <span data-ttu-id="ae4aa-155">Autorisation avec accès en lecture public complet</span><span class="sxs-lookup"><span data-stu-id="ae4aa-155">Permission with full public read access</span></span> | <span data-ttu-id="ae4aa-156">Autorisation avec accès en lecture public pour les objets blob uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-156">Permission with public read access for blobs only</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ae4aa-157">List Containers</span><span class="sxs-lookup"><span data-stu-id="ae4aa-157">List Containers</span></span> |<span data-ttu-id="ae4aa-158">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-158">Owner only</span></span> |<span data-ttu-id="ae4aa-159">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-159">Owner only</span></span> |
| <span data-ttu-id="ae4aa-160">Create Container</span><span class="sxs-lookup"><span data-stu-id="ae4aa-160">Create Container</span></span> |<span data-ttu-id="ae4aa-161">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-161">Owner only</span></span> |<span data-ttu-id="ae4aa-162">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-162">Owner only</span></span> |
| <span data-ttu-id="ae4aa-163">Get Container Properties</span><span class="sxs-lookup"><span data-stu-id="ae4aa-163">Get Container Properties</span></span> |<span data-ttu-id="ae4aa-164">Tout</span><span class="sxs-lookup"><span data-stu-id="ae4aa-164">All</span></span> |<span data-ttu-id="ae4aa-165">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-165">Owner only</span></span> |
| <span data-ttu-id="ae4aa-166">Get Container Metadata</span><span class="sxs-lookup"><span data-stu-id="ae4aa-166">Get Container Metadata</span></span> |<span data-ttu-id="ae4aa-167">Tout</span><span class="sxs-lookup"><span data-stu-id="ae4aa-167">All</span></span> |<span data-ttu-id="ae4aa-168">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-168">Owner only</span></span> |
| <span data-ttu-id="ae4aa-169">Set Container Metadata</span><span class="sxs-lookup"><span data-stu-id="ae4aa-169">Set Container Metadata</span></span> |<span data-ttu-id="ae4aa-170">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-170">Owner only</span></span> |<span data-ttu-id="ae4aa-171">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-171">Owner only</span></span> |
| <span data-ttu-id="ae4aa-172">Get Container ACL</span><span class="sxs-lookup"><span data-stu-id="ae4aa-172">Get Container ACL</span></span> |<span data-ttu-id="ae4aa-173">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-173">Owner only</span></span> |<span data-ttu-id="ae4aa-174">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-174">Owner only</span></span> |
| <span data-ttu-id="ae4aa-175">Set Container ACL</span><span class="sxs-lookup"><span data-stu-id="ae4aa-175">Set Container ACL</span></span> |<span data-ttu-id="ae4aa-176">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-176">Owner only</span></span> |<span data-ttu-id="ae4aa-177">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-177">Owner only</span></span> |
| <span data-ttu-id="ae4aa-178">Delete Container</span><span class="sxs-lookup"><span data-stu-id="ae4aa-178">Delete Container</span></span> |<span data-ttu-id="ae4aa-179">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-179">Owner only</span></span> |<span data-ttu-id="ae4aa-180">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-180">Owner only</span></span> |
| <span data-ttu-id="ae4aa-181">List Blobs</span><span class="sxs-lookup"><span data-stu-id="ae4aa-181">List Blobs</span></span> |<span data-ttu-id="ae4aa-182">Tout</span><span class="sxs-lookup"><span data-stu-id="ae4aa-182">All</span></span> |<span data-ttu-id="ae4aa-183">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-183">Owner only</span></span> |
| <span data-ttu-id="ae4aa-184">Put Blob</span><span class="sxs-lookup"><span data-stu-id="ae4aa-184">Put Blob</span></span> |<span data-ttu-id="ae4aa-185">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-185">Owner only</span></span> |<span data-ttu-id="ae4aa-186">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-186">Owner only</span></span> |
| <span data-ttu-id="ae4aa-187">Get Blob</span><span class="sxs-lookup"><span data-stu-id="ae4aa-187">Get Blob</span></span> |<span data-ttu-id="ae4aa-188">Tout</span><span class="sxs-lookup"><span data-stu-id="ae4aa-188">All</span></span> |<span data-ttu-id="ae4aa-189">Tout</span><span class="sxs-lookup"><span data-stu-id="ae4aa-189">All</span></span> |
| <span data-ttu-id="ae4aa-190">Get Blob Properties</span><span class="sxs-lookup"><span data-stu-id="ae4aa-190">Get Blob Properties</span></span> |<span data-ttu-id="ae4aa-191">Tout</span><span class="sxs-lookup"><span data-stu-id="ae4aa-191">All</span></span> |<span data-ttu-id="ae4aa-192">Tout</span><span class="sxs-lookup"><span data-stu-id="ae4aa-192">All</span></span> |
| <span data-ttu-id="ae4aa-193">Set Blob Properties</span><span class="sxs-lookup"><span data-stu-id="ae4aa-193">Set Blob Properties</span></span> |<span data-ttu-id="ae4aa-194">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-194">Owner only</span></span> |<span data-ttu-id="ae4aa-195">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-195">Owner only</span></span> |
| <span data-ttu-id="ae4aa-196">Get Blob Metadata</span><span class="sxs-lookup"><span data-stu-id="ae4aa-196">Get Blob Metadata</span></span> |<span data-ttu-id="ae4aa-197">Tout</span><span class="sxs-lookup"><span data-stu-id="ae4aa-197">All</span></span> |<span data-ttu-id="ae4aa-198">Tout</span><span class="sxs-lookup"><span data-stu-id="ae4aa-198">All</span></span> |
| <span data-ttu-id="ae4aa-199">Set Blob Metadata</span><span class="sxs-lookup"><span data-stu-id="ae4aa-199">Set Blob Metadata</span></span> |<span data-ttu-id="ae4aa-200">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-200">Owner only</span></span> |<span data-ttu-id="ae4aa-201">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-201">Owner only</span></span> |
| <span data-ttu-id="ae4aa-202">Put Block</span><span class="sxs-lookup"><span data-stu-id="ae4aa-202">Put Block</span></span> |<span data-ttu-id="ae4aa-203">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-203">Owner only</span></span> |<span data-ttu-id="ae4aa-204">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-204">Owner only</span></span> |
| <span data-ttu-id="ae4aa-205">Get Block List (blocs validés uniquement)</span><span class="sxs-lookup"><span data-stu-id="ae4aa-205">Get Block List (committed blocks only)</span></span> |<span data-ttu-id="ae4aa-206">Tout</span><span class="sxs-lookup"><span data-stu-id="ae4aa-206">All</span></span> |<span data-ttu-id="ae4aa-207">Tout</span><span class="sxs-lookup"><span data-stu-id="ae4aa-207">All</span></span> |
| <span data-ttu-id="ae4aa-208">Get Block List (blocs non validés uniquement ou tous les blocs)</span><span class="sxs-lookup"><span data-stu-id="ae4aa-208">Get Block List (uncommitted blocks only or all blocks)</span></span> |<span data-ttu-id="ae4aa-209">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-209">Owner only</span></span> |<span data-ttu-id="ae4aa-210">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-210">Owner only</span></span> |
| <span data-ttu-id="ae4aa-211">Put Block List</span><span class="sxs-lookup"><span data-stu-id="ae4aa-211">Put Block List</span></span> |<span data-ttu-id="ae4aa-212">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-212">Owner only</span></span> |<span data-ttu-id="ae4aa-213">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-213">Owner only</span></span> |
| <span data-ttu-id="ae4aa-214">Delete Blob</span><span class="sxs-lookup"><span data-stu-id="ae4aa-214">Delete Blob</span></span> |<span data-ttu-id="ae4aa-215">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-215">Owner only</span></span> |<span data-ttu-id="ae4aa-216">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-216">Owner only</span></span> |
| <span data-ttu-id="ae4aa-217">Copie d'un objet blob</span><span class="sxs-lookup"><span data-stu-id="ae4aa-217">Copy Blob</span></span> |<span data-ttu-id="ae4aa-218">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-218">Owner only</span></span> |<span data-ttu-id="ae4aa-219">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-219">Owner only</span></span> |
| <span data-ttu-id="ae4aa-220">Snapshot Blob</span><span class="sxs-lookup"><span data-stu-id="ae4aa-220">Snapshot Blob</span></span> |<span data-ttu-id="ae4aa-221">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-221">Owner only</span></span> |<span data-ttu-id="ae4aa-222">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-222">Owner only</span></span> |
| <span data-ttu-id="ae4aa-223">Lease Blob</span><span class="sxs-lookup"><span data-stu-id="ae4aa-223">Lease Blob</span></span> |<span data-ttu-id="ae4aa-224">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-224">Owner only</span></span> |<span data-ttu-id="ae4aa-225">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-225">Owner only</span></span> |
| <span data-ttu-id="ae4aa-226">Put Page</span><span class="sxs-lookup"><span data-stu-id="ae4aa-226">Put Page</span></span> |<span data-ttu-id="ae4aa-227">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-227">Owner only</span></span> |<span data-ttu-id="ae4aa-228">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-228">Owner only</span></span> |
| <span data-ttu-id="ae4aa-229">Get Page Ranges</span><span class="sxs-lookup"><span data-stu-id="ae4aa-229">Get Page Ranges</span></span> |<span data-ttu-id="ae4aa-230">Tout</span><span class="sxs-lookup"><span data-stu-id="ae4aa-230">All</span></span> |<span data-ttu-id="ae4aa-231">Tout</span><span class="sxs-lookup"><span data-stu-id="ae4aa-231">All</span></span> |
| <span data-ttu-id="ae4aa-232">Append Blob</span><span class="sxs-lookup"><span data-stu-id="ae4aa-232">Append Blob</span></span> |<span data-ttu-id="ae4aa-233">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-233">Owner only</span></span> |<span data-ttu-id="ae4aa-234">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="ae4aa-234">Owner only</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ae4aa-235">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ae4aa-235">Next steps</span></span>

* [<span data-ttu-id="ae4aa-236">Authentification pour hello Services de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="ae4aa-236">Authentication for hello Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [<span data-ttu-id="ae4aa-237">Utilisation des signatures d’accès partagé (SAP)</span><span class="sxs-lookup"><span data-stu-id="ae4aa-237">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="ae4aa-238">Délégation de l'accès avec une signature d'accès partagé</span><span class="sxs-lookup"><span data-stu-id="ae4aa-238">Delegating Access with a Shared Access Signature</span></span>](https://msdn.microsoft.com/library/azure/ee395415.aspx)
