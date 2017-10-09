---
title: "fichiers aaaUpload à un compte Azure Media Services à l’aide de Aspera | Documents Microsoft"
description: "Ce didacticiel vous guide tout au long des étapes hello du téléchargement des fichiers dans un compte de stockage qui est associé à un compte de service de média à l’aide de hello ** Aspera Server sur la demande ** le service sur Azure."
services: media-services
documentationcenter: 
author: johndeu
manager: cfowler
editor: 
ms.assetid: 8812623a-b425-4a0f-9e05-0ee6c839b6f9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/17/2017
ms.author: juliako
ms.openlocfilehash: 7213f016cc1b7f262b14db7b39b478a03970d1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-aspera-server-on-demand-service-on-azure"></a><span data-ttu-id="0f5cc-103">Télécharger des fichiers dans un compte Media Services à l’aide de hello Aspera Server On Demand service sur Azure</span><span class="sxs-lookup"><span data-stu-id="0f5cc-103">Upload files into a Media Services account using hello Aspera Server On Demand service on Azure</span></span>

## <a name="overview"></a><span data-ttu-id="0f5cc-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="0f5cc-104">Overview</span></span>

<span data-ttu-id="0f5cc-105">**Aspera** est un logiciel de transfert de fichiers à haut débit.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-105">**Aspera** is a high-speed file transfer software.</span></span> <span data-ttu-id="0f5cc-106">Le service **Aspera Server On Demand** pour Azure permet de charger et télécharger rapidement des fichiers volumineux directement dans un espace de stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-106">**Aspera Server On Demand** for Azure enables high-speed upload and download of large files directly into Azure Blob object storage.</span></span> <span data-ttu-id="0f5cc-107">Pour plus d’informations sur **Aspera On Demand**, consultez hello [Aspera Cloud](http://cloud.asperasoft.com/) site.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-107">For information about **Aspera On Demand**, see hello [Aspera Cloud](http://cloud.asperasoft.com/) site.</span></span> 
  
<span data-ttu-id="0f5cc-108">**Serveur de Aspera On Demand** pour Azure est disponible à l’achat de hello [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span><span class="sxs-lookup"><span data-stu-id="0f5cc-108">**Aspera Server On Demand** for Azure is available for purchase from hello [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span></span> <span data-ttu-id="0f5cc-109">Dans commande toocomplete un achat de **Aspera Server On Demand** pour Azure, veuillez vous connecter à Azure Marketplace avec votre Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-109">In order toocomplete a purchase of **Aspera Server On Demand** for Azure, please log into Azure Marketplace with your Windows Live ID.</span></span>

<span data-ttu-id="0f5cc-110">Ce didacticiel vous guide tout au long des étapes hello du téléchargement des fichiers dans un compte de stockage qui est associé à un compte de service de média à l’aide de hello **Aspera Server On Demand** service sur Azure.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-110">This tutorial walks you through hello steps of uploading files into a storage account that is associated with a Media Services account using hello **Aspera Server On Demand** service on Azure.</span></span> 

<span data-ttu-id="0f5cc-111">Vous trouverez un exemple qui montre comment toouse Azure fonctionne avec Aspera et Media Services [ici](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span><span class="sxs-lookup"><span data-stu-id="0f5cc-111">You can find an example that shows how toouse Azure functions with Aspera and Media Services [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span></span>

>[!NOTE]
><span data-ttu-id="0f5cc-112">Il existe une limite toohello taille maximale prise en charge pour le traitement des processeurs de support (PA) avec Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-112">There is a limit toohello maximum file size supported for processing with Azure Media Services media processors (MPs).</span></span> <span data-ttu-id="0f5cc-113">Consultez [cela](media-services-quotas-and-limitations.md) pour plus d’informations sur la limite de taille de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="0f5cc-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0f5cc-114">Prerequisites</span></span> 

<span data-ttu-id="0f5cc-115">toocomplete ce didacticiel, vous devez :</span><span class="sxs-lookup"><span data-stu-id="0f5cc-115">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="0f5cc-116">Un identifiant Windows Live.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-116">A Windows Live ID</span></span>
* <span data-ttu-id="0f5cc-117">Un [compte Azure](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="0f5cc-117">An [Azure account](https://azure.microsoft.com).</span></span> <span data-ttu-id="0f5cc-118">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0f5cc-118">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="0f5cc-119">Un [compte Azure Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="0f5cc-119">An [Azure Media Services account](media-services-portal-create-account.md).</span></span>

## <a name="purchase-aspera-on-demand-for-azure"></a><span data-ttu-id="0f5cc-120">Acheter Aspera On Demand pour Azure</span><span class="sxs-lookup"><span data-stu-id="0f5cc-120">Purchase Aspera On Demand for Azure</span></span>

<span data-ttu-id="0f5cc-121">Une fois que vous êtes connecté à Azure Marketplace, suivez ces étapes de base de toocomplete votre achat de Aspera On Demand pour Azure.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-121">Once you have logged into Azure Marketplace,  follow these basic steps toocomplete your purchase of Aspera On Demand for Azure.</span></span>

1. <span data-ttu-id="0f5cc-122">Recherchez Aspera et sélectionnez « Server On Demand ».</span><span class="sxs-lookup"><span data-stu-id="0f5cc-122">Search for Aspera and select 'Server On Demand'.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. <span data-ttu-id="0f5cc-124">Passez en revue les plans d’abonnement hello et cliquez sur « S’inscrire »</span><span class="sxs-lookup"><span data-stu-id="0f5cc-124">Review hello subscription plans and click on 'Sign Up'</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. <span data-ttu-id="0f5cc-126">Renseignez les spécificités de hello pour votre serveur d’abonnement de la demande.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-126">Fill in hello specifics for your Server on Demand subscription.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. <span data-ttu-id="0f5cc-128">Cliquez sur hello **niveau tarifaire** et sélectionnez votre volume mensuel souhaité dans le panneau de configuration hello sub.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-128">Click on hello **Pricing Tier** and select your desired monthly volume in hello sub panel.</span></span> <span data-ttu-id="0f5cc-129">Bonjour **détails du Plan** Panneau de configuration, sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-129">In hello **Plan details** panel, select **OK**.</span></span> <span data-ttu-id="0f5cc-130">Ensuite, dans hello **Choisissez votre niveau tarifaire** du panneau, cliquez sur **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-130">Then, in hello **Choose your Pricing Tier** panel, click **Select**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. <span data-ttu-id="0f5cc-132">Cliquez sur **juridiques** tooview et acceptez les conditions juridiques de hello dans Panneau de configuration hello sub.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-132">Click on **Legal terms** tooview and accept hello legal terms in hello sub panel.</span></span> <span data-ttu-id="0f5cc-133">Une fois que vous avez consulté les conditions juridiques hello, cliquez sur **bon**.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-133">Once you have reviewed hello legal terms, click **Purchase**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. <span data-ttu-id="0f5cc-135">Terminer l’achat de hello en cliquant sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-135">Complete hello purchase by clicking **Create**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. <span data-ttu-id="0f5cc-137">annonce Hello du tableau de bord Azure approvisionne les service hello.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-137">hello Azure dashboard will announce that it is provisioning hello service.</span></span>  <span data-ttu-id="0f5cc-138">Une fois qu’il est terminé avec l’allocation, vous trouverez un nouvel abonnement hello en effectuant une recherche dans les ressources nom hello du service de hello.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-138">Once it is completed with provisioning, you can find hello new subscription by searching in your resources for hello name of hello service.</span></span> <span data-ttu-id="0f5cc-139">Lorsque vous avez trouvé le service hello, double-cliquez sur portail de gestion du service toolaunch hello.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-139">Once you have found hello service, double click on it toolaunch hello service management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. <span data-ttu-id="0f5cc-141">Lancez le portail de gestion Aspera hello.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-141">Launch hello Aspera management portal.</span></span> <span data-ttu-id="0f5cc-142">Une fois que vous avez trouvé votre nouveau service Aspera, vous pouvez obtenir le portail de gestion toohello accès, en cliquant sur le service de hello.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-142">Once you have found your new Aspera service, you can gain access toohello management portal, by clicking on hello service.</span></span>  <span data-ttu-id="0f5cc-143">Un nouveau panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-143">A new panel will be launched.</span></span> <span data-ttu-id="0f5cc-144">Dans ce nouveau panneau de configuration, vous devez tooclick sur hello **nom de la ressource** de votre nouveau service.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-144">From within that new panel, you need tooclick on hello **Resource Name** of your new service.</span></span>  <span data-ttu-id="0f5cc-145">Bonjour suivant capture d’écran, le nom de ressource de hello est 'AsperaTransferDemo'.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-145">In hello following screenshot, hello resource name is 'AsperaTransferDemo'.</span></span> <span data-ttu-id="0f5cc-146">Une fois que vous cliquez sur le nom de la ressource hello, un autre panneau est lancé.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-146">Once you click on hello resource name, another panel is launched.</span></span> <span data-ttu-id="0f5cc-147">Ce panneau contient un lien « Gérer ».</span><span class="sxs-lookup"><span data-stu-id="0f5cc-147">In that newly launched panel, you will see a 'Manage' link.</span></span> <span data-ttu-id="0f5cc-148">Cliquez sur hello le portail de gestion Aspera 'Gérer' lien toolaunch hello.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-148">Click on hello 'Manage' link toolaunch hello Aspera management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. <span data-ttu-id="0f5cc-150">En cliquant sur hello lien gérer, vous obtiendrez une page d’inscription toohello, ce qui est nécessaire tooaccess hello service.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-150">By clicking on hello manage link, you will get toohello registration page, which is required tooaccess hello service.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. <span data-ttu-id="0f5cc-152">À ce stade, vous aurez accès toohello Aspera portail de gestion, où vous pouvez créer des touches d’accès rapide, téléchargez Aspera clients et les licences, afficher l’utilisation et en savoir plus sur les API de hello.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-152">At this point, you should have access toohello Aspera service management portal, where you can create access keys, download Aspera clients and licenses, view usage and learn about hello APIs.</span></span>

    <span data-ttu-id="0f5cc-153">Hello capture d’écran suivante montre la création de l’accès hello.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-153">hello following screenshot shows hello access creation.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    <span data-ttu-id="0f5cc-155">Hello capture d’écran suivante montre l’utilisation de hello reporting interfaces dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-155">hello following screenshot shows hello usage reporting interfaces in hello portal.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a><span data-ttu-id="0f5cc-157">Chargement de fichiers avec Aspera</span><span class="sxs-lookup"><span data-stu-id="0f5cc-157">Upload files with Aspera</span></span>

1. <span data-ttu-id="0f5cc-158">Téléchargez et installez le logiciel client hello Aspera :</span><span class="sxs-lookup"><span data-stu-id="0f5cc-158">Download and install hello Aspera client software:</span></span>
    
    * [<span data-ttu-id="0f5cc-159">Plug-in de navigateur</span><span class="sxs-lookup"><span data-stu-id="0f5cc-159">Browser plugin</span></span>](http://downloads.asperasoft.com/connect2/)
    * [<span data-ttu-id="0f5cc-160">Client enrichi</span><span class="sxs-lookup"><span data-stu-id="0f5cc-160">Rich client</span></span>](http://downloads.asperasoft.com/en/downloads/2)

2. <span data-ttu-id="0f5cc-161">Effectuez votre premier transfert.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-161">Make your first transfer.</span></span> <span data-ttu-id="0f5cc-162">Dans l’ordre toouse hello Aspera client tootransfer avec le service de transfert Aspera de hello, vous toocomplete hello éléments suivants sont nécessaires :</span><span class="sxs-lookup"><span data-stu-id="0f5cc-162">In order toouse hello Aspera client tootransfer with hello Aspera transfer service, you need toocomplete hello following:</span></span> 

    1. <span data-ttu-id="0f5cc-163">Créer une clé d’accès, à l’aide du portail de Aspera hello.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-163">Create an access key, using hello Aspera portal.</span></span>  
    2. <span data-ttu-id="0f5cc-164">Téléchargement et installation client de licence hello Aspera (logiciel sont accessibles dans le portail de Aspera hello).</span><span class="sxs-lookup"><span data-stu-id="0f5cc-164">Download, install, and license hello Aspera client (software can be found in hello Aspera portal).</span></span>  

    >[!NOTE]
    ><span data-ttu-id="0f5cc-165">Lisez le guide du client hello Aspera des informations de configuration.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-165">Please read hello Aspera client guide for configuration information.</span></span>
    
    3. <span data-ttu-id="0f5cc-166">Récupérer des informations de votre compte de stockage qui est associé à votre compte de média Azure à l’aide de hello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0f5cc-166">Retrieve some information of your storage account that is associated with your Azure Media Account using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="0f5cc-167">Plus précisément, nom et la clé et nom de conteneur stockage hello dans toowhich vous souhaitez tooplace votre contenu.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-167">Specifically, name and key, and hello storage blob container name in toowhich you want tooplace your content.</span></span> 

        * <span data-ttu-id="0f5cc-168">informations de stockage hello tooget à partir du portail de hello : recherchez votre compte de stockage, cliquez sur les touches d’accès hello et copier hello hello et nom de la clé de votre compte.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-168">tooget hello storage info from hello portal: find your storage account, click on hello Access keys and copy hello name and hello key of your account.</span></span>
        * <span data-ttu-id="0f5cc-169">nom du conteneur tooget hello : recherchez votre compte de stockage, sélectionnez **BLOB**, sélectionnez nom hello de conteneur hello contenu tooupload hello.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-169">tooget hello container name: find your storage account, select **Blobs**, select hello name of hello container you want tooupload hello content into.</span></span> 

    <span data-ttu-id="0f5cc-170">Voici la capture d’écran de hello du client de Aspera hello **Gestionnaire de connexions** où vous devez spécifier le type de stockage 'Azure' hello et informations d’identification ainsi que de conteneur d’objets blob hello.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-170">Below is hello screenshot of hello Aspera client **Connection Manager** where you must specify hello 'Azure' storage type and credentials as well as hello blob container.</span></span>

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a><span data-ttu-id="0f5cc-172">Ressources</span><span class="sxs-lookup"><span data-stu-id="0f5cc-172">Resources</span></span>

<span data-ttu-id="0f5cc-173">Hello suivant des ressources ont été mentionné dans cet article.</span><span class="sxs-lookup"><span data-stu-id="0f5cc-173">hello following resources were mentioned in this article.</span></span> 

* [<span data-ttu-id="0f5cc-174">Plug-in de connexion de navigateur</span><span class="sxs-lookup"><span data-stu-id="0f5cc-174">Connect Browser Plugin</span></span>](http://downloads.asperasoft.com/connect2/)
* [<span data-ttu-id="0f5cc-175">Guide de connexion</span><span class="sxs-lookup"><span data-stu-id="0f5cc-175">Connect Guide</span></span>](http://downloads.asperasoft.com/en/documentation/8)
* [<span data-ttu-id="0f5cc-176">Client Aspera</span><span class="sxs-lookup"><span data-stu-id="0f5cc-176">Aspera Client</span></span>](http://downloads.asperasoft.com/en/downloads/2)
* [<span data-ttu-id="0f5cc-177">Guide client</span><span class="sxs-lookup"><span data-stu-id="0f5cc-177">Client Guide</span></span>](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a><span data-ttu-id="0f5cc-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0f5cc-178">Next steps</span></span>

<span data-ttu-id="0f5cc-179">Vous pouvez désormais [copier des objets blob d’un compte de stockage dans un compte AMS](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span><span class="sxs-lookup"><span data-stu-id="0f5cc-179">You can now [copy blobs from a storage account into an AMS account ](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="0f5cc-180">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="0f5cc-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0f5cc-181">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="0f5cc-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

