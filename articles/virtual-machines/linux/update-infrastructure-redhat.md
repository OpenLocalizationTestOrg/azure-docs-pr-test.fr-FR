---
title: "aaaRed Infrastructure de mise à jour du fonctionnement (RHUI) | Documents Microsoft"
description: "Découvrez l’infrastructure RHUI (Red Hat Update Infrastructure) pour les instances Red Hat Enterprise Linux à la demande dans Microsoft Azure"
services: virtual-machines-linux
documentationcenter: 
author: BorisB2015
manager: timlt
editor: 
ms.assetid: f495f1b4-ae24-46b9-8d26-c617ce3daf3a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/13/2017
ms.author: borisb
ms.openlocfilehash: cc244857104b25e4e61862c518db77e915e137ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a><span data-ttu-id="b224e-103">Infrastructure RHUI (Red Hat Update Infrastructure) pour machines virtuelles Red Hat Enterprise Linux à la demande dans Azure</span><span class="sxs-lookup"><span data-stu-id="b224e-103">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>
<span data-ttu-id="b224e-104">Machines virtuelles créées à partir de hello sur demande Red Hat Enterprise Linux (RHEL) images disponibles dans Azure Marketplace sont inscrits tooaccess hello Red Hat mise à jour Infrastructure (RHUI) est déployé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b224e-104">Virtual machines created from hello on-demand Red Hat Enterprise Linux (RHEL) images available in Azure Marketplace are registered tooaccess hello Red Hat Update Infrastructure (RHUI) deployed in Azure.</span></span>  <span data-ttu-id="b224e-105">les instances RHEL de demande Hello ont référentiel d’yum régionaux accès tooa et tooreceive en mesure des mises à jour incrémentielles.</span><span class="sxs-lookup"><span data-stu-id="b224e-105">hello on-demand RHEL instances have access tooa regional yum repository and able tooreceive incremental updates.</span></span>

<span data-ttu-id="b224e-106">liste des référentiels yum Hello, qui est gérée par RHUI, est configurée dans votre instance RHEL lors de la configuration.</span><span class="sxs-lookup"><span data-stu-id="b224e-106">hello yum repository list, which is managed by RHUI, is configured in your RHEL instance during provisioning.</span></span> <span data-ttu-id="b224e-107">Vous n’avez pas besoin toodo aucune configuration supplémentaire - exécuter `yum update` une fois votre instance RHEL dernières mises à jour tooget prêt hello.</span><span class="sxs-lookup"><span data-stu-id="b224e-107">You don't need toodo any additional configuration - run `yum update` after your RHEL instance is ready tooget hello latest updates.</span></span>

> [!NOTE]
> <span data-ttu-id="b224e-108">En septembre 2016, nous avons déployé une mise à jour RHUI d’Azure et en janvier 2017, nous avons commencé l’arrêt en plusieurs phases de hello plus anciens RHUI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="b224e-108">In September 2016 we deployed an updated Azure RHUI and in January 2017 we started phased shutdown of hello older Azure RHUI.</span></span> <span data-ttu-id="b224e-109">Si vous avez utilisé les images RHEL hello (ou leurs instantanés) à partir de septembre 2016 ou version ultérieure - probablement aucune action n’est requise.</span><span class="sxs-lookup"><span data-stu-id="b224e-109">If you have been using hello RHEL images (or their snapshots) from September 2016 or later - likely no action is required.</span></span> <span data-ttu-id="b224e-110">Si, toutefois, vous devez les anciens instantanés/VMs, leur configuration doit toobe mis à jour pour un accès ininterrompu toohello RHUI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="b224e-110">If, however, you have older snapshots/VMs, their configuration needs toobe updated for uninterrupted access toohello Azure RHUI.</span></span>
> 

## <a name="rhui-azure-infrastructure-update"></a><span data-ttu-id="b224e-111">Mise à jour de l’infrastructure RHUI Azure</span><span class="sxs-lookup"><span data-stu-id="b224e-111">RHUI Azure Infrastructure Update</span></span>
<span data-ttu-id="b224e-112">Depuis septembre 2016, Azure propose un nouvel ensemble de serveurs d’infrastructure de mise à jour de Red Hat (RHUI).</span><span class="sxs-lookup"><span data-stu-id="b224e-112">As of September 2016, Azure has a new set of Red Hat Update Infrastructure (RHUI) servers.</span></span> <span data-ttu-id="b224e-113">Ces serveurs sont déployés avec [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) de sorte qu’un simple point de terminaison (rhui-1.micrsoft.com) peut être utilisé par n’importe quelle machine virtuelle, quelle que soit la région.</span><span class="sxs-lookup"><span data-stu-id="b224e-113">These servers are deployed with [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) so that a single endpoint (rhui-1.microsoft.com) can be used by any VM regardless of region.</span></span> <span data-ttu-id="b224e-114">Hello nouvelles images de RHEL paiement à l’utilisation (retenues à la source) dans les nouveaux serveurs Azure RHUI de point toohello hello Azure Marketplace (versions datées de septembre 2016 ou version ultérieures) et ne nécessitent pas d’action supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="b224e-114">hello new RHEL Pay-As-You-Go (PAYG) images in hello Azure Marketplace (versions dated September 2016 or later) point toohello new Azure RHUI servers and do not require any additional action.</span></span>

### <a name="determine-if-action-is-required"></a><span data-ttu-id="b224e-115">Déterminer si une action est requise</span><span class="sxs-lookup"><span data-stu-id="b224e-115">Determine if action is required</span></span>
<span data-ttu-id="b224e-116">Si vous rencontrez des problèmes de connexion tooAzure RHUI à partir de votre machine virtuelle de Azure RHEL retenues à la source, procédez comme suit</span><span class="sxs-lookup"><span data-stu-id="b224e-116">If you are experiencing problems connecting tooAzure RHUI from your Azure RHEL PAYG VM, follow these steps</span></span>
1. <span data-ttu-id="b224e-117">Examen de la configuration de machine virtuelle pour le point de terminaison RHUI Azure</span><span class="sxs-lookup"><span data-stu-id="b224e-117">Inspect VM configuration for Azure RHUI endpoint</span></span>

    <span data-ttu-id="b224e-118">Vérifiez si `/etc/yum.repos.d/rh-cloud.repo` fichier contient également les référence`rhui-[1-3].microsoft.com` dans baseurl de `[rhui-microsoft-azure-rhel*]` section du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="b224e-118">Check if `/etc/yum.repos.d/rh-cloud.repo` file contains reference too`rhui-[1-3].microsoft.com` in baseurl of `[rhui-microsoft-azure-rhel*]` section of hello file.</span></span> <span data-ttu-id="b224e-119">Si elle est, vous utilisez hello nouvelle RHUI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="b224e-119">If it is - you are using hello new Azure RHUI.</span></span>

    <span data-ttu-id="b224e-120">Si pointant tooa emplacement avec hello modèle `mirrorlist.*cds[1-4].cloudapp.net` -mise à jour de la configuration hello est requis.</span><span class="sxs-lookup"><span data-stu-id="b224e-120">If it pointing tooa location with hello following pattern `mirrorlist.*cds[1-4].cloudapp.net` - hello configuration update is required.</span></span>

    <span data-ttu-id="b224e-121">Si vous utilisez la nouvelle configuration de hello et toujours pas vous connecter tooAzure RHUI - fichier un cas de prise en charge par Microsoft ou Red Hat.</span><span class="sxs-lookup"><span data-stu-id="b224e-121">If you are using hello new configuration and still cannot connect tooAzure RHUI - file a support case with Microsoft or Red Hat.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b224e-122">RHUI tooAzure hébergé d’accès est machines virtuelles de toohello limité dans [plages d’adresses IP de centre de données Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="b224e-122">Access tooAzure-hosted RHUI is limited toohello VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
    > 

2. <span data-ttu-id="b224e-123">Si hello ancien Azure RHUI est toujours disponible lorsque vous effectuez cette vérification et vous souhaitez que la configuration de hello tooautomatically mise à jour, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b224e-123">If hello old Azure RHUI is still available when you do this check and you would like tooautomatically update hello configuration, execute hello following command:</span></span>

    <span data-ttu-id="b224e-124">`sudo yum update RHEL6`ou `sudo yum update RHEL7` en fonction de la version de famille RHEL hello.</span><span class="sxs-lookup"><span data-stu-id="b224e-124">`sudo yum update RHEL6` or `sudo yum update RHEL7` depending on hello RHEL family version.</span></span>

3. <span data-ttu-id="b224e-125">Si vous pouvez connecter n’est plus toohello ancien RHUI d’Azure, suivez hello manuelles décrites dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="b224e-125">If you can no longer connect toohello old Azure RHUI, follow hello manual steps described in hello next section.</span></span>

4. <span data-ttu-id="b224e-126">Assurez-vous que la configuration hello tooupdate hello source image/capture instantanée affectées de machine virtuelle a été configuré à partir de.</span><span class="sxs-lookup"><span data-stu-id="b224e-126">Make sure tooupdate hello configuration on hello source image/snapshot affected VM was provisioned from.</span></span>

### <a name="phased-shutdown-of-hello-old-azure-rhui"></a><span data-ttu-id="b224e-127">Arrêt en plusieurs phases de hello ancien Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="b224e-127">Phased shutdown of hello old Azure RHUI</span></span>
<span data-ttu-id="b224e-128">Lors de l’arrêt de hello Hello ancien RHUI Azure nous restreindre accéder aux tooit comme suit :</span><span class="sxs-lookup"><span data-stu-id="b224e-128">During hello shutdown of hello old Azure RHUI we restrict access tooit as follows:</span></span>

1. <span data-ttu-id="b224e-129">Restreindre davantage le tooset d’accès (ACL) des adresses IP qui sont déjà connectés tooit.</span><span class="sxs-lookup"><span data-stu-id="b224e-129">Further restrict access (ACL) tooset of IP addresses that are already connecting tooit.</span></span> <span data-ttu-id="b224e-130">Effets possibles : Si vous continuez à l’aide de hello ancien Azure RHUI - vos nouvelles machines virtuelles ne peuvent pas être en mesure de tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="b224e-130">Possible side-effects: if you continue using hello old Azure RHUI - your new VMs may not be able tooconnect tooit.</span></span> <span data-ttu-id="b224e-131">RHEL machines virtuelles avec des adresses IP dynamiques séquence d’arrêt/libérer/start reçoive la nouvelle adresse IP et donc également pu échouent tooconnect toohello ancien Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="b224e-131">RHEL VMs with dynamic IPs that go through shutdown/deallocate/start sequence may receive new IP and hence also could start failing tooconnect toohello old Azure RHUI</span></span>

2. <span data-ttu-id="b224e-132">Arrêtez les serveurs de distribution du contenu de mise en miroir.</span><span class="sxs-lookup"><span data-stu-id="b224e-132">Shutdown of mirror content delivery servers.</span></span> <span data-ttu-id="b224e-133">Effets possibles : comme nous arrêter CDSes plus vous pouvez voir plus `yum update` la maintenance de temps, les délais d’attente plus jusqu’au hello point lorsque vous pourrez ne plus se connecter toohello ancien RHUI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="b224e-133">Possible side-effects: as we shut down more CDSes you may see longer `yum update` servicing time, more timeouts up until hello point when you can no longer connect toohello old Azure RHUI.</span></span>

### <a name="hello-ips-for-hello-new-rhui-content-delivery-servers-are"></a><span data-ttu-id="b224e-134">Hello des adresses IP pour les nouveaux serveurs de diffusion de contenu RHUI hello sont</span><span class="sxs-lookup"><span data-stu-id="b224e-134">hello IPs for hello new RHUI content delivery servers are</span></span>
<span data-ttu-id="b224e-135">Si vous utilisez toofurther de configuration réseau restreindre l’accès à partir d’ordinateurs virtuels de RHEL retenues à la source, assurez-vous que hello suivant des adresses IP est autorisée pour `yum update` toowork en fonction de l’environnement hello dans.</span><span class="sxs-lookup"><span data-stu-id="b224e-135">If you are using network configuration toofurther restrict access from RHEL PAYG VMs, make sure hello following IPs are allowed for `yum update` toowork depending on hello environment you are in.</span></span> 

```
# Azure Global
13.91.47.76
40.85.190.91
52.187.75.218
52.174.163.213

# Azure US Government
13.72.186.193

# Azure Germany
51.5.243.77
51.4.228.145
```

### <a name="manual-update-procedure-toouse-hello-new-azure-rhui-servers"></a><span data-ttu-id="b224e-136">Mise à jour manuelle procédure toouse hello nouveaux Azure RHUI serveurs</span><span class="sxs-lookup"><span data-stu-id="b224e-136">Manual update procedure toouse hello new Azure RHUI servers</span></span>
<span data-ttu-id="b224e-137">Signature de clé publique de téléchargement (via curl) hello</span><span class="sxs-lookup"><span data-stu-id="b224e-137">Download (via curl) hello public key signature</span></span>

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

<span data-ttu-id="b224e-138">Vérifiez la clé de hello téléchargé</span><span class="sxs-lookup"><span data-stu-id="b224e-138">Verify hello downloaded key</span></span>

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="b224e-139">Vérifiez la sortie de hello, vérifiez les `keyid` et `user ID packet`:</span><span class="sxs-lookup"><span data-stu-id="b224e-139">Check hello output, verify `keyid` and `user ID packet`:</span></span>

```bash
Version: GnuPG v1.4.7 (GNU/Linux)
:public key packet:
        version 4, algo 1, created 1446074508, expires 0
        pkey[0]: [2048 bits]
        pkey[1]: [17 bits]
        keyid: EB3E94ADBE1229CF
:user ID packet: "Microsoft (Release signing) <gpgsecurity@microsoft.com>"
:signature packet: algo 1, keyid EB3E94ADBE1229CF
        version 4, created 1446074508, md5len 0, sigclass 0x13
        digest algo 2, begin of digest 1a 9b
        hashed subpkt 2 len 4 (sig created 2015-10-28)
        hashed subpkt 27 len 1 (key flags: 03)
        hashed subpkt 11 len 5 (pref-sym-algos: 9 8 7 3 2)
        hashed subpkt 21 len 3 (pref-hash-algos: 2 8 3)
        hashed subpkt 22 len 2 (pref-zip-algos: 2 1)
        hashed subpkt 30 len 1 (features: 01)
        hashed subpkt 23 len 1 (key server preferences: 80)
        subpkt 16 len 8 (issuer key ID EB3E94ADBE1229CF)
        data: [2047 bits]
```

<span data-ttu-id="b224e-140">Installer la clé publique de hello</span><span class="sxs-lookup"><span data-stu-id="b224e-140">Install hello public key</span></span>

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="b224e-141">Télécharger, vérifier et installer le package RPM Client</span><span class="sxs-lookup"><span data-stu-id="b224e-141">Download, Verify, and Install Client RPM</span></span>

<span data-ttu-id="b224e-142">Télécharger : pour RHEL 6</span><span class="sxs-lookup"><span data-stu-id="b224e-142">Download: For RHEL 6</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

<span data-ttu-id="b224e-143">pour RHEL 7</span><span class="sxs-lookup"><span data-stu-id="b224e-143">For RHEL 7</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

<span data-ttu-id="b224e-144">Vérifier :</span><span class="sxs-lookup"><span data-stu-id="b224e-144">Verify:</span></span>

```bash
rpm -Kv azureclient.rpm
```

<span data-ttu-id="b224e-145">Vérifiez dans la sortie de cette signature de hello package est OK</span><span class="sxs-lookup"><span data-stu-id="b224e-145">Check in output that signature of hello package is OK</span></span>

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

<span data-ttu-id="b224e-146">Installer hello tr/min</span><span class="sxs-lookup"><span data-stu-id="b224e-146">Install hello RPM</span></span>

```bash
sudo rpm -U azureclient.rpm
```

<span data-ttu-id="b224e-147">À la fin, vérifiez que vous avez accès hello du formulaire Azure RHUI machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="b224e-147">Upon completion, verify that you can access Azure RHUI form hello VM</span></span>

### <a name="all-in-one-script-for-automating-hello-preceding-task"></a><span data-ttu-id="b224e-148">Script tout-en-un pour l’automatisation hello précédant la tâche</span><span class="sxs-lookup"><span data-stu-id="b224e-148">All-in-one script for automating hello preceding task</span></span>
<span data-ttu-id="b224e-149">Utilisez hello script suivant en tant que tâche de hello tooautomate nécessaires de mise à jour des serveurs affectés Azure RHUI de nouveau toohello machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="b224e-149">Use hello following script as needed tooautomate hello task of updating affected VMs toohello new Azure RHUI servers.</span></span>

```sh
# Download key
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 

# Validate key
if ! gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release | grep -q "keyid: EB3E94ADBE1229CF"; then
    echo "Keyfile azure.asc NOT valid. Exiting."
    exit 1
fi

# Install Key
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release

# Download RPM package
if grep -q "release 7" /etc/redhat-release; then
    ver=7
elif  grep -q "release 6" /etc/redhat-release; then
    ver=6
else
    echo "Version not supported, exiting"
    exit 1
fi

url=https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel$ver/rhui-azure-rhel$ver-2.0-2.noarch.rpm
curl -o azureclient.rpm "$url"

# Verify package
if ! rpm -Kv azureclient.rpm | grep -q "key ID be1229cf: OK"; then
    echo "RPM failed validation ($url)"
    exit 1
fi

# Install package
sudo rpm -U azureclient.rpm
```

## <a name="rhui-overview"></a><span data-ttu-id="b224e-150">Vue d’ensemble de RHUI</span><span class="sxs-lookup"><span data-stu-id="b224e-150">RHUI overview</span></span>
<span data-ttu-id="b224e-151">[Infrastructure de mise à jour de Red Hat](https://access.redhat.com/products/red-hat-update-infrastructure) propose une solution hautement évolutive toomanage yum référentiel pour les instances de cloud de Red Hat Enterprise Linux qui sont hébergés par les fournisseurs de cloud de certifiés Red Hat.</span><span class="sxs-lookup"><span data-stu-id="b224e-151">[Red Hat Update Infrastructure](https://access.redhat.com/products/red-hat-update-infrastructure) offers a highly scalable solution toomanage yum repository content for Red Hat Enterprise Linux cloud instances that are hosted by Red Hat-certified cloud providers.</span></span> <span data-ttu-id="b224e-152">Selon le projet de pâtes hello en amont, RHUI permet aux fournisseurs cloud toolocally miroir hébergée de Red Hat du contenu de référentiel, créer des référentiels personnalisés avec leur propre contenu et rendre ces référentiels disponibles tooa grand groupe d’utilisateurs finaux via un équilibrage de la charge système de livraison de contenu.</span><span class="sxs-lookup"><span data-stu-id="b224e-152">Based on hello upstream Pulp project, RHUI allows cloud providers toolocally mirror Red Hat-hosted repository content, create custom repositories with their own content, and make those repositories available tooa large group of end users through a load-balanced content delivery system.</span></span>

## <a name="regions-where-rhui-is-available"></a><span data-ttu-id="b224e-153">Régions où RHUI est disponible</span><span class="sxs-lookup"><span data-stu-id="b224e-153">Regions where RHUI is available</span></span>
<span data-ttu-id="b224e-154">L’infrastructure RHUI est disponible dans toutes les régions où les images RHEL à la demande sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="b224e-154">RHUI is available in all regions where RHEL on-demand images are available.</span></span> <span data-ttu-id="b224e-155">Elle comprend actuellement publiques toutes les régions répertoriées sur hello [tableau de bord Azure status](https://azure.microsoft.com/status/) page, les régions Azure du gouvernement et Azure situés en Allemagne.</span><span class="sxs-lookup"><span data-stu-id="b224e-155">It currently includes all public regions listed on hello [Azure status dashboard](https://azure.microsoft.com/status/) page, Azure US Government and Azure Germany regions.</span></span> <span data-ttu-id="b224e-156">L’accès à l’infrastructure RHUI pour les machines virtuelles mises en service à partir d’images RHEL à la demande est inclus dans leur prix.</span><span class="sxs-lookup"><span data-stu-id="b224e-156">RHUI access for VMs provisioned from RHEL on-demand images is included in their price.</span></span> <span data-ttu-id="b224e-157">Disponibilité du cloud régionales et nationales supplémentaire sera mise à jour en disponibilité à la demande RHEL Bonjour futures.</span><span class="sxs-lookup"><span data-stu-id="b224e-157">Additional regional/national cloud availability will be updated as we expand RHEL on-demand availability in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="b224e-158">RHUI tooAzure hébergé d’accès est machines virtuelles de toohello limité dans [plages d’adresses IP de centre de données Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="b224e-158">Access tooAzure-hosted RHUI is limited toohello VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
> 
> 

## <a name="get-updates-from-another-update-repository"></a><span data-ttu-id="b224e-159">Obtenir des mises à jour à partir d’un autre référentiel de mise à jour</span><span class="sxs-lookup"><span data-stu-id="b224e-159">Get updates from another update repository</span></span>
<span data-ttu-id="b224e-160">Si vous avez besoin de mises à jour tooget à partir d’un référentiel autre mise à jour (au lieu de RHUI hébergés par Azure), vous devez toounregister vos instances de RHUI.</span><span class="sxs-lookup"><span data-stu-id="b224e-160">If you need tooget updates from a different update repository (instead of Azure-hosted RHUI), first you need toounregister your instances from RHUI.</span></span> <span data-ttu-id="b224e-161">Vous devez toore-s’inscrire avec l’infrastructure de mises à jour souhaitée hello (telles que Red Hat Satellite ou Red Hat Customer Portal CDN).</span><span class="sxs-lookup"><span data-stu-id="b224e-161">Then you need toore-register them with hello desired update infrastructure (such as Red Hat Satellite or Red Hat Customer Portal CDN).</span></span> <span data-ttu-id="b224e-162">Vous aurez besoin d’abonnements Red Hat appropriés pour ces services, et d’une inscription pour l’ [accès cloud Red Hat dans Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="b224e-162">You will need appropriate Red Hat subscriptions for these services and registration for [Red Hat Cloud Access in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span></span>

<span data-ttu-id="b224e-163">toounregister RHUI et infrastructure de mise à jour réinscrivez tooyour, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b224e-163">toounregister RHUI and reregister tooyour update infrastructure follow these steps:</span></span>

1. <span data-ttu-id="b224e-164">Modifiez /etc/yum.repos.d/rh-cloud.repo et tous les `enabled=1` trop`enabled=0`.</span><span class="sxs-lookup"><span data-stu-id="b224e-164">Edit /etc/yum.repos.d/rh-cloud.repo and change all `enabled=1` too`enabled=0`.</span></span> <span data-ttu-id="b224e-165">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b224e-165">For example:</span></span>
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. <span data-ttu-id="b224e-166">Modifiez /etc/yum/pluginconf.d/rhnplugin.conf et `enabled=0` trop`enabled=1`.</span><span class="sxs-lookup"><span data-stu-id="b224e-166">Edit /etc/yum/pluginconf.d/rhnplugin.conf and change `enabled=0` too`enabled=1`.</span></span>
3. <span data-ttu-id="b224e-167">Inscrivez ensuite à l’infrastructure de votre choix de hello, comme portail des clients Red Hat.</span><span class="sxs-lookup"><span data-stu-id="b224e-167">Then register with hello desired infrastructure, such as Red Hat Customer Portal.</span></span> <span data-ttu-id="b224e-168">Suivez Red Hat guide de solution sur [comment tooregister et s’abonner à un toohello système portail des clients Red Hat](https://access.redhat.com/solutions/253273).</span><span class="sxs-lookup"><span data-stu-id="b224e-168">Follow Red Hat solution guide on [how tooregister and subscribe a system toohello Red Hat Customer Portal](https://access.redhat.com/solutions/253273).</span></span>

> [!NOTE]
> <span data-ttu-id="b224e-169">Accès toohello RHUI de hébergés par Azure est inclus dans le prix d’image hello RHEL paiement à l’utilisation (retenues à la source).</span><span class="sxs-lookup"><span data-stu-id="b224e-169">Access toohello Azure-hosted RHUI is included in hello RHEL Pay-As-You-Go (PAYG) image price.</span></span> <span data-ttu-id="b224e-170">Annuler l’inscription d’une machine virtuelle RHEL de retenue à la source à partir de hello RHUI de hébergés par Azure ne convertit pas hello virtual machine dans le type Bring-Your-propre-licence (BYOL) machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b224e-170">Unregistering a PAYG RHEL VM from hello Azure-hosted RHUI does not convert hello virtual machine into Bring-Your-Own-License (BYOL) type VM.</span></span> <span data-ttu-id="b224e-171">Si vous inscrivez hello même machine virtuelle avec une autre source de mises à jour vous pouvez subir des frais doubles : la première fois des frais de logiciels Azure RHEL et hello deuxième fois pour les abonnements de Red Hat.</span><span class="sxs-lookup"><span data-stu-id="b224e-171">If you register hello same VM with another source of updates you may be incurring double charges: first time for Azure RHEL software fee, and hello second time for Red Hat subscription(s).</span></span> 
> 
> <span data-ttu-id="b224e-172">Si vous devez régulièrement toouse une infrastructure de mise à jour autre que RHUI de hébergés par Azure envisagez de créer et déployer vos propres images (BYOL-type), comme décrit dans [créer et télécharger Red Hat-machine virtuelle pour Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) l’article.</span><span class="sxs-lookup"><span data-stu-id="b224e-172">If you consistently need toouse an update infrastructure other than Azure-hosted RHUI consider creating and deploying your own (BYOL-type) images as described in [Create and Upload Red Hat-based virtual machine for Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article.</span></span>
> 

## <a name="next-steps"></a><span data-ttu-id="b224e-173">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b224e-173">Next steps</span></span>
<span data-ttu-id="b224e-174">toocreate un ordinateur Red Hat Enterprise Linux virtuel à partir d’image de paiement à l’utilisation de Azure Marketplace et tirer parti de la RHUI de hébergés par Azure accédez trop[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span><span class="sxs-lookup"><span data-stu-id="b224e-174">toocreate a Red Hat Enterprise Linux VM from Azure Marketplace Pay-As-You-Go image and leverage Azure-hosted RHUI go too[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span></span> <span data-ttu-id="b224e-175">Vous serez en mesure de toouse `yum update` dans votre instance RHEL sans toute configuration supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="b224e-175">You will be able toouse `yum update` in your RHEL instance without any additional setup.</span></span>

