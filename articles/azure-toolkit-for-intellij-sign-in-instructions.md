---
title: Instructions de connexion pour le Kit de ressources Azure pour IntelliJ | Documents Microsoft
description: "Découvrez comment vous connecter à Microsoft Azure à l’aide du Kit de ressources Azure pour IntelliJ."
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
ms.openlocfilehash: 4e2ed072bdaea0a71fef042c0c72b7656a42bbe8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-intellij"></a>Instructions de connexion pour le Kit de ressources Azure pour IntelliJ

Le Kit de ressources Azure pour IntelliJ vous permet de vous connecter à votre compte Azure à l’aide de deux méthodes :

  * **Interactive**: vous entrez vos informations d’identification Azure chaque fois que vous vous connectez à votre compte Azure.
  * **Automatisée** : vous créez un fichier d’informations d’identification que vous pouvez utiliser pour vous connecter automatiquement à votre compte Azure.

Les sections suivantes décrivent comment utiliser chaque méthode.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-interactively"></a>Connexion à votre compte Azure de façon interactive

Pour vous connecter à Azure en entrant manuellement vos informations d’identification, procédez comme suit :

1. Ouvrez votre projet avec IntelliJ IDEA.

2. Cliquez sur **Outils**, pointez sur **Azure**, puis cliquez sur **Connexion à Microsoft Azure**.

   ![Commande IntelliJ de connexion à Azure][I01]

3. Dans la fenêtre **Connexion à Azure** qui s’affiche, sélectionnez **Interactive**, puis cliquez sur **Se connecter**.

   ![Fenêtre Connexion à Azure avec l’option Interactive activée][I02]

4. Dans la boîte de dialogue **Connexion à Azure** qui s’affiche, entrez vos informations d’identification Azure, puis cliquez sur **Se connecter**.

   ![Boîte de dialogue Connexion à Azure][I03]

5. Lorsque la boîte de dialogue **Sélectionner des abonnements**, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.

   ![Boîte de dialogue Sélectionner des abonnements][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a>Déconnexion de votre compte Azure après vous être connecté de manière interactive

Après que vous avez configuré votre compte en procédant de la manière décrite les étapes précédentes, vous êtes automatiquement déconnecté de votre compte Azure à chaque redémarrage d’IntelliJ IDEA. En revanche, si vous souhaitez vous déconnecter de votre compte Azure *sans* redémarrer IntelliJ IDEA, procédez comme suit.

1. Dans IntelliJ IDEA, dans le menu **Outils**, pointez sur **Azure**, puis cliquez sur **Déconnexion de Microsoft Azure**.

   ![Commande IntelliJ de déconnexion d’Azure][L01]

2. Dans la fenêtre de confirmation **e déconnecter de Microsoft Azure**, cliquez sur **Oui**.

   ![Fenêtre de confirmation de déconnexion d’Azure][L02]

## <a name="sign-in-to-your-azure-account-automatically"></a>Connexion automatique à votre compte Azure

Cette section vous guide dans la création d’un fichier d’informations d’identification contenant les données de votre principal de service. Une fois ce processus terminé, Eclipse utilise le fichier d’informations d’identification pour vous connecter automatiquement à Azure chaque fois que vous ouvrez votre projet.

1. Ouvrez votre projet avec IntelliJ IDEA.

2. Dans le menu **Outils**, pointez sur **Azure**, puis cliquez sur **Connexion à Microsoft Azure**.

   ![Commande IntelliJ de connexion à Azure][A01]

3. Dans la fenêtre **Connexion à Microsoft Azure**, sélectionnez **Automatisée**, puis cliquez sur **Nouveau**.

   ![Fenêtre Connexion à Microsoft Azure avec l’option Automatique activée][A02]

4. Dans la boîte de dialogue **Connexion à Azure** qui s’affiche, entrez vos informations d’identification Azure, puis cliquez sur **Se connecter**.

   ![Boîte de dialogue Connexion à Azure][A03]

5. Dans la fenêtre **Créer les fichiers d’authentification**, sélectionnez les abonnements que vous souhaitez utiliser, choisissez votre répertoire de destination, puis cliquez sur **Démarrer**.

   ![Fenêtre Créer les fichiers d’authentification][A04]

6. Dans la boîte de dialogue **État de création du principal de service** qui s’affiche, une fois vos fichiers créés, cliquez sur **OK**.

   ![Boîte de dialogue État de création du principal de service][A05]

7. Dans la fenêtre **Connexion à Microsoft Azure**, cliquez sur **Se connecter**.

   ![Boîte de dialogue Connexion à Azure][A06]

8. Lorsque la boîte de dialogue **Sélectionner des abonnements**, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.

   ![Boîte de dialogue Sélectionner des abonnements][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a>Déconnexion de votre compte Azure après vous être connecté automatiquement

Après que vous avez configuré votre compte en suivant la procédure précédente, le Kit de ressources Azure vous connecte automatiquement à votre compte Azure chaque fois que vous redémarrez IntelliJ IDEA. Toutefois, pour vous déconnecter de votre compte Azure et empêcher le Kit de ressources Azure de vous connecter automatiquement, procédez comme suit :

1. Dans IntelliJ IDEA, dans le menu **Outils**, pointez sur **Azure**, puis cliquez sur **Déconnexion de Microsoft Azure**.

   ![Commande IntelliJ de déconnexion d’Azure][L01]

2. Dans la fenêtre de confirmation **e déconnecter de Microsoft Azure**, cliquez sur **Oui**.

   ![Fenêtre de confirmation de déconnexion d’Azure][L03]

## <a name="sign-in-to-your-azure-account-automatically-by-using-an-existing-credentials-file"></a>Connexion automatique à votre compte Azure à l’aide d’un fichier d’informations d’identification existant

Si vous vous déconnectez de votre compte Azure alors que vous utilisez IntelliJ IDEA, vous devez utiliser un fichier d’informations d’identification existant pour vous reconnecter automatiquement au compte. Pour configurer le Kit de ressources Azure pour Eclipse afin d’utiliser un fichier d’informations d’identification existant, procédez comme suit :

1. Ouvrez votre projet avec IntelliJ IDEA.

2. Dans le menu **Outils**, pointez sur **Azure**, puis cliquez sur **Connexion à Microsoft Azure**.

   ![Commande IntelliJ de connexion à Azure][A01]

3. Dans la fenêtre **Connexion à Microsoft Azure**, sélectionnez **Automatisée**, puis cliquez sur **Parcourir**.

   ![Fenêtre Connexion à Microsoft Azure avec l’option Automatique activée][A02]

4. Dans la boîte de dialogue **Sélectionner le fichier d’authentification**, choisissez un fichier d’informations d’identification créé précédemment, puis cliquez sur **Sélectionner**.

   ![Boîte de dialogue Sélectionner le fichier d’authentification][A08]

5. Dans la fenêtre **Connexion à Microsoft Azure**, cliquez sur **Se connecter**.

   ![Fenêtre Connexion à Microsoft Azure avec l’option Automatique activée][A06]

6. Lorsque la boîte de dialogue **Sélectionner des abonnements**, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.

   ![Boîte de dialogue Sélectionner des abonnements][A07]

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les boîtes à outils Azure pour les environnements de développement Java, consultez les liens suivants :

* [Kit de ressources Azure pour Eclipse]
  * [Nouveautés du Kit de ressources Azure pour Eclipse]
  * [Installation du kit de ressources Azure pour Eclipse]
  * [Instructions de connexion pour le Kit de ressources Azure pour Eclipse]
  * [Créer une application web Hello World pour Azure dans Eclipse]
* [Kit de ressources Azure pour IntelliJ]
  * [Nouveautés du Kit de ressources Azure pour IntelliJ]
  * [Installation du kit de ressources Azure pour IntelliJ]
  * *Instructions de connexion pour le Kit de ressources Azure pour IntelliJ* (cet article)
  * [Créer une application web Hello World pour Azure dans IntelliJ]

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez le [Centre de développement Java pour Azure] et les [outils Java pour Visual Studio Team Services].

<!-- URL List -->

[Kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij.md
[Créer une application web Hello World pour Azure dans Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Créer une application web Hello World pour Azure dans IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installation du kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Installation du kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instructions de connexion pour le Kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Nouveautés du Kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Nouveautés du Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/
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
