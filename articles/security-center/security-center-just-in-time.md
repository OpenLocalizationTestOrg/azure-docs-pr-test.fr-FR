---
title: "aaaJust dans la machine virtuelle de temps d’accès dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous guide comment juste-à-temps tooyour Azure d’accéder aux accès de machine virtuelle dans Azure Security Center vous permet de contrôler les ordinateurs virtuels."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: terrylan
ms.openlocfilehash: e6b58dd2c686cb227392b294e85914df5a546016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a><span data-ttu-id="d4713-103">Gérer l’accès Juste à temps à la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d4713-103">Manage virtual machine access using just in time</span></span>

<span data-ttu-id="d4713-104">Juste-à-temps virtual machine (VM) accès peut être utilisé toolock vers le bas le trafic entrant tooyour les machines virtuelles Azure, réduire l’exposition tooattacks tout en offrant un accès facile tooconnect tooVMs si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d4713-104">Just in time virtual machine (VM) access can be used toolock down inbound traffic tooyour Azure VMs, reducing exposure tooattacks while providing easy access tooconnect tooVMs when needed.</span></span>

> [!NOTE]
> <span data-ttu-id="d4713-105">Hello juste-à-temps est en version préliminaire et disponible sur hello niveau Standard de centre de sécurité.</span><span class="sxs-lookup"><span data-stu-id="d4713-105">hello just in time feature is in preview and available on hello Standard tier of Security Center.</span></span>  <span data-ttu-id="d4713-106">Consultez [tarification](security-center-pricing.md) niveaux de tarification du toolearn en savoir plus sur le centre de sécurité.</span><span class="sxs-lookup"><span data-stu-id="d4713-106">See [Pricing](security-center-pricing.md) toolearn more about Security Center's pricing tiers.</span></span>
>
>

## <a name="attack-scenario"></a><span data-ttu-id="d4713-107">Scénario d’attaque</span><span class="sxs-lookup"><span data-stu-id="d4713-107">Attack scenario</span></span>

<span data-ttu-id="d4713-108">Force brute des attaques généralement les ports de gestion cible comme un tooa d’accès signifie toogain machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d4713-108">Brute force attacks commonly target management ports as a means toogain access tooa VM.</span></span> <span data-ttu-id="d4713-109">En cas de réussite, un intrus peut prendre le contrôle hello VM et établir une brèche dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="d4713-109">If successful, an attacker can take control over hello VM and establish a foothold into your environment.</span></span>

<span data-ttu-id="d4713-110">Attaque en force brute de tooreduce monodirectionnelle exposition tooa est durée hello toolimit pendant laquelle un port est ouvert.</span><span class="sxs-lookup"><span data-stu-id="d4713-110">One way tooreduce exposure tooa brute force attack is toolimit hello amount of time that a port is open.</span></span> <span data-ttu-id="d4713-111">Les ports de gestion ne pas les ouvrir toobe besoin à tout moment.</span><span class="sxs-lookup"><span data-stu-id="d4713-111">Management ports do not need toobe open at all times.</span></span> <span data-ttu-id="d4713-112">Il leur suffit de toobe ouverte lorsque vous est connecté toohello machine virtuelle, par exemple tooperform tâches de maintenance ou de gestion.</span><span class="sxs-lookup"><span data-stu-id="d4713-112">They only need toobe open while you are connected toohello VM, for example tooperform management or maintenance tasks.</span></span> <span data-ttu-id="d4713-113">Lorsque juste-à-temps est activé, le centre de sécurité utilise [groupe de sécurité réseau](../virtual-network/virtual-networks-nsg.md) règles (NSG), qui restreignent l’accès toomanagement ports afin qu’ils ne peuvent pas être ciblés par les attaquants.</span><span class="sxs-lookup"><span data-stu-id="d4713-113">When just in time is enabled, Security Center uses [Network Security Group](../virtual-network/virtual-networks-nsg.md) (NSG) rules, which restrict access toomanagement ports so they cannot be targeted by attackers.</span></span>

![Scénario Juste à temps][1]

## <a name="how-does-just-in-time-access-work"></a><span data-ttu-id="d4713-115">Comment l’accès Juste à temps fonctionne-t-il ?</span><span class="sxs-lookup"><span data-stu-id="d4713-115">How does just in time access work?</span></span>

<span data-ttu-id="d4713-116">Lorsque juste-à-temps est activé, le centre de sécurité bloque le trafic entrant tooyour machines virtuelles Azure en créant une règle de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="d4713-116">When just in time is enabled, Security Center locks down inbound traffic tooyour Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="d4713-117">Vous sélectionnez les ports hello sur hello VM toowhich le trafic entrant sera verrouillé.</span><span class="sxs-lookup"><span data-stu-id="d4713-117">You select hello ports on hello VM toowhich inbound traffic will be locked down.</span></span> <span data-ttu-id="d4713-118">Ces ports sont contrôlées par hello juste-à-solution de temps.</span><span class="sxs-lookup"><span data-stu-id="d4713-118">These ports are controlled by hello just in time solution.</span></span>

<span data-ttu-id="d4713-119">Lorsqu’un utilisateur demande l’accès tooa machine virtuelle, le centre de sécurité vérifie que l’utilisateur hello a [contrôle d’accès en fonction du rôle (RBAC)](../active-directory/role-based-access-control-configure.md) autorisations qui fournissent un accès en écriture pour hello ressource Azure.</span><span class="sxs-lookup"><span data-stu-id="d4713-119">When a user requests access tooa VM, Security Center checks that hello user has [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) permissions that provide write access for hello Azure resource.</span></span> <span data-ttu-id="d4713-120">Si elles ont des autorisations en écriture, hello demande est approuvée et centre de sécurité configure automatiquement les groupes de sécurité réseau (NSG) hello tooallow entrant ports de gestion du trafic toohello pour durée hello spécifié.</span><span class="sxs-lookup"><span data-stu-id="d4713-120">If they have write permissions, hello request is approved and Security Center automatically configures hello Network Security Groups (NSGs) tooallow inbound traffic toohello management ports for hello amount of time you specified.</span></span> <span data-ttu-id="d4713-121">Une fois hello délai expiré, centre de sécurité restaure États précédents de hello NSG tootheir.</span><span class="sxs-lookup"><span data-stu-id="d4713-121">After hello time has expired, Security Center restores hello NSGs tootheir previous states.</span></span>

> [!NOTE]
> <span data-ttu-id="d4713-122">L’accès Juste à temps à la machine virtuelle Security Center prend en charge uniquement les machines virtuelles déployées par le biais d’Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d4713-122">Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="d4713-123">toolearn d’informations sur hello classique et les modèles de déploiement Resource Manager, consultez [Azure Resource Manager et déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d4713-123">toolearn more about hello classic and Resource Manager deployment models see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
>
>

## <a name="using-just-in-time-access"></a><span data-ttu-id="d4713-124">Utilisation de l’accès Juste à temps</span><span class="sxs-lookup"><span data-stu-id="d4713-124">Using just in time access</span></span>

<span data-ttu-id="d4713-125">Hello **juste à l’accès des ordinateurs virtuels de temps** vignette sur hello **centre de sécurité** panneau montre le nombre hello de machines virtuelles configurées pour juste-à-temps accès et hello le numéro approuvées de demandes d’accès effectuées Bonjour la semaine dernière.</span><span class="sxs-lookup"><span data-stu-id="d4713-125">hello **Just in time VM access** tile on hello **Security Center** blade shows hello number of VMs configured for just in time access and hello number of approved access requests made in hello last week.</span></span>

<span data-ttu-id="d4713-126">Sélectionnez hello **juste à l’accès des ordinateurs virtuels de temps** vignette et hello **juste à l’accès des ordinateurs virtuels de temps** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="d4713-126">Select hello **Just in time VM access** tile and hello **Just in time VM access** blade opens.</span></span>

![Vignette Accès Juste à temps à la machine virtuelle][2]

<span data-ttu-id="d4713-128">Hello **juste à l’accès des ordinateurs virtuels de temps** panneau fournit des informations sur l’état de vos machines virtuelles hello :</span><span class="sxs-lookup"><span data-stu-id="d4713-128">hello **Just in time VM access** blade provides information on hello state of your VMs:</span></span>

- <span data-ttu-id="d4713-129">**Configuré** -les ordinateurs virtuels qui ont été configuré toosupport juste-à-accès des ordinateurs virtuels de temps.</span><span class="sxs-lookup"><span data-stu-id="d4713-129">**Configured** - VMs that have been configured toosupport just in time VM access.</span></span> <span data-ttu-id="d4713-130">données Hello présentées sont pourquoi la semaine dernière et inclut pour chaque numéro de hello de machine virtuelle de demandes approuvées, date du dernier accès et l’heure et dernier utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d4713-130">hello data presented is for hello last week and includes for each VM hello number of approved requests, last access date and time, and last user.</span></span>
- <span data-ttu-id="d4713-131">**Recommandé** : machines virtuelles qui peuvent prendre en charge l’accès Juste à temps à la machine virtuelle, mais n’ont pas été configurées dans cette optique.</span><span class="sxs-lookup"><span data-stu-id="d4713-131">**Recommended** - VMs that can support just in time VM access but have not been configured to.</span></span> <span data-ttu-id="d4713-132">Nous vous recommandons d’activer le contrôle d’accès Juste à temps à la machine virtuelle pour ces machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="d4713-132">We recommend that you enable just in time VM access control for these VMs.</span></span> <span data-ttu-id="d4713-133">Consultez [Activer l’accès Juste à temps à la machine virtuelle](#enable-just-in-time-vm-access).</span><span class="sxs-lookup"><span data-stu-id="d4713-133">See [Enable just in time VM access](#enable-just-in-time-vm-access).</span></span>
- <span data-ttu-id="d4713-134">**Aucune recommandation** -raisons qui peuvent provoquer une machine virtuelle pas les toobe recommandé sont :</span><span class="sxs-lookup"><span data-stu-id="d4713-134">**No recommendation** - Reasons that can cause a VM not toobe recommended are:</span></span>
  - <span data-ttu-id="d4713-135">Manquant NSG - hello juste-à-solution de temps nécessite une toobe de groupe de sécurité réseau en place.</span><span class="sxs-lookup"><span data-stu-id="d4713-135">Missing NSG - hello just in time solution requires an NSG toobe in place.</span></span>
  - <span data-ttu-id="d4713-136">Machine virtuelle classique : l’accès Juste à temps à la machine virtuelle Security Center prend en charge uniquement les machines virtuelles déployées par le biais d’Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d4713-136">Classic VM - Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="d4713-137">Un déploiement classique n’est pas pris en charge par hello juste-à-solution de temps.</span><span class="sxs-lookup"><span data-stu-id="d4713-137">A classic deployment is not supported by hello just in time solution.</span></span>
  - <span data-ttu-id="d4713-138">Autre - une machine virtuelle est dans cette catégorie si hello juste-à-temps solution est désactivée dans la stratégie de sécurité hello d’abonnement de hello ou un groupe de ressources hello ou cette machine virtuelle hello est manquant pour une adresse IP publique et n’a pas un groupe de sécurité réseau en place.</span><span class="sxs-lookup"><span data-stu-id="d4713-138">Other - A VM is in this category if hello just in time solution is turned off in hello security policy of hello subscription or hello resource group, or that hello VM is missing a public IP and doesn't have an NSG in place.</span></span>

## <a name="configuring-a-just-in-time-access-policy"></a><span data-ttu-id="d4713-139">Configuration d’une stratégie d’accès Juste à temps</span><span class="sxs-lookup"><span data-stu-id="d4713-139">Configuring a just in time access policy</span></span>

<span data-ttu-id="d4713-140">hello tooselect machines virtuelles que vous souhaitez tooenable :</span><span class="sxs-lookup"><span data-stu-id="d4713-140">tooselect hello VMs that you want tooenable:</span></span>

1. <span data-ttu-id="d4713-141">Sur hello **juste à l’accès des ordinateurs virtuels de temps** panneau, sélectionnez hello **recommandé** onglet.</span><span class="sxs-lookup"><span data-stu-id="d4713-141">On hello **Just in time VM access** blade, select hello **Recommended** tab.</span></span>

  ![Activer l’accès Juste à temps à la machine virtuelle][3]

2. <span data-ttu-id="d4713-143">Sous **machines virtuelles**, sélectionnez les machines virtuelles de hello que vous souhaitez tooenable.</span><span class="sxs-lookup"><span data-stu-id="d4713-143">Under **VMs**, select hello VMs that you want tooenable.</span></span> <span data-ttu-id="d4713-144">Cela permet de placer un ordinateur virtuel de tooa suivant coche.</span><span class="sxs-lookup"><span data-stu-id="d4713-144">This puts a checkmark next tooa VM.</span></span>
3. <span data-ttu-id="d4713-145">Sélectionnez **Enable JIT on VMs** (Activer JIT sur les machines virtuelles).</span><span class="sxs-lookup"><span data-stu-id="d4713-145">Select **Enable JIT on VMs**.</span></span>
4. <span data-ttu-id="d4713-146">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d4713-146">Select **Save**.</span></span>

### <a name="default-ports"></a><span data-ttu-id="d4713-147">Ports par défaut</span><span class="sxs-lookup"><span data-stu-id="d4713-147">Default ports</span></span>

<span data-ttu-id="d4713-148">Vous pouvez voir des ports par défaut hello centre de sécurité recommande l’activation juste-à-temps.</span><span class="sxs-lookup"><span data-stu-id="d4713-148">You can see hello default ports that Security Center recommends enabling just in time.</span></span>

1. <span data-ttu-id="d4713-149">Sur hello **juste à l’accès des ordinateurs virtuels de temps** panneau, sélectionnez hello **recommandé** onglet.</span><span class="sxs-lookup"><span data-stu-id="d4713-149">On hello **Just in time VM access** blade, select hello **Recommended** tab.</span></span>

  ![Afficher les ports par défaut][6]

2. <span data-ttu-id="d4713-151">Sous **Machines virtuelles**, sélectionnez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d4713-151">Under **VMs**, select a VM.</span></span> <span data-ttu-id="d4713-152">Cela permet de placer une coche suivant toohello VM et ouvre hello **configuration de l’accès JIT VM** panneau.</span><span class="sxs-lookup"><span data-stu-id="d4713-152">This puts a checkmark next toohello VM and opens hello **JIT VM access configuration** blade.</span></span> <span data-ttu-id="d4713-153">Ce panneau affiche les ports par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="d4713-153">This blade displays hello default ports.</span></span>

### <a name="add-ports"></a><span data-ttu-id="d4713-154">Ajouter des ports</span><span class="sxs-lookup"><span data-stu-id="d4713-154">Add ports</span></span>

<span data-ttu-id="d4713-155">À partir de hello **configuration de l’accès JIT VM** panneau, vous pouvez également ajouter et configurer un nouveau port sur lequel vous souhaitez hello tooenable juste-à-solution de temps.</span><span class="sxs-lookup"><span data-stu-id="d4713-155">From hello **JIT VM access configuration** blade, you can also add and configure a new port on which you want tooenable hello just in time solution.</span></span>

1. <span data-ttu-id="d4713-156">Sur hello **configuration de l’accès JIT VM** panneau, sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d4713-156">On hello **JIT VM access configuration** blade, select **Add**.</span></span> <span data-ttu-id="d4713-157">Cette opération ouvre hello **configuration du port ajouter** panneau.</span><span class="sxs-lookup"><span data-stu-id="d4713-157">This opens hello **Add port configuration** blade.</span></span>

  ![Configuration du port][7]

2. <span data-ttu-id="d4713-159">Sur **configuration du port ajouter** panneau, vous identifiez port hello, type de protocole, autorisé des adresses IP source et au maximum le temps de demande.</span><span class="sxs-lookup"><span data-stu-id="d4713-159">On **Add port configuration** blade, you identify hello port, protocol type, allowed source IPs, and maximum request time.</span></span>

  <span data-ttu-id="d4713-160">Autorisé des adresses IP source est hello IP plages tooget autorisées sur une demande approuvée.</span><span class="sxs-lookup"><span data-stu-id="d4713-160">Allowed source IPs are hello IP ranges allowed tooget access upon an approved request.</span></span>

  <span data-ttu-id="d4713-161">Durée maximale de la demande est la fenêtre de temps maximal hello ouverture d’un port spécifique.</span><span class="sxs-lookup"><span data-stu-id="d4713-161">Maximum request time is hello maximum time window that a specific port can be opened.</span></span>

3. <span data-ttu-id="d4713-162">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="d4713-162">Select **OK**.</span></span>

## <a name="requesting-access-tooa-vm"></a><span data-ttu-id="d4713-163">Demande d’accès tooa machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d4713-163">Requesting access tooa VM</span></span>

<span data-ttu-id="d4713-164">toorequest tooa d’accès aux ordinateurs virtuels :</span><span class="sxs-lookup"><span data-stu-id="d4713-164">toorequest access tooa VM:</span></span>

1. <span data-ttu-id="d4713-165">Sur hello **juste à l’accès des ordinateurs virtuels de temps** panneau, sélectionnez hello **configuré** onglet.</span><span class="sxs-lookup"><span data-stu-id="d4713-165">On hello **Just in time VM access** blade, select hello **Configured** tab.</span></span>
2. <span data-ttu-id="d4713-166">Sous **machines virtuelles**, sélectionnez les machines virtuelles de hello que vous souhaitez tooenable accès.</span><span class="sxs-lookup"><span data-stu-id="d4713-166">Under **VMs**, select hello VMs that you want tooenable access.</span></span> <span data-ttu-id="d4713-167">Cela permet de placer un ordinateur virtuel de tooa suivant coche.</span><span class="sxs-lookup"><span data-stu-id="d4713-167">This puts a checkmark next tooa VM.</span></span>
3. <span data-ttu-id="d4713-168">Sélectionnez **Demander l’accès**.</span><span class="sxs-lookup"><span data-stu-id="d4713-168">Select **Request access**.</span></span> <span data-ttu-id="d4713-169">Cette opération ouvre hello **demander l’accès** panneau.</span><span class="sxs-lookup"><span data-stu-id="d4713-169">This opens hello **Request access** blade.</span></span>

  ![Demande l’accès tooa machine virtuelle][4]

4. <span data-ttu-id="d4713-171">Sur hello **demander l’accès** panneau, que vous configurez pour chaque tooopen de ports hello machine virtuelle, ainsi que l’adresse IP source hello hello port est ouvert la fenêtre de temps tooand hello pour le hello port est ouvert.</span><span class="sxs-lookup"><span data-stu-id="d4713-171">On hello **Request access** blade, you configure for each VM hello ports tooopen along with hello source IP that hello port is opened tooand hello time window for which hello port is opened.</span></span> <span data-ttu-id="d4713-172">Vous pouvez demander des ports toohello uniquement d’accès qui sont configurés dans hello simplement dans la stratégie.</span><span class="sxs-lookup"><span data-stu-id="d4713-172">You can request access only toohello ports that are configured in hello just in time policy.</span></span> <span data-ttu-id="d4713-173">Chaque port a une durée maximale autorisée dérivée hello simplement dans la stratégie.</span><span class="sxs-lookup"><span data-stu-id="d4713-173">Each port has a maximum allowed time derived from hello just in time policy.</span></span>
5. <span data-ttu-id="d4713-174">Sélectionnez **Ports ouverts**.</span><span class="sxs-lookup"><span data-stu-id="d4713-174">Select **Open ports**.</span></span>

## <a name="editing-a-just-in-time-access-policy"></a><span data-ttu-id="d4713-175">Modification d’une stratégie d’accès Juste à temps</span><span class="sxs-lookup"><span data-stu-id="d4713-175">Editing a just in time access policy</span></span>

<span data-ttu-id="d4713-176">Vous pouvez modifier l’ordinateur virtuel existant juste-à-stratégie par ajout et configuration d’un nouveau tooopen de port pour cette machine virtuelle, ou en modifiant un autre paramètre tooan connexe déjà protégé port.</span><span class="sxs-lookup"><span data-stu-id="d4713-176">You can change a VM's existing just in time policy by adding and configuring a new port tooopen for that VM, or by changing any other parameter related tooan already protected port.</span></span>

<span data-ttu-id="d4713-177">Dans commande tooedit existant juste-à-stratégie d’une machine virtuelle, hello **configuré** onglet est utilisé :</span><span class="sxs-lookup"><span data-stu-id="d4713-177">In order tooedit an existing just in time policy of a VM, hello **Configured** tab is used:</span></span>

1. <span data-ttu-id="d4713-178">Sous **machines virtuelles**, sélectionnez une machine virtuelle tooadd un tooby de port sur les points de hello trois au sein de la ligne de hello pour cette machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d4713-178">Under **VMs**, select a VM tooadd a port tooby clicking on hello three dots within hello row for that VM.</span></span> <span data-ttu-id="d4713-179">Un menu s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="d4713-179">This opens a menu.</span></span>
2. <span data-ttu-id="d4713-180">Sélectionnez **modifier** dans le menu de hello.</span><span class="sxs-lookup"><span data-stu-id="d4713-180">Select **Edit** in hello menu.</span></span> <span data-ttu-id="d4713-181">Cette opération ouvre hello **configuration de l’accès JIT VM** panneau.</span><span class="sxs-lookup"><span data-stu-id="d4713-181">This opens hello **JIT VM access configuration** blade.</span></span>

  ![Modifier la stratégie][8]

3. <span data-ttu-id="d4713-183">Sur hello **configuration de l’accès JIT VM** panneau, vous pouvez modifier les paramètres existants hello d’un port déjà protégé en cliquant sur son port ou vous pouvez sélectionner **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d4713-183">On hello **JIT VM access configuration** blade, you can either edit hello existing settings of an already protected port by clicking on its port, or you can select **Add**.</span></span> <span data-ttu-id="d4713-184">Cette opération ouvre hello **configuration du port ajouter** panneau.</span><span class="sxs-lookup"><span data-stu-id="d4713-184">This opens hello **Add port configuration** blade.</span></span>

  ![Ajouter un port][7]

4. <span data-ttu-id="d4713-186">Sur **configuration du port ajouter** panneau identifier le port de hello, type de protocole, des adresses IP sources autorisées et durée maximale de la demande.</span><span class="sxs-lookup"><span data-stu-id="d4713-186">On **Add port configuration** blade identify hello port, protocol type, allowed source IPs, and maximum request time.</span></span>
5. <span data-ttu-id="d4713-187">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="d4713-187">Select **OK**.</span></span>
6. <span data-ttu-id="d4713-188">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d4713-188">Select **Save**.</span></span>

## <a name="auditing-just-in-time-access-activity"></a><span data-ttu-id="d4713-189">Audit de l’activité d’accès Juste à temps</span><span class="sxs-lookup"><span data-stu-id="d4713-189">Auditing just in time access activity</span></span>

<span data-ttu-id="d4713-190">Vous pouvez obtenir des informations sur les activités des machines virtuelles à l’aide de la recherche dans les journaux.</span><span class="sxs-lookup"><span data-stu-id="d4713-190">You can gain insights into VM activities using log search.</span></span> <span data-ttu-id="d4713-191">journaux de tooview :</span><span class="sxs-lookup"><span data-stu-id="d4713-191">tooview logs:</span></span>

1. <span data-ttu-id="d4713-192">Sur hello **juste à l’accès des ordinateurs virtuels de temps** panneau, sélectionnez hello **configuré** onglet.</span><span class="sxs-lookup"><span data-stu-id="d4713-192">On hello **Just in time VM access** blade, select hello **Configured** tab.</span></span>
2. <span data-ttu-id="d4713-193">Sous **machines virtuelles**, sélectionnez une informations tooview de machine virtuelle sur en cliquant sur les points de hello trois au sein de la ligne de hello pour cette machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d4713-193">Under **VMs**, select a VM tooview information about by clicking on hello three dots within hello row for that VM.</span></span> <span data-ttu-id="d4713-194">Un menu s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="d4713-194">This opens a menu.</span></span>
3. <span data-ttu-id="d4713-195">Sélectionnez **le journal d’activité** dans le menu de hello.</span><span class="sxs-lookup"><span data-stu-id="d4713-195">Select **Activity Log** in hello menu.</span></span> <span data-ttu-id="d4713-196">Cette opération ouvre hello **le journal d’activité** panneau.</span><span class="sxs-lookup"><span data-stu-id="d4713-196">This opens hello **Activity log** blade.</span></span>

![Sélectionner un journal d’activité][9]

<span data-ttu-id="d4713-198">Hello **le journal d’activité** panneau fournit une vue filtrée des opérations précédentes pour cette machine virtuelle, ainsi que l’abonnement, date et l’heure.</span><span class="sxs-lookup"><span data-stu-id="d4713-198">hello **Activity log** blade provides a filtered view of previous operations for that VM along with time, date, and subscription.</span></span>

![Afficher le journal d’activité][5]

<span data-ttu-id="d4713-200">Vous pouvez télécharger les informations du journal hello en sélectionnant **cliquez ici tous les éléments hello de type toodownload en tant que volume partagé de cluster**.</span><span class="sxs-lookup"><span data-stu-id="d4713-200">You can download hello log information by selecting **Click here toodownload all hello items as CSV**.</span></span>

<span data-ttu-id="d4713-201">Modifier les filtres de hello et sélectionnez **appliquer** toocreate une recherche et un journal.</span><span class="sxs-lookup"><span data-stu-id="d4713-201">Modify hello filters and select **Apply** toocreate a search and log.</span></span>

## <a name="using-just-in-time-vm-access-via-powershell"></a><span data-ttu-id="d4713-202">Utilisation de l’accès Juste à temps à la machine virtuelle par le biais de PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4713-202">Using just in time VM access via PowerShell</span></span>

<span data-ttu-id="d4713-203">Bonjour toouse de commande juste-à-solution de temps via PowerShell, assurez-vous que vous avez hello [dernière](/powershell/azure/install-azurerm-ps) Azure PowerShell version.</span><span class="sxs-lookup"><span data-stu-id="d4713-203">In order toouse hello just in time solution via PowerShell, make sure you have hello [latest](/powershell/azure/install-azurerm-ps) Azure PowerShell version.</span></span>
<span data-ttu-id="d4713-204">Une fois que vous le faites, vous devez tooinstall hello [dernière](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Security Center à partir de la galerie de PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="d4713-204">Once you do, you need tooinstall hello [latest](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Security Center from hello PowerShell gallery.</span></span>

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a><span data-ttu-id="d4713-205">Configuration d’une stratégie Juste à temps pour une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d4713-205">Configuring a just in time policy for a VM</span></span>

<span data-ttu-id="d4713-206">tooconfigure seulement dans la stratégie sur un ordinateur virtuel spécifique, vous devez toorun cette commande dans votre session PowerShell : Set-ASCJITAccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="d4713-206">tooconfigure a just in time policy on a specific VM, you need toorun this command in your PowerShell session: Set-ASCJITAccessPolicy.</span></span>
<span data-ttu-id="d4713-207">Suivez hello applet de commande documentation toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="d4713-207">Follow hello cmdlet documentation toolearn more.</span></span>

### <a name="requesting-access-tooa-vm"></a><span data-ttu-id="d4713-208">Demande d’accès tooa machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d4713-208">Requesting access tooa VM</span></span>

<span data-ttu-id="d4713-209">tooaccess un ordinateur virtuel spécifique qui est protégé par Bonjour juste-à-solution de temps, vous devez toorun cette commande dans votre session PowerShell : ASCJITAccess appeler.</span><span class="sxs-lookup"><span data-stu-id="d4713-209">tooaccess a specific VM that is protected with hello just in time solution, you need toorun this command in your PowerShell session: Invoke-ASCJITAccess.</span></span>
<span data-ttu-id="d4713-210">Suivez hello applet de commande documentation toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="d4713-210">Follow hello cmdlet documentation toolearn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4713-211">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d4713-211">Next steps</span></span>
<span data-ttu-id="d4713-212">Dans cet article, vous avez appris comment juste à temps accès machine virtuelle dans le centre de sécurité permet de contrôler l’accès tooyour Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="d4713-212">In this article, you learned how just in time VM access in Security Center helps you control access tooyour Azure virtual machines.</span></span>

<span data-ttu-id="d4713-213">toolearn en savoir plus sur le centre de sécurité, voir hello :</span><span class="sxs-lookup"><span data-stu-id="d4713-213">toolearn more about Security Center, see hello following:</span></span>

- <span data-ttu-id="d4713-214">[Définition de stratégies de sécurité](security-center-policies.md) — Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="d4713-214">[Setting security policies](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
- <span data-ttu-id="d4713-215">[Gestion des recommandations de sécurité](security-center-recommendations.md) : découvrez la façon dont les recommandations peuvent vous aider à protéger vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="d4713-215">[Managing security recommendations](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
- <span data-ttu-id="d4713-216">[Contrôle d’intégrité de la sécurité](security-center-monitoring.md) — Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="d4713-216">[Security health monitoring](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
- <span data-ttu-id="d4713-217">[La gestion et de répondre toosecurity alertes](security-center-managing-and-responding-alerts.md) : en savoir comment les alertes toosecurity toomanage et y répondre.</span><span class="sxs-lookup"><span data-stu-id="d4713-217">[Managing and responding toosecurity alerts](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
- <span data-ttu-id="d4713-218">[Surveillance des solutions de partenaire](security-center-partner-solutions.md) — Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.</span><span class="sxs-lookup"><span data-stu-id="d4713-218">[Monitoring partner solutions](security-center-partner-solutions.md) — Learn how toomonitor hello health status of your partner solutions.</span></span>
- <span data-ttu-id="d4713-219">[Forum aux questions du centre de sécurité](security-center-faq.md) : Forum aux questions sur l’utilisation hello service de recherche.</span><span class="sxs-lookup"><span data-stu-id="d4713-219">[Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
- <span data-ttu-id="d4713-220">[Blog sur la sécurité Azure](https://blogs.msdn.microsoft.com/azuresecurity/) : accédez à des billets de blog sur la sécurité et la conformité Azure.</span><span class="sxs-lookup"><span data-stu-id="d4713-220">[Azure Security blog](https://blogs.msdn.microsoft.com/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>


<!--Image references-->
[1]: ./media/security-center-just-in-time/just-in-time-scenario.png
[2]: ./media/security-center-just-in-time/just-in-time.png
[3]: ./media/security-center-just-in-time/enable-just-in-time-access.png
[4]: ./media/security-center-just-in-time/request-access-to-a-vm.png
[5]: ./media/security-center-just-in-time/activity-log.png
[6]: ./media/security-center-just-in-time/default-ports.png
[7]: ./media/security-center-just-in-time/add-a-port.png
[8]: ./media/security-center-just-in-time/edit-policy.png
[9]: ./media/security-center-just-in-time/select-activity-log.png
