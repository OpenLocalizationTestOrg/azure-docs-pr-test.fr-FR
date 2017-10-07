---
title: "aaaIntegrate le coffre de clés avec SQL Server sur des machines virtuelles Windows Azure (Resource Manager) | Documents Microsoft"
description: "Découvrez comment tooautomate hello configuration du chiffrement de SQL Server pour une utilisation avec le coffre de clés Azure. Cette rubrique explique comment toouse Azure Key Vault Integration avec les machines virtuelles SQL Server créé avec le Gestionnaire de ressources."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: cd66dfb1-0e9b-4fb0-a471-9deaf4ab4ab8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: jroth
ms.openlocfilehash: 0d36d3d075d6538c18cd5ecb43c19a4b000a99e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a>Configurer Azure Key Vault Integration pour SQL Server sur des machines virtuelles Azure (Resource Manager)
> [!div class="op_single_selector"]
> * [Gestionnaire de ressources](virtual-machines-windows-ps-sql-keyvault.md)
> * [Classique](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a>Vue d’ensemble
Il existe plusieurs fonctionnalités de chiffrement SQL Server, telles que le [chiffrement transparent des données (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), le [chiffrement au niveau des colonnes (CLE)](https://msdn.microsoft.com/library/ms173744.aspx) et le [chiffrement de sauvegarde](https://msdn.microsoft.com/library/dn449489.aspx). Ces formes de chiffrement nécessitent toomanage et stockent des clés de chiffrement de hello utilisé pour le chiffrement. Hello service d’Azure Key Vault (AKV) est conçue tooimprove hello sécurité et gestion de ces clés dans un emplacement sécurisé et hautement disponible. Hello [connecteur SQL Server](http://www.microsoft.com/download/details.aspx?id=45344) permet à SQL Server toouse ces clés à partir d’Azure Key Vault.

Si vous exécutez SQL Server locale d’ordinateurs, il sont [étapes que vous pouvez suivre tooaccess coffre de clés Azure à partir de votre ordinateur local, SQL Server](https://msdn.microsoft.com/library/dn198405.aspx). Mais pour SQL Server dans des machines virtuelles Azure, vous pouvez gagner du temps à l’aide de hello *Azure Key Vault Integration* fonctionnalité.

Lorsque cette fonctionnalité est activée, elle installe hello connecteur SQL Server, configure automatiquement tooaccess de fournisseur EKM hello coffre de clés Azure et crée hello d’informations d’identification tooallow vous tooaccess votre archivage. Si vous avez examiné étapes hello Bonjour mentionné précédemment documentation locale, vous pouvez voir que cette fonctionnalité automatise les étapes 2 et 3. Vous devez toujours toodo manuellement seul Hello est clés et coffre de clés toocreate hello. À partir de là, hello ensemble le programme d’installation de votre VM SQL est automatisée. Une fois que cette fonctionnalité a terminé cette installation, vous pouvez exécuter toobegin d’instructions T-SQL chiffrement des sauvegardes des bases de données comme vous le feriez normalement.

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a>Activation et configuration de l’intégration AKV
Vous pouvez activer l’intégration AKV lors de l’approvisionnement ou vous pouvez la configurer pour les machines virtuelles existantes.

### <a name="new-vms"></a>Nouvelles machines virtuelles
Si vous configurez un nouvel ordinateur virtuel de SQL Server avec le Gestionnaire de ressources, hello portail Azure fournit un tooenable étape intégration d’Azure Key Vault. fonctionnalité de coffre de clés Azure Hello est disponible uniquement pour les hello Enterprise, Developer et éditions d’évaluation de SQL Server.

![Intégration du coffre de clés Azure SQL](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

Pour une description détaillée de la configuration, consultez [configurer un ordinateur virtuel de SQL Server Bonjour Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Machines virtuelles existantes
Pour les machines virtuelles SQL Server existantes, sélectionnez votre machine virtuelle SQL Server. Puis sélectionnez hello **configuration de SQL Server** section Hello **paramètres** panneau.

![Intégration AKV SQL pour les machines virtuelles existantes](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

Bonjour **configuration de SQL Server** panneau, cliquez sur hello **modifier** bouton Bonjour section d’intégration de coffre de clés automatisé.

![Configurer l’intégration AKV SQL pour les machines virtuelles existantes](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

Lorsque vous avez terminé, cliquez sur hello **OK** bouton bas hello Hello **configuration de SQL Server** panneau toosave vos modifications.

> [!NOTE]
> Vous pouvez également configurer l’intégration AKV à l’aide d’un modèle. Pour plus d’informations, consultez l’article [Azure quickstart template for Azure Key Vault integration](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update)(Modèle de démarrage rapide d’Azure pour l’intégration d’Azure Key Vault).
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

