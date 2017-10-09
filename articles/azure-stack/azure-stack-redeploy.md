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
# <a name="redeploy-azure-stack"></a><span data-ttu-id="29221-103">Redéployer Azure Stack</span><span class="sxs-lookup"><span data-stu-id="29221-103">Redeploy Azure Stack</span></span>
<span data-ttu-id="29221-104">tooredeploy pile d’Azure, vous devez démarrer sur à partir de zéro comme décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="29221-104">tooredeploy Azure Stack, you must start over from scratch as described below.</span></span>

## <a name="steps-tooredeploy-azure-stack"></a><span data-ttu-id="29221-105">Étapes tooredeploy pile d’Azure</span><span class="sxs-lookup"><span data-stu-id="29221-105">Steps tooredeploy Azure Stack</span></span>
1. <span data-ttu-id="29221-106">Sur l’hôte du kit de développement de hello, ouvrez une console PowerShell avec élévation de privilèges > accédez toohello asdk-installer.ps1 script > Exécuter > cliquez sur **redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="29221-106">On hello development kit host, open an elevated PowerShell console > navigate toohello asdk-installer.ps1 script > run it > click **Reboot**.</span></span>
2. <span data-ttu-id="29221-107">Sélectionnez hello de base du système d’exploitation (pas **Azure pile**) et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="29221-107">Select hello base operating system (not **Azure Stack**) and click **Next**.</span></span>
3. <span data-ttu-id="29221-108">Après le redémarrage de l’hôte de kit de développement hello, supprimez-le hello CloudBuilder.vhdx qui a été utilisé dans le cadre du déploiement précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="29221-108">After hello development kit host reboots, delete hello CloudBuilder.vhdx file that was used as part of hello previous deployment.</span></span>
4. <span data-ttu-id="29221-109">[Déployer le kit de développement hello](azure-stack-run-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="29221-109">[Deploy hello development kit](azure-stack-run-powershell-script.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="29221-110">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="29221-110">Next steps</span></span>
[<span data-ttu-id="29221-111">Se connecter tooAzure pile</span><span class="sxs-lookup"><span data-stu-id="29221-111">Connect tooAzure Stack</span></span>](azure-stack-connect-azure-stack.md)

