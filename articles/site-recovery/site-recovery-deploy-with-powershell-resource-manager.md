---
title: aaaReplicate machines virtuelles de Hyper-V avec PowerShell et le Gestionnaire de ressources Azure | Documents Microsoft
description: "Automatiser la réplication des ordinateurs virtuels Hyper-V tooAzure hello avec Azure Site Recovery à l’aide de PowerShell et le Gestionnaire de ressources Azure."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: 
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: 4fb15ce2e9ad54f1dd6f54ff769eb912aa4b0272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="999f6-103">Réplication de machines virtuelles Hyper-V en local dans Azure avec PowerShell et Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="999f6-103">Replicate between on-premises Hyper-V virtual machines and Azure by using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="999f6-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="999f6-104">Azure Portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="999f6-105">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="999f6-105">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
> * [<span data-ttu-id="999f6-106">Portail Classic</span><span class="sxs-lookup"><span data-stu-id="999f6-106">Classic Portal</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a><span data-ttu-id="999f6-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="999f6-107">Overview</span></span>
<span data-ttu-id="999f6-108">Azure Site Recovery contribue stratégie récupération tooyour commerciale la continuité des activités et d’urgence en coordonnant la réplication, le basculement et récupération des machines virtuelles dans un nombre de scénarios de déploiement.</span><span class="sxs-lookup"><span data-stu-id="999f6-108">Azure Site Recovery contributes tooyour business continuity and disaster recovery strategy by orchestrating replication, failover, and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="999f6-109">Pour obtenir une liste complète des scénarios de déploiement, consultez hello [vue d’ensemble d’Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="999f6-109">For a full list of deployment scenarios, see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="999f6-110">Azure PowerShell est un module qui fournit des applets de commande toomanage Azure via Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="999f6-110">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="999f6-111">Il peut fonctionner avec deux types de modules : hello module de profil Azure, ou le module de gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="999f6-111">It can work with two types of modules: hello Azure Profile module, or hello Azure Resource Manager module.</span></span>

<span data-ttu-id="999f6-112">Les applets de commande PowerShell de Site Recovery, disponibles avec Azure PowerShell pour Azure Resource Manager, vous permettent de protéger et récupérer vos serveurs dans Azure.</span><span class="sxs-lookup"><span data-stu-id="999f6-112">Site Recovery PowerShell cmdlets, available with Azure PowerShell for Azure Resource Manager, help you protect and recover your servers in Azure.</span></span>

<span data-ttu-id="999f6-113">Cet article décrit comment toouse Windows PowerShell, avec Azure Resource Manager toodeploy Site Recovery tooconfigure et orchestrer tooAzure de protection de serveur.</span><span class="sxs-lookup"><span data-stu-id="999f6-113">This article describes how toouse Windows PowerShell, together with Azure Resource Manager, toodeploy Site Recovery tooconfigure and orchestrate server protection tooAzure.</span></span> <span data-ttu-id="999f6-114">exemple Hello utilisée dans cet article vous montre comment tooprotect, basculer et récupérer des ordinateurs virtuels sur un tooAzure hôte Hyper-V, à l’aide d’Azure PowerShell avec Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="999f6-114">hello example used in this article shows you how tooprotect, fail over, and recover virtual machines on a Hyper-V host tooAzure, by using Azure PowerShell with Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="999f6-115">Hello applets de commande PowerShell de récupération de Site actuellement permettent de hello tooconfigure suivant : un tooanother de site de Virtual Machine Manager, un tooAzure de site de Virtual Machine Manager et un tooAzure de site Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="999f6-115">hello Site Recovery PowerShell cmdlets currently allow you tooconfigure hello following: one Virtual Machine Manager site tooanother, a Virtual Machine Manager site tooAzure, and a Hyper-V site tooAzure.</span></span>
>
>

<span data-ttu-id="999f6-116">Vous n’avez pas besoin toobe un toouse expert PowerShell cet article, mais vous n’avez pas besoin de toounderstand hello concepts de base, tels que des modules, applets de commande et des sessions.</span><span class="sxs-lookup"><span data-stu-id="999f6-116">You don't need toobe a PowerShell expert toouse this article, but you do need toounderstand hello basic concepts, such as modules, cmdlets, and sessions.</span></span> <span data-ttu-id="999f6-117">Pour plus d'informations sur Windows PowerShell, consultez la page [Prise en main de Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span><span class="sxs-lookup"><span data-stu-id="999f6-117">For more information about Windows PowerShell, see [Getting Started with Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="999f6-118">Vous pouvez également lire l’article [Utilisation d’Azure PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md)pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="999f6-118">You can also read more about [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

> [!NOTE]
> <span data-ttu-id="999f6-119">Les partenaires Microsoft qui font partie du programme de fournisseur de solutions de Cloud (CSP) hello peuvent configurer et gérer la protection des serveurs de leurs clients respectifs CSP abonnements (client) tootheir clients.</span><span class="sxs-lookup"><span data-stu-id="999f6-119">Microsoft partners that are part of hello Cloud Solution Provider (CSP) program can configure and manage protection of their customers' servers tootheir customers' respective CSP subscriptions (tenant subscriptions).</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="999f6-120">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="999f6-120">Before you start</span></span>
<span data-ttu-id="999f6-121">Assurez-vous que les conditions préalables sont remplies :</span><span class="sxs-lookup"><span data-stu-id="999f6-121">Make sure you have these prerequisites in place:</span></span>

* <span data-ttu-id="999f6-122">Un compte [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="999f6-122">A [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="999f6-123">Vous pouvez commencer avec une [version d'évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="999f6-123">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="999f6-124">Vous pouvez aussi consulter la [Tarification Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="999f6-124">In addition, you can read about [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="999f6-125">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="999f6-125">Azure PowerShell 1.0.</span></span> <span data-ttu-id="999f6-126">Pour plus d’informations sur cette version et comment tooinstall, consultez [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="999f6-126">For information about this release and how tooinstall it, see [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span></span>
* <span data-ttu-id="999f6-127">Hello [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) et [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules.</span><span class="sxs-lookup"><span data-stu-id="999f6-127">hello [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) and [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules.</span></span> <span data-ttu-id="999f6-128">Vous pouvez obtenir les versions les plus récentes de ces modules hello de hello [galerie PowerShell](https://www.powershellgallery.com/)</span><span class="sxs-lookup"><span data-stu-id="999f6-128">You can get hello latest versions of these modules from hello [PowerShell gallery](https://www.powershellgallery.com/)</span></span>

<span data-ttu-id="999f6-129">Cet article explique comment toouse Azure Powershell avec Azure Resource Manager tooconfigure et gérer la protection de vos serveurs.</span><span class="sxs-lookup"><span data-stu-id="999f6-129">This article illustrates how toouse Azure Powershell with Azure Resource Manager tooconfigure and manage protection of your servers.</span></span> <span data-ttu-id="999f6-130">exemple Hello utilisée dans cet article vous montre comment tooprotect une machine virtuelle, en cours d’exécution sur un ordinateur hôte Hyper-V, tooAzure.</span><span class="sxs-lookup"><span data-stu-id="999f6-130">hello example used in this article shows you how tooprotect a virtual machine, running on a Hyper-V host, tooAzure.</span></span> <span data-ttu-id="999f6-131">Hello, suivant les conditions préalables est des exemples de toothis spécifique.</span><span class="sxs-lookup"><span data-stu-id="999f6-131">hello following prerequisites are specific toothis example.</span></span> <span data-ttu-id="999f6-132">Pour un ensemble plus complet de la configuration requise pour hello différents scénarios de récupération de Site, consultez la documentation de toohello se rapportant toothat scénario.</span><span class="sxs-lookup"><span data-stu-id="999f6-132">For a more comprehensive set of requirements for hello various Site Recovery scenarios, refer toohello documentation pertaining toothat scenario.</span></span>

* <span data-ttu-id="999f6-133">Un hôte Hyper-V exécuté sous Windows Server 2012 R2 ou Microsoft Hyper-V Server 2012 R2 et hébergeant une ou plusieurs machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="999f6-133">A Hyper-V host running Windows Server 2012 R2 or Microsoft Hyper-V Server 2012 R2 containing one or more virtual machines.</span></span>
* <span data-ttu-id="999f6-134">Serveurs Hyper-V connecté toohello Internet, directement ou via un proxy.</span><span class="sxs-lookup"><span data-stu-id="999f6-134">Hyper-V servers connected toohello Internet, either directly or through a proxy.</span></span>
* <span data-ttu-id="999f6-135">Hello machines virtuelles tooprotect doivent respecter les [conditions préalables requises de l’ordinateur virtuel](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="999f6-135">hello virtual machines you want tooprotect should conform with [Virtual Machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

## <a name="step-1-sign-in-tooyour-azure-account"></a><span data-ttu-id="999f6-136">Étape 1 : Se connecter tooyour compte Azure</span><span class="sxs-lookup"><span data-stu-id="999f6-136">Step 1: Sign in tooyour Azure account</span></span>
1. <span data-ttu-id="999f6-137">Ouvrez une console PowerShell et exécuter cette commande toosign dans tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="999f6-137">Open a PowerShell console and run this command toosign in tooyour Azure account.</span></span> <span data-ttu-id="999f6-138">applet de commande Hello affiche une page web qui vous demande vos informations d’identification de compte.</span><span class="sxs-lookup"><span data-stu-id="999f6-138">hello cmdlet brings up a web page that will prompt you for your account credentials.</span></span>

        Login-AzureRmAccount

    <span data-ttu-id="999f6-139">Ou bien, vous pouvez également inclure vos informations d’identification de compte comme un paramètre toohello `Login-AzureRmAccount` applet de commande, à l’aide de hello `-Credential` paramètre.</span><span class="sxs-lookup"><span data-stu-id="999f6-139">Alternately, you could also include your account credentials as a parameter toohello `Login-AzureRmAccount` cmdlet, by using hello `-Credential` parameter.</span></span>

    <span data-ttu-id="999f6-140">Si vous êtes CSP fonctionne pour le compte d’un client, spécifiez les clients hello en tant que client, à l’aide de leur nom de domaine principal tenantID ou locataire.</span><span class="sxs-lookup"><span data-stu-id="999f6-140">If you are CSP partner working on behalf of a tenant, specify hello customer as a tenant, by using their tenantID or tenant primary domain name.</span></span>

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. <span data-ttu-id="999f6-141">Un compte peut avoir plusieurs abonnements, donc vous devez associer abonnement hello toouse avec un compte de hello.</span><span class="sxs-lookup"><span data-stu-id="999f6-141">An account can have several subscriptions, so you should associate hello subscription you want toouse with hello account.</span></span>

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. <span data-ttu-id="999f6-142">Vérifiez que votre abonnement est inscrit toouse hello Azure fournisseurs de Services de récupération et la récupération de Site, à l’aide de hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="999f6-142">Verify that your subscription is registered toouse hello Azure providers for Recovery Services and Site Recovery, by using hello following commands:</span></span>

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   <span data-ttu-id="999f6-143">Dans la sortie de hello de ces commandes, si hello **RegistrationState** est défini trop**inscrit**, vous pouvez passer tooStep 2.</span><span class="sxs-lookup"><span data-stu-id="999f6-143">In hello output of these commands, if hello **RegistrationState** is set too**Registered**, you can proceed tooStep 2.</span></span> <span data-ttu-id="999f6-144">Si ce n’est pas le cas, vous devez inscrire le fournisseur de hello manquant dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="999f6-144">If not, you should register hello missing provider in your subscription.</span></span>

   <span data-ttu-id="999f6-145">hello tooregister fournisseur Azure Site Recovery Services et de récupération, exécutez hello suivant les commandes :</span><span class="sxs-lookup"><span data-stu-id="999f6-145">tooregister hello Azure provider for Site Recovery and Recovery Services, run hello following commands:</span></span>

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   <span data-ttu-id="999f6-146">Vérifiez que les fournisseurs hello a été correctement inscrit à l’aide de hello suivant de commandes : `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` et `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span><span class="sxs-lookup"><span data-stu-id="999f6-146">Verify that hello providers registered successfully by using hello following commands: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` and `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span></span>

## <a name="step-2-set-up-hello-recovery-services-vault"></a><span data-ttu-id="999f6-147">Étape 2 : Configurer hello de coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="999f6-147">Step 2: Set up hello Recovery Services vault</span></span>
1. <span data-ttu-id="999f6-148">Créer un groupe de ressources Azure Resource Manager, dans lequel vous allez créer hello coffre, ou utiliser un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="999f6-148">Create an Azure Resource Manager resource group in which you'll create hello vault, or use an existing resource group.</span></span> <span data-ttu-id="999f6-149">Vous pouvez créer un nouveau groupe de ressources à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="999f6-149">You can create a new resource group by using hello following command:</span></span>

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    <span data-ttu-id="999f6-150">Lorsque la variable de hello $ResourceGroupName contient le nom hello hello du groupe de ressources et vous souhaitez toocreate variable de hello $Geo contient hello Azure région dans le groupe de ressources hello toocreate (par exemple, « Brésil Sud »).</span><span class="sxs-lookup"><span data-stu-id="999f6-150">where hello $ResourceGroupName variable contains hello name of hello resource group you want toocreate, and hello $Geo variable contains hello Azure region in which toocreate hello resource group (for example, "Brazil South").</span></span>

    <span data-ttu-id="999f6-151">Vous pouvez obtenir une liste des groupes de ressources dans votre abonnement à l’aide de hello `Get-AzureRmResourceGroup` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="999f6-151">You can obtain a list of resource groups in your subscription by using hello `Get-AzureRmResourceGroup` cmdlet.</span></span>
2. <span data-ttu-id="999f6-152">Créez un coffre Azure Recovery Services de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="999f6-152">Create a new Azure Recovery Services vault as follows:</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    <span data-ttu-id="999f6-153">Vous pouvez récupérer une liste des archivages existants à l’aide de hello `Get-AzureRmRecoveryServicesVault` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="999f6-153">You can retrieve a list of existing vaults by using hello `Get-AzureRmRecoveryServicesVault` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="999f6-154">Si vous souhaitez tooperform les opérations sur des coffres de récupération de Site créées à l’aide du portail classique de hello ou un module PowerShell Azure Service Management de hello, vous pouvez récupérer une liste de ces coffres à l’aide de hello `Get-AzureRmSiteRecoveryVault` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="999f6-154">If you wish tooperform operations on Site Recovery vaults created using hello classic portal or hello Azure Service Management PowerShell module, you can retrieve a list of such vaults by using hello `Get-AzureRmSiteRecoveryVault` cmdlet.</span></span> <span data-ttu-id="999f6-155">Il est recommandé de créer un coffre Recovery Services pour toutes les nouvelles opérations.</span><span class="sxs-lookup"><span data-stu-id="999f6-155">You should create a new Recovery Services vault for all new operations.</span></span> <span data-ttu-id="999f6-156">les coffres de récupération de Site Hello que vous avez créé précédemment sont pris en charge, mais n’ont pas les fonctionnalités plus récentes hello.</span><span class="sxs-lookup"><span data-stu-id="999f6-156">hello Site Recovery vaults you've created earlier are supported, but don't have hello latest features.</span></span>
>
>

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="999f6-157">Étape 3 : Configurer les Services de récupération hello coffre contexte</span><span class="sxs-lookup"><span data-stu-id="999f6-157">Step 3: Set hello Recovery Services vault context</span></span>
1. <span data-ttu-id="999f6-158">Définir le contexte de coffre hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="999f6-158">Set hello vault context by running hello following command:</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-hello-site"></a><span data-ttu-id="999f6-159">Étape 4 : Créer un site Hyper-V et générer une nouvelle clé d’inscription de coffre pour le site de hello.</span><span class="sxs-lookup"><span data-stu-id="999f6-159">Step 4: Create a Hyper-V site and generate a new vault registration key for hello site.</span></span>
1. <span data-ttu-id="999f6-160">Créez un nouveau site Hyper-V comme suit :</span><span class="sxs-lookup"><span data-stu-id="999f6-160">Create a new Hyper-V site as follows:</span></span>

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    <span data-ttu-id="999f6-161">Cette applet de commande démarre un site de récupération de Site travail toocreate hello et retourne un objet de tâche de récupération de Site.</span><span class="sxs-lookup"><span data-stu-id="999f6-161">This cmdlet starts a Site Recovery job toocreate hello site, and returns a Site Recovery job object.</span></span> <span data-ttu-id="999f6-162">Attendre hello travail toocomplete et vérifiez que le travail hello est terminée avec succès.</span><span class="sxs-lookup"><span data-stu-id="999f6-162">Wait for hello job toocomplete and verify that hello job completed successfully.</span></span>

    <span data-ttu-id="999f6-163">Vous pouvez récupérer l’objet de tâche hello et ainsi vérifier état actuel de hello hello du travail de, à l’aide d’applet de commande Get-AzureRmSiteRecoveryJob de hello.</span><span class="sxs-lookup"><span data-stu-id="999f6-163">You can retrieve hello job object, and thereby check hello current status of hello job, by using hello Get-AzureRmSiteRecoveryJob cmdlet.</span></span>
2. <span data-ttu-id="999f6-164">Générez et téléchargez une clé d’inscription pour le site de hello, comme suit :</span><span class="sxs-lookup"><span data-stu-id="999f6-164">Generate and download a registration key for hello site, as follows:</span></span>

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    <span data-ttu-id="999f6-165">Hello de copie téléchargé hôte de la clé toohello Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="999f6-165">Copy hello downloaded key toohello Hyper-V host.</span></span> <span data-ttu-id="999f6-166">Vous devez le site toohello hôte hello tooregister clé hello Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="999f6-166">You need hello key tooregister hello Hyper-V host toohello site.</span></span>

## <a name="step-5-install-hello-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a><span data-ttu-id="999f6-167">Étape 5 : Installer le fournisseur Azure Site Recovery hello et Azure Recovery Services Agent sur votre hôte Hyper-V</span><span class="sxs-lookup"><span data-stu-id="999f6-167">Step 5: Install hello Azure Site Recovery provider and Azure Recovery Services Agent on your Hyper-V host</span></span>
1. <span data-ttu-id="999f6-168">Télécharger installer hello pour la version la plus récente du fournisseur hello dans hello [Microsoft](https://aka.ms/downloaddra).</span><span class="sxs-lookup"><span data-stu-id="999f6-168">Download hello installer for hello latest version of hello provider from [Microsoft](https://aka.ms/downloaddra).</span></span>
2. <span data-ttu-id="999f6-169">Programme d’installation de l’exécution hello sur votre ordinateur hôte Hyper-V et à fin hello d’installation de hello continuer étape d’inscription de toohello.</span><span class="sxs-lookup"><span data-stu-id="999f6-169">Run hello installer on your Hyper-V host, and at hello end of hello installation continue toohello registration step.</span></span>
3. <span data-ttu-id="999f6-170">Lorsque vous y êtes invité, fournissez hello téléchargé la clé d’inscription de site et de terminer l’inscription du site de toohello hôte hello Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="999f6-170">When prompted, provide hello downloaded site registration key, and complete registration of hello Hyper-V host toohello site.</span></span>
4. <span data-ttu-id="999f6-171">Vérifiez que cet ordinateur hôte Hyper-V de hello est toohello inscrits à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="999f6-171">Verify that hello Hyper-V host is registered toohello site by using hello following command:</span></span>

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-hello-protection-container"></a><span data-ttu-id="999f6-172">Étape 6 : Créer une stratégie de réplication et associez-la à un conteneur de protection de hello</span><span class="sxs-lookup"><span data-stu-id="999f6-172">Step 6: Create a replication policy and associate it with hello protection container</span></span>
1. <span data-ttu-id="999f6-173">Créez une stratégie de réplication comme suit :</span><span class="sxs-lookup"><span data-stu-id="999f6-173">Create a replication policy as follows:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    <span data-ttu-id="999f6-174">Bonjour à cocher retourné tooensure de travail Création de la stratégie de réplication hello réussit.</span><span class="sxs-lookup"><span data-stu-id="999f6-174">Check hello returned job tooensure that hello replication policy creation succeeds.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="999f6-175">Hello compte de stockage spécifié doit être dans hello même région Azure que votre coffre Recovery Services, ainsi que la géo-réplication activée.</span><span class="sxs-lookup"><span data-stu-id="999f6-175">hello storage account specified should be in hello same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="999f6-176">Si hello spécifié de récupération de compte de stockage est de type de stockage de Azure (classique), basculement Hello protégé machines recover hello machine tooAzure IaaS (classique).</span><span class="sxs-lookup"><span data-stu-id="999f6-176">If hello specified Recovery storage account is of type Azure Storage (Classic), failover of hello protected machines recover hello machine tooAzure IaaS (Classic).</span></span>
   > * <span data-ttu-id="999f6-177">Si hello spécifié le compte de stockage de récupération est de type de stockage de Azure (Azure Resource Manager), basculement Hello protégé machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="999f6-177">If hello specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of hello protected machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span></span>
   >
   >
2. <span data-ttu-id="999f6-178">Obtenir hello protection conteneur toohello site correspondant, comme suit :</span><span class="sxs-lookup"><span data-stu-id="999f6-178">Get hello protection container corresponding toohello site, as follows:</span></span>

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. <span data-ttu-id="999f6-179">Démarrez association hello du conteneur de protection hello avec la stratégie de réplication hello, comme suit :</span><span class="sxs-lookup"><span data-stu-id="999f6-179">Start hello association of hello protection container with hello replication policy, as follows:</span></span>

     <span data-ttu-id="999f6-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span><span class="sxs-lookup"><span data-stu-id="999f6-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span></span>

   <span data-ttu-id="999f6-181">Attendez hello association tâche toocomplete et vérifiez qu’il s’est terminée avec succès.</span><span class="sxs-lookup"><span data-stu-id="999f6-181">Wait for hello association job toocomplete, and ensure that it completed successfully.</span></span>

## <a name="step-7-enable-protection-for-virtual-machines"></a><span data-ttu-id="999f6-182">Étape 7 : Activation de la protection des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="999f6-182">Step 7: Enable protection for virtual machines</span></span>
1. <span data-ttu-id="999f6-183">Obtenir hello protection entité correspondante toohello machine virtuelle tooprotect, comme suit :</span><span class="sxs-lookup"><span data-stu-id="999f6-183">Get hello protection entity corresponding toohello VM you want tooprotect, as follows:</span></span>

        $VMFriendlyName = "Fabrikam-app"                    #Name of hello VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. <span data-ttu-id="999f6-184">Démarrer la protection de machine virtuelle de hello, comme suit :</span><span class="sxs-lookup"><span data-stu-id="999f6-184">Start protecting hello virtual machine, as follows:</span></span>

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > <span data-ttu-id="999f6-185">Hello compte de stockage spécifié doit être dans hello même région Azure que votre coffre Recovery Services, ainsi que la géo-réplication activée.</span><span class="sxs-lookup"><span data-stu-id="999f6-185">hello storage account specified should be in hello same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="999f6-186">Si hello spécifié de récupération de compte de stockage est de type de stockage de Azure (classique), basculement Hello protégé machines recover hello machine tooAzure IaaS (classique).</span><span class="sxs-lookup"><span data-stu-id="999f6-186">If hello specified Recovery storage account is of type Azure Storage (Classic), failover of hello protected machines recover hello machine tooAzure IaaS (Classic).</span></span>
   > * <span data-ttu-id="999f6-187">Si hello spécifié le compte de stockage de récupération est de type de stockage de Azure (Azure Resource Manager), basculement Hello protégé machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="999f6-187">If hello specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of hello protected machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span></span>
   >
   > <span data-ttu-id="999f6-188">Si hello machine virtuelle que vous protégez comporte plus d’un disque attaché tooit, spécifiez le disque du système d’exploitation hello à l’aide de hello *OSDiskName* paramètre.</span><span class="sxs-lookup"><span data-stu-id="999f6-188">If hello VM you are protecting has more than one disk attached tooit, specify hello operating system disk by using hello *OSDiskName* parameter.</span></span>
   >
   >
3. <span data-ttu-id="999f6-189">Attendez que hello machines virtuelles tooreach un état de protection après la réplication initiale de hello.</span><span class="sxs-lookup"><span data-stu-id="999f6-189">Wait for hello virtual machines tooreach a protected state after hello initial replication.</span></span> <span data-ttu-id="999f6-190">Cela peut prendre un certain temps, en fonction de facteurs tels que la quantité de hello de toobe de données répliquée et hello tooAzure de la bande passante disponible en amont.</span><span class="sxs-lookup"><span data-stu-id="999f6-190">This can take a while, depending on factors such as hello amount of data toobe replicated and hello available upstream bandwidth tooAzure.</span></span> <span data-ttu-id="999f6-191">État de la tâche Hello et ÉtatDescription sont mis à jour, procédez comme suit à hello atteindre un état de protection de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="999f6-191">hello job State and StateDescription are updated as follows, upon hello VM reaching a protected state.</span></span>

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. <span data-ttu-id="999f6-192">Mettre à jour les propriétés de récupération, telles que hello taille de rôle de machine virtuelle et hello réseau Azure tooattach hello du réseau interface cartes tooupon basculement de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="999f6-192">Update recovery properties, such as hello VM role size, and hello Azure network tooattach hello virtual machine's network interface cards tooupon failover.</span></span>

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update hello virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a><span data-ttu-id="999f6-193">Étape 8 : Exécution d’un test de basculement</span><span class="sxs-lookup"><span data-stu-id="999f6-193">Step 8: Run a test failover</span></span>
1. <span data-ttu-id="999f6-194">Exécutez une tâche de test de basculement, en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="999f6-194">Run a test failover job, as follows:</span></span>

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. <span data-ttu-id="999f6-195">Vérifiez que le test hello que machine virtuelle est créée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="999f6-195">Verify that hello test VM is created in Azure.</span></span> <span data-ttu-id="999f6-196">(travail de basculement de test hello est suspendu, après avoir créé la machine virtuelle de test hello dans Azure.</span><span class="sxs-lookup"><span data-stu-id="999f6-196">(hello test failover job is suspended, after creating hello test VM in Azure.</span></span> <span data-ttu-id="999f6-197">Hello tâche se termine par un nettoyage des artefacts hello créé lors de la reprise du travail de hello, comme illustré dans l’étape suivante de hello.)</span><span class="sxs-lookup"><span data-stu-id="999f6-197">hello job completes by cleaning up hello created artefacts upon resuming hello job, as illustrated in hello next step.)</span></span>
3. <span data-ttu-id="999f6-198">Hello complète test de basculement, comme suit :</span><span class="sxs-lookup"><span data-stu-id="999f6-198">Complete hello test failover, as follows:</span></span>

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a><span data-ttu-id="999f6-199">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="999f6-199">Next Steps</span></span>
<span data-ttu-id="999f6-200">[En savoir plus](https://msdn.microsoft.com/library/azure/mt637930.aspx) sur Azure Site Recovery avec les applets de commande PowerShell Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="999f6-200">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
