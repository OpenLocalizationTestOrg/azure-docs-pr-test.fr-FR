---
title: "Synchronisation de contenu à partir d’un dossier cloud dans Azure App Service"
description: "Apprenez à déployer votre application dans Azure App Service via la synchronisation de contenu à partir d’un dossier cloud."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 88d3a670-303a-4fa2-9de9-715cc904acec
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 010e7dc492abefaa3afe814c0322af9f6fe5acd2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="sync-content-from-a-cloud-folder-to-azure-app-service"></a><span data-ttu-id="1abb9-103">Synchronisation de contenu à partir d’un dossier cloud dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="1abb9-103">Sync content from a cloud folder to Azure App Service</span></span>
<span data-ttu-id="1abb9-104">Ce didacticiel vous montre comment déployer dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) en synchronisant votre contenu à partir de services de stockage cloud populaires, tels que Dropbox et OneDrive.</span><span class="sxs-lookup"><span data-stu-id="1abb9-104">This tutorial shows you how to deploy to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by syncing your content from popular cloud storage services like Dropbox and OneDrive.</span></span> 

## <span data-ttu-id="1abb9-105"><a name="overview"></a>Vue d’ensemble du déploiement de la synchronisation de contenu</span><span class="sxs-lookup"><span data-stu-id="1abb9-105"><a name="overview"></a>Overview of content sync deployment</span></span>
<span data-ttu-id="1abb9-106">Le déploiement à la demande de synchronisation de contenu est généré par le [moteur de déploiement Kudu](https://github.com/projectkudu/kudu/wiki) intégré à App Service.</span><span class="sxs-lookup"><span data-stu-id="1abb9-106">The on-demand content sync deployment is powered by the [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki) integrated with App Service.</span></span> <span data-ttu-id="1abb9-107">Dans le [portail Azure](https://portal.azure.com), vous pouvez désigner un dossier dans votre stockage cloud, travailler avec votre code d’application et votre contenu dans ce dossier et à synchroniser avec App Service sur un simple clic.</span><span class="sxs-lookup"><span data-stu-id="1abb9-107">In the [Azure Portal](https://portal.azure.com), you can designate a folder in your cloud storage, work with your app code and content in that folder, and sync to App Service with the click of a button.</span></span> <span data-ttu-id="1abb9-108">La synchronisation de contenu utilise le processus Kudu pour la génération et le déploiement.</span><span class="sxs-lookup"><span data-stu-id="1abb9-108">Content sync utilizes the Kudu process for build and deployment.</span></span> 

## <span data-ttu-id="1abb9-109"><a name="contentsync"></a>Activation du déploiement de la synchronisation de contenu</span><span class="sxs-lookup"><span data-stu-id="1abb9-109"><a name="contentsync"></a>How to enable content sync deployment</span></span>
<span data-ttu-id="1abb9-110">Pour activer la synchronisation de contenu à partir du [portail Azure](https://portal.azure.com), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1abb9-110">To enable content sync from the [Azure Portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="1abb9-111">Dans le portail Azure, dans le panneau de votre application, cliquez sur **Paramètres** > **Source du déploiement**.</span><span class="sxs-lookup"><span data-stu-id="1abb9-111">In your app's blade in the Azure Portal, click **Settings** > **Deployment Source**.</span></span> <span data-ttu-id="1abb9-112">Cliquez sur **Choisir une source**, puis sélectionnez **OneDrive** ou **Dropbox** comme source pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="1abb9-112">Click **Choose Source**, then select **OneDrive** or **Dropbox** as the source for deployment.</span></span> 
   
    ![Synchronisation de contenu](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > <span data-ttu-id="1abb9-114">En raison de différences sous-jacentes entre les API, **OneDrive Entreprise** n’est pas pris en charge pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="1abb9-114">Because of underlying differences in the APIs, **OneDrive for Business** is not supported at this time.</span></span> 
   > 
   > 
2. <span data-ttu-id="1abb9-115">Complétez le flux de travail d’autorisation pour permettre à App Service d’accéder à un chemin spécifique désigné prédéfini pour OneDrive ou Dropbox, où votre contenu App Service sera stocké.</span><span class="sxs-lookup"><span data-stu-id="1abb9-115">Complete the authorization workflow to enable App Service to access a specific pre-defined designated path for OneDrive or Dropbox where all of your App Service content will be stored.</span></span>  
    <span data-ttu-id="1abb9-116">Après l’autorisation, la plateforme App Service vous donnera la possibilité de créer un dossier de contenu sous le chemin d’accès au contenu désigné ou de choisir un dossier de contenu existant sous ce chemin d’accès au contenu désigné.</span><span class="sxs-lookup"><span data-stu-id="1abb9-116">After authorization the App Service platform will give you the option to create a content folder under the designated content path, or to choose an existing content folder under this designated content path.</span></span> <span data-ttu-id="1abb9-117">Les chemins d’accès de contenu désignés dans vos comptes de stockage cloud utilisés pour la synchronisation App Service sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="1abb9-117">The designated content paths under your cloud storage accounts used for App Service sync are the following:</span></span>  
   
   * <span data-ttu-id="1abb9-118">**OneDrive** : `Apps\Azure Web Apps`</span><span class="sxs-lookup"><span data-stu-id="1abb9-118">**OneDrive**: `Apps\Azure Web Apps`</span></span> 
   * <span data-ttu-id="1abb9-119">**Dropbox** : `Dropbox\Apps\Azure`</span><span class="sxs-lookup"><span data-stu-id="1abb9-119">**Dropbox**: `Dropbox\Apps\Azure`</span></span>
3. <span data-ttu-id="1abb9-120">Après la synchronisation initiale du contenu, la synchronisation de contenu peut être lancée à la demande à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1abb9-120">After the initial content sync the content sync can be initiated on demand from the Azure portal.</span></span> <span data-ttu-id="1abb9-121">L’historique de déploiement est disponible dans le panneau **Déploiements** .</span><span class="sxs-lookup"><span data-stu-id="1abb9-121">Deployment history is available with the **Deployments** blade.</span></span>
   
    ![Historique des déploiements](./media/app-service-deploy-content-sync/onedrive_sync.png)

<span data-ttu-id="1abb9-123">Vous trouverez plus d’informations pour le déploiement Dropbox sous [Déployer à partir de Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span><span class="sxs-lookup"><span data-stu-id="1abb9-123">More information for Dropbox deployment is available under [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span></span> 

