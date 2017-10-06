---
title: "aaaSign dans des Instructions pour hello boîte à outils Azure pour Eclipse | Documents Microsoft"
description: "Découvrez comment toosign dans Microsoft Azure à l’aide de hello boîte à outils Azure pour Eclipse."
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
ms.openlocfilehash: 95be64750ca0147f76dae8f364fad80cb9ccc969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sign-in-instructions-for-hello-azure-toolkit-for-eclipse"></a>Connexion Azure dans des Instructions pour hello boîte à outils Azure pour Eclipse

Hello boîte à outils Azure pour Eclipse fournit deux méthodes pour la connexion à votre compte Azure :

  * **Interactive** : si vous utilisez cette méthode, vous devez entrer vos informations d’identification Azure à chaque fois que vous vous connectez à votre compte Azure.
  * **Automatisée** - lorsque vous utilisez cette méthode, vous allez créer un fichier d’informations d’identification qui contient vos données de principal du service, après laquelle vous pouvez utiliser le signe de tooautomatically fichier hello informations d’identification à votre compte Azure.

Hello étapes Bonjour les sections suivantes décrivent comment toouse chaque méthode.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a>Connexion interactive à votre compte Azure

Hello suit illustre comment toosign dans Azure en entrant manuellement vos informations d’identification Azure.

1. Ouvrez votre projet avec Eclipse.

1. Cliquez successivement sur **Outils**, **Azure** et **Se connecter**.

   ![Menu d’Eclipse pour la connexion à Azure][I01]

1. Hello lorsque **Azure Sign In** boîte de dialogue s’affiche, sélectionnez **Interactive**, puis cliquez sur **connexion**.

   ![Boîte de dialogue Se connecter][I02]

1. Hello lorsque **Azure journal dans** boîte de dialogue s’affiche, entrez vos informations d’identification Azure, puis cliquez sur **connexion**.

   ![Boîte de dialogue Connexion à Azure][I03]

1. Hello lorsque **sélectionnez les abonnements** boîte de dialogue s’affiche, abonnements hello select que vous souhaitez toouse, puis cliquez sur **OK**.

   ![Boîte de dialogue Sélectionner des abonnements][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a>Déconnexion de votre compte Azure lorsque vous vous êtes connecté de manière interactive

Après avoir configuré les étapes hello dans la section précédente de hello, sera automatiquement déconnecté de votre compte Azure, chaque fois que vous redémarrez Eclipse. Toutefois, si vous souhaitez toosign hors de votre compte Azure sans avoir à redémarrer Eclipse, utilisez hello comme suit.

1. Dans Eclipse, cliquez successivement sur **Outils**, **Azure** et **Se déconnecter**.

   ![Menu d’Eclipse pour la déconnexion d’Azure][L01]

1. Hello lorsque **Azure se déconnecter** boîte de dialogue s’affiche, cliquez sur **Oui**.

   ![Boîte de dialogue Se déconnecter][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-toouse-in-hello-future"></a>Connecter automatiquement à votre compte Azure et la création d’un informations d’identification de fichier toouse Bonjour future

Hello étapes suivantes vous guidera dans la création d’un fichier d’informations d’identification qui contient vos données de principal du service. Une fois que vous avez terminé ces étapes, la volonté d’Eclipse automatiquement utilisez hello informations d’identification de fichier tooautomatically signe que vous dans Azure chaque fois que vous ouvrez votre projet.

1. Ouvrez votre projet avec Eclipse.

1. Cliquez successivement sur **Outils**, **Azure** et **Se connecter**.

   ![Menu d’Eclipse pour la connexion à Azure][A01]

1. Hello lorsque **Azure Sign In** boîte de dialogue s’affiche, sélectionnez **automatisée**, puis cliquez sur **nouveau**.

   ![Boîte de dialogue Se connecter][A02]

1. Hello lorsque **Azure journal dans** boîte de dialogue s’affiche, entrez vos informations d’identification Azure, puis cliquez sur **connexion**.

   ![Boîte de dialogue Connexion à Azure][A03]

1. Hello lorsque **créer les fichiers d’authentification** boîte de dialogue s’affiche, abonnements hello select que vous souhaitez toouse, choisissez votre répertoire de destination, puis cliquez sur **Démarrer**.

   ![Boîte de dialogue Connexion à Azure][A04]

1. Hello **état de création d’un système Principal du Service** boîte de dialogue s’affiche et une fois que vos fichiers ont été créées avec succès, cliquez sur **OK**.

   ![Boîte de dialogue Service Principal Creation Status (État de création du principal de service)][A05]

1. Hello lorsque **Azure Sign In** boîte de dialogue s’affiche, cliquez sur **connexion**.

   ![Boîte de dialogue Connexion à Azure][A06]

1. Hello lorsque **sélectionnez les abonnements** boîte de dialogue s’affiche, abonnements hello select que vous souhaitez toouse, puis cliquez sur **OK**.

   ![Boîte de dialogue Sélectionner des abonnements][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a>Déconnexion de votre compte Azure lorsque vous vous êtes connecté automatiquement

Après avoir configuré les étapes hello dans la section précédente de hello, hello boîte à outils Azure sera automatiquement connecté à votre compte Azure, chaque fois que vous redémarrez Eclipse. Toutefois, toosign hors de votre compte Azure et hello boîte à outils Azure empêche de vous connecter automatiquement, utilisez les hello comme suit.

1. Dans Eclipse, cliquez successivement sur **Outils**, **Azure** et **Se déconnecter**.

   ![Menu d’Eclipse pour la déconnexion d’Azure][L01]

1. Hello lorsque **Azure se déconnecter** boîte de dialogue s’affiche, cliquez sur **Oui**.

   ![Boîte de dialogue Se déconnecter][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a>Connexion automatique à votre compte Azure et utilisation d’un fichier d’informations d’identification que vous avez déjà créé

Si vous vous connectez en dehors d’Azure lorsque vous utilisez Eclipse, vous devez tooreconfigure hello boîte à outils Azure pour Eclipse toouse un fichier d’informations d’identification qui ont créé avant de vous connecter automatiquement à votre compte Azure. Hello étapes suivantes vous guidera dans la configuration toouse de boîte à outils Azure hello un fichier d’informations d’identification existant.

1. Ouvrez votre projet avec Eclipse.

1. Cliquez successivement sur **Outils**, **Azure** et **Se connecter**.

   ![Menu d’Eclipse pour la connexion à Azure][A01]

1. Hello lorsque **Azure Sign In** boîte de dialogue s’affiche, sélectionnez **automatisée**, puis cliquez sur **Parcourir**.

   ![Boîte de dialogue Se connecter][A02]

1. Hello lorsque **sélectionner le fichier authentifié** boîte de dialogue s’affiche, sélectionnez un fichier d’informations d’identification que vous avez créé précédemment, puis cliquez sur **sélectionnez**.

   ![Boîte de dialogue Se connecter][A08]

1. Hello lorsque **Azure Sign In** boîte de dialogue s’affiche, cliquez sur **connexion**.

   ![Boîte de dialogue Connexion à Azure][A06]

1. Hello lorsque **sélectionnez les abonnements** boîte de dialogue s’affiche, abonnements hello select que vous souhaitez toouse, puis cliquez sur **OK**.

   ![Boîte de dialogue Sélectionner des abonnements][A07]

## <a name="see-also"></a>Voir aussi
Pour plus d’informations sur hello boîtes à outils Azure pour Java IDE, consultez hello suivant liens :

* [boîte à outils Azure pour Eclipse]
  * [Nouveautés dans hello boîte à outils Azure pour Eclipse]
  * [Lors de l’installation hello boîte à outils Azure pour Eclipse]
  * *Authentification dans des Instructions pour hello boîte à outils Azure pour Eclipse (Cet Article)*
  * [Créer une application web « Hello World » pour Azure dans Eclipse]
* [Kit de ressources Azure pour IntelliJ]
  * [Nouveautés dans hello Azure Toolkit pour IntelliJ]
  * [Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]
  * [Authentification dans des Instructions pour hello Azure Toolkit pour IntelliJ]
  * [Créer une application web « Hello World » pour Azure dans IntelliJ]

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure] et hello [outils Java pour Visual Studio Team Services].

<!-- URL List -->

[boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij.md
[Créer une application web « Hello World » pour Azure dans Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Créer une application web « Hello World » pour Azure dans IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Lors de l’installation hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Sign In Instructions for hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Authentification dans des Instructions pour hello Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Nouveautés dans hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Nouveautés dans hello Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[centre de développement Java Azure]: https://azure.microsoft.com/develop/java/
[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
