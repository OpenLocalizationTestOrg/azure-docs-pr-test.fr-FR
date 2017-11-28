---
title: aaaIntegrate un compte de stockage Azure avec Azure CDN | Documents Microsoft
description: "Découvrez comment le contenu toouse hello réseau de distribution de contenu (CDN) Azure toodeliver à large bande passante en mettant en cache les objets BLOB depuis le stockage Azure."
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
ms.openlocfilehash: e44716969d6a784265cc4b1da34f0d021a17b38d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a><span data-ttu-id="668c5-103">Intégrer un compte de stockage Azure à Azure CDN</span><span class="sxs-lookup"><span data-stu-id="668c5-103">Integrate an Azure storage account with Azure CDN</span></span>
<span data-ttu-id="668c5-104">CDN peut être activé toocache de contenu à partir de votre stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="668c5-104">CDN can be enabled toocache content from your Azure storage.</span></span> <span data-ttu-id="668c5-105">Elle offre aux développeurs une solution globale pour la diffusion de contenu haut débit en mettant en cache des objets BLOB et le contenu statique des instances de calcul sur des nœuds physiques dans hello États-Unis, Europe, Asie, en Australie et en Amérique du Sud.</span><span class="sxs-lookup"><span data-stu-id="668c5-105">It offers developers a global solution for delivering high-bandwidth content by caching blobs and static content of compute instances at physical nodes in hello United States, Europe, Asia, Australia and South America.</span></span>

## <a name="step-1-create-a-storage-account"></a><span data-ttu-id="668c5-106">Étape 1 : création d’un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="668c5-106">Step 1: Create a storage account</span></span>
<span data-ttu-id="668c5-107">Utilisez hello suivant la procédure toocreate un nouveau compte de stockage pour un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="668c5-107">Use hello following procedure toocreate a new storage account for a Azure subscription.</span></span> <span data-ttu-id="668c5-108">Un compte de stockage donne accès aux services de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="668c5-108">A storage account gives access to Azure storage services.</span></span> <span data-ttu-id="668c5-109">compte de stockage Hello représente le niveau le plus élevé de l’espace de noms hello pour accéder à chacun des composants de service de stockage Azure hello hello : services, les services de file d’attente et les services de la Table d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="668c5-109">hello storage account represents hello highest level of hello namespace for accessing each of hello Azure storage service components: Blob services, Queue services, and Table services.</span></span> <span data-ttu-id="668c5-110">Pour plus d’informations, consultez toohello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="668c5-110">For more information, refer toohello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span></span>

<span data-ttu-id="668c5-111">toocreate un compte de stockage, vous devez être administrateur de service hello ou un coadministrateur pour hello associé abonnement.</span><span class="sxs-lookup"><span data-stu-id="668c5-111">toocreate a storage account, you must be either hello service administrator or a co-administrator for hello associated subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="668c5-112">Il existe plusieurs méthodes que vous pouvez utiliser toocreate un compte de stockage, y compris hello portail Azure et Powershell.</span><span class="sxs-lookup"><span data-stu-id="668c5-112">There are several methods you can use toocreate a storage account, including hello Azure Portal and Powershell.</span></span>  <span data-ttu-id="668c5-113">Pour ce didacticiel, nous utiliserons hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="668c5-113">For this tutorial, we'll be using hello Azure Portal.</span></span>  
> 
> 

<span data-ttu-id="668c5-114">**toocreate un compte de stockage pour un abonnement Azure**</span><span class="sxs-lookup"><span data-stu-id="668c5-114">**toocreate a storage account for an Azure subscription**</span></span>

1. <span data-ttu-id="668c5-115">Connectez-vous à toohello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="668c5-115">Sign in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="668c5-116">Dans le coin supérieur gauche hello, sélectionnez **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="668c5-116">In hello upper left corner, select **New**.</span></span> <span data-ttu-id="668c5-117">Bonjour **nouveau** boîte de dialogue, sélectionnez **données + stockage**, puis cliquez sur **compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="668c5-117">In hello **New** Dialog, select **Data  + Storage**, then click **Storage account**.</span></span>
    
    <span data-ttu-id="668c5-118">Hello **créer le compte de stockage** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="668c5-118">hello **Create storage account** blade appears.</span></span>   

    ![Créer un compte de stockage][create-new-storage-account]  

3. <span data-ttu-id="668c5-120">Bonjour **nom** , tapez un nom de sous-domaine.</span><span class="sxs-lookup"><span data-stu-id="668c5-120">In hello **Name** field, type a subdomain name.</span></span> <span data-ttu-id="668c5-121">Cette entrée peut être composée de 3 à 24 lettres minuscules et chiffres.</span><span class="sxs-lookup"><span data-stu-id="668c5-121">This entry can contain 3-24 lowercase letters and numbers.</span></span>
   
    <span data-ttu-id="668c5-122">Cette valeur devient le nom d’hôte hello dans hello URI qui est utilisé pour adresser des objets Blob, file d’attente ou Table de ressources pour l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="668c5-122">This value becomes hello host name within hello URI that is used to address Blob, Queue, or Table resources for hello subscription.</span></span> <span data-ttu-id="668c5-123">Pour répondre à une ressource de conteneur Bonjour service Blob, vous utiliseriez un URI Bonjour suivant le format, où  *&lt;StorageAccountLabel&gt;*  fait référence vous avez tapé une valeur toohello **entrer une URL**:</span><span class="sxs-lookup"><span data-stu-id="668c5-123">To address a container resource in hello Blob service, you would use a URI in hello following format, where *&lt;StorageAccountLabel&gt;* refers toohello value you typed in **Enter a URL**:</span></span>
   
    <span data-ttu-id="668c5-124">http://*&lt;LibelléCompteStockage&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span><span class="sxs-lookup"><span data-stu-id="668c5-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span></span>
   
    <span data-ttu-id="668c5-125">**Important :** hello sous-domaine de hello URL étiquette forms hello du compte de stockage URI et doit être unique parmi tous les services hébergés dans Azure.</span><span class="sxs-lookup"><span data-stu-id="668c5-125">**Important:** hello URL label forms hello subdomain of hello storage  account URI and must be unique among all hosted services in  Azure.</span></span>
   
    <span data-ttu-id="668c5-126">Cette valeur est également utilisée comme nom hello de ce compte de stockage dans le portail de hello, ou lors de l’accès par programme de ce compte.</span><span class="sxs-lookup"><span data-stu-id="668c5-126">This value is also used as hello name of this storage account in hello portal, or when accessing this account programmatically.</span></span>
4. <span data-ttu-id="668c5-127">Laisser les valeurs par défaut hello pour **modèle de déploiement**, **compte kind**, **performances**, et **réplication**.</span><span class="sxs-lookup"><span data-stu-id="668c5-127">Leave hello defaults for **Deployment model**, **Account kind**, **Performance**, and **Replication**.</span></span> 
5. <span data-ttu-id="668c5-128">Sélectionnez hello **abonnement** que compte de stockage hello est utilisée avec.</span><span class="sxs-lookup"><span data-stu-id="668c5-128">Select hello **Subscription** that hello storage account will be used with.</span></span>
6. <span data-ttu-id="668c5-129">Sélectionnez ou créez un **groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="668c5-129">Select or create a **Resource Group**.</span></span>  <span data-ttu-id="668c5-130">Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="668c5-130">For more information on Resource Groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="668c5-131">Sélectionnez l’emplacement de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="668c5-131">Select a location for your storage account.</span></span>
8. <span data-ttu-id="668c5-132">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="668c5-132">Click **Create**.</span></span> <span data-ttu-id="668c5-133">Hello de création de compte de stockage hello peut durer plusieurs minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="668c5-133">hello process of creating hello storage account might take several minutes toocomplete.</span></span>

## <a name="step-2-enable-cdn-for-hello-storage-account"></a><span data-ttu-id="668c5-134">Étape 2 : Activer le CDN pour le compte de stockage hello</span><span class="sxs-lookup"><span data-stu-id="668c5-134">Step 2: Enable CDN for hello storage account</span></span>

<span data-ttu-id="668c5-135">Avec l’intégration les plus récents de hello, vous pouvez maintenant activer CDN pour votre compte de stockage sans quitter votre extension de portail de stockage.</span><span class="sxs-lookup"><span data-stu-id="668c5-135">With hello newest integration, you can now enable CDN for your storage account without leaving your storage portal extension.</span></span> 

1. <span data-ttu-id="668c5-136">Sélectionnez le compte de stockage hello, rechercher « CDN » ou faites défiler vers le bas à partir du menu de navigation gauche hello, puis cliquez sur « Azure CDN ».</span><span class="sxs-lookup"><span data-stu-id="668c5-136">Select hello storage account, search "CDN" or scroll down from hello left navigation menu, then click "Azure CDN".</span></span>
    
    <span data-ttu-id="668c5-137">Hello **Azure CDN** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="668c5-137">hello **Azure CDN** blade appears.</span></span>

    ![cdn enable navigation][cdn-enable-navigation]
    
2. <span data-ttu-id="668c5-139">Créer un nouveau point de terminaison en entrant les informations hello requis</span><span class="sxs-lookup"><span data-stu-id="668c5-139">Create a new endpoint by entering hello required information</span></span>
    - <span data-ttu-id="668c5-140">**Profil CDN** : vous pouvez en créer un nouveau ou utiliser un profil existant.</span><span class="sxs-lookup"><span data-stu-id="668c5-140">**CDN Profile**: You can create a new or use an existing profile.</span></span>
    - <span data-ttu-id="668c5-141">**Niveau de tarification**: vous ne devez tooselect une tarification niveau si vous créez un nouveau profil CDN.</span><span class="sxs-lookup"><span data-stu-id="668c5-141">**Pricing tier**: You only need tooselect a pricing tier if you create a new CDN profile.</span></span>
    - <span data-ttu-id="668c5-142">**Nom du point de terminaison CDN** : entrez le nom de point de terminaison de votre choix.</span><span class="sxs-lookup"><span data-stu-id="668c5-142">**CDN endpoint name**: Enter an endpoint name per your choice.</span></span>

    > [!TIP]
    > <span data-ttu-id="668c5-143">point de terminaison CDN Hello créé utilise le nom d’hôte hello de votre compte de stockage comme origine par défaut.</span><span class="sxs-lookup"><span data-stu-id="668c5-143">hello created CDN endpoint uses hello hostname of your storage account as origin by default.</span></span>

    <span data-ttu-id="668c5-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span><span class="sxs-lookup"><span data-stu-id="668c5-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span></span>

3. <span data-ttu-id="668c5-145">Après la création, le nouveau point de terminaison hello s’afficheront dans la liste de point de terminaison hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="668c5-145">After creation, hello new endpoint will show up in hello endpoint list above.</span></span>

    ![cdn storage new endpoint][cdn-storage-new-endpoint]

> [!NOTE]
> <span data-ttu-id="668c5-147">Vous pouvez également passer tooAzure CDN extension tooenable CDN. [Didacticiel](#Tutorial-cdn-create-profile).</span><span class="sxs-lookup"><span data-stu-id="668c5-147">You can also go tooAzure CDN extension tooenable CDN.[Tutorial](#Tutorial-cdn-create-profile).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a><span data-ttu-id="668c5-148">Étape 3 : Activer d’autres fonctionnalités du CDN</span><span class="sxs-lookup"><span data-stu-id="668c5-148">Step 3: Enable additional CDN features</span></span>

<span data-ttu-id="668c5-149">À partir du Panneau de « Azure CDN » de compte de stockage, cliquez sur le point de terminaison CDN hello à partir du Panneau de configuration hello liste tooopen CDN.</span><span class="sxs-lookup"><span data-stu-id="668c5-149">From storage account "Azure CDN" blade, click hello CDN endpoint from hello list tooopen CDN configuration blade.</span></span> <span data-ttu-id="668c5-150">Vous pouvez activer des fonctionnalités supplémentaires du CDN pour la livraison, comme la compression, la chaîne de requête et le filtrage géographique.</span><span class="sxs-lookup"><span data-stu-id="668c5-150">You can enable additional CDN features for your delivery, such as compression, query string, geo filtering.</span></span> <span data-ttu-id="668c5-151">Vous pouvez également ajouter le point de terminaison CDN domaine personnalisé mappage tooyour et activer HTTPS de domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="668c5-151">You can also add custom domain mapping tooyour CDN endpoint and enable custom domain HTTPS.</span></span>
    
![Configuration CDN stockage CDN][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a><span data-ttu-id="668c5-153">Étape 4 : accès au contenu du CDN</span><span class="sxs-lookup"><span data-stu-id="668c5-153">Step 4: Access CDN content</span></span>
<span data-ttu-id="668c5-154">Utilisez hello URL du CDN tooaccess mis en cache le contenu sur hello CDN, fourni dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="668c5-154">tooaccess cached content on hello CDN, use hello CDN URL provided in hello portal.</span></span> <span data-ttu-id="668c5-155">adresse Hello pour un objet blob mis en cache sera similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="668c5-155">hello address for a cached blob will be similar toohello following:</span></span>

<span data-ttu-id="668c5-156">http://<*nom_point_de_terminaison*\>.azureedge.net/<*MonConteneurPublic*\>/<*Nom_blob*\></span><span class="sxs-lookup"><span data-stu-id="668c5-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span></span>

> [!NOTE]
> <span data-ttu-id="668c5-157">Une fois que vous activez le compte de stockage de tooa accès CDN, tous les objets disponibles publiquement sont éligibles pour la mise en cache de périmètre CDN.</span><span class="sxs-lookup"><span data-stu-id="668c5-157">Once you enable CDN access tooa storage account, all publicly available objects are eligible for CDN edge caching.</span></span> <span data-ttu-id="668c5-158">Si vous modifiez un objet qui est actuellement mis en cache hello CDN, hello nouveau contenu n’est plus disponible via hello CDN jusqu'à ce que hello CDN actualise son contenu lors de la période de durée de vie contenu hello mis en cache expire.</span><span class="sxs-lookup"><span data-stu-id="668c5-158">If you modify an object that is currently cached in hello CDN, hello new content will not be available via hello CDN until hello CDN refreshes its content when hello cached content time-to-live period expires.</span></span>
> 
> 

## <a name="step-5-remove-content-from-hello-cdn"></a><span data-ttu-id="668c5-159">Étape 5 : Supprimer le contenu à partir de hello CDN</span><span class="sxs-lookup"><span data-stu-id="668c5-159">Step 5: Remove content from hello CDN</span></span>
<span data-ttu-id="668c5-160">Si vous ne souhaitez plus toocache un objet Bonjour Azure réseau CDN (Content Delivery), vous pouvez effectuer l’une des hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="668c5-160">If you no longer wish toocache an object in hello Azure Content Delivery Network (CDN), you can take one of hello following steps:</span></span>

* <span data-ttu-id="668c5-161">Vous pouvez rendre hello privé de conteneur au lieu de public.</span><span class="sxs-lookup"><span data-stu-id="668c5-161">You can make hello container private instead of public.</span></span> <span data-ttu-id="668c5-162">Consultez [gérer l’accès en lecture anonyme toocontainers et les objets BLOB](../storage/blobs/storage-manage-access-to-resources.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="668c5-162">See [Manage anonymous read access toocontainers and blobs](../storage/blobs/storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="668c5-163">Vous pouvez désactiver ou supprimer le point de terminaison CDN hello à l’aide du portail de gestion de hello.</span><span class="sxs-lookup"><span data-stu-id="668c5-163">You can disable or delete hello CDN endpoint using hello Management Portal.</span></span>
* <span data-ttu-id="668c5-164">Vous pouvez modifier votre toorequests plus de temps de réponse service hébergé toono pour l’objet de hello.</span><span class="sxs-lookup"><span data-stu-id="668c5-164">You can modify your hosted service toono longer respond toorequests for hello object.</span></span>

<span data-ttu-id="668c5-165">Un objet déjà mis en cache dans hello CDN reste dans le cache jusqu'à ce que hello time-to-live pour l’objet de hello expire ou jusqu'à ce que le point de terminaison hello est purgée.</span><span class="sxs-lookup"><span data-stu-id="668c5-165">An object already cached in hello CDN will remain cached until hello time-to-live period for hello object expires or until hello endpoint is purged.</span></span> <span data-ttu-id="668c5-166">Lors de l’expiration de la période de durée de vie de hello, hello CDN vérifiera toosee indique si le point de terminaison CDN hello est toujours valide et objet hello toujours accessible de manière anonyme.</span><span class="sxs-lookup"><span data-stu-id="668c5-166">When hello time-to-live period expires, hello CDN will check toosee whether hello CDN endpoint is still valid and hello object still anonymously accessible.</span></span> <span data-ttu-id="668c5-167">Si elle n’est pas le cas, puis les objet hello sont ne sont plus mises en cache.</span><span class="sxs-lookup"><span data-stu-id="668c5-167">If it is not, then hello object will no longer be cached.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="668c5-168">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="668c5-168">Additional resources</span></span>
* [<span data-ttu-id="668c5-169">Comment tooa de contenu CDN tooMap un domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="668c5-169">How tooMap CDN Content tooa Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="668c5-170">Activer HTTPS pour votre domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="668c5-170">Enable HTTPS for your custom domain</span></span>](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
