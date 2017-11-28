---
title: "Création d’une application web dans Azure App Service à l’aide du Kit de développement logiciel (SDK) Azure pour Java"
description: "Apprenez à créer une application web sur Azure App Service par programme à l’aide du Kit de développement logiciel (SDK) Azure pour Java."
tags: azure-classic-portal
services: app-service-web
documentationcenter: Java
author: donntrenton
manager: erikre
editor: jimbe
ms.assetid: 8954c456-1275-4d57-aff4-ca7d6374b71e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/25/2016
ms.author: v-donntr
ms.openlocfilehash: 08bb53de8cf437a5a2b1c3b38bce9f81b8349493
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-the-azure-sdk-for-java"></a><span data-ttu-id="83942-103">Création d’une application web dans Azure App Service à l’aide du Kit de développement logiciel (SDK) Azure pour Java</span><span class="sxs-lookup"><span data-stu-id="83942-103">Create a Web App in Azure App Service using the Azure SDK for Java</span></span>
<!-- Azure Active Directory workflow is not yet available on the Azure Portal -->

## <a name="overview"></a><span data-ttu-id="83942-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="83942-104">Overview</span></span>
<span data-ttu-id="83942-105">Cette procédure pas à pas vous montre comment créer un Kit de développement logiciel (SDK) Azure pour une application Java qui crée une application web dans [Azure App Service][Azure App Service], puis comment déployer une application vers celle-ci.</span><span class="sxs-lookup"><span data-stu-id="83942-105">This walkthrough shows you how to create an Azure SDK for Java application that creates a Web App in [Azure App Service][Azure App Service], then deploy an application to it.</span></span> <span data-ttu-id="83942-106">Elle comprend deux parties :</span><span class="sxs-lookup"><span data-stu-id="83942-106">It consists of two parts:</span></span>

* <span data-ttu-id="83942-107">La première partie montre comment créer une application Java qui crée une application web.</span><span class="sxs-lookup"><span data-stu-id="83942-107">Part 1 demonstrates how to build a Java application that creates a web app.</span></span>
* <span data-ttu-id="83942-108">La deuxième partie montre comment créer une simple application JSP « Hello World » , puis utiliser un client FTP pour déployer le code sur App Service.</span><span class="sxs-lookup"><span data-stu-id="83942-108">Part 2 demonstrates how to create a simple JSP "Hello World" application, then use an FTP client to deploy code to App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83942-109">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="83942-109">Prerequisites</span></span>
### <a name="software-installations"></a><span data-ttu-id="83942-110">Installations de logiciels</span><span class="sxs-lookup"><span data-stu-id="83942-110">Software Installations</span></span>
<span data-ttu-id="83942-111">Le code d'application AzureWebDemo dans cet article a été écrit à l'aide du Kit de développement logiciel (SDK) Azure Java 0.7.0, que vous pouvez installer à l'aide de [Web Platform Installer][Web Platform Installer] (WebPI).</span><span class="sxs-lookup"><span data-stu-id="83942-111">The AzureWebDemo application code in this article was written using Azure Java SDK 0.7.0, which you can install using the [Web Platform Installer][Web Platform Installer] (WebPI).</span></span> <span data-ttu-id="83942-112">En outre, veillez à utiliser la dernière version de la [boîte à outils Azure pour Eclipse][Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="83942-112">In addition, make sure to use the latest version of the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="83942-113">Après avoir installé le Kit de développement logiciel (SDK), mettez à jour les dépendances de votre projet Eclipse en exécutant **Mettre à jour l’index** dans les **référentiels Maven**, puis ajoutez de nouveau la version la plus récente de chaque package dans la fenêtre **Dépendances**.</span><span class="sxs-lookup"><span data-stu-id="83942-113">After you install the SDK, update the dependencies in your Eclipse project by running **Update Index** in **Maven Repositories**, then re-add the latest version of each package in the **Dependencies** window.</span></span> <span data-ttu-id="83942-114">Vous pouvez vérifier la version de votre logiciel installé dans Eclipse en cliquant sur **Aide > Détails de l’installation** ; vous devez avoir au moins les versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="83942-114">You can verify the version of your installed software in Eclipse by clicking **Help > Installation Details**; you should have at least the following versions:</span></span>

* <span data-ttu-id="83942-115">Package pour les bibliothèques Microsoft Azure pour Java 0.7.0.20150309</span><span class="sxs-lookup"><span data-stu-id="83942-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span></span>
* <span data-ttu-id="83942-116">Environnement de développement intégré (IDE) Eclipse pour développeurs Java EE 4.4.2.20150219</span><span class="sxs-lookup"><span data-stu-id="83942-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span></span>

### <a name="create-and-configure-cloud-resources-in-azure"></a><span data-ttu-id="83942-117">Création et configuration de ressources de cloud dans Azure</span><span class="sxs-lookup"><span data-stu-id="83942-117">Create and Configure Cloud Resources in Azure</span></span>
<span data-ttu-id="83942-118">Avant de commencer cette procédure, vous devez disposer d’un abonnement Azure actif et définir une valeur Active Directory (AD) par défaut sur Azure.</span><span class="sxs-lookup"><span data-stu-id="83942-118">Before you begin this procedure, you need to have an active Azure subscription and set up a default Active Directory (AD) on Azure.</span></span>

### <a name="create-an-active-directory-ad-in-azure"></a><span data-ttu-id="83942-119">Création d’un annuaire Active Directory (AD) dans Azure</span><span class="sxs-lookup"><span data-stu-id="83942-119">Create an Active Directory (AD) in Azure</span></span>
<span data-ttu-id="83942-120">Si vous ne disposez pas déjà d’un annuaire Active Directory (AD) dans votre abonnement Azure, connectez-vous au [Portail Azure Classic][Azure classic portal] avec votre compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="83942-120">If you do not already have an Active Directory (AD) on your Azure subscription, log into the [Azure classic portal][Azure classic portal] with your Microsoft account.</span></span> <span data-ttu-id="83942-121">Si vous disposez de plusieurs abonnements, cliquez sur **Abonnements** et sélectionnez l’annuaire par défaut pour l’abonnement que vous souhaitez utiliser pour ce projet.</span><span class="sxs-lookup"><span data-stu-id="83942-121">If you have multiple subscriptions, click **Subscriptions** and select the default directory for the subscription you want to use for this project.</span></span> <span data-ttu-id="83942-122">Cliquez sur **Appliquer** pour basculer vers cette vue d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="83942-122">Then click **Apply** to switch to that subscription view.</span></span>

1. <span data-ttu-id="83942-123">Sélectionnez **Active Directory** dans le menu à gauche.</span><span class="sxs-lookup"><span data-stu-id="83942-123">Select **Active Directory** from the menu at left.</span></span> <span data-ttu-id="83942-124">**Cliquez sur Nouveau > Annuaire > Création personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="83942-124">**Click New > Directory > Custom Create**.</span></span>
2. <span data-ttu-id="83942-125">Dans **Ajouter un annuaire**, sélectionnez **Créer un nouvel annuaire**.</span><span class="sxs-lookup"><span data-stu-id="83942-125">In **Add Directory**, select **Create New Directory**.</span></span>
3. <span data-ttu-id="83942-126">Dans **Nom**, entrez un nom d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="83942-126">In **Name**, enter a directory name.</span></span>
4. <span data-ttu-id="83942-127">Dans **Domaine**, entrez un nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="83942-127">In **Domain**, enter a domain name.</span></span> <span data-ttu-id="83942-128">Il s’agit d’un nom de domaine de base qui est inclus par défaut avec votre annuaire ; il se présente sous la forme `<domain_name>.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="83942-128">This is a basic domain name that is included by default with your directory; it has the form `<domain_name>.onmicrosoft.com`.</span></span> <span data-ttu-id="83942-129">Vous pouvez définir son nom sur la base du nom d’annuaire ou d’un autre nom de domaine que vous possédez.</span><span class="sxs-lookup"><span data-stu-id="83942-129">You can name it based on the directory name or another domain name that you own.</span></span> <span data-ttu-id="83942-130">Par la suite, vous pouvez ajouter un autre nom de domaine que votre organisation utilise déjà.</span><span class="sxs-lookup"><span data-stu-id="83942-130">Later, you can add another domain name that your organization already uses.</span></span>
5. <span data-ttu-id="83942-131">Dans **Pays ou région**, sélectionnez votre paramètre régional.</span><span class="sxs-lookup"><span data-stu-id="83942-131">In **Country or region**, select your locale.</span></span>

<span data-ttu-id="83942-132">Pour plus d'informations sur AD, consultez la page [Qu'est-ce qu'un annuaire Azure AD][What is an Azure AD directory]?</span><span class="sxs-lookup"><span data-stu-id="83942-132">For more information on AD, see [What is an Azure AD directory][What is an Azure AD directory]?</span></span>

### <a name="create-a-management-certificate-for-azure"></a><span data-ttu-id="83942-133">Création d’un certificat de gestion pour Azure</span><span class="sxs-lookup"><span data-stu-id="83942-133">Create a Management Certificate for Azure</span></span>
<span data-ttu-id="83942-134">Le Kit de développement logiciel (SDK) Azure pour Java utilise des certificats de gestion pour s’authentifier avec des abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="83942-134">The Azure SDK for Java uses management certificates to authenticate with Azure subscriptions.</span></span> <span data-ttu-id="83942-135">Il s’agit de certificats X.509 v3 vous permettant d’authentifier une application cliente qui utilise l’API Gestion des services pour agir au nom du propriétaire de l’abonnement afin de gérer les ressources d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="83942-135">These are X.509 v3 certificates you use to authenticate a client application that uses the Service Management API to act on behalf of the subscription owner to manage subscription resources.</span></span>

<span data-ttu-id="83942-136">Le code de cette procédure utilise un certificat auto-signé pour l’authentification auprès d’Azure.</span><span class="sxs-lookup"><span data-stu-id="83942-136">The code in this procedure uses a self-signed certificate to authenticate with Azure.</span></span> <span data-ttu-id="83942-137">Pour cette procédure, vous devez créer un certificat et le télécharger sur le [Portail Azure Classic][Azure classic portal] au préalable.</span><span class="sxs-lookup"><span data-stu-id="83942-137">For this procedure, you need to create a certificate and upload it to the [Azure classic portal][Azure classic portal] beforehand.</span></span> <span data-ttu-id="83942-138">Cela implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="83942-138">This involves the following steps:</span></span>

* <span data-ttu-id="83942-139">Générer un fichier PFX représentant votre certificat client et l’enregistrer en local</span><span class="sxs-lookup"><span data-stu-id="83942-139">Generate a PFX file representing your client certificate and save it locally.</span></span>
* <span data-ttu-id="83942-140">Générer un certificat de gestion (fichier CER) à partir du fichier PFX</span><span class="sxs-lookup"><span data-stu-id="83942-140">Generate a management certificate (CER file) from the PFX file.</span></span>
* <span data-ttu-id="83942-141">Télécharger le fichier CER vers votre abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="83942-141">Upload the CER file to your Azure subscription.</span></span>
* <span data-ttu-id="83942-142">Convertir le fichier PFX au format JKS, car Java utilise ce format pour s’authentifier à l’aide de certificats</span><span class="sxs-lookup"><span data-stu-id="83942-142">Convert the PFX file into JKS, because Java uses that format to authenticate using certificates.</span></span>
* <span data-ttu-id="83942-143">Écrire le code d’authentification de l’application, qui fait référence au fichier JKS local</span><span class="sxs-lookup"><span data-stu-id="83942-143">Write the application's authentication code, which refers to the local JKS file.</span></span>

<span data-ttu-id="83942-144">Lorsque vous effectuez cette procédure, le certificat CER réside dans votre abonnement Azure et le certificat JKS réside sur votre lecteur local.</span><span class="sxs-lookup"><span data-stu-id="83942-144">When you complete this procedure, the CER certificate will reside in your Azure subscription and the JKS certificate will reside on your local drive.</span></span> <span data-ttu-id="83942-145">Pour plus d’informations sur les certificats de gestion, consultez la page [Créer et télécharger un certificat de gestion pour Microsoft Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="83942-145">For more information on management certificates, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="create-a-certificate"></a><span data-ttu-id="83942-146">Création d’un certificat</span><span class="sxs-lookup"><span data-stu-id="83942-146">Create a certificate</span></span>
<span data-ttu-id="83942-147">Pour créer votre propre certificat auto-signé, ouvrez une console de commandes sur votre système d’exploitation et exécutez les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="83942-147">To create your own self-signed certificate, open a command console on your operating system and run the following commands.</span></span>

> <span data-ttu-id="83942-148">**Remarque :** le JDK doit être installé sur l’ordinateur sur lequel vous exécutez cette commande.</span><span class="sxs-lookup"><span data-stu-id="83942-148">**Note:**  The computer on which you run this command must have the JDK installed.</span></span> <span data-ttu-id="83942-149">En outre, le chemin d’accès vers l’outil keytool dépend de l’emplacement où vous installez le JDK.</span><span class="sxs-lookup"><span data-stu-id="83942-149">Also, the path to the keytool depends on the location in which you install the JDK.</span></span> <span data-ttu-id="83942-150">Pour plus d’informations, consultez la rubrique [Outil de gestion de clés et de certificats (keytool)][Key and Certificate Management Tool (keytool)] dans la documentation en ligne de Java.</span><span class="sxs-lookup"><span data-stu-id="83942-150">For more information, see [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] in the Java online docs.</span></span>
> 
> 

<span data-ttu-id="83942-151">Pour créer le fichier .pfx :</span><span class="sxs-lookup"><span data-stu-id="83942-151">To create the .pfx file:</span></span>

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

<span data-ttu-id="83942-152">Pour créer le fichier .cer :</span><span class="sxs-lookup"><span data-stu-id="83942-152">To create the .cer file:</span></span>

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

<span data-ttu-id="83942-153">où :</span><span class="sxs-lookup"><span data-stu-id="83942-153">where:</span></span>

* <span data-ttu-id="83942-154">`<java-install-dir>` correspond au chemin d’accès vers le répertoire où vous avez installé Java.</span><span class="sxs-lookup"><span data-stu-id="83942-154">`<java-install-dir>` is the path to the directory in which you installed Java.</span></span>
* <span data-ttu-id="83942-155">`<keystore-id>` correspond à l’identificateur d’entrée keystore (par exemple, `AzureRemoteAccess`).</span><span class="sxs-lookup"><span data-stu-id="83942-155">`<keystore-id>` is the keystore entry identifier (for example, `AzureRemoteAccess`).</span></span>
* <span data-ttu-id="83942-156">`<cert-store-dir>` correspond au chemin d’accès vers le répertoire dans lequel vous souhaitez stocker les certificats (par exemple `C:/Certificates`).</span><span class="sxs-lookup"><span data-stu-id="83942-156">`<cert-store-dir>` is the path to the directory in which you want to store certificates (for example `C:/Certificates`).</span></span>
* <span data-ttu-id="83942-157">`<cert-file-name>` correspond au nom du fichier de certificat (par exemple `AzureWebDemoCert`).</span><span class="sxs-lookup"><span data-stu-id="83942-157">`<cert-file-name>` is the name of the certificate file (for example `AzureWebDemoCert`).</span></span>
* <span data-ttu-id="83942-158">`<password>` correspond au mot de passe que vous choisissez pour protéger le certificat ; il doit comporter au moins 6 caractères.</span><span class="sxs-lookup"><span data-stu-id="83942-158">`<password>` is the password you choose to protect the certificate; it must be at least 6 characters long.</span></span> <span data-ttu-id="83942-159">Vous avez la possibilité de n’entrer aucun mot de passe, même si cela n’est pas recommandé.</span><span class="sxs-lookup"><span data-stu-id="83942-159">You can enter no password, although this is not recommended.</span></span>
* <span data-ttu-id="83942-160">`<dname>` correspond au nom unique X.500 à associer à l’alias, et est utilisé en tant que champs de l’émetteur et du sujet dans le certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="83942-160">`<dname>` is the X.500 Distinguished Name to be associated with alias, and is used as the issuer and subject fields in the self-signed certificate.</span></span>

<span data-ttu-id="83942-161">Pour plus d'informations, consultez [Create and upload a management certificate for Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="83942-161">For more information, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="upload-the-certificate"></a><span data-ttu-id="83942-162">Téléchargement du certificat</span><span class="sxs-lookup"><span data-stu-id="83942-162">Upload the certificate</span></span>
<span data-ttu-id="83942-163">Pour télécharger un certificat auto-signé dans Azure, accédez à la page **Paramètres** dans le Portail Azure Classic, puis cliquez sur l’onglet **Certificats de gestion**. Cliquez sur **Télécharger** en bas de la page et naviguez jusqu’à l’emplacement du fichier CER que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="83942-163">To upload a self-signed certificate to Azure, go to the **Settings** page in the classic portal, then click the **Management Certificates** tab. Click **Upload** at the bottom of the page and navigate to the location of the CER file you created.</span></span>

#### <a name="convert-the-pfx-file-into-jks"></a><span data-ttu-id="83942-164">Conversion du fichier PFX au format JKS</span><span class="sxs-lookup"><span data-stu-id="83942-164">Convert the PFX file into JKS</span></span>
<span data-ttu-id="83942-165">Dans l’invite de commandes Windows (en mode d’exécution d’administrateur), accédez avec la commande cd au répertoire contenant les certificats et exécutez la commande suivante, où `<java-install-dir>` correspond au répertoire où vous avez installé Java sur votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="83942-165">In the Windows Command Prompt (running as admin), cd to the directory containing the certificates and run the following command, where `<java-install-dir>` is the directory in which you installed Java on your computer:</span></span>

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. <span data-ttu-id="83942-166">Lorsque vous y êtes invité, entrez le mot de passe keystore de la destination ; ce sera le mot de passe pour le fichier JKS.</span><span class="sxs-lookup"><span data-stu-id="83942-166">When prompted, enter the destination keystore password; this will be the password for the JKS file.</span></span>
2. <span data-ttu-id="83942-167">Lorsque vous y êtes invité, entrez le mot de passe keystore source ; il s’agit du mot de passe que vous avez spécifié pour le fichier PFX.</span><span class="sxs-lookup"><span data-stu-id="83942-167">When prompted, enter the source keystore password; this is the password you specified for the PFX file.</span></span>

<span data-ttu-id="83942-168">Les deux mots de passe ne doivent pas être identiques.</span><span class="sxs-lookup"><span data-stu-id="83942-168">The two passwords do not have to be the same.</span></span> <span data-ttu-id="83942-169">Vous avez la possibilité de n’entrer aucun mot de passe, même si cela n’est pas recommandé.</span><span class="sxs-lookup"><span data-stu-id="83942-169">You can enter no password, although this is not recommended.</span></span>

## <a name="build-a-web-app-creation-application"></a><span data-ttu-id="83942-170">Création d’une application de création d’application web</span><span class="sxs-lookup"><span data-stu-id="83942-170">Build a Web App creation application</span></span>
### <a name="create-the-eclipse-workspace-and-maven-project"></a><span data-ttu-id="83942-171">Création de l’espace de travail Eclipse et du projet Maven</span><span class="sxs-lookup"><span data-stu-id="83942-171">Create the Eclipse Workspace and Maven Project</span></span>
<span data-ttu-id="83942-172">Dans cette section, vous créez un espace de travail et un projet Maven pour l’application de création d’applications web, nommée AzureWebDemo.</span><span class="sxs-lookup"><span data-stu-id="83942-172">In this section you create a workspace and a Maven project for the web app creation application, named AzureWebDemo.</span></span>

1. <span data-ttu-id="83942-173">Créez un projet Maven.</span><span class="sxs-lookup"><span data-stu-id="83942-173">Create a new Maven project.</span></span> <span data-ttu-id="83942-174">Cliquez sur **Fichier > Nouveau > Projet Maven**.</span><span class="sxs-lookup"><span data-stu-id="83942-174">Click **File > New > Maven Project**.</span></span> <span data-ttu-id="83942-175">Dans **Nouveau projet Maven**, sélectionnez **Créer un projet simple** et **Utiliser l’emplacement de l’espace de travail par défaut**.</span><span class="sxs-lookup"><span data-stu-id="83942-175">In **New Maven Project**, select **Create a simple project** and **Use default workspace location**.</span></span>
2. <span data-ttu-id="83942-176">Dans la deuxième page de **Nouveau projet Maven**, spécifiez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="83942-176">On the second page of **New Maven Project**, specify the following:</span></span>
   
   * <span data-ttu-id="83942-177">ID de groupe : `com.<username>.azure.webdemo`</span><span class="sxs-lookup"><span data-stu-id="83942-177">Group ID: `com.<username>.azure.webdemo`</span></span>
   * <span data-ttu-id="83942-178">ID d’artefact : AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="83942-178">Artifact ID: AzureWebDemo</span></span>
   * <span data-ttu-id="83942-179">Version : 0.0.1-SNAPSHOT</span><span class="sxs-lookup"><span data-stu-id="83942-179">Version: 0.0.1-SNAPSHOT</span></span>
   * <span data-ttu-id="83942-180">Packaging : ar</span><span class="sxs-lookup"><span data-stu-id="83942-180">Packaging: jar</span></span>
   * <span data-ttu-id="83942-181">Nom : AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="83942-181">Name: AzureWebDemo</span></span>
     
     <span data-ttu-id="83942-182">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="83942-182">Click **Finish**.</span></span>
3. <span data-ttu-id="83942-183">Ouvrez le fichier pom.xml du nouveau projet dans l’Explorateur de projets.</span><span class="sxs-lookup"><span data-stu-id="83942-183">Open the new project's pom.xml file in Project Explorer.</span></span> <span data-ttu-id="83942-184">Sélectionnez l’onglet **Dépendances** . Comme il s’agit d’un nouveau projet, aucun package n’est encore répertorié.</span><span class="sxs-lookup"><span data-stu-id="83942-184">Select the **Dependencies** tab. As this is a new project, no packages are listed yet.</span></span>
4. <span data-ttu-id="83942-185">Ouvrez la vue Référentiels Maven.</span><span class="sxs-lookup"><span data-stu-id="83942-185">Open the Maven Repositories view.</span></span> <span data-ttu-id="83942-186">**Cliquez sur Fenêtre &gt; Afficher la vue &gt; Autres &gt; Maven &gt; Référentiels Maven**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="83942-186">**Click Window > Show View > Other > Maven > Maven Repositories** and click **OK**.</span></span> <span data-ttu-id="83942-187">La vue **Référentiels Maven** s’affiche en bas de l’IDE.</span><span class="sxs-lookup"><span data-stu-id="83942-187">The **Maven Repositories** view will appear at the bottom of the IDE.</span></span>
5. <span data-ttu-id="83942-188">Ouvrez **Référentiels globaux**, cliquez avec le bouton droit sur le référentiel **central**, puis sélectionnez **Reconstruire l’index**.</span><span class="sxs-lookup"><span data-stu-id="83942-188">Open **Global Repositories**, right-click the **central** repository, and select **Rebuild Index**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="83942-189">Cette étape peut prendre plusieurs minutes selon la vitesse de votre connexion.</span><span class="sxs-lookup"><span data-stu-id="83942-189">This step can take several minutes depending on the speed of your connection.</span></span> <span data-ttu-id="83942-190">Une fois l’index reconstruit, vous devez voir les packages Microsoft Azure dans le référentiel Maven **central** .</span><span class="sxs-lookup"><span data-stu-id="83942-190">When the index rebuilds, you should see the Microsoft Azure packages in the **central** Maven repository.</span></span>
6. <span data-ttu-id="83942-191">Dans **Dépendances**, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="83942-191">In **Dependencies**, click **Add**.</span></span> <span data-ttu-id="83942-192">Dans **Entrer l’ID de groupe...**, entrez `azure-management`.</span><span class="sxs-lookup"><span data-stu-id="83942-192">In **Enter Group ID...** enter `azure-management`.</span></span> <span data-ttu-id="83942-193">Sélectionnez les packages pour la gestion de base et la gestion de App Service Web Apps :</span><span class="sxs-lookup"><span data-stu-id="83942-193">Select the packages for base management and App Service Web Apps management:</span></span>
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > <span data-ttu-id="83942-194">**Remarque :** si vous mettez à jour les dépendances après la publication d’une nouvelle version, il vous faudra ajouter à nouveau chacune des dépendances dans cette liste.</span><span class="sxs-lookup"><span data-stu-id="83942-194">**Note:** If you are updating the dependencies after a new version release, you need to re-add each of the dependencies in this list.</span></span>
   > <span data-ttu-id="83942-195">Après avoir cliqué sur **Ajouter** et sélectionné chaque dépendance, celle-ci apparaît avec le nouveau numéro de version dans la liste **Dépendances**.</span><span class="sxs-lookup"><span data-stu-id="83942-195">After you click **Add** and select each dependency, it appears with the new version number in the **Dependencies** list.</span></span>
   > 
   > 

<span data-ttu-id="83942-196">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="83942-196">Click **OK**.</span></span> <span data-ttu-id="83942-197">Les packages Azure apparaissent alors dans la liste **Dépendances** .</span><span class="sxs-lookup"><span data-stu-id="83942-197">The Azure packages then appear in the **Dependencies** list.</span></span>

### <a name="writing-java-code-to-create-a-web-app-by-calling-the-azure-sdk"></a><span data-ttu-id="83942-198">Écriture de code Java pour créer une application web en appelant le SDK Azure</span><span class="sxs-lookup"><span data-stu-id="83942-198">Writing Java Code to Create a Web App by Calling the Azure SDK</span></span>
<span data-ttu-id="83942-199">Ensuite, écrivez le code qui appelle les API dans le Kit de développement logiciel (SDK) Azure pour Java afin de créer l’application web App Service.</span><span class="sxs-lookup"><span data-stu-id="83942-199">Next, write the code that calls APIs in the Azure SDK for Java to create the App Service web app.</span></span>

1. <span data-ttu-id="83942-200">Créez une classe Java pour contenir le code de point d’entrée principal.</span><span class="sxs-lookup"><span data-stu-id="83942-200">Create a Java class to contain the main entry point code.</span></span> <span data-ttu-id="83942-201">Dans l’Explorateur de projets, cliquez avec le bouton droit sur le nœud du projet et sélectionnez **Nouveau > Classe**.</span><span class="sxs-lookup"><span data-stu-id="83942-201">In Project Explorer, right-click on the project node and select **New > Class**.</span></span>
2. <span data-ttu-id="83942-202">Dans **Nouvelle classe Java**, nommez la classe `WebCreator` et activez la case **public static void main**.</span><span class="sxs-lookup"><span data-stu-id="83942-202">In **New Java Class**, name the class `WebCreator` and check the **public static void main** checkbox.</span></span> <span data-ttu-id="83942-203">Les sélections doivent apparaître comme suit :</span><span class="sxs-lookup"><span data-stu-id="83942-203">The selections should appear as follows:</span></span>
   
    ![][2]
3. <span data-ttu-id="83942-204">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="83942-204">Click **Finish**.</span></span> <span data-ttu-id="83942-205">Le fichier WebCreator.java s’affiche dans l’Explorateur de projets.</span><span class="sxs-lookup"><span data-stu-id="83942-205">The WebCreator.java file appears in Project Explorer.</span></span>

### <a name="calling-the-azure-api-to-create-an-app-service-web-app"></a><span data-ttu-id="83942-206">Appel de l’API Azure pour créer une application web App Service</span><span class="sxs-lookup"><span data-stu-id="83942-206">Calling the Azure API to Create an App Service Web App</span></span>
#### <a name="add-necessary-imports"></a><span data-ttu-id="83942-207">Ajout des importations nécessaires</span><span class="sxs-lookup"><span data-stu-id="83942-207">Add necessary imports</span></span>
<span data-ttu-id="83942-208">Dans WebCreator.java, ajoutez les importations ci-après ; celles-ci donnent accès aux classes dans les bibliothèques de gestion et permettent ainsi d’utiliser les API Azure :</span><span class="sxs-lookup"><span data-stu-id="83942-208">In WebCreator.java, add the following imports; these imports provide access to classes in the management libraries for consuming Azure APIs:</span></span>

    // General imports
    import java.net.URI;
    import java.util.ArrayList;

    // Imports for Exceptions
    import java.io.IOException;
    import java.net.URISyntaxException;
    import javax.xml.parsers.ParserConfigurationException;
    import com.microsoft.windowsazure.exception.ServiceException;
    import org.xml.sax.SAXException;

    // Imports for Azure App Service management configuration
    import com.microsoft.windowsazure.Configuration;
    import com.microsoft.windowsazure.management.configuration.ManagementConfiguration;

    // Service management imports for App Service Web Apps creation
    import com.microsoft.windowsazure.management.websites.*;
    import com.microsoft.windowsazure.management.websites.models.*;

    // Imports for authentication
    import com.microsoft.windowsazure.core.utils.KeyStoreType;


#### <a name="define-the-main-entry-point-class"></a><span data-ttu-id="83942-209">Définition de la classe de point d’entrée principal</span><span class="sxs-lookup"><span data-stu-id="83942-209">Define the main entry point class</span></span>
<span data-ttu-id="83942-210">Étant donné que l’objectif de l’application AzureWebDemo consiste à créer une application web App Service, nommez la classe principale pour cette application `WebAppCreator`.</span><span class="sxs-lookup"><span data-stu-id="83942-210">Because the purpose of the AzureWebDemo application is to create an App Service Web App, name the main class for this application `WebAppCreator`.</span></span> <span data-ttu-id="83942-211">Cette classe fournit le code de point d’entrée principal qui appelle l’API Gestion de services Azure pour créer l’application web.</span><span class="sxs-lookup"><span data-stu-id="83942-211">This class provides the main entry point code that calls the Azure Service Management API to create the web app.</span></span>

<span data-ttu-id="83942-212">Ajoutez les définitions de paramètre suivantes pour l’application web et l’espace web.</span><span class="sxs-lookup"><span data-stu-id="83942-212">Add the following parameter definitions for the web app and webspace.</span></span> <span data-ttu-id="83942-213">Vous devez fournir vos propres informations de certificat et d’ID d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="83942-213">You will need to provide your own Azure subscription ID and certificate information.</span></span>

    public class WebAppCreator {

        // Parameter definitions used for authentication.
        private static String uri = "https://management.core.windows.net/";
        private static String subscriptionId = "<subscription-id>";
        private static String keyStoreLocation = "<certificate-store-path>";
        private static String keyStorePassword = "<certificate-password>";

        // Define web app parameter values.
        private static String webAppName = "WebDemoWebApp";
        private static String domainName = ".azurewebsites.net";
        private static String webSpaceName = WebSpaceNames.WESTUSWEBSPACE;
        private static String appServicePlanName = "WebDemoAppServicePlan";

<span data-ttu-id="83942-214">où :</span><span class="sxs-lookup"><span data-stu-id="83942-214">where:</span></span>

* <span data-ttu-id="83942-215">`<subscription-id>` correspond à l’ID d’abonnement Azure dans lequel vous souhaitez créer la ressource.</span><span class="sxs-lookup"><span data-stu-id="83942-215">`<subscription-id>` is the Azure subscription ID in which you want to create the resource.</span></span>
* <span data-ttu-id="83942-216">`<certificate-store-path>` correspond au chemin d’accès et au nom de fichier pour le fichier JKS dans votre annuaire local de magasins de certificats.</span><span class="sxs-lookup"><span data-stu-id="83942-216">`<certificate-store-path>` is the path and filename to the JKS file in your local certificate store directory.</span></span> <span data-ttu-id="83942-217">Par exemple, `C:/Certificates/CertificateName.jks` pour Linux et `C:\Certificates\CertificateName.jks` pour Windows.</span><span class="sxs-lookup"><span data-stu-id="83942-217">For example, `C:/Certificates/CertificateName.jks` for Linux and `C:\Certificates\CertificateName.jks` for Windows.</span></span>
* <span data-ttu-id="83942-218">`<certificate-password>` correspond au mot de passe que vous avez spécifié lorsque vous avez créé votre certificat JKS.</span><span class="sxs-lookup"><span data-stu-id="83942-218">`<certificate-password>` is the password you specified when you created your JKS certificate.</span></span>
* <span data-ttu-id="83942-219">`webAppName` peut être n’importe quel nom que vous avez choisi ; cette procédure utilise le nom `WebDemoWebApp`.</span><span class="sxs-lookup"><span data-stu-id="83942-219">`webAppName` can be any name you choose; this procedure uses the name `WebDemoWebApp`.</span></span> <span data-ttu-id="83942-220">Le nom de domaine complet est le `webAppName` avec le `domainName` ajouté, de sorte que dans ce cas le domaine complet est `webdemowebapp.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="83942-220">The full domain name is the `webAppName` with the `domainName` appended, so in this case the full domain is `webdemowebapp.azurewebsites.net`.</span></span>
* <span data-ttu-id="83942-221">`domainName` doit être spécifié comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="83942-221">`domainName` should be specified as shown above.</span></span>
* <span data-ttu-id="83942-222">`webSpaceName` doit être l’une des valeurs définies dans la classe [WebSpaceNames][WebSpaceNames].</span><span class="sxs-lookup"><span data-stu-id="83942-222">`webSpaceName` should be one of the values defined in the [WebSpaceNames][WebSpaceNames] class.</span></span>
* <span data-ttu-id="83942-223">`appServicePlanName` doit être spécifié comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="83942-223">`appServicePlanName` should be specified as shown above.</span></span>

> <span data-ttu-id="83942-224">**Remarque :** chaque fois que vous exécutez cette application, vous devez modifier la valeur de `webAppName` et `appServicePlanName` (ou supprimer l’application web sur le portail Azure) avant d’exécuter à nouveau l’application.</span><span class="sxs-lookup"><span data-stu-id="83942-224">**Note:** Each time you run this application, you need to change the value of `webAppName` and `appServicePlanName` (or delete the web app on the Azure Portal) before running the application again.</span></span> <span data-ttu-id="83942-225">Sinon, l’exécution échoue, car la même ressource existe déjà sur Azure.</span><span class="sxs-lookup"><span data-stu-id="83942-225">Otherwise, execution will fail because the same resource already exists on Azure.</span></span>
> 
> 

#### <a name="define-the-web-creation-method"></a><span data-ttu-id="83942-226">Définition de la méthode de création web</span><span class="sxs-lookup"><span data-stu-id="83942-226">Define the web creation method</span></span>
<span data-ttu-id="83942-227">Ensuite, définissez une méthode de création de l’application web.</span><span class="sxs-lookup"><span data-stu-id="83942-227">Next, define a method to create the web app.</span></span> <span data-ttu-id="83942-228">Cette méthode, `createWebApp`, spécifie les paramètres de l’application web et l’espace web.</span><span class="sxs-lookup"><span data-stu-id="83942-228">This method, `createWebApp`, specifies the parameters of the web app and the webspace.</span></span> <span data-ttu-id="83942-229">Elle crée et configure également le client App Service Web Apps, qui est défini par l’objet [WebSiteManagementClient][WebSiteManagementClient].</span><span class="sxs-lookup"><span data-stu-id="83942-229">It also creates and configures the App Service Web Apps management client, which is defined by the [WebSiteManagementClient][WebSiteManagementClient] object.</span></span> <span data-ttu-id="83942-230">Le client de gestion est essentiel à la création d’applications web.</span><span class="sxs-lookup"><span data-stu-id="83942-230">The management client is key to creating Web Apps.</span></span> <span data-ttu-id="83942-231">Il fournit des services web RESTful qui permettent aux applications de gérer des applications web (exécution d’opérations telles que create, update et delete) en appelant l’API Gestion des services.</span><span class="sxs-lookup"><span data-stu-id="83942-231">It provides RESTful web services that allow applications to manage web apps (performing operations such as create, update, and delete) by calling the service management API.</span></span>

    private static void createWebApp() throws Exception {

        // Specify configuration settings for the App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path to the JKS file
            keyStorePassword,  // Password for the JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create the App Service Web Apps management client to call Azure APIs
        // and pass it the App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for the web app with the specified parameters.
        WebHostingPlanCreateParameters appServicePlanParams = new WebHostingPlanCreateParameters();
        appServicePlanParams.setName(appServicePlanName);
        appServicePlanParams.setSKU(SkuOptions.Free);
        webAppManagementClient.getWebHostingPlansOperations().create(webSpaceName, appServicePlanParams);

        // Set webspace parameters.
        WebSiteCreateParameters.WebSpaceDetails webSpaceDetails = new WebSiteCreateParameters.WebSpaceDetails();
        webSpaceDetails.setGeoRegion(GeoRegionNames.WESTUS);
        webSpaceDetails.setPlan(WebSpacePlanNames.VIRTUALDEDICATEDPLAN);
        webSpaceDetails.setName(webSpaceName);

        // Set web app parameters.
        // Note that the server farm name takes the Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define the web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create the web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output the HTTP status code of the response; 200 indicates the request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output the name of the web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

<span data-ttu-id="83942-232">Le code génère l’état HTTP de la réponse indiquant la réussite ou l’échec, et en cas de réussite, génère le nom de l’application web créée.</span><span class="sxs-lookup"><span data-stu-id="83942-232">The code will output the HTTP status of the response indicating success or failure, and if successful, will output the name of the created web app.</span></span>

#### <a name="define-the-main-method"></a><span data-ttu-id="83942-233">Définition de la méthode main()</span><span class="sxs-lookup"><span data-stu-id="83942-233">Define the main() method</span></span>
<span data-ttu-id="83942-234">Fournissez le code de la méthode main() qui appelle createWebApp() pour créer l’application web.</span><span class="sxs-lookup"><span data-stu-id="83942-234">Provide the main() method code that calls createWebApp() to create the web app.</span></span>

<span data-ttu-id="83942-235">Enfin, appelez `createWebApp` à partir de `main` :</span><span class="sxs-lookup"><span data-stu-id="83942-235">Finally, call `createWebApp` from `main`:</span></span>

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-the-application-and-verify-web-app-creation"></a><span data-ttu-id="83942-236">Exécution de l’application et vérification de la création de l’application web</span><span class="sxs-lookup"><span data-stu-id="83942-236">Run the application and verify web app creation</span></span>
<span data-ttu-id="83942-237">Pour vérifier que votre application s’exécute, cliquez sur **Exécuter > Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="83942-237">To verify that your application runs, click **Run > Run**.</span></span> <span data-ttu-id="83942-238">Au terme de l’exécution de l’application, vous devez voir la sortie suivante dans la console Eclipse :</span><span class="sxs-lookup"><span data-stu-id="83942-238">When the application completes running, you should see the following output in the Eclipse console:</span></span>

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

<span data-ttu-id="83942-239">Connectez-vous au Portail Azure Classic et cliquez sur **Applications web**.</span><span class="sxs-lookup"><span data-stu-id="83942-239">Log into the Azure classic portal and click **Web Apps**.</span></span> <span data-ttu-id="83942-240">La nouvelle application web doit apparaître dans la liste des applications web dans les quelques minutes qui suivent.</span><span class="sxs-lookup"><span data-stu-id="83942-240">The new web app should appear in the Web Apps list within a few minutes.</span></span>

## <a name="deploying-an-application-to-the-web-app"></a><span data-ttu-id="83942-241">Déploiement d’une application sur l’application web</span><span class="sxs-lookup"><span data-stu-id="83942-241">Deploying an Application to the Web App</span></span>
<span data-ttu-id="83942-242">Une fois que vous avez exécuté AzureWebDemo et créé la nouvelle application web, connectez-vous au Portail Classic, cliquez sur **Applications web**, puis sélectionnez **WebDemoWebApp** in the **Applications web** .</span><span class="sxs-lookup"><span data-stu-id="83942-242">After you have run AzureWebDemo and created the new web app, log into the classic portal, click **Web Apps**, and select **WebDemoWebApp** in the **Web Apps** list.</span></span> <span data-ttu-id="83942-243">Dans la page de tableau de bord de l’application web, cliquez sur **Parcourir** (ou cliquez sur l’URL, `webdemowebapp.azurewebsites.net`) pour y accéder.</span><span class="sxs-lookup"><span data-stu-id="83942-243">In the web app's dashboard page, click **Browse** (or click the URL, `webdemowebapp.azurewebsites.net`) to navigate to it.</span></span> <span data-ttu-id="83942-244">Seule une page d’espace réservé vide s’affiche, car aucun contenu n’a été publié sur l’application web.</span><span class="sxs-lookup"><span data-stu-id="83942-244">You will see a blank placeholder page, because no content has been published to the web app yet.</span></span>

<span data-ttu-id="83942-245">Ensuite, vous créez une application « Hello World » et la déployez sur l’application web.</span><span class="sxs-lookup"><span data-stu-id="83942-245">Next you will create a "Hello World" application and deploy it to the web app.</span></span>

### <a name="create-a-jsp-hello-world-application"></a><span data-ttu-id="83942-246">Création d’une application JSP Hello World</span><span class="sxs-lookup"><span data-stu-id="83942-246">Create a JSP Hello World application</span></span>
#### <a name="create-the-application"></a><span data-ttu-id="83942-247">Création de l'application</span><span class="sxs-lookup"><span data-stu-id="83942-247">Create the application</span></span>
<span data-ttu-id="83942-248">Pour illustrer le déploiement d’une application sur le web, la procédure suivante vous montre comment créer une application Java « Hello World » simple et la télécharger sur l’application web App Service créée par votre application.</span><span class="sxs-lookup"><span data-stu-id="83942-248">In order to demonstrate how to deploy an application to the web, the following procedure shows you how to create a simple "Hello World" Java application and upload it to the App Service Web App that your application created.</span></span>

1. <span data-ttu-id="83942-249">Cliquez sur **Fichier > Nouveau > Projet Web dynamique**.</span><span class="sxs-lookup"><span data-stu-id="83942-249">Click **File > New > Dynamic Web Project**.</span></span> <span data-ttu-id="83942-250">Nommez-le `JSPHello`.</span><span class="sxs-lookup"><span data-stu-id="83942-250">Name it `JSPHello`.</span></span> <span data-ttu-id="83942-251">Il est inutile de modifier d’autres paramètres dans cette boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="83942-251">You do not need to change any other settings in this dialog.</span></span> <span data-ttu-id="83942-252">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="83942-252">Click **Finish**.</span></span>
   
    ![][3]
2. <span data-ttu-id="83942-253">Dans l’Explorateur de projets, développez le projet **JSPHello** , cliquez avec le bouton droit sur **WebContent**, puis cliquez sur **Nouveau > Fichier JSP**.</span><span class="sxs-lookup"><span data-stu-id="83942-253">In Project Explorer, expand the **JSPHello** project, right-click **WebContent**, then click **New > JSP File**.</span></span> <span data-ttu-id="83942-254">Dans la boîte de dialogue Nouveau fichier JSP, nommez le nouveau fichier `index.jsp`.</span><span class="sxs-lookup"><span data-stu-id="83942-254">In the New JSP File dialog, name the new file `index.jsp`.</span></span> <span data-ttu-id="83942-255">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="83942-255">Click **Next**.</span></span>
3. <span data-ttu-id="83942-256">Dans la boîte de dialogue **Select JSP Template**, sélectionnez **New JSP File (html)**, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="83942-256">In the **Select JSP Template** dialog, select **New JSP File (html)** and click **Finish**.</span></span>
4. <span data-ttu-id="83942-257">Dans index.jsp, ajoutez le code suivant dans les sections des balises `<head>` et `<body>` :</span><span class="sxs-lookup"><span data-stu-id="83942-257">In index.jsp, add the following code in the `<head>` and `<body>` tag sections:</span></span>
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, the time is <%= date %> 
        </body>

#### <a name="run-the-hello-world-application-in-localhost"></a><span data-ttu-id="83942-258">Exécution de l’application Hello World dans localhost</span><span class="sxs-lookup"><span data-stu-id="83942-258">Run the Hello World application in localhost</span></span>
<span data-ttu-id="83942-259">Avant d’exécuter cette application, vous devez configurer certaines propriétés.</span><span class="sxs-lookup"><span data-stu-id="83942-259">Before you run this application, you need to configure a few properties.</span></span>

1. <span data-ttu-id="83942-260">Cliquez avec le bouton droit sur le projet **JSPHello** et sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="83942-260">Right-click the **JSPHello** project and select **Properties**.</span></span>
2. <span data-ttu-id="83942-261">Dans la boîte de dialogue **Propriétés** : sélectionnez **Chemin d’accès de la génération Java**, sélectionnez l’onglet **Ordre et exportation**, activez la case **Bibliothèque système JRE**, puis cliquez sur **Haut** pour déplacer l’élément vers le haut de la liste.</span><span class="sxs-lookup"><span data-stu-id="83942-261">In the **Properties** dialog: select **Java Build Path**, select the **Order and Export** tab, check **JRE System Library**, then click **Up** to move it to the top of the list.</span></span>
   
    ![][4]
3. <span data-ttu-id="83942-262">Également dans la boîte de dialogue **Propriétés**, sélectionnez **Runtimes ciblés**, puis cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="83942-262">Also in the **Properties** dialog: select **Targeted Runtimes** and click **New**.</span></span>
4. <span data-ttu-id="83942-263">Dans la boîte de dialogue **Nouvel environnement d’exécution serveur**, sélectionnez un serveur tel que **Apache Tomcat v7.0**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="83942-263">In the **New Server Runtime Environment** dialog, select a server such as **Apache Tomcat v7.0** and click **Next**.</span></span> <span data-ttu-id="83942-264">Dans la boîte de dialogue **Serveur Tomcat**, définissez **Nom** sur `Apache Tomcat v7.0`, et définissez **Répertoire d’installation Tomcat** sur le répertoire dans lequel vous avez installé la version du serveur Tomcat que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="83942-264">In the **Tomcat Server** dialog, set **Name** to `Apache Tomcat v7.0`, and set **Tomcat Installation Directory** to the directory in which you installed the version of Tomcat server you want to use.</span></span>
   
    ![][5]
   
    <span data-ttu-id="83942-265">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="83942-265">Click **Finish**.</span></span>
5. <span data-ttu-id="83942-266">Vous revenez ensuite à la page **Runtimes ciblés** de la boîte de dialogue **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="83942-266">You then return to the **Targeted Runtimes** page of the **Properties** dialog.</span></span> <span data-ttu-id="83942-267">Sélectionnez **Apache Tomcat v7.0**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="83942-267">Select **Apache Tomcat v7.0**, then click **OK**.</span></span>
   
    ![][6]
6. <span data-ttu-id="83942-268">Dans le menu **Exécuter** d’Eclipse, cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="83942-268">In the Eclipse **Run** menu, click **Run**.</span></span> <span data-ttu-id="83942-269">Dans la boîte de dialogue **Exécuter en tant que**, sélectionnez **Exécuter sur le serveur**.</span><span class="sxs-lookup"><span data-stu-id="83942-269">In the **Run As** dialog, select **Run on Server**.</span></span> <span data-ttu-id="83942-270">Dans la boîte de dialogue **Exécuter sur le serveur**, sélectionnez **Serveur Tomcat v7.0** :</span><span class="sxs-lookup"><span data-stu-id="83942-270">In the **Run on Server** dialog, select **Tomcat v7.0 Server**:</span></span>
   
    ![][7]
   
    <span data-ttu-id="83942-271">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="83942-271">Click **Finish**.</span></span>
7. <span data-ttu-id="83942-272">Lorsque l’application s’exécute, la page **JSPHello** doit apparaître dans une fenêtre localhost dans Eclipse (`http://localhost:8080/JSPHello/`), avec le message suivant :</span><span class="sxs-lookup"><span data-stu-id="83942-272">When the application runs, you should see the **JSPHello** page appear in a localhost window in Eclipse (`http://localhost:8080/JSPHello/`), displaying the following message:</span></span>
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-the-application-as-a-war"></a><span data-ttu-id="83942-273">Exportation de l’application en tant que fichier WAR</span><span class="sxs-lookup"><span data-stu-id="83942-273">Export the application as a WAR</span></span>
<span data-ttu-id="83942-274">Exportez les fichiers de projet web en tant que fichier d’archive (WAR) web afin de le déployer sur l’application web.</span><span class="sxs-lookup"><span data-stu-id="83942-274">Export the web project files as a web archive (WAR) file so that you can deploy it to the web app.</span></span> <span data-ttu-id="83942-275">Les fichiers de projet web suivants se trouvent dans le dossier WebContent :</span><span class="sxs-lookup"><span data-stu-id="83942-275">The following web project files reside in the WebContent folder:</span></span>

    META-INF
    WEB-INF
    index.jsp

1. <span data-ttu-id="83942-276">Cliquez avec le bouton droit sur le dossier WebContent et sélectionnez **Exporter**.</span><span class="sxs-lookup"><span data-stu-id="83942-276">Right-click the WebContent folder and select **Export**.</span></span>
2. <span data-ttu-id="83942-277">Dans la boîte de dialogue **Exporter la sélection**, cliquez sur **Web > WAR**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="83942-277">In the **Export Select** dialog, click **Web > WAR** file, then click **Next**.</span></span>
3. <span data-ttu-id="83942-278">Dans la boîte de dialogue **Exportation WAR** , sélectionnez le répertoire src dans le projet actuel, et incluez le nom du fichier WAR à la fin.</span><span class="sxs-lookup"><span data-stu-id="83942-278">In the **WAR Export** dialog, select the src directory in the current project, and include the name of the WAR file at the end.</span></span> <span data-ttu-id="83942-279">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="83942-279">For example:</span></span>
   
    `<project-path>/JSPHello/src/JSPHello.war`

<span data-ttu-id="83942-280">Pour plus d’informations sur le déploiement de fichiers WAR, consultez la page [Ajout d’une application à votre site Web Java sur Azure](web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="83942-280">For more information on deploying WAR files, see [Add a Java application to Azure App Service Web Apps](web-sites-java-add-app.md).</span></span>

### <a name="deploying-the-hello-world-application-using-ftp"></a><span data-ttu-id="83942-281">Déploiement de l’application Hello World à l’aide d’un client FTP</span><span class="sxs-lookup"><span data-stu-id="83942-281">Deploying the Hello World Application Using FTP</span></span>
<span data-ttu-id="83942-282">Sélectionnez un client FTP tiers pour publier l’application.</span><span class="sxs-lookup"><span data-stu-id="83942-282">Select a third-party FTP client to publish the application.</span></span> <span data-ttu-id="83942-283">Cette procédure décrit deux options : la console Kudu intégrée à Azure ; et FileZilla, un outil populaire présentant une interface utilisateur graphique pratique.</span><span class="sxs-lookup"><span data-stu-id="83942-283">This procedure describes two options: the Kudu console built into Azure; and FileZilla, a popular tool with a convenient, graphical UI.</span></span>

> <span data-ttu-id="83942-284">**Remarque :** le Kit de ressources Azure pour Eclipse prend en charge le déploiement vers les comptes de stockage et les services cloud, mais pas le déploiement sur des applications web pour le moment.</span><span class="sxs-lookup"><span data-stu-id="83942-284">**Note:** The Azure Toolkit for Eclipse supports deployment to storage accounts and cloud services, but does not currently support deployment to web apps.</span></span> <span data-ttu-id="83942-285">Vous pouvez effectuer un déploiement sur des comptes de stockage et des services cloud à l’aide d’un projet de déploiement Azure comme décrit dans [Création d’une application Hello World pour Azure dans Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), mais pas sur des applications web.</span><span class="sxs-lookup"><span data-stu-id="83942-285">You can deploy to storage accounts and cloud services using an Azure Deployment Project as described in [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), but not to web apps.</span></span> <span data-ttu-id="83942-286">Utilisez d’autres méthodes telles que FTP ou GitHub pour transférer des fichiers vers votre application web.</span><span class="sxs-lookup"><span data-stu-id="83942-286">Use other methods such as FTP or GitHub to transfer files to your web app.</span></span>
> 
> <span data-ttu-id="83942-287">**Remarque :** nous ne recommandons pas d’utiliser le client FTP à partir de l’invite de commandes Windows (l’utilitaire FTP.EXE de ligne de commandes fourni avec Windows).</span><span class="sxs-lookup"><span data-stu-id="83942-287">**Note:** We do not recommend using FTP from the Windows command prompt (the command-line FTP.EXE utility that ships with Windows).</span></span> <span data-ttu-id="83942-288">Les clients FTP qui utilisent le mode FTP actif, par exemple FTP.EXE, ne fonctionnent souvent pas sur les pare-feu.</span><span class="sxs-lookup"><span data-stu-id="83942-288">FTP clients that use active FTP, such as FTP.EXE, often fail to work over firewalls.</span></span> <span data-ttu-id="83942-289">Le mode FTP actif spécifie une adresse basée sur le réseau local interne, à laquelle un serveur FTP ne parviendra probablement pas à se connecter.</span><span class="sxs-lookup"><span data-stu-id="83942-289">Active FTP specifies an internal LAN-based address, to which an FTP server will likely fail to connect.</span></span>
> 
> 

<span data-ttu-id="83942-290">Pour plus d’informations sur le déploiement vers une application web App Service à l’aide du FTP, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="83942-290">For more information on deployment to an App Service web app using FTP, see the following topics:</span></span>

* [<span data-ttu-id="83942-291">Déployer à l’aide d’un utilitaire FTP</span><span class="sxs-lookup"><span data-stu-id="83942-291">Deploy using an FTP utility</span></span>](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a><span data-ttu-id="83942-292">Configurer les informations d'identification du déploiement</span><span class="sxs-lookup"><span data-stu-id="83942-292">Set up deployment credentials</span></span>
<span data-ttu-id="83942-293">Assurez-vous que vous avez exécuté l’application **AzureWebDemo** pour créer une application web.</span><span class="sxs-lookup"><span data-stu-id="83942-293">Make sure you have run the **AzureWebDemo** application to create a web app.</span></span> <span data-ttu-id="83942-294">Vous allez transférer des fichiers vers cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="83942-294">You will transfer files to this location.</span></span>

1. <span data-ttu-id="83942-295">Connectez-vous au Portail Classic et cliquez sur **Applications Web**.</span><span class="sxs-lookup"><span data-stu-id="83942-295">Log into the classic portal and click **Web Apps**.</span></span> <span data-ttu-id="83942-296">Vérifiez que **WebDemoWebApp** apparaît dans la liste des applications web et qu’il est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="83942-296">Make sure **WebDemoWebApp** appears in the list of web apps, and make sure that it is running.</span></span> <span data-ttu-id="83942-297">Cliquez sur **WebDemoWebApp** pour ouvrir sa page **Tableau de bord**.</span><span class="sxs-lookup"><span data-stu-id="83942-297">Click **WebDemoWebApp** to open its **Dashboard** page.</span></span>
2. <span data-ttu-id="83942-298">Dans la page **Tableau de bord** sous **Aperçu rapide**, cliquez sur **Configurer les informations d’identification du déploiement** (si vous disposez déjà de ces informations, l’option suivante apparaît : **Réinitialisez vos informations d’identification de déploiement**).</span><span class="sxs-lookup"><span data-stu-id="83942-298">On the **Dashboard** page, under **Quick Glance**, click **Set up your deployment credentials** (if you already have deployment credentials, this reads **Reset your deployment credentials**).</span></span>
   
    <span data-ttu-id="83942-299">Les informations d'identification du déploiement sont associées à un compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="83942-299">Deployment credentials are associated with a Microsoft account.</span></span> <span data-ttu-id="83942-300">Vous devez spécifier un nom d’utilisateur et un mot de passe que vous pouvez utiliser pour le déploiement à l’aide de Git et de FTP.</span><span class="sxs-lookup"><span data-stu-id="83942-300">You need to specify a username and password that you can use to deploy using Git and FTP.</span></span> <span data-ttu-id="83942-301">Vous pouvez utiliser ces informations d’identification pour effectuer un déploiement sur n’importe quelle application web dans tous les abonnements Azure associés à votre compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="83942-301">You can use these credentials to deploy to any web app in all Azure subscriptions associated with your Microsoft account.</span></span> <span data-ttu-id="83942-302">Fournissez les informations d’identification du déploiement Git et FTP dans la boîte de dialogue, et enregistrez le nom d’utilisateur et le mot de passe en vue d’une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="83942-302">Provide Git and FTP deployment credentials in the dialog, and record the username and password for future use.</span></span>

#### <a name="get-ftp-connection-information"></a><span data-ttu-id="83942-303">Obtention des informations de connexion FTP</span><span class="sxs-lookup"><span data-stu-id="83942-303">Get FTP connection information</span></span>
<span data-ttu-id="83942-304">Pour utiliser le FTP pour déployer des fichiers d’application vers l’application web nouvellement créée, vous devez obtenir les informations de connexion.</span><span class="sxs-lookup"><span data-stu-id="83942-304">To use FTP to deploy application files to the newly created web app, you need to obtain connection information.</span></span> <span data-ttu-id="83942-305">Il existe deux méthodes pour cela.</span><span class="sxs-lookup"><span data-stu-id="83942-305">There are two ways to obtain connection information.</span></span> <span data-ttu-id="83942-306">Une façon consiste à visiter la page **Tableau de bord** de l’application web ; l’autre manière consiste à télécharger le profil de publication de l’application web.</span><span class="sxs-lookup"><span data-stu-id="83942-306">One way is to visit the web app's **Dashboard** page; the other way is to download the web app's publish profile.</span></span> <span data-ttu-id="83942-307">Le profil de publication est un fichier XML qui fournit des informations telles que le nom d’hôte FTP et les informations d’identification d’ouverture de session pour vos applications web dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="83942-307">The publish profile is an XML file that provides information such as FTP host name and logon credentials for your web apps in Azure App Service.</span></span> <span data-ttu-id="83942-308">Vous pouvez utiliser ce nom d’utilisateur et ce mot de passe pour effectuer un déploiement sur n’importe quelle application web dans tous les abonnements associés au compte Azure, pas uniquement celui-ci.</span><span class="sxs-lookup"><span data-stu-id="83942-308">You can use this username and password to deploy to any web app in all subscriptions associated with the Azure account, not only this one.</span></span>

<span data-ttu-id="83942-309">Pour obtenir les informations de connexion FTP à partir du panneau de l’application web dans le [portail Azure][Azure Portal] :</span><span class="sxs-lookup"><span data-stu-id="83942-309">To obtain FTP connection information from the web app's blade in the [Azure Portal][Azure Portal]:</span></span>

1. <span data-ttu-id="83942-310">Sous **Essentials**, recherchez et copiez le **Nom d’hôte FTP**.</span><span class="sxs-lookup"><span data-stu-id="83942-310">Under **Essentials**, find and copy the **FTP hostname**.</span></span> <span data-ttu-id="83942-311">Il s’agit d’un URI similaire à `ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="83942-311">This is a URI similar to `ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span></span>
2. <span data-ttu-id="83942-312">Sous **Essentials**, recherchez et copiez le **Nom d’utilisateur FTP/déploiement**.</span><span class="sxs-lookup"><span data-stu-id="83942-312">Under **Essentials**, find and copy **FTP/Deployment username**.</span></span> <span data-ttu-id="83942-313">Il se présente sous la forme *nomappweb\déploiement-nomutilisateur* ; par exemple `WebDemoWebApp\deployer77`.</span><span class="sxs-lookup"><span data-stu-id="83942-313">This will have the form *webappname\deployment-username*; for example `WebDemoWebApp\deployer77`.</span></span>

<span data-ttu-id="83942-314">Pour obtenir les informations de connexion FTP à partir du profil de publication :</span><span class="sxs-lookup"><span data-stu-id="83942-314">To obtain FTP connection information from the publish profile:</span></span>

1. <span data-ttu-id="83942-315">Dans le panneau de l’application web, cliquez sur **Obtenir le profil de publication**.</span><span class="sxs-lookup"><span data-stu-id="83942-315">In the web app's blade, click **Get publish profile**.</span></span> <span data-ttu-id="83942-316">Cette action télécharge un fichier .publishsettings sur votre disque local.</span><span class="sxs-lookup"><span data-stu-id="83942-316">This will download a .publishsettings file to your local drive.</span></span>
2. <span data-ttu-id="83942-317">Ouvrez le fichier .publishsettings dans un éditeur XML ou un éditeur de texte et recherchez l’élément `<publishProfile>` contenant `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="83942-317">Open the .publishsettings file in an XML editor or text editor and find the `<publishProfile>` element containing `publishMethod="FTP"`.</span></span> <span data-ttu-id="83942-318">Il doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="83942-318">It should look like the following:</span></span>
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. <span data-ttu-id="83942-319">Notez que les paramètres `publishProfile` de l’application web sont mappés vers les paramètres du Gestionnaire de Site FileZilla comme suit :</span><span class="sxs-lookup"><span data-stu-id="83942-319">Note that the web app's `publishProfile` settings map to the FileZilla Site Manager settings as follows:</span></span>

* <span data-ttu-id="83942-320">`publishUrl` est identique au **Nom d’hôte FTP**, la valeur que vous définissez dans **Hôte**.</span><span class="sxs-lookup"><span data-stu-id="83942-320">`publishUrl` is the same as **FTP host name**, the value you set in **Host**.</span></span>
* <span data-ttu-id="83942-321">`publishMethod="FTP"` signifie que vous définissez **Protocole** sur **FTP - File Transfer Protocol** et **Chiffrement** sur **Utiliser le FTP simple**.</span><span class="sxs-lookup"><span data-stu-id="83942-321">`publishMethod="FTP"` means that you set **Protocol** to **FTP - File Transfer Protocol**, and **Encryption** to **Use plain FTP**.</span></span>
* <span data-ttu-id="83942-322">`userName` et `userPWD` sont des clés pour les valeurs de nom d’utilisateur et de mot de passe spécifiées lorsque vous réinitialisez les informations d’identification de déploiement.</span><span class="sxs-lookup"><span data-stu-id="83942-322">`userName` and `userPWD` are keys for the actual username and password values you specified when you reset the deployment credentials.</span></span> <span data-ttu-id="83942-323">`userName` est identique à **Déploiement / FTP utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="83942-323">`userName` is the same as **Deployment / FTP user**.</span></span> <span data-ttu-id="83942-324">Elles sont mappées vers **Utilisateur** et **Mot de passe** dans FileZilla.</span><span class="sxs-lookup"><span data-stu-id="83942-324">They map to **User** and **Password** in FileZilla.</span></span>
* <span data-ttu-id="83942-325">`ftpPassiveMode="True"` signifie que le site FTP utilise le transfert FTP passif ; sélectionnez **Passif** on the **Paramètres de transfert** .</span><span class="sxs-lookup"><span data-stu-id="83942-325">`ftpPassiveMode="True"` means that the FTP site uses passive FTP transfer; select **Passive** on the **Transfer Settings** tab.</span></span>

#### <a name="configure-the-web-app-to-host-a-java-application"></a><span data-ttu-id="83942-326">Configuration de l’application web pour héberger une application Java</span><span class="sxs-lookup"><span data-stu-id="83942-326">Configure the Web App to host a Java application</span></span>
<span data-ttu-id="83942-327">Avant de publier l’application, vous devez modifier quelques paramètres de configuration afin que l’application web puisse héberger une application Java.</span><span class="sxs-lookup"><span data-stu-id="83942-327">Before you publish the application, you need to change a few configuration settings so that the web app can host a Java application.</span></span>

1. <span data-ttu-id="83942-328">Dans le Portail Classic, accédez à la page **Tableau de bord** de l’application web et cliquez sur **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="83942-328">In the classic portal, go to the web app's **Dashboard** page and click **Configure**.</span></span> <span data-ttu-id="83942-329">Dans la page **Configurer** , spécifiez les paramètres suivants.</span><span class="sxs-lookup"><span data-stu-id="83942-329">On the **Configure** page, specify the following settings.</span></span>
2. <span data-ttu-id="83942-330">Dans **Version Java**, la valeur par défaut est **Off** ; sélectionnez la version Java ciblée par votre application cible ; par exemple 1.7.0_51.</span><span class="sxs-lookup"><span data-stu-id="83942-330">In **Java version** the default is **Off**; select the Java version your application targets; for example 1.7.0_51.</span></span> <span data-ttu-id="83942-331">Après cela, assurez-vous également que **Conteneur Web** est défini sur une version de Tomcat Server.</span><span class="sxs-lookup"><span data-stu-id="83942-331">After you do this, also make sure that **Web container** is set to a version of Tomcat Server.</span></span>
3. <span data-ttu-id="83942-332">Dans **Documents par défaut**, ajoutez index.jsp et déplacez-le vers le haut de la liste.</span><span class="sxs-lookup"><span data-stu-id="83942-332">In **Default Documents**, add index.jsp and move it up to the top of the list.</span></span> <span data-ttu-id="83942-333">(Le fichier par défaut pour les applications web est hostingstart.html.)</span><span class="sxs-lookup"><span data-stu-id="83942-333">(The default file for web apps is hostingstart.html.)</span></span>
4. <span data-ttu-id="83942-334">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="83942-334">Click **Save**.</span></span>

#### <a name="publish-your-application-using-kudu"></a><span data-ttu-id="83942-335">Publication de votre application à l’aide de Kudu</span><span class="sxs-lookup"><span data-stu-id="83942-335">Publish your application using Kudu</span></span>
<span data-ttu-id="83942-336">Un moyen de publier l’application consiste à utiliser la console de débogage Kudu intégrée à Azure.</span><span class="sxs-lookup"><span data-stu-id="83942-336">One way to publish the application is to use the Kudu debug console built into Azure.</span></span> <span data-ttu-id="83942-337">Kudu est réputé comme étant stable et homogène avec App Service Web Apps et Tomcat Server.</span><span class="sxs-lookup"><span data-stu-id="83942-337">Kudu is known to be stable and consistent with App Service Web Apps and Tomcat Server.</span></span> <span data-ttu-id="83942-338">Vous accédez à la console de l’application web en accédant à une URL sous la forme suivante :</span><span class="sxs-lookup"><span data-stu-id="83942-338">You access the console for the web app by browsing to a URL of the following form:</span></span>

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. <span data-ttu-id="83942-339">Pour cette procédure, la console Kudu se trouve à l’adresse suivante ; accédez à cet emplacement :</span><span class="sxs-lookup"><span data-stu-id="83942-339">For this procedure, the Kudu console is located at the following URL; browse to this location:</span></span>
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. <span data-ttu-id="83942-340">Dans le menu principal, sélectionnez **Console de débogage > CMD**.</span><span class="sxs-lookup"><span data-stu-id="83942-340">From the top menu, select **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="83942-341">À partir de la ligne de commande de la console, accédez à `/site/wwwroot` (ou cliquez sur `site`, puis sur `wwwroot` dans l’affichage de répertoire en haut de la page) :</span><span class="sxs-lookup"><span data-stu-id="83942-341">In the console command line, navigate to `/site/wwwroot` (or click `site`, then `wwwroot` in the directory view at the top of the page):</span></span>
   
    `cd /site/wwwroot`
4. <span data-ttu-id="83942-342">Une fois que vous avez spécifié **Version Java**, Tomcat Server doit créer un répertoire webapps.</span><span class="sxs-lookup"><span data-stu-id="83942-342">After you specify **Java version**, Tomcat server should create a webapps directory.</span></span> <span data-ttu-id="83942-343">À partir de la ligne de commande de la console, accédez au répertoire webapps :</span><span class="sxs-lookup"><span data-stu-id="83942-343">In the console command line, navigate to the webapps directory:</span></span>
   
    `mkdir webapps`
   
    `cd webapps`
5. <span data-ttu-id="83942-344">Faites glisser JSPHello.war à partir de `<project-path>/JSPHello/src/` et déposez-le dans l’affichage de répertoire Kudu sous `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="83942-344">Drag JSPHello.war from `<project-path>/JSPHello/src/` and drop it into the Kudu directory view under `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="83942-345">Ne le faites pas glisser vers la zone « Faire glisser pour télécharger et compresser », étant donné que Tomcat le décompressera.</span><span class="sxs-lookup"><span data-stu-id="83942-345">Do not drag it to the "Drag here to upload and zip" area, because Tomcat will unzip it.</span></span>
   
   ![][8]

<span data-ttu-id="83942-346">Au départ, JSPHello.war apparaît dans la zone de répertoire tout seul :</span><span class="sxs-lookup"><span data-stu-id="83942-346">At first JSPHello.war appears in the directory area by itself:</span></span>

  ![][9]

<span data-ttu-id="83942-347">Après un court délai (probablement moins de 5 minutes), Tomcat Server décompresse le fichier WAR dans un répertoire JSPHello décompressé.</span><span class="sxs-lookup"><span data-stu-id="83942-347">In a short time (probably less than 5 minutes) Tomcat Server will unzip the WAR file into an unpacked JSPHello directory.</span></span> <span data-ttu-id="83942-348">Cliquez sur le répertoire ROOT pour voir si index.jsp a été décompressé et copié à cet endroit.</span><span class="sxs-lookup"><span data-stu-id="83942-348">Click the ROOT directory to see whether index.jsp has been unzipped and copied there.</span></span> <span data-ttu-id="83942-349">Dans ce cas, accédez au répertoire webapps pour voir si le répertoire JSPHello décompressé a été créé.</span><span class="sxs-lookup"><span data-stu-id="83942-349">If so, navigate back to the webapps directory to see whether the unpacked JSPHello directory has been created.</span></span> <span data-ttu-id="83942-350">Si vous ne voyez pas ces éléments, attendez et recommencez.</span><span class="sxs-lookup"><span data-stu-id="83942-350">If you do not see these items, wait and repeat.</span></span>

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a><span data-ttu-id="83942-351">Publication de votre application à l’aide de FileZilla (facultatif)</span><span class="sxs-lookup"><span data-stu-id="83942-351">Publish your application using FileZilla (optional)</span></span>
<span data-ttu-id="83942-352">Un autre outil que vous pouvez utiliser pour publier l’application est FileZilla, un client FTP tiers populaire présentant une interface utilisateur graphique pratique.</span><span class="sxs-lookup"><span data-stu-id="83942-352">Another tool you can use to publish the application is FileZilla, a popular third-party FTP client with a convenient, graphical UI.</span></span> <span data-ttu-id="83942-353">Vous pouvez télécharger et installer FileZilla à partir de [http://filezilla-project.org/](http://filezilla-project.org/) si vous ne l’avez pas déjà.</span><span class="sxs-lookup"><span data-stu-id="83942-353">You can download and install FileZilla from [http://filezilla-project.org/](http://filezilla-project.org/) if you do not already have it.</span></span> <span data-ttu-id="83942-354">Pour plus d’informations sur l’utilisation du client, consultez la [Documentation de FileZilla](https://wiki.filezilla-project.org/Documentation) et cette entrée de blog sur les [Clients FTP - 4e partie : FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span><span class="sxs-lookup"><span data-stu-id="83942-354">For more information on using the client, see the [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) and this blog entry on [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span></span>

1. <span data-ttu-id="83942-355">Dans FileZilla, cliquez sur **Fichier > Gestionnaire de Sites**.</span><span class="sxs-lookup"><span data-stu-id="83942-355">In FileZilla, click **File > Site Manager**.</span></span>
2. <span data-ttu-id="83942-356">Dans la boîte de dialogue **Gestionnaire de Sites**, cliquez sur **Nouveau Site**.</span><span class="sxs-lookup"><span data-stu-id="83942-356">In the **Site Manager** dialog, click **New Site**.</span></span> <span data-ttu-id="83942-357">Un nouveau site FTP vierge apparaît dans **Sélectionnez une entrée** vous invitant à fournir un nom.</span><span class="sxs-lookup"><span data-stu-id="83942-357">A new blank FTP site will appear in **Select Entry** prompting you to provide a name.</span></span> <span data-ttu-id="83942-358">Dans le cadre de cette procédure, nommez-le `AzureWebDemo-FTP`.</span><span class="sxs-lookup"><span data-stu-id="83942-358">For this procedure, name it `AzureWebDemo-FTP`.</span></span>
   
    <span data-ttu-id="83942-359">Dans l’onglet **Configurer** , spécifiez les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="83942-359">On the **General** tab, specify the following settings:</span></span>
   
   * <span data-ttu-id="83942-360">**Hôte :** Entrez le **Nom d'hôte FTP** que vous avez copié à partir du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="83942-360">**Host:** Enter the **FTP Host Name** that you copied from the dashboard.</span></span>
   * <span data-ttu-id="83942-361">**Port :** (Laissez ce champ vide, car il s'agit d'un transfert passif et le serveur déterminera le port à utiliser.)</span><span class="sxs-lookup"><span data-stu-id="83942-361">**Port:** (Leave this blank, as this is a passive transfer and the server will determine the port to use.)</span></span>
   * <span data-ttu-id="83942-362">**Protocole :** FTP File Transfer Protocol</span><span class="sxs-lookup"><span data-stu-id="83942-362">**Protocol:** FTP File Transfer Protocol</span></span>
   * <span data-ttu-id="83942-363">**Chiffrement :** Utiliser un chiffrement FTP simple</span><span class="sxs-lookup"><span data-stu-id="83942-363">**Encryption:** Use plain FTP</span></span>
   * <span data-ttu-id="83942-364">**Type d'ouverture de session :** Normal</span><span class="sxs-lookup"><span data-stu-id="83942-364">**Logon Type:** Normal</span></span>
   * <span data-ttu-id="83942-365">**Utilisateur :** Entrez l’utilisateur FTP / déploiement que vous avez copié à partir du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="83942-365">**User:** Enter the Deployment / FTP user that you copied from the dashboard.</span></span> <span data-ttu-id="83942-366">Il s'agit du nom d'utilisateur FTP complet, qui se présente sous la forme *nomappweb\nomutilisateur*.</span><span class="sxs-lookup"><span data-stu-id="83942-366">This is the full FTP username, which has the form *webappname\username*.</span></span>
   * <span data-ttu-id="83942-367">**Mot de passe :** Entrez le mot de passe que vous avez spécifié lorsque vous avez défini les informations d'identification de déploiement.</span><span class="sxs-lookup"><span data-stu-id="83942-367">**Password:** Enter the password that you specified when you set the deployment credentials.</span></span>
     
     <span data-ttu-id="83942-368">Sous l’onglet **Paramètres de transfert**, sélectionnez **Passif**.</span><span class="sxs-lookup"><span data-stu-id="83942-368">On the **Transfer Settings** tab, select **Passive**.</span></span>
3. <span data-ttu-id="83942-369">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="83942-369">Click **Connect**.</span></span> <span data-ttu-id="83942-370">Si la connexion aboutit, la console de FileZilla affiche un message `Status: Connected` et émet une commande `LIST` pour répertorier le contenu du répertoire.</span><span class="sxs-lookup"><span data-stu-id="83942-370">If successful, FileZilla's console will display a `Status: Connected` message and issue a `LIST` command to list the directory contents.</span></span>
4. <span data-ttu-id="83942-371">Dans le volet **Site local** , sélectionnez le répertoire source dans lequel réside le fichier JSPHello.war ; le chemin d’accès est semblable au suivant :</span><span class="sxs-lookup"><span data-stu-id="83942-371">In the **Local** site panel, select the source directory in which the JSPHello.war file resides; the path will be similar to the following:</span></span>
   
    `<project-path>/JSPHello/src/`
5. <span data-ttu-id="83942-372">Dans le volet **Site distant** , sélectionnez le dossier de destination.</span><span class="sxs-lookup"><span data-stu-id="83942-372">In the **Remote** site panel, select the destination folder.</span></span> <span data-ttu-id="83942-373">Vous allez déployer le fichier WAR dans le répertoire `webapps` sous la racine de l’application web.</span><span class="sxs-lookup"><span data-stu-id="83942-373">You will deploy the WAR file to the `webapps` directory under the web app's root.</span></span> <span data-ttu-id="83942-374">Accédez à `/site/wwwroot`, cliquez avec le bouton droit sur `wwwroot`, puis sélectionnez **Créer un dossier**.</span><span class="sxs-lookup"><span data-stu-id="83942-374">Navigate to `/site/wwwroot`, right-click on `wwwroot`, and select **Create directory**.</span></span> <span data-ttu-id="83942-375">Nommez le répertoire `webapps` et accédez à ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="83942-375">Name the directory `webapps` and enter that directory.</span></span>
6. <span data-ttu-id="83942-376">Transférez JSPHello.war vers `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="83942-376">Transfer JSPHello.war to `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="83942-377">Sélectionnez JSPHello.war dans la liste de fichiers **Local**, cliquez avec le bouton droit dessus et sélectionnez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="83942-377">Select JSPHello.war in the **Local** file list, right-click on it and select **Upload**.</span></span> <span data-ttu-id="83942-378">Il doit s’afficher dans `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="83942-378">You should see it appear in `/site/wwwroot/webapps`.</span></span>
7. <span data-ttu-id="83942-379">Une fois que vous avez copié JSPHello.war dans le répertoire webapps, Tomcat Server décompresse automatiquement les fichiers du fichier WAR.</span><span class="sxs-lookup"><span data-stu-id="83942-379">After you copy JSPHello.war to the webapps directory, Tomcat Server will automatically unpack (unzip) the files in the WAR file.</span></span> <span data-ttu-id="83942-380">Bien que Tomcat Server commence la décompression presque immédiatement, il peut se passer un certain délai (parfois plusieurs heures) avant que les fichiers s’affichent dans le client FTP.</span><span class="sxs-lookup"><span data-stu-id="83942-380">Although Tomcat Server begins unpacking almost immediately, it might take a long time (possibly hours) for the files to appear in the FTP client.</span></span>

#### <a name="run-the-hello-world-application-on-the-web-app"></a><span data-ttu-id="83942-381">Exécution de l’application Hello World dans l’application web</span><span class="sxs-lookup"><span data-stu-id="83942-381">Run the Hello World application on the Web App</span></span>
1. <span data-ttu-id="83942-382">Après avoir téléchargé le fichier WAR et vérifié que Tomcat Server a créé un répertoire `JSPHello` décompressé, accédez à `http://webdemowebapp.azurewebsites.net/JSPHello` pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="83942-382">After you have uploaded the WAR file and verified that Tomcat server has created an unpacked `JSPHello` directory, browse to `http://webdemowebapp.azurewebsites.net/JSPHello` to run the application.</span></span>
   
   > <span data-ttu-id="83942-383">**Remarque :** si vous cliquez sur **Parcourir** à partir du Portail Classic, il se peut que la page web par défaut s’affiche avec le message suivant : « Cette application web de type Java a été créée. »</span><span class="sxs-lookup"><span data-stu-id="83942-383">**Note:** If you click **Browse** from the classic portal, you might get the default webpage, saying "This Java based web application has been successfully created."</span></span> <span data-ttu-id="83942-384">» Vous devrez peut-être actualiser la page web pour afficher la sortie de l’application au lieu de la page web par défaut.</span><span class="sxs-lookup"><span data-stu-id="83942-384">You might have to refresh the webpage in order to view the application output instead of the default webpage.</span></span>
   > 
   > 
2. <span data-ttu-id="83942-385">Lorsque l’application s’exécute, une page web s’affiche avec la sortie suivante :</span><span class="sxs-lookup"><span data-stu-id="83942-385">When the application runs, you should see a web page with the following output:</span></span>
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a><span data-ttu-id="83942-386">Nettoyage des ressources Azure</span><span class="sxs-lookup"><span data-stu-id="83942-386">Clean up Azure resources</span></span>
<span data-ttu-id="83942-387">Cette procédure crée une application web App Service.</span><span class="sxs-lookup"><span data-stu-id="83942-387">This procedure creates an App Service web app.</span></span> <span data-ttu-id="83942-388">La ressource vous sera facturée aussi longtemps qu’elle existe.</span><span class="sxs-lookup"><span data-stu-id="83942-388">You will be billed for the resource as long as it exists.</span></span> <span data-ttu-id="83942-389">Sauf si vous envisagez de continuer à utiliser l’application web à des fins de test ou de développement, pensez à l’arrêter ou à la supprimer.</span><span class="sxs-lookup"><span data-stu-id="83942-389">Unless you plan to continue using the web app for testing or development, you should consider stopping or deleting it.</span></span> <span data-ttu-id="83942-390">Une application web qui a été arrêtée continuera à faire l’objet de frais réduits, mais vous pouvez la redémarrer à tout moment.</span><span class="sxs-lookup"><span data-stu-id="83942-390">A web app that has been stopped will still incur a small charge, but you can restart it at any time.</span></span> <span data-ttu-id="83942-391">La suppression d’une application web a pour conséquence la suppression de toutes les données que vous avez téléchargées dans celle-ci.</span><span class="sxs-lookup"><span data-stu-id="83942-391">Deleting a web app erases all data you have uploaded to it.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

[1]: ./media/java-create-azure-website-using-java-sdk/eclipse-maven-repositories-rebuild-index.png
[2]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-java-class.png
[3]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-dynamic-web-project.png
[4]: ./media/java-create-azure-website-using-java-sdk/eclipse-java-build-path.png
[5]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-tomcat-server.png
[6]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-properties-page.png
[7]: ./media/java-create-azure-website-using-java-sdk/eclipse-run-on-server.png
[8]: ./media/java-create-azure-website-using-java-sdk/kudu-console-drag-drop.png
[9]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-1.png
[10]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-2.png


[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[Web Platform Installer]: http://go.microsoft.com/fwlink/?LinkID=252838
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh690946.aspx
[Azure classic portal]: https://manage.windowsazure.com
[What is an Azure AD directory]: http://technet.microsoft.com/library/jj573650.aspx
[Create and Upload a Management Certificate for Azure]: ../cloud-services/cloud-services-certs-create.md
[Key and Certificate Management Tool (keytool)]: http://docs.oracle.com/javase/6/docs/technotes/tools/windows/keytool.html
[WebSiteManagementClient]: http://azure.github.io/azure-sdk-for-java/com/microsoft/azure/management/websites/WebSiteManagementClient.html
[WebSpaceNames]: http://dl.windowsazure.com/javadoc/com/microsoft/windowsazure/management/websites/models/WebSpaceNames.html
[Azure Portal]: https://portal.azure.com
