---
title: aaaCreate des batteries de serveurs SharePoint dans Azure | Documents Microsoft
description: "Créez rapidement une nouvelle batterie de serveurs SharePoint 2013 ou SharePoint 2016 dans Azure à l’aide de hello Azure marketplace de portail."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d71c7177d9b99cf377bab767342508007285b452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-sharepoint-server-farms-using-hello-azure-portal-marketplace"></a>Créer des batteries de serveurs SharePoint à l’aide de hello Azure marketplace de portail

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a>Batteries de serveurs SharePoint 2013
Marketplace de portail Microsoft Azure hello, vous pouvez créer rapidement des batteries de serveurs SharePoint Server 2013 préconfigurées. Cela peut vous faire gagner un temps précieux lorsque vous avez besoin d'une batterie de serveurs SharePoint de base ou à haute disponibilité pour un environnement de test/développement ou si vous envisagez l'adoption de SharePoint Server 2013 comme solution de collaboration pour votre entreprise.

> [!NOTE]
> Hello **batterie de serveurs SharePoint** élément Bonjour Azure Marketplace de hello portail Azure a été supprimé. Elle a été remplacée par hello **batterie SharePoint 2013 non - HA** et **batterie de serveurs SharePoint 2013 à haute disponibilité** éléments.
>
>

batterie de serveurs SharePoint base Hello se compose de trois machines virtuelles dans cette configuration.

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

Vous pouvez utiliser cette configuration de batterie comme configuration simplifiée pour le développement d'applications SharePoint ou pour votre évaluation initiale de SharePoint 2013.

toocreate hello base (trois serveurs) batterie de serveurs SharePoint :

1. Cliquez [ici](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).
2. Cliquez sur **Déployer**.
3. Sur hello **batterie SharePoint 2013 non - HA** volet, cliquez sur **créer**.
4. Spécifiez des paramètres sur les étapes de hello Hello **créer batterie SharePoint 2013 non - HA** volet, puis cliquez sur **créer**.

batterie de serveurs SharePoint de haute disponibilité Hello se compose de neuf machines virtuelles dans cette configuration.

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

Vous pouvez utiliser cette charges client plus élevées de batterie de serveurs configuration tootest, la haute disponibilité d’un site SharePoint externe hello et groupes de disponibilité AlwaysOn de SQL Server pour une batterie de serveurs SharePoint. Vous pouvez également l'utiliser pour le développement d'applications SharePoint dans un environnement à haute disponibilité.

toocreate hello haute disponibilité (serveur neuf) batterie de serveurs SharePoint :

1. Cliquez [ici](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).
2. Cliquez sur **Déployer**.
3. Sur hello **batterie de serveurs SharePoint 2013 à haute disponibilité** volet, cliquez sur **créer**.
4. Spécifiez des paramètres sur les étapes de hello sept Hello **créer 2013 à haute disponibilité batterie de serveurs SharePoint** volet, puis cliquez sur **créer**.

> [!NOTE]
> Vous ne pouvez pas créer de hello **batterie SharePoint 2013 non - HA** ou **batterie de serveurs SharePoint 2013 à haute disponibilité** avec une version d’évaluation gratuite de Azure.
>
>

Hello portail Azure crée deux de ces batteries de serveurs dans un réseau virtuel cloud uniquement avec une présence sur le web sur Internet. Aucun site-à-site VPN ou ExpressRoute connexion tooyour arrière organisation réseau est.

> [!NOTE]
> Lorsque vous créez hello base ou les batteries SharePoint haute disponibilité à l’aide de hello portail Azure, vous ne pouvez pas spécifier un groupe de ressources existant. toowork contourner cette limitation, créez ces batteries de serveurs avec Azure PowerShell. Pour plus d’informations, consultez la page [Créer des batteries de serveurs de développement/test SharePoint 2013 avec le portail Azure](https://technet.microsoft.com/library/mt743093.aspx#powershell).
>
>

## <a name="sharepoint-2016-farms"></a>Batteries de serveurs SharePoint 2016
Consultez [cet article](https://technet.microsoft.com/library/mt723354.aspx) pour hello de toobuild instructions hello suivant monoserveur SharePoint Server 2016 de batterie de serveurs.

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-hello-sharepoint-farms"></a>La gestion des batteries de serveurs SharePoint hello
Vous pouvez administrer des serveurs de hello de ces batteries de serveurs via des connexions Bureau à distance. Pour plus d’informations, consultez [ouvrir une session sur l’ordinateur virtuel de toohello](quick-create-portal.md#connect-to-virtual-machine).

À partir du site Central Administration SharePoint de hello, vous pouvez configurer mes sites, les applications SharePoint et autres fonctionnalités. Pour plus d'informations, consultez la page sur la [configuration de SharePoint](http://technet.microsoft.com/library/ee836142.aspx).

## <a name="next-steps"></a>Étapes suivantes
* Découvrez d’autres [configurations de SharePoint](https://technet.microsoft.com/library/dn635309.aspx) dans les services d’infrastructure Azure.
