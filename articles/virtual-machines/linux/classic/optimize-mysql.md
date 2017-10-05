---
title: "Optimiser les performances de MySQL sur Linux | Microsoft Docs"
description: "Apprenez à optimiser MySQL sur une machine virtuelle Azure exécutant Linux."
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
ms.openlocfilehash: 8f2ec884fa98e989448ac11675e71f39aa21fa7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a><span data-ttu-id="54775-103">Optimiser les performances de MySQL sur les machines virtuelles Linux Azure</span><span class="sxs-lookup"><span data-stu-id="54775-103">Optimize MySQL Performance on Azure Linux VMs</span></span>
<span data-ttu-id="54775-104">De nombreux facteurs, en matière de choix de matériel virtuel et de configuration logicielle, ont une incidence sur les performances de MySQL sur Azure.</span><span class="sxs-lookup"><span data-stu-id="54775-104">There are many factors that affect MySQL performance on Azure, both in virtual hardware selection and software configuration.</span></span> <span data-ttu-id="54775-105">Cet article se concentre sur l’optimisation des performances grâce aux configurations de stockage, système et de base de données.</span><span class="sxs-lookup"><span data-stu-id="54775-105">This article focuses on optimizing performance through storage, system, and database configurations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54775-106">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager](../../../resource-manager-deployment-model.md) et classique.</span><span class="sxs-lookup"><span data-stu-id="54775-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="54775-107">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="54775-107">This article covers using the classic deployment model.</span></span> <span data-ttu-id="54775-108">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="54775-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="54775-109">Pour plus d’informations sur les optimisations de machines virtuelles Linux avec le modèle Resource Manager, consultez [Optimiser votre machine virtuelle Linux sur Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="54775-109">For information about Linux VM optimizations with the Resource Manager model, see [Optimize your Linux VM on Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="utilize-raid-on-an-azure-virtual-machine"></a><span data-ttu-id="54775-110">Utiliser RAID sur une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="54775-110">Utilize RAID on an Azure virtual machine</span></span>
<span data-ttu-id="54775-111">Le stockage est le facteur clé en matière d’incidence sur les performances de base de données dans les environnements de cloud.</span><span class="sxs-lookup"><span data-stu-id="54775-111">Storage is the key factor that affects database performance in cloud environments.</span></span> <span data-ttu-id="54775-112">Grâce à la concurrence, RAID peut fournir un accès plus rapide qu’un seul disque.</span><span class="sxs-lookup"><span data-stu-id="54775-112">Compared to a single disk, RAID can provide faster access via concurrency.</span></span> <span data-ttu-id="54775-113">Pour plus d’informations, consultez [Niveaux RAID standard](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span><span class="sxs-lookup"><span data-stu-id="54775-113">For more information, see [Standard RAID levels](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span></span>   

<span data-ttu-id="54775-114">Le débit d’E/S disque et le temps de réponse d’E/S dans Azure peuvent être améliorés grâce à RAID.</span><span class="sxs-lookup"><span data-stu-id="54775-114">Disk I/O throughput and I/O response time in Azure can be improved through RAID.</span></span> <span data-ttu-id="54775-115">Nos tests de laboratoire montrent que le débit d’E/S disque peut être multiplié par deux et le temps de réponse d’E/S réduit de moitié en moyenne lorsque le nombre de disques RAID est doublé (de deux à quatre, quatre à huit, etc.).</span><span class="sxs-lookup"><span data-stu-id="54775-115">Our lab tests show that disk I/O throughput can be doubled and I/O response time can be reduced by half on average when the number of RAID disks is doubled (from two to four, four to eight, etc.).</span></span> <span data-ttu-id="54775-116">Voir l’ [annexe A](#AppendixA) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="54775-116">See [Appendix A](#AppendixA) for details.</span></span>  

<span data-ttu-id="54775-117">En plus des E/S disque, augmenter le niveau RAID améliore également les performances MySQL.</span><span class="sxs-lookup"><span data-stu-id="54775-117">In addition to disk I/O, MySQL performance improves when you increase the RAID level.</span></span>  <span data-ttu-id="54775-118">Voir l’ [annexe B](#AppendixB) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="54775-118">See [Appendix B](#AppendixB) for details.</span></span>  

<span data-ttu-id="54775-119">Il peut être intéressant de prendre en compte la taille de segment.</span><span class="sxs-lookup"><span data-stu-id="54775-119">You might also want to consider the chunk size.</span></span> <span data-ttu-id="54775-120">En règle générale, lorsque vous disposez d’une plus grande taille de segment, vous obtenez une surcharge inférieure, en particulier pour les écritures de grande taille.</span><span class="sxs-lookup"><span data-stu-id="54775-120">In general, when you have a larger chunk size, you get lower overhead, especially for large writes.</span></span> <span data-ttu-id="54775-121">Toutefois, lorsque la taille de segment est trop élevée, cela peut renforcer la surcharge et vous empêcher de tirer parti de RAID.</span><span class="sxs-lookup"><span data-stu-id="54775-121">However, when the chunk size is too large, it might add additional overhead that prevents you from taking advantage of RAID.</span></span> <span data-ttu-id="54775-122">La taille actuelle de la valeur par défaut est de 512 Ko, ce qui est le plus approprié pour les environnements de production standard.</span><span class="sxs-lookup"><span data-stu-id="54775-122">The current default size is 512 KB, which is proven to be optimal for most general production environments.</span></span> <span data-ttu-id="54775-123">Voir l’ [annexe C](#AppendixC) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="54775-123">See [Appendix C](#AppendixC) for details.</span></span>   

<span data-ttu-id="54775-124">Il existe des limites sur le nombre de disques que vous pouvez ajouter, selon le type de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="54775-124">There are limits on how many disks you can add for different virtual machine types.</span></span> <span data-ttu-id="54775-125">Ces limites sont présentées en détail sur la page [Tailles de machines virtuelles et services cloud pour Microsoft Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="54775-125">These limits are detailed in [Virtual machine and cloud service sizes for Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span> <span data-ttu-id="54775-126">Vous aurez besoin de quatre disques de données attachés pour suivre l’exemple RAID de cet article, même si vous pouvez choisir de configurer RAID avec moins de disques.</span><span class="sxs-lookup"><span data-stu-id="54775-126">You will need four attached data disks to follow the RAID example in this article, although you can choose to set up RAID with fewer disks.</span></span>  

<span data-ttu-id="54775-127">Cet article suppose que vous avez déjà créé une machine virtuelle Linux et que MYSQL est installé et configuré.</span><span class="sxs-lookup"><span data-stu-id="54775-127">This article assumes you have already created a Linux virtual machine and have MYSQL installed and configured.</span></span> <span data-ttu-id="54775-128">Pour plus d’informations sur la prise en main, consultez la page Installation de MySQL sur Azure.</span><span class="sxs-lookup"><span data-stu-id="54775-128">For more information on getting started, see How to install MySQL on Azure.</span></span>  

### <a name="set-up-raid-on-azure"></a><span data-ttu-id="54775-129">Configurer RAID sur Azure</span><span class="sxs-lookup"><span data-stu-id="54775-129">Set up RAID on Azure</span></span>
<span data-ttu-id="54775-130">Les étapes suivantes montrent comment créer RAID dans Azure à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="54775-130">The following steps show how to create RAID on Azure by using the Azure portal.</span></span> <span data-ttu-id="54775-131">Vous pouvez également configurer RAID à l’aide de scripts Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54775-131">You can also set up RAID by using Windows PowerShell scripts.</span></span>
<span data-ttu-id="54775-132">Dans cet exemple, nous allons configurer RAID 0 avec quatre disques.</span><span class="sxs-lookup"><span data-stu-id="54775-132">In this example, we will configure RAID 0 with four disks.</span></span>  

#### <a name="add-a-data-disk-to-your-virtual-machine"></a><span data-ttu-id="54775-133">Ajouter un disque de données à votre machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="54775-133">Add a data disk to your virtual machine</span></span>
<span data-ttu-id="54775-134">Dans le portail Azure, accédez au tableau de bord et sélectionnez la machine virtuelle à laquelle vous souhaitez ajouter un disque de données.</span><span class="sxs-lookup"><span data-stu-id="54775-134">In the Azure portal, go to the dashboard and select the virtual machine to which you want to add a data disk.</span></span> <span data-ttu-id="54775-135">Dans cet exemple, la machine virtuelle est mysqlnode1.</span><span class="sxs-lookup"><span data-stu-id="54775-135">In this example, the virtual machine is mysqlnode1.</span></span>  

<!--![Virtual machines][1]-->

<span data-ttu-id="54775-136">Cliquez sur **Disques**, puis cliquez sur **Attach New** (Attacher nouveau).</span><span class="sxs-lookup"><span data-stu-id="54775-136">Click **Disks** and then click **Attach New**.</span></span>

![Les machines virtuelles ajoutent des disques.](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

<span data-ttu-id="54775-138">Créez un nouveau disque de 500 Go.</span><span class="sxs-lookup"><span data-stu-id="54775-138">Create a new 500 GB disk.</span></span> <span data-ttu-id="54775-139">Assurez-vous que **Host Cache Preference** (Préférence de cache hôte) a la valeur **Aucun**.</span><span class="sxs-lookup"><span data-stu-id="54775-139">Make sure that **Host Cache Preference** is set to **None**.</span></span>  <span data-ttu-id="54775-140">Lorsque vous avez terminé, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="54775-140">When you're finished, click **OK**.</span></span>

![Attacher un disque vide](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


<span data-ttu-id="54775-142">Cela ajoute un disque vide à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="54775-142">This adds one empty disk into your virtual machine.</span></span> <span data-ttu-id="54775-143">Répétez cette étape trois fois afin de disposer de quatre disques de données pour RAID.</span><span class="sxs-lookup"><span data-stu-id="54775-143">Repeat this step three more times so that you have four data disks for RAID.</span></span>  

<span data-ttu-id="54775-144">Vous pouvez voir les disques ajoutés à la machine virtuelle en examinant le journal des messages du noyau.</span><span class="sxs-lookup"><span data-stu-id="54775-144">You can see the added drives in the virtual machine by looking at the kernel message log.</span></span> <span data-ttu-id="54775-145">Par exemple, pour voir cela avec Ubuntu, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="54775-145">For example, to see this on Ubuntu, use the following command:</span></span>  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-the-additional-disks"></a><span data-ttu-id="54775-146">Création de RAID avec les disques supplémentaires</span><span class="sxs-lookup"><span data-stu-id="54775-146">Create RAID with the additional disks</span></span>
<span data-ttu-id="54775-147">Les étapes suivantes décrivent la [configuration logicielle de RAID sur Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="54775-147">The following steps describe how to [configure software RAID on Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="54775-148">Si vous utilisez le système de fichiers XFS, exécutez les étapes ci-dessous après avoir créé le RAID.</span><span class="sxs-lookup"><span data-stu-id="54775-148">If you are using the XFS file system, execute the following steps after you have created RAID.</span></span>
>
>

<span data-ttu-id="54775-149">Pour installer XFS sur Debian, Ubuntu ou Linux Mint, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="54775-149">To install XFS on Debian, Ubuntu, or Linux Mint, use the following command:</span></span>  

    apt-get -y install xfsprogs  

<span data-ttu-id="54775-150">Pour installer XFS sur Fedora, CentOS ou RHEL, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="54775-150">To install XFS on Fedora, CentOS, or RHEL, use the following command:</span></span>  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a><span data-ttu-id="54775-151">Configuration d’un nouveau chemin d’accès de stockage</span><span class="sxs-lookup"><span data-stu-id="54775-151">Set up a new storage path</span></span>
<span data-ttu-id="54775-152">Utilisez la commande suivante pour configurer un nouveau chemin d’accès de stockage :</span><span class="sxs-lookup"><span data-stu-id="54775-152">Use the following command to set up a new storage path:</span></span>  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-the-original-data-to-the-new-storage-path"></a><span data-ttu-id="54775-153">Copie des données d’origine vers le nouveau chemin d’accès de stockage</span><span class="sxs-lookup"><span data-stu-id="54775-153">Copy the original data to the new storage path</span></span>
<span data-ttu-id="54775-154">Utilisez la commande suivante pour copier des données dans le nouveau chemin d’accès de stockage :</span><span class="sxs-lookup"><span data-stu-id="54775-154">Use the following command to copy data to the new storage path:</span></span>  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-the-data-disk"></a><span data-ttu-id="54775-155">Modification des autorisations pour que MySQL puisse accéder (en lecture et écriture) au disque de données</span><span class="sxs-lookup"><span data-stu-id="54775-155">Modify permissions so MySQL can access (read and write) the data disk</span></span>
<span data-ttu-id="54775-156">Utilisez la commande suivante pour modifier les autorisations :</span><span class="sxs-lookup"><span data-stu-id="54775-156">Use the following command to modify permissions:</span></span>  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-the-disk-io-scheduling-algorithm"></a><span data-ttu-id="54775-157">Ajustement de l’algorithme de planification d’E/S disque</span><span class="sxs-lookup"><span data-stu-id="54775-157">Adjust the disk I/O scheduling algorithm</span></span>
<span data-ttu-id="54775-158">Linux implémente quatre types d’algorithmes de planification d’E/S :</span><span class="sxs-lookup"><span data-stu-id="54775-158">Linux implements four types of I/O scheduling algorithms:</span></span>  

* <span data-ttu-id="54775-159">Algorithme NOOP (aucune opération)</span><span class="sxs-lookup"><span data-stu-id="54775-159">NOOP algorithm (No Operation)</span></span>
* <span data-ttu-id="54775-160">Algorithme d’échéance (échéance)</span><span class="sxs-lookup"><span data-stu-id="54775-160">Deadline algorithm (Deadline)</span></span>
* <span data-ttu-id="54775-161">Algorithme de file d’attente complètement juste (CFQ)</span><span class="sxs-lookup"><span data-stu-id="54775-161">Completely fair queuing algorithm (CFQ)</span></span>
* <span data-ttu-id="54775-162">Algorithme de période de budget (anticipatif)</span><span class="sxs-lookup"><span data-stu-id="54775-162">Budget period algorithm (Anticipatory)</span></span>  

<span data-ttu-id="54775-163">Vous pouvez sélectionner différents planificateurs d’E/S sous différents scénarios pour optimiser les performances.</span><span class="sxs-lookup"><span data-stu-id="54775-163">You can select different I/O schedulers under different scenarios to optimize performance.</span></span> <span data-ttu-id="54775-164">Dans un environnement à accès complètement aléatoire, il n’existe pas de grande différence entre les algorithmes CFQ et d’échéance du point de vue des performances.</span><span class="sxs-lookup"><span data-stu-id="54775-164">In a completely random access environment, there is not a significant difference between the CFQ and Deadline algorithms for performance.</span></span> <span data-ttu-id="54775-165">Nous vous recommandons de définir l’environnement de base de données MySQL sur échéance pour la stabilité.</span><span class="sxs-lookup"><span data-stu-id="54775-165">We recommend that you set the MySQL database environment to Deadline for stability.</span></span> <span data-ttu-id="54775-166">En cas de nombreuses E/S séquentielles, CFQ peut réduire les performances d’E/S de disque.</span><span class="sxs-lookup"><span data-stu-id="54775-166">If there is a lot of sequential I/O, CFQ might reduce disk I/O performance.</span></span>   

<span data-ttu-id="54775-167">Pour les disques SSD et autres équipements, NOOP ou échéance peuvent fournir de meilleures performances que le planificateur par défaut.</span><span class="sxs-lookup"><span data-stu-id="54775-167">For SSD and other equipment, NOOP or Deadline can achieve better performance than the default scheduler.</span></span>   

<span data-ttu-id="54775-168">Avant le noyau 2.5, l’algorithme de planification d’E/S par défaut est échéance.</span><span class="sxs-lookup"><span data-stu-id="54775-168">Prior to the kernel 2.5, the default I/O scheduling algorithm is Deadline.</span></span> <span data-ttu-id="54775-169">À partir du noyau 2.6.18, CFQ est devenu l’algorithme de planification d’E/S par défaut.</span><span class="sxs-lookup"><span data-stu-id="54775-169">Starting with the kernel 2.6.18, CFQ became the default I/O scheduling algorithm.</span></span>  <span data-ttu-id="54775-170">Vous pouvez spécifier ce paramètre au moment du démarrage du noyau ou le modifier dynamiquement lorsque le système est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="54775-170">You can specify this setting at kernel boot time or dynamically modify this setting when the system is running.</span></span>  

<span data-ttu-id="54775-171">L’exemple suivant montre comment vérifier et définir le planificateur par défaut sur l’algorithme NOOP dans la famille de distribution Debian.</span><span class="sxs-lookup"><span data-stu-id="54775-171">The following example demonstrates how to check and set the default scheduler to the NOOP algorithm in the Debian distribution family.</span></span>  

### <a name="view-the-current-io-scheduler"></a><span data-ttu-id="54775-172">Visualiser le planificateur d’E/S actuel</span><span class="sxs-lookup"><span data-stu-id="54775-172">View the current I/O scheduler</span></span>
<span data-ttu-id="54775-173">Pour afficher le planificateur, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="54775-173">To view the scheduler run the following command:</span></span>  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

<span data-ttu-id="54775-174">Vous verrez la sortie suivante, indiquant le planificateur actuel :</span><span class="sxs-lookup"><span data-stu-id="54775-174">You will see following output, which indicates the current scheduler:</span></span>  

    noop [deadline] cfq


### <a name="change-the-current-device-devsda-of-the-io-scheduling-algorithm"></a><span data-ttu-id="54775-175">Changer le dispositif actuel (/dev/sda) de l’algorithme de planification d’E/S</span><span class="sxs-lookup"><span data-stu-id="54775-175">Change the current device (/dev/sda) of the I/O scheduling algorithm</span></span>
<span data-ttu-id="54775-176">Exécutez les commandes suivantes pour modifier le dispositif actuel :</span><span class="sxs-lookup"><span data-stu-id="54775-176">Run the following commands to change the current device:</span></span>  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> <span data-ttu-id="54775-177">Définir cette propriété pour /dev/sda uniquement n’est pas utile.</span><span class="sxs-lookup"><span data-stu-id="54775-177">Setting this for /dev/sda alone is not useful.</span></span> <span data-ttu-id="54775-178">Elle doit être définie sur tous les disques de données où réside la base de données.</span><span class="sxs-lookup"><span data-stu-id="54775-178">It must be set on all data disks where the database resides.</span></span>  
>
>

<span data-ttu-id="54775-179">Vous devriez voir la sortie suivante, qui indique que grub.cfg a été régénéré avec succès et que le planificateur par défaut a été mis à jour vers NOOP :</span><span class="sxs-lookup"><span data-stu-id="54775-179">You should see the following output, indicating that grub.cfg has been rebuilt successfully and that the default scheduler has been updated to NOOP:</span></span>  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

<span data-ttu-id="54775-180">Pour la famille de distribution Red Hat, la commande suivante suffit :</span><span class="sxs-lookup"><span data-stu-id="54775-180">For the Red Hat distribution family, you need only the following command:</span></span>

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a><span data-ttu-id="54775-181">Configuration des paramètres d’opérations de fichier système</span><span class="sxs-lookup"><span data-stu-id="54775-181">Configure system file operations settings</span></span>
<span data-ttu-id="54775-182">Une meilleure pratique consiste à désactiver la fonctionnalité de journalisation *atime* sur le système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="54775-182">One best practice is to disable the *atime* logging feature on the file system.</span></span> <span data-ttu-id="54775-183">Atime est le dernier temps d’accès au fichier.</span><span class="sxs-lookup"><span data-stu-id="54775-183">Atime is the last file access time.</span></span> <span data-ttu-id="54775-184">Chaque fois qu’un fichier est accessible, le système de fichiers enregistre l’horodatage dans le journal.</span><span class="sxs-lookup"><span data-stu-id="54775-184">Whenever a file is accessed, the file system records the timestamp in the log.</span></span> <span data-ttu-id="54775-185">Toutefois, cette information est rarement utilisée.</span><span class="sxs-lookup"><span data-stu-id="54775-185">However, this information is rarely used.</span></span> <span data-ttu-id="54775-186">Vous pouvez la désactiver si vous n’en avez pas besoin, ce qui réduit le temps global d’accès au disque.</span><span class="sxs-lookup"><span data-stu-id="54775-186">You can disable it if you don't need it, which will reduce overall disk access time.</span></span>  

<span data-ttu-id="54775-187">Pour désactiver la journalisation atime, vous devez modifier le fichier de configuration système /etc/ fstab et ajouter l’option **noatime** .</span><span class="sxs-lookup"><span data-stu-id="54775-187">To disable atime logging, you need to modify the file system configuration file /etc/ fstab and add the **noatime** option.</span></span>  

<span data-ttu-id="54775-188">Par exemple, modifiez le fichier vim /etc/fstab, en ajoutant noatime comme indiqué dans l’exemple ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="54775-188">For example, edit the vim /etc/fstab file, adding the noatime as shown in the following sample:</span></span>  

    # CLOUD_IMG: This file was created/modified by the Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add the “noatime” option below to disable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

<span data-ttu-id="54775-189">Puis, remontez le système de fichiers avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="54775-189">Then, remount the file system with the following command:</span></span>  

    mount -o remount /RAID0

<span data-ttu-id="54775-190">Testez le résultat modifié.</span><span class="sxs-lookup"><span data-stu-id="54775-190">Test the modified result.</span></span> <span data-ttu-id="54775-191">Lorsque vous modifiez le fichier de test, le temps d’accès n’est pas actualisé.</span><span class="sxs-lookup"><span data-stu-id="54775-191">When you modify the test file, the access time is not updated.</span></span> <span data-ttu-id="54775-192">Les exemples suivants montrent à quoi ressemble le code avant et après la modification.</span><span class="sxs-lookup"><span data-stu-id="54775-192">The following examples show what the code looks like before and after modification.</span></span>

<span data-ttu-id="54775-193">Avant :</span><span class="sxs-lookup"><span data-stu-id="54775-193">Before:</span></span>        

![Code avant la modification de l’accès][5]

<span data-ttu-id="54775-195">Après :</span><span class="sxs-lookup"><span data-stu-id="54775-195">After:</span></span>

![Code après la modification de l’accès][6]

## <a name="increase-the-maximum-number-of-system-handles-for-high-concurrency"></a><span data-ttu-id="54775-197">Augmentation du nombre maximal de handles du système pour la concurrence élevée</span><span class="sxs-lookup"><span data-stu-id="54775-197">Increase the maximum number of system handles for high concurrency</span></span>
<span data-ttu-id="54775-198">MySQL est une base de données à forte concurrence.</span><span class="sxs-lookup"><span data-stu-id="54775-198">MySQL is a high concurrency database.</span></span> <span data-ttu-id="54775-199">Le nombre de handles concurrents est de 1024 pour Linux, ce qui n’est pas toujours suffisant.</span><span class="sxs-lookup"><span data-stu-id="54775-199">The default number of concurrent handles is 1024 for Linux, which is not always sufficient.</span></span> <span data-ttu-id="54775-200">Utilisez les étapes suivantes pour augmenter les handles simultanés maximaux du système pour prendre en charge la haute concurrence de MySQL.</span><span class="sxs-lookup"><span data-stu-id="54775-200">Use the following steps to increase the maximum concurrent handles of the system to support high concurrency of MySQL.</span></span>

### <a name="modify-the-limitsconf-file"></a><span data-ttu-id="54775-201">Modification du fichier limits.conf</span><span class="sxs-lookup"><span data-stu-id="54775-201">Modify the limits.conf file</span></span>
<span data-ttu-id="54775-202">Ajoutez les quatre lignes suivantes dans le fichier /etc/security/limits.conf pour augmenter le nombre maximal de handles simultanés autorisés.</span><span class="sxs-lookup"><span data-stu-id="54775-202">To increase the maximum allowed concurrent handles, add the following four lines in the /etc/security/limits.conf file.</span></span> <span data-ttu-id="54775-203">Notez que 65536 est le nombre maximal que le système peut prendre en charge.</span><span class="sxs-lookup"><span data-stu-id="54775-203">Note that 65536 is the maximum number that the system can support.</span></span>   

    * <span data-ttu-id="54775-204">soft nofile 65536</span><span class="sxs-lookup"><span data-stu-id="54775-204">soft nofile 65536</span></span>
    * <span data-ttu-id="54775-205">hard nofile 65536</span><span class="sxs-lookup"><span data-stu-id="54775-205">hard nofile 65536</span></span>
    * <span data-ttu-id="54775-206">soft nproc 65536</span><span class="sxs-lookup"><span data-stu-id="54775-206">soft nproc 65536</span></span>
    * <span data-ttu-id="54775-207">hard nproc 65536</span><span class="sxs-lookup"><span data-stu-id="54775-207">hard nproc 65536</span></span>

### <a name="update-the-system-for-the-new-limits"></a><span data-ttu-id="54775-208">Mise à jour du système pour les nouvelles limites</span><span class="sxs-lookup"><span data-stu-id="54775-208">Update the system for the new limits</span></span>
<span data-ttu-id="54775-209">Pour mettre à jour le système, exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="54775-209">To update the system, run the following commands:</span></span>  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-the-limits-are-updated-at-boot-time"></a><span data-ttu-id="54775-210">Assurez-vous que les limites sont mises à jour au moment du démarrage</span><span class="sxs-lookup"><span data-stu-id="54775-210">Ensure that the limits are updated at boot time</span></span>
<span data-ttu-id="54775-211">Placez les commandes de démarrage suivantes dans le fichier /etc/rc.local afin qu’elles prennent effet lors du démarrage.</span><span class="sxs-lookup"><span data-stu-id="54775-211">Put the following startup commands in the /etc/rc.local file so it will take effect at boot time.</span></span>  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a><span data-ttu-id="54775-212">Optimisation de base de données MySQL</span><span class="sxs-lookup"><span data-stu-id="54775-212">MySQL database optimization</span></span>
<span data-ttu-id="54775-213">Vous pouvez utiliser la même stratégie de réglage de performances pour configurer MySQL sur Azure que sur un ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="54775-213">To configure MySQL on Azure, you can use the same performance-tuning strategy you use on an on-premises machine.</span></span>  

<span data-ttu-id="54775-214">Les règles d’optimisation d’E/S principales sont :</span><span class="sxs-lookup"><span data-stu-id="54775-214">The main I/O optimization rules are:</span></span>   

* <span data-ttu-id="54775-215">Augmentez la taille du cache.</span><span class="sxs-lookup"><span data-stu-id="54775-215">Increase the cache size.</span></span>
* <span data-ttu-id="54775-216">Réduisez le délai de réponse E/S.</span><span class="sxs-lookup"><span data-stu-id="54775-216">Reduce I/O response time.</span></span>  

<span data-ttu-id="54775-217">Pour optimiser les paramètres du serveur MySQL, vous pouvez mettre à jour le fichier my.cnf, qui est le fichier de configuration par défaut du serveur et des ordinateurs clients.</span><span class="sxs-lookup"><span data-stu-id="54775-217">To optimize MySQL server settings, you can update the my.cnf file, which is the default configuration file for both server and client computers.</span></span>  

<span data-ttu-id="54775-218">Les éléments de configuration suivants sont les principaux facteurs qui ont une incidence sur les performances de MySQL :</span><span class="sxs-lookup"><span data-stu-id="54775-218">The following configuration items are the main factors that affect MySQL performance:</span></span>  

* <span data-ttu-id="54775-219">**innodb_buffer_pool_size** : le pool de mémoires tampons contient les données mises en mémoire tampon et l’index.</span><span class="sxs-lookup"><span data-stu-id="54775-219">**innodb_buffer_pool_size**: The buffer pool contains buffered data and the index.</span></span> <span data-ttu-id="54775-220">Il est généralement défini sur 70 % de la mémoire physique.</span><span class="sxs-lookup"><span data-stu-id="54775-220">This is usually set to 70 percent of physical memory.</span></span>
* <span data-ttu-id="54775-221">**innodb_log_file_size** : il s’agit de la taille du journal de rétablissement.</span><span class="sxs-lookup"><span data-stu-id="54775-221">**innodb_log_file_size**: This is the redo log size.</span></span> <span data-ttu-id="54775-222">Vous utilisez des journaux de rétablissement pour vous assurer que les opérations d’écriture sont rapides, fiables et récupérables après une panne.</span><span class="sxs-lookup"><span data-stu-id="54775-222">You use redo logs to ensure that write operations are fast, reliable, and recoverable after a crash.</span></span> <span data-ttu-id="54775-223">Il est défini sur 512 Mo, afin de vous donner suffisamment d’espace disque pour la journalisation des opérations d’écriture.</span><span class="sxs-lookup"><span data-stu-id="54775-223">This is set to 512 MB, which will give you plenty of space for logging write operations.</span></span>
* <span data-ttu-id="54775-224">**max_connections** : parfois, les applications ne ferment pas les connexions correctement.</span><span class="sxs-lookup"><span data-stu-id="54775-224">**max_connections**: Sometimes applications do not close connections properly.</span></span> <span data-ttu-id="54775-225">Une valeur supérieure accordera au serveur davantage de temps pour recycler les connexions inactives.</span><span class="sxs-lookup"><span data-stu-id="54775-225">A larger value will give the server more time to recycle idled connections.</span></span> <span data-ttu-id="54775-226">Le nombre maximal de connexions est de 10 000, mais le maximum recommandé est de 5 000.</span><span class="sxs-lookup"><span data-stu-id="54775-226">The maximum number of connections is 10,000, but the recommended maximum is 5,000.</span></span>
* <span data-ttu-id="54775-227">**Innodb_file_per_table** : ce paramètre active ou désactive la capacité de InnoDB de stocker des tables dans des fichiers distincts.</span><span class="sxs-lookup"><span data-stu-id="54775-227">**Innodb_file_per_table**: This setting enables or disables the ability of InnoDB to store tables in separate files.</span></span> <span data-ttu-id="54775-228">Activer l’option garantit que plusieurs opérations d’administration avancées peuvent être appliquées efficacement.</span><span class="sxs-lookup"><span data-stu-id="54775-228">Turn on the option to ensure that several advanced administration operations can be applied efficiently.</span></span> <span data-ttu-id="54775-229">Du point de vue des performances, elle peut accélérer la transmission d’espace de table et optimiser les performances de gestion de débris.</span><span class="sxs-lookup"><span data-stu-id="54775-229">From a performance point of view, it can speed up the table space transmission and optimize the debris management performance.</span></span> <span data-ttu-id="54775-230">Le paramètre recommandé pour cette option est ON.</span><span class="sxs-lookup"><span data-stu-id="54775-230">The recommended setting for this option is ON.</span></span></br></br>
<span data-ttu-id="54775-231">À partir de MySQL 5.6, le paramètre par défaut est ON, donc aucune action n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="54775-231">From MySQL 5.6, the default setting is ON, so no action is required.</span></span> <span data-ttu-id="54775-232">Pour les versions antérieures, le paramètre par défaut est OFF.</span><span class="sxs-lookup"><span data-stu-id="54775-232">For earlier versions, the default setting is OFF.</span></span> <span data-ttu-id="54775-233">Le paramètre doit être modifié avant le chargement des données, étant donné que seules les tables nouvellement créées sont affectées.</span><span class="sxs-lookup"><span data-stu-id="54775-233">The setting should be changed before data is loaded, because only newly created tables are affected.</span></span>
* <span data-ttu-id="54775-234">**innodb_flush_log_at_trx_commit** : la valeur par défaut est 1 et l’étendue 0~2.</span><span class="sxs-lookup"><span data-stu-id="54775-234">**innodb_flush_log_at_trx_commit**: The default value is 1, with the scope set to 0~2.</span></span> <span data-ttu-id="54775-235">La valeur par défaut est l’option la plus adaptée pour une base de données MySQL autonome.</span><span class="sxs-lookup"><span data-stu-id="54775-235">The default value is the most suitable option for standalone MySQL DB.</span></span> <span data-ttu-id="54775-236">Choisir 2 offre la meilleure intégrité des données et convient à Master dans le cluster MySQL.</span><span class="sxs-lookup"><span data-stu-id="54775-236">The setting of 2 enables the most data integrity and is suitable for Master in MySQL Cluster.</span></span> <span data-ttu-id="54775-237">Choisir 0 autorise la perte de données, ce qui peut avoir une incidence sur la fiabilité (dans certains cas avec de meilleures performances) et convient à Slave dans le cluster MySQL.</span><span class="sxs-lookup"><span data-stu-id="54775-237">The setting of 0 allows data loss, which can affect reliability (in some cases with better performance), and is suitable for Slave in MySQL Cluster.</span></span>
* <span data-ttu-id="54775-238">**Innodb_log_buffer_size** : le tampon journal autorise les transactions à s’exécuter, sans avoir à vider le journal sur le disque avant la validation des transactions.</span><span class="sxs-lookup"><span data-stu-id="54775-238">**Innodb_log_buffer_size**: The log buffer allows transactions to run without having to flush the log to disk before the transactions commit.</span></span> <span data-ttu-id="54775-239">Toutefois, s’il existe des objets binaires ou un champ de texte volumineux, le cache est consommé rapidement et des E/S disque fréquentes seront déclenchées.</span><span class="sxs-lookup"><span data-stu-id="54775-239">However, if there is large binary object or text field, the cache will be consumed quickly and frequent disk I/O will be triggered.</span></span> <span data-ttu-id="54775-240">Il est préférable d’augmenter la taille de la mémoire tampon si la variable d’état Innodb_log_waits n’est pas 0.</span><span class="sxs-lookup"><span data-stu-id="54775-240">It is better increase the buffer size if Innodb_log_waits state variable is not 0.</span></span>
* <span data-ttu-id="54775-241">**query_cache_size** : le meilleur choix consiste à la désactiver dès le départ.</span><span class="sxs-lookup"><span data-stu-id="54775-241">**query_cache_size**: The best option is to disable it from the outset.</span></span> <span data-ttu-id="54775-242">Définissez query_cache_size sur 0 (ce qui est le paramètre par défaut dans MySQL 5.6) et utilisez d’autres méthodes pour accélérer les requêtes.</span><span class="sxs-lookup"><span data-stu-id="54775-242">Set query_cache_size to 0 (this is the default setting in MySQL 5.6) and use other methods to speed up queries.</span></span>  

<span data-ttu-id="54775-243">Consultez [l’Annexe D](#AppendixD) pour obtenir une comparaison des performances avant et après l’optimisation.</span><span class="sxs-lookup"><span data-stu-id="54775-243">See [Appendix D](#AppendixD) for a comparison of performance before and after the optimization.</span></span>

## <a name="turn-on-the-mysql-slow-query-log-for-analyzing-the-performance-bottleneck"></a><span data-ttu-id="54775-244">Activation du journal des requêtes lentes MySQL pour analyser le goulot d’étranglement de performances</span><span class="sxs-lookup"><span data-stu-id="54775-244">Turn on the MySQL slow query log for analyzing the performance bottleneck</span></span>
<span data-ttu-id="54775-245">Le journal des requêtes lentes MySQL peut vous aider à identifier les requêtes lentes pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="54775-245">The MySQL slow query log can help you identify the slow queries for MySQL.</span></span> <span data-ttu-id="54775-246">Après avoir activé le journal des requêtes lentes MySQL, vous pouvez utiliser les outils MySQL comme **mysqldumpslow** pour identifier le goulot d’étranglement de performances.</span><span class="sxs-lookup"><span data-stu-id="54775-246">After enabling the MySQL slow query log, you can use MySQL tools like **mysqldumpslow** to identify the performance bottleneck.</span></span>  

<span data-ttu-id="54775-247">Par défaut, cette option n’est pas activée.</span><span class="sxs-lookup"><span data-stu-id="54775-247">By default, this is not enabled.</span></span> <span data-ttu-id="54775-248">Activer le journal des requêtes lentes peut consommer des ressources du processeur.</span><span class="sxs-lookup"><span data-stu-id="54775-248">Turning on the slow query log might consume some CPU resources.</span></span> <span data-ttu-id="54775-249">Nous vous recommandons d’activer ce dernier temporairement, pour résoudre les goulots d’étranglement de performances.</span><span class="sxs-lookup"><span data-stu-id="54775-249">We recommend that you enable this temporarily for troubleshooting performance bottlenecks.</span></span> <span data-ttu-id="54775-250">Pour activer le journal des requêtes lentes :</span><span class="sxs-lookup"><span data-stu-id="54775-250">To turn on the slow query log:</span></span>

1. <span data-ttu-id="54775-251">Modifiez le fichier my.cnf en ajoutant les lignes suivantes à la fin :</span><span class="sxs-lookup"><span data-stu-id="54775-251">Modify the my.cnf file by adding the following lines to the end:</span></span>

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. <span data-ttu-id="54775-252">Redémarrez le serveur MySQL.</span><span class="sxs-lookup"><span data-stu-id="54775-252">Restart the MySQL server.</span></span>

        service  mysql  restart

3. <span data-ttu-id="54775-253">Vérifiez si le paramètre prend effet à l’aide de la commande **show**.</span><span class="sxs-lookup"><span data-stu-id="54775-253">Check whether the setting is taking effect by using the **show** command.</span></span>

![Journal des requêtes lentes ON][7]   

![Résultats du journal des requêtes lentes][8]

<span data-ttu-id="54775-256">Dans cet exemple, vous pouvez voir que la fonctionnalité de requête lente a été activée.</span><span class="sxs-lookup"><span data-stu-id="54775-256">In this example, you can see that the slow query feature has been turned on.</span></span> <span data-ttu-id="54775-257">Vous pouvez ensuite utiliser l’outil **mysqldumpslow** pour déterminer les goulots d’étranglement et optimiser les performances, comme l’ajout d’index.</span><span class="sxs-lookup"><span data-stu-id="54775-257">You can then use the **mysqldumpslow** tool to determine performance bottlenecks and optimize performance, such as adding indexes.</span></span>

## <a name="appendices"></a><span data-ttu-id="54775-258">Annexes</span><span class="sxs-lookup"><span data-stu-id="54775-258">Appendices</span></span>
<span data-ttu-id="54775-259">Vous trouverez ci-dessous des exemples de données de test de performances obtenues sur un environnement lab ciblé.</span><span class="sxs-lookup"><span data-stu-id="54775-259">The following are sample performance test data produced in a targeted lab environment.</span></span> <span data-ttu-id="54775-260">Ils fournissent des informations générales sur la tendance des données de performances, avec différentes approches de réglage des performances.</span><span class="sxs-lookup"><span data-stu-id="54775-260">They provide general background on the performance data trend with different performance tuning approaches.</span></span> <span data-ttu-id="54775-261">Les résultats peuvent varier selon les versions de produit ou l’environnement.</span><span class="sxs-lookup"><span data-stu-id="54775-261">The results might vary under different environment or product versions.</span></span>

### <span data-ttu-id="54775-262"><a name="AppendixA"></a>Annexe A</span><span class="sxs-lookup"><span data-stu-id="54775-262"><a name="AppendixA"></a>Appendix A</span></span>  
<span data-ttu-id="54775-263">**Performances du disque (IOPS) avec des niveaux RAID différents**</span><span class="sxs-lookup"><span data-stu-id="54775-263">**Disk performance (IOPS) with different RAID levels**</span></span>

![E/S par seconde du disque avec des niveaux RAID différents][9]

<span data-ttu-id="54775-265">**Commandes de test**</span><span class="sxs-lookup"><span data-stu-id="54775-265">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> <span data-ttu-id="54775-266">La charge de travail de ce test utilise 64 threads, pour tenter d’atteindre la limite supérieure de RAID.</span><span class="sxs-lookup"><span data-stu-id="54775-266">The workload of this test uses 64 threads, trying to reach the upper limit of RAID.</span></span>
>
>

### <span data-ttu-id="54775-267"><a name="AppendixB"></a>Annexe B</span><span class="sxs-lookup"><span data-stu-id="54775-267"><a name="AppendixB"></a>Appendix B</span></span>  
<span data-ttu-id="54775-268">**Comparaison des performances (débit) MySQL avec des niveaux RAID différents** </span><span class="sxs-lookup"><span data-stu-id="54775-268">**MySQL performance (throughput) comparison with different RAID levels** </span></span>  
<span data-ttu-id="54775-269">(système de fichiers XFS)</span><span class="sxs-lookup"><span data-stu-id="54775-269">(XFS file system)</span></span>

![Comparaison des performances MySQL avec des niveaux RAID différents][10]  
![Comparaison des performances MySQL avec des niveaux RAID différents][11]

<span data-ttu-id="54775-272">**Commandes de test**</span><span class="sxs-lookup"><span data-stu-id="54775-272">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

<span data-ttu-id="54775-273">**Comparaison des performances (OLTP) MySQL avec des niveaux RAID différents**</span><span class="sxs-lookup"><span data-stu-id="54775-273">**MySQL performance (OLTP) comparison with different RAID levels**</span></span>  
<span data-ttu-id="54775-274">![Comparaison des performances (OLTP) MySQL avec des niveaux RAID différents][12]</span><span class="sxs-lookup"><span data-stu-id="54775-274">![MySQL performance (OLTP) comparison with different RAID levels][12]</span></span>

<span data-ttu-id="54775-275">**Commandes de test**</span><span class="sxs-lookup"><span data-stu-id="54775-275">**Test commands**</span></span>

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <span data-ttu-id="54775-276"><a name="AppendixC"></a>Annexe C</span><span class="sxs-lookup"><span data-stu-id="54775-276"><a name="AppendixC"></a>Appendix C</span></span>   
<span data-ttu-id="54775-277">**Comparaison des performances (IOPS) de disque avec différentes tailles de segment**</span><span class="sxs-lookup"><span data-stu-id="54775-277">**Disk performance (IOPS) comparison for different chunk sizes**</span></span>  
<span data-ttu-id="54775-278">(système de fichiers XFS)</span><span class="sxs-lookup"><span data-stu-id="54775-278">(XFS file system)</span></span>

![][13]

<span data-ttu-id="54775-279">**Commandes de test**</span><span class="sxs-lookup"><span data-stu-id="54775-279">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

<span data-ttu-id="54775-280">La taille des fichiers utilisés pour ce test est de 30 Go et 1 Go respectivement, avec le système de fichiers XFS RAID 0 (4 disques).</span><span class="sxs-lookup"><span data-stu-id="54775-280">The file sizes used for this testing are 30 GB and 1 GB, respectively, with RAID 0 (4 disks) XFS file system.</span></span>

### <span data-ttu-id="54775-281"><a name="AppendixD"></a>Annexe D</span><span class="sxs-lookup"><span data-stu-id="54775-281"><a name="AppendixD"></a>Appendix D</span></span>  
<span data-ttu-id="54775-282">**Comparaison des performances (débit) MySQL avant et après l’optimisation**</span><span class="sxs-lookup"><span data-stu-id="54775-282">**MySQL performance (throughput) comparison before and after optimization**</span></span>  
<span data-ttu-id="54775-283">(système de fichiers XFS)</span><span class="sxs-lookup"><span data-stu-id="54775-283">(XFS File System)</span></span>

![Comparaison des performances (débit) MySQL avant et après l’optimisation][14]

<span data-ttu-id="54775-285">**Commandes de test**</span><span class="sxs-lookup"><span data-stu-id="54775-285">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

<span data-ttu-id="54775-286">**Le paramètre de configuration pour la valeur par défaut et l’optimisation est le suivant :**</span><span class="sxs-lookup"><span data-stu-id="54775-286">**The configuration setting for default and optimization is as follows:**</span></span>

| <span data-ttu-id="54775-287">parameters</span><span class="sxs-lookup"><span data-stu-id="54775-287">Parameters</span></span> | <span data-ttu-id="54775-288">Default</span><span class="sxs-lookup"><span data-stu-id="54775-288">Default</span></span> | <span data-ttu-id="54775-289">Optimisation</span><span class="sxs-lookup"><span data-stu-id="54775-289">Optimization</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54775-290">**innodb_buffer_pool_size**</span><span class="sxs-lookup"><span data-stu-id="54775-290">**innodb_buffer_pool_size**</span></span> |<span data-ttu-id="54775-291">Aucune</span><span class="sxs-lookup"><span data-stu-id="54775-291">None</span></span> |<span data-ttu-id="54775-292">7 Go</span><span class="sxs-lookup"><span data-stu-id="54775-292">7 GB</span></span> |
| <span data-ttu-id="54775-293">**innodb_log_file_size**</span><span class="sxs-lookup"><span data-stu-id="54775-293">**innodb_log_file_size**</span></span> |<span data-ttu-id="54775-294">5 Mo</span><span class="sxs-lookup"><span data-stu-id="54775-294">5 MB</span></span> |<span data-ttu-id="54775-295">512 Mo</span><span class="sxs-lookup"><span data-stu-id="54775-295">512 MB</span></span> |
| <span data-ttu-id="54775-296">**max_connections**</span><span class="sxs-lookup"><span data-stu-id="54775-296">**max_connections**</span></span> |<span data-ttu-id="54775-297">100</span><span class="sxs-lookup"><span data-stu-id="54775-297">100</span></span> |<span data-ttu-id="54775-298">5 000</span><span class="sxs-lookup"><span data-stu-id="54775-298">5000</span></span> |
| <span data-ttu-id="54775-299">**innodb_file_per_table**</span><span class="sxs-lookup"><span data-stu-id="54775-299">**innodb_file_per_table**</span></span> |<span data-ttu-id="54775-300">0</span><span class="sxs-lookup"><span data-stu-id="54775-300">0</span></span> |<span data-ttu-id="54775-301">1</span><span class="sxs-lookup"><span data-stu-id="54775-301">1</span></span> |
| <span data-ttu-id="54775-302">**innodb_flush_log_at_trx_commit**</span><span class="sxs-lookup"><span data-stu-id="54775-302">**innodb_flush_log_at_trx_commit**</span></span> |<span data-ttu-id="54775-303">1</span><span class="sxs-lookup"><span data-stu-id="54775-303">1</span></span> |<span data-ttu-id="54775-304">2</span><span class="sxs-lookup"><span data-stu-id="54775-304">2</span></span> |
| <span data-ttu-id="54775-305">**innodb_log_buffer_size**</span><span class="sxs-lookup"><span data-stu-id="54775-305">**innodb_log_buffer_size**</span></span> |<span data-ttu-id="54775-306">8 Mo</span><span class="sxs-lookup"><span data-stu-id="54775-306">8 MB</span></span> |<span data-ttu-id="54775-307">128 Mo</span><span class="sxs-lookup"><span data-stu-id="54775-307">128 MB</span></span> |
| <span data-ttu-id="54775-308">**query_cache_size**</span><span class="sxs-lookup"><span data-stu-id="54775-308">**query_cache_size**</span></span> |<span data-ttu-id="54775-309">16 Mo</span><span class="sxs-lookup"><span data-stu-id="54775-309">16 MB</span></span> |<span data-ttu-id="54775-310">0</span><span class="sxs-lookup"><span data-stu-id="54775-310">0</span></span> |

<span data-ttu-id="54775-311">Pour obtenir plus de détails sur les [paramètres de configuration d’optimisation](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), consultez les [instructions officielles de MySQL](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span><span class="sxs-lookup"><span data-stu-id="54775-311">For more detailed [optimization configuration parameters](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), refer to the [MySQL official instructions](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span></span>  

  <span data-ttu-id="54775-312">**Environnement de test**</span><span class="sxs-lookup"><span data-stu-id="54775-312">**Test environment**</span></span>  

| <span data-ttu-id="54775-313">Matériel</span><span class="sxs-lookup"><span data-stu-id="54775-313">Hardware</span></span> | <span data-ttu-id="54775-314">Détails</span><span class="sxs-lookup"><span data-stu-id="54775-314">Details</span></span> |
| --- | --- |
| <span data-ttu-id="54775-315">UC</span><span class="sxs-lookup"><span data-stu-id="54775-315">CPU</span></span> |<span data-ttu-id="54775-316">AMD Opteron(tm) Processeur 4171 HE/4 cœurs</span><span class="sxs-lookup"><span data-stu-id="54775-316">AMD Opteron(tm) Processor 4171 HE/4 cores</span></span> |
| <span data-ttu-id="54775-317">Mémoire</span><span class="sxs-lookup"><span data-stu-id="54775-317">Memory</span></span> |<span data-ttu-id="54775-318">14 Go</span><span class="sxs-lookup"><span data-stu-id="54775-318">14 GB</span></span> |
| <span data-ttu-id="54775-319">Disque</span><span class="sxs-lookup"><span data-stu-id="54775-319">Disk</span></span> |<span data-ttu-id="54775-320">10 Go/disque</span><span class="sxs-lookup"><span data-stu-id="54775-320">10 GB/disk</span></span> |
| <span data-ttu-id="54775-321">SE</span><span class="sxs-lookup"><span data-stu-id="54775-321">OS</span></span> |<span data-ttu-id="54775-322">Ubuntu 14.04.1 LTS</span><span class="sxs-lookup"><span data-stu-id="54775-322">Ubuntu 14.04.1 LTS</span></span> |

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

