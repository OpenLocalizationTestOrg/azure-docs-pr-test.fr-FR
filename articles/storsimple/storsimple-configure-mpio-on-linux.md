---
title: "aaaConfigure MPIO sur un hôte Linux de StorSimple | Documents Microsoft"
description: "Configurer MPIO sur l’ordinateur hôte Linux StorSimple connecté tooa CentOS 6.6 en cours d’exécution"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: tysonn
ms.assetid: ca289eed-12b7-4e2e-9117-adf7e2034f2f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: alkohli
ms.openlocfilehash: d9f7e02903243494c909313fb2c33ac690764274
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a><span data-ttu-id="1098c-103">Configuration de MPIO sur un hôte StorSimple exécutant CentOS</span><span class="sxs-lookup"><span data-stu-id="1098c-103">Configure MPIO on a StorSimple host running CentOS</span></span>
<span data-ttu-id="1098c-104">Cet article explique hello étapes tooconfigure requis e/s de gestion multivoie (MPIO) sur un serveur hôte Centos 6.6.</span><span class="sxs-lookup"><span data-stu-id="1098c-104">This article explains hello steps required tooconfigure Multipathing IO (MPIO) on your Centos 6.6 host server.</span></span> <span data-ttu-id="1098c-105">serveur hôte de Hello est un appareil de Microsoft Azure StorSimple tooyour connecté pour la haute disponibilité via des initiateurs iSCSI.</span><span class="sxs-lookup"><span data-stu-id="1098c-105">hello host server is connected tooyour Microsoft Azure StorSimple device for high availability via iSCSI initiators.</span></span> <span data-ttu-id="1098c-106">Il décrit en détail hello la détection automatique des périphériques MPIO et hello spécifique le programme d’installation pour des volumes StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1098c-106">It describes in detail hello automatic discovery of multipath devices and hello specific setup only for StorSimple volumes.</span></span>

<span data-ttu-id="1098c-107">Cette procédure est applicable tooall des modèles de hello d’unités StorSimple 8000 series.</span><span class="sxs-lookup"><span data-stu-id="1098c-107">This procedure is applicable tooall hello models of StorSimple 8000 series devices.</span></span>

> [!NOTE]
> <span data-ttu-id="1098c-108">Cette procédure ne peut pas être utilisée pour un appareil virtuel StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1098c-108">This procedure cannot be used for a StorSimple virtual device.</span></span> <span data-ttu-id="1098c-109">Pour plus d’informations, consultez Comment tooconfigure hébergent les serveurs pour votre appareil virtuel.</span><span class="sxs-lookup"><span data-stu-id="1098c-109">For more information, see how tooconfigure host servers for your virtual device.</span></span>
> 
> 

## <a name="about-multipathing"></a><span data-ttu-id="1098c-110">À propos de la gestion multivoie</span><span class="sxs-lookup"><span data-stu-id="1098c-110">About multipathing</span></span>
<span data-ttu-id="1098c-111">fonctionnalité de gestion multivoie Hello vous permet de tooconfigure plusieurs chemins d’accès d’e/s entre un serveur hôte et un périphérique de stockage.</span><span class="sxs-lookup"><span data-stu-id="1098c-111">hello multipathing feature allows you tooconfigure multiple I/O paths between a host server and a storage device.</span></span> <span data-ttu-id="1098c-112">Ces chemins d’accès d’E/S sont des connexions SAN physiques pouvant inclure des câbles distincts, des commutateurs, des interfaces réseau et des contrôleurs.</span><span class="sxs-lookup"><span data-stu-id="1098c-112">These I/O paths are physical SAN connections that can include separate cables, switches, network interfaces, and controllers.</span></span> <span data-ttu-id="1098c-113">Chemins d’accès multiples agrège les chemins d’accès d’e/s hello, tooconfigure un nouveau périphérique qui est associé à tous les chemins d’accès hello agrégée.</span><span class="sxs-lookup"><span data-stu-id="1098c-113">Multipathing aggregates hello I/O paths, tooconfigure a new device that is associated with all of hello aggregated paths.</span></span>

<span data-ttu-id="1098c-114">objectif de Hello de chemins d’accès multiples est double :</span><span class="sxs-lookup"><span data-stu-id="1098c-114">hello purpose of multipathing is two-fold:</span></span>

* <span data-ttu-id="1098c-115">**Haute disponibilité**: il fournit un chemin alternatif en cas de n’importe quel élément du chemin d’accès de hello d’e/s (par exemple, un câble, un commutateur, une interface réseau ou un contrôleur).</span><span class="sxs-lookup"><span data-stu-id="1098c-115">**High availability**: It provides an alternate path if any element of hello I/O path (such as a cable, switch, network interface, or controller) fails.</span></span>
* <span data-ttu-id="1098c-116">**L’équilibrage de charge**: selon la configuration de hello votre dispositif de stockage, elle peut améliorer les performances de hello en détectant des charges sur les chemins d’accès d’e/s de hello et dynamiquement rééquilibrer les charges.</span><span class="sxs-lookup"><span data-stu-id="1098c-116">**Load balancing**: Depending on hello configuration of your storage device, it can improve hello performance by detecting loads on hello I/O paths and dynamically rebalancing those loads.</span></span>

### <a name="about-multipathing-components"></a><span data-ttu-id="1098c-117">À propos des composants de la gestion multivoie</span><span class="sxs-lookup"><span data-stu-id="1098c-117">About multipathing components</span></span>
<span data-ttu-id="1098c-118">Sous Linux, la gestion multivoie comprend des composants du noyau et des composants de l’espace utilisateur comme présenté ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1098c-118">Multipathing in Linux consists of kernel components and user-space components as tabulated below.</span></span>

* <span data-ttu-id="1098c-119">**Noyau**: composant principal de hello est hello *mappeur de périphérique* qui redirige les e/s et prend en charge de basculement pour les chemins d’accès et les groupes de chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="1098c-119">**Kernel**: hello main component is hello *device-mapper* that reroutes I/O and supports failover for paths and path groups.</span></span>

* <span data-ttu-id="1098c-120">**Espace utilisateur**: il s’agit *multipath-tools* qui permettent de gérer complémentaires appareils en demandant le module de chemins d’accès multiples hello-mise en correspondance le toodo.</span><span class="sxs-lookup"><span data-stu-id="1098c-120">**User-space**: These are *multipath-tools* that manage multipathed devices by instructing hello device-mapper multipath module what toodo.</span></span> <span data-ttu-id="1098c-121">outils de Hello se composent de :</span><span class="sxs-lookup"><span data-stu-id="1098c-121">hello tools consist of:</span></span>
   
   * <span data-ttu-id="1098c-122">**Multipath**: répertorie et configure les appareils à chemins d’accès multiples.</span><span class="sxs-lookup"><span data-stu-id="1098c-122">**Multipath**: lists and configures multipathed devices.</span></span>
   * <span data-ttu-id="1098c-123">**Multipathd**: démon qui exécute des chemins d’accès de hello MPIO et des analyses.</span><span class="sxs-lookup"><span data-stu-id="1098c-123">**Multipathd**: daemon that executes multipath and monitors hello paths.</span></span>
   * <span data-ttu-id="1098c-124">**Nom de devmap**: fournit un tooudev nom du périphérique significative pour devmaps.</span><span class="sxs-lookup"><span data-stu-id="1098c-124">**Devmap-name**: provides a meaningful device-name tooudev for devmaps.</span></span>
   * <span data-ttu-id="1098c-125">**Kpartx**: mappe devmaps linéaire toodevice partitions toomake MPIO maps avec partitions.</span><span class="sxs-lookup"><span data-stu-id="1098c-125">**Kpartx**: maps linear devmaps toodevice partitions toomake multipath maps partitionable.</span></span>
   * <span data-ttu-id="1098c-126">**Multipath.conf**: fichier de configuration de MPIO démon qui est utilisé toooverwrite hello configuration intégrée table.</span><span class="sxs-lookup"><span data-stu-id="1098c-126">**Multipath.conf**: configuration file for multipath daemon that is used toooverwrite hello built-in configuration table.</span></span>

### <a name="about-hello-multipathconf-configuration-file"></a><span data-ttu-id="1098c-127">Sur le fichier de configuration multipath.conf hello</span><span class="sxs-lookup"><span data-stu-id="1098c-127">About hello multipath.conf configuration file</span></span>
<span data-ttu-id="1098c-128">fichier de configuration Hello `/etc/multipath.conf` met un grand nombre de hello multivoie fonctionnalités configurables par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1098c-128">hello configuration file `/etc/multipath.conf` makes many of hello multipathing features user-configurable.</span></span> <span data-ttu-id="1098c-129">Hello `multipath` démon de noyau de commande et hello `multipathd` utiliser des informations figurant dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="1098c-129">hello `multipath` command and hello kernel daemon `multipathd` use information found in this file.</span></span> <span data-ttu-id="1098c-130">fichier de Hello est consulté uniquement lors de la configuration de hello de périphériques de chemins d’accès multiples hello.</span><span class="sxs-lookup"><span data-stu-id="1098c-130">hello file is consulted only during hello configuration of hello multipath devices.</span></span> <span data-ttu-id="1098c-131">Assurez-vous que toutes les modifications sont effectuées avant d’exécuter hello `multipath` commande.</span><span class="sxs-lookup"><span data-stu-id="1098c-131">Make sure that all changes are made before you run hello `multipath` command.</span></span> <span data-ttu-id="1098c-132">Si vous modifiez le fichier de hello par la suite, vous devez toostop et démarrer multipathd pour effet de tootake modifications hello.</span><span class="sxs-lookup"><span data-stu-id="1098c-132">If you modify hello file afterwards, you will need toostop and start multipathd again for hello changes tootake effect.</span></span>

<span data-ttu-id="1098c-133">Hello multipath.conf a cinq sections :</span><span class="sxs-lookup"><span data-stu-id="1098c-133">hello multipath.conf has five sections:</span></span>

- <span data-ttu-id="1098c-134">**Valeurs par défaut au niveau système***(defaults)*: vous pouvez remplacer les valeurs par défaut au niveau système.</span><span class="sxs-lookup"><span data-stu-id="1098c-134">**System level defaults** *(defaults)*: You can override system level defaults.</span></span>
- <span data-ttu-id="1098c-135">**Sur liste noire les appareils** *(liste de blocage)*: vous pouvez spécifier la liste hello des appareils qui ne doivent pas être contrôlés par le mappeur de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="1098c-135">**Blacklisted devices** *(blacklist)*: You can specify hello list of devices that should not be controlled by device-mapper.</span></span>
- <span data-ttu-id="1098c-136">**Blocage des exceptions** *(blacklist_exceptions)*: vous pouvez identifier toobe des appareils spécifiques considéré comme des périphériques MPIO même si répertoriés dans la liste de blocage hello.</span><span class="sxs-lookup"><span data-stu-id="1098c-136">**Blacklist exceptions** *(blacklist_exceptions)*: You can identify specific devices toobe treated as multipath devices even if listed in hello blacklist.</span></span>
- <span data-ttu-id="1098c-137">**Paramètres spécifiques de contrôleur de stockage** *(appareils)*: vous pouvez spécifier des paramètres de configuration qui seront appliqués toodevices qui contiennent des informations de produit et de fournisseur.</span><span class="sxs-lookup"><span data-stu-id="1098c-137">**Storage controller specific settings** *(devices)*: You can specify configuration settings that will be applied toodevices that have Vendor and Product information.</span></span>
- <span data-ttu-id="1098c-138">**Paramètres spécifiques d’appareil** *(multipaths)*: vous pouvez utiliser ce paramètres de configuration de section toofine ajuster hello pour les LUN individuelles.</span><span class="sxs-lookup"><span data-stu-id="1098c-138">**Device specific settings** *(multipaths)*: You can use this section toofine-tune hello configuration settings for individual LUNs.</span></span>

## <a name="configure-multipathing-on-storsimple-connected-toolinux-host"></a><span data-ttu-id="1098c-139">Configurer plusieurs chemins d’accès sur l’ordinateur hôte connecté tooLinux de StorSimple</span><span class="sxs-lookup"><span data-stu-id="1098c-139">Configure multipathing on StorSimple connected tooLinux host</span></span>
<span data-ttu-id="1098c-140">Un appareil connecté StorSimple tooa même hôte Linux peut être configuré pour la haute disponibilité et l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="1098c-140">A StorSimple device connected tooa Linux host can be configured for high availability and load balancing.</span></span> <span data-ttu-id="1098c-141">Par exemple, si le même hôte Linux hello possède deux interfaces toohello connecté les périphériques SAN et hello a deux interfaces connectées toohello SAN tels situés sur ces interfaces hello même sous-réseau, puis il y aura des chemins de 4 accès disponible.</span><span class="sxs-lookup"><span data-stu-id="1098c-141">For example, if hello Linux host has two interfaces connected toohello SAN and hello device has two interfaces connected toohello SAN such that these interfaces are on hello same subnet, then there will be 4 paths available.</span></span> <span data-ttu-id="1098c-142">Toutefois, si chaque interface de données sur l’interface de périphérique et l’hôte hello est sur un sous-réseau IP différent (et non routables), puis les chemins d’accès seulement 2 sera disponibles.</span><span class="sxs-lookup"><span data-stu-id="1098c-142">However, if each DATA interface on hello device and host interface are on a different IP subnet (and not routable), then only 2 paths will be available.</span></span> <span data-ttu-id="1098c-143">Vous pouvez configurer les chemins d’accès multiples tooautomatically découvrir tous les chemins d’accès disponibles hello, choisissez un algorithme d’équilibrage de charge pour les chemins d’accès, appliquer des paramètres de configuration spécifiques pour les volumes StorSimple uniquement, puis activer et vérifier les chemins d’accès multiples.</span><span class="sxs-lookup"><span data-stu-id="1098c-143">You can configure multipathing tooautomatically discover all hello available paths, choose a load-balancing algorithm for those paths, apply specific configuration settings for StorSimple-only volumes, and then enable and verify multipathing.</span></span>

<span data-ttu-id="1098c-144">Hello procédure suivante décrit comment plusieurs chemins d’accès tooconfigure lorsqu’un appareil StorSimple avec deux interfaces réseau hôte connecté tooa avec deux interfaces réseau.</span><span class="sxs-lookup"><span data-stu-id="1098c-144">hello following procedure describes how tooconfigure multipathing when a StorSimple device with two network interfaces is connected tooa host with two network interfaces.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1098c-145">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1098c-145">Prerequisites</span></span>
<span data-ttu-id="1098c-146">Cette section détaille hello configuration requise pour le serveur de CentOS et que votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1098c-146">This section details hello configuration prerequisites for CentOS server and your StorSimple device.</span></span>

### <a name="on-centos-host"></a><span data-ttu-id="1098c-147">Sur l’hôte CentOS</span><span class="sxs-lookup"><span data-stu-id="1098c-147">On CentOS host</span></span>
1. <span data-ttu-id="1098c-148">Assurez-vous que votre hôte CentOS possède 2 interfaces réseau activées.</span><span class="sxs-lookup"><span data-stu-id="1098c-148">Make sure that your CentOS host has 2 network interfaces enabled.</span></span> <span data-ttu-id="1098c-149">Entrez :</span><span class="sxs-lookup"><span data-stu-id="1098c-149">Type:</span></span>
   
    `ifconfig`
   
    <span data-ttu-id="1098c-150">Hello suivant montre la sortie de hello lorsque deux interfaces réseau (`eth0` et `eth1`) sont présents sur l’ordinateur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="1098c-150">hello following example shows hello output when two network interfaces (`eth0` and `eth1`) are present on hello host.</span></span>
   
        [root@centosSS ~]# ifconfig
        eth0  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:41  
          inet addr:10.126.162.65  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3341/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3341/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
         RX packets:36536 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6312 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:13994127 (13.3 MiB)  TX bytes:645654 (630.5 KiB)
   
        eth1  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:42  
          inet addr:10.126.162.66  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3342/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3342/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25962 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:2597350 (2.4 MiB)  TX bytes:754 (754.0 b)
   
        loLink encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:12 errors:0 dropped:0 overruns:0 frame:0
          TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:720 (720.0 b)  TX bytes:720 (720.0 b)
2. <span data-ttu-id="1098c-151">Installez *iSCSI-initiator-utils* sur votre serveur CentOS.</span><span class="sxs-lookup"><span data-stu-id="1098c-151">Install *iSCSI-initiator-utils* on your CentOS server.</span></span> <span data-ttu-id="1098c-152">Effectuer hello suivant les étapes tooinstall *iSCSI-initiateur-utils*.</span><span class="sxs-lookup"><span data-stu-id="1098c-152">Perform hello following steps tooinstall *iSCSI-initiator-utils*.</span></span>
   
   1. <span data-ttu-id="1098c-153">Connectez-vous en tant que `root` à votre hôte CentOS.</span><span class="sxs-lookup"><span data-stu-id="1098c-153">Log on as `root` into your CentOS host.</span></span>
   2. <span data-ttu-id="1098c-154">Installer hello *iSCSI-initiateur-utils*.</span><span class="sxs-lookup"><span data-stu-id="1098c-154">Install hello *iSCSI-initiator-utils*.</span></span> <span data-ttu-id="1098c-155">Entrez :</span><span class="sxs-lookup"><span data-stu-id="1098c-155">Type:</span></span>
      
       `yum install iscsi-initiator-utils`
   3. <span data-ttu-id="1098c-156">Après avoir hello *iSCSI-initiateur-utils* est correctement installé, démarrez le service iSCSI hello.</span><span class="sxs-lookup"><span data-stu-id="1098c-156">After hello *iSCSI-Initiator-utils* is successfully installed, start hello iSCSI service.</span></span> <span data-ttu-id="1098c-157">Entrez :</span><span class="sxs-lookup"><span data-stu-id="1098c-157">Type:</span></span>
      
       `service iscsid start`
      
       <span data-ttu-id="1098c-158">Il arrive, `iscsid` ne peut pas démarrer et hello `--force` option peut être nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1098c-158">On occasions, `iscsid` may not actually start and hello `--force` option may be needed</span></span>
   4. <span data-ttu-id="1098c-159">tooensure que votre initiateur iSCSI est activé lors du démarrage, utilisez hello `chkconfig` service de hello tooenable de commandes.</span><span class="sxs-lookup"><span data-stu-id="1098c-159">tooensure that your iSCSI initiator is enabled during boot time, use hello `chkconfig` command tooenable hello service.</span></span>
      
       `chkconfig iscsi on`
   5. <span data-ttu-id="1098c-160">tooverify qui il a été correctement le programme d’installation, exécutez la commande hello :</span><span class="sxs-lookup"><span data-stu-id="1098c-160">tooverify that that it was properly setup, run hello command:</span></span>
      
       `chkconfig --list | grep iscsi`
      
       <span data-ttu-id="1098c-161">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="1098c-161">A sample output is shown below.</span></span>
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       <span data-ttu-id="1098c-162">À partir de hello exemple ci-dessus, vous pouvez voir que votre environnement iSCSI s’exécutera sur l’heure de démarrage sur les niveaux d’exécution 2, 3, 4 et 5.</span><span class="sxs-lookup"><span data-stu-id="1098c-162">From hello above example, you can see that your iSCSI environment will run on boot time on run levels 2, 3, 4, and 5.</span></span>
3. <span data-ttu-id="1098c-163">Installez *device-mapper-multipath*.</span><span class="sxs-lookup"><span data-stu-id="1098c-163">Install *device-mapper-multipath*.</span></span> <span data-ttu-id="1098c-164">Entrez :</span><span class="sxs-lookup"><span data-stu-id="1098c-164">Type:</span></span>
   
    `yum install device-mapper-multipath`
   
    <span data-ttu-id="1098c-165">installation de Hello démarre.</span><span class="sxs-lookup"><span data-stu-id="1098c-165">hello installation will start.</span></span> <span data-ttu-id="1098c-166">Type **Y** toocontinue lorsque vous êtes invité à confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="1098c-166">Type **Y** toocontinue when prompted for confirmation.</span></span>

### <a name="on-storsimple-device"></a><span data-ttu-id="1098c-167">Sur l’appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="1098c-167">On StorSimple device</span></span>
<span data-ttu-id="1098c-168">Votre appareil StorSimple doit disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1098c-168">Your StorSimple device should have:</span></span>

* <span data-ttu-id="1098c-169">Deux interfaces activées pour iSCSI minimum.</span><span class="sxs-lookup"><span data-stu-id="1098c-169">A minimum of two interfaces enabled for iSCSI.</span></span> <span data-ttu-id="1098c-170">tooverify que les deux interfaces sont compatible iSCSI sur votre appareil StorSimple, procédez hello Bonjour portail classique Azure pour votre appareil StorSimple comme suit :</span><span class="sxs-lookup"><span data-stu-id="1098c-170">tooverify that two interfaces are iSCSI-enabled on your StorSimple device, perform hello following steps in hello Azure classic portal for your StorSimple device:</span></span>
  
  1. <span data-ttu-id="1098c-171">Vous connecter au portail classique de hello pour votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1098c-171">Log into hello classic portal for your StorSimple device.</span></span>
  2. <span data-ttu-id="1098c-172">Sélectionnez votre service StorSimple Manager, cliquez sur **périphériques** et choisissez l’appareil StorSimple spécifique hello.</span><span class="sxs-lookup"><span data-stu-id="1098c-172">Select your StorSimple Manager service, click **Devices** and choose hello specific StorSimple device.</span></span> <span data-ttu-id="1098c-173">Cliquez sur **configurer** et vérifiez les paramètres d’interface réseau hello.</span><span class="sxs-lookup"><span data-stu-id="1098c-173">Click **Configure** and verify hello network interface settings.</span></span> <span data-ttu-id="1098c-174">Une capture d’écran avec deux interfaces réseau compatibles iSCSI est affichée ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1098c-174">A screenshot with two iSCSI-enabled network interfaces is shown below.</span></span> <span data-ttu-id="1098c-175">Ici, pour DATA 2 et DATA 3, les deux interfaces 10 Gigabit Ethernet sont activées pour iSCSI.</span><span class="sxs-lookup"><span data-stu-id="1098c-175">Here DATA 2 and DATA 3, both 10 GbE interfaces are enabled for iSCSI.</span></span>
     
      ![Configuration de MPIO StorSimple DATA 2](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![Configuration de MPIO StorSimple DATA 3](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      <span data-ttu-id="1098c-178">Bonjour **configurer** page</span><span class="sxs-lookup"><span data-stu-id="1098c-178">In hello **Configure** page</span></span>
     
     1. <span data-ttu-id="1098c-179">Assurez-vous que les deux interfaces réseau sont compatibles iSCSI.</span><span class="sxs-lookup"><span data-stu-id="1098c-179">Ensure that both network interfaces are iSCSI-enabled.</span></span> <span data-ttu-id="1098c-180">Hello **compatible iSCSI** champ doit être défini trop**Oui**.</span><span class="sxs-lookup"><span data-stu-id="1098c-180">hello **iSCSI enabled** field should be set too**Yes**.</span></span>
     2. <span data-ttu-id="1098c-181">Assurez-vous que les interfaces réseau hello ont hello même vitesse, les deux doivent être de 1 GbE ou 10 GbE.</span><span class="sxs-lookup"><span data-stu-id="1098c-181">Ensure that hello network interfaces have hello same speed, both should be 1 GbE or 10 GbE.</span></span>
     3. <span data-ttu-id="1098c-182">Notez les adresses IPv4 de hello des interfaces de hello compatible iSCSI et enregistrer pour une utilisation ultérieure sur l’ordinateur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="1098c-182">Note hello IPv4 addresses of hello iSCSI-enabled interfaces and save for later use on hello host.</span></span>
* <span data-ttu-id="1098c-183">interfaces d’iSCSI Hello sur votre appareil StorSimple doivent être accessibles à partir du serveur de CentOS hello.</span><span class="sxs-lookup"><span data-stu-id="1098c-183">hello iSCSI interfaces on your StorSimple device should be reachable from hello CentOS server.</span></span>
      <span data-ttu-id="1098c-184">tooverify, vous devez les adresses IP tooprovide hello des interfaces réseau iSCSI StorSimple sur votre serveur hôte.</span><span class="sxs-lookup"><span data-stu-id="1098c-184">tooverify this, you need tooprovide hello IP addresses of your StorSimple iSCSI-enabled network interfaces on your host server.</span></span> <span data-ttu-id="1098c-185">Hello commandes utilisées et hello sortie correspondante avec DATA2 (10.126.162.25) et DATA3 (10.126.162.26) est indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1098c-185">hello commands used and hello corresponding output with DATA2 (10.126.162.25) and DATA3 (10.126.162.26) is shown below:</span></span>
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a><span data-ttu-id="1098c-186">Configuration matérielle</span><span class="sxs-lookup"><span data-stu-id="1098c-186">Hardware configuration</span></span>
<span data-ttu-id="1098c-187">Nous vous conseillons de vous connectez hello deux iSCSI interfaces réseau sur les chemins d’accès distincts pour assurer la redondance.</span><span class="sxs-lookup"><span data-stu-id="1098c-187">We recommend that you connect hello two iSCSI network interfaces on separate paths for redundancy.</span></span> <span data-ttu-id="1098c-188">figure Hello ci-dessous montre la configuration matérielle recommandée de hello pour la haute disponibilité et l’équilibrage de charge de gestion multivoie pour votre serveur de CentOS et l’appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1098c-188">hello figure below shows hello recommended hardware configuration for high availability and load-balancing multipathing for your CentOS server and StorSimple device.</span></span>

![Configuration matérielle de MPIO pour StorSimple tooLinux hôte](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

<span data-ttu-id="1098c-190">Comme indiqué dans hello précédant figure :</span><span class="sxs-lookup"><span data-stu-id="1098c-190">As shown in hello preceding figure:</span></span>

* <span data-ttu-id="1098c-191">Votre appareil StorSimple est une configuration active/passive avec deux contrôleurs.</span><span class="sxs-lookup"><span data-stu-id="1098c-191">Your StorSimple device is in an active-passive configuration with two controllers.</span></span>
* <span data-ttu-id="1098c-192">Deux commutateurs SAN sont des contrôleurs de périphériques connectés tooyour.</span><span class="sxs-lookup"><span data-stu-id="1098c-192">Two SAN switches are connected tooyour device controllers.</span></span>
* <span data-ttu-id="1098c-193">Deux initiateurs iSCSI sont activés sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1098c-193">Two iSCSI initiators are enabled on your StorSimple device.</span></span>
* <span data-ttu-id="1098c-194">Deux interfaces réseau sont activées sur votre hôte CentOS.</span><span class="sxs-lookup"><span data-stu-id="1098c-194">Two network interfaces are enabled on your CentOS host.</span></span>

<span data-ttu-id="1098c-195">Hello ci-dessus configuration produira 4 chemins d’accès distincts entre votre appareil et hello l’hôte si les interfaces hello hôte et les données sont routables.</span><span class="sxs-lookup"><span data-stu-id="1098c-195">hello above configuration will yield 4 separate paths between your device and hello host if hello host and data interfaces are routable.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="1098c-196">Nous vous recommandons de ne pas mélanger les interfaces réseau 1 Gigabit Ethernet et 10 Gigabit Ethernet pour la gestion multivoie.</span><span class="sxs-lookup"><span data-stu-id="1098c-196">We recommend that you do not mix 1 GbE and 10 GbE network interfaces for multipathing.</span></span> <span data-ttu-id="1098c-197">Lorsque vous utilisez deux interfaces réseau, les deux interfaces hello doivent être de type identiques de hello.</span><span class="sxs-lookup"><span data-stu-id="1098c-197">When using two network interfaces, both hello interfaces should be hello identical type.</span></span>
> * <span data-ttu-id="1098c-198">Sur votre appareil StorSimple, DATA0, DATA1, DATA4 et DATA5 sont des interfaces 1 Gigabit Ethernet, alors que DATA2 et DATA3 sont des interfaces réseau 10 Gigabit Ethernet.|</span><span class="sxs-lookup"><span data-stu-id="1098c-198">On your StorSimple device, DATA0, DATA1, DATA4 and DATA5 are 1 GbE interfaces whereas DATA2 and DATA3 are 10 GbE network interfaces.|</span></span>
> 
> 

## <a name="configuration-steps"></a><span data-ttu-id="1098c-199">Configuration</span><span class="sxs-lookup"><span data-stu-id="1098c-199">Configuration steps</span></span>
<span data-ttu-id="1098c-200">les étapes de configuration Hello pour les chemins d’accès multiples impliquent la configuration de hello les chemins disponibles pour la détection automatique, en spécifiant toouse algorithme hello l’équilibrage de charge, l’activation de plusieurs chemins d’accès et enfin vérification de la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="1098c-200">hello configuration steps for multipathing involve configuring hello available paths for automatic discovery, specifying hello load-balancing algorithm toouse, enabling multipathing and finally verifying hello configuration.</span></span> <span data-ttu-id="1098c-201">Chacune de ces étapes est décrite en détail dans les sections suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="1098c-201">Each of these steps is discussed in detail in hello following sections.</span></span>

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a><span data-ttu-id="1098c-202">Étape 1 : Configurer la gestion multivoie pour la détection automatique</span><span class="sxs-lookup"><span data-stu-id="1098c-202">Step 1: Configure multipathing for automatic discovery</span></span>
<span data-ttu-id="1098c-203">les appareils pris en charge MPIO Hello peuvent être automatiquement détectés et configurés.</span><span class="sxs-lookup"><span data-stu-id="1098c-203">hello multipath-supported devices can be automatically discovered and configured.</span></span>

1. <span data-ttu-id="1098c-204">Initialisez le fichier `/etc/multipath.conf` .</span><span class="sxs-lookup"><span data-stu-id="1098c-204">Initialize `/etc/multipath.conf` file.</span></span> <span data-ttu-id="1098c-205">Entrez :</span><span class="sxs-lookup"><span data-stu-id="1098c-205">Type:</span></span>
   
     `mpathconf --enable`
   
    <span data-ttu-id="1098c-206">Hello ci-dessus commande créera un `sample/etc/multipath.conf` fichier.</span><span class="sxs-lookup"><span data-stu-id="1098c-206">hello above command will create a `sample/etc/multipath.conf` file.</span></span>
2. <span data-ttu-id="1098c-207">Démarrez le service de gestion multivoie.</span><span class="sxs-lookup"><span data-stu-id="1098c-207">Start multipath service.</span></span> <span data-ttu-id="1098c-208">Entrez :</span><span class="sxs-lookup"><span data-stu-id="1098c-208">Type:</span></span>
   
    `service multipathd start`
   
    <span data-ttu-id="1098c-209">Vous verrez hello suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="1098c-209">You will see hello following output:</span></span>
   
    `Starting multipathd daemon:`
3. <span data-ttu-id="1098c-210">Activez la détection automatique des chemins d’accès multiples.</span><span class="sxs-lookup"><span data-stu-id="1098c-210">Enable automatic discovery of multipaths.</span></span> <span data-ttu-id="1098c-211">Entrez :</span><span class="sxs-lookup"><span data-stu-id="1098c-211">Type:</span></span>
   
    `mpathconf --find_multipaths y`
   
    <span data-ttu-id="1098c-212">Cela modifiera la section de paramètres par défaut hello de votre `multipath.conf` comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1098c-212">This will modify hello defaults section of your `multipath.conf` as shown below:</span></span>
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a><span data-ttu-id="1098c-213">Étape 2 : Configurer la gestion multivoie pour les volumes StorSimple</span><span class="sxs-lookup"><span data-stu-id="1098c-213">Step 2: Configure multipathing for StorSimple volumes</span></span>
<span data-ttu-id="1098c-214">Par défaut, tous les appareils sont noirs répertoriés dans le fichier de multipath.conf hello et seront ignorés.</span><span class="sxs-lookup"><span data-stu-id="1098c-214">By default, all devices are black listed in hello multipath.conf file and will be bypassed.</span></span> <span data-ttu-id="1098c-215">Vous devez toocreate blacklist exceptions tooallow multivoie pour les volumes à partir d’appareils StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1098c-215">You will need toocreate blacklist exceptions tooallow multipathing for volumes from StorSimple devices.</span></span>

1. <span data-ttu-id="1098c-216">Modifier hello `/etc/mulitpath.conf` fichier.</span><span class="sxs-lookup"><span data-stu-id="1098c-216">Edit hello `/etc/mulitpath.conf` file.</span></span> <span data-ttu-id="1098c-217">Entrez :</span><span class="sxs-lookup"><span data-stu-id="1098c-217">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="1098c-218">Recherchez la section de blacklist_exceptions de hello dans le fichier de multipath.conf hello.</span><span class="sxs-lookup"><span data-stu-id="1098c-218">Locate hello blacklist_exceptions section in hello multipath.conf file.</span></span> <span data-ttu-id="1098c-219">Votre appareil StorSimple doit toobe répertorié comme une exception de la liste de blocage dans cette section.</span><span class="sxs-lookup"><span data-stu-id="1098c-219">Your StorSimple device needs toobe listed as a blacklist exception in this section.</span></span> <span data-ttu-id="1098c-220">Vous pouvez ne pas commenter pertinentes de lignes dans cette toomodify fichier il comme indiqué ci-dessous (utilisez uniquement hello modèle spécifique de l’appareil que vous utilisez hello) :</span><span class="sxs-lookup"><span data-stu-id="1098c-220">You can uncomment relevant lines in this file toomodify it as shown below (use only hello specific model of hello device you are using):</span></span>
   
        blacklist_exceptions {
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8100*"
            }
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8600*"
            }
           }

### <a name="step-3-configure-round-robin-multipathing"></a><span data-ttu-id="1098c-221">Étape 3 : Configurer la gestion multivoie de tourniquet (round robin)</span><span class="sxs-lookup"><span data-stu-id="1098c-221">Step 3: Configure round-robin multipathing</span></span>
<span data-ttu-id="1098c-222">Cet algorithme d’équilibrage de charge utilise contrôleur actif de tous les hello toohello multipaths disponible de manière à charge équilibrée, tourniquet.</span><span class="sxs-lookup"><span data-stu-id="1098c-222">This load-balancing algorithm uses all hello available multipaths toohello active controller in a balanced, round-robin fashion.</span></span>

1. <span data-ttu-id="1098c-223">Modifier hello `/etc/multipath.conf` fichier.</span><span class="sxs-lookup"><span data-stu-id="1098c-223">Edit hello `/etc/multipath.conf` file.</span></span> <span data-ttu-id="1098c-224">Entrez :</span><span class="sxs-lookup"><span data-stu-id="1098c-224">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="1098c-225">Sous hello `defaults` section, jeu hello `path_grouping_policy` trop`multibus`.</span><span class="sxs-lookup"><span data-stu-id="1098c-225">Under hello `defaults` section, set hello `path_grouping_policy` too`multibus`.</span></span> <span data-ttu-id="1098c-226">Hello `path_grouping_policy` spécifie multipaths toounspecified tooapply de la stratégie hello par défaut chemin d’accès au regroupement.</span><span class="sxs-lookup"><span data-stu-id="1098c-226">hello `path_grouping_policy` specifies hello default path grouping policy tooapply toounspecified multipaths.</span></span> <span data-ttu-id="1098c-227">section des valeurs par défaut de Hello se présente comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1098c-227">hello defaults section will look as shown below.</span></span>
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> <span data-ttu-id="1098c-228">Hello les valeurs les plus courantes de `path_grouping_policy` incluent :</span><span class="sxs-lookup"><span data-stu-id="1098c-228">hello most common values of `path_grouping_policy` include:</span></span>
> 
> * <span data-ttu-id="1098c-229">basculement = 1 chemin d’accès par groupe de priorité</span><span class="sxs-lookup"><span data-stu-id="1098c-229">failover = 1 path per priority group</span></span>
> * <span data-ttu-id="1098c-230">multibus = tous les chemins d’accès valides dans 1 groupe de priorité</span><span class="sxs-lookup"><span data-stu-id="1098c-230">multibus = all valid paths in 1 priority group</span></span>
> 
> 

### <a name="step-4-enable-multipathing"></a><span data-ttu-id="1098c-231">Étape 4 : Activer la gestion multivoie</span><span class="sxs-lookup"><span data-stu-id="1098c-231">Step 4: Enable multipathing</span></span>
1. <span data-ttu-id="1098c-232">Redémarrez hello `multipathd` démon.</span><span class="sxs-lookup"><span data-stu-id="1098c-232">Restart hello `multipathd` daemon.</span></span> <span data-ttu-id="1098c-233">Entrez :</span><span class="sxs-lookup"><span data-stu-id="1098c-233">Type:</span></span>
   
    `service multipathd restart`
2. <span data-ttu-id="1098c-234">sortie de Hello sera comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1098c-234">hello output will be as shown below:</span></span>
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a><span data-ttu-id="1098c-235">Étape 5 : Vérifier la gestion multivoie</span><span class="sxs-lookup"><span data-stu-id="1098c-235">Step 5: Verify multipathing</span></span>
1. <span data-ttu-id="1098c-236">D’abord vous assurer que connexion iSCSI est établie avec l’appareil StorSimple hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1098c-236">First make sure that iSCSI connection is established with hello StorSimple device as follows:</span></span>
   
   <span data-ttu-id="1098c-237">a.</span><span class="sxs-lookup"><span data-stu-id="1098c-237">a.</span></span> <span data-ttu-id="1098c-238">Détectez votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1098c-238">Discover your StorSimple device.</span></span> <span data-ttu-id="1098c-239">Entrez :</span><span class="sxs-lookup"><span data-stu-id="1098c-239">Type:</span></span>
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on hello device>:<iSCSI port on StorSimple device>
    ```
    
    <span data-ttu-id="1098c-240">sortie Hello lorsque l’adresse IP DATA0 est 10.126.162.25 et port 3260 est ouvert sur l’appareil StorSimple hello pour le trafic iSCSI sortant est comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1098c-240">hello output when IP address for DATA0 is 10.126.162.25 and port 3260 is opened on hello StorSimple device for outbound iSCSI traffic is as shown below:</span></span>
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    <span data-ttu-id="1098c-241">Hello de copie IQN de votre appareil StorSimple, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, à partir de hello précédant la sortie.</span><span class="sxs-lookup"><span data-stu-id="1098c-241">Copy hello IQN of your StorSimple device, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, from hello preceding output.</span></span>

   <span data-ttu-id="1098c-242">b.</span><span class="sxs-lookup"><span data-stu-id="1098c-242">b.</span></span> <span data-ttu-id="1098c-243">Connectez appareil toohello à l’aide de IQN cible.</span><span class="sxs-lookup"><span data-stu-id="1098c-243">Connect toohello device using target IQN.</span></span> <span data-ttu-id="1098c-244">l’appareil StorSimple Hello est ici de cible iSCSI hello.</span><span class="sxs-lookup"><span data-stu-id="1098c-244">hello StorSimple device is hello iSCSI target here.</span></span> <span data-ttu-id="1098c-245">Entrez :</span><span class="sxs-lookup"><span data-stu-id="1098c-245">Type:</span></span>

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    <span data-ttu-id="1098c-246">Hello suivant montre la sortie avec une nom qualifié de la cible de `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span><span class="sxs-lookup"><span data-stu-id="1098c-246">hello following example shows output with a target IQN of `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span></span> <span data-ttu-id="1098c-247">sortie de Hello indique que vous avez correctement connecté deux interfaces réseau iSCSI de toohello sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="1098c-247">hello output indicates that you have successfully connected toohello two iSCSI-enabled network interfaces on your device.</span></span>

    ```
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    <span data-ttu-id="1098c-248">Si vous voyez l’interface qu’un seul hôte et deux chemins d’accès ici, vous devez tooenable les deux interfaces hello sur l’ordinateur hôte iSCSI.</span><span class="sxs-lookup"><span data-stu-id="1098c-248">If you see only one host interface and two paths here, then you need tooenable both hello interfaces on host for iSCSI.</span></span> <span data-ttu-id="1098c-249">Vous pouvez suivre hello [des instructions dans la documentation de Linux](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span><span class="sxs-lookup"><span data-stu-id="1098c-249">You can follow hello [detailed instructions in Linux documentation](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span></span>

2. <span data-ttu-id="1098c-250">Un volume est un serveur de CentOS toohello exposé à partir de l’appareil StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="1098c-250">A volume is exposed toohello CentOS server from hello StorSimple device.</span></span> <span data-ttu-id="1098c-251">Pour plus d’informations, consultez [étape 6 : création d’un volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via hello portail classique Azure sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1098c-251">For more information, see [Step 6: Create a volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via hello Azure classic portal on your StorSimple device.</span></span>

3. <span data-ttu-id="1098c-252">Vérifiez les chemins d’accès disponibles hello.</span><span class="sxs-lookup"><span data-stu-id="1098c-252">Verify hello available paths.</span></span> <span data-ttu-id="1098c-253">Entrez :</span><span class="sxs-lookup"><span data-stu-id="1098c-253">Type:</span></span>

      ```
      multipath –l
      ```

      <span data-ttu-id="1098c-254">Hello, l’exemple suivant montre la sortie hello pour les deux interfaces réseau sur une interface réseau StorSimple périphérique connecté tooa hôte unique, avec deux chemins d’accès disponibles.</span><span class="sxs-lookup"><span data-stu-id="1098c-254">hello following example shows hello output for two network interfaces on a StorSimple device connected tooa single host network interface with two available paths.</span></span>

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        hello following example shows hello output for two network interfaces on a StorSimple device connected tootwo host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After hello paths are configured, refer toohello specific instructions on your host operating system (Centos 6.6) toomount and format this volume.

## <a name="troubleshoot-multipathing"></a><span data-ttu-id="1098c-255">Résolution des problèmes de la gestion multivoie</span><span class="sxs-lookup"><span data-stu-id="1098c-255">Troubleshoot multipathing</span></span>
<span data-ttu-id="1098c-256">Cette section fournit des conseils utiles si vous rencontrez des problèmes lors de la configuration de la gestion multivoie.</span><span class="sxs-lookup"><span data-stu-id="1098c-256">This section provides some helpful tips if you run into any issues during multipathing configuration.</span></span>

<span data-ttu-id="1098c-257">Q :</span><span class="sxs-lookup"><span data-stu-id="1098c-257">Q.</span></span> <span data-ttu-id="1098c-258">Je ne vois pas les modifications de hello dans `multipath.conf` fichier prennent effet.</span><span class="sxs-lookup"><span data-stu-id="1098c-258">I do not see hello changes in `multipath.conf` file taking effect.</span></span>

<span data-ttu-id="1098c-259">R :</span><span class="sxs-lookup"><span data-stu-id="1098c-259">A.</span></span> <span data-ttu-id="1098c-260">Si vous avez apporté les modifications de toohello `multipath.conf` fichier, vous devrez le service de gestion multivoie toorestart hello.</span><span class="sxs-lookup"><span data-stu-id="1098c-260">If you have made any changes toohello `multipath.conf` file, you will need toorestart hello multipathing service.</span></span> <span data-ttu-id="1098c-261">Tapez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1098c-261">Type hello following command:</span></span>

    service multipathd restart

<span data-ttu-id="1098c-262">Q :</span><span class="sxs-lookup"><span data-stu-id="1098c-262">Q.</span></span> <span data-ttu-id="1098c-263">J’ai activé un deux interfaces réseau sur l’appareil StorSimple hello et deux interfaces réseau sur l’ordinateur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="1098c-263">I have enabled two network interfaces on hello StorSimple device and two network interfaces on hello host.</span></span> <span data-ttu-id="1098c-264">Lorsque la liste de chemins d’accès disponibles de hello, je vois uniquement deux chemins d’accès.</span><span class="sxs-lookup"><span data-stu-id="1098c-264">When I list hello available paths, I see only two paths.</span></span> <span data-ttu-id="1098c-265">Chemins d’accès disponibles quatre toosee prévu.</span><span class="sxs-lookup"><span data-stu-id="1098c-265">I expected toosee four available paths.</span></span>

<span data-ttu-id="1098c-266">R :</span><span class="sxs-lookup"><span data-stu-id="1098c-266">A.</span></span> <span data-ttu-id="1098c-267">Vérifiez que hello deux chemins sur hello même sous-réseau et routable.</span><span class="sxs-lookup"><span data-stu-id="1098c-267">Make sure that hello two paths are on hello same subnet and routable.</span></span> <span data-ttu-id="1098c-268">Si les interfaces réseau hello se trouvent sur différents réseaux locaux virtuels et non routables, vous verrez uniquement deux chemins d’accès.</span><span class="sxs-lookup"><span data-stu-id="1098c-268">If hello network interfaces are on different vLANs and not routable, you will see only two paths.</span></span> <span data-ttu-id="1098c-269">Une façon tooverify il s’agit de toomake assurer que vous pouvez joindre les deux interfaces d’hôte hello à partir d’une interface réseau sur l’appareil StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="1098c-269">One way tooverify this is toomake sure that you can reach both hello host interfaces from a network interface on hello StorSimple device.</span></span> <span data-ttu-id="1098c-270">Vous devez trop[contactez le Support Microsoft](storsimple-contact-microsoft-support.md) que cette vérification peut uniquement être effectuée via une session de support.</span><span class="sxs-lookup"><span data-stu-id="1098c-270">You will need too[contact Microsoft Support](storsimple-contact-microsoft-support.md) as this verification can only be done via a support session.</span></span>

<span data-ttu-id="1098c-271">Q :</span><span class="sxs-lookup"><span data-stu-id="1098c-271">Q.</span></span> <span data-ttu-id="1098c-272">Lorsque je répertorie les chemins d’accès disponibles, je ne vois aucune sortie.</span><span class="sxs-lookup"><span data-stu-id="1098c-272">When I list available paths, I do not see any output.</span></span>

<span data-ttu-id="1098c-273">R :</span><span class="sxs-lookup"><span data-stu-id="1098c-273">A.</span></span> <span data-ttu-id="1098c-274">En règle générale, ne subit des chemins d’accès complémentaires suggère un problème avec le démon de chemins d’accès multiples hello et il est très probablement que n’importe quel problème ici se trouve dans hello `multipath.conf` fichier.</span><span class="sxs-lookup"><span data-stu-id="1098c-274">Typically, not seeing any multipathed paths suggests a problem with hello multipathing daemon, and it’s most likely that any problem here lies in hello `multipath.conf` file.</span></span>

<span data-ttu-id="1098c-275">Il est également important de vérifier que vous permet de visualiser certains disques après la connexion toohello cible, car aucune réponse à partir des listes de chemins d’accès multiples hello ne peut aussi signifier que vous n’avez pas tous les disques.</span><span class="sxs-lookup"><span data-stu-id="1098c-275">It would also be worth checking that you can actually see some disks after connecting toohello target, as no response from hello multipath listings could also mean you don’t have any disks.</span></span>

* <span data-ttu-id="1098c-276">Utilisez hello suivant bus SCSI de commande toorescan hello :</span><span class="sxs-lookup"><span data-stu-id="1098c-276">Use hello following command toorescan hello SCSI bus:</span></span>
  
    <span data-ttu-id="1098c-277">`$ rescan-scsi-bus.sh `(partie du package sg3_utils)</span><span class="sxs-lookup"><span data-stu-id="1098c-277">`$ rescan-scsi-bus.sh `(part of sg3_utils package)</span></span>
* <span data-ttu-id="1098c-278">Tapez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="1098c-278">Type hello following commands:</span></span>
  
    `$ dmesg | grep sd*`
     
     <span data-ttu-id="1098c-279">Ou</span><span class="sxs-lookup"><span data-stu-id="1098c-279">Or</span></span>
  
    `$ fdisk –l`
  
    <span data-ttu-id="1098c-280">Celles-ci renverront les détails des disques récemment ajoutés.</span><span class="sxs-lookup"><span data-stu-id="1098c-280">These will return details of recently added disks.</span></span>
* <span data-ttu-id="1098c-281">toodetermine s’il s’agit d’un disque StorSimple, utilisez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="1098c-281">toodetermine whether it is a StorSimple disk, use hello following commands:</span></span>
  
    `cat /sys/block/<DISK>/device/model`
  
    <span data-ttu-id="1098c-282">Cela renvoie une chaîne qui déterminera s’il s’agit d’un disque StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1098c-282">This will return a string, which will determine if it’s a StorSimple disk.</span></span>

<span data-ttu-id="1098c-283">Cause moins probable mais possible, la présence d’un PID iSCSI obsolète.</span><span class="sxs-lookup"><span data-stu-id="1098c-283">A less likely but possible cause could also be stale iscsid pid.</span></span> <span data-ttu-id="1098c-284">Utilisez hello suivant commande toolog hors tension à partir des sessions iSCSI hello :</span><span class="sxs-lookup"><span data-stu-id="1098c-284">Use hello following command toolog off from hello iSCSI sessions:</span></span>

    iscsiadm -m node --logout -p <Target_IP>

<span data-ttu-id="1098c-285">Répétez cette commande pour toutes les interfaces réseau de hello connecté sur la cible iSCSI hello, qui est votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1098c-285">Repeat this command for all hello connected network interfaces on hello iSCSI target, which is your StorSimple device.</span></span> <span data-ttu-id="1098c-286">Une fois que vous avez déconnecté de toutes les sessions iSCSI de hello, utilisez session iSCSI de hello iSCSI cible IQN tooreestablish hello.</span><span class="sxs-lookup"><span data-stu-id="1098c-286">Once you have logged off from all hello iSCSI sessions, use hello iSCSI target IQN tooreestablish hello iSCSI session.</span></span> <span data-ttu-id="1098c-287">Tapez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1098c-287">Type hello following command:</span></span>

    iscsiadm -m node --login -T <TARGET_IQN>


<span data-ttu-id="1098c-288">Q :</span><span class="sxs-lookup"><span data-stu-id="1098c-288">Q.</span></span> <span data-ttu-id="1098c-289">Je ne sais pas si mon appareil figure dans la liste approuvée.</span><span class="sxs-lookup"><span data-stu-id="1098c-289">I am not sure if my device is whitelisted.</span></span>

<span data-ttu-id="1098c-290">R :</span><span class="sxs-lookup"><span data-stu-id="1098c-290">A.</span></span> <span data-ttu-id="1098c-291">tooverify si votre appareil est dans la liste approuvée, utilisez hello commande interactive dépannage suivante :</span><span class="sxs-lookup"><span data-stu-id="1098c-291">tooverify whether your device is whitelisted, use hello following troubleshooting interactive command:</span></span>

    multipathd –k
    multipathd> show devices
    available block devices:
    ram0 devnode blacklisted, unmonitored
    ram1 devnode blacklisted, unmonitored
    ram2 devnode blacklisted, unmonitored
    ram3 devnode blacklisted, unmonitored
    ram4 devnode blacklisted, unmonitored
    ram5 devnode blacklisted, unmonitored
    ram6 devnode blacklisted, unmonitored
    ram7 devnode blacklisted, unmonitored
    ram8 devnode blacklisted, unmonitored
    ram9 devnode blacklisted, unmonitored
    ram10 devnode blacklisted, unmonitored
    ram11 devnode blacklisted, unmonitored
    ram12 devnode blacklisted, unmonitored
    ram13 devnode blacklisted, unmonitored
    ram14 devnode blacklisted, unmonitored
    ram15 devnode blacklisted, unmonitored
    loop0 devnode blacklisted, unmonitored
    loop1 devnode blacklisted, unmonitored
    loop2 devnode blacklisted, unmonitored
    loop3 devnode blacklisted, unmonitored
    loop4 devnode blacklisted, unmonitored
    loop5 devnode blacklisted, unmonitored
    loop6 devnode blacklisted, unmonitored
    loop7 devnode blacklisted, unmonitored
    sr0 devnode blacklisted, unmonitored
    sda devnode whitelisted, monitored
    dm-0 devnode blacklisted, unmonitored
    dm-1 devnode blacklisted, unmonitored
    dm-2 devnode blacklisted, unmonitored
    sdb devnode whitelisted, monitored
    sdc devnode whitelisted, monitored
    dm-3 devnode blacklisted, unmonitored


<span data-ttu-id="1098c-292">Pour plus d’informations, consultez trop[utiliser la résolution des problèmes de commande interactive pour les chemins d’accès multiples](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span><span class="sxs-lookup"><span data-stu-id="1098c-292">For more information, go too[use troubleshooting interactive command for multipathing](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span></span>

## <a name="list-of-useful-commands"></a><span data-ttu-id="1098c-293">Liste des commandes utiles</span><span class="sxs-lookup"><span data-stu-id="1098c-293">List of useful commands</span></span>
| <span data-ttu-id="1098c-294">Tapez </span><span class="sxs-lookup"><span data-stu-id="1098c-294">Type</span></span> | <span data-ttu-id="1098c-295">Commande</span><span class="sxs-lookup"><span data-stu-id="1098c-295">Command</span></span> | <span data-ttu-id="1098c-296">Description</span><span class="sxs-lookup"><span data-stu-id="1098c-296">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1098c-297">**iSCSI**</span><span class="sxs-lookup"><span data-stu-id="1098c-297">**iSCSI**</span></span> |`service iscsid start` |<span data-ttu-id="1098c-298">Démarrer le service iSCSI</span><span class="sxs-lookup"><span data-stu-id="1098c-298">Start iSCSI service</span></span> |
| &nbsp; |`service iscsid stop` |<span data-ttu-id="1098c-299">Arrêter le service iSCSI</span><span class="sxs-lookup"><span data-stu-id="1098c-299">Stop iSCSI service</span></span> |
| &nbsp; |`service iscsid restart` |<span data-ttu-id="1098c-300">Redémarrer le service iSCSI</span><span class="sxs-lookup"><span data-stu-id="1098c-300">Restart iSCSI service</span></span> |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |<span data-ttu-id="1098c-301">Découvrir les cibles disponibles sur hello spécifié adresse</span><span class="sxs-lookup"><span data-stu-id="1098c-301">Discover available targets on hello specified address</span></span> |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |<span data-ttu-id="1098c-302">Connectez-vous à toohello de cible iSCSI</span><span class="sxs-lookup"><span data-stu-id="1098c-302">Log in toohello iSCSI target</span></span> |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |<span data-ttu-id="1098c-303">Se déconnecter du serveur cible iSCSI hello</span><span class="sxs-lookup"><span data-stu-id="1098c-303">Log out from hello iSCSI target</span></span> |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |<span data-ttu-id="1098c-304">Imprimer le nom de l'initiateur iSCSI</span><span class="sxs-lookup"><span data-stu-id="1098c-304">Print iSCSI initiator name</span></span> |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |<span data-ttu-id="1098c-305">Vérifier l’état de hello de session iSCSI de hello et volume détectés sur l’ordinateur hôte de hello</span><span class="sxs-lookup"><span data-stu-id="1098c-305">Check hello state of hello iSCSI session and volume discovered on hello host</span></span> |
| &nbsp; |`iscsi –m session` |<span data-ttu-id="1098c-306">Affiche toutes les sessions iSCSI de hello établies entre l’appareil StorSimple hello et un hôte de hello</span><span class="sxs-lookup"><span data-stu-id="1098c-306">Shows all hello iSCSI sessions established between hello host and hello StorSimple device</span></span> |
|  | | |
| <span data-ttu-id="1098c-307">**Gestion multivoie**</span><span class="sxs-lookup"><span data-stu-id="1098c-307">**Multipathing**</span></span> |`service multipathd start` |<span data-ttu-id="1098c-308">Démarrer le démon multivoie</span><span class="sxs-lookup"><span data-stu-id="1098c-308">Start multipath daemon</span></span> |
| &nbsp; |`service multipathd stop` |<span data-ttu-id="1098c-309">Arrêter le démon multivoie</span><span class="sxs-lookup"><span data-stu-id="1098c-309">Stop multipath daemon</span></span> |
| &nbsp; |`service multipathd restart` |<span data-ttu-id="1098c-310">Redémarrer le démon multivoie</span><span class="sxs-lookup"><span data-stu-id="1098c-310">Restart multipath daemon</span></span> |
| &nbsp; |`chkconfig multipathd on` </br> <span data-ttu-id="1098c-311">OU</span><span class="sxs-lookup"><span data-stu-id="1098c-311">OR</span></span> </br> `mpathconf –with_chkconfig y` |<span data-ttu-id="1098c-312">Activer les chemins d’accès multiples démon toostart au moment du démarrage</span><span class="sxs-lookup"><span data-stu-id="1098c-312">Enable multipath daemon toostart at boot time</span></span> |
| &nbsp; |`multipathd –k` |<span data-ttu-id="1098c-313">Démarrez la console interactive de hello pour la résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="1098c-313">Start hello interactive console for troubleshooting</span></span> |
| &nbsp; |`multipath –l` |<span data-ttu-id="1098c-314">Lister les connexions et les périphériques multivoie</span><span class="sxs-lookup"><span data-stu-id="1098c-314">List multipath connections and devices</span></span> |
| &nbsp; |`mpathconf --enable` |<span data-ttu-id="1098c-315">Créer un exemple de fichier mulitpath.conf dans `/etc/mulitpath.conf`</span><span class="sxs-lookup"><span data-stu-id="1098c-315">Create a sample mulitpath.conf file in `/etc/mulitpath.conf`</span></span> |
|  | | |

## <a name="next-steps"></a><span data-ttu-id="1098c-316">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1098c-316">Next steps</span></span>
<span data-ttu-id="1098c-317">Comme vous configurez MPIO sur un hôte Linux, vous devrez peut-être également toohello toorefer suivant CentoS 6.6 documents :</span><span class="sxs-lookup"><span data-stu-id="1098c-317">As you are configuring MPIO on Linux host, you may also need toorefer toohello following CentoS 6.6 documents:</span></span>

* [<span data-ttu-id="1098c-318">Configuration de MPIO sur CentOS</span><span class="sxs-lookup"><span data-stu-id="1098c-318">Setting up MPIO on CentOS</span></span>](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [<span data-ttu-id="1098c-319">Guide de formation Linux</span><span class="sxs-lookup"><span data-stu-id="1098c-319">Linux Training Guide</span></span>](http://linux-training.be/files/books/LinuxAdm.pdf)

