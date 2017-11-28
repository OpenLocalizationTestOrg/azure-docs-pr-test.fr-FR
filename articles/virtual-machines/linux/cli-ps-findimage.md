---
title: "les images Linux VM aaaSelect avec hello CLI d’Azure | Documents Microsoft"
description: "Découvrez comment toouse hello serveur de publication toodetermine hello CLI d’Azure, offre, référence (SKU) et la version pour les images de machine virtuelle du Marketplace."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7a858e38-4f17-4e8e-a28a-c7f801101721
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/24/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0b115b8654bc156b5bfadba53a6b002a105acb68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-linux-vm-images-in-hello-azure-marketplace-with-hello-azure-cli"></a><span data-ttu-id="13567-103">Comment toofind Linux VM images Bonjour Azure Marketplace par hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="13567-103">How toofind Linux VM images in hello Azure Marketplace with hello Azure CLI</span></span>
<span data-ttu-id="13567-104">Cette rubrique décrit comment toouse hello images de machine virtuelle Azure CLI 2.0 toofind Bonjour Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="13567-104">This topic describes how toouse hello Azure CLI 2.0 toofind VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="13567-105">Utilisez cette toospecify informations une image de Marketplace lorsque vous créez un VM Linux.</span><span class="sxs-lookup"><span data-stu-id="13567-105">Use this information toospecify a Marketplace image when you create a Linux VM.</span></span>

<span data-ttu-id="13567-106">Assurez-vous que vous avez installé hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) et sont enregistrés dans tooan compte Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="13567-106">Make sure that you installed hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and are logged in tooan Azure account (`az login`).</span></span>

## <a name="terminology"></a><span data-ttu-id="13567-107">Terminologie</span><span class="sxs-lookup"><span data-stu-id="13567-107">Terminology</span></span>

<span data-ttu-id="13567-108">Images de Marketplace sont identifiées dans hello CLI et d’autres outils Azure selon tooa hiérarchie :</span><span class="sxs-lookup"><span data-stu-id="13567-108">Marketplace images are identified in hello CLI and other Azure tools according tooa hierarchy:</span></span>

* <span data-ttu-id="13567-109">**Serveur de publication** -hello organisation qui a créé l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="13567-109">**Publisher** - hello organization that created hello image.</span></span> <span data-ttu-id="13567-110">Exemple : Canonical</span><span class="sxs-lookup"><span data-stu-id="13567-110">Example: Canonical</span></span>
* <span data-ttu-id="13567-111">**Offre** : groupe d’images associées, créé par un éditeur.</span><span class="sxs-lookup"><span data-stu-id="13567-111">**Offer** - A group of related images created by a publisher.</span></span> <span data-ttu-id="13567-112">Exemple : Ubuntu Server</span><span class="sxs-lookup"><span data-stu-id="13567-112">Example: Ubuntu Server</span></span>
* <span data-ttu-id="13567-113">**Référence SKU** : instance d’une offre, par exemple une version majeure d’un logiciel.</span><span class="sxs-lookup"><span data-stu-id="13567-113">**SKU** - An instance of an offer, such as a major release of a distribution.</span></span> <span data-ttu-id="13567-114">Exemple : 16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="13567-114">Example: 16.04-LTS</span></span>
* <span data-ttu-id="13567-115">**Version** -hello numéro de version d’une image de référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="13567-115">**Version** - hello version number of an image SKU.</span></span> <span data-ttu-id="13567-116">Lorsque vous spécifiez l’image de hello, vous pouvez remplacer le numéro de version hello avec « dernier », qui sélectionne la version la plus récente de la distribution de hello hello.</span><span class="sxs-lookup"><span data-stu-id="13567-116">When specifying hello image, you can replace hello version number with "latest", which selects hello latest version of hello distribution.</span></span>

<span data-ttu-id="13567-117">toospecify une image de Marketplace, vous utilisez généralement hello image *URN*.</span><span class="sxs-lookup"><span data-stu-id="13567-117">toospecify a Marketplace image, you typically use hello image *URN*.</span></span> <span data-ttu-id="13567-118">Hello URN combine ces valeurs, séparées par le signe deux-points ( :) de hello : *Publisher*:*offrent*:*référence (SKU)*:*Version*.</span><span class="sxs-lookup"><span data-stu-id="13567-118">hello URN combines these values, separated by hello colon (:) character: *Publisher*:*Offer*:*Sku*:*Version*.</span></span> 


## <a name="list-popular-images"></a><span data-ttu-id="13567-119">Liste des images populaires</span><span class="sxs-lookup"><span data-stu-id="13567-119">List popular images</span></span>

<span data-ttu-id="13567-120">Exécutez hello [liste d’images de machine virtuelle de az](/cli/azure/vm/image#list) commande, sans hello `--all` option, toosee une liste de machine virtuelle populaires images Bonjour Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="13567-120">Run hello [az vm image list](/cli/azure/vm/image#list) command, without hello `--all` option, toosee a list of popular VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="13567-121">Par exemple, exécutez hello suivant commande toodisplay une liste mise en cache d’images courantes dans un format de table :</span><span class="sxs-lookup"><span data-stu-id="13567-121">For example, run hello following command toodisplay a cached list of popular images in table format:</span></span>

```azurecli
az vm image list --output table
```

<span data-ttu-id="13567-122">sortie de Hello inclut hello URN (hello valeur Bonjour *Urn* colonne), qui vous utilisez toospecify hello image.</span><span class="sxs-lookup"><span data-stu-id="13567-122">hello output includes hello URN (hello value in hello *Urn* column), which you use toospecify hello image.</span></span> <span data-ttu-id="13567-123">Lorsque vous créez une machine virtuelle avec l’un de ces images Marketplace populaires, vous pouvez spécifier les alias d’URN hello, tel que *UbuntuLTS*.</span><span class="sxs-lookup"><span data-stu-id="13567-123">When creating a VM with one of these popular Marketplace images, you can alternatively specify hello URN alias, such as *UbuntuLTS*.</span></span>

```
You are viewing an offline list of images, use --all tooretrieve an up-to-date list
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
...
```

## <a name="find-specific-images"></a><span data-ttu-id="13567-124">Recherche d’images spécifiques</span><span class="sxs-lookup"><span data-stu-id="13567-124">Find specific images</span></span>

<span data-ttu-id="13567-125">toofind une image de machine virtuelle spécifique Bonjour Marketplace, utilisez hello `az vm image list` avec hello `--all` option.</span><span class="sxs-lookup"><span data-stu-id="13567-125">toofind a specific VM image in hello Marketplace, use hello `az vm image list` command with hello `--all` option.</span></span> <span data-ttu-id="13567-126">Cette version de la commande hello prend quelques toocomplete de temps et peut retourner une sortie longue, donc vous généralement filtrez la liste de hello par `--publisher` ou un autre paramètre.</span><span class="sxs-lookup"><span data-stu-id="13567-126">This version of hello command takes some time toocomplete and can return lengthy output, so you usually filter hello list by `--publisher` or another parameter.</span></span> 

<span data-ttu-id="13567-127">Par exemple, hello commande suivante affiche toutes les offres Debian (n’oubliez pas que sans hello `--all` basculer, il recherche uniquement dans le cache local d’images courantes hello) :</span><span class="sxs-lookup"><span data-stu-id="13567-127">For example, hello following command displays all Debian offers (remember that without hello `--all` switch, it only searches hello local cache of common images):</span></span>

```azurecli
az vm image list --offer Debian --all --output table 

```

<span data-ttu-id="13567-128">Résultat partiel :</span><span class="sxs-lookup"><span data-stu-id="13567-128">Partial output:</span></span> 
```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  --------------
Debian   credativ     7                  credativ:Debian:7:7.0.201602010                  7.0.201602010
Debian   credativ     7                  credativ:Debian:7:7.0.201603020                  7.0.201603020
Debian   credativ     7                  credativ:Debian:7:7.0.201604050                  7.0.201604050
Debian   credativ     7                  credativ:Debian:7:7.0.201604200                  7.0.201604200
Debian   credativ     7                  credativ:Debian:7:7.0.201606280                  7.0.201606280
Debian   credativ     7                  credativ:Debian:7:7.0.201609120                  7.0.201609120
Debian   credativ     7                  credativ:Debian:7:7.0.201611020                  7.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
Debian   credativ     8                  credativ:Debian:8:8.0.201708040                  8.0.201708040
...
```

<span data-ttu-id="13567-129">Appliquer des filtres similaires avec hello `--location`, `--publisher`, et `--sku` options.</span><span class="sxs-lookup"><span data-stu-id="13567-129">Apply similar filters with hello `--location`, `--publisher`, and `--sku` options.</span></span> <span data-ttu-id="13567-130">Vous pouvez même effectuer des correspondances partielles sur un filtre, par exemple rechercher `--offer Deb` toofind toutes les images Debian.</span><span class="sxs-lookup"><span data-stu-id="13567-130">You can even perform partial matches on a filter, such as searching for `--offer Deb` toofind all Debian images.</span></span>

<span data-ttu-id="13567-131">Si vous ne spécifiez pas un emplacement particulier avec hello `--location` , hello les valeurs d’option pour `westus` sont retournés par défaut.</span><span class="sxs-lookup"><span data-stu-id="13567-131">If you don't specify a particular location with hello `--location` option, hello values for `westus` are returned by default.</span></span> <span data-ttu-id="13567-132">(définissez un autre emplacement par défaut en exécutant la commande `az configure --defaults location=<location>`).</span><span class="sxs-lookup"><span data-stu-id="13567-132">(Set a different default location by running `az configure --defaults location=<location>`.)</span></span>

<span data-ttu-id="13567-133">Par exemple, hello commande suivante répertorie toutes les références SKU 8 Debian dans `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="13567-133">For example, hello following command lists all Debian 8 SKUs in `westeurope`:</span></span>

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

<span data-ttu-id="13567-134">Résultat partiel :</span><span class="sxs-lookup"><span data-stu-id="13567-134">Partial output:</span></span>

```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  -------------
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
...
```

## <a name="navigate-hello-images"></a><span data-ttu-id="13567-135">Parcourir les images hello</span><span class="sxs-lookup"><span data-stu-id="13567-135">Navigate hello images</span></span> 
<span data-ttu-id="13567-136">Une autre façon toofind une image dans un emplacement est toorun hello [image de machine virtuelle az liste-Éditeurs](/cli/azure/vm/image#list-publishers), [image de machine virtuelle az liste-offres](/cli/azure/vm/image#list-offers), et [image de machine virtuelle az liste-SKU](/cli/azure/vm/image#list-skus) commandes dans la séquence.</span><span class="sxs-lookup"><span data-stu-id="13567-136">Another way toofind an image in a location is toorun hello [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers), and [az vm image list-skus](/cli/azure/vm/image#list-skus) commands in sequence.</span></span> <span data-ttu-id="13567-137">Ces commandes vous permettent de déterminer les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="13567-137">With these commands, you determine these values:</span></span>

1. <span data-ttu-id="13567-138">Serveurs de publication liste hello image.</span><span class="sxs-lookup"><span data-stu-id="13567-138">List hello image publishers.</span></span>
2. <span data-ttu-id="13567-139">pour un éditeur donné, en répertoriant ses offres ;</span><span class="sxs-lookup"><span data-stu-id="13567-139">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="13567-140">pour une offre donnée, en répertoriant ses références SKU.</span><span class="sxs-lookup"><span data-stu-id="13567-140">For a given offer, list their SKUs.</span></span>


<span data-ttu-id="13567-141">Par exemple, hello commande suivante répertorie les éditeurs d’image hello Bonjour emplacement de l’ouest des États-Unis :</span><span class="sxs-lookup"><span data-stu-id="13567-141">For example, hello following command lists hello image publishers in hello West US location:</span></span>

```azurecli
az vm image list-publishers --location westus --output table
```

<span data-ttu-id="13567-142">Résultat partiel :</span><span class="sxs-lookup"><span data-stu-id="13567-142">Partial output:</span></span>

```
Location    Name
----------  ----------------------------------------------------
westus      1e
westus      4psa
westus      7isolutions
westus      a10networks
westus      abiquo
westus      accellion
westus      Acronis
westus      Acronis.Backup
westus      actian_matrix
westus      actifio
westus      activeeon
westus      adatao
...
```
<span data-ttu-id="13567-143">Utilisez que cette toofind informations offre à partir d’un éditeur spécifique.</span><span class="sxs-lookup"><span data-stu-id="13567-143">Use this information toofind offers from a specific publisher.</span></span> <span data-ttu-id="13567-144">Par exemple, si canoniques est un serveur de publication image Bonjour emplacement de l’ouest des États-Unis, recherchez leurs offres en exécutant `azure vm image list-offers`.</span><span class="sxs-lookup"><span data-stu-id="13567-144">For example, if Canonical is an image publisher in hello West US location, find their offers by running `azure vm image list-offers`.</span></span> <span data-ttu-id="13567-145">Passez l’emplacement de hello et publisher hello comme hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="13567-145">Pass hello location and hello publisher as in hello following example:</span></span>

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

<span data-ttu-id="13567-146">Output:</span><span class="sxs-lookup"><span data-stu-id="13567-146">Output:</span></span>

```
Location    Name
----------  -------------------------
westus      Ubuntu15.04Snappy
westus      Ubuntu15.04SnappyDocker
westus      UbunturollingSnappy
westus      UbuntuServer
westus      Ubuntu_Core
westus      Ubuntu_Snappy_Core
westus      Ubuntu_Snappy_Core_Docker
```
<span data-ttu-id="13567-147">Vous voyez que dans la région ouest des États-Unis hello, canoniques publie hello **UbuntuServer** offrent sur Azure.</span><span class="sxs-lookup"><span data-stu-id="13567-147">You see that in hello West US region, Canonical publishes hello **UbuntuServer** offer on Azure.</span></span> <span data-ttu-id="13567-148">Mais les références (SKU) ? l’exécution de ces valeurs, tooget `azure vm image list-skus` et définissez hello, publisher et l’emplacement offre que vous avez découvert :</span><span class="sxs-lookup"><span data-stu-id="13567-148">But what SKUs? tooget those values, run `azure vm image list-skus` and set hello location, publisher, and offer that you have discovered:</span></span>

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

<span data-ttu-id="13567-149">Output:</span><span class="sxs-lookup"><span data-stu-id="13567-149">Output:</span></span>

```
Location    Name
----------  -----------------
westus      12.04.3-LTS
westus      12.04.4-LTS
westus      12.04.5-DAILY-LTS
westus      12.04.5-LTS
westus      12.10
westus      14.04.0-LTS
westus      14.04.1-LTS
westus      14.04.2-LTS
westus      14.04.3-LTS
westus      14.04.4-LTS
westus      14.04.5-DAILY-LTS
westus      14.04.5-LTS
westus      16.04-beta
westus      16.04-DAILY-LTS
westus      16.04-LTS
westus      16.04.0-LTS
westus      16.10
westus      16.10-DAILY
westus      17.04
westus      17.04-DAILY
westus      17.10-DAILY
```

<span data-ttu-id="13567-150">Enfin, utilisez hello `az vm image list` commande toofind une version spécifique de hello SKU souhaité, par exemple, **16.04-LTS**:</span><span class="sxs-lookup"><span data-stu-id="13567-150">Finally, use hello `az vm image list` command toofind a specific version of hello SKU you want, for example, **16.04-LTS**:</span></span>

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

<span data-ttu-id="13567-151">Output:</span><span class="sxs-lookup"><span data-stu-id="13567-151">Output:</span></span>

```
Offer         Publisher    Sku        Urn                                               Version
------------  -----------  ---------  ------------------------------------------------  ---------------
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611220  16.04.201611220
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611300  16.04.201611300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612050  16.04.201612050
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612140  16.04.201612140
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612210  16.04.201612210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201701130  16.04.201701130
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702020  16.04.201702020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702200  16.04.201702200
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702210  16.04.201702210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702240  16.04.201702240
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703020  16.04.201703020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703030  16.04.201703030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703070  16.04.201703070
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703270  16.04.201703270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703280  16.04.201703280
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703300  16.04.201703300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705080  16.04.201705080
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705160  16.04.201705160
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706100  16.04.201706100
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706191  16.04.201706191
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707210  16.04.201707210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707270  16.04.201707270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708030  16.04.201708030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708110  16.04.201708110
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708151  16.04.201708151
```
## <a name="next-steps"></a><span data-ttu-id="13567-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="13567-152">Next steps</span></span>
<span data-ttu-id="13567-153">Maintenant vous pouvez choisir précisément hello image que vous voulez toouse en prenant acte de hello valeur URN.</span><span class="sxs-lookup"><span data-stu-id="13567-153">Now you can choose precisely hello image you want toouse by taking note of hello URN value.</span></span> <span data-ttu-id="13567-154">Passez cette valeur avec hello `--image` paramètre lorsque vous créez une machine virtuelle avec hello [az vm créer](/cli/azure/vm#create) commande.</span><span class="sxs-lookup"><span data-stu-id="13567-154">Pass this value with hello `--image` parameter when you create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="13567-155">N’oubliez pas que vous pouvez éventuellement remplacer le numéro de version hello Bonjour URN avec « dernier ».</span><span class="sxs-lookup"><span data-stu-id="13567-155">Remember that you can optionally replace hello version number in hello URN with "latest".</span></span> <span data-ttu-id="13567-156">Cette version est toujours version la plus récente de la distribution de hello hello.</span><span class="sxs-lookup"><span data-stu-id="13567-156">This version is always hello latest version of hello distribution.</span></span> <span data-ttu-id="13567-157">toocreate un ordinateur virtuel rapidement en utilisant les informations d’URN hello, consultez [créer et gérer des ordinateurs virtuels Linux par hello CLI d’Azure](tutorial-manage-vm.md).</span><span class="sxs-lookup"><span data-stu-id="13567-157">toocreate a virtual machine quickly by using hello URN information, see [Create and Manage Linux VMs with hello Azure CLI](tutorial-manage-vm.md).</span></span>
