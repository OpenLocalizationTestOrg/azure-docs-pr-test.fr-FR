---
title: aaaAzure liste des comptes de stockage
description: "Gérer les paramètres de votre compte de stockage à l’aide de hello boîte à outils Azure pour Eclipse"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 35e25881ca95ae4050a26283e4726d9549b37f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-account-list"></a>Liste des comptes Azure Storage
Activer des comptes de stockage Azure télécharger toobe emplacements utilisé pour votre JDK, serveur d’applications et composants arbitraires, ainsi que pour stocker l’état lors de l’utilisation de la mise en cache. Eclipse conserve une liste des comptes de stockage connus qui sont des projets tooyour disponibles dans votre espace de travail Eclipse. tooopen hello **comptes de stockage** boîte de dialogue, qui est utilisé toomanage qui répertorient, dans Eclipse, cliquez sur **fenêtre**, cliquez sur **préférences**, développez **Azure** , puis cliquez sur **comptes de stockage**.

Hello Voici hello **comptes de stockage** boîte de dialogue.

![][ic719496]

Vous pouvez également ouvrir cette boîte de dialogue à partir d’un **comptes** lien dans les boîtes de dialogue qui utilisent des comptes de stockage, tels que les suivants hello :

* Hello **JDK** onglet Hello **Configuration du serveur** boîte de dialogue.
* Hello **Server** onglet Hello **Configuration du serveur** boîte de dialogue.
* Hello **ajouter un composant** boîte de dialogue.
* Hello **mise en cache** boîte de dialogue Propriétés.

## <a name="tooimport-your-storage-accounts-using-a-publish-settings-file"></a>tooimport des comptes de votre stockage en utilisant un fichier de paramètres de publication
1. Au sein de hello **comptes de stockage** boîte de dialogue, cliquez sur **importer à partir du fichier de paramètres de publication**.

2. (Ignorer cette étape si vous avez déjà enregistré un ordinateur local de publier les paramètres fichier tooyour). Bonjour **importation des informations d’abonnement** boîte de dialogue, cliquez sur **télécharger le fichier PUBLISH-SETTINGS**. Si vous n’êtes pas encore connecté à votre compte Azure, vous serez invité à toolog dans. Ensuite, vous êtes invité à entrer toosave Azure publier le fichier de paramètres. (Vous pouvez ignorer hello instructions sur les pages d’ouverture de session hello - ils sont fournis par hello portail Azure et sont destinées aux utilisateurs de Visual Studio) Enregistrez-le tooyour les ordinateur local.

3. Toujours en hello **importation des informations d’abonnement** boîte de dialogue, cliquez sur hello **Parcourir** bouton, hello sélectionnez Publier le fichier de paramètres que vous avez précédemment enregistré localement, puis cliquez sur **ouvrir**.

4. Cliquez sur **OK** tooclose hello **importation des informations d’abonnement** boîte de dialogue.

## <a name="toocreate-a-new-storage-account"></a>toocreate un compte de stockage
1. Au sein de hello **comptes de stockage** boîte de dialogue, cliquez sur **ajouter**.

2. Au sein de hello **ajouter un compte de stockage** boîte de dialogue, cliquez sur **nouveau**.

3. Au sein de hello **nouveau compte de stockage** boîte de dialogue, spécifiez des valeurs pour les éléments suivants de hello :

   * Nom du compte de stockage.

   * Emplacement du compte de stockage hello.

   * Description du compte de stockage hello.

   * compte de stockage Hello abonnement toowhich hello appartient.

4. Cliquez sur **OK** tooclose hello **nouveau compte de stockage** boîte de dialogue.

Il peut prendre plusieurs minutes avant que votre toobe de compte de stockage créé. Après sa création, cliquez sur **OK** tooclose hello **ajouter un compte de stockage** boîte de dialogue et votre compte de stockage seront ajouté toohello la liste des comptes de stockage disponibles.

## <a name="tooadd-an-existing-storage-account-toohello-list"></a>tooadd une liste de toohello de compte de stockage existant
1. Si vous ne figure pas un stockage Azure compte, créez-le en suivant les étapes de hello répertoriés dans hello **toocreate une nouvelle section de compte de stockage** ci-dessus. (Vous pouvez également créer un compte de stockage à hello [portail de gestion Azure][Azure Management Portal].)

2. Au sein de hello **comptes de stockage** boîte de dialogue, cliquez sur **ajouter**.

3. Au sein de hello **ajouter un compte de stockage** boîte de dialogue, entrez des valeurs pour **nom** et **clé d’accès**. clé d’accès et de nom de compte Hello doit être d’un compte de stockage Azure existant. Hello d’utilisation **stockage** section Hello [portail de gestion Azure] [ Azure Management Portal] tooview noms et des clés de votre compte de stockage. Votre **ajouter un compte de stockage** boîte de dialogue recherche similaire toohello suivant.
   
   ![][ic719497]

4. Cliquez sur **OK** tooclose hello **ajouter un compte de stockage** boîte de dialogue.

## <a name="toomodify-a-storage-account-toouse-a-new-access-key"></a>toomodify un toouse de compte de stockage une nouvelle clé d’accès
1. Au sein de hello **comptes de stockage** boîte de dialogue, cliquez sur le compte de stockage hello que vous souhaitez tooedit, puis sur **modifier**.

2. Au sein de hello **modifier compte clé d’accès** boîte de dialogue Modifier hello **clé d’accès** valeur.

3. Cliquez sur **OK** tooclose hello **clé de l’accès du compte de stockage modifier** boîte de dialogue.

## <a name="tooremove-a-storage-account-from-hello-list-maintained-in-eclipse"></a>tooremove un compte de stockage à partir de la liste d’Eclipse hello
1. Au sein de hello **comptes de stockage** boîte de dialogue, cliquez sur le compte de stockage hello que vous souhaitez tooedit, puis sur **supprimer**.

2. Cliquez sur **OK** lorsque tooremove demandée hello compte de stockage.

> [!NOTE]
> Suppression de compte de stockage hello via hello **comptes de stockage** dialogue supprime uniquement à partir de la liste de hello des comptes de stockage visibles dans Eclipse. Elle ne supprime pas le compte de stockage hello à partir de votre abonnement Azure. En outre, compte de stockage hello peut réapparaître dans votre liste lorsqu’Eclipse recharge les détails hello de votre abonnement.
> 
> 

## <a name="see-also"></a>Voir aussi
[Kit de ressources Azure pour Eclipse][Azure Toolkit for Eclipse]

[Lors de l’installation hello boîte à outils Azure pour Eclipse][Installing hello Azure Toolkit for Eclipse] 

[Création d’une application Hello World pour Azure dans Eclipse][Creating a Hello World Application for Azure in Eclipse]

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
