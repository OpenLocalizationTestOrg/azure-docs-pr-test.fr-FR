---
title: "Mise en route avec le coffre de clés dans la pile de Azure | Documents Microsoft"
description: "Commencer à l’aide de la pile d’Azure Key Vault"
services: azure-stack
documentationcenter: 
author: rlfmendes
manager: natmack
editor: 
ms.assetid: b973be33-2fc1-4ee6-976a-84ed270e7254
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: ricardom
ms.openlocfilehash: 32fad3ce17c877db661573e67c9cb5948b3c78fa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-key-vault"></a><span data-ttu-id="a0c12-103">Mise en route avec le coffre de clés</span><span class="sxs-lookup"><span data-stu-id="a0c12-103">Getting started with Key Vault</span></span>
<span data-ttu-id="a0c12-104">Cette section décrit les étapes pour créer un coffre, gérer les clés et les clés secrètes ainsi que pour autoriser des utilisateurs ou des applications pour appeler des opérations dans le coffre dans la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="a0c12-104">This section describes the steps to create a vault, manage keys and secrets as well as authorize users or applications to invoke operations in the vault in Azure Stack.</span></span> <span data-ttu-id="a0c12-105">Les étapes suivantes supposent un abonnement locataire existe et KeyVault service est enregistré au sein de cet abonnement.</span><span class="sxs-lookup"><span data-stu-id="a0c12-105">The following steps assume a tenant subscription exists and KeyVault service is registered within that subscription.</span></span> <span data-ttu-id="a0c12-106">Tous les exemples de commandes sont basées sur les applets de commande KeyVault disponibles dans le cadre du kit SDK Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0c12-106">All the example commands are based on the KeyVault cmdlets available as part of the Azure PowerShell SDK.</span></span>

## <a name="enabling-the-tenant-subscription-for-vault-operations"></a><span data-ttu-id="a0c12-107">L’activation de l’abonnement du client pour les opérations d’archivage</span><span class="sxs-lookup"><span data-stu-id="a0c12-107">Enabling the tenant subscription for Vault operations</span></span>
<span data-ttu-id="a0c12-108">Avant de pouvoir émettre des opérations par rapport à un coffre-fort, vous devez vous assurer que votre abonnement est activé pour les opérations d’archivage.</span><span class="sxs-lookup"><span data-stu-id="a0c12-108">Before you can issue operations against any vault, you need to ensure that your subscription is enabled for vault operations.</span></span> <span data-ttu-id="a0c12-109">Vous pouvez confirmer qu’en émettant la commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="a0c12-109">You can confirm that by issuing the following PowerShell command:</span></span>

    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -AutoSize

<span data-ttu-id="a0c12-110">La sortie de la commande ci-dessus doit signaler les « Enregistré » pour l’état « Registration » de chaque ligne.</span><span class="sxs-lookup"><span data-stu-id="a0c12-110">The output of the above command should report “Registered” for the “Registration” state of every row.</span></span>

    ProviderNamespace RegistrationState ResourceTypes Locations
    Microsoft.KeyVault Registered {operations} {local}
    Microsoft.KeyVault Registered {vaults} {local}
    Microsoft.KeyVault Registered {vaults/secrets} {local}


 <span data-ttu-id="a0c12-111">Si tel n’est pas le cas, vous devez appeler la commande suivante pour inscrire le service KeyVault dans votre abonnement :</span><span class="sxs-lookup"><span data-stu-id="a0c12-111">If that’s not the case, you should invoke the following command to register the KeyVault service within your subscription:</span></span>

    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault

<span data-ttu-id="a0c12-112">Et ce qui suit est la sortie de la commande :</span><span class="sxs-lookup"><span data-stu-id="a0c12-112">And the folowing is the output of the command:</span></span>

    ProviderNamespace : Microsoft.KeyVault
    RegistrationState : Registered
    ResourceTypes : {operations, vaults, vaults/secrets}
    Locations : {local}


> [!NOTE]
> <span data-ttu-id="a0c12-113">Si vous obtenez l’erreur : «*l’abonnement n’est pas inscrit auprès d’Azure Key Vault*» lors de l’appel des applets de commande KeyVault, vérifiez que vous avez activé le fournisseur de ressources KeyVault par les instructions ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="a0c12-113">If you get the error: "*The subscription is not registered with Azure Key Vault*" when invoking KeyVault cmdlets, please confirm you have enabled the KeyVault resource provider per instructions above.</span></span>
> 
> 

## <a name="creating-a-hardened-container-a-vault-in-azure-stack-to-store-and-manage-cryptographic-keys-and-secrets"></a><span data-ttu-id="a0c12-114">Création d’un conteneur de sécurisation renforcé (un coffre) dans la pile de Azure pour stocker et gérer des clés de chiffrement et des clés secrètes</span><span class="sxs-lookup"><span data-stu-id="a0c12-114">Creating a hardened container (a vault) in Azure Stack to store and manage cryptographic keys and secrets</span></span>
<span data-ttu-id="a0c12-115">Pour créer un coffre, un locataire devez d’abord créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a0c12-115">In order to create a Vault, a tenant should first create a resource group.</span></span> <span data-ttu-id="a0c12-116">Les commandes PowerShell créent un groupe de ressources, puis un coffre dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a0c12-116">The following PowerShell commands create a resource group and then a Vault in that Resource Group.</span></span> <span data-ttu-id="a0c12-117">L’exemple inclut également les sorties à partir de cette applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a0c12-117">The example also includes the typical output from that cmdlet.</span></span>

### <a name="creating-a-resource-group"></a><span data-ttu-id="a0c12-118">Création d’un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="a0c12-118">Creating a resource group:</span></span>
    New-AzureRmResourceGroup -Name vaultrg010 -Location local -Verbose -Force

<span data-ttu-id="a0c12-119">Output:</span><span class="sxs-lookup"><span data-stu-id="a0c12-119">Output:</span></span>

    VERBOSE: Performing the operation "Replacing resource group ..." on target "".
    VERBOSE: 12:52:51 PM - Created resource group 'vaultrg010' in location 'local'
    ResourceGroupName : vaultrg010
    Location : local
    ProvisioningState : Succeeded
    Tags :
    ResourceId : /subscriptions/fa881715-3802-42cc-a54e-a06adf61584d/resourceGroups/vaultrg010


### <a name="creating-a-vault"></a><span data-ttu-id="a0c12-120">Création d’un coffre :</span><span class="sxs-lookup"><span data-stu-id="a0c12-120">Creating a vault:</span></span>
    New-AzureRmKeyVault -VaultName vault010 -ResourceGroupName vaultrg010 -Location local -Verbose

<span data-ttu-id="a0c12-121">Output:</span><span class="sxs-lookup"><span data-stu-id="a0c12-121">Output:</span></span>

    VaultUri : https://vault010.vault.local.azurestack.global
    TenantId : 5454420b-2e38-4b9e-8b56-1712d321cf33
    TenantName : 5454420b-2e38-4b9e-8b56-1712d321cf33
    Sku : Standard
    EnabledForDeployment : False
    EnabledForTemplateDeployment : False
    EnabledForDiskEncryption : False
    AccessPolicies : {5454420b-2e38-4b9e-8b56-1712d321cf33}
    AccessPoliciesText :
    Tenant ID : 5454420b-2e38-4b9e-8b56-1712d321cf33
    Object ID : ca342e90-f6aa-435b-a11c-dfe5ef0bfeeb
    Application ID :
    Display Name : Tenant Admin (tenantadmin1@msazurestack.onmicrosoft.com)
    Permissions to Keys : get, create, delete, list, update, import, backup, restore
    Permissions to Secrets : all
    OriginalVault : Microsoft.Azure.Management.KeyVault.Vault
    ResourceId : /subscriptions/fa881715-3802-42cc-a54e-a06adf61584d/resourceGroups/vaultrg010/providers/Microsoft.KeyVault/vaults/vault010
    VaultName : vault010
    ResourceGroupName : vaultrg010
    Location : local
    Tags : {}
    TagsTable :

<span data-ttu-id="a0c12-122">La sortie de cette applet de commande affiche les propriétés du coffre de clés que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="a0c12-122">The output of this cmdlet shows properties of the key vault that you’ve just created.</span></span> <span data-ttu-id="a0c12-123">Les deux propriétés les plus importantes sont :</span><span class="sxs-lookup"><span data-stu-id="a0c12-123">The two most important properties are:</span></span>

* <span data-ttu-id="a0c12-124">**Nom de coffre**: dans l’exemple, il s’agit de **vault010**.</span><span class="sxs-lookup"><span data-stu-id="a0c12-124">**Vault Name**: In the example, this is **vault010**.</span></span> <span data-ttu-id="a0c12-125">Vous allez utiliser ce nom pour les autres applets de commande Key Vault.</span><span class="sxs-lookup"><span data-stu-id="a0c12-125">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="a0c12-126">**URI de coffre**: dans l’exemple, il s’agit d’https://vault010.vault.local.azurestack.global.</span><span class="sxs-lookup"><span data-stu-id="a0c12-126">**Vault URI**: In the example, this is https://vault010.vault.local.azurestack.global.</span></span> <span data-ttu-id="a0c12-127">Les applications qui utilisent votre coffre via son API REST doivent utiliser cet URI.</span><span class="sxs-lookup"><span data-stu-id="a0c12-127">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="a0c12-128">Votre compte Azure est pour l’instant le seul autorisé à effectuer des opérations sur ce</span><span class="sxs-lookup"><span data-stu-id="a0c12-128">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="a0c12-129">coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="a0c12-129">As yet, nobody else is.</span></span>

## <a name="operating-on-keys-and-secrets"></a><span data-ttu-id="a0c12-130">Fonctionne sur les clés et les clés secrètes</span><span class="sxs-lookup"><span data-stu-id="a0c12-130">Operating on Keys and Secrets</span></span>
<span data-ttu-id="a0c12-131">Après avoir créé un coffre, suivez les étapes ci-dessous pour créer, gérer les clés et les secrets :</span><span class="sxs-lookup"><span data-stu-id="a0c12-131">After creating a vault, follow the below steps to create manage keys and secrets:</span></span>

### <a name="creating-a-key"></a><span data-ttu-id="a0c12-132">Création d’une clé</span><span class="sxs-lookup"><span data-stu-id="a0c12-132">Creating a key</span></span>
<span data-ttu-id="a0c12-133">Pour créer une clé, utilisez la **Add-AzureKeyVaultKey** par l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a0c12-133">In order to create a key, use the **Add-AzureKeyVaultKey** per the example below.</span></span> <span data-ttu-id="a0c12-134">Après la création réussie de la clé, l’applet de commande affiche les détails de la clé nouvellement créées.</span><span class="sxs-lookup"><span data-stu-id="a0c12-134">After successful key creation, the cmdlet will output the newly created key details.</span></span>

    Add-AzureKeyVaultKey -VaultName \$vaultName -Name\$keyVaultKeyName -Verbose -Destination Software

<span data-ttu-id="a0c12-135">Voici la sortie de la *Add-AzureKeyVaultKey* applet de commande :</span><span class="sxs-lookup"><span data-stu-id="a0c12-135">The following is the output of the *Add-AzureKeyVaultKey* cmdlet:</span></span>

    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes
    Key : {"kid":"https://vault010.vault.local.azurestack.global/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff","kty":"RSA","key\_ops":\["encrypt"
    ,"decrypt","sign","verify","wrapKey","unwrapKey"\],"n":"nDkcBQCyyLnXtbwFMnXOWzPDqWKiyjf0G3QTxvuN\_MansEn9X-91q4\_WFmRBCd5zWBqz671iuZO\_D4r0P25
    Fe2lAq\_3T1gATVNGR7LTEU9W5h8AoY10bmt4e0y66Jn2vUV-UTCz4\_vtKSKoiuNXHFR\_tGZ-6YX-frqKIiC8pbE4Qvz1x-c7E-eM\_Cpu87koL95n-Hl3wQRQRPXEPRR6gcHR5E74D1
    gLEFCWKySTo4nXtLoeBMNK5QYEBZIAS61ACbR4czjHn6ty-tZeVTc7hyK\_UO2EbJovQIAhyayfq018uNtCBzjjkqJKnY34kviVCPoTQqOdpHa0FHrloe5FeIw","e":"AQAB"}
    VaultName : vault010
    Name : keyVaultKeyName001
    Version : 86062b02b10342688f3b0b3713e343ff
    Id : https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff

<span data-ttu-id="a0c12-136">Vous pouvez maintenant référencer cette clé que vous avez créée ou téléchargée dans Azure Key Vault à l’aide de son URI.</span><span class="sxs-lookup"><span data-stu-id="a0c12-136">You can now reference this key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="a0c12-137">Utilisez **https://vault010.vault.local.azurestack.global:443/clés/keyVaultKeyName001** pour obtenir la version actuelle ; toujours utiliser **https://vault010.vault.local.azurestack.global:443/clés keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff** pour obtenir cette version spécifique.</span><span class="sxs-lookup"><span data-stu-id="a0c12-137">Use **https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001** to always get the current version; and use **https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff** to get this specific version.</span></span>

### <a name="retrieving-a-key"></a><span data-ttu-id="a0c12-138">La récupération d’une clé</span><span class="sxs-lookup"><span data-stu-id="a0c12-138">Retrieving a key</span></span>
<span data-ttu-id="a0c12-139">Utilisez le **Get-AzureKeyVaultKey** pour récupérer une clé et ses détails par l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="a0c12-139">Use the **Get-AzureKeyVaultKey** to retrieve a key and its details per the following example:</span></span>

    Get-AzureKeyVaultKey -VaultName vault010 -Name keyVaultKeyName001

<span data-ttu-id="a0c12-140">Voici la sortie de Get-AzureKeyVaultKey</span><span class="sxs-lookup"><span data-stu-id="a0c12-140">The following is the output of Get-AzureKeyVaultKey</span></span>

    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes
    Key : {"kid":"https://vault010.vault.local.azurestack.global/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff","kty":"RSA","key\_ops":\["encrypt"
    ,"decrypt","sign","verify","wrapKey","unwrapKey"\],"n":"nDkcBQCyyLnXtbwFMnXOWzPDqWKiyjf0G3QTxvuN\_MansEn9X-91q4\_WFmRBCd5zWBqz671iuZO\_D4r0P25
    Fe2lAq\_3T1gATVNGR7LTEU9W5h8AoY10bmt4e0y66Jn2vUV-UTCz4\_vtKSKoiuNXHFR\_tGZ-6YX-frqKIiC8pbE4Qvz1x-c7E-eM\_Cpu87koL95n-Hl3wQRQRPXEPRR6gcHR5E74D1
    gLEFCWKySTo4nXtLoeBMNK5QYEBZIAS61ACbR4czjHn6ty-tZeVTc7hyK\_UO2EbJovQIAhyayfq018uNtCBzjjkqJKnY34kviVCPoTQqOdpHa0FHrloe5FeIw","e":"AQAB"}
    VaultName : vault010
    Name : keyVaultKeyName001
    Version : 86062b02b10342688f3b0b3713e343ff
    Id : https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff

### <a name="setting-a-secret"></a><span data-ttu-id="a0c12-141">Définition d’une clé secrète</span><span class="sxs-lookup"><span data-stu-id="a0c12-141">Setting a secret</span></span>
    $secretvalue = ConvertTo-SecureString 'User@123' -AsPlainText -Force
    Set-AzureKeyVaultSecret -Name MySecret-VaultName vault010 -SecretValue $secretvalue

<span data-ttu-id="a0c12-142">Sortie</span><span class="sxs-lookup"><span data-stu-id="a0c12-142">Output</span></span>

    Vault Name : vault010
    Name : MySecret
    Version : 65a387f2ed4a416180e852b970846f5b
    Id : https://vault010.vault.local.azurestack.global:443/secrets/MySecret/65a387f2ed4a416180e852b970846f5b
    Enabled : True
    Expires :
    Not Before :
    Created : 8/17/2016 10:49:52 PM
    Updated : 8/17/2016 10:49:52 PM
    Content Type :
    Tags : 

### <a name="retrieving-a-secret"></a><span data-ttu-id="a0c12-143">La récupération d’une clé secrète</span><span class="sxs-lookup"><span data-stu-id="a0c12-143">Retrieving a secret</span></span>
    Get-AzureKeyVaultSecret -VaultName vault010

<span data-ttu-id="a0c12-144">Sortie</span><span class="sxs-lookup"><span data-stu-id="a0c12-144">Output</span></span>

    Vault Name : vault010
    Name : MySecret
    Version :
    Id : https://vault010.vault.local.azurestack.global:443/secrets/MySecret
    Enabled : True
    Expires :
    Not Before :
    Created : 8/17/2016 10:49:52 PM
    Updated : 8/17/2016 10:49:52 PM
    Content Type :
    Tags :

<span data-ttu-id="a0c12-145">À présent, votre coffre de clés et la clé/le secret sont prêts à être utilisés par les applications</span><span class="sxs-lookup"><span data-stu-id="a0c12-145">Now, your key vault and key or secret is ready for applications to use.</span></span>
<span data-ttu-id="a0c12-146">qui doivent recevoir les autorisations adéquates.</span><span class="sxs-lookup"><span data-stu-id="a0c12-146">You must authorize applications to use them.</span></span>

## <a name="authorize-the-application-to-use-the-key-or-secret"></a><span data-ttu-id="a0c12-147">Autorisation de l’application à utiliser la clé ou le secret</span><span class="sxs-lookup"><span data-stu-id="a0c12-147">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="a0c12-148">Pour autoriser l’application d’accéder à la clé ou le secret dans le coffre, utilisez la commande Set -**AzureRmKeyVaultAccessPolicy** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a0c12-148">To authorize the application to access the key or secret in the vault, use the Set-**AzureRmKeyVaultAccessPolicy** cmdlet.</span></span>

<span data-ttu-id="a0c12-149">Par exemple, si le nom de votre coffre est *ContosoKeyVault* et dispose de l’application que vous souhaitez autoriser un *ID Client* de *8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed*et que vous vous souhaitez autoriser l’application pour déchiffrer et vous connecter avec des clés dans le coffre, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a0c12-149">For example, if your vault name is *ContosoKeyVault* and the application you want to authorize has a *Client ID* of *8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed*, and you want to authorize the application to decrypt and sign with keys in your vault, run the following:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

<span data-ttu-id="a0c12-150">Si vous souhaitez autoriser cette même application à lire les éléments secrets de votre coffre, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a0c12-150">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get


## <a name="next-steps"></a><span data-ttu-id="a0c12-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a0c12-151">Next steps</span></span>
[<span data-ttu-id="a0c12-152">Déployer une machine virtuelle avec un mot de passe Key Vault</span><span class="sxs-lookup"><span data-stu-id="a0c12-152">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)

[<span data-ttu-id="a0c12-153">Déployer une machine virtuelle avec un certificat Key Vault</span><span class="sxs-lookup"><span data-stu-id="a0c12-153">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

