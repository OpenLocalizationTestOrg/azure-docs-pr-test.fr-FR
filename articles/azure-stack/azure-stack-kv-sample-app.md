---
title: "Autoriser l’application à récupérer les secrets d’un coffre de clés dans Azure Stack | Microsoft Docs"
description: "Utiliser un exemple d’application à utiliser avec Azure Stack Key Vault"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 3748b719-e269-4b48-8d7d-d75a84b0e1e5
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/04/2017
ms.author: sngun
ms.openlocfilehash: 4b517526d89e7f6c2649e2f12810b4db705defa3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="run-the-sample-application-for-key-vault"></a><span data-ttu-id="ff3f9-103">Exécutez l’exemple d’application pour le coffre de clés</span><span class="sxs-lookup"><span data-stu-id="ff3f9-103">Run the sample application for Key Vault</span></span>

<span data-ttu-id="ff3f9-104">Dans ce guide, vous utiliserez un exemple d’application pour extraire les secrets et des mots de passe à partir du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="ff3f9-104">In this guide, you'll use a sample application to retrieve secrets and passwords from Key Vault.</span></span>

## <a name="download-the-samples-and-prepare"></a><span data-ttu-id="ff3f9-105">Télécharger les exemples et préparer</span><span class="sxs-lookup"><span data-stu-id="ff3f9-105">Download the samples and prepare</span></span>
<span data-ttu-id="ff3f9-106">Télécharger les exemples de client Azure Key Vault à partir de la [page d’exemples de client Azure Key Vault](https://www.microsoft.com/en-us/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="ff3f9-106">Download the Azure Key Vault client samples from the [Azure Key Vault client samples page](https://www.microsoft.com/en-us/download/details.aspx?id=45343).</span></span>

<span data-ttu-id="ff3f9-107">Extrayez le contenu du fichier .zip sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="ff3f9-107">Extract the contents of the .zip file to your local computer.</span></span>

<span data-ttu-id="ff3f9-108">Lecture la **README.md** fichier (il s’agit d’un fichier texte), puis suivez les instructions.</span><span class="sxs-lookup"><span data-stu-id="ff3f9-108">Read the **README.md** file (this is a text file), and then follow the instructions.</span></span>

## <a name="run-sample-1--hellokeyvault"></a><span data-ttu-id="ff3f9-109">Exécuter l’exemple #1--HelloKeyVault</span><span class="sxs-lookup"><span data-stu-id="ff3f9-109">Run Sample #1--HelloKeyVault</span></span>
<span data-ttu-id="ff3f9-110">HelloKeyVault est une application console qui vous guide à travers les scénarios clés qui sont prises en charge par le coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="ff3f9-110">HelloKeyVault is a console application that walks through the key scenarios that are supported by Key Vault:</span></span>

1. <span data-ttu-id="ff3f9-111">Créer et d’importation d’une clé (clé de module de sécurité matériel ou logiciel)</span><span class="sxs-lookup"><span data-stu-id="ff3f9-111">Create/import a key (HSM or software key)</span></span>
2. <span data-ttu-id="ff3f9-112">Chiffrer une clé secrète à l’aide d’une clé de contenu</span><span class="sxs-lookup"><span data-stu-id="ff3f9-112">Encrypt a secret using a content key</span></span>
3. <span data-ttu-id="ff3f9-113">Encapsuler la clé de contenu à l’aide d’une clé de coffre de clés</span><span class="sxs-lookup"><span data-stu-id="ff3f9-113">Wrap the content key using a Key Vault key</span></span>
4. <span data-ttu-id="ff3f9-114">Désencapsuler la clé de contenu</span><span class="sxs-lookup"><span data-stu-id="ff3f9-114">Unwrap the content key</span></span>
5. <span data-ttu-id="ff3f9-115">Déchiffrer la clé secrète</span><span class="sxs-lookup"><span data-stu-id="ff3f9-115">Decrypt the secret</span></span>
6. <span data-ttu-id="ff3f9-116">Définir une clé secrète</span><span class="sxs-lookup"><span data-stu-id="ff3f9-116">Set a secret</span></span>

<span data-ttu-id="ff3f9-117">Cette application de console doit s’exécuter sans modification, à ceci près que les paramètres de configuration appropriés dans App.Config seront mise à jour après les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ff3f9-117">That console application should run with no changes, except that the appropriate configuration settings in App.Config will be updated according to the following steps:</span></span>

1. <span data-ttu-id="ff3f9-118">Mettre à jour les paramètres de configuration d’application dans HelloKeyVault\App.config avec votre URL du coffre, un ID d’application principal et un secret.</span><span class="sxs-lookup"><span data-stu-id="ff3f9-118">Update the app configuration settings in HelloKeyVault\App.config with your vault URL, application principal ID, and secret.</span></span> <span data-ttu-id="ff3f9-119">Les informations peuvent également être générées à l’aide de **scripts\GetAppConfigSettings.ps1**.</span><span class="sxs-lookup"><span data-stu-id="ff3f9-119">The information can optionally be generated using **scripts\GetAppConfigSettings.ps1**.</span></span>
2. <span data-ttu-id="ff3f9-120">Mettre à jour les valeurs des variables obligatoires dans GetAppConfigSettings.ps1.</span><span class="sxs-lookup"><span data-stu-id="ff3f9-120">Update the values of the mandatory variables in GetAppConfigSettings.ps1.</span></span>
3. <span data-ttu-id="ff3f9-121">Lancez la fenêtre Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff3f9-121">Launch the Windows PowerShell window.</span></span>
4. <span data-ttu-id="ff3f9-122">Dans la fenêtre PowerShell, exécutez le script GetAppConfigSettings.ps1.</span><span class="sxs-lookup"><span data-stu-id="ff3f9-122">Run the GetAppConfigSettings.ps1 script within the PowerShell window.</span></span>
5. <span data-ttu-id="ff3f9-123">Copier les résultats du script dans le fichier HelloKeyVault\App.config.</span><span class="sxs-lookup"><span data-stu-id="ff3f9-123">Copy the results of the script to the HelloKeyVault\App.config file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff3f9-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ff3f9-124">Next steps</span></span>
[<span data-ttu-id="ff3f9-125">Déployer une machine virtuelle avec un mot de passe Key Vault</span><span class="sxs-lookup"><span data-stu-id="ff3f9-125">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)

[<span data-ttu-id="ff3f9-126">Déployer une machine virtuelle avec un certificat Key Vault</span><span class="sxs-lookup"><span data-stu-id="ff3f9-126">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

