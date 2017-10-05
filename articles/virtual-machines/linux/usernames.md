---
title: "Sélection de noms d’utilisateur pour Linux | Microsoft Docs"
description: "Apprenez à sélectionner des noms d'utilisateur pour une machine virtuelle Linux dans Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 33b50c97-92f1-46c9-a623-e37f67459c5c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 1874d72e5f88816036667932371ff28704d186c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a><span data-ttu-id="085fa-103">Sélection de noms d'utilisateur pour Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="085fa-103">Selecting User Names for Linux on Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="085fa-104">Quand vous configurez une machine virtuelle Linux sur Azure, vous devez spécifier le nom d’utilisateur non racine que vous pourrez utiliser ultérieurement pour vous connecter à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="085fa-104">When you provision a Linux virtual machine on Azure you must specify the name of a non-root user that you can later use to log into the VM.</span></span> <span data-ttu-id="085fa-105">Vous pouvez choisir le nom du nouvel utilisateur, ou en cas d’approvisionnement via le portail Azure Classic, vous pouvez accepter le nom par défaut, « azureuser ».</span><span class="sxs-lookup"><span data-stu-id="085fa-105">You may choose the name of the new user, or if provisioning via the Azure classic portal you can accept the default name "azureuser".</span></span>

<span data-ttu-id="085fa-106">Dans la plupart des cas, ce nouvel utilisateur n’existe pas dans l’image de base et sera créé pendant le processus d’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="085fa-106">In most cases this user won't exist on the base image and will be created during the provisioning process.</span></span> <span data-ttu-id="085fa-107">Si l’utilisateur existe dans l’image de machine virtuelle de base, l’agent Linux Azure configure simplement le mot de passe et/ou la clé SSH pour cet utilisateur selon les informations indiquées lors de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="085fa-107">If the user exists on the base VM image, then the Azure Linux agent simply configures the password and/or SSH key for that user based on the information you specified when creating the VM.</span></span>

<span data-ttu-id="085fa-108">**Toutefois**, Linux définit un ensemble de noms d’utilisateur à ne pas utiliser pour la création de nouveaux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="085fa-108">**However**, Linux defines a set of user names that should not be used.</span></span> <span data-ttu-id="085fa-109">Le processus d’approvisionnement **échoue** si vous essayez d’approvisionner une machine virtuelle Linux via un utilisateur système existant, défini comme utilisateur avec un ID utilisateur de 0 à 99.</span><span class="sxs-lookup"><span data-stu-id="085fa-109">The provisioning process will **fail** if you try to provision a Linux VM using an existing system user, which is defined as a user with UID 0-99.</span></span> <span data-ttu-id="085fa-110">L’utilisateur `root` , présentant l’ID utilisateur 0, en est un bon exemple.</span><span class="sxs-lookup"><span data-stu-id="085fa-110">A typical example is the `root` user, which has UID 0.</span></span>

* <span data-ttu-id="085fa-111">Voir aussi [Base standard Linux : plages d’ID utilisateur](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span><span class="sxs-lookup"><span data-stu-id="085fa-111">See also: [Linux Standard Base - User ID Ranges](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span></span>

<span data-ttu-id="085fa-112">Voici une liste d’utilisateurs système intégrés courants pour CentOS et Ubuntu que vous devez éviter d’utiliser lors de l’approvisionnement d’une machine virtuelle Linux sur Azure.</span><span class="sxs-lookup"><span data-stu-id="085fa-112">The following is a list of common built-in system users for CentOS and Ubuntu that you should avoid using when provisioning a Linux virtual machine on Azure.</span></span> <span data-ttu-id="085fa-113">Cette liste n’est qu’un exemple. Reportez-vous à la documentation relative à votre distribution pour vous assurer que le nom d’utilisateur que vous choisissez n’est pas en conflit avec un utilisateur système existant.</span><span class="sxs-lookup"><span data-stu-id="085fa-113">This list is just an example, please refer to the documentation for your distribution to ensure that the username you choose does not conflict with an existing system user.</span></span>

## <a name="centos"></a><span data-ttu-id="085fa-114">CentOS</span><span class="sxs-lookup"><span data-stu-id="085fa-114">CentOS</span></span>
* <span data-ttu-id="085fa-115">abrt</span><span class="sxs-lookup"><span data-stu-id="085fa-115">abrt</span></span>
* <span data-ttu-id="085fa-116">adm</span><span class="sxs-lookup"><span data-stu-id="085fa-116">adm</span></span>
* <span data-ttu-id="085fa-117">audio</span><span class="sxs-lookup"><span data-stu-id="085fa-117">audio</span></span>
* <span data-ttu-id="085fa-118">bin</span><span class="sxs-lookup"><span data-stu-id="085fa-118">bin</span></span>
* <span data-ttu-id="085fa-119">cdrom</span><span class="sxs-lookup"><span data-stu-id="085fa-119">cdrom</span></span>
* <span data-ttu-id="085fa-120">cgred</span><span class="sxs-lookup"><span data-stu-id="085fa-120">cgred</span></span>
* <span data-ttu-id="085fa-121">daemon</span><span class="sxs-lookup"><span data-stu-id="085fa-121">daemon</span></span>
* <span data-ttu-id="085fa-122">dbus</span><span class="sxs-lookup"><span data-stu-id="085fa-122">dbus</span></span>
* <span data-ttu-id="085fa-123">dialout</span><span class="sxs-lookup"><span data-stu-id="085fa-123">dialout</span></span>
* <span data-ttu-id="085fa-124">dip</span><span class="sxs-lookup"><span data-stu-id="085fa-124">dip</span></span>
* <span data-ttu-id="085fa-125">disk</span><span class="sxs-lookup"><span data-stu-id="085fa-125">disk</span></span>
* <span data-ttu-id="085fa-126">floppy</span><span class="sxs-lookup"><span data-stu-id="085fa-126">floppy</span></span>
* <span data-ttu-id="085fa-127">ftp</span><span class="sxs-lookup"><span data-stu-id="085fa-127">ftp</span></span>
* <span data-ttu-id="085fa-128">ftp</span><span class="sxs-lookup"><span data-stu-id="085fa-128">ftp</span></span>
* <span data-ttu-id="085fa-129">games</span><span class="sxs-lookup"><span data-stu-id="085fa-129">games</span></span>
* <span data-ttu-id="085fa-130">gopher</span><span class="sxs-lookup"><span data-stu-id="085fa-130">gopher</span></span>
* <span data-ttu-id="085fa-131">haldaemon</span><span class="sxs-lookup"><span data-stu-id="085fa-131">haldaemon</span></span>
* <span data-ttu-id="085fa-132">halt</span><span class="sxs-lookup"><span data-stu-id="085fa-132">halt</span></span>
* <span data-ttu-id="085fa-133">kmem</span><span class="sxs-lookup"><span data-stu-id="085fa-133">kmem</span></span>
* <span data-ttu-id="085fa-134">lock</span><span class="sxs-lookup"><span data-stu-id="085fa-134">lock</span></span>
* <span data-ttu-id="085fa-135">lp</span><span class="sxs-lookup"><span data-stu-id="085fa-135">lp</span></span>
* <span data-ttu-id="085fa-136">mail</span><span class="sxs-lookup"><span data-stu-id="085fa-136">mail</span></span>
* <span data-ttu-id="085fa-137">man</span><span class="sxs-lookup"><span data-stu-id="085fa-137">man</span></span>
* <span data-ttu-id="085fa-138">mem</span><span class="sxs-lookup"><span data-stu-id="085fa-138">mem</span></span>
* <span data-ttu-id="085fa-139">nfsnobody</span><span class="sxs-lookup"><span data-stu-id="085fa-139">nfsnobody</span></span>
* <span data-ttu-id="085fa-140">nobody</span><span class="sxs-lookup"><span data-stu-id="085fa-140">nobody</span></span>
* <span data-ttu-id="085fa-141">ntp</span><span class="sxs-lookup"><span data-stu-id="085fa-141">ntp</span></span>
* <span data-ttu-id="085fa-142">operator</span><span class="sxs-lookup"><span data-stu-id="085fa-142">operator</span></span>
* <span data-ttu-id="085fa-143">oprofile</span><span class="sxs-lookup"><span data-stu-id="085fa-143">oprofile</span></span>
* <span data-ttu-id="085fa-144">postdrop</span><span class="sxs-lookup"><span data-stu-id="085fa-144">postdrop</span></span>
* <span data-ttu-id="085fa-145">postfix</span><span class="sxs-lookup"><span data-stu-id="085fa-145">postfix</span></span>
* <span data-ttu-id="085fa-146">qpidd</span><span class="sxs-lookup"><span data-stu-id="085fa-146">qpidd</span></span>
* <span data-ttu-id="085fa-147">root</span><span class="sxs-lookup"><span data-stu-id="085fa-147">root</span></span>
* <span data-ttu-id="085fa-148">rpc</span><span class="sxs-lookup"><span data-stu-id="085fa-148">rpc</span></span>
* <span data-ttu-id="085fa-149">rpcuser</span><span class="sxs-lookup"><span data-stu-id="085fa-149">rpcuser</span></span>
* <span data-ttu-id="085fa-150">saslauth</span><span class="sxs-lookup"><span data-stu-id="085fa-150">saslauth</span></span>
* <span data-ttu-id="085fa-151">shutdown</span><span class="sxs-lookup"><span data-stu-id="085fa-151">shutdown</span></span>
* <span data-ttu-id="085fa-152">slocate</span><span class="sxs-lookup"><span data-stu-id="085fa-152">slocate</span></span>
* <span data-ttu-id="085fa-153">sshd</span><span class="sxs-lookup"><span data-stu-id="085fa-153">sshd</span></span>
* <span data-ttu-id="085fa-154">stapdev</span><span class="sxs-lookup"><span data-stu-id="085fa-154">stapdev</span></span>
* <span data-ttu-id="085fa-155">stapusr</span><span class="sxs-lookup"><span data-stu-id="085fa-155">stapusr</span></span>
* <span data-ttu-id="085fa-156">sync</span><span class="sxs-lookup"><span data-stu-id="085fa-156">sync</span></span>
* <span data-ttu-id="085fa-157">sys</span><span class="sxs-lookup"><span data-stu-id="085fa-157">sys</span></span>
* <span data-ttu-id="085fa-158">tape</span><span class="sxs-lookup"><span data-stu-id="085fa-158">tape</span></span>
* <span data-ttu-id="085fa-159">test</span><span class="sxs-lookup"><span data-stu-id="085fa-159">test</span></span>
* <span data-ttu-id="085fa-160">tcpdump</span><span class="sxs-lookup"><span data-stu-id="085fa-160">tcpdump</span></span>
* <span data-ttu-id="085fa-161">tty</span><span class="sxs-lookup"><span data-stu-id="085fa-161">tty</span></span>
* <span data-ttu-id="085fa-162">users</span><span class="sxs-lookup"><span data-stu-id="085fa-162">users</span></span>
* <span data-ttu-id="085fa-163">utempter</span><span class="sxs-lookup"><span data-stu-id="085fa-163">utempter</span></span>
* <span data-ttu-id="085fa-164">utmp</span><span class="sxs-lookup"><span data-stu-id="085fa-164">utmp</span></span>
* <span data-ttu-id="085fa-165">uucp</span><span class="sxs-lookup"><span data-stu-id="085fa-165">uucp</span></span>
* <span data-ttu-id="085fa-166">vcsa</span><span class="sxs-lookup"><span data-stu-id="085fa-166">vcsa</span></span>
* <span data-ttu-id="085fa-167">video</span><span class="sxs-lookup"><span data-stu-id="085fa-167">video</span></span>
* <span data-ttu-id="085fa-168">wheel</span><span class="sxs-lookup"><span data-stu-id="085fa-168">wheel</span></span>

## <a name="ubuntu"></a><span data-ttu-id="085fa-169">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="085fa-169">Ubuntu</span></span>
* <span data-ttu-id="085fa-170">adm</span><span class="sxs-lookup"><span data-stu-id="085fa-170">adm</span></span>
* <span data-ttu-id="085fa-171">admin</span><span class="sxs-lookup"><span data-stu-id="085fa-171">admin</span></span>
* <span data-ttu-id="085fa-172">audio</span><span class="sxs-lookup"><span data-stu-id="085fa-172">audio</span></span>
* <span data-ttu-id="085fa-173">backup</span><span class="sxs-lookup"><span data-stu-id="085fa-173">backup</span></span>
* <span data-ttu-id="085fa-174">bin</span><span class="sxs-lookup"><span data-stu-id="085fa-174">bin</span></span>
* <span data-ttu-id="085fa-175">cdrom</span><span class="sxs-lookup"><span data-stu-id="085fa-175">cdrom</span></span>
* <span data-ttu-id="085fa-176">crontab</span><span class="sxs-lookup"><span data-stu-id="085fa-176">crontab</span></span>
* <span data-ttu-id="085fa-177">daemon</span><span class="sxs-lookup"><span data-stu-id="085fa-177">daemon</span></span>
* <span data-ttu-id="085fa-178">dialout</span><span class="sxs-lookup"><span data-stu-id="085fa-178">dialout</span></span>
* <span data-ttu-id="085fa-179">dip</span><span class="sxs-lookup"><span data-stu-id="085fa-179">dip</span></span>
* <span data-ttu-id="085fa-180">disk</span><span class="sxs-lookup"><span data-stu-id="085fa-180">disk</span></span>
* <span data-ttu-id="085fa-181">fax</span><span class="sxs-lookup"><span data-stu-id="085fa-181">fax</span></span>
* <span data-ttu-id="085fa-182">floppy</span><span class="sxs-lookup"><span data-stu-id="085fa-182">floppy</span></span>
* <span data-ttu-id="085fa-183">fuse</span><span class="sxs-lookup"><span data-stu-id="085fa-183">fuse</span></span>
* <span data-ttu-id="085fa-184">games</span><span class="sxs-lookup"><span data-stu-id="085fa-184">games</span></span>
* <span data-ttu-id="085fa-185">gnats</span><span class="sxs-lookup"><span data-stu-id="085fa-185">gnats</span></span>
* <span data-ttu-id="085fa-186">irc</span><span class="sxs-lookup"><span data-stu-id="085fa-186">irc</span></span>
* <span data-ttu-id="085fa-187">kmem</span><span class="sxs-lookup"><span data-stu-id="085fa-187">kmem</span></span>
* <span data-ttu-id="085fa-188">landscape</span><span class="sxs-lookup"><span data-stu-id="085fa-188">landscape</span></span>
* <span data-ttu-id="085fa-189">libuuid</span><span class="sxs-lookup"><span data-stu-id="085fa-189">libuuid</span></span>
* <span data-ttu-id="085fa-190">list</span><span class="sxs-lookup"><span data-stu-id="085fa-190">list</span></span>
* <span data-ttu-id="085fa-191">lp</span><span class="sxs-lookup"><span data-stu-id="085fa-191">lp</span></span>
* <span data-ttu-id="085fa-192">mail</span><span class="sxs-lookup"><span data-stu-id="085fa-192">mail</span></span>
* <span data-ttu-id="085fa-193">man</span><span class="sxs-lookup"><span data-stu-id="085fa-193">man</span></span>
* <span data-ttu-id="085fa-194">messagebus</span><span class="sxs-lookup"><span data-stu-id="085fa-194">messagebus</span></span>
* <span data-ttu-id="085fa-195">mlocate</span><span class="sxs-lookup"><span data-stu-id="085fa-195">mlocate</span></span>
* <span data-ttu-id="085fa-196">netdev</span><span class="sxs-lookup"><span data-stu-id="085fa-196">netdev</span></span>
* <span data-ttu-id="085fa-197">news</span><span class="sxs-lookup"><span data-stu-id="085fa-197">news</span></span>
* <span data-ttu-id="085fa-198">nobody</span><span class="sxs-lookup"><span data-stu-id="085fa-198">nobody</span></span>
* <span data-ttu-id="085fa-199">nogroup</span><span class="sxs-lookup"><span data-stu-id="085fa-199">nogroup</span></span>
* <span data-ttu-id="085fa-200">operator</span><span class="sxs-lookup"><span data-stu-id="085fa-200">operator</span></span>
* <span data-ttu-id="085fa-201">plugdev</span><span class="sxs-lookup"><span data-stu-id="085fa-201">plugdev</span></span>
* <span data-ttu-id="085fa-202">proxy</span><span class="sxs-lookup"><span data-stu-id="085fa-202">proxy</span></span>
* <span data-ttu-id="085fa-203">root</span><span class="sxs-lookup"><span data-stu-id="085fa-203">root</span></span>
* <span data-ttu-id="085fa-204">sasl</span><span class="sxs-lookup"><span data-stu-id="085fa-204">sasl</span></span>
* <span data-ttu-id="085fa-205">shadow</span><span class="sxs-lookup"><span data-stu-id="085fa-205">shadow</span></span>
* <span data-ttu-id="085fa-206">src</span><span class="sxs-lookup"><span data-stu-id="085fa-206">src</span></span>
* <span data-ttu-id="085fa-207">ssh</span><span class="sxs-lookup"><span data-stu-id="085fa-207">ssh</span></span>
* <span data-ttu-id="085fa-208">sshd</span><span class="sxs-lookup"><span data-stu-id="085fa-208">sshd</span></span>
* <span data-ttu-id="085fa-209">staff</span><span class="sxs-lookup"><span data-stu-id="085fa-209">staff</span></span>
* <span data-ttu-id="085fa-210">sudo</span><span class="sxs-lookup"><span data-stu-id="085fa-210">sudo</span></span>
* <span data-ttu-id="085fa-211">sync</span><span class="sxs-lookup"><span data-stu-id="085fa-211">sync</span></span>
* <span data-ttu-id="085fa-212">sys</span><span class="sxs-lookup"><span data-stu-id="085fa-212">sys</span></span>
* <span data-ttu-id="085fa-213">syslog</span><span class="sxs-lookup"><span data-stu-id="085fa-213">syslog</span></span>
* <span data-ttu-id="085fa-214">tape</span><span class="sxs-lookup"><span data-stu-id="085fa-214">tape</span></span>
* <span data-ttu-id="085fa-215">tty</span><span class="sxs-lookup"><span data-stu-id="085fa-215">tty</span></span>
* <span data-ttu-id="085fa-216">users</span><span class="sxs-lookup"><span data-stu-id="085fa-216">users</span></span>
* <span data-ttu-id="085fa-217">utmp</span><span class="sxs-lookup"><span data-stu-id="085fa-217">utmp</span></span>
* <span data-ttu-id="085fa-218">uucp</span><span class="sxs-lookup"><span data-stu-id="085fa-218">uucp</span></span>
* <span data-ttu-id="085fa-219">video</span><span class="sxs-lookup"><span data-stu-id="085fa-219">video</span></span>
* <span data-ttu-id="085fa-220">voice</span><span class="sxs-lookup"><span data-stu-id="085fa-220">voice</span></span>
* <span data-ttu-id="085fa-221">whoopsie</span><span class="sxs-lookup"><span data-stu-id="085fa-221">whoopsie</span></span>
* <span data-ttu-id="085fa-222">www-data</span><span class="sxs-lookup"><span data-stu-id="085fa-222">www-data</span></span>

