---
ms.assetid: 
title: "Coffre de clé aaaAzure - delete toouse souple avec l’interface CLI"
description: "Exemples d’utilisation de la suppression réversible avec extraits de code CLI"
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 672f5210ab119c244ca712f0bb80b653b50ea79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-cli"></a><span data-ttu-id="c94b9-103">Comment toouse le coffre de clés soft-suppression avec l’interface CLI</span><span class="sxs-lookup"><span data-stu-id="c94b9-103">How toouse Key Vault soft-delete with CLI</span></span>

<span data-ttu-id="c94b9-104">La fonctionnalité de suppression réversible d’Azure Key Vault permet de récupérer des coffres et des objets de coffres qui ont été supprimés.</span><span class="sxs-lookup"><span data-stu-id="c94b9-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="c94b9-105">Plus précisément, les adresses de soft-suppression hello les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="c94b9-105">Specifically, soft-delete addresses hello following scenarios:</span></span>

- <span data-ttu-id="c94b9-106">Prise en charge de la suppression récupérable d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="c94b9-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="c94b9-107">Prise en charge de la suppression récupérable d’objets de coffre de clés (clés, secrets et certificats)</span><span class="sxs-lookup"><span data-stu-id="c94b9-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c94b9-108">Prérequis</span><span class="sxs-lookup"><span data-stu-id="c94b9-108">Prerequisites</span></span>

- <span data-ttu-id="c94b9-109">Azure CLI 2.0 - Si vous ne l’avez pas encore installé pour votre environnement, consultez [Gestion de Key Vault à l’aide de l’interface de ligne de commande (CLI) 2.0](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="c94b9-109">Azure CLI 2.0 - If you don't have this setup for your environment, see [Manage Key Vault using CLI 2.0](key-vault-manage-with-cli2.md).</span></span>

<span data-ttu-id="c94b9-110">Pour obtenir des informations de référence propres à Key Vault pour l’interface CLI, consultez la [référence Key Vault Azure CLI 2.0](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="c94b9-110">For Key Vault specific reference information for CLI, see [Azure CLI 2.0 Key Vault reference](https://docs.microsoft.com/cli/azure/keyvault).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="c94b9-111">Autorisations requises</span><span class="sxs-lookup"><span data-stu-id="c94b9-111">Required permissions</span></span>

<span data-ttu-id="c94b9-112">Les opérations Key Vault sont gérées séparément par l’intermédiaire d’autorisations de contrôle d’accès en fonction du rôle (RBAC) comme suit :</span><span class="sxs-lookup"><span data-stu-id="c94b9-112">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="c94b9-113">Opération</span><span class="sxs-lookup"><span data-stu-id="c94b9-113">Operation</span></span> | <span data-ttu-id="c94b9-114">Description</span><span class="sxs-lookup"><span data-stu-id="c94b9-114">Description</span></span> | <span data-ttu-id="c94b9-115">Autorisation utilisateur</span><span class="sxs-lookup"><span data-stu-id="c94b9-115">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="c94b9-116">Liste</span><span class="sxs-lookup"><span data-stu-id="c94b9-116">List</span></span>|<span data-ttu-id="c94b9-117">Énumère les coffres de clé supprimés.</span><span class="sxs-lookup"><span data-stu-id="c94b9-117">Lists deleted key vaults.</span></span>|<span data-ttu-id="c94b9-118">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="c94b9-118">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="c94b9-119">Recover</span><span class="sxs-lookup"><span data-stu-id="c94b9-119">Recover</span></span>|<span data-ttu-id="c94b9-120">Restaure un coffre de clés supprimé.</span><span class="sxs-lookup"><span data-stu-id="c94b9-120">Restores a deleted key vault.</span></span>|<span data-ttu-id="c94b9-121">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="c94b9-121">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="c94b9-122">Purge</span><span class="sxs-lookup"><span data-stu-id="c94b9-122">Purge</span></span>|<span data-ttu-id="c94b9-123">Supprime définitivement un coffre de clés supprimé et tout son contenu.</span><span class="sxs-lookup"><span data-stu-id="c94b9-123">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="c94b9-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="c94b9-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="c94b9-125">Pour plus d’informations sur les autorisations et le contrôle d’accès, consultez [Sécuriser votre coffre de clés](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="c94b9-125">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="c94b9-126">Activation de la suppression réversible</span><span class="sxs-lookup"><span data-stu-id="c94b9-126">Enabling soft-delete</span></span>

<span data-ttu-id="c94b9-127">toorecover en mesure de toobe un coffre de clés supprimé ou des objets stockés dans une clé de coffre, vous devez d’abord activer soft-suppression de ce coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="c94b9-127">toobe able toorecover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="c94b9-128">Coffre de clés existant</span><span class="sxs-lookup"><span data-stu-id="c94b9-128">Existing key vault</span></span>

<span data-ttu-id="c94b9-129">Pour un coffre de clés existant nommé ContosoVault, vous pouvez activer la suppression réversible comme suit.</span><span class="sxs-lookup"><span data-stu-id="c94b9-129">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="c94b9-130">Actuellement, vous devez hello écriture de toouse Azure Resource Manager ressource manipulation toodirectly *enableSoftDelete* toohello de propriété de ressource du coffre de clé.</span><span class="sxs-lookup"><span data-stu-id="c94b9-130">Currently you need toouse Azure Resource Manager resource manipulation toodirectly write hello *enableSoftDelete* property toohello Key Vault resource.</span></span>

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a><span data-ttu-id="c94b9-131">Nouveau coffre de clés</span><span class="sxs-lookup"><span data-stu-id="c94b9-131">New key vault</span></span>

<span data-ttu-id="c94b9-132">L’activation du soft-suppression pour un nouveau coffre de clés est effectuée au moment de la création en ajoutant l’indicateur d’activation de soft-suppression de hello tooyour créer la commande.</span><span class="sxs-lookup"><span data-stu-id="c94b9-132">Enabling soft-delete for a new key vault is done at creation time by adding hello soft-delete enable flag tooyour create command.</span></span>

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="c94b9-133">Vérifier l’activation de la suppression réversible</span><span class="sxs-lookup"><span data-stu-id="c94b9-133">Verify soft-delete enablement</span></span>

<span data-ttu-id="c94b9-134">tooverify un coffre de clés a soft-suppression activée, exécution hello *afficher* de commandes et recherchez hello « Logicielle supprimer est-il activé ? »</span><span class="sxs-lookup"><span data-stu-id="c94b9-134">tooverify that a key vault has soft-delete enabled, run hello *show* command and look for hello 'Soft Delete Enabled?'</span></span> <span data-ttu-id="c94b9-135">et sa valeur (true ou false).</span><span class="sxs-lookup"><span data-stu-id="c94b9-135">attribute and its setting, true or false.</span></span>

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="c94b9-136">Suppression d’un coffre de clés protégé par la suppression réversible</span><span class="sxs-lookup"><span data-stu-id="c94b9-136">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="c94b9-137">commande de Hello toodelete (ou supprimer) un coffre de clés reste hello, mais ses modifications du comportement selon que vous avez activé soft-suppression ou non.</span><span class="sxs-lookup"><span data-stu-id="c94b9-137">hello command toodelete (or remove) a key vault remains hello same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
><span data-ttu-id="c94b9-138">Si vous exécutez la commande précédente hello pour un coffre de clés qui ne dispose pas de soft-suppression est activée, vous supprimer définitivement ce coffre de clés et tout son contenu sans les options de récupération.</span><span class="sxs-lookup"><span data-stu-id="c94b9-138">If you run hello previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="c94b9-139">Comment la suppression réversible protège-t-elle votre coffre de clés ?</span><span class="sxs-lookup"><span data-stu-id="c94b9-139">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="c94b9-140">Quand la suppression réversible est activée :</span><span class="sxs-lookup"><span data-stu-id="c94b9-140">With soft-delete enabled:</span></span>

- <span data-ttu-id="c94b9-141">Lorsqu’un coffre de clés est supprimé, il est supprimé de son groupe de ressources et placé dans un espace de noms réservé qui n’est associé à emplacement hello où il a été créé.</span><span class="sxs-lookup"><span data-stu-id="c94b9-141">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with hello location where it was created.</span></span> 
- <span data-ttu-id="c94b9-142">Les objets dans une clé supprimée de coffre, telles que les clés, les secrets et des certificats, sont inaccessibles et restent alors que leur conteneur coffre de clés est en état de hello supprimé.</span><span class="sxs-lookup"><span data-stu-id="c94b9-142">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in hello deleted state.</span></span> 
- <span data-ttu-id="c94b9-143">nom DNS de Hello pour un coffre de clés dans un état supprimé est toujours réservé pour un nouvel archivage de clés portant le même nom ne peut pas être créé.</span><span class="sxs-lookup"><span data-stu-id="c94b9-143">hello DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="c94b9-144">Vous pouvez consulter les coffres de clé d’état supprimé, associés à votre abonnement, à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c94b9-144">You may view deleted state key vaults, associated with your subscription, using hello following command:</span></span>

```azurecli
az keyvault list-deleted
```

<span data-ttu-id="c94b9-145">Hello *ID de ressource* Bonjour sortie fait référence toohello ID de ressource d’origine de ce coffre.</span><span class="sxs-lookup"><span data-stu-id="c94b9-145">hello *Resource ID* in hello output refers toohello original resource ID of this vault.</span></span> <span data-ttu-id="c94b9-146">Ce coffre de clés étant maintenant à l’état supprimé, il n’existe aucune ressource avec cet ID de ressource.</span><span class="sxs-lookup"><span data-stu-id="c94b9-146">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="c94b9-147">Hello *Id* champ peut être utilisé tooidentify hello ressource lors de la récupération ou de purge.</span><span class="sxs-lookup"><span data-stu-id="c94b9-147">hello *Id* field can be used tooidentify hello resource when recovering, or purging.</span></span> <span data-ttu-id="c94b9-148">Hello *Date de Purge planifiée* champ indique quand le coffre hello est définitivement supprimé (purge) si aucune action n’est effectuée pour cet archivage supprimé.</span><span class="sxs-lookup"><span data-stu-id="c94b9-148">hello *Scheduled Purge Date* field indicates when hello vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="c94b9-149">Bonjour par défaut rétention toocalculate période, utilisé Bonjour *Date de Purge planifiée*, est de 90 jours.</span><span class="sxs-lookup"><span data-stu-id="c94b9-149">hello default retention period, used toocalculate hello *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="c94b9-150">Récupération d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="c94b9-150">Recovering a key vault</span></span>

<span data-ttu-id="c94b9-151">toorecover un coffre de clés, vous avez besoin de nom de coffre de clés toospecify hello, groupe de ressources et l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="c94b9-151">toorecover a key vault, you need toospecify hello key vault name, resource group, and location.</span></span> <span data-ttu-id="c94b9-152">Remarque hello hello emplacement et le groupe de ressources de hello supprimé le coffre de clés dont vous avez besoin pour un processus de récupération de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="c94b9-152">Note hello location and hello resource group of hello deleted key vault as you need these for a key vault recovery process.</span></span>

```azurecli
az keyvault recover --location westus --name ContosoVault
```

<span data-ttu-id="c94b9-153">Une fois un coffre de clés est récupéré, hello il en résulte une nouvelle ressource avec l’ID de ressource du coffre de clés hello d’origine</span><span class="sxs-lookup"><span data-stu-id="c94b9-153">When a key vault is recovered, hello result is a new resource with hello key vault's original resource ID.</span></span> <span data-ttu-id="c94b9-154">Si le groupe de ressources hello où le coffre de clés hello existait a été supprimé, un nouveau groupe de ressources portant le même nom doit être créé avant de pouvoir récupérer le coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="c94b9-154">If hello resource group where hello key vault existed has been removed, a new resource group with same name must be created before hello key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="c94b9-155">Objets de coffre de clés et suppression réversible</span><span class="sxs-lookup"><span data-stu-id="c94b9-155">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="c94b9-156">Pour une clé nommée « ContosoFirstKey » dans un coffre de clés nommé « ContosoVault » avec la suppression réversible activée, voici comment vous supprimeriez cette clé.</span><span class="sxs-lookup"><span data-stu-id="c94b9-156">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="c94b9-157">Quand la suppression réversible est activée pour votre coffre de clés, une clé supprimée apparaît toujours comme ayant été supprimée, sauf quand vous énumérez ou récupérez explicitement les clés supprimées.</span><span class="sxs-lookup"><span data-stu-id="c94b9-157">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="c94b9-158">La plupart des opérations sur une clé dans l’état de hello supprimée échoue, à l’exception répertoriant une clé supprimée, sa récupération ou il purge.</span><span class="sxs-lookup"><span data-stu-id="c94b9-158">Most operations on a key in hello deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="c94b9-159">Par exemple, toorequest les clés de toolist supprimé dans un coffre de clés, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c94b9-159">For example, toorequest toolist deleted keys in a key vault, use hello following command:</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a><span data-ttu-id="c94b9-160">État de transition</span><span class="sxs-lookup"><span data-stu-id="c94b9-160">Transition state</span></span> 

<span data-ttu-id="c94b9-161">Lorsque vous supprimez une clé dans un coffre de clés avec soft-suppression est activée, elle peut prendre quelques secondes que hello transition toocomplete.</span><span class="sxs-lookup"><span data-stu-id="c94b9-161">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for hello transition toocomplete.</span></span> <span data-ttu-id="c94b9-162">Au cours de cet état de transition, il peut apparaître que cette clé hello n’est pas dans état actif de hello ou hello supprimé.</span><span class="sxs-lookup"><span data-stu-id="c94b9-162">During this transition state, it may appear that hello key is not in hello active state or hello deleted state.</span></span> <span data-ttu-id="c94b9-163">Cette commande répertorie toutes les clés supprimées dans votre coffre de clés nommé « ContosoVault ».</span><span class="sxs-lookup"><span data-stu-id="c94b9-163">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="c94b9-164">Utilisation de la suppression réversible avec des objets de coffre de clés</span><span class="sxs-lookup"><span data-stu-id="c94b9-164">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="c94b9-165">À l’instar de coffres de clé, une clé supprimée, secret ou des certificats reste dans un état supprimé pour too90 jours, sauf si vous le récupérer ou purger.</span><span class="sxs-lookup"><span data-stu-id="c94b9-165">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up too90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="c94b9-166">Clés</span><span class="sxs-lookup"><span data-stu-id="c94b9-166">Keys</span></span>

<span data-ttu-id="c94b9-167">toorecover une clé supprimée :</span><span class="sxs-lookup"><span data-stu-id="c94b9-167">toorecover a deleted key:</span></span>

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="c94b9-168">toopermanently supprimer une clé :</span><span class="sxs-lookup"><span data-stu-id="c94b9-168">toopermanently delete a key:</span></span>

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="c94b9-169">Le vidage d’une clé entraîne sa suppression définitive, ce qui signifie que vous ne pourrez pas la récupérer.</span><span class="sxs-lookup"><span data-stu-id="c94b9-169">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="c94b9-170">Hello **récupérer** et **purger** actions ont leurs propres autorisations associés liées une stratégie d’accès de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="c94b9-170">hello **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="c94b9-171">Pour un tooexecute en mesure de toobe principal utilisateur ou un service une **récupérer** ou **purger** action qu’ils doivent autorisé hello respectifs pour cet objet (clé ou le secret) dans la stratégie d’accès hello coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="c94b9-171">For a user or service principal toobe able tooexecute a **recover** or **purge** action they must have hello respective permission for that object (key or secret) in hello key vault access policy.</span></span> <span data-ttu-id="c94b9-172">Par défaut, hello **purger** autorisation n’est pas ajoutée la stratégie d’accès du coffre de clés tooa lorsque hello contextuel 'all' est utilisé toogrant toutes les autorisations tooa utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c94b9-172">By default, hello **purge** permission is not added tooa key vault's access policy when hello 'all' shortcut is used toogrant all permissions tooa user.</span></span> <span data-ttu-id="c94b9-173">Vous devez accorder explicitement l’autorisation**purge**.</span><span class="sxs-lookup"><span data-stu-id="c94b9-173">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="c94b9-174">Par exemple, hello suivant accorde de la commande user@contoso.com tooperform d’autorisation plusieurs opérations sur les clés dans *ContosoVault* notamment **purger**.</span><span class="sxs-lookup"><span data-stu-id="c94b9-174">For example, hello following command grants user@contoso.com permission tooperform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="c94b9-175">Définir une stratégie d’accès au coffre de clés</span><span class="sxs-lookup"><span data-stu-id="c94b9-175">Set a key vault access policy</span></span>

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> <span data-ttu-id="c94b9-176">Si vous avez un coffre de clés pour lequel la suppression réversible vient d’être activée, vous ne disposerez peut-être pas des autorisations **recover** et **purge**.</span><span class="sxs-lookup"><span data-stu-id="c94b9-176">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="c94b9-177">Secrets</span><span class="sxs-lookup"><span data-stu-id="c94b9-177">Secrets</span></span>

<span data-ttu-id="c94b9-178">Comme les clés, les secrets dans un coffre de clés sont gérés avec leurs propres commandes.</span><span class="sxs-lookup"><span data-stu-id="c94b9-178">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="c94b9-179">Suivant, sont des commandes de hello pour suppression, liste, la récupération et la purge des clés secrètes.</span><span class="sxs-lookup"><span data-stu-id="c94b9-179">Following, are hello commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="c94b9-180">Supprimer un secret nommé SQLPassword :</span><span class="sxs-lookup"><span data-stu-id="c94b9-180">Delete a secret named SQLPassword:</span></span> 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- <span data-ttu-id="c94b9-181">Énumérer tous les secrets supprimés dans un coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="c94b9-181">List all deleted secrets in a key vault:</span></span> 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- <span data-ttu-id="c94b9-182">Restaurer un secret de l’état de hello supprimé :</span><span class="sxs-lookup"><span data-stu-id="c94b9-182">Recover a secret in hello deleted state:</span></span> 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- <span data-ttu-id="c94b9-183">Vider un secret à l’état supprimé :</span><span class="sxs-lookup"><span data-stu-id="c94b9-183">Purge a secret in deleted state:</span></span> 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="c94b9-184">Le vidage d’un secret entraîne sa suppression définitive, ce qui signifie que vous ne pourrez pas le récupérer.</span><span class="sxs-lookup"><span data-stu-id="c94b9-184">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="c94b9-185">Vidage et coffres de clé</span><span class="sxs-lookup"><span data-stu-id="c94b9-185">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="c94b9-186">Objets de coffre de clés</span><span class="sxs-lookup"><span data-stu-id="c94b9-186">Key vault objects</span></span>

<span data-ttu-id="c94b9-187">Le vidage d’une clé, d’un secret ou d’un certificat entraîne sa suppression définitive, ce qui signifie que vous ne pourrez pas le récupérer.</span><span class="sxs-lookup"><span data-stu-id="c94b9-187">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="c94b9-188">coffre de clés Hello qui contenait hello supprimé objet toutefois reste intact ainsi que tous les autres objets dans le coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="c94b9-188">hello key vault that contained hello deleted object will however remain intact as will all other objects in hello key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="c94b9-189">Coffres de clé en tant que conteneurs</span><span class="sxs-lookup"><span data-stu-id="c94b9-189">Key vaults as containers</span></span>
<span data-ttu-id="c94b9-190">Quand un coffre de clés est vidé, tout son contenu, notamment les clés, les secrets et les certificats, sont supprimés définitivement.</span><span class="sxs-lookup"><span data-stu-id="c94b9-190">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="c94b9-191">toopurge un coffre de clés, utilisez hello `az keyvault purge` commande.</span><span class="sxs-lookup"><span data-stu-id="c94b9-191">toopurge a key vault, use hello `az keyvault purge` command.</span></span> <span data-ttu-id="c94b9-192">Vous pouvez localiser hello coffres clé supprimé de votre abonnement à l’aide de la commande hello `az keyvault list-deleted`.</span><span class="sxs-lookup"><span data-stu-id="c94b9-192">You can find hello location your subscription's deleted key vaults using hello command `az keyvault list-deleted`.</span></span>

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
><span data-ttu-id="c94b9-193">Le vidage d’un coffre de clés entraîne sa suppression définitive, ce qui signifie que vous ne pourrez pas le récupérer.</span><span class="sxs-lookup"><span data-stu-id="c94b9-193">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="c94b9-194">Autorisations de vidage requises</span><span class="sxs-lookup"><span data-stu-id="c94b9-194">Purge permissions required</span></span>
- <span data-ttu-id="c94b9-195">toopurge un coffre de clés supprimé, telles que le coffre hello et tout son contenu est définitivement supprimées, hello utilisateur doit RBAC autorisation tooperform un *Microsoft.KeyVault/locations/deletedVaults/purge/action* opération.</span><span class="sxs-lookup"><span data-stu-id="c94b9-195">toopurge a deleted key vault, such that hello vault and all its contents are permanently removed, hello user needs RBAC permission tooperform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="c94b9-196">clé de hello supprimé de toolist, le coffre hello un utilisateur doit RBAC autorisation tooperform *Microsoft.KeyVault/deletedVaults/read* autorisation.</span><span class="sxs-lookup"><span data-stu-id="c94b9-196">toolist hello deleted key, hello vault a user needs RBAC permission tooperform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="c94b9-197">Par défaut, seul un administrateur d’abonnement dispose de ces autorisations.</span><span class="sxs-lookup"><span data-stu-id="c94b9-197">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="c94b9-198">Vidage planifié</span><span class="sxs-lookup"><span data-stu-id="c94b9-198">Scheduled purge</span></span>

<span data-ttu-id="c94b9-199">Liste des objets de votre coffre de clés supprimées montre lorsqu’ils sont toobe schedled supprimé par le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="c94b9-199">Listing your deleted key vault objects shows when they are schedled toobe purged by Key Vault.</span></span> <span data-ttu-id="c94b9-200">Hello *Date de Purge planifiée* champ indique quand un objet de coffre de clés est définitivement supprimé, si aucune action n’est effectuée.</span><span class="sxs-lookup"><span data-stu-id="c94b9-200">hello *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="c94b9-201">Par défaut, la période de rétention hello pour un objet supprimé de coffre de clés est 90 jours.</span><span class="sxs-lookup"><span data-stu-id="c94b9-201">By default, hello retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="c94b9-202">Un objet de coffre dont le vidage est déclenché par son champ *Date de vidage planifiée* est supprimé définitivement.</span><span class="sxs-lookup"><span data-stu-id="c94b9-202">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="c94b9-203">Il n’est pas récupérable.</span><span class="sxs-lookup"><span data-stu-id="c94b9-203">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="c94b9-204">Autres ressources</span><span class="sxs-lookup"><span data-stu-id="c94b9-204">Other resources</span></span>

- <span data-ttu-id="c94b9-205">Pour obtenir une présentation de la fonctionnalité de suppression réversible, consultez [Présentation de la suppression réversible d’Azure Key Vault](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="c94b9-205">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="c94b9-206">Pour obtenir une vue d’ensemble de l’utilisation d’Azure Key Vault, consultez [Bien démarrer avec Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c94b9-206">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

