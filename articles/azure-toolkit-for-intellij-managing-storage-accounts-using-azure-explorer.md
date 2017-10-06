---
title: "les comptes de stockage aaaManage à l’aide de hello Explorateur Azure pour IntelliJ | Documents Microsoft"
description: "Découvrez comment toomanage votre stockage Azure des comptes à l’aide de hello Explorateur Azure pour IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: b094bdcd2fa2782cb12b67c96ac406fbe4c1aa3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-by-using-hello-azure-explorer-for-intellij"></a>Gérer les comptes de stockage à l’aide de hello Explorateur Azure pour IntelliJ

Hello Explorateur Azure, qui fait partie de hello Azure Toolkit pour IntelliJ, fournit aux développeurs Java une solution facile à utiliser pour la gestion des comptes de stockage de leur compte Azure à partir d’à l’intérieur de hello IntelliJ environnement de développement intégré (IDE).

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a>Créer un compte de stockage dans IntelliJ

toocreate un compte de stockage à l’aide de hello Explorateur Azure, procédez comme hello suivant :

1. Se connecter à l’aide de hello tooyour compte Azure [instructions connectez-vous pour hello boîte à outils Azure pour Eclipse]. 

2. Bonjour **Explorateur Azure** afficher, développez hello **Azure** nœud, avec le bouton droit **comptes de stockage**, puis cliquez sur **créer un compte de stockage**.

   ![Commande Créer un compte de stockage][CS01]

3. Bonjour **créer un compte de stockage** boîte de dialogue, spécifiez hello options suivantes :

   ![Boîte de dialogue Créer un compte de stockage][CS02]

   * **Nom**: Spécifie le nom hello hello nouveau compte de stockage.

   * **Type de compte**: Spécifie le type hello de toocreate de compte de stockage (par exemple, « stockage d’objets Blob »). Pour plus d’informations, consultez la rubrique [À propos des comptes de stockage Azure]. 

   * **Performances**: Spécifie le compte de stockage de l’offre toouse à partir du serveur de publication sélectionné hello (par exemple, « Premium »). Pour plus d’informations, voir [Objectifs de scalabilité et de performances de Stockage Azure]. 

   * **Réplication**: Spécifie la réplication hello hello compte de stockage (par exemple, « redondance de Zone »). Pour plus d’informations, consultez [Réplication de Stockage Azure]. 

   * **Abonnement**: Spécifie hello abonnement Azure que vous souhaitez toouse hello nouveau compte de stockage.

   * **Emplacement**: Spécifie l’emplacement de hello où votre compte de stockage sera créé (par exemple, « Ouest des États-Unis »).

   * **Groupe de ressources**: Spécifie le groupe de ressources hello pour votre machine virtuelle. Sélectionnez une des options suivantes de hello :
      * **Créer de nouveaux**: Spécifie que vous souhaitez toocreate un groupe de ressources.
      * **Utiliser l’existant** : spécifie que vous allez opérer un choix dans une liste de groupes de ressources associés à votre compte Azure.

4. Lorsque vous avez spécifié toutes hello précédant options, cliquez sur **OK**.

## <a name="create-a-storage-container-in-intellij"></a>Créer un conteneur de stockage dans IntelliJ

toocreate un conteneur de stockage à l’aide de hello Explorateur Azure, procédez comme hello suivant :

1. Bonjour Azure Explorateur, compte de stockage hello où vous souhaitez toocreate un conteneur, puis cliquez avec le bouton droit **créer un conteneur blob**.

   ![Commande Créer un conteneur d’objets blob][CC01]

2. Bonjour **créer un conteneur blob** boîte de dialogue, spécifiez hello votre conteneur, puis cliquez sur **OK**. Pour plus d’informations sur l’affectation de noms aux conteneurs de stockage, consultez [Affectation de noms et références aux conteneurs, objets blob et métadonnées].

   ![Boîte de dialogue de création d’un conteneur d’objets blob][CC02]

## <a name="delete-a-storage-container-in-intellij"></a>Supprimer un conteneur de stockage dans IntelliJ

toodelete un conteneur de stockage à l’aide de hello Explorateur Azure, procédez comme hello suivant :

1. Bonjour Explorateur Azure, cliquez sur le conteneur de stockage hello, puis cliquez sur **supprimer**.

   ![Commande Supprimer un conteneur de stockage][DC01]

2. Dans la fenêtre de confirmation hello, cliquez sur **Oui**.

   ![Fenêtre de confirmation de la suppression d’un conteneur de stockage][DC02]

## <a name="delete-a-storage-account-in-intellij"></a>Supprimer un compte de stockage dans IntelliJ

toodelete un compte de stockage à l’aide de hello Explorateur Azure, procédez comme hello suivant :

1. Bonjour **Explorateur Azure** afficher, cliquez sur le compte de stockage hello, puis sélectionnez **supprimer**.

   ![Menu de suppression d’un compte de stockage][DS01]

2. Dans la fenêtre de confirmation hello, cliquez sur **Oui**.

   ![Fenêtre de confirmation de la suppression d’un compte de stockage][DS02]

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les comptes de stockage Azure, la taille et la tarification, consultez hello suivant des ressources :

* [Introduction tooMicrosoft stockage Azure]
* [À propos des comptes de stockage Azure]
* Tailles des comptes de stockage Azure
  * [Tailles des machines virtuelles Windows dans Azure]
  * [Tailles des machines virtuelles Linux dans Azure]
* Tarification des comptes de stockage Azure
  * [Tarification des comptes de stockage Windows]
  * [Tarification des comptes de stockage Linux]

Pour plus d’informations sur les boîtes à outils Azure pour Java IDE, consultez hello suivant des ressources :

* [boîte à outils Azure pour Eclipse]
  * [Nouveautés de hello boîte à outils Azure pour Eclipse]
  * [Lors de l’installation hello boîte à outils Azure pour Eclipse]
  * [instructions connectez-vous pour hello boîte à outils Azure pour Eclipse]
  * [Créer une application web Hello World pour Azure dans Eclipse]
* [Kit de ressources Azure pour IntelliJ]
  * [Quelles sont les nouveautés Bonjour Azure Toolkit pour IntelliJ]
  * [Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]
  * [Instructions d’authentification pour hello boîte à outils Azure pour IntelliJ]
  * [Créer une application web Hello World pour Azure dans IntelliJ]

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez [Centre de développement Java pour Azure] et [Outils Java pour Visual Studio Team Services].

<!-- URL List -->

[boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij.md
[Créer une application web Hello World pour Azure dans Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Créer une application web Hello World pour Azure dans IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Lors de l’installation hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[instructions connectez-vous pour hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Instructions d’authentification pour hello boîte à outils Azure pour IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Nouveautés de hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Quelles sont les nouveautés Bonjour Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/
[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/

[Introduction tooMicrosoft stockage Azure]: /azure/storage/storage-introduction
[À propos des comptes de stockage Azure]: /azure/storage/storage-create-storage-account
[Réplication de Stockage Azure]: /azure/storage/storage-redundancy
[Objectifs de scalabilité et de performances de Stockage Azure]: /azure/storage/storage-scalability-targets
[Affectation de noms et références aux conteneurs, objets blob et métadonnées]: http://go.microsoft.com/fwlink/?LinkId=255555

[Tailles des machines virtuelles Windows dans Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tailles des machines virtuelles Linux dans Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Tarification des comptes de stockage Windows]: /pricing/details/virtual-machines/windows/
[Tarification des comptes de stockage Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC02.png
