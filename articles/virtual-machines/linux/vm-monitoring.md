---
title: "aaaEnable ou la désactivation de surveillance de machine virtuelle Azure"
description: "Décrit comment tooEnable ou désactiver l’analyse machine virtuelle Azure"
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
ms.openlocfilehash: 39c2211e4e5f3ad364513b52c5acc70c00b432fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a><span data-ttu-id="7f8e2-103">Activation ou désactivation de l’analyse de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="7f8e2-103">Enable or Disable Azure VM Monitoring</span></span>

<span data-ttu-id="7f8e2-104">Cette section décrit comment tooenable ou la désactivation de la surveillance sur Virtual machines en cours d’exécution sur Azure.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-104">This section describes how tooenable or disable monitoring on Virtual machines running on Azure.</span></span> <span data-ttu-id="7f8e2-105">Vous pouvez activer ou désactiver l’analyse à l’aide de portail de hello ou une Interface de ligne de commande de Azure pour Mac, Linux et Windows (hello CLI d’Azure).</span><span class="sxs-lookup"><span data-stu-id="7f8e2-105">You can enable or disable monitoring using hello portal or Azure Command-line Interface for Mac, Linux, and Windows (hello Azure CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f8e2-106">Ce document décrit la version 2.3 de hello Extension Diagnostics Linux, ce qui a été déconseillée.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-106">This document describes version 2.3 of hello Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="7f8e2-107">La version 2.3 sera prise en charge jusqu’au 30 juin 2018.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-107">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="7f8e2-108">La version 3.0 de hello Extension Diagnostics Linux peut être activée à la place.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-108">Version 3.0 of hello Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="7f8e2-109">Pour plus d’informations, consultez [hello documentation](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="7f8e2-109">For more information, see [hello documentation](./diagnostic-extension.md).</span></span>

## <a name="enable--disable-monitoring-through-hello-azure-portal"></a><span data-ttu-id="7f8e2-110">Activer / désactiver l’analyse hello par le biais du portail Azure</span><span class="sxs-lookup"><span data-stu-id="7f8e2-110">Enable / Disable Monitoring through hello Azure portal</span></span>

<span data-ttu-id="7f8e2-111">Vous pouvez activer l’analyse de votre machine virtuelle Azure, qui fournit les données relatives à votre instance par périodes d’une minute.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-111">You can enable  monitoring of your Azure VM, which provides data about your instance in 1-minute periods.</span></span> <span data-ttu-id="7f8e2-112">(des modifications du stockage s’appliquent).</span><span class="sxs-lookup"><span data-stu-id="7f8e2-112">(storage changes apply).</span></span> <span data-ttu-id="7f8e2-113">Les données de diagnostic détaillées seront ensuite disponibles pour hello machine virtuelle dans les graphiques portail hello ou via l’API de hello.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-113">Detailed diagnostics data is then available for hello VM in hello portal graphs or through hello API.</span></span> <span data-ttu-id="7f8e2-114">Par défaut, le portail Azure active l’analyse basée sur l’hôte d’un ensemble limité d’indicateurs de performance.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-114">By default, Azure portal enables host-based monitoring of a limited set of metrics.</span></span> <span data-ttu-id="7f8e2-115">Vous pouvez activer l’analyse des métriques à partir d’une machine virtuelle lors de hello que machine virtuelle est en cours d’exécution ou arrêté.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-115">You can enable monitoring of metrics from within a VM while hello VM is running or in stopped state.</span></span>

* <span data-ttu-id="7f8e2-116">Ouvrez hello Azure portail à [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7f8e2-116">Open hello Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
* <span data-ttu-id="7f8e2-117">Bonjour barre de navigation gauche, cliquez sur les ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-117">In hello left navigation, click Virtual machines.</span></span>
* <span data-ttu-id="7f8e2-118">Dans hello répertorier les machines virtuelles, sélectionnez une instance en cours d’exécution ou arrêtée.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-118">In hello list Virtual machines, select a running or stopped instance.</span></span> <span data-ttu-id="7f8e2-119">Panneau de « Ordinateur virtuel » Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-119">hello "Virtual machine" blade opens.</span></span>
* <span data-ttu-id="7f8e2-120">Cliquez sur Tous les paramètres.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-120">Click All settings.</span></span>
* <span data-ttu-id="7f8e2-121">Cliquez sur Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-121">Click Diagnostics.</span></span>
* <span data-ttu-id="7f8e2-122">Modifier l’état tooOn ou désactivé.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-122">Change status tooOn or Off.</span></span> <span data-ttu-id="7f8e2-123">Vous pouvez également choisir dans ce niveau de hello Panneau de détails que vous aimeriez tooenable pour votre machine virtuelle de l’analyse.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-123">You can also pick in this blade hello level of monitoring details you would like tooenable for your virtual machine.</span></span>

![Activer ou désactiver l’analyse via hello portail Azure.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a><span data-ttu-id="7f8e2-125">Activation et désactivation de l’analyse avec l’interface de ligne de commande (CLI) Azure</span><span class="sxs-lookup"><span data-stu-id="7f8e2-125">Enable / Disable Monitoring with Azure CLI</span></span>

<span data-ttu-id="7f8e2-126">tooenable d’analyse pour une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-126">tooenable monitoring for an Azure VM.</span></span>

* <span data-ttu-id="7f8e2-127">Créez un fichier (nommé PrivateConfig.json, par exemple) :</span><span class="sxs-lookup"><span data-stu-id="7f8e2-127">Create a file (named such as PrivateConfig.json):</span></span>

```json
{
        "storageAccountName":"hello storage account tooreceive data",
        "storageAccountKey":"hello key of hello account"
}
```

* <span data-ttu-id="7f8e2-128">Activez l’extension hello via l’interface CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-128">Enable hello extension via Azure CLI.</span></span>

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

<span data-ttu-id="7f8e2-129">Pour plus d’informations, consultez [performances et les données de diagnostic de Linux VM utilisation de l’Extension Diagnostics Linux tooMonitor](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7f8e2-129">For more information, see [Using Linux Diagnostic Extension tooMonitor Linux VM’s performance and diagnostic data](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
