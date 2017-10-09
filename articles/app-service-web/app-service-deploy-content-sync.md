---
title: "contenu d’aaaSync à partir d’un tooAzure de dossier du Service d’applications cloud"
description: "En savoir plus toodeploy votre tooAzure d’application du Service d’applications via le contenu de la synchronisation à partir d’un dossier de cloud."
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
ms.openlocfilehash: e1c6d53a427c36126d9cdb33cc21b4126b9d9c2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sync-content-from-a-cloud-folder-tooazure-app-service"></a><span data-ttu-id="a20bd-103">Contenu de synchronisation à partir d’un tooAzure de dossier du Service d’applications cloud</span><span class="sxs-lookup"><span data-stu-id="a20bd-103">Sync content from a cloud folder tooAzure App Service</span></span>
<span data-ttu-id="a20bd-104">Ce didacticiel vous montre comment toodeploy trop[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) en synchronisant votre contenu à partir des services de stockage cloud populaires tels que Dropbox et OneDrive.</span><span class="sxs-lookup"><span data-stu-id="a20bd-104">This tutorial shows you how toodeploy too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by syncing your content from popular cloud storage services like Dropbox and OneDrive.</span></span> 

## <span data-ttu-id="a20bd-105"><a name="overview"></a>Vue d’ensemble du déploiement de la synchronisation de contenu</span><span class="sxs-lookup"><span data-stu-id="a20bd-105"><a name="overview"></a>Overview of content sync deployment</span></span>
<span data-ttu-id="a20bd-106">déploiement de la demande de synchronisation de contenu Hello est rendue possible par hello [moteur de déploiement Kudu](https://github.com/projectkudu/kudu/wiki) intégré avec le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="a20bd-106">hello on-demand content sync deployment is powered by hello [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki) integrated with App Service.</span></span> <span data-ttu-id="a20bd-107">Bonjour [Azure Portal](https://portal.azure.com), vous pouvez désigner un dossier dans votre stockage cloud, travailler avec votre code d’application et le contenu dans ce dossier et synchronisation tooApp Service avec hello sur un bouton.</span><span class="sxs-lookup"><span data-stu-id="a20bd-107">In hello [Azure Portal](https://portal.azure.com), you can designate a folder in your cloud storage, work with your app code and content in that folder, and sync tooApp Service with hello click of a button.</span></span> <span data-ttu-id="a20bd-108">Synchronisation de contenu utilise des processus de Kudu hello pour la génération et de déploiement.</span><span class="sxs-lookup"><span data-stu-id="a20bd-108">Content sync utilizes hello Kudu process for build and deployment.</span></span> 

## <span data-ttu-id="a20bd-109"><a name="contentsync"></a>Déploiement de la synchronisation tooenable contenu</span><span class="sxs-lookup"><span data-stu-id="a20bd-109"><a name="contentsync"></a>How tooenable content sync deployment</span></span>
<span data-ttu-id="a20bd-110">tooenable de synchronisation de contenu à partir de hello [Azure Portal](https://portal.azure.com), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a20bd-110">tooenable content sync from hello [Azure Portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="a20bd-111">Dans le panneau de votre application Bonjour portail Azure, cliquez sur **paramètres** > **Source du déploiement**.</span><span class="sxs-lookup"><span data-stu-id="a20bd-111">In your app's blade in hello Azure Portal, click **Settings** > **Deployment Source**.</span></span> <span data-ttu-id="a20bd-112">Cliquez sur **choisir la Source de**, puis sélectionnez **OneDrive** ou **Dropbox** en tant que source de hello pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="a20bd-112">Click **Choose Source**, then select **OneDrive** or **Dropbox** as hello source for deployment.</span></span> 
   
    ![Synchronisation de contenu](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > <span data-ttu-id="a20bd-114">En raison des différences sous-jacentes Bonjour API, **OneDrive entreprise** n’est pas prise en charge pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="a20bd-114">Because of underlying differences in hello APIs, **OneDrive for Business** is not supported at this time.</span></span> 
   > 
   > 
2. <span data-ttu-id="a20bd-115">Hello complète d’autorisation workflow tooenable tooaccess du Service d’applications spécifique prédéfinies chemin d’accès désigné pour OneDrive ou Dropbox où tout votre contenu du Service d’applications sera stocké.</span><span class="sxs-lookup"><span data-stu-id="a20bd-115">Complete hello authorization workflow tooenable App Service tooaccess a specific pre-defined designated path for OneDrive or Dropbox where all of your App Service content will be stored.</span></span>  
    <span data-ttu-id="a20bd-116">Après hello d’autorisation vous donne une plateforme de Service de l’application hello option toocreate un dossier de contenu sous hello désignée chemin d’accès au contenu ou toochoose un dossier de contenu existant dans ce chemin de contenu désigné.</span><span class="sxs-lookup"><span data-stu-id="a20bd-116">After authorization hello App Service platform will give you hello option toocreate a content folder under hello designated content path, or toochoose an existing content folder under this designated content path.</span></span> <span data-ttu-id="a20bd-117">les chemins de contenu Hello désigné sous vos comptes de stockage cloud utilisés pour la synchronisation du Service d’applications sont les suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="a20bd-117">hello designated content paths under your cloud storage accounts used for App Service sync are hello following:</span></span>  
   
   * <span data-ttu-id="a20bd-118">**OneDrive** : `Apps\Azure Web Apps`</span><span class="sxs-lookup"><span data-stu-id="a20bd-118">**OneDrive**: `Apps\Azure Web Apps`</span></span> 
   * <span data-ttu-id="a20bd-119">**Dropbox** : `Dropbox\Apps\Azure`</span><span class="sxs-lookup"><span data-stu-id="a20bd-119">**Dropbox**: `Dropbox\Apps\Azure`</span></span>
3. <span data-ttu-id="a20bd-120">Après avoir hello de synchronisation de contenu hello initiale de synchronisation de contenu peut être lancée à la demande de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a20bd-120">After hello initial content sync hello content sync can be initiated on demand from hello Azure portal.</span></span> <span data-ttu-id="a20bd-121">L’historique de déploiement est disponible avec hello **déploiements** panneau.</span><span class="sxs-lookup"><span data-stu-id="a20bd-121">Deployment history is available with hello **Deployments** blade.</span></span>
   
    ![Historique des déploiements](./media/app-service-deploy-content-sync/onedrive_sync.png)

<span data-ttu-id="a20bd-123">Vous trouverez plus d’informations pour le déploiement Dropbox sous [Déployer à partir de Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span><span class="sxs-lookup"><span data-stu-id="a20bd-123">More information for Dropbox deployment is available under [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span></span> 

