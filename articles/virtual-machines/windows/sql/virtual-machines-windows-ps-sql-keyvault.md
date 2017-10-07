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
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a><span data-ttu-id="33da5-104">Configurer Azure Key Vault Integration pour SQL Server sur des machines virtuelles Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="33da5-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="33da5-105">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="33da5-105">Resource Manager</span></span>](virtual-machines-windows-ps-sql-keyvault.md)
> * [<span data-ttu-id="33da5-106">Classique</span><span class="sxs-lookup"><span data-stu-id="33da5-106">Classic</span></span>](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="33da5-107">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="33da5-107">Overview</span></span>
<span data-ttu-id="33da5-108">Il existe plusieurs fonctionnalités de chiffrement SQL Server, telles que le [chiffrement transparent des données (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), le [chiffrement au niveau des colonnes (CLE)](https://msdn.microsoft.com/library/ms173744.aspx) et le [chiffrement de sauvegarde](https://msdn.microsoft.com/library/dn449489.aspx).</span><span class="sxs-lookup"><span data-stu-id="33da5-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span></span> <span data-ttu-id="33da5-109">Ces formes de chiffrement nécessitent toomanage et stockent des clés de chiffrement de hello utilisé pour le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="33da5-109">These forms of encryption require you toomanage and store hello cryptographic keys you use for encryption.</span></span> <span data-ttu-id="33da5-110">Hello service d’Azure Key Vault (AKV) est conçue tooimprove hello sécurité et gestion de ces clés dans un emplacement sécurisé et hautement disponible.</span><span class="sxs-lookup"><span data-stu-id="33da5-110">hello Azure Key Vault (AKV) service is designed tooimprove hello security and management of these keys in a secure and highly available location.</span></span> <span data-ttu-id="33da5-111">Hello [connecteur SQL Server](http://www.microsoft.com/download/details.aspx?id=45344) permet à SQL Server toouse ces clés à partir d’Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="33da5-111">hello [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server toouse these keys from Azure Key Vault.</span></span>

<span data-ttu-id="33da5-112">Si vous exécutez SQL Server locale d’ordinateurs, il sont [étapes que vous pouvez suivre tooaccess coffre de clés Azure à partir de votre ordinateur local, SQL Server](https://msdn.microsoft.com/library/dn198405.aspx).</span><span class="sxs-lookup"><span data-stu-id="33da5-112">If you running SQL Server with on-premises machines, there are [steps you can follow tooaccess Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span></span> <span data-ttu-id="33da5-113">Mais pour SQL Server dans des machines virtuelles Azure, vous pouvez gagner du temps à l’aide de hello *Azure Key Vault Integration* fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="33da5-113">But for SQL Server in Azure VMs, you can save time by using hello *Azure Key Vault Integration* feature.</span></span>

<span data-ttu-id="33da5-114">Lorsque cette fonctionnalité est activée, elle installe hello connecteur SQL Server, configure automatiquement tooaccess de fournisseur EKM hello coffre de clés Azure et crée hello d’informations d’identification tooallow vous tooaccess votre archivage.</span><span class="sxs-lookup"><span data-stu-id="33da5-114">When this feature is enabled, it automatically installs hello SQL Server Connector, configures hello EKM provider tooaccess Azure Key Vault, and creates hello credential tooallow you tooaccess your vault.</span></span> <span data-ttu-id="33da5-115">Si vous avez examiné étapes hello Bonjour mentionné précédemment documentation locale, vous pouvez voir que cette fonctionnalité automatise les étapes 2 et 3.</span><span class="sxs-lookup"><span data-stu-id="33da5-115">If you looked at hello steps in hello previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span></span> <span data-ttu-id="33da5-116">Vous devez toujours toodo manuellement seul Hello est clés et coffre de clés toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="33da5-116">hello only thing you would still need toodo manually is toocreate hello key vault and keys.</span></span> <span data-ttu-id="33da5-117">À partir de là, hello ensemble le programme d’installation de votre VM SQL est automatisée.</span><span class="sxs-lookup"><span data-stu-id="33da5-117">From there, hello entire setup of your SQL VM is automated.</span></span> <span data-ttu-id="33da5-118">Une fois que cette fonctionnalité a terminé cette installation, vous pouvez exécuter toobegin d’instructions T-SQL chiffrement des sauvegardes des bases de données comme vous le feriez normalement.</span><span class="sxs-lookup"><span data-stu-id="33da5-118">Once this feature has completed this setup, you can execute T-SQL statements toobegin encrypting your databases or backups as you normally would.</span></span>

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a><span data-ttu-id="33da5-119">Activation et configuration de l’intégration AKV</span><span class="sxs-lookup"><span data-stu-id="33da5-119">Enabling and configuring AKV integration</span></span>
<span data-ttu-id="33da5-120">Vous pouvez activer l’intégration AKV lors de l’approvisionnement ou vous pouvez la configurer pour les machines virtuelles existantes.</span><span class="sxs-lookup"><span data-stu-id="33da5-120">You can enable AKV integration during provisioning or configure it for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="33da5-121">Nouvelles machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="33da5-121">New VMs</span></span>
<span data-ttu-id="33da5-122">Si vous configurez un nouvel ordinateur virtuel de SQL Server avec le Gestionnaire de ressources, hello portail Azure fournit un tooenable étape intégration d’Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="33da5-122">If you are provisioning a new SQL Server virtual machine with Resource Manager, hello Azure portal provides a step tooenable Azure Key Vault integration.</span></span> <span data-ttu-id="33da5-123">fonctionnalité de coffre de clés Azure Hello est disponible uniquement pour les hello Enterprise, Developer et éditions d’évaluation de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="33da5-123">hello Azure Key Vault feature is available only for hello Enterprise, Developer and Evaluation Editions of SQL Server.</span></span>

![Intégration du coffre de clés Azure SQL](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

<span data-ttu-id="33da5-125">Pour une description détaillée de la configuration, consultez [configurer un ordinateur virtuel de SQL Server Bonjour Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="33da5-125">For a detailed walkthrough of provisioning, see [Provision a SQL Server virtual machine in hello Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="33da5-126">Machines virtuelles existantes</span><span class="sxs-lookup"><span data-stu-id="33da5-126">Existing VMs</span></span>
<span data-ttu-id="33da5-127">Pour les machines virtuelles SQL Server existantes, sélectionnez votre machine virtuelle SQL Server.</span><span class="sxs-lookup"><span data-stu-id="33da5-127">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="33da5-128">Puis sélectionnez hello **configuration de SQL Server** section Hello **paramètres** panneau.</span><span class="sxs-lookup"><span data-stu-id="33da5-128">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Intégration AKV SQL pour les machines virtuelles existantes](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

<span data-ttu-id="33da5-130">Bonjour **configuration de SQL Server** panneau, cliquez sur hello **modifier** bouton Bonjour section d’intégration de coffre de clés automatisé.</span><span class="sxs-lookup"><span data-stu-id="33da5-130">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated Key Vault integration section.</span></span>

![Configurer l’intégration AKV SQL pour les machines virtuelles existantes](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

<span data-ttu-id="33da5-132">Lorsque vous avez terminé, cliquez sur hello **OK** bouton bas hello Hello **configuration de SQL Server** panneau toosave vos modifications.</span><span class="sxs-lookup"><span data-stu-id="33da5-132">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

> [!NOTE]
> <span data-ttu-id="33da5-133">Vous pouvez également configurer l’intégration AKV à l’aide d’un modèle.</span><span class="sxs-lookup"><span data-stu-id="33da5-133">You can also configure AKV integration using a template.</span></span> <span data-ttu-id="33da5-134">Pour plus d’informations, consultez l’article [Azure quickstart template for Azure Key Vault integration](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update)(Modèle de démarrage rapide d’Azure pour l’intégration d’Azure Key Vault).</span><span class="sxs-lookup"><span data-stu-id="33da5-134">For more information, see [Azure quickstart template for Azure Key Vault integration](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span></span>
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

