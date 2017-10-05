---
title: " Gérer un serveur de configuration dans Azure Site Recovery | Microsoft Docs"
description: "Cet article explique comment définir et gérer un serveur de configuration."
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
ms.openlocfilehash: 36da8c7d0f3ace194522e5288f26069cf46d470e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-configuration-server"></a><span data-ttu-id="37c42-103">Gérer un serveur de configuration</span><span class="sxs-lookup"><span data-stu-id="37c42-103">Manage a Configuration Server</span></span>

<span data-ttu-id="37c42-104">Le serveur de configuration fait office de coordinateur entre les services Site Recovery et votre infrastructure locale.</span><span class="sxs-lookup"><span data-stu-id="37c42-104">Configuration Server acts as a coordinator between the Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="37c42-105">Cet article explique comment configurer et gérer le serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="37c42-105">This article describes how you can set up, configure, and manage the Configuration Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37c42-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="37c42-106">Prerequisites</span></span>
<span data-ttu-id="37c42-107">Vous trouverez ci-dessous des informations sur la configuration minimale requise pour le matériel, le logiciel et le réseau pour configurer un serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="37c42-107">The following are the minimum hardware, software, and network configuration required to set up a Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="37c42-108">La [planification de la capacité](site-recovery-capacity-planner.md) est une étape importante pour vous assurer de déployer le serveur de configuration avec une configuration répondant à vos exigences de charge.</span><span class="sxs-lookup"><span data-stu-id="37c42-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step to ensure that you deploy the Configuration Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="37c42-109">Pour en savoir plus, consultez la section [Exigences de dimensionnement d’un serveur de configuration](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="37c42-109">Read more about [Sizing requirements for a Configuration Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-the-configuration-server-software"></a><span data-ttu-id="37c42-110">Téléchargement du logiciel serveur de configuration</span><span class="sxs-lookup"><span data-stu-id="37c42-110">Downloading the Configuration Server software</span></span>
1. <span data-ttu-id="37c42-111">Connectez-vous au portail Azure et accédez à votre coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="37c42-111">Log on to the Azure portal and browse to your Recovery Services Vault.</span></span>
2. <span data-ttu-id="37c42-112">Sélectionnez **Infrastructure Site Recovery** > **Serveurs de configuration** (sous For VMware & Physical Machines [Pour VMware et machines physiques]).</span><span class="sxs-lookup"><span data-stu-id="37c42-112">Browse to **Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>

  ![Page Ajouter des serveurs](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. <span data-ttu-id="37c42-114">Cliquez sur le bouton **+Serveurs**.</span><span class="sxs-lookup"><span data-stu-id="37c42-114">Click the **+Servers** button.</span></span>
4. <span data-ttu-id="37c42-115">Dans la page **Ajouter un serveur** , cliquez sur le bouton Télécharger pour télécharger la clé d’inscription.</span><span class="sxs-lookup"><span data-stu-id="37c42-115">On the **Add Server** page, click the Download button to download the Registration key.</span></span> <span data-ttu-id="37c42-116">Vous avez besoin de cette clé pendant l’installation du serveur de configuration pour l’inscrire auprès du service Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="37c42-116">You need this key during the Configuration Server installation to register it with Azure Site Recovery service.</span></span>
5. <span data-ttu-id="37c42-117">Cliquez sur le lien **Download the Microsoft Azure Site Recovery Unified Setup (Télécharger le programme d’installation unifiée de Microsoft Azure Site Recovery)** pour télécharger la dernière version du serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="37c42-117">Click the **Download the Microsoft Azure Site Recovery Unified Setup** link to download the latest version of the Configuration Server.</span></span>

  ![Page de téléchargement](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  <span data-ttu-id="37c42-119">La dernière version du serveur de configuration peut être téléchargée directement à partir de la [page de téléchargement du Centre de téléchargement Microsoft](http://aka.ms/unifiedsetup).</span><span class="sxs-lookup"><span data-stu-id="37c42-119">Latest version of the Configuration Server can be downloaded directly from [Microsoft Download Center download page](http://aka.ms/unifiedsetup)</span></span>

## <a name="installing-and-registering-a-configuration-server-from-gui"></a><span data-ttu-id="37c42-120">Installation et inscription d’un serveur de configuration à partir de l’interface graphique utilisateur</span><span class="sxs-lookup"><span data-stu-id="37c42-120">Installing and Registering a Configuration Server from GUI</span></span>
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a><span data-ttu-id="37c42-121">Installation et inscription d’un serveur de configuration à l’aide de la ligne de commande</span><span class="sxs-lookup"><span data-stu-id="37c42-121">Installing and registering a Configuration Server using Command line</span></span>

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a><span data-ttu-id="37c42-122">Exemple d’utilisation</span><span class="sxs-lookup"><span data-stu-id="37c42-122">Sample usage</span></span>
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a><span data-ttu-id="37c42-123">Arguments de la ligne de commande du programme d’installation du serveur de configuration</span><span class="sxs-lookup"><span data-stu-id="37c42-123">Configuration Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a><span data-ttu-id="37c42-124">Créer un fichier d’informations d’identification de MySql</span><span class="sxs-lookup"><span data-stu-id="37c42-124">Create a MySql credentials file</span></span>
<span data-ttu-id="37c42-125">Le paramètre MySQLCredsFilePath prend un fichier en tant qu’entrée.</span><span class="sxs-lookup"><span data-stu-id="37c42-125">MySQLCredsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="37c42-126">Créez le fichier au format suivant et transmettez-le comme paramètre MySQLCredsFilePath d’entrée.</span><span class="sxs-lookup"><span data-stu-id="37c42-126">Create the file using the following format and pass it as input MySQLCredsFilePath parameter.</span></span>
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="37c42-127">Créer un fichier de configuration des paramètres de proxy</span><span class="sxs-lookup"><span data-stu-id="37c42-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="37c42-128">Le paramètre ProxySettingsFilePath prend un fichier en tant qu’entrée.</span><span class="sxs-lookup"><span data-stu-id="37c42-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="37c42-129">Créez le fichier au format suivant et transmettez-le comme paramètre ProxySettingsFilePath d’entrée.</span><span class="sxs-lookup"><span data-stu-id="37c42-129">Create the file using the following format and pass it as input ProxySettingsFilePath parameter.</span></span>

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a><span data-ttu-id="37c42-130">Modification des paramètres de proxy du serveur de configuration</span><span class="sxs-lookup"><span data-stu-id="37c42-130">Modifying proxy settings for Configuration Server</span></span>
1. <span data-ttu-id="37c42-131">Connectez-vous à votre serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="37c42-131">Login to your Configuration Server.</span></span>
2. <span data-ttu-id="37c42-132">Lancez l’exécutable cspsconfigtool.exe à l’aide du raccourci sur votre serveur.</span><span class="sxs-lookup"><span data-stu-id="37c42-132">Launch the cspsconfigtool.exe using the shortcut on your.</span></span>
3. <span data-ttu-id="37c42-133">Cliquez sur l’onglet **Vault Registration (Inscription du coffre)**.</span><span class="sxs-lookup"><span data-stu-id="37c42-133">Click the **Vault Registration** tab.</span></span>
4. <span data-ttu-id="37c42-134">Téléchargez un nouveau fichier d’inscription du coffre à partir du portail et indiquez-le comme entrée de l’outil.</span><span class="sxs-lookup"><span data-stu-id="37c42-134">Download a new Vault Registration file from the portal and provide it as input to the tool.</span></span>

  ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. <span data-ttu-id="37c42-136">Indiquez les détails du nouveau serveur proxy, puis cliquez sur le bouton **Inscrire**.</span><span class="sxs-lookup"><span data-stu-id="37c42-136">Provide the new Proxy Server details and click the **Register** button.</span></span>
6. <span data-ttu-id="37c42-137">Ouvrez une fenêtre de commandes PowerShell administrateur.</span><span class="sxs-lookup"><span data-stu-id="37c42-137">Open an Admin PowerShell command window.</span></span>
7. <span data-ttu-id="37c42-138">Exécutez la commande suivante</span><span class="sxs-lookup"><span data-stu-id="37c42-138">Run the following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  <span data-ttu-id="37c42-139">Si vous avez attaché des serveurs de processus de montée en puissance parallèle à ce serveur de configuration, vous devez [corriger les paramètres de proxy sur tous les serveurs de processus de montée en puissance parallèle](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) de votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="37c42-139">If you have Scale-out Process servers attached to this Configuration Server, you need to [fix the proxy settings on all the scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) in your deployment.</span></span>

## <a name="re-register-a-configuration-server-with-the-same-recovery-services-vault"></a><span data-ttu-id="37c42-140">Réinscription d’un serveur de configuration auprès du même coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="37c42-140">Re-register a Configuration Server with the same Recovery Services Vault</span></span>
  1. <span data-ttu-id="37c42-141">Connectez-vous à votre serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="37c42-141">Login to your Configuration Server.</span></span>
  2. <span data-ttu-id="37c42-142">Lancez l’exécutable cspsconfigtool.exe à l’aide du raccourci sur votre bureau.</span><span class="sxs-lookup"><span data-stu-id="37c42-142">Launch the cspsconfigtool.exe using the shortcut on your desktop.</span></span>
  3. <span data-ttu-id="37c42-143">Cliquez sur l’onglet **Vault Registration (Inscription du coffre)**.</span><span class="sxs-lookup"><span data-stu-id="37c42-143">Click the **Vault Registration** tab.</span></span>
  4. <span data-ttu-id="37c42-144">Téléchargez un nouveau fichier d’inscription à partir du portail et indiquez-le comme entrée de l’outil.</span><span class="sxs-lookup"><span data-stu-id="37c42-144">Download a new Registration file from the portal and provide it as input to the tool.</span></span>
        <span data-ttu-id="37c42-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span><span class="sxs-lookup"><span data-stu-id="37c42-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span></span>
  5. <span data-ttu-id="37c42-146">Indiquez les détails du serveur proxy, puis cliquez sur le bouton **Inscrire**.</span><span class="sxs-lookup"><span data-stu-id="37c42-146">Provide the Proxy Server details and click the **Register** button.</span></span>  
  6. <span data-ttu-id="37c42-147">Ouvrez une fenêtre de commandes PowerShell administrateur.</span><span class="sxs-lookup"><span data-stu-id="37c42-147">Open an Admin PowerShell command window.</span></span>
  7. <span data-ttu-id="37c42-148">Exécutez la commande suivante</span><span class="sxs-lookup"><span data-stu-id="37c42-148">Run the following command</span></span>

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  <span data-ttu-id="37c42-149">Si vous avez attaché des serveurs de processus de montée en puissance parallèle à ce serveur de configuration, vous devez [réinscrire tous les serveurs de processus de montée en puissance parallèle](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) de votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="37c42-149">If you have Scale-out Process servers attached to this Configuration Server, you need to [re-register all the scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) in your deployment.</span></span>

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a><span data-ttu-id="37c42-150">Inscription d’un serveur de configuration auprès d’un autre coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="37c42-150">Registering a Configuration Server with a different Recovery Services Vault.</span></span>
1. <span data-ttu-id="37c42-151">Connectez-vous à votre serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="37c42-151">Login to your Configuration Server.</span></span>
2. <span data-ttu-id="37c42-152">À partir d’une invite de commandes d’administration, exécutez la commande indiquée ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="37c42-152">from an admin command prompt, run the command</span></span>

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. <span data-ttu-id="37c42-153">Lancez l’exécutable cspsconfigtool.exe à l’aide du raccourci sur votre serveur.</span><span class="sxs-lookup"><span data-stu-id="37c42-153">Launch the cspsconfigtool.exe using the shortcut on your.</span></span>
4. <span data-ttu-id="37c42-154">Cliquez sur l’onglet **Vault Registration (Inscription du coffre)**.</span><span class="sxs-lookup"><span data-stu-id="37c42-154">Click the **Vault Registration** tab.</span></span>
5. <span data-ttu-id="37c42-155">Téléchargez un nouveau fichier d’inscription à partir du portail et indiquez-le comme entrée de l’outil.</span><span class="sxs-lookup"><span data-stu-id="37c42-155">Download a new Registration file from the portal and provide it as input to the tool.</span></span>

    ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. <span data-ttu-id="37c42-157">Indiquez les détails du serveur proxy, puis cliquez sur le bouton **Inscrire**.</span><span class="sxs-lookup"><span data-stu-id="37c42-157">Provide the Proxy Server details and click the **Register** button.</span></span>  
7. <span data-ttu-id="37c42-158">Ouvrez une fenêtre de commandes PowerShell administrateur.</span><span class="sxs-lookup"><span data-stu-id="37c42-158">Open an Admin PowerShell command window.</span></span>
8. <span data-ttu-id="37c42-159">Exécutez la commande suivante</span><span class="sxs-lookup"><span data-stu-id="37c42-159">Run the following command</span></span>
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a><span data-ttu-id="37c42-160">Désaffectation d’un serveur de configuration</span><span class="sxs-lookup"><span data-stu-id="37c42-160">Decommissioning a Configuration Server</span></span>
<span data-ttu-id="37c42-161">Effectuez les opérations suivantes avant de désaffecter votre serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="37c42-161">Ensure the following before you start decommissioning your Configuration Server.</span></span>
1. <span data-ttu-id="37c42-162">Désactivez la protection de toutes les machines virtuelles relevant de ce serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="37c42-162">Disable protection for all virtual machines under this Configuration Server.</span></span>
2. <span data-ttu-id="37c42-163">Dissociez toutes les stratégies de réplication du serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="37c42-163">Disassociate all Replication policies from the Configuration Server.</span></span>
3. <span data-ttu-id="37c42-164">Supprimez tous les serveurs vCenter/hôtes vSphere associés au serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="37c42-164">Delete all vCenters servers/vSphere hosts that are associated to the Configuration Server.</span></span>

### <a name="delete-the-configuration-server-from-azure-portal"></a><span data-ttu-id="37c42-165">Supprimer le serveur de configuration du portail Azure</span><span class="sxs-lookup"><span data-stu-id="37c42-165">Delete the Configuration Server from Azure portal</span></span>
1. <span data-ttu-id="37c42-166">Dans le portail Azure, sélectionnez **Infrastructure Site Recovery** > **Serveurs de configuration** dans le menu Coffre.</span><span class="sxs-lookup"><span data-stu-id="37c42-166">In Azure portal, browse to **Site Recovery Infrastructure** > **Configuration Servers** from the Vault menu.</span></span>
2. <span data-ttu-id="37c42-167">Cliquez sur le serveur de configuration que vous souhaitez désaffecter.</span><span class="sxs-lookup"><span data-stu-id="37c42-167">Click the Configuration Server that you want to decommission.</span></span>
3. <span data-ttu-id="37c42-168">Dans la page des détails du serveur de configuration, cliquez sur le bouton Supprimer.</span><span class="sxs-lookup"><span data-stu-id="37c42-168">On the Configuration Server's details page, click the Delete button.</span></span>

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. <span data-ttu-id="37c42-170">Cliquez sur **Oui** pour confirmer la suppression du serveur.</span><span class="sxs-lookup"><span data-stu-id="37c42-170">Click **Yes** to confirm the deletion of the server.</span></span>

  >[!WARNING]
  <span data-ttu-id="37c42-171">Si vous disposez de machines virtuelles, de stratégies de réplication ou de serveurs vCenter/hôtes vSphere associés à ce serveur de configuration, vous ne pouvez pas supprimer le serveur.</span><span class="sxs-lookup"><span data-stu-id="37c42-171">If you have any virtual machines, Replication policies or vCenter servers/vSphere hosts associated with this Configuration Server, you cannot delete the server.</span></span> <span data-ttu-id="37c42-172">Supprimez ces entités avant d’essayer de supprimer le coffre.</span><span class="sxs-lookup"><span data-stu-id="37c42-172">Delete these entities before you try to delete the vault.</span></span>

### <a name="uninstall-the-configuration-server-software-and-its-dependencies"></a><span data-ttu-id="37c42-173">Désinstaller le logiciel serveur de configuration et ses dépendances</span><span class="sxs-lookup"><span data-stu-id="37c42-173">Uninstall the Configuration Server software and its dependencies</span></span>
  > [!TIP]
  <span data-ttu-id="37c42-174">Si vous envisagez de réutiliser le serveur de configuration avec Azure Site Recovery, vous pouvez passer directement à l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="37c42-174">If you plan to reuse the Configuration Server with Azure Site Recovery again, then you can skip to step 4 directly</span></span>

1. <span data-ttu-id="37c42-175">Connectez-vous au serveur de configuration en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="37c42-175">Log on to the Configuration Server as an Administrator.</span></span>
2. <span data-ttu-id="37c42-176">Ouvrez le Panneau de configuration > Programme > Désinstaller des programmes.</span><span class="sxs-lookup"><span data-stu-id="37c42-176">Open up Control Panel > Program > Uninstall Programs</span></span>
3. <span data-ttu-id="37c42-177">Désinstallez les programmes dans la séquence suivante :</span><span class="sxs-lookup"><span data-stu-id="37c42-177">Uninstall the programs in the following sequence:</span></span>
  * <span data-ttu-id="37c42-178">Agent Microsoft Azure Recovery Services</span><span class="sxs-lookup"><span data-stu-id="37c42-178">Microsoft Azure Recovery Services Agent</span></span>
  * <span data-ttu-id="37c42-179">Service Mobilité/Serveur cible maître Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="37c42-179">Microsoft Azure Site Recovery Mobility Service/Master Target server</span></span>
  * <span data-ttu-id="37c42-180">Fournisseur Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="37c42-180">Microsoft Azure Site Recovery Provider</span></span>
  * <span data-ttu-id="37c42-181">Serveur de configuration/Serveur de processus Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="37c42-181">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="37c42-182">Dépendances du serveur de configuration Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="37c42-182">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="37c42-183">MySQL Server 5.5</span><span class="sxs-lookup"><span data-stu-id="37c42-183">MySQL Server 5.5</span></span>
4. <span data-ttu-id="37c42-184">Exécutez la commande suivante à partir d’une invite de commandes d’administration :</span><span class="sxs-lookup"><span data-stu-id="37c42-184">Run the following command from and admin command prompt.</span></span>
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a><span data-ttu-id="37c42-185">Renouveler les certificats SSL du serveur de configuration</span><span class="sxs-lookup"><span data-stu-id="37c42-185">Renew Configuration Server Secure Socket Layer(SSL) Certificates</span></span>
<span data-ttu-id="37c42-186">Le serveur de configuration possède un serveur web intégré, qui orchestre les activités du service Mobilité, des serveurs de processus et des serveurs maîtres cibles connectés au serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="37c42-186">The Configuration Server has an inbuilt webserver, which orchestrates the activities of the Mobility Service, Process Servers, and Master Target servers connected to the Configuration Server.</span></span> <span data-ttu-id="37c42-187">Le serveur web du serveur de configuration utilise un certificat SSL pour authentifier ses clients.</span><span class="sxs-lookup"><span data-stu-id="37c42-187">The Configuration Server's webserver uses an SSL certificate to authenticate its clients.</span></span> <span data-ttu-id="37c42-188">Ce certificat a un délai d’expiration de trois ans et peut être renouvelé à tout moment à l’aide de la méthode suivante :</span><span class="sxs-lookup"><span data-stu-id="37c42-188">This certificate has an expiry of three years and can be renewed at any time using the following method:</span></span>

> [!WARNING]
<span data-ttu-id="37c42-189">L’expiration du certificat peut être appliquée uniquement sur les versions 9.4.XXXX.X ou supérieures.</span><span class="sxs-lookup"><span data-stu-id="37c42-189">Certificate expiry can be performed only on version 9.4.XXXX.X or higher.</span></span> <span data-ttu-id="37c42-190">Mettez à niveau tous les composants Azure Site Recovery (serveur de configuration, serveur de processus, serveur cible maître, service Mobilité) avant de commencer le flux de travail de renouvellement des certificats.</span><span class="sxs-lookup"><span data-stu-id="37c42-190">Upgrade all the Azure Site Recovery components (Configuration Server, Process Server, Master Target Server, Mobility Service) before you start the Renew Certificates workflow.</span></span>

1. <span data-ttu-id="37c42-191">Dans le portail Azure, sélectionnez votre Coffre > Infrastructure Site Recovery > Serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="37c42-191">On the Azure portal, browse to your Vault > Site Recovery Infrastructure > Configuration Server.</span></span>
2. <span data-ttu-id="37c42-192">Cliquez sur le serveur de configuration pour lequel vous devez renouveler le certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="37c42-192">Click the Configuration Server for which you need to renew the SSL Certificate for.</span></span>
3. <span data-ttu-id="37c42-193">Sous Intégrité du serveur de configuration, vous pouvez observer la date d’expiration du certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="37c42-193">Under the Configuration Server health, you can see the expiry date for the SSL Certificate.</span></span>
4. <span data-ttu-id="37c42-194">Renouvelez le certificat en cliquant sur l’action **Renouveler les certificats** comme illustré ci-après :</span><span class="sxs-lookup"><span data-stu-id="37c42-194">Renew the certificate by clicking the **Renew Certificates** action as shown in the following image:</span></span>

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a><span data-ttu-id="37c42-196">Avertissement relatif à l’expiration du certificat SSL</span><span class="sxs-lookup"><span data-stu-id="37c42-196">Secure Socket Layer certificate expiry warning</span></span>

> [!NOTE]
<span data-ttu-id="37c42-197">La validité du certificat SSL de toutes les installations qui ont été effectuées avant mai 2016 a été définie sur un an.</span><span class="sxs-lookup"><span data-stu-id="37c42-197">The SSL Certificate's validity for all installations that happened before May 2016 was set to one year.</span></span> <span data-ttu-id="37c42-198">Vous avez commencé à voir des notifications d’expiration de certificat s’afficher dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="37c42-198">you have started seeing certificate expiry notifications showing up in the Azure portal.</span></span>

1. <span data-ttu-id="37c42-199">Si le certificat SSL du serveur de configuration arrive à expiration dans les deux prochains mois, le service commence à en informer les utilisateurs via le portail Azure et la messagerie électronique (vous devez être abonné aux notifications Azure Site Recovery).</span><span class="sxs-lookup"><span data-stu-id="37c42-199">If the Configuration Server's SSL certificate is going to expire in the next two months, the service starts notifying users via the Azure portal & email (you need to be subscribed to Azure Site Recovery notifications).</span></span> <span data-ttu-id="37c42-200">Une bannière de notification est affichée dans la page des ressources du coffre.</span><span class="sxs-lookup"><span data-stu-id="37c42-200">You start seeing a notification banner on the Vault's resource page.</span></span>

  ![certificate-notification](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. <span data-ttu-id="37c42-202">Cliquez sur la bannière pour obtenir des informations supplémentaires sur l’expiration du certificat.</span><span class="sxs-lookup"><span data-stu-id="37c42-202">Click the banner to get additional details on the Certificate expiry.</span></span>

  ![certificate-details](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  <span data-ttu-id="37c42-204">Si un bouton **Mettre à niveau maintenant** s’affiche à la place d’un bouton **Renouveler maintenant**,</span><span class="sxs-lookup"><span data-stu-id="37c42-204">If instead of a **Renew Now** button you see an **Upgrade Now** button.</span></span> <span data-ttu-id="37c42-205">cela signifie que certains composants de votre environnement n’ont pas encore été mis à niveau vers 9.4.xxxx.x ou supérieur.</span><span class="sxs-lookup"><span data-stu-id="37c42-205">This means that there are some components in your environment that have not yet been upgraded to 9.4.xxxx.x or higher versions.</span></span>

## <a name="sizing-requirements-for-a-configuration-server"></a><span data-ttu-id="37c42-206">Exigences de dimensionnement d’un serveur de configuration</span><span class="sxs-lookup"><span data-stu-id="37c42-206">Sizing requirements for a Configuration Server</span></span>

| <span data-ttu-id="37c42-207">**UC**</span><span class="sxs-lookup"><span data-stu-id="37c42-207">**CPU**</span></span> | <span data-ttu-id="37c42-208">**Mémoire**</span><span class="sxs-lookup"><span data-stu-id="37c42-208">**Memory**</span></span> | <span data-ttu-id="37c42-209">**Taille du disque cache**</span><span class="sxs-lookup"><span data-stu-id="37c42-209">**Cache disk size**</span></span> | <span data-ttu-id="37c42-210">**Taux de modification des données**</span><span class="sxs-lookup"><span data-stu-id="37c42-210">**Data change rate**</span></span> | <span data-ttu-id="37c42-211">**Machines protégées**</span><span class="sxs-lookup"><span data-stu-id="37c42-211">**Protected machines**</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="37c42-212">8 processeurs virtuels (2 sockets * 4 cœurs à 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="37c42-212">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="37c42-213">16 Go</span><span class="sxs-lookup"><span data-stu-id="37c42-213">16 GB</span></span> |<span data-ttu-id="37c42-214">300 Go</span><span class="sxs-lookup"><span data-stu-id="37c42-214">300 GB</span></span> |<span data-ttu-id="37c42-215">500 Go ou moins</span><span class="sxs-lookup"><span data-stu-id="37c42-215">500 GB or less</span></span> |<span data-ttu-id="37c42-216">Répliquez moins de 100 machines.</span><span class="sxs-lookup"><span data-stu-id="37c42-216">Replicate fewer than 100 machines.</span></span> |
| <span data-ttu-id="37c42-217">12 processeurs virtuels (2 sockets * 6 cœurs à 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="37c42-217">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="37c42-218">18 Go</span><span class="sxs-lookup"><span data-stu-id="37c42-218">18 GB</span></span> |<span data-ttu-id="37c42-219">600 Go</span><span class="sxs-lookup"><span data-stu-id="37c42-219">600 GB</span></span> |<span data-ttu-id="37c42-220">500 Go à 1 To</span><span class="sxs-lookup"><span data-stu-id="37c42-220">500 GB to 1 TB</span></span> |<span data-ttu-id="37c42-221">Répliquez entre 100 et 150 machines.</span><span class="sxs-lookup"><span data-stu-id="37c42-221">Replicate between 100-150 machines.</span></span> |
| <span data-ttu-id="37c42-222">16 processeurs virtuels (2 sockets * 8 cœurs à 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="37c42-222">16 vCPUs (2 sockets * 8 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="37c42-223">32 Go</span><span class="sxs-lookup"><span data-stu-id="37c42-223">32 GB</span></span> |<span data-ttu-id="37c42-224">1 To</span><span class="sxs-lookup"><span data-stu-id="37c42-224">1 TB</span></span> |<span data-ttu-id="37c42-225">1 To à 2 To</span><span class="sxs-lookup"><span data-stu-id="37c42-225">1 TB to 2 TB</span></span> |<span data-ttu-id="37c42-226">Répliquez entre 150 et 200 machines.</span><span class="sxs-lookup"><span data-stu-id="37c42-226">Replicate between 150-200 machines.</span></span> |

  >[!TIP]
  <span data-ttu-id="37c42-227">Si l’activité quotidienne des données excède 2 To ou que vous envisagez de répliquer plus de 200 machines virtuelles, il est recommandé de déployer d’autres serveurs de processus pour équilibrer la charge du trafic de réplication.</span><span class="sxs-lookup"><span data-stu-id="37c42-227">If your daily data churn exceeds 2 TB, or you plan to replicate more than 200 virtual machines, it is recommended to deploy additional process servers to load balance the replication traffic.</span></span> <span data-ttu-id="37c42-228">Pour en savoir plus, consultez l’article How to deploy Scale-out Process servers (Déploiement des serveurs de processus de montée en puissance parallèle).</span><span class="sxs-lookup"><span data-stu-id="37c42-228">Learn more about How to deploy Scale-out Process severs.</span></span>


## <a name="common-issues"></a><span data-ttu-id="37c42-229">Problèmes courants</span><span class="sxs-lookup"><span data-stu-id="37c42-229">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
