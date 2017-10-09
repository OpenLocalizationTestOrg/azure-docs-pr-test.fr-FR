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
# <a name="install-visual-studio-and-connect-tooazure-stack"></a>Installation de Visual Studio et connectez-vous tooAzure pile

Utilisation des tooauthor de Visual Studio et le déploiement d’Azure Resource Manager [modèles](azure-stack-arm-templates.md) dans la pile de Azure. Vous pouvez utiliser hello les étapes décrites dans cette tooinstall article Visual Studio, soit à partir de [Kit de développement Azure pile](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), ou à partir d’un client externe basé sur Windows si vous êtes connecté via [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn). Ces étapes effectuent une nouvelle installation de Visual Studio 2015 Community Edition. Pour en savoir plus sur la coexistence entre d’autres versions de Visual Studio, consultez [cet article](https://msdn.microsoft.com/library/ms246609.aspx).

## <a name="install-visual-studio"></a>Installation de Visual Studio
1. Téléchargez et exécutez hello [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).             
2. Recherchez **Visual Studio Community 2015 avec Microsoft Azure SDK - 2.9.6**, cliquez sur **Ajouter**, puis **Installer**.

    ![Capture d’écran des étapes d’installation de WebPI](./media/azure-stack-install-visual-studio/image1.png) 

3. Désinstaller hello **Microsoft Azure PowerShell** qui est installé dans le cadre de hello Azure SDK.

    ![Capture d’écran de l’interface Ajout/Suppression de programmes pour Azure PowerShell](./media/azure-stack-install-visual-studio/image2.png) 

4. [Installer PowerShell pour Azure Stack](azure-stack-powershell-install.md)

5. Redémarrez le système d’exploitation de hello après l’installation de hello.

## <a name="connect-tooazure-stack"></a>Se connecter tooAzure pile

1. Lancez Visual Studio.

2. À partir de hello **vue** menu, sélectionnez **Cloud Explorer**.

3. Dans le volet de nouveau hello, sélectionnez **ajouter un compte** et connectez-vous avec vos informations d’identification Azure Active Directory.  
    ![Capture d’écran de Cloud Explorer, une fois connecté et connecté tooAzure pile](./media/azure-stack-install-visual-studio/image6.png)

Une fois connecté, vous pouvez [déployer des modèles](azure-stack-deploy-template-visual-studio.md) ou parcourir les types de ressources disponibles et des groupes de ressources toocreate vos propres modèles.  

## <a name="next-steps"></a>Étapes suivantes

 - [Développer des modèles pour Azure Stack](azure-stack-develop-templates.md)
