---
ms.assetid: 
title: "Azure Key Vault - Utilisation de la suppression réversible avec PowerShell"
description: "Exemples d’utilisation de la suppression réversible avec extraits de code PowerShell"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/21/2017
ms.author: bruceper
ms.openlocfilehash: 8cf0674f7eb139e50da4a3c22a8d8376a86b0dcc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-key-vault-soft-delete-with-powershell"></a><span data-ttu-id="e6e93-103">Utilisation de la suppression réversible Key Vault avec l’interface PowerShell</span><span class="sxs-lookup"><span data-stu-id="e6e93-103">How to use Key Vault soft-delete with PowerShell</span></span>

<span data-ttu-id="e6e93-104">La fonctionnalité de suppression réversible d’Azure Key Vault permet de récupérer des coffres et des objets de coffres qui ont été supprimés.</span><span class="sxs-lookup"><span data-stu-id="e6e93-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="e6e93-105">La suppression réversible traite plus particulièrement les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="e6e93-105">Specifically, soft-delete addresses the following scenarios:</span></span>

- <span data-ttu-id="e6e93-106">Prise en charge de la suppression récupérable d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="e6e93-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="e6e93-107">Prise en charge de la suppression récupérable d’objets de coffre de clés (clés, secrets et certificats)</span><span class="sxs-lookup"><span data-stu-id="e6e93-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6e93-108">Prérequis</span><span class="sxs-lookup"><span data-stu-id="e6e93-108">Prerequisites</span></span>

- <span data-ttu-id="e6e93-109">Azure PowerShell 4.0.0 ou version ultérieure - Si ce n’est pas encore fait, installez Azure PowerShell et associez-le à votre abonnement Azure. Voir [Guide pratique pour installer et configurer Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e6e93-109">Azure PowerShell 4.0.0 or later - If you don't have this already setup, install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span> 

>[!NOTE]
> <span data-ttu-id="e6e93-110">Il existe une version obsolète de notre fichier de mise en forme de sortie Key Vault PowerShell qui **peut** se charger dans votre environnement à la place de la version correcte.</span><span class="sxs-lookup"><span data-stu-id="e6e93-110">There is an outdated version of our Key Vault PowerShell output formatting file that **may** be loaded into your environment instead of the correct version.</span></span> <span data-ttu-id="e6e93-111">Nous prévoyons de publier une version mise à jour de PowerShell avec la correction nécessaire de la mise en forme de sortie ; cette rubrique sera mise à jour à cette occasion.</span><span class="sxs-lookup"><span data-stu-id="e6e93-111">We are anticipating an updated version of PowerShell to contain the needed correction for the output formatting and will update this topic at that time.</span></span> <span data-ttu-id="e6e93-112">D’ici là, si vous rencontrez ce problème de mise en forme, voici comment le contourner :</span><span class="sxs-lookup"><span data-stu-id="e6e93-112">The current workaround, should you encounter this formatting problem, is:</span></span>
> - <span data-ttu-id="e6e93-113">Utilisez la requête suivante si vous ne voyez pas la propriété de suppression réversible activée qui est décrite dans cette rubrique : `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span><span class="sxs-lookup"><span data-stu-id="e6e93-113">Use the following query if you notice you're not seeing the soft-delete enabled property described in this topic: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span></span>


<span data-ttu-id="e6e93-114">Pour obtenir des informations de référence propres à Key Vault pour PowerShell, consultez la [référence Key Vault Azure PowerShell](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="e6e93-114">For Key Vault specific refernece information for PowerShell, see [Azure Key Vault PowerShell reference](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="e6e93-115">Autorisations requises</span><span class="sxs-lookup"><span data-stu-id="e6e93-115">Required permissions</span></span>

<span data-ttu-id="e6e93-116">Les opérations Key Vault sont gérées séparément par l’intermédiaire d’autorisations de contrôle d’accès en fonction du rôle (RBAC) comme suit :</span><span class="sxs-lookup"><span data-stu-id="e6e93-116">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="e6e93-117">Opération</span><span class="sxs-lookup"><span data-stu-id="e6e93-117">Operation</span></span> | <span data-ttu-id="e6e93-118">Description</span><span class="sxs-lookup"><span data-stu-id="e6e93-118">Description</span></span> | <span data-ttu-id="e6e93-119">Autorisation utilisateur</span><span class="sxs-lookup"><span data-stu-id="e6e93-119">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="e6e93-120">Liste</span><span class="sxs-lookup"><span data-stu-id="e6e93-120">List</span></span>|<span data-ttu-id="e6e93-121">Énumère les coffres de clé supprimés.</span><span class="sxs-lookup"><span data-stu-id="e6e93-121">Lists deleted key vaults.</span></span>|<span data-ttu-id="e6e93-122">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="e6e93-122">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="e6e93-123">Recover</span><span class="sxs-lookup"><span data-stu-id="e6e93-123">Recover</span></span>|<span data-ttu-id="e6e93-124">Restaure un coffre de clés supprimé.</span><span class="sxs-lookup"><span data-stu-id="e6e93-124">Restores a deleted key vault.</span></span>|<span data-ttu-id="e6e93-125">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="e6e93-125">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="e6e93-126">Purge</span><span class="sxs-lookup"><span data-stu-id="e6e93-126">Purge</span></span>|<span data-ttu-id="e6e93-127">Supprime définitivement un coffre de clés supprimé et tout son contenu.</span><span class="sxs-lookup"><span data-stu-id="e6e93-127">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="e6e93-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="e6e93-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="e6e93-129">Pour plus d’informations sur les autorisations et le contrôle d’accès, consultez [Sécuriser votre coffre de clés](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="e6e93-129">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="e6e93-130">Activation de la suppression réversible</span><span class="sxs-lookup"><span data-stu-id="e6e93-130">Enabling soft-delete</span></span>

<span data-ttu-id="e6e93-131">Pour pouvoir récupérer un coffre de clés supprimé ou des objets stockés dans un coffre de clés, vous devez d’abord activer la suppression réversible pour ce coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="e6e93-131">To be able to recover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="e6e93-132">Coffre de clés existant</span><span class="sxs-lookup"><span data-stu-id="e6e93-132">Existing key vault</span></span>

<span data-ttu-id="e6e93-133">Pour un coffre de clés existant nommé ContosoVault, vous pouvez activer la suppression réversible comme suit.</span><span class="sxs-lookup"><span data-stu-id="e6e93-133">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="e6e93-134">Actuellement, vous devez utiliser la manipulation des ressources Azure Resource Manager pour écrire directement la propriété *enableSoftDelete* dans la ressource Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e6e93-134">Currently you need to use Azure Resource Manager resource manipulation to directly write the *enableSoftDelete* property to the Key Vault resource.</span></span>

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a><span data-ttu-id="e6e93-135">Nouveau coffre de clés</span><span class="sxs-lookup"><span data-stu-id="e6e93-135">New key vault</span></span>

<span data-ttu-id="e6e93-136">L’activation de la suppression réversible pour un nouveau coffre de clés s’effectue au moment de la création en ajoutant l’indicateur « soft-delete enable » à votre commande de création.</span><span class="sxs-lookup"><span data-stu-id="e6e93-136">Enabling soft-delete for a new key vault is done at creation time by adding the soft-delete enable flag to your create command.</span></span>

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="e6e93-137">Vérifier l’activation de la suppression réversible</span><span class="sxs-lookup"><span data-stu-id="e6e93-137">Verify soft-delete enablement</span></span>

<span data-ttu-id="e6e93-138">Pour vérifier que la suppression réversible est activée pour un coffre de clés, exécutez la commande *show* et recherchez l’attribut « Soft Delete Enabled ? »</span><span class="sxs-lookup"><span data-stu-id="e6e93-138">To verify that a key vault has soft-delete enabled, run the *get* command and look for the 'Soft Delete Enabled?'</span></span> <span data-ttu-id="e6e93-139">et sa valeur (true ou false).</span><span class="sxs-lookup"><span data-stu-id="e6e93-139">attribute and its setting, true or false.</span></span>

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="e6e93-140">Suppression d’un coffre de clés protégé par la suppression réversible</span><span class="sxs-lookup"><span data-stu-id="e6e93-140">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="e6e93-141">La commande de suppression d’un coffre de clés reste la même, mais son comportement varie selon que vous avez activé ou non la suppression réversible.</span><span class="sxs-lookup"><span data-stu-id="e6e93-141">The command to delete (or remove) a key vault remains the same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
><span data-ttu-id="e6e93-142">Si vous exécutez la commande précédente pour un coffre de clés pour lequel la suppression réversible n’est pas activée, vous supprimez définitivement ce coffre de clés et tout son contenu, sans aucune option de récupération.</span><span class="sxs-lookup"><span data-stu-id="e6e93-142">If you run the previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="e6e93-143">Comment la suppression réversible protège-t-elle votre coffre de clés ?</span><span class="sxs-lookup"><span data-stu-id="e6e93-143">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="e6e93-144">Quand la suppression réversible est activée :</span><span class="sxs-lookup"><span data-stu-id="e6e93-144">With soft-delete enabled:</span></span>

- <span data-ttu-id="e6e93-145">Quand un coffre de clés est supprimé, il est enlevé de son groupe de ressources et placé dans un espace de noms réservé qui n’est associé qu’à l’emplacement où il a été créé.</span><span class="sxs-lookup"><span data-stu-id="e6e93-145">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with the location where it was created.</span></span> 
- <span data-ttu-id="e6e93-146">Les objets d’un coffre de clés supprimé (tels que les clés, les secrets et les certificats) sont inaccessibles et le demeurent tant que leur coffre de clés conteneur est à l’état supprimé.</span><span class="sxs-lookup"><span data-stu-id="e6e93-146">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in the deleted state.</span></span> 
- <span data-ttu-id="e6e93-147">Le nom DNS d’un coffre de clés à l’état supprimé est toujours réservé. Vous ne pourrez donc pas créer de nouveau coffre de clés avec le même nom.</span><span class="sxs-lookup"><span data-stu-id="e6e93-147">The DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="e6e93-148">Vous pouvez afficher les coffres de clé associés à votre abonnement qui sont à l’état supprimé en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e6e93-148">You may view deleted state key vaults, associated with your subscription, using the following command:</span></span>

```powershell
PS C:\> Get-AzureRmKeyVault -InRemovedStateVault 

Name           : ContosoVault
Location             : westus
Id                   : /subscriptions/xxx/providers/Microsoft.KeyVault/locations/westus/deletedVaults/ContosoVault
Resource ID          : /subscriptions/xxx/resourceGroups/ContosoVault/providers/Microsoft.KeyVault/vaults/ContosoVault
Deletion Date        : 5/9/2017 12:14:14 AM
Scheduled Purge Date : 8/7/2017 12:14:14 AM
Tags                 :
```

<span data-ttu-id="e6e93-149">L’*ID de ressource* dans la sortie fait référence à l’ID de ressource d’origine de ce coffre.</span><span class="sxs-lookup"><span data-stu-id="e6e93-149">The *Resource ID* in the output refers to the original resource ID of this vault.</span></span> <span data-ttu-id="e6e93-150">Ce coffre de clés étant maintenant à l’état supprimé, il n’existe aucune ressource avec cet ID de ressource.</span><span class="sxs-lookup"><span data-stu-id="e6e93-150">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="e6e93-151">Vous pouvez utiliser le champ *Id* pour identifier la ressource lors de la récupération ou du vidage.</span><span class="sxs-lookup"><span data-stu-id="e6e93-151">The *Id* field can be used to identify the resource when recovering, or purging.</span></span> <span data-ttu-id="e6e93-152">Le champ *Date de vidage planifiée* indique quand le coffre sera définitivement supprimé (vidé) si aucune action n’est effectuée pour ce coffre supprimé.</span><span class="sxs-lookup"><span data-stu-id="e6e93-152">The *Scheduled Purge Date* field indicates when the vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="e6e93-153">La période de rétention par défaut, utilisée pour calculer la *Date de vidage planifiée*, est de 90 jours.</span><span class="sxs-lookup"><span data-stu-id="e6e93-153">The default retention period, used to calculate the *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="e6e93-154">Récupération d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="e6e93-154">Recovering a key vault</span></span>

<span data-ttu-id="e6e93-155">Pour récupérer un coffre de clés, vous devez spécifier le nom du coffre de clés, le groupe de ressources et l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="e6e93-155">To recover a key vault, you need to specify the key vault name, resource group, and location.</span></span> <span data-ttu-id="e6e93-156">Notez l’emplacement et le groupe de ressources du coffre de clés supprimé, car vous en aurez besoin pour le processus de récupération de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="e6e93-156">Note the location and the resource group of the deleted key vault as you need these for a key vault recovery process.</span></span>

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

<span data-ttu-id="e6e93-157">Quand un coffre de clés est récupéré, le résultat est une ressource avec l’ID de ressource d’origine du coffre de clés</span><span class="sxs-lookup"><span data-stu-id="e6e93-157">When a key vault is recovered, the result is a new resource with the key vault's original resource ID.</span></span> <span data-ttu-id="e6e93-158">Si le groupe de ressources dans lequel existait le coffre de clés a été supprimé, vous devez créer un groupe de ressources du même nom pour que le coffre de clés puisse être récupéré.</span><span class="sxs-lookup"><span data-stu-id="e6e93-158">If the resource group where the key vault existed has been removed, a new resource group with same name must be created before the key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="e6e93-159">Objets de coffre de clés et suppression réversible</span><span class="sxs-lookup"><span data-stu-id="e6e93-159">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="e6e93-160">Pour une clé nommée « ContosoFirstKey » dans un coffre de clés nommé « ContosoVault » avec la suppression réversible activée, voici comment vous supprimeriez cette clé.</span><span class="sxs-lookup"><span data-stu-id="e6e93-160">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="e6e93-161">Quand la suppression réversible est activée pour votre coffre de clés, une clé supprimée apparaît toujours comme ayant été supprimée, sauf quand vous énumérez ou récupérez explicitement les clés supprimées.</span><span class="sxs-lookup"><span data-stu-id="e6e93-161">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="e6e93-162">La plupart des opérations effectuées sur une clé à l’état supprimé échoueront, sauf l’énumération d’une clé supprimée, sa récupération ou son vidage.</span><span class="sxs-lookup"><span data-stu-id="e6e93-162">Most operations on a key in the deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="e6e93-163">Par exemple, pour demander à énumérer les clés supprimées dans un coffre de clés, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e6e93-163">For example, to request to list deleted keys in a key vault, use the following command:</span></span>

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a><span data-ttu-id="e6e93-164">État de transition</span><span class="sxs-lookup"><span data-stu-id="e6e93-164">Transition state</span></span> 

<span data-ttu-id="e6e93-165">Quand vous supprimez une clé dans un coffre de clés pour lequel la suppression réversible est activée, la transition peut prendre quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="e6e93-165">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for the transition to complete.</span></span> <span data-ttu-id="e6e93-166">Pendant cet état de transition, il peut sembler que la clé n’est pas à l’état actif ou à l’état supprimé.</span><span class="sxs-lookup"><span data-stu-id="e6e93-166">During this transition state, it may appear that the key is not in the active state or the deleted state.</span></span> <span data-ttu-id="e6e93-167">Cette commande répertorie toutes les clés supprimées dans votre coffre de clés nommé « ContosoVault ».</span><span class="sxs-lookup"><span data-stu-id="e6e93-167">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```powershell
  Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
  Vault Name           : ContosoVault
  Name                 : ContosoFirstKey
  Id                   : https://ContosoVault.vault.azure.net:443/keys/ContosoFirstKey
  Deleted Date         : 2/14/2017 8:20:52 PM
  Scheduled Purge Date : 5/15/2017 8:20:52 PM
  Enabled              : True
  Expires              :
  Not Before           :
  Created              : 2/14/2017 8:16:07 PM
  Updated              : 2/14/2017 8:16:07 PM
  Tags                 :
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="e6e93-168">Utilisation de la suppression réversible avec des objets de coffre de clés</span><span class="sxs-lookup"><span data-stu-id="e6e93-168">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="e6e93-169">Tout comme les coffres de clés, une clé, un secret ou un certificat supprimé(e) reste à l’état supprimé pendant 90 jours, sauf si vous le récupérez ou si vous le videz.</span><span class="sxs-lookup"><span data-stu-id="e6e93-169">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up to 90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="e6e93-170">Clés</span><span class="sxs-lookup"><span data-stu-id="e6e93-170">Keys</span></span>

<span data-ttu-id="e6e93-171">Pour récupérer une clé supprimée</span><span class="sxs-lookup"><span data-stu-id="e6e93-171">To recover a deleted key:</span></span>

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="e6e93-172">Pour supprimer définitivement une clé</span><span class="sxs-lookup"><span data-stu-id="e6e93-172">To permanently delete a key:</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
><span data-ttu-id="e6e93-173">Le vidage d’une clé entraîne sa suppression définitive, ce qui signifie que vous ne pourrez pas la récupérer.</span><span class="sxs-lookup"><span data-stu-id="e6e93-173">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="e6e93-174">Les actions **recover** et **purge** ont leurs propres autorisations associées dans une stratégie d’accès au coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="e6e93-174">The **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="e6e93-175">Pour qu’un utilisateur ou un principal de service puisse exécuter une action **recover** ou **purge**, il doit disposer de l’autorisation correspondante pour cet objet (clé ou secret) dans la stratégie d’accès au coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="e6e93-175">For a user or service principal to be able to execute a **recover** or **purge** action they must have the respective permission for that object (key or secret) in the key vault access policy.</span></span> <span data-ttu-id="e6e93-176">Par défaut, l’autorisation **purge** n’est pas ajoutée à la stratégie d’accès d’un coffre de clés quand le raccourci « all » est utilisé pour accorder toutes les autorisations à un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e6e93-176">By default, the **purge** permission is not added to a key vault's access policy when the 'all' shortcut is used to grant all permissions to a user.</span></span> <span data-ttu-id="e6e93-177">Vous devez accorder explicitement l’autorisation**purge**.</span><span class="sxs-lookup"><span data-stu-id="e6e93-177">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="e6e93-178">Par exemple, la commande suivante accorde à user@contoso.com l’autorisation d’effectuer plusieurs opérations sur les clés dans *ContosoVault*, notamment **purge**.</span><span class="sxs-lookup"><span data-stu-id="e6e93-178">For example, the following command grants user@contoso.com permission to perform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="e6e93-179">Définir une stratégie d’accès au coffre de clés</span><span class="sxs-lookup"><span data-stu-id="e6e93-179">Set a key vault access policy</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> <span data-ttu-id="e6e93-180">Si vous avez un coffre de clés pour lequel la suppression réversible vient d’être activée, vous ne disposerez peut-être pas des autorisations **recover** et **purge**.</span><span class="sxs-lookup"><span data-stu-id="e6e93-180">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="e6e93-181">Secrets</span><span class="sxs-lookup"><span data-stu-id="e6e93-181">Secrets</span></span>

<span data-ttu-id="e6e93-182">Comme les clés, les secrets dans un coffre de clés sont gérés avec leurs propres commandes.</span><span class="sxs-lookup"><span data-stu-id="e6e93-182">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="e6e93-183">Vous trouverez ci-dessous les commandes de suppression, d’énumération, de récupération et de vidage des secrets.</span><span class="sxs-lookup"><span data-stu-id="e6e93-183">Following, are the commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="e6e93-184">Supprimer un secret nommé SQLPassword :</span><span class="sxs-lookup"><span data-stu-id="e6e93-184">Delete a secret named SQLPassword:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- <span data-ttu-id="e6e93-185">Énumérer tous les secrets supprimés dans un coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="e6e93-185">List all deleted secrets in a key vault:</span></span> 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- <span data-ttu-id="e6e93-186">Récupérer un secret à l’état supprimé :</span><span class="sxs-lookup"><span data-stu-id="e6e93-186">Recover a secret in the deleted state:</span></span> 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- <span data-ttu-id="e6e93-187">Vider un secret à l’état supprimé :</span><span class="sxs-lookup"><span data-stu-id="e6e93-187">Purge a secret in deleted state:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
><span data-ttu-id="e6e93-188">Le vidage d’un secret entraîne sa suppression définitive, ce qui signifie que vous ne pourrez pas le récupérer.</span><span class="sxs-lookup"><span data-stu-id="e6e93-188">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="e6e93-189">Vidage et coffres de clé</span><span class="sxs-lookup"><span data-stu-id="e6e93-189">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="e6e93-190">Objets de coffre de clés</span><span class="sxs-lookup"><span data-stu-id="e6e93-190">Key vault objects</span></span>

<span data-ttu-id="e6e93-191">Le vidage d’une clé, d’un secret ou d’un certificat entraîne sa suppression définitive, ce qui signifie que vous ne pourrez pas le récupérer.</span><span class="sxs-lookup"><span data-stu-id="e6e93-191">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="e6e93-192">Le coffre de clés qui contenait l’objet supprimé sera toutefois conservé, de même que tous les autres objets dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="e6e93-192">The key vault that contained the deleted object will however remain intact as will all other objects in the key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="e6e93-193">Coffres de clé en tant que conteneurs</span><span class="sxs-lookup"><span data-stu-id="e6e93-193">Key vaults as containers</span></span>
<span data-ttu-id="e6e93-194">Quand un coffre de clés est vidé, tout son contenu, notamment les clés, les secrets et les certificats, sont supprimés définitivement.</span><span class="sxs-lookup"><span data-stu-id="e6e93-194">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="e6e93-195">Pour vider un coffre de clés, utilisez la commande `Remove-AzureRmKeyVault` avec l’option `-InRemovedState` et spécifiez l’emplacement du coffre de clés supprimé avec l’argument `-Location location`.</span><span class="sxs-lookup"><span data-stu-id="e6e93-195">To purge a key vault, use the `Remove-AzureRmKeyVault` command with the option `-InRemovedState` and by specifying the location of the deleted key vault with the `-Location location` argument.</span></span> <span data-ttu-id="e6e93-196">Vous pouvez déterminer l’emplacement d’un coffre supprimé à l’aide de la commande `Get-AzureRmKeyVault -InRemovedState`.</span><span class="sxs-lookup"><span data-stu-id="e6e93-196">You can find the location of a deleted vault using the command `Get-AzureRmKeyVault -InRemovedState`.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
><span data-ttu-id="e6e93-197">Le vidage d’un coffre de clés entraîne sa suppression définitive, ce qui signifie que vous ne pourrez pas le récupérer.</span><span class="sxs-lookup"><span data-stu-id="e6e93-197">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="e6e93-198">Autorisations de vidage requises</span><span class="sxs-lookup"><span data-stu-id="e6e93-198">Purge permissions required</span></span>
- <span data-ttu-id="e6e93-199">Pour vider un coffre de clés supprimé, et ainsi faire en sorte que le coffre et tout son contenu soient supprimés définitivement, l’utilisateur a besoin d’une autorisation RBAC pour effectuer une opération *Microsoft.KeyVault/locations/deletedVaults/purge/action*.</span><span class="sxs-lookup"><span data-stu-id="e6e93-199">To purge a deleted key vault, such that the vault and all its contents are permanently removed, the user needs RBAC permission to perform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="e6e93-200">Pour répertorier le coffre de clés supprimé, l’utilisateur a besoin de l’autorisation RBAC pour effectuer une opération *Microsoft.KeyVault/deletedVaults/read*.</span><span class="sxs-lookup"><span data-stu-id="e6e93-200">To list the deleted key, the vault a user needs RBAC permission to perform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="e6e93-201">Par défaut, seul un administrateur d’abonnement dispose de ces autorisations.</span><span class="sxs-lookup"><span data-stu-id="e6e93-201">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="e6e93-202">Vidage planifié</span><span class="sxs-lookup"><span data-stu-id="e6e93-202">Scheduled purge</span></span>

<span data-ttu-id="e6e93-203">La liste des objets de votre coffre de clés supprimés indique quand est planifiée leur suppression définitive par Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e6e93-203">Listing your deleted key vault objects shows when they are schedled to be purged by Key Vault.</span></span> <span data-ttu-id="e6e93-204">Le champ *Date de vidage planifiée* indique quand un objet de coffre de clés sera supprimé définitivement si aucune action n’est effectuée.</span><span class="sxs-lookup"><span data-stu-id="e6e93-204">The *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="e6e93-205">Par défaut, la période de rétention d’un objet de coffre de clés supprimé est de 90 jours.</span><span class="sxs-lookup"><span data-stu-id="e6e93-205">By default, the retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="e6e93-206">Un objet de coffre dont le vidage est déclenché par son champ *Date de vidage planifiée* est supprimé définitivement.</span><span class="sxs-lookup"><span data-stu-id="e6e93-206">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="e6e93-207">Il n’est pas récupérable.</span><span class="sxs-lookup"><span data-stu-id="e6e93-207">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="e6e93-208">Autres ressources</span><span class="sxs-lookup"><span data-stu-id="e6e93-208">Other resources</span></span>

- <span data-ttu-id="e6e93-209">Pour obtenir une présentation de la fonctionnalité de suppression réversible, consultez [Présentation de la suppression réversible d’Azure Key Vault](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="e6e93-209">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="e6e93-210">Pour obtenir une vue d’ensemble de l’utilisation d’Azure Key Vault, consultez [Bien démarrer avec Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e6e93-210">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

