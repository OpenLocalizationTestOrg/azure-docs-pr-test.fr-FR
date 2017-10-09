---
title: "modèle de gestionnaire de ressources Azure aaaExport | Documents Microsoft"
description: "Utilisez Gestion de ressources Azure tooexport un modèle à partir d’un groupe de ressources existant."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 5f5ca940-eef8-4125-b6a0-f44ba04ab5ab
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/06/2017
ms.author: tomfitz
ms.openlocfilehash: 94daa4812da2fec705044ca31c8e74e6d59bd53f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a>Exporter un modèle Azure Resource Manager à partir de ressources existantes
Dans cet article, vous apprendrez comment tooexport un modèle de gestionnaire de ressources à partir de ressources existants dans votre abonnement. Vous pouvez utiliser ce toogain modèle généré une meilleure compréhension de la syntaxe de modèle.

Il existe deux façons tooexport un modèle :

* Vous pouvez exporter hello **modèle réel utilisé pour le déploiement**. modèle exporté du Hello inclut toutes les variables et les paramètres de hello exactement comme ils apparaissent dans le modèle d’origine de hello. Cette approche est utile lorsque vous avez déployé des ressources via le portail de hello et souhaitez toosee hello modèle toocreate ces ressources. Ce modèle est facilement utilisable. 
* Vous pouvez exporter un **généré le modèle qui représente l’état actuel de hello hello du groupe de ressources**. modèle exporté du Hello n’est pas basé sur un modèle que vous avez utilisé pour le déploiement. Au lieu de cela, il crée un modèle qui est un instantané hello du groupe de ressources. modèle exporté du Hello possède de nombreuses valeurs codées en dur et probablement pas autant de paramètres que vous définissez généralement. Cette approche est utile lorsque vous avez modifié le groupe de ressources hello après le déploiement. Ce modèle doit généralement être modifié avant d’être utilisable.

Cette rubrique montre les deux approches via le portail de hello.

## <a name="deploy-resources"></a>Déployer des ressources
Commençons par tooAzure de ressources que vous pouvez utiliser pour l’exportation en tant que modèle de déploiement. Si vous avez déjà un groupe de ressources dans votre abonnement que vous souhaitez tooexport tooa modèle, vous pouvez ignorer cette section. reste Hello de cet article suppose que vous avez déployé l’application hello web et les solutions de base de données SQL présentées dans cette section. Si vous utilisez une autre solution, votre expérience peut être un peu différente, mais les étapes hello tooexport un modèle sont hello même. 

1. Bonjour [portail Azure](https://portal.azure.com), sélectionnez **nouveau**.
   
      ![sélectionner nouveau](./media/resource-manager-export-template/new.png)
2. Recherchez **web application + SQL** et sélectionnez-le dans les options disponibles hello.
   
      ![recherche application web et SQL](./media/resource-manager-export-template/webapp-sql.png)

3. Sélectionnez **Créer**.

      ![sélectionner créer](./media/resource-manager-export-template/create.png)

4. Indiquez les valeurs de hello requis pour hello web app et de la base de données SQL. Sélectionnez **Créer**.

      ![fournir une valeur web et SQL](./media/resource-manager-export-template/provide-web-values.png)

déploiement de Hello peut prendre une minute. Après déploiement de hello, votre abonnement contient des solutions de hello.

## <a name="view-template-from-deployment-history"></a>Voir un modèle à partir de l’historique de déploiement
1. Accédez à panneau de groupe de ressources toohello pour votre nouveau groupe de ressources. Notez que ce panneau hello affiche le résultat de hello du dernier déploiement de hello. Sélectionnez ce lien.
   
      ![panneau du groupe de ressources](./media/resource-manager-export-template/select-deployment.png)
2. Vous voyez un historique des déploiements pour le groupe de hello. Dans ce cas, les lames hello répertorie probablement un seul déploiement. Sélectionnez ce déploiement.
   
     ![dernier déploiement](./media/resource-manager-export-template/select-history.png)
3. Panneau de Hello affiche un résumé du déploiement de hello. Hello résumé inclut les valeurs hello que vous avez fourni pour les paramètres état hello du déploiement de hello et ses opérations. modèle hello toosee que vous avez utilisé pour le déploiement de hello, sélectionnez **modèle d’affichage de**.
   
     ![afficher le résumé du déploiement](./media/resource-manager-export-template/view-template.png)
4. Le Gestionnaire de ressources récupère hello suivant sept fichiers pour vous :
   
   1. **Modèle** -modèle hello qui définit l’infrastructure hello pour votre solution. Lorsque vous avez créé le compte de stockage hello via le portail de hello, Gestionnaire de ressources utilisé un toodeploy modèle il et enregistré ce modèle pour référence ultérieure.
   2. **Paramètres** -un fichier de paramètres que vous pouvez utiliser toopass dans les valeurs durant le déploiement. Il contient des valeurs hello que vous avez fourni pendant le déploiement de première hello. Vous pouvez modifier ces valeurs lorsque vous redéployez le modèle de hello.
   3. **CLI** -fichier de script Azure une interface de ligne de commande (CLI) que vous pouvez utiliser le modèle de hello toodeploy.
   3. **CLI 2.0** -fichier de script Azure une interface de ligne de commande (CLI) que vous pouvez utiliser le modèle de hello toodeploy.
   4. **PowerShell** -fichier de script d’un Azure PowerShell que vous pouvez utiliser le modèle de hello toodeploy.
   5. **.NET** -classe A .NET que vous pouvez utiliser le modèle de hello toodeploy.
   6. **Ruby** -classe A Ruby que vous pouvez utiliser le modèle de hello toodeploy.
      
      fichiers de Hello sont disponibles via des liens entre les lames hello. Par défaut, panneau de hello affiche le modèle de hello.
      
       ![Afficher le modèle](./media/resource-manager-export-template/see-template.png)
      
Ce modèle est le modèle réel de hello utilisé toocreate votre application web et la base de données SQL. Notez qu’il contient des paramètres qui vous permettent de tooprovide des valeurs différentes au cours du déploiement. toolearn en savoir plus sur la structure de hello d’un modèle, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).

## <a name="export-hello-template-from-resource-group"></a>Exporter le modèle de hello du groupe de ressources
Si vous avez manuellement modifié vos ressources ou l’ajout de ressources dans plusieurs déploiements, la récupération d’un modèle à partir de l’historique de déploiement hello ne reflète pas état actuel de hello hello du groupe de ressources. Cette section vous montre comment tooexport un modèle qui reflète hello état actuel du groupe de ressources hello. 

> [!NOTE]
> Vous ne pouvez pas exporter un modèle pour un groupe de ressources qui contient plus de 200 ressources.
> 
> 

1. modèle de hello tooview pour un groupe de ressources, sélectionnez **script d’automatisation**.
   
      ![exporter un groupe de ressources](./media/resource-manager-export-template/select-automation.png)
   
     Le Gestionnaire de ressources prend la valeur hello ressources hello groupe de ressources et génère un modèle pour ces ressources. Pas tous les types de ressources prend en charge la fonction de modèle d’exportation hello. Vous pouvez voir un message d’erreur indiquant qu’il existe un problème avec l’exportation de hello. Vous apprendrez comment toohandle ces problèmes dans hello [correctif exportation problèmes](#fix-export-issues) section.
2. Vous consultez à nouveau hello six fichiers que vous pouvez utiliser la solution de hello tooredeploy. Toutefois, ce modèle de temps de hello est légèrement différent. Notez que le modèle hello généré contient moins de paramètres que le modèle hello dans la section précédente. En outre, nombre de valeurs hello (par exemple, l’emplacement et les valeurs de SKU) sont codés en dur dans ce modèle, plutôt que d’accepter une valeur de paramètre. Avant de réutiliser ce modèle, vous pourriez tooedit hello modèle toomake améliore l’utilisation des paramètres. 
   
3. Vous disposez de deux options pour continuer toowork avec ce modèle. Vous pouvez télécharger le modèle de hello et travailler dessus localement avec un éditeur JSON. Ou bien, vous pouvez enregistrer la bibliothèque de modèles de tooyour hello et travailler dessus via le portail de hello.
   
     Si vous savez à l’aide d’un éditeur JSON comme [VS Code](https://code.visualstudio.com/) ou [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), vous pouvez télécharger le modèle hello localement et à l’aide de cet éditeur. toowork localement, sélectionnez **télécharger**.
   
      ![télécharger un modèle](./media/resource-manager-export-template/download-template.png)
   
     Si vous n’êtes pas configuré avec un éditeur JSON, vous préférerez peut-être modifier le modèle hello via le portail de hello. reste Hello de cette rubrique suppose que vous avez enregistré la bibliothèque de modèles de tooyour hello dans le portail de hello. Toutefois, vous vous hello même toohello modèle modifications de la syntaxe si en local avec un éditeur JSON ou via le portail de hello. toowork via le portail de hello, sélectionnez **ajouter toolibrary**.
   
      ![Ajouter toolibrary](./media/resource-manager-export-template/add-to-library.png)
   
     Lorsque vous ajoutez une bibliothèque de toohello de modèles, donner au modèle de hello un nom et une description. Sélectionnez ensuite **Enregistrer**.
   
     ![définir les valeurs du modèle](./media/resource-manager-export-template/save-library-template.png)
4. tooview un modèle enregistré dans votre bibliothèque, sélectionnez **davantage de services**, type **modèles** toofilter des résultats, sélectionnez **modèles**.
   
      ![trouver des modèles](./media/resource-manager-export-template/find-templates.png)
5. Sélectionnez modèle hello portant hello, que vous avez enregistré.
   
      ![sélectionner un modèle](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-hello-template"></a>Personnaliser le modèle de hello
fonctionnement du modèle Hello exportée précis que si vous souhaitez toocreate hello même web app et la base de données SQL pour chaque déploiement. Toutefois, Resource Manager propose des options permettant de déployer des modèles avec une plus grande flexibilité. Cet article explique les paramètres tooadd pour hello base de mot de passe et le nom d’administrateur. Vous pouvez utiliser cette même tooadd d’approche davantage de flexibilité pour les autres valeurs dans le modèle de hello.

1. modèle de toocustomize hello, sélectionnez **modifier**.
   
     ![afficher le modèle](./media/resource-manager-export-template/select-edit.png)
2. Sélectionnez le modèle de hello.
   
     ![modifier un modèle](./media/resource-manager-export-template/select-added-template.png)
3. les valeurs hello toobe toopass en mesure que vous pouvez toospecify pendant le déploiement, ajoutent hello suivant deux paramètres toohello **paramètres** section dans le modèle de hello :

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. toouse nouveaux paramètres hello, remplacez la définition de serveur SQL hello Bonjour **ressources** section. Notez que **administratorLogin** et **administratorLoginPassword** utilisent maintenant des valeurs de paramètre.

   ```json
   {
       "comments": "Generalized from resource: '/subscriptions/{subscription-id}/resourceGroups/exportsite/providers/Microsoft.Sql/servers/tfserverexport'.",
       "type": "Microsoft.Sql/servers",
       "kind": "v12.0",
       "name": "[parameters('servers_tfserverexport_name')]",
       "apiVersion": "2014-04-01-preview",
       "location": "South Central US",
       "scale": null,
       "properties": {
           "administratorLogin": "[parameters('administratorLogin')]",
           "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
           "version": "12.0"
       },
       "dependsOn": []
   },
   ```

6. Sélectionnez **OK** lorsque vous avez terminé la modification de modèle de hello.
7. Sélectionnez **enregistrer** modèle toohello de modifications de hello toosave.
   
     ![enregistrer un modèle](./media/resource-manager-export-template/save-template.png)
8. modèle de tooredeploy hello mis à jour, sélectionnez **déployer**.
   
     ![déployer un modèle](./media/resource-manager-export-template/redeploy-template.png)
9. Fournir des valeurs de paramètre et sélectionnez une ressource toodeploy hello regrouper à.


## <a name="fix-export-issues"></a>Résoudre les problèmes d’exportation
Pas tous les types de ressources prend en charge la fonction de modèle d’exportation hello. tooresolve ce problème, ajoutez les ressources manquantes hello dans votre modèle. message d’erreur Hello inclut les types de ressources hello qui ne peuvent pas être exportées. Recherchez le type de ressource dans [Référence de modèle](/azure/templates/). Par exemple, toomanually ajouter une passerelle de réseau virtuel, consultez [référence de modèle Microsoft.Network/virtualNetworkGateways](/azure/templates/microsoft.network/virtualnetworkgateways).

> [!NOTE]
> Vous rencontrerez des problèmes d’exportation uniquement lors de l’exportation à partir d’un groupe de ressources et non à partir de votre historique de déploiement. Si votre dernier déploiement représente avec précision l’état actuel de hello hello du groupe de ressources, vous devez exporter le modèle de hello à partir de l’historique de déploiement hello plutôt qu’à partir du groupe de ressources hello. Exporter à partir d’un groupe de ressources lorsque vous avez apporté des modifications toohello ressource groupe qui ne sont pas définis dans un modèle unique.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Vous avez appris comment tooexport un modèle à partir des ressources que vous avez créé dans le portail de hello.

* Vous pouvez déployer un modèle avec [PowerShell](resource-group-template-deploy.md), [l’interface de ligne de commande Azure](resource-group-template-deploy-cli.md) ou [l’API REST](resource-group-template-deploy-rest.md).
* toosee tooexport un modèle via PowerShell, voir [à l’aide de Azure PowerShell avec Azure Resource Manager](powershell-azure-resource-manager.md).
* toosee tooexport un modèle via l’interface CLI d’Azure, voir [hello d’utilisation CLI d’Azure pour Mac, Linux et Windows avec Azure Resource Manager](xplat-cli-azure-resource-manager.md).

