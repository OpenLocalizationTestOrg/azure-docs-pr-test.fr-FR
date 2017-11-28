---
title: "Installer Visual Studio et se connecter à Azure Stack | Microsoft Docs"
description: "Découvrez les étapes nécessaires pour installer Visual Studio et se connecter à Azure Stack."
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
ms.openlocfilehash: 62ad9ebfd829d9555b9e4bc70f8a7f0c8ff0f901
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="install-visual-studio-and-connect-to-azure-stack"></a><span data-ttu-id="45b2c-103">Installer Visual Studio et se connecter à Azure Stack</span><span class="sxs-lookup"><span data-stu-id="45b2c-103">Install Visual Studio and connect to Azure Stack</span></span>

<span data-ttu-id="45b2c-104">Utilisez Visual Studio pour créer et déployer des [modèles](azure-stack-arm-templates.md) Azure Resource Manager dans Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="45b2c-104">Use Visual Studio to author and deploy Azure Resource Manager [templates](azure-stack-arm-templates.md) in Azure Stack.</span></span> <span data-ttu-id="45b2c-105">Vous pouvez utiliser les étapes décrites dans cet article pour installer Visual Studio à partir du [Kit de développement Azure Stack](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop) ou à partir d’un client externe Windows si vous êtes connecté par le biais d’un [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span><span class="sxs-lookup"><span data-stu-id="45b2c-105">You can use the steps described in this article to install Visual Studio either from [Azure Stack Development Kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are connected through [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span></span> <span data-ttu-id="45b2c-106">Ces étapes effectuent une nouvelle installation de Visual Studio 2015 Community Edition.</span><span class="sxs-lookup"><span data-stu-id="45b2c-106">These steps perform a new installation of Visual Studio 2015 Community Edition.</span></span> <span data-ttu-id="45b2c-107">Pour en savoir plus sur la coexistence entre d’autres versions de Visual Studio, consultez [cet article](https://msdn.microsoft.com/library/ms246609.aspx).</span><span class="sxs-lookup"><span data-stu-id="45b2c-107">Read more about [coexistence](https://msdn.microsoft.com/library/ms246609.aspx) between other Visual Studio versions.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="45b2c-108">Installation de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="45b2c-108">Install Visual Studio</span></span>
1. <span data-ttu-id="45b2c-109">Téléchargez et exécutez [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="45b2c-109">Download and run the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>             
2. <span data-ttu-id="45b2c-110">Recherchez **Visual Studio Community 2015 avec Microsoft Azure SDK - 2.9.6**, cliquez sur **Ajouter**, puis **Installer**.</span><span class="sxs-lookup"><span data-stu-id="45b2c-110">Search for **Visual Studio Community 2015 with Microsoft Azure SDK - 2.9.6**, click **Add**, and **Install**.</span></span>

    ![Capture d’écran des étapes d’installation de WebPI](./media/azure-stack-install-visual-studio/image1.png) 

3. <span data-ttu-id="45b2c-112">Désinstallez la version de **Microsoft Azure PowerShell** installée dans le cadre du SDK Azure.</span><span class="sxs-lookup"><span data-stu-id="45b2c-112">Uninstall the **Microsoft Azure PowerShell** that is installed as part of the Azure SDK.</span></span>

    ![Capture d’écran de l’interface Ajout/Suppression de programmes pour Azure PowerShell](./media/azure-stack-install-visual-studio/image2.png) 

4. [<span data-ttu-id="45b2c-114">Installer PowerShell pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="45b2c-114">Install PowerShell for Azure Stack</span></span>](azure-stack-powershell-install.md)

5. <span data-ttu-id="45b2c-115">Redémarrez le système d’exploitation après l’installation.</span><span class="sxs-lookup"><span data-stu-id="45b2c-115">Restart the operating system after the installation completes.</span></span>

## <a name="connect-to-azure-stack"></a><span data-ttu-id="45b2c-116">Se connecter à Azure Stack</span><span class="sxs-lookup"><span data-stu-id="45b2c-116">Connect to Azure Stack</span></span>

1. <span data-ttu-id="45b2c-117">Lancez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="45b2c-117">Launch Visual Studio.</span></span>

2. <span data-ttu-id="45b2c-118">Dans le menu **Affichage**, sélectionnez **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="45b2c-118">From the **View** menu, select **Cloud Explorer**.</span></span>

3. <span data-ttu-id="45b2c-119">Dans le nouveau volet, sélectionnez **Ajouter un compte** et connectez-vous avec vos informations d’identification Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="45b2c-119">In the new pane, select **Add Account** and sign in with your Azure Active Directory credentials.</span></span>  
    <span data-ttu-id="45b2c-120">![Capture d’écran de Cloud Explorer une fois connecté et connecté à Azure Stack](./media/azure-stack-install-visual-studio/image6.png)</span><span class="sxs-lookup"><span data-stu-id="45b2c-120">![Screenshot of Cloud Explorer once logged in and connected to Azure Stack](./media/azure-stack-install-visual-studio/image6.png)</span></span>

<span data-ttu-id="45b2c-121">Une fois connecté, vous pouvez [déployer des modèles](azure-stack-deploy-template-visual-studio.md) ou parcourir les types de ressources et les groupes de ressources disponibles pour créer vos propres modèles.</span><span class="sxs-lookup"><span data-stu-id="45b2c-121">Once logged in, you can [deploy templates](azure-stack-deploy-template-visual-studio.md) or browse available resource types and resource groups to create your own templates.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="45b2c-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="45b2c-122">Next Steps</span></span>

 - [<span data-ttu-id="45b2c-123">Développer des modèles pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="45b2c-123">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
