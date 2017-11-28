---
title: "aaaDeploy hello service de mobilité de récupération de Site dans Azure Automation DSC | Documents Microsoft"
description: "Décrit comment toouse Azure Automation DSC tooautomatically déployer Azure Site Recovery mobilité hello et agent Azure VM de VMware et de tooAzure de réplication de serveur physique"
services: site-recovery
documentationcenter: 
author: krnese
manager: lorenr
editor: 
ms.assetid: 1f8cd3ac-0522-48eb-a5f0-679ee9192ddb
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: krnese
ms.openlocfilehash: 52cdd13ceb61718a21137180c55db86919af5929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a><span data-ttu-id="07d02-103">Déployer le service de mobilité hello dans Azure Automation DSC pour la réplication de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="07d02-103">Deploy hello Mobility service with Azure Automation DSC for replication of VM</span></span>
<span data-ttu-id="07d02-104">Dans Operations Management Suite, nous fournissons une solution complète de sauvegarde et de récupération d’urgence que vous pouvez exploiter dans le cadre de votre plan de continuité d’activité.</span><span class="sxs-lookup"><span data-stu-id="07d02-104">In Operations Management Suite, we provide you with a comprehensive backup and disaster recovery solution that you can use as part of your business continuity plan.</span></span>

<span data-ttu-id="07d02-105">Nous avions commencé avec Hyper-V en utilisant Hyper-V Replica.</span><span class="sxs-lookup"><span data-stu-id="07d02-105">We started this journey together with Hyper-V by using Hyper-V Replica.</span></span> <span data-ttu-id="07d02-106">Mais nous avons développé toosupport une installation hétérogène, car les clients ont plusieurs hyperviseurs et plateformes dans leurs clouds.</span><span class="sxs-lookup"><span data-stu-id="07d02-106">But we have expanded toosupport a heterogeneous setup because customers have multiple hypervisors and platforms in their clouds.</span></span>

<span data-ttu-id="07d02-107">Si vous exécutez les charges de travail VMware et/ou vos serveurs physiques aujourd'hui, un serveur d’administration exécute tous les Hello composants d’Azure Site Recovery dans votre environnement toohandle hello communication et les données de la réplication avec Azure, quand Azure est la destination.</span><span class="sxs-lookup"><span data-stu-id="07d02-107">If you are running VMware workloads and/or physical servers today, a management server runs all of hello Azure Site Recovery components in your environment toohandle hello communication and data replication with Azure, when Azure is your destination.</span></span>

## <a name="deploy-hello-site-recovery-mobility-service-by-using-automation-dsc"></a><span data-ttu-id="07d02-108">Déployer le service de mobilité de récupération de Site hello à l’aide d’Automation DSC</span><span class="sxs-lookup"><span data-stu-id="07d02-108">Deploy hello Site Recovery Mobility service by using Automation DSC</span></span>
<span data-ttu-id="07d02-109">Commençons par analyser rapidement les opérations réellement effectuées par ce serveur d’administration.</span><span class="sxs-lookup"><span data-stu-id="07d02-109">Let's start by doing a quick breakdown of what this management server does.</span></span>

<span data-ttu-id="07d02-110">serveur d’administration Hello exécute plusieurs rôles de serveur.</span><span class="sxs-lookup"><span data-stu-id="07d02-110">hello management server runs several server roles.</span></span> <span data-ttu-id="07d02-111">L’un de ces rôles est la *configuration*, qui coordonne la communication et gère les processus de réplication et de récupération des données.</span><span class="sxs-lookup"><span data-stu-id="07d02-111">One of these roles is *configuration*, which coordinates communication and manages data replication and recovery processes.</span></span>

<span data-ttu-id="07d02-112">En outre, hello *processus* rôle fait Office de passerelle de réplication.</span><span class="sxs-lookup"><span data-stu-id="07d02-112">In addition, hello *process* role acts as a replication gateway.</span></span> <span data-ttu-id="07d02-113">Ce rôle reçoit des données de réplication à partir d’ordinateurs de la source protégée, elle optimise avec la mise en cache, la compression et le chiffrement et envoie ensuite compte de stockage Azure tooan.</span><span class="sxs-lookup"><span data-stu-id="07d02-113">This role receives replication data from protected source machines, optimizes it with caching, compression, and encryption, and then sends it tooan Azure storage account.</span></span> <span data-ttu-id="07d02-114">Une des fonctions hello pour le rôle de processus hello est également toopush installation de machines de tooprotected de service de mobilité hello et effectuer la détection automatique des ordinateurs virtuels VMware.</span><span class="sxs-lookup"><span data-stu-id="07d02-114">One of hello functions for hello process role is also toopush installation of hello Mobility service tooprotected machines and perform automatic discovery of VMware VMs.</span></span>

<span data-ttu-id="07d02-115">En l’absence d’une restauration à partir d’Azure, hello *cible maître* rôle traitera les données de réplication hello dans le cadre de cette opération.</span><span class="sxs-lookup"><span data-stu-id="07d02-115">If there's a failback from Azure, hello *master target* role will handle hello replication data as part of this operation.</span></span>

<span data-ttu-id="07d02-116">Pour les ordinateurs de hello protégé, nous s’appuient sur hello *service mobilité*.</span><span class="sxs-lookup"><span data-stu-id="07d02-116">For hello protected machines, we rely on hello *Mobility service*.</span></span> <span data-ttu-id="07d02-117">Ce composant est déployé tooevery machine (VMware VM ou serveur physique) que vous souhaitez tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="07d02-117">This component is deployed tooevery machine (VMware VM or physical server) that you want tooreplicate tooAzure.</span></span> <span data-ttu-id="07d02-118">Il capture les écritures de données sur l’ordinateur de hello et les transmet le serveur d’administration toohello (rôle de processus).</span><span class="sxs-lookup"><span data-stu-id="07d02-118">It captures data writes on hello machine and forwards them toohello management server (process role).</span></span>

<span data-ttu-id="07d02-119">Lorsque vous êtes confronté à la continuité d’activité, il est important toounderstand vos charges de travail, votre infrastructure et les composants de hello impliqués.</span><span class="sxs-lookup"><span data-stu-id="07d02-119">When you're dealing with business continuity, it's important toounderstand your workloads, your infrastructure, and hello components involved.</span></span> <span data-ttu-id="07d02-120">Vous pouvez ensuite requise hello pour votre objectif de temps de récupération (RTO) et l’objectif de point de récupération (RPO).</span><span class="sxs-lookup"><span data-stu-id="07d02-120">You can then meet hello requirements for your recovery time objective (RTO) and recovery point objective (RPO).</span></span> <span data-ttu-id="07d02-121">Dans ce contexte, hello service mobilité est tooensuring clé vos charges de travail protégés comme prévu.</span><span class="sxs-lookup"><span data-stu-id="07d02-121">In this context, hello Mobility service is key tooensuring that your workloads are protected as you would expect.</span></span>

<span data-ttu-id="07d02-122">Alors, comment pouvez-vous nous assurer de manière optimisée que l’installation est protégée et fiable, à l’aide de certains composants Operations Management Suite ?</span><span class="sxs-lookup"><span data-stu-id="07d02-122">So how can you, in an optimized way, ensure that you have a reliable protected setup with help from some Operations Management Suite components?</span></span>

<span data-ttu-id="07d02-123">Cet article fournit un exemple de comment vous pouvez utiliser Azure Automation état Configuration souhaité (DSC), ainsi que de la récupération de Site, tooensure qui :</span><span class="sxs-lookup"><span data-stu-id="07d02-123">This article provides an example of how you can use Azure Automation Desired State Configuration (DSC), together with Site Recovery, tooensure that:</span></span>

* <span data-ttu-id="07d02-124">service de mobilité Hello et l’agent de machine virtuelle Azure sont toohello déployé des ordinateurs Windows que vous souhaitez tooprotect.</span><span class="sxs-lookup"><span data-stu-id="07d02-124">hello Mobility service and Azure VM agent are deployed toohello Windows machines that you want tooprotect.</span></span>
* <span data-ttu-id="07d02-125">service de mobilité Hello et l’agent de machine virtuelle Azure sont toujours en cours d’exécution lorsque Azure est la cible de réplication hello.</span><span class="sxs-lookup"><span data-stu-id="07d02-125">hello Mobility service and Azure VM agent are always running when Azure is hello replication target.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07d02-126">Composants requis</span><span class="sxs-lookup"><span data-stu-id="07d02-126">Prerequisites</span></span>
* <span data-ttu-id="07d02-127">Un programme d’installation de référentiel toostore hello requis</span><span class="sxs-lookup"><span data-stu-id="07d02-127">A repository toostore hello required setup</span></span>
* <span data-ttu-id="07d02-128">Un tooregister de phrase secrète de référentiel toostore hello requis avec le serveur d’administration hello</span><span class="sxs-lookup"><span data-stu-id="07d02-128">A repository toostore hello required passphrase tooregister with hello management server</span></span>

  > [!NOTE]
  > <span data-ttu-id="07d02-129">Une phrase secrète unique est générée pour chaque serveur d’administration.</span><span class="sxs-lookup"><span data-stu-id="07d02-129">A unique passphrase is generated for each management server.</span></span> <span data-ttu-id="07d02-130">Si vous vous apprêtez à toodeploy plusieurs serveurs d’administration, vous avez tooensure que hello correct de mot de passe est stocké dans le fichier de passphrase.txt hello.</span><span class="sxs-lookup"><span data-stu-id="07d02-130">If you are going toodeploy multiple management servers, you have tooensure that hello correct passphrase is stored in hello passphrase.txt file.</span></span>
  >
  >
* <span data-ttu-id="07d02-131">Windows Management Framework (WMF) 5.0 est installé sur les ordinateurs hello que vous souhaitez tooenable pour la protection (il s’agit d’une exigence pour Automation DSC)</span><span class="sxs-lookup"><span data-stu-id="07d02-131">Windows Management Framework (WMF) 5.0 installed on hello machines that you want tooenable for protection (a requirement for Automation DSC)</span></span>

  > [!NOTE]
  > <span data-ttu-id="07d02-132">Si vous voulez que les ordinateurs de DSC pour Windows toouse qui disposent de WMF 4.0, consultez la section de hello [DSC d’utilisation dans des environnements déconnectés](## Use DSC in disconnected environments).</span><span class="sxs-lookup"><span data-stu-id="07d02-132">If you want toouse DSC for Windows machines that have WMF 4.0 installed, see hello section [Use DSC in disconnected environments](## Use DSC in disconnected environments).</span></span>
  

<span data-ttu-id="07d02-133">service de mobilité Hello peut être installé via la ligne de commande hello et accepte plusieurs arguments.</span><span class="sxs-lookup"><span data-stu-id="07d02-133">hello Mobility service can be installed through hello command line and accepts several arguments.</span></span> <span data-ttu-id="07d02-134">C’est pourquoi vous avez besoin des fichiers binaires de hello toohave (après les extraire à partir de votre programme d’installation) et les stocker dans un endroit où vous pouvez les récupérer à l’aide d’une configuration DSC.</span><span class="sxs-lookup"><span data-stu-id="07d02-134">That’s why you need toohave hello binaries (after extracting them from your setup) and store them in a place where you can retrieve them by using a DSC configuration.</span></span>

## <a name="step-1-extract-binaries"></a><span data-ttu-id="07d02-135">Étape 1 : extraction des fichiers binaires</span><span class="sxs-lookup"><span data-stu-id="07d02-135">Step 1: Extract binaries</span></span>
1. <span data-ttu-id="07d02-136">fichiers hello tooextract dont vous avez besoin pour cette configuration, accédez à toohello suivant active sur votre serveur d’administration :</span><span class="sxs-lookup"><span data-stu-id="07d02-136">tooextract hello files that you need for this setup, browse toohello following directory on your management server:</span></span>

    <span data-ttu-id="07d02-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span><span class="sxs-lookup"><span data-stu-id="07d02-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span></span>

    <span data-ttu-id="07d02-138">Dans ce dossier, vous devriez voir un fichier MSI nommé :</span><span class="sxs-lookup"><span data-stu-id="07d02-138">In this folder, you should see an MSI file named:</span></span>

    <span data-ttu-id="07d02-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span><span class="sxs-lookup"><span data-stu-id="07d02-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span></span>

    <span data-ttu-id="07d02-140">Utilisez hello suivant le programme d’installation de commande tooextract hello :</span><span class="sxs-lookup"><span data-stu-id="07d02-140">Use hello following command tooextract hello installer:</span></span>

    <span data-ttu-id="07d02-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span><span class="sxs-lookup"><span data-stu-id="07d02-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span></span>
2. <span data-ttu-id="07d02-142">Sélectionnez tous les fichiers et les envoyer tooa de dossier (zippé) compressé.</span><span class="sxs-lookup"><span data-stu-id="07d02-142">Select all files and send them tooa compressed (zipped) folder.</span></span>

<span data-ttu-id="07d02-143">Vous avez maintenant binaires hello que vous avez besoin du programme d’installation de tooautomate hello Hello service mobilité à l’aide d’Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="07d02-143">You now have hello binaries that you need tooautomate hello setup of hello Mobility service by using Automation DSC.</span></span>

### <a name="passphrase"></a><span data-ttu-id="07d02-144">Phrase secrète</span><span class="sxs-lookup"><span data-stu-id="07d02-144">Passphrase</span></span>
<span data-ttu-id="07d02-145">Ensuite, vous devez toodetermine où vous souhaitez tooplace ce dossier compressé.</span><span class="sxs-lookup"><span data-stu-id="07d02-145">Next, you need toodetermine where you want tooplace this zipped folder.</span></span> <span data-ttu-id="07d02-146">Vous pouvez utiliser un compte de stockage Azure, comme indiqué par la suite, toostore hello phrase secrète que vous avez besoin pour le programme d’installation hello.</span><span class="sxs-lookup"><span data-stu-id="07d02-146">You can use an Azure storage account, as shown later, toostore hello passphrase that you need for hello setup.</span></span> <span data-ttu-id="07d02-147">l’agent de Hello inscrira puis avec le serveur d’administration hello dans le cadre du processus de hello.</span><span class="sxs-lookup"><span data-stu-id="07d02-147">hello agent will then register with hello management server as part of hello process.</span></span>

<span data-ttu-id="07d02-148">phrase secrète Hello que vous avez obtenu lorsque vous avez déployé le serveur d’administration hello peut être enregistré fichier de texte tooa comme passphrase.txt.</span><span class="sxs-lookup"><span data-stu-id="07d02-148">hello passphrase that you got when you deployed hello management server can be saved tooa text file as passphrase.txt.</span></span>

<span data-ttu-id="07d02-149">Placez le dossier zippé de hello et mot de passe hello dans un conteneur dédié Bonjour compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="07d02-149">Place both hello zipped folder and hello passphrase in a dedicated container in hello Azure storage account.</span></span>

![Emplacement du dossier](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

<span data-ttu-id="07d02-151">Si vous préférez tookeep ces fichiers sur un partage sur votre réseau, vous pouvez le faire.</span><span class="sxs-lookup"><span data-stu-id="07d02-151">If you prefer tookeep these files on a share on your network, you can do so.</span></span> <span data-ttu-id="07d02-152">Vous devez simplement tooensure que les ressources hello DSC que vous utiliserez ultérieurement ont accès et peuvent obtenir le programme d’installation hello et la phrase secrète.</span><span class="sxs-lookup"><span data-stu-id="07d02-152">You just need tooensure that hello DSC resource that you will be using later has access and can get hello setup and passphrase.</span></span>

## <a name="step-2-create-hello-dsc-configuration"></a><span data-ttu-id="07d02-153">Étape 2 : Créer la configuration de hello DSC</span><span class="sxs-lookup"><span data-stu-id="07d02-153">Step 2: Create hello DSC configuration</span></span>
<span data-ttu-id="07d02-154">le programme d’installation Hello dépend de WMF 5.0.</span><span class="sxs-lookup"><span data-stu-id="07d02-154">hello setup depends on WMF 5.0.</span></span> <span data-ttu-id="07d02-155">Pour hello machine toosuccessfully configuration hello via Automation DSC, WMF 5.0 doit toobe présent.</span><span class="sxs-lookup"><span data-stu-id="07d02-155">For hello machine toosuccessfully apply hello configuration through Automation DSC, WMF 5.0 needs toobe present.</span></span>

<span data-ttu-id="07d02-156">environnement de Hello utilise hello suivant l’exemple de configuration DSC :</span><span class="sxs-lookup"><span data-stu-id="07d02-156">hello environment uses hello following example DSC configuration:</span></span>

```powershell
configuration ASRMobilityService {

    $RemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    $RemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    $RemoteAzureAgent = 'http://go.microsoft.com/fwlink/p/?LinkId=394789'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node localhost {

        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
```
<span data-ttu-id="07d02-157">configuration de Hello fera suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="07d02-157">hello configuration will do hello following:</span></span>

* <span data-ttu-id="07d02-158">les variables Hello indiquera les configuration hello où tooget hello les fichiers binaires pour le service de mobilité hello et agent de machine virtuelle Azure hello, où tooget hello phrase secrète et toostore hello de sortie.</span><span class="sxs-lookup"><span data-stu-id="07d02-158">hello variables will tell hello configuration where tooget hello binaries for hello Mobility service and hello Azure VM agent, where tooget hello passphrase, and where toostore hello output.</span></span>
* <span data-ttu-id="07d02-159">Hello configuration importera ressources xPSDesiredStateConfiguration DSC de hello, afin que vous puissiez utiliser `xRemoteFile` fichiers hello toodownload référentiel de hello.</span><span class="sxs-lookup"><span data-stu-id="07d02-159">hello configuration will import hello xPSDesiredStateConfiguration DSC resource, so that you can use `xRemoteFile` toodownload hello files from hello repository.</span></span>
* <span data-ttu-id="07d02-160">configuration de Hello créera un répertoire où vous souhaitez les fichiers binaires de toostore hello.</span><span class="sxs-lookup"><span data-stu-id="07d02-160">hello configuration will create a directory where you want toostore hello binaries.</span></span>
* <span data-ttu-id="07d02-161">ressource archive de Hello extrait les fichiers hello à partir du dossier compressé hello.</span><span class="sxs-lookup"><span data-stu-id="07d02-161">hello archive resource will extract hello files from hello zipped folder.</span></span>
* <span data-ttu-id="07d02-162">ressource d’installation de package de Hello installera le service de mobilité de hello de hello UNIFIEDAGENT. Programme d’installation EXE avec des arguments spécifiques hello.</span><span class="sxs-lookup"><span data-stu-id="07d02-162">hello package Install resource will install hello Mobility service from hello UNIFIEDAGENT.EXE installer with hello specific arguments.</span></span> <span data-ttu-id="07d02-163">(variables hello construire les arguments hello peut-être toobe modifié tooreflect votre environnement.)</span><span class="sxs-lookup"><span data-stu-id="07d02-163">(hello variables that construct hello arguments need toobe changed tooreflect your environment.)</span></span>
* <span data-ttu-id="07d02-164">Hello AzureAgent ressource installera l’agent Azure VM hello, ce qui est recommandé sur chaque machine virtuelle qui s’exécute dans Azure.</span><span class="sxs-lookup"><span data-stu-id="07d02-164">hello package AzureAgent resource will install hello Azure VM agent, which is recommended on every VM that runs in Azure.</span></span> <span data-ttu-id="07d02-165">l’agent de machine virtuelle Azure Hello rend également possible tooadd extensions toohello machine virtuelle après le basculement.</span><span class="sxs-lookup"><span data-stu-id="07d02-165">hello Azure VM agent also makes it possible tooadd extensions toohello VM after failover.</span></span>
* <span data-ttu-id="07d02-166">Hello service ou les ressources garantit que hello liées à des services de mobilité et hello services Azure sont toujours en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="07d02-166">hello service resource or resources will ensure that hello related Mobility services and hello Azure services are always running.</span></span>

<span data-ttu-id="07d02-167">Enregistrer la configuration de hello sous **ASRMobilityService**.</span><span class="sxs-lookup"><span data-stu-id="07d02-167">Save hello configuration as **ASRMobilityService**.</span></span>

> [!NOTE]
> <span data-ttu-id="07d02-168">N’oubliez pas tooreplace hello CSIP dans votre configuration tooreflect hello réel management server, afin que hello agent est connecté correctement et utilisera le mot de passe correct hello.</span><span class="sxs-lookup"><span data-stu-id="07d02-168">Remember tooreplace hello CSIP in your configuration tooreflect hello actual management server, so that hello agent will be connected correctly and will use hello correct passphrase.</span></span>
>
>

## <a name="step-3-upload-tooautomation-dsc"></a><span data-ttu-id="07d02-169">Étape 3 : Téléchargez tooAutomation DSC</span><span class="sxs-lookup"><span data-stu-id="07d02-169">Step 3: Upload tooAutomation DSC</span></span>
<span data-ttu-id="07d02-170">Étant donné que configuration hello DSC que vous avez effectuées pour importer un module de ressources DSC requis (xPSDesiredStateConfiguration), vous devez tooimport ce module dans Automation avant le téléchargement de la configuration de hello DSC.</span><span class="sxs-lookup"><span data-stu-id="07d02-170">Because hello DSC configuration that you made will import a required DSC resource module (xPSDesiredStateConfiguration), you need tooimport that module in Automation before you upload hello DSC configuration.</span></span>

<span data-ttu-id="07d02-171">Connexion tooyour compte Automation, parcourir trop**actifs** > **Modules**, puis cliquez sur **parcourir la galerie**.</span><span class="sxs-lookup"><span data-stu-id="07d02-171">Sign in tooyour Automation account, browse too**Assets** > **Modules**, and click **Browse Gallery**.</span></span>

<span data-ttu-id="07d02-172">Ici, vous pouvez rechercher pour le module de hello et importez-le tooyour compte.</span><span class="sxs-lookup"><span data-stu-id="07d02-172">Here you can search for hello module and import it tooyour account.</span></span>

![Importer le module](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

<span data-ttu-id="07d02-174">Lorsque vous avez terminé de cela, accédez tooyour ordinateur où vous avez des modules du Gestionnaire de ressources Azure hello installés et continuer la configuration de DSC tooimport hello nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="07d02-174">When you finish this, go tooyour machine where you have hello Azure Resource Manager modules installed and proceed tooimport hello newly created DSC configuration.</span></span>

### <a name="import-cmdlets"></a><span data-ttu-id="07d02-175">Importer les applets de commande</span><span class="sxs-lookup"><span data-stu-id="07d02-175">Import cmdlets</span></span>
<span data-ttu-id="07d02-176">Dans PowerShell, connectez-vous tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="07d02-176">In PowerShell, sign in tooyour Azure subscription.</span></span> <span data-ttu-id="07d02-177">Modifier hello applets de commande tooreflect votre environnement et capturer les informations de votre compte Automation dans une variable :</span><span class="sxs-lookup"><span data-stu-id="07d02-177">Modify hello cmdlets tooreflect your environment and capture your Automation account information in a variable:</span></span>

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

<span data-ttu-id="07d02-178">Télécharger hello configuration tooAutomation DSC à l’aide de hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="07d02-178">Upload hello configuration tooAutomation DSC by using hello following cmdlet:</span></span>

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-hello-configuration-in-automation-dsc"></a><span data-ttu-id="07d02-179">Compilation de configuration hello dans Automation DSC</span><span class="sxs-lookup"><span data-stu-id="07d02-179">Compile hello configuration in Automation DSC</span></span>
<span data-ttu-id="07d02-180">Ensuite, vous devez configuration hello toocompile Automation DSC, afin que vous puissiez démarrer tooregister nœuds tooit.</span><span class="sxs-lookup"><span data-stu-id="07d02-180">Next, you need toocompile hello configuration in Automation DSC, so that you can start tooregister nodes tooit.</span></span> <span data-ttu-id="07d02-181">Que faire, hello suivant l’applet de commande en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="07d02-181">You achieve that by running hello following cmdlet:</span></span>

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

<span data-ttu-id="07d02-182">Cela peut prendre quelques minutes, étant donné que vous déployez essentiellement le service collecteur DSC hello configuration toohello hébergé.</span><span class="sxs-lookup"><span data-stu-id="07d02-182">This can take a few minutes, because you're basically deploying hello configuration toohello hosted DSC pull service.</span></span>

<span data-ttu-id="07d02-183">Une fois que vous compilez la configuration de hello, vous pouvez récupérer des informations sur les travaux hello à l’aide de PowerShell (Get-AzureRmAutomationDscCompilationJob) ou à l’aide de hello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="07d02-183">After you compile hello configuration, you can retrieve hello job information by using PowerShell (Get-AzureRmAutomationDscCompilationJob) or by using hello [Azure portal](https://portal.azure.com/).</span></span>

![Tâche de récupération](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

<span data-ttu-id="07d02-185">Vous avez maintenant publié et téléchargé votre tooAutomation de configuration DSC DSC.</span><span class="sxs-lookup"><span data-stu-id="07d02-185">You have now successfully published and uploaded your DSC configuration tooAutomation DSC.</span></span>

## <a name="step-4-onboard-machines-tooautomation-dsc"></a><span data-ttu-id="07d02-186">Étape 4 : Machines intégré tooAutomation DSC</span><span class="sxs-lookup"><span data-stu-id="07d02-186">Step 4: Onboard machines tooAutomation DSC</span></span>
> [!NOTE]
> <span data-ttu-id="07d02-187">Une des conditions préalables de hello pour ce scénario est que vos ordinateurs Windows sont mis à jour avec la version la plus récente de WMF hello.</span><span class="sxs-lookup"><span data-stu-id="07d02-187">One of hello prerequisites for completing this scenario is that your Windows machines are updated with hello latest version of WMF.</span></span> <span data-ttu-id="07d02-188">Vous pouvez télécharger et installer la version correcte de hello pour votre plateforme de hello [centre de téléchargement](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="07d02-188">You can download and install hello correct version for your platform from hello [Download Center](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>
>
>

<span data-ttu-id="07d02-189">Vous allez maintenant créer un metaconfig pour DSC que vous allez appliquer tooyour nœuds.</span><span class="sxs-lookup"><span data-stu-id="07d02-189">You will now create a metaconfig for DSC that you will apply tooyour nodes.</span></span> <span data-ttu-id="07d02-190">toosucceed avec cela, vous devez tooretrieve hello point de terminaison URL et hello clé primaire pour votre compte Automation sélectionné dans Azure.</span><span class="sxs-lookup"><span data-stu-id="07d02-190">toosucceed with this, you need tooretrieve hello endpoint URL and hello primary key for your selected Automation account in Azure.</span></span> <span data-ttu-id="07d02-191">Vous pouvez trouver ces valeurs sous **clés** sur hello **tous les paramètres** panneau pour hello compte Automation.</span><span class="sxs-lookup"><span data-stu-id="07d02-191">You can find these values under **Keys** on hello **All settings** blade for hello Automation account.</span></span>

![Valeurs de clé](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

<span data-ttu-id="07d02-193">Dans cet exemple, vous disposez d’un serveur physique Windows Server 2012 R2 que vous souhaitez tooprotect à l’aide de récupération de Site.</span><span class="sxs-lookup"><span data-stu-id="07d02-193">In this example, you have a Windows Server 2012 R2 physical server that you want tooprotect by using Site Recovery.</span></span>

### <a name="check-for-any-pending-file-rename-operations-in-hello-registry"></a><span data-ttu-id="07d02-194">Recherchez les opérations de changement de nom de fichier dans le Registre de hello en attente</span><span class="sxs-lookup"><span data-stu-id="07d02-194">Check for any pending file rename operations in hello registry</span></span>
<span data-ttu-id="07d02-195">Avant de commencer serveur hello de tooassociate avec le point de terminaison Automation DSC hello, nous vous recommandons de vérifier pour les opérations de changement de nom de fichier dans le Registre de hello en attente.</span><span class="sxs-lookup"><span data-stu-id="07d02-195">Before you start tooassociate hello server with hello Automation DSC endpoint, we recommend that you check for any pending file rename operations in hello registry.</span></span> <span data-ttu-id="07d02-196">Ils peuvent interdire le programme d’installation Bonjour de terminer en raison tooa redémarrage en attente.</span><span class="sxs-lookup"><span data-stu-id="07d02-196">They might prohibit hello setup from finishing due tooa pending reboot.</span></span>

<span data-ttu-id="07d02-197">Exécutez hello suivant tooverify applet de commande qu’il n’existe aucun redémarrage en attente sur le serveur de hello :</span><span class="sxs-lookup"><span data-stu-id="07d02-197">Run hello following cmdlet tooverify that there’s no pending reboot on hello server:</span></span>

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
<span data-ttu-id="07d02-198">Si cela apparaît vide, vous êtes tooproceed OK.</span><span class="sxs-lookup"><span data-stu-id="07d02-198">If this shows empty, you are OK tooproceed.</span></span> <span data-ttu-id="07d02-199">Si ce n’est pas le cas, vous devez résoudre ce problème en redémarrant le serveur de hello pendant une fenêtre de maintenance.</span><span class="sxs-lookup"><span data-stu-id="07d02-199">If not, you should address this by rebooting hello server during a maintenance window.</span></span>

<span data-ttu-id="07d02-200">configuration de hello tooapply sur le serveur de hello, hello PowerShell Integrated Scripting Environment (ISE) de démarrer et exécuter hello script suivant.</span><span class="sxs-lookup"><span data-stu-id="07d02-200">tooapply hello configuration on hello server, start hello PowerShell Integrated Scripting Environment (ISE) and run hello following script.</span></span> <span data-ttu-id="07d02-201">Il s’agit essentiellement une configuration DSC locale qui sera hello Gestionnaire de Configuration Local moteur tooregister avec hello service Automation DSC de demander et de récupérer la configuration spécifique de hello (ASRMobilityService.localhost).</span><span class="sxs-lookup"><span data-stu-id="07d02-201">This is essentially a DSC local configuration that will instruct hello Local Configuration Manager engine tooregister with hello Automation DSC service and retrieve hello specific configuration (ASRMobilityService.localhost).</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration metaconfig {
    param (
        $URL,
        $Key
    )
    node localhost {
        Settings {
            RefreshFrequencyMins = '30'
            RebootNodeIfNeeded = $true
            RefreshMode = 'PULL'
            ActionAfterReboot = 'ContinueConfiguration'
            ConfigurationMode = 'ApplyAndMonitor'
            AllowModuleOverwrite = $true
        }

        ResourceRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }

        ConfigurationRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
            ConfigurationNames = 'ASRMobilityService.localhost'
        }

        ReportServerWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }
    }
}
metaconfig -URL 'https://we-agentservice-prod-1.azure-automation.net/accounts/<YOURAAAccountID>' -Key '<YOURAAAccountKey>'

Set-DscLocalConfigurationManager .\metaconfig -Force -Verbose
```

<span data-ttu-id="07d02-202">Cette configuration entraîne hello Gestionnaire de Configuration Local tooregister moteur lui-même avec Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="07d02-202">This configuration will cause hello Local Configuration Manager engine tooregister itself with Automation DSC.</span></span> <span data-ttu-id="07d02-203">Il détermine également comment le moteur de hello doit fonctionner, ce qu’il doit faire s’il existe une dérive de la configuration (ApplyAndAutoCorrect) et comment il doit continuer avec la configuration de hello si un redémarrage est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="07d02-203">It will also determine how hello engine should operate, what it should do if there's a configuration drift (ApplyAndAutoCorrect), and how it should proceed with hello configuration if a reboot is required.</span></span>

<span data-ttu-id="07d02-204">Une fois que vous exécutez ce script, nœud de hello doit démarrer tooregister avec Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="07d02-204">After you run this script, hello node should start tooregister with Automation DSC.</span></span>

![Enregistrement du nœud en cours](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

<span data-ttu-id="07d02-206">Si vous revenez toohello portail Azure, vous pouvez voir ce nœud nouvellement inscrit hello maintenant s’affiche dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="07d02-206">If you go back toohello Azure portal, you can see that hello newly registered node has now appeared in hello portal.</span></span>

![Nœud dans le portail de hello](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

<span data-ttu-id="07d02-208">Sur le serveur de hello, vous pouvez exécuter hello suivant PowerShell tooverify applet de commande qui hello nœud a été correctement enregistré :</span><span class="sxs-lookup"><span data-stu-id="07d02-208">On hello server, you can run hello following PowerShell cmdlet tooverify that hello node has been registered correctly:</span></span>

```powershell
Get-DscLocalConfigurationManager
```

<span data-ttu-id="07d02-209">Une fois la configuration de hello a été extraite et appliquées toohello serveur, vous pouvez vérifier cela en exécutant hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="07d02-209">After hello configuration has been pulled and applied toohello server, you can verify this by running hello following cmdlet:</span></span>

```powershell
Get-DscConfigurationStatus
```

<span data-ttu-id="07d02-210">sortie de Hello montre que ce serveur hello a extraite avec succès sa configuration :</span><span class="sxs-lookup"><span data-stu-id="07d02-210">hello output shows that hello server has successfully pulled its configuration:</span></span>

![Sortie](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

<span data-ttu-id="07d02-212">En outre, le programme d’installation de hello mobilité service a son propre journal qui se trouvent à *lecteur_système*\ProgramData\ASRSetupLogs.</span><span class="sxs-lookup"><span data-stu-id="07d02-212">In addition, hello Mobility service setup has its own log that can be found at *SystemDrive*\ProgramData\ASRSetupLogs.</span></span>

<span data-ttu-id="07d02-213">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="07d02-213">That’s it.</span></span> <span data-ttu-id="07d02-214">Vous avez désormais déployé et inscrit le service de mobilité hello sur ordinateur hello que vous souhaitez tooprotect à l’aide de récupération de Site.</span><span class="sxs-lookup"><span data-stu-id="07d02-214">You have now successfully deployed and registered hello Mobility service on hello machine that you want tooprotect by using Site Recovery.</span></span> <span data-ttu-id="07d02-215">DSC permet de garantir que les services hello requis sont toujours en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="07d02-215">DSC will make sure that hello required services are always running.</span></span>

![Déploiement réussi](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

<span data-ttu-id="07d02-217">Une fois que le serveur d’administration hello détecte un déploiement réussi de hello, vous pouvez configurer la protection et activer la réplication sur l’ordinateur de hello à l’aide de récupération de Site.</span><span class="sxs-lookup"><span data-stu-id="07d02-217">After hello management server detects hello successful deployment, you can configure protection and enable replication on hello machine by using Site Recovery.</span></span>

## <a name="use-dsc-in-disconnected-environments"></a><span data-ttu-id="07d02-218">Utilisation de DSC dans des environnements déconnectés</span><span class="sxs-lookup"><span data-stu-id="07d02-218">Use DSC in disconnected environments</span></span>
<span data-ttu-id="07d02-219">Si vos ordinateurs ne sont pas connecté toohello Internet, vous pouvez toujours s’appuient sur DSC toodeploy et configurer le service de mobilité hello sur les charges de travail hello que vous souhaitez tooprotect.</span><span class="sxs-lookup"><span data-stu-id="07d02-219">If your machines aren’t connected toohello Internet, you can still rely on DSC toodeploy and configure hello Mobility service on hello workloads that you want tooprotect.</span></span>

<span data-ttu-id="07d02-220">Vous pouvez instancier votre propre serveur de collecteur DSC dans votre environnement tooessentially fournir hello les mêmes fonctionnalités que vous obtenez d’Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="07d02-220">You can instantiate your own DSC pull server in your environment tooessentially provide hello same capabilities that you get from Automation DSC.</span></span> <span data-ttu-id="07d02-221">Autrement dit, les clients de hello seront hello configuration du collecteur (après son inscription) toohello DSC de point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="07d02-221">That is, hello clients will pull hello configuration (after it's registered) toohello DSC endpoint.</span></span> <span data-ttu-id="07d02-222">Toutefois, une autre option est toomanually push hello DSC configuration tooyour les ordinateurs, localement ou à distance.</span><span class="sxs-lookup"><span data-stu-id="07d02-222">However, another option is toomanually push hello DSC configuration tooyour machines, either locally or remotely.</span></span>

<span data-ttu-id="07d02-223">Notez que dans cet exemple, il existe un paramètre ajouté pour le nom de l’ordinateur hello.</span><span class="sxs-lookup"><span data-stu-id="07d02-223">Note that in this example, there's an added parameter for hello computer name.</span></span> <span data-ttu-id="07d02-224">les fichiers distants Hello se trouvent désormais sur un partage distant doit être accessible par les ordinateurs hello que vous souhaitez tooprotect.</span><span class="sxs-lookup"><span data-stu-id="07d02-224">hello remote files are now located on a remote share that should be accessible by hello machines that you want tooprotect.</span></span> <span data-ttu-id="07d02-225">fin de Hello du script de hello applique la configuration de hello, puis démarre tooapply hello DSC configuration toohello cible ordinateur.</span><span class="sxs-lookup"><span data-stu-id="07d02-225">hello end of hello script enacts hello configuration and then starts tooapply hello DSC configuration toohello target computer.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="07d02-226">Composants requis</span><span class="sxs-lookup"><span data-stu-id="07d02-226">Prerequisites</span></span>
<span data-ttu-id="07d02-227">Vérifiez que hello xPSDesiredStateConfiguration PowerShell est installé.</span><span class="sxs-lookup"><span data-stu-id="07d02-227">Make sure that hello xPSDesiredStateConfiguration PowerShell module is installed.</span></span> <span data-ttu-id="07d02-228">Pour les ordinateurs Windows où WMF 5.0 est installé, vous pouvez installer le module xPSDesiredStateConfiguration de hello en exécutant hello suivant l’applet de commande sur les ordinateurs cibles de hello :</span><span class="sxs-lookup"><span data-stu-id="07d02-228">For Windows machines where WMF 5.0 is installed, you can install hello xPSDesiredStateConfiguration module by running hello following cmdlet on hello target machines:</span></span>

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

<span data-ttu-id="07d02-229">Vous pouvez également télécharger et enregistrer le module de hello en cas de besoin toodistribute il tooWindows les ordinateurs qui disposent de WMF 4.0.</span><span class="sxs-lookup"><span data-stu-id="07d02-229">You can also download and save hello module in case you need toodistribute it tooWindows machines that have WMF 4.0.</span></span> <span data-ttu-id="07d02-230">Exécutez cette applet de commande sur une machine sur laquelle PowerShellGet (WMF 5.0) est installé :</span><span class="sxs-lookup"><span data-stu-id="07d02-230">Run this cmdlet on a machine where PowerShellGet (WMF 5.0) is present:</span></span>

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

<span data-ttu-id="07d02-231">Assurez-vous également de WMF 4.0, ce hello [mise à jour Windows 8.1 KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) est installé sur les ordinateurs hello.</span><span class="sxs-lookup"><span data-stu-id="07d02-231">Also for WMF 4.0, ensure that hello [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) is installed on hello machines.</span></span>

<span data-ttu-id="07d02-232">Hello configuration suivante peut être appliquée tooWindows les ordinateurs qui ont WMF 5.0 et WMF 4.0 :</span><span class="sxs-lookup"><span data-stu-id="07d02-232">hello following configuration can be pushed tooWindows machines that have WMF 5.0 and WMF 4.0:</span></span>

```powershell
configuration ASRMobilityService {
    param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullOrEmpty()]
        [System.String] $ComputerName
    )

    $RemoteFile = '\\myfileserver\share\asr.zip'
    $RemotePassphrase = '\\myfileserver\share\passphrase.txt'
    $RemoteAzureAgent = '\\myfileserver\share\AzureVmAgent.msi'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node $ComputerName {      
        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
ASRMobilityService -ComputerName 'MyTargetComputerName'

Start-DscConfiguration .\ASRMobilityService -Wait -Force -Verbose
```

<span data-ttu-id="07d02-233">Si vous souhaitez tooinstantiate votre propre serveur de collecteur DSC sur vos capacités d’hello toomimic réseau d’entreprise que vous pouvez obtenir à partir de l’Automation DSC, consultez [configuration d’un serveur de collecteur web DSC](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="07d02-233">If you want tooinstantiate your own DSC pull server on your corporate network toomimic hello capabilities that you can get from Automation DSC, see [Setting up a DSC web pull server](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span></span>

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="07d02-234">Déploiement d’une configuration DSC à l’aide d’un modèle Azure Resource Manager (facultatif)</span><span class="sxs-lookup"><span data-stu-id="07d02-234">Optional: Deploy a DSC configuration by using an Azure Resource Manager template</span></span>
<span data-ttu-id="07d02-235">Cet article se sont concentrées sur comment vous pouvez créer votre propre tooautomatically de configuration DSC déployer le service de mobilité hello et hello Agent de machine virtuelle Azure--et vous assurer qu’ils s’exécutent sur des ordinateurs de hello que vous souhaitez tooprotect.</span><span class="sxs-lookup"><span data-stu-id="07d02-235">This article has focused on how you can create your own DSC configuration tooautomatically deploy hello Mobility service and hello Azure VM Agent--and ensure that they are running on hello machines that you want tooprotect.</span></span> <span data-ttu-id="07d02-236">Nous avons également un modèle Azure Resource Manager qui sera déployée de ce compte d’Azure Automation DSC configuration tooa nouveau ou existant.</span><span class="sxs-lookup"><span data-stu-id="07d02-236">We also have an Azure Resource Manager template that will deploy this DSC configuration tooa new or existing Azure Automation account.</span></span> <span data-ttu-id="07d02-237">modèle de Hello utilisera les paramètres d’entrée toocreate Automation actifs qui contiendront les variables hello pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="07d02-237">hello template will use input parameters toocreate Automation assets that will contain hello variables for your environment.</span></span>

<span data-ttu-id="07d02-238">Après avoir déployé le modèle de hello, vous pouvez simplement faire référence toostep 4 dans ce guide de tooonboard vos ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="07d02-238">After you deploy hello template, you can simply refer toostep 4 in this guide tooonboard your machines.</span></span>

<span data-ttu-id="07d02-239">modèle de Hello fera suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="07d02-239">hello template will do hello following:</span></span>

1. <span data-ttu-id="07d02-240">Utilisation d’un compte Automation existant ou création d’un nouveau compte</span><span class="sxs-lookup"><span data-stu-id="07d02-240">Use an existing Automation account or create a new one</span></span>
2. <span data-ttu-id="07d02-241">Prenez les paramètres d’entrée pour :</span><span class="sxs-lookup"><span data-stu-id="07d02-241">Take input parameters for:</span></span>
   * <span data-ttu-id="07d02-242">ASRRemoteFile--emplacement hello où vous avez stocké le programme d’installation de service de mobilité hello</span><span class="sxs-lookup"><span data-stu-id="07d02-242">ASRRemoteFile--hello location where you have stored hello Mobility service setup</span></span>
   * <span data-ttu-id="07d02-243">ASRPassphrase--emplacement hello où vous avez stocké le fichier de passphrase.txt hello</span><span class="sxs-lookup"><span data-stu-id="07d02-243">ASRPassphrase--hello location where you have stored hello passphrase.txt file</span></span>
   * <span data-ttu-id="07d02-244">ASRCSEndpoint--adresse IP de hello de votre serveur d’administration</span><span class="sxs-lookup"><span data-stu-id="07d02-244">ASRCSEndpoint--hello IP address of your management server</span></span>
3. <span data-ttu-id="07d02-245">Importer le module PowerShell de xPSDesiredStateConfiguration hello</span><span class="sxs-lookup"><span data-stu-id="07d02-245">Import hello xPSDesiredStateConfiguration PowerShell module</span></span>
4. <span data-ttu-id="07d02-246">Créer et compiler la configuration DSC de hello</span><span class="sxs-lookup"><span data-stu-id="07d02-246">Create and compile hello DSC configuration</span></span>

<span data-ttu-id="07d02-247">Hello toutes les étapes précédentes aura lieu dans l’ordre de droite hello, afin que vous pouvez démarrer l’intégration de vos ordinateurs pour la protection.</span><span class="sxs-lookup"><span data-stu-id="07d02-247">All hello preceding steps will happen in hello right order, so that you can start onboarding your machines for protection.</span></span>

<span data-ttu-id="07d02-248">modèle Hello, avec des instructions pour le déploiement, se trouve sur [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span><span class="sxs-lookup"><span data-stu-id="07d02-248">hello template, with instructions for deployment, is located on [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span></span>

<span data-ttu-id="07d02-249">Déployer le modèle de hello à l’aide de PowerShell :</span><span class="sxs-lookup"><span data-stu-id="07d02-249">Deploy hello template by using PowerShell:</span></span>

```powershell
$RGDeployArgs = @{
    Name = 'DSC3'
    ResourceGroupName = 'KNOMS'
    TemplateFile = 'https://raw.githubusercontent.com/krnese/AzureDeploy/master/OMS/MSOMS/DSC/azuredeploy.json'
    OMSAutomationAccountName = 'KNOMSAA'
    ASRRemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    ASRRemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    ASRCSEndpoint = '10.0.0.115'
    DSCJobGuid = [System.Guid]::NewGuid().ToString()
}
New-AzureRmResourceGroupDeployment @RGDeployArgs -Verbose
```

## <a name="next-steps"></a><span data-ttu-id="07d02-250">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="07d02-250">Next steps</span></span>
<span data-ttu-id="07d02-251">Une fois que vous déployez des agents de service de mobilité hello, vous pouvez [activer la réplication](site-recovery-vmware-to-azure.md) pour les ordinateurs virtuels de hello.</span><span class="sxs-lookup"><span data-stu-id="07d02-251">After you deploy hello Mobility service agents, you can [enable replication](site-recovery-vmware-to-azure.md) for hello virtual machines.</span></span>
