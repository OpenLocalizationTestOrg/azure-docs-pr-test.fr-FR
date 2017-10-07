---
title: "aaaGet a démarré avec des modèles privés | Documents Microsoft"
description: "Ajouter, gérer et partager vos modèles privés à l’aide de hello portail Azure, hello CLI d’Azure ou PowerShell."
services: marketplace-customer
documentationcenter: 
author: VybavaRamadoss
manager: asimm
editor: 
tags: marketplace, azure-resource-manager
keywords: 
ms.assetid: 6ec20778-b578-4885-acb5-104b0e51ea1a
ms.service: marketplace
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: vybavar
ms.openlocfilehash: 1fe2c6422f62a98f7ae9ba5c61b9639d993f0bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-private-templates-on-hello-azure-portal"></a>Prise en main des modèles privés sur hello portail Azure
Un [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) modèle est un modèle déclaratif utilisé toodefine votre déploiement. Vous pouvez définir des toodeploy de ressources hello pour une solution et spécifier les paramètres et les variables qui vous permettent de valeurs tooinput pour différents environnements. Hello modèle se compose de JSON et les expressions que vous pouvez utiliser les valeurs de tooconstruct pour votre déploiement.

Vous pouvez utiliser hello nouvelle **modèles** fonctionnalité Bonjour [Azure Portal](https://portal.azure.com) avec hello **Microsoft.Gallery** fournisseur de ressources comme une extension de hello [ Azure Marketplace](https://azure.microsoft.com/marketplace/) tooenable utilisateurs toocreate, gérer et déployer des modèles de privé à partir d’une bibliothèque personnelle.

Ce document présente l’ajout, la gestion et le partage privé **modèle** à l’aide de hello portail Azure.

## <a name="guidance"></a>Assistance
Hello suggestions suivantes vous permettra de tirer pleinement parti des **modèles** lorsque vous travaillez avec vos solutions :

* Un **Modèle** est une ressource d’encapsulation qui contient un modèle Resource Manager et des métadonnées supplémentaires. Il comporte très comme élément tooan Bonjour Marketplace. Hello principale différence est qu’il est un élément privé en tant qu’éléments de Marketplace publics toohello exécutée.
* Hello **modèles** bibliothèque fonctionne bien pour les utilisateurs qui ont besoin de toocustomize leurs déploiements.
* **Modèles** conviennent aux utilisateurs ayant besoin d’un référentiel simple dans Azure.
* Commencez par un modèle Resource Manager existant. Recherchez des modèles dans [github](https://github.com/Azure/azure-quickstart-templates) ou [exportez des modèles](../azure-resource-manager/resource-manager-export-template.md) à partir d’un groupe de ressources existant.
* **Modèles** liée toohello utilisateurs en les publie. nom du serveur de publication Hello est visible tooeveryone disposant d’un accès en lecture tooit.
* **Modèles** sont des ressources Azure Resource Manager et ne peuvent être renommés une fois publiés.

## <a name="add-a-template-resource"></a>Ajouter une ressource de Modèle
Il existe deux façons toocreate un **modèle** ressource Bonjour portail Azure.

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a>Méthode 1 : Créer une ressource de Modèle à partir d’un groupe de ressources en cours d’exécution
1. Accédez tooan groupe de ressources existant sur hello portail Azure. Sélectionnez **Exporter le modèle** dans **Paramètres**.
2. Une fois le modèle de gestionnaire de ressources hello est exporté, utilisez hello **enregistrer le modèle** bouton toosave il toohello **modèles** référentiel. Cliquez [ici](../azure-resource-manager/resource-manager-export-template.md)pour obtenir des informations complètes sur l’exportation des modèles.
   <br /><br />
   ![Exportation de groupe de ressources](media/rg-export-portal1.PNG)  <br />
3. Sélectionnez hello **enregistrer tooTemplate** bouton de commande.
   <br /><br />
4. Entrez hello informations suivantes :
   
   * Nom : nom de l’objet de modèle hello (Remarque : il s’agit d’un nom de base Azure Resource Manager. Toutes les restrictions d’affectation de noms s’appliquent et ces derniers ne peuvent être modifiés une fois créés).
   * Description : résumé sur le modèle de hello.
     
     ![Enregistrer un Modèle](media/save-template-portal1.PNG)  <br />
5. Cliquez sur **Enregistrer**.
   
   > [!NOTE]
   > Hello Panneau de modèle d’exportation affiche des notifications lorsque hello modèle exporté du Gestionnaire de ressources comporte des erreurs, mais vous serez toujours en mesure de toosave cette toohello de modèle de gestionnaire de ressources modèles. Assurez-vous que vous vérifiez et corrigez les problèmes de modèle de n’importe quel gestionnaire de ressources avant redéploiement hello exportée modèle du Gestionnaire de ressources.
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a>Méthode 2: Ajouter une nouvelle ressource de Modèle à partir du panneau Parcourir
Vous pouvez également ajouter un nouveau **modèle** à partir de zéro à l’aide de hello + ajouter bouton de commande dans **Parcourir > modèles**. Vous devez tooprovide un nom, Description et hello modèle du Gestionnaire de ressources JSON.

![Ajouter un Modèle](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> Microsoft.Gallery est un fournisseur de ressources Azure basé sur le client. Bonjour ressource de modèle est utilisateur toohello liée qui l’a créée. Il n’est pas liée tooany des abonnement spécifique. Un abonnement doit toobe choisi uniquement lors du déploiement d’un modèle.
> 
> 

## <a name="view-template-resources"></a>Afficher les ressources de Modèle
Tous les **modèles** tooyou disponible peut être consulté à **Parcourir > modèles**. Cela inclut les **Modèles** que vous avez créés, ainsi que ceux ayant été partagés avec vous avec différents niveaux d’autorisation. Plus de détails dans hello [le contrôle d’accès](#access-control-for-a-tenant-resource-provider) section ci-dessous.

![Afficher le Modèle](media/view-template-portal1.PNG)  <br />

Vous pouvez afficher les détails de hello d’un **modèle** en cliquant sur un élément dans la liste de hello.

![Afficher le Modèle](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a>Modifier une ressource de Modèle
Vous pouvez lancer des flux d’édition hello pour un **modèle** par élément de hello avec le bouton droit sur la liste de navigation hello ou en choisissant le bouton de commande hello modifier.

![Modifier un Modèle](media/edit-template-portal1a.PNG)  <br />

Vous pouvez modifier la description de hello ou le texte du modèle de gestionnaire de ressources. Vous ne pouvez pas modifier le nom de hello puisqu’il s’agit d’un nom de ressource du Gestionnaire de ressources. Lorsque vous modifiez le modèle de gestionnaire de ressources hello JSON nous validera tooensure qu’il s’agit d’un JSON valide. Choisissez **OK** , puis **enregistrer** toosave votre modèle mis à jour.

![Modifier un Modèle](media/edit-template-portal2a.PNG)  <br />

Une fois hello **modèle** est enregistrée une notification de confirmation s’affiche.

![Modifier un Modèle](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a>Déployer une ressource de modèle
Vous pouvez déployer tout **Modèle** pour lequel vous disposez d’autorisations de **lecture**. flux de déploiement Hello lance le panneau de déploiement Azure modèle standard hello. Renseignez les valeurs hello pour tooproceed de paramètres de modèle de gestionnaire de ressources hello avec le déploiement de hello.

![Déployer un modèle](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a>Partager une ressource de Modèle
Une ressource de **Modèle** peut être partagée avec vos homologues. Partage se comporte de la même façon trop[attribution de rôle pour n’importe quelle ressource sur Azure](../active-directory/role-based-access-control-configure.md). Hello **modèle** propriétaire accorde des autorisations tooother les utilisateurs peuvent interagir avec une ressource de modèle. Hello personne ou le groupe de personnes, vous partagez hello **modèle** avec sera modèle de gestionnaire de ressources en mesure de toosee hello et ses propriétés de la galerie.

### <a name="access-control-for-hello-microsoftgallery-resources"></a>Contrôle d’accès pour les ressources Microsoft.Gallery hello
| Rôle | Autorisations |
| --- | --- |
| Propriétaire |Permet un contrôle total sur la ressource de modèle hello, y compris le partage |
| Lecteur |Permet de lire et Execute(Deploy) sur hello ressource de modèle |
| Collaborateur |Accorde l’autorisation de modifier et supprimer sur hello ressource de modèle. Utilisateur ne peuvent pas partager hello modèle avec d’autres utilisateurs |

Sélectionnez **partage** sur l’élément de navigation hello par avec le bouton droit ou sur le panneau d’affichage hello d’un élément spécifique. Cette opération lance une expérience de partage.

![Partager le modèle](media/share-template-portal1a.png)  <br />

 Vous pouvez maintenant choisir un rôle et une tooa de l’accès des tooprovide l’utilisateur ou un groupe particulier **modèle**. les rôles disponibles Hello sont propriétaire, collaborateur et le lecteur. Plus de détails dans hello [le contrôle d’accès](#access-control-for-a-tenant-resource-provider) section ci-dessus.

![Partager le modèle](media/share-template-portal2b.png)  <br />

![Partager le modèle](media/share-template-portal3b.png)  <br />

Cliquez sur **Sélectionner**, puis sur **OK**. Vous pouvez maintenant voir hello utilisateurs ou groupes vous avez ajouté les ressources toohello.

![Partager le modèle](media/share-template-portal4b.png)  <br />

> [!NOTE]
> Un modèle peut être partagé uniquement avec des utilisateurs et groupes Bonjour même locataire Azure Active Directory. Si vous partagez un modèle avec une adresse de messagerie qui n’est pas dans votre client, une invitation sera envoyée demandant le locataire de hello toojoin hello utilisateur en tant qu’invité.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* toolearn sur la création de modèles du Gestionnaire de ressources, consultez [création de modèles](../azure-resource-manager/resource-group-authoring-templates.md)
* les fonctions hello toounderstand que vous pouvez utiliser dans un modèle de gestionnaire de ressources, consultez [fonctions de modèle](../azure-resource-manager/resource-group-template-functions.md)
* Pour obtenir des instructions sur la conception de vos modèles, consultez [Meilleures pratiques relatives à la conception des modèles Azure Resource Manager](../azure-resource-manager/best-practices-resource-manager-design-templates.md)

