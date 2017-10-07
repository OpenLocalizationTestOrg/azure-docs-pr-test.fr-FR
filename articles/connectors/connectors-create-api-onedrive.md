---
title: connecteur de OneDrive aaaAdd hello dans vos applications logiques | Documents Microsoft
description: "Vue d’ensemble du connecteur de OneDrive hello avec des paramètres de l’API REST"
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
ms.openlocfilehash: 8303794bb3c2844de288f87f40639abb84c160fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-onedrive-connector"></a><span data-ttu-id="e844e-103">Prise en main connecteur de OneDrive hello</span><span class="sxs-lookup"><span data-stu-id="e844e-103">Get started with hello OneDrive connector</span></span>
<span data-ttu-id="e844e-104">Se connecter tooOneDrive toomanage vos fichiers, y compris le téléchargement, get, supprimez des fichiers et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="e844e-104">Connect tooOneDrive toomanage your files, including upload, get, delete files, and more.</span></span> 

<span data-ttu-id="e844e-105">Avec OneDrive, vous pouvez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e844e-105">With OneDrive, you:</span></span> 

* <span data-ttu-id="e844e-106">Créer votre flux de travail en stockant des fichiers dans OneDrive, ou mettre à jour des fichiers existants dans OneDrive.</span><span class="sxs-lookup"><span data-stu-id="e844e-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span></span> 
* <span data-ttu-id="e844e-107">Utilisez des déclencheurs toostart votre flux de travail lorsqu’un fichier est créé ou mis à jour au sein de votre OneDrive.</span><span class="sxs-lookup"><span data-stu-id="e844e-107">Use triggers toostart your workflow when a file is created or updated within your OneDrive.</span></span>
* <span data-ttu-id="e844e-108">Utiliser des actions toocreate un fichier, supprimer un fichier et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="e844e-108">Use actions toocreate a file, delete a file, and more.</span></span> <span data-ttu-id="e844e-109">Par exemple, lorsqu’un nouveau courrier électronique Office 365 est reçu avec une pièce jointe (déclencheur), créer un nouveau fichier dans OneDrive (action).</span><span class="sxs-lookup"><span data-stu-id="e844e-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span></span>

<span data-ttu-id="e844e-110">Cette rubrique vous montre comment toouse hello dans une application de la logique d’un connecteur OneDrive, et également les listes hello déclencheurs et actions.</span><span class="sxs-lookup"><span data-stu-id="e844e-110">This topic shows you how toouse hello OneDrive connector in a logic app, and also lists hello triggers and actions.</span></span>

<span data-ttu-id="e844e-111">toolearn en savoir plus sur les applications de la logique, consultez [quelles sont les applications logique](../logic-apps/logic-apps-what-are-logic-apps.md) et [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e844e-111">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooonedrive"></a><span data-ttu-id="e844e-112">Se connecter tooOneDrive</span><span class="sxs-lookup"><span data-stu-id="e844e-112">Connect tooOneDrive</span></span>
<span data-ttu-id="e844e-113">Avant que votre application logique peut accéder à n’importe quel service, vous créez tout d’abord un *connexion* toohello service.</span><span class="sxs-lookup"><span data-stu-id="e844e-113">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="e844e-114">Une connexion permet d’assurer la connectivité entre une application logique et un autre service.</span><span class="sxs-lookup"><span data-stu-id="e844e-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="e844e-115">Par exemple, tooconnect tooOneDrive, vous devez d’abord un OneDrive *connexion*.</span><span class="sxs-lookup"><span data-stu-id="e844e-115">For example, tooconnect tooOneDrive, you first need a OneDrive *connection*.</span></span> <span data-ttu-id="e844e-116">toocreate une connexion, entrez des informations d’identification de hello que vous utilisez normalement le service de hello tooaccess tooconnect pour vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="e844e-116">toocreate a connection, enter hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="e844e-117">Par conséquent, avec OneDrive, entrez hello authentification tooyour OneDrive compte toocreate hello à la connexion.</span><span class="sxs-lookup"><span data-stu-id="e844e-117">So, with OneDrive, enter hello credentials tooyour OneDrive account  toocreate hello connection.</span></span>

### <a name="create-hello-connection"></a><span data-ttu-id="e844e-118">Créer la connexion de hello</span><span class="sxs-lookup"><span data-stu-id="e844e-118">Create hello connection</span></span>
> [!INCLUDE [Steps toocreate a connection tooOneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="e844e-119">Utilisation d’un déclencheur</span><span class="sxs-lookup"><span data-stu-id="e844e-119">Use a trigger</span></span>
<span data-ttu-id="e844e-120">Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="e844e-120">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="e844e-121">Déclencheurs « interrogent « service de hello à un intervalle et la fréquence à laquelle vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="e844e-121">Triggers "poll" hello service at an interval and frequency that you want.</span></span> <span data-ttu-id="e844e-122">[En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="e844e-122">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="e844e-123">Dans l’application de la logique de hello, tapez « onedrive » tooget une liste des déclencheurs de hello :</span><span class="sxs-lookup"><span data-stu-id="e844e-123">In hello logic app, type "onedrive" tooget a list of hello triggers:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="e844e-124">Sélectionnez **Quand un fichier est modifié**.</span><span class="sxs-lookup"><span data-stu-id="e844e-124">Select **When a file is modified**.</span></span> <span data-ttu-id="e844e-125">Si une connexion existe déjà, puis sélectionnez le bouton tooselect un dossier de hello afficher le sélecteur.</span><span class="sxs-lookup"><span data-stu-id="e844e-125">If a connection already exists, then select hello Show Picker button tooselect a folder.</span></span>
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    <span data-ttu-id="e844e-126">Si vous êtes invité à toosign dans, puis entrez le signe de hello dans Détails toocreate hello de connexion.</span><span class="sxs-lookup"><span data-stu-id="e844e-126">If you are prompted toosign in, then enter hello sign in details toocreate hello connection.</span></span> <span data-ttu-id="e844e-127">[Créer la connexion de hello](connectors-create-api-onedrive.md#create-the-connection) dans cette rubrique répertorie les étapes de hello.</span><span class="sxs-lookup"><span data-stu-id="e844e-127">[Create hello connection](connectors-create-api-onedrive.md#create-the-connection) in this topic lists hello steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="e844e-128">Dans cet exemple, application logique de hello, s’exécute lorsqu’un fichier dans le dossier hello que vous choisissez est mis à jour.</span><span class="sxs-lookup"><span data-stu-id="e844e-128">In this example, hello logic app runs when a file in hello folder you choose is updated.</span></span> <span data-ttu-id="e844e-129">résultats de hello toosee de ce déclencheur, ajouter une autre action qui vous envoie un message électronique.</span><span class="sxs-lookup"><span data-stu-id="e844e-129">toosee hello results of this trigger, add another action that sends you an email.</span></span> <span data-ttu-id="e844e-130">Par exemple, ajouter hello Outlook Office 365 *envoyer un courrier électronique* action qui envoie par courrier électronique vous lorsqu’un fichier est mis à jour.</span><span class="sxs-lookup"><span data-stu-id="e844e-130">For example, add hello Office 365 Outlook *Send an email* action that emails you when a file is updated.</span></span> 

3. <span data-ttu-id="e844e-131">Sélectionnez hello **modifier** bouton et définissez hello **fréquence** et **intervalle** valeurs.</span><span class="sxs-lookup"><span data-stu-id="e844e-131">Select hello **Edit** button and set hello **Frequency** and **Interval** values.</span></span> <span data-ttu-id="e844e-132">Par exemple, si vous souhaitez hello déclencheur toopoll toutes les 15 minutes, puis définissez hello **fréquence** trop**Minute**et ensemble hello **intervalle** trop**15**.</span><span class="sxs-lookup"><span data-stu-id="e844e-132">For example, if you want hello trigger toopoll every 15 minutes, then set hello **Frequency** too**Minute**, and set hello **Interval** too**15**.</span></span> 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. <span data-ttu-id="e844e-133">**Enregistrer** vos modifications (situé dans l’angle supérieur gauche de la barre d’outils hello).</span><span class="sxs-lookup"><span data-stu-id="e844e-133">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="e844e-134">Votre application logique est enregistrée et peut être activée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="e844e-134">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="e844e-135">Utilisation d’une action</span><span class="sxs-lookup"><span data-stu-id="e844e-135">Use an action</span></span>
<span data-ttu-id="e844e-136">Une action est une opération effectuée par flux de travail hello défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="e844e-136">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="e844e-137">[En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="e844e-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="e844e-138">Sélectionnez le signe plus hello.</span><span class="sxs-lookup"><span data-stu-id="e844e-138">Select hello plus sign.</span></span> <span data-ttu-id="e844e-139">Vous voyez plusieurs choix : **ajouter une action**, **ajouter une condition**, ou l’un des hello **plus** options.</span><span class="sxs-lookup"><span data-stu-id="e844e-139">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. <span data-ttu-id="e844e-140">Choisissez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="e844e-140">Choose **Add an action**.</span></span>
3. <span data-ttu-id="e844e-141">Dans la zone de texte hello, tapez « onedrive » tooget une liste de toutes les actions disponibles hello.</span><span class="sxs-lookup"><span data-stu-id="e844e-141">In hello text box, type “onedrive” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. <span data-ttu-id="e844e-142">Dans notre exemple, choisissez **OneDrive - Créer un fichier**.</span><span class="sxs-lookup"><span data-stu-id="e844e-142">In our example, choose **OneDrive - Create file**.</span></span> <span data-ttu-id="e844e-143">Si une connexion existe déjà, puis sélectionnez hello **chemin d’accès du dossier** tooput hello de fichier, entrez hello **nom de fichier**, puis choisissez hello **contenu du fichier** souhaité :</span><span class="sxs-lookup"><span data-stu-id="e844e-143">If a connection already exists, then select hello **Folder Path** tooput hello file, enter hello **File Name**, and choose hello **File Content** you want:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    <span data-ttu-id="e844e-144">Si vous êtes invité hello informations de connexion, puis entrez connexion de hello toocreate hello détails.</span><span class="sxs-lookup"><span data-stu-id="e844e-144">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="e844e-145">[Créer la connexion de hello](connectors-create-api-onedrive.md#create-the-connection) dans cette rubrique décrit ces propriétés.</span><span class="sxs-lookup"><span data-stu-id="e844e-145">[Create hello connection](connectors-create-api-onedrive.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="e844e-146">Dans cet exemple, nous allons créer un nouveau fichier dans un dossier OneDrive.</span><span class="sxs-lookup"><span data-stu-id="e844e-146">In this example, we create a new file in a OneDrive folder.</span></span> <span data-ttu-id="e844e-147">Vous pouvez utiliser la sortie à partir d’un autre fichier OneDrive de déclencheur toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="e844e-147">You can use output from another trigger toocreate hello OneDrive file.</span></span> <span data-ttu-id="e844e-148">Par exemple, ajouter hello Outlook Office 365 *lorsqu’un nouvel e-mail arrive* déclencheur.</span><span class="sxs-lookup"><span data-stu-id="e844e-148">For example, add hello Office 365 Outlook *When a new email arrives* trigger.</span></span> <span data-ttu-id="e844e-149">Ajoutez ensuite hello OneDrive *créer un fichier* action qui utilise une hello des pièces jointes et les champs de Type de contenu dans un fichier ForEach toocreate hello nouveau dans OneDrive.</span><span class="sxs-lookup"><span data-stu-id="e844e-149">Then add hello OneDrive *Create file* action that uses hello Attachments and Content-Type fields within a ForEach toocreate hello new file in OneDrive.</span></span> 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. <span data-ttu-id="e844e-150">**Enregistrer** vos modifications (situé dans l’angle supérieur gauche de la barre d’outils hello).</span><span class="sxs-lookup"><span data-stu-id="e844e-150">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="e844e-151">Votre application logique est enregistrée et peut être activée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="e844e-151">Your logic app is saved and may be automatically enabled.</span></span>


## <a name="connector-specific-details"></a><span data-ttu-id="e844e-152">Détails spécifiques du connecteur</span><span class="sxs-lookup"><span data-stu-id="e844e-152">Connector-specific details</span></span>

<span data-ttu-id="e844e-153">Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/onedriveconnector/).</span><span class="sxs-lookup"><span data-stu-id="e844e-153">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/onedriveconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="e844e-154">Autres connecteurs</span><span class="sxs-lookup"><span data-stu-id="e844e-154">More connectors</span></span>
<span data-ttu-id="e844e-155">Revenir en arrière toohello [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="e844e-155">Go back toohello [APIs list](apis-list.md).</span></span>
