---
title: "aaaCreate et publier un élément du Marketplace dans la pile de Azure | Documents Microsoft"
description: "Créez et publiez un article de Marketplace dans Azure Stack."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 77e5f60c-a86e-4d54-aa8d-288e9a889386
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: erikje
ms.openlocfilehash: 6f6a7af96f9d8de9098ac7eee4ba2ac9bc3d6a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-publish-a-marketplace-item"></a>Créer et publier un article de la Place de marché
## <a name="create-a-marketplace-item"></a>Créer un élément de Marketplace
1. [Télécharger](http://www.aka.ms/azurestackmarketplaceitem) outil du Gestionnaire de package de la galerie Azure hello et élément de Azure Marketplace de pile exemple hello.
2. Ouvrez l’élément du Marketplace exemple hello et renommer hello **SimpleVMTemplate** dossier. (Hello utilisez même nom que votre élément Marketplace--par exemple, **Contoso.TodoList**.) Ce dossier contient les éléments suivants :
   
       /Contoso.TodoList/
       /Contoso.TodoList/Manifest.json
       /Contoso.TodoList/UIDefinition.json
       /Contoso.TodoList/Icons/
       /Contoso.TodoList/Strings/
       /Contoso.TodoList/DeploymentTemplates/
3. [Créez un modèle Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) ou choisissez un modèle sur GitHub. élément du Marketplace Hello utilise cette toocreate modèle une ressource.
4. toomake assurer que les ressources hello peuvent être déployés avec succès, tester le modèle hello avec hello API de pile Microsoft Azure.
5. Si votre modèle repose sur une image de machine virtuelle, suivez les instructions de hello trop[ajouter un tooAzure d’image de machine virtuelle pile](azure-stack-add-vm-image.md).
6. Enregistrer votre modèle Azure Resource Manager Bonjour **/Contoso.TodoList/DeploymentTemplates/** dossier.
7. Choisissez les icônes de hello et du texte pour votre élément de Marketplace. Ajouter des icônes toohello **icônes** dossier et ajoutez le texte toohello **ressources** fichier Bonjour **chaînes** dossier. Utilisez hello Small, Medium, Large et à l’échelle de convention d’affectation de noms pour les icônes. Vous trouverez une description détaillée sur la page [Référence : interface utilisateur de l’article de Marketplace](#reference-marketplace-item-ui).
   
   > [!NOTE]
   > Toutes les tailles d’icône quatre (petite, moyenne, grande, l’échelle) sont requis pour la création d’élément du Marketplace hello correctement.
   > 
   > 
8. Bonjour **manifest.json** , modifiez **nom** nom toohello de votre élément de Marketplace. Modifiez également **publisher** tooyour nom ou la société.
9. Sous **artefacts**, modifiez **nom** et **chemin d’accès** toohello les informations correctes pour le modèle Azure Resource Manager hello que vous avez incluses.
   
         "artifacts": [
            {
                "name": "Type your template name",
                "type": "Template",
                "path": "DeploymentTemplates\\Type your path",
                "isDefault": true
            }
10. Remplacez **mes éléments de Marketplace** avec une liste de catégories hello où doit apparaître votre élément du Marketplace.
    
             "categories":[
                 "My Marketplace Items"
              ],
11. Pour d’autres modifications toomanifest.json, consultez trop[référence : Marketplace élément manifest.json](#reference-marketplace-item-manifestjson).
12. dossiers de hello toopackage dans un fichier .azpkg, ouvrez une invite de commandes et exécutez les hello de commande suivante :
    
        AzureGalleryPackager.exe package –m <path toomanifest.json> -o <output location for hello package>
    
    > [!NOTE]
    > package de sortie toohello Hello chemin d’accès complet doit exister. Par exemple, si le chemin de sortie hello est C:\MarketPlaceItem\yourpackage.azpkg, le dossier hello C:\MarketPlaceItem doit exister.
    > 
    > 

## <a name="publish-a-marketplace-item"></a>Publier un élément du Marketplace
1. Utilisez PowerShell ou l’Explorateur de stockage Azure tooupload votre tooAzure d’article (.azpkg) Marketplace stockage d’objets Blob. Vous pouvez télécharger le stockage de Azure pile toolocal ou télécharger tooAzure stockage. (Il est un emplacement temporaire pour le package de hello.) Assurez-vous que cet objet blob hello est accessible publiquement.
2. Sur l’ordinateur virtuel du client hello dans l’environnement de Microsoft Azure pile hello, assurez-vous que votre session PowerShell est configurée avec vos informations d’identification d’administrateur de service. Vous trouverez des instructions sur la manière de tooauthenticate PowerShell dans la pile d’Azure dans [déployer un modèle avec PowerShell](azure-stack-deploy-template-powershell.md).
3. Hello d’utilisation **Add-AzureRMGalleryItem** PowerShell applet de commande toopublish hello Marketplace élément tooAzure pile. Par exemple :
   
       Add-AzureRMGalleryItem -GalleryItemUri `
       https://sample.blob.core.windows.net/gallerypackages/Microsoft.SimpleTemplate.1.0.0.azpkg –Verbose
   
   | Paramètre | Description |
   | --- | --- |
   | SubscriptionID |ID d’abonnement d’administrateur. Vous pouvez le récupérer avec PowerShell. Si vous préférez tooget dans le portail de hello, accédez d’abonnement du fournisseur toohello et copiez l’ID d’abonnement hello. |
   | GalleryItemUri |URI d’objet BLOB pour votre package de galerie qui a déjà été téléchargé toostorage. |
   | Apiversion |Définir sur **2015-04-01**. |
4. Accédez à toohello portal. Vous pouvez maintenant voir élément du Marketplace hello dans portail hello--en tant qu’administrateur ou en tant que client.
   
   > [!NOTE]
   > package de Hello peut prendre plusieurs minutes tooappear.
   > 
   > 
5. Votre élément de Marketplace a été enregistré toohello Azure Marketplace de pile. Vous pouvez choisir toodelete à partir de votre emplacement de stockage d’objets Blob.
6. Vous pouvez supprimer un élément du Marketplace à l’aide de hello **Remove-AzureRMGalleryItem** applet de commande. Exemple :
   
        Remove-AzureRMGalleryItem -Name Microsoft.SimpleTemplate.1.0.0  –Verbose
   
   > [!NOTE]
   > Hello Marketplace UI peut indiquer une erreur après avoir supprimé un élément. Erreur de hello toofix, cliquez sur **paramètres** dans le portail de hello. Sélectionnez ensuite **Ignorer les modifications** sous **Personnalisation du portail**.
   > 
   > 

## <a name="reference-marketplace-item-manifestjson"></a>Référence : manifest.json d’un article de Marketplace
### <a name="identity-information"></a>Informations d’identité
| Nom | Requis | Type | Contraintes | Description |
| --- | --- | --- | --- | --- |
| Nom |X |String |[A-Za-z0-9]+ | |
| Éditeur |X |String |[A-Za-z0-9]+ | |
| Version |X |String |[SemVer v2](http://semver.org/) | |

### <a name="metadata"></a>Metadata
| Nom | Requis | Type | Contraintes | Description |
| --- | --- | --- | --- | --- |
| DisplayName |X |String |Recommandation : 80 caractères |portail de Hello affichera ne peut-être pas votre nom de l’élément en douceur si elle est supérieure à 80 caractères. |
| PublisherDisplayName |X |String |Recommandation : 30 caractères |portail de Hello affichera ne peut-être pas le nom de votre serveur de publication en douceur si elle est supérieure à 30 caractères. |
| PublisherLegalName |X |String |256 caractères maximum | |
| Résumé |X |String |60 caractères too100 | |
| LongSummary |X |String |140 caractères too256 |Non encore applicable dans Azure Stack |
| Description |X |[HTML](https://auxdocs.azurewebsites.net/en-us/documentation/articles/gallery-metadata#html-sanitization) |500 too5, 000 caractères | |

### <a name="images"></a>Images
Hello Marketplace utilise hello suivant des icônes :

| Nom | Largeur | Hauteur | Remarques |
| --- | --- | --- | --- |
| Large |255 px |115 px |Toujours obligatoire |
| Grande |115 px |115 px |Toujours obligatoire |
| Moyenne |90 px |90 px |Toujours obligatoire |
| Petite |40 px |40 px |Toujours obligatoire |
| Capture d'écran |533 px |32 px |Facultatif |

### <a name="categories"></a>Catégories
Chaque élément du Marketplace doit être marqué avec une catégorie qui identifie où les éléments hello s’affiche sur l’interface utilisateur du portail hello. Vous pouvez choisir une des catégories existantes de hello dans la pile de Azure (calcul, données + stockage, etc.) ou choisir un nouveau.

### <a name="links"></a>Liens
Chaque élément du Marketplace peut inclure différents contenus tooadditional de liens. liens de Hello sont spécifiés sous forme de liste de noms et d’URI.

| Nom | Requis | Type | Contraintes | Description |
| --- | --- | --- | --- | --- |
| DisplayName |X |String |64 caractères maximum | |
| Uri |X |URI | | |

### <a name="additional-properties"></a>Propriétés supplémentaires
Dans toohello Ajout précédant les métadonnées, les auteurs de Marketplace peuvent fournir des données de paire clé/valeur personnalisée dans hello suivant du formulaire :

| Nom | Requis | Type | Contraintes | Description |
| --- | --- | --- | --- | --- |
| DisplayName |X |String |25 caractères maximum | |
| Valeur |X |String |30 caractères maximum | |

### <a name="html-sanitization"></a>Nettoyage du HTML
Pour n’importe quel champ permettant à HTML, hello attributs et les éléments suivants sont autorisés :

h1, h2, h3, h4, h5, p, ol, ul, li, a[target|href], br, strong, em, b, i

## <a name="reference-marketplace-item-ui"></a>Référence : interface utilisateur d’article de Marketplace
Icônes et du texte pour les éléments du Marketplace comme indiqué dans le portail d’Azure pile hello sont les suivantes.

### <a name="create-blade"></a>Panneau Créer
![Panneau Créer](media/azure-stack-marketplace-item-ui-reference/image1.png)

### <a name="marketplace-item-details-blade"></a>Panneau Détails de l’élément du Marketplace
![Panneau Détails de l’élément du Marketplace](media/azure-stack-marketplace-item-ui-reference/image3.png)

