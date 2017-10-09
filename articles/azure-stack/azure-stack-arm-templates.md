---
title: "modèles Azure Resource Manager d’aaaUse dans la pile de Azure | Documents Microsoft"
description: "Découvrez comment les modèles Azure Resource Manager toouse dans les ressources Azure pile tooprovision."
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
ms.author: helaw
ms.openlocfilehash: bcc73756fa712ecff9791301d43d227112be8362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-resource-manager-templates-in-azure-stack"></a>Utiliser les modèles Azure Resource Manager dans Azure Stack
Les modèles de gestionnaire de ressources Azure déploiement et approvisionnement des toutes les ressources hello pour votre application dans une opération unique et coordonnée. Vous pouvez également redéployer modèles toomake modifications toohello ressources hello groupe de ressources.

Ces modèles peuvent être déployés avec le portail de Microsoft Azure pile hello, PowerShell, ligne de commande hello et Visual Studio.

Hello suivant des modèles de démarrage rapide est disponible sur [GitHub](http://aka.ms/azurestackgithub):

## <a name="deploy-sharepoint-non-high-availability"></a>Déploiement de SharePoint (sans haute disponibilité)
Utiliser hello DSC PowerShell extension toocreate un SharePoint 2013 batterie de serveurs comprenant hello suivant des ressources :

* Un réseau virtuel
* Trois comptes de stockage
* Deux équilibreurs de charge externes
* Une machine virtuelle configurée en tant que contrôleur de domaine dans une nouvelle forêt avec un domaine unique
* Une machine virtuelle configurée sous la forme d’un serveur autonome SQL Server 2014
* Une machine virtuelle configurée comme une batterie de serveurs SharePoint 2013 composée d’un seul ordinateur

## <a name="deploy-ad-non-high-availability"></a>Déployer AD (sans haute disponibilité)
Utilisez hello DSC PowerShell extension toocreate un serveur de contrôleur de domaine Active Directory qui inclut hello suivant des ressources :

* Un réseau virtuel
* Un compte de stockage
* Un équilibreur de charge externe
* Une machine virtuelle configurée en tant que contrôleur de domaine dans une nouvelle forêt avec un domaine unique

## <a name="deploy-adsql-non-high-availability"></a>Déploiement d’AD/SQL (sans haute disponibilité)
Utiliser hello DSC PowerShell extension toocreate un SQL Server 2014 serveur autonome qui inclut hello suivant des ressources :

* Un réseau virtuel
* deux comptes de stockage ;
* Un équilibreur de charge externe
* Une machine virtuelle configurée en tant que contrôleur de domaine dans une nouvelle forêt avec un domaine unique
* Une machine virtuelle configurée sous la forme d’un serveur autonome SQL Server 2014

## <a name="vm-dsc-extension-azure-automation-pull-server"></a>VM-DSC-Extension-Azure-Automation-Pull-Server
Utilisez hello DSC PowerShell extension tooconfigure un ordinateur virtuel existant de Configuration Manager (local) et l’inscrire tooan serveur collecteur Azure Automation compte DSC.

## <a name="create-a-virtual-machine-from-a-user-image"></a>Création d’une machine virtuelle à partir d’une image utilisateur
Créez une machine virtuelle à partir d’une image utilisateur personnalisée. Ce modèle déploie également un réseau virtuel (avec DNS), une adresse IP publique et une interface réseau.

## <a name="simple-vm"></a>Machine virtuelle simple
Déployez une machine virtuelle Windows comprenant un réseau virtuel (avec DNS), une adresse IP publique et une interface réseau.

## <a name="cancel-a-running-template-deployment"></a>Annuler le déploiement d’un modèle en cours d’exécution
toocancel un déploiement de modèle en cours d’exécution, utilisez hello `Stop-AzureRmResourceGroupDeployment` applet de commande PowerShell.

## <a name="next-steps"></a>Étapes suivantes
[Déployer des modèles de portail de hello](azure-stack-deploy-template-portal.md)

[Présentation d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)

