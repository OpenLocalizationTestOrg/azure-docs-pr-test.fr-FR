---
title: "Gérer Key Vault dans Azure Stack à l’aide de PowerShell | Microsoft Docs"
description: "Découvrez comment gérer Key Vault dans Azure Stack à l’aide de PowerShell."
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
ms.openlocfilehash: 71320f8c55d014db6843e6247c53cc07832efc32
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-key-vault-in-azure-stack-using-powershell"></a><span data-ttu-id="d108c-103">Gérer Key Vault dans Azure Stack à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="d108c-103">Manage Key Vault in Azure Stack using PowerShell</span></span>

<span data-ttu-id="d108c-104">Cet article montre comment créer et gérer Key Vault dans Azure Stack à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d108c-104">This article helps you get started to create and manage Key Vault in Azure Stack by using PowerShell.</span></span> <span data-ttu-id="d108c-105">Les applets de commande PowerShell Key Vault décrites dans cet article sont disponibles dans le cadre du SDK Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d108c-105">The Key Vault PowerShell cmdlets described in this article are available as a part of the Azure PowerShell SDK.</span></span> <span data-ttu-id="d108c-106">Les sections suivantes décrivent les applets de commande PowerShell nécessaires pour créer un coffre, stocker et gérer les clés de chiffrement et les secrets, et autoriser des utilisateurs ou des applications à appeler des opérations dans le coffre.</span><span class="sxs-lookup"><span data-stu-id="d108c-106">The following sections describe the PowerShell cmdlets that are required to create a vault, store, and manage cryptographic keys and secrets as well as authorize users or applications to invoke operations in the vault.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d108c-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d108c-107">Prerequisites</span></span>
* <span data-ttu-id="d108c-108">[Installez PowerShell pour Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="d108c-108">[Install PowerShell for Azure Stack.](azure-stack-powershell-install.md)</span></span>  
* <span data-ttu-id="d108c-109">Les administrateurs de cloud Azure pile doivent avoir [créé une offre](azure-stack-create-offer.md) qui inclut le service de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="d108c-109">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes the Key Vault service.</span></span>  
* <span data-ttu-id="d108c-110">Les utilisateurs doivent [s’abonner à une offre](azure-stack-subscribe-plan-provision-vm.md) qui inclut le service Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d108c-110">Users must [subscribe to an offer](azure-stack-subscribe-plan-provision-vm.md) that includes the Key Vault service.</span></span> 
* [<span data-ttu-id="d108c-111">Configurez l’environnement PowerShell de l’utilisateur Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="d108c-111">Configure the Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)

## <a name="enable-your-tenant-subscription-for-vault-operations"></a><span data-ttu-id="d108c-112">Activer votre abonnement de locataire pour les opérations de coffre</span><span class="sxs-lookup"><span data-stu-id="d108c-112">Enable your tenant subscription for vault operations</span></span>

<span data-ttu-id="d108c-113">Avant de pouvoir exécuter des opérations sur un coffre de clés, vous devez vérifier que votre abonnement de locataire est activé pour les opérations de coffre.</span><span class="sxs-lookup"><span data-stu-id="d108c-113">Before you can issue any operations against a key vault, you need to ensure that your tenant subscription is enabled for vault operations.</span></span> <span data-ttu-id="d108c-114">Pour cela, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d108c-114">To verify, run the following command:</span></span>

```PowerShell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -Autosize
```
<span data-ttu-id="d108c-115">**Sortie**</span><span class="sxs-lookup"><span data-stu-id="d108c-115">**Output**</span></span>

<span data-ttu-id="d108c-116">Si votre abonnement est activé pour les opérations de coffre, la sortie indique que « RegistrationState » est « Registered » pour tous les types de ressources d’un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="d108c-116">If your subscription is enabled for vault operations, the output shows “RegistrationState” equals “Registered” for all resource types of a key vault.</span></span>

![état de l’inscription](media/azure-stack-kv-manage-powershell/image1.png)

<span data-ttu-id="d108c-118">Si tel n’est pas le cas, exécutez la commande suivante pour inscrire le service Key Vaults dans votre abonnement :</span><span class="sxs-lookup"><span data-stu-id="d108c-118">If that’s not the case, invoke the following command to register the Key Vault service in your subscription:</span></span>

```PowerShell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault
```

<span data-ttu-id="d108c-119">**Sortie**</span><span class="sxs-lookup"><span data-stu-id="d108c-119">**Output**</span></span>

<span data-ttu-id="d108c-120">Si l’inscription réussit, la sortie suivante est retournée :</span><span class="sxs-lookup"><span data-stu-id="d108c-120">If the registration is successful, the following output is returned:</span></span>

![inscription](media/azure-stack-kv-manage-powershell/image2.png)

<span data-ttu-id="d108c-122">Les sections suivantes partent du principe que le service Key Vaults est inscrit dans l’abonnement de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d108c-122">The following sections assume Key Vault service is registered within the user subscription.</span></span> <span data-ttu-id="d108c-123">Lors de l’appel des commandes Key Vaults, si vous recevez une erreur « L’abonnement n’est pas inscrit pour utiliser l’espace de noms « Microsoft.KeyVault » », vérifiez que vous avez [activé le fournisseur de ressources Key Vaults](#enable-your-tenant-subscription-for-vault-operations) conformément aux instructions mentionnées plus haut.</span><span class="sxs-lookup"><span data-stu-id="d108c-123">When invoking key vault commands, if you get an error- "The subscription is not registered to use namespace ‘Microsoft.KeyVault" then, confirm that you have [enabled the Key Vault resource provider](#enable-your-tenant-subscription-for-vault-operations) as per instructions mentioned earlier.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="d108c-124">Création d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="d108c-124">Create a key vault</span></span> 

<span data-ttu-id="d108c-125">Avant de créer un coffre de clés, créez un groupe de ressources pour que toutes les ressources associées au coffre de clés existent dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="d108c-125">Before you create a key vault, create a resource group so that all key vault related resources exist in a resource group.</span></span> <span data-ttu-id="d108c-126">Utilisez la commande suivante pour créer un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="d108c-126">Use the following command to create a new resource group:</span></span>

```PowerShell
New-AzureRmResourceGroup -Name “VaultRG” -Location local -verbose -Force

```

<span data-ttu-id="d108c-127">**Sortie**</span><span class="sxs-lookup"><span data-stu-id="d108c-127">**Output**</span></span>

![new resource group](media/azure-stack-kv-manage-powershell/image3.png)

<span data-ttu-id="d108c-129">Maintenant, utilisez la commande **New-AzureRMKeyVault** pour créer un coffre de clés dans le groupe de ressources que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="d108c-129">Now, use the **New-AzureRMKeyVault** command to create a key vault in the resource group that you created earlier.</span></span> <span data-ttu-id="d108c-130">Cette commande lit trois paramètres obligatoires : le nom du groupe de ressources, le nom du coffre de clés et l’emplacement géographique.</span><span class="sxs-lookup"><span data-stu-id="d108c-130">This command reads three mandatory parameters- resource group name, key vault name, and geographic location.</span></span> 

<span data-ttu-id="d108c-131">Exécutez la commande suivante pour créer un coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="d108c-131">Run the following command to create a key vault:</span></span>

```PowerShell
New-AzureRmKeyVault -VaultName “Vault01” -ResourceGroupName “VaultRG” -Location local -verbose
```
<span data-ttu-id="d108c-132">**Sortie**</span><span class="sxs-lookup"><span data-stu-id="d108c-132">**Output**</span></span>

![nouveau coffre de clés](media/azure-stack-kv-manage-powershell/image4.png)

<span data-ttu-id="d108c-134">La sortie de cette commande affiche les propriétés du coffre de clés que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="d108c-134">The output of this command shows the properties of the key vault that you created.</span></span> <span data-ttu-id="d108c-135">Quand une application accède à ce coffre, elle utilise la propriété **Vault URI** indiquée dans la sortie.</span><span class="sxs-lookup"><span data-stu-id="d108c-135">When an application accesses this vault, it uses the **Vault URI** property shown in the output.</span></span> <span data-ttu-id="d108c-136">Par exemple, l’URI de coffre ici est **https://vault01.vault.local.azurestack.external**.</span><span class="sxs-lookup"><span data-stu-id="d108c-136">For example, the vault URI here is **https://vault01.vault.local.azurestack.external**.</span></span> <span data-ttu-id="d108c-137">Les applications qui interagissent avec ce coffre de clés par le biais de l’API REST doivent utiliser cet URI.</span><span class="sxs-lookup"><span data-stu-id="d108c-137">Applications interacting with this key vault through REST API must use this URI.</span></span>

<span data-ttu-id="d108c-138">Dans les déploiements AD FS, quand vous créez un coffre de clés à l’aide de PowerShell, vous pouvez recevoir un avertissement indiquant que la stratégie d’accès n’est pas définie</span><span class="sxs-lookup"><span data-stu-id="d108c-138">In ADFS-based deployments, when you create a key vault by using PowerShell, you might receive a warning that says "Access policy is not set.</span></span> <span data-ttu-id="d108c-139">et qu’aucun utilisateur ou application n’est autorisé à utiliser ce coffre.</span><span class="sxs-lookup"><span data-stu-id="d108c-139">No user or application has access permission to use this vault".</span></span> <span data-ttu-id="d108c-140">Pour résoudre ce problème, définissez une stratégie d’accès pour le coffre à l’aide de la commande [Set-AzureRmKeyVaultAccessPolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret) :</span><span class="sxs-lookup"><span data-stu-id="d108c-140">To resolve this issue, set an access policy for the vault by using the [Set-AzureRmKeyVaultAccessPolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret) command:</span></span>

```PowerShell
# Obtain the security identifier(SID) of the active directory user
$adUser = Get-ADUser -Filter "Name -eq '{Active directory user name}'"
$objectSID = $adUser.SID.Value 

#Set the key vault access policy
Set-AzureRmKeyVaultAccessPolicy -VaultName "{key vault name}" -ResourceGroupName "{resource group name}" -ObjectId "{object SID}" -PermissionsToKeys {permissionsToKeys} -PermissionsToSecrets {permissionsToSecrets} -BypassObjectIdValidation 
```

## <a name="manage-keys-and-secrets"></a><span data-ttu-id="d108c-141">Gérer les clés et les secrets</span><span class="sxs-lookup"><span data-stu-id="d108c-141">Manage keys and secrets</span></span>

<span data-ttu-id="d108c-142">Après avoir créé un coffre, effectuez les étapes suivantes pour créer et gérer les clés et les secrets dans le coffre.</span><span class="sxs-lookup"><span data-stu-id="d108c-142">After creating a vault, use the following steps to create and manage keys and secrets within the vault.</span></span>

### <a name="create-a-key"></a><span data-ttu-id="d108c-143">Créer une clé</span><span class="sxs-lookup"><span data-stu-id="d108c-143">Create a key</span></span>

<span data-ttu-id="d108c-144">Utilisez la commande **Add-AzureKeyVaultKey** pour créer ou importer une clé protégée par un logiciel dans un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="d108c-144">Use the **Add-AzureKeyVaultKey** command to create or import a software protected key in a key vault.</span></span> 

```PowerShell
Add-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01” -verbose -Destination Software
```
<span data-ttu-id="d108c-145">Le paramètre **Destination** permet de spécifier que la clé est protégée par un logiciel.</span><span class="sxs-lookup"><span data-stu-id="d108c-145">The **Destination** parameter is used to specify that the key is software protected.</span></span> <span data-ttu-id="d108c-146">Une fois l’opération terminée, la commande affiche les détails de la clé créée.</span><span class="sxs-lookup"><span data-stu-id="d108c-146">When the key is successfully created, the command outputs the details of the created key.</span></span>

<span data-ttu-id="d108c-147">**Sortie**</span><span class="sxs-lookup"><span data-stu-id="d108c-147">**Output**</span></span>

![Nouvelle clé](media/azure-stack-kv-manage-powershell/image5.png)

<span data-ttu-id="d108c-149">Vous pouvez maintenant référencer la clé créée à l’aide de son URI.</span><span class="sxs-lookup"><span data-stu-id="d108c-149">You can now reference the created key by using its URI.</span></span> <span data-ttu-id="d108c-150">Si vous créez ou importez une clé qui a le même nom qu’une clé existante, la clé d’origine est mise à jour avec les valeurs spécifiées dans la nouvelle clé.</span><span class="sxs-lookup"><span data-stu-id="d108c-150">If you create or import a key that has same name as an existing key, the original key is updated with the values that are specified in the new key.</span></span>  <span data-ttu-id="d108c-151">Vous pouvez accéder à la version précédente à l’aide de l’URI propre à la version de la clé.</span><span class="sxs-lookup"><span data-stu-id="d108c-151">You can access the previous version by using the version-specific URI of the key.</span></span> <span data-ttu-id="d108c-152">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="d108c-152">For example,</span></span> 

* <span data-ttu-id="d108c-153">Utilisez **https://vault10.vault.local.azurestack.external:443/clés/key01** pour toujours obtenir la version actuelle.</span><span class="sxs-lookup"><span data-stu-id="d108c-153">Use **https://vault10.vault.local.azurestack.external:443/keys/key01** to always get the current version</span></span>  
* <span data-ttu-id="d108c-154">Utilisez **https://vault010.vault.local.azurestack.external:443/clés/key01/d0b36ee2e3d14e9f967b8b6b1d38938a** pour obtenir cette version spécifique.</span><span class="sxs-lookup"><span data-stu-id="d108c-154">Use **https://vault010.vault.local.azurestack.external:443/keys/key01/d0b36ee2e3d14e9f967b8b6b1d38938a** to get this specific version</span></span>

### <a name="get-a-key"></a><span data-ttu-id="d108c-155">Obtenir une clé</span><span class="sxs-lookup"><span data-stu-id="d108c-155">Get a key</span></span>

<span data-ttu-id="d108c-156">Utilisez la commande **Get-AzureKeyVaultKey** pour lire une clé et ses détails.</span><span class="sxs-lookup"><span data-stu-id="d108c-156">Use the **Get-AzureKeyVaultKey** command to read a key and its details.</span></span>

```PowerShell
Get-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01”
```

### <a name="create-a-secret"></a><span data-ttu-id="d108c-157">Créer un secret</span><span class="sxs-lookup"><span data-stu-id="d108c-157">Create a secret</span></span>

<span data-ttu-id="d108c-158">Utilisez la commande **Set-AzureKeyVaultSecret** pour créer ou mettre à jour un secret dans un coffre.</span><span class="sxs-lookup"><span data-stu-id="d108c-158">Use the **Set-AzureKeyVaultSecret** command to create or update a secret in a vault.</span></span> <span data-ttu-id="d108c-159">Si le secret n’existe pas encore, il est créé. S’il existe déjà, une nouvelle version est créée.</span><span class="sxs-lookup"><span data-stu-id="d108c-159">A secret is created if it doesn’t already exist, and a new version of the secret is created if it already exists.</span></span>

```PowerShell
$secretvalue = ConvertTo-SecureString “User@123” -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01” -SecretValue $secretvalue
```

<span data-ttu-id="d108c-160">**Sortie**</span><span class="sxs-lookup"><span data-stu-id="d108c-160">**Output**</span></span>

![créer un secret](media/azure-stack-kv-manage-powershell/image6.png)

### <a name="get-a-secret"></a><span data-ttu-id="d108c-162">Obtenir un secret</span><span class="sxs-lookup"><span data-stu-id="d108c-162">Get a secret</span></span>

<span data-ttu-id="d108c-163">Utilisez la commande **Get-AzureKeyVaultSecret** pour lire un secret dans un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="d108c-163">Use the **Get-AzureKeyVaultSecret** command to read a secret in a key vault.</span></span> <span data-ttu-id="d108c-164">Cette commande peut retourner toutes les versions ou des versions spécifiques d’un secret.</span><span class="sxs-lookup"><span data-stu-id="d108c-164">This command can return all or specific versions of a secret.</span></span> 

```PowerShell
Get-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01”
```

<span data-ttu-id="d108c-165">Après avoir créé des clés et des secrets, vous pouvez autoriser des applications externes à les utiliser.</span><span class="sxs-lookup"><span data-stu-id="d108c-165">After creating keys and secrets, you can authorize external applications to use them.</span></span>

## <a name="authorize-an-application-to-use-a-key-or-secret"></a><span data-ttu-id="d108c-166">Autoriser une application à utiliser une clé ou un secret</span><span class="sxs-lookup"><span data-stu-id="d108c-166">Authorize an application to use a key or secret</span></span>

<span data-ttu-id="d108c-167">Pour autoriser une application à accéder à une clé ou à un secret dans le coffre, utilisez la commande **Set-AzureRmKeyVaultAccessPolicy**.</span><span class="sxs-lookup"><span data-stu-id="d108c-167">To authorize an application to access a key or secret in the key vault, use the **Set-AzureRmKeyVaultAccessPolicy** command.</span></span>
<span data-ttu-id="d108c-168">Par exemple, si le nom de votre coffre est ContosoKeyVault et que l’ID client de l’application que vous souhaitez autoriser est 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed,</span><span class="sxs-lookup"><span data-stu-id="d108c-168">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a Client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed.</span></span> <span data-ttu-id="d108c-169">exécutez la commande suivante pour autoriser l’application.</span><span class="sxs-lookup"><span data-stu-id="d108c-169">Run the following command to authorize the application.</span></span> <span data-ttu-id="d108c-170">Si vous le souhaitez, vous pouvez spécifier le paramètre **PermissionsToKeys** pour définir des autorisations pour un utilisateur, une application ou un groupe de sécurité :</span><span class="sxs-lookup"><span data-stu-id="d108c-170">Optionally, you can specify the **PermissionsToKeys** parameter to set permissions for a user, application, or a security group:</span></span>

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign
```

<span data-ttu-id="d108c-171">Si vous souhaitez autoriser cette même application à lire les secrets de votre coffre, exécutez l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d108c-171">If you want to authorize that same application to read secrets in your vault, run the following cmdlet:</span></span>

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300 -PermissionsToKeys Get
```

## <a name="next-steps"></a><span data-ttu-id="d108c-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d108c-172">Next Steps</span></span>
* [<span data-ttu-id="d108c-173">Déployer une machine virtuelle avec un mot de passe stocké dans un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="d108c-173">Deploy a VM with password stored in a Key Vault</span></span>](azure-stack-kv-deploy-vm-with-secret.md)  
* [<span data-ttu-id="d108c-174">Déployer une machine virtuelle avec un certificat stocké dans un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="d108c-174">Deploy a VM with certificate stored in Key Vault</span></span>](azure-stack-kv-push-secret-into-vm.md) 
