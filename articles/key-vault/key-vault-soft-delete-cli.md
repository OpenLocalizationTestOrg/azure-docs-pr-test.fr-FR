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
# <a name="how-toouse-key-vault-soft-delete-with-cli"></a>Comment toouse le coffre de clés soft-suppression avec l’interface CLI

La fonctionnalité de suppression réversible d’Azure Key Vault permet de récupérer des coffres et des objets de coffres qui ont été supprimés. Plus précisément, les adresses de soft-suppression hello les scénarios suivants :

- Prise en charge de la suppression récupérable d’un coffre de clés
- Prise en charge de la suppression récupérable d’objets de coffre de clés (clés, secrets et certificats)

## <a name="prerequisites"></a>Prérequis

- Azure CLI 2.0 - Si vous ne l’avez pas encore installé pour votre environnement, consultez [Gestion de Key Vault à l’aide de l’interface de ligne de commande (CLI) 2.0](key-vault-manage-with-cli2.md).

Pour obtenir des informations de référence propres à Key Vault pour l’interface CLI, consultez la [référence Key Vault Azure CLI 2.0](https://docs.microsoft.com/cli/azure/keyvault).

## <a name="required-permissions"></a>Autorisations requises

Les opérations Key Vault sont gérées séparément par l’intermédiaire d’autorisations de contrôle d’accès en fonction du rôle (RBAC) comme suit :

| Opération | Description | Autorisation utilisateur |
|:--|:--|:--|
|Liste|Énumère les coffres de clé supprimés.|Microsoft.KeyVault/deletedVaults/read|
|Recover|Restaure un coffre de clés supprimé.|Microsoft.KeyVault/vaults/write|
|Purge|Supprime définitivement un coffre de clés supprimé et tout son contenu.|Microsoft.KeyVault/locations/deletedVaults/purge/action|

Pour plus d’informations sur les autorisations et le contrôle d’accès, consultez [Sécuriser votre coffre de clés](key-vault-secure-your-key-vault.md).

## <a name="enabling-soft-delete"></a>Activation de la suppression réversible

toorecover en mesure de toobe un coffre de clés supprimé ou des objets stockés dans une clé de coffre, vous devez d’abord activer soft-suppression de ce coffre de clés.

### <a name="existing-key-vault"></a>Coffre de clés existant

Pour un coffre de clés existant nommé ContosoVault, vous pouvez activer la suppression réversible comme suit. 

>[!NOTE]
>Actuellement, vous devez hello écriture de toouse Azure Resource Manager ressource manipulation toodirectly *enableSoftDelete* toohello de propriété de ressource du coffre de clé.

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a>Nouveau coffre de clés

L’activation du soft-suppression pour un nouveau coffre de clés est effectuée au moment de la création en ajoutant l’indicateur d’activation de soft-suppression de hello tooyour créer la commande.

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a>Vérifier l’activation de la suppression réversible

tooverify un coffre de clés a soft-suppression activée, exécution hello *afficher* de commandes et recherchez hello « Logicielle supprimer est-il activé ? » et sa valeur (true ou false).

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a>Suppression d’un coffre de clés protégé par la suppression réversible

commande de Hello toodelete (ou supprimer) un coffre de clés reste hello, mais ses modifications du comportement selon que vous avez activé soft-suppression ou non.

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
>Si vous exécutez la commande précédente hello pour un coffre de clés qui ne dispose pas de soft-suppression est activée, vous supprimer définitivement ce coffre de clés et tout son contenu sans les options de récupération.

### <a name="how-soft-delete-protects-your-key-vaults"></a>Comment la suppression réversible protège-t-elle votre coffre de clés ?

Quand la suppression réversible est activée :

- Lorsqu’un coffre de clés est supprimé, il est supprimé de son groupe de ressources et placé dans un espace de noms réservé qui n’est associé à emplacement hello où il a été créé. 
- Les objets dans une clé supprimée de coffre, telles que les clés, les secrets et des certificats, sont inaccessibles et restent alors que leur conteneur coffre de clés est en état de hello supprimé. 
- nom DNS de Hello pour un coffre de clés dans un état supprimé est toujours réservé pour un nouvel archivage de clés portant le même nom ne peut pas être créé.  

Vous pouvez consulter les coffres de clé d’état supprimé, associés à votre abonnement, à l’aide de hello de commande suivante :

```azurecli
az keyvault list-deleted
```

Hello *ID de ressource* Bonjour sortie fait référence toohello ID de ressource d’origine de ce coffre. Ce coffre de clés étant maintenant à l’état supprimé, il n’existe aucune ressource avec cet ID de ressource. Hello *Id* champ peut être utilisé tooidentify hello ressource lors de la récupération ou de purge. Hello *Date de Purge planifiée* champ indique quand le coffre hello est définitivement supprimé (purge) si aucune action n’est effectuée pour cet archivage supprimé. Bonjour par défaut rétention toocalculate période, utilisé Bonjour *Date de Purge planifiée*, est de 90 jours.

## <a name="recovering-a-key-vault"></a>Récupération d’un coffre de clés

toorecover un coffre de clés, vous avez besoin de nom de coffre de clés toospecify hello, groupe de ressources et l’emplacement. Remarque hello hello emplacement et le groupe de ressources de hello supprimé le coffre de clés dont vous avez besoin pour un processus de récupération de coffre de clés.

```azurecli
az keyvault recover --location westus --name ContosoVault
```

Une fois un coffre de clés est récupéré, hello il en résulte une nouvelle ressource avec l’ID de ressource du coffre de clés hello d’origine Si le groupe de ressources hello où le coffre de clés hello existait a été supprimé, un nouveau groupe de ressources portant le même nom doit être créé avant de pouvoir récupérer le coffre de clés hello.

## <a name="key-vault-objects-and-soft-delete"></a>Objets de coffre de clés et suppression réversible

Pour une clé nommée « ContosoFirstKey » dans un coffre de clés nommé « ContosoVault » avec la suppression réversible activée, voici comment vous supprimeriez cette clé.

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

Quand la suppression réversible est activée pour votre coffre de clés, une clé supprimée apparaît toujours comme ayant été supprimée, sauf quand vous énumérez ou récupérez explicitement les clés supprimées. La plupart des opérations sur une clé dans l’état de hello supprimée échoue, à l’exception répertoriant une clé supprimée, sa récupération ou il purge. 

Par exemple, toorequest les clés de toolist supprimé dans un coffre de clés, utilisez hello de commande suivante :

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a>État de transition 

Lorsque vous supprimez une clé dans un coffre de clés avec soft-suppression est activée, elle peut prendre quelques secondes que hello transition toocomplete. Au cours de cet état de transition, il peut apparaître que cette clé hello n’est pas dans état actif de hello ou hello supprimé. Cette commande répertorie toutes les clés supprimées dans votre coffre de clés nommé « ContosoVault ».

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a>Utilisation de la suppression réversible avec des objets de coffre de clés

À l’instar de coffres de clé, une clé supprimée, secret ou des certificats reste dans un état supprimé pour too90 jours, sauf si vous le récupérer ou purger. 

#### <a name="keys"></a>Clés

toorecover une clé supprimée :

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

toopermanently supprimer une clé :

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
>Le vidage d’une clé entraîne sa suppression définitive, ce qui signifie que vous ne pourrez pas la récupérer.

Hello **récupérer** et **purger** actions ont leurs propres autorisations associés liées une stratégie d’accès de coffre de clés. Pour un tooexecute en mesure de toobe principal utilisateur ou un service une **récupérer** ou **purger** action qu’ils doivent autorisé hello respectifs pour cet objet (clé ou le secret) dans la stratégie d’accès hello coffre de clés. Par défaut, hello **purger** autorisation n’est pas ajoutée la stratégie d’accès du coffre de clés tooa lorsque hello contextuel 'all' est utilisé toogrant toutes les autorisations tooa utilisateur. Vous devez accorder explicitement l’autorisation**purge**. Par exemple, hello suivant accorde de la commande user@contoso.com tooperform d’autorisation plusieurs opérations sur les clés dans *ContosoVault* notamment **purger**.

#### <a name="set-a-key-vault-access-policy"></a>Définir une stratégie d’accès au coffre de clés

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> Si vous avez un coffre de clés pour lequel la suppression réversible vient d’être activée, vous ne disposerez peut-être pas des autorisations **recover** et **purge**.

#### <a name="secrets"></a>Secrets

Comme les clés, les secrets dans un coffre de clés sont gérés avec leurs propres commandes. Suivant, sont des commandes de hello pour suppression, liste, la récupération et la purge des clés secrètes.

- Supprimer un secret nommé SQLPassword : 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- Énumérer tous les secrets supprimés dans un coffre de clés : 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- Restaurer un secret de l’état de hello supprimé : 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- Vider un secret à l’état supprimé : 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
>Le vidage d’un secret entraîne sa suppression définitive, ce qui signifie que vous ne pourrez pas le récupérer.

## <a name="purging-and-key-vaults"></a>Vidage et coffres de clé

### <a name="key-vault-objects"></a>Objets de coffre de clés

Le vidage d’une clé, d’un secret ou d’un certificat entraîne sa suppression définitive, ce qui signifie que vous ne pourrez pas le récupérer. coffre de clés Hello qui contenait hello supprimé objet toutefois reste intact ainsi que tous les autres objets dans le coffre de clés hello. 

### <a name="key-vaults-as-containers"></a>Coffres de clé en tant que conteneurs
Quand un coffre de clés est vidé, tout son contenu, notamment les clés, les secrets et les certificats, sont supprimés définitivement. toopurge un coffre de clés, utilisez hello `az keyvault purge` commande. Vous pouvez localiser hello coffres clé supprimé de votre abonnement à l’aide de la commande hello `az keyvault list-deleted`.

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
>Le vidage d’un coffre de clés entraîne sa suppression définitive, ce qui signifie que vous ne pourrez pas le récupérer.

### <a name="purge-permissions-required"></a>Autorisations de vidage requises
- toopurge un coffre de clés supprimé, telles que le coffre hello et tout son contenu est définitivement supprimées, hello utilisateur doit RBAC autorisation tooperform un *Microsoft.KeyVault/locations/deletedVaults/purge/action* opération. 
- clé de hello supprimé de toolist, le coffre hello un utilisateur doit RBAC autorisation tooperform *Microsoft.KeyVault/deletedVaults/read* autorisation. 
- Par défaut, seul un administrateur d’abonnement dispose de ces autorisations. 

### <a name="scheduled-purge"></a>Vidage planifié

Liste des objets de votre coffre de clés supprimées montre lorsqu’ils sont toobe schedled supprimé par le coffre de clés. Hello *Date de Purge planifiée* champ indique quand un objet de coffre de clés est définitivement supprimé, si aucune action n’est effectuée. Par défaut, la période de rétention hello pour un objet supprimé de coffre de clés est 90 jours.

>[!NOTE]
>Un objet de coffre dont le vidage est déclenché par son champ *Date de vidage planifiée* est supprimé définitivement. Il n’est pas récupérable.

## <a name="other-resources"></a>Autres ressources

- Pour obtenir une présentation de la fonctionnalité de suppression réversible, consultez [Présentation de la suppression réversible d’Azure Key Vault](key-vault-ovw-soft-delete.md).
- Pour obtenir une vue d’ensemble de l’utilisation d’Azure Key Vault, consultez [Bien démarrer avec Azure Key Vault](key-vault-get-started.md).

