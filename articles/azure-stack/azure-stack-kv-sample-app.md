---
title: "les secrets de coffre de clés Azure pile aaaAllow application tooretrieve | Documents Microsoft"
description: "Utiliser un toowork d’application exemple avec la pile d’Azure Key Vault"
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
ms.openlocfilehash: 2ff3f0bab86d9d1934b463f72124863d29dbe696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-for-key-vault"></a><span data-ttu-id="3984d-103">Exécutez l’exemple d’application hello pour le coffre de clés</span><span class="sxs-lookup"><span data-stu-id="3984d-103">Run hello sample application for Key Vault</span></span>

<span data-ttu-id="3984d-104">Dans ce guide, vous allez utiliser un tooretrieve d’application exemple secrets et des mots de passe à partir du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="3984d-104">In this guide, you'll use a sample application tooretrieve secrets and passwords from Key Vault.</span></span>

## <a name="download-hello-samples-and-prepare"></a><span data-ttu-id="3984d-105">Télécharger les exemples hello et préparer</span><span class="sxs-lookup"><span data-stu-id="3984d-105">Download hello samples and prepare</span></span>
<span data-ttu-id="3984d-106">Télécharger des exemples de client de coffre de clés Azure hello de hello [page d’exemples de client Azure Key Vault](https://www.microsoft.com/en-us/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="3984d-106">Download hello Azure Key Vault client samples from hello [Azure Key Vault client samples page](https://www.microsoft.com/en-us/download/details.aspx?id=45343).</span></span>

<span data-ttu-id="3984d-107">Extrayez le contenu hello de l’ordinateur local du tooyour fichier .zip hello.</span><span class="sxs-lookup"><span data-stu-id="3984d-107">Extract hello contents of hello .zip file tooyour local computer.</span></span>

<span data-ttu-id="3984d-108">Hello de lecture **README.md** fichier (il s’agit d’un fichier texte), puis suivez les instructions de hello.</span><span class="sxs-lookup"><span data-stu-id="3984d-108">Read hello **README.md** file (this is a text file), and then follow hello instructions.</span></span>

## <a name="run-sample-1--hellokeyvault"></a><span data-ttu-id="3984d-109">Exécuter l’exemple #1--HelloKeyVault</span><span class="sxs-lookup"><span data-stu-id="3984d-109">Run Sample #1--HelloKeyVault</span></span>
<span data-ttu-id="3984d-110">HelloKeyVault est une application console qui vous guide à travers les scénarios clés hello qui sont pris en charge par le coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="3984d-110">HelloKeyVault is a console application that walks through hello key scenarios that are supported by Key Vault:</span></span>

1. <span data-ttu-id="3984d-111">Créer et d’importation d’une clé (clé de module de sécurité matériel ou logiciel)</span><span class="sxs-lookup"><span data-stu-id="3984d-111">Create/import a key (HSM or software key)</span></span>
2. <span data-ttu-id="3984d-112">Chiffrer une clé secrète à l’aide d’une clé de contenu</span><span class="sxs-lookup"><span data-stu-id="3984d-112">Encrypt a secret using a content key</span></span>
3. <span data-ttu-id="3984d-113">Encapsuler la clé de contenu hello à l’aide d’une clé de coffre de clés</span><span class="sxs-lookup"><span data-stu-id="3984d-113">Wrap hello content key using a Key Vault key</span></span>
4. <span data-ttu-id="3984d-114">Désencapsuler la clé de contenu hello</span><span class="sxs-lookup"><span data-stu-id="3984d-114">Unwrap hello content key</span></span>
5. <span data-ttu-id="3984d-115">Déchiffrer un secret de hello</span><span class="sxs-lookup"><span data-stu-id="3984d-115">Decrypt hello secret</span></span>
6. <span data-ttu-id="3984d-116">Définir une clé secrète</span><span class="sxs-lookup"><span data-stu-id="3984d-116">Set a secret</span></span>

<span data-ttu-id="3984d-117">Cette application de console doit s’exécuter sans modification, à ceci près que les paramètres de configuration appropriés hello dans App.Config seront mise à jour en fonction de toohello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3984d-117">That console application should run with no changes, except that hello appropriate configuration settings in App.Config will be updated according toohello following steps:</span></span>

1. <span data-ttu-id="3984d-118">Mettre à jour les paramètres de configuration d’application hello dans HelloKeyVault\App.config avec votre URL du coffre, un ID d’application principal et un secret.</span><span class="sxs-lookup"><span data-stu-id="3984d-118">Update hello app configuration settings in HelloKeyVault\App.config with your vault URL, application principal ID, and secret.</span></span> <span data-ttu-id="3984d-119">informations de Hello peuvent également être générées à l’aide de **scripts\GetAppConfigSettings.ps1**.</span><span class="sxs-lookup"><span data-stu-id="3984d-119">hello information can optionally be generated using **scripts\GetAppConfigSettings.ps1**.</span></span>
2. <span data-ttu-id="3984d-120">Mettre à jour les valeurs hello des variables obligatoire de hello dans GetAppConfigSettings.ps1.</span><span class="sxs-lookup"><span data-stu-id="3984d-120">Update hello values of hello mandatory variables in GetAppConfigSettings.ps1.</span></span>
3. <span data-ttu-id="3984d-121">Lancez la fenêtre Windows PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="3984d-121">Launch hello Windows PowerShell window.</span></span>
4. <span data-ttu-id="3984d-122">Exécutez le script de GetAppConfigSettings.ps1 de hello dans la fenêtre de PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="3984d-122">Run hello GetAppConfigSettings.ps1 script within hello PowerShell window.</span></span>
5. <span data-ttu-id="3984d-123">Copier les résultats hello hello toohello HelloKeyVault\App.config du fichier de script.</span><span class="sxs-lookup"><span data-stu-id="3984d-123">Copy hello results of hello script toohello HelloKeyVault\App.config file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3984d-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3984d-124">Next steps</span></span>
[<span data-ttu-id="3984d-125">Déployer une machine virtuelle avec un mot de passe Key Vault</span><span class="sxs-lookup"><span data-stu-id="3984d-125">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)

[<span data-ttu-id="3984d-126">Déployer une machine virtuelle avec un certificat Key Vault</span><span class="sxs-lookup"><span data-stu-id="3984d-126">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

