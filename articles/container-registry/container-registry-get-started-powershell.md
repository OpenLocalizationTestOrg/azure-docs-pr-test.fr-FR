---
title: "référentiels de Registre de conteneur aaaAzure | Documents Microsoft"
description: "Comment toouse les référentiels de Registre de conteneur Azure pour les images de Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: cristyg
ms.openlocfilehash: 448fb812f537c9502041ce5fb372b0681a9dac4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-powershell"></a>Créer un Registre de conteneur Docker privé à l’aide de hello Azure PowerShell
Utiliser les commandes dans [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate un Registre de conteneur et de gérer ses paramètres de votre ordinateur Windows. Vous pouvez également créer et gérer des registres de conteneur à l’aide de hello [portail Azure](container-registry-get-started-portal.md), hello [CLI d’Azure](container-registry-get-started-azure-cli.md), ou par programme avec hello Registre de conteneur [API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).


* Pour des informations et des concepts, consultez [hello vue d’ensemble](container-registry-intro.md)
* Pour obtenir une liste complète des applets de commande pris en charge, consultez [Applets de commande de gestion d’Azure Container Registry](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).


## <a name="prerequisites"></a>Composants requis
* **Azure PowerShell**: tooinstall et prise en main Azure PowerShell, consultez hello [des instructions d’installation](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps). Connectez-vous à tooyour abonnement Azure en exécutant `Login-AzureRMAccount`. Pour plus d’informations, consultez [Bien démarrer avec Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).
* **Groupe de ressources** : créez un [groupe de ressources](../azure-resource-manager/resource-group-overview.md#resource-groups) avant de créer un registre de conteneur, ou utilisez un groupe de ressources existant. Assurez-vous que le groupe de ressources hello est dans un emplacement où le service de Registre de conteneur de hello est [disponible](https://azure.microsoft.com/regions/services/). toocreate un groupe de ressources à l’aide d’Azure PowerShell, consultez [hello référence PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).
* **Compte de stockage** (facultatif) : créez un Azure standard [compte de stockage](../storage/common/storage-introduction.md) tooback Registre de conteneur hello Bonjour même emplacement. Si vous ne spécifiez pas un compte de stockage lors de la création d’un Registre avec `New-AzureRMContainerRegistry`, commande hello crée une pour vous. toocreate un stockage compte à l’aide de PowerShell, consultez [hello référence PowerShell](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount). Pour l’instant, l’offre Stockage Premium n’est pas prise en charge.
* **Principal de service** (facultatif) : lorsque vous créez un registre avec PowerShell, par défaut son accès n’est pas configuré. Selon vos besoins, vous pouvez affecter un Registre tooa principal de service Azure Active Directory existant ou créer et affecter un nouveau. Vous pouvez également activer compte d’utilisateur admin du Registre hello. Consultez les sections hello plus loin dans cet article. Pour plus d’informations sur l’accès au Registre, consultez [authentifier avec le Registre de conteneur hello](container-registry-authentication.md).

## <a name="create-a-container-registry"></a>Créer un registre de conteneur
Exécutez hello `New-AzureRMContainerRegistry` commande toocreate un Registre de conteneur.

> [!TIP]
> Lorsque vous créez un registre, spécifiez un nom de domaine global unique de niveau supérieur, contenant uniquement des chiffres et des lettres. nom de Registre Hello dans les exemples hello est `MyRegistry`, mais remplacer par un nom unique de votre choix.
>
>

Hello utilise hello Registre de conteneur toocreate minimal de paramètres de commande suivante `MyRegistry` dans le groupe de ressources hello `MyResourceGroup` Bonjour emplacement Amérique du Sud :

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* `-StorageAccountName` est facultatif. Si ce n’est pas spécifié, un compte de stockage est créé avec un nom composé du nom de Registre hello et un horodatage dans hello spécifié le groupe de ressources.

## <a name="assign-a-service-principal"></a>Affecter un principal de service
Utilisez tooassign de commandes PowerShell Azure Active Directory [principal du service](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa Registre. Hello principal du service dans ces exemples se voit attribuer hello propriétaire du rôle, mais vous pouvez affecter [autres rôles](../active-directory/role-based-access-control-configure.md) si vous le souhaitez.

### <a name="create-a-service-principal"></a>Créer un principal du service
Bonjour la commande suivante, un principal de service est créé. Spécifiez un mot de passe fort avec hello `-Password` paramètre.

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a>Affecter un principal de service existant ou nouveau
Vous pouvez affecter un nouveau paramètre ou un Registre tooa principal de service existant. tooassign il propriétaire du rôle accès toohello exécution de Registre, un toohello similaire commande l’exemple suivant :

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-toohello-registry-with-hello-service-principal"></a>Connectez-vous au Registre toohello avec principal du service hello
Après avoir affecté Registre toohello principal du service hello, vous pouvez vous connecter avec hello de commande suivante :

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a>Gérer les informations d’identification de l’administrateur
Un compte d’administrateur est automatiquement créé pour chaque registre de conteneur et est désactivé par défaut. Hello exemples suivants illustrent les commandes PowerShell toomanage hello admin informations d’identification pour votre Registre de conteneur.

### <a name="obtain-admin-user-credentials"></a>Obtenir les informations d’identification de l’utilisateur Admin
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a>Activer l’utilisateur Admin pour un registre existant
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a>Désactiver l’utilisateur Admin pour un registre existant
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a>Étapes suivantes
* [Push de votre première image à l’aide de hello Docker CLI](container-registry-get-started-docker-cli.md)
