---
title: "Intégrer un compte de stockage Azure à Azure CDN | Microsoft Docs"
description: "Découvrez comment utiliser le réseau de distribution de contenu (CDN) Azure pour diffuser du contenu haut débit en mettant en cache les objets blob à partir d’Azure Storage."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: cbc2ff98-916d-4339-8959-622823c5b772
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 511076935d06ed0908341044e37069e74530be49
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a><span data-ttu-id="3e99b-103">Intégrer un compte de stockage Azure à Azure CDN</span><span class="sxs-lookup"><span data-stu-id="3e99b-103">Integrate an Azure storage account with Azure CDN</span></span>
<span data-ttu-id="3e99b-104">CDN peut être activé pour mettre du contenu en cache depuis le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="3e99b-104">CDN can be enabled to cache content from your Azure storage.</span></span> <span data-ttu-id="3e99b-105">Il offre aux développeurs une solution globale pour la diffusion de contenu haut débit en mettant en cache les objets blob et le contenu statique des instances de calcul sur des nœuds physiques aux États-Unis, en Europe, en Asie, en Australie et en Amérique du Sud.</span><span class="sxs-lookup"><span data-stu-id="3e99b-105">It offers developers a global solution for delivering high-bandwidth content by caching blobs and static content of compute instances at physical nodes in the United States, Europe, Asia, Australia and South America.</span></span>

## <a name="step-1-create-a-storage-account"></a><span data-ttu-id="3e99b-106">Étape 1 : création d’un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="3e99b-106">Step 1: Create a storage account</span></span>
<span data-ttu-id="3e99b-107">Utilisez la procédure suivante pour créer un compte de stockage pour un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="3e99b-107">Use the following procedure to create a new storage account for a Azure subscription.</span></span> <span data-ttu-id="3e99b-108">Un compte de stockage donne accès aux services de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="3e99b-108">A storage account gives access to Azure storage services.</span></span> <span data-ttu-id="3e99b-109">Le compte de stockage représente le niveau le plus élevé de l’espace de noms pour l’accès à chacun des composants du service de stockage Azure : services BLOB, services de file d’attente et services de Table.</span><span class="sxs-lookup"><span data-stu-id="3e99b-109">The storage account represents the highest level of the namespace for accessing each of the Azure storage service components: Blob services, Queue services, and Table services.</span></span> <span data-ttu-id="3e99b-110">Pour plus d'informations, consultez [Introduction à Microsoft Azure Storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3e99b-110">For more information, refer to the [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md).</span></span>

<span data-ttu-id="3e99b-111">Pour créer un compte de stockage, vous devez être l’administrateur de service ou un co-administrateur de l’abonnement associé.</span><span class="sxs-lookup"><span data-stu-id="3e99b-111">To create a storage account, you must be either the service administrator or a co-administrator for the associated subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="3e99b-112">Il existe plusieurs méthodes que vous pouvez utiliser pour créer un compte de stockage, y compris le portail Azure et Powershell.</span><span class="sxs-lookup"><span data-stu-id="3e99b-112">There are several methods you can use to create a storage account, including the Azure Portal and Powershell.</span></span>  <span data-ttu-id="3e99b-113">Pour ce didacticiel, nous allons utiliser le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3e99b-113">For this tutorial, we'll be using the Azure Portal.</span></span>  
> 
> 

<span data-ttu-id="3e99b-114">**Pour créer un compte de stockage pour un abonnement Azure**</span><span class="sxs-lookup"><span data-stu-id="3e99b-114">**To create a storage account for an Azure subscription**</span></span>

1. <span data-ttu-id="3e99b-115">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3e99b-115">Sign in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3e99b-116">Dans le coin supérieur gauche, sélectionnez **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="3e99b-116">In the upper left corner, select **New**.</span></span> <span data-ttu-id="3e99b-117">Dans la boîte de dialogue **Nouveau**, sélectionnez **Données + stockage**, puis cliquez sur **Compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="3e99b-117">In the **New** Dialog, select **Data  + Storage**, then click **Storage account**.</span></span>
    
    <span data-ttu-id="3e99b-118">Le panneau **Créer un compte de stockage** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3e99b-118">The **Create storage account** blade appears.</span></span>   

    ![Créer un compte de stockage][create-new-storage-account]  

3. <span data-ttu-id="3e99b-120">Dans le champ **Nom** , tapez un nom de sous-domaine.</span><span class="sxs-lookup"><span data-stu-id="3e99b-120">In the **Name** field, type a subdomain name.</span></span> <span data-ttu-id="3e99b-121">Cette entrée peut être composée de 3 à 24 lettres minuscules et chiffres.</span><span class="sxs-lookup"><span data-stu-id="3e99b-121">This entry can contain 3-24 lowercase letters and numbers.</span></span>
   
    <span data-ttu-id="3e99b-122">Cette valeur devient le nom d’hôte contenu dans l’URI utilisé pour adresser les ressources d’objets blob, de files d’attente et de tables pour l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="3e99b-122">This value becomes the host name within the URI that is used to address Blob, Queue, or Table resources for the subscription.</span></span> <span data-ttu-id="3e99b-123">Pour adresser une ressource de conteneur dans le service BLOB, vous utilisez un URI au format suivant, où *&lt;LibelléCompteStockage&gt;* fait référence à la valeur entrée dans **Enter a URL** :</span><span class="sxs-lookup"><span data-stu-id="3e99b-123">To address a container resource in the Blob service, you would use a URI in the following format, where *&lt;StorageAccountLabel&gt;* refers to the value you typed in **Enter a URL**:</span></span>
   
    <span data-ttu-id="3e99b-124">http://*&lt;LibelléCompteStockage&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span><span class="sxs-lookup"><span data-stu-id="3e99b-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span></span>
   
    <span data-ttu-id="3e99b-125">**Important :** l’étiquette de l’URL forme le sous-domaine de l’URI du compte de stockage et doit être unique parmi tous les services hébergés dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3e99b-125">**Important:** The URL label forms the subdomain of the storage  account URI and must be unique among all hosted services in  Azure.</span></span>
   
    <span data-ttu-id="3e99b-126">Cette valeur est également utilisée comme nom pour ce compte de stockage dans le portail ou lors de l’accès à ce compte par programme.</span><span class="sxs-lookup"><span data-stu-id="3e99b-126">This value is also used as the name of this storage account in the portal, or when accessing this account programmatically.</span></span>
4. <span data-ttu-id="3e99b-127">Conservez les valeurs par défaut des champs **Modèle de déploiement**, **Type de compte**, **Performances** et **Réplication**.</span><span class="sxs-lookup"><span data-stu-id="3e99b-127">Leave the defaults for **Deployment model**, **Account kind**, **Performance**, and **Replication**.</span></span> 
5. <span data-ttu-id="3e99b-128">Sélectionnez l' **abonnement** à utiliser avec le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="3e99b-128">Select the **Subscription** that the storage account will be used with.</span></span>
6. <span data-ttu-id="3e99b-129">Sélectionnez ou créez un **groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="3e99b-129">Select or create a **Resource Group**.</span></span>  <span data-ttu-id="3e99b-130">Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="3e99b-130">For more information on Resource Groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="3e99b-131">Sélectionnez l’emplacement de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="3e99b-131">Select a location for your storage account.</span></span>
8. <span data-ttu-id="3e99b-132">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="3e99b-132">Click **Create**.</span></span> <span data-ttu-id="3e99b-133">Le processus de création du compte de stockage peut durer quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="3e99b-133">The process of creating the storage account might take several minutes to complete.</span></span>

## <a name="step-2-enable-cdn-for-the-storage-account"></a><span data-ttu-id="3e99b-134">Étape 2 : Activation du CDN pour le compte de stockage</span><span class="sxs-lookup"><span data-stu-id="3e99b-134">Step 2: Enable CDN for the storage account</span></span>

<span data-ttu-id="3e99b-135">Avec l’intégration la plus récente, vous pouvez maintenant activer CDN pour votre compte de stockage sans quitter votre extension de portail de stockage.</span><span class="sxs-lookup"><span data-stu-id="3e99b-135">With the newest integration, you can now enable CDN for your storage account without leaving your storage portal extension.</span></span> 

1. <span data-ttu-id="3e99b-136">Sélectionnez le compte de stockage, recherchez « CDN » ou faites défiler vers le bas dans le menu de navigation de gauche, puis cliquez sur « Azure CDN ».</span><span class="sxs-lookup"><span data-stu-id="3e99b-136">Select the storage account, search "CDN" or scroll down from the left navigation menu, then click "Azure CDN".</span></span>
    
    <span data-ttu-id="3e99b-137">Le panneau **Azure CDN** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3e99b-137">The **Azure CDN** blade appears.</span></span>

    ![cdn enable navigation][cdn-enable-navigation]
    
2. <span data-ttu-id="3e99b-139">Créer un nouveau point de terminaison en entrant les informations requises</span><span class="sxs-lookup"><span data-stu-id="3e99b-139">Create a new endpoint by entering the required information</span></span>
    - <span data-ttu-id="3e99b-140">**Profil CDN** : vous pouvez en créer un nouveau ou utiliser un profil existant.</span><span class="sxs-lookup"><span data-stu-id="3e99b-140">**CDN Profile**: You can create a new or use an existing profile.</span></span>
    - <span data-ttu-id="3e99b-141">**Niveau de tarification** : vous devez sélectionner un niveau de tarification uniquement si vous créez un nouveau profil CDN.</span><span class="sxs-lookup"><span data-stu-id="3e99b-141">**Pricing tier**: You only need to select a pricing tier if you create a new CDN profile.</span></span>
    - <span data-ttu-id="3e99b-142">**Nom du point de terminaison CDN** : entrez le nom de point de terminaison de votre choix.</span><span class="sxs-lookup"><span data-stu-id="3e99b-142">**CDN endpoint name**: Enter an endpoint name per your choice.</span></span>

    > [!TIP]
    > <span data-ttu-id="3e99b-143">Le point de terminaison CDN créé utilise le nom d’hôte de votre compte de stockage en tant qu’origine par défaut.</span><span class="sxs-lookup"><span data-stu-id="3e99b-143">The created CDN endpoint uses the hostname of your storage account as origin by default.</span></span>

    <span data-ttu-id="3e99b-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span><span class="sxs-lookup"><span data-stu-id="3e99b-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span></span>

3. <span data-ttu-id="3e99b-145">Après création, le nouveau point de terminaison s’affiche dans la liste de points de terminaison ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="3e99b-145">After creation, the new endpoint will show up in the endpoint list above.</span></span>

    ![cdn storage new endpoint][cdn-storage-new-endpoint]

> [!NOTE]
> <span data-ttu-id="3e99b-147">Vous pouvez également accéder à l’extension Azure CDN pour activer le CDN. [Didacticiel](#Tutorial-cdn-create-profile).</span><span class="sxs-lookup"><span data-stu-id="3e99b-147">You can also go to Azure CDN extension to enable CDN.[Tutorial](#Tutorial-cdn-create-profile).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a><span data-ttu-id="3e99b-148">Étape 3 : Activer d’autres fonctionnalités du CDN</span><span class="sxs-lookup"><span data-stu-id="3e99b-148">Step 3: Enable additional CDN features</span></span>

<span data-ttu-id="3e99b-149">Dans le panneau « Azure CDN » du compte de stockage, cliquez sur le point de terminaison CDN dans la liste pour ouvrir le panneau de configuration du CDN.</span><span class="sxs-lookup"><span data-stu-id="3e99b-149">From storage account "Azure CDN" blade, click the CDN endpoint from the list to open CDN configuration blade.</span></span> <span data-ttu-id="3e99b-150">Vous pouvez activer des fonctionnalités supplémentaires du CDN pour la livraison, comme la compression, la chaîne de requête et le filtrage géographique.</span><span class="sxs-lookup"><span data-stu-id="3e99b-150">You can enable additional CDN features for your delivery, such as compression, query string, geo filtering.</span></span> <span data-ttu-id="3e99b-151">Vous pouvez également ajouter le mappage de domaine personnalisé pour votre point de terminaison CDN et activer HTTPS sur les domaines personnalisés.</span><span class="sxs-lookup"><span data-stu-id="3e99b-151">You can also add custom domain mapping to your CDN endpoint and enable custom domain HTTPS.</span></span>
    
![Configuration CDN stockage CDN][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a><span data-ttu-id="3e99b-153">Étape 4 : accès au contenu du CDN</span><span class="sxs-lookup"><span data-stu-id="3e99b-153">Step 4: Access CDN content</span></span>
<span data-ttu-id="3e99b-154">Pour accéder au contenu mis en cache sur le CDN, utilisez l’URL CDN fournie dans le portail.</span><span class="sxs-lookup"><span data-stu-id="3e99b-154">To access cached content on the CDN, use the CDN URL provided in the portal.</span></span> <span data-ttu-id="3e99b-155">L’adresse d’un objet blob mis en cache est au format suivant :</span><span class="sxs-lookup"><span data-stu-id="3e99b-155">The address for a cached blob will be similar to the following:</span></span>

<span data-ttu-id="3e99b-156">http://<*nom_point_de_terminaison*\>.azureedge.net/<*MonConteneurPublic*\>/<*Nom_blob*\></span><span class="sxs-lookup"><span data-stu-id="3e99b-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span></span>

> [!NOTE]
> <span data-ttu-id="3e99b-157">Dès que vous activez un accès au CDN pour un compte de stockage, tous les objets disponibles publiquement peuvent bénéficier de la mise en cache de périmètre du CDN.</span><span class="sxs-lookup"><span data-stu-id="3e99b-157">Once you enable CDN access to a storage account, all publicly available objects are eligible for CDN edge caching.</span></span> <span data-ttu-id="3e99b-158">Si vous modifiez un objet actuellement mis en cache dans le CDN, le nouveau contenu n’est pas disponible via le CDN avant son actualisation, c’est-à-dire une fois sa durée de vie écoulée.</span><span class="sxs-lookup"><span data-stu-id="3e99b-158">If you modify an object that is currently cached in the CDN, the new content will not be available via the CDN until the CDN refreshes its content when the cached content time-to-live period expires.</span></span>
> 
> 

## <a name="step-5-remove-content-from-the-cdn"></a><span data-ttu-id="3e99b-159">Étape 5 : Suppression de contenu du CDN</span><span class="sxs-lookup"><span data-stu-id="3e99b-159">Step 5: Remove content from the CDN</span></span>
<span data-ttu-id="3e99b-160">Si vous ne souhaitez plus mettre en cache un objet dans le réseau de distribution de contenu (CDN) Azure, vous pouvez procéder comme suit :</span><span class="sxs-lookup"><span data-stu-id="3e99b-160">If you no longer wish to cache an object in the Azure Content Delivery Network (CDN), you can take one of the following steps:</span></span>

* <span data-ttu-id="3e99b-161">Vous pouvez changer le statut du conteneur de public à privé.</span><span class="sxs-lookup"><span data-stu-id="3e99b-161">You can make the container private instead of public.</span></span> <span data-ttu-id="3e99b-162">Pour plus d'informations, consultez [Gestion de l'accès en lecture anonyme aux conteneurs et aux objets blob](../storage/blobs/storage-manage-access-to-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="3e99b-162">See [Manage anonymous read access to containers and blobs](../storage/blobs/storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="3e99b-163">Vous pouvez désactiver ou supprimer le point de terminaison CDN à l’aide du portail de gestion.</span><span class="sxs-lookup"><span data-stu-id="3e99b-163">You can disable or delete the CDN endpoint using the Management Portal.</span></span>
* <span data-ttu-id="3e99b-164">Vous pouvez modifier votre service hébergé pour qu’il ne réponde plus aux demandes de l’objet.</span><span class="sxs-lookup"><span data-stu-id="3e99b-164">You can modify your hosted service to no longer respond to requests for the object.</span></span>

<span data-ttu-id="3e99b-165">Un objet déjà mis en cache dans le CDN y reste jusqu'à ce que sa durée de vie expire ou que le point de terminaison soit purgé.</span><span class="sxs-lookup"><span data-stu-id="3e99b-165">An object already cached in the CDN will remain cached until the time-to-live period for the object expires or until the endpoint is purged.</span></span> <span data-ttu-id="3e99b-166">Après cela, le CDN vérifie si le point de terminaison CDN est encore valide et si l’objet est encore accessible de manière anonyme.</span><span class="sxs-lookup"><span data-stu-id="3e99b-166">When the time-to-live period expires, the CDN will check to see whether the CDN endpoint is still valid and the object still anonymously accessible.</span></span> <span data-ttu-id="3e99b-167">S’il ne l’est pas, l’objet n’est plus mis en cache.</span><span class="sxs-lookup"><span data-stu-id="3e99b-167">If it is not, then the object will no longer be cached.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3e99b-168">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3e99b-168">Additional resources</span></span>
* [<span data-ttu-id="3e99b-169">Mappage du contenu CDN à un domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="3e99b-169">How to Map CDN Content to a Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="3e99b-170">Activer HTTPS pour votre domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="3e99b-170">Enable HTTPS for your custom domain</span></span>](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
