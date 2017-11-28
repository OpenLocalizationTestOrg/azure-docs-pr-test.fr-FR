---
title: "Avant de déployer App Service sur Azure Stack | Microsoft Docs"
description: "Étapes à effectuer avant de déployer App Service sur Azure Stack"
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
ms.openlocfilehash: 3cba11acc6279f24d0a47af8978610180724c0a2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="before-you-get-started-with-app-service-on-azure-stack"></a><span data-ttu-id="fcb99-103">Avant de commencer avec App Service sur Azure Stack</span><span class="sxs-lookup"><span data-stu-id="fcb99-103">Before you get started with App Service on Azure Stack</span></span>

<span data-ttu-id="fcb99-104">Vous avez besoin de quelques éléments pour installer Azure App Service sur Azure Stack :</span><span class="sxs-lookup"><span data-stu-id="fcb99-104">You need a few items to install Azure App Service on Azure Stack:</span></span>

- <span data-ttu-id="fcb99-105">Un déploiement terminé du [Kit de développement Azure Stack](azure-stack-run-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="fcb99-105">A completed deployment of the [Azure Stack development kit](azure-stack-run-powershell-script.md).</span></span>
- <span data-ttu-id="fcb99-106">Suffisamment d’espace dans votre système Azure Stack pour un petit déploiement d’App Service sur Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="fcb99-106">Enough space in your Azure Stack system for a small deployment of App Service on Azure Stack.</span></span>  <span data-ttu-id="fcb99-107">L’espace requis est d’environ 20 Go d’espace disque.</span><span class="sxs-lookup"><span data-stu-id="fcb99-107">The required space is roughly 20 GB of disk space.</span></span>
- <span data-ttu-id="fcb99-108">Une image de machine virtuelle Windows Server à utiliser lorsque vous créez des machines virtuelles pour App Service sur Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="fcb99-108">A Windows Server VM image for use when you create virtual machines for App Service on Azure Stack.</span></span>
- <span data-ttu-id="fcb99-109">[Un serveur qui exécute SQL Server](#SQL-Server).</span><span class="sxs-lookup"><span data-stu-id="fcb99-109">[A server that's running SQL Server](#SQL-Server).</span></span>

>[!NOTE] 
> <span data-ttu-id="fcb99-110">Les étapes suivantes sont *toutes* exécutées sur l’ordinateur hôte Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="fcb99-110">The following steps *all* take place on the Azure Stack host machine.</span></span>

<span data-ttu-id="fcb99-111">Pour déployer un fournisseur de ressources, vous devez exécuter l’ISE PowerShell en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="fcb99-111">To deploy a resource provider, you must run the PowerShell Integrated Scripting Environment (ISE) as an administrator.</span></span> <span data-ttu-id="fcb99-112">Pour cette raison, vous devez autoriser les cookies et JavaScript dans le profil Internet Explorer que vous utilisez pour vous connecter à Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fcb99-112">For this reason, you need to allow cookies and JavaScript in the Internet Explorer profile that you use to sign in to Azure Active Directory.</span></span>

## <a name="turn-off-internet-explorer-enhanced-security"></a><span data-ttu-id="fcb99-113">Désactiver la sécurité renforcée d’Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="fcb99-113">Turn off Internet Explorer enhanced security</span></span>

1.  <span data-ttu-id="fcb99-114">Connectez-vous sur la machine du Kit de développement Azure Stack en tant que **AzureStack/administrator**, puis ouvrez le **Gestionnaire de serveur**.</span><span class="sxs-lookup"><span data-stu-id="fcb99-114">Sign in to the Azure Stack development kit machine as **AzureStack/administrator**, and then open **Server Manager**.</span></span>

2.  <span data-ttu-id="fcb99-115">Désactivez la **Configuration de sécurité renforcée d’Internet Explorer** pour les administrateurs et les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="fcb99-115">Turn off **Internet Explorer Enhanced Security Configuration** for both admins and users.</span></span>

3.  <span data-ttu-id="fcb99-116">Connectez-vous sur la machine du Kit de développement Azure Stack en tant qu’administrateur, puis ouvrez le **Gestionnaire de serveur**.</span><span class="sxs-lookup"><span data-stu-id="fcb99-116">Sign in to the Azure Stack development kit machine as an administrator, and then open **Server Manager**.</span></span>

4.  <span data-ttu-id="fcb99-117">Désactivez la **Configuration de sécurité renforcée d’Internet Explorer** pour les administrateurs et les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="fcb99-117">Turn off **Internet Explorer Enhanced Security Configuration** for both admins and users.</span></span>

## <a name="enable-cookies"></a><span data-ttu-id="fcb99-118">Activer les cookies</span><span class="sxs-lookup"><span data-stu-id="fcb99-118">Enable cookies</span></span>

1.  <span data-ttu-id="fcb99-119">Sélectionnez **Démarrer** > **Toutes les applications** > **Accessoires Windows**.</span><span class="sxs-lookup"><span data-stu-id="fcb99-119">Select **Start** > **All apps** > **Windows accessories**.</span></span> <span data-ttu-id="fcb99-120">Cliquez avec le bouton droit sur **Internet Explorer** > **Plus** > **Exécuter en tant qu’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="fcb99-120">Right-click **Internet Explorer** > **More** > **Run as an administrator**.</span></span>

2.  <span data-ttu-id="fcb99-121">Si vous y êtes invité, sélectionnez **Utiliser la sécurité recommandée**, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="fcb99-121">If you're prompted, select **Use recommended security**, and then select **OK**.</span></span>

3.  <span data-ttu-id="fcb99-122">Dans Internet Explorer, sélectionnez **Outils** (icône d’engrenage) > **Options Internet** > **Confidentialité** > **Avancé**.</span><span class="sxs-lookup"><span data-stu-id="fcb99-122">In Internet Explorer, select **Tools** (the gear icon) > **Internet Options** > **Privacy** > **Advanced**.</span></span>

4.  <span data-ttu-id="fcb99-123">Sélectionnez **Advanced (Avancé)**.</span><span class="sxs-lookup"><span data-stu-id="fcb99-123">Select **Advanced**.</span></span> <span data-ttu-id="fcb99-124">Vérifiez que les deux cases **Accepter** sont cochées.</span><span class="sxs-lookup"><span data-stu-id="fcb99-124">Make sure that both **Accept** check boxes are selected.</span></span> <span data-ttu-id="fcb99-125">Sélectionnez **OK** deux fois.</span><span class="sxs-lookup"><span data-stu-id="fcb99-125">Select **OK** twice.</span></span>

5.  <span data-ttu-id="fcb99-126">Fermez Internet Explorer et redémarrez l’ISE PowerShell en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="fcb99-126">Close Internet Explorer, and restart the PowerShell ISE as an administrator.</span></span>

## <a name="install-powershell-for-azure-stack"></a><span data-ttu-id="fcb99-127">Installer PowerShell pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="fcb99-127">Install PowerShell for Azure Stack</span></span>

<span data-ttu-id="fcb99-128">Pour installer PowerShell pour Azure Stack, suivez les étapes sous [Installer PowerShell](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="fcb99-128">To install PowerShell for Azure Stack, follow the steps in [Install PowerShell](azure-stack-powershell-install.md).</span></span>

## <a name="use-visual-studio-with-azure-stack"></a><span data-ttu-id="fcb99-129">Utiliser Visual Studio avec Azure Stack</span><span class="sxs-lookup"><span data-stu-id="fcb99-129">Use Visual Studio with Azure Stack</span></span>

<span data-ttu-id="fcb99-130">Pour utiliser Visual Studio avec Azure Stack, suivez les étapes sous [Installer Visual Studio](azure-stack-install-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="fcb99-130">To use Visual Studio with Azure Stack, follow the steps in [Install Visual Studio](azure-stack-install-visual-studio.md).</span></span>

## <a name="add-a-windows-server-2016-vm-image-to-azure-stack"></a><span data-ttu-id="fcb99-131">Ajouter une image de machine virtuelle Windows Server 2016 à Azure Stack</span><span class="sxs-lookup"><span data-stu-id="fcb99-131">Add a Windows Server 2016 VM image to Azure Stack</span></span>

<span data-ttu-id="fcb99-132">Étant donné qu’App Service déploie plusieurs machines virtuelles, il requiert une image de machine virtuelle Windows Server 2016 dans Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="fcb99-132">Because App Service deploys a number of virtual machines, it requires a Windows Server 2016 VM image in Azure Stack.</span></span> <span data-ttu-id="fcb99-133">Pour installer une image de machine virtuelle, suivez les étapes sous [Ajouter une image de machine virtuelle par défaut](azure-stack-add-default-image.md).</span><span class="sxs-lookup"><span data-stu-id="fcb99-133">To install a VM image, follow the steps in [Add a default virtual machine image](azure-stack-add-default-image.md).</span></span>

## <span data-ttu-id="fcb99-134"><a name="SQL-Server"></a>SQL Server</span><span class="sxs-lookup"><span data-stu-id="fcb99-134"><a name="SQL-Server"></a>SQL Server</span></span>

<span data-ttu-id="fcb99-135">App Service sur Azure Stack nécessite l’accès à une instance SQL Server pour créer et héberger deux bases de données afin d’exécuter le fournisseur de ressources App Service.</span><span class="sxs-lookup"><span data-stu-id="fcb99-135">App Service on Azure Stack requires access to a SQL Server instance to create and host two databases to run the App Service resource provider.</span></span>  <span data-ttu-id="fcb99-136">Si vous décidez de déployer une machine virtuelle SQL Server sur Azure Stack, son niveau de connectivité SQL doit être défini sur **Public**.</span><span class="sxs-lookup"><span data-stu-id="fcb99-136">Should you choose to deploy a SQL Server VM on Azure Stack it must have the SQL connectivity level set to **Public**.</span></span>  <span data-ttu-id="fcb99-137">Vous pouvez choisir l’instance SQL Server à utiliser lorsque vous choisissez les options dans le programme d’installation App Service sur Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="fcb99-137">You can choose the SQL Server instance to use when you complete the options in the App Service on Azure Stack installer.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fcb99-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fcb99-138">Next steps</span></span>

- <span data-ttu-id="fcb99-139">[Installer le fournisseur de ressources App Service](azure-stack-app-service-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="fcb99-139">[Install the App Service resource provider](azure-stack-app-service-deploy.md).</span></span>

<!--Image references-->
[1]: ./media/azure-stack-app-service-before-you-get-started/PSGallery.png
[2]: ./media/azure-stack-app-service-before-you-get-started/WebPI_InstalledProducts.png
