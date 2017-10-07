---
title: "aaaUse hello Marketplace toolkit toocreate et publier des éléments du marketplace | Documents Microsoft"
description: "Découvrez comment tooquickly créer des éléments du marketplace par hello publication du Kit de ressources"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: ByronR
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/14/2017
ms.author: helaw
ms.openlocfilehash: c1cf9ad1da44787901297eec12faf2a3dea82a6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
#  <a name="add-marketplace-items-using-publishing-tool"></a>Ajouter des éléments de Place de Marché à l’aide de l’outil de publication
Ajout de votre contenu toohello [Azure Marketplace de pile](azure-stack-marketplace.md) rend votre tooyou disponibles de solutions et de vos clients pour le déploiement.  Hello Marketplace Toolkit crée des fichiers Azure Marketplace Packages (.azpkg) en fonction de vos modèles IaaS Azure Resource Manager ou les Extensions de machine virtuelle.  Vous pouvez également utiliser des fichiers de .azpkg toopublish hello Marketplace Toolkit, soit créé avec l’outil de hello ou à l’aide de [manuelle](azure-stack-create-and-publish-marketplace-item.md) étapes.  Cette rubrique vous guide de téléchargement hello outil, création d’un élément de marketplace basé sur un modèle d’ordinateur virtuel, puis publier ce toohello élément Azure Marketplace de pile.     


## <a name="prerequisites"></a>Composants requis
 - Vous devez exécuter hello toolkit sur l’ordinateur hôte de pile de Azure hello ou avez [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) connectivité à partir de l’ordinateur hello sur lequel vous exécutez l’outil de hello.

 - Télécharger hello [modèles de démarrage rapide de pile Azure](https://github.com/Azure/AzureStack-QuickStart-Templates/archive/master.zip) et extraire.

 - Télécharger hello [outil d’empaquetage de la galerie Azure](http://aka.ms/azurestackmarketplaceitem) (AzureGalleryPackage.exe). 

 - Publication toohello marketplace nécessite des icônes et un fichier de miniature.  Vous pouvez utiliser votre propre, ou enregistrer hello [exemple](azure-stack-marketplace-publisher.md#support-files) fichiers localement pour cet exemple.

## <a name="download-hello-tool"></a>Télécharger l’outil de hello
Hello Marketplace Toolkit peut être [téléchargé à partir du référentiel de pile de Azure Tools hello](azure-stack-powershell-download.md).


##  <a name="create-marketplace-items"></a>Créer des éléments de Place de Marché
Dans cette section, vous utilisez hello Marketplace Toolkit toocreate un package de l’élément marketplace .azpkg format.  

### <a name="provide-marketplace-information-with-wizard"></a>Fournir des informations de Place de Marché avec l’Assistant
1. À partir d’une session PowerShell, exécutez hello Marketplace Toolkit :
```PowerShell
    .\MarketplaceToolkit.ps1
```

2. Cliquez sur hello **Solution** onglet.  Cet écran accepte des informations sur votre élément de Place de Marché. Entrer des informations sur l’objet que vous le souhaitez tooappear dans marketplace de hello.  Vous pouvez également spécifier un [fichier de paramètres](azure-stack-marketplace-publisher.md#use-a-parameters-file) formulaire de hello tooprepopulate.  
    
    ![capture d’écran du premier écran de la boîte à outils Place de Marché](./media/azure-stack-marketplace-publisher/image7.png)
3. Cliquez sur **Parcourir** et sélectionnez un fichier image pour chaque champ d’icône et de capture d’écran.  Vous pouvez utiliser vos propres icônes ou hello icônes exemple hello [prennent en charge les fichiers](azure-stack-marketplace-publisher.md#support-files) section.
4. Une fois que tous les champs sont remplis, sélectionnez « Aperçu de la Solution » pour afficher un aperçu de la solution hello dans hello Marketplace.  Vous pouvez réviser et modifier le texte hello, des images et capture d’écran avant de cliquer sur **suivant**.  

### <a name="import-template-and-create-package"></a>Importer le modèle et créer le package
Dans cette section, vous importez le modèle de hello et fonctionne avec une entrée pour votre solution.

1.  Cliquez sur **Parcourir** et sélectionnez hello *azuredeploy.json* à partir du dossier 101-Simple-Windows-VM hello Bonjour téléchargé les modèles.

    ![capture d’écran du deuxième écran de la boîte à outils Place de Marché](./media/azure-stack-marketplace-publisher/image8.png)
2.  Assistant Déploiement Hello est rempli avec un *base* éléments d’entrée et l’étape pour chaque paramètre spécifié dans le modèle de hello.  Vous pouvez ajouter des étapes supplémentaires et déplacer des entrées d’une étape à une autre.  Par exemple, vous souhaiterez peut-être avoir des étapes « Configuration frontale » et « Configuration backend » pour votre solution.
3.  Spécifiez hello chemin d’accès tooAzureGalleryPackager.exe.  
4.  Cliquez sur **créer** et hello Marketplace Toolkit empaquette votre solution dans un fichier .azpkg.  Une fois terminé, Assistant de hello affiche permettent de vous hello toocontinue option votre tooAzure package pile de publication et du fichier de solution de tooyour de chemin d’accès hello.


## <a name="publish-marketplace-items"></a>Publier des éléments de Place de Marché
Dans cette section, vous publiez hello marketplace élément tooyour Azure Marketplace de pile.

![capture d’écran du premier écran de la boîte à outils Place de Marché](./media/azure-stack-marketplace-publisher/image9.png)

1.  Assistant de Hello nécessite des informations toopublish votre solution :
    
    |Champ|Description|
    |-----|-----|
    | Nom de l’administrateur de service | Compte de l’administrateur de service.  Exemple : ServiceAdmin@mydomain.onmicrosoft.com |
    | Mot de passe | Mot de passe du compte d’administrateur de service. |
    | Point de terminaison d’API | Point de terminaison Azure Resource Manager Azure Stack.  Exemple : management.local.azurestack.external |
2.  Cliquez sur **publier** et journal de publication hello s’affiche.
3.  Vous est désormais en mesure de toodeploy votre élément publié via le portail d’Azure pile hello.


## <a name="use-a-parameters-file"></a>Utiliser un fichier de paramètres
Vous pouvez également utiliser un fichier toocomplete hello marketplace élément informations relatives aux paramètres.  

Hello Marketplace Toolkit inclut une *solution.parameters.ps1* vous pouvez utiliser toocreate votre propre fichier de paramètres.


## <a name="support-files"></a>Fichiers de prise en charge
| Description | Exemple |
| ----- | ----- |
| icône .png de 40x40 | ![](./media/azure-stack-marketplace-publisher/image1.png) |
| icône .png de 90x90 | ![](./media/azure-stack-marketplace-publisher/image2.png) |
| icône .png de 115x115 | ![](./media/azure-stack-marketplace-publisher/image3.png) |
| icône .png de 255x115 | ![](./media/azure-stack-marketplace-publisher/image4.png) |
| Miniature .png de 533x324 | ![](./media/azure-stack-marketplace-publisher/image5.png) |


