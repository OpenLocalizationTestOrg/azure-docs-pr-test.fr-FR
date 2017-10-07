---
title: " Gérer un serveur de traitement de montée en puissance parallèle dans Azure Site Recovery | Microsoft Docs"
description: "Cet article décrit comment tooset configurer et gérer un serveur de traitement de montée en puissance parallèle dans Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 3d72f9c2c7014a4ff2fa2af168aa55ad1452eae5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-scale-out-process-server"></a><span data-ttu-id="13a3b-103">Gérer un serveur de traitement de montée en puissance parallèle</span><span class="sxs-lookup"><span data-stu-id="13a3b-103">Manage a Scale-out Process Server</span></span>

<span data-ttu-id="13a3b-104">Serveur de traitement de montée en puissance parallèle agit en tant que coordinateur pour un transfert de données entre les services de récupération de Site hello et votre infrastructure locale.</span><span class="sxs-lookup"><span data-stu-id="13a3b-104">Scale-out Process Server acts as a coordinator for data transfer between hello Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="13a3b-105">Cet article explique comment installer, configurer et gérer un serveur de traitement de montée en puissance parallèle.</span><span class="sxs-lookup"><span data-stu-id="13a3b-105">This article describes how you can set up, configure, and manage a Scale-out Process Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13a3b-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="13a3b-106">Prerequisites</span></span>
<span data-ttu-id="13a3b-107">Hello Voici hello recommandé de matériel, logiciels et tooset de configuration requise de réseau d’un serveur de processus de montée en puissance parallèle.</span><span class="sxs-lookup"><span data-stu-id="13a3b-107">hello following are hello recommended hardware, software, and network configuration required tooset up a Scale-out Process Server.</span></span>

> [!NOTE]
> <span data-ttu-id="13a3b-108">[Planification de la capacité](site-recovery-capacity-planner.md) est un tooensure étape importante déployer hello serveur de traitement de montée en puissance parallèle avec une configuration qui convient le mieux vos exigences de charge.</span><span class="sxs-lookup"><span data-stu-id="13a3b-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step tooensure that you deploy hello Scale-out Process Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="13a3b-109">En savoir plus sur les [caractéristiques de mise à l’échelle pour un serveur de traitement de montée en puissance parallèle](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="13a3b-109">Read more about [Scaling characteristics for a Scale-out Process Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-scale-out-process-server-software"></a><span data-ttu-id="13a3b-110">Téléchargement du logiciel de serveur de traitement de montée en puissance parallèle hello</span><span class="sxs-lookup"><span data-stu-id="13a3b-110">Downloading hello Scale-out Process Server software</span></span>
1. <span data-ttu-id="13a3b-111">Ouvrez une session toohello tooyour portal et parcourir Azure coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="13a3b-111">Log on toohello Azure portal and browse tooyour Recovery Services Vault.</span></span>
2. <span data-ttu-id="13a3b-112">Parcourir trop**Infrastructure Site Recovery** > **serveurs de Configuration** (sous VMware pour les & ordinateurs physiques).</span><span class="sxs-lookup"><span data-stu-id="13a3b-112">Browse too**Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>
3. <span data-ttu-id="13a3b-113">Sélectionnez votre toodrill de serveur de configuration vers le bas dans la page des détails du serveur de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="13a3b-113">Select your configuration server toodrill down into hello configuration server's details page.</span></span>
4. <span data-ttu-id="13a3b-114">Cliquez sur hello **+ serveur de processus** bouton.</span><span class="sxs-lookup"><span data-stu-id="13a3b-114">Click hello **+ Process Server** button.</span></span>
5. <span data-ttu-id="13a3b-115">Bonjour **serveur ajouter** page, sélectionnez **une montée en puissance de déployer un serveur de processus locale** option hello **choisir où vous souhaitez toodeploy votre serveur de processus** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="13a3b-115">In hello **Add Process server** page, select **Deploy a Scale-out Process Server on-premises** option from hello **Choose where you want toodeploy your process server** drop-down.</span></span>

  ![Page Ajouter des serveurs](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. <span data-ttu-id="13a3b-117">Cliquez sur hello **téléchargement hello installation unifié de Microsoft Azure Site Recovery** lien toodownload hello version la plus récente de l’installation du serveur de processus hello montée en puissance parallèle.</span><span class="sxs-lookup"><span data-stu-id="13a3b-117">Click hello **Download hello Microsoft Azure Site Recovery Unified Setup** link toodownload hello latest version of hello Scale-out Process Server installation.</span></span>

  > [!WARNING]
  <span data-ttu-id="13a3b-118">Hello version de votre serveur de traitement de montée en puissance parallèle doit être égale tooor inférieur à la version du serveur de Configuration hello en cours d’exécution dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="13a3b-118">hello version of your Scale-out Process Server should be equal tooor lesser than hello Configuration Server version running in your environment.</span></span> <span data-ttu-id="13a3b-119">Un moyen simple tooensure version de compatibilité est toouse hello mêmes bits du programme d’installation que vous avez récemment utilisé tooinstall/mettre à jour votre serveur de Configuration.</span><span class="sxs-lookup"><span data-stu-id="13a3b-119">A simple way tooensure version compatibility is toouse hello same installer bits that you recently used tooinstall/update your Configuration Server.</span></span>

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a><span data-ttu-id="13a3b-120">Installation et inscription d’un serveur de traitement de montée en puissance parallèle à partir de l’interface graphique utilisateur</span><span class="sxs-lookup"><span data-stu-id="13a3b-120">Installing and registering a Scale-out Process Server from GUI</span></span>
<span data-ttu-id="13a3b-121">Si vous avez tooscale votre déploiement au-delà de 200 machines sources, ou un plan quotidien total évolution du taux de plus de 2 To, vous devez le volume de trafic de processus supplémentaire serveurs toohandle hello.</span><span class="sxs-lookup"><span data-stu-id="13a3b-121">If you have tooscale out your deployment beyond 200 source machines, or a total daily churn rate of more than 2 TB, you need additional process servers toohandle hello traffic volume.</span></span>

<span data-ttu-id="13a3b-122">Vérifiez hello [dimensionner des recommandations pour les serveurs de processus](#size-recommendations-for-the-process-server), puis suivez ces tooset obtenir des instructions de configuration de serveur de processus hello.</span><span class="sxs-lookup"><span data-stu-id="13a3b-122">Check hello [size recommendations for process servers](#size-recommendations-for-the-process-server), and then follow these instructions tooset up hello process server.</span></span> <span data-ttu-id="13a3b-123">Après avoir configuré le serveur de hello, vous migrez source machines toouse il.</span><span class="sxs-lookup"><span data-stu-id="13a3b-123">After setting up hello server, you migrate source machines toouse it.</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a><span data-ttu-id="13a3b-124">Installation et inscription d’un serveur de traitement de montée en puissance parallèle à l’aide de la ligne de commande</span><span class="sxs-lookup"><span data-stu-id="13a3b-124">Installing and registering a Scale-out Process Server using command-line</span></span>

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a><span data-ttu-id="13a3b-125">Exemple d’utilisation</span><span class="sxs-lookup"><span data-stu-id="13a3b-125">Sample usage</span></span>
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a><span data-ttu-id="13a3b-126">Arguments de la ligne de commande du programme d’installation du serveur de traitement de montée en puissance parallèle.</span><span class="sxs-lookup"><span data-stu-id="13a3b-126">Scale-out Process Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="13a3b-127">Créer un fichier de configuration des paramètres de proxy</span><span class="sxs-lookup"><span data-stu-id="13a3b-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="13a3b-128">Le paramètre ProxySettingsFilePath prend un fichier en tant qu’entrée.</span><span class="sxs-lookup"><span data-stu-id="13a3b-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="13a3b-129">Créer un fichier à l’aide de hello suivante, mettre en forme et passez-le en tant que paramètre ProxySettingsFilePath d’entrée.</span><span class="sxs-lookup"><span data-stu-id="13a3b-129">Create file using hello following format and pass it as input ProxySettingsFilePath parameter.</span></span>
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a><span data-ttu-id="13a3b-130">Modification des paramètres de proxy pour le serveur de traitement de montée en puissance parallèle</span><span class="sxs-lookup"><span data-stu-id="13a3b-130">Modifying proxy settings for Scale-out Process Server</span></span>
1. <span data-ttu-id="13a3b-131">Connectez-vous à votre serveur de traitement de montée en puissance parallèle.</span><span class="sxs-lookup"><span data-stu-id="13a3b-131">Login  into your Scale-out Process Server.</span></span>
2. <span data-ttu-id="13a3b-132">Ouvrez une fenêtre de commandes PowerShell administrateur.</span><span class="sxs-lookup"><span data-stu-id="13a3b-132">Open an Admin PowerShell command window.</span></span>
3. <span data-ttu-id="13a3b-133">Exécutez hello commande suivante</span><span class="sxs-lookup"><span data-stu-id="13a3b-133">Run hello following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. <span data-ttu-id="13a3b-134">Ensuite parcourir le répertoire de toohello **%PROGRAMDATA%\ASR\Agent** et hello exécution de commande suivante</span><span class="sxs-lookup"><span data-stu-id="13a3b-134">Next browse toohello directory **%PROGRAMDATA%\ASR\Agent** and run hello following command</span></span>
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a><span data-ttu-id="13a3b-135">Réinscription d’un serveur de traitement de montée en puissance parallèle</span><span class="sxs-lookup"><span data-stu-id="13a3b-135">Re-registering a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* <span data-ttu-id="13a3b-136">Ouvrez ensuite une invite de commandes administrateur.</span><span class="sxs-lookup"><span data-stu-id="13a3b-136">Next open an Admin command prompt.</span></span>
* <span data-ttu-id="13a3b-137">Parcourir le répertoire de toohello **%PROGRAMDATA%\ASR\Agent** et exécutez la commande hello</span><span class="sxs-lookup"><span data-stu-id="13a3b-137">Browse toohello directory **%PROGRAMDATA%\ASR\Agent** and run hello command</span></span>

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a><span data-ttu-id="13a3b-138">Mise à niveau d’un serveur de traitement de montée en puissance parallèle</span><span class="sxs-lookup"><span data-stu-id="13a3b-138">Upgrading a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a><span data-ttu-id="13a3b-139">Désaffectation d’un serveur de traitement de montée en puissance parallèle</span><span class="sxs-lookup"><span data-stu-id="13a3b-139">Decommissioning a Scale-out Process Server</span></span>
1. <span data-ttu-id="13a3b-140">Assurez-vous que :</span><span class="sxs-lookup"><span data-stu-id="13a3b-140">Ensure that:</span></span>
  - <span data-ttu-id="13a3b-141">État de la connexion du serveur de configuration affiche sous la forme **connecté** Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="13a3b-141">Configuration Server's connection state shows as **Connected** in hello Azure portal</span></span>
  - <span data-ttu-id="13a3b-142">Serveur de processus est toujours en mesure de toocommunicate avec le serveur de Configuration hello.</span><span class="sxs-lookup"><span data-stu-id="13a3b-142">Process Server's is still able toocommunicate with hello Configuration server.</span></span>
2. <span data-ttu-id="13a3b-143">Ouvrez une session dans le serveur de processus toohello en tant qu’administrateur</span><span class="sxs-lookup"><span data-stu-id="13a3b-143">Log in toohello process server as an administrator</span></span>
3. <span data-ttu-id="13a3b-144">Ouvrez le Panneau de configuration > Programme > Désinstaller des programmes</span><span class="sxs-lookup"><span data-stu-id="13a3b-144">Open up Control Panel > Program > Uninstall Programs</span></span>
4. <span data-ttu-id="13a3b-145">Désinstaller les programmes hello dans la séquence de hello étant donné ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="13a3b-145">Uninstall hello programs in hello sequence given following:</span></span>
  * <span data-ttu-id="13a3b-146">Serveur de configuration Microsoft Azure Site Recovery/Serveur de traitement</span><span class="sxs-lookup"><span data-stu-id="13a3b-146">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="13a3b-147">Dépendances du serveur de configuration Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="13a3b-147">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="13a3b-148">Agent Microsoft Azure Recovery Services</span><span class="sxs-lookup"><span data-stu-id="13a3b-148">Microsoft Azure Recovery Services Agent</span></span>

<span data-ttu-id="13a3b-149">Il peut prendre too15-up pour tooreflect de suppression de serveur de processus hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="13a3b-149">It can take up-too15 minutes for hello Process Server deletion tooreflect in hello Azure portal.</span></span>

  > [!NOTE]
  <span data-ttu-id="13a3b-150">Si le serveur de processus hello est toocommunicate impossible avec hello serveur de Configuration (état de la connexion dans le portail est déconnecté), vous devez toofollow hello suivant les étapes toopurge de hello serveur de Configuration.</span><span class="sxs-lookup"><span data-stu-id="13a3b-150">If hello Process server is unable toocommunicate with hello Configuration Server (Connection State in portal is Disconnected), then you need toofollow hello following steps toopurge it from hello Configuration Server.</span></span>

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a><span data-ttu-id="13a3b-151">Désinscription d’un serveur de traitement de montée en puissance parallèle déconnecté d’un serveur de configuration</span><span class="sxs-lookup"><span data-stu-id="13a3b-151">Unregistering a disconnected Scale-out Process server from a Configuration Server</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a><span data-ttu-id="13a3b-152">Exigences de dimensionnement pour un serveur de traitement de montée en puissance parallèle</span><span class="sxs-lookup"><span data-stu-id="13a3b-152">Sizing requirements for a Scale-out Process Server</span></span>

| <span data-ttu-id="13a3b-153">**Serveur de traitement supplémentaire**</span><span class="sxs-lookup"><span data-stu-id="13a3b-153">**Additional process server**</span></span> | <span data-ttu-id="13a3b-154">**Taille du disque cache**</span><span class="sxs-lookup"><span data-stu-id="13a3b-154">**Cache disk size**</span></span> | <span data-ttu-id="13a3b-155">**Taux de modification des données**</span><span class="sxs-lookup"><span data-stu-id="13a3b-155">**Data change rate**</span></span> | <span data-ttu-id="13a3b-156">**Machines protégées**</span><span class="sxs-lookup"><span data-stu-id="13a3b-156">**Protected machines**</span></span> |
| --- | --- | --- | --- |
|<span data-ttu-id="13a3b-157">4 processeurs virtuels (2 sockets * 2 cœurs @ 2,5 GHz), 8 Go de mémoire</span><span class="sxs-lookup"><span data-stu-id="13a3b-157">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8-GB memory</span></span> |<span data-ttu-id="13a3b-158">300 Go</span><span class="sxs-lookup"><span data-stu-id="13a3b-158">300 GB</span></span> |<span data-ttu-id="13a3b-159">250 Go ou moins</span><span class="sxs-lookup"><span data-stu-id="13a3b-159">250 GB or less</span></span> |<span data-ttu-id="13a3b-160">Répliquez 85 machines ou moins.</span><span class="sxs-lookup"><span data-stu-id="13a3b-160">Replicate 85 or less machines.</span></span> |
|<span data-ttu-id="13a3b-161">8 processeurs virtuels (2 sockets * 4 cœurs @ 2,5 GHz), 12 Go de mémoire</span><span class="sxs-lookup"><span data-stu-id="13a3b-161">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12-GB memory</span></span> |<span data-ttu-id="13a3b-162">600 Go</span><span class="sxs-lookup"><span data-stu-id="13a3b-162">600 GB</span></span> |<span data-ttu-id="13a3b-163">250 Go too1 to</span><span class="sxs-lookup"><span data-stu-id="13a3b-163">250 GB too1 TB</span></span> |<span data-ttu-id="13a3b-164">Répliquez entre 85 et 150 machines.</span><span class="sxs-lookup"><span data-stu-id="13a3b-164">Replicate between 85-150 machines.</span></span> |
|<span data-ttu-id="13a3b-165">12 processeurs virtuels (2 sockets * 6 cœurs @ 2,5 GHz), 24 Go de mémoire</span><span class="sxs-lookup"><span data-stu-id="13a3b-165">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24-GB memory</span></span> |<span data-ttu-id="13a3b-166">1 To</span><span class="sxs-lookup"><span data-stu-id="13a3b-166">1 TB</span></span> |<span data-ttu-id="13a3b-167">1 to too2 to</span><span class="sxs-lookup"><span data-stu-id="13a3b-167">1 TB too2 TB</span></span> |<span data-ttu-id="13a3b-168">Répliquez entre 150 et 225 machines.</span><span class="sxs-lookup"><span data-stu-id="13a3b-168">Replicate between 150-225 machines.</span></span> |
