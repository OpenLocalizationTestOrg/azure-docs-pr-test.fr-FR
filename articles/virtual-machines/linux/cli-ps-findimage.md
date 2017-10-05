---
title: "Sélectionner des images de machine virtuelle Linux avec Azure CLI | Microsoft Docs"
description: "Découvrez comment utiliser Azure CLI pour déterminer l’éditeur, l’offre, la référence (SKU) et la version d’images de machine virtuelle de la Place de marché."
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
ms.openlocfilehash: e0c27a7ee9e9a7ab1a3b004e070fa556b56a36a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-find-linux-vm-images-in-the-azure-marketplace-with-the-azure-cli"></a><span data-ttu-id="96d77-103">Comment rechercher des images de machine virtuelle Linux sur la Place de marché Microsoft Azure avec Azure CLI</span><span class="sxs-lookup"><span data-stu-id="96d77-103">How to find Linux VM images in the Azure Marketplace with the Azure CLI</span></span>
<span data-ttu-id="96d77-104">Cette rubrique décrit comment utiliser Azure CLI 2.0 pour rechercher des images de machine virtuelle sur la Place de marché Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="96d77-104">This topic describes how to use the Azure CLI 2.0 to find VM images in the Azure Marketplace.</span></span> <span data-ttu-id="96d77-105">Ces informations permettent de spécifier une image de Place de marché lorsque vous créez une machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="96d77-105">Use this information to specify a Marketplace image when you create a Linux VM.</span></span>

<span data-ttu-id="96d77-106">Veillez à installer la dernière version d’[Azure CLI 2.0](/cli/azure/install-az-cli2) et à être connecté à un compte Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="96d77-106">Make sure that you installed the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and are logged in to an Azure account (`az login`).</span></span>

## <a name="terminology"></a><span data-ttu-id="96d77-107">Terminologie</span><span class="sxs-lookup"><span data-stu-id="96d77-107">Terminology</span></span>

<span data-ttu-id="96d77-108">Les images de la Place de marché sont identifiées dans l’interface CLI et d’autres outils Azure selon une hiérarchie :</span><span class="sxs-lookup"><span data-stu-id="96d77-108">Marketplace images are identified in the CLI and other Azure tools according to a hierarchy:</span></span>

* <span data-ttu-id="96d77-109">**Éditeur** : organisation qui a créé l’image.</span><span class="sxs-lookup"><span data-stu-id="96d77-109">**Publisher** - The organization that created the image.</span></span> <span data-ttu-id="96d77-110">Exemple : Canonical</span><span class="sxs-lookup"><span data-stu-id="96d77-110">Example: Canonical</span></span>
* <span data-ttu-id="96d77-111">**Offre** : groupe d’images associées, créé par un éditeur.</span><span class="sxs-lookup"><span data-stu-id="96d77-111">**Offer** - A group of related images created by a publisher.</span></span> <span data-ttu-id="96d77-112">Exemple : Ubuntu Server</span><span class="sxs-lookup"><span data-stu-id="96d77-112">Example: Ubuntu Server</span></span>
* <span data-ttu-id="96d77-113">**Référence SKU** : instance d’une offre, par exemple une version majeure d’un logiciel.</span><span class="sxs-lookup"><span data-stu-id="96d77-113">**SKU** - An instance of an offer, such as a major release of a distribution.</span></span> <span data-ttu-id="96d77-114">Exemple : 16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="96d77-114">Example: 16.04-LTS</span></span>
* <span data-ttu-id="96d77-115">**Version** : numéro de version d’une référence SKU d’image.</span><span class="sxs-lookup"><span data-stu-id="96d77-115">**Version** - The version number of an image SKU.</span></span> <span data-ttu-id="96d77-116">Lorsque vous spécifiez l’image, vous pouvez remplacer le numéro de version par la valeur « latest », qui permet de sélectionner la dernière version de la distribution.</span><span class="sxs-lookup"><span data-stu-id="96d77-116">When specifying the image, you can replace the version number with "latest", which selects the latest version of the distribution.</span></span>

<span data-ttu-id="96d77-117">Pour spécifier une image de la Place de marché, utilisez *l’URN* de l’image.</span><span class="sxs-lookup"><span data-stu-id="96d77-117">To specify a Marketplace image, you typically use the image *URN*.</span></span> <span data-ttu-id="96d77-118">L’URN combine ces valeurs en les séparant par un caractère deux-points (:) : *Éditeur*:*Offre*:*Référence SKU*:*Version*.</span><span class="sxs-lookup"><span data-stu-id="96d77-118">The URN combines these values, separated by the colon (:) character: *Publisher*:*Offer*:*Sku*:*Version*.</span></span> 


## <a name="list-popular-images"></a><span data-ttu-id="96d77-119">Liste des images populaires</span><span class="sxs-lookup"><span data-stu-id="96d77-119">List popular images</span></span>

<span data-ttu-id="96d77-120">Exécutez la commande [az vm image list](/cli/azure/vm/image#list), sans l’option `--all` pour afficher la liste des images de machine virtuelle populaires sur la Place de marché Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="96d77-120">Run the [az vm image list](/cli/azure/vm/image#list) command, without the `--all` option, to see a list of popular VM images in the Azure Marketplace.</span></span> <span data-ttu-id="96d77-121">Par exemple, exécutez la commande suivante pour afficher une liste mise en cache d’images populaires dans un format de tableau :</span><span class="sxs-lookup"><span data-stu-id="96d77-121">For example, run the following command to display a cached list of popular images in table format:</span></span>

```azurecli
az vm image list --output table
```

<span data-ttu-id="96d77-122">La sortie inclut l’URN (la valeur qui se trouve dans la colonne *Urn*), que vous utilisez pour spécifier l’image.</span><span class="sxs-lookup"><span data-stu-id="96d77-122">The output includes the URN (the value in the *Urn* column), which you use to specify the image.</span></span> <span data-ttu-id="96d77-123">Lorsque vous créez une machine virtuelle avec l’une des images populaires de la Place de marché, vous pouvez spécifier l’alias de l’URN, tel que *UbuntuLTS*.</span><span class="sxs-lookup"><span data-stu-id="96d77-123">When creating a VM with one of these popular Marketplace images, you can alternatively specify the URN alias, such as *UbuntuLTS*.</span></span>

```
You are viewing an offline list of images, use --all to retrieve an up-to-date list
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

## <a name="find-specific-images"></a><span data-ttu-id="96d77-124">Recherche d’images spécifiques</span><span class="sxs-lookup"><span data-stu-id="96d77-124">Find specific images</span></span>

<span data-ttu-id="96d77-125">Pour rechercher une image de machine virtuelle dans la Place de marché, utilisez la commande `az vm image list` avec l’option `--all`.</span><span class="sxs-lookup"><span data-stu-id="96d77-125">To find a specific VM image in the Marketplace, use the `az vm image list` command with the `--all` option.</span></span> <span data-ttu-id="96d77-126">L’exécution de cette version de la commande peut prendre un certain temps et retourner une sortie très longue. En général, la sortie peut être filtrée à l’aide de `--publisher` ou d’un autre paramètre.</span><span class="sxs-lookup"><span data-stu-id="96d77-126">This version of the command takes some time to complete and can return lengthy output, so you usually filter the list by `--publisher` or another parameter.</span></span> 

<span data-ttu-id="96d77-127">Par exemple, la commande suivante affiche toutes les offres Debian (n’oubliez pas que, sans le commutateur `--all`, elle effectue une recherche uniquement dans le cache local d’images courantes) :</span><span class="sxs-lookup"><span data-stu-id="96d77-127">For example, the following command displays all Debian offers (remember that without the `--all` switch, it only searches the local cache of common images):</span></span>

```azurecli
az vm image list --offer Debian --all --output table 

```

<span data-ttu-id="96d77-128">Résultat partiel :</span><span class="sxs-lookup"><span data-stu-id="96d77-128">Partial output:</span></span> 
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

<span data-ttu-id="96d77-129">Appliquez des filtres similaires avec les options `--location`, `--publisher` et `--sku`.</span><span class="sxs-lookup"><span data-stu-id="96d77-129">Apply similar filters with the `--location`, `--publisher`, and `--sku` options.</span></span> <span data-ttu-id="96d77-130">Vous pouvez même établir des correspondances partielles sur un filtre, par exemple en cherchant `--offer Deb` pour trouver toutes les images Debian.</span><span class="sxs-lookup"><span data-stu-id="96d77-130">You can even perform partial matches on a filter, such as searching for `--offer Deb` to find all Debian images.</span></span>

<span data-ttu-id="96d77-131">Si vous ne spécifiez pas d’emplacement particulier avec l’option `--location`, les valeurs de `westus` sont retournées par défaut</span><span class="sxs-lookup"><span data-stu-id="96d77-131">If you don't specify a particular location with the `--location` option, the values for `westus` are returned by default.</span></span> <span data-ttu-id="96d77-132">(définissez un autre emplacement par défaut en exécutant la commande `az configure --defaults location=<location>`).</span><span class="sxs-lookup"><span data-stu-id="96d77-132">(Set a different default location by running `az configure --defaults location=<location>`.)</span></span>

<span data-ttu-id="96d77-133">Par exemple, la commande suivante répertorie toutes les références SKU Debian 8 dans `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="96d77-133">For example, the following command lists all Debian 8 SKUs in `westeurope`:</span></span>

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

<span data-ttu-id="96d77-134">Résultat partiel :</span><span class="sxs-lookup"><span data-stu-id="96d77-134">Partial output:</span></span>

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

## <a name="navigate-the-images"></a><span data-ttu-id="96d77-135">Parcourir les images</span><span class="sxs-lookup"><span data-stu-id="96d77-135">Navigate the images</span></span> 
<span data-ttu-id="96d77-136">Une autre façon de trouver une image dans un emplacement consiste à exécuter successivement les commandes [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers) et [az vm image list-skus](/cli/azure/vm/image#list-skus).</span><span class="sxs-lookup"><span data-stu-id="96d77-136">Another way to find an image in a location is to run the [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers), and [az vm image list-skus](/cli/azure/vm/image#list-skus) commands in sequence.</span></span> <span data-ttu-id="96d77-137">Ces commandes vous permettent de déterminer les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="96d77-137">With these commands, you determine these values:</span></span>

1. <span data-ttu-id="96d77-138">en répertoriant les éditeurs d’images ;</span><span class="sxs-lookup"><span data-stu-id="96d77-138">List the image publishers.</span></span>
2. <span data-ttu-id="96d77-139">pour un éditeur donné, en répertoriant ses offres ;</span><span class="sxs-lookup"><span data-stu-id="96d77-139">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="96d77-140">pour une offre donnée, en répertoriant ses références SKU.</span><span class="sxs-lookup"><span data-stu-id="96d77-140">For a given offer, list their SKUs.</span></span>


<span data-ttu-id="96d77-141">Par exemple, la commande suivante répertorie les éditeurs d’image dans l’emplacement Ouest des États-Unis :</span><span class="sxs-lookup"><span data-stu-id="96d77-141">For example, the following command lists the image publishers in the West US location:</span></span>

```azurecli
az vm image list-publishers --location westus --output table
```

<span data-ttu-id="96d77-142">Résultat partiel :</span><span class="sxs-lookup"><span data-stu-id="96d77-142">Partial output:</span></span>

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
<span data-ttu-id="96d77-143">Ces informations vous permettent de trouver des offres d’un éditeur spécifique.</span><span class="sxs-lookup"><span data-stu-id="96d77-143">Use this information to find offers from a specific publisher.</span></span> <span data-ttu-id="96d77-144">Par exemple, si Canonical est un éditeur d’image dans l’emplacement Ouest des États-Unis, vous pouvez trouver ses offres en exécutant la commande `azure vm image list-offers`.</span><span class="sxs-lookup"><span data-stu-id="96d77-144">For example, if Canonical is an image publisher in the West US location, find their offers by running `azure vm image list-offers`.</span></span> <span data-ttu-id="96d77-145">Passez l’emplacement et l’éditeur comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="96d77-145">Pass the location and the publisher as in the following example:</span></span>

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

<span data-ttu-id="96d77-146">Sortie :</span><span class="sxs-lookup"><span data-stu-id="96d77-146">Output:</span></span>

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
<span data-ttu-id="96d77-147">Nous voyons maintenant que, dans la région « West US », « Canonical » publie l’offre **UbuntuServer** sur Azure.</span><span class="sxs-lookup"><span data-stu-id="96d77-147">You see that in the West US region, Canonical publishes the **UbuntuServer** offer on Azure.</span></span> <span data-ttu-id="96d77-148">Mais quelles sont les références SKU ?</span><span class="sxs-lookup"><span data-stu-id="96d77-148">But what SKUs?</span></span> <span data-ttu-id="96d77-149">Pour obtenir ces valeurs, exécutez la commande `azure vm image list-skus` et définissez l’emplacement, l’éditeur et l’offre que vous avez découverts :</span><span class="sxs-lookup"><span data-stu-id="96d77-149">To get those values, run `azure vm image list-skus` and set the location, publisher, and offer that you have discovered:</span></span>

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

<span data-ttu-id="96d77-150">Output:</span><span class="sxs-lookup"><span data-stu-id="96d77-150">Output:</span></span>

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

<span data-ttu-id="96d77-151">Enfin, utilisez la commande `az vm image list` pour trouver une version spécifique de la référence SKU, par exemple **16.04-LTS** :</span><span class="sxs-lookup"><span data-stu-id="96d77-151">Finally, use the `az vm image list` command to find a specific version of the SKU you want, for example, **16.04-LTS**:</span></span>

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

<span data-ttu-id="96d77-152">Output:</span><span class="sxs-lookup"><span data-stu-id="96d77-152">Output:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="96d77-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="96d77-153">Next steps</span></span>
<span data-ttu-id="96d77-154">Vous pouvez maintenant choisir précisément l’image à utiliser en prenant note de la valeur URN.</span><span class="sxs-lookup"><span data-stu-id="96d77-154">Now you can choose precisely the image you want to use by taking note of the URN value.</span></span> <span data-ttu-id="96d77-155">Passez cette valeur avec le paramètre `--image` lorsque vous créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="96d77-155">Pass this value with the `--image` parameter when you create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="96d77-156">N’oubliez pas que vous pouvez remplacer le numéro de version de l’URN par « latest » (dernière version).</span><span class="sxs-lookup"><span data-stu-id="96d77-156">Remember that you can optionally replace the version number in the URN with "latest".</span></span> <span data-ttu-id="96d77-157">Cette version est toujours la dernière version de la distribution.</span><span class="sxs-lookup"><span data-stu-id="96d77-157">This version is always the latest version of the distribution.</span></span> <span data-ttu-id="96d77-158">Pour créer rapidement une machine virtuelle en utilisant les informations d’URN, consultez [Créer et gérer des machines virtuelles Linux avec l’interface Azure CLI](tutorial-manage-vm.md).</span><span class="sxs-lookup"><span data-stu-id="96d77-158">To create a virtual machine quickly by using the URN information, see [Create and Manage Linux VMs with the Azure CLI](tutorial-manage-vm.md).</span></span>
