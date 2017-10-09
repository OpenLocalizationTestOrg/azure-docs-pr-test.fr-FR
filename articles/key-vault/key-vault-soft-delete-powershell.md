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
# <a name="how-toouse-key-vault-soft-delete-with-powershell"></a>Comment toouse le coffre de clés soft-suppression avec PowerShell

La fonctionnalité de suppression réversible d’Azure Key Vault permet de récupérer des coffres et des objets de coffres qui ont été supprimés. Plus précisément, les adresses de soft-suppression hello les scénarios suivants :

- Prise en charge de la suppression récupérable d’un coffre de clés
- Prise en charge de la suppression récupérable d’objets de coffre de clés (clés, secrets et certificats)

## <a name="prerequisites"></a>Composants requis

- Azure PowerShell 4.0.0 ou version ultérieure - si vous n’avez ce déjà le programme d’installation, installez Azure PowerShell et associez-le à votre abonnement Azure, consultez [comment tooinstall et configurer Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview). 

>[!NOTE]
> Il existe une version obsolète de notre sortie PowerShell de coffre de clé mise en forme de fichiers qui **peut** être chargé dans votre environnement au lieu de la version correcte de hello. Nous anticipation de que correction de besoin d’une version mise à jour PowerShell toocontain hello pour le format de sortie hello et met à jour de cette rubrique à ce moment-là. Hello solution de contournement actuelle, si vous rencontrez ce problème de mise en forme, est :
> - Hello utilisation suivant la requête si vous remarquez que vous ne voyez hello soft-suppression activé la propriété décrite dans cette rubrique : `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.


Pour obtenir des informations de référence propres à Key Vault pour PowerShell, consultez la [référence Key Vault Azure PowerShell](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).

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

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a>Nouveau coffre de clés

L’activation du soft-suppression pour un nouveau coffre de clés est effectuée au moment de la création en ajoutant l’indicateur d’activation de soft-suppression de hello tooyour créer la commande.

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a>Vérifier l’activation de la suppression réversible

tooverify un coffre de clés a soft-suppression activée, exécution hello *obtenir* de commandes et recherchez hello « Logicielle supprimer est-il activé ? » et sa valeur (true ou false).

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a>Suppression d’un coffre de clés protégé par la suppression réversible

commande de Hello toodelete (ou supprimer) un coffre de clés reste hello, mais ses modifications du comportement selon que vous avez activé soft-suppression ou non.

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
>Si vous exécutez la commande précédente hello pour un coffre de clés qui ne dispose pas de soft-suppression est activée, vous supprimer définitivement ce coffre de clés et tout son contenu sans les options de récupération.

### <a name="how-soft-delete-protects-your-key-vaults"></a>Comment la suppression réversible protège-t-elle votre coffre de clés ?

Quand la suppression réversible est activée :

- Lorsqu’un coffre de clés est supprimé, il est supprimé de son groupe de ressources et placé dans un espace de noms réservé qui n’est associé à emplacement hello où il a été créé. 
- Les objets dans une clé supprimée de coffre, telles que les clés, les secrets et des certificats, sont inaccessibles et restent alors que leur conteneur coffre de clés est en état de hello supprimé. 
- nom DNS de Hello pour un coffre de clés dans un état supprimé est toujours réservé pour un nouvel archivage de clés portant le même nom ne peut pas être créé.  

Vous pouvez consulter les coffres de clé d’état supprimé, associés à votre abonnement, à l’aide de hello de commande suivante :

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

Hello *ID de ressource* Bonjour sortie fait référence toohello ID de ressource d’origine de ce coffre. Ce coffre de clés étant maintenant à l’état supprimé, il n’existe aucune ressource avec cet ID de ressource. Hello *Id* champ peut être utilisé tooidentify hello ressource lors de la récupération ou de purge. Hello *Date de Purge planifiée* champ indique quand le coffre hello est définitivement supprimé (purge) si aucune action n’est effectuée pour cet archivage supprimé. Bonjour par défaut rétention toocalculate période, utilisé Bonjour *Date de Purge planifiée*, est de 90 jours.

## <a name="recovering-a-key-vault"></a>Récupération d’un coffre de clés

toorecover un coffre de clés, vous avez besoin de nom de coffre de clés toospecify hello, groupe de ressources et l’emplacement. Remarque hello hello emplacement et le groupe de ressources de hello supprimé le coffre de clés dont vous avez besoin pour un processus de récupération de coffre de clés.

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

Une fois un coffre de clés est récupéré, hello il en résulte une nouvelle ressource avec l’ID de ressource du coffre de clés hello d’origine Si le groupe de ressources hello où le coffre de clés hello existait a été supprimé, un nouveau groupe de ressources portant le même nom doit être créé avant de pouvoir récupérer le coffre de clés hello.

## <a name="key-vault-objects-and-soft-delete"></a>Objets de coffre de clés et suppression réversible

Pour une clé nommée « ContosoFirstKey » dans un coffre de clés nommé « ContosoVault » avec la suppression réversible activée, voici comment vous supprimeriez cette clé.

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

Quand la suppression réversible est activée pour votre coffre de clés, une clé supprimée apparaît toujours comme ayant été supprimée, sauf quand vous énumérez ou récupérez explicitement les clés supprimées. La plupart des opérations sur une clé dans l’état de hello supprimée échoue, à l’exception répertoriant une clé supprimée, sa récupération ou il purge. 

Par exemple, toorequest les clés de toolist supprimé dans un coffre de clés, utilisez hello de commande suivante :

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a>État de transition 

Lorsque vous supprimez une clé dans un coffre de clés avec soft-suppression est activée, elle peut prendre quelques secondes que hello transition toocomplete. Au cours de cet état de transition, il peut apparaître que cette clé hello n’est pas dans état actif de hello ou hello supprimé. Cette commande répertorie toutes les clés supprimées dans votre coffre de clés nommé « ContosoVault ».

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

### <a name="using-soft-delete-with-key-vault-objects"></a>Utilisation de la suppression réversible avec des objets de coffre de clés

À l’instar de coffres de clé, une clé supprimée, secret ou des certificats reste dans un état supprimé pour too90 jours, sauf si vous le récupérer ou purger. 

#### <a name="keys"></a>Clés

toorecover une clé supprimée :

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

toopermanently supprimer une clé :

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
>Le vidage d’une clé entraîne sa suppression définitive, ce qui signifie que vous ne pourrez pas la récupérer.

Hello **récupérer** et **purger** actions ont leurs propres autorisations associés liées une stratégie d’accès de coffre de clés. Pour un tooexecute en mesure de toobe principal utilisateur ou un service une **récupérer** ou **purger** action qu’ils doivent autorisé hello respectifs pour cet objet (clé ou le secret) dans la stratégie d’accès hello coffre de clés. Par défaut, hello **purger** autorisation n’est pas ajoutée la stratégie d’accès du coffre de clés tooa lorsque hello contextuel 'all' est utilisé toogrant toutes les autorisations tooa utilisateur. Vous devez accorder explicitement l’autorisation**purge**. Par exemple, hello suivant accorde de la commande user@contoso.com tooperform d’autorisation plusieurs opérations sur les clés dans *ContosoVault* notamment **purger**.

#### <a name="set-a-key-vault-access-policy"></a>Définir une stratégie d’accès au coffre de clés

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> Si vous avez un coffre de clés pour lequel la suppression réversible vient d’être activée, vous ne disposerez peut-être pas des autorisations **recover** et **purge**.

#### <a name="secrets"></a>Secrets

Comme les clés, les secrets dans un coffre de clés sont gérés avec leurs propres commandes. Suivant, sont des commandes de hello pour suppression, liste, la récupération et la purge des clés secrètes.

- Supprimer un secret nommé SQLPassword : 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- Énumérer tous les secrets supprimés dans un coffre de clés : 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- Restaurer un secret de l’état de hello supprimé : 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- Vider un secret à l’état supprimé : 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
>Le vidage d’un secret entraîne sa suppression définitive, ce qui signifie que vous ne pourrez pas le récupérer.

## <a name="purging-and-key-vaults"></a>Vidage et coffres de clé

### <a name="key-vault-objects"></a>Objets de coffre de clés

Le vidage d’une clé, d’un secret ou d’un certificat entraîne sa suppression définitive, ce qui signifie que vous ne pourrez pas le récupérer. coffre de clés Hello qui contenait hello supprimé objet toutefois reste intact ainsi que tous les autres objets dans le coffre de clés hello. 

### <a name="key-vaults-as-containers"></a>Coffres de clé en tant que conteneurs
Quand un coffre de clés est vidé, tout son contenu, notamment les clés, les secrets et les certificats, sont supprimés définitivement. toopurge un coffre de clés, utilisez hello `Remove-AzureRmKeyVault` avec l’option de hello `-InRemovedState` et en spécifiant l’emplacement hello de coffre de clés hello supprimé par hello `-Location location` argument. Vous pouvez localiser hello un coffre supprimé à l’aide de la commande hello `Get-AzureRmKeyVault -InRemovedState`.

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
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

