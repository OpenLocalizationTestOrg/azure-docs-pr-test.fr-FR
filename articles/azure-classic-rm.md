---
title: "modes de déploiement (classique) Manager et gestion des services aaaResource | Documents Microsoft"
description: "Découvrez les différences de hello entre le Gestionnaire de ressources et les modèles de déploiement classique."
services: virtual-network
documentationcenter: 
author: telmosampaio
manager: carmonm
editor: 
tags: azure-resource-manager,azure-service-management
redirect_url: ./azure-resource-manager/resource-manager-deployment-model
ms.assetid: 18a235d8-38ac-4886-9e56-b3855c73ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: telmos
ms.openlocfilehash: e14f815ba9d79d9dd8f83b45bda78d0eba0bec56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-deployment-models"></a>Modèles de déploiement Azure
Hello plateforme Azure est en transition.  Si vous tooAzure nouveaux ou avez été l’utiliser pour les années, il est important toounderstand certaines des modifications de clé hello que nous apportons toohello plateforme pendant cette transition.

Toutes les ressources Azure prennent en charge une ou les deux hello suivant des modèles de déploiement :

* **Le Gestionnaire de ressources :** hello modèle de déploiement les plus récents pour les ressources Azure. La plupart des ressources les plus récentes prennent déjà en charge ce modèle de déploiement ; à terme, ce sera le cas de toutes les ressources.   
* **Classique :** ce modèle est pris en charge dès maintenant par la plupart des ressources Azure existantes. Nouvelles ressources ajoutées tooAzure ne prendra pas en charge ce modèle.

documentation Hello pour chaque service qui modélise il les détails de ressources Azure peut être créée avec.

## <a name="why-does-this-matter"></a>En quoi est-ce important ?
Il est important pour hello suivant raisons :

* les fonctionnalités de plateforme Windows Azure Hello que vous utilisez sont différentes entre ces deux modèles.  Par exemple, les ressources créées à l’aide du modèle de déploiement Resource Manager hello (ou simplement le Gestionnaire de ressources) peuvent être créées avec [modèles Azure Resource Manager](azure-resource-manager/resource-group-overview.md#template-deployment), alors que les ressources créées avec le modèle de déploiement classique hello ne peut pas.
* Hello des fonctions de ressources Azure individuels ou les comportements peuvent être différents entre deux modèles de hello, ou n’existent dans un modèle ou hello autres.  Par exemple, équilibrage de charge du trafic sur les ordinateurs virtuels créés avec le modèle de déploiement classique hello est *implicite* , car les machines virtuelles sont membres d’un Service Cloud Azure, et charge est automatiquement équilibré sur virtuel ordinateurs dans un service cloud. Machines virtuelles créées à l’aide du Gestionnaire de ressources ne sont pas membres d’un service cloud, et une ressource d’équilibrage de charge Azure distincte doit être *explicitement* créé tooload équilibrer le trafic entre plusieurs machines virtuelles.  
* La façon de créer, de configurer et de gérer vos ressources Azure diffère entre ces deux modèles.
* Les ressources créées à l'aide d'un des modèles de déploiement ne peuvent pas nécessairement interagir avec les ressources créées à l'aide d'un autre modèle de déploiement. Par exemple, les Machines virtuelles Azure créé à l’aide d’un modèle de déploiement peut être uniquement tooAzure connecté les réseaux virtuels créés à l’aide de hello même modèle de déploiement.    

Chacun des modèles de déploiement hello sous-jacent est une interface de programmation d’application (API) pour chaque ressource.  Il existe un [API du Gestionnaire de ressources](https://msdn.microsoft.com/library/azure/dn948464.aspx) pour le modèle de déploiement du Gestionnaire de ressources hello et un [API de gestion](https://msdn.microsoft.com/library/azure/ee460799.aspx) pour le modèle de déploiement classique hello. Les développeurs peuvent écrire toointeract de code avec ces API *directement*.  

Professionnels de l’informatique, toutefois, en général interagissent avec ces API *indirectement* en utilisant un portail graphique dans un navigateur web, à l’aide d’Azure PowerShell sur un ordinateur Windows, ou à l’aide des applets de commande hello Azure Interface de ligne de commande (CLI) soit un Ordinateur Windows, OS X ou Linux. Trois de ces méthodes indirectes utilisés par hello professionnel de l’informatique interagissent directement avec les API de hello. Cela signifie que lorsque de nouvelles fonctionnalités sont introduite toohello Azure plateforme ou des ressources, il est toujours directement disponible via l’API de hello tout d’abord, avec les méthodes indirecte hello gagner hello prise en charge de nouvelles ressources et fonctionnalités après hello API est disponibles.  

sections Hello ci-dessous expliquent comment Azure ressources sont configurés à l’aide de modèles de déploiement différentes hello via les méthodes indirecte hello trois.

## <a name="portals"></a>Portails
Azure dispose de deux portails :

* **[Portail Azure](https://manage.windowsazure.com) :** si vous utilisez Azure depuis un certain temps, vous avez utilisé ce portail. Il est toocreate utilisé et que vous configurez des ressources Azure plus anciens qui prennent en charge le modèle de déploiement classique hello. Impossible d’utiliser toocreate ou de configurer les ressources qui prennent uniquement en charge le Gestionnaire de ressources. 
* **[Portail Azure en version préliminaire](https://azure.microsoft.com/overview/preview-portal/) :** si vous utilisez une ressource Azure plus récente, vous avez certainement utilisé ce portail. Il peut être toocreate utilisé et configurer des ressources Azure. Par la suite vous être en mesure de toocreate et configurer toutes les ressources Azure avec lui. Pour certaines ressources qui prennent en charge les deux modèles de déploiement, ce portail peut être toocreate utilisé et configurez une ressource à l’aide d’un modèle de déploiement. 

Certaines fonctionnalités et ressources peuvent uniquement être créées et configurées dans un portail ou hello autres. Certaines ressources ou les fonctionnalités (encore) ne peut pas être créées ou configuré dans des portails et peuvent être configurées uniquement avec PowerShell, hello CLI, ou les deux. documentation Hello pour chaque ressource Azure décrit en détail sur lequel il peut être créé avec la méthode. 

## <a name="powershell"></a>PowerShell
Avec [PowerShell](/powershell/azureps-cmdlets-docs) vous pouvez utiliser un toocreate de scripts de ligne de commande ou l’auteur et configurer les ressources Azure à partir d’un ordinateur Windows.  Les ressources Azure individuelles ont des [applets de commande Resource Manager](/powershell/azure/overview), des [applets de commande Service Management](/powershell/azure/overview?view=azuresmps-3.7.0), ou les deux.  Certaines fonctionnalités et ressources ne peuvent être créées et/ou configuré à l’aide de PowerShell ou hello CLI. Selon les ressources hello, lors de l’utilisation des applets de commande PowerShell de gestionnaire de ressources vous avez deux options pour la création et la configuration des ressources Azure :

* **Applets de commande PowerShell :** vous pouvez créer et configurer chaque ressource Azure individuellement à l’aide d’applets de commande hello pour chaque ressource. Vous pouvez le faire à partir d'une ligne de commande ou en incluant plusieurs commandes dans un script PowerShell que vous pouvez stocker et versionner.
* **Applets de commande PowerShell avec un modèle Azure Resource Manager :** vous pouvez utiliser PowerShell toocreate Azure ressources à l’aide d’un modèle Azure Resource Manager. Les modèles peuvent être enregistrés et gérés. En savoir plus, lisez hello [déployer une application avec le modèle Azure Resource Manager](resource-group-template-deploy.md) l’article. Plusieurs [modèles Azure Quickstart](https://azure.microsoft.com/documentation/templates/) existent pour les solutions courantes. Ils peuvent également être téléchargés et modifiés.

## <a name="cli"></a>Interface de ligne de commande
Vous pouvez créer et configurer des ressources Azure à partir d’ordinateurs Windows, OS X ou Linux à l’aide de hello CLI.  Hello de lecture [installation Bonjour Azure CLI](cli-install-nodejs.md) hello de tooinstall article CLI sur votre système d’exploitation de choix. Tels que PowerShell, il existe des commandes différentes qui doivent être utilisés selon que vous créez des ressources à l’aide de [le Gestionnaire de ressources](xplat-cli-azure-resource-manager.md) ou hello [classique (gestion des services)](virtual-machines/linux/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) modèles de déploiement.

## <a name="next-steps"></a>Étapes suivantes
* Voici quelques informations supplémentaires sur [Resource Manager](azure-resource-manager/resource-group-overview.md).
* Comprendre comment trop[modèles](best-practices-resource-manager-design-templates.md).

