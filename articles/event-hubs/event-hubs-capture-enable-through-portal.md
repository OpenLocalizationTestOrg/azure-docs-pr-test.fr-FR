---
title: "Activer l’aaaAzure capturer des concentrateurs d’événements via le portail | Documents Microsoft"
description: "Activer hello capturer des concentrateurs d’événements à l’aide de hello portail Azure."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: 27c7528552c497a4d98873a22bd56a991c66247c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-event-hubs-capture-using-hello-azure-portal"></a><span data-ttu-id="22f83-103">Activer la Capture de concentrateurs d’événements à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="22f83-103">Enable Event Hubs Capture using hello Azure portal</span></span>

<span data-ttu-id="22f83-104">Vous pouvez configurer la Capture au moment de la création du hub d’événements hello à l’aide de hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="22f83-104">You can configure Capture at hello event hub creation time using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="22f83-105">Vous pouvez soit tooan de données capture hello Azure [stockage d’objets Blob](https://azure.microsoft.com/services/storage/blobs/) conteneur ou tooan [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) compte.</span><span class="sxs-lookup"><span data-stu-id="22f83-105">You can either capture hello data tooan Azure [Blob storage](https://azure.microsoft.com/services/storage/blobs/) container, or tooan [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account.</span></span>

## <a name="capture-data-tooan-azure-storage-account"></a><span data-ttu-id="22f83-106">Compte de stockage Azure tooan de données de capture</span><span class="sxs-lookup"><span data-stu-id="22f83-106">Capture data tooan Azure Storage account</span></span>  

<span data-ttu-id="22f83-107">Lorsque vous créez un concentrateur d’événements, vous pouvez activer la Capture en cliquant sur hello **sur** bouton Bonjour **concentrateur d’événements créer** panneau portail.</span><span class="sxs-lookup"><span data-stu-id="22f83-107">When you create an event hub, you can enable Capture by clicking hello **On** button in hello **Create Event Hub** portal blade.</span></span> <span data-ttu-id="22f83-108">Puis vous spécifiez un compte de stockage et un conteneur en cliquant sur **Azure Storage** Bonjour **capturer le fournisseur** boîte.</span><span class="sxs-lookup"><span data-stu-id="22f83-108">You then specify a Storage Account and container by clicking **Azure Storage** in hello **Capture Provider** box.</span></span> <span data-ttu-id="22f83-109">Comme capturer des concentrateurs d’événements d’utilise l’authentification de service avec le stockage, vous n’avez pas besoin de toospecify une chaîne de connexion de stockage.</span><span class="sxs-lookup"><span data-stu-id="22f83-109">Because Event Hubs Capture uses service-to-service authentication with storage, you do not need toospecify a storage connection string.</span></span> <span data-ttu-id="22f83-110">Sélecteur de ressources Hello sélectionne automatiquement les URI de ressource hello pour votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="22f83-110">hello resource picker selects hello resource URI for your storage account automatically.</span></span> <span data-ttu-id="22f83-111">Si vous utilisez Azure Resource Manager, vous devez fournir explicitement cet URI en tant que chaîne.</span><span class="sxs-lookup"><span data-stu-id="22f83-111">If you use Azure Resource Manager, you must supply this URI explicitly as a string.</span></span>

<span data-ttu-id="22f83-112">fenêtre Hello par défaut est de 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="22f83-112">hello default time window is 5 minutes.</span></span> <span data-ttu-id="22f83-113">valeur minimale de Hello est 1, hello 15 maximale.</span><span class="sxs-lookup"><span data-stu-id="22f83-113">hello minimum value is 1, hello maximum 15.</span></span> <span data-ttu-id="22f83-114">Hello **taille** fenêtre a une plage de 10 à 500 Mo.</span><span class="sxs-lookup"><span data-stu-id="22f83-114">hello **Size** window has a range of 10-500 MB.</span></span>

![][1]

## <a name="capture-data-tooan-azure-data-lake-store-account"></a><span data-ttu-id="22f83-115">Données tooan Azure Data Lake Store compte de capture</span><span class="sxs-lookup"><span data-stu-id="22f83-115">Capture data tooan Azure Data Lake Store account</span></span>

<span data-ttu-id="22f83-116">tooAzure de données toocapture Data Lake Store, vous créez un compte Data Lake Store et un concentrateur d’événements :</span><span class="sxs-lookup"><span data-stu-id="22f83-116">toocapture data tooAzure Data Lake Store, you create a Data Lake Store account, and an event hub:</span></span>

### <a name="create-an-azure-data-lake-store-account-and-folders"></a><span data-ttu-id="22f83-117">Créer un compte Azure Data Lake Store et des dossiers</span><span class="sxs-lookup"><span data-stu-id="22f83-117">Create an Azure Data Lake Store account and folders</span></span>

1. <span data-ttu-id="22f83-118">Créer un compte Data Lake Store, conformément aux instructions hello [prise en main Azure Data Lake Store à l’aide de hello Azure portal](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="22f83-118">Create a Data Lake Store account, following hello instructions in [Get started with Azure Data Lake Store using hello Azure portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span> 
2. <span data-ttu-id="22f83-119">Créez un dossier sous ce compte, en suivant les instructions de hello Bonjour [créer des dossiers dans un compte Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) section.</span><span class="sxs-lookup"><span data-stu-id="22f83-119">Create a folder under this account, following hello instructions in hello [Create folders in Azure Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) section.</span></span>
3. <span data-ttu-id="22f83-120">Dans le panneau de compte Data Lake Store hello, cliquez sur **Explorateur de données**.</span><span class="sxs-lookup"><span data-stu-id="22f83-120">In hello Data Lake Store account blade, click **Data Explorer**.</span></span>
4. <span data-ttu-id="22f83-121">Cliquez sur **Access** (Accès).</span><span class="sxs-lookup"><span data-stu-id="22f83-121">Click **Access**.</span></span>
5. <span data-ttu-id="22f83-122">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="22f83-122">Click **Add**.</span></span>
6. <span data-ttu-id="22f83-123">Bonjour **recherche par nom ou par courrier électronique** zone **Microsoft.EventHubs** , puis sélectionnez cette option.</span><span class="sxs-lookup"><span data-stu-id="22f83-123">In hello **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span> 
7. <span data-ttu-id="22f83-124">Hello **autorisations** onglet s’affiche.</span><span class="sxs-lookup"><span data-stu-id="22f83-124">hello **Permissions** tab appears.</span></span> <span data-ttu-id="22f83-125">Définir des autorisations de hello comme indiqué dans la figure suivante de hello :</span><span class="sxs-lookup"><span data-stu-id="22f83-125">Set hello permissions as shown in hello following figure:</span></span>

    ![][6]

8. <span data-ttu-id="22f83-126">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="22f83-126">Click **OK**.</span></span>
9. <span data-ttu-id="22f83-127">À présent, créez un dossier dans le dossier racine de hello en dossier cible de toohello de navigation en cliquant sur le nom du dossier hello.</span><span class="sxs-lookup"><span data-stu-id="22f83-127">Now, create a folder in hello root folder by browsing toohello target folder and clicking on hello folder name.</span></span>
10. <span data-ttu-id="22f83-128">Cliquez sur **Access** (Accès).</span><span class="sxs-lookup"><span data-stu-id="22f83-128">Click **Access**.</span></span>
11. <span data-ttu-id="22f83-129">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="22f83-129">Click **Add**.</span></span>
12. <span data-ttu-id="22f83-130">Bonjour **recherche par nom ou par courrier électronique** zone **Microsoft.EventHubs** , puis sélectionnez cette option.</span><span class="sxs-lookup"><span data-stu-id="22f83-130">In hello **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span>
13. <span data-ttu-id="22f83-131">Hello **autorisations** onglet s’affiche à nouveau.</span><span class="sxs-lookup"><span data-stu-id="22f83-131">hello **Permissions** tab appears again.</span></span> <span data-ttu-id="22f83-132">Définir des autorisations de hello comme indiqué dans la figure suivante de hello :</span><span class="sxs-lookup"><span data-stu-id="22f83-132">Set hello permissions as shown in hello following figure:</span></span>

    ![][5]

### <a name="create-an-event-hub"></a><span data-ttu-id="22f83-133">Création d'un concentrateur d'événements</span><span class="sxs-lookup"><span data-stu-id="22f83-133">Create an event hub</span></span>

1. <span data-ttu-id="22f83-134">Notez ce concentrateur d’événements hello doit être Bonjour même abonnement Azure que hello Azure Data Lake Store que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="22f83-134">Note that hello event hub must be in hello same Azure subscription as hello Azure Data Lake Store you just created.</span></span> <span data-ttu-id="22f83-135">Concentrateur d’événements hello créer, en cliquant sur hello **sur** sous **Capture** Bonjour **concentrateur d’événements créer** panneau portail.</span><span class="sxs-lookup"><span data-stu-id="22f83-135">Create hello event hub, clicking hello **On** button under **Capture** in hello **Create Event Hub** portal blade.</span></span> 
2. <span data-ttu-id="22f83-136">Bonjour **concentrateur d’événements créer** portail panneau, sélectionnez **Azure Data Lake Store** de hello **capturer le fournisseur** boîte.</span><span class="sxs-lookup"><span data-stu-id="22f83-136">In hello **Create Event Hub** portal blade, select **Azure Data Lake Store** from hello **Capture Provider** box.</span></span>
3. <span data-ttu-id="22f83-137">Dans **sélectionnez Data Lake Store**, spécifiez hello compte Data Lake Store que vous avez créé précédemment et hello **le chemin d’accès de données Lake** , entrez le dossier de données hello chemin d’accès toohello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="22f83-137">In **Select Data Lake Store**, specify hello Data Lake Store account you created previously, and in hello **Data Lake Path** field, enter hello path toohello data folder you created.</span></span>

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a><span data-ttu-id="22f83-138">Ajouter ou configurer la fonctionnalité Capture sur un concentrateur d’événements existant</span><span class="sxs-lookup"><span data-stu-id="22f83-138">Add or configure Capture on an existing event hub</span></span>

<span data-ttu-id="22f83-139">Vous pouvez configurer la fonctionnalité Capture sur des concentrateurs d’événements se trouvant dans des espaces de noms Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="22f83-139">You can configure Capture on existing event hubs that are in Event Hubs namespaces.</span></span> <span data-ttu-id="22f83-140">tooenable de Capture sur un concentrateur d’événements existant, ou toochange vos paramètres de Capture, cliquez sur Bonjour, espace de noms Bonjour tooload **Essentials** panneau, puis cliquez sur le concentrateur d’événements hello pour lequel vous voulez tooenable ou modifiez le paramètre de Capture hello.</span><span class="sxs-lookup"><span data-stu-id="22f83-140">tooenable Capture on an existing event hub, or toochange your Capture settings, click hello namespace tooload hello **Essentials** blade, then click hello event hub for which you want tooenable or change hello Capture setting.</span></span> <span data-ttu-id="22f83-141">Enfin, cliquez sur hello **propriétés** section Hello ouvrir le panneau et puis modifiez les paramètres de Capture hello, comme indiqué dans hello suivant chiffres :</span><span class="sxs-lookup"><span data-stu-id="22f83-141">Finally, click hello **Properties** section of hello open blade and then edit hello Capture settings, as shown in hello following figures:</span></span>

### <a name="azure-blob-storage"></a><span data-ttu-id="22f83-142">un stockage Azure Blob</span><span class="sxs-lookup"><span data-stu-id="22f83-142">Azure Blob Storage</span></span>

![][2]

### <a name="azure-data-lake-store"></a><span data-ttu-id="22f83-143">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="22f83-143">Azure Data Lake Store</span></span>

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a><span data-ttu-id="22f83-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="22f83-144">Next steps</span></span>

<span data-ttu-id="22f83-145">Vous pouvez également configurer Event Hubs Capture via des modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="22f83-145">You can also configure Event Hubs Capture using Azure Resource Manager templates.</span></span> <span data-ttu-id="22f83-146">Pour en savoir plus, consultez la section relative à [l’activation de Capture à l’aide d’un modèle Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span><span class="sxs-lookup"><span data-stu-id="22f83-146">For more information, see [Enable Capture using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span></span>
