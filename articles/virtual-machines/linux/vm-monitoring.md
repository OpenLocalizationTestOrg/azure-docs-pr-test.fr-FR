---
title: "Activation ou désactivation de l’analyse de machine virtuelle Azure"
description: "Décrit comment activer ou désactiver l’analyse de machine virtuelle Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 6ce366d2-bd4c-4fef-a8f5-a3ae2374abcc
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/08/2016
ms.author: kmouss
ms.openlocfilehash: 9b2fe579113d6ca6bfd27d82eb9d4657657d44ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a><span data-ttu-id="b3907-103">Activation ou désactivation de l’analyse de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="b3907-103">Enable or Disable Azure VM Monitoring</span></span>

<span data-ttu-id="b3907-104">Cette section décrit comment activer ou désactiver l’analyse sur les machine virtuelle exécutées sur Azure.</span><span class="sxs-lookup"><span data-stu-id="b3907-104">This section describes how to enable or disable monitoring on Virtual machines running on Azure.</span></span> <span data-ttu-id="b3907-105">Vous pouvez activer ou désactiver l’analyse à l’aide du portail ou de l’interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="b3907-105">You can enable or disable monitoring using the portal or Azure Command-line Interface for Mac, Linux, and Windows (the Azure CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3907-106">Ce document décrit la version 2.3 de l’extension de diagnostic Linux, qui est dépréciée.</span><span class="sxs-lookup"><span data-stu-id="b3907-106">This document describes version 2.3 of the Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="b3907-107">La version 2.3 sera prise en charge jusqu’au 30 juin 2018.</span><span class="sxs-lookup"><span data-stu-id="b3907-107">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="b3907-108">La version 3.0 de l’extension de diagnostic Linux peut être activée à la place.</span><span class="sxs-lookup"><span data-stu-id="b3907-108">Version 3.0 of the Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="b3907-109">Pour plus d’informations, consultez [la documentation](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="b3907-109">For more information, see [the documentation](./diagnostic-extension.md).</span></span>

## <a name="enable--disable-monitoring-through-the-azure-portal"></a><span data-ttu-id="b3907-110">Activation et désactivation de l’analyse via le portail Azure</span><span class="sxs-lookup"><span data-stu-id="b3907-110">Enable / Disable Monitoring through the Azure portal</span></span>

<span data-ttu-id="b3907-111">Vous pouvez activer l’analyse de votre machine virtuelle Azure, qui fournit les données relatives à votre instance par périodes d’une minute.</span><span class="sxs-lookup"><span data-stu-id="b3907-111">You can enable  monitoring of your Azure VM, which provides data about your instance in 1-minute periods.</span></span> <span data-ttu-id="b3907-112">(des modifications du stockage s’appliquent).</span><span class="sxs-lookup"><span data-stu-id="b3907-112">(storage changes apply).</span></span> <span data-ttu-id="b3907-113">Les données de diagnostic détaillées sont ensuite disponibles pour la machine virtuelle dans les graphes du portail ou via l’API.</span><span class="sxs-lookup"><span data-stu-id="b3907-113">Detailed diagnostics data is then available for the VM in the portal graphs or through the API.</span></span> <span data-ttu-id="b3907-114">Par défaut, le portail Azure active l’analyse basée sur l’hôte d’un ensemble limité d’indicateurs de performance.</span><span class="sxs-lookup"><span data-stu-id="b3907-114">By default, Azure portal enables host-based monitoring of a limited set of metrics.</span></span> <span data-ttu-id="b3907-115">Vous pouvez activer l’analyse d’indicateurs de performance à partir d’une machine virtuelle alors que cette dernière est en cours d’exécution ou dans l’état Arrêté.</span><span class="sxs-lookup"><span data-stu-id="b3907-115">You can enable monitoring of metrics from within a VM while the VM is running or in stopped state.</span></span>

* <span data-ttu-id="b3907-116">Ouvrez le portail Azure à l’adresse [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b3907-116">Open the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
* <span data-ttu-id="b3907-117">Dans la barre de navigation de gauche, cliquez sur Machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="b3907-117">In the left navigation, click Virtual machines.</span></span>
* <span data-ttu-id="b3907-118">Dans la liste Machines virtuelles, sélectionnez une instance en cours d’exécution ou arrêtée.</span><span class="sxs-lookup"><span data-stu-id="b3907-118">In the list Virtual machines, select a running or stopped instance.</span></span> <span data-ttu-id="b3907-119">Le panneau « Machine virtuelle » s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="b3907-119">The "Virtual machine" blade opens.</span></span>
* <span data-ttu-id="b3907-120">Cliquez sur Tous les paramètres.</span><span class="sxs-lookup"><span data-stu-id="b3907-120">Click All settings.</span></span>
* <span data-ttu-id="b3907-121">Cliquez sur Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="b3907-121">Click Diagnostics.</span></span>
* <span data-ttu-id="b3907-122">Modifiez le statut sur On (Activé) ou Off (Désactivé).</span><span class="sxs-lookup"><span data-stu-id="b3907-122">Change status to On or Off.</span></span> <span data-ttu-id="b3907-123">Dans ce panneau, vous pouvez également choisir le niveau des détails d’analyse que vous souhaitez activer pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b3907-123">You can also pick in this blade the level of monitoring details you would like to enable for your virtual machine.</span></span>

![Activation et désactivation de l’analyse via le portail Azure.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a><span data-ttu-id="b3907-125">Activation et désactivation de l’analyse avec l’interface de ligne de commande (CLI) Azure</span><span class="sxs-lookup"><span data-stu-id="b3907-125">Enable / Disable Monitoring with Azure CLI</span></span>

<span data-ttu-id="b3907-126">Pour activer l’analyse pour une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="b3907-126">To enable monitoring for an Azure VM.</span></span>

* <span data-ttu-id="b3907-127">Créez un fichier (nommé PrivateConfig.json, par exemple) :</span><span class="sxs-lookup"><span data-stu-id="b3907-127">Create a file (named such as PrivateConfig.json):</span></span>

```json
{
        "storageAccountName":"the storage account to receive data",
        "storageAccountKey":"the key of the account"
}
```

* <span data-ttu-id="b3907-128">Activez l’extension via Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b3907-128">Enable the extension via Azure CLI.</span></span>

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

<span data-ttu-id="b3907-129">Pour plus d’informations, consultez [Utilisation de l’extension de diagnostic Linux pour surveiller les données de performances et de diagnostic des machines virtuelles Linux](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b3907-129">For more information, see [Using Linux Diagnostic Extension to Monitor Linux VM’s performance and diagnostic data](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
