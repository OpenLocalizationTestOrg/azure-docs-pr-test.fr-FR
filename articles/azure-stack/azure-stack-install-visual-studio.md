---
title: aaaInstall Visual Studio et connectez-vous tooAzure pile | Documents Microsoft
description: "Découvrez les étapes de hello requises tooinstall Visual Studio et connectez-vous tooAzure pile"
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 2022dbe5-47fd-457d-9af3-6c01688171d7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: aa63f9eaf5cd72a0b2f31256c2df99fb41ca11fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-connect-tooazure-stack"></a><span data-ttu-id="b0017-103">Installation de Visual Studio et connectez-vous tooAzure pile</span><span class="sxs-lookup"><span data-stu-id="b0017-103">Install Visual Studio and connect tooAzure Stack</span></span>

<span data-ttu-id="b0017-104">Utilisation des tooauthor de Visual Studio et le déploiement d’Azure Resource Manager [modèles](azure-stack-arm-templates.md) dans la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="b0017-104">Use Visual Studio tooauthor and deploy Azure Resource Manager [templates](azure-stack-arm-templates.md) in Azure Stack.</span></span> <span data-ttu-id="b0017-105">Vous pouvez utiliser hello les étapes décrites dans cette tooinstall article Visual Studio, soit à partir de [Kit de développement Azure pile](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), ou à partir d’un client externe basé sur Windows si vous êtes connecté via [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span><span class="sxs-lookup"><span data-stu-id="b0017-105">You can use hello steps described in this article tooinstall Visual Studio either from [Azure Stack Development Kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are connected through [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span></span> <span data-ttu-id="b0017-106">Ces étapes effectuent une nouvelle installation de Visual Studio 2015 Community Edition.</span><span class="sxs-lookup"><span data-stu-id="b0017-106">These steps perform a new installation of Visual Studio 2015 Community Edition.</span></span> <span data-ttu-id="b0017-107">Pour en savoir plus sur la coexistence entre d’autres versions de Visual Studio, consultez [cet article](https://msdn.microsoft.com/library/ms246609.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0017-107">Read more about [coexistence](https://msdn.microsoft.com/library/ms246609.aspx) between other Visual Studio versions.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="b0017-108">Installation de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b0017-108">Install Visual Studio</span></span>
1. <span data-ttu-id="b0017-109">Téléchargez et exécutez hello [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0017-109">Download and run hello [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>             
2. <span data-ttu-id="b0017-110">Recherchez **Visual Studio Community 2015 avec Microsoft Azure SDK - 2.9.6**, cliquez sur **Ajouter**, puis **Installer**.</span><span class="sxs-lookup"><span data-stu-id="b0017-110">Search for **Visual Studio Community 2015 with Microsoft Azure SDK - 2.9.6**, click **Add**, and **Install**.</span></span>

    ![Capture d’écran des étapes d’installation de WebPI](./media/azure-stack-install-visual-studio/image1.png) 

3. <span data-ttu-id="b0017-112">Désinstaller hello **Microsoft Azure PowerShell** qui est installé dans le cadre de hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="b0017-112">Uninstall hello **Microsoft Azure PowerShell** that is installed as part of hello Azure SDK.</span></span>

    ![Capture d’écran de l’interface Ajout/Suppression de programmes pour Azure PowerShell](./media/azure-stack-install-visual-studio/image2.png) 

4. [<span data-ttu-id="b0017-114">Installer PowerShell pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b0017-114">Install PowerShell for Azure Stack</span></span>](azure-stack-powershell-install.md)

5. <span data-ttu-id="b0017-115">Redémarrez le système d’exploitation de hello après l’installation de hello.</span><span class="sxs-lookup"><span data-stu-id="b0017-115">Restart hello operating system after hello installation completes.</span></span>

## <a name="connect-tooazure-stack"></a><span data-ttu-id="b0017-116">Se connecter tooAzure pile</span><span class="sxs-lookup"><span data-stu-id="b0017-116">Connect tooAzure Stack</span></span>

1. <span data-ttu-id="b0017-117">Lancez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b0017-117">Launch Visual Studio.</span></span>

2. <span data-ttu-id="b0017-118">À partir de hello **vue** menu, sélectionnez **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="b0017-118">From hello **View** menu, select **Cloud Explorer**.</span></span>

3. <span data-ttu-id="b0017-119">Dans le volet de nouveau hello, sélectionnez **ajouter un compte** et connectez-vous avec vos informations d’identification Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b0017-119">In hello new pane, select **Add Account** and sign in with your Azure Active Directory credentials.</span></span>  
    <span data-ttu-id="b0017-120">![Capture d’écran de Cloud Explorer, une fois connecté et connecté tooAzure pile](./media/azure-stack-install-visual-studio/image6.png)</span><span class="sxs-lookup"><span data-stu-id="b0017-120">![Screenshot of Cloud Explorer once logged in and connected tooAzure Stack](./media/azure-stack-install-visual-studio/image6.png)</span></span>

<span data-ttu-id="b0017-121">Une fois connecté, vous pouvez [déployer des modèles](azure-stack-deploy-template-visual-studio.md) ou parcourir les types de ressources disponibles et des groupes de ressources toocreate vos propres modèles.</span><span class="sxs-lookup"><span data-stu-id="b0017-121">Once logged in, you can [deploy templates](azure-stack-deploy-template-visual-studio.md) or browse available resource types and resource groups toocreate your own templates.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="b0017-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b0017-122">Next Steps</span></span>

 - [<span data-ttu-id="b0017-123">Développer des modèles pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b0017-123">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
