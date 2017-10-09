---
title: "aaaManage Azure Key Vault à l’aide d’Azure Automation | Documents Microsoft"
description: "Découvrez comment hello service Azure Automation peut être utilisé toomanage Azure Key Vault."
services: Key-Vault, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 4e780762-19b6-4ca6-b894-ebb44c538f35
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: 7f46ecc1206a96e8aeb1d086285461cb5b205472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a>Gestion d'Azure Key Vault avec Azure Automation
Ce guide vous oblige à service d’Azure Automation toohello et comment il peut être gestion toosimplify utilisés de vos clés et les clés secrètes dans le coffre de clés Azure.

## <a name="what-is-azure-automation"></a>Qu'est-ce qu'Azure Automation ?
[Azure Automation](../automation/automation-intro.md) est un service Azure destiné à simplifier la gestion du cloud via l'automatisation des processus et la configuration de l’état souhaité. Les tâches manuelles, répétées, longue et sujettes aux erreurs à l’aide d’Azure Automation, peuvent être automatisée tooincrease fiabilité, l’efficacité et toovalue de temps pour votre organisation.

Azure Automation fournit un moteur d’exécution de flux de travail hautement fiable et à haute disponibilité qui s’adapte toomeet à vos besoins. Dans Azure Automation, les processus peuvent être lancés manuellement, par des systèmes tiers ou à des intervalles planifiés, afin que les tâches interviennent exactement au moment opportun.

Réduire la surcharge opérationnelle et de libérer de l’informatique et toofocus du personnel DevOps sur le travail qui ajoute la valeur de l’entreprise en déplaçant votre toobe de tâches de gestion de cloud exécuté automatiquement par Azure Automation.

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a>Comment Azure Automation peut-il aider à gérer Azure Key Vault ?
Le coffre de clés peuvent être géré dans Azure Automation à l’aide de hello [applets de commande de coffre de clés Azure Resource Manager](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) et [applets de commande de coffre de clés Azure Classic](https://msdn.microsoft.com/library/azure/dn868052.aspx). Hello module Azure pour gérer le coffre de clés classique est disponible automatiquement dans Azure Automation, et vous pouvez importer hello [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) dans Azure Automation, afin que vous pouvez effectuer un grand nombre de gestion de votre coffre de clés tâches au sein du service de hello. Vous pouvez également de paires de ces applets de commande dans Azure Automation avec les applets de commande hello pour les autres services Azure, les tooautomate des tâches complexes entre des services Azure et les systèmes tiers 3e.

Avec les applets de commande Azure Key Vault hello, vous pouvez effectuer ces tâches, entre autres : 

* Création et configuration d’un coffre de clés
* Création ou importation d’une clé
* Création ou mise à jour d’une clé secrète
* Mise à jour des attributs d’une clé
* Obtention d’une clé ou d’une clé secrète
* Suppression d’une clé ou d’une clé secrète

Voici quelques exemples d’utilisation de PowerShell toomanage le coffre de clés :  

* [Azure Key Vault – Étape par étape](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [Setting Up and Configuring an Azure Key Vault (Installation et configuration d’Azure Key Vault)](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello d’Azure Automation et comment il peut être utilisé toomanage coffre de clés Azure, suivez ces liens de toolearn plus sur Azure Automation.

* Consultez hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).
* Consultez hello [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).

