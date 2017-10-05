---
title: "Gestion de Azure Key Vault à l’aide de l’interface de ligne de commande (CLI) | Microsoft Docs"
description: "Utilisez ce tutoriel pour automatiser les tâches courantes dans Key Vault à l’aide de l’interface de ligne de commande CLI 2.0"
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
ms.openlocfilehash: 5da9f5eceda71ac85259193e0f183c72813e1679
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-key-vault-using-cli-20"></a><span data-ttu-id="84139-103">Gestion de Key Vault à l’aide de l’interface de ligne de commande (CLI) 2.0</span><span class="sxs-lookup"><span data-stu-id="84139-103">Manage Key Vault using CLI 2.0</span></span>
<span data-ttu-id="84139-104">Azure Key Vault est disponible dans la plupart des régions.</span><span class="sxs-lookup"><span data-stu-id="84139-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="84139-105">Pour plus d’informations, consultez la [page de tarification de Key Vault](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="84139-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="84139-106">Introduction</span><span class="sxs-lookup"><span data-stu-id="84139-106">Introduction</span></span>
<span data-ttu-id="84139-107">Ce didacticiel vous aide à démarrer avec Azure Key Vault pour créer un conteneur renforcé (un coffre) dans Azure afin de stocker et gérer les clés de chiffrement et les secrets dans Azure.</span><span class="sxs-lookup"><span data-stu-id="84139-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="84139-108">Il vous guide tout au long du processus d’utilisation de l’interface de ligne de commande interplateforme Azure pour créer un coffre qui contient une clé ou un mot de passe que vous pouvez ensuite utiliser avec une application Azure.</span><span class="sxs-lookup"><span data-stu-id="84139-108">It walks you through the process of using Azure Cross-Platform Command-Line Interface to create a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="84139-109">Il vous montre également comment une application peut ensuite utiliser cette clé ou ce mot de passe.</span><span class="sxs-lookup"><span data-stu-id="84139-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="84139-110">**Durée estimée :** 20 minutes</span><span class="sxs-lookup"><span data-stu-id="84139-110">**Estimated time to complete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="84139-111">Ce didacticiel n’inclut pas d’instructions sur l’écriture de l’application Azure abordée dans une des étapes, qui montre comment autoriser une application à utiliser une clé ou un secret dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="84139-111">This tutorial does not include instructions on how to write the Azure application that one of the steps includes, which shows how to authorize an application to use a key or secret in the key vault.</span></span>
>
> <span data-ttu-id="84139-112">Ce tutoriel utilise la dernière version d’Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="84139-112">This tutorial uses the latest Azure CLI 2.0.</span></span>
>
>

<span data-ttu-id="84139-113">Pour plus d’informations générales sur Azure Key Vault, consultez la page [Présentation d’Azure Key Vault](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="84139-113">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84139-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="84139-114">Prerequisites</span></span>
<span data-ttu-id="84139-115">Pour suivre ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="84139-115">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="84139-116">Un abonnement Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="84139-116">A subscription to Microsoft Azure.</span></span> <span data-ttu-id="84139-117">Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/pricing/free-trial)dès aujourd’hui.</span><span class="sxs-lookup"><span data-stu-id="84139-117">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="84139-118">Interface de ligne de commande Azure, version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="84139-118">Command-Line Interface version 2.0 or later.</span></span> <span data-ttu-id="84139-119">Pour installer la dernière version et l’associer à votre abonnement Azure, consultez la page [Installation et configuration de l’interface de ligne de commande multiplateforme Azure 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="84139-119">To install the latest version and connect to your Azure subscription, see [Install and Configure the Azure Cross-Platform Command-Line Interface 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="84139-120">Une application configurée pour utiliser la clé ou le mot de passe que vous créez dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="84139-120">An application that will be configured to use the key or password that you create in this tutorial.</span></span> <span data-ttu-id="84139-121">Un exemple d’application est disponible dans le [Centre de téléchargement Microsoft](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="84139-121">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="84139-122">Pour obtenir des instructions, consultez le fichier Lisez-moi fourni.</span><span class="sxs-lookup"><span data-stu-id="84139-122">For instructions, see the accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="84139-123">Obtention d’aide avec l’interface de ligne de commande interplateforme Azure</span><span class="sxs-lookup"><span data-stu-id="84139-123">Getting help with Azure Cross-Platform Command-Line Interface</span></span>
<span data-ttu-id="84139-124">Ce didacticiel suppose que vous êtes familiarisé avec l’interface de ligne de commande (Bash, Terminal, invite de commandes)</span><span class="sxs-lookup"><span data-stu-id="84139-124">This tutorial assumes that you are familiar with the command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="84139-125">Le paramètre --help ou -h peut être utilisé pour afficher l'aide relative à des commandes particulières.</span><span class="sxs-lookup"><span data-stu-id="84139-125">The --help or -h parameter can be used to view help for specific commands.</span></span> <span data-ttu-id="84139-126">Le format azure help [commande] [options] permet également de renvoyer les mêmes informations.</span><span class="sxs-lookup"><span data-stu-id="84139-126">Alternately, The azure help [command] [options] format can also be used to return the same information.</span></span> <span data-ttu-id="84139-127">Les commandes suivantes, par exemple, renvoient les mêmes informations :</span><span class="sxs-lookup"><span data-stu-id="84139-127">For example, the following commands all return the same information:</span></span>

```
az account set --help
az account set -h
```

<span data-ttu-id="84139-128">Si vous avez des doutes sur les paramètres exigés par une commande, reportez-vous à l'aide en utilisant --help, -h ou az help [commande].</span><span class="sxs-lookup"><span data-stu-id="84139-128">When in doubt about the parameters needed by a command, refer to help using --help, -h or az help [command].</span></span>

<span data-ttu-id="84139-129">Consultez également les didacticiels suivants afin de vous familiariser avec Azure Resource Manager dans l’interface de ligne de commande interplateforme Azure :</span><span class="sxs-lookup"><span data-stu-id="84139-129">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="84139-130">Installation de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="84139-130">Install Azure CLI</span></span>](/cli/azure/install-azure-cli)
* [<span data-ttu-id="84139-131">Prise en main d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="84139-131">Get started with Azure CLI 2.0</span></span>](/cli/azure/get-started-with-azure-cli)

## <a name="connect-to-your-subscriptions"></a><span data-ttu-id="84139-132">Connexion à vos abonnements</span><span class="sxs-lookup"><span data-stu-id="84139-132">Connect to your subscriptions</span></span>
<span data-ttu-id="84139-133">Pour vous connecter avec un compte professionnel, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="84139-133">To log in using an organizational account, use the following command:</span></span>

```
az login -u username@domain.com -p password
```

<span data-ttu-id="84139-134">ou si vous voulez vous connecter en tapant de façon interactive</span><span class="sxs-lookup"><span data-stu-id="84139-134">or if you want to log in by typing interactively</span></span>

```
az login
```

<span data-ttu-id="84139-135">Si vous disposez de plusieurs abonnements et que vous souhaitez spécifier un abonnement spécifique à utiliser pour Azure Key Vault, tapez la commande suivante pour afficher les abonnements de votre compte :</span><span class="sxs-lookup"><span data-stu-id="84139-135">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span></span>

```
az account list
```

<span data-ttu-id="84139-136">Ensuite, pour indiquer l’abonnement, tapez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="84139-136">Then, to specify the subscription to use, type:</span></span>

```
az account set --subscription <subscription name or ID>
```

<span data-ttu-id="84139-137">Pour plus d’informations sur la configuration de l’interface de ligne de commande multiplateforme Azure, consultez la page [Installation de l’interface de ligne de commande multiplateforme Azure](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="84139-137">For more information about configuring Azure Cross-Platform Command-Line Interface, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-new-resource-group"></a><span data-ttu-id="84139-138">Création d’un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="84139-138">Create a new resource group</span></span>
<span data-ttu-id="84139-139">Lorsque vous utilisez Azure Resource Manager, toutes les ressources associées sont créées au sein d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="84139-139">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="84139-140">Nous allons créer un groupe de ressources nommé « ContosoResourceGroup » pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="84139-140">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

<span data-ttu-id="84139-141">Le premier paramètre est le nom de groupe de ressources et le deuxième paramètre est l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="84139-141">The first parameter is resource group name and the second parameter is the location.</span></span> <span data-ttu-id="84139-142">Pour l’emplacement, utilisez la commande `az account list-locations` pour savoir comment spécifier un autre emplacement que celui de cet exemple.</span><span class="sxs-lookup"><span data-stu-id="84139-142">For location, use the command `az account list-locations` to identify how to specify an alternative location to the one in this example.</span></span> <span data-ttu-id="84139-143">Si vous avez besoin de plus d’informations, tapez : `az account list-locations -h`.</span><span class="sxs-lookup"><span data-stu-id="84139-143">If you need more information, type: `az account list-locations -h`.</span></span>

## <a name="register-the-key-vault-resource-provider"></a><span data-ttu-id="84139-144">Inscription du fournisseur de ressources Key Vault</span><span class="sxs-lookup"><span data-stu-id="84139-144">Register the Key Vault resource provider</span></span>
<span data-ttu-id="84139-145">Assurez-vous que le fournisseur de ressources Key Vault est inscrit dans votre abonnement :</span><span class="sxs-lookup"><span data-stu-id="84139-145">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

```
az provider register -n Microsoft.KeyVault
```

<span data-ttu-id="84139-146">Cette opération ne doit être effectuée qu'une fois par abonnement.</span><span class="sxs-lookup"><span data-stu-id="84139-146">This only needs to be done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="84139-147">Création d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="84139-147">Create a key vault</span></span>
<span data-ttu-id="84139-148">Utilisez la commande `az keyvault create` pour créer un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="84139-148">Use the `az keyvault create` command to create a key vault.</span></span> <span data-ttu-id="84139-149">Ce script a trois paramètres obligatoires : un nom de groupe de ressources, un nom de coffre de clés et l’emplacement géographique.</span><span class="sxs-lookup"><span data-stu-id="84139-149">This script has three mandatory parameters: a resource group name, a key vault name, and the geographic location.</span></span>

<span data-ttu-id="84139-150">Par exemple, si vous utilisez le nom de coffre ContosoKeyVault, le nom de groupe de ressources ContosoResourceGroup et l’emplacement Asie de l’Est, tapez :</span><span class="sxs-lookup"><span data-stu-id="84139-150">For example, if you use the vault name of ContosoKeyVault, the resource group name of ContosoResourceGroup, and the location of East Asia, type:</span></span>
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

<span data-ttu-id="84139-151">La sortie de cette commande affiche les propriétés du coffre de clés que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="84139-151">The output of this command shows properties of the key vault that you've just created.</span></span> <span data-ttu-id="84139-152">Les deux propriétés les plus importantes sont :</span><span class="sxs-lookup"><span data-stu-id="84139-152">The two most important properties are:</span></span>

* <span data-ttu-id="84139-153">**Nom**: dans l’exemple : ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="84139-153">**name**: In the example this is ContosoKeyVault.</span></span> <span data-ttu-id="84139-154">Vous allez utiliser ce nom pour les autres commandes Key Vault.</span><span class="sxs-lookup"><span data-stu-id="84139-154">You will use this name for other Key Vault commands.</span></span>
* <span data-ttu-id="84139-155">**vaultUri** : dans l’exemple, il s’agit de https://contosokeyvault.vault.azure.net/.</span><span class="sxs-lookup"><span data-stu-id="84139-155">**vaultUri**: In the example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="84139-156">Les applications qui utilisent votre coffre via son API REST doivent utiliser cet URI.</span><span class="sxs-lookup"><span data-stu-id="84139-156">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="84139-157">Votre compte Azure est pour l’instant le seul autorisé à effectuer des opérations sur ce</span><span class="sxs-lookup"><span data-stu-id="84139-157">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="84139-158">coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="84139-158">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-to-the-key-vault"></a><span data-ttu-id="84139-159">Ajout d’une clé ou d’un secret au coffre de clés</span><span class="sxs-lookup"><span data-stu-id="84139-159">Add a key or secret to the key vault</span></span>
<span data-ttu-id="84139-160">Si vous souhaitez qu’Azure Key Vault crée pour vous une clé protégée par logiciel, utilisez la commande `az key create` et tapez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="84139-160">If you want Azure Key Vault to create a software-protected key for you, use the `az key create` command, and type the following:</span></span>
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
<span data-ttu-id="84139-161">Toutefois, si vous avez une clé existante dans un fichier .pem enregistré sous la forme d’un fichier local dans un fichier nommé softkey.pem que vous souhaitez télécharger dans Azure Key Vault, tapez la commande suivante pour importer la clé à partir du fichier .PEM qui protège la clé par logiciel dans le service Key Vault :</span><span class="sxs-lookup"><span data-stu-id="84139-161">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want to upload to Azure Key Vault, type the following to import the key from the .PEM file, which protects the key by software in the Key Vault service:</span></span>
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
<span data-ttu-id="84139-162">Vous pouvez maintenant référencer la clé que vous avez créée ou téléchargée dans Azure Key Vault à l’aide de son URI.</span><span class="sxs-lookup"><span data-stu-id="84139-162">You can now reference the key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="84139-163">Utilisez **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** pour toujours obtenir la version actuelle, et **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** pour obtenir cette version spécifique.</span><span class="sxs-lookup"><span data-stu-id="84139-163">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span></span>

<span data-ttu-id="84139-164">Pour ajouter un secret dans le coffre, c’est-à-dire un mot de passe nommé SQLPassword avec la valeur Pa$$w0rd dans Azure Key Vault, tapez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="84139-164">To add a secret to the vault, which is a password named SQLPassword and that has the value of Pa$$w0rd to Azure Key Vault, type the following:</span></span>
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
<span data-ttu-id="84139-165">Vous pouvez maintenant référencer ce mot de passe que vous avez ajouté dans Azure Key Vault à l’aide de son URI.</span><span class="sxs-lookup"><span data-stu-id="84139-165">You can now reference this password that you added to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="84139-166">Utilisez **https://ContosoVault.vault.azure.net/secrets/SQLPassword** pour toujours obtenir la version actuelle, et **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** pour obtenir cette version spécifique.</span><span class="sxs-lookup"><span data-stu-id="84139-166">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span></span>

<span data-ttu-id="84139-167">Examinons la clé ou le secret que vous venez de créer :</span><span class="sxs-lookup"><span data-stu-id="84139-167">Let's view the key or secret that you just created:</span></span>

* <span data-ttu-id="84139-168">Pour afficher votre clé, tapez : `az keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="84139-168">To view your key, type: `az keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="84139-169">Pour afficher votre secret, tapez : `az keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="84139-169">To view your secret, type: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="84139-170">Inscription d’une application auprès d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="84139-170">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="84139-171">Cette étape est généralement effectuée par un développeur et sur un ordinateur distinct.</span><span class="sxs-lookup"><span data-stu-id="84139-171">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="84139-172">Bien que non spécifique d’Azure Key Vault, elle est incluse ici par souci d’exhaustivité.</span><span class="sxs-lookup"><span data-stu-id="84139-172">It is not specific to Azure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84139-173">Pour suivre le didacticiel, le compte, le coffre et l’application que vous inscrivez dans cette étape doivent tous se trouver dans le même répertoire Azure.</span><span class="sxs-lookup"><span data-stu-id="84139-173">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span></span>
>
>

<span data-ttu-id="84139-174">Les applications qui utilisent un coffre de clés doivent s’authentifier à l’aide d’un jeton à partir d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="84139-174">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="84139-175">Pour ce faire, le propriétaire de l’application doit d’abord inscrire l’application dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="84139-175">To do this, the owner of the application must first register the application in their Azure Active Directory.</span></span> <span data-ttu-id="84139-176">À la fin de l’inscription, le propriétaire de l’application obtient les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="84139-176">At the end of registration, the application owner gets the following values:</span></span>

* <span data-ttu-id="84139-177">Un **ID d’application** (également appelé ID de client) et une **clé d’authentification** (également appelée secret partagé).</span><span class="sxs-lookup"><span data-stu-id="84139-177">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span></span> <span data-ttu-id="84139-178">L’application doit présenter ces deux valeurs à Azure Active Directory afin d’obtenir un jeton.</span><span class="sxs-lookup"><span data-stu-id="84139-178">The application must present both of these values to Azure Active Directory, to get a token.</span></span> <span data-ttu-id="84139-179">La manière dont l’application est configurée pour cela dépend de l’application en question.</span><span class="sxs-lookup"><span data-stu-id="84139-179">How the application is configured to do this depends on the application.</span></span> <span data-ttu-id="84139-180">Pour l’exemple d’application de coffre de clés, le propriétaire de l’application définit ces valeurs dans le fichier app.config.</span><span class="sxs-lookup"><span data-stu-id="84139-180">For the Key Vault sample application, the application owner sets these values in the app.config file.</span></span>

<span data-ttu-id="84139-181">Pour inscrire votre application auprès d’Azure Active Directory :</span><span class="sxs-lookup"><span data-stu-id="84139-181">To register the application in Azure Active Directory:</span></span>

1. <span data-ttu-id="84139-182">Connectez-vous au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="84139-182">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="84139-183">Dans le volet gauche, cliquez sur **Azure Active Directory**, puis sélectionnez le répertoire dans lequel vous allez inscrire votre application.</span><span class="sxs-lookup"><span data-stu-id="84139-183">On the left, click **Azure Active Directory**, and then select the directory in which you will register your application.</span></span> <br> <br> 

> [!Note] 
> <span data-ttu-id="84139-184">Vous devez sélectionner le répertoire qui contient l’abonnement Azure avec lequel vous avez créé votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="84139-184">You must select the same directory that contains the Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="84139-185">Si vous ne savez pas de quel répertoire il s’agit, cliquez sur **Paramètres**, identifiez l’abonnement avec lequel vous avez créé votre coffre de clés et notez le nom du répertoire affiché dans la dernière colonne.</span><span class="sxs-lookup"><span data-stu-id="84139-185">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span></span>

3. <span data-ttu-id="84139-186">Cliquez sur **APPLICATIONS**.</span><span class="sxs-lookup"><span data-stu-id="84139-186">Click **APPLICATIONS**.</span></span> <span data-ttu-id="84139-187">Si aucune application n’a été ajoutée à votre répertoire, cette page affiche uniquement le lien **Ajouter une application**.</span><span class="sxs-lookup"><span data-stu-id="84139-187">If no apps have been added to your directory, this page will show only the **Add an App** link.</span></span> <span data-ttu-id="84139-188">Cliquez sur le lien. Vous pouvez également cliquer sur **AJOUTER** dans la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="84139-188">Click the link, or alternatively, you can click the **ADD** on the command bar.</span></span>
4. <span data-ttu-id="84139-189">Dans l’Assistant **AJOUTER UNE APPLICATION**, dans la page **Que voulez-vous faire ?**, cliquez sur **Ajouter une application développée par mon organisation**.</span><span class="sxs-lookup"><span data-stu-id="84139-189">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="84139-190">Dans la page **Parlez-nous de votre application**, spécifiez un nom pour votre application et sélectionnez **APPLICATION WEB ET/OU API WEB** (par défaut).</span><span class="sxs-lookup"><span data-stu-id="84139-190">On the **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (the default).</span></span> <span data-ttu-id="84139-191">Cliquez sur l’icône Suivant.</span><span class="sxs-lookup"><span data-stu-id="84139-191">Click the Next icon.</span></span>
6. <span data-ttu-id="84139-192">Dans la page **Propriétés de l’application**, spécifiez l’**URL DE CONNEXION** et l’**URI ID D’APPLICATION** pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="84139-192">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="84139-193">Si votre application n’a pas ces valeurs, vous pouvez les créer pour cette étape (par exemple, vous pouvez spécifier http://test1.contoso.com pour les deux zones).</span><span class="sxs-lookup"><span data-stu-id="84139-193">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="84139-194">Peu importe si ces sites existent. L’important est que l’URI d’ID d’application est différent pour chaque application dans votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="84139-194">It does not matter if these sites exist; what is important is that the app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="84139-195">Le répertoire utilise cette chaîne pour identifier votre application.</span><span class="sxs-lookup"><span data-stu-id="84139-195">The directory uses this string to identify your app.</span></span>
7. <span data-ttu-id="84139-196">Cliquez sur l’icône Terminé pour enregistrer vos modifications dans l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="84139-196">Click the Complete icon to save your changes in the wizard.</span></span>
8. <span data-ttu-id="84139-197">Dans la page Démarrage rapide, cliquez sur **CONFIGURER**.</span><span class="sxs-lookup"><span data-stu-id="84139-197">On the Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="84139-198">Accédez à la section **clés** , sélectionnez la durée, puis cliquez sur **ENREGISTRER**.</span><span class="sxs-lookup"><span data-stu-id="84139-198">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span></span> <span data-ttu-id="84139-199">La page est actualisée et affiche à présent une valeur de clé.</span><span class="sxs-lookup"><span data-stu-id="84139-199">The page refreshes and now shows a key value.</span></span> <span data-ttu-id="84139-200">Vous devez configurer votre application avec cette valeur de clé et la valeur d’ **ID CLIENT** .</span><span class="sxs-lookup"><span data-stu-id="84139-200">You must configure your application with this key value and the **CLIENT ID** value.</span></span> <span data-ttu-id="84139-201">(Les instructions relatives à cette configuration sont propres à l’application).</span><span class="sxs-lookup"><span data-stu-id="84139-201">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="84139-202">Copiez la valeur d’ID client à partir de cette page. Vous l’utiliserez à l’étape suivante pour définir des autorisations sur votre coffre.</span><span class="sxs-lookup"><span data-stu-id="84139-202">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span></span>

## <a name="authorize-the-application-to-use-the-key-or-secret"></a><span data-ttu-id="84139-203">Autorisation de l’application à utiliser la clé ou le secret</span><span class="sxs-lookup"><span data-stu-id="84139-203">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="84139-204">Pour autoriser l’application à accéder à la clé ou au secret dans le coffre, utilisez la commande `az keyvault set-policy` .</span><span class="sxs-lookup"><span data-stu-id="84139-204">To authorize the application to access the key or secret in the vault, use the `az keyvault set-policy` command.</span></span>

<span data-ttu-id="84139-205">Par exemple, si le nom de votre coffre est ContosoKeyVault, que l’application que vous souhaitez autoriser a l’ID client 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed et que vous souhaitez autoriser l’application à déchiffrer et à signer avec des clés dans le coffre, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="84139-205">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, then run the following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

<span data-ttu-id="84139-206">Si vous souhaitez autoriser cette même application à lire les éléments secrets de votre coffre, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="84139-206">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-to-use-a-hardware-security-module-hsm"></a><span data-ttu-id="84139-207">Si vous souhaitez utiliser un module de sécurité matériel (HSM)</span><span class="sxs-lookup"><span data-stu-id="84139-207">If you want to use a hardware security module (HSM)</span></span>
<span data-ttu-id="84139-208">Pour une meilleure garantie, vous pouvez importer ou générer des clés dans des modules de sécurité matériels (HSM) qui ne franchissent jamais les limites HSM.</span><span class="sxs-lookup"><span data-stu-id="84139-208">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="84139-209">Les modules HSM bénéficient d’une validation FIPS 140-2 de niveau 2.</span><span class="sxs-lookup"><span data-stu-id="84139-209">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="84139-210">Si cette exigence ne s’applique pas à vous, ignorez cette section et accédez à [Supprimer le coffre de clés et les clés et secrets associés](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="84139-210">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="84139-211">Pour créer ces clés protégées par HSM, vous devez disposer d'un abonnement de coffre qui prend en charge les clés protégées par HSM.</span><span class="sxs-lookup"><span data-stu-id="84139-211">To create these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="84139-212">Lorsque vous créez le coffre de clés, ajoutez le paramètre « SKU » :</span><span class="sxs-lookup"><span data-stu-id="84139-212">When you create the keyvault, add the 'sku' parameter:</span></span>

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
<span data-ttu-id="84139-213">Vous pouvez ajouter des clés protégées par logiciel (comme indiqué plus haut) et des clés protégées par HSM dans ce coffre.</span><span class="sxs-lookup"><span data-stu-id="84139-213">You can add software-protected keys (as shown earlier) and HSM-protected keys to this vault.</span></span> <span data-ttu-id="84139-214">Pour créer une clé protégée par HSM, définissez le paramètre Destination sur « HSM » :</span><span class="sxs-lookup"><span data-stu-id="84139-214">To create an HSM-protected key, set the Destination parameter to 'HSM':</span></span>

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

<span data-ttu-id="84139-215">Vous pouvez utiliser la commande suivante pour importer une clé à partir d’un fichier pem sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="84139-215">You can use the following command to import a key from a .pem file on your computer.</span></span> <span data-ttu-id="84139-216">Cette commande importe la clé dans les modules de sécurité matériels dans le service Key Vault :</span><span class="sxs-lookup"><span data-stu-id="84139-216">This command imports the key into HSMs in the Key Vault service:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
<span data-ttu-id="84139-217">La commande suivante importe un package BYOK (Bring Your Own Key, Apporter votre propre clé).</span><span class="sxs-lookup"><span data-stu-id="84139-217">The next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="84139-218">Cela vous permet de générer votre clé dans votre module de sécurité matériel local et de la transférer vers les modules de sécurité matériels du service Key Vault, sans que la clé quitte la limite HSM :</span><span class="sxs-lookup"><span data-stu-id="84139-218">This lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
<span data-ttu-id="84139-219">Pour plus d’instructions sur la génération de ce package BYOK, consultez la page [Génération et transfert de clés protégées par HSM pour le coffre de clés Azure](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="84139-219">For more detailed instructions about how to generate this BYOK package, see [How to use HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-the-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="84139-220">Supprimer le coffre de clés et les clés et secrets associés</span><span class="sxs-lookup"><span data-stu-id="84139-220">Delete the key vault and associated keys and secrets</span></span>
<span data-ttu-id="84139-221">Si vous n’avez plus besoin du coffre de clés ni de la clé ou du secret qu’il contient, vous pouvez supprimer le coffre de clés à l’aide de la commande `az keyvault delete` :</span><span class="sxs-lookup"><span data-stu-id="84139-221">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the `az keyvault delete` command:</span></span>

```
az keyvault delete --name 'ContosoKeyVault'
```

<span data-ttu-id="84139-222">Vous pouvez également supprimer un groupe de ressources Azure, qui inclut le coffre de clés et les autres ressources incluses dans ce groupe :</span><span class="sxs-lookup"><span data-stu-id="84139-222">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span></span>

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="84139-223">Autres interfaces de ligne de commande interplateformes Azure</span><span class="sxs-lookup"><span data-stu-id="84139-223">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="84139-224">Autres commandes qui peuvent être utiles pour la gestion d’Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="84139-224">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="84139-225">Cette commande permet d’obtenir un affichage sous forme de tableau de l’ensemble des clés et des propriétés sélectionnées :</span><span class="sxs-lookup"><span data-stu-id="84139-225">This command lists a tabular display of all keys and selected properties:</span></span>

<span data-ttu-id="84139-226">az keyvault key list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="84139-226">az keyvault key list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="84139-227">Cette commande affiche la liste complète des propriétés pour la clé spécifiée :</span><span class="sxs-lookup"><span data-stu-id="84139-227">This command displays a full list of properties for the specified key:</span></span>

<span data-ttu-id="84139-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="84139-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="84139-229">Cette commande permet d’obtenir un affichage sous forme de tableau de l’ensemble des secrets et des propriétés sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="84139-229">This command lists a tabular display of all secret names and selected properties:</span></span>

<span data-ttu-id="84139-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="84139-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="84139-231">Voici un exemple montrant comment supprimer une clé spécifique :</span><span class="sxs-lookup"><span data-stu-id="84139-231">Here's an example of how to remove a specific key:</span></span>

<span data-ttu-id="84139-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="84139-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="84139-233">Voici un exemple montrant comment supprimer un secret spécifique :</span><span class="sxs-lookup"><span data-stu-id="84139-233">Here's an example of how to remove a specific secret:</span></span>

<span data-ttu-id="84139-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span><span class="sxs-lookup"><span data-stu-id="84139-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span></span>


## <a name="next-steps"></a><span data-ttu-id="84139-235">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="84139-235">Next steps</span></span>
<span data-ttu-id="84139-236">Pour accéder à une documentation de référence complète sur l’interface Azure CLI pour les commandes Key Vault, consultez le document de [référence sur l’interface de ligne de commande Key Vault](/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="84139-236">For complete Azure CLI reference for key vault commands, see [Key Vault CLI reference](/cli/azure/keyvault)</span></span>

<span data-ttu-id="84139-237">Pour les références de programmation, consultez le [guide du développeur de coffre de clés Azure](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="84139-237">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>
