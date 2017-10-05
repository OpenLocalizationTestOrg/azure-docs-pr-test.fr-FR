---
title: "Déployer des modèles avec le portail dans Azure Stack | Microsoft Docs"
description: "Apprenez à utiliser le portail Azure Stack pour déployer des modèles."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: eafa60f2-16c9-4ef1-b724-47709e9ea29e
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: eb6e67dc4707b2b999efcceec1c55dc950c5996e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-templates-using-the-azure-stack-portal"></a>Déployer des modèles à l’aide du portail Azure Stack
Utilisez le portail pour déployer des modèles Azure Resource Manager dans le kit de développement Azure Stack.

Les modèles Resource Manager déploient et approvisionnent toutes les ressources de l’application en une seule opération coordonnée.

1. Connectez-vous au portail, cliquez sur **Nouveau**, **Personnalisé**, puis **Déploiement du modèle**.
2. Cliquez sur **Modifier un modèle**, puis collez le code de votre modèle JSON sur le panneau et cliquez sur **Enregistrer**.
3. Cliquez sur **Modifier les paramètres**, tapez des valeurs pour les paramètres listés, puis cliquez sur **OK**.
4. Cliquez sur **Abonnement**, choisissez l’abonnement que vous souhaitez utiliser, puis cliquez sur **OK**.
5. Cliquez sur **Groupe de ressources**, choisissez un groupe de ressources existant ou créez-en un, puis cliquez sur **OK**.
6. Cliquez sur **Créer**. Le tableau de bord contient maintenant une nouvelle vignette qui suit la progression du déploiement de votre modèle.

## <a name="next-steps"></a>Étapes suivantes
[Déployer des modèles avec PowerShell](azure-stack-deploy-template-powershell.md)

