---
title: Installation du kit de ressources Azure pour Eclipse | Microsoft Docs
description: "Apprenez à installer le Kit de ressources Azure pour Eclipse."
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
ms.openlocfilehash: 35cddba38c364dfb2f6a8646b0014d48ca4cb795
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a>Installation du kit de ressources Azure pour Eclipse
Le kit de ressources Azure pour Eclipse contient des modèles et des fonctionnalités qui vous permettent de créer, de développer, de tester et de déployer des applications Azure avec l’environnement de développement Eclipse. Le kit de ressources Azure pour Eclipse est un projet Open Source. Le code source est disponible sous la licence du MIT à partir de <https://github.com/microsoft/azure-tools-for-java>.

Les étapes suivantes vous montrent comment installer le kit de ressources Azure pour Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a>Pour installer le Kit de ressources Azure pour Eclipse
1. Démarrez Eclipse.
2. Cliquez sur le menu **Help** (Aide), puis sur **Install New Software** (Installer un nouveau logiciel), comme indiqué dans l’illustration suivante.
   
    ![Installation du kit de ressources Azure pour Eclipse][01]
3. Dans la boîte de dialogue **Available Software** (Logiciels disponibles), dans la zone de texte **Work with** (Fonctionnement avec), tapez `http://dl.microsoft.com/eclipse`, puis appuyez sur la touche **Entrée**.
4. Dans le volet **Name** (Nom), cochez **Azure Toolkit for Eclipse** (Kit de ressources Azure pour Eclipse) et décochez **Contact all update sites during install to find required software** (Contacter tous les sites de mise à jour durant l'installation pour trouver le logiciel requis). Votre écran doit se présenter comme suit :
   
    ![Installation du kit de ressources Azure pour Eclipse][02]
5. Si vous développez le **Kit de ressources Azure pour Eclipse**, les éléments suivants apparaissent :
   
   * **Application Insights Plugin for Java**: ce composant vous permet d'utiliser les services de journalisation et d'analyse de télémétrie d'Azure pour vos applications et instances de serveur.
   * **Azure Access Control Services Filter**: ce composant prend en charge l’authentification des utilisateurs de l’application avec Azure ACS, permettant les scénarios d’authentification unique et l’externalisation de la logique d’identité hors de l’application.
   * **Azure Common Plugin**: ce composant fournit les fonctionnalités communes nécessaires aux autres composants du kit de ressources.
   * **Azure Explorer for Eclipse**: ce composant fournit les fonctionnalités communes nécessaires aux autres composants du kit de ressources.
   * **Azure Plugin for Eclipse with Java**: ce composant prend en charge le développement de projets qui aident à générer, tester et déployer des applications Java pour le cloud Microsoft Azure dans Eclipse et par le biais de la ligne de commande.
   * **Azure Web Apps Plugin with Java**: ce composant prend en charge le déploiement d’applications web Java sur des conteneurs d’application web Microsoft Azure.
   * **Microsoft JDBC Driver 4.2 for SQL Server**: ce composant fournit l’API JDBC pour SQL Server et Microsoft Azure SQL Database pour Java Platform Enterprise Edition 8.
   * **Package for Apache Qpid Client Libraries for JMS**: ce composant fournit le composant client JMS du projet Apache Qpid pour permettre à votre application d’utiliser la messagerie AMQP dans Microsoft Azure.
   * **Package for Microsoft Azure Libraries for Java**: ce composant fournit des API pour accéder aux services Microsoft Azure, tels que Storage, Service Bus, le runtime de service, etc.
6. Cliquez sur **Suivant**. (Si vous rencontrez des délais d'attente inhabituels lors de l'installation du kit de ressources, assurez-vous que l'option **Contact all update sites during install to find required software** est désactivée.)
7. Dans la boîte de dialogue **Install Details** (Détails d’installation), cliquez sur **Next** (Suivant).
   
    ![Passer en revue les détails de l’installation][03]
8. Dans la boîte de dialogue **Review Licenses** (Vérifier les licences), passez en revue les termes des contrats de licence. Si vous acceptez les termes des contrats de licence, cliquez sur **I accept the terms of the license agreements** (J’accepte les termes des contrats de licence), puis sur **Finish** (Terminer). (Les étapes restantes supposent que vous acceptez les termes des contrats de licence. Si vous n'acceptez pas les termes des contrats de licence, quittez le processus d'installation.)
   
    ![Review Licenses][04]
   
    Eclipse télécharge et installe les packages requis.
   
    ![Progression de l’installation][05]
9. Si vous êtes invité à redémarrer Eclipse pour terminer l’installation, cliquez sur **Yes**(Oui).
   
    ![Invite de redémarrage][06]

## <a name="see-also"></a>Voir aussi
Pour plus d’informations sur les boîtes à outils Azure pour les environnements de développement Java, consultez les liens suivants :

* [Kit de ressources Azure pour Eclipse]
  * [Nouveautés du kit de ressources Azure pour Eclipse]
  * *Installation du kit de ressources Azure pour Eclipse*
  * [Azure Sign In Instructions for the Azure Toolkit for Eclipse] (Instructions de connexion à Azure pour le kit de ressources Azure pour Eclipse)
  * [Créer une application web « Hello World » pour Azure dans Eclipse]
* [Kit de ressources Azure pour IntelliJ]
  * [Nouveautés du Kit de ressources Azure pour IntelliJ]
  * [Installation du kit de ressources Azure pour IntelliJ]
  * [Instructions de connexion à Azure pour le kit de ressources Azure pour IntelliJ]
  * [Créer une application web « Hello World » pour Azure dans IntelliJ]

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez le [Centre de développement Java pour Azure].

<!-- URL List -->

[Kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij.md
[Créer une application web « Hello World » pour Azure dans Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Créer une application web « Hello World » pour Azure dans IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Installation du kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Azure Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Instructions de connexion à Azure pour le kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Nouveautés du kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Nouveautés du Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->
