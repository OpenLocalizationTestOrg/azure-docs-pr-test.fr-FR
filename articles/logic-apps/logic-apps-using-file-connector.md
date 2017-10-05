---
title: "Se connecter aux systèmes de fichiers locaux à partir d’Azure Logic Apps | Microsoft Docs"
description: "Se connecter à un système de fichiers local à partir du flux de travail d’applications logiques par le biais de la passerelle de données locale et du connecteur du système de fichiers"
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
ms.openlocfilehash: f33e7c58103c57e17e4e273caba1ab9b83f0cd2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-on-premises-file-systems-from-logic-apps-with-the-file-system-connector"></a><span data-ttu-id="79ad6-104">Se connecter aux systèmes de fichiers local à partir d’applications logiques avec le connecteur du système de fichiers</span><span class="sxs-lookup"><span data-stu-id="79ad6-104">Connect to on-premises file systems from logic apps with the File System connector</span></span>

<span data-ttu-id="79ad6-105">La connectivité cloud hybride est essentielle pour les applications logiques ; par conséquent, pour gérer les données et accéder en toute sécurité aux ressources locales, vos applications logiques peuvent utiliser la passerelle de données locale.</span><span class="sxs-lookup"><span data-stu-id="79ad6-105">Hybrid cloud connectivity is central to logic apps, so to manage data and securely access on-premises resources, your logic apps can use the on-premises data gateway.</span></span> <span data-ttu-id="79ad6-106">Dans cet article, nous montrons comment se connecter à un système de fichiers local avec un scénario de base : copie d’un fichier chargé sur Dropbox vers un partage de fichiers, puis envoi d’un e-mail.</span><span class="sxs-lookup"><span data-stu-id="79ad6-106">In this article, we show how to connect to an on-premises file system with a basic scenario: copy a file that's uploaded to Dropbox to a file share, then send an email.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79ad6-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="79ad6-107">Prerequisites</span></span>

- <span data-ttu-id="79ad6-108">Installez et configurez la toute dernière [passerelle de données locale](https://www.microsoft.com/download/details.aspx?id=53127).</span><span class="sxs-lookup"><span data-stu-id="79ad6-108">Install and configure the latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127).</span></span>
- <span data-ttu-id="79ad6-109">Installez la dernière passerelle de données locale, version 1.15.6150.1 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="79ad6-109">Install the latest on-premises data gateway, version 1.15.6150.1 or above.</span></span> <span data-ttu-id="79ad6-110">La rubrique [Se connecter à la passerelle de données locale](http://aka.ms/logicapps-gateway) répertorie les étapes nécessaires.</span><span class="sxs-lookup"><span data-stu-id="79ad6-110">[Connect to the on-premises data gateway](http://aka.ms/logicapps-gateway) lists the steps.</span></span> <span data-ttu-id="79ad6-111">La passerelle doit être installée sur un ordinateur local avant de pouvoir effectuer le reste des étapes.</span><span class="sxs-lookup"><span data-stu-id="79ad6-111">The gateway must be installed on an on-premises machine before you can continue with the rest of the steps.</span></span>

## <a name="add-trigger-and-actions-for-connecting-to-your-file-system"></a><span data-ttu-id="79ad6-112">Ajouter un déclencheur et des actions pour se connecter au système de fichiers</span><span class="sxs-lookup"><span data-stu-id="79ad6-112">Add trigger and actions for connecting to your file system</span></span>

1. <span data-ttu-id="79ad6-113">Créez une application logique et ajoutez ce déclencheur Dropbox : **Lorsqu’un fichier est créé**.</span><span class="sxs-lookup"><span data-stu-id="79ad6-113">Create a logic app, and add this Dropbox trigger: **When a file is created**</span></span> 
2. <span data-ttu-id="79ad6-114">Sous le déclencheur, choisissez **Étape suivante** > **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="79ad6-114">Under the trigger, choose **Next Step** > **Add an action**.</span></span> 
3. <span data-ttu-id="79ad6-115">Dans la zone de recherche, entrez `file system` pour afficher toutes les actions prises en charge pour le connecteur du système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="79ad6-115">In the search box, enter `file system` so you can view all supported actions for the File System connector.</span></span>

   ![Rechercher le connecteur de fichiers](media/logic-apps-using-file-connector/search-file-connector.png)

2. <span data-ttu-id="79ad6-117">Choisissez l’action **Créer un fichier** et créez une connexion à votre système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="79ad6-117">Choose the **Create file** action, and create a connection to your file system.</span></span>

   <span data-ttu-id="79ad6-118">Si vous n’avez pas de connexion existante, vous êtes invité à en créer une.</span><span class="sxs-lookup"><span data-stu-id="79ad6-118">If you don't have an existing connection, you are prompted to create one.</span></span>

   1. <span data-ttu-id="79ad6-119">Choisissez **Se connecter via la passerelle de données locale**.</span><span class="sxs-lookup"><span data-stu-id="79ad6-119">Choose **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="79ad6-120">D’autres propriétés s’affichent.</span><span class="sxs-lookup"><span data-stu-id="79ad6-120">More properties appear.</span></span>
   2. <span data-ttu-id="79ad6-121">Sélectionnez le dossier racine de votre système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="79ad6-121">Select your root folder for your file system.</span></span>
      
       > [!NOTE]
       > <span data-ttu-id="79ad6-122">Le dossier racine est le dossier parent principal qui est utilisé pour les chemins relatifs de toutes les actions liées aux fichiers.</span><span class="sxs-lookup"><span data-stu-id="79ad6-122">The root folder is the main parent folder, which is used for relative paths for all file-related actions.</span></span> <span data-ttu-id="79ad6-123">Vous pouvez spécifier un dossier local situé sur la machine où est installée la passerelle de données locale ; il peut également s’agir d’un partage réseau auquel la machine a accès.</span><span class="sxs-lookup"><span data-stu-id="79ad6-123">You can specify a local folder on the machine where the on-premises data gateway is installed, or the folder can be a network share that the machine can access.</span></span>

   3. <span data-ttu-id="79ad6-124">Entrez le nom d’utilisateur et le mot de passe de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="79ad6-124">Enter the username and password for the gateway.</span></span>
   4. <span data-ttu-id="79ad6-125">Sélectionnez la passerelle que vous avez installée précédemment.</span><span class="sxs-lookup"><span data-stu-id="79ad6-125">Select the gateway that you previously installed.</span></span>

       ![Configurer la connexion](media/logic-apps-using-file-connector/create-file.png)

3. <span data-ttu-id="79ad6-127">Après avoir fourni tous les détails, choisissez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="79ad6-127">After you provide all the details, choose **Create**.</span></span> 

   <span data-ttu-id="79ad6-128">Logic Apps configure et teste votre connexion pour vérifier son bon fonctionnement.</span><span class="sxs-lookup"><span data-stu-id="79ad6-128">Logic Apps configures and tests your connection, making sure that the connection works properly.</span></span> 
   <span data-ttu-id="79ad6-129">Si la connexion est correctement configurée, des options s’affichent pour l’action sélectionnée précédemment.</span><span class="sxs-lookup"><span data-stu-id="79ad6-129">If the connection is set up correctly, you see options for the action that you previously selected.</span></span> 
   <span data-ttu-id="79ad6-130">Le connecteur Système de fichiers est maintenant prêt à être utilisé.</span><span class="sxs-lookup"><span data-stu-id="79ad6-130">The file system connector is now ready for use.</span></span>

4. <span data-ttu-id="79ad6-131">Spécifiez que vous souhaitez copier des fichiers de Dropbox vers le dossier racine de votre partage de fichiers local.</span><span class="sxs-lookup"><span data-stu-id="79ad6-131">Specify that you want to copy files from Dropbox to the root folder for your on-premises file share.</span></span>

   ![Créer une action de fichier](media/logic-apps-using-file-connector/create-file-filled.png)

5. <span data-ttu-id="79ad6-133">Une fois que votre application logique a copié le fichier, ajoutez une action d’Outlook qui envoie un e-mail afin que les utilisateurs concernés soient informés de la présence du nouveau fichier.</span><span class="sxs-lookup"><span data-stu-id="79ad6-133">After your logic app copies the file, add an Outlook action that sends an email so relevant users know about the new file.</span></span> <span data-ttu-id="79ad6-134">Saisissez les destinataires, l’objet et le corps de l’e-mail.</span><span class="sxs-lookup"><span data-stu-id="79ad6-134">Enter the recipients, title, and body of the email.</span></span> 

   <span data-ttu-id="79ad6-135">Dans le sélecteur de contenu dynamique, vous pouvez choisir les sorties de données du connecteur de fichier pour pouvoir ajouter plus de détails à l’adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="79ad6-135">In the dynamic content selector, you can choose data outputs from the file connector so you can add more details to the email.</span></span>

   ![Envoyer l’action de messagerie](media/logic-apps-using-file-connector/send-email.png)

6. <span data-ttu-id="79ad6-137">Enregistrez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="79ad6-137">Save your logic app.</span></span> <span data-ttu-id="79ad6-138">Testez votre application en chargeant un fichier sur Dropbox.</span><span class="sxs-lookup"><span data-stu-id="79ad6-138">Test your app by uploading a file to Dropbox.</span></span> <span data-ttu-id="79ad6-139">Le fichier se copie sur le partage de fichiers local et vous recevrez un e-mail concernant l’opération.</span><span class="sxs-lookup"><span data-stu-id="79ad6-139">The file should get copied to the on-premises file share, and you should receive an email about the operation.</span></span>

   > [!TIP] 
   > <span data-ttu-id="79ad6-140">Apprenez à [surveiller vos applications logiques](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="79ad6-140">Learn how to [monitor your logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="79ad6-141">Félicitations, vous avez maintenant une application logique en état de fonctionnement qui peut se connecter à votre système de fichiers local.</span><span class="sxs-lookup"><span data-stu-id="79ad6-141">Congratulations, you now have a working logic app that can connect to your on-premises file system.</span></span> <span data-ttu-id="79ad6-142">Essayez de découvrir les autres fonctionnalités offertes par le connecteur, par exemple :</span><span class="sxs-lookup"><span data-stu-id="79ad6-142">Try exploring other functionalities that the connector offers, for example:</span></span>

- <span data-ttu-id="79ad6-143">Créer un fichier</span><span class="sxs-lookup"><span data-stu-id="79ad6-143">Create file</span></span>
- <span data-ttu-id="79ad6-144">Répertorier les fichiers dans un dossier</span><span class="sxs-lookup"><span data-stu-id="79ad6-144">List files in folder</span></span>
- <span data-ttu-id="79ad6-145">Ajouter un fichier</span><span class="sxs-lookup"><span data-stu-id="79ad6-145">Append file</span></span>
- <span data-ttu-id="79ad6-146">Supprimer un fichier</span><span class="sxs-lookup"><span data-stu-id="79ad6-146">Delete file</span></span>
- <span data-ttu-id="79ad6-147">Obtenir le contenu d’un fichier</span><span class="sxs-lookup"><span data-stu-id="79ad6-147">Get file content</span></span>
- <span data-ttu-id="79ad6-148">Obtenir le contenu d’un fichier à l’aide du chemin</span><span class="sxs-lookup"><span data-stu-id="79ad6-148">Get file content using path</span></span>
- <span data-ttu-id="79ad6-149">Obtenir les métadonnées d’un fichier</span><span class="sxs-lookup"><span data-stu-id="79ad6-149">Get file metadata</span></span>
- <span data-ttu-id="79ad6-150">Obtenir les métadonnées d’un fichier à l’aide du chemin</span><span class="sxs-lookup"><span data-stu-id="79ad6-150">Get file metadata using path</span></span>
- <span data-ttu-id="79ad6-151">Répertorier les fichiers dans le dossier racine</span><span class="sxs-lookup"><span data-stu-id="79ad6-151">List files in root folder</span></span>
- <span data-ttu-id="79ad6-152">Mettre à jour un fichier</span><span class="sxs-lookup"><span data-stu-id="79ad6-152">Update file</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="79ad6-153">Afficher Swagger</span><span class="sxs-lookup"><span data-stu-id="79ad6-153">View the swagger</span></span>
<span data-ttu-id="79ad6-154">Consultez les [détails sur Swagger](/connectors/fileconnector/).</span><span class="sxs-lookup"><span data-stu-id="79ad6-154">See the [swagger details](/connectors/fileconnector/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="79ad6-155">Obtenir de l'aide</span><span class="sxs-lookup"><span data-stu-id="79ad6-155">Get help</span></span>

<span data-ttu-id="79ad6-156">Pour poser des questions ou y répondre et voir ce que font les autres utilisateurs d’Azure Logic Apps, visitez le [Forum Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="79ad6-156">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="79ad6-157">Afin d’améliorer Azure Logic Apps ainsi que les connecteurs, votez pour des idées ou soumettez-en sur le [site de commentaires utilisateur Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="79ad6-157">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="79ad6-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="79ad6-158">Next steps</span></span>

- <span data-ttu-id="79ad6-159">[Se connecter à des données locales](../logic-apps/logic-apps-gateway-connection.md) à partir d’applications logiques</span><span class="sxs-lookup"><span data-stu-id="79ad6-159">[Connect to on-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
- <span data-ttu-id="79ad6-160">En savoir plus sur [l’intégration d’entreprise](../logic-apps/logic-apps-enterprise-integration-overview.md)</span><span class="sxs-lookup"><span data-stu-id="79ad6-160">Learn about [enterprise integration](../logic-apps/logic-apps-enterprise-integration-overview.md)</span></span>
