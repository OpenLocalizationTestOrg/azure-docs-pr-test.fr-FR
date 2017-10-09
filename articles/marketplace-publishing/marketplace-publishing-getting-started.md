---
title: "aaaOverview de façon toocreate et déployer un toohello offre Marketplace | Documents Microsoft"
description: "Hello étapes toobecome requis un développeur Microsoft agréé de comprendre et créer et déployer une image de machine virtuelle, le modèle, le service de données ou le service développeur Bonjour Azure Marketplace"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5343bd26-c6e4-4589-85b7-4a2c00bba8ab
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio
ms.openlocfilehash: ac5480b98b8b1021a595db951ed9c974f74415dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-and-manage-an-offer-in-hello-azure-marketplace"></a>Publier et de gérer une offre Bonjour Azure Marketplace
Cet article est fourni aux développeurs de toohelp créer, déploiement et gérer leurs solutions répertoriées Bonjour Azure Marketplace pour d’autres clients Azure et les partenaires toopurchase et les utiliser.

## <a name="marketplace-publishing"></a>Publication sur la Place de marché
Comme un serveur de publication Azure, vous pouvez distribuer et vendre vos solutions innovantes ou les développeurs de service tooother, éditeurs de logiciels indépendants, et aux professionnels informatiques de hello Marketplace. Via hello Marketplace, vous pouvez également accéder aux clients qui souhaitent tooquickly développement leurs applications sur le cloud et les solutions mobiles. Si votre solution cible les utilisateurs professionnels, vous souhaiterez peut-être tooconsider hello [AppSource](http://appsource.microsoft.com) marketplace.


## <a name="supported-types-of-solutions"></a>Types de solutions pris en charge
Hello plus important toodo comme un serveur de publication est toodefine quel type de solution offre de votre entreprise. Hello Marketplace prend en charge hello les types d’offres suivants :

|Type de solution|Machine virtuelle|Modèle de solution|
|---|---|---|
|**Définition**|Images préconfigurées dans lesquelles un système d’exploitation et une ou plusieurs applications sont entièrement installés. Image de machine virtuelle fournit toocreate nécessaire des informations de hello et déployer des ordinateurs virtuels dans hello service Azure Virtual Machines.|Structure de données capable de référencer un ou plusieurs services Azure distincts, y compris des services publiés par d’autres vendeurs. Les abonnés Azure peuvent utiliser toodeploy une ou plusieurs offres de manière unique et coordonnée.|
|**Exemple**|En tant qu’éditeur Azure, vous avez créé et validé une machine virtuelle avec un service de base de données innovant. Autres abonnés Azure souhaitez tooprocure et déploiement cette machine virtuelle dans leurs environnements de service cloud.|Comme un serveur de publication Azure, vous avez fourni un ensemble de services à partir de sur Azure qui la rendent toodeploy rapide des services de cloud avec l’équilibrage de charge, une sécurité accrue et une haute disponibilité. Autres abonnés Azure peuvent gagner du temps en procurer le modèle de solution hello qui répond à leurs objectifs. Ils n’ont pas toomanually rechercher, acquérir, déployer et configurer hello des services Azure identiques ou similaires.|

> [!NOTE]
> Certaines étapes sont partagés entre les différents types de hello de solutions, et d’autres toohello distinctes de type respectifs de la solution. Cet article fournit une brève présentation des étapes de hello, vous devez toocomplete pour n’importe quel type de solution.

## <a name="publish-a-solution"></a>Publier une application
![Nommer, inscrire, publier](media/marketplace-publishing-getting-started/img01.png)

### <a name="nominate-your-solution-for-pre-approval"></a>Nommer votre solution pour une pré-approbation
toopublish une machine virtuelle [solution](https://createopportunity.azurewebsites.net) toohello Marketplace, hello complète Microsoft Azure Certified **Solution candidature formulaire**.

>[!NOTE]
> Si vous travaillez avec un responsable de compte ou un gestionnaire de serveur partenaire DX, demandez-lui toonominate votre solution pour le programme de certification Azure hello. Vous pouvez également accéder toohello [Microsoft Azure Certified](http://createopportunity.azurewebsites.net) page Web et remplissez hello formulaire d’application. Entrez les adresse de messagerie de hello de votre responsable de compte ou le partenaire du Gestionnaire de DX Bonjour **Microsoft parrain de Contact** boîte.

Si vous répondez aux critères d’éligibilité hello Bonjour [stratégies de participation Azure Marketplace](http://go.microsoft.com/fwlink/?LinkID=526833) et votre demande est approuvée, nous commencer à travailler avec vous tooonboard votre toohello solution Marketplace.

### <a name="register-your-account-as-a-microsoft-seller"></a>Inscrire votre compte en tant que vendeur Microsoft
Inscrivez votre compte Microsoft en tant que [compte Microsoft Developer](marketplace-publishing-accounts-creation-registration.md).

### <a name="publish-your-solution"></a>Publier votre solution
toopublish un toohello solution Marketplace, procédez comme suit :
1. Répondre aux exigences techniques de hello.

    a. Répondre à hello [conditions préalables non](marketplace-publishing-pre-requisites.md).

    b. Répondre à hello [conditions préalables de la techniques de machine virtuelle](marketplace-publishing-vm-image-creation-prerequisites.md).

    c. Répondre à hello [modèle technique conditions préalables](marketplace-publishing-solution-template-creation-prerequisites.md).

2. Créez votre offre.

    a. Créez une offre de [machine virtuelle](marketplace-publishing-vm-image-creation.md).

    b. Créez votre offre de [modèle de solution](marketplace-publishing-solution-template-creation.md).

3. Créez votre offre de [contenu marketing](marketplace-publishing-push-to-staging.md).

4. Testez votre offre dans un environnement intermédiaire.

    a. Testez votre offre de machine virtuelle dans un [environnement intermédiaire](marketplace-publishing-vm-image-test-in-staging.md).

    b. Testez votre offre de modèle de solution dans un [environnement intermédiaire](marketplace-publishing-solution-template-test-in-staging.md).

5. Déployer votre toohello offre [Marketplace](marketplace-publishing-push-to-production.md).


### <a name="create-and-manage-a-virtual-machine-image"></a>Créer et gérer une image de machine virtuelle
Créez et gérez une image de machine virtuelle à l’aide des ressources suivantes :
* Créez une image de machine virtuelle [locale](marketplace-publishing-vm-image-creation-on-premise.md).
* Créer une machine virtuelle en cours d’exécution [Windows Bonjour Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Créer une machine virtuelle en cours d’exécution [Linux Bonjour Azure portal](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Résolvez les problèmes courants rencontrés lors de la [création du disque dur virtuel](marketplace-publishing-vm-image-creation-troubleshooting.md).

## <a name="manage-your-solution"></a>Gérer votre solution
Gérer votre solution à l’aide de hello suivant des ressources :
* [Guide de production après hello en lecture pour l’ordinateur virtuel offre](marketplace-publishing-vm-image-post-publishing.md)
* [Mettre à jour les détails techniques de hello d’une offre ou une référence (SKU)](marketplace-publishing-vm-image-post-publishing.md#update-the-nontechnical-details-of-an-offer-or-a-sku)
* [Mettre à jour des détails techniques hello d’une offre ou une référence (SKU)](marketplace-publishing-vm-image-post-publishing.md#update-the-technical-details-of-a-sku)
* [Ajouter une nouvelle référence (SKU) à une offre répertoriée](marketplace-publishing-vm-image-post-publishing.md#add-a-new-sku-under-a-listed-offer)
* [Modifier le nombre de disques de données de hello pour une référence (SKU) répertorié](marketplace-publishing-vm-image-post-publishing.md#change-the-data-disk-count-for-a-listed-sku)
* [Supprimer une offre répertoriée hello Marketplace](marketplace-publishing-vm-image-post-publishing.md)
* [Supprimer une référence (SKU) répertorié hello Marketplace](marketplace-publishing-vm-image-post-publishing.md#delete-a-listed-sku-from-the-marketplace)
* [Supprimer version actuelle de hello d’une référence (SKU) répertorié hello Marketplace](marketplace-publishing-vm-image-post-publishing.md#delete-the-current-version-of-a-listed-sku-from-the-marketplace)
* [Rétablir hello répertoriant les valeurs des prix tooproduction](marketplace-publishing-vm-image-post-publishing.md#revert-the-listing-price-to-production-values)
* [Rétablir les valeurs tooproduction du modèle de facturation de hello](marketplace-publishing-vm-image-post-publishing.md#revert-the-billing-model-to-production-values)
* [Rétablir le paramètre de visibilité hello d’une valeur de production toohello référence (SKU) répertorié](marketplace-publishing-vm-image-post-publishing.md#revert-the-visibility-setting-of-a-listed-sku-to-the-production-value)
* [Affichage et modification de « l’offre incitative revendeurs » des fournisseurs de solutions Cloud dans Azure Marketplace](marketplace-publishing-csp-incentive.md)
* [Présentation de votre rapport de paiement](marketplace-publishing-report-payout.md)
* [Obtenir de l’aide en tant qu’éditeur](marketplace-publishing-get-publisher-support.md)

## <a name="additional-resources"></a>Ressources supplémentaires
[Configurer Azure PowerShell](marketplace-publishing-powershell-setup.md)
