---
title: "coûts aaaManage efficacement pour SQL Server sur des machines virtuelles | Documents Microsoft"
description: "Fournit les meilleures pratiques pour le choix hello droite machine virtuelle SQL Server modèle de tarification."
services: virtual-machines-windows
documentationcenter: na
author: luisherring
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/18/2017
ms.author: jroth
ms.openlocfilehash: 6c6a4394e95b5a915ea3e7d5965730000d331036
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="pricing-guidance-for-sql-server-azure-vms"></a>Tarification des machines virtuelles SQL Server Azure

Cette rubrique fournit des informations de tarification pour les machines virtuelles SQL Server dans Azure. Il existe plusieurs options qui affectent le coût, et il est important toopick hello image de droite qui équilibre les coûts avec les besoins de l’entreprise.

## <a name="free-licensed-sql-server-editions"></a>Éditions SQL Server sous licence libre

Si vous souhaitez toodevelop, tester, ou générer une preuve de concept, puis utilisez hello sous licence libre **SQL Server Developer edition**. Cette édition a tous les éléments dans l’édition Enterprise de SQL Server, par conséquent, vous pouvez l’utiliser toobuild application de votre choix. Il n’est pas autorisée toorun en production. Un ordinateur virtuel de SQL Server Developer facture uniquement coût hello Hello machine virtuelle, ne pas pour les licences de SQL Server.

Si vous souhaitez toorun une charge de travail légère en production (< 4 cœurs, < 1 Go de mémoire, < 10 Go/base de données), puis utilisez hello sous licence libre **SQL Server Express edition**. Une machine virtuelle de SQL Express seulement facture coût hello Hello machine virtuelle, pas de licence SQL.

Pour ces charges de travail de développement/test ou de production légère, vous pouvez également faire des économies en choisissant une machine virtuelle plus petite qui correspond davantage à ces charges de travail. Hello DS1v2 peut être un bon choix pour ces charges de travail.

toocreate SQL Server 2016 Azure VM avec l’un de ces images, consultez hello suivant liens :

- [Machine virtuelle Azure SQL Server 2016 Developer](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1DeveloperWindowsServer2016-ARM)
- [Machine virtuelle Azure SQL Server 2016 Express](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1ExpressWindowsServer2016-ARM)

## <a name="paid-sql-server-editions"></a>Éditions SQL Server payantes

Si vous avez une charge de travail légère non production, utilisez une des hello suivant des éditions de SQL Server :

| Édition SQL Server | Charge de travail |
|-----|-----|
| Web | Petits sites web |
| Standard | Charges de travail toomedium petit |
| Entreprise | Charges de travail volumineuses ou critiques|

Vous avez deux options toopay, des licences de SQL Server pour ces éditions : *payer par l’utilisation de* ou *mettre votre propre licence*.

### <a name="pay-per-usage"></a>Paiement à l’utilisation

**Licence de SQL Server qui paient hello par utilisation** signifie que le coût par minute de hello de l’exécution de hello Azure VM inclut coût hello de licence de SQL Server hello. Vous pouvez voir hello tarification hello différentes éditions de SQL Server (Web, Standard, entreprise) Bonjour [page de tarification de Azure VM](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard). Hello coût est hello identique pour toutes les versions de SQL Server (2008 R2 too2016). Comme avec SQL Server licences hello en général, coût de licence par minute dépend nombre hello de cœurs de l’ordinateur virtuel.

Payer hello SQL Server par l’utilisation de licence est recommandée pour :

- Les charges de travail temporaires ou périodiques. Par exemple, une application qui doit toosupport un événement pour quelques mois chaque année, ou l’analyse de l’entreprise le lundi.
- Les charges de travail dont la durée de vie ou la mise à l’échelle ne sont pas connues. Par exemple, une application qui peut ne pas être requise dans quelques mois, ou qui peut nécessiter plus ou moins de puissance de calcul, en fonction de la demande.

toocreate SQL Server 2016 Azure VM avec l’un de ces images de paie utilisation, consultez hello suivant liens :

- [Machine virtuelle Azure Web SQL Server 2016](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016)
- [Machine virtuelle Azure Standard SQL Server 2016](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016)
- [Machine virtuelle Azure Entreprise SQL Server 2016](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016)

> [!IMPORTANT]
> Lorsque vous créez une machine virtuelle SQL Server dans hello portail Azure, hello estimation du coût mensuel affiché sur hello **choisir une taille** panneau n’inclut pas les coûts des licences de SQL Server. Il s’agit de coût hello Hello machine virtuelle autonome.
>
> ![Panneau Choisir la taille de la machine virtuelle](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-choose-size-pricing-estimate.png)
>
>Pour hello sous licence libre éditions Express et Developer de SQL Server, il s’agit de coût estimé de hello total. Mais pour Enterprise, Standard et Web, hello les coûts de licence SQL supplémentaires sur hello [page de tarification des Machines virtuelles Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/). Sur la page de tarification de hello, sélectionnez votre édition de la cible de SQL Server.

### <a name="bring-your-own-license-byol"></a>BYOL (apportez votre propre licence)

**Mettre votre propre licence SQL Server via la mobilité de licence**, également appelée tooas **BYOL**, signifie l’utilisation d’une licence en Volume SQL Server existante avec Software Assurance dans une machine virtuelle Azure. Une machine virtuelle SQL Server à l’aide de BYOL facture uniquement coût hello de l’exécution de hello machine virtuelle, ne pas pour les licences de SQL Server, étant donné que vous avez déjà acquis la Software Assurance et licences via un programme de licence en Volume.

L’apport de votre propre licence SQL par le biais de Licence Mobility est recommandé pour :

- Les charges de travail continues. Par exemple, une application qui a besoin d’opérations de l’entreprise toosupport 24 x 7.
- Les charges de travail dont la durée de vie et la mise à l’échelle sont connues. Par exemple, une application qui est nécessaire pour l’ensemble de l’année hello et la demande a été prévue.

toouse BYOL, avec une machine virtuelle SQL Server, vous devez posséder une licence pour SQL Server Standard ou Enterprise et [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx#tab=1), qui est une option requise par certains [licence en Volume](https://www.microsoft.com/en-us/download/details.aspx?id=10585) facultatif et programmes acheter avec d’autres utilisateurs.  Hello fournis via les programmes de licence en Volume des niveaux de prix varie en fonction de type hello de contrat et hello quantity et ou engagement tooSQL Server. Mais en règle générale, le placement de votre propre licence pour les charges de production en continu a hello avantages suivants :

| Avantages de la méthode BYOL | Description |
|-----|-----|
| **Réduction des coûts** | L’apport de votre propre licence SQL Server est plus économique que le paiement à l’utilisation si une charge de travail doit exécuter en permanence SQL Server Standard ou Enterprise pendant *plus de 10 mois*. |
| **Économies sur le long terme** | En moyenne, il est *30 % moins cher par année* toobuy ou renouveler une licence de SQL Server pour hello première 3 ans. En outre, après 3 ans, vous n’avez pas besoin toorenew hello licence, salaire simplement for Software Assurance. À ce stade, l’opération revient *200 % moins cher*. |
| **Réplica secondaire passif gratuit** | Un autre avantage de mettre votre propre licence est hello [libérer des licences pour un réplica secondaire passif](https://azure.microsoft.com/pricing/licensing-faq/) par SQL Server à des fins de haute disponibilité. Cela réduit la moitié Bonjour licences le coût d’un déploiement à haute disponibilité de SQL Server (par exemple, à l’aide de groupes de disponibilité AlwaysOn). Hello droits toorun hello passif base de données secondaire sont fournis via hello avantage du basculement serveurs Software Assurance. |

toocreate SQL Server 2016 Azure VM avec l’un de ces images mettre votre-propriétaire-licence, voir les machines virtuelles de hello précédés de « {BYOL} » :

- [Machine virtuelle Azure Entreprise SQL Server 2016](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1EnterpriseWindowsServer2016)
- [Machine virtuelle Azure Standard SQL Server 2016](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016)

> [!NOTE]
> Veuillez nous indiquer sous 10 jours le nombre de licences SQL Server que vous utiliserez dans Azure. Hello liens toohello précédente images ont des instructions sur la façon de toodo cela.

## <a name="avoid-unecessary-costs"></a>Éviter les coûts inutiles

Si vous utilisez des charges de travail qui n’exécutent pas en permanence, envisagez d’arrêt de la machine virtuelle de hello pendant les périodes d’inactivité hello. Vous paierez uniquement pour ce que vous utiliserez.

Par exemple, si vous essayez simplement de SQL Server sur une machine virtuelle Azure, pas souhaité tooincur frais en le laissant accidentellement en cours d’exécution pour les semaines. Une solution consiste à toouse hello [extinction automatique](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).

![Arrêt automatique des machines virtuelles SQL](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-auto-shutdown.png)

L’arrêt automatique fait partie d’un ensemble plus important de fonctionnalités similaires fournies par [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab).

Pour les autres flux de travail, envisagez l’arrêt et le redémarrage automatiques des machines virtuelles Azure avec une solution de script, comme [Azure Automation](https://azure.microsoft.com/services/automation/).

> [!IMPORTANT]
> L’arrêt et la désallocation de votre machine virtuelle sont hello ne moyen tooavoid serez facturé. Simplement l’arrêt ou à l’aide de tooshut des options d’alimentation vers le bas hello VM occasionne toujours des frais d’utilisation.

## <a name="next-steps"></a>Étapes suivantes

Pour obtenir une assistance globale sur la tarification Azure, consultez [Éviter les coûts inattendus avec la gestion de la facturation et des coûts dans Azure](../../../billing/billing-getting-started.md).

Pourquoi les Machines virtuelles plus récentes de tarification, y compris SQL Server, consultez hello [page de tarification de Azure VM](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard).

Consultez d’autres rubriques relatives aux machines virtuelles avec SQL Server à la page [Vue d’ensemble de SQL Server sur les machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md).
