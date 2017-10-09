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
ms.openlocfilehash: 37adddf8da02766559f4d61134a9d5ce47377da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-in-azure-stack-using-powershell"></a><span data-ttu-id="61e97-103">Gérer Key Vault dans Azure Stack à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="61e97-103">Manage Key Vault in Azure Stack using PowerShell</span></span>

<span data-ttu-id="61e97-104">Cet article vous aidera à obtenir toocreate démarrée et gérer le coffre de clés dans la pile d’Azure à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="61e97-104">This article helps you get started toocreate and manage Key Vault in Azure Stack by using PowerShell.</span></span> <span data-ttu-id="61e97-105">applets de commande PowerShell de coffre de clé Hello décrits dans cet article sont disponibles dans le cadre de hello Kit de développement logiciel Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="61e97-105">hello Key Vault PowerShell cmdlets described in this article are available as a part of hello Azure PowerShell SDK.</span></span> <span data-ttu-id="61e97-106">Hello sections suivantes décrivent des hello applets de commande PowerShell sont requis toocreate un coffre, stocker et gérer les clés de chiffrement et les clés secrètes ainsi autoriser des utilisateurs ou des applications opérations tooinvoke dans le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="61e97-106">hello following sections describe hello PowerShell cmdlets that are required toocreate a vault, store, and manage cryptographic keys and secrets as well as authorize users or applications tooinvoke operations in hello vault.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="61e97-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="61e97-107">Prerequisites</span></span>
* [<span data-ttu-id="61e97-108">Installer PowerShell pour Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="61e97-108">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* <span data-ttu-id="61e97-109">Les administrateurs de cloud Azure pile doivent avoir [créé une offre](azure-stack-create-offer.md) qui inclut le service de coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="61e97-109">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes hello Key Vault service.</span></span>  
* <span data-ttu-id="61e97-110">Les utilisateurs doivent [s’abonner tooan offre](azure-stack-subscribe-plan-provision-vm.md) qui inclut le service de coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="61e97-110">Users must [subscribe tooan offer](azure-stack-subscribe-plan-provision-vm.md) that includes hello Key Vault service.</span></span> 
* [<span data-ttu-id="61e97-111">Configurer l’environnement de l’utilisateur hello pile d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="61e97-111">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)

## <a name="enable-your-tenant-subscription-for-vault-operations"></a><span data-ttu-id="61e97-112">Activer votre abonnement de locataire pour les opérations de coffre</span><span class="sxs-lookup"><span data-stu-id="61e97-112">Enable your tenant subscription for vault operations</span></span>

<span data-ttu-id="61e97-113">Avant de pouvoir émettre des opérations sur un coffre de clés, vous devez tooensure votre abonnement client est activée pour les opérations de coffre.</span><span class="sxs-lookup"><span data-stu-id="61e97-113">Before you can issue any operations against a key vault, you need tooensure that your tenant subscription is enabled for vault operations.</span></span> <span data-ttu-id="61e97-114">tooverify, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="61e97-114">tooverify, run hello following command:</span></span>

```PowerShell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -Autosize
```
<span data-ttu-id="61e97-115">**Sortie**</span><span class="sxs-lookup"><span data-stu-id="61e97-115">**Output**</span></span>

<span data-ttu-id="61e97-116">Si votre abonnement est activé pour les opérations d’archivage, sortie de hello affiche « RegistrationState » est égal à « Enregistré » pour tous les types de ressources d’un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="61e97-116">If your subscription is enabled for vault operations, hello output shows “RegistrationState” equals “Registered” for all resource types of a key vault.</span></span>

![état de l’inscription](media/azure-stack-kv-manage-powershell/image1.png)

<span data-ttu-id="61e97-118">Si tel n’est pas le cas de hello, appelez hello suivant du service de coffre de clés commande tooregister hello dans votre abonnement :</span><span class="sxs-lookup"><span data-stu-id="61e97-118">If that’s not hello case, invoke hello following command tooregister hello Key Vault service in your subscription:</span></span>

```PowerShell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault
```

<span data-ttu-id="61e97-119">**Sortie**</span><span class="sxs-lookup"><span data-stu-id="61e97-119">**Output**</span></span>

<span data-ttu-id="61e97-120">Si l’inscription de hello a réussi, hello sortie suivante est retournée :</span><span class="sxs-lookup"><span data-stu-id="61e97-120">If hello registration is successful, hello following output is returned:</span></span>

![inscription](media/azure-stack-kv-manage-powershell/image2.png)

<span data-ttu-id="61e97-122">Hello sections suivantes supposent service Key Vault est enregistré au sein de l’abonnement d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="61e97-122">hello following sections assume Key Vault service is registered within hello user subscription.</span></span> <span data-ttu-id="61e97-123">Lors de l’appel des commandes de coffre de clés, si vous obtenez une erreur s’affiche : « abonnement de hello n’est pas un espace de noms toouse inscrit ' Microsoft.KeyVault », confirmez que vous avez [activé le fournisseur de ressources de coffre de clés hello](#enable-your-tenant-subscription-for-vault-operations) conformément aux instructions indiqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="61e97-123">When invoking key vault commands, if you get an error- "hello subscription is not registered toouse namespace ‘Microsoft.KeyVault" then, confirm that you have [enabled hello Key Vault resource provider](#enable-your-tenant-subscription-for-vault-operations) as per instructions mentioned earlier.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="61e97-124">Création d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="61e97-124">Create a key vault</span></span> 

<span data-ttu-id="61e97-125">Avant de créer un coffre de clés, créez un groupe de ressources pour que toutes les ressources associées au coffre de clés existent dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="61e97-125">Before you create a key vault, create a resource group so that all key vault related resources exist in a resource group.</span></span> <span data-ttu-id="61e97-126">Utilisez hello suivant commande toocreate un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="61e97-126">Use hello following command toocreate a new resource group:</span></span>

```PowerShell
New-AzureRmResourceGroup -Name “VaultRG” -Location local -verbose -Force

```

<span data-ttu-id="61e97-127">**Sortie**</span><span class="sxs-lookup"><span data-stu-id="61e97-127">**Output**</span></span>

![new resource group](media/azure-stack-kv-manage-powershell/image3.png)

<span data-ttu-id="61e97-129">À présent, utiliser hello **New-AzureRMKeyVault** commande toocreate un coffre de clés dans le groupe de ressources hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="61e97-129">Now, use hello **New-AzureRMKeyVault** command toocreate a key vault in hello resource group that you created earlier.</span></span> <span data-ttu-id="61e97-130">Cette commande lit trois paramètres obligatoires : le nom du groupe de ressources, le nom du coffre de clés et l’emplacement géographique.</span><span class="sxs-lookup"><span data-stu-id="61e97-130">This command reads three mandatory parameters- resource group name, key vault name, and geographic location.</span></span> 

<span data-ttu-id="61e97-131">Exécutez hello suivant commande toocreate un coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="61e97-131">Run hello following command toocreate a key vault:</span></span>

```PowerShell
New-AzureRmKeyVault -VaultName “Vault01” -ResourceGroupName “VaultRG” -Location local -verbose
```
<span data-ttu-id="61e97-132">**Sortie**</span><span class="sxs-lookup"><span data-stu-id="61e97-132">**Output**</span></span>

![nouveau coffre de clés](media/azure-stack-kv-manage-powershell/image4.png)

<span data-ttu-id="61e97-134">sortie Hello de cette commande affiche les propriétés de hello de coffre de clés hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="61e97-134">hello output of this command shows hello properties of hello key vault that you created.</span></span> <span data-ttu-id="61e97-135">Lorsqu’une application accède à ce coffre, elle utilise hello **coffre URI** propriété indiquée dans la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="61e97-135">When an application accesses this vault, it uses hello **Vault URI** property shown in hello output.</span></span> <span data-ttu-id="61e97-136">Par exemple, le coffre hello URI ici est **https://vault01.vault.local.azurestack.external**.</span><span class="sxs-lookup"><span data-stu-id="61e97-136">For example, hello vault URI here is **https://vault01.vault.local.azurestack.external**.</span></span> <span data-ttu-id="61e97-137">Les applications qui interagissent avec ce coffre de clés par le biais de l’API REST doivent utiliser cet URI.</span><span class="sxs-lookup"><span data-stu-id="61e97-137">Applications interacting with this key vault through REST API must use this URI.</span></span>

<span data-ttu-id="61e97-138">Dans les déploiements AD FS, quand vous créez un coffre de clés à l’aide de PowerShell, vous pouvez recevoir un avertissement indiquant que la stratégie d’accès n’est pas définie</span><span class="sxs-lookup"><span data-stu-id="61e97-138">In ADFS-based deployments, when you create a key vault by using PowerShell, you might receive a warning that says "Access policy is not set.</span></span> <span data-ttu-id="61e97-139">Aucun utilisateur ou l’application n’a accès autorisation toouse cet archivage ».</span><span class="sxs-lookup"><span data-stu-id="61e97-139">No user or application has access permission toouse this vault".</span></span> <span data-ttu-id="61e97-140">tooresolve ce problème, définissez une stratégie d’accès pour l’archivage hello par à l’aide de hello [Set-AzureRmKeyVaultAccessPolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret) commande :</span><span class="sxs-lookup"><span data-stu-id="61e97-140">tooresolve this issue, set an access policy for hello vault by using hello [Set-AzureRmKeyVaultAccessPolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret) command:</span></span>

```PowerShell
# Obtain hello security identifier(SID) of hello active directory user
$adUser = Get-ADUser -Filter "Name -eq '{Active directory user name}'"
$objectSID = $adUser.SID.Value 

#Set hello key vault access policy
Set-AzureRmKeyVaultAccessPolicy -VaultName "{key vault name}" -ResourceGroupName "{resource group name}" -ObjectId "{object SID}" -PermissionsToKeys {permissionsToKeys} -PermissionsToSecrets {permissionsToSecrets} -BypassObjectIdValidation 
```

## <a name="manage-keys-and-secrets"></a><span data-ttu-id="61e97-141">Gérer les clés et les secrets</span><span class="sxs-lookup"><span data-stu-id="61e97-141">Manage keys and secrets</span></span>

<span data-ttu-id="61e97-142">Après avoir créé un coffre, hello suivant les étapes toocreate et gérer les clés et les secrets dans le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="61e97-142">After creating a vault, use hello following steps toocreate and manage keys and secrets within hello vault.</span></span>

### <a name="create-a-key"></a><span data-ttu-id="61e97-143">Créer une clé</span><span class="sxs-lookup"><span data-stu-id="61e97-143">Create a key</span></span>

<span data-ttu-id="61e97-144">Hello d’utilisation **Add-AzureKeyVaultKey** commande toocreate ou importer une clé protégée de logiciel dans un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="61e97-144">Use hello **Add-AzureKeyVaultKey** command toocreate or import a software protected key in a key vault.</span></span> 

```PowerShell
Add-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01” -verbose -Destination Software
```
<span data-ttu-id="61e97-145">Hello **Destination** sert de paramètre toospecify cette clé hello est protégé par un logiciel.</span><span class="sxs-lookup"><span data-stu-id="61e97-145">hello **Destination** parameter is used toospecify that hello key is software protected.</span></span> <span data-ttu-id="61e97-146">Lors de la clé de hello est correctement créé, commande hello renvoie les détails de hello Hello crée de la clé.</span><span class="sxs-lookup"><span data-stu-id="61e97-146">When hello key is successfully created, hello command outputs hello details of hello created key.</span></span>

<span data-ttu-id="61e97-147">**Sortie**</span><span class="sxs-lookup"><span data-stu-id="61e97-147">**Output**</span></span>

![Nouvelle clé](media/azure-stack-kv-manage-powershell/image5.png)

<span data-ttu-id="61e97-149">Vous pouvez maintenant référencer hello créé de la clé à l’aide de son URI.</span><span class="sxs-lookup"><span data-stu-id="61e97-149">You can now reference hello created key by using its URI.</span></span> <span data-ttu-id="61e97-150">Si vous créez ou importez une clé qui a le même nom qu’une clé existante, la clé d’origine de hello est mise à jour avec les valeurs hello qui sont spécifiés dans la nouvelle clé de hello.</span><span class="sxs-lookup"><span data-stu-id="61e97-150">If you create or import a key that has same name as an existing key, hello original key is updated with hello values that are specified in hello new key.</span></span>  <span data-ttu-id="61e97-151">Vous pouvez accéder à version précédente de hello à l’aide spécifique à la version hello URI de clé de hello.</span><span class="sxs-lookup"><span data-stu-id="61e97-151">You can access hello previous version by using hello version-specific URI of hello key.</span></span> <span data-ttu-id="61e97-152">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="61e97-152">For example,</span></span> 

* <span data-ttu-id="61e97-153">Utilisez **https://vault10.vault.local.azurestack.external:443/clés/key01** tooalways obtenir la version actuelle de hello</span><span class="sxs-lookup"><span data-stu-id="61e97-153">Use **https://vault10.vault.local.azurestack.external:443/keys/key01** tooalways get hello current version</span></span>  
* <span data-ttu-id="61e97-154">Utilisez **https://vault010.vault.local.azurestack.external:443/clés/key01/d0b36ee2e3d14e9f967b8b6b1d38938a** tooget cette version spécifique</span><span class="sxs-lookup"><span data-stu-id="61e97-154">Use **https://vault010.vault.local.azurestack.external:443/keys/key01/d0b36ee2e3d14e9f967b8b6b1d38938a** tooget this specific version</span></span>

### <a name="get-a-key"></a><span data-ttu-id="61e97-155">Obtenir une clé</span><span class="sxs-lookup"><span data-stu-id="61e97-155">Get a key</span></span>

<span data-ttu-id="61e97-156">Hello d’utilisation **Get-AzureKeyVaultKey** commande tooread une clé et ses détails.</span><span class="sxs-lookup"><span data-stu-id="61e97-156">Use hello **Get-AzureKeyVaultKey** command tooread a key and its details.</span></span>

```PowerShell
Get-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01”
```

### <a name="create-a-secret"></a><span data-ttu-id="61e97-157">Créer un secret</span><span class="sxs-lookup"><span data-stu-id="61e97-157">Create a secret</span></span>

<span data-ttu-id="61e97-158">Hello d’utilisation **Set-AzureKeyVaultSecret** toocreate de commande ou de mettre à jour une clé secrète dans un coffre.</span><span class="sxs-lookup"><span data-stu-id="61e97-158">Use hello **Set-AzureKeyVaultSecret** command toocreate or update a secret in a vault.</span></span> <span data-ttu-id="61e97-159">Une clé secrète est créée si elle n’existe pas déjà, et une nouvelle version du secret de hello est créée s’il existe déjà.</span><span class="sxs-lookup"><span data-stu-id="61e97-159">A secret is created if it doesn’t already exist, and a new version of hello secret is created if it already exists.</span></span>

```PowerShell
$secretvalue = ConvertTo-SecureString “User@123” -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01” -SecretValue $secretvalue
```

<span data-ttu-id="61e97-160">**Sortie**</span><span class="sxs-lookup"><span data-stu-id="61e97-160">**Output**</span></span>

![créer un secret](media/azure-stack-kv-manage-powershell/image6.png)

### <a name="get-a-secret"></a><span data-ttu-id="61e97-162">Obtenir un secret</span><span class="sxs-lookup"><span data-stu-id="61e97-162">Get a secret</span></span>

<span data-ttu-id="61e97-163">Hello d’utilisation **Get-AzureKeyVaultSecret** commande tooread une clé secrète dans un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="61e97-163">Use hello **Get-AzureKeyVaultSecret** command tooread a secret in a key vault.</span></span> <span data-ttu-id="61e97-164">Cette commande peut retourner toutes les versions ou des versions spécifiques d’un secret.</span><span class="sxs-lookup"><span data-stu-id="61e97-164">This command can return all or specific versions of a secret.</span></span> 

```PowerShell
Get-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01”
```

<span data-ttu-id="61e97-165">Après avoir créé les clés et les clés secrètes, vous pouvez autoriser des applications externes toouse les.</span><span class="sxs-lookup"><span data-stu-id="61e97-165">After creating keys and secrets, you can authorize external applications toouse them.</span></span>

## <a name="authorize-an-application-toouse-a-key-or-secret"></a><span data-ttu-id="61e97-166">Autoriser un toouse application une clé ou une clé secrète</span><span class="sxs-lookup"><span data-stu-id="61e97-166">Authorize an application toouse a key or secret</span></span>

<span data-ttu-id="61e97-167">tooauthorize un tooaccess application une clé ou au secret dans hello clé de coffre, utilisez hello **Set-AzureRmKeyVaultAccessPolicy** commande.</span><span class="sxs-lookup"><span data-stu-id="61e97-167">tooauthorize an application tooaccess a key or secret in hello key vault, use hello **Set-AzureRmKeyVaultAccessPolicy** command.</span></span>
<span data-ttu-id="61e97-168">Par exemple, si le nom de votre coffre est ContosoKeyVault et hello application souhaité tooauthorize a l’ID Client 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed.</span><span class="sxs-lookup"><span data-stu-id="61e97-168">For example, if your vault name is ContosoKeyVault and hello application you want tooauthorize has a Client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed.</span></span> <span data-ttu-id="61e97-169">Exécutez hello après application de commande tooauthorize hello.</span><span class="sxs-lookup"><span data-stu-id="61e97-169">Run hello following command tooauthorize hello application.</span></span> <span data-ttu-id="61e97-170">Vous pouvez éventuellement spécifier hello **PermissionsToKeys** paramètre tooset autorisations pour un utilisateur, application ou un groupe de sécurité :</span><span class="sxs-lookup"><span data-stu-id="61e97-170">Optionally, you can specify hello **PermissionsToKeys** parameter tooset permissions for a user, application, or a security group:</span></span>

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign
```

<span data-ttu-id="61e97-171">Si vous souhaitez tooauthorize de ce même secrets de tooread application dans le coffre, exécutez hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="61e97-171">If you want tooauthorize that same application tooread secrets in your vault, run hello following cmdlet:</span></span>

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300 -PermissionsToKeys Get
```

## <a name="next-steps"></a><span data-ttu-id="61e97-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="61e97-172">Next Steps</span></span>
* [<span data-ttu-id="61e97-173">Déployer une machine virtuelle avec un mot de passe stocké dans un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="61e97-173">Deploy a VM with password stored in a Key Vault</span></span>](azure-stack-kv-deploy-vm-with-secret.md)  
* [<span data-ttu-id="61e97-174">Déployer une machine virtuelle avec un certificat stocké dans un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="61e97-174">Deploy a VM with certificate stored in Key Vault</span></span>](azure-stack-kv-push-secret-into-vm.md) 
