---
title: "Gestion de Azure Key Vault à l’aide de l’interface de ligne de commande (CLI) | Document Microsoft"
description: "Utilisez ce didacticiel pour automatiser les tâches courantes dans Key Vault à l’aide de l’interface de ligne de commande"
services: key-vault
documentationcenter: 
author: BrucePerlerMS
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 66be6e44-684a-411b-802e-884628458ae7
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: bruceper
ms.openlocfilehash: c2565a742ce4f6ab5f7639a54c4a475f00cbc260
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-key-vault-using-cli"></a><span data-ttu-id="5debf-103">Gestion de Key Vault à l’aide de l’interface de ligne de commande (CLI)</span><span class="sxs-lookup"><span data-stu-id="5debf-103">Manage Key Vault using CLI</span></span>

<span data-ttu-id="5debf-104">Azure Key Vault est disponible dans la plupart des régions.</span><span class="sxs-lookup"><span data-stu-id="5debf-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="5debf-105">Pour plus d’informations, consultez la [page de tarification de Key Vault](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="5debf-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="5debf-106">Introduction</span><span class="sxs-lookup"><span data-stu-id="5debf-106">Introduction</span></span>

<span data-ttu-id="5debf-107">Ce didacticiel vous aide à démarrer avec Azure Key Vault pour créer un conteneur renforcé (un coffre) dans Azure afin de stocker et gérer les clés de chiffrement et les secrets dans Azure.</span><span class="sxs-lookup"><span data-stu-id="5debf-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="5debf-108">Il vous guide tout au long du processus d’utilisation de l’interface de ligne de commande interplateforme Azure pour créer un coffre qui contient une clé ou un mot de passe que vous pouvez ensuite utiliser avec une application Azure.</span><span class="sxs-lookup"><span data-stu-id="5debf-108">It walks you through the process of using Azure Cross-Platform Command-Line Interface to create a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="5debf-109">Il vous montre également comment une application peut ensuite utiliser cette clé ou ce mot de passe.</span><span class="sxs-lookup"><span data-stu-id="5debf-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="5debf-110">**Durée estimée :** 20 minutes</span><span class="sxs-lookup"><span data-stu-id="5debf-110">**Estimated time to complete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="5debf-111">Ce didacticiel n’inclut pas d’instructions sur l’écriture de l’application Azure abordée dans une des étapes, qui montre comment autoriser une application à utiliser une clé ou un secret dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="5debf-111">This tutorial does not include instructions on how to write the Azure application that one of the steps includes, which shows how to authorize an application to use a key or secret in the key vault.</span></span>
> 
> <span data-ttu-id="5debf-112">Actuellement, vous ne pouvez pas configurer Azure Key Vault dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5debf-112">Currently, you cannot configure Azure Key Vault in the Azure portal.</span></span> <span data-ttu-id="5debf-113">À la place, utilisez ces instructions de l’interface de ligne de commande interplateforme.</span><span class="sxs-lookup"><span data-stu-id="5debf-113">Instead, use these Cross-Platform Command-Line Interface  instructions.</span></span> <span data-ttu-id="5debf-114">Ou, pour des instructions Azure PowerShell, consultez [ce didacticiel équivalent](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5debf-114">Or, for Azure PowerShell instructions, see [this equivalent tutorial](key-vault-get-started.md).</span></span>
> 
> 

<span data-ttu-id="5debf-115">Pour plus d’informations générales sur Azure Key Vault, consultez la page [Présentation d’Azure Key Vault](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="5debf-115">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5debf-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5debf-116">Prerequisites</span></span>

<span data-ttu-id="5debf-117">Pour suivre ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5debf-117">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="5debf-118">Un abonnement Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5debf-118">A subscription to Microsoft Azure.</span></span> <span data-ttu-id="5debf-119">Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/pricing/free-trial)dès aujourd’hui.</span><span class="sxs-lookup"><span data-stu-id="5debf-119">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="5debf-120">Interface de ligne de commande interplateforme Azure, version 0.9.1 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="5debf-120">Command-Line Interface version 0.9.1 or later.</span></span> <span data-ttu-id="5debf-121">Pour installer la dernière version et l’associer à votre abonnement Azure, consultez la page [Installation et configuration de l’interface de ligne de commande interplateforme Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5debf-121">To install the latest version and connect to your Azure subscription, see [Install and Configure the Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="5debf-122">Une application configurée pour utiliser la clé ou le mot de passe que vous créez dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="5debf-122">An application that will be configured to use the key or password that you create in this tutorial.</span></span> <span data-ttu-id="5debf-123">Un exemple d’application est disponible dans le [Centre de téléchargement Microsoft](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="5debf-123">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="5debf-124">Pour obtenir des instructions, consultez le fichier Lisez-moi fourni.</span><span class="sxs-lookup"><span data-stu-id="5debf-124">For instructions, see the accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="5debf-125">Obtention d’aide avec l’interface de ligne de commande interplateforme Azure</span><span class="sxs-lookup"><span data-stu-id="5debf-125">Getting help with Azure Cross-Platform Command-Line Interface</span></span>

<span data-ttu-id="5debf-126">Ce didacticiel suppose que vous êtes familiarisé avec l’interface de ligne de commande (Bash, Terminal, invite de commandes)</span><span class="sxs-lookup"><span data-stu-id="5debf-126">This tutorial assumes that you are familiar with the command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="5debf-127">Le paramètre --help ou -h peut être utilisé pour afficher l'aide relative à des commandes particulières.</span><span class="sxs-lookup"><span data-stu-id="5debf-127">The --help or -h parameter can be used to view help for specific commands.</span></span> <span data-ttu-id="5debf-128">Le format azure help [commande] [options] permet également de renvoyer les mêmes informations.</span><span class="sxs-lookup"><span data-stu-id="5debf-128">Alternately, The azure help [command] [options] format can also be used to return the same information.</span></span> <span data-ttu-id="5debf-129">Les commandes suivantes, par exemple, renvoient les mêmes informations :</span><span class="sxs-lookup"><span data-stu-id="5debf-129">For example, the following commands all return the same information:</span></span>

    azure account set --help

    azure account set -h

    azure help account set

<span data-ttu-id="5debf-130">Si vous avez des doutes sur les paramètres exigés par une commande, reportez-vous à l'aide en utilisant --help, -h ou azure help [commande].</span><span class="sxs-lookup"><span data-stu-id="5debf-130">When in doubt about the parameters needed by a command, refer to help using --help, -h or azure help [command].</span></span>

<span data-ttu-id="5debf-131">Consultez également les didacticiels suivants afin de vous familiariser avec Azure Resource Manager dans l’interface de ligne de commande interplateforme Azure :</span><span class="sxs-lookup"><span data-stu-id="5debf-131">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="5debf-132">Installation et configuration de l’interface de ligne de commande interplateforme Azure</span><span class="sxs-lookup"><span data-stu-id="5debf-132">How to install and configure Azure Cross-Platform Command Line Interface</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="5debf-133">Utilisation de l’interface de ligne de commande interplateforme Azure avec Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5debf-133">Using Azure Cross-Platform Command-Line Interface with Azure Resource Manager</span></span>](../xplat-cli-azure-resource-manager.md)

## <a name="connect-to-your-subscriptions"></a><span data-ttu-id="5debf-134">Connexion à vos abonnements</span><span class="sxs-lookup"><span data-stu-id="5debf-134">Connect to your subscriptions</span></span>

<span data-ttu-id="5debf-135">Pour vous connecter avec un compte professionnel, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5debf-135">To log in using an organizational account, use the following command:</span></span>

    azure login -u username -p password

<span data-ttu-id="5debf-136">ou si vous voulez vous connecter en tapant de façon interactive</span><span class="sxs-lookup"><span data-stu-id="5debf-136">or if you want to log in by typing interactively</span></span>

    azure login

> [!NOTE]
> <span data-ttu-id="5debf-137">La méthode par connexion fonctionne uniquement avec un compte professionnel.</span><span class="sxs-lookup"><span data-stu-id="5debf-137">The login method only works with organizational account.</span></span> <span data-ttu-id="5debf-138">Il s’agit d’un utilisateur géré par votre organisation et défini dans le client Azure Active Directory de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="5debf-138">An organizational account is a user that is managed by your organization, and defined in your organization's Azure Active Directory tenant.</span></span>
> 
> 

<span data-ttu-id="5debf-139">Si vous ne possédez pas de compte professionnel et que vous utilisez un compte Microsoft pour vous connecter à votre abonnement Azure, vous pouvez en créer un facilement en procédant comme suit.</span><span class="sxs-lookup"><span data-stu-id="5debf-139">If you do not currently have an organizational account, and are using a Microsoft account to log in to your Azure subscription, you can easily create one using the following steps.</span></span>

1. <span data-ttu-id="5debf-140">Connectez-vous au [portail de gestion Azure](https://manage.windowsazure.com/)et cliquez sur Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5debf-140">Login to the Login to the [Azure Management Portal](https://manage.windowsazure.com/), and click on Active Directory.</span></span>
2. <span data-ttu-id="5debf-141">S’il n’existe aucun annuaire, sélectionnez Create your directory et fournissez les informations demandées.</span><span class="sxs-lookup"><span data-stu-id="5debf-141">If no directory exists, select Create your directory and provide the requested information.</span></span>
3. <span data-ttu-id="5debf-142">Sélectionnez votre annuaire et ajoutez un nouvel utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5debf-142">Select your directory and add a new user.</span></span> <span data-ttu-id="5debf-143">Il s'agit d'un compte professionnel.</span><span class="sxs-lookup"><span data-stu-id="5debf-143">This new user is an organizational account.</span></span> <span data-ttu-id="5debf-144">Pendant la création de l'utilisateur, une adresse de messagerie est fournie pour l'utilisateur, ainsi qu'un mot de passe temporaire.</span><span class="sxs-lookup"><span data-stu-id="5debf-144">During the creation of the user, you will be supplied with both an e-mail address for the user and a temporary password.</span></span> <span data-ttu-id="5debf-145">Conservez ces informations, car elles vous serviront à une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="5debf-145">Save this information as it is used in another step.</span></span>
4. <span data-ttu-id="5debf-146">Dans le portail, sélectionnez Paramètres, puis Administrateurs.</span><span class="sxs-lookup"><span data-stu-id="5debf-146">From the portal, select Settings and then select Administrators.</span></span> <span data-ttu-id="5debf-147">Sélectionnez Ajouter, puis ajoutez le nouvel utilisateur en tant que coadministrateur.</span><span class="sxs-lookup"><span data-stu-id="5debf-147">Select Add, and add the new user as a co-administrator.</span></span> <span data-ttu-id="5debf-148">Cela permet au compte professionnel de gérer votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5debf-148">This allows the organizational account to manage your Azure subscription.</span></span>
5. <span data-ttu-id="5debf-149">Pour finir, déconnectez-vous du portail Azure et reconnectez-vous en utilisant le nouveau compte professionnel.</span><span class="sxs-lookup"><span data-stu-id="5debf-149">Finally, log out of the Azure portal and then log back in using the new organizational account.</span></span> <span data-ttu-id="5debf-150">Si vous vous connectez pour la première fois avec ce compte, vous êtes invité à changer le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="5debf-150">If this is the first time logging in with this account, you will be prompted to change the password.</span></span>

<span data-ttu-id="5debf-151">Pour plus d’informations sur les comptes professionnels avec Microsoft Azure, consultez la page [Inscription à Microsoft Azure en tant qu’organisation](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="5debf-151">For more information about using an organizational account with Microsoft Azure, see [Sign up for Microsoft Azure as an Organization](../active-directory/sign-up-organization.md).</span></span>

<span data-ttu-id="5debf-152">Si vous disposez de plusieurs abonnements et que vous souhaitez spécifier un abonnement spécifique à utiliser pour Azure Key Vault, tapez la commande suivante pour afficher les abonnements de votre compte :</span><span class="sxs-lookup"><span data-stu-id="5debf-152">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span></span>

    azure account list

<span data-ttu-id="5debf-153">Ensuite, pour indiquer l’abonnement, tapez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="5debf-153">Then, to specify the subscription to use, type:</span></span>

    azure account set <subscription name>

<span data-ttu-id="5debf-154">Pour plus d’informations sur la configuration de l’interface de ligne de commande interplateforme Azure, consultez la page [Installation et configuration de l’interface de ligne de commande interplateforme Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5debf-154">For more information about configuring Azure Cross-Platform Command-Line Interface, see [How to Install and Configure Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>

## <a name="switch-to-using-azure-resource-manager"></a><span data-ttu-id="5debf-155">Passage au mode Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5debf-155">Switch to using Azure Resource Manager</span></span>
<span data-ttu-id="5debf-156">Key Vault nécessitant Azure Resource Manager, tapez ce qui suit pour passer en mode Azure Resource Manager :</span><span class="sxs-lookup"><span data-stu-id="5debf-156">The Key Vault requires Azure Resource Manager, so type the following to switch to Azure Resource Manager mode:</span></span>

    azure config mode arm

## <a name="create-a-new-resource-group"></a><span data-ttu-id="5debf-157">Création d’un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="5debf-157">Create a new resource group</span></span>
<span data-ttu-id="5debf-158">Lorsque vous utilisez Azure Resource Manager, toutes les ressources associées sont créées au sein d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5debf-158">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="5debf-159">Nous allons créer un groupe de ressources nommé « ContosoResourceGroup » pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="5debf-159">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

    azure group create 'ContosoResourceGroup' 'East Asia'

<span data-ttu-id="5debf-160">Le premier paramètre est le nom de groupe de ressources et le deuxième paramètre est l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="5debf-160">The first parameter is resource group name and the second parameter is the location.</span></span> <span data-ttu-id="5debf-161">Pour l’emplacement, utilisez la commande `azure location list` pour savoir comment spécifier un autre emplacement que celui de cet exemple.</span><span class="sxs-lookup"><span data-stu-id="5debf-161">For location, use the command `azure location list` to identify how to specify an alternative location to the one in this example.</span></span> <span data-ttu-id="5debf-162">Si vous avez besoin de plus d’informations, tapez : `azure help location`</span><span class="sxs-lookup"><span data-stu-id="5debf-162">If you need more information, type: `azure help location`</span></span>

## <a name="register-the-key-vault-resource-provider"></a><span data-ttu-id="5debf-163">Inscription du fournisseur de ressources Key Vault</span><span class="sxs-lookup"><span data-stu-id="5debf-163">Register the Key Vault resource provider</span></span>
<span data-ttu-id="5debf-164">Assurez-vous que le fournisseur de ressources Key Vault est inscrit dans votre abonnement :</span><span class="sxs-lookup"><span data-stu-id="5debf-164">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

`azure provider register Microsoft.KeyVault`

<span data-ttu-id="5debf-165">Cette opération ne doit être effectuée qu'une fois par abonnement.</span><span class="sxs-lookup"><span data-stu-id="5debf-165">This only needs to be done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="5debf-166">Création d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="5debf-166">Create a key vault</span></span>

<span data-ttu-id="5debf-167">Utilisez la commande `azure keyvault create` pour créer un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="5debf-167">Use the `azure keyvault create` command to create a key vault.</span></span> <span data-ttu-id="5debf-168">Ce script a trois paramètres obligatoires : un nom de groupe de ressources, un nom de coffre de clés et l’emplacement géographique.</span><span class="sxs-lookup"><span data-stu-id="5debf-168">This script has three mandatory parameters: a resource group name, a key vault name, and the geographic location.</span></span>

<span data-ttu-id="5debf-169">Par exemple, si vous utilisez le nom de coffre ContosoKeyVault, le nom de groupe de ressources ContosoResourceGroup et l’emplacement Asie de l’Est, tapez :</span><span class="sxs-lookup"><span data-stu-id="5debf-169">For example, if you use the vault name of ContosoKeyVault, the resource group name of ContosoResourceGroup, and the location of East Asia, type:</span></span>

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

<span data-ttu-id="5debf-170">La sortie de cette commande affiche les propriétés du coffre de clés que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="5debf-170">The output of this command shows properties of the key vault that you've just created.</span></span> <span data-ttu-id="5debf-171">Les deux propriétés les plus importantes sont :</span><span class="sxs-lookup"><span data-stu-id="5debf-171">The two most important properties are:</span></span>

* <span data-ttu-id="5debf-172">**Nom**: dans l’exemple : ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="5debf-172">**Name**: In the example this is ContosoKeyVault.</span></span> <span data-ttu-id="5debf-173">Vous allez utiliser ce nom pour les autres applets de commande Key Vault.</span><span class="sxs-lookup"><span data-stu-id="5debf-173">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="5debf-174">**vaultUri** : dans l’exemple, il s’agit de https://contosokeyvault.vault.azure.net/.</span><span class="sxs-lookup"><span data-stu-id="5debf-174">**vaultUri**: In the example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="5debf-175">Les applications qui utilisent votre coffre via son API REST doivent utiliser cet URI.</span><span class="sxs-lookup"><span data-stu-id="5debf-175">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="5debf-176">Votre compte Azure est pour l’instant le seul autorisé à effectuer des opérations sur ce</span><span class="sxs-lookup"><span data-stu-id="5debf-176">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="5debf-177">coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="5debf-177">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-to-the-key-vault"></a><span data-ttu-id="5debf-178">Ajout d’une clé ou d’un secret au coffre de clés</span><span class="sxs-lookup"><span data-stu-id="5debf-178">Add a key or secret to the key vault</span></span>

<span data-ttu-id="5debf-179">Si vous souhaitez qu’Azure Key Vault crée pour vous une clé protégée par logiciel, utilisez la commande `azure key create` et tapez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="5debf-179">If you want Azure Key Vault to create a software-protected key for you, use the `azure key create` command, and type the following:</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

<span data-ttu-id="5debf-180">Toutefois, si vous avez une clé existante dans un fichier .pem enregistré sous la forme d’un fichier local dans un fichier nommé softkey.pem que vous souhaitez télécharger dans Azure Key Vault, tapez la commande suivante pour importer la clé à partir du fichier .PEM qui protège la clé par logiciel dans le service Key Vault :</span><span class="sxs-lookup"><span data-stu-id="5debf-180">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want to upload to Azure Key Vault, type the following to import the key from the .PEM file, which protects the key by software in the Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

<span data-ttu-id="5debf-181">Vous pouvez maintenant référencer la clé que vous avez créée ou téléchargée dans Azure Key Vault à l’aide de son URI.</span><span class="sxs-lookup"><span data-stu-id="5debf-181">You can now reference the key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="5debf-182">Utilisez **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** pour toujours obtenir la version actuelle, et **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** pour obtenir cette version spécifique.</span><span class="sxs-lookup"><span data-stu-id="5debf-182">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span></span>

<span data-ttu-id="5debf-183">Pour ajouter un secret dans le coffre, c’est-à-dire un mot de passe nommé SQLPassword avec la valeur Pa$$w0rd dans Azure Key Vault, tapez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="5debf-183">To add a secret to the vault, which is a password named SQLPassword and that has the value of Pa$$w0rd to Azure Key Vault, type the following:</span></span>

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

<span data-ttu-id="5debf-184">Vous pouvez maintenant référencer ce mot de passe que vous avez ajouté dans Azure Key Vault à l’aide de son URI.</span><span class="sxs-lookup"><span data-stu-id="5debf-184">You can now reference this password that you added to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="5debf-185">Utilisez **https://ContosoVault.vault.azure.net/secrets/SQLPassword** pour toujours obtenir la version actuelle, et **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** pour obtenir cette version spécifique.</span><span class="sxs-lookup"><span data-stu-id="5debf-185">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span></span>

<span data-ttu-id="5debf-186">Examinons la clé ou le secret que vous venez de créer :</span><span class="sxs-lookup"><span data-stu-id="5debf-186">Let's view the key or secret that you just created:</span></span>

* <span data-ttu-id="5debf-187">Pour afficher votre clé, tapez : `azure keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="5debf-187">To view your key, type: `azure keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="5debf-188">Pour afficher votre secret, tapez : `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="5debf-188">To view your secret, type: `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="5debf-189">Inscription d’une application auprès d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5debf-189">Register an application with Azure Active Directory</span></span>

<span data-ttu-id="5debf-190">Cette étape est généralement effectuée par un développeur et sur un ordinateur distinct.</span><span class="sxs-lookup"><span data-stu-id="5debf-190">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="5debf-191">Bien que non spécifique d’Azure Key Vault, elle est incluse ici par souci d’exhaustivité.</span><span class="sxs-lookup"><span data-stu-id="5debf-191">It is not specific to Azure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5debf-192">Pour suivre le didacticiel, le compte, le coffre et l’application que vous inscrivez dans cette étape doivent tous se trouver dans le même répertoire Azure.</span><span class="sxs-lookup"><span data-stu-id="5debf-192">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span></span>
> 
> 

<span data-ttu-id="5debf-193">Les applications qui utilisent un coffre de clés doivent s’authentifier à l’aide d’un jeton à partir d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5debf-193">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="5debf-194">Pour ce faire, le propriétaire de l’application doit d’abord inscrire l’application dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5debf-194">To do this, the owner of the application must first register the application in their Azure Active Directory.</span></span> <span data-ttu-id="5debf-195">À la fin de l’inscription, le propriétaire de l’application obtient les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="5debf-195">At the end of registration, the application owner gets the following values:</span></span>

* <span data-ttu-id="5debf-196">Un **ID d’application** (également appelé ID de client) et une **clé d’authentification** (également appelée secret partagé).</span><span class="sxs-lookup"><span data-stu-id="5debf-196">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span></span> <span data-ttu-id="5debf-197">L’application doit présenter ces deux valeurs à Azure Active Directory afin d’obtenir un jeton.</span><span class="sxs-lookup"><span data-stu-id="5debf-197">The application must present both of these values to Azure Active Directory, to get a token.</span></span> <span data-ttu-id="5debf-198">La manière dont l’application est configurée pour cela dépend de l’application en question.</span><span class="sxs-lookup"><span data-stu-id="5debf-198">How the application is configured to do this depends on the application.</span></span> <span data-ttu-id="5debf-199">Pour l’exemple d’application de coffre de clés, le propriétaire de l’application définit ces valeurs dans le fichier app.config.</span><span class="sxs-lookup"><span data-stu-id="5debf-199">For the Key Vault sample application, the application owner sets these values in the app.config file.</span></span>

<span data-ttu-id="5debf-200">Pour inscrire votre application auprès d’Azure Active Directory :</span><span class="sxs-lookup"><span data-stu-id="5debf-200">To register the application in Azure Active Directory:</span></span>

1. <span data-ttu-id="5debf-201">Connectez-vous au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5debf-201">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="5debf-202">Dans le volet gauche, cliquez sur **Active Directory**, puis sélectionnez le répertoire dans lequel vous allez inscrire votre application.</span><span class="sxs-lookup"><span data-stu-id="5debf-202">On the left, click **Active Directory**, and then select the directory in which you will register your application.</span></span> <br> <br> 

>[!NOTE] 
> <span data-ttu-id="5debf-203">Vous devez sélectionner le répertoire qui contient l’abonnement Azure avec lequel vous avez créé votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="5debf-203">You must select the same directory that contains the Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="5debf-204">Si vous ne savez pas de quel répertoire il s’agit, cliquez sur **Paramètres**, identifiez l’abonnement avec lequel vous avez créé votre coffre de clés et notez le nom du répertoire affiché dans la dernière colonne.</span><span class="sxs-lookup"><span data-stu-id="5debf-204">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span></span>

3. <span data-ttu-id="5debf-205">Cliquez sur **APPLICATIONS**.</span><span class="sxs-lookup"><span data-stu-id="5debf-205">Click **APPLICATIONS**.</span></span> <span data-ttu-id="5debf-206">Si aucune application n’a été ajoutée à votre répertoire, cette page affiche uniquement le lien **Ajouter une application**.</span><span class="sxs-lookup"><span data-stu-id="5debf-206">If no apps have been added to your directory, this page will show only the **Add an App** link.</span></span> <span data-ttu-id="5debf-207">Cliquez sur le lien. Vous pouvez également cliquer sur **AJOUTER** dans la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="5debf-207">Click the link, or alternatively, you can click the **ADD** on the command bar.</span></span>
4. <span data-ttu-id="5debf-208">Dans l’Assistant **AJOUTER UNE APPLICATION**, dans la page **Que voulez-vous faire ?**, cliquez sur **Ajouter une application développée par mon organisation**.</span><span class="sxs-lookup"><span data-stu-id="5debf-208">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="5debf-209">Dans la page **Parlez-nous de votre application**, spécifiez un nom pour votre application et sélectionnez **APPLICATION WEB ET/OU API WEB** (par défaut).</span><span class="sxs-lookup"><span data-stu-id="5debf-209">On the **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (the default).</span></span> <span data-ttu-id="5debf-210">Cliquez sur l’icône Suivant.</span><span class="sxs-lookup"><span data-stu-id="5debf-210">Click the Next icon.</span></span>
6. <span data-ttu-id="5debf-211">Dans la page **Propriétés de l’application**, spécifiez l’**URL DE CONNEXION** et l’**URI ID D’APPLICATION** pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="5debf-211">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="5debf-212">Si votre application n’a pas ces valeurs, vous pouvez les créer pour cette étape (par exemple, vous pouvez spécifier http://test1.contoso.com pour les deux zones).</span><span class="sxs-lookup"><span data-stu-id="5debf-212">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="5debf-213">Peu importe si ces sites existent. L’important est que l’URI d’ID d’application est différent pour chaque application dans votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="5debf-213">It does not matter if these sites exist; what is important is that the app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="5debf-214">Le répertoire utilise cette chaîne pour identifier votre application.</span><span class="sxs-lookup"><span data-stu-id="5debf-214">The directory uses this string to identify your app.</span></span>
7. <span data-ttu-id="5debf-215">Cliquez sur l’icône Terminé pour enregistrer vos modifications dans l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="5debf-215">Click the Complete icon to save your changes in the wizard.</span></span>
8. <span data-ttu-id="5debf-216">Dans la page Démarrage rapide, cliquez sur **CONFIGURER**.</span><span class="sxs-lookup"><span data-stu-id="5debf-216">On the Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="5debf-217">Accédez à la section **clés** , sélectionnez la durée, puis cliquez sur **ENREGISTRER**.</span><span class="sxs-lookup"><span data-stu-id="5debf-217">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span></span> <span data-ttu-id="5debf-218">La page est actualisée et affiche à présent une valeur de clé.</span><span class="sxs-lookup"><span data-stu-id="5debf-218">The page refreshes and now shows a key value.</span></span> <span data-ttu-id="5debf-219">Vous devez configurer votre application avec cette valeur de clé et la valeur d’ **ID CLIENT** .</span><span class="sxs-lookup"><span data-stu-id="5debf-219">You must configure your application with this key value and the **CLIENT ID** value.</span></span> <span data-ttu-id="5debf-220">(Les instructions relatives à cette configuration sont propres à l’application).</span><span class="sxs-lookup"><span data-stu-id="5debf-220">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="5debf-221">Copiez la valeur d’ID client à partir de cette page. Vous l’utiliserez à l’étape suivante pour définir des autorisations sur votre coffre.</span><span class="sxs-lookup"><span data-stu-id="5debf-221">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span></span>

## <a name="authorize-the-application-to-use-the-key-or-secret"></a><span data-ttu-id="5debf-222">Autorisation de l’application à utiliser la clé ou le secret</span><span class="sxs-lookup"><span data-stu-id="5debf-222">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="5debf-223">Pour autoriser l’application à accéder à la clé ou au secret dans le coffre, utilisez la commande `azure keyvault set-policy` .</span><span class="sxs-lookup"><span data-stu-id="5debf-223">To authorize the application to access the key or secret in the vault, use the `azure keyvault set-policy` command.</span></span>

<span data-ttu-id="5debf-224">Par exemple, si le nom de votre coffre est ContosoKeyVault, que l’application que vous souhaitez autoriser a l’ID client 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed et que vous souhaitez autoriser l’application à déchiffrer et à signer avec des clés dans le coffre, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5debf-224">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, then run the following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '[\"decrypt\",\"sign\"]'

> [!NOTE]
> <span data-ttu-id="5debf-225">Si vous exécutez l'invite de commandes Windows, vous devez remplacer les guillemets simples par des guillemets doubles et inclure des guillemets doubles internes.</span><span class="sxs-lookup"><span data-stu-id="5debf-225">If you are running on Windows command prompt, you should replace single quotes with double quotes, and also escape the internal double quotes.</span></span> <span data-ttu-id="5debf-226">Par exemple : "[\"decrypt\",\"sign\"]".</span><span class="sxs-lookup"><span data-stu-id="5debf-226">For example: "[\"decrypt\",\"sign\"]".</span></span>
> 
> 

<span data-ttu-id="5debf-227">Si vous souhaitez autoriser cette même application à lire les éléments secrets de votre coffre, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5debf-227">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '[\"get\"]'

## <a name="if-you-want-to-use-a-hardware-security-module-hsm"></a><span data-ttu-id="5debf-228">Si vous souhaitez utiliser un module de sécurité matériel (HSM)</span><span class="sxs-lookup"><span data-stu-id="5debf-228">If you want to use a hardware security module (HSM)</span></span>
<span data-ttu-id="5debf-229">Pour une meilleure garantie, vous pouvez importer ou générer des clés dans des modules de sécurité matériels (HSM) qui ne franchissent jamais les limites HSM.</span><span class="sxs-lookup"><span data-stu-id="5debf-229">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="5debf-230">Les modules HSM bénéficient d’une validation FIPS 140-2 de niveau 2.</span><span class="sxs-lookup"><span data-stu-id="5debf-230">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="5debf-231">Si cette exigence ne s’applique pas à vous, ignorez cette section et accédez à [Supprimer le coffre de clés et les clés et secrets associés](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="5debf-231">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="5debf-232">Pour créer ces clés protégées par HSM, vous devez disposer d'un abonnement de coffre qui prend en charge les clés protégées par HSM.</span><span class="sxs-lookup"><span data-stu-id="5debf-232">To create these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="5debf-233">Lorsque vous créez le coffre de clés, ajoutez le paramètre « SKU » :</span><span class="sxs-lookup"><span data-stu-id="5debf-233">When you create the keyvault, add the 'sku' parameter:</span></span>

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

<span data-ttu-id="5debf-234">Vous pouvez ajouter des clés protégées par logiciel (comme indiqué plus haut) et des clés protégées par HSM dans ce coffre.</span><span class="sxs-lookup"><span data-stu-id="5debf-234">You can add software-protected keys (as shown earlier) and HSM-protected keys to this vault.</span></span> <span data-ttu-id="5debf-235">Pour créer une clé protégée par HSM, définissez le paramètre Destination sur « HSM » :</span><span class="sxs-lookup"><span data-stu-id="5debf-235">To create an HSM-protected key, set the Destination parameter to 'HSM':</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

<span data-ttu-id="5debf-236">Vous pouvez utiliser la commande suivante pour importer une clé à partir d’un fichier pem sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5debf-236">You can use the following command to import a key from a .pem file on your computer.</span></span> <span data-ttu-id="5debf-237">Cette commande importe la clé dans les modules de sécurité matériels dans le service Key Vault :</span><span class="sxs-lookup"><span data-stu-id="5debf-237">This command imports the key into HSMs in the Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

<span data-ttu-id="5debf-238">La commande suivante importe un package BYOK (Bring Your Own Key, Apporter votre propre clé).</span><span class="sxs-lookup"><span data-stu-id="5debf-238">The next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="5debf-239">Cela vous permet de générer votre clé dans votre module de sécurité matériel local et de la transférer vers les modules de sécurité matériels du service Key Vault, sans que la clé quitte la limite HSM :</span><span class="sxs-lookup"><span data-stu-id="5debf-239">This lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

<span data-ttu-id="5debf-240">Pour plus d’instructions sur la génération de ce package BYOK, consultez la page [Génération et transfert de clés protégées par HSM pour le coffre de clés Azure](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="5debf-240">For more detailed instructions about how to generate this BYOK package, see [How to use HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-the-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="5debf-241">Supprimer le coffre de clés et les clés et secrets associés</span><span class="sxs-lookup"><span data-stu-id="5debf-241">Delete the key vault and associated keys and secrets</span></span>
<span data-ttu-id="5debf-242">Si vous n’avez plus besoin du coffre de clés ni de la clé ou du secret qu’il contient, vous pouvez supprimer le coffre de clés à l’aide de la commande de suppression de coffre de clés Azure :</span><span class="sxs-lookup"><span data-stu-id="5debf-242">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the azure keyvault delete command:</span></span>

    azure keyvault delete --vault-name 'ContosoKeyVault'

<span data-ttu-id="5debf-243">Vous pouvez également supprimer un groupe de ressources Azure, qui inclut le coffre de clés et les autres ressources incluses dans ce groupe :</span><span class="sxs-lookup"><span data-stu-id="5debf-243">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span></span>

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="5debf-244">Autres interfaces de ligne de commande interplateformes Azure</span><span class="sxs-lookup"><span data-stu-id="5debf-244">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="5debf-245">Autres commandes qui peuvent être utiles pour la gestion d’Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="5debf-245">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="5debf-246">Cette commande permet d’obtenir un affichage sous forme de tableau de l’ensemble des clés et des propriétés sélectionnées :</span><span class="sxs-lookup"><span data-stu-id="5debf-246">This command lists a tabular display of all keys and selected properties:</span></span>

    azure keyvault key list --vault-name 'ContosoKeyVault'

<span data-ttu-id="5debf-247">Cette commande affiche la liste complète des propriétés pour la clé spécifiée :</span><span class="sxs-lookup"><span data-stu-id="5debf-247">This command displays a full list of properties for the specified key:</span></span>

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="5debf-248">Cette commande permet d’obtenir un affichage sous forme de tableau de l’ensemble des secrets et des propriétés sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="5debf-248">This command lists a tabular display of all secret names and selected properties:</span></span>

    azure keyvault secret list --vault-name 'ContosoKeyVault'

<span data-ttu-id="5debf-249">Voici un exemple montrant comment supprimer une clé spécifique :</span><span class="sxs-lookup"><span data-stu-id="5debf-249">Here's an example of how to remove a specific key:</span></span>

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="5debf-250">Voici un exemple montrant comment supprimer un secret spécifique :</span><span class="sxs-lookup"><span data-stu-id="5debf-250">Here's an example of how to remove a specific secret:</span></span>

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a><span data-ttu-id="5debf-251">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5debf-251">Next steps</span></span>
<span data-ttu-id="5debf-252">Pour les références de programmation, consultez le [guide du développeur de coffre de clés Azure](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="5debf-252">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

