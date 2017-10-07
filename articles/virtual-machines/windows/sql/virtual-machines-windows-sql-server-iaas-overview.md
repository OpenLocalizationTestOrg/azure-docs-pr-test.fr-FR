---
title: aaaOverview de SQL Server sur des Machines virtuelles Azure | Documents Microsoft
description: "Découvrez comment toorun complète des éditions de SQL Server sur des machines virtuelles Azure. Obtenir des images de machine virtuelle SQL Server tooall de liens directs et le contenu associé."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: c505089e-6bbf-4d14-af0e-dd39a1872767
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: 07be567c76f4435961592fc0872fe41cd45bd79d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-sql-server-on-azure-virtual-machines"></a>Présentation de SQL Server sur les machines virtuelles Azure
Cette rubrique décrit les options pour l’exécution de SQL Server sur des machines virtuelles (VM), avec [relie les images de tooportal](#option-1-create-a-sql-vm-with-per-minute-licensing) et une vue d’ensemble de [tâches courantes](#manage-your-sql-vm).

> [!NOTE]
> Si vous êtes déjà familiarisé avec SQL Server et que vous souhaitiez toosee toodeploy une machine virtuelle SQL Server, voir [configurer un ordinateur virtuel de SQL Server Bonjour Azure portal](virtual-machines-windows-portal-sql-server-provision.md).
> 
> 

## <a name="overview"></a>Vue d'ensemble
Si vous êtes un administrateur de base de données ou un développeur, machines virtuelles Azure fournissent un moyen toomove votre local SQL Server les charges de travail et applications toohello Cloud. Hello vidéo suivante fournit une vue d’ensemble technique des machines virtuelles Azure de SQL Server.

> [!VIDEO https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016/player]
> 
> 

Hello vidéo couvre hello suivant les zones suivantes :

| Temps | Domaine |
| --- | --- |
| 00:21 |Que sont les machines virtuelles Azure ? |
| 01:45 |Sécurité |
| 02:50 |Connectivité |
| 03:30 |Performances et fiabilité de stockage |
| 05:20 |Tailles de machine virtuelle |
| 05:54 |Haute disponibilité et SLA |
| 07:30 |Prise en charge de la configuration |
| 08:00 |Surveillance |
| 08:32 |Démo : Création d’une machine virtuelle SQL Server 2016 |

> [!NOTE]
> Hello vidéo se concentre sur SQL Server 2016, mais Azure fournit des images de machine virtuelle pour plusieurs versions de SQL Server, y compris 2012, 2014 et 2016. 
> 
> 

## <a name="scenarios"></a>Scénarios
Il existe de nombreuses raisons que vous pouvez choisir toohost vos données dans Azure. Si votre application se déplace tooAzure, elle améliore les performances tooalso déplacement hello des données. Mais il existe d’autres avantages. Vous avez automatiquement accès toomultiple des centres de données pour une récupération d’urgence et de présence globale. les données de salutation sont également hautement sécurisé et fiable.

L’exécution de SQL Server sur des machines virtuelles Azure vous permet de stocker des données relationnelles dans Azure. C’est un bon choix pour plusieurs scénarios. Par exemple, vous pourriez tooconfigure hello Azure VM de même ordinateur SQL Server local, tooan possible. Vous pouvez également toorun des applications et services sur hello même serveur de base de données. Deux ressources principales peuvent vous aider à réfléchir à d’autres scénarios et considérations :

* [SQL Server sur des machines virtuelles](https://azure.microsoft.com/services/virtual-machines/sql-server/) fournit une vue d’ensemble des scénarios de meilleures hello pour l’utilisation de SQL Server sur des machines virtuelles Azure. 
* [Choisir une option de SQL Server cloud : Base de données SQL Azure (PaaS) ou SQL Server sur des machines virtuelles Azure (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md) compare de manière détaillée l’exécution de SQL Database et de SQL Server sur une machine virtuelle.

## <a name="create-a-new-sql-vm"></a>Créer une nouvelle machine virtuelle SQL
Hello sections suivantes fournissent des liens directs toohello portail Azure pour les images de la galerie de machine virtuelle SQL Server hello. En fonction de l’image de hello que vous sélectionnez, vous pouvez soit payer pour les coûts de licence SQL Server sur une base par minute, ou vous pouvez mettre votre propre licence (BYOL).

Trouver des instructions pas à pas pour la création d’un VM SQL nouveau didacticiel hello [configurer un ordinateur virtuel de SQL Server Bonjour Azure portal](virtual-machines-windows-portal-sql-server-provision.md). En outre, consultez hello [les procédures recommandées pour les machines virtuelles SQL Server](virtual-machines-windows-sql-performance.md), qui explique comment ordinateur approprié tooselect hello taille et d’autre fonctionnalités disponible lors de la configuration.

## <a name="option-1-create-a-sql-vm-with-per-minute-licensing"></a>Option 1 : Créer une machine virtuelle SQL avec licence à la minute
Hello tableau suivant fournit une matrice des images de SQL Server plus récente hello dans la galerie de machine virtuelle hello. Cliquez sur n’importe quel toobegin lien Créer un VM SQL nouvelle avec votre version spécifiée, une édition et un système d’exploitation. 

> [!TIP]
> toounderstand hello machine virtuelle et la tarification de SQL pour ces images, consultez [tarification des conseils pour les machines virtuelles Azure de SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md).

| Version | Système d’exploitation | Édition |
| --- | --- | --- |
| **SQL Server 2016 SP1** |Windows Server 2016 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1ExpressWindowsServer2016), [Developer](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1DeveloperWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2WebWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2ExpressWindowsServer2012R2) |
| **SQL Server 2012 SP3** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3WebWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3ExpressWindowsServer2012R2) |

En outre la liste toothis, autres combinaisons de systèmes d’exploitation et les versions de SQL Server sont disponibles. Trouver d’autres images via une recherche marketplace Bonjour portail Azure. 

## <a id="BYOL"></a> Option 2 : Créer une machine virtuelle SQL avec une licence existante
Vous pouvez également apporter votre propre licence (modèle BYOL). Dans ce scénario, vous ne payez hello machine virtuelle sans des frais supplémentaires pour les licences de SQL Server. toouse votre propre licence, la matrice de hello utilisation des versions de SQL Server, les éditions et les systèmes d’exploitation ci-dessous. Dans le portail hello, ces noms de l’image sont préfixés avec **{BYOL}**.

> [!TIP]
> Apporter votre propre licence peut être avantageux sur le long terme pour des charges de travail de production continue. Pour en savoir plus, consultez l’article [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Tarification des machines virtuelles SQL Server Azure).

| Version | Système d’exploitation | Édition |
| --- | --- | --- |
| **SQL Server 2016 SP1** |Windows Server 2016 |[BYOL Enterprise](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016), [BYOL Standard](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[BYOL Enterprise](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP2EnterpriseWindowsServer2012R2), [BYOL Standard](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP2StandardWindowsServer2012R2) |
| **SQL Server 2012 SP2** |Windows Server 2012 R2 |[BYOL Enterprise](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3EnterpriseWindowsServer2012R2), [BYOL Standard](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3StandardWindowsServer2012R2) |

En outre la liste toothis, autres combinaisons de systèmes d’exploitation et les versions de SQL Server sont disponibles. Rechercher les autres images via une recherche marketplace Bonjour Azure portal (recherche de « {BYOL} SQL Server »).

> [!IMPORTANT]
> images de toouse BYOL VM, vous devez disposer d’un contrat d’entreprise avec [License Mobility via Software Assurance sur Azure](https://azure.microsoft.com/pricing/license-mobility/). Vous devez également posséder une licence valide pour hello/édition de la version de SQL Server, vous souhaitez toouse. Vous devez [fournir hello nécessaires BYOL informations tooMicrosoft](http://d36cz9buwru1tt.cloudfront.net/License_Mobility_Customer_Verification_Guide.pdf) dans **10** jours à compter de la mise en service votre machine virtuelle. 

> [!NOTE]
> Il n’est pas hello toochange possible votre propre licence de modèle d’un toouse de machine virtuelle SQL Server de paie par minute de licence. Dans ce cas, vous devez créer un VM BYOL nouvelle et migrer vos bases de données toohello nouvelle machine virtuelle. 

## <a name="manage-your-sql-vm"></a>Gérer votre machine virtuelle SQL
Après avoir approvisionné votre machine virtuelle SQL Server, vous pouvez effectuer plusieurs tâches de gestion facultatives. Par bien des aspects, vous configurez et gérez SQL Server exactement comme vous le feriez avec une instance SQL Server locale. Toutefois, certaines tâches sont tooAzure spécifique. Hello sections suivantes illustrent certaines de ces zones avec les informations de toomore de liens.

### <a name="connect-toohello-vm"></a>Se connecter toohello machine virtuelle
Une des étapes de gestion plus simples hello est tooconnect tooyour machine virtuelle SQL Server via des outils, tels que SQL Server Management Studio (SSMS). Pour obtenir des instructions sur tooconnect tooyour nouveau SQL Server virtuelle, voir [connecter tooa Machine virtuelle de SQL Server sur Azure](virtual-machines-windows-sql-connect.md).

### <a name="migrate-your-data"></a>Migration de vos données
Si vous avez une base de données existante, vous souhaiterez toomove que toohello nouvellement approvisionnés SQL VM. Pour obtenir la liste des options de migration et des instructions, consultez [migrer une base de données de tooSQL Server sur une machine virtuelle Azure](virtual-machines-windows-migrate-sql.md).

### <a name="configure-high-availability"></a>Configurer la haute disponibilité
Si vous avez besoin d’une haute disponibilité, pensez à configurer les groupes de disponibilité SQL Server. Cela implique la présence de plusieurs machines virtuelles Azure dans un réseau virtuel. Hello portail Azure a un modèle qui définit cette configuration pour vous. Pour plus d’informations, voir [Configurer un groupe de disponibilité AlwaysOn dans des machines virtuelles Azure Resource Manager](virtual-machines-windows-portal-sql-alwayson-availability-groups.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Si vous souhaitez toomanually configurer votre groupe de disponibilité et l’écouteur associé, consultez [configurer des groupes de disponibilité AlwaysOn dans Azure VM](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

Pour plus d’informations sur la haute disponibilité, consultez [Haute disponibilité et récupération d’urgence pour SQL Server sur des machines virtuelles Azure](virtual-machines-windows-sql-high-availability-dr.md).

### <a name="back-up-your-data"></a>Sauvegarde de vos données
Machines virtuelles Azure peuvent tirer parti de [sauvegarde automatisée](virtual-machines-windows-sql-automated-backup.md), qui crée régulièrement des sauvegardes de votre stockage tooblob de base de données. Vous pouvez utiliser cette technique manuellement. Pour plus d’informations, voir [Utilisation du stockage Azure pour la sauvegarde et la restauration de SQL Server](virtual-machines-windows-use-storage-sql-server-backup-restore.md). Pour une vue d’ensemble des options de sauvegarde et de restauration, voir [Sauvegarde et restauration de SQL Server dans les machines virtuelles Azure](virtual-machines-windows-sql-backup-recovery.md).

### <a name="automate-updates"></a>Automatiser les mises à jour
Machines virtuelles Azure peuvent utiliser [correctifs automatiques](virtual-machines-windows-sql-automated-patching.md) tooschedule une fenêtre de maintenance pour l’installation importants de windows et SQL Server met à jour automatiquement.

### <a name="customer-experience-improvement-program-ceip"></a>Programme d’amélioration du produit (CEIP)
Hello programme (amélioration) est activée par défaut. Ce régulièrement envoie des rapports tooMicrosoft toohelp améliorer SQL Server. Il n’existe aucune tâche de gestion nécessaire avec le CEIP, sauf si vous souhaitez toodisable après l’approvisionnement. Vous pouvez personnaliser ou désactiver hello CEIP en vous connectant toohello machine virtuelle avec le Bureau à distance. Puis exécutez hello **SQL serveur de rapports d’erreurs et d’utilisation** utilitaire. Suivez hello instructions toodisable reporting. 

Pour plus d’informations, consultez hello section CEIP de hello [accepter les termes du contrat de licence](https://msdn.microsoft.com/library/ms143343.aspx) rubrique. 

## <a name="next-steps"></a>Étapes suivantes

Pour toute question sur la tarification, consultez [tarification des conseils pour les machines virtuelles Azure de SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md) et hello [Azure page de tarification](https://azure.microsoft.com/pricing/details/virtual-machines/windows/). Sélectionnez votre édition de la cible de SQL Server dans hello **du système d’exploitation/Software** liste. Puis afficher les prix de hello pour les machines virtuelles différentes tailles.

D’autres questions ? Tout d’abord, consultez hello [SQL Server sur le Forum aux questions sur Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-faq.md). Mais également d’ajouter votre bas toohello questions ou des commentaires de n’importe quel toointeract de rubriques SQL VM avec la Communauté Microsoft et hello.
