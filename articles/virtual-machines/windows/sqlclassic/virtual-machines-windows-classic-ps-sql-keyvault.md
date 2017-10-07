---
title: "aaaIntegrate le coffre de clés avec SQL Server sur des machines virtuelles Windows Azure (classique) | Documents Microsoft"
description: "Découvrez comment tooautomate hello configuration du chiffrement de SQL Server pour une utilisation avec le coffre de clés Azure. Cette rubrique explique comment créer, toouse Azure Key Vault Integration avec les machines virtuelles SQL Server dans le modèle de déploiement classique hello."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: ab8d41a7-1971-4032-ab71-eb435c455dc1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 02/17/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 54664875b76dac7271d5a9f00b3f41fdc9c08491
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-classic"></a>Configurer Azure Key Vault Integration pour SQL Server sur des machines virtuelles Azure (Classic)
> [!div class="op_single_selector"]
> * [Gestionnaire de ressources](../sql/virtual-machines-windows-ps-sql-keyvault.md)
> * [Classique](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a>Vue d’ensemble
Il existe plusieurs fonctionnalités de chiffrement SQL Server, telles que le [chiffrement transparent des données (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), le [chiffrement au niveau des colonnes (CLE)](https://msdn.microsoft.com/library/ms173744.aspx) et le [chiffrement de sauvegarde](https://msdn.microsoft.com/library/dn449489.aspx). Ces formes de chiffrement nécessitent toomanage et stockent des clés de chiffrement de hello utilisé pour le chiffrement. Hello service d’Azure Key Vault (AKV) est conçue tooimprove hello sécurité et gestion de ces clés dans un emplacement sécurisé et hautement disponible. Hello [connecteur SQL Server](http://www.microsoft.com/download/details.aspx?id=45344) permet à SQL Server toouse ces clés à partir d’Azure Key Vault.

> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../azure-resource-manager/resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.

Si vous exécutez SQL Server avec les ordinateurs locaux, des [étapes que vous pouvez suivre tooaccess coffre de clés Azure à partir de votre ordinateur local, SQL Server](https://msdn.microsoft.com/library/dn198405.aspx). Mais pour SQL Server dans des machines virtuelles Azure, vous pouvez gagner du temps à l’aide de hello *Azure Key Vault Integration* fonctionnalité. Avec quelques tooenable d’applets de commande Azure PowerShell cette fonctionnalité, vous pouvez automatiser hello configuration nécessaire pour un tooaccess SQL VM votre coffre de clés.

Lorsque cette fonctionnalité est activée, elle installe hello connecteur SQL Server, configure automatiquement tooaccess de fournisseur EKM hello coffre de clés Azure et crée hello d’informations d’identification tooallow vous tooaccess votre archivage. Si vous avez examiné étapes hello Bonjour mentionné précédemment documentation locale, vous pouvez voir que cette fonctionnalité automatise les étapes 2 et 3. Vous devez toujours toodo manuellement seul Hello est clés et coffre de clés toocreate hello. À partir de là, hello ensemble le programme d’installation de votre VM SQL est automatisée. Une fois que cette fonctionnalité a terminé cette installation, vous pouvez exécuter toobegin d’instructions T-SQL chiffrement des sauvegardes des bases de données comme vous le feriez normalement.

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="configure-akv-integration"></a>Configuration d'AKV Integration
Utilisez PowerShell tooconfigure Azure Key Vault Integration. Hello les sections suivantes fournit une vue d’ensemble de paramètres de hello requis, puis un exemple de script PowerShell.

### <a name="install-hello-sql-server-iaas-extension"></a>Installer hello IaaS Extension de SQL Server
Tout d’abord, [installer hello IaaS Extension de SQL Server](../classic/sql-server-agent-extension.md).

### <a name="understand-hello-input-parameters"></a>Comprendre les paramètres d’entrée hello
Hello paramètres hello de listes de table suivants requis toorun de script PowerShell hello dans la section suivante de hello.

| Paramètre | Description | Exemple |
| --- | --- | --- |
| **$akvURL** |**URL de coffre de clés Hello** |« https://contosokeyvault.vault.azure.net/ » |
| **$spName** |**Nom du principal du service** |« fde2b411-33d5-4e11-af04eb07b669ccf2 » |
| **$spSecret** |**Secret du principal du service** |« 9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM= » |
| **$credName** |**Nom d’identification**: AKV Integration crée des informations d’identification dans SQL Server, ce qui permet de hello VM toohave accès toohello coffre de clés. Choisissez un nom pour cette identification. |« mycred1 » |
| **$vmName** |**Nom de machine virtuelle**: nom hello d’un VM SQL créé précédemment. |« myvmname » |
| **$serviceName** |**Nom du service**: nom du Service Cloud hello associé hello SQL VM. |« mycloudservicename » |

### <a name="enable-akv-integration-with-powershell"></a>Activation d'AKV Integration avec PowerShell
Hello **New-AzureVMSqlServerKeyVaultCredentialConfig** applet de commande crée un objet de configuration pour la fonctionnalité d’Azure Key Vault Integration hello. Hello **Set-AzureVMSqlServerExtension** configure cette intégration avec hello **KeyVaultCredentialSettings** paramètre. Hello suivant les étapes indiquent comment toouse ces commandes.

1. Dans Azure PowerShell, d’abord configurer les paramètres d’entrée hello avec les valeurs spécifiques comme décrit dans les sections précédentes hello de cette rubrique. Hello script suivant est un exemple.
   
        $akvURL = "https://contosokeyvault.vault.azure.net/"
        $spName = "fde2b411-33d5-4e11-af04eb07b669ccf2"
        $spSecret = "9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="
        $credName = "mycred1"
        $vmName = "myvmname"
        $serviceName = "mycloudservicename"
2. Suivant de hello utilisation tooconfigure de script, puis activer l’intégration de AKV.
   
        $secureakv =  $spSecret | ConvertTo-SecureString -AsPlainText -Force
        $akvs = New-AzureVMSqlServerKeyVaultCredentialConfig -Enable -CredentialName $credname -AzureKeyVaultUrl $akvURL -ServicePrincipalName $spName -ServicePrincipalSecret $secureakv
        Get-AzureVM -ServiceName $serviceName -Name $vmName | Set-AzureVMSqlServerExtension -KeyVaultCredentialSettings $akvs | Update-AzureVM

Hello, Extension de l’Agent IaaS SQL met à jour hello SQL VM avec cette nouvelle configuration.

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

