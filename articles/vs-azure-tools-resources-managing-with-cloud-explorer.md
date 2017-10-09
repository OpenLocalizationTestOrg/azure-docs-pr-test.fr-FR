---
title: aaaManaging Azure ressources de Cloud Explorer | Documents Microsoft
description: "Découvrez comment toouse Cloud Explorer toobrowse et gérer des ressources Azure dans Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/25/2017
ms.author: kraigb
ms.openlocfilehash: 8a81660074d5d04be063df9e25076b7a97586514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a>Gérer les ressources hello associés à vos comptes Azure dans Visual Studio Cloud Explorer
Cloud Explorer Active vous tooview vos ressources Azure et les groupes de ressources, examiner leurs propriétés et effectuer des actions de diagnostics essentiels de développeur à partir de Visual Studio. 

Comme hello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer repose sur la pile du Gestionnaire de ressources Azure hello. Par conséquent, Cloud Explorer comprend des ressources, telles que les groupes de ressources Azure, et des services Azure, notamment Logic Apps et API Apps, et prend en charge le [contrôle d’accès en fonction du rôle](active-directory/role-based-access-control-configure.md) (RBAC). 

## <a name="prerequisites"></a>Composants requis
- [Visual Studio 2017](https://www.visualstudio.com/downloads/) avec hello **la charge de travail Azure** sélectionné, ou une version antérieure de Visual Studio avec hello [Microsoft Azure SDK pour .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).
- Compte Microsoft Azure : si vous ne possédez pas de compte, vous pouvez [vous inscrire à un essai gratuit](http://go.microsoft.com/fwlink/?LinkId=623901) ou [activer les avantages de votre abonnement Visual Studio](http://go.microsoft.com/fwlink/?LinkId=623901).

> [!NOTE]
> tooview Cloud Explorer, sélectionnez **vue** > **Cloud Explorer** sur la barre de menus hello.   
> 
> 

## <a name="add-an-azure-account-toocloud-explorer"></a>Ajouter un compte Azure de tooCloud Explorer
ressources de hello tooview associés à un compte Azure, vous devez d’abord ajouter hello compte tooCloud Explorer. 

1. Dans **Cloud Explorer**, sélectionnez **Paramètres de compte Azure**.

    ![Icône des paramètres de compte Azure Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. Sélectionnez **Ajouter un nouveau compte**. 

    ![Lien Ajouter un compte Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. Connectez-vous à toohello dont vous souhaitez que les ressources de compte Azure toobrowse. 

1. Une fois connecté tooan compte Azure, affichent les abonnements hello associés à ce compte. Sélectionnez hello cases à cocher pour les abonnements de compte hello vous souhaitez toobrowse, puis sélectionnez **appliquer**. 
 
    ![Cloud Explorer : sélectionnez toodisplay des abonnements Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. Après avoir sélectionné les abonnements dont vous souhaitez que les ressources hello toobrowse, ces abonnements et des ressources affichent Bonjour Cloud Explorer.

    ![Listing des ressources Cloud Explorer pour un compte Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a>Supprimer un compte Azure de Cloud Explorer 

1. Dans **Cloud Explorer**, sélectionnez **Paramètres de compte Azure**.

    ![Icône des paramètres de compte Azure Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. Suivant toohello compte tooremove, sélectionnez **supprimer**.

    ![Icône des paramètres de compte Azure Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a>Afficher les types ou les groupes de ressources
tooview vos ressources Azure, vous pouvez choisir le **Types de ressources** ou **groupes de ressources** vue.

1. Dans **Cloud Explorer**, sélectionnez hello liste déroulante Affichage de ressources.

    ![Affichage de ressources de l’Explorateur déroulante liste tooselect hello souhaité de cloud computing](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. À partir du menu contextuel de hello, sélectionnez hello affichage de votre choix : 

    - **Types de ressources** affichage - hello commun utilisé sur hello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), affiche vos ressources Azure classés par leur type, telles que les applications web, les comptes de stockage et les machines virtuelles. 
    - **Groupes de ressources** afficher - ressources Azure de classe par groupe de ressources Azure hello auquel ils sont associés. Un groupe de ressources est un regroupement de ressources Azure, généralement utilisé par une application spécifique. toolearn savoir plus sur les groupes de ressources Azure, consultez [vue d’ensemble du Gestionnaire de ressources Azure](./azure-resource-manager/resource-group-overview.md).

    Hello image suivante présente une comparaison des hello deux affichages de ressources :

    ![Comparaison des affichages des ressources Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a>Afficher et parcourir les ressources dans Cloud Explorer
toonavigate tooan ressource Azure et afficher les informations dans le Cloud Explorer, développez l’élément hello type ou groupe de ressources et puis sélectionnez les ressources hello. Lorsque vous sélectionnez une ressource, les informations s’affichent dans les onglets de hello deux - **Actions** et **propriétés** - bas hello Cloud Explorer. 

- **Actions** onglet - listes hello actions possibles dans Cloud Explorer pour la ressource de hello sélectionné. Vous pouvez également afficher ces options en cliquant sur hello ressource tooview son menu contextuel.

- **Propriétés** onglet - affiche les propriétés hello de ressource hello, telles que son groupe de type, de paramètres régionaux et de ressources auquel il est associé.

Hello image suivante montre une comparaison de l’exemple de ce que vous voyez sur chaque onglet pour un Service d’application :

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

Chaque ressource a d’action hello **ouvrir dans le portail**. Lorsque vous sélectionnez cette action, Cloud Explorer affiche les ressources hello sélectionné Bonjour [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040). Hello **ouvrir dans le portail** fonctionnalité est pratique pour parcourir les ressources de toodeeply imbriquée.

Actions supplémentaires et des valeurs de propriété peuvent également apparaître en fonction de hello ressource Azure. Par exemple, les applications web et logique ont également les actions hello **ouvrir dans le navigateur** et **attacher le débogueur** en outre trop**ouvrir dans le portail**. Éditeurs de tooopen actions s’affichent lorsque vous choisissez un objet blob de compte de stockage, une file d’attente ou une table. Les applications Azure ont des propriétés **URL** et **État**, tandis que les ressources de stockage ont des propriétés clé et chaîne de connexion.

## <a name="find-resources-in-cloud-explorer"></a>Trouver des ressources dans Cloud Explorer
ressources toolocate avec un nom spécifique dans vos abonnements de compte Azure, entrez les nom hello Bonjour **recherche** zone dans l’Explorateur de Cloud.

![Trouver des ressources dans Cloud Explorer](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

Lorsque vous entrez des caractères dans hello **recherche** zone, uniquement les ressources qui correspondent à ces caractères s’affichent dans l’arborescence des ressources hello.
