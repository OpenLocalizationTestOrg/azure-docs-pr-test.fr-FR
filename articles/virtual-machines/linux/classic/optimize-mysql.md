---
title: aaaOptimize des performances de MySQL sur Linux | Documents Microsoft
description: "Découvrez comment toooptimize MySQL en cours d’exécution sur une machine virtuelle Azure (VM) Linux en cours d’exécution."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0c1c7fc5-a528-4d84-b65d-2df225f2233f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: ningk
ms.openlocfilehash: 9e6458723233721e06f30b9de33635d403eefcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a><span data-ttu-id="7a0b5-103">Optimiser les performances de MySQL sur les machines virtuelles Linux Azure</span><span class="sxs-lookup"><span data-stu-id="7a0b5-103">Optimize MySQL Performance on Azure Linux VMs</span></span>
<span data-ttu-id="7a0b5-104">De nombreux facteurs, en matière de choix de matériel virtuel et de configuration logicielle, ont une incidence sur les performances de MySQL sur Azure.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-104">There are many factors that affect MySQL performance on Azure, both in virtual hardware selection and software configuration.</span></span> <span data-ttu-id="7a0b5-105">Cet article se concentre sur l’optimisation des performances grâce aux configurations de stockage, système et de base de données.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-105">This article focuses on optimizing performance through storage, system, and database configurations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a0b5-106">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager](../../../resource-manager-deployment-model.md) et classique.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="7a0b5-107">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-107">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="7a0b5-108">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="7a0b5-109">Pour plus d’informations sur les optimisations de Linux VM avec modèle de gestionnaire de ressources hello, consultez [optimiser votre VM Linux sur Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7a0b5-109">For information about Linux VM optimizations with hello Resource Manager model, see [Optimize your Linux VM on Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="utilize-raid-on-an-azure-virtual-machine"></a><span data-ttu-id="7a0b5-110">Utiliser RAID sur une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="7a0b5-110">Utilize RAID on an Azure virtual machine</span></span>
<span data-ttu-id="7a0b5-111">Le stockage est un facteur clé hello qui affecte les performances de base de données dans les environnements de cloud.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-111">Storage is hello key factor that affects database performance in cloud environments.</span></span> <span data-ttu-id="7a0b5-112">Disque unique tooa comparés RAID peut fournir un accès plus rapide via la concurrence.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-112">Compared tooa single disk, RAID can provide faster access via concurrency.</span></span> <span data-ttu-id="7a0b5-113">Pour plus d’informations, consultez [Niveaux RAID standard](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span><span class="sxs-lookup"><span data-stu-id="7a0b5-113">For more information, see [Standard RAID levels](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span></span>   

<span data-ttu-id="7a0b5-114">Le débit d’E/S disque et le temps de réponse d’E/S dans Azure peuvent être améliorés grâce à RAID.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-114">Disk I/O throughput and I/O response time in Azure can be improved through RAID.</span></span> <span data-ttu-id="7a0b5-115">Nos tests de laboratoire montrent que débit d’e/s disque peut être doublé et temps de réponse d’e/s peut être réduit de moitié en moyenne lorsque le nombre de hello de disques RAID est doublé (à partir de deux toofour, quatre tooeight, etc.).</span><span class="sxs-lookup"><span data-stu-id="7a0b5-115">Our lab tests show that disk I/O throughput can be doubled and I/O response time can be reduced by half on average when hello number of RAID disks is doubled (from two toofour, four tooeight, etc.).</span></span> <span data-ttu-id="7a0b5-116">Voir l’ [annexe A](#AppendixA) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-116">See [Appendix A](#AppendixA) for details.</span></span>  

<span data-ttu-id="7a0b5-117">En outre e/s toodisk MySQL performances sont améliorées lorsque vous augmentez le niveau RAID de hello.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-117">In addition toodisk I/O, MySQL performance improves when you increase hello RAID level.</span></span>  <span data-ttu-id="7a0b5-118">Voir l’ [annexe B](#AppendixB) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-118">See [Appendix B](#AppendixB) for details.</span></span>  

<span data-ttu-id="7a0b5-119">Vous pourriez également la taille de segment tooconsider hello.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-119">You might also want tooconsider hello chunk size.</span></span> <span data-ttu-id="7a0b5-120">En règle générale, lorsque vous disposez d’une plus grande taille de segment, vous obtenez une surcharge inférieure, en particulier pour les écritures de grande taille.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-120">In general, when you have a larger chunk size, you get lower overhead, especially for large writes.</span></span> <span data-ttu-id="7a0b5-121">Toutefois, lorsque la taille de segment hello est trop volumineux, il peut ajouter une charge supplémentaire qui vous empêche de tirer parti de RAID.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-121">However, when hello chunk size is too large, it might add additional overhead that prevents you from taking advantage of RAID.</span></span> <span data-ttu-id="7a0b5-122">taille par défaut actuel de Hello est de 512 Ko, ce qui s’avère idéal pour les environnements de production plus générales toobe.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-122">hello current default size is 512 KB, which is proven toobe optimal for most general production environments.</span></span> <span data-ttu-id="7a0b5-123">Voir l’ [annexe C](#AppendixC) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-123">See [Appendix C](#AppendixC) for details.</span></span>   

<span data-ttu-id="7a0b5-124">Il existe des limites sur le nombre de disques que vous pouvez ajouter, selon le type de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-124">There are limits on how many disks you can add for different virtual machine types.</span></span> <span data-ttu-id="7a0b5-125">Ces limites sont présentées en détail sur la page [Tailles de machines virtuelles et services cloud pour Microsoft Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="7a0b5-125">These limits are detailed in [Virtual machine and cloud service sizes for Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span> <span data-ttu-id="7a0b5-126">Vous aurez besoin dans les données attachées disques toofollow hello RAID par exemple dans cet article, mais vous pouvez choisir tooset RAID avec moins de disques.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-126">You will need four attached data disks toofollow hello RAID example in this article, although you can choose tooset up RAID with fewer disks.</span></span>  

<span data-ttu-id="7a0b5-127">Cet article suppose que vous avez déjà créé une machine virtuelle Linux et que MYSQL est installé et configuré.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-127">This article assumes you have already created a Linux virtual machine and have MYSQL installed and configured.</span></span> <span data-ttu-id="7a0b5-128">Pour plus d’informations sur la prise en main, consultez Comment tooinstall MySQL sur Azure.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-128">For more information on getting started, see How tooinstall MySQL on Azure.</span></span>  

### <a name="set-up-raid-on-azure"></a><span data-ttu-id="7a0b5-129">Configurer RAID sur Azure</span><span class="sxs-lookup"><span data-stu-id="7a0b5-129">Set up RAID on Azure</span></span>
<span data-ttu-id="7a0b5-130">Hello étapes suivantes montrent comment toocreate RAID sur Azure à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-130">hello following steps show how toocreate RAID on Azure by using hello Azure portal.</span></span> <span data-ttu-id="7a0b5-131">Vous pouvez également configurer RAID à l’aide de scripts Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-131">You can also set up RAID by using Windows PowerShell scripts.</span></span>
<span data-ttu-id="7a0b5-132">Dans cet exemple, nous allons configurer RAID 0 avec quatre disques.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-132">In this example, we will configure RAID 0 with four disks.</span></span>  

#### <a name="add-a-data-disk-tooyour-virtual-machine"></a><span data-ttu-id="7a0b5-133">Ajouter un ordinateur virtuel de données disque tooyour</span><span class="sxs-lookup"><span data-stu-id="7a0b5-133">Add a data disk tooyour virtual machine</span></span>
<span data-ttu-id="7a0b5-134">Bonjour portail Azure, accédez toohello le tableau de bord et sélectionnez hello toowhich de machine virtuelle souhaité tooadd un disque de données.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-134">In hello Azure portal, go toohello dashboard and select hello virtual machine toowhich you want tooadd a data disk.</span></span> <span data-ttu-id="7a0b5-135">Dans cet exemple, la machine virtuelle de hello est mysqlnode1.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-135">In this example, hello virtual machine is mysqlnode1.</span></span>  

<!--![Virtual machines][1]-->

<span data-ttu-id="7a0b5-136">Cliquez sur **Disques**, puis cliquez sur **Attach New** (Attacher nouveau).</span><span class="sxs-lookup"><span data-stu-id="7a0b5-136">Click **Disks** and then click **Attach New**.</span></span>

![Les machines virtuelles ajoutent des disques.](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

<span data-ttu-id="7a0b5-138">Créez un nouveau disque de 500 Go.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-138">Create a new 500 GB disk.</span></span> <span data-ttu-id="7a0b5-139">Assurez-vous que **préférences de Cache hôte** est défini trop**aucun**.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-139">Make sure that **Host Cache Preference** is set too**None**.</span></span>  <span data-ttu-id="7a0b5-140">Lorsque vous avez terminé, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-140">When you're finished, click **OK**.</span></span>

![Attacher un disque vide](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


<span data-ttu-id="7a0b5-142">Cela ajoute un disque vide à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-142">This adds one empty disk into your virtual machine.</span></span> <span data-ttu-id="7a0b5-143">Répétez cette étape trois fois afin de disposer de quatre disques de données pour RAID.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-143">Repeat this step three more times so that you have four data disks for RAID.</span></span>  

<span data-ttu-id="7a0b5-144">Vous pouvez voir hello ajouté les lecteurs dans la machine virtuelle de hello en examinant le journal des messages hello du noyau.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-144">You can see hello added drives in hello virtual machine by looking at hello kernel message log.</span></span> <span data-ttu-id="7a0b5-145">Par exemple, toosee cela sur Ubuntu, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7a0b5-145">For example, toosee this on Ubuntu, use hello following command:</span></span>  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-hello-additional-disks"></a><span data-ttu-id="7a0b5-146">Créer RAID avec hello des disques supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7a0b5-146">Create RAID with hello additional disks</span></span>
<span data-ttu-id="7a0b5-147">Hello étapes suivantes décrivent comment trop[configurer le logiciel RAID sur Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7a0b5-147">hello following steps describe how too[configure software RAID on Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="7a0b5-148">Si vous utilisez un système de fichiers XFS hello, exécutez hello comme suit après avoir créé RAID.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-148">If you are using hello XFS file system, execute hello following steps after you have created RAID.</span></span>
>
>

<span data-ttu-id="7a0b5-149">tooinstall XFS sur Debian et Ubuntu Linux Mint, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7a0b5-149">tooinstall XFS on Debian, Ubuntu, or Linux Mint, use hello following command:</span></span>  

    apt-get -y install xfsprogs  

<span data-ttu-id="7a0b5-150">tooinstall XFS sur Fedora, CentOS ou RHEL, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7a0b5-150">tooinstall XFS on Fedora, CentOS, or RHEL, use hello following command:</span></span>  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a><span data-ttu-id="7a0b5-151">Configuration d’un nouveau chemin d’accès de stockage</span><span class="sxs-lookup"><span data-stu-id="7a0b5-151">Set up a new storage path</span></span>
<span data-ttu-id="7a0b5-152">Utilisez hello suivant tooset de commande d’un nouveau chemin d’accès de stockage :</span><span class="sxs-lookup"><span data-stu-id="7a0b5-152">Use hello following command tooset up a new storage path:</span></span>  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-hello-original-data-toohello-new-storage-path"></a><span data-ttu-id="7a0b5-153">Copie hello d’origine toohello nouveau stockage chemin de données</span><span class="sxs-lookup"><span data-stu-id="7a0b5-153">Copy hello original data toohello new storage path</span></span>
<span data-ttu-id="7a0b5-154">Utilisez hello suivant commande toocopy données toohello nouveau stockage chemin d’accès :</span><span class="sxs-lookup"><span data-stu-id="7a0b5-154">Use hello following command toocopy data toohello new storage path:</span></span>  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-hello-data-disk"></a><span data-ttu-id="7a0b5-155">Modifier les autorisations pour MySQL puisse accéder aux (lecture et écriture) disque de données hello</span><span class="sxs-lookup"><span data-stu-id="7a0b5-155">Modify permissions so MySQL can access (read and write) hello data disk</span></span>
<span data-ttu-id="7a0b5-156">Utilisez hello commande toomodify autorisations suivantes :</span><span class="sxs-lookup"><span data-stu-id="7a0b5-156">Use hello following command toomodify permissions:</span></span>  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-hello-disk-io-scheduling-algorithm"></a><span data-ttu-id="7a0b5-157">Ajuster les e/s de disque hello algorithme de planification</span><span class="sxs-lookup"><span data-stu-id="7a0b5-157">Adjust hello disk I/O scheduling algorithm</span></span>
<span data-ttu-id="7a0b5-158">Linux implémente quatre types d’algorithmes de planification d’E/S :</span><span class="sxs-lookup"><span data-stu-id="7a0b5-158">Linux implements four types of I/O scheduling algorithms:</span></span>  

* <span data-ttu-id="7a0b5-159">Algorithme NOOP (aucune opération)</span><span class="sxs-lookup"><span data-stu-id="7a0b5-159">NOOP algorithm (No Operation)</span></span>
* <span data-ttu-id="7a0b5-160">Algorithme d’échéance (échéance)</span><span class="sxs-lookup"><span data-stu-id="7a0b5-160">Deadline algorithm (Deadline)</span></span>
* <span data-ttu-id="7a0b5-161">Algorithme de file d’attente complètement juste (CFQ)</span><span class="sxs-lookup"><span data-stu-id="7a0b5-161">Completely fair queuing algorithm (CFQ)</span></span>
* <span data-ttu-id="7a0b5-162">Algorithme de période de budget (anticipatif)</span><span class="sxs-lookup"><span data-stu-id="7a0b5-162">Budget period algorithm (Anticipatory)</span></span>  

<span data-ttu-id="7a0b5-163">Vous pouvez sélectionner différents planificateurs d’e/s sous performances toooptimize de différents scénarios.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-163">You can select different I/O schedulers under different scenarios toooptimize performance.</span></span> <span data-ttu-id="7a0b5-164">Dans un environnement d’accès complètement aléatoire, il n'est pas une différence significative entre hello CFQ et les algorithmes d’échéance pour les performances.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-164">In a completely random access environment, there is not a significant difference between hello CFQ and Deadline algorithms for performance.</span></span> <span data-ttu-id="7a0b5-165">Nous vous recommandons de définir tooDeadline d’environnement hello MySQL de base de données pour la stabilité.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-165">We recommend that you set hello MySQL database environment tooDeadline for stability.</span></span> <span data-ttu-id="7a0b5-166">En cas de nombreuses E/S séquentielles, CFQ peut réduire les performances d’E/S de disque.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-166">If there is a lot of sequential I/O, CFQ might reduce disk I/O performance.</span></span>   

<span data-ttu-id="7a0b5-167">Pour les disques SSD et d’autres équipements, NOOP ou échéance permettre obtenir de meilleures performances que le planificateur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-167">For SSD and other equipment, NOOP or Deadline can achieve better performance than hello default scheduler.</span></span>   

<span data-ttu-id="7a0b5-168">Toohello préalable noyau 2.5, e/s de la valeur par défaut hello planification algorithme est échéance.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-168">Prior toohello kernel 2.5, hello default I/O scheduling algorithm is Deadline.</span></span> <span data-ttu-id="7a0b5-169">CFQ à partir du noyau de hello 2.6.18, est devenu l’algorithme de planification d’e/s par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-169">Starting with hello kernel 2.6.18, CFQ became hello default I/O scheduling algorithm.</span></span>  <span data-ttu-id="7a0b5-170">Vous pouvez spécifier ce paramètre au moment du démarrage du noyau ou modifier ce paramètre de manière dynamique lorsque le système de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-170">You can specify this setting at kernel boot time or dynamically modify this setting when hello system is running.</span></span>  

<span data-ttu-id="7a0b5-171">Bonjour à l’exemple suivant montre comment toocheck et ensemble hello algorithme NOOP toohello du planificateur par défaut dans la famille de distribution Debian hello.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-171">hello following example demonstrates how toocheck and set hello default scheduler toohello NOOP algorithm in hello Debian distribution family.</span></span>  

### <a name="view-hello-current-io-scheduler"></a><span data-ttu-id="7a0b5-172">Planificateur de vue hello actuel d’e/s</span><span class="sxs-lookup"><span data-stu-id="7a0b5-172">View hello current I/O scheduler</span></span>
<span data-ttu-id="7a0b5-173">Planificateur de hello tooview exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7a0b5-173">tooview hello scheduler run hello following command:</span></span>  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

<span data-ttu-id="7a0b5-174">Après la sortie, ce qui indique le planificateur actuel de hello s’affiche :</span><span class="sxs-lookup"><span data-stu-id="7a0b5-174">You will see following output, which indicates hello current scheduler:</span></span>  

    noop [deadline] cfq


### <a name="change-hello-current-device-devsda-of-hello-io-scheduling-algorithm"></a><span data-ttu-id="7a0b5-175">Changer de périphérique en cours hello (/ dev/sda) de l’algorithme de planification hello d’e/s</span><span class="sxs-lookup"><span data-stu-id="7a0b5-175">Change hello current device (/dev/sda) of hello I/O scheduling algorithm</span></span>
<span data-ttu-id="7a0b5-176">Exécutez hello suivant de commandes toochange hello appareil :</span><span class="sxs-lookup"><span data-stu-id="7a0b5-176">Run hello following commands toochange hello current device:</span></span>  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> <span data-ttu-id="7a0b5-177">Définir cette propriété pour /dev/sda uniquement n’est pas utile.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-177">Setting this for /dev/sda alone is not useful.</span></span> <span data-ttu-id="7a0b5-178">Elle doit être définie sur tous les disques de données où se trouve la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-178">It must be set on all data disks where hello database resides.</span></span>  
>
>

<span data-ttu-id="7a0b5-179">Vous devez voir hello suivant de sortie, indiquant que grub.cfg a été reconstruite avec succès et que le planificateur par défaut hello a été mis à jour tooNOOP :</span><span class="sxs-lookup"><span data-stu-id="7a0b5-179">You should see hello following output, indicating that grub.cfg has been rebuilt successfully and that hello default scheduler has been updated tooNOOP:</span></span>  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

<span data-ttu-id="7a0b5-180">Pourquoi la famille de distribution Red Hat, vous devez uniquement hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7a0b5-180">For hello Red Hat distribution family, you need only hello following command:</span></span>

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a><span data-ttu-id="7a0b5-181">Configuration des paramètres d’opérations de fichier système</span><span class="sxs-lookup"><span data-stu-id="7a0b5-181">Configure system file operations settings</span></span>
<span data-ttu-id="7a0b5-182">Une meilleure pratique est toodisable hello *atime* fonctionnalité de journalisation sur le système de fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-182">One best practice is toodisable hello *atime* logging feature on hello file system.</span></span> <span data-ttu-id="7a0b5-183">Atime est le dernier temps d’accès fichier hello.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-183">Atime is hello last file access time.</span></span> <span data-ttu-id="7a0b5-184">Chaque fois qu’un fichier est accédé, les enregistrements de système de fichier hello hello horodatage dans le journal de hello.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-184">Whenever a file is accessed, hello file system records hello timestamp in hello log.</span></span> <span data-ttu-id="7a0b5-185">Toutefois, cette information est rarement utilisée.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-185">However, this information is rarely used.</span></span> <span data-ttu-id="7a0b5-186">Vous pouvez la désactiver si vous n’en avez pas besoin, ce qui réduit le temps global d’accès au disque.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-186">You can disable it if you don't need it, which will reduce overall disk access time.</span></span>  

<span data-ttu-id="7a0b5-187">toodisable atime journalisation, vous devez toomodify hello fichier system configuration fichier trouve fstab et ajouter hello **noatime** option.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-187">toodisable atime logging, you need toomodify hello file system configuration file /etc/ fstab and add hello **noatime** option.</span></span>  

<span data-ttu-id="7a0b5-188">Par exemple, modifiez hello vim/etc/fstab fichier en ajoutant hello noatime comme indiqué dans hello suivant l’exemple :</span><span class="sxs-lookup"><span data-stu-id="7a0b5-188">For example, edit hello vim /etc/fstab file, adding hello noatime as shown in hello following sample:</span></span>  

    # CLOUD_IMG: This file was created/modified by hello Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add hello “noatime” option below toodisable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

<span data-ttu-id="7a0b5-189">Ensuite, remontez le système de fichiers hello avec hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7a0b5-189">Then, remount hello file system with hello following command:</span></span>  

    mount -o remount /RAID0

<span data-ttu-id="7a0b5-190">Hello de test modifié le résultat.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-190">Test hello modified result.</span></span> <span data-ttu-id="7a0b5-191">Lorsque vous modifiez le fichier de test hello, temps d’accès hello n’est pas mis à jour.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-191">When you modify hello test file, hello access time is not updated.</span></span> <span data-ttu-id="7a0b5-192">Bonjour suivant illustrent les exemples ressemble le code hello avant et après modification.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-192">hello following examples show what hello code looks like before and after modification.</span></span>

<span data-ttu-id="7a0b5-193">Avant :</span><span class="sxs-lookup"><span data-stu-id="7a0b5-193">Before:</span></span>        

![Code avant la modification de l’accès][5]

<span data-ttu-id="7a0b5-195">Après :</span><span class="sxs-lookup"><span data-stu-id="7a0b5-195">After:</span></span>

![Code après la modification de l’accès][6]

## <a name="increase-hello-maximum-number-of-system-handles-for-high-concurrency"></a><span data-ttu-id="7a0b5-197">Augmenter le nombre maximal de hello de handles du système d’accès concurrentiel élevé</span><span class="sxs-lookup"><span data-stu-id="7a0b5-197">Increase hello maximum number of system handles for high concurrency</span></span>
<span data-ttu-id="7a0b5-198">MySQL est une base de données à forte concurrence.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-198">MySQL is a high concurrency database.</span></span> <span data-ttu-id="7a0b5-199">nombre de handles simultanées par défaut de Hello est 1024 pour Linux, ce qui n’est pas toujours suffisant.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-199">hello default number of concurrent handles is 1024 for Linux, which is not always sufficient.</span></span> <span data-ttu-id="7a0b5-200">Les étapes suivantes de hello utilisation tooincrease hello maximale simultanées poignées de hello système toosupport élevé d’accès concurrentiel de MySQL.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-200">Use hello following steps tooincrease hello maximum concurrent handles of hello system toosupport high concurrency of MySQL.</span></span>

### <a name="modify-hello-limitsconf-file"></a><span data-ttu-id="7a0b5-201">Modifier le fichier de limits.conf hello</span><span class="sxs-lookup"><span data-stu-id="7a0b5-201">Modify hello limits.conf file</span></span>
<span data-ttu-id="7a0b5-202">hello tooincrease maximale autorisée de descripteurs simultanées, ajouter hello quatre lignes dans le fichier de /etc/security/limits.conf hello suivantes.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-202">tooincrease hello maximum allowed concurrent handles, add hello following four lines in hello /etc/security/limits.conf file.</span></span> <span data-ttu-id="7a0b5-203">Notez que 65536 est le nombre maximal de hello système de hello pouvant prendre en charge.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-203">Note that 65536 is hello maximum number that hello system can support.</span></span>   

    * <span data-ttu-id="7a0b5-204">soft nofile 65536</span><span class="sxs-lookup"><span data-stu-id="7a0b5-204">soft nofile 65536</span></span>
    * <span data-ttu-id="7a0b5-205">hard nofile 65536</span><span class="sxs-lookup"><span data-stu-id="7a0b5-205">hard nofile 65536</span></span>
    * <span data-ttu-id="7a0b5-206">soft nproc 65536</span><span class="sxs-lookup"><span data-stu-id="7a0b5-206">soft nproc 65536</span></span>
    * <span data-ttu-id="7a0b5-207">hard nproc 65536</span><span class="sxs-lookup"><span data-stu-id="7a0b5-207">hard nproc 65536</span></span>

### <a name="update-hello-system-for-hello-new-limits"></a><span data-ttu-id="7a0b5-208">Mettre à jour système hello pour les nouvelles limites de hello</span><span class="sxs-lookup"><span data-stu-id="7a0b5-208">Update hello system for hello new limits</span></span>
<span data-ttu-id="7a0b5-209">système de hello tooupdate, exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="7a0b5-209">tooupdate hello system, run hello following commands:</span></span>  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-hello-limits-are-updated-at-boot-time"></a><span data-ttu-id="7a0b5-210">Assurez-vous que les limites de hello sont mis à jour au moment du démarrage</span><span class="sxs-lookup"><span data-stu-id="7a0b5-210">Ensure that hello limits are updated at boot time</span></span>
<span data-ttu-id="7a0b5-211">Placez hello suivant les commandes de démarrage dans le fichier de /etc/rc.local hello afin qu’il prendra effet au moment du démarrage.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-211">Put hello following startup commands in hello /etc/rc.local file so it will take effect at boot time.</span></span>  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a><span data-ttu-id="7a0b5-212">Optimisation de base de données MySQL</span><span class="sxs-lookup"><span data-stu-id="7a0b5-212">MySQL database optimization</span></span>
<span data-ttu-id="7a0b5-213">tooconfigure MySQL sur Azure, vous pouvez utiliser hello même stratégie réglage des performances que vous utilisez sur un ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-213">tooconfigure MySQL on Azure, you can use hello same performance-tuning strategy you use on an on-premises machine.</span></span>  

<span data-ttu-id="7a0b5-214">règles d’optimisation Hello principales d’e/s sont :</span><span class="sxs-lookup"><span data-stu-id="7a0b5-214">hello main I/O optimization rules are:</span></span>   

* <span data-ttu-id="7a0b5-215">Augmenter la taille du cache hello.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-215">Increase hello cache size.</span></span>
* <span data-ttu-id="7a0b5-216">Réduisez le délai de réponse E/S.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-216">Reduce I/O response time.</span></span>  

<span data-ttu-id="7a0b5-217">paramètres du serveur MySQL toooptimize, vous pouvez mettre à jour fichier my.cnf hello, qui est le fichier de configuration par défaut hello pour des ordinateurs clients et serveur.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-217">toooptimize MySQL server settings, you can update hello my.cnf file, which is hello default configuration file for both server and client computers.</span></span>  

<span data-ttu-id="7a0b5-218">Hello des éléments de configuration suivants sont hello principaux facteurs qui affectent les performances de MySQL :</span><span class="sxs-lookup"><span data-stu-id="7a0b5-218">hello following configuration items are hello main factors that affect MySQL performance:</span></span>  

* <span data-ttu-id="7a0b5-219">**innodb_buffer_pool_size**: pool de mémoires tampons hello contient les données mises en mémoire tampon et l’index de hello.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-219">**innodb_buffer_pool_size**: hello buffer pool contains buffered data and hello index.</span></span> <span data-ttu-id="7a0b5-220">Cela a généralement la valeur % too70 de mémoire physique.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-220">This is usually set too70 percent of physical memory.</span></span>
* <span data-ttu-id="7a0b5-221">**innodb_log_file_size**: taille de journal de restauration par progression hello.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-221">**innodb_log_file_size**: This is hello redo log size.</span></span> <span data-ttu-id="7a0b5-222">Vous utilisez tooensure de journaux de restauration par progression que les opérations d’écriture sont récupérables, fiable et rapide après un incident.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-222">You use redo logs tooensure that write operations are fast, reliable, and recoverable after a crash.</span></span> <span data-ttu-id="7a0b5-223">A la valeur too512 Mo, ce qui vous donne suffisamment d’espace disque pour la journalisation des opérations d’écriture.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-223">This is set too512 MB, which will give you plenty of space for logging write operations.</span></span>
* <span data-ttu-id="7a0b5-224">**max_connections** : parfois, les applications ne ferment pas les connexions correctement.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-224">**max_connections**: Sometimes applications do not close connections properly.</span></span> <span data-ttu-id="7a0b5-225">Une valeur supérieure, vous accordez hello serveur toorecycle désactivé des connexions plus de temps.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-225">A larger value will give hello server more time toorecycle idled connections.</span></span> <span data-ttu-id="7a0b5-226">Hello le nombre maximal de connexions est 10 000, mais hello recommandé maximale est de 5 000.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-226">hello maximum number of connections is 10,000, but hello recommended maximum is 5,000.</span></span>
* <span data-ttu-id="7a0b5-227">**Innodb_file_per_table**: ce paramètre Active ou désactive la possibilité de hello des tables de toostore InnoDB dans des fichiers distincts.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-227">**Innodb_file_per_table**: This setting enables or disables hello ability of InnoDB toostore tables in separate files.</span></span> <span data-ttu-id="7a0b5-228">Activez tooensure d’option hello que plusieurs opérations d’administration avancées peuvent être appliquées efficacement.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-228">Turn on hello option tooensure that several advanced administration operations can be applied efficiently.</span></span> <span data-ttu-id="7a0b5-229">À partir d’un point de vue des performances, il peut accélérer la transmission d’espace table hello et optimiser les performances de gestion de débris hello.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-229">From a performance point of view, it can speed up hello table space transmission and optimize hello debris management performance.</span></span> <span data-ttu-id="7a0b5-230">Hello recommandé pour cette option est activé.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-230">hello recommended setting for this option is ON.</span></span></br></br>
<span data-ttu-id="7a0b5-231">À partir de MySQL 5.6, hello par défaut est ON, par conséquent, aucune action n’est requise.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-231">From MySQL 5.6, hello default setting is ON, so no action is required.</span></span> <span data-ttu-id="7a0b5-232">Pour les versions antérieures, hello par défaut est OFF.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-232">For earlier versions, hello default setting is OFF.</span></span> <span data-ttu-id="7a0b5-233">paramètre de Hello doit être modifié avant le chargement de données, car seules les tables nouvellement créés sont affectées.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-233">hello setting should be changed before data is loaded, because only newly created tables are affected.</span></span>
* <span data-ttu-id="7a0b5-234">**innodb_flush_log_at_trx_commit**: valeur par défaut de hello est 1, avec hello étendue too0 ~ 2.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-234">**innodb_flush_log_at_trx_commit**: hello default value is 1, with hello scope set too0~2.</span></span> <span data-ttu-id="7a0b5-235">valeur par défaut de Hello est l’option la plus appropriée pour la base de données MySQL autonome hello.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-235">hello default value is hello most suitable option for standalone MySQL DB.</span></span> <span data-ttu-id="7a0b5-236">Hello de 2 permet hello plus l’intégrité des données et est adapté aux maître dans un MySQL Cluster.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-236">hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL Cluster.</span></span> <span data-ttu-id="7a0b5-237">le paramètre Hello 0 permet de perte de données, ce qui peut affecter la fiabilité, dans certains cas avec de meilleures performances et convient aux subordonné dans un MySQL Cluster.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-237">hello setting of 0 allows data loss, which can affect reliability (in some cases with better performance), and is suitable for Slave in MySQL Cluster.</span></span>
* <span data-ttu-id="7a0b5-238">**Innodb_log_buffer_size**: tampon de journal hello permet des transactions toorun sans avoir tooflush hello journal toodisk avant la validation des transactions hello.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-238">**Innodb_log_buffer_size**: hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit.</span></span> <span data-ttu-id="7a0b5-239">Toutefois, s’il existe des objets binaires volumineux ou un champ de texte, le cache de hello est consommé rapidement et e/s disque fréquentes sera déclenché.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-239">However, if there is large binary object or text field, hello cache will be consumed quickly and frequent disk I/O will be triggered.</span></span> <span data-ttu-id="7a0b5-240">Il est mieux augmenter la taille de mémoire tampon hello si la variable d’état Innodb_log_waits n’est pas 0.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-240">It is better increase hello buffer size if Innodb_log_waits state variable is not 0.</span></span>
* <span data-ttu-id="7a0b5-241">**query_cache_size**: hello meilleure option est toodisable à partir du début de hello.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-241">**query_cache_size**: hello best option is toodisable it from hello outset.</span></span> <span data-ttu-id="7a0b5-242">Too0 query_cache_size (il s’agit de paramètre par défaut de hello dans MySQL 5.6) et utiliser d’autres toospeed méthodes des requêtes.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-242">Set query_cache_size too0 (this is hello default setting in MySQL 5.6) and use other methods toospeed up queries.</span></span>  

<span data-ttu-id="7a0b5-243">Consultez [annexe D](#AppendixD) pour une comparaison des performances avant et après l’optimisation de hello.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-243">See [Appendix D](#AppendixD) for a comparison of performance before and after hello optimization.</span></span>

## <a name="turn-on-hello-mysql-slow-query-log-for-analyzing-hello-performance-bottleneck"></a><span data-ttu-id="7a0b5-244">Activer le journal des requêtes lentes hello MySQL pour l’analyse hello goulot d’étranglement</span><span class="sxs-lookup"><span data-stu-id="7a0b5-244">Turn on hello MySQL slow query log for analyzing hello performance bottleneck</span></span>
<span data-ttu-id="7a0b5-245">journal des requêtes lentes Hello MySQL peut vous aider à identifier les requêtes lentes hello pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-245">hello MySQL slow query log can help you identify hello slow queries for MySQL.</span></span> <span data-ttu-id="7a0b5-246">Après avoir activé le journal des requêtes lentes hello MySQL, vous pouvez utiliser les outils MySQL comme **mysqldumpslow** goulot d’étranglement de performances tooidentify hello.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-246">After enabling hello MySQL slow query log, you can use MySQL tools like **mysqldumpslow** tooidentify hello performance bottleneck.</span></span>  

<span data-ttu-id="7a0b5-247">Par défaut, cette option n’est pas activée.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-247">By default, this is not enabled.</span></span> <span data-ttu-id="7a0b5-248">Journal des requêtes lentes hello sous tension peut consommer des ressources du processeur.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-248">Turning on hello slow query log might consume some CPU resources.</span></span> <span data-ttu-id="7a0b5-249">Nous vous recommandons d’activer ce dernier temporairement, pour résoudre les goulots d’étranglement de performances.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-249">We recommend that you enable this temporarily for troubleshooting performance bottlenecks.</span></span> <span data-ttu-id="7a0b5-250">tooturn sur le journal des requêtes lentes hello :</span><span class="sxs-lookup"><span data-stu-id="7a0b5-250">tooturn on hello slow query log:</span></span>

1. <span data-ttu-id="7a0b5-251">Modifier le fichier my.cnf de hello en ajoutant hello suivant lignes toohello fin :</span><span class="sxs-lookup"><span data-stu-id="7a0b5-251">Modify hello my.cnf file by adding hello following lines toohello end:</span></span>

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. <span data-ttu-id="7a0b5-252">Redémarrez le serveur MySQL de hello.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-252">Restart hello MySQL server.</span></span>

        service  mysql  restart

3. <span data-ttu-id="7a0b5-253">Vérifiez si le paramètre de hello prend effet à l’aide de hello **afficher** commande.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-253">Check whether hello setting is taking effect by using hello **show** command.</span></span>

![Journal des requêtes lentes ON][7]   

![Résultats du journal des requêtes lentes][8]

<span data-ttu-id="7a0b5-256">Dans cet exemple, vous pouvez voir que cette fonctionnalité de requête lentes hello a été activée.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-256">In this example, you can see that hello slow query feature has been turned on.</span></span> <span data-ttu-id="7a0b5-257">Vous pouvez ensuite utiliser hello **mysqldumpslow** outil toodetermine les goulots d’étranglement et optimiser les performances, telles que l’ajout d’index.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-257">You can then use hello **mysqldumpslow** tool toodetermine performance bottlenecks and optimize performance, such as adding indexes.</span></span>

## <a name="appendices"></a><span data-ttu-id="7a0b5-258">Annexes</span><span class="sxs-lookup"><span data-stu-id="7a0b5-258">Appendices</span></span>
<span data-ttu-id="7a0b5-259">Hello Voici des exemples de données test de performances produits dans un environnement lab ciblé.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-259">hello following are sample performance test data produced in a targeted lab environment.</span></span> <span data-ttu-id="7a0b5-260">Ils fournissent des informations générales sur les tendances de données de performances hello avec des performances différentes approches de paramétrage.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-260">They provide general background on hello performance data trend with different performance tuning approaches.</span></span> <span data-ttu-id="7a0b5-261">résultats de Hello peuvent varier sous différentes versions de produit ou d’environnement.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-261">hello results might vary under different environment or product versions.</span></span>

### <span data-ttu-id="7a0b5-262"><a name="AppendixA"></a>Annexe A</span><span class="sxs-lookup"><span data-stu-id="7a0b5-262"><a name="AppendixA"></a>Appendix A</span></span>  
<span data-ttu-id="7a0b5-263">**Performances du disque (IOPS) avec des niveaux RAID différents**</span><span class="sxs-lookup"><span data-stu-id="7a0b5-263">**Disk performance (IOPS) with different RAID levels**</span></span>

![E/S par seconde du disque avec des niveaux RAID différents][9]

<span data-ttu-id="7a0b5-265">**Commandes de test**</span><span class="sxs-lookup"><span data-stu-id="7a0b5-265">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> <span data-ttu-id="7a0b5-266">la charge de travail Hello de ce test utilise 64 threads, la tentative de limite supérieure de hello tooreach de RAID.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-266">hello workload of this test uses 64 threads, trying tooreach hello upper limit of RAID.</span></span>
>
>

### <span data-ttu-id="7a0b5-267"><a name="AppendixB"></a>Annexe B</span><span class="sxs-lookup"><span data-stu-id="7a0b5-267"><a name="AppendixB"></a>Appendix B</span></span>  
<span data-ttu-id="7a0b5-268">**Comparaison des performances (débit) MySQL avec des niveaux RAID différents** </span><span class="sxs-lookup"><span data-stu-id="7a0b5-268">**MySQL performance (throughput) comparison with different RAID levels** </span></span>  
<span data-ttu-id="7a0b5-269">(système de fichiers XFS)</span><span class="sxs-lookup"><span data-stu-id="7a0b5-269">(XFS file system)</span></span>

![Comparaison des performances MySQL avec des niveaux RAID différents][10]  
![Comparaison des performances MySQL avec des niveaux RAID différents][11]

<span data-ttu-id="7a0b5-272">**Commandes de test**</span><span class="sxs-lookup"><span data-stu-id="7a0b5-272">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

<span data-ttu-id="7a0b5-273">**Comparaison des performances (OLTP) MySQL avec des niveaux RAID différents**</span><span class="sxs-lookup"><span data-stu-id="7a0b5-273">**MySQL performance (OLTP) comparison with different RAID levels**</span></span>  
<span data-ttu-id="7a0b5-274">![Comparaison des performances (OLTP) MySQL avec des niveaux RAID différents][12]</span><span class="sxs-lookup"><span data-stu-id="7a0b5-274">![MySQL performance (OLTP) comparison with different RAID levels][12]</span></span>

<span data-ttu-id="7a0b5-275">**Commandes de test**</span><span class="sxs-lookup"><span data-stu-id="7a0b5-275">**Test commands**</span></span>

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <span data-ttu-id="7a0b5-276"><a name="AppendixC"></a>Annexe C</span><span class="sxs-lookup"><span data-stu-id="7a0b5-276"><a name="AppendixC"></a>Appendix C</span></span>   
<span data-ttu-id="7a0b5-277">**Comparaison des performances (IOPS) de disque avec différentes tailles de segment**</span><span class="sxs-lookup"><span data-stu-id="7a0b5-277">**Disk performance (IOPS) comparison for different chunk sizes**</span></span>  
<span data-ttu-id="7a0b5-278">(système de fichiers XFS)</span><span class="sxs-lookup"><span data-stu-id="7a0b5-278">(XFS file system)</span></span>

![][13]

<span data-ttu-id="7a0b5-279">**Commandes de test**</span><span class="sxs-lookup"><span data-stu-id="7a0b5-279">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

<span data-ttu-id="7a0b5-280">tailles des fichiers Hello utilisés pour ce test sont 30 Go et 1 Go, respectivement, avec RAID 0 (4 disques) XFS système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="7a0b5-280">hello file sizes used for this testing are 30 GB and 1 GB, respectively, with RAID 0 (4 disks) XFS file system.</span></span>

### <span data-ttu-id="7a0b5-281"><a name="AppendixD"></a>Annexe D</span><span class="sxs-lookup"><span data-stu-id="7a0b5-281"><a name="AppendixD"></a>Appendix D</span></span>  
<span data-ttu-id="7a0b5-282">**Comparaison des performances (débit) MySQL avant et après l’optimisation**</span><span class="sxs-lookup"><span data-stu-id="7a0b5-282">**MySQL performance (throughput) comparison before and after optimization**</span></span>  
<span data-ttu-id="7a0b5-283">(système de fichiers XFS)</span><span class="sxs-lookup"><span data-stu-id="7a0b5-283">(XFS File System)</span></span>

![Comparaison des performances (débit) MySQL avant et après l’optimisation][14]

<span data-ttu-id="7a0b5-285">**Commandes de test**</span><span class="sxs-lookup"><span data-stu-id="7a0b5-285">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

<span data-ttu-id="7a0b5-286">**Hello de configuration par défaut et l’optimisation est comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7a0b5-286">**hello configuration setting for default and optimization is as follows:**</span></span>

| <span data-ttu-id="7a0b5-287">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7a0b5-287">Parameters</span></span> | <span data-ttu-id="7a0b5-288">Default</span><span class="sxs-lookup"><span data-stu-id="7a0b5-288">Default</span></span> | <span data-ttu-id="7a0b5-289">Optimisation</span><span class="sxs-lookup"><span data-stu-id="7a0b5-289">Optimization</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7a0b5-290">**innodb_buffer_pool_size**</span><span class="sxs-lookup"><span data-stu-id="7a0b5-290">**innodb_buffer_pool_size**</span></span> |<span data-ttu-id="7a0b5-291">Aucune</span><span class="sxs-lookup"><span data-stu-id="7a0b5-291">None</span></span> |<span data-ttu-id="7a0b5-292">7 Go</span><span class="sxs-lookup"><span data-stu-id="7a0b5-292">7 GB</span></span> |
| <span data-ttu-id="7a0b5-293">**innodb_log_file_size**</span><span class="sxs-lookup"><span data-stu-id="7a0b5-293">**innodb_log_file_size**</span></span> |<span data-ttu-id="7a0b5-294">5 Mo</span><span class="sxs-lookup"><span data-stu-id="7a0b5-294">5 MB</span></span> |<span data-ttu-id="7a0b5-295">512 Mo</span><span class="sxs-lookup"><span data-stu-id="7a0b5-295">512 MB</span></span> |
| <span data-ttu-id="7a0b5-296">**max_connections**</span><span class="sxs-lookup"><span data-stu-id="7a0b5-296">**max_connections**</span></span> |<span data-ttu-id="7a0b5-297">100</span><span class="sxs-lookup"><span data-stu-id="7a0b5-297">100</span></span> |<span data-ttu-id="7a0b5-298">5 000</span><span class="sxs-lookup"><span data-stu-id="7a0b5-298">5000</span></span> |
| <span data-ttu-id="7a0b5-299">**innodb_file_per_table**</span><span class="sxs-lookup"><span data-stu-id="7a0b5-299">**innodb_file_per_table**</span></span> |<span data-ttu-id="7a0b5-300">0</span><span class="sxs-lookup"><span data-stu-id="7a0b5-300">0</span></span> |<span data-ttu-id="7a0b5-301">1</span><span class="sxs-lookup"><span data-stu-id="7a0b5-301">1</span></span> |
| <span data-ttu-id="7a0b5-302">**innodb_flush_log_at_trx_commit**</span><span class="sxs-lookup"><span data-stu-id="7a0b5-302">**innodb_flush_log_at_trx_commit**</span></span> |<span data-ttu-id="7a0b5-303">1</span><span class="sxs-lookup"><span data-stu-id="7a0b5-303">1</span></span> |<span data-ttu-id="7a0b5-304">2</span><span class="sxs-lookup"><span data-stu-id="7a0b5-304">2</span></span> |
| <span data-ttu-id="7a0b5-305">**innodb_log_buffer_size**</span><span class="sxs-lookup"><span data-stu-id="7a0b5-305">**innodb_log_buffer_size**</span></span> |<span data-ttu-id="7a0b5-306">8 Mo</span><span class="sxs-lookup"><span data-stu-id="7a0b5-306">8 MB</span></span> |<span data-ttu-id="7a0b5-307">128 Mo</span><span class="sxs-lookup"><span data-stu-id="7a0b5-307">128 MB</span></span> |
| <span data-ttu-id="7a0b5-308">**query_cache_size**</span><span class="sxs-lookup"><span data-stu-id="7a0b5-308">**query_cache_size**</span></span> |<span data-ttu-id="7a0b5-309">16 Mo</span><span class="sxs-lookup"><span data-stu-id="7a0b5-309">16 MB</span></span> |<span data-ttu-id="7a0b5-310">0</span><span class="sxs-lookup"><span data-stu-id="7a0b5-310">0</span></span> |

<span data-ttu-id="7a0b5-311">Pour plus [les paramètres de configuration de l’optimisation](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), consultez toohello [instructions officielles de MySQL](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span><span class="sxs-lookup"><span data-stu-id="7a0b5-311">For more detailed [optimization configuration parameters](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), refer toohello [MySQL official instructions](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span></span>  

  <span data-ttu-id="7a0b5-312">**Environnement de test**</span><span class="sxs-lookup"><span data-stu-id="7a0b5-312">**Test environment**</span></span>  

| <span data-ttu-id="7a0b5-313">Matériel</span><span class="sxs-lookup"><span data-stu-id="7a0b5-313">Hardware</span></span> | <span data-ttu-id="7a0b5-314">Détails</span><span class="sxs-lookup"><span data-stu-id="7a0b5-314">Details</span></span> |
| --- | --- |
| <span data-ttu-id="7a0b5-315">UC</span><span class="sxs-lookup"><span data-stu-id="7a0b5-315">CPU</span></span> |<span data-ttu-id="7a0b5-316">AMD Opteron(tm) Processeur 4171 HE/4 cœurs</span><span class="sxs-lookup"><span data-stu-id="7a0b5-316">AMD Opteron(tm) Processor 4171 HE/4 cores</span></span> |
| <span data-ttu-id="7a0b5-317">Mémoire</span><span class="sxs-lookup"><span data-stu-id="7a0b5-317">Memory</span></span> |<span data-ttu-id="7a0b5-318">14 Go</span><span class="sxs-lookup"><span data-stu-id="7a0b5-318">14 GB</span></span> |
| <span data-ttu-id="7a0b5-319">Disque</span><span class="sxs-lookup"><span data-stu-id="7a0b5-319">Disk</span></span> |<span data-ttu-id="7a0b5-320">10 Go/disque</span><span class="sxs-lookup"><span data-stu-id="7a0b5-320">10 GB/disk</span></span> |
| <span data-ttu-id="7a0b5-321">SE</span><span class="sxs-lookup"><span data-stu-id="7a0b5-321">OS</span></span> |<span data-ttu-id="7a0b5-322">Ubuntu 14.04.1 LTS</span><span class="sxs-lookup"><span data-stu-id="7a0b5-322">Ubuntu 14.04.1 LTS</span></span> |

[1]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-01.png
[2]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-02.png
[3]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-03.png
[4]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-04.png
[5]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-05.png
[6]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-06.png
[7]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-07.png
[8]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-08.png
[9]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-09.png
[10]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-10.png
[11]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-11.png
[12]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-12.png
[13]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-13.png
[14]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-14.png

