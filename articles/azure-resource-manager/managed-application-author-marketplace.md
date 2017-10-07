---
title: "aaaAzure gérés applications Bonjour Marketplace | Documents Microsoft"
description: "Décrit les Azure applications managées qui sont disponibles via hello Marketplace."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b3cdf3f1fccdd47db699e4892ae8bce35118bfd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-in-hello-marketplace"></a>Azure géré applications Bonjour Marketplace

 MSP, éditeurs de logiciels indépendants et les intégrateurs système (SIs) peuvent utiliser Azure géré applications toooffer leurs clients d’Azure Marketplace de tooall solutions. Ces solutions réduisent la maintenance de hello et surcharge de maintenance pour les clients. Serveurs de publication peuvent vendre infrastructure et les logiciels via hello Marketplace. Elles peuvent attacher support opérationnel toomanaged applications et services. Pour plus d’informations, consultez [Vue d’ensemble des applications gérées](managed-application-overview.md).

Cet article explique comment un MSP, éditeurs de logiciels ou SI peut publier un toohello application Marketplace et le rendre disponible toocustomers.

## <a name="prerequisites-for-publishing-a-managed-application"></a>Conditions préalables à la publication d’une application gérée

Conditions préalables des toolisting Bonjour Marketplace :

* Techniques

    *  Pour plus d’informations sur la structure de base de hello et syntaxe des modèles Azure Resource Manager, consultez [modèles Azure Resource Manager](resource-group-authoring-templates.md).
    *  solutions de modèle complète tooview, consultez [modèles de démarrage rapide d’Azure](https://azure.microsoft.com/en-us/documentation/templates/) ou hello [référentiel de modèle de démarrage rapide](https://github.com/azure/azure-quickstart-templates).
    *  Pour plus d’informations sur comment toocreate hello interface pour les clients qui déploient votre application via hello Marketplace, consultez [créer un fichier de définition d’interface utilisateur](managed-application-createuidefinition-overview.md).

* Non techniques (critères de l’entreprise)

    *   Votre entreprise ou ses filiales doit se trouver dans un pays où les ventes sont pris en charge par hello Marketplace.
    *   Votre produit doit avoir une licence d’une manière qui est compatible avec les modèles de facturation pris en charge par hello Marketplace.
    *   Vous êtes responsable de la toocustomers disponibles du support technique de façon commercialement raisonnable. prise en charge Hello peut être gratuit, payé, ou via la Communauté prend en charge.
    *   Il vous incombe de gérer les licences de vos logiciels et de toutes les dépendances de logiciels tiers.
    *   Vous devez fournir le contenu qui répond aux critères de votre toobe offre répertoriés dans hello Marketplace et hello portail Azure.
    *   Vous devez accepter les termes du contrat de toohello de stratégies de Participation hello Azure Marketplace et le contrat d’éditeur.
    *   Vous devez accepter toocomply avec Microsoft Azure Certified accord hello les conditions d’utilisation et déclaration de confidentialité de Microsoft.

## <a name="create-a-new-azure-application-offer"></a>Création d’une offre d’application Azure

Une fois les conditions préalables hello, vous êtes prêt toocreate votre offre de l’application managée. Voici une brève présentation de ce que sont une offre et une référence (SKU).

### <a name="offer"></a>Offer

offre Hello pour une application managée correspond classe tooa du produit à partir d’un serveur de publication de l’offre. Si vous avez un nouveau type de solution / l’application que vous souhaitez toomake disponible dans hello Marketplace, vous pouvez le configurer en tant qu’une offre. Une offre est une collection de références (SKU). Toutes les offres apparaît comme son propre entité Bonjour Marketplace.

### <a name="sku"></a>SKU

Une référence (SKU) est hello plus petite être achetée unité d’une offre. Vous pouvez utiliser une référence (SKU) au sein de hello même toodifferentiate de classe (offre) produit entre :

* Les différentes fonctionnalités prises en charge.
* Indique si les offre hello sont gérée ou non gérée.
* Les modèles de facturation pris en charge.

Une référence (SKU) s’affiche sous l’offre de parent hello Bonjour Marketplace. Il apparaît comme son propre entité être achetée Bonjour portail Azure.

### <a name="set-up-an-offer"></a>Configuration d’une offre

1. Connectez-vous à toohello [portail du partenaire de nuage](https://cloudpartner.azure.com/).

2. Dans le volet de navigation hello hello gauche, sélectionnez **+ nouvelle offre** > **des Applications Azure**.

    ![Nouvelle offre](./media/managed-application-author-marketplace/newOffer.png)

3. Remplir des formulaires hello apparaissant sur hello restant dans hello **éditeur** vue. Les champs obligatoires sont indiqués par un astérisque rouge (*).

    ![Paramètres de l’offre](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    Quatre formes principales sont toocreate utilisé une application managée :

    a. Paramètres de l’offre

    b. Références (SKU)

    c. Marketplace

    d. Support

Ces formes sont décrites en détail dans les sections suivantes de hello.

## <a name="offer-settings-form"></a>Formulaire des paramètres de l’offre
Utiliser ce paramètres de l’offre de base toospecify hello.

1. Renseignez hello **offrent des paramètres** formulaire. les champs différents Hello sont :

    a. **ID offre**: cet identificateur unique identifie offre hello dans un profil de serveur de publication. Cet ID est visible dans les URL de produit, les modèles Resource Manager et les états de facturation. Il ne peut comprendre que des caractères alphanumériques en minuscules ou des tirets (-). Hello ID ne peut pas se terminer dans un tiret. Il est limité tooa jusqu'à 50 caractères. Ce champ est verrouillé une fois l’offre publiée.

    b. **ID de l’éditeur**: utiliser ce profil de serveur de publication de liste déroulante toochoose hello souhaité toopublish cette offre sous. Ce champ est verrouillé une fois l’offre publiée.

    c. **Nom**: ce nom d’affichage pour votre offre apparaît dans hello Marketplace et dans le portail de hello. Il ne peut pas comprendre plus de 50 caractères. Incluez un nom de marque reconnaissable pour votre produit. N’incluez pas ici le nom de votre entreprise, sauf si c’est le nom sous lequel l’offre est commercialisée. Si vous êtes marketing cette offre sur votre propre site Web, assurez-vous que ce nom hello est exactement comment il apparaît sur votre site Web.

2. Sélectionnez **enregistrer** toosave votre progression. 

## <a name="skus-form"></a>Formulaire de références (SKU)
étape suivante de Hello est SKU tooadd pour votre offre.

1. Sélectionnez **Références** > **Nouvelle référence**. 

    ![Sélectionner option de nouvelle référence](./media/managed-application-author-marketplace/newOffer_skus.png)

2. Saisissez un **ID de référence**. Un ID de référence (SKU) est un identificateur unique pour hello référence (SKU) au sein d’une offre. Cet ID est visible dans les URL de produit, les modèles Resource Manager et les états de facturation. Il ne peut comprendre que des caractères alphanumériques en minuscules ou des tirets (-). Hello ID ne peut pas se terminer par un tiret, et il est limité tooa jusqu'à 50 caractères. Ce champ est verrouillé une fois l’offre publiée. Vous pouvez avoir plusieurs références (SKU) au sein d’une même offre. Vous avez besoin d’une référence (SKU) pour chaque image que vous prévoyez toopublish.

3. Remplir hello **détails de la référence (SKU)** section hello suivant du formulaire :

    ![Fournir une nouvelle référence (SKU)](./media/managed-application-author-marketplace/newOffer_newsku.png)

    Renseignez hello champs qui suivent :
    
    a. **Titre** : saisissez un titre pour cette référence. Ce titre s’affiche dans la galerie de hello pour cet élément.

    b. **Summary** (Résumé) : saisissez un bref résumé décrivant cette référence (SKU). Ce texte s’affiche sous le titre de hello.

    c. **Description**: entrez une description détaillée hello référence (SKU).

    d. **Type de référence (SKU)**: hello valeurs autorisées sont **Application managée** et **des modèles de Solution**. Dans le cas présent, sélectionnez **Managed Application** (Application gérée).

4. Remplir hello **détails du Package** section hello suivant du formulaire :

    ![Package](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    Renseignez hello champs qui suivent :

    a. **Version actuelle**: entrez une version de package hello vous téléchargez. Il doit être au format de hello `{number}.{number}.{number}{number}`.

    b. **Sélectionnez un fichier de package**: hello suivant des fichiers qui sont compressés dans un fichier .zip contient :
    * **applianceMainTemplate.json**: fichier de modèle de déploiement hello qui a utilisé l’application toodeploy hello solution. Pour plus d’informations sur la façon de fichiers de modèle de déploiement toocreate, consultez [créer votre premier modèle Azure Resource Manager](resource-manager-create-first-template.md).
    * **appliancecreateUIDefinition.json**: ce fichier est utilisé par hello toogenerate portail Azure hello interface utilisateur qui a utilisé tooprovision cette solution/application. Pour plus d’informations, consultez la page [Prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).
    * **mainTemplate.json**: ce fichier de modèle contient uniquement des ressources Microsoft.Solution/appliances hello. fichier de mainTemplate Hello inclut hello propriétés suivantes :

        *  **type**: utilisez **Marketplace** pour les applications managées Bonjour Marketplace.
        *  **ManagedResourceGroupId**: ce groupe de ressources dans l’abonnement du client hello est où toutes les ressources hello définis dans applianceMainTemplate.json sont déployés.
        *  **PublisherPackageId**: cette chaîne identifie de façon unique le package de hello. Fournir la valeur hello format hello `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.

Obtenir hello **ID d’offre** et **ID de l’éditeur** de hello publication portail, comme indiqué dans hello suivant image :

![ID de l’offre](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
Obtenir hello **ID de référence (SKU)**, comme indiqué dans hello suivant image :

![RÉFÉRENCE (SKU)](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
Obtenir le package de hello **Version**, comme indiqué dans hello suivant image :

![Version du package](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  En fonction de hello précédents exemples, hello valeur de **PublisherPackageId** est `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.

  Exemple de fichier mainTemplate.json :

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify hello name of hello storage account"
        }
      },
      "storageAccountType": {
        "type": "string"
      }
    },
    "variables": {
      "managedResourceGroup": "[concat(resourceGroup().id,uniquestring(resourceGroup().id))]"
    },
    "resources": [{
      "type": "Microsoft.Solutions/appliances",
      "apiVersion": "2016-09-01-preview",
      "name": "[concat(parameters('storageAccountNamePrefix'), '-', 'managed')]",
      "location": "[resourceGroup().location]",
      "kind": "marketplace",
      "properties": {
        "managedResourceGroupId": "[variables('managedResourceGroup')]",
        "PublisherPackageId":"azureappliancetest.ravmanagedapptest.ravpreviewmanagedsku.1.0.0",
        "parameters": {
          "storageAccountName": {
            "value": "[parameters('storageAccountNamePrefix')]"
          },
          "storageAccountType": {
            "value": "[parameters('storageAccountType')]"
          }
        }
      }
    }],
    "outputs": {

    }
  }
  ```

Ce package doit contenir tous les autres modèles imbriqués ou des scripts qui sont requis toosuccessfully configurer cette application. Hello mainTemplate.json, applianceMainTemplate.json et applianceCreateUIDefinition.json fichiers doivent être présents dans le dossier racine hello.

* **Autorisations**: cette propriété définit qui obtient un niveau d’accès et hello d’accès toohello des ressources dans les abonnements des clients. serveur de publication Hello peut utiliser application hello de toomanage au nom de client de hello.
* **PrincipalId**: cette propriété est l’identificateur d’Azure Active Directory (Azure AD) hello d’un utilisateur, un groupe d’utilisateurs ou une application qui a attribué certaines autorisations sur les ressources hello hello l’abonnement du client. Hello définition de rôle décrit les autorisations de hello. 
* **Définition de rôle**: cette propriété est une liste de tous les hello contrôle d’accès en fonction du rôle (RBAC) rôles intégrés fournis par Azure AD. Vous pouvez sélectionner le rôle hello qui des ressources hello toomanage toouse plus appropriés pour le compte du client de hello.

Vous pouvez ajouter plusieurs autorisations. Nous vous recommandons de créer un groupe d’utilisateurs AD et de spécifier son ID dans **PrincipalId**. De cette manière, vous pouvez ajouter le groupe d’utilisateurs plus d’utilisateurs toohello sans Bonjour besoin tooupdate Bonjour référence (SKU).

Pour plus d’informations sur RBAC, consultez [prise en main RBAC Bonjour Azure portal](../active-directory/role-based-access-control-what-is.md).

## <a name="marketplace-form"></a>Formulaire Marketplace

demande de Hello formulaire de Marketplace pour les champs qui apparaissent sur hello [Azure Marketplace](https://azuremarketplace.microsoft.com) et hello [portail Azure](https://portal.azure.com/).

### <a name="preview-subscription-ids"></a>ID d’abonnement pour version préliminaire

Entrez une liste d’ID qui peuvent accéder à hello offre après sa publication d’abonnement Azure. Vous pouvez utiliser ces offre de hello prévisualisé tootest blanc dans la liste des abonnements avant de le rendre live. Vous pouvez compiler une liste blanche d’abonnements too100 dans le portail du partenaire hello.

### <a name="suggested-categories"></a>Catégories suggérées

Sélectionnez les catégories de toofive à partir de la liste hello associé à votre offre permettre être mieux. Ces catégories est utilisée toomap vos catégories de produit toohello offre qui sont disponibles dans hello [Azure Marketplace](https://azuremarketplace.microsoft.com) et hello [portail Azure](https://portal.azure.com/).

#### <a name="azure-marketplace"></a>Azure Marketplace

Résumé de Hello de votre application managée affiche hello champs qui suivent :

![Résumé sur la place de marché](./media/managed-application-author-marketplace/publishvm10.png)

Hello **vue d’ensemble** onglet pour votre application managée affiche hello champs qui suivent :

![Présentation de la Place de marché](./media/managed-application-author-marketplace/publishvm11.png)

Hello **Plans + tarification** onglet pour votre application managée affiche hello champs qui suivent :

![Plans sur la place de marché](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a>Portail Azure

Résumé de Hello de votre application managée affiche hello champs qui suivent :

![Résumé sur le portail](./media/managed-application-author-marketplace/publishvm12.png)

vue d’ensemble de Hello pour votre application managée affiche hello champs qui suivent :

![Présentation du portail](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a>Instructions concernant le logo

Suivez ces instructions pour un logo que vous téléchargez dans le portail du partenaire de Cloud hello :

*   Hello conception Azure a une palette de couleurs simple. Limiter le nombre des principaux hello et les couleurs de base de données secondaire sur votre logo.
*   couleurs du thème Hello du portail de hello sont blancs et noir. N’utilisez pas ces couleurs comme couleur d’arrière-plan hello pour votre logo. Utilisez une couleur qui rend votre logo dans le portail de hello. Nous vous recommandons d’utiliser des couleurs primaires simples. *Si vous utilisez un arrière-plan transparent, assurez-vous que le logo de hello et le texte ne sont pas blancs, noir, ou en bleu.*
*   N’utilisez pas un arrière-plan dégradé sur le logo de hello.
*   Ne pas placer du texte sur le logo de hello, même pas votre entreprise ou le nom de marque. Hello apparence de votre logo doit être plat et éviter des dégradés.
*   Assurez-vous que le logo de hello n’est pas étirée.

#### <a name="hero-logo"></a>Bannière

logo de héros Hello est facultative. serveur de publication Hello peut choisir tooupload pas un logo héros. Une fois que l’icône de héros hello est téléchargé, il ne peut pas être supprimé. À ce stade, les partenaires hello doivent respecter les règles de Marketplace de hello pour les icônes de héros.

Suivez ces instructions pour l’icône du logo héros hello :

*   nom complet de l’éditeur Hello, titre de plan hello et offre hello résumée s’affichent en blanc. Par conséquent, n’utilisez une couleur claire pour l’arrière-plan hello d’icône de héros hello. Les arrière-plans noirs, blancs et transparents ne sont pas autorisés pour les icônes.
*   Une fois que l’offre de hello est répertorié, serveur de publication hello le nom complet, titre de plan hello, offre hello résumée et hello **créer** bouton sont incorporés par programmation à l’intérieur du logo de héros hello. Par conséquent, n’entrez pas de texte lorsque vous concevez le logo de héros hello. Laisser un espace vide sur hello droite, car le texte hello est inclus par programme dans l’espace. espace vide Hello texte hello doit être hello droite 415 x 100 pixels. Elle est décalée par 370 pixels de hello gauche.

    ![Exemple d’icône de bannière](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a>Formulaire de prise en charge

Remplir hello **prennent en charge** formulaire avec prise en charge des contacts à partir de votre entreprise. Ces informations peuvent être les contacts de support d’ingénierie et client.

## <a name="publish-an-offer"></a>Publication d’une offre

Une fois que vous remplissez toutes les sections hello, sélectionnez **publier** processus hello toostart qui rend votre toocustomers disponible offre.

## <a name="next-steps"></a>Étapes suivantes

* Pour une introduction toomanaged les applications, voir [vue d’ensemble de Managed application](managed-application-overview.md).
* Pour plus d’informations sur la consommation d’une application managée à partir de hello Marketplace, consultez [Azure de consommer gérés applications Bonjour Marketplace](managed-application-consume-marketplace.md).
* Pour plus d’informations sur la publication d’une application gérée de catalogue de services, consultez l’article [Créer et publier une application gérée de catalogue de services](managed-application-publishing.md).
* Pour plus d’informations sur l’utilisation d’une application gérée de catalogue de services, consultez l’article [Utiliser une application gérée du catalogue de services](managed-application-consumption.md).
