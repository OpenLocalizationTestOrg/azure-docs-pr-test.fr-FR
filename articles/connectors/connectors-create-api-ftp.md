---
title: "aaaLearn comment toouse hello dans les applications de la logique d’un connecteur FTP | Documents Microsoft"
description: "Créez des applications logiques avec Azure App Service. Se connecter tooFTP server toomanage vos fichiers. Vous pouvez exécuter diverses actions, comme charger, mettre à jour, obtenir et supprimer des fichiers dans le serveur FTP."
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
ms.openlocfilehash: a7020df2005ebb34fc569627ae0516b8528cc7a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-ftp-connector"></a><span data-ttu-id="1f2fd-105">Prise en main connecteur FTP de hello</span><span class="sxs-lookup"><span data-stu-id="1f2fd-105">Get started with hello FTP connector</span></span>
<span data-ttu-id="1f2fd-106">Utilisez hello FTP connecteur toomonitor, gérer et créer des fichiers sur un serveur FTP.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-106">Use hello FTP connector toomonitor, manage and create files on an  FTP server.</span></span> 

<span data-ttu-id="1f2fd-107">toouse [n’importe quel connecteur](apis-list.md), vous devez tout d’abord toocreate une application logique.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-107">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="1f2fd-108">Vous pouvez démarrer maintenant en [créant une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="1f2fd-108">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooftp"></a><span data-ttu-id="1f2fd-109">Se connecter tooFTP</span><span class="sxs-lookup"><span data-stu-id="1f2fd-109">Connect tooFTP</span></span>
<span data-ttu-id="1f2fd-110">Avant que votre application logique peut accéder à n’importe quel service, vous devez tout d’abord toocreate un *connexion* toohello service.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-110">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="1f2fd-111">Une [connexion](connectors-overview.md) permet d’assurer la connectivité entre une application logique et un autre service.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-111">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-tooftp"></a><span data-ttu-id="1f2fd-112">Créer un tooFTP de connexion</span><span class="sxs-lookup"><span data-stu-id="1f2fd-112">Create a connection tooFTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooFTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a><span data-ttu-id="1f2fd-113">Utiliser un déclencheur FTP</span><span class="sxs-lookup"><span data-stu-id="1f2fd-113">Use a FTP trigger</span></span>
<span data-ttu-id="1f2fd-114">Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-114">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="1f2fd-115">[En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="1f2fd-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="1f2fd-116">connecteur FTP Hello nécessite un serveur FTP qui est accessible à partir de hello Internet et qui est configuré toooperate avec le mode passif.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-116">hello FTP connector requires an FTP server that  is accessible from hello Internet and is configured toooperate with PASSIVE mode.</span></span> <span data-ttu-id="1f2fd-117">En outre, le connecteur de hello FTP est **non compatible avec implicite FTPS (FTP sur SSL)**.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-117">Also, hello FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span></span> <span data-ttu-id="1f2fd-118">connecteur de Hello FTP prend uniquement en charge explicite FTPS (FTP sur SSL).</span><span class="sxs-lookup"><span data-stu-id="1f2fd-118">hello FTP connector only supports explicit FTPS (FTP over SSL).</span></span>  
> 
> 

<span data-ttu-id="1f2fd-119">Dans cet exemple, je vous indiquent comment toouse hello **FTP - lorsqu’un fichier est ajouté ou modifié** déclencher tooinitiate un flux de travail logique application lorsqu’un fichier est ajouté à ou modifié sur un serveur FTP.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-119">In this example, I will show you how toouse hello **FTP - When a file is added or modified** trigger tooinitiate a logic app workflow when a file is added to, or modified on, an FTP server.</span></span> <span data-ttu-id="1f2fd-120">Dans un exemple d’entreprise, vous pouvez utiliser cette toomonitor déclencheur un dossier FTP pour les nouveaux fichiers qui représentent des commandes des clients.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-120">In an enterprise example, you could use this trigger toomonitor an FTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="1f2fd-121">Vous pouvez ensuite utiliser une action de connecteur FTP comme **obtenir le contenu du fichier** contenu de hello tooget de commande hello pour poursuivre le traitement et de stockage dans votre base de données de commandes.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-121">You could then use an FTP connector action such as **Get file content** tooget hello contents of hello order for further processing and storage in your orders database.</span></span>

1. <span data-ttu-id="1f2fd-122">Entrez *ftp* dans la zone de recherche de hello sur le Concepteur d’applications hello logique, puis sélectionnez hello **FTP - lorsqu’un fichier est ajouté ou modifié** déclencheur</span><span class="sxs-lookup"><span data-stu-id="1f2fd-122">Enter *ftp* in hello search box on hello logic apps designer then select hello **FTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="1f2fd-123">![Image de déclencheur FTP 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="1f2fd-123">![FTP trigger image 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span></span>  
   <span data-ttu-id="1f2fd-124">Hello **lorsqu’un fichier est ajouté ou modifié** contrôle s’ouvre</span><span class="sxs-lookup"><span data-stu-id="1f2fd-124">hello **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="1f2fd-125">![Image de déclencheur FTP 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="1f2fd-125">![FTP trigger image 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span></span>  
2. <span data-ttu-id="1f2fd-126">Sélectionnez hello **...**  situé sur le côté droit de hello du contrôle de hello.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-126">Select hello **...** located on hello right side of hello control.</span></span> <span data-ttu-id="1f2fd-127">Cette opération ouvre le contrôle de sélecteur de dossier hello</span><span class="sxs-lookup"><span data-stu-id="1f2fd-127">This opens hello folder picker control</span></span>  
   <span data-ttu-id="1f2fd-128">![Image de déclencheur FTP 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span><span class="sxs-lookup"><span data-stu-id="1f2fd-128">![FTP trigger image 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span></span>  
3. <span data-ttu-id="1f2fd-129">Sélectionnez hello  **>**  (flèche droite) et recherchez le dossier de hello toofind que vous souhaitez toomonitor pour les fichiers nouveaux ou modifiés.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-129">Select hello **>** (right arrow) and browse toofind hello folder that you want toomonitor for new or modified files.</span></span> <span data-ttu-id="1f2fd-130">Sélectionnez le dossier de hello et notez le dossier de hello est maintenant affichée dans hello **dossier** contrôle.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-130">Select hello folder and notice hello folder is now displayed in hello **Folder** control.</span></span>  
   <span data-ttu-id="1f2fd-131">![Image de déclencheur FTP 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span><span class="sxs-lookup"><span data-stu-id="1f2fd-131">![FTP trigger image 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span></span>   

<span data-ttu-id="1f2fd-132">À ce stade, votre application logique a été configurée avec un déclencheur qui commence une série de hello autres déclencheurs et les actions dans le flux de travail hello lorsqu’un fichier est modifié ou créé dans le dossier FTP hello.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-132">At this point, your logic app has been configured with a trigger that will begin a run of hello other triggers and actions in hello workflow when a file is either modified or created in hello specific FTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="1f2fd-133">Pour un toobe application logique fonctionnelle, il doit contenir au moins un déclencheur et une action.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-133">For a logic app toobe functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="1f2fd-134">Suivez les étapes de hello de hello suivant section tooadd une action.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-134">Follow hello steps in hello next section tooadd an action.</span></span>  
> 
> 

## <a name="use-a-ftp-action"></a><span data-ttu-id="1f2fd-135">Utiliser une action FTP</span><span class="sxs-lookup"><span data-stu-id="1f2fd-135">Use a FTP action</span></span>
<span data-ttu-id="1f2fd-136">Une action est une opération effectuée par flux de travail hello défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-136">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="1f2fd-137">[En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="1f2fd-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="1f2fd-138">Maintenant que vous avez ajouté un déclencheur, suivez ces étapes de tooadd une action qui obtiennent contenu hello de fichier nouveau ou modifié hello trouvés par le déclencheur de hello.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-138">Now that you have added a trigger, follow these steps tooadd an action that will get hello contents of hello new or modified file found by hello trigger.</span></span>    

1. <span data-ttu-id="1f2fd-139">Sélectionnez **+ nouvelle étape** contenu hello tooadd hello hello action tooget du fichier hello sur le serveur de hello FTP</span><span class="sxs-lookup"><span data-stu-id="1f2fd-139">Select **+ New step** tooadd hello hello action tooget hello contents of hello file on hello FTP server</span></span>  
2. <span data-ttu-id="1f2fd-140">Sélectionnez hello **ajouter une action** lien.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-140">Select hello **Add an action** link.</span></span>  
   <span data-ttu-id="1f2fd-141">![Image d’action FTP 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span><span class="sxs-lookup"><span data-stu-id="1f2fd-141">![FTP action image 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span></span>  
3. <span data-ttu-id="1f2fd-142">Entrez *FTP* toosearch pour toutes les actions liées tooFTP.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-142">Enter *FTP* toosearch for all actions related tooFTP.</span></span>
4. <span data-ttu-id="1f2fd-143">Sélectionnez **FTP - obtenir le contenu du fichier** comme hello action tootake lorsqu’un fichier nouveau ou modifié est trouvé dans le dossier de hello FTP.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-143">Select **FTP - Get file content**  as hello action tootake when a new or modified file is found in hello FTP folder.</span></span>      
   <span data-ttu-id="1f2fd-144">![Image d’action FTP 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span><span class="sxs-lookup"><span data-stu-id="1f2fd-144">![FTP action image 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span></span>  
   <span data-ttu-id="1f2fd-145">Hello **obtenir le contenu du fichier** contrôle s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-145">hello **Get file content** control opens.</span></span> <span data-ttu-id="1f2fd-146">**Remarque**: vous est demandée tooauthorize votre tooaccess d’application logique votre serveur FTP de compte si vous le n'avez pas fait précédemment.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-146">**Note**: you will be prompted tooauthorize your logic app tooaccess your FTP server account if you have not done so previously.</span></span>  
   <span data-ttu-id="1f2fd-147">![Image d’action FTP 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span><span class="sxs-lookup"><span data-stu-id="1f2fd-147">![FTP action image 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span></span>   
5. <span data-ttu-id="1f2fd-148">Sélectionnez hello **fichier** contrôle (hello un espace blanc situé sous **fichier***).</span><span class="sxs-lookup"><span data-stu-id="1f2fd-148">Select hello **File** control (hello white space located below **FILE***).</span></span> <span data-ttu-id="1f2fd-149">Ici, vous pouvez utiliser une des hello différentes propriétés de fichier nouveau ou modifié hello trouvé sur le serveur FTP de hello.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-149">Here, you can use any of hello various properties from hello new or modified file found on hello FTP server.</span></span>  
6. <span data-ttu-id="1f2fd-150">Sélectionnez hello **le contenu du fichier** option.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-150">Select hello **File content** option.</span></span>  
   <span data-ttu-id="1f2fd-151">![Image d’action FTP 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span><span class="sxs-lookup"><span data-stu-id="1f2fd-151">![FTP action image 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span></span>   
7. <span data-ttu-id="1f2fd-152">contrôle de Hello est mise à jour, indiquant que hello **FTP - obtenir le contenu du fichier** action obtiendrez hello *le contenu du fichier* du fichier de hello nouvelles ou modifiées sur le serveur de hello FTP.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-152">hello control is updated, indicating that hello **FTP - Get file content** action will get hello *file content* of hello new or modified file on hello FTP server.</span></span>      
   <span data-ttu-id="1f2fd-153">![Image d’action FTP 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span><span class="sxs-lookup"><span data-stu-id="1f2fd-153">![FTP action image 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span></span>     
8. <span data-ttu-id="1f2fd-154">Enregistrez votre travail, puis ajoutez un tootest de dossier FTP de fichiers toohello votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-154">Save your work then add a file toohello FTP folder tootest your workflow.</span></span>    

<span data-ttu-id="1f2fd-155">À ce stade, l’application de hello logique a été configuré avec un déclencheur toomonitor un dossier sur un serveur FTP et le flux de travail initier hello lorsqu’il détecte un nouveau fichier ou un fichier modifié sur le serveur de hello FTP.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-155">At this point, hello logic app has been configured with a trigger toomonitor a folder on an FTP server and initiate hello workflow when it finds either a new file or a modified file on hello FTP server.</span></span> 

<span data-ttu-id="1f2fd-156">application logique de Hello a également été configurée avec une action tooget hello hello nouvelles ou modifiées fichier.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-156">hello logic app also has been configured with an action tooget hello contents of hello new or modified file.</span></span>

<span data-ttu-id="1f2fd-157">Vous pouvez maintenant ajouter une autre action, par exemple hello [SQL Server - ligne d’insertion](connectors-create-api-sqlazure.md) action tooinsert hello contenu du hello nouvelle ou modifiée dans une table de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="1f2fd-157">You can now add another action such as hello [SQL Server - insert row](connectors-create-api-sqlazure.md) action tooinsert hello contents of hello new or modified file into a SQL database table.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="1f2fd-158">Détails spécifiques du connecteur</span><span class="sxs-lookup"><span data-stu-id="1f2fd-158">Connector-specific details</span></span>

<span data-ttu-id="1f2fd-159">Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/ftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="1f2fd-159">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/ftpconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1f2fd-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1f2fd-160">Next Steps</span></span>
[<span data-ttu-id="1f2fd-161">Créer une application logique</span><span class="sxs-lookup"><span data-stu-id="1f2fd-161">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

