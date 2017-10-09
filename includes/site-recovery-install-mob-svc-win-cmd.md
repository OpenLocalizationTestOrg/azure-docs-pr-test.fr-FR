1. <span data-ttu-id="bf5d6-101">Copiez le dossier local hello installer tooa (par exemple, C:\Temp) sur le serveur hello que tooprotect.</span><span class="sxs-lookup"><span data-stu-id="bf5d6-101">Copy hello installer tooa local folder (for example, C:\Temp) on hello server that you want tooprotect.</span></span> <span data-ttu-id="bf5d6-102">Exécutez hello suivant de commandes en tant qu’administrateur à l’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="bf5d6-102">Run hello following commands as an administrator at a command prompt:</span></span>

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. <span data-ttu-id="bf5d6-103">tooinstall Service mobilité, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bf5d6-103">tooinstall Mobility Service, run hello following command:</span></span>

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. <span data-ttu-id="bf5d6-104">L’agent de hello doit maintenant toobe inscrit avec hello serveur de Configuration.</span><span class="sxs-lookup"><span data-stu-id="bf5d6-104">Now hello agent needs toobe registered with hello Configuration Server.</span></span>

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a><span data-ttu-id="bf5d6-105">Arguments de ligne de commande du programme d’installation du service Mobilité</span><span class="sxs-lookup"><span data-stu-id="bf5d6-105">Mobility Service installer command-line arguments</span></span>

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| <span data-ttu-id="bf5d6-106">Paramètre</span><span class="sxs-lookup"><span data-stu-id="bf5d6-106">Parameter</span></span>|<span data-ttu-id="bf5d6-107">Type</span><span class="sxs-lookup"><span data-stu-id="bf5d6-107">Type</span></span>|<span data-ttu-id="bf5d6-108">Description</span><span class="sxs-lookup"><span data-stu-id="bf5d6-108">Description</span></span>|<span data-ttu-id="bf5d6-109">Valeurs possibles</span><span class="sxs-lookup"><span data-stu-id="bf5d6-109">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="bf5d6-110">/Role</span><span class="sxs-lookup"><span data-stu-id="bf5d6-110">/Role</span></span>|<span data-ttu-id="bf5d6-111">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="bf5d6-111">Mandatory</span></span>|<span data-ttu-id="bf5d6-112">Spécifie si le service Mobilité (MS) doit être installé ou si MasterTarget(MT) doit être installé</span><span class="sxs-lookup"><span data-stu-id="bf5d6-112">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="bf5d6-113">MS</span><span class="sxs-lookup"><span data-stu-id="bf5d6-113">MS</span></span> </br> <span data-ttu-id="bf5d6-114">MT</span><span class="sxs-lookup"><span data-stu-id="bf5d6-114">MT</span></span>|
|<span data-ttu-id="bf5d6-115">/InstallLocation</span><span class="sxs-lookup"><span data-stu-id="bf5d6-115">/InstallLocation</span></span>|<span data-ttu-id="bf5d6-116">Facultatif</span><span class="sxs-lookup"><span data-stu-id="bf5d6-116">Optional</span></span>|<span data-ttu-id="bf5d6-117">Emplacement où est installé le service Mobilité</span><span class="sxs-lookup"><span data-stu-id="bf5d6-117">Location where Mobility Service is installed</span></span>|<span data-ttu-id="bf5d6-118">N’importe quel dossier sur l’ordinateur de hello</span><span class="sxs-lookup"><span data-stu-id="bf5d6-118">Any folder on hello computer</span></span>|
|<span data-ttu-id="bf5d6-119">/Platform</span><span class="sxs-lookup"><span data-stu-id="bf5d6-119">/Platform</span></span>|<span data-ttu-id="bf5d6-120">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="bf5d6-120">Mandatory</span></span>|<span data-ttu-id="bf5d6-121">Spécifie la plateforme hello sur quel hello Service mobilité est installé</span><span class="sxs-lookup"><span data-stu-id="bf5d6-121">Specifies hello platform on which hello Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="bf5d6-122">- **VMware** : utilisez cette valeur si vous installez le service Mobilité sur une machine virtuelle exécutée sur des *hôtes VMware vSphere ESXi*, des *hôtes Hyper-V* et des *serveurs physiques*</span><span class="sxs-lookup"><span data-stu-id="bf5d6-122">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="bf5d6-123">- **Azure** : utilisez cette valeur si vous installez l’agent sur une machine virtuelle Azure IaaS</span><span class="sxs-lookup"><span data-stu-id="bf5d6-123">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="bf5d6-124">VMware</span><span class="sxs-lookup"><span data-stu-id="bf5d6-124">VMware</span></span> </br> <span data-ttu-id="bf5d6-125">Les tables Azure</span><span class="sxs-lookup"><span data-stu-id="bf5d6-125">Azure</span></span>|
|<span data-ttu-id="bf5d6-126">/Silent</span><span class="sxs-lookup"><span data-stu-id="bf5d6-126">/Silent</span></span>|<span data-ttu-id="bf5d6-127">Facultatif</span><span class="sxs-lookup"><span data-stu-id="bf5d6-127">Optional</span></span>|<span data-ttu-id="bf5d6-128">Spécifie le programme d’installation de toorun hello en mode silencieux</span><span class="sxs-lookup"><span data-stu-id="bf5d6-128">Specifies toorun hello installer in silent mode</span></span>| <span data-ttu-id="bf5d6-129">N/D</span><span class="sxs-lookup"><span data-stu-id="bf5d6-129">NA</span></span>|

>[!TIP]
> <span data-ttu-id="bf5d6-130">les journaux d’installation Hello se trouvent sous %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span><span class="sxs-lookup"><span data-stu-id="bf5d6-130">hello setup logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span></span>

#### <a name="mobility-service-registration-command-line-arguments"></a><span data-ttu-id="bf5d6-131">Arguments de ligne de commande de l’inscription du service Mobilité</span><span class="sxs-lookup"><span data-stu-id="bf5d6-131">Mobility Service registration command-line arguments</span></span>

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | <span data-ttu-id="bf5d6-132">Paramètre</span><span class="sxs-lookup"><span data-stu-id="bf5d6-132">Parameter</span></span>|<span data-ttu-id="bf5d6-133">Type</span><span class="sxs-lookup"><span data-stu-id="bf5d6-133">Type</span></span>|<span data-ttu-id="bf5d6-134">Description</span><span class="sxs-lookup"><span data-stu-id="bf5d6-134">Description</span></span>|<span data-ttu-id="bf5d6-135">Valeurs possibles</span><span class="sxs-lookup"><span data-stu-id="bf5d6-135">Possible values</span></span>|
  |-|-|-|-|
  |<span data-ttu-id="bf5d6-136">/CSEndPoint</span><span class="sxs-lookup"><span data-stu-id="bf5d6-136">/CSEndPoint</span></span> |<span data-ttu-id="bf5d6-137">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="bf5d6-137">Mandatory</span></span>|<span data-ttu-id="bf5d6-138">Adresse IP du serveur de configuration hello</span><span class="sxs-lookup"><span data-stu-id="bf5d6-138">IP address of hello configuration server</span></span>| <span data-ttu-id="bf5d6-139">Une adresse IP valide</span><span class="sxs-lookup"><span data-stu-id="bf5d6-139">Any valid IP address</span></span>|
  |<span data-ttu-id="bf5d6-140">/PassphraseFilePath</span><span class="sxs-lookup"><span data-stu-id="bf5d6-140">/PassphraseFilePath</span></span>|<span data-ttu-id="bf5d6-141">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="bf5d6-141">Mandatory</span></span>|<span data-ttu-id="bf5d6-142">Emplacement de la phrase secrète de hello</span><span class="sxs-lookup"><span data-stu-id="bf5d6-142">Location of hello passphrase</span></span> |<span data-ttu-id="bf5d6-143">N’importe quel chemin d’accès UNC ou local valide</span><span class="sxs-lookup"><span data-stu-id="bf5d6-143">Any valid UNC or local file path</span></span>|


>[!TIP]
> <span data-ttu-id="bf5d6-144">Hello AgentConfiguration journaux se trouvent sous %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span><span class="sxs-lookup"><span data-stu-id="bf5d6-144">hello AgentConfiguration logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span></span>
