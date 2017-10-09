---
title: aaaRedeploy Azure pile | Documents Microsoft
description: "Redéployer Azure Stack."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 795af5ea-892d-40b1-a080-42e4472e4bba
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: erikje
ms.openlocfilehash: ec26745bcb54edd7c26960eec55d41504aff1911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-azure-stack"></a>Redéployer Azure Stack
tooredeploy pile d’Azure, vous devez démarrer sur à partir de zéro comme décrit ci-dessous.

## <a name="steps-tooredeploy-azure-stack"></a>Étapes tooredeploy pile d’Azure
1. Sur l’hôte du kit de développement de hello, ouvrez une console PowerShell avec élévation de privilèges > accédez toohello asdk-installer.ps1 script > Exécuter > cliquez sur **redémarrer**.
2. Sélectionnez hello de base du système d’exploitation (pas **Azure pile**) et cliquez sur **suivant**.
3. Après le redémarrage de l’hôte de kit de développement hello, supprimez-le hello CloudBuilder.vhdx qui a été utilisé dans le cadre du déploiement précédent de hello.
4. [Déployer le kit de développement hello](azure-stack-run-powershell-script.md).

## <a name="next-steps"></a>Étapes suivantes
[Se connecter tooAzure pile](azure-stack-connect-azure-stack.md)

