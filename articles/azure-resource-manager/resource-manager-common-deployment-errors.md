---
title: "erreurs de déploiement Azure courantes aaaTroubleshoot | Documents Microsoft"
description: "Décrit comment tooresolve les erreurs courantes lors du déploiement de tooAzure de ressources à l’aide du Gestionnaire de ressources Azure."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "Erreur de déploiement, déploiement d’azure, déployez tooazure"
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 8571e9941879eb5586e4258a785b6a09247da771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a>Résolution des erreurs courantes dans des déploiements Azure avec Azure Resource Manager
Cette rubrique décrit comment résoudre certaines erreurs courantes liées au déploiement d’Azure que vous pouvez rencontrer.

Hello suivant des codes d’erreur est décrites dans cette rubrique :

* [AccountNameInvalid](#accountnameinvalid)
* [Échec de l’autorisation](#authorization-failed)
* [BadRequest](#badrequest)
* [DeploymentFailed](#deploymentfailed)
* [DisallowedOperation](#disallowedoperation)
* [InvalidContentLink](#invalidcontentlink)
* [InvalidTemplate](#invalidtemplate)
* [MissingSubscriptionRegistration](#noregisteredproviderfound)
* [NotFound](#notfound)
* [NoRegisteredProviderFound](#noregisteredproviderfound)
* [OperationNotAllowed](#quotaexceeded)
* [ParentResourceNotFound](#parentresourcenotfound)
* [QuotaExceeded](#quotaexceeded)
* [RequestDisallowedByPolicy](#requestdisallowedbypolicy)
* [ResourceNotFound](#notfound)
* [SkuNotAvailable](#skunotavailable)
* [StorageAccountAlreadyExists](#storagenamenotunique)
* [StorageAccountAlreadyTaken](#storagenamenotunique)

## <a name="deploymentfailed"></a>DeploymentFailed

Ce code d’erreur indique une erreur de déploiement général, mais il n’est pas code d’erreur hello vous devez toostart résolution des problèmes. code d’erreur Hello réellement vous aide à résoudre le problème de hello est généralement un niveau en dessous de cette erreur. Par exemple, hello image suivante montre hello **RequestDisallowedByPolicy** code d’erreur qui se trouve sous l’erreur de déploiement hello.

![afficher le code d'erreur](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a>SkuNotAvailable

Lors du déploiement d’une ressource (en général, un ordinateur virtuel), hello message erreur et le code d’erreur suivant peut s’afficher :

```
Code: SkuNotAvailable
Message: hello requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy tooa different location.
```

Vous recevez cette erreur lorsque la ressource de hello référence (SKU) que vous avez sélectionné (par exemple, la taille de machine virtuelle) n’est pas disponible pour l’emplacement hello que vous avez sélectionné. tooresolve ce problème, vous devez toodetermine les références (SKU) disponibles dans une région. Vous pouvez utiliser PowerShell, hello portail ou un toofind d’opération REST références disponibles.

- Pour PowerShell, utilisez [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) et filtrez par emplacement. Vous devez disposer de hello dernière version de PowerShell pour cette commande.

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  résultats de Hello incluent une liste de références (SKU) pour l’emplacement de hello et des restrictions pour cette version de Windows.

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- toouse hello [portal](https://portal.azure.com), connectez-vous au portail de toohello et ajouter une ressource via une interface de hello. Lorsque vous définissez les valeurs hello, vous voyez hello références disponibles pour cette ressource. Vous n’avez pas besoin de déploiement de hello toocomplete.

    ![Références disponibles](./media/resource-manager-common-deployment-errors/view-sku.png)

- toouse hello API REST pour les machines virtuelles, envoyer hello demande :

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  Elle retourne des références (SKU) et les régions disponibles dans hello suivant le format :

  ```json
  {
    "value": [
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A0",
        "tier": "Standard",
        "size": "A0",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A1",
        "tier": "Standard",
        "size": "A1",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      ...
    ]
  }    
  ```

Si vous êtes toofind Impossible d’une référence (SKU) appropriée dans cette région ou une autre région qui répond aux besoins de votre entreprise, envoyer un [demande de référence (SKU)](https://aka.ms/skurestriction) tooAzure prise en charge.

## <a name="disallowedoperation"></a>DisallowedOperation

```
Code: DisallowedOperation
Message: hello current subscription type is not permitted tooperform operations on any provider 
namespace. Please use a different subscription.
```

Si vous recevez cette erreur, vous utilisez un abonnement qui n’est pas autorisée tooaccess tous les services Azure autres que Azure Active Directory. Vous pouvez avoir ce type d’abonnement quand vous avez besoin de portail classique de hello tooaccess toodeploy ressources ne sont pas autorisées. tooresolve ce problème, vous devez utiliser un abonnement qui contient des ressources de toodeploy d’autorisation.  

tooview vos abonnements disponibles avec PowerShell, utilisez :

```powershell
Get-AzureRmSubscription
```

Et tooset hello abonnement, utilisez :

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

tooview vos abonnements disponibles avec Azure CLI 2.0, utilisez :

```azurecli
az account list
```

Et tooset hello abonnement, utilisez :

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a>InvalidTemplate
Cette erreur peut résulter de différents types d’erreurs.

- Erreur de syntaxe

   Si vous recevez un message d’erreur qui indique la validation du modèle a échoué hello, vous avez peut-être un problème de syntaxe dans votre modèle.

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   Cette erreur est toomake facile, car les expressions de modèle peuvent être complexes. Par exemple, hello affectation de nom suivante pour un compte de stockage contient un jeu de crochets, trois fonctions, trois jeux de parenthèses, un seul jeu de guillemets simples et une propriété :

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   Si vous ne fournissez pas de syntaxe de correspondance hello, modèle de hello génère une valeur qui est différente de celle de votre intention.

   Lorsque vous recevez ce type d’erreur, lisez attentivement la syntaxe d’expression hello. Vous pouvez utiliser un éditeur JSON comme [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) ou [Visual Studio Code](resource-manager-vs-code.md), qui vous signale des erreurs de syntaxe.

- Longueurs de segments incorrectes

   Une autre erreur de modèle non valide se produit lorsque le nom de la ressource hello n’est pas au format correct de hello.

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'hello template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   Une ressource de niveau racine doit avoir un segment inférieur dans nom hello que dans le type de ressource hello. Chaque segment se différencie par une barre oblique. Dans l’exemple suivant de hello, type de hello possède deux segments et nom de hello a un seul segment, donc il est un **nom valide**.

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   Mais hello l’exemple suivant est **pas un nom valide** , car il a hello même nombre de segments en tant que type de hello.

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   Pour les ressources enfants, hello type et le nom ont hello même nombre de segments. Ce nombre de segments de sens, car le nom complet de hello et type pour les enfants hello inclut le type et le nom du parent hello. Par conséquent, nom complet de hello dispose toujours d’un segment à moins que complet de type hello.

  ```json
  "resources": [
      {
          "type": "Microsoft.KeyVault/vaults",
          "name": "contosokeyvault",
          ...
          "resources": [
              {
                  "type": "secrets",
                  "name": "appPassword",
                  ...
              }
          ]
      }
  ]
  ```

   Lors de l’obtention de segments hello droit peuvent être compliquées avec les types de gestionnaire de ressources qui sont appliquées sur des fournisseurs de ressources. Par exemple, l’application d’un site web de ressource verrou tooa nécessite un type avec quatre segments. Par conséquent, le nom de hello est trois segments :

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- La copie de l’index n’est pas prévue.

   Ce problème survient **InvalidTemplate** erreur lorsque vous avez appliqué hello **copie** partie tooa d’élément de modèle hello qui ne prend pas en charge cet élément. Vous pouvez uniquement appliquer le type de ressource hello copie élément tooa. Vous ne pouvez pas appliquer de propriété tooa de copie au sein d’un type de ressource. Par exemple, vous appliquez la machine virtuelle de tooa copie, mais ne peut pas appliquer les disques toohello du système d’exploitation pour un ordinateur virtuel. Dans certains cas, vous pouvez convertir un toocreate des ressources de parent enfant ressource tooa une boucle de copie. Pour plus d’informations sur l’utilisation de copy, voir [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).

- Le paramètre n’est pas valide.

   Si le modèle de hello spécifie les valeurs autorisées pour un paramètre, et vous fournir une valeur qui n’est pas un de ces valeurs, vous recevez un toohello similaire message l’erreur suivante :

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'hello provided value {parameter value}
  for hello template parameter {parameter name} is not valid. hello parameter value is not
  part of hello allowed values
  ``` 

   Vérifiez hello valeurs autorisées dans le modèle de hello et fournir une au cours du déploiement.

- Dépendance circulaire détectée

   Vous recevez cette erreur lorsque les ressources dépendent eux d’une manière qui empêche le déploiement hello de démarrer. À cause de l’effet combiné d’interdépendances, plusieurs ressources attendent d’autres ressources qui sont elles aussi en attente. Par exemple, la ressource 1 dépend de la ressource 3, la ressource 2 de la ressource 1 et la ressource 3 de la ressource 2. Vous pouvez généralement résoudre ce problème en supprimant les dépendances inutiles. 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a>NotFound et ResourceNotFound
Lorsque votre modèle inclut le nom hello d’une ressource qui ne peut pas être résolue, vous recevez une erreur similaire à :

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

Si vous essayez de hello toodeploy ressource dans le modèle de hello manquante, vérifiez si vous devez tooadd une dépendance. Resource Manager optimise le déploiement en créant des ressources en parallèle, quand cela est possible. Si une ressource doit être déployée après une autre ressource, vous devez toouse hello **dependsOn** élément dans votre toocreate modèle une dépendance sur hello autre ressource. Par exemple, lorsque vous déployez une application web, hello plan App Service doit exister. Si vous n’avez pas spécifié cette application web de hello dépend hello plan App Service, le Gestionnaire de ressources crée les deux ressources à hello même temps. Vous recevez une erreur indiquant que hello ressources du plan App Service est introuvable, car il n’existe pas encore lors de la tentative de tooset une propriété sur l’application web hello. Vous éviter cette erreur en définissant la dépendance de hello dans hello web app.

```json
{
  "apiVersion": "2015-08-01",
  "type": "Microsoft.Web/sites",
  "dependsOn": [
    "[variables('hostingPlanName')]"
  ],
  ...
}
```

Pour obtenir des conseils sur la résolution des erreurs de dépendance, consultez [Vérifier la séquence de déploiement](#check-deployment-sequence).

Cette erreur est également survenir lors de la ressource de hello existe dans un autre groupe de ressources que hello un déploiement sur. Dans ce cas, utilisez hello [fonction resourceId](resource-group-template-functions-resource.md#resourceid) nom qualifié complet de hello tooget de ressource de hello.

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

Si vous essayez de toouse hello [référence](resource-group-template-functions-resource.md#reference) ou [listKeys](resource-group-template-functions-resource.md#listkeys) fonctions avec une ressource qui ne peut pas être résolu, vous recevez hello l’erreur suivante :

```
Code=ResourceNotFound;
Message=hello Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

Recherchez une expression qui inclut hello **référence** (fonction). Vérifiez que les valeurs de paramètre hello sont corrects.

## <a name="parentresourcenotfound"></a>ParentResourceNotFound

Lorsqu’une ressource est une ressource de tooanother parent, ressource parente de hello doit exister avant de créer la ressource de hello enfant. Si elle n’existe pas encore, vous recevez hello l’erreur suivante :

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

nom Hello de ressource enfant de hello inclut nom hello du parent. Par exemple, une base de données SQL peut être définie de la manière suivante :

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

Mais, si vous ne spécifiez pas une dépendance sur la ressource parent de hello, ressource enfant de hello peut obtenir déployé avant le parent de hello. tooresolve cette erreur, inclure une dépendance.

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a>StorageAccountAlreadyExists et StorageAccountAlreadyTaken
Pour les comptes de stockage, vous devez fournir un nom pour la ressource hello qui est unique dans Azure. Si vous ne fournissez pas un nom unique, une erreur de ce type s’affiche :

```
Code=StorageAccountAlreadyTaken
Message=hello storage account named mystorage is already taken.
```

Vous pouvez créer un nom unique en concaténant votre convention d’affectation de noms avec un résultat de hello hello [uniqueString](resource-group-template-functions-string.md#uniquestring) (fonction).

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

Si vous déployez un compte de stockage avec hello de même nom qu’un compte de stockage existant dans votre abonnement, mais fournissent un autre emplacement, vous recevez une erreur indiquant compte de stockage hello existe déjà dans un autre emplacement. Supprimez le compte de stockage existant hello, ou fournissez hello même emplacement que hello compte de stockage existant.

## <a name="accountnameinvalid"></a>AccountNameInvalid
Vous consultez hello **AccountNameInvalid** lors de la tentative de toogive un stockage compte un nom qui inclut des caractères interdits. Ce nom doit comprendre entre 3 et 24 caractères, uniquement des lettres en minuscules et des nombres. Hello [uniqueString](resource-group-template-functions-string.md#uniquestring) fonction retourne 13 caractères. Si vous concaténez un préfixe toohello **uniqueString** entraîner, fournir un préfixe est de 11 caractères ou moins.

## <a name="badrequest"></a>BadRequest

L’état BadRequest peut survenir lorsque vous spécifiez une valeur de propriété non valide. Par exemple, si vous fournissez une valeur incorrecte de la référence (SKU) pour un compte de stockage, déploiement de hello échoue. toodetermine les valeurs valides pour la propriété, examinez hello [API REST](/rest/api) pour le type de ressource hello vous déployez.

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a>NoRegisteredProviderFound et MissingSubscriptionRegistration
Lors du déploiement de ressources, vous pouvez hello suivant le code d’erreur de réception et de message :

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

Vous pouvez sinon recevoir un message similaire indiquant :

```
Code: MissingSubscriptionRegistration
Message: hello subscription is not registered toouse namespace {resource-provider-namespace}
```

Ces erreurs apparaissent pour l’une des trois raisons suivantes :

1. fournisseur de ressources Hello n’a pas été inscrit pour votre abonnement
2. Version de l’API non prises en charge pour le type de ressource hello
3. Emplacement non pris en charge pour le type de ressource hello

message d’erreur Hello doit vous fournir des suggestions pour les emplacements de hello pris en charge et les versions d’API. Vous pouvez modifier votre tooone modèle Hello valeurs suggérées. La plupart des fournisseurs sont inscrits automatiquement par hello Azure portal ou hello une interface de ligne que vous utilisez, mais pas toutes. Si vous n’avez pas utilisé un fournisseur de ressources particulier avant, vous devrez peut-être tooregister ce fournisseur. Vous pouvez en savoir plus sur les fournisseurs de ressources via PowerShell ou l’interface de ligne de commande Azure.

**Portail**

Vous pouvez voir l’état de l’inscription hello et enregistrer un espace de noms du fournisseur de ressources via le portail de hello.

1. Sur votre abonnement, sélectionnez **Fournisseurs de ressources**.

   ![sélectionner Fournisseurs de ressources](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. Examinez la liste hello des fournisseurs de ressources et si nécessaire, sélectionnez hello **inscrire** fournisseur de ressources de lien tooregister hello du type de hello vous essayez de toodeploy.

   ![répertorier les fournisseurs de ressources](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

**PowerShell**

toosee votre statut d’enregistrement, utilisez **Get-AzureRmResourceProvider**.

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

tooregister un fournisseur, utilisez **AzureRmResourceProvider de Registre** et fournissez hello nom de fournisseur de ressources hello vous souhaitez tooregister.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

tooget les emplacements de hello pris en charge pour un type particulier de ressource, utilisez :

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

tooget hello pris en charge les versions d’API pour un type particulier de ressource, utilisez :

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

**Interface de ligne de commande Azure**

toosee si le fournisseur de hello est inscrit, utilisez hello `azure provider list` commande.

```azurecli
az provider list
```

tooregister un fournisseur de ressources, utilisez hello `azure provider register` de commandes et spécifiez hello *espace de noms* tooregister.

```azurecli
az provider register --namespace Microsoft.Cdn
```

emplacements de hello pris en charge toosee et versions d’API pour un type de ressource, utilisez :

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a>QuotaExceeded et OperationNotAllowed
Vous pouvez rencontrer des problèmes quand un déploiement dépasse un quota qui peut concerner entre autres les groupes de ressources, les abonnements ou les comptes. Par exemple, votre abonnement est peut-être configuré de nombre de hello toolimit de cœurs pour une région. Si vous essayez de toodeploy une machine virtuelle avec davantage de cœurs que hello Montant admis, vous recevez une erreur indiquant que hello quota a été dépassé.
Pour obtenir des informations complètes sur les quotas, consultez [Abonnement Azure et limites, quotas et contraintes du service](../azure-subscription-service-limits.md).

tooexamine les quotas de votre abonnement pour cœurs, vous pouvez utiliser hello `azure vm list-usage` commande hello CLI d’Azure. Bonjour à l’exemple suivant illustre ce quota de cœurs hello pour un compte d’évaluation gratuite est 4 :

```azurecli
az vm list-usage --location "South Central US"
```

Résultat :

```azurecli
[
  {
    "currentValue": 0,
    "limit": 2000,
    "name": {
      "localizedValue": "Availability Sets",
      "value": "availabilitySets"
    }
  },
  ...
]
```

Si vous déployez un modèle qui crée le plus de quatre cœurs dans la région ouest des États-Unis hello, vous obtenez une erreur de déploiement qui ressemble à :

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

Dans PowerShell, vous pouvez également utiliser hello **Get-AzureRmVMUsage** applet de commande.

```powershell
Get-AzureRmVMUsage
```

Résultat :

```powershell
...
CurrentValue : 0
Limit        : 4
Name         : {
                 "value": "cores",
                 "localizedValue": "Total Regional Cores"
               }
Unit         : null
...
```

Dans ces cas, vous devez accéder toohello portail et votre quota pour la région de hello dans lequel vous souhaitez toodeploy un tooraise de problème de prise en charge du fichier.

> [!NOTE]
> N’oubliez pas que pour les groupes de ressources, le quota de hello est pour chacune des régions, pas pour tout abonnement de hello. Si vous avez besoin de 30 cœurs toodeploy ouest des États-Unis, vous avez tooask pour 30 cœurs de gestionnaire de ressources dans l’ouest des États-Unis. Si vous avez besoin de cœurs de 30 toodeploy dans un des hello régions toowhich vous avez accès, vous devez demander de 30 cœurs de gestionnaire de ressources dans toutes les régions.
>
>

## <a name="invalidcontentlink"></a>InvalidContentLink
Lorsque vous recevez le message d’erreur hello :

```
Code=InvalidContentLink
Message=Unable toodownload deployment content from ...
```

Vous avez probablement tenté modèle imbriqué toolink tooa qui n’est pas disponible. Vérifiez hello URI que vous avez fourni pour les modèles imbriqués hello. Si le modèle de hello existe dans un compte de stockage, vérifiez que hello URI est accessible. Vous devrez peut-être toopass un jeton SAP. Pour plus d’informations, consultez [Utilisation de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).

## <a name="requestdisallowedbypolicy"></a>RequestDisallowedByPolicy
Vous recevez cette erreur lorsque votre abonnement inclut une stratégie de ressources qui empêche une action que vous essayez de tooperform durant le déploiement. Dans le message d’erreur hello, recherchez l’identificateur de stratégie hello.

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

Dans **PowerShell**, fournir cet identificateur de stratégie en tant que hello **Id** détails du paramètre tooretrieve sur la stratégie hello qui a bloqué votre déploiement.

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

Dans **CLI d’Azure**, fournir le nom hello de définition de stratégie hello :

```azurecli
az policy definition show --name regionPolicyAssignment
```

Pour plus d’informations, consultez hello suivant des articles :

- [Erreur RequestDisallowedByPolicy](resource-manager-policy-requestdisallowedbypolicy-error.md)
- [Utiliser les ressources de la stratégie toomanage et contrôler l’accès](resource-manager-policy.md).

## <a name="authorization-failed"></a>Échec de l’autorisation
Vous pouvez recevoir une erreur lors du déploiement car hello compte ou le service principal d’essayer de ressources de hello toodeploy n’a pas accès tooperform ces actions. Azure Active Directory permet de vous ou votre toocontrol administrateur les identités peuvent accéder à quelles ressources avec un plus grand degré de précision. Par exemple, si le rôle de lecteur toohello est affecté à votre compte, vous n’êtes pas en mesure de toocreate ressources. Dans ce cas, vous voyez un message d’erreur indiquant que l’autorisation a échoué.

Pour plus d’informations sur le contrôle d’accès en fonction du rôle, consultez la rubrique [Contrôle d’accès en fonction du rôle d’Azure](../active-directory/role-based-access-control-configure.md).


## <a name="next-steps"></a>Étapes suivantes
* toolearn sur l’audit des actions, consultez [auditer les opérations effectuées avec le Gestionnaire de ressources](resource-group-audit.md).
* toolearn sur les erreurs de hello toodetermine actions pendant le déploiement, consultez [afficher les opérations de déploiement](resource-manager-deployment-operations.md).
