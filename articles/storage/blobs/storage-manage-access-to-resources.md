---
title: "Activer l’accès en lecture public pour les conteneurs et les objets blob dans Stockage Blob Azure | Microsoft Docs"
description: "Découvrez comment autoriser l’accès anonyme aux conteneurs et aux objets Blob et comment utiliser un programme pour y accéder."
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
ms.openlocfilehash: 8d4f4c7c208baf0db6155eb78a53e37c4ec1e023
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-anonymous-read-access-to-containers-and-blobs"></a><span data-ttu-id="43c94-103">Gestion de l’accès en lecture anonyme aux conteneurs et aux objets blob</span><span class="sxs-lookup"><span data-stu-id="43c94-103">Manage anonymous read access to containers and blobs</span></span>
<span data-ttu-id="43c94-104">Vous pouvez activer l’accès en lecture anonyme public pour un conteneur et ses objets blob dans Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="43c94-104">You can enable anonymous, public read access to a container and its blobs in Azure Blob storage.</span></span> <span data-ttu-id="43c94-105">En procédant ainsi, vous pouvez accorder un accès en lecture seule à ces ressources sans partager votre clé de compte et sans exiger de signature d’accès partagé (SAP).</span><span class="sxs-lookup"><span data-stu-id="43c94-105">By doing so, you can grant read-only access to these resources without sharing your account key, and without requiring a shared access signature (SAS).</span></span>

<span data-ttu-id="43c94-106">L’accès en lecture public est idéal dans les situations où vous voulez conférer à certains objets blob un accès en lecture anonyme permanent.</span><span class="sxs-lookup"><span data-stu-id="43c94-106">Public read access is best for scenarios where you want certain blobs to always be available for anonymous read access.</span></span> <span data-ttu-id="43c94-107">Pour un contrôle plus précis, vous pouvez créer une signature d’accès partagé.</span><span class="sxs-lookup"><span data-stu-id="43c94-107">For more fine-grained control, you can create a shared access signature.</span></span> <span data-ttu-id="43c94-108">Les signatures d’accès partagé vous permettent d’accorder un accès restreint avec différentes autorisations sur une période donnée.</span><span class="sxs-lookup"><span data-stu-id="43c94-108">Shared access signatures enable you to provide restricted access using different permissions, for a specific time period.</span></span> <span data-ttu-id="43c94-109">Pour plus d’informations sur la création de signatures d’accès partagé, consultez [Utilisation des signatures d’accès partagé (SAP) dans le Stockage Azure](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="43c94-109">For more information about creating shared access signatures, see [Using shared access signatures (SAS) in Azure Storage](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="grant-anonymous-users-permissions-to-containers-and-blobs"></a><span data-ttu-id="43c94-110">Accorder à des utilisateurs anonymes des autorisations d’accès aux conteneurs et objets blob</span><span class="sxs-lookup"><span data-stu-id="43c94-110">Grant anonymous users permissions to containers and blobs</span></span>
<span data-ttu-id="43c94-111">Par défaut, un conteneur et tous les objets blob qu'il contient sont accessibles uniquement par le propriétaire du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="43c94-111">By default, a container and any blobs within it may be accessed only by the owner of the storage account.</span></span> <span data-ttu-id="43c94-112">Pour fournir aux utilisateurs anonymes des autorisations de lecture sur un conteneur et ses objets blob, vous pouvez configurer les autorisations du conteneur afin d’autoriser l’accès public.</span><span class="sxs-lookup"><span data-stu-id="43c94-112">To give anonymous users read permissions to a container and its blobs, you can set the container permissions to allow public access.</span></span> <span data-ttu-id="43c94-113">Les utilisateurs anonymes peuvent lire les objets blob d’un conteneur accessible publiquement sans avoir à authentifier la demande.</span><span class="sxs-lookup"><span data-stu-id="43c94-113">Anonymous users can read blobs within a publicly accessible container without authenticating the request.</span></span>

<span data-ttu-id="43c94-114">Vous pouvez configurer un conteneur avec les autorisations suivantes :</span><span class="sxs-lookup"><span data-stu-id="43c94-114">You can configure a container with the following permissions:</span></span>

* <span data-ttu-id="43c94-115">**No public read access (Aucun accès en lecture public) :** seul le propriétaire du compte de stockage peut accéder au conteneur et à ses objets blob.</span><span class="sxs-lookup"><span data-stu-id="43c94-115">**No public read access:** The container and its blobs can be accessed only by the storage account owner.</span></span> <span data-ttu-id="43c94-116">Il s’agit de la configuration par défaut de tous les nouveaux conteneurs.</span><span class="sxs-lookup"><span data-stu-id="43c94-116">This is the default for all new containers.</span></span>
* <span data-ttu-id="43c94-117">**Accès en lecture public pour les objets blobs uniquement :** les objets blob présents dans le conteneur peuvent être lus par une demande anonyme, mais les données du conteneur ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="43c94-117">**Public read access for blobs only:** Blobs within the container can be read by anonymous request, but container data is not available.</span></span> <span data-ttu-id="43c94-118">Les clients anonymes ne peuvent pas énumérer les objets blob présents dans le conteneur.</span><span class="sxs-lookup"><span data-stu-id="43c94-118">Anonymous clients cannot enumerate the blobs within the container.</span></span>
* <span data-ttu-id="43c94-119">**Accès en lecture public total :** toutes les données du conteneur et des objets blob peuvent être lues par une demande anonyme.</span><span class="sxs-lookup"><span data-stu-id="43c94-119">**Full public read access:** All container and blob data can be read by anonymous request.</span></span> <span data-ttu-id="43c94-120">Les clients peuvent énumérer les objets blob présents dans le conteneur par une demande anonyme, mais ne peuvent pas énumérer les conteneurs présents dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="43c94-120">Clients can enumerate blobs within the container by anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="43c94-121">Vous pouvez définir les autorisations de conteneur par les moyens suivants :</span><span class="sxs-lookup"><span data-stu-id="43c94-121">You can use the following to set container permissions:</span></span>

* [<span data-ttu-id="43c94-122">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="43c94-122">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="43c94-123">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="43c94-123">Azure PowerShell</span></span>](../common/storage-powershell-guide-full.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#how-to-manage-azure-blobs)
* [<span data-ttu-id="43c94-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="43c94-124">Azure CLI 2.0</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-and-manage-blobs)
* <span data-ttu-id="43c94-125">Par programmation, en utilisant l’une des bibliothèques clientes de stockage ou l’API REST</span><span class="sxs-lookup"><span data-stu-id="43c94-125">Programmatically, by using one of the storage client libraries or the REST API</span></span>

### <a name="set-container-permissions-in-the-azure-portal"></a><span data-ttu-id="43c94-126">Définir des autorisations de conteneur dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="43c94-126">Set container permissions in the Azure portal</span></span>
<span data-ttu-id="43c94-127">Pour définir des autorisations de conteneur dans le [portail Azure](https://portal.azure.com), effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="43c94-127">To set container permissions in the [Azure portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="43c94-128">Ouvrez le panneau de votre **Compte de stockage** dans le portail.</span><span class="sxs-lookup"><span data-stu-id="43c94-128">Open your **Storage account** blade in the portal.</span></span> <span data-ttu-id="43c94-129">Vous pouvez trouver votre compte de stockage en sélectionnant **Comptes de stockage** dans le panneau de menu principal du portail.</span><span class="sxs-lookup"><span data-stu-id="43c94-129">You can find your storage account by selecting **Storage accounts** in the main portal menu blade.</span></span>
1. <span data-ttu-id="43c94-130">Sous l’élément **SERVICE BLOB** du panneau de menu, sélectionnez **Conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="43c94-130">Under **BLOB SERVICE** on the menu blade, select **Containers**.</span></span>
1. <span data-ttu-id="43c94-131">Cliquez avec le bouton droit sur la ligne du conteneur ou sélectionnez les points de suspension pour ouvrir le **menu contextuel** du conteneur.</span><span class="sxs-lookup"><span data-stu-id="43c94-131">Right-click on the container row or select the ellipsis to open the container's **Context menu**.</span></span>
1. <span data-ttu-id="43c94-132">Sélectionnez **Stratégie d’accès** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="43c94-132">Select **Access policy** in the context menu.</span></span>
1. <span data-ttu-id="43c94-133">Sélectionnez un **type d’accès** dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="43c94-133">Select an **Access type** from the drop down menu.</span></span>

    ![Boîte de dialogue Modifier les métadonnées du conteneur](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a><span data-ttu-id="43c94-135">Définir des autorisations de conteneur avec .NET</span><span class="sxs-lookup"><span data-stu-id="43c94-135">Set container permissions with .NET</span></span>
<span data-ttu-id="43c94-136">Pour définir les autorisations d’un conteneur en utilisant C# et la bibliothèque cliente de stockage pour .NET, vous devez d’abord récupérer les autorisations existantes du conteneur en appelant la méthode **GetPermissions**.</span><span class="sxs-lookup"><span data-stu-id="43c94-136">To set permissions for a container using C# and the Storage Client Library for .NET, first retrieve the container's existing permissions by calling the **GetPermissions** method.</span></span> <span data-ttu-id="43c94-137">Définissez ensuite la propriété **PublicAccess** de l’objet **BlobContainerPermissions** qui est retourné par la méthode **GetPermissions**.</span><span class="sxs-lookup"><span data-stu-id="43c94-137">Then set the **PublicAccess** property for the **BlobContainerPermissions** object that is returned by the **GetPermissions** method.</span></span> <span data-ttu-id="43c94-138">Pour finir, appelez la méthode **SetPermissions** avec les autorisations mises à jour.</span><span class="sxs-lookup"><span data-stu-id="43c94-138">Finally, call the **SetPermissions** method with the updated permissions.</span></span>

<span data-ttu-id="43c94-139">Dans l’exemple suivant, nous définissons les autorisations du conteneur pour permettre un accès en lecture public complet.</span><span class="sxs-lookup"><span data-stu-id="43c94-139">The following example sets the container's permissions to full public read access.</span></span> <span data-ttu-id="43c94-140">Pour autoriser un accès en lecture public pour les objets Blob uniquement, définissez la propriété **PublicAccess** sur **BlobContainerPublicAccessType.Blob**.</span><span class="sxs-lookup"><span data-stu-id="43c94-140">To set permissions to public read access for blobs only, set the **PublicAccess** property to **BlobContainerPublicAccessType.Blob**.</span></span> <span data-ttu-id="43c94-141">Pour supprimer toutes les autorisations pour les utilisateurs anonymes, définissez la propriété sur **BlobContainerPublicAccessType.Off**.</span><span class="sxs-lookup"><span data-stu-id="43c94-141">To remove all permissions for anonymous users, set the property to **BlobContainerPublicAccessType.Off**.</span></span>

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a><span data-ttu-id="43c94-142">Accéder anonymement aux conteneurs et aux objets Blob</span><span class="sxs-lookup"><span data-stu-id="43c94-142">Access containers and blobs anonymously</span></span>
<span data-ttu-id="43c94-143">Un client ayant un accès anonyme aux conteneurs et aux objets Blob peut utiliser des constructeurs qui ne nécessitent pas d’informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="43c94-143">A client that accesses containers and blobs anonymously can use constructors that do not require credentials.</span></span> <span data-ttu-id="43c94-144">Les exemples suivants illustrent différentes manières de référencer des ressources de service Blob de façon anonyme.</span><span class="sxs-lookup"><span data-stu-id="43c94-144">The following examples show a few different ways to reference Blob service resources anonymously.</span></span>

### <a name="create-an-anonymous-client-object"></a><span data-ttu-id="43c94-145">Créer un objet de client anonyme</span><span class="sxs-lookup"><span data-stu-id="43c94-145">Create an anonymous client object</span></span>
<span data-ttu-id="43c94-146">Vous pouvez créer un nouvel objet de client de service pour permettre un accès anonyme en spécifiant le point de terminaison du service Blob associé au compte.</span><span class="sxs-lookup"><span data-stu-id="43c94-146">You can create a new service client object for anonymous access by providing the Blob service endpoint for the account.</span></span> <span data-ttu-id="43c94-147">Toutefois, vous devez également connaître le nom d’un conteneur attaché à ce compte qui est disponible pour un accès anonyme.</span><span class="sxs-lookup"><span data-stu-id="43c94-147">However, you must also know the name of a container in that account that's available for anonymous access.</span></span>

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create the client object using the Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference to a container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read the container's properties. Note this is only possible when the container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a><span data-ttu-id="43c94-148">Référencer un conteneur de manière anonyme</span><span class="sxs-lookup"><span data-stu-id="43c94-148">Reference a container anonymously</span></span>
<span data-ttu-id="43c94-149">Si vous disposez de l’URL permettant d’accéder à un conteneur accessible de manière anonyme, vous pouvez l’utiliser pour référencer directement le conteneur.</span><span class="sxs-lookup"><span data-stu-id="43c94-149">If you have the URL to a container that is anonymously available, you can use it to reference the container directly.</span></span>

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference to a container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in the container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a><span data-ttu-id="43c94-150">Référencer un objet Blob de façon anonyme</span><span class="sxs-lookup"><span data-stu-id="43c94-150">Reference a blob anonymously</span></span>
<span data-ttu-id="43c94-151">Si vous disposez de l’URL permettant d’accéder à un objet Blob accessible de manière anonyme, vous pouvez l’utiliser pour référencer directement l’objet Blob :</span><span class="sxs-lookup"><span data-stu-id="43c94-151">If you have the URL to a blob that is available for anonymous access, you can reference the blob directly using that URL:</span></span>

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-to-anonymous-users"></a><span data-ttu-id="43c94-152">Fonctionnalités accessibles aux utilisateurs anonymes</span><span class="sxs-lookup"><span data-stu-id="43c94-152">Features available to anonymous users</span></span>
<span data-ttu-id="43c94-153">Le tableau suivant indique les opérations pouvant être appelées par les utilisateurs anonymes quand la liste de contrôle d’accès (ACL, Access Control List) est définie pour autoriser l’accès public.</span><span class="sxs-lookup"><span data-stu-id="43c94-153">The following table shows which operations may be called by anonymous users when a container's ACL is set to allow public access.</span></span>

| <span data-ttu-id="43c94-154">Opération REST</span><span class="sxs-lookup"><span data-stu-id="43c94-154">REST Operation</span></span> | <span data-ttu-id="43c94-155">Autorisation avec accès en lecture public complet</span><span class="sxs-lookup"><span data-stu-id="43c94-155">Permission with full public read access</span></span> | <span data-ttu-id="43c94-156">Autorisation avec accès en lecture public pour les objets blob uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-156">Permission with public read access for blobs only</span></span> |
| --- | --- | --- |
| <span data-ttu-id="43c94-157">List Containers</span><span class="sxs-lookup"><span data-stu-id="43c94-157">List Containers</span></span> |<span data-ttu-id="43c94-158">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-158">Owner only</span></span> |<span data-ttu-id="43c94-159">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-159">Owner only</span></span> |
| <span data-ttu-id="43c94-160">Create Container</span><span class="sxs-lookup"><span data-stu-id="43c94-160">Create Container</span></span> |<span data-ttu-id="43c94-161">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-161">Owner only</span></span> |<span data-ttu-id="43c94-162">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-162">Owner only</span></span> |
| <span data-ttu-id="43c94-163">Get Container Properties</span><span class="sxs-lookup"><span data-stu-id="43c94-163">Get Container Properties</span></span> |<span data-ttu-id="43c94-164">Tout</span><span class="sxs-lookup"><span data-stu-id="43c94-164">All</span></span> |<span data-ttu-id="43c94-165">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-165">Owner only</span></span> |
| <span data-ttu-id="43c94-166">Get Container Metadata</span><span class="sxs-lookup"><span data-stu-id="43c94-166">Get Container Metadata</span></span> |<span data-ttu-id="43c94-167">Tout</span><span class="sxs-lookup"><span data-stu-id="43c94-167">All</span></span> |<span data-ttu-id="43c94-168">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-168">Owner only</span></span> |
| <span data-ttu-id="43c94-169">Set Container Metadata</span><span class="sxs-lookup"><span data-stu-id="43c94-169">Set Container Metadata</span></span> |<span data-ttu-id="43c94-170">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-170">Owner only</span></span> |<span data-ttu-id="43c94-171">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-171">Owner only</span></span> |
| <span data-ttu-id="43c94-172">Get Container ACL</span><span class="sxs-lookup"><span data-stu-id="43c94-172">Get Container ACL</span></span> |<span data-ttu-id="43c94-173">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-173">Owner only</span></span> |<span data-ttu-id="43c94-174">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-174">Owner only</span></span> |
| <span data-ttu-id="43c94-175">Set Container ACL</span><span class="sxs-lookup"><span data-stu-id="43c94-175">Set Container ACL</span></span> |<span data-ttu-id="43c94-176">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-176">Owner only</span></span> |<span data-ttu-id="43c94-177">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-177">Owner only</span></span> |
| <span data-ttu-id="43c94-178">Delete Container</span><span class="sxs-lookup"><span data-stu-id="43c94-178">Delete Container</span></span> |<span data-ttu-id="43c94-179">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-179">Owner only</span></span> |<span data-ttu-id="43c94-180">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-180">Owner only</span></span> |
| <span data-ttu-id="43c94-181">List Blobs</span><span class="sxs-lookup"><span data-stu-id="43c94-181">List Blobs</span></span> |<span data-ttu-id="43c94-182">Tout</span><span class="sxs-lookup"><span data-stu-id="43c94-182">All</span></span> |<span data-ttu-id="43c94-183">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-183">Owner only</span></span> |
| <span data-ttu-id="43c94-184">Put Blob</span><span class="sxs-lookup"><span data-stu-id="43c94-184">Put Blob</span></span> |<span data-ttu-id="43c94-185">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-185">Owner only</span></span> |<span data-ttu-id="43c94-186">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-186">Owner only</span></span> |
| <span data-ttu-id="43c94-187">Get Blob</span><span class="sxs-lookup"><span data-stu-id="43c94-187">Get Blob</span></span> |<span data-ttu-id="43c94-188">Tout</span><span class="sxs-lookup"><span data-stu-id="43c94-188">All</span></span> |<span data-ttu-id="43c94-189">Tout</span><span class="sxs-lookup"><span data-stu-id="43c94-189">All</span></span> |
| <span data-ttu-id="43c94-190">Get Blob Properties</span><span class="sxs-lookup"><span data-stu-id="43c94-190">Get Blob Properties</span></span> |<span data-ttu-id="43c94-191">Tout</span><span class="sxs-lookup"><span data-stu-id="43c94-191">All</span></span> |<span data-ttu-id="43c94-192">Tout</span><span class="sxs-lookup"><span data-stu-id="43c94-192">All</span></span> |
| <span data-ttu-id="43c94-193">Set Blob Properties</span><span class="sxs-lookup"><span data-stu-id="43c94-193">Set Blob Properties</span></span> |<span data-ttu-id="43c94-194">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-194">Owner only</span></span> |<span data-ttu-id="43c94-195">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-195">Owner only</span></span> |
| <span data-ttu-id="43c94-196">Get Blob Metadata</span><span class="sxs-lookup"><span data-stu-id="43c94-196">Get Blob Metadata</span></span> |<span data-ttu-id="43c94-197">Tout</span><span class="sxs-lookup"><span data-stu-id="43c94-197">All</span></span> |<span data-ttu-id="43c94-198">Tout</span><span class="sxs-lookup"><span data-stu-id="43c94-198">All</span></span> |
| <span data-ttu-id="43c94-199">Set Blob Metadata</span><span class="sxs-lookup"><span data-stu-id="43c94-199">Set Blob Metadata</span></span> |<span data-ttu-id="43c94-200">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-200">Owner only</span></span> |<span data-ttu-id="43c94-201">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-201">Owner only</span></span> |
| <span data-ttu-id="43c94-202">Put Block</span><span class="sxs-lookup"><span data-stu-id="43c94-202">Put Block</span></span> |<span data-ttu-id="43c94-203">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-203">Owner only</span></span> |<span data-ttu-id="43c94-204">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-204">Owner only</span></span> |
| <span data-ttu-id="43c94-205">Get Block List (blocs validés uniquement)</span><span class="sxs-lookup"><span data-stu-id="43c94-205">Get Block List (committed blocks only)</span></span> |<span data-ttu-id="43c94-206">Tout</span><span class="sxs-lookup"><span data-stu-id="43c94-206">All</span></span> |<span data-ttu-id="43c94-207">Tout</span><span class="sxs-lookup"><span data-stu-id="43c94-207">All</span></span> |
| <span data-ttu-id="43c94-208">Get Block List (blocs non validés uniquement ou tous les blocs)</span><span class="sxs-lookup"><span data-stu-id="43c94-208">Get Block List (uncommitted blocks only or all blocks)</span></span> |<span data-ttu-id="43c94-209">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-209">Owner only</span></span> |<span data-ttu-id="43c94-210">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-210">Owner only</span></span> |
| <span data-ttu-id="43c94-211">Put Block List</span><span class="sxs-lookup"><span data-stu-id="43c94-211">Put Block List</span></span> |<span data-ttu-id="43c94-212">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-212">Owner only</span></span> |<span data-ttu-id="43c94-213">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-213">Owner only</span></span> |
| <span data-ttu-id="43c94-214">Delete Blob</span><span class="sxs-lookup"><span data-stu-id="43c94-214">Delete Blob</span></span> |<span data-ttu-id="43c94-215">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-215">Owner only</span></span> |<span data-ttu-id="43c94-216">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-216">Owner only</span></span> |
| <span data-ttu-id="43c94-217">Copie d'un objet blob</span><span class="sxs-lookup"><span data-stu-id="43c94-217">Copy Blob</span></span> |<span data-ttu-id="43c94-218">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-218">Owner only</span></span> |<span data-ttu-id="43c94-219">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-219">Owner only</span></span> |
| <span data-ttu-id="43c94-220">Snapshot Blob</span><span class="sxs-lookup"><span data-stu-id="43c94-220">Snapshot Blob</span></span> |<span data-ttu-id="43c94-221">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-221">Owner only</span></span> |<span data-ttu-id="43c94-222">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-222">Owner only</span></span> |
| <span data-ttu-id="43c94-223">Lease Blob</span><span class="sxs-lookup"><span data-stu-id="43c94-223">Lease Blob</span></span> |<span data-ttu-id="43c94-224">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-224">Owner only</span></span> |<span data-ttu-id="43c94-225">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-225">Owner only</span></span> |
| <span data-ttu-id="43c94-226">Put Page</span><span class="sxs-lookup"><span data-stu-id="43c94-226">Put Page</span></span> |<span data-ttu-id="43c94-227">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-227">Owner only</span></span> |<span data-ttu-id="43c94-228">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-228">Owner only</span></span> |
| <span data-ttu-id="43c94-229">Get Page Ranges</span><span class="sxs-lookup"><span data-stu-id="43c94-229">Get Page Ranges</span></span> |<span data-ttu-id="43c94-230">Tout</span><span class="sxs-lookup"><span data-stu-id="43c94-230">All</span></span> |<span data-ttu-id="43c94-231">Tout</span><span class="sxs-lookup"><span data-stu-id="43c94-231">All</span></span> |
| <span data-ttu-id="43c94-232">Append Blob</span><span class="sxs-lookup"><span data-stu-id="43c94-232">Append Blob</span></span> |<span data-ttu-id="43c94-233">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-233">Owner only</span></span> |<span data-ttu-id="43c94-234">Propriétaire uniquement</span><span class="sxs-lookup"><span data-stu-id="43c94-234">Owner only</span></span> |

## <a name="next-steps"></a><span data-ttu-id="43c94-235">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="43c94-235">Next steps</span></span>

* [<span data-ttu-id="43c94-236">Authentification pour les services de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="43c94-236">Authentication for the Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [<span data-ttu-id="43c94-237">Utilisation des signatures d’accès partagé (SAP)</span><span class="sxs-lookup"><span data-stu-id="43c94-237">Using Shared Access Signatures (SAS)</span></span>](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="43c94-238">Délégation de l'accès avec une signature d'accès partagé</span><span class="sxs-lookup"><span data-stu-id="43c94-238">Delegating Access with a Shared Access Signature</span></span>](https://msdn.microsoft.com/library/azure/ee395415.aspx)
