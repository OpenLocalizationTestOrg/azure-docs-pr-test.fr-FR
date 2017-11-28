1. <span data-ttu-id="0f50f-101">Copiez le programme d’installation dans un dossier local (par exemple C:\Temp) sur le serveur que vous souhaitez protéger.</span><span class="sxs-lookup"><span data-stu-id="0f50f-101">Copy the installer to a local folder (for example, C:\Temp) on the server that you want to protect.</span></span> <span data-ttu-id="0f50f-102">Exécutez les commandes suivantes en tant qu’administrateur à l’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="0f50f-102">Run the following commands as an administrator at a command prompt:</span></span>

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. <span data-ttu-id="0f50f-103">Pour installer le service Mobilité, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0f50f-103">To install Mobility Service, run the following command:</span></span>

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. <span data-ttu-id="0f50f-104">Désormais, l’agent doit être inscrit auprès du serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="0f50f-104">Now the agent needs to be registered with the Configuration Server.</span></span>

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a><span data-ttu-id="0f50f-105">Arguments de ligne de commande du programme d’installation du service Mobilité</span><span class="sxs-lookup"><span data-stu-id="0f50f-105">Mobility Service installer command-line arguments</span></span>

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| <span data-ttu-id="0f50f-106">Paramètre</span><span class="sxs-lookup"><span data-stu-id="0f50f-106">Parameter</span></span>|<span data-ttu-id="0f50f-107">Type</span><span class="sxs-lookup"><span data-stu-id="0f50f-107">Type</span></span>|<span data-ttu-id="0f50f-108">Description</span><span class="sxs-lookup"><span data-stu-id="0f50f-108">Description</span></span>|<span data-ttu-id="0f50f-109">Valeurs possibles</span><span class="sxs-lookup"><span data-stu-id="0f50f-109">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="0f50f-110">/Role</span><span class="sxs-lookup"><span data-stu-id="0f50f-110">/Role</span></span>|<span data-ttu-id="0f50f-111">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="0f50f-111">Mandatory</span></span>|<span data-ttu-id="0f50f-112">Spécifie si le service Mobilité (MS) doit être installé ou si MasterTarget(MT) doit être installé</span><span class="sxs-lookup"><span data-stu-id="0f50f-112">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="0f50f-113">MS</span><span class="sxs-lookup"><span data-stu-id="0f50f-113">MS</span></span> </br> <span data-ttu-id="0f50f-114">MT</span><span class="sxs-lookup"><span data-stu-id="0f50f-114">MT</span></span>|
|<span data-ttu-id="0f50f-115">/InstallLocation</span><span class="sxs-lookup"><span data-stu-id="0f50f-115">/InstallLocation</span></span>|<span data-ttu-id="0f50f-116">Facultatif</span><span class="sxs-lookup"><span data-stu-id="0f50f-116">Optional</span></span>|<span data-ttu-id="0f50f-117">Emplacement où est installé le service Mobilité</span><span class="sxs-lookup"><span data-stu-id="0f50f-117">Location where Mobility Service is installed</span></span>|<span data-ttu-id="0f50f-118">N’importe quel dossier sur l’ordinateur</span><span class="sxs-lookup"><span data-stu-id="0f50f-118">Any folder on the computer</span></span>|
|<span data-ttu-id="0f50f-119">/Platform</span><span class="sxs-lookup"><span data-stu-id="0f50f-119">/Platform</span></span>|<span data-ttu-id="0f50f-120">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="0f50f-120">Mandatory</span></span>|<span data-ttu-id="0f50f-121">Spécifie la plateforme sur laquelle le service Mobilité est installé</span><span class="sxs-lookup"><span data-stu-id="0f50f-121">Specifies the platform on which the Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="0f50f-122">- **VMware** : utilisez cette valeur si vous installez le service Mobilité sur une machine virtuelle exécutée sur des *hôtes VMware vSphere ESXi*, des *hôtes Hyper-V* et des *serveurs physiques*</span><span class="sxs-lookup"><span data-stu-id="0f50f-122">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="0f50f-123">- **Azure** : utilisez cette valeur si vous installez l’agent sur une machine virtuelle Azure IaaS</span><span class="sxs-lookup"><span data-stu-id="0f50f-123">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="0f50f-124">VMware</span><span class="sxs-lookup"><span data-stu-id="0f50f-124">VMware</span></span> </br> <span data-ttu-id="0f50f-125">Les tables Azure</span><span class="sxs-lookup"><span data-stu-id="0f50f-125">Azure</span></span>|
|<span data-ttu-id="0f50f-126">/Silent</span><span class="sxs-lookup"><span data-stu-id="0f50f-126">/Silent</span></span>|<span data-ttu-id="0f50f-127">Facultatif</span><span class="sxs-lookup"><span data-stu-id="0f50f-127">Optional</span></span>|<span data-ttu-id="0f50f-128">Précise d’exécuter le programme d’installation en mode silencieux</span><span class="sxs-lookup"><span data-stu-id="0f50f-128">Specifies to run the installer in silent mode</span></span>| <span data-ttu-id="0f50f-129">N/D</span><span class="sxs-lookup"><span data-stu-id="0f50f-129">NA</span></span>|

>[!TIP]
> <span data-ttu-id="0f50f-130">Les journaux d’installation se trouvent sous %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span><span class="sxs-lookup"><span data-stu-id="0f50f-130">The setup logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span></span>

#### <a name="mobility-service-registration-command-line-arguments"></a><span data-ttu-id="0f50f-131">Arguments de ligne de commande de l’inscription du service Mobilité</span><span class="sxs-lookup"><span data-stu-id="0f50f-131">Mobility Service registration command-line arguments</span></span>

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | <span data-ttu-id="0f50f-132">Paramètre</span><span class="sxs-lookup"><span data-stu-id="0f50f-132">Parameter</span></span>|<span data-ttu-id="0f50f-133">Type</span><span class="sxs-lookup"><span data-stu-id="0f50f-133">Type</span></span>|<span data-ttu-id="0f50f-134">Description</span><span class="sxs-lookup"><span data-stu-id="0f50f-134">Description</span></span>|<span data-ttu-id="0f50f-135">Valeurs possibles</span><span class="sxs-lookup"><span data-stu-id="0f50f-135">Possible values</span></span>|
  |-|-|-|-|
  |<span data-ttu-id="0f50f-136">/CSEndPoint</span><span class="sxs-lookup"><span data-stu-id="0f50f-136">/CSEndPoint</span></span> |<span data-ttu-id="0f50f-137">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="0f50f-137">Mandatory</span></span>|<span data-ttu-id="0f50f-138">Adresse IP du serveur de configuration</span><span class="sxs-lookup"><span data-stu-id="0f50f-138">IP address of the configuration server</span></span>| <span data-ttu-id="0f50f-139">Une adresse IP valide</span><span class="sxs-lookup"><span data-stu-id="0f50f-139">Any valid IP address</span></span>|
  |<span data-ttu-id="0f50f-140">/PassphraseFilePath</span><span class="sxs-lookup"><span data-stu-id="0f50f-140">/PassphraseFilePath</span></span>|<span data-ttu-id="0f50f-141">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="0f50f-141">Mandatory</span></span>|<span data-ttu-id="0f50f-142">Emplacement de la phrase secrète</span><span class="sxs-lookup"><span data-stu-id="0f50f-142">Location of the passphrase</span></span> |<span data-ttu-id="0f50f-143">N’importe quel chemin d’accès UNC ou local valide</span><span class="sxs-lookup"><span data-stu-id="0f50f-143">Any valid UNC or local file path</span></span>|


>[!TIP]
> <span data-ttu-id="0f50f-144">Les journaux AgentConfiguration se trouvent sous %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span><span class="sxs-lookup"><span data-stu-id="0f50f-144">The AgentConfiguration logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span></span>
