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
# <a name="installing-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="5bba9-103">Installation du kit de ressources Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="5bba9-103">Installing the Azure Toolkit for Eclipse</span></span>
<span data-ttu-id="5bba9-104">Le kit de ressources Azure pour Eclipse contient des modèles et des fonctionnalités qui vous permettent de créer, de développer, de tester et de déployer des applications Azure avec l’environnement de développement Eclipse.</span><span class="sxs-lookup"><span data-stu-id="5bba9-104">The Azure Toolkit for Eclipse provides templates and functionality that allow you to easily create, develop, test, and deploy Azure applications using the Eclipse development environment.</span></span> <span data-ttu-id="5bba9-105">Le kit de ressources Azure pour Eclipse est un projet Open Source.</span><span class="sxs-lookup"><span data-stu-id="5bba9-105">The Azure Toolkit for Eclipse is an Open Source project.</span></span> <span data-ttu-id="5bba9-106">Le code source est disponible sous la licence du MIT à partir de <https://github.com/microsoft/azure-tools-for-java>.</span><span class="sxs-lookup"><span data-stu-id="5bba9-106">The source code is available under the MIT License from <https://github.com/microsoft/azure-tools-for-java>.</span></span>

<span data-ttu-id="5bba9-107">Les étapes suivantes vous montrent comment installer le kit de ressources Azure pour Eclipse.</span><span class="sxs-lookup"><span data-stu-id="5bba9-107">The following steps show you how to install the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="5bba9-108">Pour installer le Kit de ressources Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="5bba9-108">To install the Azure Toolkit for Eclipse</span></span>
1. <span data-ttu-id="5bba9-109">Démarrez Eclipse.</span><span class="sxs-lookup"><span data-stu-id="5bba9-109">Start Eclipse.</span></span>
2. <span data-ttu-id="5bba9-110">Cliquez sur le menu **Help** (Aide), puis sur **Install New Software** (Installer un nouveau logiciel), comme indiqué dans l’illustration suivante.</span><span class="sxs-lookup"><span data-stu-id="5bba9-110">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>
   
    ![Installation du kit de ressources Azure pour Eclipse][01]
3. <span data-ttu-id="5bba9-112">Dans la boîte de dialogue **Available Software** (Logiciels disponibles), dans la zone de texte **Work with** (Fonctionnement avec), tapez `http://dl.microsoft.com/eclipse`, puis appuyez sur la touche **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="5bba9-112">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse` followed by the **Enter** key.</span></span>
4. <span data-ttu-id="5bba9-113">Dans le volet **Name** (Nom), cochez **Azure Toolkit for Eclipse** (Kit de ressources Azure pour Eclipse) et décochez **Contact all update sites during install to find required software** (Contacter tous les sites de mise à jour durant l'installation pour trouver le logiciel requis).</span><span class="sxs-lookup"><span data-stu-id="5bba9-113">In the **Name** pane, check **Azure Toolkit for Eclipse**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="5bba9-114">Votre écran doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="5bba9-114">Your screen should appear similar to the following:</span></span>
   
    ![Installation du kit de ressources Azure pour Eclipse][02]
5. <span data-ttu-id="5bba9-116">Si vous développez le **Kit de ressources Azure pour Eclipse**, les éléments suivants apparaissent :</span><span class="sxs-lookup"><span data-stu-id="5bba9-116">If you expand the **Azure Toolkit for Eclipse**, you will see the following items:</span></span>
   
   * <span data-ttu-id="5bba9-117">**Application Insights Plugin for Java**: ce composant vous permet d'utiliser les services de journalisation et d'analyse de télémétrie d'Azure pour vos applications et instances de serveur.</span><span class="sxs-lookup"><span data-stu-id="5bba9-117">**Application Insights Plugin for Java**: This component allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span>
   * <span data-ttu-id="5bba9-118">**Azure Access Control Services Filter**: ce composant prend en charge l’authentification des utilisateurs de l’application avec Azure ACS, permettant les scénarios d’authentification unique et l’externalisation de la logique d’identité hors de l’application.</span><span class="sxs-lookup"><span data-stu-id="5bba9-118">**Azure Access Control Services Filter**: This component provides support for authenticating application users with Azure ACS, enabling single sign-on scenarios and externalizing identity logic from the application.</span></span>
   * <span data-ttu-id="5bba9-119">**Azure Common Plugin**: ce composant fournit les fonctionnalités communes nécessaires aux autres composants du kit de ressources.</span><span class="sxs-lookup"><span data-stu-id="5bba9-119">**Azure Common Plugin**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="5bba9-120">**Azure Explorer for Eclipse**: ce composant fournit les fonctionnalités communes nécessaires aux autres composants du kit de ressources.</span><span class="sxs-lookup"><span data-stu-id="5bba9-120">**Azure Explorer for Eclipse**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="5bba9-121">**Azure Plugin for Eclipse with Java**: ce composant prend en charge le développement de projets qui aident à générer, tester et déployer des applications Java pour le cloud Microsoft Azure dans Eclipse et par le biais de la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="5bba9-121">**Azure Plugin for Eclipse with Java**: This component provides support for developing projects that help build, test and deploy Java applications for the Microsoft Azure cloud in Eclipse and via command line.</span></span>
   * <span data-ttu-id="5bba9-122">**Azure Web Apps Plugin with Java**: ce composant prend en charge le déploiement d’applications web Java sur des conteneurs d’application web Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5bba9-122">**Azure Web Apps Plugin with Java**: This component provides support for deploying Java web applications to Microsoft Azure Web App containers.</span></span>
   * <span data-ttu-id="5bba9-123">**Microsoft JDBC Driver 4.2 for SQL Server**: ce composant fournit l’API JDBC pour SQL Server et Microsoft Azure SQL Database pour Java Platform Enterprise Edition 8.</span><span class="sxs-lookup"><span data-stu-id="5bba9-123">**Microsoft JDBC Driver 4.2 for SQL Server**: This component provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span>
   * <span data-ttu-id="5bba9-124">**Package for Apache Qpid Client Libraries for JMS**: ce composant fournit le composant client JMS du projet Apache Qpid pour permettre à votre application d’utiliser la messagerie AMQP dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5bba9-124">**Package for Apache Qpid Client Libraries for JMS**: This component provides the JMS client component from the Apache Qpid project to enable your application to use AMQP messaging in Microsoft Azure.</span></span>
   * <span data-ttu-id="5bba9-125">**Package for Microsoft Azure Libraries for Java**: ce composant fournit des API pour accéder aux services Microsoft Azure, tels que Storage, Service Bus, le runtime de service, etc.</span><span class="sxs-lookup"><span data-stu-id="5bba9-125">**Package for Microsoft Azure Libraries for Java**: This component provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span>
6. <span data-ttu-id="5bba9-126">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="5bba9-126">Click **Next**.</span></span> <span data-ttu-id="5bba9-127">(Si vous rencontrez des délais d'attente inhabituels lors de l'installation du kit de ressources, assurez-vous que l'option **Contact all update sites during install to find required software** est désactivée.)</span><span class="sxs-lookup"><span data-stu-id="5bba9-127">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>
7. <span data-ttu-id="5bba9-128">Dans la boîte de dialogue **Install Details** (Détails d’installation), cliquez sur **Next** (Suivant).</span><span class="sxs-lookup"><span data-stu-id="5bba9-128">In the **Install Details** dialog, click **Next**.</span></span>
   
    ![Passer en revue les détails de l’installation][03]
8. <span data-ttu-id="5bba9-130">Dans la boîte de dialogue **Review Licenses** (Vérifier les licences), passez en revue les termes des contrats de licence.</span><span class="sxs-lookup"><span data-stu-id="5bba9-130">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="5bba9-131">Si vous acceptez les termes des contrats de licence, cliquez sur **I accept the terms of the license agreements** (J’accepte les termes des contrats de licence), puis sur **Finish** (Terminer).</span><span class="sxs-lookup"><span data-stu-id="5bba9-131">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="5bba9-132">(Les étapes restantes supposent que vous acceptez les termes des contrats de licence.</span><span class="sxs-lookup"><span data-stu-id="5bba9-132">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="5bba9-133">Si vous n'acceptez pas les termes des contrats de licence, quittez le processus d'installation.)</span><span class="sxs-lookup"><span data-stu-id="5bba9-133">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>
   
    ![Review Licenses][04]
   
    <span data-ttu-id="5bba9-135">Eclipse télécharge et installe les packages requis.</span><span class="sxs-lookup"><span data-stu-id="5bba9-135">Eclipse will download and install the requisite packages.</span></span>
   
    ![Progression de l’installation][05]
9. <span data-ttu-id="5bba9-137">Si vous êtes invité à redémarrer Eclipse pour terminer l’installation, cliquez sur **Yes**(Oui).</span><span class="sxs-lookup"><span data-stu-id="5bba9-137">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>
   
    ![Invite de redémarrage][06]

## <a name="see-also"></a><span data-ttu-id="5bba9-139">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="5bba9-139">See Also</span></span>
<span data-ttu-id="5bba9-140">Pour plus d’informations sur les boîtes à outils Azure pour les environnements de développement Java, consultez les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="5bba9-140">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="5bba9-141">[Kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5bba9-141">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5bba9-142">[Nouveautés du kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5bba9-142">[What's New in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5bba9-143">*Installation du kit de ressources Azure pour Eclipse*</span><span class="sxs-lookup"><span data-stu-id="5bba9-143">*Installing the Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="5bba9-144">[Azure Sign In Instructions for the Azure Toolkit for Eclipse] (Instructions de connexion à Azure pour le kit de ressources Azure pour Eclipse)</span><span class="sxs-lookup"><span data-stu-id="5bba9-144">[Sign In Instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5bba9-145">[Créer une application web « Hello World » pour Azure dans Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5bba9-145">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="5bba9-146">[Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="5bba9-146">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5bba9-147">[Nouveautés du Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="5bba9-147">[What's New in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5bba9-148">[Installation du kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="5bba9-148">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5bba9-149">[Instructions de connexion à Azure pour le kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="5bba9-149">[Sign In Instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5bba9-150">[Créer une application web « Hello World » pour Azure dans IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="5bba9-150">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="5bba9-151">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez le [Centre de développement Java pour Azure].</span><span class="sxs-lookup"><span data-stu-id="5bba9-151">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="5bba9-152">[Kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="5bba9-152">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="5bba9-153">[Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="5bba9-153">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="5bba9-154">[Créer une application web « Hello World » pour Azure dans Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="5bba9-154">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="5bba9-155">[Créer une application web « Hello World » pour Azure dans IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="5bba9-155">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
<span data-ttu-id="5bba9-156">[Installation du kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="5bba9-156">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="5bba9-157">[Azure Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="5bba9-157">[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="5bba9-158">[Instructions de connexion à Azure pour le kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="5bba9-158">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="5bba9-159">[Nouveautés du kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="5bba9-159">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="5bba9-160">[Nouveautés du Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="5bba9-160">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="5bba9-161">[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="5bba9-161">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->
