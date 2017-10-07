---
title: "aaaManage Azure Key Vault à l’aide de CLI | Documents Microsoft"
description: "Utilisez ce didacticiel tooautomate des tâches courantes dans le coffre de clés à l’aide de hello CLI 2.0"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ambapat
ms.openlocfilehash: 76855c0ea09b6b307159468382a6a63627205556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli-20"></a><span data-ttu-id="cbc6f-103">Gestion de Key Vault à l’aide de l’interface de ligne de commande (CLI) 2.0</span><span class="sxs-lookup"><span data-stu-id="cbc6f-103">Manage Key Vault using CLI 2.0</span></span>
<span data-ttu-id="cbc6f-104">Azure Key Vault est disponible dans la plupart des régions.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="cbc6f-105">Pour plus d’informations, consultez hello [page de tarification de coffre de clés](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="cbc6f-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="cbc6f-106">Introduction</span><span class="sxs-lookup"><span data-stu-id="cbc6f-106">Introduction</span></span>
<span data-ttu-id="cbc6f-107">Utilisez ce didacticiel toohelp que vous obtenez en main d’Azure Key Vault toocreate un conteneur renforcé (un coffre) dans Azure, toostore et gérer les clés de chiffrement et les clés secrètes dans Azure.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-107">Use this tutorial toohelp you get started with Azure Key Vault toocreate a hardened container (a vault) in Azure, toostore and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="cbc6f-108">Il vous guide tout au long des processus de hello d’à l’aide d’une Interface de ligne multiplateforme Azure toocreate un coffre qui contient une clé ou un mot de passe que vous pouvez ensuite utiliser avec une application Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-108">It walks you through hello process of using Azure Cross-Platform Command-Line Interface toocreate a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="cbc6f-109">Il vous montre également comment une application peut ensuite utiliser cette clé ou ce mot de passe.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="cbc6f-110">**Estimation du temps toocomplete :** 20 minutes</span><span class="sxs-lookup"><span data-stu-id="cbc6f-110">**Estimated time toocomplete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="cbc6f-111">Ce didacticiel n’inclut pas d’obtenir des instructions sur la façon dont toowrite hello Azure application incluant une des étapes de hello, qui montre comment tooauthorize un toouse application une clé ou au secret dans la clé de hello coffre.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-111">This tutorial does not include instructions on how toowrite hello Azure application that one of hello steps includes, which shows how tooauthorize an application toouse a key or secret in hello key vault.</span></span>
>
> <span data-ttu-id="cbc6f-112">Ce didacticiel utilise hello dernière Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-112">This tutorial uses hello latest Azure CLI 2.0.</span></span>
>
>

<span data-ttu-id="cbc6f-113">Pour plus d’informations générales sur Azure Key Vault, consultez la page [Présentation d’Azure Key Vault](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="cbc6f-113">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbc6f-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="cbc6f-114">Prerequisites</span></span>
<span data-ttu-id="cbc6f-115">toocomplete ce didacticiel, vous devez avoir hello suivant :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-115">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="cbc6f-116">Un abonnement tooMicrosoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-116">A subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="cbc6f-117">Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/pricing/free-trial)dès aujourd’hui.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-117">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="cbc6f-118">Interface de ligne de commande Azure, version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-118">Command-Line Interface version 2.0 or later.</span></span> <span data-ttu-id="cbc6f-119">tooinstall hello version la plus récente et se connecter tooyour abonnement Azure, consultez [installer et configurer hello une Interface de ligne de Cross-Platform Azure 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cbc6f-119">tooinstall hello latest version and connect tooyour Azure subscription, see [Install and Configure hello Azure Cross-Platform Command-Line Interface 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="cbc6f-120">Une application qui sera la clé de hello toouse configuré ou le mot de passe que vous créez dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-120">An application that will be configured toouse hello key or password that you create in this tutorial.</span></span> <span data-ttu-id="cbc6f-121">Un exemple d’application est disponible à partir de hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="cbc6f-121">A sample application is available from hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="cbc6f-122">Pour obtenir des instructions, consultez hello qui accompagne le fichier Lisez-moi.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-122">For instructions, see hello accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="cbc6f-123">Obtention d’aide avec l’interface de ligne de commande interplateforme Azure</span><span class="sxs-lookup"><span data-stu-id="cbc6f-123">Getting help with Azure Cross-Platform Command-Line Interface</span></span>
<span data-ttu-id="cbc6f-124">Ce didacticiel suppose que vous êtes familiarisé avec une interface de ligne hello (interpréteur de commandes, Terminal Server, invite de commandes)</span><span class="sxs-lookup"><span data-stu-id="cbc6f-124">This tutorial assumes that you are familiar with hello command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="cbc6f-125">Hello--help ou-h paramètre peut être utilisé tooview aide pour des commandes spécifiques.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-125">hello --help or -h parameter can be used tooview help for specific commands.</span></span> <span data-ttu-id="cbc6f-126">Ou bien, l’aide hello azure [commande] [options] format peut également être utilisé tooreturn hello mêmes informations.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-126">Alternately, hello azure help [command] [options] format can also be used tooreturn hello same information.</span></span> <span data-ttu-id="cbc6f-127">Par exemple, suivant de hello commandes retournent tous les hello les mêmes informations :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-127">For example, hello following commands all return hello same information:</span></span>

```
az account set --help
az account set -h
```

<span data-ttu-id="cbc6f-128">En cas de doute sur les paramètres de hello requis par une commande, reportez-vous à l’aide de toohelp--help, -h ou az help [commande].</span><span class="sxs-lookup"><span data-stu-id="cbc6f-128">When in doubt about hello parameters needed by a command, refer toohelp using --help, -h or az help [command].</span></span>

<span data-ttu-id="cbc6f-129">Vous pouvez également lire hello suivant tooget didacticiels familiarisé avec Azure Resource Manager dans une Interface de ligne multiplateforme Azure :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-129">You can also read hello following tutorials tooget familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="cbc6f-130">Installation de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="cbc6f-130">Install Azure CLI</span></span>](/cli/azure/install-azure-cli)
* [<span data-ttu-id="cbc6f-131">Prise en main d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="cbc6f-131">Get started with Azure CLI 2.0</span></span>](/cli/azure/get-started-with-azure-cli)

## <a name="connect-tooyour-subscriptions"></a><span data-ttu-id="cbc6f-132">Se connecter tooyour abonnements</span><span class="sxs-lookup"><span data-stu-id="cbc6f-132">Connect tooyour subscriptions</span></span>
<span data-ttu-id="cbc6f-133">toolog à l’aide d’un compte professionnel, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-133">toolog in using an organizational account, use hello following command:</span></span>

```
az login -u username@domain.com -p password
```

<span data-ttu-id="cbc6f-134">ou si vous voulez toolog en tapant de manière interactive</span><span class="sxs-lookup"><span data-stu-id="cbc6f-134">or if you want toolog in by typing interactively</span></span>

```
az login
```

<span data-ttu-id="cbc6f-135">Si vous avez plusieurs abonnements et que vous souhaitez toospecify un un toouse spécifique pour Azure Key Vault, tapez Bonjour suivant toosee les abonnements de hello pour votre compte :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-135">If you have multiple subscriptions and want toospecify a specific one toouse for Azure Key Vault, type hello following toosee hello subscriptions for your account:</span></span>

```
az account list
```

<span data-ttu-id="cbc6f-136">Ensuite, toospecify hello abonnement toouse, type :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-136">Then, toospecify hello subscription toouse, type:</span></span>

```
az account set --subscription <subscription name or ID>
```

<span data-ttu-id="cbc6f-137">Pour plus d’informations sur la configuration de l’interface de ligne de commande multiplateforme Azure, consultez la page [Installation de l’interface de ligne de commande multiplateforme Azure](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cbc6f-137">For more information about configuring Azure Cross-Platform Command-Line Interface, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-new-resource-group"></a><span data-ttu-id="cbc6f-138">Création d’un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="cbc6f-138">Create a new resource group</span></span>
<span data-ttu-id="cbc6f-139">Lorsque vous utilisez Azure Resource Manager, toutes les ressources associées sont créées au sein d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-139">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="cbc6f-140">Nous allons créer un groupe de ressources nommé « ContosoResourceGroup » pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-140">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

<span data-ttu-id="cbc6f-141">premier paramètre de Hello est le nom de groupe de ressources et hello deuxième paramètre est emplacement de hello.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-141">hello first parameter is resource group name and hello second parameter is hello location.</span></span> <span data-ttu-id="cbc6f-142">Pour l’emplacement, utilisez la commande hello `az account list-locations` tooidentify comment toospecify un autre emplacement toohello un dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-142">For location, use hello command `az account list-locations` tooidentify how toospecify an alternative location toohello one in this example.</span></span> <span data-ttu-id="cbc6f-143">Si vous avez besoin de plus d’informations, tapez : `az account list-locations -h`.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-143">If you need more information, type: `az account list-locations -h`.</span></span>

## <a name="register-hello-key-vault-resource-provider"></a><span data-ttu-id="cbc6f-144">Inscrire le fournisseur de ressources hello coffre de clés</span><span class="sxs-lookup"><span data-stu-id="cbc6f-144">Register hello Key Vault resource provider</span></span>
<span data-ttu-id="cbc6f-145">Assurez-vous que le fournisseur de ressources Key Vault est inscrit dans votre abonnement :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-145">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

```
az provider register -n Microsoft.KeyVault
```

<span data-ttu-id="cbc6f-146">Cette opération ne doit toobe réalisée une fois par abonnement.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-146">This only needs toobe done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="cbc6f-147">Création d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="cbc6f-147">Create a key vault</span></span>
<span data-ttu-id="cbc6f-148">Hello d’utilisation `az keyvault create` commande toocreate un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-148">Use hello `az keyvault create` command toocreate a key vault.</span></span> <span data-ttu-id="cbc6f-149">Ce script a trois paramètres obligatoires : un nom de groupe de ressources, d’un coffre de clés et d’un emplacement géographique de hello.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-149">This script has three mandatory parameters: a resource group name, a key vault name, and hello geographic location.</span></span>

<span data-ttu-id="cbc6f-150">Par exemple, si vous utilisez le nom du coffre hello de ContosoKeyVault, nom de groupe de ressources hello de ContosoResourceGroup et l’emplacement de hello d’Asie orientale, tapez :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-150">For example, if you use hello vault name of ContosoKeyVault, hello resource group name of ContosoResourceGroup, and hello location of East Asia, type:</span></span>
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

<span data-ttu-id="cbc6f-151">sortie Hello de cette commande affiche les propriétés du coffre de clés hello que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-151">hello output of this command shows properties of hello key vault that you've just created.</span></span> <span data-ttu-id="cbc6f-152">propriétés les plus importantes Hello deux sont :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-152">hello two most important properties are:</span></span>

* <span data-ttu-id="cbc6f-153">**nom**: dans l’exemple de hello, cela est ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-153">**name**: In hello example this is ContosoKeyVault.</span></span> <span data-ttu-id="cbc6f-154">Vous allez utiliser ce nom pour les autres commandes Key Vault.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-154">You will use this name for other Key Vault commands.</span></span>
* <span data-ttu-id="cbc6f-155">**vaultUri**: dans l’exemple de hello, cela est https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-155">**vaultUri**: In hello example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="cbc6f-156">Les applications qui utilisent votre coffre via son API REST doivent utiliser cet URI.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-156">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="cbc6f-157">Votre compte Azure est désormais toutes les opérations sur cette clé de coffre tooperform autorisé.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-157">Your Azure account is now authorized tooperform any operations on this key vault.</span></span> <span data-ttu-id="cbc6f-158">coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-158">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-toohello-key-vault"></a><span data-ttu-id="cbc6f-159">Ajouter une clé ou un coffre de clés secrètes toohello</span><span class="sxs-lookup"><span data-stu-id="cbc6f-159">Add a key or secret toohello key vault</span></span>
<span data-ttu-id="cbc6f-160">Si vous souhaitez que le coffre de clés Azure toocreate une clé protégée par logiciel pour vous, utilisez hello `az key create` de commandes et tapez Bonjour qui suit :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-160">If you want Azure Key Vault toocreate a software-protected key for you, use hello `az key create` command, and type hello following:</span></span>
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
<span data-ttu-id="cbc6f-161">Toutefois, si vous avez une clé existante dans un fichier .pem enregistré en tant que fichier local dans un fichier nommé softkey.pem que vous souhaitez tooupload tooAzure le coffre de clés, tapez Bonjour suivant clé de hello tooimport hello. Fichier PEM, qui protège la clé de hello par logiciel dans hello service Key Vault :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-161">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want tooupload tooAzure Key Vault, type hello following tooimport hello key from hello .PEM file, which protects hello key by software in hello Key Vault service:</span></span>
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
<span data-ttu-id="cbc6f-162">Vous pouvez maintenant référencer clé hello que vous avez créé ou téléchargé tooAzure le coffre de clés, à l’aide de son URI.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-162">You can now reference hello key that you created or uploaded tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="cbc6f-163">Utilisez **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways obtenir la version actuelle de hello et utiliser **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget cette version spécifique.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-163">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways get hello current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget this specific version.</span></span>

<span data-ttu-id="cbc6f-164">tooadd un coffre toohello secrète, qui est un mot de passe nommé SQLPassword et qui a valeur hello Pa$ $w0rd tooAzure le coffre de clés, hello du type suivant :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-164">tooadd a secret toohello vault, which is a password named SQLPassword and that has hello value of Pa$$w0rd tooAzure Key Vault, type hello following:</span></span>
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
<span data-ttu-id="cbc6f-165">Vous pouvez maintenant référencer ce mot de passe que vous avez ajouté tooAzure le coffre de clés, à l’aide de son URI.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-165">You can now reference this password that you added tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="cbc6f-166">Utilisez **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways obtenir la version actuelle de hello et utiliser **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget cette version spécifique.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-166">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways get hello current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget this specific version.</span></span>

<span data-ttu-id="cbc6f-167">Examinons la clé de hello ou le secret que vous venez de créer :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-167">Let's view hello key or secret that you just created:</span></span>

* <span data-ttu-id="cbc6f-168">tooview votre type de clé, :`az keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="cbc6f-168">tooview your key, type: `az keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="cbc6f-169">tooview votre secret principal, type :`az keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="cbc6f-169">tooview your secret, type: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="cbc6f-170">Inscription d’une application auprès d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cbc6f-170">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="cbc6f-171">Cette étape est généralement effectuée par un développeur et sur un ordinateur distinct.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-171">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="cbc6f-172">Il n’est pas spécifique tooAzure le coffre de clés, mais est inclus ici, par souci d’exhaustivité.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-172">It is not specific tooAzure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbc6f-173">didacticiel de hello toocomplete, votre compte, le coffre de hello et l’application hello que vous inscrivez dans cette étape doivent toutes être Bonjour même annuaire Azure.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-173">toocomplete hello tutorial, your account, hello vault, and hello application that you will register in this step must all be in hello same Azure directory.</span></span>
>
>

<span data-ttu-id="cbc6f-174">Les applications qui utilisent un coffre de clés doivent s’authentifier à l’aide d’un jeton à partir d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-174">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="cbc6f-175">toodo, hello propriétaire de l’application hello doit inscrire tout d’abord des application hello dans leur annuaire Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-175">toodo this, hello owner of hello application must first register hello application in their Azure Active Directory.</span></span> <span data-ttu-id="cbc6f-176">À fin hello d’enregistrement, le propriétaire de l’application hello obtient hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-176">At hello end of registration, hello application owner gets hello following values:</span></span>

* <span data-ttu-id="cbc6f-177">Un **ID d’Application** (également appelé ID de Client) et **clé d’authentification** (également appelé un secret partagé hello).</span><span class="sxs-lookup"><span data-stu-id="cbc6f-177">An **Application ID** (also known as a Client ID) and **authentication key** (also known as hello shared secret).</span></span> <span data-ttu-id="cbc6f-178">application Hello doit présenter les deux de ces valeurs de tooAzure Active Directory, tooget un jeton.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-178">hello application must present both of these values tooAzure Active Directory, tooget a token.</span></span> <span data-ttu-id="cbc6f-179">Comment application hello est configuré toodo que cela dépend application hello.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-179">How hello application is configured toodo this depends on hello application.</span></span> <span data-ttu-id="cbc6f-180">Pour un exemple d’application le coffre de clés de hello, le propriétaire de l’application hello définit ces valeurs dans le fichier app.config hello.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-180">For hello Key Vault sample application, hello application owner sets these values in hello app.config file.</span></span>

<span data-ttu-id="cbc6f-181">application hello tooregister dans Azure Active Directory :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-181">tooregister hello application in Azure Active Directory:</span></span>

1. <span data-ttu-id="cbc6f-182">Se connecter toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-182">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="cbc6f-183">Sur hello gauche, cliquez sur **Azure Active Directory**, puis sélectionnez le répertoire hello dans lequel vous allez inscrire votre application.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-183">On hello left, click **Azure Active Directory**, and then select hello directory in which you will register your application.</span></span> <br> <br> 

> [!Note] 
> <span data-ttu-id="cbc6f-184">Vous devez sélectionner hello même répertoire contienne hello abonnement Azure avec lequel vous avez créé votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-184">You must select hello same directory that contains hello Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="cbc6f-185">Si vous ne savez pas quel répertoire cela est, cliquez sur **paramètres**, d’identifier l’abonnement hello avec lequel vous avez créé votre coffre de clés et nom de hello note du répertoire de hello affiché dans la dernière colonne de hello.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-185">If you do not know which directory this is, click **Settings**, identify hello subscription with which you created your key vault, and note hello name of hello directory displayed in hello last column.</span></span>

3. <span data-ttu-id="cbc6f-186">Cliquez sur **APPLICATIONS**.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-186">Click **APPLICATIONS**.</span></span> <span data-ttu-id="cbc6f-187">Si aucune application n’a été ajoutée tooyour active, cette page affiche uniquement hello **ajouter une application** lien.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-187">If no apps have been added tooyour directory, this page will show only hello **Add an App** link.</span></span> <span data-ttu-id="cbc6f-188">Cliquez sur le lien de hello, ou vous pouvez également cliquer hello **ajouter** sur la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-188">Click hello link, or alternatively, you can click hello **ADD** on hello command bar.</span></span>
4. <span data-ttu-id="cbc6f-189">Bonjour **ajouter une APPLICATION** Assistant, sur hello **comment vous souhaitez toodo ?** , cliquez sur **ajouter une application développée par mon organisation**.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-189">In hello **ADD APPLICATION** wizard, on hello **What do you want toodo?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="cbc6f-190">Sur hello **Parlez-nous de votre application** page, spécifiez un nom pour votre application et sélectionnez **WEB APPLICATION et/ou API WEB** (hello par défaut).</span><span class="sxs-lookup"><span data-stu-id="cbc6f-190">On hello **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (hello default).</span></span> <span data-ttu-id="cbc6f-191">Cliquez sur icône suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-191">Click hello Next icon.</span></span>
6. <span data-ttu-id="cbc6f-192">Sur hello **propriétés de l’application** , spécifiez hello **URL de connexion** et **URI ID d’application** pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-192">On hello **App properties** page, specify hello **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="cbc6f-193">Si votre application n’a pas ces valeurs, vous pouvez les créer pour cette étape (par exemple, vous pouvez spécifier http://test1.contoso.com pour les deux zones).</span><span class="sxs-lookup"><span data-stu-id="cbc6f-193">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="cbc6f-194">Il n’a pas d’importance s’il existe de ces sites ; l’essentiel est que URI ID d’application hello pour chaque application est différente pour chaque application dans votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-194">It does not matter if these sites exist; what is important is that hello app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="cbc6f-195">répertoire de Hello utilise tooidentify de cette chaîne de votre application.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-195">hello directory uses this string tooidentify your app.</span></span>
7. <span data-ttu-id="cbc6f-196">Cliquez sur hello icône terminée toosave vos modifications dans l’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-196">Click hello Complete icon toosave your changes in hello wizard.</span></span>
8. <span data-ttu-id="cbc6f-197">Dans la page de démarrage rapide de hello, cliquez sur **configurer**.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-197">On hello Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="cbc6f-198">Faites défiler toohello **clés** section, sélectionnez la durée de hello, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-198">Scroll toohello **keys** section, select hello duration, and then click **SAVE**.</span></span> <span data-ttu-id="cbc6f-199">page de Hello actualise et affiche maintenant une valeur de clé.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-199">hello page refreshes and now shows a key value.</span></span> <span data-ttu-id="cbc6f-200">Vous devez configurer votre application avec cette valeur de clé et le hello **ID CLIENT** valeur.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-200">You must configure your application with this key value and hello **CLIENT ID** value.</span></span> <span data-ttu-id="cbc6f-201">(Les instructions relatives à cette configuration sont propres à l’application).</span><span class="sxs-lookup"><span data-stu-id="cbc6f-201">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="cbc6f-202">Copiez la valeur d’ID client hello à partir de cette page, vous allez utiliser dans hello prochaine étape tooset des autorisations sur votre coffre.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-202">Copy hello client ID value from this page, which you will use in hello next step tooset permissions on your vault.</span></span>

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a><span data-ttu-id="cbc6f-203">Autoriser hello application toouse hello clé ou le secret</span><span class="sxs-lookup"><span data-stu-id="cbc6f-203">Authorize hello application toouse hello key or secret</span></span>
<span data-ttu-id="cbc6f-204">tooauthorize hello application tooaccess hello clé ou le secret de coffre hello, utilisez hello `az keyvault set-policy` commande.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-204">tooauthorize hello application tooaccess hello key or secret in hello vault, use hello `az keyvault set-policy` command.</span></span>

<span data-ttu-id="cbc6f-205">Par exemple, si votre nom de coffre est ContosoKeyVault et hello application souhaité tooauthorize a l’ID client 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, et que vous souhaitez tooauthorize hello application toodecrypt et connectez-vous avec des clés dans le coffre, puis exécutez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-205">For example, if your vault name is ContosoKeyVault and hello application you want tooauthorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want tooauthorize hello application toodecrypt and sign with keys in your vault, then run hello following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

<span data-ttu-id="cbc6f-206">Si vous souhaitez tooauthorize que secrets de tooread même application dans le coffre, exécutez suivante de hello :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-206">If you want tooauthorize that same application tooread secrets in your vault, run hello following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a><span data-ttu-id="cbc6f-207">Si vous voulez toouse un module de sécurité matériel (HSM)</span><span class="sxs-lookup"><span data-stu-id="cbc6f-207">If you want toouse a hardware security module (HSM)</span></span>
<span data-ttu-id="cbc6f-208">Pour plus de sûreté, vous pouvez importer ou générer des clés dans les modules de sécurité matériel (HSM) qui ne quittent jamais les limites HSM hello.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-208">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="cbc6f-209">Hello HSM sont FIPS 140-2 niveau 2 validé.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-209">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="cbc6f-210">Si cette exigence ne s’applique pas tooyou, ignorez cette section et passez trop[supprimer le coffre de clés hello et les clés associées et les secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="cbc6f-210">If this requirement doesn't apply tooyou, skip this section and go too[Delete hello key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="cbc6f-211">toocreate ces clés protégées par HSM, vous devez avoir un abonnement de coffre qui prend en charge les clés protégées par HSM.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-211">toocreate these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="cbc6f-212">Lorsque vous créez hello keyvault, ajouter le paramètre de 'sku' hello :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-212">When you create hello keyvault, add hello 'sku' parameter:</span></span>

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
<span data-ttu-id="cbc6f-213">Vous pouvez ajouter des clés protégées par le logiciel (comme indiqué plus haut) et de coffre de clés protégées par HSM toothis.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-213">You can add software-protected keys (as shown earlier) and HSM-protected keys toothis vault.</span></span> <span data-ttu-id="cbc6f-214">toocreate une clé protégée par HSM, jeu hello Destination paramètre too'HSM':</span><span class="sxs-lookup"><span data-stu-id="cbc6f-214">toocreate an HSM-protected key, set hello Destination parameter too'HSM':</span></span>

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

<span data-ttu-id="cbc6f-215">Vous pouvez utiliser hello suivant commande tooimport une clé à partir d’un fichier .pem sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-215">You can use hello following command tooimport a key from a .pem file on your computer.</span></span> <span data-ttu-id="cbc6f-216">Cette commande importe la clé de hello dans les modules HSM Bonjour service Key Vault :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-216">This command imports hello key into HSMs in hello Key Vault service:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
<span data-ttu-id="cbc6f-217">commande suivant Hello importe un « apportez votre propre clé » package (BYOK).</span><span class="sxs-lookup"><span data-stu-id="cbc6f-217">hello next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="cbc6f-218">Cela vous permet de générer votre clé dans votre HSM local et la transférez tooHSMs Bonjour service Key Vault, sans clé hello en laissant la limite HSM hello :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-218">This lets you generate your key in your local HSM, and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
<span data-ttu-id="cbc6f-219">Pour plus d’instructions sur la procédure toogenerate ce package BYOK, consultez [comment toouse clés HSM-Protected avec Azure Key Vault](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="cbc6f-219">For more detailed instructions about how toogenerate this BYOK package, see [How toouse HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="cbc6f-220">Supprimer le coffre de clés hello et les clés associées et les secrets</span><span class="sxs-lookup"><span data-stu-id="cbc6f-220">Delete hello key vault and associated keys and secrets</span></span>
<span data-ttu-id="cbc6f-221">Si vous n’avez plus besoin coffre de clés hello et clé de hello ou le secret qu’il contient, vous pouvez supprimer le coffre de clés hello à l’aide de hello `az keyvault delete` commande :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-221">If you no longer need hello key vault and hello key or secret that it contains, you can delete hello key vault by using hello `az keyvault delete` command:</span></span>

```
az keyvault delete --name 'ContosoKeyVault'
```

<span data-ttu-id="cbc6f-222">Ou bien, vous pouvez supprimer un groupe de ressources Azure entier, ce qui inclut le coffre de clés hello et d’autres ressources que vous avez incluses dans ce groupe :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-222">Or, you can delete an entire Azure resource group, which includes hello key vault and any other resources that you included in that group:</span></span>

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="cbc6f-223">Autres interfaces de ligne de commande interplateformes Azure</span><span class="sxs-lookup"><span data-stu-id="cbc6f-223">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="cbc6f-224">Autres commandes qui peuvent être utiles pour la gestion d’Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-224">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="cbc6f-225">Cette commande permet d’obtenir un affichage sous forme de tableau de l’ensemble des clés et des propriétés sélectionnées :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-225">This command lists a tabular display of all keys and selected properties:</span></span>

<span data-ttu-id="cbc6f-226">az keyvault key list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="cbc6f-226">az keyvault key list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="cbc6f-227">Cette commande affiche une liste complète des propriétés de clé spécifiée de hello :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-227">This command displays a full list of properties for hello specified key:</span></span>

<span data-ttu-id="cbc6f-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="cbc6f-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="cbc6f-229">Cette commande permet d’obtenir un affichage sous forme de tableau de l’ensemble des secrets et des propriétés sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="cbc6f-229">This command lists a tabular display of all secret names and selected properties:</span></span>

<span data-ttu-id="cbc6f-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="cbc6f-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="cbc6f-231">Voici un exemple de procédure tooremove une clé spécifique :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-231">Here's an example of how tooremove a specific key:</span></span>

<span data-ttu-id="cbc6f-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="cbc6f-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="cbc6f-233">Voici un exemple de procédure tooremove un secret spécifique :</span><span class="sxs-lookup"><span data-stu-id="cbc6f-233">Here's an example of how tooremove a specific secret:</span></span>

<span data-ttu-id="cbc6f-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span><span class="sxs-lookup"><span data-stu-id="cbc6f-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span></span>


## <a name="next-steps"></a><span data-ttu-id="cbc6f-235">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cbc6f-235">Next steps</span></span>
<span data-ttu-id="cbc6f-236">Pour accéder à une documentation de référence complète sur l’interface Azure CLI pour les commandes Key Vault, consultez le document de [référence sur l’interface de ligne de commande Key Vault](/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="cbc6f-236">For complete Azure CLI reference for key vault commands, see [Key Vault CLI reference](/cli/azure/keyvault)</span></span>

<span data-ttu-id="cbc6f-237">Pour les références de programmation, consultez [hello guide du développeur Azure Key Vault](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="cbc6f-237">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>
