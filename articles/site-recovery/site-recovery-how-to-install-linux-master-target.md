---
title: "aaaHow tooinstall serveur cible maître Linux pour basculement à partir d’Azure site tooon | Documents Microsoft"
description: "Pour reprotéger une machine virtuelle Linux, vous avez besoin d’un serveur cible maître Linux. Découvrez comment tooinstall une."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: d7c55d115712b9862414979f89efb1f177c5f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-linux-master-target-server"></a><span data-ttu-id="d69b5-104">Installer un serveur cible maître Linux</span><span class="sxs-lookup"><span data-stu-id="d69b5-104">Install a Linux master target server</span></span>
<span data-ttu-id="d69b5-105">Après avoir effectué sur vos ordinateurs virtuels, vous pouvez échouer hello arrière machines virtuelles toohello sur site local.</span><span class="sxs-lookup"><span data-stu-id="d69b5-105">After you fail over your virtual machines, you can fail back hello virtual machines toohello on-premises site.</span></span> <span data-ttu-id="d69b5-106">toofail précédent, vous devez tooreprotect hello virtual machine à partir du site local de toohello Azure.</span><span class="sxs-lookup"><span data-stu-id="d69b5-106">toofail back, you need tooreprotect hello virtual machine from Azure toohello on-premises site.</span></span> <span data-ttu-id="d69b5-107">Pour ce processus, vous avez besoin d’un trafic de hello tooreceive local du serveur de cible maître.</span><span class="sxs-lookup"><span data-stu-id="d69b5-107">For this process, you need an on-premises master target server tooreceive hello traffic.</span></span> 

<span data-ttu-id="d69b5-108">Si votre machine virtuelle protégée est de type Windows, vous avez besoin d’un serveur cible maître Windows.</span><span class="sxs-lookup"><span data-stu-id="d69b5-108">If your protected virtual machine is a Windows virtual machine, then you need a Windows master target.</span></span> <span data-ttu-id="d69b5-109">Si vous avez une machine virtuelle Linux, vous avez besoin d’un serveur cible maître Linux.</span><span class="sxs-lookup"><span data-stu-id="d69b5-109">For a Linux virtual machine, you need a Linux master target.</span></span> <span data-ttu-id="d69b5-110">Toolearn les étapes suivantes de hello en lecture comment toocreate et installer une Linux maître cible.</span><span class="sxs-lookup"><span data-stu-id="d69b5-110">Read hello following steps toolearn how toocreate and install a Linux master target.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d69b5-111">À partir de la version du serveur cible maître de hello 9.10.0, serveur cible maître de la dernière hello peut être uniquement installé sur un serveur d’Ubuntu 16.04.</span><span class="sxs-lookup"><span data-stu-id="d69b5-111">Starting with release of hello 9.10.0 master target server, hello latest master target server can be only installed on an Ubuntu 16.04 server.</span></span> <span data-ttu-id="d69b5-112">Les nouvelles installations ne sont pas autorisées sur les serveurs de CentOS6.6.</span><span class="sxs-lookup"><span data-stu-id="d69b5-112">New installations aren't allowed on  CentOS6.6 servers.</span></span> <span data-ttu-id="d69b5-113">Toutefois, vous pouvez continuer tooupgrade vos serveurs de la cible principale ancienne aide hello 9.10.0 version.</span><span class="sxs-lookup"><span data-stu-id="d69b5-113">However, you can continue tooupgrade your old master target servers by using hello 9.10.0 version.</span></span>

## <a name="overview"></a><span data-ttu-id="d69b5-114">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="d69b5-114">Overview</span></span>
<span data-ttu-id="d69b5-115">Cet article fournit des instructions pour la tooinstall une Linux maître cible.</span><span class="sxs-lookup"><span data-stu-id="d69b5-115">This article provides instructions for how tooinstall a Linux master target.</span></span>

<span data-ttu-id="d69b5-116">Valider des commentaires ou des questions à fin hello de cet article ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="d69b5-116">Post comments or questions at hello end of this article or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d69b5-117">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d69b5-117">Prerequisites</span></span>

* <span data-ttu-id="d69b5-118">hôte de hello toochoose sur le toodeploy hello serveur cible maître, déterminer si la restauration automatique hello va toobe tooan existante sur site ordinateur virtuel ou la machine virtuelle tooa.</span><span class="sxs-lookup"><span data-stu-id="d69b5-118">toochoose hello host on which toodeploy hello master target, determine if hello failback is going toobe tooan existing on-premises virtual machine or tooa new virtual machine.</span></span> 
    * <span data-ttu-id="d69b5-119">Pour un ordinateur virtuel existant, hôte hello du serveur cible maître hello doit avoir accès aux banques de données toohello de la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-119">For an existing virtual machine, hello host of hello master target should have access toohello data stores of hello virtual machine.</span></span>
    * <span data-ttu-id="d69b5-120">Si l’ordinateur virtuel local, hello n’existe pas, la machine virtuelle de la restauration automatique hello est créé sur le même hôte que le serveur cible maître hello de hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-120">If hello on-premises virtual machine does not exist, hello failback virtual machine is created on hello same host as hello master target.</span></span> <span data-ttu-id="d69b5-121">Vous pouvez choisir n’importe quel hôte ESXi tooinstall serveur cible maître hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-121">You can choose any ESXi host tooinstall hello master target.</span></span>
* <span data-ttu-id="d69b5-122">serveur cible maître Hello doit être sur un réseau qui peut communiquer avec le serveur de processus hello et serveur de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-122">hello master target should be on a network that can communicate with hello process server and hello configuration server.</span></span>
* <span data-ttu-id="d69b5-123">version de Hello du serveur cible maître hello doit être égal tooor précédemment que dans les versions de serveur de processus hello et serveur de configuration hello hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-123">hello version of hello master target must be equal tooor earlier than hello versions of hello process server and hello configuration server.</span></span> <span data-ttu-id="d69b5-124">Par exemple, si la version hello hello du serveur de configuration est 9.4, version hello du serveur cible maître hello peut être 9.4 ou 9.3 mais pas 9.5.</span><span class="sxs-lookup"><span data-stu-id="d69b5-124">For example, if hello version of hello configuration server is 9.4, hello version of hello master target can be 9.4 or 9.3 but not 9.5.</span></span>
* <span data-ttu-id="d69b5-125">serveur cible maître Hello ne peut être un ordinateur virtuel VMware et non à un serveur physique.</span><span class="sxs-lookup"><span data-stu-id="d69b5-125">hello master target can only be a VMware virtual machine and not a physical server.</span></span>

## <a name="create-hello-master-target-according-toohello-sizing-guidelines"></a><span data-ttu-id="d69b5-126">Créer le serveur cible maître hello en fonction des instructions de dimensionnement de toohello</span><span class="sxs-lookup"><span data-stu-id="d69b5-126">Create hello master target according toohello sizing guidelines</span></span>

<span data-ttu-id="d69b5-127">Créer un serveur cible maître hello conformément aux hello suivant les instructions de dimensionnement :</span><span class="sxs-lookup"><span data-stu-id="d69b5-127">Create hello master target in accordance with hello following sizing guidelines:</span></span>
- <span data-ttu-id="d69b5-128">**RAM** : 6 Go ou plus</span><span class="sxs-lookup"><span data-stu-id="d69b5-128">**RAM**: 6 GB or more</span></span>
- <span data-ttu-id="d69b5-129">**Taille du disque du système d’exploitation**: 100 Go ou plus (tooinstall CentOS6.6)</span><span class="sxs-lookup"><span data-stu-id="d69b5-129">**OS disk size**: 100 GB or more (tooinstall CentOS6.6)</span></span>
- <span data-ttu-id="d69b5-130">**Taille du disque supplémentaire pour le lecteur de conservation** : 1 To</span><span class="sxs-lookup"><span data-stu-id="d69b5-130">**Additional disk size for retention drive**: 1 TB</span></span>
- <span data-ttu-id="d69b5-131">**Cœurs d’UC** : 4 cœurs ou plus</span><span class="sxs-lookup"><span data-stu-id="d69b5-131">**CPU cores**: 4 cores or more</span></span>

<span data-ttu-id="d69b5-132">Ubuntu noyaux sont prises en charge de charge Hello qui suit.</span><span class="sxs-lookup"><span data-stu-id="d69b5-132">hello following supported Ubuntu kernels are supported.</span></span>


|<span data-ttu-id="d69b5-133">Série de noyau</span><span class="sxs-lookup"><span data-stu-id="d69b5-133">Kernel Series</span></span>  |<span data-ttu-id="d69b5-134">Prend en charge des trop</span><span class="sxs-lookup"><span data-stu-id="d69b5-134">Support up too</span></span> |
|---------|---------|
|<span data-ttu-id="d69b5-135">4.4</span><span class="sxs-lookup"><span data-stu-id="d69b5-135">4.4</span></span>      |<span data-ttu-id="d69b5-136">4.4.0-81-generic</span><span class="sxs-lookup"><span data-stu-id="d69b5-136">4.4.0-81-generic</span></span>         |
|<span data-ttu-id="d69b5-137">4.8</span><span class="sxs-lookup"><span data-stu-id="d69b5-137">4.8</span></span>      |<span data-ttu-id="d69b5-138">4.8.0-56-generic</span><span class="sxs-lookup"><span data-stu-id="d69b5-138">4.8.0-56-generic</span></span>         |
|<span data-ttu-id="d69b5-139">4.10</span><span class="sxs-lookup"><span data-stu-id="d69b5-139">4.10</span></span>     |<span data-ttu-id="d69b5-140">4.10.0-24-generic</span><span class="sxs-lookup"><span data-stu-id="d69b5-140">4.10.0-24-generic</span></span>        |


## <a name="deploy-hello-master-target-server"></a><span data-ttu-id="d69b5-141">Déployer le serveur cible maître de hello</span><span class="sxs-lookup"><span data-stu-id="d69b5-141">Deploy hello master target server</span></span>

### <a name="install-ubuntu-16042-minimal"></a><span data-ttu-id="d69b5-142">Installer Ubuntu version 16.04.2 Minimal</span><span class="sxs-lookup"><span data-stu-id="d69b5-142">Install Ubuntu 16.04.2 Minimal</span></span>

<span data-ttu-id="d69b5-143">Prendre hello suivant le système d’exploitation de hello étapes tooinstall hello Ubuntu 16.04.2 64 bits.</span><span class="sxs-lookup"><span data-stu-id="d69b5-143">Take hello following hello steps tooinstall hello Ubuntu 16.04.2 64-bit operating system.</span></span>

<span data-ttu-id="d69b5-144">**Étape 1 :** accédez toohello [lien de téléchargement](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) et choisissez le miroir le plus proche de hello à partir de laquelle télécharger un fichier ISO du Ubuntu 16.04.2 minimale 64 bits.</span><span class="sxs-lookup"><span data-stu-id="d69b5-144">**Step 1:** Go toohello [download link](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) and choose hello closest mirror from which download an Ubuntu 16.04.2 minimal 64-bit ISO.</span></span>

<span data-ttu-id="d69b5-145">Conserver un fichier ISO du Ubuntu 16.04.2 minimale 64 bits dans le lecteur de DVD de hello et démarrer hello système.</span><span class="sxs-lookup"><span data-stu-id="d69b5-145">Keep an Ubuntu 16.04.2 minimal 64-bit ISO in hello DVD drive and start hello system.</span></span>

<span data-ttu-id="d69b5-146">**Étape 2 :** sélectionnez **French** (Français) comme langue par défaut, puis appuyez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-146">**Step 2:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Sélectionner une langue](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

<span data-ttu-id="d69b5-148">**Étape 3 :** sélectionnez **Install Ubuntu Server** (Installer le serveur Ubuntu), puis appuyez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-148">**Step 3:** Select **Install Ubuntu Server**, and then select **Enter**.</span></span>

![Sélectionner l’option d’installation du serveur Ubuntu](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

<span data-ttu-id="d69b5-150">**Étape 4 :** sélectionnez **French** (Français) comme langue par défaut, puis appuyez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-150">**Step 4:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Sélectionner French (Français) comme langue par défaut](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

<span data-ttu-id="d69b5-152">**Étape 5 :** sélectionnez hello option appropriée dans hello **fuseau horaire** liste d’options et sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-152">**Step 5:** Select hello appropriate option from hello **Time Zone** options list, and then select **Enter**.</span></span>

![Sélectionnez le fuseau horaire correct de hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

<span data-ttu-id="d69b5-154">**Étape 6 :** sélectionnez **non** (hello option par défaut), puis sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-154">**Step 6:** Select **No** (hello default option), and then select **Enter**.</span></span>


![Configurer hello clavier](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

<span data-ttu-id="d69b5-156">**Étape 7 :** sélectionnez **anglais (États-Unis)** comme hello pays d’origine pour le clavier de hello et sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-156">**Step 7:** Select **English (US)** as hello country of origin for hello keyboard, and then select **Enter**.</span></span>

![Sélectionnez des États-Unis comme pays hello d’origine](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

<span data-ttu-id="d69b5-158">**Étape 8 :** sélectionnez **anglais (États-Unis)** comme disposition du clavier hello, puis sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-158">**Step 8:** Select **English (US)** as hello keyboard layout, and then select **Enter**.</span></span>

![Sélectionnez l’anglais (États-Unis) en tant que la disposition du clavier hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

<span data-ttu-id="d69b5-160">**Étape 9 :** entrer de nom d’hôte hello pour votre serveur Bonjour **nom d’hôte** zone, puis sélectionnez **continuer**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-160">**Step 9:** Enter hello hostname for your server in hello **Hostname** box, and then select **Continue**.</span></span>

![Entrez le nom d’hôte hello pour votre serveur](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

<span data-ttu-id="d69b5-162">**Étape 10 :** toocreate un compte d’utilisateur, entrez le nom d’utilisateur hello et sélectionnez **continuer**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-162">**Step 10:** toocreate a user account, enter hello user name, and then select **Continue**.</span></span>

![Création d'un compte d'utilisateur](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

<span data-ttu-id="d69b5-164">**Étape 11 :** mot de passe hello hello nouveau compte d’utilisateur, puis sélectionnez **continuer**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-164">**Step 11:** Enter hello password for hello new user account, and then select **Continue**.</span></span>

![Entrez le mot de passe hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

<span data-ttu-id="d69b5-166">**Étape 12 :** confirmer hello mot de passe utilisateur hello et sélectionnez **continuer**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-166">**Step 12:** Confirm hello password for hello new user, and then select **Continue**.</span></span>

![Confirmer les mots de passe hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

<span data-ttu-id="d69b5-168">**Étape 13 :** sélectionnez **non** (hello option par défaut), puis sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-168">**Step 13:** Select **No** (hello default option), and then select **Enter**.</span></span>

![Configurer des utilisateurs et des mots de passe](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

<span data-ttu-id="d69b5-170">**Étape 14 :** si le fuseau horaire hello affichée est correcte, sélectionnez **Oui** (hello option par défaut), puis sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-170">**Step 14:** If hello time zone that's displayed is correct, select **Yes** (hello default option), and then select **Enter**.</span></span>

<span data-ttu-id="d69b5-171">tooreconfigure votre fuseau horaire, sélectionnez **non**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-171">tooreconfigure your time zone, select **No**.</span></span>

![Configurer l’horloge hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

<span data-ttu-id="d69b5-173">**Étape 15 :** hello options de la méthode de partitionnement, sélectionnez **guidée - utiliser l’intégralité du disque**, puis sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-173">**Step 15:** From hello partitioning method options, select **Guided - use entire disk**, and then select **Enter**.</span></span>

![Sélectionnez hello option de méthode de partitionnement](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

<span data-ttu-id="d69b5-175">**Étape 16 :** sélectionnez hello disque approprié à partir de hello **sélectionnez disque toopartition** options, puis sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-175">**Step 16:** Select hello appropriate disk from hello **Select disk toopartition** options, and then select **Enter**.</span></span>


![Sélectionnez le disque hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

<span data-ttu-id="d69b5-177">**Étape 17 :** sélectionnez **Oui** toowrite hello toodisk de modifications, puis sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-177">**Step 17:** Select **Yes** toowrite hello changes toodisk, and then select **Enter**.</span></span>

![Écrire hello modifications toodisk](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

<span data-ttu-id="d69b5-179">**Étape 18 :** sélectionnez l’option par défaut de hello, sélectionnez **continuer**, puis sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-179">**Step 18:** Select hello default option, select **Continue**, and then select **Enter**.</span></span>

![Sélectionnez l’option par défaut de hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

<span data-ttu-id="d69b5-181">**Étape 19 :** l’option hello approprié pour la gestion des mises à niveau sur votre système, puis **entrée**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-181">**Step 19:** Select hello appropriate option for managing upgrades on your system, and then select **Enter**.</span></span>

![Sélectionnez comment toomanage mises à niveau](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> <span data-ttu-id="d69b5-183">Étant donné que le serveur cible maître de Azure Site Recovery hello requiert une version spécifique de hello Ubuntu, vous devez tooensure ce noyau hello mises à niveau sont désactivés pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-183">Because hello Azure Site Recovery master target server requires a very specific version of hello Ubuntu, you need tooensure that hello kernel upgrades are disabled for hello virtual machine.</span></span> <span data-ttu-id="d69b5-184">Si elles sont activées, les mises à niveau régulières provoquent toomalfunction de serveur cible maître hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-184">If they are enabled, then any regular upgrades cause hello master target server toomalfunction.</span></span> <span data-ttu-id="d69b5-185">Veillez à sélectionner hello **aucune mise à jour automatique** option.</span><span class="sxs-lookup"><span data-stu-id="d69b5-185">Make sure you select hello **No automatic updates** option.</span></span>


<span data-ttu-id="d69b5-186">**Étape 20 :** sélectionnez les options par défaut.</span><span class="sxs-lookup"><span data-stu-id="d69b5-186">**Step 20:** Select default options.</span></span> <span data-ttu-id="d69b5-187">Si vous souhaitez openSSH pour établir une connexion SSH, sélectionnez hello **OpenSSH server** option et sélectionnez **continuer**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-187">If you want openSSH for SSH connect, select hello **OpenSSH server** option, and then select **Continue**.</span></span>

![Sélectionner les logiciels](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

<span data-ttu-id="d69b5-189">**Étape 21 :** sélectionnez **Yes** (Oui), puis appuyez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-189">**Step 21:** Select **Yes**, and then select **Enter**.</span></span>

![Chargeur de démarrage de l’installation n’hello GRUB](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

<span data-ttu-id="d69b5-191">**Étape 22 :** sélectionnez hello appareil approprié pour l’installation de chargeur de démarrage de hello (de préférence **/dev/sda**), puis sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-191">**Step 22:** Select hello appropriate device for hello boot loader installation (preferably **/dev/sda**), and then select **Enter**.</span></span>

![Sélectionner un appareil pour l’installation du chargeur de démarrage](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

<span data-ttu-id="d69b5-193">**Étape 23 :** sélectionnez **continuer**, puis sélectionnez **entrée** installation de hello toofinish.</span><span class="sxs-lookup"><span data-stu-id="d69b5-193">**Step 23:** Select **Continue**, and then select **Enter** toofinish hello installation.</span></span>

![Terminer l’installation de hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

<span data-ttu-id="d69b5-195">Une fois l’installation de hello est terminée, connectez-vous toohello machine virtuelle avec les informations d’identification d’utilisateur nouveau hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-195">After hello installation has finished, sign in toohello VM with hello new user credentials.</span></span> <span data-ttu-id="d69b5-196">(Consultez trop**étape 10** pour plus d’informations.)</span><span class="sxs-lookup"><span data-stu-id="d69b5-196">(Refer too**Step 10** for more information.)</span></span>

<span data-ttu-id="d69b5-197">Étapes hello décrits dans hello suivant capture d’écran tooset hello racine mot de passe utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d69b5-197">Take hello steps that are described in hello following screenshot tooset hello ROOT user password.</span></span> <span data-ttu-id="d69b5-198">Ensuite, connectez-vous en tant qu’utilisateur ROOT.</span><span class="sxs-lookup"><span data-stu-id="d69b5-198">Then sign in as ROOT user.</span></span>

![Mot de passe utilisateur ensemble hello racine](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-hello-machine-for-configuration-as-a-master-target-server"></a><span data-ttu-id="d69b5-200">Préparer l’ordinateur hello pour la configuration comme un serveur cible maître</span><span class="sxs-lookup"><span data-stu-id="d69b5-200">Prepare hello machine for configuration as a master target server</span></span>
<span data-ttu-id="d69b5-201">Ensuite, préparez l’ordinateur hello pour la configuration comme un serveur cible maître.</span><span class="sxs-lookup"><span data-stu-id="d69b5-201">Next, prepare hello machine for configuration as a master target server.</span></span>

<span data-ttu-id="d69b5-202">ID de hello tooget pour chaque disque SCSI dans une machine virtuelle Linux, activer hello **disque. EnableUUID = TRUE** paramètre.</span><span class="sxs-lookup"><span data-stu-id="d69b5-202">tooget hello ID for each SCSI hard disk in a Linux virtual machine, enable hello **disk.EnableUUID = TRUE** parameter.</span></span>

<span data-ttu-id="d69b5-203">tooenable étapes de ce paramètre, hello take suivant :</span><span class="sxs-lookup"><span data-stu-id="d69b5-203">tooenable this parameter, take hello following steps:</span></span>

1. <span data-ttu-id="d69b5-204">Arrêtez votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d69b5-204">Shut down your virtual machine.</span></span>

2. <span data-ttu-id="d69b5-205">Entrée hello pour l’ordinateur virtuel de hello dans le volet gauche de hello d’avec le bouton droit et sélectionnez **modifier les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-205">Right-click hello entry for hello virtual machine in hello left pane, and then select **Edit Settings**.</span></span>

3. <span data-ttu-id="d69b5-206">Sélectionnez hello **Options** onglet.</span><span class="sxs-lookup"><span data-stu-id="d69b5-206">Select hello **Options** tab.</span></span>

4. <span data-ttu-id="d69b5-207">Dans le volet gauche de hello, sélectionnez **avancé** > **général**, puis sélectionnez hello **les paramètres de Configuration** bouton dans la partie inférieure droite de hello d’écran hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-207">In hello left pane, select **Advanced** > **General**, and then select hello **Configuration Parameters** button on hello lower-right part of hello screen.</span></span>

    ![Onglets Options](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    <span data-ttu-id="d69b5-209">Hello **les paramètres de Configuration** option n’est pas disponible lors de la machine de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="d69b5-209">hello **Configuration Parameters** option is not available when hello machine is running.</span></span> <span data-ttu-id="d69b5-210">toomake cet onglet actif, arrêter la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-210">toomake this tab active, shut down hello virtual machine.</span></span>

5. <span data-ttu-id="d69b5-211">Vérifiez si une ligne comportant **disk.EnableUUID** existe.</span><span class="sxs-lookup"><span data-stu-id="d69b5-211">See whether a row with **disk.EnableUUID** already exists.</span></span>

    - <span data-ttu-id="d69b5-212">Si la valeur de hello existe et qu’il est défini trop**False**, modifiez la valeur de hello trop**True**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-212">If hello value exists and is set too**False**, change hello value too**True**.</span></span> <span data-ttu-id="d69b5-213">(les valeurs hello ne respectent pas la casse).</span><span class="sxs-lookup"><span data-stu-id="d69b5-213">(hello values are not case-sensitive.)</span></span>

    - <span data-ttu-id="d69b5-214">Si la valeur de hello existe et qu’il est défini trop**True**, sélectionnez **Annuler**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-214">If hello value exists and is set too**True**, select **Cancel**.</span></span>

    - <span data-ttu-id="d69b5-215">Si la valeur de hello n’existe pas, sélectionnez **ajouter une ligne**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-215">If hello value does not exist, select **Add Row**.</span></span>

    - <span data-ttu-id="d69b5-216">Dans la colonne de nom hello, ajoutez **disque. EnableUUID**, puis définissez la valeur de hello trop**TRUE**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-216">In hello name column, add **disk.EnableUUID**, and then set hello value too**TRUE**.</span></span>

    ![Vérification de la présence de disk.EnableUUID](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a><span data-ttu-id="d69b5-218">Désactiver les mises à niveau du noyau</span><span class="sxs-lookup"><span data-stu-id="d69b5-218">Disable kernel upgrades</span></span>

<span data-ttu-id="d69b5-219">Azure serveur cible maître de récupération de Site requiert une version spécifique de hello Ubuntu, assurez-vous que les mises à niveau du noyau hello sont désactivées pour l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-219">Azure Site Recovery master target server requires a very specific version of hello Ubuntu, ensure that hello kernel upgrades are disabled for hello virtual machine.</span></span>

<span data-ttu-id="d69b5-220">Si les mises à niveau du noyau sont activés, les mises à niveau régulières provoquent toomalfunction de serveur cible maître hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-220">If kernel upgrades are enabled, then any regular upgrades cause hello master target server toomalfunction.</span></span>

#### <a name="download-and-install-additional-packages"></a><span data-ttu-id="d69b5-221">Télécharger et installer les packages supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d69b5-221">Download and install additional packages</span></span>

> [!NOTE]
> <span data-ttu-id="d69b5-222">Assurez-vous que vous avez toodownload de connectivité Internet et installez des packages supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="d69b5-222">Make sure that you have Internet connectivity toodownload and install additional packages.</span></span> <span data-ttu-id="d69b5-223">Si vous n’avez pas connecté à Internet, vous devez toomanually rechercher ces packages RPM et de les installer.</span><span class="sxs-lookup"><span data-stu-id="d69b5-223">If you don't have Internet connectivity, you need toomanually find these RPM packages and install them.</span></span>

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-hello-installer-for-setup"></a><span data-ttu-id="d69b5-224">Obtenir le programme d’installation hello pour le programme d’installation</span><span class="sxs-lookup"><span data-stu-id="d69b5-224">Get hello installer for setup</span></span>

<span data-ttu-id="d69b5-225">Si votre serveur cible maître possède une connexion Internet, vous pouvez utiliser hello suivant le programme d’installation d’étapes toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-225">If your master target has Internet connectivity, you can use hello following steps toodownload hello installer.</span></span> <span data-ttu-id="d69b5-226">Dans le cas contraire, vous pouvez copier le programme d’installation hello hello serveur de processus et l’installer.</span><span class="sxs-lookup"><span data-stu-id="d69b5-226">Otherwise, you can copy hello installer from hello process server and then install it.</span></span>

#### <a name="download-hello-master-target-installation-packages"></a><span data-ttu-id="d69b5-227">Télécharger les packages d’installation du serveur cible maître hello</span><span class="sxs-lookup"><span data-stu-id="d69b5-227">Download hello master target installation packages</span></span>

<span data-ttu-id="d69b5-228">[Télécharger hello dernière Linux cible maître installation](https://aka.ms/latestlinuxmobsvc).</span><span class="sxs-lookup"><span data-stu-id="d69b5-228">[Download hello latest Linux master target installation bits](https://aka.ms/latestlinuxmobsvc).</span></span>

<span data-ttu-id="d69b5-229">toodownload à l’aide de Linux, type :</span><span class="sxs-lookup"><span data-stu-id="d69b5-229">toodownload it by using Linux, type:</span></span>

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

<span data-ttu-id="d69b5-230">Assurez-vous que vous téléchargez et décompressez le programme d’installation hello dans votre répertoire de base.</span><span class="sxs-lookup"><span data-stu-id="d69b5-230">Make sure that you download and unzip hello installer in your home directory.</span></span> <span data-ttu-id="d69b5-231">Si vous décompressez trop**/usr/Local**, puis hello installation échoue.</span><span class="sxs-lookup"><span data-stu-id="d69b5-231">If you unzip too**/usr/Local**, then hello installation  fails.</span></span>


#### <a name="access-hello-installer-from-hello-process-server"></a><span data-ttu-id="d69b5-232">Programme d’installation d’accès hello hello du serveur de processus</span><span class="sxs-lookup"><span data-stu-id="d69b5-232">Access hello installer from hello process server</span></span>

1. <span data-ttu-id="d69b5-233">Sur le serveur de processus hello, accédez trop**C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-233">On hello process server, go too**C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span></span>

2. <span data-ttu-id="d69b5-234">Copiez le fichier du programme d’installation requis hello hello serveur de processus et l’enregistrer en tant que **latestlinuxmobsvc.tar.gz** dans votre répertoire de base.</span><span class="sxs-lookup"><span data-stu-id="d69b5-234">Copy hello required installer file from hello process server, and save it as **latestlinuxmobsvc.tar.gz** in your home directory.</span></span>


### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="d69b5-235">Appliquer des modifications de configuration personnalisées</span><span class="sxs-lookup"><span data-stu-id="d69b5-235">Apply custom configuration changes</span></span>

<span data-ttu-id="d69b5-236">modifications de configuration personnalisée tooapply, utilisez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d69b5-236">tooapply custom configuration changes, use hello following steps:</span></span>


1. <span data-ttu-id="d69b5-237">Exécutez hello suivant binaire de commande toountar hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-237">Run hello following command toountar hello binary.</span></span>
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Capture d’écran de hello commande toorun](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. <span data-ttu-id="d69b5-239">La commande suivante d’exécution hello toogive autorisation.</span><span class="sxs-lookup"><span data-stu-id="d69b5-239">Run hello following command toogive permission.</span></span>
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. <span data-ttu-id="d69b5-240">Exécutez hello commande toorun hello script suivant.</span><span class="sxs-lookup"><span data-stu-id="d69b5-240">Run hello following command toorun hello script.</span></span>
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> <span data-ttu-id="d69b5-241">Exécuter le script hello qu’une seule fois sur le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-241">Run hello script only once on hello server.</span></span> <span data-ttu-id="d69b5-242">Hello serveur arrêté.</span><span class="sxs-lookup"><span data-stu-id="d69b5-242">Shut down hello server.</span></span> <span data-ttu-id="d69b5-243">Redémarrez hello serveur après avoir ajouté un disque, comme décrit dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-243">Then restart hello server after you add a disk, as described in hello next section.</span></span>

### <a name="add-a-retention-disk-toohello-linux-master-target-virtual-machine"></a><span data-ttu-id="d69b5-244">Ajouter une machine virtuelle de rétention disque toohello Linux cible maître</span><span class="sxs-lookup"><span data-stu-id="d69b5-244">Add a retention disk toohello Linux master target virtual machine</span></span>

<span data-ttu-id="d69b5-245">Utilisez hello suivant les étapes toocreate un disque de rétention :</span><span class="sxs-lookup"><span data-stu-id="d69b5-245">Use hello following steps toocreate a retention disk:</span></span>

1. <span data-ttu-id="d69b5-246">Attacher une disque de 1 to toohello Linux cible maître machine virtuelle et ensuite démarrer hello ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d69b5-246">Attach a new 1-TB disk toohello Linux master target virtual machine, and then start hello machine.</span></span>

2. <span data-ttu-id="d69b5-247">Hello d’utilisation **multipath -ll** ID de commande toolearn hello MPIO du disque de rétention hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-247">Use hello **multipath -ll** command toolearn hello multipath ID of hello retention disk.</span></span>

    ```
    multipath -ll
    ```
    ![ID de chemins d’accès multiples Hello du disque de rétention de hello](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. <span data-ttu-id="d69b5-249">Formater le lecteur hello et créer un système de fichiers sur le nouveau lecteur de hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-249">Format hello drive, and then create a file system on hello new drive.</span></span>

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Création d’un système de fichiers sur le lecteur de hello](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. <span data-ttu-id="d69b5-251">Après avoir créé le système de fichiers hello, montez le disque de rétention hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-251">After you create hello file system, mount hello retention disk.</span></span>
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Disque de rétention de montage hello](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. <span data-ttu-id="d69b5-253">Créer hello **fstab** lecteur de rétention entrée toomount hello chaque fois hello système démarre.</span><span class="sxs-lookup"><span data-stu-id="d69b5-253">Create hello **fstab** entry toomount hello retention drive every time hello system starts.</span></span>
    ```
    vi /etc/fstab
    ```
    <span data-ttu-id="d69b5-254">Sélectionnez **insérer** toobegin modification hello fichier.</span><span class="sxs-lookup"><span data-stu-id="d69b5-254">Select **Insert** toobegin editing hello file.</span></span> <span data-ttu-id="d69b5-255">Créer une nouvelle ligne, puis insérez hello après le texte.</span><span class="sxs-lookup"><span data-stu-id="d69b5-255">Create a new line, and then insert hello following text.</span></span> <span data-ttu-id="d69b5-256">Modifier l’ID de plusieurs chemins de disque hello basé sur les ID de chemins d’accès multiples hello mis en surbrillance à partir de la commande précédente hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-256">Edit hello disk multipath ID based on hello highlighted multipath ID from hello previous command.</span></span>

    <span data-ttu-id="d69b5-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span><span class="sxs-lookup"><span data-stu-id="d69b5-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span></span>

    <span data-ttu-id="d69b5-258">Sélectionnez **ÉCHAP**, puis tapez **: wq** (écrire et quittez) fenêtre de l’éditeur tooclose hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-258">Select **Esc**, and then type **:wq** (write and quit) tooclose hello editor window.</span></span>

### <a name="install-hello-master-target"></a><span data-ttu-id="d69b5-259">Installer le serveur cible maître hello</span><span class="sxs-lookup"><span data-stu-id="d69b5-259">Install hello master target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d69b5-260">version de Hello du serveur cible maître de hello doit être égal tooor précédemment que dans les versions de serveur de processus hello et serveur de configuration hello hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-260">hello version of hello master target server must be equal tooor earlier than hello versions of hello process server and hello configuration server.</span></span> <span data-ttu-id="d69b5-261">Si cette condition n’est pas remplie, la reprotection aboutit, mais la réplication échoue.</span><span class="sxs-lookup"><span data-stu-id="d69b5-261">If this condition is not met, reprotect succeeds, but replication fails.</span></span>


> [!NOTE]
> <span data-ttu-id="d69b5-262">Avant d’installer de serveur cible maître de hello, vérifiez que hello **/etc/hosts** fichier sur l’ordinateur virtuel de hello contient des entrées qui mappent hello nom d’hôte local toohello adresses IP qui sont associés à toutes les cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="d69b5-262">Before you install hello master target server, check that hello **/etc/hosts** file on hello virtual machine contains entries that map hello local hostname toohello IP addresses that are associated with all network adapters.</span></span>

1. <span data-ttu-id="d69b5-263">Copier la phrase secrète de hello à partir de **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** sur le serveur de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-263">Copy hello passphrase from **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** on hello configuration server.</span></span> <span data-ttu-id="d69b5-264">Puis l’enregistrer en tant que **passphrase.txt** Bonjour même répertoire local en exécutant hello la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d69b5-264">Then save it as **passphrase.txt** in hello same local directory by running hello following command:</span></span>

    ```
    echo <passphrase> >passphrase.txt
    ```
    <span data-ttu-id="d69b5-265">Exemple :</span><span class="sxs-lookup"><span data-stu-id="d69b5-265">Example:</span></span> 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. <span data-ttu-id="d69b5-266">Notez l’adresse IP du serveur de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-266">Note hello configuration server's IP address.</span></span> <span data-ttu-id="d69b5-267">Vous en avez besoin dans l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-267">You need it in hello next step.</span></span>

3. <span data-ttu-id="d69b5-268">Exécutez hello suivant du serveur cible maître de commande tooinstall hello et inscrire le serveur de hello avec le serveur de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-268">Run hello following command tooinstall hello master target server and register hello server with hello configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    <span data-ttu-id="d69b5-269">Exemple :</span><span class="sxs-lookup"><span data-stu-id="d69b5-269">Example:</span></span> 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    <span data-ttu-id="d69b5-270">Attendez la fin du script de hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-270">Wait until hello script finishes.</span></span> <span data-ttu-id="d69b5-271">Si le serveur cible maître hello inscrit avec succès, serveur cible maître hello est répertorié sur hello **Infrastructure Site Recovery** page du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-271">If hello master target registers sucessfully, hello master target is listed on hello **Site Recovery Infrastructure** page of hello portal.</span></span>


#### <a name="install-hello-master-target-by-using-interactive-installation"></a><span data-ttu-id="d69b5-272">Installer le serveur cible maître hello à l’aide d’une installation interactive</span><span class="sxs-lookup"><span data-stu-id="d69b5-272">Install hello master target by using interactive installation</span></span>

1. <span data-ttu-id="d69b5-273">Exécutez hello suivant cible de commande tooinstall hello maître.</span><span class="sxs-lookup"><span data-stu-id="d69b5-273">Run hello following command tooinstall hello master target.</span></span> <span data-ttu-id="d69b5-274">Pour le rôle de l’agent hello, choisissez **cible maître**.</span><span class="sxs-lookup"><span data-stu-id="d69b5-274">For hello agent role, choose **Master Target**.</span></span>

    ```
    ./install
    ```

2. <span data-ttu-id="d69b5-275">Choisissez l’emplacement par défaut de hello pour l’installation, puis sélectionnez **entrée** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="d69b5-275">Choose hello default location for installation, and then select **Enter** toocontinue.</span></span>

    ![Choix d’un emplacement par défaut pour l’installation du serveur cible maître](./media/site-recovery-how-to-install-linux-master-target/image17.png)

<span data-ttu-id="d69b5-277">Une fois l’installation de hello est terminée, inscrire le serveur de configuration de hello en utilisant la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-277">After hello installation has finished, register hello configuration server by using hello command line.</span></span>

1. <span data-ttu-id="d69b5-278">Notez l’adresse IP de hello hello du serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="d69b5-278">Note hello IP address of hello configuration server.</span></span> <span data-ttu-id="d69b5-279">Vous en avez besoin dans l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-279">You need it in hello next step.</span></span>

2. <span data-ttu-id="d69b5-280">Exécutez hello suivant du serveur cible maître de commande tooinstall hello et inscrire le serveur de hello avec le serveur de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-280">Run hello following command tooinstall hello master target server and register hello server with hello configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    <span data-ttu-id="d69b5-281">Exemple :</span><span class="sxs-lookup"><span data-stu-id="d69b5-281">Example:</span></span> 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   <span data-ttu-id="d69b5-282">Attendez la fin du script de hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-282">Wait until hello script finishes.</span></span> <span data-ttu-id="d69b5-283">Si le serveur cible maître hello est correctement inscrit, serveur cible maître hello est répertorié sur hello **Infrastructure Site Recovery** page du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-283">If hello master target is registered succesfully, hello master target is listed on hello **Site Recovery Infrastructure** page of hello portal.</span></span>


### <a name="upgrade-hello-master-target"></a><span data-ttu-id="d69b5-284">Mettre à niveau le serveur cible maître hello</span><span class="sxs-lookup"><span data-stu-id="d69b5-284">Upgrade hello master target</span></span>

<span data-ttu-id="d69b5-285">Exécutez le programme d’installation hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-285">Run hello installer.</span></span> <span data-ttu-id="d69b5-286">Il détecte automatiquement que l’agent hello est installé sur le serveur cible maître hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-286">It automatically detects that hello agent is installed on hello master target.</span></span> <span data-ttu-id="d69b5-287">tooupgrade, sélectionnez **Y**.  Après avoir hello le programme d’installation est terminée, vérifiez la version de hello du serveur cible maître hello installé à l’aide de hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="d69b5-287">tooupgrade, select **Y**.  After hello setup has been completed, check hello version of hello master target installed by using hello following command.</span></span>

    ```
    cat /usr/local/.vx_version
    ```

<span data-ttu-id="d69b5-288">Vous pouvez voir que hello **Version** champ indique le numéro de version de hello du serveur cible maître hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-288">You can see that hello **Version** field gives hello version number of hello master target.</span></span>

### <a name="install-vmware-tools-on-hello-master-target-server"></a><span data-ttu-id="d69b5-289">Installer les outils VMware sur le serveur cible maître de hello</span><span class="sxs-lookup"><span data-stu-id="d69b5-289">Install VMware tools on hello master target server</span></span>

<span data-ttu-id="d69b5-290">Vous devez tooinstall les outils VMware sur le serveur cible maître hello afin qu’il peut découvrir des magasins de données hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-290">You need tooinstall VMware tools on hello master target so that it can discover hello data stores.</span></span> <span data-ttu-id="d69b5-291">Si les outils hello ne sont pas installés, écran de reprotection hello n’est pas répertorié dans les magasins de données hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-291">If hello tools are not installed, hello reprotect screen isn't listed in hello data stores.</span></span> <span data-ttu-id="d69b5-292">Après l’installation des outils de hello VMware, vous devez toorestart.</span><span class="sxs-lookup"><span data-stu-id="d69b5-292">After installation of hello VMware tools, you need toorestart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d69b5-293">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d69b5-293">Next steps</span></span>
<span data-ttu-id="d69b5-294">Une fois l’installation de hello et l’inscription du serveur cible maître hello a finsihed, vous pouvez voir serveur cible maître hello apparaissent sur hello **cible maître** section **Infrastructure Site Recovery**, sous hello vue d’ensemble du serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="d69b5-294">After hello installation and registration of hello master target has finsihed, you can see hello master target appear on hello **Master Target** section in **Site Recovery Infrastructure**, under hello configuration server overview.</span></span>

<span data-ttu-id="d69b5-295">Vous pouvez maintenant procéder à la [reprotection](site-recovery-how-to-reprotect.md), puis à la restauration automatique.</span><span class="sxs-lookup"><span data-stu-id="d69b5-295">You can now proceed with [reprotection](site-recovery-how-to-reprotect.md), followed by failback.</span></span>

## <a name="common-issues"></a><span data-ttu-id="d69b5-296">Problèmes courants</span><span class="sxs-lookup"><span data-stu-id="d69b5-296">Common issues</span></span>

* <span data-ttu-id="d69b5-297">Veillez à ne pas activer Storage vMotion sur des composants de gestion tels qu’un serveur cible maître.</span><span class="sxs-lookup"><span data-stu-id="d69b5-297">Make sure you do not turn on Storage vMotion on any management components such as a master target.</span></span> <span data-ttu-id="d69b5-298">Si le serveur cible maître hello déplace après une reprotection réussie, les disques de machine virtuelle hello (VMDK) ne peut pas être détachées.</span><span class="sxs-lookup"><span data-stu-id="d69b5-298">If hello master target moves after a successful reprotect, hello virtual machine disks (VMDKs) cannot be detached.</span></span> <span data-ttu-id="d69b5-299">Dans ce cas, la restauration automatique échoue.</span><span class="sxs-lookup"><span data-stu-id="d69b5-299">In this case, failback fails.</span></span>

* <span data-ttu-id="d69b5-300">serveur cible maître Hello ne doit pas posséder de toutes les captures instantanées sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="d69b5-300">hello master target should not have any snapshots on hello virtual machine.</span></span> <span data-ttu-id="d69b5-301">Si des instantanés sont présents, la restauration automatique échoue.</span><span class="sxs-lookup"><span data-stu-id="d69b5-301">If there are snapshots, failback fails.</span></span>

* <span data-ttu-id="d69b5-302">En raison des configurations de carte réseau de personnalisée toosome à certains clients, interface de réseau hello est désactivée lors du démarrage et l’agent de hello cible maître ne peut pas initialiser.</span><span class="sxs-lookup"><span data-stu-id="d69b5-302">Due toosome custom NIC configurations at some customers, hello network interface is disabled during startup, and hello master target agent cannot initialize.</span></span> <span data-ttu-id="d69b5-303">Vérifiez que hello propriétés suivantes sont définies correctement.</span><span class="sxs-lookup"><span data-stu-id="d69b5-303">Make sure that hello following properties are correctly set.</span></span> <span data-ttu-id="d69b5-304">Vérifiez ces propriétés Bonjour Ethernet de carte /etc/sysconfig/network-scripts/ifcfg du fichier-eth *.</span><span class="sxs-lookup"><span data-stu-id="d69b5-304">Check these properties in hello Ethernet card file's /etc/sysconfig/network-scripts/ifcfg-eth*.</span></span>
    * <span data-ttu-id="d69b5-305">BOOTPROTO=dhcp</span><span class="sxs-lookup"><span data-stu-id="d69b5-305">BOOTPROTO=dhcp</span></span>
    * <span data-ttu-id="d69b5-306">ONBOOT=yes</span><span class="sxs-lookup"><span data-stu-id="d69b5-306">ONBOOT=yes</span></span>
