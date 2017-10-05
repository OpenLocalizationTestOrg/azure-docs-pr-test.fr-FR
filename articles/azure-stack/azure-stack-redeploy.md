---
title: "Redéployer Azure Stack | Microsoft Docs"
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
ms.openlocfilehash: 891cde9b16bbbb51729129b6ad7a0f3794307baa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="redeploy-azure-stack"></a><span data-ttu-id="8041a-103">Redéployer Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8041a-103">Redeploy Azure Stack</span></span>
<span data-ttu-id="8041a-104">Pour redéployer Azure Stack, vous devez recommencer à partir de zéro comme décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8041a-104">To redeploy Azure Stack, you must start over from scratch as described below.</span></span>

## <a name="steps-to-redeploy-azure-stack"></a><span data-ttu-id="8041a-105">Procédure de redéploiement d’Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8041a-105">Steps to redeploy Azure Stack</span></span>
1. <span data-ttu-id="8041a-106">Sur l’hôte du kit de développement, ouvrez une console PowerShell avec élévation de privilèges > accédez au script asdk-installer.ps1 > exécutez-le > cliquez sur **Redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="8041a-106">On the development kit host, open an elevated PowerShell console > navigate to the asdk-installer.ps1 script > run it > click **Reboot**.</span></span>
2. <span data-ttu-id="8041a-107">Sélectionnez le système d’exploitation de base (et non pas **Azure Stack**), puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="8041a-107">Select the base operating system (not **Azure Stack**) and click **Next**.</span></span>
3. <span data-ttu-id="8041a-108">Après le redémarrage de l’hôte du kit de développement, supprimez le fichier CloudBuilder.vhdx qui a été utilisé lors du déploiement précédent.</span><span class="sxs-lookup"><span data-stu-id="8041a-108">After the development kit host reboots, delete the CloudBuilder.vhdx file that was used as part of the previous deployment.</span></span>
4. <span data-ttu-id="8041a-109">[Déployer le kit de développement](azure-stack-run-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="8041a-109">[Deploy the development kit](azure-stack-run-powershell-script.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8041a-110">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8041a-110">Next steps</span></span>
[<span data-ttu-id="8041a-111">Se connecter à Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8041a-111">Connect to Azure Stack</span></span>](azure-stack-connect-azure-stack.md)

