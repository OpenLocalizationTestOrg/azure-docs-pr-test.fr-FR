---
title: "Ajouter le connecteur Stockage Blob Azure à vos applications logiques | Microsoft Docs"
description: Prise en main et configuration du connecteur Stockage Blob Azure dans une application logique
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5dc3f75-6bea-420b-b250-183668d2848d
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/02/2017
ms.author: mandia; ladocs
ms.openlocfilehash: bc7908868828bd1628633cf9e57f8c44f8000827
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-blob-storage-connector-in-a-logic-app"></a><span data-ttu-id="21cb2-103">Utilisation du connecteur Stockage Blob Azure dans une application logique</span><span class="sxs-lookup"><span data-stu-id="21cb2-103">Use the Azure blob storage connector in a logic app</span></span>
<span data-ttu-id="21cb2-104">Le connecteur Stockage Blob Azure permet de télécharger, de mettre à jour, d’obtenir et de supprimer des objets blob dans votre compte de stockage, le tout au sein d’une application logique.</span><span class="sxs-lookup"><span data-stu-id="21cb2-104">Use the Azure Blob storage connector to upload, update, get, and delete blobs in your storage account, all within a logic app.</span></span>  

<span data-ttu-id="21cb2-105">Avec Azure Blob Storage, vous pouvez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="21cb2-105">With Azure blob storage, you:</span></span>

* <span data-ttu-id="21cb2-106">Créez votre workflow en téléchargeant les nouveaux projets ou en extrayant les fichiers récemment mis à jour.</span><span class="sxs-lookup"><span data-stu-id="21cb2-106">Build your workflow by uploading new projects, or getting files that have been recently updated.</span></span>
* <span data-ttu-id="21cb2-107">Utilisez des actions pour obtenir les métadonnées d’un fichier, supprimer un fichier, copier des fichiers, etc.</span><span class="sxs-lookup"><span data-stu-id="21cb2-107">Use actions to get file metadata, delete a file, copy files, and more.</span></span> <span data-ttu-id="21cb2-108">Par exemple, lorsqu’un outil est mis à jour dans un site web Azure (déclencheur), vous pouvez mettre à jour un fichier dans le stockage blob (action).</span><span class="sxs-lookup"><span data-stu-id="21cb2-108">For example, when a tool is updated in an Azure web site (a trigger), then update a file in blob storage (an action).</span></span> 

<span data-ttu-id="21cb2-109">Cette rubrique décrit comment utiliser le connecteur de stockage blob dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="21cb2-109">This topic shows you how to use the blob storage connector in a logic app.</span></span>

<span data-ttu-id="21cb2-110">Pour plus d’informations sur Logic Apps, voir [Qu’est-ce qu’une application logique ?](../logic-apps/logic-apps-what-are-logic-apps.md) et [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="21cb2-110">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<span data-ttu-id="21cb2-111">Pour plus d’informations sur Logic Apps, voir [Qu’est-ce qu’une application logique ?](../logic-apps/logic-apps-what-are-logic-apps.md) et [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="21cb2-111">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-azure-blob-storage"></a><span data-ttu-id="21cb2-112">Connexion au stockage d’objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="21cb2-112">Connect to Azure blob storage</span></span>
<span data-ttu-id="21cb2-113">Pour que votre application logique puisse accéder à un service, vous devez d’abord créer une *connexion* à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="21cb2-113">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="21cb2-114">Une connexion permet d’assurer la connectivité entre une application logique et un autre service.</span><span class="sxs-lookup"><span data-stu-id="21cb2-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="21cb2-115">Par exemple, pour vous connecter à un compte de stockage, commencez par créer une *connexion* de stockage des objets blob.</span><span class="sxs-lookup"><span data-stu-id="21cb2-115">For example, to connect to a storage account, you first create a blob storage *connection*.</span></span> <span data-ttu-id="21cb2-116">Pour créer une connexion, entrez les informations d’identification que vous utilisez généralement pour accéder au service auquel vous souhaitez vous connecter.</span><span class="sxs-lookup"><span data-stu-id="21cb2-116">To create a connection, enter the credentials you normally use to access the service you are connecting to.</span></span> <span data-ttu-id="21cb2-117">Ainsi, dans le cas d’Azure Storage, entrez les informations d’identification de votre compte de stockage pour créer la connexion.</span><span class="sxs-lookup"><span data-stu-id="21cb2-117">So with Azure storage, enter the credentials to your storage account to create the connection.</span></span> 

#### <a name="create-the-connection"></a><span data-ttu-id="21cb2-118">Créer la connexion</span><span class="sxs-lookup"><span data-stu-id="21cb2-118">Create the connection</span></span>
> [!INCLUDE [Create a connection to Azure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a><span data-ttu-id="21cb2-119">Utilisation d’un déclencheur</span><span class="sxs-lookup"><span data-stu-id="21cb2-119">Use a trigger</span></span>
<span data-ttu-id="21cb2-120">Ce connecteur ne possède aucun déclencheur.</span><span class="sxs-lookup"><span data-stu-id="21cb2-120">This connector does not have any triggers.</span></span> <span data-ttu-id="21cb2-121">Utilisez d’autres déclencheurs pour démarrer l’application logique, notamment un déclencheur de périodicité, un déclencheur Webhook HTTP, des déclencheurs disponibles avec d’autres connecteurs, etc.</span><span class="sxs-lookup"><span data-stu-id="21cb2-121">Use other triggers to start the logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="21cb2-122">[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md) vous fournit un exemple.</span><span class="sxs-lookup"><span data-stu-id="21cb2-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="21cb2-123">Utilisation d’une action</span><span class="sxs-lookup"><span data-stu-id="21cb2-123">Use an action</span></span>
<span data-ttu-id="21cb2-124">Une action est une opération effectuée par le flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="21cb2-124">An action is an operation carried out by the workflow defined in a logic app.</span></span>

1. <span data-ttu-id="21cb2-125">Sélectionnez le signe plus.</span><span class="sxs-lookup"><span data-stu-id="21cb2-125">Select the plus sign.</span></span> <span data-ttu-id="21cb2-126">Vous disposez de plusieurs options : **Ajouter une action**, **Ajouter une condition** ou l’une des options **Plus**.</span><span class="sxs-lookup"><span data-stu-id="21cb2-126">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. <span data-ttu-id="21cb2-127">Choisissez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="21cb2-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="21cb2-128">Dans la zone de texte, saisissez « blob » pour obtenir la liste de toutes les actions disponibles.</span><span class="sxs-lookup"><span data-stu-id="21cb2-128">In the text box, type “blob” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. <span data-ttu-id="21cb2-129">Dans notre exemple, choisissez **AzureBlob - Obtenir les métadonnées d’un fichier à l’aide du chemin**.</span><span class="sxs-lookup"><span data-stu-id="21cb2-129">In our example, choose **AzureBlob - Get file metadata using path**.</span></span> <span data-ttu-id="21cb2-130">Si une connexion existe déjà, sélectionnez le bouton **...** (Afficher le sélecteur) pour sélectionner un fichier.</span><span class="sxs-lookup"><span data-stu-id="21cb2-130">If a connection already exists, then select the **...** (Show Picker) button to select a file.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    <span data-ttu-id="21cb2-131">Si vous êtes invité à saisir les informations de connexion, entrez les informations requises pour créer la connexion.</span><span class="sxs-lookup"><span data-stu-id="21cb2-131">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="21cb2-132">La section [Créer la connexion](connectors-create-api-azureblobstorage.md#create-the-connection) dans cette rubrique décrit ces propriétés.</span><span class="sxs-lookup"><span data-stu-id="21cb2-132">[Create the connection](connectors-create-api-azureblobstorage.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="21cb2-133">Dans cet exemple, nous obtiendrons les métadonnées d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="21cb2-133">In this example, we get the metadata of a file.</span></span> <span data-ttu-id="21cb2-134">Pour consulter les métadonnées, ajoutez une autre action qui crée un nouveau fichier à l’aide d’un autre connecteur.</span><span class="sxs-lookup"><span data-stu-id="21cb2-134">To see the metadata, add another action that creates a new file using another connector.</span></span> <span data-ttu-id="21cb2-135">Par exemple, ajoutez une action OneDrive qui crée un nouveau fichier « test » basé sur les métadonnées.</span><span class="sxs-lookup"><span data-stu-id="21cb2-135">For example, add a OneDrive action that creates a new "test" file based on the metadata.</span></span> 


5. <span data-ttu-id="21cb2-136">**Enregistrez** vos modifications (dans le coin supérieur gauche de la barre d’outils).</span><span class="sxs-lookup"><span data-stu-id="21cb2-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="21cb2-137">Votre application logique est enregistrée et peut être activée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="21cb2-137">Your logic app is saved and may be automatically enabled.</span></span>

> [!TIP]
> <span data-ttu-id="21cb2-138">L’[Explorateur de stockage](http://storageexplorer.com/) est un excellent outil pour gérer plusieurs comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="21cb2-138">[Storage Explorer](http://storageexplorer.com/) is a great tool to  manage multiple storage accounts.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="21cb2-139">Détails spécifiques aux connecteurs</span><span class="sxs-lookup"><span data-stu-id="21cb2-139">Connector-specific details</span></span>

<span data-ttu-id="21cb2-140">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/azureblobconnector/).</span><span class="sxs-lookup"><span data-stu-id="21cb2-140">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/azureblobconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="21cb2-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="21cb2-141">Next steps</span></span>
<span data-ttu-id="21cb2-142">[Créez une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="21cb2-142">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="21cb2-143">Explorez les autres connecteurs disponibles dans les applications logiques en consultant notre [liste d’API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="21cb2-143">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

