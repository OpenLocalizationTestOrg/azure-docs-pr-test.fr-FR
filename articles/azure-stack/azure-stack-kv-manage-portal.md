---
title: "aaaManage le coffre de clés dans la pile de Azure à l’aide de PowerShell | Documents Microsoft"
description: "Découvrez comment toomanage le coffre de clés dans la pile de Azure à l’aide de PowerShell."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 0a3aa6eb0b2c2976935d995a0bf6f226dc4eac84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-in-azure-stack-using-hello-portal"></a><span data-ttu-id="c0387-103">Gérer le coffre de clés dans la pile d’Azure à l’aide du portail de hello</span><span class="sxs-lookup"><span data-stu-id="c0387-103">Manage Key Vault in Azure Stack using hello portal</span></span>

<span data-ttu-id="c0387-104">Vous pouvez gérer le coffre de clés dans la pile d’Azure à l’aide du portail de pile de Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c0387-104">You can manage Key Vault in Azure Stack by using hello Azure Stack portal.</span></span> <span data-ttu-id="c0387-105">Cet article vous aidera à obtenir toocreate démarrée et gérer le coffre de clés dans la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="c0387-105">This article helps you get started toocreate and manage Key Vault in Azure Stack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c0387-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c0387-106">Prerequisites</span></span>  

* <span data-ttu-id="c0387-107">Les administrateurs de cloud Azure pile doivent avoir [créé une offre](azure-stack-create-offer.md) qui inclut le service de coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="c0387-107">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes hello Key Vault service.</span></span>  
* <span data-ttu-id="c0387-108">Les utilisateurs doivent [s’abonner tooan offre](azure-stack-subscribe-plan-provision-vm.md) qui inclut le service de coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="c0387-108">Users must [subscribe tooan offer](azure-stack-subscribe-plan-provision-vm.md) that includes hello Key Vault service.</span></span>  
 
## <a name="create-a-key-vault"></a><span data-ttu-id="c0387-109">Création d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="c0387-109">Create a key vault</span></span> 

1. <span data-ttu-id="c0387-110">Se connecter dans le portail de l’utilisateur toohello (https://portal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="c0387-110">Sign in toohello user portal(https://portal.local.azurestack.external).</span></span>  

2. <span data-ttu-id="c0387-111">À partir du tableau de bord hello, cliquez sur **Nouveau > sécurité + identité > coffre de clés**.</span><span class="sxs-lookup"><span data-stu-id="c0387-111">From hello dashboard, click **New > Security + Identity > Key Vault**.</span></span>  

    ![Écran de KV](media/azure-stack-kv-manage-portal/image1.png)  

3. <span data-ttu-id="c0387-113">Sur hello **créer un coffre de clés** panneau, attribuer un **nom** pour votre archivage.</span><span class="sxs-lookup"><span data-stu-id="c0387-113">On hello **Create Key Vault** blade, assign a **Name** for your vault.</span></span> <span data-ttu-id="c0387-114">Nom du coffre peut contenir uniquement des caractères alphanumériques, trait d’union caractère spécial hello (-), et il ne doit pas commencer par un chiffre.</span><span class="sxs-lookup"><span data-stu-id="c0387-114">Vault name can contain only alphanumeric characters, hello special character hyphen (-), and it shouldn’t start with a number.</span></span>  

4. <span data-ttu-id="c0387-115">Choisissez un **abonnement** à partir de la liste de hello des abonnements disponibles.</span><span class="sxs-lookup"><span data-stu-id="c0387-115">Choose a **Subscription** from hello list of available subscriptions.</span></span> <span data-ttu-id="c0387-116">Tous les abonnements qui offrent un service de coffre de clés hello sont affichent dans la déroulante hello.</span><span class="sxs-lookup"><span data-stu-id="c0387-116">All subscriptions that offer hello Key Vault service are displayed in hello drop-down.</span></span>  

5. <span data-ttu-id="c0387-117">Sélectionnez un **Groupe de ressources** existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="c0387-117">Select an existing **Resource Group** or create a new one.</span></span>  

6. <span data-ttu-id="c0387-118">Sélectionnez hello **niveau tarifaire**.</span><span class="sxs-lookup"><span data-stu-id="c0387-118">Select hello **Pricing tier**.</span></span>  
    >[!NOTE]
    > <span data-ttu-id="c0387-119">Les coffres de clés dans le Kit de développement Azure Stack prennent uniquement en charge les SKU **Standard**.</span><span class="sxs-lookup"><span data-stu-id="c0387-119">Key vaults in Azure Stack Development Kit support **Standard** SKU only.</span></span>

7. <span data-ttu-id="c0387-120">Sélectionnez une **Stratégie d’accès** existante ou créez-en une.</span><span class="sxs-lookup"><span data-stu-id="c0387-120">Choose an existing **Access policies** or create a new one.</span></span> <span data-ttu-id="c0387-121">Stratégie d’accès vous permet de toogrant les autorisations pour un utilisateur, d’application ou d’une sécurité tooperform regrouper des opérations avec ce coffre.</span><span class="sxs-lookup"><span data-stu-id="c0387-121">Access policy allows you toogrant permissions for a user, application, or a security group tooperform operations with this vault.</span></span>  

8. <span data-ttu-id="c0387-122">Si vous le souhaitez, choisissez une **stratégie d’accès avancé** fonctionnalités hello tooenable accéder aux Machines tooVirtual pour le déploiement, tooResource le Gestionnaire de déploiement d’un modèle d’accès et accéder tooAzure chiffrement de disque pour le volume chiffrement.</span><span class="sxs-lookup"><span data-stu-id="c0387-122">Optionally, choose an **Advanced access policy** tooenable hello features like access tooVirtual Machines for deployment, access tooResource Manager for template deployment and access tooAzure Disk Encryption for volume encryption.</span></span> 
  
9.  <span data-ttu-id="c0387-123">Après avoir configuré les paramètres de hello, cliquez sur **OK** , puis **créer**.</span><span class="sxs-lookup"><span data-stu-id="c0387-123">After configuring hello settings, click **OK** and then **Create**.</span></span> <span data-ttu-id="c0387-124">Déploiement de coffre de clés hello démarre.</span><span class="sxs-lookup"><span data-stu-id="c0387-124">This starts hello key vault deployment.</span></span> 

## <a name="manage-keys-and-secrets"></a><span data-ttu-id="c0387-125">Gérer les clés et les secrets</span><span class="sxs-lookup"><span data-stu-id="c0387-125">Manage keys and secrets</span></span>

<span data-ttu-id="c0387-126">Après avoir créé un coffre, hello suivant les étapes toocreate et gérer les clés et les secrets dans le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="c0387-126">After you create a vault, use hello following steps toocreate and manage keys and secrets within hello vault.</span></span>

## <a name="create-a-key"></a><span data-ttu-id="c0387-127">Créer une clé</span><span class="sxs-lookup"><span data-stu-id="c0387-127">Create a key</span></span>

1. <span data-ttu-id="c0387-128">Se connecter dans le portail de l’utilisateur toohello (https://portal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="c0387-128">Sign in toohello user portal (https://portal.local.azurestack.external).</span></span>  

2. <span data-ttu-id="c0387-129">À partir du tableau de bord hello, cliquez sur **toutes les ressources** > coffre de clés hello select que vous avez créé précédemment > cliquez sur hello **clés** vignette.</span><span class="sxs-lookup"><span data-stu-id="c0387-129">From hello dashboard, click **All resources** > select hello key vault that you created earlier> click hello **Keys** tile.</span></span>  

3. <span data-ttu-id="c0387-130">À partir de hello **clés** panneau, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c0387-130">From hello **Keys** blade, click **Add**.</span></span> 

4. <span data-ttu-id="c0387-131">Sur hello **créer une clé** panneau, formulaire de liste hello de **Options**, choisissez la méthode hello que vous souhaitez toouse toocreate une clé.</span><span class="sxs-lookup"><span data-stu-id="c0387-131">On hello **Create a key** blade, form hello list of **Options**, choose hello method that you want toouse toocreate a key.</span></span> <span data-ttu-id="c0387-132">Vous pouvez **Générer** une nouvelle clé, **Charger** une clé existante ou **Restaurer la sauvegarde** d’une clé.</span><span class="sxs-lookup"><span data-stu-id="c0387-132">You can **Generate** a new key, **Upload** an existing key, or **Restore Backup** key.</span></span>  

5. <span data-ttu-id="c0387-133">Entrez un **Nom** pour votre clé.</span><span class="sxs-lookup"><span data-stu-id="c0387-133">Enter a **Name** for your key.</span></span> <span data-ttu-id="c0387-134">nom de la clé Hello peut contenir uniquement des caractères alphanumériques et des tirets de caractère spécial hello (-).</span><span class="sxs-lookup"><span data-stu-id="c0387-134">hello key name can contain only alphanumeric characters and hello special character hyphen (-).</span></span>  

6. <span data-ttu-id="c0387-135">Éventuellement, configurez les valeurs **Définir la date d’activation** et **Définir la date d’expiration** pour votre clé.</span><span class="sxs-lookup"><span data-stu-id="c0387-135">Optionally, configure **Set activation date** and **Set expiration date** values for your key.</span></span>  

7. <span data-ttu-id="c0387-136">Cliquez sur **créer** déploiement de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="c0387-136">Click **Create** toostart hello deployment.</span></span>  

<span data-ttu-id="c0387-137">Une fois la clé de hello est correctement créé, vous pouvez le sélectionner dans hello **clés** panneau et afficher ou modifier ses propriétés.</span><span class="sxs-lookup"><span data-stu-id="c0387-137">After hello key is successfully created, you can select it from hello **Keys** blade and view or modify its properties.</span></span> <span data-ttu-id="c0387-138">section des propriétés Hello contient hello **identificateur de clé**, un URI à laquelle des applications externes peuvent accéder à cette clé.</span><span class="sxs-lookup"><span data-stu-id="c0387-138">hello properties section contains hello **Key Identifier**, a URI by which external applications can access this key.</span></span> <span data-ttu-id="c0387-139">opérations de toolimit sur cette clé, configurez les paramètres sous **opérations autorisées**.</span><span class="sxs-lookup"><span data-stu-id="c0387-139">toolimit operations on this key, configure settings under **Permitted operations**.</span></span>

![URI de clé](media/azure-stack-kv-manage-portal/image4.png)  

## <a name="create-a-secret"></a><span data-ttu-id="c0387-141">Créer un secret</span><span class="sxs-lookup"><span data-stu-id="c0387-141">Create a secret</span></span> 

1. <span data-ttu-id="c0387-142">Se connecter dans le portail de l’utilisateur toohello (https://portal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="c0387-142">Sign in toohello user portal (https://portal.local.azurestack.external).</span></span>  
2. <span data-ttu-id="c0387-143">À partir du tableau de bord hello, cliquez sur **toutes les ressources** > coffre de clés hello select que vous avez créé précédemment > cliquez sur hello **Secrets** vignette.</span><span class="sxs-lookup"><span data-stu-id="c0387-143">From hello dashboard, click **All resources** > select hello key vault that you created earlier> click hello **Secrets** tile.</span></span>  

3. <span data-ttu-id="c0387-144">À partir de hello **Secrets** panneau, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c0387-144">From hello **Secrets** blade, click **Add**.</span></span>  

4. <span data-ttu-id="c0387-145">Sur hello **créer une clé secrète** panneau, à partir de la liste des hello **options de téléchargement**, choisissez une option en fonction duquel vous voulez toocreate un secret.</span><span class="sxs-lookup"><span data-stu-id="c0387-145">On hello **Create a secret** blade, from hello list of **Upload options**, choose an option by which you want toocreate a secret.</span></span> <span data-ttu-id="c0387-146">Vous pouvez créer une clé secrète **manuellement** en entrant une valeur pour la clé secrète de hello, ou en téléchargeant un **certificat** à partir de votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="c0387-146">You can create a secret **Manually** by entering a value for hello secret, or by uploading a **Certificate** from your local machine.</span></span>  

5. <span data-ttu-id="c0387-147">Entrez un **nom** pour secret de hello.</span><span class="sxs-lookup"><span data-stu-id="c0387-147">Enter a **Name** for hello secret.</span></span> <span data-ttu-id="c0387-148">nom de clé secrète Hello peut contenir uniquement des caractères alphanumériques et des tirets de caractère spécial hello (-).</span><span class="sxs-lookup"><span data-stu-id="c0387-148">hello secret name can contain only alphanumeric characters and hello special character hyphen (-).</span></span>  

6. <span data-ttu-id="c0387-149">Si vous le souhaitez, spécifier hello **le type de contenu**et configurez les valeurs de **définir la date d’activation** et **définir la date d’expiration** valeurs pour la clé secrète de hello.</span><span class="sxs-lookup"><span data-stu-id="c0387-149">Optionally, specify hello **Content type**, and configure values for **Set activation date** and **Set expiration date** values for hello secret.</span></span>  

7. <span data-ttu-id="c0387-150">Cliquez sur Créer toostart hello déploiement.</span><span class="sxs-lookup"><span data-stu-id="c0387-150">Click Create toostart hello deployment.</span></span>  

<span data-ttu-id="c0387-151">Une fois que le secret de hello est correctement créé, vous pouvez le sélectionner dans hello **Secrets** panneau et afficher ou modifier ses propriétés.</span><span class="sxs-lookup"><span data-stu-id="c0387-151">After hello secret is successfully created, you can select it from hello **Secrets** blade and view or modify its properties.</span></span> <span data-ttu-id="c0387-152">section des propriétés Hello contient **identificateur de clé secrète**, un URI par lequel les applications externes peuvent accéder à ce mot de passe.</span><span class="sxs-lookup"><span data-stu-id="c0387-152">hello properties section contains **Secret Identifier**, a URI by which external applications can access this secret.</span></span> 

![URI de secret](media/azure-stack-kv-manage-portal/image5.png) 


## <a name="next-steps"></a><span data-ttu-id="c0387-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c0387-154">Next Steps</span></span>
* [<span data-ttu-id="c0387-155">Déployer un ordinateur virtuel par la récupération de mot de passe hello stocké dans un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="c0387-155">Deploy a VM by retrieving hello password stored in a key vault</span></span>](azure-stack-kv-deploy-vm-with-secret.md)  
* [<span data-ttu-id="c0387-156">Déployer une machine virtuelle avec un certificat stocké dans un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="c0387-156">Deploy a VM with certificate stored in a key vault</span></span>](azure-stack-kv-push-secret-into-vm.md)     


