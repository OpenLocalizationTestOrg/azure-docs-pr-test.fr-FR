---
title: "aaaInstalling hello boîte à outils Azure pour Eclipse | Documents Microsoft"
description: "Découvrez comment tooinstall hello boîte à outils Azure pour Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6c195fab2b47fb5c42541a8cf52be4ec88d27b5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="installing-hello-azure-toolkit-for-eclipse"></a>Lors de l’installation hello boîte à outils Azure pour Eclipse
Hello boîte à outils Azure pour Eclipse fournit des modèles et les fonctionnalités qui vous permettent de tooeasily créent, développer, tester et déployer des applications Azure à l’aide d’environnement de développement Eclipse hello. Hello boîte à outils Azure pour Eclipse est un projet Open Source. code source de Hello est disponible sous licence du MIT de hello de <https://github.com/microsoft/azure-tools-for-java>.

Hello suit vous montre comment tooinstall hello boîte à outils Azure pour Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="tooinstall-hello-azure-toolkit-for-eclipse"></a>tooinstall hello boîte à outils Azure pour Eclipse
1. Démarrez Eclipse.
2. Cliquez sur hello **aide** menu, puis sur **installer le nouveau logiciel**, comme indiqué dans hello après l’illustration.
   
    ![Lors de l’installation hello boîte à outils Azure pour Eclipse][01]
3. Bonjour **logiciels disponibles** boîte de dialogue, dans hello **travailler avec** zone de texte, tapez `http://dl.microsoft.com/eclipse` suivie hello **entrée** clé.
4. Bonjour **nom** volet, vérifiez **boîte à outils Azure pour Eclipse**, puis décochez **contacter sites au cours de mise à jour de l’installation toofind requis logiciel**. Votre écran doit ressembler similaire toohello suivantes :
   
    ![Lors de l’installation hello boîte à outils Azure pour Eclipse][02]
5. Si vous développez hello **boîte à outils Azure pour Eclipse**, vous verrez hello éléments suivants :
   
   * **Plug-in d’application Insights pour Java**: ce composant vous permet de services de journalisation et d’analyse de télémétrie pour vos applications et les instances de serveur de toouse Azure.
   * **Filtre Azure Access Control service**: ce composant prend en charge l’authentification des utilisateurs d’applications avec Azure ACS, l’activation de scénarios d’authentification uniques et externalisation logique d’identité à partir de l’application hello.
   * **Plug-in commun Azure**: ce composant fournit des fonctionnalités communes hello requises par d’autres composants de boîte à outils.
   * **Explorateur Azure pour Eclipse**: ce composant fournit des fonctionnalités communes hello requises par d’autres composants de boîte à outils.
   * **Plug-in Azure pour Eclipse avec Java**: ce composant prend en charge pour le développement de projets qui aident à créer, tester et déployer des applications Java pour le cloud de Microsoft Azure hello dans Eclipse et via la ligne de commande.
   * **Plug-in de l’applications Web Azure avec Java**: ce composant prend en charge pour le déploiement de conteneurs d’application Web Azure tooMicrosoft Java web applications.
   * **Microsoft JDBC Driver 4.2 for SQL Server**: ce composant fournit l’API JDBC pour SQL Server et Microsoft Azure SQL Database pour Java Platform Enterprise Edition 8.
   * **Package pour les bibliothèques de Client Qpid Apache pour JMS**: ce composant fournit le composant de client JMS hello de hello Apache Qpid projet tooenable votre toouse AMQP la messagerie dans Microsoft Azure.
   * **Package for Microsoft Azure Libraries for Java**: ce composant fournit des API pour accéder aux services Microsoft Azure, tels que Storage, Service Bus, le runtime de service, etc.
6. Cliquez sur **Suivant**. (Si vous rencontrez des délais d’attente inhabituels lors de l’installation des outils d’analyse hello, vérifiez que **contacter sites au cours de mise à jour de l’installation toofind requis logiciel** est désactivée.)
7. Bonjour **détails d’installation** boîte de dialogue, cliquez sur **suivant**.
   
    ![Passer en revue les détails de l’installation][03]
8. Bonjour **consulter les licences** boîte de dialogue, passez en revue les termes du contrat de hello hello de contrats de licence. Si vous acceptez les termes du contrat de hello hello de contrats de licence, cliquez sur **J’accepte les termes de hello hello de contrats de licence** puis cliquez sur **Terminer**. (les étapes restantes hello supposent que vous acceptez les termes de hello hello de contrats de licence. Si vous n’acceptez pas les termes du contrat de hello hello de contrats de licence, quitter le processus d’installation hello :)
   
    ![Review Licenses][04]
   
    Eclipse télécharge et installe les packages requis hello.
   
    ![Progression de l’installation][05]
9. Si vous y êtes invité installation de toocomplete toorestart Eclipse, cliquez sur **Oui**.
   
    ![Invite de redémarrage][06]

## <a name="see-also"></a>Voir aussi
Pour plus d’informations sur hello boîtes à outils Azure pour Java IDE, consultez hello suivant liens :

* [boîte à outils Azure pour Eclipse]
  * [Nouveautés dans hello boîte à outils Azure pour Eclipse]
  * *Lors de l’installation hello boîte à outils Azure pour Eclipse (Cet Article)*
  * [Authentification dans des Instructions pour hello boîte à outils Azure pour Eclipse]
  * [Créer une application web « Hello World » pour Azure dans Eclipse]
* [Kit de ressources Azure pour IntelliJ]
  * [Nouveautés dans hello Azure Toolkit pour IntelliJ]
  * [Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]
  * [Authentification dans des Instructions pour hello Azure Toolkit pour IntelliJ]
  * [Créer une application web « Hello World » pour Azure dans IntelliJ]

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure].

<!-- URL List -->

[boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij.md
[Créer une application web « Hello World » pour Azure dans Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Créer une application web « Hello World » pour Azure dans IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Authentification dans des Instructions pour hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Authentification dans des Instructions pour hello Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Nouveautés dans hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Nouveautés dans hello Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[centre de développement Java Azure]: https://azure.microsoft.com/develop/java/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->
