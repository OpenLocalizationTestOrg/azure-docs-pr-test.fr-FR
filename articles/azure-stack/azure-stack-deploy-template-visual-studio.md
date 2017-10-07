---
title: "modèles d’aaaDeploy avec Visual Studio, dans la pile de Azure | Documents Microsoft"
description: "Découvrez comment les modèles toodeploy avec Visual Studio, dans la pile de Azure."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 628da2ae-64cc-42e0-b8b7-a6a3724cb974
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: aea917b585a30ef4fbe7263db66f0659b56b21bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-templates-in-azure-stack-using-visual-studio"></a>Déploiement de modèles dans Azure Stack à l’aide de Visual Studio

Utilisez le kit de développement Visual Studio toodeploy Azure Resource Manager modèles toohello pile d’Azure.

1. [Installer et connecter](azure-stack-install-visual-studio.md) tooAzure pile avec Visual Studio.
2. Ouvrez Visual Studio.
3. Cliquez sur **fichier**, cliquez sur **nouveau**et Bonjour **nouveau projet** boîte dialogue, cliquez sur **groupe de ressources Azure**.
4. Entrez un **nom** pour hello nouveau projet, puis cliquez sur **OK**.
5. Bonjour **sélectionner un modèle Azure** boîte de dialogue, modification hello *afficher les modèles de cet emplacement* déroulante trop**démarrage rapide de pile Azure**
6. Cliquez sur **101-create-storage-account**, puis cliquez sur **OK**.  
7. Dans le nouveau projet, vous pouvez voir une liste des modèles de hello disponibles en développant hello **modèles** nœud Bonjour **l’Explorateur de solutions** volet.
8. Bonjour **l’Explorateur de solutions** volet, avec le bouton hello nom de votre projet, cliquez sur **déployer**, puis cliquez sur **nouveau déploiement**.
9. Bonjour **déployer tooResource groupe** la boîte de dialogue hello **abonnement** liste déroulante, sélectionnez votre abonnement Microsoft Azure pile.
10. Bonjour **groupe de ressources** liste, choisissez un groupe de ressources existant ou créez-en un.
11. Bonjour **emplacement du groupe de ressources** liste, choisissez un emplacement, puis cliquez sur **déployer**.
12. Bonjour **modifier les paramètres** boîte de dialogue, entrez des valeurs pour les paramètres hello (qui varient selon le modèle), puis cliquez sur **enregistrer**.

## <a name="next-steps"></a>Étapes suivantes
[Déployer des modèles de ligne de commande hello](azure-stack-deploy-template-command-line.md)

[Développer des modèles pour Azure Stack](azure-stack-develop-templates.md)

