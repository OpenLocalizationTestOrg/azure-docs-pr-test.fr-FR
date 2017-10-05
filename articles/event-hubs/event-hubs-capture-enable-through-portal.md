---
title: "Activer Azure Event Hubs Capture à l’aide du portail | Microsoft Docs"
description: "Activez la fonctionnalité Event Hubs Capture à l’aide du portail Azure."
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
ms.openlocfilehash: 0cbf45dce922647f2996f929d2c7cf885a2f4db4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="enable-event-hubs-capture-using-the-azure-portal"></a><span data-ttu-id="ec557-103">Activer Event Hubs Capture à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="ec557-103">Enable Event Hubs Capture using the Azure portal</span></span>

<span data-ttu-id="ec557-104">Vous pouvez configurer la fonctionnalité Capture lors de la création du concentrateur d’événements, à l’aide du [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ec557-104">You can configure Capture at the event hub creation time using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ec557-105">Vous pouvez capturer les données vers un conteneur de [Stockage Blob](https://azure.microsoft.com/services/storage/blobs/) Azure, ou vers un compte [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span><span class="sxs-lookup"><span data-stu-id="ec557-105">You can either capture the data to an Azure [Blob storage](https://azure.microsoft.com/services/storage/blobs/) container, or to an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account.</span></span>

## <a name="capture-data-to-an-azure-storage-account"></a><span data-ttu-id="ec557-106">Capturer des données vers un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="ec557-106">Capture data to an Azure Storage account</span></span>  

<span data-ttu-id="ec557-107">Lorsque vous créez un concentrateur d’événements, vous pouvez activer la Capture en cliquant sur le **sur** situé dans le **concentrateur d’événements créer** panneau portail.</span><span class="sxs-lookup"><span data-stu-id="ec557-107">When you create an event hub, you can enable Capture by clicking the **On** button in the **Create Event Hub** portal blade.</span></span> <span data-ttu-id="ec557-108">Précisez ensuite le compte et le conteneur de stockage à utiliser en cliquant sur **Stockage Azure** dans la zone **Fournisseur de capture**.</span><span class="sxs-lookup"><span data-stu-id="ec557-108">You then specify a Storage Account and container by clicking **Azure Storage** in the **Capture Provider** box.</span></span> <span data-ttu-id="ec557-109">Comme Event Hubs Capture utilise l’authentification de service à service avec le stockage, il est inutile de spécifier une chaîne de connexion de stockage.</span><span class="sxs-lookup"><span data-stu-id="ec557-109">Because Event Hubs Capture uses service-to-service authentication with storage, you do not need to specify a storage connection string.</span></span> <span data-ttu-id="ec557-110">Le sélecteur de ressources sélectionne automatiquement l’URI de ressource pour votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ec557-110">The resource picker selects the resource URI for your storage account automatically.</span></span> <span data-ttu-id="ec557-111">Si vous utilisez Azure Resource Manager, vous devez fournir explicitement cet URI en tant que chaîne.</span><span class="sxs-lookup"><span data-stu-id="ec557-111">If you use Azure Resource Manager, you must supply this URI explicitly as a string.</span></span>

<span data-ttu-id="ec557-112">La fenêtre temporelle par défaut est de cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="ec557-112">The default time window is 5 minutes.</span></span> <span data-ttu-id="ec557-113">La valeur minimum est 1, la valeur maximum 15.</span><span class="sxs-lookup"><span data-stu-id="ec557-113">The minimum value is 1, the maximum 15.</span></span> <span data-ttu-id="ec557-114">La fenêtre **Taille** présente une plage de 10 à 500 Mo.</span><span class="sxs-lookup"><span data-stu-id="ec557-114">The **Size** window has a range of 10-500 MB.</span></span>

![][1]

## <a name="capture-data-to-an-azure-data-lake-store-account"></a><span data-ttu-id="ec557-115">Capturer des données vers un compte Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ec557-115">Capture data to an Azure Data Lake Store account</span></span>

<span data-ttu-id="ec557-116">Pour capturer des données vers Azure Data Lake Store, vous créez un compte Data Lake Store et un concentrateur d’événements :</span><span class="sxs-lookup"><span data-stu-id="ec557-116">To capture data to Azure Data Lake Store, you create a Data Lake Store account, and an event hub:</span></span>

### <a name="create-an-azure-data-lake-store-account-and-folders"></a><span data-ttu-id="ec557-117">Créer un compte Azure Data Lake Store et des dossiers</span><span class="sxs-lookup"><span data-stu-id="ec557-117">Create an Azure Data Lake Store account and folders</span></span>

1. <span data-ttu-id="ec557-118">Pour créer un compte Data Lake Store, suivez les instructions de [Prise en main d’Azure Data Lake Store avec le portail Azure](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ec557-118">Create a Data Lake Store account, following the instructions in [Get started with Azure Data Lake Store using the Azure portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span> 
2. <span data-ttu-id="ec557-119">Pour créer un dossier dans ce compte, suivez les instructions dans la section [Créer des dossiers dans un compte Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md#createfolder).</span><span class="sxs-lookup"><span data-stu-id="ec557-119">Create a folder under this account, following the instructions in the [Create folders in Azure Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) section.</span></span>
3. <span data-ttu-id="ec557-120">Dans le panneau de compte Data Lake Store, cliquez sur **Explorateur de données**.</span><span class="sxs-lookup"><span data-stu-id="ec557-120">In the Data Lake Store account blade, click **Data Explorer**.</span></span>
4. <span data-ttu-id="ec557-121">Cliquez sur **Access** (Accès).</span><span class="sxs-lookup"><span data-stu-id="ec557-121">Click **Access**.</span></span>
5. <span data-ttu-id="ec557-122">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="ec557-122">Click **Add**.</span></span>
6. <span data-ttu-id="ec557-123">Dans la zone **Search by name or email**(Recherche par nom ou e-mail), tapez **Microsoft.EventHubs** et sélectionnez cette option.</span><span class="sxs-lookup"><span data-stu-id="ec557-123">In the **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span> 
7. <span data-ttu-id="ec557-124">L’onglet **Permissions** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ec557-124">The **Permissions** tab appears.</span></span> <span data-ttu-id="ec557-125">Définissez les autorisations comme indiqué dans la figure suivante :</span><span class="sxs-lookup"><span data-stu-id="ec557-125">Set the permissions as shown in the following figure:</span></span>

    ![][6]

8. <span data-ttu-id="ec557-126">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ec557-126">Click **OK**.</span></span>
9. <span data-ttu-id="ec557-127">Créez maintenant un dossier dans le dossier racine en naviguant vers le dossier cible et en cliquant sur son nom.</span><span class="sxs-lookup"><span data-stu-id="ec557-127">Now, create a folder in the root folder by browsing to the target folder and clicking on the folder name.</span></span>
10. <span data-ttu-id="ec557-128">Cliquez sur **Access** (Accès).</span><span class="sxs-lookup"><span data-stu-id="ec557-128">Click **Access**.</span></span>
11. <span data-ttu-id="ec557-129">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="ec557-129">Click **Add**.</span></span>
12. <span data-ttu-id="ec557-130">Dans la zone **Search by name or email**(Recherche par nom ou e-mail), tapez **Microsoft.EventHubs** et sélectionnez cette option.</span><span class="sxs-lookup"><span data-stu-id="ec557-130">In the **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span>
13. <span data-ttu-id="ec557-131">L’onglet **Permissions** s’affiche de nouveau.</span><span class="sxs-lookup"><span data-stu-id="ec557-131">The **Permissions** tab appears again.</span></span> <span data-ttu-id="ec557-132">Définissez les autorisations comme indiqué dans la figure suivante :</span><span class="sxs-lookup"><span data-stu-id="ec557-132">Set the permissions as shown in the following figure:</span></span>

    ![][5]

### <a name="create-an-event-hub"></a><span data-ttu-id="ec557-133">Création d'un concentrateur d'événements</span><span class="sxs-lookup"><span data-stu-id="ec557-133">Create an event hub</span></span>

1. <span data-ttu-id="ec557-134">Remarque : le concentrateur d’événements doit se trouver dans le même abonnement Azure que le compte Azure Data Lake Store que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="ec557-134">Note that the event hub must be in the same Azure subscription as the Azure Data Lake Store you just created.</span></span> <span data-ttu-id="ec557-135">Créer le concentrateur d’événements, en cliquant sur le **sur** sous **capturer** dans les **concentrateur d’événements créer** panneau portail.</span><span class="sxs-lookup"><span data-stu-id="ec557-135">Create the event hub, clicking the **On** button under **Capture** in the **Create Event Hub** portal blade.</span></span> 
2. <span data-ttu-id="ec557-136">Dans le **concentrateur d’événements créer** portail panneau, sélectionnez **Azure Data Lake Store** à partir de la **capturer le fournisseur** boîte.</span><span class="sxs-lookup"><span data-stu-id="ec557-136">In the **Create Event Hub** portal blade, select **Azure Data Lake Store** from the **Capture Provider** box.</span></span>
3. <span data-ttu-id="ec557-137">Dans **Sélectionner Data Lake Store**, spécifiez le compte Data Lake Store que vous avez créé précédemment, puis entrez le chemin d’accès au dossier de données que vous avez créé dans le champ **Chemin d’accès Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="ec557-137">In **Select Data Lake Store**, specify the Data Lake Store account you created previously, and in the **Data Lake Path** field, enter the path to the data folder you created.</span></span>

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a><span data-ttu-id="ec557-138">Ajouter ou configurer la fonctionnalité Capture sur un concentrateur d’événements existant</span><span class="sxs-lookup"><span data-stu-id="ec557-138">Add or configure Capture on an existing event hub</span></span>

<span data-ttu-id="ec557-139">Vous pouvez configurer la fonctionnalité Capture sur des concentrateurs d’événements se trouvant dans des espaces de noms Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="ec557-139">You can configure Capture on existing event hubs that are in Event Hubs namespaces.</span></span> <span data-ttu-id="ec557-140">Pour activer Capture sur un concentrateur d’événements existant, ou pour modifier les paramètres de cette fonctionnalité, cliquez sur l’espace de noms afin de charger le panneau **Essentials**, puis cliquez sur le concentrateur d’événements pour lequel vous souhaitez activer ou modifier la configuration de Capture.</span><span class="sxs-lookup"><span data-stu-id="ec557-140">To enable Capture on an existing event hub, or to change your Capture settings, click the namespace to load the **Essentials** blade, then click the event hub for which you want to enable or change the Capture setting.</span></span> <span data-ttu-id="ec557-141">Enfin, cliquez sur le **propriétés** section du panneau ouvert, puis modifiez les paramètres de Capture, comme indiqué dans les figures suivantes :</span><span class="sxs-lookup"><span data-stu-id="ec557-141">Finally, click the **Properties** section of the open blade and then edit the Capture settings, as shown in the following figures:</span></span>

### <a name="azure-blob-storage"></a><span data-ttu-id="ec557-142">un stockage Azure Blob</span><span class="sxs-lookup"><span data-stu-id="ec557-142">Azure Blob Storage</span></span>

![][2]

### <a name="azure-data-lake-store"></a><span data-ttu-id="ec557-143">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ec557-143">Azure Data Lake Store</span></span>

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a><span data-ttu-id="ec557-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ec557-144">Next steps</span></span>

<span data-ttu-id="ec557-145">Vous pouvez également configurer Event Hubs Capture via des modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ec557-145">You can also configure Event Hubs Capture using Azure Resource Manager templates.</span></span> <span data-ttu-id="ec557-146">Pour en savoir plus, consultez la section relative à [l’activation de Capture à l’aide d’un modèle Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span><span class="sxs-lookup"><span data-stu-id="ec557-146">For more information, see [Enable Capture using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span></span>
