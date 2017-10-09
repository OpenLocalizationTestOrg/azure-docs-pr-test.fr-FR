---
title: aaaInstall Symantec Endpoint Protection sur un ordinateur virtuel Windows Azure | Documents Microsoft
description: "Découvrez comment tooinstall et configurer l’extension de sécurité hello Symantec Endpoint Protection sur un nouveau ou machine virtuelle Azure existante créée avec le modèle de déploiement classique hello."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 19dcebc7-da6b-4510-907b-d64088e81fa2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: iainfou
ms.openlocfilehash: cb6083366185c26c9f43ff94d835cd90725de5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a><span data-ttu-id="eb51d-103">Comment tooinstall et configurer Symantec Endpoint Protection sur une machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="eb51d-103">How tooinstall and configure Symantec Endpoint Protection on a Windows VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="eb51d-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="eb51d-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="eb51d-105">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="eb51d-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="eb51d-106">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="eb51d-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="eb51d-107">Cet article vous montre comment tooinstall et configurer le client de Symantec Endpoint Protection hello sur un ordinateur virtuel existant (VM) exécutant Windows Server.</span><span class="sxs-lookup"><span data-stu-id="eb51d-107">This article shows you how tooinstall and configure hello Symantec Endpoint Protection client on an existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="eb51d-108">Le client complet inclut des services tels qu’une protection antivirus et anti-programmes espions, un pare-feu et une prévention contre les intrusions.</span><span class="sxs-lookup"><span data-stu-id="eb51d-108">This full client includes services such as virus and spyware protection, firewall, and intrusion prevention.</span></span> <span data-ttu-id="eb51d-109">client de Hello est installé comme une extension de sécurité à l’aide de hello Agent de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="eb51d-109">hello client is installed as a security extension by using hello VM Agent.</span></span>

<span data-ttu-id="eb51d-110">Si vous avez un abonnement auprès de Symantec pour une solution sur site, vous pouvez l’utiliser tooprotect vos machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="eb51d-110">If you have an existing subscription from Symantec for an on-premises solution, you can use it tooprotect your Azure virtual machines.</span></span> <span data-ttu-id="eb51d-111">Si vous n’êtes pas encore client, vous pouvez vous inscrire pour une version d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="eb51d-111">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="eb51d-112">Pour plus d’informations sur cette solution, consultez la rubrique [Symantec Endpoint Protection sur la plateforme Azure de Microsoft][Symantec].</span><span class="sxs-lookup"><span data-stu-id="eb51d-112">For more information about this solution, see [Symantec Endpoint Protection on Microsoft's Azure platform][Symantec].</span></span> <span data-ttu-id="eb51d-113">Cette page contient également des informations de toolicensing de liens et des instructions pour l’installation de client de hello si vous êtes déjà un client de Symantec.</span><span class="sxs-lookup"><span data-stu-id="eb51d-113">This page also has links toolicensing information and instructions for installing hello client if you're already a Symantec customer.</span></span>

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a><span data-ttu-id="eb51d-114">Installation de Symantec Endpoint Protection sur une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="eb51d-114">Install Symantec Endpoint Protection on an existing VM</span></span>
<span data-ttu-id="eb51d-115">Avant de commencer, vous devez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="eb51d-115">Before you begin, you need hello following:</span></span>

* <span data-ttu-id="eb51d-116">module d’Azure PowerShell Hello, version 0.8.2 ou version ultérieure, sur votre ordinateur de travail.</span><span class="sxs-lookup"><span data-stu-id="eb51d-116">hello Azure PowerShell module, version 0.8.2 or later, on your work computer.</span></span> <span data-ttu-id="eb51d-117">Vous pouvez vérifier la version de hello d’Azure PowerShell que vous avez installés avec hello **azure de Get-Module | version de format-table** commande.</span><span class="sxs-lookup"><span data-stu-id="eb51d-117">You can check hello version of Azure PowerShell that you have installed with hello **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="eb51d-118">Pour obtenir des instructions et une version plus récente de lien toohello, consultez [comment tooInstall et configurer Azure PowerShell][PS].</span><span class="sxs-lookup"><span data-stu-id="eb51d-118">For instructions and a link toohello latest version, see [How tooInstall and Configure Azure PowerShell][PS].</span></span> <span data-ttu-id="eb51d-119">Ouvrez une session à l’aide d’abonnement Azure tooyour `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="eb51d-119">Log in tooyour Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="eb51d-120">Hello Agent de machine virtuelle en cours d’exécution hello Machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="eb51d-120">hello VM Agent running on hello Azure Virtual Machine.</span></span>

<span data-ttu-id="eb51d-121">Tout d’abord, vérifiez que hello Qu'agent de machine virtuelle est déjà installé sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="eb51d-121">First, verify that hello VM Agent is already installed on hello virtual machine.</span></span> <span data-ttu-id="eb51d-122">Renseignez nom du service cloud hello et nom de machine virtuelle et exécutez hello suivant de commandes à partir d’une invite de commandes de niveau administrateur Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eb51d-122">Fill in hello cloud service name and virtual machine name, and then run hello following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="eb51d-123">Remplacez tout le contenu du devis hello, y compris hello < et >.</span><span class="sxs-lookup"><span data-stu-id="eb51d-123">Replace everything within hello quotes, including hello < and > characters.</span></span>

> [!TIP]
> <span data-ttu-id="eb51d-124">Si vous ne connaissez pas le service cloud hello et les noms des ordinateurs virtuels, exécutez **Get-AzureVM** noms de hello toolist pour tous les ordinateurs virtuels dans votre abonnement actuel.</span><span class="sxs-lookup"><span data-stu-id="eb51d-124">If you don't know hello cloud service and virtual machine names, run **Get-AzureVM** toolist hello names for all virtual machines in your current subscription.</span></span>

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="eb51d-125">Si hello **écriture-host** commande affiche **True**, hello l’Agent VM est installé.</span><span class="sxs-lookup"><span data-stu-id="eb51d-125">If hello **write-host** command displays **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="eb51d-126">S’il affiche **False**, consultez les instructions hello et un toohello lien Télécharger Bonjour billet de blog Azure [Agent de machine virtuelle et Extensions - partie 2][Agent].</span><span class="sxs-lookup"><span data-stu-id="eb51d-126">If it displays **False**, see hello instructions and a link toohello download in hello Azure blog post [VM Agent and Extensions - Part 2][Agent].</span></span>

<span data-ttu-id="eb51d-127">Si hello Agent de machine virtuelle est installé, exécutez ces agent Symantec Endpoint Protection de commandes tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="eb51d-127">If hello VM Agent is installed, run these commands tooinstall hello Symantec Endpoint Protection agent.</span></span>

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

<span data-ttu-id="eb51d-128">tooverify qui hello d’extension de sécurité Symantec a été installé et est à jour :</span><span class="sxs-lookup"><span data-stu-id="eb51d-128">tooverify that hello Symantec security extension has been installed and is up-to-date:</span></span>

1. <span data-ttu-id="eb51d-129">Ouvrez une session sur l’ordinateur virtuel de toohello.</span><span class="sxs-lookup"><span data-stu-id="eb51d-129">Log on toohello virtual machine.</span></span> <span data-ttu-id="eb51d-130">Pour obtenir des instructions, consultez [comment tooLog sur tooa Machine virtuelle exécutant Windows Server][Logon].</span><span class="sxs-lookup"><span data-stu-id="eb51d-130">For instructions, see [How tooLog on tooa Virtual Machine Running Windows Server][Logon].</span></span>
2. <span data-ttu-id="eb51d-131">Pour Windows Server 2008 R2, cliquez sur **Démarrer > Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="eb51d-131">For Windows Server 2008 R2, click **Start > Symantec Endpoint Protection**.</span></span> <span data-ttu-id="eb51d-132">Pour Windows Server 2012 ou Windows Server 2012 R2, à partir de l’écran d’accueil hello, tapez **Symantec**, puis cliquez sur **Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="eb51d-132">For Windows Server 2012 or Windows Server 2012 R2, from hello start screen, type **Symantec**, and then click **Symantec Endpoint Protection**.</span></span>
3. <span data-ttu-id="eb51d-133">À partir de hello **état** onglet Hello **état-Symantec Endpoint Protection** fenêtre, appliquer des mises à jour ou redémarrer si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="eb51d-133">From hello **Status** tab of hello **Status-Symantec Endpoint Protection** window, apply updates or restart if needed.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eb51d-134">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="eb51d-134">Additional resources</span></span>
<span data-ttu-id="eb51d-135">[Comment tooLog sur tooa Machine virtuelle exécutant Windows Server][Logon]</span><span class="sxs-lookup"><span data-stu-id="eb51d-135">[How tooLog on tooa Virtual Machine Running Windows Server][Logon]</span></span>

<span data-ttu-id="eb51d-136">[Fonctionnalités et extensions de machine virtuelle Azure][Ext]</span><span class="sxs-lookup"><span data-stu-id="eb51d-136">[Azure VM Extensions and Features][Ext]</span></span>

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
