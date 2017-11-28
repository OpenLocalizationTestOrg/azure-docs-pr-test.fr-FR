---
title: " Gérer un serveur de configuration dans Azure Site Recovery | Microsoft Docs"
description: "Cet article décrit comment tooset et gérer un serveur de Configuration."
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
ms.openlocfilehash: 2852bcd25409121be46a1ebf135ebfcdce6e5de5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-configuration-server"></a><span data-ttu-id="b168a-103">Gérer un serveur de configuration</span><span class="sxs-lookup"><span data-stu-id="b168a-103">Manage a Configuration Server</span></span>

<span data-ttu-id="b168a-104">Configuration serveur agit en tant que coordinateur entre les services de récupération de Site de hello et votre infrastructure locale.</span><span class="sxs-lookup"><span data-stu-id="b168a-104">Configuration Server acts as a coordinator between hello Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="b168a-105">Cet article décrit comment vous pouvez configurer, configurer et gérer hello serveur de Configuration.</span><span class="sxs-lookup"><span data-stu-id="b168a-105">This article describes how you can set up, configure, and manage hello Configuration Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b168a-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b168a-106">Prerequisites</span></span>
<span data-ttu-id="b168a-107">Hello Voici tooset configuration requise de réseau d’un serveur de Configuration, logicielle et matérielle hello.</span><span class="sxs-lookup"><span data-stu-id="b168a-107">hello following are hello minimum hardware, software, and network configuration required tooset up a Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="b168a-108">[Planification de la capacité](site-recovery-capacity-planner.md) est un tooensure étape importante déployer hello avec une configuration de serveur de Configuration qui convient le mieux vos exigences de charge.</span><span class="sxs-lookup"><span data-stu-id="b168a-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step tooensure that you deploy hello Configuration Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="b168a-109">Pour en savoir plus, consultez la section [Exigences de dimensionnement d’un serveur de configuration](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="b168a-109">Read more about [Sizing requirements for a Configuration Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-configuration-server-software"></a><span data-ttu-id="b168a-110">Téléchargement du logiciel de serveur de Configuration hello</span><span class="sxs-lookup"><span data-stu-id="b168a-110">Downloading hello Configuration Server software</span></span>
1. <span data-ttu-id="b168a-111">Ouvrez une session toohello tooyour portal et parcourir Azure coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="b168a-111">Log on toohello Azure portal and browse tooyour Recovery Services Vault.</span></span>
2. <span data-ttu-id="b168a-112">Parcourir trop**Infrastructure Site Recovery** > **serveurs de Configuration** (sous VMware pour les & ordinateurs physiques).</span><span class="sxs-lookup"><span data-stu-id="b168a-112">Browse too**Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>

  ![Page Ajouter des serveurs](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. <span data-ttu-id="b168a-114">Cliquez sur hello **+ serveurs** bouton.</span><span class="sxs-lookup"><span data-stu-id="b168a-114">Click hello **+Servers** button.</span></span>
4. <span data-ttu-id="b168a-115">Sur hello **ajouter un serveur** , cliquez sur la clé d’inscription de hello téléchargement bouton toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="b168a-115">On hello **Add Server** page, click hello Download button toodownload hello Registration key.</span></span> <span data-ttu-id="b168a-116">Vous avez besoin de cette clé pendant hello Configuration Server installation tooregister avec le service Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b168a-116">You need this key during hello Configuration Server installation tooregister it with Azure Site Recovery service.</span></span>
5. <span data-ttu-id="b168a-117">Cliquez sur hello **téléchargement hello installation unifié de Microsoft Azure Site Recovery** lien toodownload hello version la plus récente du serveur de Configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="b168a-117">Click hello **Download hello Microsoft Azure Site Recovery Unified Setup** link toodownload hello latest version of hello Configuration Server.</span></span>

  ![Page de téléchargement](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  <span data-ttu-id="b168a-119">Dernière version du serveur de Configuration de hello peut être téléchargée directement à partir de [page de téléchargement Microsoft Download Center](http://aka.ms/unifiedsetup)</span><span class="sxs-lookup"><span data-stu-id="b168a-119">Latest version of hello Configuration Server can be downloaded directly from [Microsoft Download Center download page](http://aka.ms/unifiedsetup)</span></span>

## <a name="installing-and-registering-a-configuration-server-from-gui"></a><span data-ttu-id="b168a-120">Installation et inscription d’un serveur de configuration à partir de l’interface graphique utilisateur</span><span class="sxs-lookup"><span data-stu-id="b168a-120">Installing and Registering a Configuration Server from GUI</span></span>
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a><span data-ttu-id="b168a-121">Installation et inscription d’un serveur de configuration à l’aide de la ligne de commande</span><span class="sxs-lookup"><span data-stu-id="b168a-121">Installing and registering a Configuration Server using Command line</span></span>

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a><span data-ttu-id="b168a-122">Exemple d’utilisation</span><span class="sxs-lookup"><span data-stu-id="b168a-122">Sample usage</span></span>
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a><span data-ttu-id="b168a-123">Arguments de la ligne de commande du programme d’installation du serveur de configuration</span><span class="sxs-lookup"><span data-stu-id="b168a-123">Configuration Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a><span data-ttu-id="b168a-124">Créer un fichier d’informations d’identification de MySql</span><span class="sxs-lookup"><span data-stu-id="b168a-124">Create a MySql credentials file</span></span>
<span data-ttu-id="b168a-125">Le paramètre MySQLCredsFilePath prend un fichier en tant qu’entrée.</span><span class="sxs-lookup"><span data-stu-id="b168a-125">MySQLCredsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="b168a-126">Créer un fichier hello à l’aide de hello suivante, mettre en forme et passez-le en tant que paramètre d’entrée de MySQLCredsFilePath.</span><span class="sxs-lookup"><span data-stu-id="b168a-126">Create hello file using hello following format and pass it as input MySQLCredsFilePath parameter.</span></span>
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="b168a-127">Créer un fichier de configuration des paramètres de proxy</span><span class="sxs-lookup"><span data-stu-id="b168a-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="b168a-128">Le paramètre ProxySettingsFilePath prend un fichier en tant qu’entrée.</span><span class="sxs-lookup"><span data-stu-id="b168a-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="b168a-129">Créer un fichier hello à l’aide de hello suivante, mettre en forme et passez-le en tant que paramètre d’entrée de ProxySettingsFilePath.</span><span class="sxs-lookup"><span data-stu-id="b168a-129">Create hello file using hello following format and pass it as input ProxySettingsFilePath parameter.</span></span>

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a><span data-ttu-id="b168a-130">Modification des paramètres de proxy du serveur de configuration</span><span class="sxs-lookup"><span data-stu-id="b168a-130">Modifying proxy settings for Configuration Server</span></span>
1. <span data-ttu-id="b168a-131">Connexion tooyour serveur de Configuration.</span><span class="sxs-lookup"><span data-stu-id="b168a-131">Login tooyour Configuration Server.</span></span>
2. <span data-ttu-id="b168a-132">Lancez cspsconfigtool.exe hello à l’aide du raccourci de hello sur votre.</span><span class="sxs-lookup"><span data-stu-id="b168a-132">Launch hello cspsconfigtool.exe using hello shortcut on your.</span></span>
3. <span data-ttu-id="b168a-133">Cliquez sur hello **inscription du coffre** onglet.</span><span class="sxs-lookup"><span data-stu-id="b168a-133">Click hello **Vault Registration** tab.</span></span>
4. <span data-ttu-id="b168a-134">Télécharger un nouveau fichier d’inscription du coffre à partir du portail de hello et fournit en tant qu’outil de toohello d’entrée.</span><span class="sxs-lookup"><span data-stu-id="b168a-134">Download a new Vault Registration file from hello portal and provide it as input toohello tool.</span></span>

  ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. <span data-ttu-id="b168a-136">Fournissez les détails du nouveau serveur Proxy de hello et cliquez sur hello **inscrire** bouton.</span><span class="sxs-lookup"><span data-stu-id="b168a-136">Provide hello new Proxy Server details and click hello **Register** button.</span></span>
6. <span data-ttu-id="b168a-137">Ouvrez une fenêtre de commandes PowerShell administrateur.</span><span class="sxs-lookup"><span data-stu-id="b168a-137">Open an Admin PowerShell command window.</span></span>
7. <span data-ttu-id="b168a-138">Exécutez hello commande suivante</span><span class="sxs-lookup"><span data-stu-id="b168a-138">Run hello following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  <span data-ttu-id="b168a-139">Si vous avez des serveurs de traitement de la montée en puissance parallèle attaché toothis serveur de Configuration, vous devez trop[corriger les paramètres de proxy hello sur tous les serveurs de processus de montée en puissance parallèle hello](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) dans votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="b168a-139">If you have Scale-out Process servers attached toothis Configuration Server, you need too[fix hello proxy settings on all hello scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) in your deployment.</span></span>

## <a name="re-register-a-configuration-server-with-hello-same-recovery-services-vault"></a><span data-ttu-id="b168a-140">Réinscrire sur un serveur de Configuration avec hello même coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="b168a-140">Re-register a Configuration Server with hello same Recovery Services Vault</span></span>
  1. <span data-ttu-id="b168a-141">Connexion tooyour serveur de Configuration.</span><span class="sxs-lookup"><span data-stu-id="b168a-141">Login tooyour Configuration Server.</span></span>
  2. <span data-ttu-id="b168a-142">Lancez cspsconfigtool.exe hello à l’aide du raccourci de hello sur votre bureau.</span><span class="sxs-lookup"><span data-stu-id="b168a-142">Launch hello cspsconfigtool.exe using hello shortcut on your desktop.</span></span>
  3. <span data-ttu-id="b168a-143">Cliquez sur hello **inscription du coffre** onglet.</span><span class="sxs-lookup"><span data-stu-id="b168a-143">Click hello **Vault Registration** tab.</span></span>
  4. <span data-ttu-id="b168a-144">Télécharger un nouveau fichier d’inscription à partir du portail de hello et fournit en tant qu’outil de toohello d’entrée.</span><span class="sxs-lookup"><span data-stu-id="b168a-144">Download a new Registration file from hello portal and provide it as input toohello tool.</span></span>
        <span data-ttu-id="b168a-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span><span class="sxs-lookup"><span data-stu-id="b168a-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span></span>
  5. <span data-ttu-id="b168a-146">Fournir des détails du serveur Proxy hello et cliquez sur hello **inscrire** bouton.</span><span class="sxs-lookup"><span data-stu-id="b168a-146">Provide hello Proxy Server details and click hello **Register** button.</span></span>  
  6. <span data-ttu-id="b168a-147">Ouvrez une fenêtre de commandes PowerShell administrateur.</span><span class="sxs-lookup"><span data-stu-id="b168a-147">Open an Admin PowerShell command window.</span></span>
  7. <span data-ttu-id="b168a-148">Exécutez hello commande suivante</span><span class="sxs-lookup"><span data-stu-id="b168a-148">Run hello following command</span></span>

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  <span data-ttu-id="b168a-149">Si vous avez des serveurs de traitement de la montée en puissance parallèle attaché toothis serveur de Configuration, vous devez trop[réinscrire tous les serveurs de traitement de montée en puissance parallèle de hello](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) dans votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="b168a-149">If you have Scale-out Process servers attached toothis Configuration Server, you need too[re-register all hello scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) in your deployment.</span></span>

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a><span data-ttu-id="b168a-150">Inscription d’un serveur de configuration auprès d’un autre coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="b168a-150">Registering a Configuration Server with a different Recovery Services Vault.</span></span>
1. <span data-ttu-id="b168a-151">Connexion tooyour serveur de Configuration.</span><span class="sxs-lookup"><span data-stu-id="b168a-151">Login tooyour Configuration Server.</span></span>
2. <span data-ttu-id="b168a-152">à partir d’une invite de commandes administrateur, exécutez la commande hello</span><span class="sxs-lookup"><span data-stu-id="b168a-152">from an admin command prompt, run hello command</span></span>

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. <span data-ttu-id="b168a-153">Lancez cspsconfigtool.exe hello à l’aide du raccourci de hello sur votre.</span><span class="sxs-lookup"><span data-stu-id="b168a-153">Launch hello cspsconfigtool.exe using hello shortcut on your.</span></span>
4. <span data-ttu-id="b168a-154">Cliquez sur hello **inscription du coffre** onglet.</span><span class="sxs-lookup"><span data-stu-id="b168a-154">Click hello **Vault Registration** tab.</span></span>
5. <span data-ttu-id="b168a-155">Télécharger un nouveau fichier d’inscription à partir du portail de hello et fournit en tant qu’outil de toohello d’entrée.</span><span class="sxs-lookup"><span data-stu-id="b168a-155">Download a new Registration file from hello portal and provide it as input toohello tool.</span></span>

    ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. <span data-ttu-id="b168a-157">Fournir des détails du serveur Proxy hello et cliquez sur hello **inscrire** bouton.</span><span class="sxs-lookup"><span data-stu-id="b168a-157">Provide hello Proxy Server details and click hello **Register** button.</span></span>  
7. <span data-ttu-id="b168a-158">Ouvrez une fenêtre de commandes PowerShell administrateur.</span><span class="sxs-lookup"><span data-stu-id="b168a-158">Open an Admin PowerShell command window.</span></span>
8. <span data-ttu-id="b168a-159">Exécutez hello commande suivante</span><span class="sxs-lookup"><span data-stu-id="b168a-159">Run hello following command</span></span>
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a><span data-ttu-id="b168a-160">Désaffectation d’un serveur de configuration</span><span class="sxs-lookup"><span data-stu-id="b168a-160">Decommissioning a Configuration Server</span></span>
<span data-ttu-id="b168a-161">Vérifiez les éléments suivants de hello avant de commencer la mise hors service de votre serveur de Configuration.</span><span class="sxs-lookup"><span data-stu-id="b168a-161">Ensure hello following before you start decommissioning your Configuration Server.</span></span>
1. <span data-ttu-id="b168a-162">Désactivez la protection de toutes les machines virtuelles relevant de ce serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="b168a-162">Disable protection for all virtual machines under this Configuration Server.</span></span>
2. <span data-ttu-id="b168a-163">Dissociez toutes les stratégies de réplication à partir de hello serveur de Configuration.</span><span class="sxs-lookup"><span data-stu-id="b168a-163">Disassociate all Replication policies from hello Configuration Server.</span></span>
3. <span data-ttu-id="b168a-164">Supprimer tous les hôtes de serveurs/vSphere vCenter qui sont associé toohello serveur de Configuration.</span><span class="sxs-lookup"><span data-stu-id="b168a-164">Delete all vCenters servers/vSphere hosts that are associated toohello Configuration Server.</span></span>

### <a name="delete-hello-configuration-server-from-azure-portal"></a><span data-ttu-id="b168a-165">Supprimer hello serveur de Configuration à partir du portail Azure</span><span class="sxs-lookup"><span data-stu-id="b168a-165">Delete hello Configuration Server from Azure portal</span></span>
1. <span data-ttu-id="b168a-166">Dans le portail Azure, accédez trop**Infrastructure Site Recovery** > **serveurs de Configuration** à partir du menu de coffre hello.</span><span class="sxs-lookup"><span data-stu-id="b168a-166">In Azure portal, browse too**Site Recovery Infrastructure** > **Configuration Servers** from hello Vault menu.</span></span>
2. <span data-ttu-id="b168a-167">Cliquez sur hello serveur de Configuration que vous souhaitez toodecommission.</span><span class="sxs-lookup"><span data-stu-id="b168a-167">Click hello Configuration Server that you want toodecommission.</span></span>
3. <span data-ttu-id="b168a-168">Dans la page des détails du serveur de Configuration hello, cliquez sur Supprimer hello.</span><span class="sxs-lookup"><span data-stu-id="b168a-168">On hello Configuration Server's details page, click hello Delete button.</span></span>

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. <span data-ttu-id="b168a-170">Cliquez sur **Oui** tooconfirm la suppression hello du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="b168a-170">Click **Yes** tooconfirm hello deletion of hello server.</span></span>

  >[!WARNING]
  <span data-ttu-id="b168a-171">Si vous disposez d’ordinateurs virtuels, les stratégies de réplication ou les hôtes de serveurs/vSphere vCenter associés à ce serveur de Configuration, vous ne pouvez pas supprimer les serveur hello.</span><span class="sxs-lookup"><span data-stu-id="b168a-171">If you have any virtual machines, Replication policies or vCenter servers/vSphere hosts associated with this Configuration Server, you cannot delete hello server.</span></span> <span data-ttu-id="b168a-172">Supprimer ces entités avant d’essayer de coffre de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="b168a-172">Delete these entities before you try toodelete hello vault.</span></span>

### <a name="uninstall-hello-configuration-server-software-and-its-dependencies"></a><span data-ttu-id="b168a-173">Désinstaller le logiciel de serveur de Configuration hello et ses dépendances</span><span class="sxs-lookup"><span data-stu-id="b168a-173">Uninstall hello Configuration Server software and its dependencies</span></span>
  > [!TIP]
  <span data-ttu-id="b168a-174">Si vous envisagez de nouveau tooreuse hello serveur de Configuration avec Azure Site Recovery, vous pouvez ignorer toostep 4 directement</span><span class="sxs-lookup"><span data-stu-id="b168a-174">If you plan tooreuse hello Configuration Server with Azure Site Recovery again, then you can skip toostep 4 directly</span></span>

1. <span data-ttu-id="b168a-175">Ouvrez une session sur le serveur de Configuration de toohello en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="b168a-175">Log on toohello Configuration Server as an Administrator.</span></span>
2. <span data-ttu-id="b168a-176">Ouvrez le Panneau de configuration > Programme > Désinstaller des programmes</span><span class="sxs-lookup"><span data-stu-id="b168a-176">Open up Control Panel > Program > Uninstall Programs</span></span>
3. <span data-ttu-id="b168a-177">Désinstaller des programmes hello Bonjour suivant séquence :</span><span class="sxs-lookup"><span data-stu-id="b168a-177">Uninstall hello programs in hello following sequence:</span></span>
  * <span data-ttu-id="b168a-178">Agent Microsoft Azure Recovery Services</span><span class="sxs-lookup"><span data-stu-id="b168a-178">Microsoft Azure Recovery Services Agent</span></span>
  * <span data-ttu-id="b168a-179">Service Mobilité/Serveur cible maître Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="b168a-179">Microsoft Azure Site Recovery Mobility Service/Master Target server</span></span>
  * <span data-ttu-id="b168a-180">Fournisseur Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="b168a-180">Microsoft Azure Site Recovery Provider</span></span>
  * <span data-ttu-id="b168a-181">Serveur de configuration/Serveur de processus Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="b168a-181">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="b168a-182">Dépendances du serveur de configuration Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="b168a-182">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="b168a-183">MySQL Server 5.5</span><span class="sxs-lookup"><span data-stu-id="b168a-183">MySQL Server 5.5</span></span>
4. <span data-ttu-id="b168a-184">Exécutez hello suivant de commande à partir d’et invite de commandes d’administration.</span><span class="sxs-lookup"><span data-stu-id="b168a-184">Run hello following command from and admin command prompt.</span></span>
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a><span data-ttu-id="b168a-185">Renouveler les certificats SSL du serveur de configuration</span><span class="sxs-lookup"><span data-stu-id="b168a-185">Renew Configuration Server Secure Socket Layer(SSL) Certificates</span></span>
<span data-ttu-id="b168a-186">Hello Configuration serveur possède un serveur Web intégré, qui orchestre les activités hello Hello Service mobilité, serveurs de traitement, et serveurs cibles maîtres connecté toohello serveur de Configuration.</span><span class="sxs-lookup"><span data-stu-id="b168a-186">hello Configuration Server has an inbuilt webserver, which orchestrates hello activities of hello Mobility Service, Process Servers, and Master Target servers connected toohello Configuration Server.</span></span> <span data-ttu-id="b168a-187">serveur Web du serveur de Configuration Hello utilise un tooauthenticate du certificat SSL à ses clients.</span><span class="sxs-lookup"><span data-stu-id="b168a-187">hello Configuration Server's webserver uses an SSL certificate tooauthenticate its clients.</span></span> <span data-ttu-id="b168a-188">Ce certificat a un délai d’expiration de trois ans et peut être renouvelé à tout moment à l’aide de hello suivant de méthode :</span><span class="sxs-lookup"><span data-stu-id="b168a-188">This certificate has an expiry of three years and can be renewed at any time using hello following method:</span></span>

> [!WARNING]
<span data-ttu-id="b168a-189">L’expiration du certificat peut être appliquée uniquement sur les versions 9.4.XXXX.X ou supérieures.</span><span class="sxs-lookup"><span data-stu-id="b168a-189">Certificate expiry can be performed only on version 9.4.XXXX.X or higher.</span></span> <span data-ttu-id="b168a-190">Mettre à niveau tous les composants d’Azure Site Recovery hello (serveur de Configuration, serveur de processus, serveur cible maître, Service mobilité) avant de démarrer le flux de travail hello renouveler les certificats.</span><span class="sxs-lookup"><span data-stu-id="b168a-190">Upgrade all hello Azure Site Recovery components (Configuration Server, Process Server, Master Target Server, Mobility Service) before you start hello Renew Certificates workflow.</span></span>

1. <span data-ttu-id="b168a-191">On hello portail Azure, accédez tooyour coffre > Infrastructure Site Recovery > serveur de Configuration.</span><span class="sxs-lookup"><span data-stu-id="b168a-191">On hello Azure portal, browse tooyour Vault > Site Recovery Infrastructure > Configuration Server.</span></span>
2. <span data-ttu-id="b168a-192">Cliquez sur le serveur de Configuration pour lesquels vous avez besoin toorenew hello hello certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="b168a-192">Click hello Configuration Server for which you need toorenew hello SSL Certificate for.</span></span>
3. <span data-ttu-id="b168a-193">Sous hello l’intégrité du serveur de Configuration, vous pouvez voir la date d’expiration hello pour hello certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="b168a-193">Under hello Configuration Server health, you can see hello expiry date for hello SSL Certificate.</span></span>
4. <span data-ttu-id="b168a-194">Renouveler les certificats de hello en cliquant sur hello **renouveler les certificats** action, comme indiqué dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="b168a-194">Renew hello certificate by clicking hello **Renew Certificates** action as shown in hello following image:</span></span>

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a><span data-ttu-id="b168a-196">Avertissement relatif à l’expiration du certificat SSL</span><span class="sxs-lookup"><span data-stu-id="b168a-196">Secure Socket Layer certificate expiry warning</span></span>

> [!NOTE]
<span data-ttu-id="b168a-197">Hello validité du certificat SSL pour toutes les installations qui ont eu lieu avant mai 2016 a été définie tooone année.</span><span class="sxs-lookup"><span data-stu-id="b168a-197">hello SSL Certificate's validity for all installations that happened before May 2016 was set tooone year.</span></span> <span data-ttu-id="b168a-198">vous avez démarré l’affichage des notifications d’expiration de certificat s’affiche dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b168a-198">you have started seeing certificate expiry notifications showing up in hello Azure portal.</span></span>

1. <span data-ttu-id="b168a-199">Si le certificat SSL du serveur de Configuration hello va tooexpire Bonjour deux mois, service de hello démarre la notification des utilisateurs via le portail Azure Bonjour par courrier électronique (vous devez toobe abonné tooAzure Site Recovery notifications).</span><span class="sxs-lookup"><span data-stu-id="b168a-199">If hello Configuration Server's SSL certificate is going tooexpire in hello next two months, hello service starts notifying users via hello Azure portal & email (you need toobe subscribed tooAzure Site Recovery notifications).</span></span> <span data-ttu-id="b168a-200">Commencer à voir une bannière de notification sur la page de ressource du coffre hello.</span><span class="sxs-lookup"><span data-stu-id="b168a-200">You start seeing a notification banner on hello Vault's resource page.</span></span>

  ![certificate-notification](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. <span data-ttu-id="b168a-202">Cliquez sur hello bannière tooget plus d’informations sur l’expiration du certificat hello.</span><span class="sxs-lookup"><span data-stu-id="b168a-202">Click hello banner tooget additional details on hello Certificate expiry.</span></span>

  ![certificate-details](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  <span data-ttu-id="b168a-204">Si un bouton **Mettre à niveau maintenant** s’affiche à la place d’un bouton **Renouveler maintenant**,</span><span class="sxs-lookup"><span data-stu-id="b168a-204">If instead of a **Renew Now** button you see an **Upgrade Now** button.</span></span> <span data-ttu-id="b168a-205">Cela signifie qu’il n’y a certains composants de votre environnement qui n’ont pas encore été mis à niveau too9.4.xxxx.x ou versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="b168a-205">This means that there are some components in your environment that have not yet been upgraded too9.4.xxxx.x or higher versions.</span></span>

## <a name="sizing-requirements-for-a-configuration-server"></a><span data-ttu-id="b168a-206">Exigences de dimensionnement d’un serveur de configuration</span><span class="sxs-lookup"><span data-stu-id="b168a-206">Sizing requirements for a Configuration Server</span></span>

| <span data-ttu-id="b168a-207">**UC**</span><span class="sxs-lookup"><span data-stu-id="b168a-207">**CPU**</span></span> | <span data-ttu-id="b168a-208">**Mémoire**</span><span class="sxs-lookup"><span data-stu-id="b168a-208">**Memory**</span></span> | <span data-ttu-id="b168a-209">**Taille du disque cache**</span><span class="sxs-lookup"><span data-stu-id="b168a-209">**Cache disk size**</span></span> | <span data-ttu-id="b168a-210">**Taux de modification des données**</span><span class="sxs-lookup"><span data-stu-id="b168a-210">**Data change rate**</span></span> | <span data-ttu-id="b168a-211">**Machines protégées**</span><span class="sxs-lookup"><span data-stu-id="b168a-211">**Protected machines**</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="b168a-212">8 processeurs virtuels (2 sockets * 4 cœurs à 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="b168a-212">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="b168a-213">16 Go</span><span class="sxs-lookup"><span data-stu-id="b168a-213">16 GB</span></span> |<span data-ttu-id="b168a-214">300 Go</span><span class="sxs-lookup"><span data-stu-id="b168a-214">300 GB</span></span> |<span data-ttu-id="b168a-215">500 Go ou moins</span><span class="sxs-lookup"><span data-stu-id="b168a-215">500 GB or less</span></span> |<span data-ttu-id="b168a-216">Répliquez moins de 100 machines.</span><span class="sxs-lookup"><span data-stu-id="b168a-216">Replicate fewer than 100 machines.</span></span> |
| <span data-ttu-id="b168a-217">12 processeurs virtuels (2 sockets * 6 cœurs à 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="b168a-217">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="b168a-218">18 Go</span><span class="sxs-lookup"><span data-stu-id="b168a-218">18 GB</span></span> |<span data-ttu-id="b168a-219">600 Go</span><span class="sxs-lookup"><span data-stu-id="b168a-219">600 GB</span></span> |<span data-ttu-id="b168a-220">500 Go too1 to</span><span class="sxs-lookup"><span data-stu-id="b168a-220">500 GB too1 TB</span></span> |<span data-ttu-id="b168a-221">Répliquez entre 100 et 150 machines.</span><span class="sxs-lookup"><span data-stu-id="b168a-221">Replicate between 100-150 machines.</span></span> |
| <span data-ttu-id="b168a-222">16 processeurs virtuels (2 sockets * 8 cœurs à 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="b168a-222">16 vCPUs (2 sockets * 8 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="b168a-223">32 Go</span><span class="sxs-lookup"><span data-stu-id="b168a-223">32 GB</span></span> |<span data-ttu-id="b168a-224">1 To</span><span class="sxs-lookup"><span data-stu-id="b168a-224">1 TB</span></span> |<span data-ttu-id="b168a-225">1 to too2 to</span><span class="sxs-lookup"><span data-stu-id="b168a-225">1 TB too2 TB</span></span> |<span data-ttu-id="b168a-226">Répliquez entre 150 et 200 machines.</span><span class="sxs-lookup"><span data-stu-id="b168a-226">Replicate between 150-200 machines.</span></span> |

  >[!TIP]
  <span data-ttu-id="b168a-227">Si vos données quotidiennes pendant dépasse 2 To, ou vous envisagez de tooreplicate plus de 200 machines virtuelles, il est recommandé de toodeploy processus supplémentaire serveurs tooload solde hello le trafic de réplication.</span><span class="sxs-lookup"><span data-stu-id="b168a-227">If your daily data churn exceeds 2 TB, or you plan tooreplicate more than 200 virtual machines, it is recommended toodeploy additional process servers tooload balance hello replication traffic.</span></span> <span data-ttu-id="b168a-228">Découvrez comment les serveurs de toodeploy processus de montée en puissance parallèle.</span><span class="sxs-lookup"><span data-stu-id="b168a-228">Learn more about How toodeploy Scale-out Process severs.</span></span>


## <a name="common-issues"></a><span data-ttu-id="b168a-229">Problèmes courants</span><span class="sxs-lookup"><span data-stu-id="b168a-229">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
