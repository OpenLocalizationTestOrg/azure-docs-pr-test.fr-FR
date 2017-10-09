1. <span data-ttu-id="20494-101">Copiez hello installer tooa dossier local (par exemple, /tmp) sur le serveur hello que tooprotect.</span><span class="sxs-lookup"><span data-stu-id="20494-101">Copy hello installer tooa local folder (for example, /tmp) on hello server that you want tooprotect.</span></span> <span data-ttu-id="20494-102">Dans un terminal, exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="20494-102">In a terminal, run hello following commands:</span></span>
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. <span data-ttu-id="20494-103">tooinstall Service mobilité, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="20494-103">tooinstall Mobility Service, run hello following command:</span></span>

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. <span data-ttu-id="20494-104">Une fois l’installation terminée, hello Service mobilité a besoin de serveur de configuration tooget toohello inscrits.</span><span class="sxs-lookup"><span data-stu-id="20494-104">Once installation is complete, hello Mobility Service needs tooget registered toohello configuration server.</span></span> <span data-ttu-id="20494-105">Exécutez hello suivant commande tooregister hello Service mobilité avec le serveur de Configuration.</span><span class="sxs-lookup"><span data-stu-id="20494-105">Run hello following command tooregister hello Mobility Service with Configuration server.</span></span>

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a><span data-ttu-id="20494-106">Ligne de commande du programme d’installation du service Mobilité</span><span class="sxs-lookup"><span data-stu-id="20494-106">Mobility Service installer command-line</span></span>

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|<span data-ttu-id="20494-107">Paramètre</span><span class="sxs-lookup"><span data-stu-id="20494-107">Parameter</span></span>|<span data-ttu-id="20494-108">Type</span><span class="sxs-lookup"><span data-stu-id="20494-108">Type</span></span>|<span data-ttu-id="20494-109">Description</span><span class="sxs-lookup"><span data-stu-id="20494-109">Description</span></span>|<span data-ttu-id="20494-110">Valeurs possibles</span><span class="sxs-lookup"><span data-stu-id="20494-110">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="20494-111">-r</span><span class="sxs-lookup"><span data-stu-id="20494-111">-r</span></span> |<span data-ttu-id="20494-112">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="20494-112">Mandatory</span></span>|<span data-ttu-id="20494-113">Spécifie si le service Mobilité (MS) doit être installé ou si MasterTarget(MT) doit être installé</span><span class="sxs-lookup"><span data-stu-id="20494-113">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="20494-114">MS</span><span class="sxs-lookup"><span data-stu-id="20494-114">MS</span></span> </br> <span data-ttu-id="20494-115">MT</span><span class="sxs-lookup"><span data-stu-id="20494-115">MT</span></span>|
|<span data-ttu-id="20494-116">-d</span><span class="sxs-lookup"><span data-stu-id="20494-116">-d</span></span> |<span data-ttu-id="20494-117">Facultatif</span><span class="sxs-lookup"><span data-stu-id="20494-117">Optional</span></span>|<span data-ttu-id="20494-118">Emplacement où sera installé le service Mobilité</span><span class="sxs-lookup"><span data-stu-id="20494-118">Location where Mobility Service will be installed</span></span>|<span data-ttu-id="20494-119">/usr/local/ASR</span><span class="sxs-lookup"><span data-stu-id="20494-119">/usr/local/ASR</span></span>|
|<span data-ttu-id="20494-120">-v</span><span class="sxs-lookup"><span data-stu-id="20494-120">-v</span></span>|<span data-ttu-id="20494-121">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="20494-121">Mandatory</span></span>|<span data-ttu-id="20494-122">Spécifie la plateforme hello sur quel hello Service mobilité est installé</span><span class="sxs-lookup"><span data-stu-id="20494-122">Specifies hello platform on which hello Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="20494-123">- **VMware** : utilisez cette valeur si vous installez le service Mobilité sur une machine virtuelle exécutée sur des *hôtes VMware vSphere ESXi*, des *hôtes Hyper-V* et des *serveurs physiques*</span><span class="sxs-lookup"><span data-stu-id="20494-123">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="20494-124">- **Azure** : utilisez cette valeur si vous installez l’agent sur une machine virtuelle Azure IaaS</span><span class="sxs-lookup"><span data-stu-id="20494-124">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="20494-125">VMware</span><span class="sxs-lookup"><span data-stu-id="20494-125">VMware</span></span> </br> <span data-ttu-id="20494-126">Les tables Azure</span><span class="sxs-lookup"><span data-stu-id="20494-126">Azure</span></span>|
|<span data-ttu-id="20494-127">-q</span><span class="sxs-lookup"><span data-stu-id="20494-127">-q</span></span>|<span data-ttu-id="20494-128">Facultatif</span><span class="sxs-lookup"><span data-stu-id="20494-128">Optional</span></span>|<span data-ttu-id="20494-129">Spécifie le programme d’installation toorun en mode silencieux</span><span class="sxs-lookup"><span data-stu-id="20494-129">Specifies toorun installer in silent mode</span></span>| <span data-ttu-id="20494-130">N/A</span><span class="sxs-lookup"><span data-stu-id="20494-130">N/A</span></span>|


#### <a name="mobility-service-configuration-command-line"></a><span data-ttu-id="20494-131">Ligne de commande de configuration du service Mobilité</span><span class="sxs-lookup"><span data-stu-id="20494-131">Mobility Service configuration command-line</span></span>

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|<span data-ttu-id="20494-132">Paramètre</span><span class="sxs-lookup"><span data-stu-id="20494-132">Parameter</span></span>|<span data-ttu-id="20494-133">Type</span><span class="sxs-lookup"><span data-stu-id="20494-133">Type</span></span>|<span data-ttu-id="20494-134">Description</span><span class="sxs-lookup"><span data-stu-id="20494-134">Description</span></span>|<span data-ttu-id="20494-135">Valeurs possibles</span><span class="sxs-lookup"><span data-stu-id="20494-135">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="20494-136">-i</span><span class="sxs-lookup"><span data-stu-id="20494-136">-i</span></span> |<span data-ttu-id="20494-137">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="20494-137">Mandatory</span></span>|<span data-ttu-id="20494-138">Adresse IP du serveur de Configuration de hello</span><span class="sxs-lookup"><span data-stu-id="20494-138">IP of hello Configuration Server</span></span>|<span data-ttu-id="20494-139">Une adresse IP valide</span><span class="sxs-lookup"><span data-stu-id="20494-139">Any valid IP Address</span></span>|
|<span data-ttu-id="20494-140">-P</span><span class="sxs-lookup"><span data-stu-id="20494-140">-P</span></span> |<span data-ttu-id="20494-141">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="20494-141">Mandatory</span></span>|<span data-ttu-id="20494-142">Fichier de hello de chemin d’accès complet du fichier où le mot de passe de connexion hello est enregistré</span><span class="sxs-lookup"><span data-stu-id="20494-142">Full file path hello file where hello connection passphrase is saved</span></span>|<span data-ttu-id="20494-143">N’importe quel dossier valide</span><span class="sxs-lookup"><span data-stu-id="20494-143">Any valid folder</span></span>|
