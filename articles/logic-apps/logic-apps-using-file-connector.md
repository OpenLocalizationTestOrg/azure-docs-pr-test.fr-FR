---
title: "systèmes à partir d’Azure Logic Apps du fichier local tooon aaaConnect | Documents Microsoft"
description: "Connecter des systèmes de fichiers local tooon à partir de votre flux de travail application logique via la passerelle de données locale hello et le connecteur du système de fichiers"
keywords: "systèmes de fichiers"
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: LADocs; deli
ms.openlocfilehash: beb5565293def4aba81f63f19e77d7498aac38c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-file-systems-from-logic-apps-with-hello-file-system-connector"></a><span data-ttu-id="ab60f-104">Connecter des systèmes de fichiers local tooon à partir de la logique des applications avec le connecteur de système de fichiers hello</span><span class="sxs-lookup"><span data-stu-id="ab60f-104">Connect tooon-premises file systems from logic apps with hello File System connector</span></span>

<span data-ttu-id="ab60f-105">Connectivité de cloud hybride est applications toologic central, c’est le cas toomanage données et en toute sécurité accès aux ressources locales, vos applications logiques peuvent utiliser passerelle de données locale hello.</span><span class="sxs-lookup"><span data-stu-id="ab60f-105">Hybrid cloud connectivity is central toologic apps, so toomanage data and securely access on-premises resources, your logic apps can use hello on-premises data gateway.</span></span> <span data-ttu-id="ab60f-106">Dans cet article, nous montrons comment tooconnect tooan local système de fichiers avec un scénario de base : copier un fichier de tooDropbox téléchargé tooa partage de fichiers, puis envoyer un courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="ab60f-106">In this article, we show how tooconnect tooan on-premises file system with a basic scenario: copy a file that's uploaded tooDropbox tooa file share, then send an email.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab60f-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ab60f-107">Prerequisites</span></span>

- <span data-ttu-id="ab60f-108">Installer et configurer hello dernières [passerelle de données locale](https://www.microsoft.com/download/details.aspx?id=53127).</span><span class="sxs-lookup"><span data-stu-id="ab60f-108">Install and configure hello latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127).</span></span>
- <span data-ttu-id="ab60f-109">Installer la passerelle de données de local dernière hello, version 1.15.6150.1 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="ab60f-109">Install hello latest on-premises data gateway, version 1.15.6150.1 or above.</span></span> <span data-ttu-id="ab60f-110">[Se connecter à la passerelle de données locale toohello](http://aka.ms/logicapps-gateway) listes hello étapes.</span><span class="sxs-lookup"><span data-stu-id="ab60f-110">[Connect toohello on-premises data gateway](http://aka.ms/logicapps-gateway) lists hello steps.</span></span> <span data-ttu-id="ab60f-111">passerelle de Hello doit être installé sur un ordinateur local avant de pouvoir continuer avec hello étapes restantes de hello.</span><span class="sxs-lookup"><span data-stu-id="ab60f-111">hello gateway must be installed on an on-premises machine before you can continue with hello rest of hello steps.</span></span>

## <a name="add-trigger-and-actions-for-connecting-tooyour-file-system"></a><span data-ttu-id="ab60f-112">Ajouter le déclencheur et les actions pour la connexion de système de fichiers tooyour</span><span class="sxs-lookup"><span data-stu-id="ab60f-112">Add trigger and actions for connecting tooyour file system</span></span>

1. <span data-ttu-id="ab60f-113">Créez une application logique et ajoutez ce déclencheur Dropbox : **Lorsqu’un fichier est créé**.</span><span class="sxs-lookup"><span data-stu-id="ab60f-113">Create a logic app, and add this Dropbox trigger: **When a file is created**</span></span> 
2. <span data-ttu-id="ab60f-114">Sous le déclencheur de hello, choisissez **étape suivante** > **ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="ab60f-114">Under hello trigger, choose **Next Step** > **Add an action**.</span></span> 
3. <span data-ttu-id="ab60f-115">Dans la zone de recherche de hello, entrez `file system` afin de pouvoir consulter les actions toutes prises en charge pour le connecteur du système de fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="ab60f-115">In hello search box, enter `file system` so you can view all supported actions for hello File System connector.</span></span>

   ![Rechercher le connecteur de fichiers](media/logic-apps-using-file-connector/search-file-connector.png)

2. <span data-ttu-id="ab60f-117">Choisissez hello **créer un fichier** action et créer un système de fichiers de connexion tooyour.</span><span class="sxs-lookup"><span data-stu-id="ab60f-117">Choose hello **Create file** action, and create a connection tooyour file system.</span></span>

   <span data-ttu-id="ab60f-118">Si vous n’avez pas une connexion existante, vous êtes invité à toocreate une.</span><span class="sxs-lookup"><span data-stu-id="ab60f-118">If you don't have an existing connection, you are prompted toocreate one.</span></span>

   1. <span data-ttu-id="ab60f-119">Choisissez **Se connecter via la passerelle de données locale**.</span><span class="sxs-lookup"><span data-stu-id="ab60f-119">Choose **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="ab60f-120">D’autres propriétés s’affichent.</span><span class="sxs-lookup"><span data-stu-id="ab60f-120">More properties appear.</span></span>
   2. <span data-ttu-id="ab60f-121">Sélectionnez le dossier racine de votre système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="ab60f-121">Select your root folder for your file system.</span></span>
      
       > [!NOTE]
       > <span data-ttu-id="ab60f-122">Hello dossier racine est hello parent principal, qui est utilisé pour les chemins d’accès relatifs pour toutes les actions liées aux fichiers.</span><span class="sxs-lookup"><span data-stu-id="ab60f-122">hello root folder is hello main parent folder, which is used for relative paths for all file-related actions.</span></span> <span data-ttu-id="ab60f-123">Vous pouvez spécifier un dossier local sur l’ordinateur hello où passerelle de données locale hello est installée ou dossier de hello peut être un partage réseau qui hello ordinateur peut accéder.</span><span class="sxs-lookup"><span data-stu-id="ab60f-123">You can specify a local folder on hello machine where hello on-premises data gateway is installed, or hello folder can be a network share that hello machine can access.</span></span>

   3. <span data-ttu-id="ab60f-124">Entrez hello username et password pour la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="ab60f-124">Enter hello username and password for hello gateway.</span></span>
   4. <span data-ttu-id="ab60f-125">Sélectionnez hello passerelle que vous avez installé précédemment.</span><span class="sxs-lookup"><span data-stu-id="ab60f-125">Select hello gateway that you previously installed.</span></span>

       ![Configurer la connexion](media/logic-apps-using-file-connector/create-file.png)

3. <span data-ttu-id="ab60f-127">Après avoir fourni tous les détails de hello, choisissez **créer**.</span><span class="sxs-lookup"><span data-stu-id="ab60f-127">After you provide all hello details, choose **Create**.</span></span> 

   <span data-ttu-id="ab60f-128">Logique d’applications configure et teste votre connexion, en veillant à ce que les connexions hello fonctionnement correctement.</span><span class="sxs-lookup"><span data-stu-id="ab60f-128">Logic Apps configures and tests your connection, making sure that hello connection works properly.</span></span> 
   <span data-ttu-id="ab60f-129">Si la connexion de hello est correctement configuré, vous voyez des options pour l’action hello que vous avez sélectionné précédemment.</span><span class="sxs-lookup"><span data-stu-id="ab60f-129">If hello connection is set up correctly, you see options for hello action that you previously selected.</span></span> 
   <span data-ttu-id="ab60f-130">connecteur de système de fichiers Hello est maintenant prêt à être utilisé.</span><span class="sxs-lookup"><span data-stu-id="ab60f-130">hello file system connector is now ready for use.</span></span>

4. <span data-ttu-id="ab60f-131">Spécifier que vous souhaitez toocopy les fichiers du dossier racine de toohello Dropbox pour le partage de fichiers local.</span><span class="sxs-lookup"><span data-stu-id="ab60f-131">Specify that you want toocopy files from Dropbox toohello root folder for your on-premises file share.</span></span>

   ![Créer une action de fichier](media/logic-apps-using-file-connector/create-file-filled.png)

5. <span data-ttu-id="ab60f-133">Une fois le fichier logique application copies hello, ajoutez une action d’Outlook qui envoie un message électronique afin que les utilisateurs concernés sachent sur le nouveau fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="ab60f-133">After your logic app copies hello file, add an Outlook action that sends an email so relevant users know about hello new file.</span></span> <span data-ttu-id="ab60f-134">Entrez les destinataires hello, titre et le corps des messages électroniques de hello.</span><span class="sxs-lookup"><span data-stu-id="ab60f-134">Enter hello recipients, title, and body of hello email.</span></span> 

   <span data-ttu-id="ab60f-135">Dans le sélecteur de contenu dynamique hello, vous pouvez choisir les sorties de données à partir du connecteur de fichier hello afin de pouvoir ajouter par courrier électronique des toohello plus de détails.</span><span class="sxs-lookup"><span data-stu-id="ab60f-135">In hello dynamic content selector, you can choose data outputs from hello file connector so you can add more details toohello email.</span></span>

   ![Envoyer l’action de messagerie](media/logic-apps-using-file-connector/send-email.png)

6. <span data-ttu-id="ab60f-137">Enregistrez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="ab60f-137">Save your logic app.</span></span> <span data-ttu-id="ab60f-138">Testez votre application en chargeant un fichier tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="ab60f-138">Test your app by uploading a file tooDropbox.</span></span> <span data-ttu-id="ab60f-139">fichier de Hello doit obtenir le partage de fichiers copiés toohello local, et vous devez recevoir un message électronique à propos de l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="ab60f-139">hello file should get copied toohello on-premises file share, and you should receive an email about hello operation.</span></span>

   > [!TIP] 
   > <span data-ttu-id="ab60f-140">Découvrez comment trop[surveiller vos applications logiques](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="ab60f-140">Learn how too[monitor your logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="ab60f-141">Félicitations, vous avez maintenant une application logique qui peut se connecter de système de fichiers local tooyour.</span><span class="sxs-lookup"><span data-stu-id="ab60f-141">Congratulations, you now have a working logic app that can connect tooyour on-premises file system.</span></span> <span data-ttu-id="ab60f-142">Essayez d’Explorer les autres fonctionnalités hello offres du connecteur, par exemple :</span><span class="sxs-lookup"><span data-stu-id="ab60f-142">Try exploring other functionalities that hello connector offers, for example:</span></span>

- <span data-ttu-id="ab60f-143">Créer un fichier</span><span class="sxs-lookup"><span data-stu-id="ab60f-143">Create file</span></span>
- <span data-ttu-id="ab60f-144">Répertorier les fichiers dans un dossier</span><span class="sxs-lookup"><span data-stu-id="ab60f-144">List files in folder</span></span>
- <span data-ttu-id="ab60f-145">Ajouter un fichier</span><span class="sxs-lookup"><span data-stu-id="ab60f-145">Append file</span></span>
- <span data-ttu-id="ab60f-146">Supprimer un fichier</span><span class="sxs-lookup"><span data-stu-id="ab60f-146">Delete file</span></span>
- <span data-ttu-id="ab60f-147">Obtenir le contenu d’un fichier</span><span class="sxs-lookup"><span data-stu-id="ab60f-147">Get file content</span></span>
- <span data-ttu-id="ab60f-148">Obtenir le contenu d’un fichier à l’aide du chemin</span><span class="sxs-lookup"><span data-stu-id="ab60f-148">Get file content using path</span></span>
- <span data-ttu-id="ab60f-149">Obtenir les métadonnées d’un fichier</span><span class="sxs-lookup"><span data-stu-id="ab60f-149">Get file metadata</span></span>
- <span data-ttu-id="ab60f-150">Obtenir les métadonnées d’un fichier à l’aide du chemin</span><span class="sxs-lookup"><span data-stu-id="ab60f-150">Get file metadata using path</span></span>
- <span data-ttu-id="ab60f-151">Répertorier les fichiers dans le dossier racine</span><span class="sxs-lookup"><span data-stu-id="ab60f-151">List files in root folder</span></span>
- <span data-ttu-id="ab60f-152">Mettre à jour un fichier</span><span class="sxs-lookup"><span data-stu-id="ab60f-152">Update file</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="ab60f-153">Swagger hello de vue</span><span class="sxs-lookup"><span data-stu-id="ab60f-153">View hello swagger</span></span>
<span data-ttu-id="ab60f-154">Consultez hello [swagger détails](/connectors/fileconnector/).</span><span class="sxs-lookup"><span data-stu-id="ab60f-154">See hello [swagger details](/connectors/fileconnector/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="ab60f-155">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="ab60f-155">Get help</span></span>

<span data-ttu-id="ab60f-156">tooask questions, répondre aux questions et savoir quels autres Azure Logic Apps font les utilisateurs, visitez hello [forum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="ab60f-156">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="ab60f-157">toohelp améliorer Azure Logic Apps et connecteurs, voter pour ou envoyer vos idées à hello [site de commentaires utilisateur Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="ab60f-157">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab60f-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ab60f-158">Next steps</span></span>

- <span data-ttu-id="ab60f-159">[Se connecter aux données local tooon](../logic-apps/logic-apps-gateway-connection.md) à partir d’applications de logique</span><span class="sxs-lookup"><span data-stu-id="ab60f-159">[Connect tooon-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
- <span data-ttu-id="ab60f-160">En savoir plus sur [l’intégration d’entreprise](../logic-apps/logic-apps-enterprise-integration-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ab60f-160">Learn about [enterprise integration](../logic-apps/logic-apps-enterprise-integration-overview.md)</span></span>
