---
title: "instructions d’aaaSign pour hello boîte à outils Azure pour IntelliJ | Documents Microsoft"
description: "Découvrez comment toosign dans tooMicrosoft Azure à l’aide de hello boîte à outils Azure pour IntelliJ."
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
ms.openlocfilehash: 2de781fc19267cce133b1e6456481497e165fce4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-instructions-for-hello-azure-toolkit-for-intellij"></a>Instructions d’authentification pour hello boîte à outils Azure pour IntelliJ

Bonjour Azure Toolkit pour IntelliJ propose deux méthodes pour établir la connexion tooyour compte Azure :

  * **Interactive**: vous permet d’entrer vos informations d’identification Azure chaque fois que vous vous connecterez dans tooyour compte Azure.
  * **Automatisée**: vous créez un fichier d’informations d’identification que vous pouvez utiliser l’authentification tooautomatically dans tooyour compte Azure.

Hello sections suivantes décrivent comment toouse chaque méthode.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-tooyour-azure-account-interactively"></a>Se connecter interactivement tooyour compte Azure

toosign dans tooAzure en entrant manuellement vos informations d’identification Azure, procédez comme hello suivant :

1. Ouvrez votre projet avec IntelliJ IDEA.

2. Cliquez sur **outils**, pointez trop**Azure**, puis cliquez sur **Azure Sign In**.

   ![Hello IntelliJ Azure signe de commandes][I01]

3. Bonjour **Azure Sign In** fenêtre, sélectionnez **Interactive**, puis cliquez sur **connectez-vous**.

   ![Bonjour Azure fenêtre de connexion avec Interactive sélectionné][I02]

4. Bonjour **Azure journal dans** boîte de dialogue s’affiche, entrez vos informations d’identification Azure, puis cliquez sur **connectez-vous**.

   ![fenêtre de boîte de dialogue de connexion Azure Hello][I03]

5. Bonjour **sélectionnez les abonnements** boîte de dialogue, les abonnements hello select que vous souhaitez toouse, puis cliquez sur **OK**.

   ![boîte de dialogue Sélectionnez les abonnements Hello][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a>Déconnexion de votre compte Azure après vous être connecté de manière interactive

Après avoir configuré votre compte à l’aide de hello étapes précédentes, vous allez être automatiquement déconnecté votre compte Azure, chaque fois que vous redémarrez IntelliJ idée. Toutefois, si vous souhaitez dans votre compte Azure toosign *sans* redémarrage IntelliJ idée, hello suivant.

1. Dans l’idée IntelliJ, hello **outils** menu, pointez trop**Azure**, puis cliquez sur **Azure se déconnecter**.

   ![Hello commande IntelliJ Azure se déconnecter][L01]

2. Bonjour **Azure se déconnecter** fenêtre de confirmation, cliquez sur **Oui**.

   ![fenêtre Hello Azure se déconnecter confirmation][L02]

## <a name="sign-in-tooyour-azure-account-automatically"></a>Se connecter automatiquement tooyour compte Azure

Cette section vous guide dans la création d’un fichier d’informations d’identification contenant les données de votre principal de service. Après avoir terminé ce processus, Eclipse utilise hello tooautomatically informations d’identification de fichier signe dans tooAzure chaque fois que vous ouvrez votre projet.

1. Ouvrez votre projet avec IntelliJ IDEA.

2. Sur hello **outils** menu, pointez trop**Azure**, puis cliquez sur **Azure Sign In**.

   ![Hello IntelliJ Azure signe de commandes][A01]

3. Bonjour **Azure Sign In** fenêtre, sélectionnez **automatisée**, puis cliquez sur **nouveau**.

   ![Bonjour Azure fenêtre de connexion avec automatisée sélectionnée][A02]

4. Bonjour **boîte de dialogue de connexion Azure** fenêtre, entrez vos informations d’identification Azure, puis cliquez sur **connectez-vous**.

   ![fenêtre de boîte de dialogue de connexion Azure Hello][A03]

5. Bonjour **créer des fichiers de l’authentification** (fenêtre), les abonnements hello select que vous souhaitez toouse, choisissez votre répertoire de destination, puis cliquez sur **Démarrer**.

   ![fenêtre Créer les fichiers d’authentification de Hello][A04]

6. Bonjour **état de la création de Principal du Service** boîte de dialogue, une fois que vos fichiers ont été créées avec succès, cliquez sur **OK**.

   ![Hello, boîte de dialogue État de la création de Principal du Service][A05]

7. Bonjour **Azure Sign In** fenêtre, cliquez sur **connectez-vous**.

   ![Boîte de dialogue Connexion à Azure][A06]

8. Bonjour **sélectionnez les abonnements** boîte de dialogue, les abonnements hello select que vous souhaitez toouse, puis cliquez sur **OK**.

   ![boîte de dialogue Sélectionnez les abonnements Hello][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a>Déconnexion de votre compte Azure après vous être connecté automatiquement

Après avoir configuré votre compte à l’aide des étapes précédentes de hello, hello boîte à outils Azure vous connecte automatiquement tooyour compte Azure, chaque fois que vous redémarrez IntelliJ idée. Toutefois, toosign hors de votre compte Azure et empêcher hello boîte à outils Azure à partir de la connexion automatique, hello suivant :

1. Dans l’idée IntelliJ, hello **outils** menu, pointez trop**Azure**, puis cliquez sur **Azure se déconnecter**.

   ![Hello commande IntelliJ Azure se déconnecter][L01]

2. Bonjour **Azure se déconnecter** fenêtre de confirmation, cliquez sur **Oui**.

   ![fenêtre Hello Azure se déconnecter confirmation][L03]

## <a name="sign-in-tooyour-azure-account-automatically-by-using-an-existing-credentials-file"></a>Connectez-vous tooyour compte Azure automatiquement à l’aide d’un fichier d’informations d’identification existant

Si vous vous déconnecter de votre compte Azure lorsque vous utilisez IntelliJ idée, vous devez utiliser un signe de tooautomatically du fichier d’informations d’identification existantes dans toohello compte. tooconfigure hello boîte à outils Azure pour Eclipse toouse un fichier d’informations d’identification existant, procédez comme hello suivant :

1. Ouvrez votre projet avec IntelliJ IDEA.

2. Sur hello **outils** menu, pointez trop**Azure**, puis cliquez sur **Azure Sign In**.

   ![Hello IntelliJ Azure signe de commandes][A01]

3. Bonjour **Azure Sign In** fenêtre, sélectionnez **automatisée**, puis cliquez sur **Parcourir**.

   ![Bonjour Azure fenêtre de connexion avec automatisée sélectionnée][A02]

4. Bonjour **sélectionner le fichier d’authentification** boîte de dialogue, sélectionnez un fichier d’informations d’identification créé précédemment, puis cliquez sur **sélectionnez**.

   ![boîte de dialogue Sélectionner le fichier d’authentification Hello][A08]

5. Bonjour **Azure Sign In** fenêtre, cliquez sur **connectez-vous**.

   ![Bonjour Azure fenêtre de connexion avec automatisée sélectionnée][A06]

6. Bonjour **sélectionnez les abonnements** boîte de dialogue, les abonnements hello select que vous souhaitez toouse, puis cliquez sur **OK**.

   ![boîte de dialogue Sélectionnez les abonnements Hello][A07]

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur hello boîtes à outils Azure pour Java IDE, consultez hello suivant liens :

* [boîte à outils Azure pour Eclipse]
  * [Nouveautés de hello boîte à outils Azure pour Eclipse]
  * [Lors de l’installation hello boîte à outils Azure pour Eclipse]
  * [Instructions de connexion pour hello boîte à outils Azure pour Eclipse]
  * [Créer une application web Hello World pour Azure dans Eclipse]
* [Kit de ressources Azure pour IntelliJ]
  * [Quelles sont les nouveautés Bonjour Azure Toolkit pour IntelliJ]
  * [Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]
  * *Instructions d’authentification pour hello boîte à outils Azure pour IntelliJ* (cet article)
  * [Créer une application web Hello World pour Azure dans IntelliJ]

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure] et hello [outils Java pour Visual Studio Team Services].

<!-- URL List -->

[boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij.md
[Créer une application web Hello World pour Azure dans Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Créer une application web Hello World pour Azure dans IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Lors de l’installation hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instructions de connexion pour hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign-in instructions for hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Nouveautés de hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Quelles sont les nouveautés Bonjour Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[centre de développement Java Azure]: https://azure.microsoft.com/develop/java/
[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
