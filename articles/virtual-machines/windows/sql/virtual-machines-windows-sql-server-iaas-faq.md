---
title: aaaSQL serveur sur le Forum aux questions sur les ordinateurs virtuels de Azure | Documents Microsoft
description: "Cet article fournit des réponses aux questions sur SQL Server en cours d’exécution sur des machines virtuelles Azure d’elles sonttrop."
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
ms.openlocfilehash: 70a8777bf765dcc69f433aa1fb59eb94929caab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-sql-server-on-azure-virtual-machines"></a>Forum Aux Questions (FAQ) relatives à SQL Server sur les machines virtuelles Azure
Cette rubrique fournit des questions courantes sur l’exécution toosome réponses Hello [SQL Server sur des Machines virtuelles Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="frequently-asked-questions"></a>Forum Aux Questions (FAQ)

1. **Comment créer une machine virtuelle Azure avec SQL Server ?**

    solution la plus simple Hello est toocreate une Machine virtuelle qui inclut SQL Server. Pour un didacticiel sur l’inscription à Azure et la création d’un VM SQL à partir du portail de hello, consultez [configurer un ordinateur virtuel de SQL Server Bonjour Azure Portal](virtual-machines-windows-portal-sql-server-provision.md). Vous pouvez sélectionner une image de machine virtuelle qui utilise des licences de paie par minute SQL Server, ou vous pouvez utiliser une image qui vous permet de toobring votre propre licence SQL Server. Vous avez également option hello de manuellement l’installation de SQL Server sur une machine virtuelle et de réutilisation d’une licence sur site. Si vous utilisez votre propre licence, vous devez posséder [License Mobility via Software Assurance sur Azure](https://azure.microsoft.com/pricing/license-mobility/). Pour en savoir plus, consultez l’article [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Tarification des machines virtuelles SQL Server Azure).

1. **Qu’est la différence de hello entre les machines virtuelles SQL et hello service de base de données SQL ?**

    Conceptuellement, l’exécution de SQL Server sur une machine virtuelle Azure n’est pas si différente de l’exécution de SQL Server dans un centre de données distant. En revanche, la [base de données SQL](../../../sql-database/sql-database-technical-overview.md) fournit une base de données relationnelle complète en tant que service. Avec la base de données SQL, il est inutile machines toohello accès hébergeant vos bases de données. Pour obtenir une comparaison complète, consultez la rubrique [Choisir une option de SQL Server cloud : Base de données SQL Azure (PaaS) ou SQL Server sur des machines virtuelles Azure (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md).

1. **Comment puis-je migrer me toohello de base de données locale SQL Server Cloud ?**

    Créez tout d’abord une machine virtuelle Azure avec une instance SQL Server. Migrez ensuite votre instance toothat de bases de données sur site. Pour les stratégies de migration de données, consultez [migrer un tooSQL de base de données SQL Server serveur dans une machine virtuelle Azure](virtual-machines-windows-migrate-sql.md).

1. **Puis-je installer une deuxième instance de SQL Server sur hello même machine virtuelle ? Puis-je modifier les fonctionnalités installées de l’instance par défaut de hello ?**

    Oui. Hello support d’installation de SQL Server se trouve dans un dossier sur hello **C** lecteur. Exécutez **Setup.exe** de cette instances de SQL Server nouvelles emplacement tooadd ou de toochange autres installé des fonctionnalités de SQL Server sur l’ordinateur de hello. Notez que certaines fonctionnalités, telles que la sauvegarde automatisée, les correctifs automatiques et Azure Key Vault Integration, fonctionnent uniquement sur l’instance par défaut de hello.

1. **Puis-je désinstaller instance par défaut de hello de SQL Server ?**

    Oui. Cependant, vous devez observer quelques considérations. Comme indiqué dans la réponse précédente hello, fonctionnalités qui reposent sur hello [Extension de l’Agent SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md) ne fonctionneront que sur l’instance par défaut de hello. Si vous désinstallez d’instance par défaut de hello, extension de hello recherché toolook et peut générer des erreurs du journal des événements. Ces erreurs proviennent de hello deux sources suivantes : **gestion des informations d’identification Microsoft SQL Server** et **Microsoft SQL Server IaaS Agent**. Une des erreurs de hello peut être semblable toohello suivantes :
    
        A network-related or instance-specific error occurred while establishing a connection tooSQL Server. hello server was not found or was not accessible. 
        
    Si vous choisissez instance par défaut de hello toouninstall, également désinstaller hello [Extension de l’Agent SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md) également.

1. **Procédure de mise à niveau des tooa nouvelle version/édition de SQL Server dans une machine virtuelle Azure de hello ?**

    Il n'existe actuellement aucune mise à niveau sur place pour une instance SQL Server exécutée sur une machine virtuelle Azure. Créer une machine virtuelle Azure avec la version/édition de SQL Server hello souhaité, puis migrez vos bases de données toohello nouveau serveur à l’aide de la norme [techniques de migration des données](virtual-machines-windows-migrate-sql.md).

1. **Comment installer ma copie sous licence de SQL Server sur une machine virtuelle Azure ?**

    Il existe deux façons toodo cela. Vous pouvez configurer un des hello [des images de machine virtuelle qui prend en charge licences](virtual-machines-windows-sql-server-iaas-overview.md#BYOL). Une autre option est toocopy hello SQL Server installation media tooa machine virtuelle Windows Server, puis installez SQL Server sur la machine virtuelle de hello. Pour des raisons de licence, vous devez posséder [License Mobility via Software Assurance sur Azure](https://azure.microsoft.com/pricing/license-mobility/). Pour en savoir plus, consultez l’article [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Tarification des machines virtuelles SQL Server Azure).

1. **Puis-je modifier un toouse VM mon propre licence SQL Server si elle a été créée à partir d’une des images de paiement à l’utilisation de la galerie hello ?**

    Non. Vous pouvez passer pas à partir de toousing de licence de paie par minute votre propre licence. Créer un nouvel ordinateur virtuel Azure à l’aide de hello [les images BYOL](virtual-machines-windows-sql-server-iaas-overview.md#BYOL), puis migrer vos bases de données toohello nouveau serveur à l’aide de la norme [techniques de migration des données](virtual-machines-windows-migrate-sql.md).

1. **Les instances de cluster de basculement (FCI) SQL Server sont-elles prises en charge sur les machines virtuelles Azure ?**

   Oui. Vous pouvez [créer un Cluster de basculement Windows sur Windows Server 2016](virtual-machines-windows-portal-sql-create-failover-cluster.md) et utiliser des espaces de stockage Direct (S2D) pour le stockage de cluster hello. Vous pouvez également utiliser les solutions de clustering ou de stockage tierces comme décrit dans [Haute disponibilité et récupération d’urgence pour SQL Server sur les machines virtuelles Azure](virtual-machines-windows-sql-high-availability-dr.md#azure-only-high-availability-solutions).

1. **J’ai toopay toolicense SQL Server sur une machine virtuelle Azure si elle est uniquement utilisée pour la mise en veille ou de basculement ?**

    Vous n’avez pas toopay toolicense un SQL Server participant en tant qu’un réplica secondaire passif dans un déploiement à haute disponibilité, si vous disposez de Software Assurance et que vous utilisez la mobilité de licence comme décrit dans [FAQ sur les licences Virtual Machine](http://azure.microsoft.com/pricing/licensing-faq/).

1. **Comment les mises à jour et les service packs sont-ils appliqués sur une machine virtuelle SQL Server ?**

    Machines virtuelles vous permettent de vérifier sur l’ordinateur hôte de hello, notamment quand et comment vous appliquez des mises à jour. Hello système d’exploitation, vous pouvez appliquer manuellement les mises à jour windows, ou vous pouvez activer un service de planification appelé [correctifs automatiques](virtual-machines-windows-sql-automated-patching.md). La mise à jour corrective automatisée installe toutes les mises à jour importantes, y compris les mises à jour de SQL Server de cette catégorie. Autres tooSQL de mises à jour facultatives que serveur doit être installé manuellement.

1. **Il est possible tooset les configurations ne pas affiché dans la galerie de machine virtuelle hello (par exemple Windows 2008 R2 + SQL Server 2012) ?**

    Non. Pour les images de la galerie de machine virtuelle qui incluent SQL Server, vous devez sélectionner une des hello images fournie.

1. **Comment installer les outils SQL Data sur ma machine virtuelle Azure ?**

     Téléchargez et installez les outils de données SQL hello à partir [Microsoft SQL Server Data Tools - Business Intelligence pour Visual Studio 2013](https://www.microsoft.com/en-us/download/details.aspx?id=42313).

## <a name="resources"></a>Ressources

Pour une vue d’ensemble de SQL Server sur des Machines virtuelles Azure, visionnez la vidéo de hello [machine virtuelle Azure est la plateforme de meilleures hello pour SQL Server 2016](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016). Vous pouvez également obtenir une bonne introduction rubrique hello [SQL Server sur une vue d’ensemble des Machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md).

Les autres ressources incluent :

* [Configurer un ordinateur virtuel de SQL Server dans hello portail Azure](virtual-machines-windows-portal-sql-server-provision.md)
* [Migration d’une base de données de tooSQL Server sur une machine virtuelle Azure](virtual-machines-windows-migrate-sql.md)
* [Haute disponibilité et récupération d’urgence pour SQL Server dans Azure Virtual Machines](virtual-machines-windows-sql-high-availability-dr.md)
* [Meilleures pratiques relatives aux performances de SQL Server dans les machines virtuelles Azure](virtual-machines-windows-sql-performance.md)
* [Modèles d'application et stratégies de développement pour SQL Server dans Azure Virtual Machines](virtual-machines-windows-sql-server-app-patterns-dev-strategies.md) 