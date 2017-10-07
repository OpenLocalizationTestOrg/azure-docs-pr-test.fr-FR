---
title: "aaaManage Azure Key Vault à l’aide de CLI | Documents Microsoft"
description: "Utilisez ce didacticiel tooautomate des tâches courantes dans le coffre de clés à l’aide de hello CLI"
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
ms.openlocfilehash: 9ef506faa67e1f0db5b9e303300d63b135ddd7b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli"></a><span data-ttu-id="146a0-103">Gestion de Key Vault à l’aide de l’interface de ligne de commande (CLI)</span><span class="sxs-lookup"><span data-stu-id="146a0-103">Manage Key Vault using CLI</span></span>

<span data-ttu-id="146a0-104">Azure Key Vault est disponible dans la plupart des régions.</span><span class="sxs-lookup"><span data-stu-id="146a0-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="146a0-105">Pour plus d’informations, consultez hello [page de tarification de coffre de clés](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="146a0-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="146a0-106">Introduction</span><span class="sxs-lookup"><span data-stu-id="146a0-106">Introduction</span></span>

<span data-ttu-id="146a0-107">Utilisez ce didacticiel toohelp que vous obtenez en main d’Azure Key Vault toocreate un conteneur renforcé (un coffre) dans Azure, toostore et gérer les clés de chiffrement et les clés secrètes dans Azure.</span><span class="sxs-lookup"><span data-stu-id="146a0-107">Use this tutorial toohelp you get started with Azure Key Vault toocreate a hardened container (a vault) in Azure, toostore and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="146a0-108">Il vous guide tout au long des processus de hello d’à l’aide d’une Interface de ligne multiplateforme Azure toocreate un coffre qui contient une clé ou un mot de passe que vous pouvez ensuite utiliser avec une application Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="146a0-108">It walks you through hello process of using Azure Cross-Platform Command-Line Interface toocreate a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="146a0-109">Il vous montre également comment une application peut ensuite utiliser cette clé ou ce mot de passe.</span><span class="sxs-lookup"><span data-stu-id="146a0-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="146a0-110">**Estimation du temps toocomplete :** 20 minutes</span><span class="sxs-lookup"><span data-stu-id="146a0-110">**Estimated time toocomplete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="146a0-111">Ce didacticiel n’inclut pas d’obtenir des instructions sur la façon dont toowrite hello Azure application incluant une des étapes de hello, qui montre comment tooauthorize un toouse application une clé ou au secret dans la clé de hello coffre.</span><span class="sxs-lookup"><span data-stu-id="146a0-111">This tutorial does not include instructions on how toowrite hello Azure application that one of hello steps includes, which shows how tooauthorize an application toouse a key or secret in hello key vault.</span></span>
> 
> <span data-ttu-id="146a0-112">Actuellement, vous ne pouvez pas configurer le coffre de clés Azure Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="146a0-112">Currently, you cannot configure Azure Key Vault in hello Azure portal.</span></span> <span data-ttu-id="146a0-113">À la place, utilisez ces instructions de l’interface de ligne de commande interplateforme.</span><span class="sxs-lookup"><span data-stu-id="146a0-113">Instead, use these Cross-Platform Command-Line Interface  instructions.</span></span> <span data-ttu-id="146a0-114">Ou, pour des instructions Azure PowerShell, consultez [ce didacticiel équivalent](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="146a0-114">Or, for Azure PowerShell instructions, see [this equivalent tutorial](key-vault-get-started.md).</span></span>
> 
> 

<span data-ttu-id="146a0-115">Pour plus d’informations générales sur Azure Key Vault, consultez la page [Présentation d’Azure Key Vault](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="146a0-115">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="146a0-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="146a0-116">Prerequisites</span></span>

<span data-ttu-id="146a0-117">toocomplete ce didacticiel, vous devez avoir hello suivant :</span><span class="sxs-lookup"><span data-stu-id="146a0-117">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="146a0-118">Un abonnement tooMicrosoft Azure.</span><span class="sxs-lookup"><span data-stu-id="146a0-118">A subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="146a0-119">Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/pricing/free-trial)dès aujourd’hui.</span><span class="sxs-lookup"><span data-stu-id="146a0-119">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="146a0-120">Interface de ligne de commande interplateforme Azure, version 0.9.1 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="146a0-120">Command-Line Interface version 0.9.1 or later.</span></span> <span data-ttu-id="146a0-121">tooinstall hello version la plus récente et se connecter tooyour abonnement Azure, consultez [installer et configurer hello Interface de ligne de commande Azure Cross-Platform](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="146a0-121">tooinstall hello latest version and connect tooyour Azure subscription, see [Install and Configure hello Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="146a0-122">Une application qui sera la clé de hello toouse configuré ou le mot de passe que vous créez dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="146a0-122">An application that will be configured toouse hello key or password that you create in this tutorial.</span></span> <span data-ttu-id="146a0-123">Un exemple d’application est disponible à partir de hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="146a0-123">A sample application is available from hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="146a0-124">Pour obtenir des instructions, consultez hello qui accompagne le fichier Lisez-moi.</span><span class="sxs-lookup"><span data-stu-id="146a0-124">For instructions, see hello accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="146a0-125">Obtention d’aide avec l’interface de ligne de commande interplateforme Azure</span><span class="sxs-lookup"><span data-stu-id="146a0-125">Getting help with Azure Cross-Platform Command-Line Interface</span></span>

<span data-ttu-id="146a0-126">Ce didacticiel suppose que vous êtes familiarisé avec une interface de ligne hello (interpréteur de commandes, Terminal Server, invite de commandes)</span><span class="sxs-lookup"><span data-stu-id="146a0-126">This tutorial assumes that you are familiar with hello command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="146a0-127">Hello--help ou-h paramètre peut être utilisé tooview aide pour des commandes spécifiques.</span><span class="sxs-lookup"><span data-stu-id="146a0-127">hello --help or -h parameter can be used tooview help for specific commands.</span></span> <span data-ttu-id="146a0-128">Ou bien, l’aide hello azure [commande] [options] format peut également être utilisé tooreturn hello mêmes informations.</span><span class="sxs-lookup"><span data-stu-id="146a0-128">Alternately, hello azure help [command] [options] format can also be used tooreturn hello same information.</span></span> <span data-ttu-id="146a0-129">Par exemple, suivant de hello commandes retournent tous les hello les mêmes informations :</span><span class="sxs-lookup"><span data-stu-id="146a0-129">For example, hello following commands all return hello same information:</span></span>

    azure account set --help

    azure account set -h

    azure help account set

<span data-ttu-id="146a0-130">En cas de doute sur les paramètres de hello requis par une commande, reportez-vous à l’aide de toohelp--aide,-h ou azure help [commande].</span><span class="sxs-lookup"><span data-stu-id="146a0-130">When in doubt about hello parameters needed by a command, refer toohelp using --help, -h or azure help [command].</span></span>

<span data-ttu-id="146a0-131">Vous pouvez également lire hello suivant tooget didacticiels familiarisé avec Azure Resource Manager dans une Interface de ligne multiplateforme Azure :</span><span class="sxs-lookup"><span data-stu-id="146a0-131">You can also read hello following tutorials tooget familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="146a0-132">Comment tooinstall et configurer l’Interface de ligne de commande interplateforme Azure</span><span class="sxs-lookup"><span data-stu-id="146a0-132">How tooinstall and configure Azure Cross-Platform Command Line Interface</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="146a0-133">Utilisation de l’interface de ligne de commande interplateforme Azure avec Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="146a0-133">Using Azure Cross-Platform Command-Line Interface with Azure Resource Manager</span></span>](../xplat-cli-azure-resource-manager.md)

## <a name="connect-tooyour-subscriptions"></a><span data-ttu-id="146a0-134">Se connecter tooyour abonnements</span><span class="sxs-lookup"><span data-stu-id="146a0-134">Connect tooyour subscriptions</span></span>

<span data-ttu-id="146a0-135">toolog à l’aide d’un compte professionnel, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="146a0-135">toolog in using an organizational account, use hello following command:</span></span>

    azure login -u username -p password

<span data-ttu-id="146a0-136">ou si vous voulez toolog en tapant de manière interactive</span><span class="sxs-lookup"><span data-stu-id="146a0-136">or if you want toolog in by typing interactively</span></span>

    azure login

> [!NOTE]
> <span data-ttu-id="146a0-137">méthode de connexion Hello fonctionne uniquement avec un compte professionnel.</span><span class="sxs-lookup"><span data-stu-id="146a0-137">hello login method only works with organizational account.</span></span> <span data-ttu-id="146a0-138">Il s’agit d’un utilisateur géré par votre organisation et défini dans le client Azure Active Directory de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="146a0-138">An organizational account is a user that is managed by your organization, and defined in your organization's Azure Active Directory tenant.</span></span>
> 
> 

<span data-ttu-id="146a0-139">Si vous ne disposez pas actuellement d’un compte professionnel et que vous utilisez un toolog de compte Microsoft dans tooyour abonnement Azure, vous pouvez facilement créer un à l’aide de hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="146a0-139">If you do not currently have an organizational account, and are using a Microsoft account toolog in tooyour Azure subscription, you can easily create one using hello following steps.</span></span>

1. <span data-ttu-id="146a0-140">Connexion toohello connexion toohello [portail de gestion Azure](https://manage.windowsazure.com/), puis cliquez sur Active Directory.</span><span class="sxs-lookup"><span data-stu-id="146a0-140">Login toohello Login toohello [Azure Management Portal](https://manage.windowsazure.com/), and click on Active Directory.</span></span>
2. <span data-ttu-id="146a0-141">Si aucun répertoire n’existe, sélectionnez Créer votre annuaire et hello de fournir les informations demandées.</span><span class="sxs-lookup"><span data-stu-id="146a0-141">If no directory exists, select Create your directory and provide hello requested information.</span></span>
3. <span data-ttu-id="146a0-142">Sélectionnez votre annuaire et ajoutez un nouvel utilisateur.</span><span class="sxs-lookup"><span data-stu-id="146a0-142">Select your directory and add a new user.</span></span> <span data-ttu-id="146a0-143">Il s'agit d'un compte professionnel.</span><span class="sxs-lookup"><span data-stu-id="146a0-143">This new user is an organizational account.</span></span> <span data-ttu-id="146a0-144">Lors de la création de hello d’utilisateur de hello, vous sont fournies avec une adresse de messagerie pour l’utilisateur de hello et un mot de passe temporaire.</span><span class="sxs-lookup"><span data-stu-id="146a0-144">During hello creation of hello user, you will be supplied with both an e-mail address for hello user and a temporary password.</span></span> <span data-ttu-id="146a0-145">Conservez ces informations, car elles vous serviront à une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="146a0-145">Save this information as it is used in another step.</span></span>
4. <span data-ttu-id="146a0-146">À partir du portail de hello, sélectionnez Paramètres, puis sélectionnez les administrateurs.</span><span class="sxs-lookup"><span data-stu-id="146a0-146">From hello portal, select Settings and then select Administrators.</span></span> <span data-ttu-id="146a0-147">Sélectionnez Ajouter et ajouter un nouvel utilisateur de hello en tant que coadministrateur.</span><span class="sxs-lookup"><span data-stu-id="146a0-147">Select Add, and add hello new user as a co-administrator.</span></span> <span data-ttu-id="146a0-148">Ainsi, hello compte professionnel toomanage votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="146a0-148">This allows hello organizational account toomanage your Azure subscription.</span></span>
5. <span data-ttu-id="146a0-149">Enfin, se déconnecter hello le portail Azure et puis reconnectez-vous à l’aide du nouveau compte d’organisation hello.</span><span class="sxs-lookup"><span data-stu-id="146a0-149">Finally, log out of hello Azure portal and then log back in using hello new organizational account.</span></span> <span data-ttu-id="146a0-150">S’il s’agit de hello première connexion avec ce compte, vous serez mot de passe hello toochange demandées.</span><span class="sxs-lookup"><span data-stu-id="146a0-150">If this is hello first time logging in with this account, you will be prompted toochange hello password.</span></span>

<span data-ttu-id="146a0-151">Pour plus d’informations sur les comptes professionnels avec Microsoft Azure, consultez la page [Inscription à Microsoft Azure en tant qu’organisation](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="146a0-151">For more information about using an organizational account with Microsoft Azure, see [Sign up for Microsoft Azure as an Organization](../active-directory/sign-up-organization.md).</span></span>

<span data-ttu-id="146a0-152">Si vous avez plusieurs abonnements et que vous souhaitez toospecify un un toouse spécifique pour Azure Key Vault, tapez Bonjour suivant toosee les abonnements de hello pour votre compte :</span><span class="sxs-lookup"><span data-stu-id="146a0-152">If you have multiple subscriptions and want toospecify a specific one toouse for Azure Key Vault, type hello following toosee hello subscriptions for your account:</span></span>

    azure account list

<span data-ttu-id="146a0-153">Ensuite, toospecify hello abonnement toouse, type :</span><span class="sxs-lookup"><span data-stu-id="146a0-153">Then, toospecify hello subscription toouse, type:</span></span>

    azure account set <subscription name>

<span data-ttu-id="146a0-154">Pour plus d’informations sur la configuration de l’Interface de ligne de commande Azure inter-plateformes, consultez [comment tooInstall et configurer l’Interface de ligne de commande multiplateforme Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="146a0-154">For more information about configuring Azure Cross-Platform Command-Line Interface, see [How tooInstall and Configure Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>

## <a name="switch-toousing-azure-resource-manager"></a><span data-ttu-id="146a0-155">Commutateur toousing Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="146a0-155">Switch toousing Azure Resource Manager</span></span>
<span data-ttu-id="146a0-156">Hello coffre de clés requiert Azure Resource Manager, tapez Bonjour suivant le mode de gestionnaire de ressources tooswitch tooAzure :</span><span class="sxs-lookup"><span data-stu-id="146a0-156">hello Key Vault requires Azure Resource Manager, so type hello following tooswitch tooAzure Resource Manager mode:</span></span>

    azure config mode arm

## <a name="create-a-new-resource-group"></a><span data-ttu-id="146a0-157">Création d’un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="146a0-157">Create a new resource group</span></span>
<span data-ttu-id="146a0-158">Lorsque vous utilisez Azure Resource Manager, toutes les ressources associées sont créées au sein d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="146a0-158">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="146a0-159">Nous allons créer un groupe de ressources nommé « ContosoResourceGroup » pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="146a0-159">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

    azure group create 'ContosoResourceGroup' 'East Asia'

<span data-ttu-id="146a0-160">premier paramètre de Hello est le nom de groupe de ressources et hello deuxième paramètre est emplacement de hello.</span><span class="sxs-lookup"><span data-stu-id="146a0-160">hello first parameter is resource group name and hello second parameter is hello location.</span></span> <span data-ttu-id="146a0-161">Pour l’emplacement, utilisez la commande hello `azure location list` tooidentify comment toospecify un autre emplacement toohello un dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="146a0-161">For location, use hello command `azure location list` tooidentify how toospecify an alternative location toohello one in this example.</span></span> <span data-ttu-id="146a0-162">Si vous avez besoin de plus d’informations, tapez : `azure help location`</span><span class="sxs-lookup"><span data-stu-id="146a0-162">If you need more information, type: `azure help location`</span></span>

## <a name="register-hello-key-vault-resource-provider"></a><span data-ttu-id="146a0-163">Inscrire le fournisseur de ressources hello coffre de clés</span><span class="sxs-lookup"><span data-stu-id="146a0-163">Register hello Key Vault resource provider</span></span>
<span data-ttu-id="146a0-164">Assurez-vous que le fournisseur de ressources Key Vault est inscrit dans votre abonnement :</span><span class="sxs-lookup"><span data-stu-id="146a0-164">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

`azure provider register Microsoft.KeyVault`

<span data-ttu-id="146a0-165">Cette opération ne doit toobe réalisée une fois par abonnement.</span><span class="sxs-lookup"><span data-stu-id="146a0-165">This only needs toobe done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="146a0-166">Création d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="146a0-166">Create a key vault</span></span>

<span data-ttu-id="146a0-167">Hello d’utilisation `azure keyvault create` commande toocreate un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="146a0-167">Use hello `azure keyvault create` command toocreate a key vault.</span></span> <span data-ttu-id="146a0-168">Ce script a trois paramètres obligatoires : un nom de groupe de ressources, d’un coffre de clés et d’un emplacement géographique de hello.</span><span class="sxs-lookup"><span data-stu-id="146a0-168">This script has three mandatory parameters: a resource group name, a key vault name, and hello geographic location.</span></span>

<span data-ttu-id="146a0-169">Par exemple, si vous utilisez le nom du coffre hello de ContosoKeyVault, nom de groupe de ressources hello de ContosoResourceGroup et l’emplacement de hello d’Asie orientale, tapez :</span><span class="sxs-lookup"><span data-stu-id="146a0-169">For example, if you use hello vault name of ContosoKeyVault, hello resource group name of ContosoResourceGroup, and hello location of East Asia, type:</span></span>

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

<span data-ttu-id="146a0-170">sortie Hello de cette commande affiche les propriétés du coffre de clés hello que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="146a0-170">hello output of this command shows properties of hello key vault that you've just created.</span></span> <span data-ttu-id="146a0-171">propriétés les plus importantes Hello deux sont :</span><span class="sxs-lookup"><span data-stu-id="146a0-171">hello two most important properties are:</span></span>

* <span data-ttu-id="146a0-172">**Nom**: dans l’exemple de hello, cela est ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="146a0-172">**Name**: In hello example this is ContosoKeyVault.</span></span> <span data-ttu-id="146a0-173">Vous allez utiliser ce nom pour les autres applets de commande Key Vault.</span><span class="sxs-lookup"><span data-stu-id="146a0-173">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="146a0-174">**vaultUri**: dans l’exemple de hello, cela est https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="146a0-174">**vaultUri**: In hello example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="146a0-175">Les applications qui utilisent votre coffre via son API REST doivent utiliser cet URI.</span><span class="sxs-lookup"><span data-stu-id="146a0-175">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="146a0-176">Votre compte Azure est désormais toutes les opérations sur cette clé de coffre tooperform autorisé.</span><span class="sxs-lookup"><span data-stu-id="146a0-176">Your Azure account is now authorized tooperform any operations on this key vault.</span></span> <span data-ttu-id="146a0-177">coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="146a0-177">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-toohello-key-vault"></a><span data-ttu-id="146a0-178">Ajouter une clé ou un coffre de clés secrètes toohello</span><span class="sxs-lookup"><span data-stu-id="146a0-178">Add a key or secret toohello key vault</span></span>

<span data-ttu-id="146a0-179">Si vous souhaitez que le coffre de clés Azure toocreate une clé protégée par logiciel pour vous, utilisez hello `azure key create` de commandes et tapez Bonjour qui suit :</span><span class="sxs-lookup"><span data-stu-id="146a0-179">If you want Azure Key Vault toocreate a software-protected key for you, use hello `azure key create` command, and type hello following:</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

<span data-ttu-id="146a0-180">Toutefois, si vous avez une clé existante dans un fichier .pem enregistré en tant que fichier local dans un fichier nommé softkey.pem que vous souhaitez tooupload tooAzure le coffre de clés, tapez Bonjour suivant clé de hello tooimport hello. Fichier PEM, qui protège la clé de hello par logiciel dans hello service Key Vault :</span><span class="sxs-lookup"><span data-stu-id="146a0-180">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want tooupload tooAzure Key Vault, type hello following tooimport hello key from hello .PEM file, which protects hello key by software in hello Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

<span data-ttu-id="146a0-181">Vous pouvez maintenant référencer clé hello que vous avez créé ou téléchargé tooAzure le coffre de clés, à l’aide de son URI.</span><span class="sxs-lookup"><span data-stu-id="146a0-181">You can now reference hello key that you created or uploaded tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="146a0-182">Utilisez **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways obtenir la version actuelle de hello et utiliser **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget cette version spécifique.</span><span class="sxs-lookup"><span data-stu-id="146a0-182">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways get hello current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget this specific version.</span></span>

<span data-ttu-id="146a0-183">tooadd un coffre toohello secrète, qui est un mot de passe nommé SQLPassword et qui a valeur hello Pa$ $w0rd tooAzure le coffre de clés, hello du type suivant :</span><span class="sxs-lookup"><span data-stu-id="146a0-183">tooadd a secret toohello vault, which is a password named SQLPassword and that has hello value of Pa$$w0rd tooAzure Key Vault, type hello following:</span></span>

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

<span data-ttu-id="146a0-184">Vous pouvez maintenant référencer ce mot de passe que vous avez ajouté tooAzure le coffre de clés, à l’aide de son URI.</span><span class="sxs-lookup"><span data-stu-id="146a0-184">You can now reference this password that you added tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="146a0-185">Utilisez **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways obtenir la version actuelle de hello et utiliser **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget cette version spécifique.</span><span class="sxs-lookup"><span data-stu-id="146a0-185">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways get hello current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget this specific version.</span></span>

<span data-ttu-id="146a0-186">Examinons la clé de hello ou le secret que vous venez de créer :</span><span class="sxs-lookup"><span data-stu-id="146a0-186">Let's view hello key or secret that you just created:</span></span>

* <span data-ttu-id="146a0-187">tooview votre type de clé, :`azure keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="146a0-187">tooview your key, type: `azure keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="146a0-188">tooview votre secret principal, type :`azure keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="146a0-188">tooview your secret, type: `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="146a0-189">Inscription d’une application auprès d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="146a0-189">Register an application with Azure Active Directory</span></span>

<span data-ttu-id="146a0-190">Cette étape est généralement effectuée par un développeur et sur un ordinateur distinct.</span><span class="sxs-lookup"><span data-stu-id="146a0-190">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="146a0-191">Il n’est pas spécifique tooAzure le coffre de clés, mais est inclus ici, par souci d’exhaustivité.</span><span class="sxs-lookup"><span data-stu-id="146a0-191">It is not specific tooAzure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="146a0-192">didacticiel de hello toocomplete, votre compte, le coffre de hello et l’application hello que vous inscrivez dans cette étape doivent toutes être Bonjour même annuaire Azure.</span><span class="sxs-lookup"><span data-stu-id="146a0-192">toocomplete hello tutorial, your account, hello vault, and hello application that you will register in this step must all be in hello same Azure directory.</span></span>
> 
> 

<span data-ttu-id="146a0-193">Les applications qui utilisent un coffre de clés doivent s’authentifier à l’aide d’un jeton à partir d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="146a0-193">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="146a0-194">toodo, hello propriétaire de l’application hello doit inscrire tout d’abord des application hello dans leur annuaire Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="146a0-194">toodo this, hello owner of hello application must first register hello application in their Azure Active Directory.</span></span> <span data-ttu-id="146a0-195">À fin hello d’enregistrement, le propriétaire de l’application hello obtient hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="146a0-195">At hello end of registration, hello application owner gets hello following values:</span></span>

* <span data-ttu-id="146a0-196">Un **ID d’Application** (également appelé ID de Client) et **clé d’authentification** (également appelé un secret partagé hello).</span><span class="sxs-lookup"><span data-stu-id="146a0-196">An **Application ID** (also known as a Client ID) and **authentication key** (also known as hello shared secret).</span></span> <span data-ttu-id="146a0-197">application Hello doit présenter les deux de ces valeurs de tooAzure Active Directory, tooget un jeton.</span><span class="sxs-lookup"><span data-stu-id="146a0-197">hello application must present both of these values tooAzure Active Directory, tooget a token.</span></span> <span data-ttu-id="146a0-198">Comment application hello est configuré toodo que cela dépend application hello.</span><span class="sxs-lookup"><span data-stu-id="146a0-198">How hello application is configured toodo this depends on hello application.</span></span> <span data-ttu-id="146a0-199">Pour un exemple d’application le coffre de clés de hello, le propriétaire de l’application hello définit ces valeurs dans le fichier app.config hello.</span><span class="sxs-lookup"><span data-stu-id="146a0-199">For hello Key Vault sample application, hello application owner sets these values in hello app.config file.</span></span>

<span data-ttu-id="146a0-200">application hello tooregister dans Azure Active Directory :</span><span class="sxs-lookup"><span data-stu-id="146a0-200">tooregister hello application in Azure Active Directory:</span></span>

1. <span data-ttu-id="146a0-201">Se connecter toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="146a0-201">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="146a0-202">Sur hello gauche, cliquez sur **Active Directory**, puis sélectionnez le répertoire hello dans lequel vous allez inscrire votre application.</span><span class="sxs-lookup"><span data-stu-id="146a0-202">On hello left, click **Active Directory**, and then select hello directory in which you will register your application.</span></span> <br> <br> 

>[!NOTE] 
> <span data-ttu-id="146a0-203">Vous devez sélectionner hello même répertoire contienne hello abonnement Azure avec lequel vous avez créé votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="146a0-203">You must select hello same directory that contains hello Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="146a0-204">Si vous ne savez pas quel répertoire cela est, cliquez sur **paramètres**, d’identifier l’abonnement hello avec lequel vous avez créé votre coffre de clés et nom de hello note du répertoire de hello affiché dans la dernière colonne de hello.</span><span class="sxs-lookup"><span data-stu-id="146a0-204">If you do not know which directory this is, click **Settings**, identify hello subscription with which you created your key vault, and note hello name of hello directory displayed in hello last column.</span></span>

3. <span data-ttu-id="146a0-205">Cliquez sur **APPLICATIONS**.</span><span class="sxs-lookup"><span data-stu-id="146a0-205">Click **APPLICATIONS**.</span></span> <span data-ttu-id="146a0-206">Si aucune application n’a été ajoutée tooyour active, cette page affiche uniquement hello **ajouter une application** lien.</span><span class="sxs-lookup"><span data-stu-id="146a0-206">If no apps have been added tooyour directory, this page will show only hello **Add an App** link.</span></span> <span data-ttu-id="146a0-207">Cliquez sur le lien de hello, ou vous pouvez également cliquer hello **ajouter** sur la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="146a0-207">Click hello link, or alternatively, you can click hello **ADD** on hello command bar.</span></span>
4. <span data-ttu-id="146a0-208">Bonjour **ajouter une APPLICATION** Assistant, sur hello **comment vous souhaitez toodo ?** , cliquez sur **ajouter une application développée par mon organisation**.</span><span class="sxs-lookup"><span data-stu-id="146a0-208">In hello **ADD APPLICATION** wizard, on hello **What do you want toodo?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="146a0-209">Sur hello **Parlez-nous de votre application** page, spécifiez un nom pour votre application et sélectionnez **WEB APPLICATION et/ou API WEB** (hello par défaut).</span><span class="sxs-lookup"><span data-stu-id="146a0-209">On hello **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (hello default).</span></span> <span data-ttu-id="146a0-210">Cliquez sur icône suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="146a0-210">Click hello Next icon.</span></span>
6. <span data-ttu-id="146a0-211">Sur hello **propriétés de l’application** , spécifiez hello **URL de connexion** et **URI ID d’application** pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="146a0-211">On hello **App properties** page, specify hello **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="146a0-212">Si votre application n’a pas ces valeurs, vous pouvez les créer pour cette étape (par exemple, vous pouvez spécifier http://test1.contoso.com pour les deux zones).</span><span class="sxs-lookup"><span data-stu-id="146a0-212">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="146a0-213">Il n’a pas d’importance s’il existe de ces sites ; l’essentiel est que URI ID d’application hello pour chaque application est différente pour chaque application dans votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="146a0-213">It does not matter if these sites exist; what is important is that hello app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="146a0-214">répertoire de Hello utilise tooidentify de cette chaîne de votre application.</span><span class="sxs-lookup"><span data-stu-id="146a0-214">hello directory uses this string tooidentify your app.</span></span>
7. <span data-ttu-id="146a0-215">Cliquez sur hello icône terminée toosave vos modifications dans l’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="146a0-215">Click hello Complete icon toosave your changes in hello wizard.</span></span>
8. <span data-ttu-id="146a0-216">Dans la page de démarrage rapide de hello, cliquez sur **configurer**.</span><span class="sxs-lookup"><span data-stu-id="146a0-216">On hello Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="146a0-217">Faites défiler toohello **clés** section, sélectionnez la durée de hello, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="146a0-217">Scroll toohello **keys** section, select hello duration, and then click **SAVE**.</span></span> <span data-ttu-id="146a0-218">page de Hello actualise et affiche maintenant une valeur de clé.</span><span class="sxs-lookup"><span data-stu-id="146a0-218">hello page refreshes and now shows a key value.</span></span> <span data-ttu-id="146a0-219">Vous devez configurer votre application avec cette valeur de clé et le hello **ID CLIENT** valeur.</span><span class="sxs-lookup"><span data-stu-id="146a0-219">You must configure your application with this key value and hello **CLIENT ID** value.</span></span> <span data-ttu-id="146a0-220">(Les instructions relatives à cette configuration sont propres à l’application).</span><span class="sxs-lookup"><span data-stu-id="146a0-220">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="146a0-221">Copiez la valeur d’ID client hello à partir de cette page, vous allez utiliser dans hello prochaine étape tooset des autorisations sur votre coffre.</span><span class="sxs-lookup"><span data-stu-id="146a0-221">Copy hello client ID value from this page, which you will use in hello next step tooset permissions on your vault.</span></span>

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a><span data-ttu-id="146a0-222">Autoriser hello application toouse hello clé ou le secret</span><span class="sxs-lookup"><span data-stu-id="146a0-222">Authorize hello application toouse hello key or secret</span></span>
<span data-ttu-id="146a0-223">tooauthorize hello application tooaccess hello clé ou le secret de coffre hello, utilisez hello `azure keyvault set-policy` commande.</span><span class="sxs-lookup"><span data-stu-id="146a0-223">tooauthorize hello application tooaccess hello key or secret in hello vault, use hello `azure keyvault set-policy` command.</span></span>

<span data-ttu-id="146a0-224">Par exemple, si votre nom de coffre est ContosoKeyVault et hello application souhaité tooauthorize a l’ID client 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, et que vous souhaitez tooauthorize hello application toodecrypt et connectez-vous avec des clés dans le coffre, puis exécutez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="146a0-224">For example, if your vault name is ContosoKeyVault and hello application you want tooauthorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want tooauthorize hello application toodecrypt and sign with keys in your vault, then run hello following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '[\"decrypt\",\"sign\"]'

> [!NOTE]
> <span data-ttu-id="146a0-225">Si vous exécutez sur l’invite de commandes Windows, vous devez remplacer les guillemets simples avec des guillemets doubles et également d’échappement hello interne des guillemets doubles.</span><span class="sxs-lookup"><span data-stu-id="146a0-225">If you are running on Windows command prompt, you should replace single quotes with double quotes, and also escape hello internal double quotes.</span></span> <span data-ttu-id="146a0-226">Par exemple : "[\"decrypt\",\"sign\"]".</span><span class="sxs-lookup"><span data-stu-id="146a0-226">For example: "[\"decrypt\",\"sign\"]".</span></span>
> 
> 

<span data-ttu-id="146a0-227">Si vous souhaitez tooauthorize que secrets de tooread même application dans le coffre, exécutez suivante de hello :</span><span class="sxs-lookup"><span data-stu-id="146a0-227">If you want tooauthorize that same application tooread secrets in your vault, run hello following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '[\"get\"]'

## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a><span data-ttu-id="146a0-228">Si vous voulez toouse un module de sécurité matériel (HSM)</span><span class="sxs-lookup"><span data-stu-id="146a0-228">If you want toouse a hardware security module (HSM)</span></span>
<span data-ttu-id="146a0-229">Pour plus de sûreté, vous pouvez importer ou générer des clés dans les modules de sécurité matériel (HSM) qui ne quittent jamais les limites HSM hello.</span><span class="sxs-lookup"><span data-stu-id="146a0-229">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="146a0-230">Hello HSM sont FIPS 140-2 niveau 2 validé.</span><span class="sxs-lookup"><span data-stu-id="146a0-230">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="146a0-231">Si cette exigence ne s’applique pas tooyou, ignorez cette section et passez trop[supprimer le coffre de clés hello et les clés associées et les secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="146a0-231">If this requirement doesn't apply tooyou, skip this section and go too[Delete hello key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="146a0-232">toocreate ces clés protégées par HSM, vous devez avoir un abonnement de coffre qui prend en charge les clés protégées par HSM.</span><span class="sxs-lookup"><span data-stu-id="146a0-232">toocreate these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="146a0-233">Lorsque vous créez hello keyvault, ajouter le paramètre de 'sku' hello :</span><span class="sxs-lookup"><span data-stu-id="146a0-233">When you create hello keyvault, add hello 'sku' parameter:</span></span>

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

<span data-ttu-id="146a0-234">Vous pouvez ajouter des clés protégées par le logiciel (comme indiqué plus haut) et de coffre de clés protégées par HSM toothis.</span><span class="sxs-lookup"><span data-stu-id="146a0-234">You can add software-protected keys (as shown earlier) and HSM-protected keys toothis vault.</span></span> <span data-ttu-id="146a0-235">toocreate une clé protégée par HSM, jeu hello Destination paramètre too'HSM':</span><span class="sxs-lookup"><span data-stu-id="146a0-235">toocreate an HSM-protected key, set hello Destination parameter too'HSM':</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

<span data-ttu-id="146a0-236">Vous pouvez utiliser hello suivant commande tooimport une clé à partir d’un fichier .pem sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="146a0-236">You can use hello following command tooimport a key from a .pem file on your computer.</span></span> <span data-ttu-id="146a0-237">Cette commande importe la clé de hello dans les modules HSM Bonjour service Key Vault :</span><span class="sxs-lookup"><span data-stu-id="146a0-237">This command imports hello key into HSMs in hello Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

<span data-ttu-id="146a0-238">commande suivant Hello importe un « apportez votre propre clé » package (BYOK).</span><span class="sxs-lookup"><span data-stu-id="146a0-238">hello next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="146a0-239">Cela vous permet de générer votre clé dans votre HSM local et la transférez tooHSMs Bonjour service Key Vault, sans clé hello en laissant la limite HSM hello :</span><span class="sxs-lookup"><span data-stu-id="146a0-239">This lets you generate your key in your local HSM, and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

<span data-ttu-id="146a0-240">Pour plus d’instructions sur la procédure toogenerate ce package BYOK, consultez [comment toouse clés HSM-Protected avec Azure Key Vault](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="146a0-240">For more detailed instructions about how toogenerate this BYOK package, see [How toouse HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="146a0-241">Supprimer le coffre de clés hello et les clés associées et les secrets</span><span class="sxs-lookup"><span data-stu-id="146a0-241">Delete hello key vault and associated keys and secrets</span></span>
<span data-ttu-id="146a0-242">Si vous n’avez plus besoin coffre de clés hello et clé de hello ou le secret qu’il contient, vous pouvez supprimer le coffre de clés hello en utilisant la commande de suppression keyvault hello azure :</span><span class="sxs-lookup"><span data-stu-id="146a0-242">If you no longer need hello key vault and hello key or secret that it contains, you can delete hello key vault by using hello azure keyvault delete command:</span></span>

    azure keyvault delete --vault-name 'ContosoKeyVault'

<span data-ttu-id="146a0-243">Ou bien, vous pouvez supprimer un groupe de ressources Azure entier, ce qui inclut le coffre de clés hello et d’autres ressources que vous avez incluses dans ce groupe :</span><span class="sxs-lookup"><span data-stu-id="146a0-243">Or, you can delete an entire Azure resource group, which includes hello key vault and any other resources that you included in that group:</span></span>

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="146a0-244">Autres interfaces de ligne de commande interplateformes Azure</span><span class="sxs-lookup"><span data-stu-id="146a0-244">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="146a0-245">Autres commandes qui peuvent être utiles pour la gestion d’Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="146a0-245">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="146a0-246">Cette commande permet d’obtenir un affichage sous forme de tableau de l’ensemble des clés et des propriétés sélectionnées :</span><span class="sxs-lookup"><span data-stu-id="146a0-246">This command lists a tabular display of all keys and selected properties:</span></span>

    azure keyvault key list --vault-name 'ContosoKeyVault'

<span data-ttu-id="146a0-247">Cette commande affiche une liste complète des propriétés de clé spécifiée de hello :</span><span class="sxs-lookup"><span data-stu-id="146a0-247">This command displays a full list of properties for hello specified key:</span></span>

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="146a0-248">Cette commande permet d’obtenir un affichage sous forme de tableau de l’ensemble des secrets et des propriétés sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="146a0-248">This command lists a tabular display of all secret names and selected properties:</span></span>

    azure keyvault secret list --vault-name 'ContosoKeyVault'

<span data-ttu-id="146a0-249">Voici un exemple de procédure tooremove une clé spécifique :</span><span class="sxs-lookup"><span data-stu-id="146a0-249">Here's an example of how tooremove a specific key:</span></span>

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="146a0-250">Voici un exemple de procédure tooremove un secret spécifique :</span><span class="sxs-lookup"><span data-stu-id="146a0-250">Here's an example of how tooremove a specific secret:</span></span>

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a><span data-ttu-id="146a0-251">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="146a0-251">Next steps</span></span>
<span data-ttu-id="146a0-252">Pour les références de programmation, consultez [hello guide du développeur Azure Key Vault](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="146a0-252">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

