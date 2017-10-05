---
title: "Découvrez comment utiliser le connecteur FTP dans des applications logiques | Microsoft Docs"
description: "Créez des applications logiques avec Azure App Service. Connectez-vous à un serveur FTP pour gérer vos fichiers. Vous pouvez exécuter diverses actions, comme charger, mettre à jour, obtenir et supprimer des fichiers dans le serveur FTP."
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
tags: connectors
ms.assetid: d83c55fe-eb59-4b7b-a5ec-afac5c772616
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/22/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 61bfbedfd4f1e84b6976099323a32f3a720634c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-ftp-connector"></a><span data-ttu-id="3260b-105">Prise en main du connecteur FTP</span><span class="sxs-lookup"><span data-stu-id="3260b-105">Get started with the FTP connector</span></span>
<span data-ttu-id="3260b-106">Utilisez le connecteur FTP pour surveiller, gérer et créer des fichiers sur un serveur FTP.</span><span class="sxs-lookup"><span data-stu-id="3260b-106">Use the FTP connector to monitor, manage and create files on an  FTP server.</span></span> 

<span data-ttu-id="3260b-107">Pour utiliser [n’importe quel connecteur](apis-list.md), vous devez commencer par créer une application logique.</span><span class="sxs-lookup"><span data-stu-id="3260b-107">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="3260b-108">Vous pouvez démarrer maintenant en [créant une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3260b-108">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-ftp"></a><span data-ttu-id="3260b-109">Se connecter à FTP</span><span class="sxs-lookup"><span data-stu-id="3260b-109">Connect to FTP</span></span>
<span data-ttu-id="3260b-110">Pour que votre application logique puisse accéder à un service, vous devez commencer par créer une *connexion* à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="3260b-110">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="3260b-111">Une [connexion](connectors-overview.md) permet d’assurer la connectivité entre une application logique et un autre service.</span><span class="sxs-lookup"><span data-stu-id="3260b-111">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-ftp"></a><span data-ttu-id="3260b-112">Créer une connexion à FTP</span><span class="sxs-lookup"><span data-stu-id="3260b-112">Create a connection to FTP</span></span>
> [!INCLUDE [Steps to create a connection to FTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a><span data-ttu-id="3260b-113">Utiliser un déclencheur FTP</span><span class="sxs-lookup"><span data-stu-id="3260b-113">Use a FTP trigger</span></span>
<span data-ttu-id="3260b-114">Un déclencheur est un événement qui peut être utilisé pour lancer le flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="3260b-114">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="3260b-115">[En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="3260b-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="3260b-116">Le connecteur FTP requiert un serveur FTP accessible à partir d’Internet et configuré pour fonctionner en mode PASSIF.</span><span class="sxs-lookup"><span data-stu-id="3260b-116">The FTP connector requires an FTP server that  is accessible from the Internet and is configured to operate with PASSIVE mode.</span></span> <span data-ttu-id="3260b-117">En outre, le connecteur FTP **n’est pas compatible avec le protocole FTPS (FTP sur SSL) implicite**.</span><span class="sxs-lookup"><span data-stu-id="3260b-117">Also, the FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span></span> <span data-ttu-id="3260b-118">Le connecteur FTP prend uniquement en charge FTPS (FTP sur SSL) en mode explicite.</span><span class="sxs-lookup"><span data-stu-id="3260b-118">The FTP connector only supports explicit FTPS (FTP over SSL).</span></span>  
> 
> 

<span data-ttu-id="3260b-119">Dans cet exemple, nous allons vous indiquer comment utiliser le déclencheur **FTP - Lors de l’ajout ou de la modification d’un fichier** pour initialiser un workflow d’application logique lorsqu’un fichier est ajouté à un serveur FTP ou modifié sur ce dernier.</span><span class="sxs-lookup"><span data-stu-id="3260b-119">In this example, I will show you how to use the **FTP - When a file is added or modified** trigger to initiate a logic app workflow when a file is added to, or modified on, an FTP server.</span></span> <span data-ttu-id="3260b-120">Dans un contexte d’entreprise, vous pourriez utiliser ce déclencheur pour surveiller l’apparition dans un dossier FTP de nouveaux fichiers représentant des commandes émanant de clients.</span><span class="sxs-lookup"><span data-stu-id="3260b-120">In an enterprise example, you could use this trigger to monitor an FTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="3260b-121">Vous pourriez ensuite utiliser une action de connecteur FTP telle que **Obtenir le contenu d’un fichier** pour récupérer le contenu de la commande à des fins de traitement ultérieur et de stockage dans votre base de données de commandes.</span><span class="sxs-lookup"><span data-stu-id="3260b-121">You could then use an FTP connector action such as **Get file content** to get the contents of the order for further processing and storage in your orders database.</span></span>

1. <span data-ttu-id="3260b-122">Entrez *ftp* dans la zone de recherche du Concepteur d’applications logiques, puis sélectionnez le déclencheur **FTP - Lors de l’ajout ou de la modification d’un fichier**.</span><span class="sxs-lookup"><span data-stu-id="3260b-122">Enter *ftp* in the search box on the logic apps designer then select the **FTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="3260b-123">![Image de déclencheur FTP 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="3260b-123">![FTP trigger image 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span></span>  
   <span data-ttu-id="3260b-124">Le contrôle **Lors de l’ajout ou de la modification d’un fichier** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3260b-124">The **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="3260b-125">![Image de déclencheur FTP 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="3260b-125">![FTP trigger image 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span></span>  
2. <span data-ttu-id="3260b-126">Sélectionnez le **...** situé à droite du contrôle.</span><span class="sxs-lookup"><span data-stu-id="3260b-126">Select the **...** located on the right side of the control.</span></span> <span data-ttu-id="3260b-127">Cette opération ouvre le contrôle de sélecteur de dossier </span><span class="sxs-lookup"><span data-stu-id="3260b-127">This opens the folder picker control</span></span>  
   <span data-ttu-id="3260b-128">![Image de déclencheur FTP 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span><span class="sxs-lookup"><span data-stu-id="3260b-128">![FTP trigger image 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span></span>  
3. <span data-ttu-id="3260b-129">Sélectionnez le symbole **>** (flèche droite) et recherchez le dossier dans lequel vous souhaitez surveiller l’apparition de fichiers nouveaux ou modifiés.</span><span class="sxs-lookup"><span data-stu-id="3260b-129">Select the **>** (right arrow) and browse to find the folder that you want to monitor for new or modified files.</span></span> <span data-ttu-id="3260b-130">Sélectionnez le dossier et remarquez qu’il apparaît à présent dans le contrôle **Dossier**.</span><span class="sxs-lookup"><span data-stu-id="3260b-130">Select the folder and notice the folder is now displayed in the **Folder** control.</span></span>  
   <span data-ttu-id="3260b-131">![Image de déclencheur FTP 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span><span class="sxs-lookup"><span data-stu-id="3260b-131">![FTP trigger image 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span></span>   

<span data-ttu-id="3260b-132">À ce stade, votre application logique a été configurée avec un déclencheur qui lance une série d’autres déclencheurs et actions dans le workflow lorsqu’un fichier est modifié ou créé dans le dossier FTP sélectionné.</span><span class="sxs-lookup"><span data-stu-id="3260b-132">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow when a file is either modified or created in the specific FTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="3260b-133">Pour qu’une application logique soit fonctionnelle, elle doit contenir au moins un déclencheur et une action.</span><span class="sxs-lookup"><span data-stu-id="3260b-133">For a logic app to be functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="3260b-134">Suivez les étapes décrites dans la section suivante pour ajouter une action.</span><span class="sxs-lookup"><span data-stu-id="3260b-134">Follow the steps in the next section to add an action.</span></span>  
> 
> 

## <a name="use-a-ftp-action"></a><span data-ttu-id="3260b-135">Utiliser une action FTP</span><span class="sxs-lookup"><span data-stu-id="3260b-135">Use a FTP action</span></span>
<span data-ttu-id="3260b-136">Une action est une opération effectuée par le flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="3260b-136">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="3260b-137">[En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="3260b-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="3260b-138">Une fois le déclencheur ajouté, procédez comme suit pour ajouter une action qui récupérera le contenu du fichier nouveau ou modifié trouvé par le déclencheur.</span><span class="sxs-lookup"><span data-stu-id="3260b-138">Now that you have added a trigger, follow these steps to add an action that will get the contents of the new or modified file found by the trigger.</span></span>    

1. <span data-ttu-id="3260b-139">Sélectionnez **+ Nouvelle étape** pour ajouter l’action permettant d’obtenir le contenu du fichier sur le serveur FTP.</span><span class="sxs-lookup"><span data-stu-id="3260b-139">Select **+ New step** to add the the action to get the contents of the file on the FTP server</span></span>  
2. <span data-ttu-id="3260b-140">Sélectionnez le lien **Ajouter une action** .</span><span class="sxs-lookup"><span data-stu-id="3260b-140">Select the **Add an action** link.</span></span>  
   <span data-ttu-id="3260b-141">![Image d’action FTP 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span><span class="sxs-lookup"><span data-stu-id="3260b-141">![FTP action image 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span></span>  
3. <span data-ttu-id="3260b-142">Entrez *FTP* pour rechercher toutes les actions associées à FTP.</span><span class="sxs-lookup"><span data-stu-id="3260b-142">Enter *FTP* to search for all actions related to FTP.</span></span>
4. <span data-ttu-id="3260b-143">Sélectionnez **FTP - Obtenir le contenu d’un fichier** comme action à exécuter lorsqu’un fichier nouveau ou modifié est trouvé dans le dossier FTP.</span><span class="sxs-lookup"><span data-stu-id="3260b-143">Select **FTP - Get file content**  as the action to take when a new or modified file is found in the FTP folder.</span></span>      
   <span data-ttu-id="3260b-144">![Image d’action FTP 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span><span class="sxs-lookup"><span data-stu-id="3260b-144">![FTP action image 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span></span>  
   <span data-ttu-id="3260b-145">Le contrôle **Obtenir le contenu d’un fichier** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3260b-145">The **Get file content** control opens.</span></span> <span data-ttu-id="3260b-146">**Remarque** : vous serez invité à autoriser votre application logique à accéder à votre compte de serveur FTP, si vous ne l’avez pas fait précédemment.</span><span class="sxs-lookup"><span data-stu-id="3260b-146">**Note**: you will be prompted to authorize your logic app to access your FTP server account if you have not done so previously.</span></span>  
   <span data-ttu-id="3260b-147">![Image d’action FTP 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span><span class="sxs-lookup"><span data-stu-id="3260b-147">![FTP action image 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span></span>   
5. <span data-ttu-id="3260b-148">Sélectionnez le contrôle **Fichier** (espace blanc situé sous **FICHIER***).</span><span class="sxs-lookup"><span data-stu-id="3260b-148">Select the **File** control (the white space located below **FILE***).</span></span> <span data-ttu-id="3260b-149">Ce contrôle vous permet d’utiliser les diverses propriétés du fichier nouveau ou modifié trouvé sur le serveur FTP.</span><span class="sxs-lookup"><span data-stu-id="3260b-149">Here, you can use any of the various properties from the new or modified file found on the FTP server.</span></span>  
6. <span data-ttu-id="3260b-150">Sélectionnez l’option **Contenu du fichier**.</span><span class="sxs-lookup"><span data-stu-id="3260b-150">Select the **File content** option.</span></span>  
   <span data-ttu-id="3260b-151">![Image d’action FTP 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span><span class="sxs-lookup"><span data-stu-id="3260b-151">![FTP action image 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span></span>   
7. <span data-ttu-id="3260b-152">Le contrôle est mis à jour, ce qui indique que l’action **FTP - Obtenir le contenu d’un fichier** récupérera le *contenu du fichier* nouveau ou modifié sur le serveur FTP.</span><span class="sxs-lookup"><span data-stu-id="3260b-152">The control is updated, indicating that the **FTP - Get file content** action will get the *file content* of the new or modified file on the FTP server.</span></span>      
   <span data-ttu-id="3260b-153">![Image d’action FTP 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span><span class="sxs-lookup"><span data-stu-id="3260b-153">![FTP action image 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span></span>     
8. <span data-ttu-id="3260b-154">Enregistrez votre travail, puis ajoutez un fichier au dossier FTP pour tester votre workflow.</span><span class="sxs-lookup"><span data-stu-id="3260b-154">Save your work then add a file to the FTP folder to test your workflow.</span></span>    

<span data-ttu-id="3260b-155">À ce stade, l’application logique a été configurée avec un déclencheur pour surveiller un dossier d’un serveur FTP et pour initialiser le workflow lorsqu’elle détecte un fichier nouveau ou modifié sur le serveur FTP.</span><span class="sxs-lookup"><span data-stu-id="3260b-155">At this point, the logic app has been configured with a trigger to monitor a folder on an FTP server and initiate the workflow when it finds either a new file or a modified file on the FTP server.</span></span> 

<span data-ttu-id="3260b-156">L’application logique a également été configurée avec une action destinée à récupérer le contenu du fichier nouveau ou modifié.</span><span class="sxs-lookup"><span data-stu-id="3260b-156">The logic app also has been configured with an action to get the contents of the new or modified file.</span></span>

<span data-ttu-id="3260b-157">Vous pouvez à présent ajouter une autre action, telle que l’action [SQL Server - Insérer une ligne](connectors-create-api-sqlazure.md), pour insérer le contenu du fichier nouveau ou modifié dans une table de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="3260b-157">You can now add another action such as the [SQL Server - insert row](connectors-create-api-sqlazure.md) action to insert the contents of the new or modified file into a SQL database table.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="3260b-158">Détails spécifiques aux connecteurs</span><span class="sxs-lookup"><span data-stu-id="3260b-158">Connector-specific details</span></span>

<span data-ttu-id="3260b-159">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/ftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="3260b-159">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/ftpconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3260b-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3260b-160">Next Steps</span></span>
[<span data-ttu-id="3260b-161">Créer une application logique</span><span class="sxs-lookup"><span data-stu-id="3260b-161">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

