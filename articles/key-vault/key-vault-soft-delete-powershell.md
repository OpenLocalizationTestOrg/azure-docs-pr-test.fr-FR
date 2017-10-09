---
ms.assetid: 
title: "Coffre de clé aaaAzure - comment toouse soft-suppression avec PowerShell"
description: "Exemples d’utilisation de la suppression réversible avec extraits de code PowerShell"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/21/2017
ms.author: bruceper
ms.openlocfilehash: 4968b700a14f764ea1be7de2bf3697664f255f95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-powershell"></a><span data-ttu-id="e43a3-103">Comment toouse le coffre de clés soft-suppression avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="e43a3-103">How toouse Key Vault soft-delete with PowerShell</span></span>

<span data-ttu-id="e43a3-104">La fonctionnalité de suppression réversible d’Azure Key Vault permet de récupérer des coffres et des objets de coffres qui ont été supprimés.</span><span class="sxs-lookup"><span data-stu-id="e43a3-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="e43a3-105">Plus précisément, les adresses de soft-suppression hello les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="e43a3-105">Specifically, soft-delete addresses hello following scenarios:</span></span>

- <span data-ttu-id="e43a3-106">Prise en charge de la suppression récupérable d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="e43a3-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="e43a3-107">Prise en charge de la suppression récupérable d’objets de coffre de clés (clés, secrets et certificats)</span><span class="sxs-lookup"><span data-stu-id="e43a3-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e43a3-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e43a3-108">Prerequisites</span></span>

- <span data-ttu-id="e43a3-109">Azure PowerShell 4.0.0 ou version ultérieure - si vous n’avez ce déjà le programme d’installation, installez Azure PowerShell et associez-le à votre abonnement Azure, consultez [comment tooinstall et configurer Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e43a3-109">Azure PowerShell 4.0.0 or later - If you don't have this already setup, install Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span> 

>[!NOTE]
> <span data-ttu-id="e43a3-110">Il existe une version obsolète de notre sortie PowerShell de coffre de clé mise en forme de fichiers qui **peut** être chargé dans votre environnement au lieu de la version correcte de hello.</span><span class="sxs-lookup"><span data-stu-id="e43a3-110">There is an outdated version of our Key Vault PowerShell output formatting file that **may** be loaded into your environment instead of hello correct version.</span></span> <span data-ttu-id="e43a3-111">Nous anticipation de que correction de besoin d’une version mise à jour PowerShell toocontain hello pour le format de sortie hello et met à jour de cette rubrique à ce moment-là.</span><span class="sxs-lookup"><span data-stu-id="e43a3-111">We are anticipating an updated version of PowerShell toocontain hello needed correction for hello output formatting and will update this topic at that time.</span></span> <span data-ttu-id="e43a3-112">Hello solution de contournement actuelle, si vous rencontrez ce problème de mise en forme, est :</span><span class="sxs-lookup"><span data-stu-id="e43a3-112">hello current workaround, should you encounter this formatting problem, is:</span></span>
> - <span data-ttu-id="e43a3-113">Hello utilisation suivant la requête si vous remarquez que vous ne voyez hello soft-suppression activé la propriété décrite dans cette rubrique : `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span><span class="sxs-lookup"><span data-stu-id="e43a3-113">Use hello following query if you notice you're not seeing hello soft-delete enabled property described in this topic: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span></span>


<span data-ttu-id="e43a3-114">Pour obtenir des informations de référence propres à Key Vault pour PowerShell, consultez la [référence Key Vault Azure PowerShell](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="e43a3-114">For Key Vault specific refernece information for PowerShell, see [Azure Key Vault PowerShell reference](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="e43a3-115">Autorisations requises</span><span class="sxs-lookup"><span data-stu-id="e43a3-115">Required permissions</span></span>

<span data-ttu-id="e43a3-116">Les opérations Key Vault sont gérées séparément par l’intermédiaire d’autorisations de contrôle d’accès en fonction du rôle (RBAC) comme suit :</span><span class="sxs-lookup"><span data-stu-id="e43a3-116">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="e43a3-117">Opération</span><span class="sxs-lookup"><span data-stu-id="e43a3-117">Operation</span></span> | <span data-ttu-id="e43a3-118">Description</span><span class="sxs-lookup"><span data-stu-id="e43a3-118">Description</span></span> | <span data-ttu-id="e43a3-119">Autorisation utilisateur</span><span class="sxs-lookup"><span data-stu-id="e43a3-119">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="e43a3-120">Liste</span><span class="sxs-lookup"><span data-stu-id="e43a3-120">List</span></span>|<span data-ttu-id="e43a3-121">Énumère les coffres de clé supprimés.</span><span class="sxs-lookup"><span data-stu-id="e43a3-121">Lists deleted key vaults.</span></span>|<span data-ttu-id="e43a3-122">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="e43a3-122">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="e43a3-123">Recover</span><span class="sxs-lookup"><span data-stu-id="e43a3-123">Recover</span></span>|<span data-ttu-id="e43a3-124">Restaure un coffre de clés supprimé.</span><span class="sxs-lookup"><span data-stu-id="e43a3-124">Restores a deleted key vault.</span></span>|<span data-ttu-id="e43a3-125">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="e43a3-125">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="e43a3-126">Purge</span><span class="sxs-lookup"><span data-stu-id="e43a3-126">Purge</span></span>|<span data-ttu-id="e43a3-127">Supprime définitivement un coffre de clés supprimé et tout son contenu.</span><span class="sxs-lookup"><span data-stu-id="e43a3-127">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="e43a3-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="e43a3-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="e43a3-129">Pour plus d’informations sur les autorisations et le contrôle d’accès, consultez [Sécuriser votre coffre de clés](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="e43a3-129">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="e43a3-130">Activation de la suppression réversible</span><span class="sxs-lookup"><span data-stu-id="e43a3-130">Enabling soft-delete</span></span>

<span data-ttu-id="e43a3-131">toorecover en mesure de toobe un coffre de clés supprimé ou des objets stockés dans une clé de coffre, vous devez d’abord activer soft-suppression de ce coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="e43a3-131">toobe able toorecover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="e43a3-132">Coffre de clés existant</span><span class="sxs-lookup"><span data-stu-id="e43a3-132">Existing key vault</span></span>

<span data-ttu-id="e43a3-133">Pour un coffre de clés existant nommé ContosoVault, vous pouvez activer la suppression réversible comme suit.</span><span class="sxs-lookup"><span data-stu-id="e43a3-133">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="e43a3-134">Actuellement, vous devez hello écriture de toouse Azure Resource Manager ressource manipulation toodirectly *enableSoftDelete* toohello de propriété de ressource du coffre de clé.</span><span class="sxs-lookup"><span data-stu-id="e43a3-134">Currently you need toouse Azure Resource Manager resource manipulation toodirectly write hello *enableSoftDelete* property toohello Key Vault resource.</span></span>

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a><span data-ttu-id="e43a3-135">Nouveau coffre de clés</span><span class="sxs-lookup"><span data-stu-id="e43a3-135">New key vault</span></span>

<span data-ttu-id="e43a3-136">L’activation du soft-suppression pour un nouveau coffre de clés est effectuée au moment de la création en ajoutant l’indicateur d’activation de soft-suppression de hello tooyour créer la commande.</span><span class="sxs-lookup"><span data-stu-id="e43a3-136">Enabling soft-delete for a new key vault is done at creation time by adding hello soft-delete enable flag tooyour create command.</span></span>

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="e43a3-137">Vérifier l’activation de la suppression réversible</span><span class="sxs-lookup"><span data-stu-id="e43a3-137">Verify soft-delete enablement</span></span>

<span data-ttu-id="e43a3-138">tooverify un coffre de clés a soft-suppression activée, exécution hello *obtenir* de commandes et recherchez hello « Logicielle supprimer est-il activé ? »</span><span class="sxs-lookup"><span data-stu-id="e43a3-138">tooverify that a key vault has soft-delete enabled, run hello *get* command and look for hello 'Soft Delete Enabled?'</span></span> <span data-ttu-id="e43a3-139">et sa valeur (true ou false).</span><span class="sxs-lookup"><span data-stu-id="e43a3-139">attribute and its setting, true or false.</span></span>

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="e43a3-140">Suppression d’un coffre de clés protégé par la suppression réversible</span><span class="sxs-lookup"><span data-stu-id="e43a3-140">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="e43a3-141">commande de Hello toodelete (ou supprimer) un coffre de clés reste hello, mais ses modifications du comportement selon que vous avez activé soft-suppression ou non.</span><span class="sxs-lookup"><span data-stu-id="e43a3-141">hello command toodelete (or remove) a key vault remains hello same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
><span data-ttu-id="e43a3-142">Si vous exécutez la commande précédente hello pour un coffre de clés qui ne dispose pas de soft-suppression est activée, vous supprimer définitivement ce coffre de clés et tout son contenu sans les options de récupération.</span><span class="sxs-lookup"><span data-stu-id="e43a3-142">If you run hello previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="e43a3-143">Comment la suppression réversible protège-t-elle votre coffre de clés ?</span><span class="sxs-lookup"><span data-stu-id="e43a3-143">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="e43a3-144">Quand la suppression réversible est activée :</span><span class="sxs-lookup"><span data-stu-id="e43a3-144">With soft-delete enabled:</span></span>

- <span data-ttu-id="e43a3-145">Lorsqu’un coffre de clés est supprimé, il est supprimé de son groupe de ressources et placé dans un espace de noms réservé qui n’est associé à emplacement hello où il a été créé.</span><span class="sxs-lookup"><span data-stu-id="e43a3-145">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with hello location where it was created.</span></span> 
- <span data-ttu-id="e43a3-146">Les objets dans une clé supprimée de coffre, telles que les clés, les secrets et des certificats, sont inaccessibles et restent alors que leur conteneur coffre de clés est en état de hello supprimé.</span><span class="sxs-lookup"><span data-stu-id="e43a3-146">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in hello deleted state.</span></span> 
- <span data-ttu-id="e43a3-147">nom DNS de Hello pour un coffre de clés dans un état supprimé est toujours réservé pour un nouvel archivage de clés portant le même nom ne peut pas être créé.</span><span class="sxs-lookup"><span data-stu-id="e43a3-147">hello DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="e43a3-148">Vous pouvez consulter les coffres de clé d’état supprimé, associés à votre abonnement, à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e43a3-148">You may view deleted state key vaults, associated with your subscription, using hello following command:</span></span>

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

<span data-ttu-id="e43a3-149">Hello *ID de ressource* Bonjour sortie fait référence toohello ID de ressource d’origine de ce coffre.</span><span class="sxs-lookup"><span data-stu-id="e43a3-149">hello *Resource ID* in hello output refers toohello original resource ID of this vault.</span></span> <span data-ttu-id="e43a3-150">Ce coffre de clés étant maintenant à l’état supprimé, il n’existe aucune ressource avec cet ID de ressource.</span><span class="sxs-lookup"><span data-stu-id="e43a3-150">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="e43a3-151">Hello *Id* champ peut être utilisé tooidentify hello ressource lors de la récupération ou de purge.</span><span class="sxs-lookup"><span data-stu-id="e43a3-151">hello *Id* field can be used tooidentify hello resource when recovering, or purging.</span></span> <span data-ttu-id="e43a3-152">Hello *Date de Purge planifiée* champ indique quand le coffre hello est définitivement supprimé (purge) si aucune action n’est effectuée pour cet archivage supprimé.</span><span class="sxs-lookup"><span data-stu-id="e43a3-152">hello *Scheduled Purge Date* field indicates when hello vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="e43a3-153">Bonjour par défaut rétention toocalculate période, utilisé Bonjour *Date de Purge planifiée*, est de 90 jours.</span><span class="sxs-lookup"><span data-stu-id="e43a3-153">hello default retention period, used toocalculate hello *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="e43a3-154">Récupération d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="e43a3-154">Recovering a key vault</span></span>

<span data-ttu-id="e43a3-155">toorecover un coffre de clés, vous avez besoin de nom de coffre de clés toospecify hello, groupe de ressources et l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="e43a3-155">toorecover a key vault, you need toospecify hello key vault name, resource group, and location.</span></span> <span data-ttu-id="e43a3-156">Remarque hello hello emplacement et le groupe de ressources de hello supprimé le coffre de clés dont vous avez besoin pour un processus de récupération de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="e43a3-156">Note hello location and hello resource group of hello deleted key vault as you need these for a key vault recovery process.</span></span>

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

<span data-ttu-id="e43a3-157">Une fois un coffre de clés est récupéré, hello il en résulte une nouvelle ressource avec l’ID de ressource du coffre de clés hello d’origine</span><span class="sxs-lookup"><span data-stu-id="e43a3-157">When a key vault is recovered, hello result is a new resource with hello key vault's original resource ID.</span></span> <span data-ttu-id="e43a3-158">Si le groupe de ressources hello où le coffre de clés hello existait a été supprimé, un nouveau groupe de ressources portant le même nom doit être créé avant de pouvoir récupérer le coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="e43a3-158">If hello resource group where hello key vault existed has been removed, a new resource group with same name must be created before hello key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="e43a3-159">Objets de coffre de clés et suppression réversible</span><span class="sxs-lookup"><span data-stu-id="e43a3-159">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="e43a3-160">Pour une clé nommée « ContosoFirstKey » dans un coffre de clés nommé « ContosoVault » avec la suppression réversible activée, voici comment vous supprimeriez cette clé.</span><span class="sxs-lookup"><span data-stu-id="e43a3-160">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="e43a3-161">Quand la suppression réversible est activée pour votre coffre de clés, une clé supprimée apparaît toujours comme ayant été supprimée, sauf quand vous énumérez ou récupérez explicitement les clés supprimées.</span><span class="sxs-lookup"><span data-stu-id="e43a3-161">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="e43a3-162">La plupart des opérations sur une clé dans l’état de hello supprimée échoue, à l’exception répertoriant une clé supprimée, sa récupération ou il purge.</span><span class="sxs-lookup"><span data-stu-id="e43a3-162">Most operations on a key in hello deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="e43a3-163">Par exemple, toorequest les clés de toolist supprimé dans un coffre de clés, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e43a3-163">For example, toorequest toolist deleted keys in a key vault, use hello following command:</span></span>

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a><span data-ttu-id="e43a3-164">État de transition</span><span class="sxs-lookup"><span data-stu-id="e43a3-164">Transition state</span></span> 

<span data-ttu-id="e43a3-165">Lorsque vous supprimez une clé dans un coffre de clés avec soft-suppression est activée, elle peut prendre quelques secondes que hello transition toocomplete.</span><span class="sxs-lookup"><span data-stu-id="e43a3-165">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for hello transition toocomplete.</span></span> <span data-ttu-id="e43a3-166">Au cours de cet état de transition, il peut apparaître que cette clé hello n’est pas dans état actif de hello ou hello supprimé.</span><span class="sxs-lookup"><span data-stu-id="e43a3-166">During this transition state, it may appear that hello key is not in hello active state or hello deleted state.</span></span> <span data-ttu-id="e43a3-167">Cette commande répertorie toutes les clés supprimées dans votre coffre de clés nommé « ContosoVault ».</span><span class="sxs-lookup"><span data-stu-id="e43a3-167">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

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

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="e43a3-168">Utilisation de la suppression réversible avec des objets de coffre de clés</span><span class="sxs-lookup"><span data-stu-id="e43a3-168">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="e43a3-169">À l’instar de coffres de clé, une clé supprimée, secret ou des certificats reste dans un état supprimé pour too90 jours, sauf si vous le récupérer ou purger.</span><span class="sxs-lookup"><span data-stu-id="e43a3-169">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up too90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="e43a3-170">Clés</span><span class="sxs-lookup"><span data-stu-id="e43a3-170">Keys</span></span>

<span data-ttu-id="e43a3-171">toorecover une clé supprimée :</span><span class="sxs-lookup"><span data-stu-id="e43a3-171">toorecover a deleted key:</span></span>

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="e43a3-172">toopermanently supprimer une clé :</span><span class="sxs-lookup"><span data-stu-id="e43a3-172">toopermanently delete a key:</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
><span data-ttu-id="e43a3-173">Le vidage d’une clé entraîne sa suppression définitive, ce qui signifie que vous ne pourrez pas la récupérer.</span><span class="sxs-lookup"><span data-stu-id="e43a3-173">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="e43a3-174">Hello **récupérer** et **purger** actions ont leurs propres autorisations associés liées une stratégie d’accès de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="e43a3-174">hello **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="e43a3-175">Pour un tooexecute en mesure de toobe principal utilisateur ou un service une **récupérer** ou **purger** action qu’ils doivent autorisé hello respectifs pour cet objet (clé ou le secret) dans la stratégie d’accès hello coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="e43a3-175">For a user or service principal toobe able tooexecute a **recover** or **purge** action they must have hello respective permission for that object (key or secret) in hello key vault access policy.</span></span> <span data-ttu-id="e43a3-176">Par défaut, hello **purger** autorisation n’est pas ajoutée la stratégie d’accès du coffre de clés tooa lorsque hello contextuel 'all' est utilisé toogrant toutes les autorisations tooa utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e43a3-176">By default, hello **purge** permission is not added tooa key vault's access policy when hello 'all' shortcut is used toogrant all permissions tooa user.</span></span> <span data-ttu-id="e43a3-177">Vous devez accorder explicitement l’autorisation**purge**.</span><span class="sxs-lookup"><span data-stu-id="e43a3-177">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="e43a3-178">Par exemple, hello suivant accorde de la commande user@contoso.com tooperform d’autorisation plusieurs opérations sur les clés dans *ContosoVault* notamment **purger**.</span><span class="sxs-lookup"><span data-stu-id="e43a3-178">For example, hello following command grants user@contoso.com permission tooperform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="e43a3-179">Définir une stratégie d’accès au coffre de clés</span><span class="sxs-lookup"><span data-stu-id="e43a3-179">Set a key vault access policy</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> <span data-ttu-id="e43a3-180">Si vous avez un coffre de clés pour lequel la suppression réversible vient d’être activée, vous ne disposerez peut-être pas des autorisations **recover** et **purge**.</span><span class="sxs-lookup"><span data-stu-id="e43a3-180">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="e43a3-181">Secrets</span><span class="sxs-lookup"><span data-stu-id="e43a3-181">Secrets</span></span>

<span data-ttu-id="e43a3-182">Comme les clés, les secrets dans un coffre de clés sont gérés avec leurs propres commandes.</span><span class="sxs-lookup"><span data-stu-id="e43a3-182">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="e43a3-183">Suivant, sont des commandes de hello pour suppression, liste, la récupération et la purge des clés secrètes.</span><span class="sxs-lookup"><span data-stu-id="e43a3-183">Following, are hello commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="e43a3-184">Supprimer un secret nommé SQLPassword :</span><span class="sxs-lookup"><span data-stu-id="e43a3-184">Delete a secret named SQLPassword:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- <span data-ttu-id="e43a3-185">Énumérer tous les secrets supprimés dans un coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="e43a3-185">List all deleted secrets in a key vault:</span></span> 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- <span data-ttu-id="e43a3-186">Restaurer un secret de l’état de hello supprimé :</span><span class="sxs-lookup"><span data-stu-id="e43a3-186">Recover a secret in hello deleted state:</span></span> 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- <span data-ttu-id="e43a3-187">Vider un secret à l’état supprimé :</span><span class="sxs-lookup"><span data-stu-id="e43a3-187">Purge a secret in deleted state:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
><span data-ttu-id="e43a3-188">Le vidage d’un secret entraîne sa suppression définitive, ce qui signifie que vous ne pourrez pas le récupérer.</span><span class="sxs-lookup"><span data-stu-id="e43a3-188">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="e43a3-189">Vidage et coffres de clé</span><span class="sxs-lookup"><span data-stu-id="e43a3-189">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="e43a3-190">Objets de coffre de clés</span><span class="sxs-lookup"><span data-stu-id="e43a3-190">Key vault objects</span></span>

<span data-ttu-id="e43a3-191">Le vidage d’une clé, d’un secret ou d’un certificat entraîne sa suppression définitive, ce qui signifie que vous ne pourrez pas le récupérer.</span><span class="sxs-lookup"><span data-stu-id="e43a3-191">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="e43a3-192">coffre de clés Hello qui contenait hello supprimé objet toutefois reste intact ainsi que tous les autres objets dans le coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="e43a3-192">hello key vault that contained hello deleted object will however remain intact as will all other objects in hello key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="e43a3-193">Coffres de clé en tant que conteneurs</span><span class="sxs-lookup"><span data-stu-id="e43a3-193">Key vaults as containers</span></span>
<span data-ttu-id="e43a3-194">Quand un coffre de clés est vidé, tout son contenu, notamment les clés, les secrets et les certificats, sont supprimés définitivement.</span><span class="sxs-lookup"><span data-stu-id="e43a3-194">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="e43a3-195">toopurge un coffre de clés, utilisez hello `Remove-AzureRmKeyVault` avec l’option de hello `-InRemovedState` et en spécifiant l’emplacement hello de coffre de clés hello supprimé par hello `-Location location` argument.</span><span class="sxs-lookup"><span data-stu-id="e43a3-195">toopurge a key vault, use hello `Remove-AzureRmKeyVault` command with hello option `-InRemovedState` and by specifying hello location of hello deleted key vault with hello `-Location location` argument.</span></span> <span data-ttu-id="e43a3-196">Vous pouvez localiser hello un coffre supprimé à l’aide de la commande hello `Get-AzureRmKeyVault -InRemovedState`.</span><span class="sxs-lookup"><span data-stu-id="e43a3-196">You can find hello location of a deleted vault using hello command `Get-AzureRmKeyVault -InRemovedState`.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
><span data-ttu-id="e43a3-197">Le vidage d’un coffre de clés entraîne sa suppression définitive, ce qui signifie que vous ne pourrez pas le récupérer.</span><span class="sxs-lookup"><span data-stu-id="e43a3-197">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="e43a3-198">Autorisations de vidage requises</span><span class="sxs-lookup"><span data-stu-id="e43a3-198">Purge permissions required</span></span>
- <span data-ttu-id="e43a3-199">toopurge un coffre de clés supprimé, telles que le coffre hello et tout son contenu est définitivement supprimées, hello utilisateur doit RBAC autorisation tooperform un *Microsoft.KeyVault/locations/deletedVaults/purge/action* opération.</span><span class="sxs-lookup"><span data-stu-id="e43a3-199">toopurge a deleted key vault, such that hello vault and all its contents are permanently removed, hello user needs RBAC permission tooperform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="e43a3-200">clé de hello supprimé de toolist, le coffre hello un utilisateur doit RBAC autorisation tooperform *Microsoft.KeyVault/deletedVaults/read* autorisation.</span><span class="sxs-lookup"><span data-stu-id="e43a3-200">toolist hello deleted key, hello vault a user needs RBAC permission tooperform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="e43a3-201">Par défaut, seul un administrateur d’abonnement dispose de ces autorisations.</span><span class="sxs-lookup"><span data-stu-id="e43a3-201">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="e43a3-202">Vidage planifié</span><span class="sxs-lookup"><span data-stu-id="e43a3-202">Scheduled purge</span></span>

<span data-ttu-id="e43a3-203">Liste des objets de votre coffre de clés supprimées montre lorsqu’ils sont toobe schedled supprimé par le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="e43a3-203">Listing your deleted key vault objects shows when they are schedled toobe purged by Key Vault.</span></span> <span data-ttu-id="e43a3-204">Hello *Date de Purge planifiée* champ indique quand un objet de coffre de clés est définitivement supprimé, si aucune action n’est effectuée.</span><span class="sxs-lookup"><span data-stu-id="e43a3-204">hello *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="e43a3-205">Par défaut, la période de rétention hello pour un objet supprimé de coffre de clés est 90 jours.</span><span class="sxs-lookup"><span data-stu-id="e43a3-205">By default, hello retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="e43a3-206">Un objet de coffre dont le vidage est déclenché par son champ *Date de vidage planifiée* est supprimé définitivement.</span><span class="sxs-lookup"><span data-stu-id="e43a3-206">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="e43a3-207">Il n’est pas récupérable.</span><span class="sxs-lookup"><span data-stu-id="e43a3-207">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="e43a3-208">Autres ressources</span><span class="sxs-lookup"><span data-stu-id="e43a3-208">Other resources</span></span>

- <span data-ttu-id="e43a3-209">Pour obtenir une présentation de la fonctionnalité de suppression réversible, consultez [Présentation de la suppression réversible d’Azure Key Vault](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="e43a3-209">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="e43a3-210">Pour obtenir une vue d’ensemble de l’utilisation d’Azure Key Vault, consultez [Bien démarrer avec Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e43a3-210">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

