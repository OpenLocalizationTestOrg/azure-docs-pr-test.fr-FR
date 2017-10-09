---
title: "ressources aaaManage avec hello CLI d’Azure | Documents Microsoft"
description: Utilisez hello Azure Interface de ligne de commande (CLI) toomanage Azure ressources et les groupes
editor: 
manager: timlt
documentationcenter: 
author: tfitzmac
services: azure-resource-manager
ms.assetid: bb0af466-4f65-4559-ac3a-43985fa096ff
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: tomfitz
ms.openlocfilehash: 3df70e123d14d3bbf2648c71970bac1db4afc025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cli-toomanage-azure-resources-and-resource-groups"></a>Utilisez hello CLI d’Azure toomanage Azure ressources et groupes de ressources
> [!div class="op_single_selector"]
> * [Portail](resource-group-portal.md) 
> * [Interface de ligne de commande Azure](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [API REST](resource-manager-rest-api.md)
> 
> 

Bonjour Azure Interface de ligne (Azure) est un ou plusieurs outils, vous pouvez utiliser toodeploy et gérer les ressources avec le Gestionnaire de ressources. Cet article présente toomanage façons courantes Azure ressources et groupes de ressources à l’aide de hello CLI d’Azure en mode de gestionnaire de ressources. Pour plus d’informations sur l’utilisation des ressources de toodeploy hello CLI, consultez [déployer des ressources avec des modèles de gestionnaire de ressources et CLI d’Azure](resource-group-template-deploy-cli.md). Pour plus d’informations sur le Gestionnaire de ressources et les ressources Azure, visitez hello [vue d’ensemble du Gestionnaire de ressources Azure](resource-group-overview.md).

> [!NOTE]
> toomanage Azure ressources avec hello CLI d’Azure, vous devez trop[installer hello CLI d’Azure](../cli-install-nodejs.md), et [connecter tooAzure](../xplat-cli-connect.md) à l’aide de hello `azure login` commande. Vérifiez que hello est CLI est en mode de gestionnaire de ressources (exécutez `azure config mode arm`). Si vous avez effectué ces opérations, vous êtes prêt toogo.
> 
> 

## <a name="get-resource-groups-and-resources"></a>Obtenir des ressources et des groupes de ressources
### <a name="resource-groups"></a>Groupes de ressources
tooget une liste de tous les groupes de ressources dans votre abonnement et leurs emplacements, exécutez la commande.

    azure group list


### <a name="resources"></a>Ressources
 nom de toutes les ressources dans un groupe, tel que celui avec toolist *testRG*, utilisez hello de commande suivante :

    azure resource list testRG

tooview une ressource individuelle dans le groupe de hello, par exemple un ordinateur virtuel nommé *MyUbuntuVM*, utilisez une commande semblable à hello suivante :

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

Hello d’avis **Microsoft.Compute/virtualMachines** paramètre. Ce paramètre indique le type hello de ressource hello que vous demandent des informations.

> [!NOTE]
> Lorsque vous utilisez hello **ressource azure** commandes autres que hello **liste** de commande, vous devez spécifier la version hello API de ressource de hello avec hello **-o** paramètre. Si vous ne savez pas sur la version de l’API hello, consultez le fichier de modèle hello et trouver le champ d’apiVersion hello pour la ressource de hello. Pour plus d’informations sur les versions d’API dans Gestionnaire des ressources, consultez [Fournisseurs et types de ressources](resource-manager-supported-services.md).
> 
> 

Lors de l’affichage des détails sur une ressource, il est souvent utile toouse hello `--json` paramètre. Ce paramètre rend hello de sortie plus lisible, car certaines valeurs sont des structures imbriquées ou des collections. exemple Hello illustre le retour de résultats hello Hello **afficher** en tant que document JSON.

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> Si vous le souhaitez, enregistrer hello toofile de données JSON à l’aide de hello &gt; fichier tooa de caractère toodirect hello sortie. Par exemple :
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a>Balises
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a>Gestion des ressources
tooadd une ressource telle qu’un groupe de ressources tooa du compte de stockage, exécutez une commande semblable à :

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

En outre toospecifying hello version de l’API de ressource de hello avec hello **-o** paramètre, utilisez hello **-p** paramètre toopass un format JSON en chaîne tout ou des propriétés supplémentaires.

toodelete une ressource existante comme une ressource d’ordinateur virtuel, utilisez une commande semblable à hello suivante :

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

toomove existant groupe de ressources tooanother ressources ou d’un abonnement, utilisez hello **du déplacement des Ressources azure** commande. Hello suivant montre l’exemple de comment toomove un Cache Redis tooa nouveau groupe de ressources. Bonjour **-i** paramètre, fournir une liste séparée par des virgules de toomove d’id de ressources hello.

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-tooresources"></a>Contrôle l’accès tooresources
Vous pouvez utiliser hello CLI d’Azure toocreate et gérer les stratégies toocontrol accès tooAzure ressources. Pour plus d’informations sur les définitions de stratégie et d’assignation tooresources de stratégies, consultez [utiliser les ressources de la stratégie toomanage et contrôler l’accès](resource-manager-policy.md).

Par exemple, définir hello suivant stratégie toodeny toutes les demandes où emplacement n’est pas ouest des États-Unis ou Amérique du Nord et enregistrez-le policy.json de fichier de définition de stratégie toohello :

    {
    "if" : {
        "not" : {
        "field" : "location",
        "in" : ["westus" ,  "northcentralus"]
        }
    },
    "then" : {
        "effect" : "deny"
    }
    }

Puis exécutez hello **création d’une définition de stratégie** commande :

    azure policy definition create MyPolicy -p c:\temp\policy.json

Cette commande montre suivant toohello similaire de sortie :

    + Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy

    data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny

 tooassign une stratégie au niveau de la portée de hello souhaitée, utilisez hello **PolicyDefinitionId** retourné à partir de la commande précédente hello. Dans l’exemple suivant de hello, cette étendue est abonnement de hello, mais vous pouvez définir l’étendue tooresource groupes ou des ressources individuelles :

    azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/

Vous pouvez obtenir, modifier ou supprimer des définitions de stratégie à l’aide de hello **afficher de définition de stratégie**, **jeu de définition de stratégie**, et **supprimer de la définition de la stratégie** commandes.

De même, vous pouvez obtenir, modifier ou supprimer des attributions de stratégies à l’aide de hello **afficher d’attribution de stratégie**, **jeu d’attribution de stratégie**, et **supprimer de l’affectation de stratégie** commandes .

## <a name="export-a-resource-group-as-a-template"></a>Exporter un groupe de ressources en tant que modèle
Pour un groupe de ressources existant, vous pouvez afficher le modèle de gestionnaire de ressources hello pour le groupe de ressources hello. Exportation de modèle de hello offre deux avantages :

1. Vous pouvez automatiser facilement les futurs déploiements de solution de hello car toute infrastructure hello est défini dans le modèle de hello.
2. Vous pouvez vous familiariser avec la syntaxe de modèle en examinant hello JSON qui représente votre solution.

À l’aide de hello CLI d’Azure, vous pouvez exporter un modèle qui représente l’état actuel de hello de votre groupe de ressources, ou téléchargez le modèle hello qui a été utilisé pour un déploiement particulier.

* **Exporter le modèle hello pour un groupe de ressources** -cela est utile lorsque le groupe de ressources tooa de modifications, et que vous avez besoin de tooretrieve hello représentation JSON de son état actuel. Toutefois, le modèle généré de hello contient uniquement un nombre minimal de paramètres et aucune variable. La plupart des valeurs hello dans le modèle de hello est codés en dur. Avant de déployer le modèle de hello généré, vous souhaiterez tooconvert plusieurs des valeurs de hello dans les paramètres afin que vous pouvez personnaliser le déploiement hello pour différents environnements.
  
    modèle de hello tooexport pour un groupe tooa local répertoire des ressources, exécutez hello `azure group export` commande comme indiqué dans hello l’exemple suivant. (Indiquez un répertoire local adapté à l’environnement de votre système d’exploitation.)
  
        azure group export testRG ~/azure/templates/
* **Télécharger le modèle hello pour un déploiement particulier** --Ceci est utile lorsque vous avez besoin de modèle réel tooview hello qui a été utilisé toodeploy ressources. modèle de Hello inclut tous les paramètres et les variables définies pour le déploiement d’origine de hello. Toutefois, si une personne de votre organisation a le groupe de ressources toohello modifications en dehors de la définition de hello dans le modèle de hello, ce modèle ne représente pas état actuel de hello hello du groupe de ressources.
  
    modèle de hello toodownload utilisé pour un répertoire tooa local de déploiement particulier, exécutez hello `azure group deployment template download` commande. Par exemple :
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> L’exportation de modèle est en version préliminaire. Elle n’est pas encore prise en charge par tous les types de ressources. Lors de la tentative de tooexport un modèle, vous pouvez voir une erreur indiquant que certaines ressources n’ont pas été exportés. Le cas échéant, définissez ces ressources manuellement dans votre modèle après l’avoir téléchargé.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* tooget les détails des opérations de déploiement et de résoudre les erreurs de déploiement avec hello CLI d’Azure, consultez [afficher les opérations de déploiement](resource-manager-deployment-operations.md).
* Si vous souhaitez toouse hello CLI tooset d’une application ou tooaccess des ressources de script, consultez [CLI d’Azure utilisation toocreate un principal de service tooaccess ressources](resource-group-authenticate-service-principal-cli.md).
* Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).

