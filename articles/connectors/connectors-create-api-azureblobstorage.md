---
title: "aaaAdd hello stockage d’objets blob Azure dans vos applications de la logique d’un connecteur | Documents Microsoft"
description: "Prise en main et de configurer le connecteur de stockage d’objets blob Azure hello dans une application de logique"
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
ms.openlocfilehash: add61287ef1b2228ef9d3f54ce082807bad6858b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-blob-storage-connector-in-a-logic-app"></a><span data-ttu-id="e5d0c-103">Utiliser le connecteur de stockage d’objets blob Azure hello dans une application de logique</span><span class="sxs-lookup"><span data-stu-id="e5d0c-103">Use hello Azure blob storage connector in a logic app</span></span>
<span data-ttu-id="e5d0c-104">Tooupload de connecteur utilisez hello Azure Blob storage, mettre à jour, obtenir et supprimer des objets BLOB dans votre compte de stockage, toutes les tâches dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-104">Use hello Azure Blob storage connector tooupload, update, get, and delete blobs in your storage account, all within a logic app.</span></span>  

<span data-ttu-id="e5d0c-105">Avec Azure Blob Storage, vous pouvez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e5d0c-105">With Azure blob storage, you:</span></span>

* <span data-ttu-id="e5d0c-106">Créez votre workflow en téléchargeant les nouveaux projets ou en extrayant les fichiers récemment mis à jour.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-106">Build your workflow by uploading new projects, or getting files that have been recently updated.</span></span>
* <span data-ttu-id="e5d0c-107">Utilisez les métadonnées du fichier actions tooget, supprimer un fichier, copier les fichiers et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-107">Use actions tooget file metadata, delete a file, copy files, and more.</span></span> <span data-ttu-id="e5d0c-108">Par exemple, lorsqu’un outil est mis à jour dans un site web Azure (déclencheur), vous pouvez mettre à jour un fichier dans le stockage blob (action).</span><span class="sxs-lookup"><span data-stu-id="e5d0c-108">For example, when a tool is updated in an Azure web site (a trigger), then update a file in blob storage (an action).</span></span> 

<span data-ttu-id="e5d0c-109">Cette rubrique vous montre comment toouse hello blob connecteur dans une application de la logique de stockage.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-109">This topic shows you how toouse hello blob storage connector in a logic app.</span></span>

<span data-ttu-id="e5d0c-110">toolearn en savoir plus sur les applications de la logique, consultez [quelles sont les applications logique](../logic-apps/logic-apps-what-are-logic-apps.md) et [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e5d0c-110">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<span data-ttu-id="e5d0c-111">toolearn en savoir plus sur les applications de la logique, consultez [quelles sont les applications logique](../logic-apps/logic-apps-what-are-logic-apps.md) et [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e5d0c-111">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooazure-blob-storage"></a><span data-ttu-id="e5d0c-112">Connecter le stockage d’objets blob tooAzure</span><span class="sxs-lookup"><span data-stu-id="e5d0c-112">Connect tooAzure blob storage</span></span>
<span data-ttu-id="e5d0c-113">Avant que votre application logique peut accéder à n’importe quel service, vous créez tout d’abord un *connexion* toohello service.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-113">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="e5d0c-114">Une connexion permet d’assurer la connectivité entre une application logique et un autre service.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="e5d0c-115">Par exemple, le compte de stockage tooconnect tooa vous tout d’abord créez un stockage d’objets blob *connexion*.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-115">For example, tooconnect tooa storage account, you first create a blob storage *connection*.</span></span> <span data-ttu-id="e5d0c-116">toocreate une connexion, entrez des informations d’identification de hello que vous utilisez normalement le service de hello tooaccess vous êtes connecté.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-116">toocreate a connection, enter hello credentials you normally use tooaccess hello service you are connecting to.</span></span> <span data-ttu-id="e5d0c-117">Par conséquent, avec le stockage Azure, entrez connexion hello de hello informations d’identification tooyour stockage compte toocreate.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-117">So with Azure storage, enter hello credentials tooyour storage account toocreate hello connection.</span></span> 

#### <a name="create-hello-connection"></a><span data-ttu-id="e5d0c-118">Créer la connexion de hello</span><span class="sxs-lookup"><span data-stu-id="e5d0c-118">Create hello connection</span></span>
> [!INCLUDE [Create a connection tooAzure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a><span data-ttu-id="e5d0c-119">Utilisation d’un déclencheur</span><span class="sxs-lookup"><span data-stu-id="e5d0c-119">Use a trigger</span></span>
<span data-ttu-id="e5d0c-120">Ce connecteur ne possède aucun déclencheur.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-120">This connector does not have any triggers.</span></span> <span data-ttu-id="e5d0c-121">Utilisez l’autre application logique de déclencheurs toostart hello, comme un déclencheur de périodicité, un déclencheur HTTP Webhook, déclencheurs disponibles avec tous les autres connecteurs et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-121">Use other triggers toostart hello logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="e5d0c-122">[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md) vous fournit un exemple.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="e5d0c-123">Utilisation d’une action</span><span class="sxs-lookup"><span data-stu-id="e5d0c-123">Use an action</span></span>
<span data-ttu-id="e5d0c-124">Une action est une opération effectuée par flux de travail hello défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-124">An action is an operation carried out by hello workflow defined in a logic app.</span></span>

1. <span data-ttu-id="e5d0c-125">Sélectionnez le signe plus hello.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-125">Select hello plus sign.</span></span> <span data-ttu-id="e5d0c-126">Vous voyez plusieurs choix : **ajouter une action**, **ajouter une condition**, ou l’un des hello **plus** options.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-126">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. <span data-ttu-id="e5d0c-127">Choisissez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="e5d0c-128">Dans la zone de texte hello, tapez « blob » tooget une liste de toutes les actions disponibles hello.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-128">In hello text box, type “blob” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. <span data-ttu-id="e5d0c-129">Dans notre exemple, choisissez **AzureBlob - Obtenir les métadonnées d’un fichier à l’aide du chemin**.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-129">In our example, choose **AzureBlob - Get file metadata using path**.</span></span> <span data-ttu-id="e5d0c-130">Si une connexion existe déjà, puis sélectionnez hello **...** Tooselect de bouton (Afficher sélecteur) un fichier.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-130">If a connection already exists, then select hello **...** (Show Picker) button tooselect a file.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    <span data-ttu-id="e5d0c-131">Si vous êtes invité hello informations de connexion, puis entrez connexion de hello toocreate hello détails.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-131">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="e5d0c-132">[Créer la connexion de hello](connectors-create-api-azureblobstorage.md#create-the-connection) dans cette rubrique décrit ces propriétés.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-132">[Create hello connection](connectors-create-api-azureblobstorage.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="e5d0c-133">Dans cet exemple, nous obtenons hello les métadonnées d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-133">In this example, we get hello metadata of a file.</span></span> <span data-ttu-id="e5d0c-134">toosee hello des métadonnées, ajoutez une autre action qui crée un nouveau fichier à l’aide d’un autre connecteur.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-134">toosee hello metadata, add another action that creates a new file using another connector.</span></span> <span data-ttu-id="e5d0c-135">Par exemple, ajouter une action OneDrive qui crée un nouveau fichier de « test » en fonction de métadonnées de hello.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-135">For example, add a OneDrive action that creates a new "test" file based on hello metadata.</span></span> 


5. <span data-ttu-id="e5d0c-136">**Enregistrer** vos modifications (situé dans l’angle supérieur gauche de la barre d’outils hello).</span><span class="sxs-lookup"><span data-stu-id="e5d0c-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="e5d0c-137">Votre application logique est enregistrée et peut être activée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-137">Your logic app is saved and may be automatically enabled.</span></span>

> [!TIP]
> <span data-ttu-id="e5d0c-138">[Explorateur de stockage](http://storageexplorer.com/) est un excellent outil gérer trop de plusieurs comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="e5d0c-138">[Storage Explorer](http://storageexplorer.com/) is a great tool too manage multiple storage accounts.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="e5d0c-139">Détails spécifiques du connecteur</span><span class="sxs-lookup"><span data-stu-id="e5d0c-139">Connector-specific details</span></span>

<span data-ttu-id="e5d0c-140">Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/azureblobconnector/).</span><span class="sxs-lookup"><span data-stu-id="e5d0c-140">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/azureblobconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e5d0c-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e5d0c-141">Next steps</span></span>
<span data-ttu-id="e5d0c-142">[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e5d0c-142">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="e5d0c-143">Explorer hello tous les autres connecteurs disponibles dans les applications logique à notre [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="e5d0c-143">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

