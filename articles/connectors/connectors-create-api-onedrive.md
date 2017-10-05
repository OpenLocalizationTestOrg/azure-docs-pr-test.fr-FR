---
title: "Ajouter le connecteur OneDrive à vos applications logiques | Microsoft Docs"
description: "Vue d’ensemble du connecteur OneDrive avec les paramètres de l’API REST"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 47a8582a-1b1a-4fc3-beb5-97c60c4306fe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 63bd33bf4e09b98aa53dcfec9fcc4a0109204952
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-onedrive-connector"></a><span data-ttu-id="d6506-103">Prise en main du connecteur OneDrive</span><span class="sxs-lookup"><span data-stu-id="d6506-103">Get started with the OneDrive connector</span></span>
<span data-ttu-id="d6506-104">Connexion à OneDrive pour gérer vos fichiers, y compris le téléchargement de fichiers, la suppression de fichiers, et plus encore.</span><span class="sxs-lookup"><span data-stu-id="d6506-104">Connect to OneDrive to manage your files, including upload, get, delete files, and more.</span></span> 

<span data-ttu-id="d6506-105">Avec OneDrive, vous pouvez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d6506-105">With OneDrive, you:</span></span> 

* <span data-ttu-id="d6506-106">Créer votre flux de travail en stockant des fichiers dans OneDrive, ou mettre à jour des fichiers existants dans OneDrive.</span><span class="sxs-lookup"><span data-stu-id="d6506-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span></span> 
* <span data-ttu-id="d6506-107">Utiliser des déclencheurs pour lancer votre flux de travail lorsqu’un fichier est créé ou mis à jour dans votre OneDrive.</span><span class="sxs-lookup"><span data-stu-id="d6506-107">Use triggers to start your workflow when a file is created or updated within your OneDrive.</span></span>
* <span data-ttu-id="d6506-108">Utiliser des actions pour créer un fichier, supprimer un fichier et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="d6506-108">Use actions to create a file, delete a file, and more.</span></span> <span data-ttu-id="d6506-109">Par exemple, lorsqu’un nouveau courrier électronique Office 365 est reçu avec une pièce jointe (déclencheur), créer un nouveau fichier dans OneDrive (action).</span><span class="sxs-lookup"><span data-stu-id="d6506-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span></span>

<span data-ttu-id="d6506-110">Cette rubrique décrit comment utiliser le connecteur OneDrive dans une application logique, et répertorie les déclencheurs et les actions.</span><span class="sxs-lookup"><span data-stu-id="d6506-110">This topic shows you how to use the OneDrive connector in a logic app, and also lists the triggers and actions.</span></span>

<span data-ttu-id="d6506-111">Pour plus d’informations sur Logic Apps, voir [Qu’est-ce qu’une application logique ?](../logic-apps/logic-apps-what-are-logic-apps.md) et [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="d6506-111">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-onedrive"></a><span data-ttu-id="d6506-112">Connexion à OneDrive</span><span class="sxs-lookup"><span data-stu-id="d6506-112">Connect to OneDrive</span></span>
<span data-ttu-id="d6506-113">Pour que votre application logique puisse accéder à un service, vous devez d’abord créer une *connexion* à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="d6506-113">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="d6506-114">Une connexion permet d’assurer la connectivité entre une application logique et un autre service.</span><span class="sxs-lookup"><span data-stu-id="d6506-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="d6506-115">Par exemple, pour vous connecter à OneDrive, vous devez préalablement disposer d’une *connexion* OneDrive.</span><span class="sxs-lookup"><span data-stu-id="d6506-115">For example, to connect to OneDrive, you first need a OneDrive *connection*.</span></span> <span data-ttu-id="d6506-116">Pour créer une connexion, entrez les informations d’identification que vous utilisez généralement pour accéder au service auquel vous souhaitez vous connecter.</span><span class="sxs-lookup"><span data-stu-id="d6506-116">To create a connection, enter the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="d6506-117">Ensuite, dans OneDrive, entrez les informations d’identification de votre compte OneDrive pour créer la connexion.</span><span class="sxs-lookup"><span data-stu-id="d6506-117">So, with OneDrive, enter the credentials to your OneDrive account  to create the connection.</span></span>

### <a name="create-the-connection"></a><span data-ttu-id="d6506-118">Créer la connexion</span><span class="sxs-lookup"><span data-stu-id="d6506-118">Create the connection</span></span>
> [!INCLUDE [Steps to create a connection to OneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="d6506-119">Utilisation d’un déclencheur</span><span class="sxs-lookup"><span data-stu-id="d6506-119">Use a trigger</span></span>
<span data-ttu-id="d6506-120">Un déclencheur est un événement qui peut être utilisé pour lancer le flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="d6506-120">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="d6506-121">Les déclencheurs « interrogent » le service à l’intervalle et à la fréquence de votre choix.</span><span class="sxs-lookup"><span data-stu-id="d6506-121">Triggers "poll" the service at an interval and frequency that you want.</span></span> <span data-ttu-id="d6506-122">[En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="d6506-122">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="d6506-123">Dans l’application logique, saisissez « onedrive » pour obtenir la liste des déclencheurs :</span><span class="sxs-lookup"><span data-stu-id="d6506-123">In the logic app, type "onedrive" to get a list of the triggers:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="d6506-124">Sélectionnez **Quand un fichier est modifié**.</span><span class="sxs-lookup"><span data-stu-id="d6506-124">Select **When a file is modified**.</span></span> <span data-ttu-id="d6506-125">Si une connexion existe déjà, sélectionnez le bouton Afficher le sélecteur pour sélectionner un dossier.</span><span class="sxs-lookup"><span data-stu-id="d6506-125">If a connection already exists, then select the Show Picker button to select a folder.</span></span>
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    <span data-ttu-id="d6506-126">Si vous êtes invité à vous connecter, entrez les informations de connexion pour créer la connexion.</span><span class="sxs-lookup"><span data-stu-id="d6506-126">If you are prompted to sign in, then enter the sign in details to create the connection.</span></span> <span data-ttu-id="d6506-127">La section [Créer la connexion](connectors-create-api-onedrive.md#create-the-connection) figurant dans cette rubrique répertorie les étapes.</span><span class="sxs-lookup"><span data-stu-id="d6506-127">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this topic lists the steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="d6506-128">Dans cet exemple, l’application logique s’exécute lorsqu’un fichier est mis à jour dans le dossier que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="d6506-128">In this example, the logic app runs when a file in the folder you choose is updated.</span></span> <span data-ttu-id="d6506-129">Pour consulter les résultats de ce déclencheur, ajoutez une autre action qui vous envoie un courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="d6506-129">To see the results of this trigger, add another action that sends you an email.</span></span> <span data-ttu-id="d6506-130">Par exemple, ajoutez l’action Office 365 Outlook *Envoyer un courrier électronique* qui vous avertit par e-mail quand un fichier est mis à jour.</span><span class="sxs-lookup"><span data-stu-id="d6506-130">For example, add the Office 365 Outlook *Send an email* action that emails you when a file is updated.</span></span> 

3. <span data-ttu-id="d6506-131">Sélectionnez le bouton **Modifier**, puis renseignez les valeurs **Fréquence** et **Intervalle**.</span><span class="sxs-lookup"><span data-stu-id="d6506-131">Select the **Edit** button and set the **Frequency** and **Interval** values.</span></span> <span data-ttu-id="d6506-132">Par exemple, si vous souhaitez que le déclencheur interroge le service toutes les 15 minutes, définissez le champ **Fréquence** sur **Minute**, et le champ **Intervalle** sur **15**.</span><span class="sxs-lookup"><span data-stu-id="d6506-132">For example, if you want the trigger to poll every 15 minutes, then set the **Frequency** to **Minute**, and set the **Interval** to **15**.</span></span> 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. <span data-ttu-id="d6506-133">**Enregistrez** vos modifications (dans le coin supérieur gauche de la barre d’outils).</span><span class="sxs-lookup"><span data-stu-id="d6506-133">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="d6506-134">Votre application logique est enregistrée et peut être activée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="d6506-134">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="d6506-135">Utilisation d’une action</span><span class="sxs-lookup"><span data-stu-id="d6506-135">Use an action</span></span>
<span data-ttu-id="d6506-136">Une action est une opération effectuée par le flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="d6506-136">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="d6506-137">[En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="d6506-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="d6506-138">Sélectionnez le signe plus.</span><span class="sxs-lookup"><span data-stu-id="d6506-138">Select the plus sign.</span></span> <span data-ttu-id="d6506-139">Vous disposez de plusieurs options : **Ajouter une action**, **Ajouter une condition** ou l’une des options **Plus**.</span><span class="sxs-lookup"><span data-stu-id="d6506-139">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. <span data-ttu-id="d6506-140">Choisissez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="d6506-140">Choose **Add an action**.</span></span>
3. <span data-ttu-id="d6506-141">Dans la zone de texte, saisissez « onedrive » pour obtenir la liste de toutes les actions disponibles.</span><span class="sxs-lookup"><span data-stu-id="d6506-141">In the text box, type “onedrive” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. <span data-ttu-id="d6506-142">Dans notre exemple, choisissez **OneDrive - Créer un fichier**.</span><span class="sxs-lookup"><span data-stu-id="d6506-142">In our example, choose **OneDrive - Create file**.</span></span> <span data-ttu-id="d6506-143">Si une connexion existe déjà, sélectionnez le **chemin du dossier** où placer le fichier, entrez le **nom de fichier** et choisissez le **contenu du fichier** souhaité :</span><span class="sxs-lookup"><span data-stu-id="d6506-143">If a connection already exists, then select the **Folder Path** to put the file, enter the **File Name**, and choose the **File Content** you want:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    <span data-ttu-id="d6506-144">Si vous êtes invité à saisir les informations de connexion, entrez les informations requises pour créer la connexion.</span><span class="sxs-lookup"><span data-stu-id="d6506-144">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="d6506-145">La section [Créer la connexion](connectors-create-api-onedrive.md#create-the-connection) figurant dans cette rubrique décrit ces propriétés.</span><span class="sxs-lookup"><span data-stu-id="d6506-145">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="d6506-146">Dans cet exemple, nous allons créer un nouveau fichier dans un dossier OneDrive.</span><span class="sxs-lookup"><span data-stu-id="d6506-146">In this example, we create a new file in a OneDrive folder.</span></span> <span data-ttu-id="d6506-147">Vous pouvez utiliser les résultats d’un autre déclencheur pour créer le fichier OneDrive.</span><span class="sxs-lookup"><span data-stu-id="d6506-147">You can use output from another trigger to create the OneDrive file.</span></span> <span data-ttu-id="d6506-148">Par exemple, ajoutez le déclencheur Outlook Office 365 *Lorsqu’un nouveau courrier électronique arrive*.</span><span class="sxs-lookup"><span data-stu-id="d6506-148">For example, add the Office 365 Outlook *When a new email arrives* trigger.</span></span> <span data-ttu-id="d6506-149">Puis ajoutez l’action OneDrive *Créer un fichier* qui utilise les champs Pièces jointes et Type de contenu d’une instruction ForEach pour créer le fichier dans OneDrive.</span><span class="sxs-lookup"><span data-stu-id="d6506-149">Then add the OneDrive *Create file* action that uses the Attachments and Content-Type fields within a ForEach to create the new file in OneDrive.</span></span> 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. <span data-ttu-id="d6506-150">**Enregistrez** vos modifications (dans le coin supérieur gauche de la barre d’outils).</span><span class="sxs-lookup"><span data-stu-id="d6506-150">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="d6506-151">Votre application logique est enregistrée et peut être activée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="d6506-151">Your logic app is saved and may be automatically enabled.</span></span>


## <a name="connector-specific-details"></a><span data-ttu-id="d6506-152">Détails spécifiques aux connecteurs</span><span class="sxs-lookup"><span data-stu-id="d6506-152">Connector-specific details</span></span>

<span data-ttu-id="d6506-153">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/onedriveconnector/).</span><span class="sxs-lookup"><span data-stu-id="d6506-153">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/onedriveconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="d6506-154">Autres connecteurs</span><span class="sxs-lookup"><span data-stu-id="d6506-154">More connectors</span></span>
<span data-ttu-id="d6506-155">Revenir à la [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="d6506-155">Go back to the [APIs list](apis-list.md).</span></span>