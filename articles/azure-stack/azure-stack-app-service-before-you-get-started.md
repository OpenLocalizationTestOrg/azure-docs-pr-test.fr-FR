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
# <a name="before-you-get-started-with-app-service-on-azure-stack"></a>Avant de commencer avec App Service sur Azure Stack

Vous avez besoin de quelques éléments tooinstall du Service d’applications Azure sur la pile de Azure :

- Un déploiement terminé de hello [kit de développement Azure pile](azure-stack-run-powershell-script.md).
- Suffisamment d’espace dans votre système Azure Stack pour un petit déploiement d’App Service sur Azure Stack.  Hello espace requis est d’environ 20 Go d’espace disque.
- Une image de machine virtuelle Windows Server à utiliser lorsque vous créez des machines virtuelles pour App Service sur Azure Stack.
- [Un serveur qui exécute SQL Server](#SQL-Server).

>[!NOTE] 
> Hello comme suit *tous les* ont lieu sur l’ordinateur hôte de pile de Azure hello.

toodeploy un fournisseur de ressources, vous devez exécuter hello PowerShell Integrated Scripting Environment (ISE) en tant qu’administrateur. Pour cette raison, vous devez tooallow cookies et JavaScript dans le profil d’Internet Explorer hello utiliser toosign dans tooAzure Active Directory.

## <a name="turn-off-internet-explorer-enhanced-security"></a>Désactiver la sécurité renforcée d’Internet Explorer

1.  Connectez-vous à ordinateur de kit de développement de Azure pile toohello en tant que **AzureStack/administrateur**, puis ouvrez **le Gestionnaire de serveur**.

2.  Désactivez la **Configuration de sécurité renforcée d’Internet Explorer** pour les administrateurs et les utilisateurs.

3.  Connectez-vous à ordinateur de kit de développement de Azure pile toohello en tant qu’administrateur, puis ouvrez **le Gestionnaire de serveur**.

4.  Désactivez la **Configuration de sécurité renforcée d’Internet Explorer** pour les administrateurs et les utilisateurs.

## <a name="enable-cookies"></a>Activer les cookies

1.  Sélectionnez **Démarrer** > **Toutes les applications** > **Accessoires Windows**. Cliquez avec le bouton droit sur **Internet Explorer** > **Plus** > **Exécuter en tant qu’administrateur**.

2.  Si vous y êtes invité, sélectionnez **Utiliser la sécurité recommandée**, puis sélectionnez **OK**.

3.  Dans Internet Explorer, sélectionnez **outils** (icône d’engrenage hello) > **Options Internet** > **confidentialité** > **avancé**.

4.  Sélectionnez **Advanced (Avancé)**. Vérifiez que les deux cases **Accepter** sont cochées. Sélectionnez **OK** deux fois.

5.  Fermez Internet Explorer et redémarrez hello PowerShell ISE en tant qu’administrateur.

## <a name="install-powershell-for-azure-stack"></a>Installer PowerShell pour Azure Stack

tooinstall PowerShell pour la pile de Azure, suivez les étapes de hello dans [installer PowerShell](azure-stack-powershell-install.md).

## <a name="use-visual-studio-with-azure-stack"></a>Utiliser Visual Studio avec Azure Stack

toouse Visual Studio avec la pile d’Azure, suivez les étapes de hello dans [installer Visual Studio](azure-stack-install-visual-studio.md).

## <a name="add-a-windows-server-2016-vm-image-tooazure-stack"></a>Ajouter un tooAzure d’image de machine virtuelle de Windows Server 2016 pile

Étant donné qu’App Service déploie plusieurs machines virtuelles, il requiert une image de machine virtuelle Windows Server 2016 dans Azure Stack. tooinstall une image de machine virtuelle, suivez les étapes de hello dans [ajouter une image de machine virtuelle par défaut](azure-stack-add-default-image.md).

## <a name="SQL-Server"></a>SQL Server

Service application sur Azure pile nécessite l’accès tooa SQL Server instance toocreate et hôte deux bases de données toorun hello fournisseur de ressources du Service d’applications.  Si vous choisissez toodeploy une machine virtuelle SQL Server sur la pile Azure qu’il doit être le niveau de connectivité SQL hello trop**Public**.  Vous pouvez choisir hello SQL Server instance toouse lorsque vous effectuez des options hello Bonjour du Service d’applications sur le programme d’installation de la pile de Azure.

## <a name="next-steps"></a>Étapes suivantes

- [Installer hello fournisseur de ressources du Service d’applications](azure-stack-app-service-deploy.md).

<!--Image references-->
[1]: ./media/azure-stack-app-service-before-you-get-started/PSGallery.png
[2]: ./media/azure-stack-app-service-before-you-get-started/WebPI_InstalledProducts.png
