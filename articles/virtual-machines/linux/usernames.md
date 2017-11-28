---
title: "aaaSelecting noms d’utilisateur pour Linux | Documents Microsoft"
description: "Découvrez comment des noms tooselect utilisateur pour un ordinateur virtuel de Linux dans Azure."
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
ms.openlocfilehash: c65e2ac46f40bb8c9d74cccbaf248a070c0fa6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a><span data-ttu-id="f60f9-103">Sélection de noms d'utilisateur pour Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="f60f9-103">Selecting User Names for Linux on Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="f60f9-104">Lorsque vous configurez un ordinateur virtuel de Linux sur Azure, vous devez spécifier nom hello d’un utilisateur non racine que vous pouvez utiliser ultérieurement toolog dans hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f60f9-104">When you provision a Linux virtual machine on Azure you must specify hello name of a non-root user that you can later use toolog into hello VM.</span></span> <span data-ttu-id="f60f9-105">Vous pouvez choisir le nom hello du nouvel utilisateur de hello, ou si la configuration via hello portail Azure classic accepter par défaut de hello nom « azureuser ».</span><span class="sxs-lookup"><span data-stu-id="f60f9-105">You may choose hello name of hello new user, or if provisioning via hello Azure classic portal you can accept hello default name "azureuser".</span></span>

<span data-ttu-id="f60f9-106">Dans la plupart des cas, cet utilisateur n’existe pas sur l’image de base hello et sera créé pendant le processus d’approvisionnement de hello.</span><span class="sxs-lookup"><span data-stu-id="f60f9-106">In most cases this user won't exist on hello base image and will be created during hello provisioning process.</span></span> <span data-ttu-id="f60f9-107">Si l’utilisateur hello existe sur l’image de machine virtuelle base hello, puis hello Azure Linux agent simplement configure un mot de passe hello et/ou une clé SSH pour cet utilisateur en fonction des informations hello que vous avez spécifié lors de la création de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f60f9-107">If hello user exists on hello base VM image, then hello Azure Linux agent simply configures hello password and/or SSH key for that user based on hello information you specified when creating hello VM.</span></span>

<span data-ttu-id="f60f9-108">**Toutefois**, Linux définit un ensemble de noms d’utilisateur à ne pas utiliser pour la création de nouveaux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f60f9-108">**However**, Linux defines a set of user names that should not be used.</span></span> <span data-ttu-id="f60f9-109">Hello mise en service du processus sera **échouer** si vous essayez de tooprovision une VM Linux à l’aide d’un utilisateur système existant, qui est défini en tant qu’utilisateur avec UID 0 et 99.</span><span class="sxs-lookup"><span data-stu-id="f60f9-109">hello provisioning process will **fail** if you try tooprovision a Linux VM using an existing system user, which is defined as a user with UID 0-99.</span></span> <span data-ttu-id="f60f9-110">Un exemple classique est hello `root` utilisateur, ce qui a des UID 0.</span><span class="sxs-lookup"><span data-stu-id="f60f9-110">A typical example is hello `root` user, which has UID 0.</span></span>

* <span data-ttu-id="f60f9-111">Voir aussi [Base standard Linux : plages d’ID utilisateur](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span><span class="sxs-lookup"><span data-stu-id="f60f9-111">See also: [Linux Standard Base - User ID Ranges](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span></span>

<span data-ttu-id="f60f9-112">Hello Voici une liste des utilisateurs système intégré commun CentOS et Ubuntu que vous devez éviter d’utiliser lors de la configuration d’un ordinateur virtuel de Linux sur Azure.</span><span class="sxs-lookup"><span data-stu-id="f60f9-112">hello following is a list of common built-in system users for CentOS and Ubuntu that you should avoid using when provisioning a Linux virtual machine on Azure.</span></span> <span data-ttu-id="f60f9-113">Cette liste est juste un exemple, consultez toohello documentation pour votre tooensure distribution username hello que vous choisissez ne sont pas en conflit avec un utilisateur système existant.</span><span class="sxs-lookup"><span data-stu-id="f60f9-113">This list is just an example, please refer toohello documentation for your distribution tooensure that hello username you choose does not conflict with an existing system user.</span></span>

## <a name="centos"></a><span data-ttu-id="f60f9-114">CentOS</span><span class="sxs-lookup"><span data-stu-id="f60f9-114">CentOS</span></span>
* <span data-ttu-id="f60f9-115">abrt</span><span class="sxs-lookup"><span data-stu-id="f60f9-115">abrt</span></span>
* <span data-ttu-id="f60f9-116">adm</span><span class="sxs-lookup"><span data-stu-id="f60f9-116">adm</span></span>
* <span data-ttu-id="f60f9-117">audio</span><span class="sxs-lookup"><span data-stu-id="f60f9-117">audio</span></span>
* <span data-ttu-id="f60f9-118">bin</span><span class="sxs-lookup"><span data-stu-id="f60f9-118">bin</span></span>
* <span data-ttu-id="f60f9-119">cdrom</span><span class="sxs-lookup"><span data-stu-id="f60f9-119">cdrom</span></span>
* <span data-ttu-id="f60f9-120">cgred</span><span class="sxs-lookup"><span data-stu-id="f60f9-120">cgred</span></span>
* <span data-ttu-id="f60f9-121">daemon</span><span class="sxs-lookup"><span data-stu-id="f60f9-121">daemon</span></span>
* <span data-ttu-id="f60f9-122">dbus</span><span class="sxs-lookup"><span data-stu-id="f60f9-122">dbus</span></span>
* <span data-ttu-id="f60f9-123">dialout</span><span class="sxs-lookup"><span data-stu-id="f60f9-123">dialout</span></span>
* <span data-ttu-id="f60f9-124">dip</span><span class="sxs-lookup"><span data-stu-id="f60f9-124">dip</span></span>
* <span data-ttu-id="f60f9-125">disk</span><span class="sxs-lookup"><span data-stu-id="f60f9-125">disk</span></span>
* <span data-ttu-id="f60f9-126">floppy</span><span class="sxs-lookup"><span data-stu-id="f60f9-126">floppy</span></span>
* <span data-ttu-id="f60f9-127">ftp</span><span class="sxs-lookup"><span data-stu-id="f60f9-127">ftp</span></span>
* <span data-ttu-id="f60f9-128">ftp</span><span class="sxs-lookup"><span data-stu-id="f60f9-128">ftp</span></span>
* <span data-ttu-id="f60f9-129">games</span><span class="sxs-lookup"><span data-stu-id="f60f9-129">games</span></span>
* <span data-ttu-id="f60f9-130">gopher</span><span class="sxs-lookup"><span data-stu-id="f60f9-130">gopher</span></span>
* <span data-ttu-id="f60f9-131">haldaemon</span><span class="sxs-lookup"><span data-stu-id="f60f9-131">haldaemon</span></span>
* <span data-ttu-id="f60f9-132">halt</span><span class="sxs-lookup"><span data-stu-id="f60f9-132">halt</span></span>
* <span data-ttu-id="f60f9-133">kmem</span><span class="sxs-lookup"><span data-stu-id="f60f9-133">kmem</span></span>
* <span data-ttu-id="f60f9-134">lock</span><span class="sxs-lookup"><span data-stu-id="f60f9-134">lock</span></span>
* <span data-ttu-id="f60f9-135">lp</span><span class="sxs-lookup"><span data-stu-id="f60f9-135">lp</span></span>
* <span data-ttu-id="f60f9-136">mail</span><span class="sxs-lookup"><span data-stu-id="f60f9-136">mail</span></span>
* <span data-ttu-id="f60f9-137">man</span><span class="sxs-lookup"><span data-stu-id="f60f9-137">man</span></span>
* <span data-ttu-id="f60f9-138">mem</span><span class="sxs-lookup"><span data-stu-id="f60f9-138">mem</span></span>
* <span data-ttu-id="f60f9-139">nfsnobody</span><span class="sxs-lookup"><span data-stu-id="f60f9-139">nfsnobody</span></span>
* <span data-ttu-id="f60f9-140">nobody</span><span class="sxs-lookup"><span data-stu-id="f60f9-140">nobody</span></span>
* <span data-ttu-id="f60f9-141">ntp</span><span class="sxs-lookup"><span data-stu-id="f60f9-141">ntp</span></span>
* <span data-ttu-id="f60f9-142">operator</span><span class="sxs-lookup"><span data-stu-id="f60f9-142">operator</span></span>
* <span data-ttu-id="f60f9-143">oprofile</span><span class="sxs-lookup"><span data-stu-id="f60f9-143">oprofile</span></span>
* <span data-ttu-id="f60f9-144">postdrop</span><span class="sxs-lookup"><span data-stu-id="f60f9-144">postdrop</span></span>
* <span data-ttu-id="f60f9-145">postfix</span><span class="sxs-lookup"><span data-stu-id="f60f9-145">postfix</span></span>
* <span data-ttu-id="f60f9-146">qpidd</span><span class="sxs-lookup"><span data-stu-id="f60f9-146">qpidd</span></span>
* <span data-ttu-id="f60f9-147">root</span><span class="sxs-lookup"><span data-stu-id="f60f9-147">root</span></span>
* <span data-ttu-id="f60f9-148">rpc</span><span class="sxs-lookup"><span data-stu-id="f60f9-148">rpc</span></span>
* <span data-ttu-id="f60f9-149">rpcuser</span><span class="sxs-lookup"><span data-stu-id="f60f9-149">rpcuser</span></span>
* <span data-ttu-id="f60f9-150">saslauth</span><span class="sxs-lookup"><span data-stu-id="f60f9-150">saslauth</span></span>
* <span data-ttu-id="f60f9-151">shutdown</span><span class="sxs-lookup"><span data-stu-id="f60f9-151">shutdown</span></span>
* <span data-ttu-id="f60f9-152">slocate</span><span class="sxs-lookup"><span data-stu-id="f60f9-152">slocate</span></span>
* <span data-ttu-id="f60f9-153">sshd</span><span class="sxs-lookup"><span data-stu-id="f60f9-153">sshd</span></span>
* <span data-ttu-id="f60f9-154">stapdev</span><span class="sxs-lookup"><span data-stu-id="f60f9-154">stapdev</span></span>
* <span data-ttu-id="f60f9-155">stapusr</span><span class="sxs-lookup"><span data-stu-id="f60f9-155">stapusr</span></span>
* <span data-ttu-id="f60f9-156">sync</span><span class="sxs-lookup"><span data-stu-id="f60f9-156">sync</span></span>
* <span data-ttu-id="f60f9-157">sys</span><span class="sxs-lookup"><span data-stu-id="f60f9-157">sys</span></span>
* <span data-ttu-id="f60f9-158">tape</span><span class="sxs-lookup"><span data-stu-id="f60f9-158">tape</span></span>
* <span data-ttu-id="f60f9-159">test</span><span class="sxs-lookup"><span data-stu-id="f60f9-159">test</span></span>
* <span data-ttu-id="f60f9-160">tcpdump</span><span class="sxs-lookup"><span data-stu-id="f60f9-160">tcpdump</span></span>
* <span data-ttu-id="f60f9-161">tty</span><span class="sxs-lookup"><span data-stu-id="f60f9-161">tty</span></span>
* <span data-ttu-id="f60f9-162">users</span><span class="sxs-lookup"><span data-stu-id="f60f9-162">users</span></span>
* <span data-ttu-id="f60f9-163">utempter</span><span class="sxs-lookup"><span data-stu-id="f60f9-163">utempter</span></span>
* <span data-ttu-id="f60f9-164">utmp</span><span class="sxs-lookup"><span data-stu-id="f60f9-164">utmp</span></span>
* <span data-ttu-id="f60f9-165">uucp</span><span class="sxs-lookup"><span data-stu-id="f60f9-165">uucp</span></span>
* <span data-ttu-id="f60f9-166">vcsa</span><span class="sxs-lookup"><span data-stu-id="f60f9-166">vcsa</span></span>
* <span data-ttu-id="f60f9-167">video</span><span class="sxs-lookup"><span data-stu-id="f60f9-167">video</span></span>
* <span data-ttu-id="f60f9-168">wheel</span><span class="sxs-lookup"><span data-stu-id="f60f9-168">wheel</span></span>

## <a name="ubuntu"></a><span data-ttu-id="f60f9-169">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="f60f9-169">Ubuntu</span></span>
* <span data-ttu-id="f60f9-170">adm</span><span class="sxs-lookup"><span data-stu-id="f60f9-170">adm</span></span>
* <span data-ttu-id="f60f9-171">admin</span><span class="sxs-lookup"><span data-stu-id="f60f9-171">admin</span></span>
* <span data-ttu-id="f60f9-172">audio</span><span class="sxs-lookup"><span data-stu-id="f60f9-172">audio</span></span>
* <span data-ttu-id="f60f9-173">backup</span><span class="sxs-lookup"><span data-stu-id="f60f9-173">backup</span></span>
* <span data-ttu-id="f60f9-174">bin</span><span class="sxs-lookup"><span data-stu-id="f60f9-174">bin</span></span>
* <span data-ttu-id="f60f9-175">cdrom</span><span class="sxs-lookup"><span data-stu-id="f60f9-175">cdrom</span></span>
* <span data-ttu-id="f60f9-176">crontab</span><span class="sxs-lookup"><span data-stu-id="f60f9-176">crontab</span></span>
* <span data-ttu-id="f60f9-177">daemon</span><span class="sxs-lookup"><span data-stu-id="f60f9-177">daemon</span></span>
* <span data-ttu-id="f60f9-178">dialout</span><span class="sxs-lookup"><span data-stu-id="f60f9-178">dialout</span></span>
* <span data-ttu-id="f60f9-179">dip</span><span class="sxs-lookup"><span data-stu-id="f60f9-179">dip</span></span>
* <span data-ttu-id="f60f9-180">disk</span><span class="sxs-lookup"><span data-stu-id="f60f9-180">disk</span></span>
* <span data-ttu-id="f60f9-181">fax</span><span class="sxs-lookup"><span data-stu-id="f60f9-181">fax</span></span>
* <span data-ttu-id="f60f9-182">floppy</span><span class="sxs-lookup"><span data-stu-id="f60f9-182">floppy</span></span>
* <span data-ttu-id="f60f9-183">fuse</span><span class="sxs-lookup"><span data-stu-id="f60f9-183">fuse</span></span>
* <span data-ttu-id="f60f9-184">games</span><span class="sxs-lookup"><span data-stu-id="f60f9-184">games</span></span>
* <span data-ttu-id="f60f9-185">gnats</span><span class="sxs-lookup"><span data-stu-id="f60f9-185">gnats</span></span>
* <span data-ttu-id="f60f9-186">irc</span><span class="sxs-lookup"><span data-stu-id="f60f9-186">irc</span></span>
* <span data-ttu-id="f60f9-187">kmem</span><span class="sxs-lookup"><span data-stu-id="f60f9-187">kmem</span></span>
* <span data-ttu-id="f60f9-188">landscape</span><span class="sxs-lookup"><span data-stu-id="f60f9-188">landscape</span></span>
* <span data-ttu-id="f60f9-189">libuuid</span><span class="sxs-lookup"><span data-stu-id="f60f9-189">libuuid</span></span>
* <span data-ttu-id="f60f9-190">list</span><span class="sxs-lookup"><span data-stu-id="f60f9-190">list</span></span>
* <span data-ttu-id="f60f9-191">lp</span><span class="sxs-lookup"><span data-stu-id="f60f9-191">lp</span></span>
* <span data-ttu-id="f60f9-192">mail</span><span class="sxs-lookup"><span data-stu-id="f60f9-192">mail</span></span>
* <span data-ttu-id="f60f9-193">man</span><span class="sxs-lookup"><span data-stu-id="f60f9-193">man</span></span>
* <span data-ttu-id="f60f9-194">messagebus</span><span class="sxs-lookup"><span data-stu-id="f60f9-194">messagebus</span></span>
* <span data-ttu-id="f60f9-195">mlocate</span><span class="sxs-lookup"><span data-stu-id="f60f9-195">mlocate</span></span>
* <span data-ttu-id="f60f9-196">netdev</span><span class="sxs-lookup"><span data-stu-id="f60f9-196">netdev</span></span>
* <span data-ttu-id="f60f9-197">news</span><span class="sxs-lookup"><span data-stu-id="f60f9-197">news</span></span>
* <span data-ttu-id="f60f9-198">nobody</span><span class="sxs-lookup"><span data-stu-id="f60f9-198">nobody</span></span>
* <span data-ttu-id="f60f9-199">nogroup</span><span class="sxs-lookup"><span data-stu-id="f60f9-199">nogroup</span></span>
* <span data-ttu-id="f60f9-200">operator</span><span class="sxs-lookup"><span data-stu-id="f60f9-200">operator</span></span>
* <span data-ttu-id="f60f9-201">plugdev</span><span class="sxs-lookup"><span data-stu-id="f60f9-201">plugdev</span></span>
* <span data-ttu-id="f60f9-202">proxy</span><span class="sxs-lookup"><span data-stu-id="f60f9-202">proxy</span></span>
* <span data-ttu-id="f60f9-203">root</span><span class="sxs-lookup"><span data-stu-id="f60f9-203">root</span></span>
* <span data-ttu-id="f60f9-204">sasl</span><span class="sxs-lookup"><span data-stu-id="f60f9-204">sasl</span></span>
* <span data-ttu-id="f60f9-205">shadow</span><span class="sxs-lookup"><span data-stu-id="f60f9-205">shadow</span></span>
* <span data-ttu-id="f60f9-206">src</span><span class="sxs-lookup"><span data-stu-id="f60f9-206">src</span></span>
* <span data-ttu-id="f60f9-207">ssh</span><span class="sxs-lookup"><span data-stu-id="f60f9-207">ssh</span></span>
* <span data-ttu-id="f60f9-208">sshd</span><span class="sxs-lookup"><span data-stu-id="f60f9-208">sshd</span></span>
* <span data-ttu-id="f60f9-209">staff</span><span class="sxs-lookup"><span data-stu-id="f60f9-209">staff</span></span>
* <span data-ttu-id="f60f9-210">sudo</span><span class="sxs-lookup"><span data-stu-id="f60f9-210">sudo</span></span>
* <span data-ttu-id="f60f9-211">sync</span><span class="sxs-lookup"><span data-stu-id="f60f9-211">sync</span></span>
* <span data-ttu-id="f60f9-212">sys</span><span class="sxs-lookup"><span data-stu-id="f60f9-212">sys</span></span>
* <span data-ttu-id="f60f9-213">syslog</span><span class="sxs-lookup"><span data-stu-id="f60f9-213">syslog</span></span>
* <span data-ttu-id="f60f9-214">tape</span><span class="sxs-lookup"><span data-stu-id="f60f9-214">tape</span></span>
* <span data-ttu-id="f60f9-215">tty</span><span class="sxs-lookup"><span data-stu-id="f60f9-215">tty</span></span>
* <span data-ttu-id="f60f9-216">users</span><span class="sxs-lookup"><span data-stu-id="f60f9-216">users</span></span>
* <span data-ttu-id="f60f9-217">utmp</span><span class="sxs-lookup"><span data-stu-id="f60f9-217">utmp</span></span>
* <span data-ttu-id="f60f9-218">uucp</span><span class="sxs-lookup"><span data-stu-id="f60f9-218">uucp</span></span>
* <span data-ttu-id="f60f9-219">video</span><span class="sxs-lookup"><span data-stu-id="f60f9-219">video</span></span>
* <span data-ttu-id="f60f9-220">voice</span><span class="sxs-lookup"><span data-stu-id="f60f9-220">voice</span></span>
* <span data-ttu-id="f60f9-221">whoopsie</span><span class="sxs-lookup"><span data-stu-id="f60f9-221">whoopsie</span></span>
* <span data-ttu-id="f60f9-222">www-data</span><span class="sxs-lookup"><span data-stu-id="f60f9-222">www-data</span></span>

