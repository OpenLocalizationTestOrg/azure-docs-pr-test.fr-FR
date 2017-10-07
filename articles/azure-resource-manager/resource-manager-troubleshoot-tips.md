---
title: "erreurs de déploiement Azure aaaUnderstand | Documents Microsoft"
description: "Décrit comment toolearn sur les erreurs de déploiement Azure."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "Erreur de déploiement, déploiement d’azure, déployez tooazure"
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: tomfitz
ms.openlocfilehash: a335e121e9b908a763374907e34b1f6e823d6e96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-deployment-errors"></a>Comprendre les erreurs de déploiement Azure
Cette rubrique décrit les erreurs de déploiement et vous explique comment obtenir plus d’informations sur une erreur. Pour des erreurs de déploiement toocommon résolutions, consultez [résoudre les erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).

## <a name="two-types-of-errors"></a>Deux types d’erreur
Il existe deux types d’erreurs que vous pouvez rencontrer :

* des erreurs de validation
* des erreurs de déploiement

Hello suivant image montre le journal d’activité hello pour un abonnement. Deux déploiements sont représentés. Dans un déploiement, le modèle de hello validation a échoué (**Validate**) et ne pas été effectuée. Dans hello autre déploiement, modèle de hello ont réussi la validation, mais a échoué lors de la création de ressources de hello (**écrire des déploiements**). 

![afficher le code d'erreur](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

Les erreurs de validation sont liées à des scénarios pouvant être identifiés avant le déploiement. Elles incluent des erreurs de syntaxe dans votre modèle, ou lors de la tentative ressources toodeploy dépassent vos quotas d’abonnement. Erreurs de déploiement sont dues aux conditions qui se produisent pendant le processus de déploiement hello. Ils comprennent la tentative de tooaccess une ressource qui est déployée en parallèle.

Les deux types de retour d’erreurs que vous utilisez tootroubleshoot hello déploiement un code d’erreur. Les deux types d’erreurs s’affichent dans hello [le journal d’activité](resource-group-audit.md). Toutefois, les erreurs de validation n’apparaissent pas dans l’historique de votre déploiement, car le déploiement de hello jamais démarré.

## <a name="determine-error-code"></a>Déterminer le code d’erreur

Vous pouvez en savoir plus sur une erreur en examinant de message d’erreur hello et code d’erreur hello. Hello [résoudre les erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md) article répertorie les résolutions par code d’erreur. Cette rubrique montre comment toouse hello le code d’erreur hello toodiscover portail Azure.

### <a name="validation-errors"></a>Erreurs de validation

Lors du déploiement via le portail de hello, vous voyez une erreur de validation après avoir soumis vos valeurs.

![afficher l’erreur de validation dans le portail](./media/resource-manager-troubleshoot-tips/validation-error.png)

Sélectionnez le message de type hello pour plus de détails. Bonjour suivant l’image, vous voyez un **InvalidTemplateDeployment** d’erreur et un message qui indique une stratégie de déploiement bloqué.

![afficher les détails de validation](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a>Erreurs de déploiement

Lors de l’opération de hello passe la validation, mais échoue pendant le déploiement, vous voyez erreur hello dans les notifications de hello. Sélectionnez hello notification.

![erreur de notification](./media/resource-manager-troubleshoot-tips/notification.png)

Vous voyez plus d’informations sur le déploiement de hello. Sélectionnez hello option toofind plus d’informations sur l’erreur de hello.

![échec du déploiement](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

Vous consultez codes d’erreur et le message d’erreur hello. Notez qu’il y a deux codes d’erreur. Hello premier code d’erreur (**DeploymentFailed**) est une erreur générale qui ne fournit pas de hello détails que vous avez besoin d’erreur de hello toosolve. Hello deuxième code d’erreur (**StorageAccountNotFound**) fournit des détails hello vous avez besoin. 

![détails de l’erreur](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a>Activer l’enregistrement du débogage
Vous devez parfois plus d’informations sur toodiscover de demande et de réponse hello cause du problème. Avec PowerShell ou l’interface de ligne de commande Azure, vous pouvez demander la journalisation d’informations supplémentaires lors d’un déploiement.

- PowerShell

   Dans PowerShell, définissez hello **DeploymentDebugLogLevel** tooAll de paramètre, le ResponseContent ou RequestContent.

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   Examinez le contenu de demande de hello avec hello suivant l’applet de commande :

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   Ou bien, hello du contenu à l’aide de la réponse :

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   Ces informations peuvent vous aider à déterminer si une valeur dans le modèle de hello est incorrectement définie.

- Interface de ligne de commande Azure

   Examiner les opérations de déploiement hello avec hello de commande suivante :

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- Modèle imbriqué

   toolog les informations de débogage pour un modèle imbriqué, utilisez hello **debugSetting** élément.

  ```json
  {
      "apiVersion": "2016-09-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
          "mode": "Incremental",
          "templateLink": {
              "uri": "{template-uri}",
              "contentVersion": "1.0.0.0"
          },
          "debugSetting": {
             "detailLevel": "requestContent, responseContent"
          }
      }
  }
  ```


## <a name="create-a-troubleshooting-template"></a>Création d’un modèle de résolution des problèmes
Dans certains cas, hello tootroubleshoot de façon plus simple votre modèle est tootest des parties de celui-ci. Vous pouvez créer un modèle simplifié qui vous permet de toofocus sur la partie hello que vous pensez être provoque l’erreur de hello. Par exemple, supposons que vous recevez une erreur lorsque vous référencez une ressource. Au lieu de traiter un modèle complet, créez un modèle qui retourne une partie hello qui peut être à l’origine de votre problème. Il peut vous aider à déterminer si vous passez dans les paramètres appropriés de hello, à l’aide des fonctions de modèle correctement, et obtention de la ressource de hello souhaitées.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageName": {
        "type": "string"
    },
    "storageResourceGroup": {
        "type": "string"
    }
  },
  "variables": {},
  "resources": [],
  "outputs": {
    "exampleOutput": {
        "value": "[reference(resourceId(parameters('storageResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('storageName')), '2016-05-01')]",
        "type" : "object"
    }
  }
}
```

Ou bien, supposons que vous rencontrez des erreurs de déploiement que vous pensez être liés tooincorrectly définir des dépendances. vous pouvez tester votre modèle en le divisant en modèles plus simples. Commencez par créer un modèle déployant une seule ressource (comme un serveur SQL Server). Lorsque vous êtes sûr que cette ressource est correctement définie, ajoutez une ressource qui en dépend (par exemple une base de données SQL). Une fois ces deux ressources correctement définies, ajoutez les autres ressources dépendantes (telles que les stratégies d’audit). Entre chaque déploiement de test, supprimez hello groupe toomake que vous correctement test hello des dépendances de ressource. 

## <a name="check-deployment-sequence"></a>Vérifier la séquence de déploiement

De nombreuses erreurs de déploiement se produisent lorsque des ressources sont déployées selon une séquence inattendue. Ces erreurs surviennent lorsque les dépendances ne sont pas définies correctement. Lorsqu’il manque une dépendance nécessaire, une ressource tentatives toouse qu'une valeur pour une autre ressource mais hello autres n’existe pas encore. Vous obtenez une erreur indiquant qu’une ressource est introuvable. Si vous rencontrez ce type d’erreur par intermittence, car le temps de déploiement hello pour chaque ressource peut varier. Par exemple, votre premier toodeploy de tentative de vos ressources réussit car une ressource requise se termine de façon aléatoire dans le temps. Toutefois, votre deuxième tentative échoue car hello requis de ressource ne s’est pas terminée dans le temps. 

Toutefois, vous souhaitez que les dépendances de paramètre tooavoid qui ne sont pas nécessaires. Lorsque vous avez des dépendances inutiles, vous prolonger la durée hello du déploiement de hello en empêchant les ressources qui ne sont pas dépendants sur eux d’être déployé en parallèle. En outre, vous pouvez créer des dépendances circulaires qui bloquent le déploiement de hello. Hello [référence](resource-group-template-functions-resource.md#reference) fonction crée une dépendance implicite sur la ressource hello référencée lorsque cette ressource est déployée dans hello même modèle. Par conséquent, vous pouvez avoir des dépendances plus que les dépendances de hello spécifiés dans hello **dependsOn** propriété. Hello [resourceId](resource-group-template-functions-resource.md#resourceid) fonction ne pas créer une relation implicite ou valider l’existence de la ressource de hello.

Lorsque vous rencontrez des problèmes de dépendance, vous devez toogain idée commande hello de déploiement de ressources. ordre de hello tooview d’opérations de déploiement :

1. Sélectionnez l’historique de déploiement hello pour votre groupe de ressources.

   ![sélectionner l’historique de déploiement](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. Sélectionnez un déploiement à partir de l’historique de hello, puis sélectionnez **événements**.

   ![sélectionner les événements de déploiement](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. Examiner la séquence de hello d’événements pour chaque ressource. État de toohello attention de chaque opération de paie. Par exemple, hello image suivante montre trois comptes de stockage déploiement en parallèle. Notez que hello trois comptes de stockage sont démarrés à hello même temps.

   ![déploiement en parallèle](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   image de Hello suivant montre trois comptes de stockage qui ne sont pas déployés en parallèle. compte de stockage deuxième Hello varie selon le premier compte de stockage hello et compte de stockage tiers hello dépend de la deuxième compte de stockage hello. Par conséquent, premier compte de stockage hello est démarré, accepté et s’est terminée avant hello est redémarrée.

   ![déploiement séquentiel](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

Même pour les scénarios plus complexes, vous pouvez utiliser hello même technique toodiscover lorsque le déploiement est démarré et s’est terminée pour chaque ressource. Examinez votre toosee d’événements de déploiement si la séquence de hello est différente de celle attendue. Dans ce cas, réévaluez les dépendances hello pour cette ressource.

Resource Manager identifie les dépendances circulaires lors de la validation du modèle. Il renvoie un message d’erreur indiquant spécifiquement qu’il existe une dépendance circulaire. toosolve une dépendance circulaire :

1. Dans votre modèle, de trouver la ressource hello identifié une dépendance circulaire hello. 
2. Pour cette ressource, examinez hello **dependsOn** propriété et toutes les utilisations de hello **référence** toosee les ressources dont il dépend de la fonction. 
3. Examinez ces toosee de ressources que les ressources dont ils dépendent. Suivre les dépendances de hello jusqu'à ce que vous remarquez une ressource dont dépend la ressource d’origine de hello.
5. Pour les ressources de hello impliquées dans une dépendance circulaire hello, examinez attentivement toutes les utilisations de hello **dependsOn** propriété tooidentify toutes les dépendances qui ne sont pas nécessaires. Supprimer ces dépendances. Si vous n’êtes pas certain qu’une dépendance soit nécessaire, essayez de la supprimer. 
6. Redéployez le modèle de hello.

Suppression des valeurs de hello **dependsOn** propriété peut provoquer des erreurs lorsque vous déployez le modèle de hello. Si vous rencontrez une erreur, ajoutez la dépendance hello dans le modèle de hello. 

Si cette approche ne résout pas une dépendance circulaire hello, déplacez la partie de votre logique de déploiement dans les ressources enfants (par exemple, des extensions ou des paramètres de configuration). Configurer les toodeploy de ressources enfant après ressources hello impliquées dans une dépendance circulaire hello. Par exemple, supposons que vous déployez deux machines virtuelles, mais vous devez définir des propriétés sur chacun d’eux qui font référence toohello autres. Vous pouvez les déployer dans hello suivant l’ordre :

1. Machine virtuelle 1
2. Machine virtuelle 2
3. L’extension sur la machine virtuelle 1 dépend des machines virtuelles 1 et 2. extension de Hello définit des valeurs sur vm1 qu’il obtient à partir de l’ordinateur virtuel 2.
4. L’extension sur la machine virtuelle 2 dépend des machines virtuelles 1 et 2. extension de Hello définit des valeurs sur vm2 qu’il obtient de vm1.

Hello même approche fonctionne pour les applications de Service d’applications. Envisagez de passer des valeurs de configuration dans une ressource enfant de ressource d’application hello. Vous pouvez déployer des applications web deux Bonjour suivant l’ordre :

1. Application web 1
2. Application web 2
3. La configuration de l’application web 1 dépend des applications web 1 et 2. Elle contient des paramètres d’application avec les valeurs de l’application web 2.
4. La configuration de l’application web 2 dépend des applications web 1 et 2. Elle contient des paramètres d’application avec les valeurs de l’application web 1.


## <a name="next-steps"></a>Étapes suivantes
* Pour des erreurs de déploiement toocommon résolutions, consultez [résoudre les erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).
* toolearn sur l’audit des actions, consultez [auditer les opérations effectuées avec le Gestionnaire de ressources](resource-group-audit.md).
* toolearn sur les erreurs de hello toodetermine actions pendant le déploiement, consultez [afficher les opérations de déploiement](resource-manager-deployment-operations.md).
