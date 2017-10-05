---
title: Forum Aux Questions (FAQ) concernant SQL Server sur les machines virtuelles Azure | Microsoft Docs
description: "Cet article fournit des réponses aux questions fréquemment posées sur l'exécution de SQL Server sur les machines virtuelles Azure."
services: virtual-machines-windows
documentationcenter: 
author: v-shysun
manager: felixwu
editor: 
tags: azure-service-management
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: v-shysun
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 447ece9653a4cf69153f9c85e222e3ea4e8bae16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="frequently-asked-questions-for-sql-server-on-azure-virtual-machines"></a>Forum Aux Questions (FAQ) relatives à SQL Server sur les machines virtuelles Azure
Cette rubrique fournit des réponses à la plupart des questions courantes sur l’exécution de [SQL Server sur les machines virtuelles Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="frequently-asked-questions"></a>Forum Aux Questions (FAQ)

1. **Comment créer une machine virtuelle Azure avec SQL Server ?**

    La solution la plus simple consiste à créer une machine virtuelle qui inclut SQL Server. Pour obtenir un didacticiel sur l’inscription à Azure et la création d’une machine virtuelle SQL à partir du portail, consultez la rubrique [Approvisionnement d’une machine virtuelle SQL Server dans le portail Azure](virtual-machines-windows-portal-sql-server-provision.md). Vous pouvez sélectionner une image de machine virtuelle qui utilise la gestion de licences SQL Server avec paiement à la minute ou vous pouvez utiliser une image qui vous permet d’utiliser votre propre licence SQL Server. Vous avez également la possibilité d’installer manuellement SQL Server sur une machine virtuelle et de réutiliser une licence locale. Si vous utilisez votre propre licence, vous devez posséder [License Mobility via Software Assurance sur Azure](https://azure.microsoft.com/pricing/license-mobility/). Pour en savoir plus, consultez l’article [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Tarification des machines virtuelles SQL Server Azure).

1. **Quelle est la différence entre les machines virtuelles SQL et le service SQL Database ?**

    Conceptuellement, l’exécution de SQL Server sur une machine virtuelle Azure n’est pas si différente de l’exécution de SQL Server dans un centre de données distant. En revanche, la [base de données SQL](../../../sql-database/sql-database-technical-overview.md) fournit une base de données relationnelle complète en tant que service. Avec SQL Database, vous n’avez pas besoin d’accéder aux machines qui hébergent vos bases de données. Pour obtenir une comparaison complète, consultez la rubrique [Choisir une option de SQL Server cloud : Base de données SQL Azure (PaaS) ou SQL Server sur des machines virtuelles Azure (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md).

1. **Comment migrer ma base de données SQL Server locale vers le cloud ?**

    Créez tout d’abord une machine virtuelle Azure avec une instance SQL Server. Puis migrez vos bases de données locales vers cette instance. Pour les stratégies de migration de données, consultez la rubrique [Migrer une base de données SQL Server vers SQL Server dans une machine virtuelle Azure](virtual-machines-windows-migrate-sql.md).

1. **Puis-je installer une seconde instance SQL Server sur la même machine virtuelle ? Puis-je modifier les fonctionnalités installées de l’instance par défaut ?**

    Oui. Le support d’installation de SQL Server se trouve dans un dossier sur le lecteur **C** . Exécutez **Setup.exe** à partir de cet emplacement pour ajouter de nouvelles instances SQL Server ou pour modifier d’autres fonctionnalités SQL Server installées sur la machine. Notez que certaines fonctionnalités comme la sauvegarde automatisée, la mise à jour corrective automatisée et Azure Key Vault Integration fonctionnent uniquement sur l’instance par défaut.

1. **Puis-je désinstaller l’instance SQL Server par défaut ?**

    Oui. Cependant, vous devez observer quelques considérations. Comme indiqué dans la réponse précédente, les fonctionnalités qui reposent sur [l’extension de l’agent IaaS SQL Server](virtual-machines-windows-sql-server-agent-extension.md) fonctionnent uniquement sur l’instance par défaut. Si vous désinstallez l’instance par défaut, l’extension continue à la rechercher et peut générer des erreurs du journal des événements. Ces erreurs peuvent avoir deux sources : **gestion des informations d’identification Microsoft SQL Server** et **agent IaaS Microsoft SQL Server**. L’une des erreurs peut se présenter comme suit :
    
        A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. 
        
    Si vous décidez de désinstaller l’instance par défaut, vous devez également désinstaller [l’extension de l’agent IaaS SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

1. **Comment mettre à niveau vers une nouvelle version/édition de SQL Server dans une machine virtuelle Azure ?**

    Il n'existe actuellement aucune mise à niveau sur place pour une instance SQL Server exécutée sur une machine virtuelle Azure. Créez une machine virtuelle Azure avec la version/édition de SQL Server souhaitée, puis migrez vos bases de données vers le nouveau serveur à l’aide des [techniques de migration de données](virtual-machines-windows-migrate-sql.md)standard.

1. **Comment installer ma copie sous licence de SQL Server sur une machine virtuelle Azure ?**

    Il existe deux façons d'effectuer cette opération. Vous pouvez configurer l’une des [images de machine virtuelle qui prend en charge des licences](virtual-machines-windows-sql-server-iaas-overview.md#BYOL). Une autre option consiste à copier le support d’installation de SQL Server sur une machine virtuelle Windows Server, puis d’installer SQL Server sur la machine virtuelle. Pour des raisons de licence, vous devez posséder [License Mobility via Software Assurance sur Azure](https://azure.microsoft.com/pricing/license-mobility/). Pour en savoir plus, consultez l’article [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Tarification des machines virtuelles SQL Server Azure).

1. **Puis-je modifier une machine virtuelle pour utiliser ma propre licence SQL Server si elle a été créée à partir de l’une des images de la galerie avec paiement à l’utilisation ?**

    Non. Vous ne pouvez pas passer du mode de licence avec paiement à la minute à l’utilisation de votre propre licence. Créez une machine virtuelle Azure avec l’une des [images BYOL](virtual-machines-windows-sql-server-iaas-overview.md#BYOL), puis migrez vos bases de données vers le nouveau serveur à l’aide des [techniques de migration de données](virtual-machines-windows-migrate-sql.md) standard.

1. **Les instances de cluster de basculement (FCI) SQL Server sont-elles prises en charge sur les machines virtuelles Azure ?**

   Oui. Vous pouvez [créer un cluster de basculement Windows sur Windows Server 2016](virtual-machines-windows-portal-sql-create-failover-cluster.md) et utiliser les espaces de stockage direct (S2D) pour le stockage du cluster. Vous pouvez également utiliser les solutions de clustering ou de stockage tierces comme décrit dans [Haute disponibilité et récupération d’urgence pour SQL Server sur les machines virtuelles Azure](virtual-machines-windows-sql-high-availability-dr.md#azure-only-high-availability-solutions).

1. **Dois-je payer une licence SQL Server sur une machine virtuelle Azure si elle est utilisée uniquement pour le mode veille ou le basculement ?**

    Vous n’avez pas à payer une licence pour une instance SQL Server participant en tant que réplica secondaire passif dans un déploiement haute disponibilité, si vous disposez de Software Assurance et utilisez License Mobility comme décrit dans [FAQ sur les licences de machine virtuelle](http://azure.microsoft.com/pricing/licensing-faq/).

1. **Comment les mises à jour et les Service Packs sont-ils appliqués sur une machine virtuelle SQL Server ?**

    Les machines virtuelles vous permettent de contrôler la machine hôte, y compris quand et comment appliquer les mises à jour. Pour le système d’exploitation, vous pouvez appliquer manuellement les mises à jour Windows, ou activer un service de planification appelé [Mise à jour corrective automatisée](virtual-machines-windows-sql-automated-patching.md). La mise à jour corrective automatisée installe toutes les mises à jour importantes, y compris les mises à jour de SQL Server de cette catégorie. Les autres mises à jour SQL Server facultatives doivent être installées manuellement.

1. **Est-il possible de définir des configurations non affichées dans la galerie de machines virtuelles (par exemple, Windows 2008 R2 + SQL Server 2012) ?**

    Non. Pour les images de la galerie de machines virtuelles incluant SQL Server, vous devez sélectionner une des images fournies.

1. **Comment installer les outils SQL Data sur ma machine virtuelle Azure ?**

     Téléchargez et installez les outils SQL Data à partir de [Microsoft SQL Server Data Tools - Business Intelligence pour Visual Studio 2013 ](https://www.microsoft.com/en-us/download/details.aspx?id=42313).

## <a name="resources"></a>Ressources

Pour obtenir une vue d’ensemble de SQL Server sur les machines virtuelles Azure, regardez la vidéo [Azure VM is the best platform for SQL Server 2016](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016). Une bonne présentation est également disponible à la rubrique [Vue d’ensemble de SQL Server sur les machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md).

Les autres ressources incluent :

* [Approvisionnement d’une machine virtuelle SQL Server dans le portail Azure](virtual-machines-windows-portal-sql-server-provision.md)
* [Migrating a Database to SQL Server on an Azure VM](virtual-machines-windows-migrate-sql.md)
* [Haute disponibilité et récupération d’urgence pour SQL Server dans Azure Virtual Machines](virtual-machines-windows-sql-high-availability-dr.md)
* [Meilleures pratiques relatives aux performances de SQL Server dans les machines virtuelles Azure](virtual-machines-windows-sql-performance.md)
* [Modèles d'application et stratégies de développement pour SQL Server dans Azure Virtual Machines](virtual-machines-windows-sql-server-app-patterns-dev-strategies.md) 