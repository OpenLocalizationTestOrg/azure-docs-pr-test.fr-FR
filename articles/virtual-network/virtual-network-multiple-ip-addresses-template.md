---
title: "aaaMultiple des adresses IP pour les machines virtuelles - modèle | Documents Microsoft"
description: "Découvrez comment tooassign des adresses IP multiples virtuels tooa à l’aide d’un modèle Azure Resource Manager."
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/08/2016
ms.author: jdial
ms.openlocfilehash: e7660257b2d5c7da4b8b86771abe51a2c5012fa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-an-azure-resource-manager-template"></a>Affecter plusieurs adresses IP des ordinateurs toovirtual à l’aide d’un modèle Azure Resource Manager

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

Cet article explique comment toocreate un ordinateur virtuel (VM) au cours du déploiement d’Azure Resource Manager hello modèle à l’aide d’un modèle de gestionnaire de ressources. Toohello ne peut pas être assignées à plusieurs des adresses IP publiques et privées même NIC lors du déploiement d’une machine virtuelle via le modèle de déploiement classique hello. toolearn plus d’informations sur les modèles de déploiement Azure, lisez hello [comprendre les modèles de déploiement](../resource-manager-deployment-model.md) l’article.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name="template-description"></a>Description du modèle

Déploiement d’un modèle vous permet de tooquickly et créer régulièrement des ressources Azure avec des valeurs de configuration différente. Hello de lecture [procédure pas à pas de gestionnaire de ressources du modèle](../azure-resource-manager/resource-manager-template-walkthrough.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article si vous n’êtes pas familiarisé avec les modèles Azure Resource Manager. Hello [déployer une machine virtuelle avec plusieurs adresses IP](https://azure.microsoft.com/resources/templates/101-vm-multiple-ipconfig) modèle est utilisé dans cet article.

<a name="resources"></a>Le déploiement du modèle hello crée hello suivant des ressources :

|Ressource|Nom|Description|
|---|---|---|
|Interface réseau|*myNic1*|trois configurations IP Hello, décrites dans la section du scénario hello de cet article sont créées et affectées toothis carte réseau.|
|Ressource d’adresse IP publique|2 sont créés : *myPublicIP* et *myPublicIP2*|Ces ressources sont affectés à des adresses IP publiques statiques et toohello *IPConfig-1* et *IPConfig-2* configurations IP décrites dans le scénario de hello.|
|Machine virtuelle|*myVM1*|Une machine virtuelle DS3 standard.|
|Réseau virtuel|*myVNet1*|Un réseau virtuel avec un sous-réseau nommé *mySubnet*.|
|Compte de stockage|Déploiement de toohello unique|Un compte de stockage.|

<a name="parameters"></a>Lorsque vous déployez le modèle de hello, vous devez spécifier des valeurs pour hello paramètres suivants :

|Nom|Description|
|---|---|
|adminUsername|Nom d’utilisateur administrateur. nom d’utilisateur Hello doit se conformer [configuration requise du nom d’utilisateur Azure](../virtual-machines/windows/faq.md?toc=%2fazure%2fvirtual-network%2ftoc.json).|
|adminPassword|Mot de passe hello de mot de passe administrateur doit se conformer [les exigences de mot de passe Azure](../virtual-machines/windows/faq.md?toc=%2fazure%2fvirtual-network%2ftoc.json#what-are-the-password-requirements-when-creating-a-vm).|
|dnsLabelPrefix|Nom DNS de PublicIPAddressName1. nom DNS de Hello résoudra tooone d’adresses IP publiques hello affecté toohello machine virtuelle. Hello nom doit être unique au sein de hello Azure région (emplacement) que vous créez hello machine virtuelle dans.|
|dnsLabelPrefix1|Nom DNS de PublicIPAddressName2. nom DNS de Hello résoudra tooone d’adresses IP publiques hello affecté toohello machine virtuelle. Hello nom doit être unique au sein de hello Azure région (emplacement) que vous créez hello machine virtuelle dans.|
|OSVersion:|version de Linux/Windows Hello pour hello machine virtuelle. système d’exploitation de Hello est une image de tous les correctifs nécessaires de hello étant donné la version de Windows/Linux sélectionnée.|
|imagePublisher|Éditeur d’image de Windows/Linux Hello pour hello sélectionné de machine virtuelle.|
|imageOffer|image de Windows/Linux Hello pour hello sélectionné de machine virtuelle.|

Chacune des ressources hello déployés par le modèle de hello est configuré avec plusieurs paramètres par défaut. Vous pouvez afficher ces paramètres par le biais de hello méthodes suivantes :

- **Afficher le modèle hello sur GitHub :** si vous êtes familiarisé avec les modèles, vous pouvez afficher les paramètres de hello dans hello [modèle](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json).
- **Afficher les paramètres de hello après le déploiement :** si vous n’êtes pas familiarisé avec les modèles, vous pouvez déployer le modèle de hello à l’aide des étapes de l’une des hello les sections suivantes et ensuite afficher les paramètres de hello après le déploiement.

Vous pouvez utiliser hello portail Azure, PowerShell ou le modèle de hello toodeploy hello Azure interface de ligne de commande (CLI). Toutes les méthodes produisent hello même résultat. modèle toodeploy hello hello terminé les étapes dans un des hello les sections suivantes :

## <a name="deploy-using-hello-azure-portal"></a>Déployer à l’aide de hello portail Azure

étapes du modèle de hello toodeploy à l’aide de hello portail Azure, hello complet suivant :

1. Modifier le modèle de hello, si vous le souhaitez. modèle de Hello déploie les ressources de hello et les paramètres répertoriés dans hello [ressources](#resources) section de cet article. toolearn plus d’informations sur les modèles et comment tooauthor les, consultez l’article hello [les modèles de programmation Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-network%2ftoc.json)l’article.
2. Déployer le modèle de hello avec l’une des méthodes suivantes de hello :
    - **Modèle hello SELECT dans le portail de hello :** hello terminé les étapes Bonjour [déployer des ressources à partir du modèle personnalisé](../azure-resource-manager/resource-group-template-deploy-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#deploy-resources-from-custom-template) l’article. Choisissez hello de modèle existant nommé *101-vm-multiple-ipconfig*.
    - **Directement :** cliquez sur hello suivant le modèle de hello tooopen bouton directement dans le portail de hello :<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-vm-multiple-ipconfig%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

Quelle que soit la méthode hello vous choisissez, vous aurez besoin des valeurs de toosupply de hello [paramètres](#parameters) répertoriés précédemment dans cet article. Après le déployée hello machine virtuelle, vous connecter toohello machine virtuelle et ajouter les étapes hello privé IP adresses toohello système d’exploitation vous avez déployé en effectuant hello Bonjour [ajouter une adresse IP traite le système d’exploitation de l’ordinateur virtuel tooa](#os-config) section de cet article. N’ajoutez pas hello publique IP adresses toohello système d’exploitation.

## <a name="deploy-using-powershell"></a>Déployer à l’aide de PowerShell

modèle de hello toodeploy à l’aide de PowerShell, hello complète comme suit :

1. Déployer des modèles de hello en effectuant les étapes hello Bonjour [déployer un modèle avec PowerShell](../azure-resource-manager/resource-group-template-deploy-cli.md) l’article. Hello décrit plusieurs options pour le déploiement d’un modèle. Si vous choisissez toodeploy à l’aide de hello `-TemplateUri parameter`, hello URI pour ce modèle est *https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json*. Si vous choisissez toodeploy à l’aide de hello `-TemplateFile` paramètre, copiez le contenu de hello du hello [fichier modèle](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json) à partir de GitHub dans un nouveau fichier sur votre ordinateur. Modifier le contenu du modèle hello, si vous le souhaitez. modèle de Hello déploie les ressources de hello et les paramètres répertoriés dans hello [ressources](#resources) section de cet article. toolearn plus d’informations sur les modèles et comment tooauthor les, consultez l’article hello [les modèles de programmation Azure Resource Manager ](../azure-resource-manager/resource-group-authoring-templates.md)l’article.

    Quel que soit l’option hello choisie modèle hello toodeploy, vous devez fournir des valeurs pour les valeurs de paramètre hello répertoriés dans hello [paramètres](#parameters) section de cet article. Si vous choisissez les paramètres de toosupply à l’aide d’un fichier de paramètres, copiez le contenu hello Hello [fichier de paramètres](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.parameters.json) à partir de GitHub dans un nouveau fichier sur votre ordinateur. Modifiez les valeurs hello dans le fichier de hello. Vous avez créé en tant que valeur hello Pourquoi utiliser un fichier hello `-TemplateParameterFile` paramètre.

    toodetermine les valeurs valides pour hello OSVersion, ImagePublisher et les paramètres d’imageOffer, hello terminé les étapes Bonjour [naviguer et sélectionnez l’article images de machine virtuelle Windows](../virtual-machines/windows/cli-ps-findimage.md) l’article.

    >[!TIP]
    >Si vous ne savez pas si un dnslabelprefix est disponible, entrez hello `Test-AzureRmDnsAvailability -DomainNameLabel <name-you-want-to-use> -Location <location>` toofind de commande out. Si elle est disponible, commande hello retournera `True`.

2. Après le déployée hello machine virtuelle, vous connecter toohello machine virtuelle et ajouter les étapes hello privé IP adresses toohello système d’exploitation vous avez déployé en effectuant hello Bonjour [ajouter une adresse IP traite le système d’exploitation de l’ordinateur virtuel tooa](#os-config) section de cet article. N’ajoutez pas hello publique IP adresses toohello système d’exploitation.

## <a name="deploy-using-hello-azure-cli"></a>Déployer à l’aide de hello CLI d’Azure

modèle de hello toodeploy à l’aide de hello Azure CLI 1.0, hello complète comme suit :

1. Déployer des modèles de hello en effectuant les étapes hello Bonjour [déployer un modèle avec hello CLI d’Azure](../azure-resource-manager/resource-group-template-deploy-cli.md) l’article. Hello décrit plusieurs options pour le déploiement de modèle de hello. Si vous choisissez toodeploy à l’aide de hello `--template-uri` (-f), hello URI pour ce modèle est *https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json*. Si vous choisissez toodeploy à l’aide de hello `--template-file` (-f) du paramètre, copiez le contenu de hello du hello [fichier modèle](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json) à partir de GitHub dans un nouveau fichier sur votre ordinateur. Modifier le contenu du modèle hello, si vous le souhaitez. modèle de Hello déploie les ressources de hello et les paramètres répertoriés dans hello [ressources](#resources) section de cet article. toolearn plus d’informations sur les modèles et comment tooauthor les, consultez l’article hello [les modèles de programmation Azure Resource Manager ](../azure-resource-manager/resource-group-authoring-templates.md)l’article.

    Quel que soit l’option hello choisie modèle hello toodeploy, vous devez fournir des valeurs pour les valeurs de paramètre hello répertoriés dans hello [paramètres](#parameters) section de cet article. Si vous choisissez les paramètres de toosupply à l’aide d’un fichier de paramètres, copiez le contenu hello Hello [fichier de paramètres](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.parameters.json) à partir de GitHub dans un nouveau fichier sur votre ordinateur. Modifiez les valeurs hello dans le fichier de hello. Vous avez créé en tant que valeur hello Pourquoi utiliser un fichier hello `--parameters-file` (-e) paramètre.

    toodetermine les valeurs valides pour hello OSVersion, ImagePublisher et les paramètres d’imageOffer, hello terminé les étapes Bonjour [naviguer et sélectionnez l’article images de machine virtuelle Windows](../virtual-machines/windows/cli-ps-findimage.md) l’article.

2. Après le déployée hello machine virtuelle, vous connecter toohello machine virtuelle et ajouter les étapes hello privé IP adresses toohello système d’exploitation vous avez déployé en effectuant hello Bonjour [ajouter une adresse IP traite le système d’exploitation de l’ordinateur virtuel tooa](#os-config) section de cet article. N’ajoutez pas hello publique IP adresses toohello système d’exploitation.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
