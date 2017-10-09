---
title: "aaaBefore que vous déployez le Service d’applications sur la pile de Azure | Documents Microsoft"
description: "Toocomplete étapes avant de déployer le Service d’applications sur la pile de Azure"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: anwestg
ms.openlocfilehash: fad758232ef2795105036640c2a26abf3fa2c3c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="before-you-get-started-with-app-service-on-azure-stack"></a><span data-ttu-id="9fe7a-103">Avant de commencer avec App Service sur Azure Stack</span><span class="sxs-lookup"><span data-stu-id="9fe7a-103">Before you get started with App Service on Azure Stack</span></span>

<span data-ttu-id="9fe7a-104">Vous avez besoin de quelques éléments tooinstall du Service d’applications Azure sur la pile de Azure :</span><span class="sxs-lookup"><span data-stu-id="9fe7a-104">You need a few items tooinstall Azure App Service on Azure Stack:</span></span>

- <span data-ttu-id="9fe7a-105">Un déploiement terminé de hello [kit de développement Azure pile](azure-stack-run-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="9fe7a-105">A completed deployment of hello [Azure Stack development kit](azure-stack-run-powershell-script.md).</span></span>
- <span data-ttu-id="9fe7a-106">Suffisamment d’espace dans votre système Azure Stack pour un petit déploiement d’App Service sur Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="9fe7a-106">Enough space in your Azure Stack system for a small deployment of App Service on Azure Stack.</span></span>  <span data-ttu-id="9fe7a-107">Hello espace requis est d’environ 20 Go d’espace disque.</span><span class="sxs-lookup"><span data-stu-id="9fe7a-107">hello required space is roughly 20 GB of disk space.</span></span>
- <span data-ttu-id="9fe7a-108">Une image de machine virtuelle Windows Server à utiliser lorsque vous créez des machines virtuelles pour App Service sur Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="9fe7a-108">A Windows Server VM image for use when you create virtual machines for App Service on Azure Stack.</span></span>
- <span data-ttu-id="9fe7a-109">[Un serveur qui exécute SQL Server](#SQL-Server).</span><span class="sxs-lookup"><span data-stu-id="9fe7a-109">[A server that's running SQL Server](#SQL-Server).</span></span>

>[!NOTE] 
> <span data-ttu-id="9fe7a-110">Hello comme suit *tous les* ont lieu sur l’ordinateur hôte de pile de Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9fe7a-110">hello following steps *all* take place on hello Azure Stack host machine.</span></span>

<span data-ttu-id="9fe7a-111">toodeploy un fournisseur de ressources, vous devez exécuter hello PowerShell Integrated Scripting Environment (ISE) en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="9fe7a-111">toodeploy a resource provider, you must run hello PowerShell Integrated Scripting Environment (ISE) as an administrator.</span></span> <span data-ttu-id="9fe7a-112">Pour cette raison, vous devez tooallow cookies et JavaScript dans le profil d’Internet Explorer hello utiliser toosign dans tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9fe7a-112">For this reason, you need tooallow cookies and JavaScript in hello Internet Explorer profile that you use toosign in tooAzure Active Directory.</span></span>

## <a name="turn-off-internet-explorer-enhanced-security"></a><span data-ttu-id="9fe7a-113">Désactiver la sécurité renforcée d’Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="9fe7a-113">Turn off Internet Explorer enhanced security</span></span>

1.  <span data-ttu-id="9fe7a-114">Connectez-vous à ordinateur de kit de développement de Azure pile toohello en tant que **AzureStack/administrateur**, puis ouvrez **le Gestionnaire de serveur**.</span><span class="sxs-lookup"><span data-stu-id="9fe7a-114">Sign in toohello Azure Stack development kit machine as **AzureStack/administrator**, and then open **Server Manager**.</span></span>

2.  <span data-ttu-id="9fe7a-115">Désactivez la **Configuration de sécurité renforcée d’Internet Explorer** pour les administrateurs et les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9fe7a-115">Turn off **Internet Explorer Enhanced Security Configuration** for both admins and users.</span></span>

3.  <span data-ttu-id="9fe7a-116">Connectez-vous à ordinateur de kit de développement de Azure pile toohello en tant qu’administrateur, puis ouvrez **le Gestionnaire de serveur**.</span><span class="sxs-lookup"><span data-stu-id="9fe7a-116">Sign in toohello Azure Stack development kit machine as an administrator, and then open **Server Manager**.</span></span>

4.  <span data-ttu-id="9fe7a-117">Désactivez la **Configuration de sécurité renforcée d’Internet Explorer** pour les administrateurs et les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9fe7a-117">Turn off **Internet Explorer Enhanced Security Configuration** for both admins and users.</span></span>

## <a name="enable-cookies"></a><span data-ttu-id="9fe7a-118">Activer les cookies</span><span class="sxs-lookup"><span data-stu-id="9fe7a-118">Enable cookies</span></span>

1.  <span data-ttu-id="9fe7a-119">Sélectionnez **Démarrer** > **Toutes les applications** > **Accessoires Windows**.</span><span class="sxs-lookup"><span data-stu-id="9fe7a-119">Select **Start** > **All apps** > **Windows accessories**.</span></span> <span data-ttu-id="9fe7a-120">Cliquez avec le bouton droit sur **Internet Explorer** > **Plus** > **Exécuter en tant qu’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="9fe7a-120">Right-click **Internet Explorer** > **More** > **Run as an administrator**.</span></span>

2.  <span data-ttu-id="9fe7a-121">Si vous y êtes invité, sélectionnez **Utiliser la sécurité recommandée**, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="9fe7a-121">If you're prompted, select **Use recommended security**, and then select **OK**.</span></span>

3.  <span data-ttu-id="9fe7a-122">Dans Internet Explorer, sélectionnez **outils** (icône d’engrenage hello) > **Options Internet** > **confidentialité** > **avancé**.</span><span class="sxs-lookup"><span data-stu-id="9fe7a-122">In Internet Explorer, select **Tools** (hello gear icon) > **Internet Options** > **Privacy** > **Advanced**.</span></span>

4.  <span data-ttu-id="9fe7a-123">Sélectionnez **Advanced (Avancé)**.</span><span class="sxs-lookup"><span data-stu-id="9fe7a-123">Select **Advanced**.</span></span> <span data-ttu-id="9fe7a-124">Vérifiez que les deux cases **Accepter** sont cochées.</span><span class="sxs-lookup"><span data-stu-id="9fe7a-124">Make sure that both **Accept** check boxes are selected.</span></span> <span data-ttu-id="9fe7a-125">Sélectionnez **OK** deux fois.</span><span class="sxs-lookup"><span data-stu-id="9fe7a-125">Select **OK** twice.</span></span>

5.  <span data-ttu-id="9fe7a-126">Fermez Internet Explorer et redémarrez hello PowerShell ISE en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="9fe7a-126">Close Internet Explorer, and restart hello PowerShell ISE as an administrator.</span></span>

## <a name="install-powershell-for-azure-stack"></a><span data-ttu-id="9fe7a-127">Installer PowerShell pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="9fe7a-127">Install PowerShell for Azure Stack</span></span>

<span data-ttu-id="9fe7a-128">tooinstall PowerShell pour la pile de Azure, suivez les étapes de hello dans [installer PowerShell](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="9fe7a-128">tooinstall PowerShell for Azure Stack, follow hello steps in [Install PowerShell](azure-stack-powershell-install.md).</span></span>

## <a name="use-visual-studio-with-azure-stack"></a><span data-ttu-id="9fe7a-129">Utiliser Visual Studio avec Azure Stack</span><span class="sxs-lookup"><span data-stu-id="9fe7a-129">Use Visual Studio with Azure Stack</span></span>

<span data-ttu-id="9fe7a-130">toouse Visual Studio avec la pile d’Azure, suivez les étapes de hello dans [installer Visual Studio](azure-stack-install-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="9fe7a-130">toouse Visual Studio with Azure Stack, follow hello steps in [Install Visual Studio](azure-stack-install-visual-studio.md).</span></span>

## <a name="add-a-windows-server-2016-vm-image-tooazure-stack"></a><span data-ttu-id="9fe7a-131">Ajouter un tooAzure d’image de machine virtuelle de Windows Server 2016 pile</span><span class="sxs-lookup"><span data-stu-id="9fe7a-131">Add a Windows Server 2016 VM image tooAzure Stack</span></span>

<span data-ttu-id="9fe7a-132">Étant donné qu’App Service déploie plusieurs machines virtuelles, il requiert une image de machine virtuelle Windows Server 2016 dans Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="9fe7a-132">Because App Service deploys a number of virtual machines, it requires a Windows Server 2016 VM image in Azure Stack.</span></span> <span data-ttu-id="9fe7a-133">tooinstall une image de machine virtuelle, suivez les étapes de hello dans [ajouter une image de machine virtuelle par défaut](azure-stack-add-default-image.md).</span><span class="sxs-lookup"><span data-stu-id="9fe7a-133">tooinstall a VM image, follow hello steps in [Add a default virtual machine image](azure-stack-add-default-image.md).</span></span>

## <span data-ttu-id="9fe7a-134"><a name="SQL-Server"></a>SQL Server</span><span class="sxs-lookup"><span data-stu-id="9fe7a-134"><a name="SQL-Server"></a>SQL Server</span></span>

<span data-ttu-id="9fe7a-135">Service application sur Azure pile nécessite l’accès tooa SQL Server instance toocreate et hôte deux bases de données toorun hello fournisseur de ressources du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="9fe7a-135">App Service on Azure Stack requires access tooa SQL Server instance toocreate and host two databases toorun hello App Service resource provider.</span></span>  <span data-ttu-id="9fe7a-136">Si vous choisissez toodeploy une machine virtuelle SQL Server sur la pile Azure qu’il doit être le niveau de connectivité SQL hello trop**Public**.</span><span class="sxs-lookup"><span data-stu-id="9fe7a-136">Should you choose toodeploy a SQL Server VM on Azure Stack it must have hello SQL connectivity level set too**Public**.</span></span>  <span data-ttu-id="9fe7a-137">Vous pouvez choisir hello SQL Server instance toouse lorsque vous effectuez des options hello Bonjour du Service d’applications sur le programme d’installation de la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="9fe7a-137">You can choose hello SQL Server instance toouse when you complete hello options in hello App Service on Azure Stack installer.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fe7a-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9fe7a-138">Next steps</span></span>

- <span data-ttu-id="9fe7a-139">[Installer hello fournisseur de ressources du Service d’applications](azure-stack-app-service-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="9fe7a-139">[Install hello App Service resource provider](azure-stack-app-service-deploy.md).</span></span>

<!--Image references-->
[1]: ./media/azure-stack-app-service-before-you-get-started/PSGallery.png
[2]: ./media/azure-stack-app-service-before-you-get-started/WebPI_InstalledProducts.png
