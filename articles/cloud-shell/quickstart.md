---
title: "démarrage rapide du Cloud Shell (version préliminaire) aaaAzure | Documents Microsoft"
description: "Démarrage rapide pour hello Azure Cloud Shell"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: e60700b92c10c331910dd8bb3c627fe1a024091c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-using-hello-azure-cloud-shell"></a><span data-ttu-id="8627c-103">Démarrage rapide pour l’utilisation de hello Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="8627c-103">Quickstart for using hello Azure Cloud Shell</span></span>

<span data-ttu-id="8627c-104">Ce document décrit en détail comment toouse hello Azure Cloud Shell Bonjour [portail Azure](https://ms.portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8627c-104">This document details how toouse hello Azure Cloud Shell in hello [Azure portal](https://ms.portal.azure.com/).</span></span>

## <a name="start-cloud-shell"></a><span data-ttu-id="8627c-105">Démarrer Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="8627c-105">Start Cloud Shell</span></span>
1. <span data-ttu-id="8627c-106">Lancez **Cloud Shell** à partir du volet de navigation supérieur hello Hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="8627c-106">Launch **Cloud Shell** from hello top navigation of hello Azure portal</span></span> <br>
![](media/shell-icon.png)
2. <span data-ttu-id="8627c-107">Sélectionnez un abonnement toocreate un compte de stockage et le partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="8627c-107">Select a subscription toocreate a storage account and Azure file share</span></span>
3. <span data-ttu-id="8627c-108">Sélectionnez Créer le stockage</span><span class="sxs-lookup"><span data-stu-id="8627c-108">Select "Create storage"</span></span>

> [!TIP]
> <span data-ttu-id="8627c-109">Vous êtes authentifié automatiquement pour Azure CLI 2.0 dans chaque session.</span><span class="sxs-lookup"><span data-stu-id="8627c-109">You are automatically authenticated for Azure CLI 2.0 in every sesssion.</span></span>

### <a name="set-your-subscription"></a><span data-ttu-id="8627c-110">Définissez votre abonnement</span><span class="sxs-lookup"><span data-stu-id="8627c-110">Set your subscription</span></span>
1. <span data-ttu-id="8627c-111">Répertoriez les événements auxquels vous avez accès :</span><span class="sxs-lookup"><span data-stu-id="8627c-111">List subscriptions you have access to:</span></span> <br>
`az account list`
2. <span data-ttu-id="8627c-112">Définissez votre abonnement préféré :</span><span class="sxs-lookup"><span data-stu-id="8627c-112">Set your preferred subscription:</span></span> <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> <span data-ttu-id="8627c-113">Votre abonnement sera mémorisé pour les sessions ultérieures avec `/home/<user>/.azure/azureProfile.json`.</span><span class="sxs-lookup"><span data-stu-id="8627c-113">Your subscription will be remembered for future sessions using `/home/<user>/.azure/azureProfile.json`.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="8627c-114">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="8627c-114">Create a resource group</span></span>
<span data-ttu-id="8627c-115">Créez un nouveau groupe de ressources dans WestUS nommé « MyRG » :</span><span class="sxs-lookup"><span data-stu-id="8627c-115">Create a new resource group in WestUS named "MyRG":</span></span> <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a><span data-ttu-id="8627c-116">Créer une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="8627c-116">Create a Linux VM</span></span>
<span data-ttu-id="8627c-117">Créez une machine virtuelle Ubuntu dans votre nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8627c-117">Create an Ubuntu VM in your new resource group.</span></span> <span data-ttu-id="8627c-118">Hello Azure CLI 2.0 créera les clés SSH et hello de configuration machine virtuelle avec eux.</span><span class="sxs-lookup"><span data-stu-id="8627c-118">hello Azure CLI 2.0 will create SSH keys and setup hello VM with them.</span></span> <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> <span data-ttu-id="8627c-119">Hello tooauthenticate de clés publiques et privées utilisées votre machine virtuelle sont placés dans `/User/.ssh/id_rsa` et `/User/.ssh/id_rsa.pub` par Azure CLI 2.0 par défaut.</span><span class="sxs-lookup"><span data-stu-id="8627c-119">hello public and private keys used tooauthenticate your VM are placed in `/User/.ssh/id_rsa` and `/User/.ssh/id_rsa.pub` by Azure CLI 2.0 by default.</span></span> <span data-ttu-id="8627c-120">Votre dossier .ssh est conservé dans l’image de 5 Go de votre partage de fichiers Azure attaché.</span><span class="sxs-lookup"><span data-stu-id="8627c-120">Your .ssh folder is persisted in your attached Azure file share's 5-GB image.</span></span>

<span data-ttu-id="8627c-121">Votre nom d’utilisateur sur cette machine virtuelle sera votre nom d’utilisateur utilisé dans Cloud Shell ($User@Azure:).</span><span class="sxs-lookup"><span data-stu-id="8627c-121">Your username on this VM will be your username used in Cloud Shell ($User@Azure:).</span></span>

### <a name="ssh-into-your-linux-vm"></a><span data-ttu-id="8627c-122">Se connecter avec SSH à votre machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="8627c-122">SSH into your Linux VM</span></span>
1. <span data-ttu-id="8627c-123">Recherchez le nom de votre machine virtuelle dans la barre de recherche du portail Azure hello</span><span class="sxs-lookup"><span data-stu-id="8627c-123">Search for your VM name in hello Azure portal search bar</span></span>
2. <span data-ttu-id="8627c-124">Cliquez sur « Connexion », puis exécutez : `ssh username@ipaddress`</span><span class="sxs-lookup"><span data-stu-id="8627c-124">Click "Connect" and run: `ssh username@ipaddress`</span></span>

![](media/sshcmd-copy.png)

<span data-ttu-id="8627c-125">Lors de la création de la connexion SSH hello, vous devez voir invite de bienvenue Ubuntu hello.</span><span class="sxs-lookup"><span data-stu-id="8627c-125">Upon establishing hello SSH connection, you should see hello Ubuntu welcome prompt.</span></span>
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a><span data-ttu-id="8627c-126">Nettoyage</span><span class="sxs-lookup"><span data-stu-id="8627c-126">Cleaning up</span></span> 
<span data-ttu-id="8627c-127">Supprimez votre groupe de ressources et toutes les ressources qu’il contient :</span><span class="sxs-lookup"><span data-stu-id="8627c-127">Delete your resource group and any resources within it:</span></span> <br>
<span data-ttu-id="8627c-128">Exécutez `az group delete -n MyRG`.</span><span class="sxs-lookup"><span data-stu-id="8627c-128">Run `az group delete -n MyRG`</span></span>

## <a name="next-steps"></a><span data-ttu-id="8627c-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8627c-129">Next Steps</span></span>
[<span data-ttu-id="8627c-130">En savoir plus sur le stockage persistant sur Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="8627c-130">Learn about persisting storage on Cloud Shell</span></span>](persisting-shell-storage.md) <br><span data-ttu-id="8627c-131">
[En savoir plus sur Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="8627c-131">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br><span data-ttu-id="8627c-132">
[En savoir plus sur le stockage de fichiers Azure](../storage/files/storage-files-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="8627c-132">
[Learn about Azure File storage](../storage/files/storage-files-introduction.md)</span></span> <br>