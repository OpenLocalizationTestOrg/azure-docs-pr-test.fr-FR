---
title: "aaaManage bases de données SQL Azure à l’aide d’Azure Automation | Documents Microsoft"
description: "Découvrez comment hello service Azure Automation peut être utilisés toomanage bases de données SQL Azure à l’échelle."
services: sql-database, automation
documentationcenter: 
author: jodoglevy
manager: jhubbard
editor: monicar
ms.assetid: 77c262a1-9b93-456d-b3c7-b2f23bdfcd61
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: jhubbard
ms.openlocfilehash: d613cca32ba86e27b9c1b952c4e723ea7f07beb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-sql-databases-using-azure-automation"></a>Gestion des bases de données SQL Azure à l'aide d'Azure Automation
Ce guide vous oblige à service d’Azure Automation toohello et comment il peut être gestion toosimplify utilisés de vos bases de données SQL Azure.

## <a name="what-is-azure-automation"></a>Qu'est-ce qu'Azure Automation ?
[Azure Automation](https://azure.microsoft.com/services/automation/) est un service Azure destiné à simplifier la gestion du cloud via l'automatisation des processus. Les tâches longues, manuelles, sujette aux erreurs et répétitives à l’aide d’Azure Automation, peuvent être automatisée tooincrease fiabilité, l’efficacité et toovalue de temps pour votre organisation.

Azure Automation fournit un moteur d’exécution de flux de travail hautement fiable et à haute disponibilité qui s’adapte toomeet vos besoins que votre organisation se développe. Dans Azure Automation, les processus peuvent être lancés manuellement, par des systèmes tiers ou à des intervalles planifiés, afin que les tâches interviennent exactement au moment opportun.

Réduire la surcharge opérationnelle et de libérer de l’informatique / toofocus du personnel DevOps sur le travail qui ajoute la valeur de l’entreprise en déplaçant votre toobe de tâches de gestion de cloud exécutés automatiquement par Azure Automation.

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a>Comment Azure Automation peut-il aider à gérer des bases de données SQL Azure ?
Base de données SQL Azure peuvent être géré dans Azure Automation à l’aide de hello [applets de commande PowerShell de base de données SQL Azure](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) qui sont disponibles dans hello [outils Azure PowerShell](/powershell/azure/overview). Azure Automation dispose de ces applets de commande PowerShell de base de données SQL Azure disponibles en dehors de la zone de hello, afin que vous pouvez effectuer toutes vos tâches de gestion de base de données SQL dans le service de hello. Vous pouvez également de paires de ces applets de commande dans Azure Automation avec les applets de commande hello pour les autres services Azure, les tooautomate des tâches complexes entre des services Azure et les systèmes tiers 3e.

Azure Automation dispose également toocommunicate de capacité hello avec les serveurs SQL directement, en émettant des commandes SQL à l’aide de PowerShell.

Hello [galerie de runbooks Azure Automation](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contient une série de produit Communauté et l’équipe runbooks tooget démarré l’automatisation de la gestion de bases de données SQL Azure, les autres services Azure et 3e systèmes tiers. La galerie de Runbooks inclut :

* [Exécuter des requêtes SQL avec une base de données SQL Server](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [Mise à l’échelle verticale (haut ou bas) d’une base de données SQL Azure selon un programme planifié](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [Tronquer une table SQL si la base de données est proche de la taille maximale](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [Indexer les tables dans une base de données SQL Azure si elles sont très fragmentées](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello d’Azure Automation et comment il peut être des bases de données SQL Azure toomanage utilisé, suivez ces liens de toolearn plus sur Azure Automation.

* [Vue d’ensemble de Microsoft Azure Automation](../automation/automation-intro.md)
* [Mon premier Runbook](../automation/automation-first-runbook-graphical.md)
* [Plan d’apprentissage pour Azure Automation](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [Azure Automation : Votre Agent SQL Bonjour Cloud](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

