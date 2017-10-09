---
title: "aaaCreate une application Web dans Azure App Service à l’aide de hello SDK Azure pour Java"
description: "Découvrez comment une application Web sur Azure App Service par programme à l’aide de toocreate hello SDK Azure pour Java."
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
ms.openlocfilehash: 42ba86b7fbb5668b3675198d0c5bb454525f706b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-hello-azure-sdk-for-java"></a><span data-ttu-id="1809e-103">Créer une application Web dans Azure App Service à l’aide de hello SDK Azure pour Java</span><span class="sxs-lookup"><span data-stu-id="1809e-103">Create a Web App in Azure App Service using hello Azure SDK for Java</span></span>
<!-- Azure Active Directory workflow is not yet available on hello Azure Portal -->

## <a name="overview"></a><span data-ttu-id="1809e-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="1809e-104">Overview</span></span>
<span data-ttu-id="1809e-105">Cette procédure pas à pas vous montre comment toocreate un kit de développement logiciel Azure pour une application Java qui crée une application Web [Azure App Service][Azure App Service], puis déployer une application tooit.</span><span class="sxs-lookup"><span data-stu-id="1809e-105">This walkthrough shows you how toocreate an Azure SDK for Java application that creates a Web App in [Azure App Service][Azure App Service], then deploy an application tooit.</span></span> <span data-ttu-id="1809e-106">Elle comprend deux parties :</span><span class="sxs-lookup"><span data-stu-id="1809e-106">It consists of two parts:</span></span>

* <span data-ttu-id="1809e-107">Partie 1 montre comment toobuild une application Java qui crée une application web.</span><span class="sxs-lookup"><span data-stu-id="1809e-107">Part 1 demonstrates how toobuild a Java application that creates a web app.</span></span>
* <span data-ttu-id="1809e-108">Partie 2 illustre comment toocreate un JSP simple « Hello World » application, puis utiliser FTP client toodeploy code tooApp Service.</span><span class="sxs-lookup"><span data-stu-id="1809e-108">Part 2 demonstrates how toocreate a simple JSP "Hello World" application, then use an FTP client toodeploy code tooApp Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1809e-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1809e-109">Prerequisites</span></span>
### <a name="software-installations"></a><span data-ttu-id="1809e-110">Installations de logiciels</span><span class="sxs-lookup"><span data-stu-id="1809e-110">Software Installations</span></span>
<span data-ttu-id="1809e-111">Hello AzureWebDemo code de l’application dans cet article a été écrit à l’aide du SDK Azure Java 0.7.0, que vous pouvez installer à l’aide de hello [Web Platform Installer] [ Web Platform Installer] (WebPI).</span><span class="sxs-lookup"><span data-stu-id="1809e-111">hello AzureWebDemo application code in this article was written using Azure Java SDK 0.7.0, which you can install using hello [Web Platform Installer][Web Platform Installer] (WebPI).</span></span> <span data-ttu-id="1809e-112">En outre, assurez-vous que toouse hello version la plus récente de hello [boîte à outils Azure pour Eclipse][Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="1809e-112">In addition, make sure toouse hello latest version of hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="1809e-113">Après avoir installé hello SDK, mettre à jour les dépendances hello dans votre projet Eclipse en exécutant **mettre à jour l’Index** dans **Maven référentiels**, puis rajoutez la version la plus récente de chaque package Bonjour hello  **Dépendances** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="1809e-113">After you install hello SDK, update hello dependencies in your Eclipse project by running **Update Index** in **Maven Repositories**, then re-add hello latest version of each package in hello **Dependencies** window.</span></span> <span data-ttu-id="1809e-114">Vous pouvez vérifier la version de hello de logiciels installés dans Eclipse en cliquant sur **aide > Détails de l’Installation**; vous doit avoir au moins hello suivants versions :</span><span class="sxs-lookup"><span data-stu-id="1809e-114">You can verify hello version of your installed software in Eclipse by clicking **Help > Installation Details**; you should have at least hello following versions:</span></span>

* <span data-ttu-id="1809e-115">Package pour les bibliothèques Microsoft Azure pour Java 0.7.0.20150309</span><span class="sxs-lookup"><span data-stu-id="1809e-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span></span>
* <span data-ttu-id="1809e-116">Environnement de développement intégré (IDE) Eclipse pour développeurs Java EE 4.4.2.20150219</span><span class="sxs-lookup"><span data-stu-id="1809e-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span></span>

### <a name="create-and-configure-cloud-resources-in-azure"></a><span data-ttu-id="1809e-117">Création et configuration de ressources de cloud dans Azure</span><span class="sxs-lookup"><span data-stu-id="1809e-117">Create and Configure Cloud Resources in Azure</span></span>
<span data-ttu-id="1809e-118">Avant de commencer cette procédure, vous devez toohave un abonnement Azure actif et configuré par défaut Active Directory (AD) sur Azure.</span><span class="sxs-lookup"><span data-stu-id="1809e-118">Before you begin this procedure, you need toohave an active Azure subscription and set up a default Active Directory (AD) on Azure.</span></span>

### <a name="create-an-active-directory-ad-in-azure"></a><span data-ttu-id="1809e-119">Création d’un annuaire Active Directory (AD) dans Azure</span><span class="sxs-lookup"><span data-stu-id="1809e-119">Create an Active Directory (AD) in Azure</span></span>
<span data-ttu-id="1809e-120">Si vous n’avez pas déjà un Active Directory (AD) sur votre abonnement Azure, connectez-vous à hello [portail Azure classic] [ Azure classic portal] avec votre compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1809e-120">If you do not already have an Active Directory (AD) on your Azure subscription, log into hello [Azure classic portal][Azure classic portal] with your Microsoft account.</span></span> <span data-ttu-id="1809e-121">Si vous avez plusieurs abonnements, cliquez sur **abonnements** et le répertoire par défaut de select hello pour l’abonnement de hello souhaité toouse pour ce projet.</span><span class="sxs-lookup"><span data-stu-id="1809e-121">If you have multiple subscriptions, click **Subscriptions** and select hello default directory for hello subscription you want toouse for this project.</span></span> <span data-ttu-id="1809e-122">Puis cliquez sur **appliquer** tooswitch toothat une vue d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="1809e-122">Then click **Apply** tooswitch toothat subscription view.</span></span>

1. <span data-ttu-id="1809e-123">Sélectionnez **Active Directory** à partir du menu hello située à gauche.</span><span class="sxs-lookup"><span data-stu-id="1809e-123">Select **Active Directory** from hello menu at left.</span></span> <span data-ttu-id="1809e-124">**Cliquez sur Nouveau &gt; Annuaire &gt; Création personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="1809e-124">**Click New > Directory > Custom Create**.</span></span>
2. <span data-ttu-id="1809e-125">Dans **Ajouter un annuaire**, sélectionnez **Créer un nouvel annuaire**.</span><span class="sxs-lookup"><span data-stu-id="1809e-125">In **Add Directory**, select **Create New Directory**.</span></span>
3. <span data-ttu-id="1809e-126">Dans **Nom**, entrez un nom d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="1809e-126">In **Name**, enter a directory name.</span></span>
4. <span data-ttu-id="1809e-127">Dans **Domaine**, entrez un nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="1809e-127">In **Domain**, enter a domain name.</span></span> <span data-ttu-id="1809e-128">Il s’agit d’un nom de domaine de base qui est inclus par défaut dans votre répertoire ; Il présente sous forme de hello `<domain_name>.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="1809e-128">This is a basic domain name that is included by default with your directory; it has hello form `<domain_name>.onmicrosoft.com`.</span></span> <span data-ttu-id="1809e-129">Vous pouvez nommer en fonction de nom de répertoire hello ou un autre nom de domaine que vous possédez.</span><span class="sxs-lookup"><span data-stu-id="1809e-129">You can name it based on hello directory name or another domain name that you own.</span></span> <span data-ttu-id="1809e-130">Par la suite, vous pouvez ajouter un autre nom de domaine que votre organisation utilise déjà.</span><span class="sxs-lookup"><span data-stu-id="1809e-130">Later, you can add another domain name that your organization already uses.</span></span>
5. <span data-ttu-id="1809e-131">Dans **Pays ou région**, sélectionnez votre paramètre régional.</span><span class="sxs-lookup"><span data-stu-id="1809e-131">In **Country or region**, select your locale.</span></span>

<span data-ttu-id="1809e-132">Pour plus d'informations sur AD, consultez la page [Qu'est-ce qu'un annuaire Azure AD][What is an Azure AD directory]?</span><span class="sxs-lookup"><span data-stu-id="1809e-132">For more information on AD, see [What is an Azure AD directory][What is an Azure AD directory]?</span></span>

### <a name="create-a-management-certificate-for-azure"></a><span data-ttu-id="1809e-133">Création d’un certificat de gestion pour Azure</span><span class="sxs-lookup"><span data-stu-id="1809e-133">Create a Management Certificate for Azure</span></span>
<span data-ttu-id="1809e-134">Hello SDK Azure pour Java utilise tooauthenticate de certificats de gestion avec des abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="1809e-134">hello Azure SDK for Java uses management certificates tooauthenticate with Azure subscriptions.</span></span> <span data-ttu-id="1809e-135">Il s’agit d’utiliser de tooauthenticate une application cliente qui utilise tooact des API de gestion hello pour le compte de ressources d’abonnement toomanage hello abonnement propriétaire de certificats X.509 v3.</span><span class="sxs-lookup"><span data-stu-id="1809e-135">These are X.509 v3 certificates you use tooauthenticate a client application that uses hello Service Management API tooact on behalf of hello subscription owner toomanage subscription resources.</span></span>

<span data-ttu-id="1809e-136">code Hello dans cette procédure utilise un certificat auto-signé de tooauthenticate avec Azure.</span><span class="sxs-lookup"><span data-stu-id="1809e-136">hello code in this procedure uses a self-signed certificate tooauthenticate with Azure.</span></span> <span data-ttu-id="1809e-137">Pour cette procédure, vous devez toocreate un certificat et le télécharger toohello [portail Azure classic] [ Azure classic portal] au préalable.</span><span class="sxs-lookup"><span data-stu-id="1809e-137">For this procedure, you need toocreate a certificate and upload it toohello [Azure classic portal][Azure classic portal] beforehand.</span></span> <span data-ttu-id="1809e-138">Cette opération implique hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1809e-138">This involves hello following steps:</span></span>

* <span data-ttu-id="1809e-139">Générer un fichier PFX représentant votre certificat client et l’enregistrer en local</span><span class="sxs-lookup"><span data-stu-id="1809e-139">Generate a PFX file representing your client certificate and save it locally.</span></span>
* <span data-ttu-id="1809e-140">Générer un certificat de gestion (fichier CER) dans le fichier PFX hello.</span><span class="sxs-lookup"><span data-stu-id="1809e-140">Generate a management certificate (CER file) from hello PFX file.</span></span>
* <span data-ttu-id="1809e-141">Téléchargez tooyour de fichier CER hello abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="1809e-141">Upload hello CER file tooyour Azure subscription.</span></span>
* <span data-ttu-id="1809e-142">Convertir le fichier PFX hello JKS, étant donné que Java utilise ce tooauthenticate de format à l’aide de certificats.</span><span class="sxs-lookup"><span data-stu-id="1809e-142">Convert hello PFX file into JKS, because Java uses that format tooauthenticate using certificates.</span></span>
* <span data-ttu-id="1809e-143">Écrire du code d’authentification de l’application hello, qui fait référence le fichier JKS toohello local.</span><span class="sxs-lookup"><span data-stu-id="1809e-143">Write hello application's authentication code, which refers toohello local JKS file.</span></span>

<span data-ttu-id="1809e-144">Lorsque vous effectuez cette procédure, certificat CER hello résidera dans votre abonnement Azure et certificat JKS hello doit résider sur votre disque local.</span><span class="sxs-lookup"><span data-stu-id="1809e-144">When you complete this procedure, hello CER certificate will reside in your Azure subscription and hello JKS certificate will reside on your local drive.</span></span> <span data-ttu-id="1809e-145">Pour plus d’informations sur les certificats de gestion, consultez la page [Créer et télécharger un certificat de gestion pour Microsoft Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="1809e-145">For more information on management certificates, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="create-a-certificate"></a><span data-ttu-id="1809e-146">Création d’un certificat</span><span class="sxs-lookup"><span data-stu-id="1809e-146">Create a certificate</span></span>
<span data-ttu-id="1809e-147">toocreate votre propre certificat auto-signé, ouvrez une console de commande sur votre système d’exploitation et exécutez hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="1809e-147">toocreate your own self-signed certificate, open a command console on your operating system and run hello following commands.</span></span>

> <span data-ttu-id="1809e-148">**Remarque :** ordinateur hello sur lequel vous exécutez cette commande doit avoir hello JDK installé.</span><span class="sxs-lookup"><span data-stu-id="1809e-148">**Note:**  hello computer on which you run this command must have hello JDK installed.</span></span> <span data-ttu-id="1809e-149">En outre, hello chemin d’accès toohello keytool dépend de l’emplacement hello dans lequel vous installez hello JDK.</span><span class="sxs-lookup"><span data-stu-id="1809e-149">Also, hello path toohello keytool depends on hello location in which you install hello JDK.</span></span> <span data-ttu-id="1809e-150">Pour plus d’informations, consultez [clé et l’outil de gestion de certificat (keytool)] [ Key and Certificate Management Tool (keytool)] dans la documentation en ligne de hello Java.</span><span class="sxs-lookup"><span data-stu-id="1809e-150">For more information, see [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] in hello Java online docs.</span></span>
> 
> 

<span data-ttu-id="1809e-151">fichier .pfx de hello toocreate :</span><span class="sxs-lookup"><span data-stu-id="1809e-151">toocreate hello .pfx file:</span></span>

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

<span data-ttu-id="1809e-152">toocreate de fichier .cer hello :</span><span class="sxs-lookup"><span data-stu-id="1809e-152">toocreate hello .cer file:</span></span>

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

<span data-ttu-id="1809e-153">où :</span><span class="sxs-lookup"><span data-stu-id="1809e-153">where:</span></span>

* <span data-ttu-id="1809e-154">`<java-install-dir>`est hello chemin d’accès toohello répertoire dans lequel vous avez installé Java.</span><span class="sxs-lookup"><span data-stu-id="1809e-154">`<java-install-dir>` is hello path toohello directory in which you installed Java.</span></span>
* <span data-ttu-id="1809e-155">`<keystore-id>`est l’identificateur de l’entrée keystore hello (par exemple, `AzureRemoteAccess`).</span><span class="sxs-lookup"><span data-stu-id="1809e-155">`<keystore-id>` is hello keystore entry identifier (for example, `AzureRemoteAccess`).</span></span>
* <span data-ttu-id="1809e-156">`<cert-store-dir>`est hello chemin toohello répertoire dans lequel vous souhaitez toostore certificats (par exemple `C:/Certificates`).</span><span class="sxs-lookup"><span data-stu-id="1809e-156">`<cert-store-dir>` is hello path toohello directory in which you want toostore certificates (for example `C:/Certificates`).</span></span>
* <span data-ttu-id="1809e-157">`<cert-file-name>`est le nom hello hello du fichier de certificat (par exemple `AzureWebDemoCert`).</span><span class="sxs-lookup"><span data-stu-id="1809e-157">`<cert-file-name>` is hello name of hello certificate file (for example `AzureWebDemoCert`).</span></span>
* <span data-ttu-id="1809e-158">`<password>`mot de passe hello vous choisissez tooprotect hello certificat ; Il doit être au moins 6 caractères.</span><span class="sxs-lookup"><span data-stu-id="1809e-158">`<password>` is hello password you choose tooprotect hello certificate; it must be at least 6 characters long.</span></span> <span data-ttu-id="1809e-159">Vous avez la possibilité de n’entrer aucun mot de passe, même si cela n’est pas recommandé.</span><span class="sxs-lookup"><span data-stu-id="1809e-159">You can enter no password, although this is not recommended.</span></span>
* <span data-ttu-id="1809e-160">`<dname>`est toobe de nom unique X.500 hello associée alias et est utilisé en tant que l’émetteur de hello et d’objet dans le certificat auto-signé de hello.</span><span class="sxs-lookup"><span data-stu-id="1809e-160">`<dname>` is hello X.500 Distinguished Name toobe associated with alias, and is used as hello issuer and subject fields in hello self-signed certificate.</span></span>

<span data-ttu-id="1809e-161">Pour plus d'informations, consultez [Create and upload a management certificate for Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="1809e-161">For more information, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="upload-hello-certificate"></a><span data-ttu-id="1809e-162">Télécharger le certificat de hello</span><span class="sxs-lookup"><span data-stu-id="1809e-162">Upload hello certificate</span></span>
<span data-ttu-id="1809e-163">tooupload tooAzure un certificat auto-signé, accédez toohello **paramètres** dans le portail classique de hello, puis cliquez sur hello **certificats de gestion** onglet. Cliquez sur **télécharger** bas hello hello page et naviguer emplacement toohello du fichier CER de hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="1809e-163">tooupload a self-signed certificate tooAzure, go toohello **Settings** page in hello classic portal, then click hello **Management Certificates** tab. Click **Upload** at hello bottom of hello page and navigate toohello location of hello CER file you created.</span></span>

#### <a name="convert-hello-pfx-file-into-jks"></a><span data-ttu-id="1809e-164">Convertir le fichier PFX hello JKS</span><span class="sxs-lookup"><span data-stu-id="1809e-164">Convert hello PFX file into JKS</span></span>
<span data-ttu-id="1809e-165">Bonjour invite de commandes Windows (en cours d’exécution en tant qu’administrateur), cd toohello répertoire contenant hello certificats et exécutez hello suivant de commande, où `<java-install-dir>` est le répertoire hello dans lequel vous avez installé Java sur votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="1809e-165">In hello Windows Command Prompt (running as admin), cd toohello directory containing hello certificates and run hello following command, where `<java-install-dir>` is hello directory in which you installed Java on your computer:</span></span>

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. <span data-ttu-id="1809e-166">Lorsque vous y êtes invité, entrez le mot de passe du magasin de clés de destination hello ; Il s’agit d’un mot de passe hello pour le fichier JKS hello.</span><span class="sxs-lookup"><span data-stu-id="1809e-166">When prompted, enter hello destination keystore password; this will be hello password for hello JKS file.</span></span>
2. <span data-ttu-id="1809e-167">Lorsque vous y êtes invité, entrez le mot de passe du magasin de clés du source de hello ; Il s’agit d’un mot de passe hello que vous avez spécifié pour le fichier PFX hello.</span><span class="sxs-lookup"><span data-stu-id="1809e-167">When prompted, enter hello source keystore password; this is hello password you specified for hello PFX file.</span></span>

<span data-ttu-id="1809e-168">deux mots de passe Hello n’ont pas de toobe hello identiques.</span><span class="sxs-lookup"><span data-stu-id="1809e-168">hello two passwords do not have toobe hello same.</span></span> <span data-ttu-id="1809e-169">Vous avez la possibilité de n’entrer aucun mot de passe, même si cela n’est pas recommandé.</span><span class="sxs-lookup"><span data-stu-id="1809e-169">You can enter no password, although this is not recommended.</span></span>

## <a name="build-a-web-app-creation-application"></a><span data-ttu-id="1809e-170">Création d’une application de création d’application web</span><span class="sxs-lookup"><span data-stu-id="1809e-170">Build a Web App creation application</span></span>
### <a name="create-hello-eclipse-workspace-and-maven-project"></a><span data-ttu-id="1809e-171">Créer hello d’espace de travail Eclipse et Maven projet</span><span class="sxs-lookup"><span data-stu-id="1809e-171">Create hello Eclipse Workspace and Maven Project</span></span>
<span data-ttu-id="1809e-172">Dans cette section, vous créez un espace de travail et un projet Maven pour l’application de la création de hello web app, nommé AzureWebDemo.</span><span class="sxs-lookup"><span data-stu-id="1809e-172">In this section you create a workspace and a Maven project for hello web app creation application, named AzureWebDemo.</span></span>

1. <span data-ttu-id="1809e-173">Créez un projet Maven.</span><span class="sxs-lookup"><span data-stu-id="1809e-173">Create a new Maven project.</span></span> <span data-ttu-id="1809e-174">Cliquez sur **Fichier > Nouveau > Projet Maven**.</span><span class="sxs-lookup"><span data-stu-id="1809e-174">Click **File > New > Maven Project**.</span></span> <span data-ttu-id="1809e-175">Dans **Nouveau projet Maven**, sélectionnez **Créer un projet simple** et **Utiliser l’emplacement de l’espace de travail par défaut**.</span><span class="sxs-lookup"><span data-stu-id="1809e-175">In **New Maven Project**, select **Create a simple project** and **Use default workspace location**.</span></span>
2. <span data-ttu-id="1809e-176">Sur la deuxième page de hello de **nouveau projet Maven**, spécifiez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="1809e-176">On hello second page of **New Maven Project**, specify hello following:</span></span>
   
   * <span data-ttu-id="1809e-177">ID de groupe : `com.<username>.azure.webdemo`</span><span class="sxs-lookup"><span data-stu-id="1809e-177">Group ID: `com.<username>.azure.webdemo`</span></span>
   * <span data-ttu-id="1809e-178">ID d’artefact : AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="1809e-178">Artifact ID: AzureWebDemo</span></span>
   * <span data-ttu-id="1809e-179">Version : 0.0.1-SNAPSHOT</span><span class="sxs-lookup"><span data-stu-id="1809e-179">Version: 0.0.1-SNAPSHOT</span></span>
   * <span data-ttu-id="1809e-180">Packaging : ar</span><span class="sxs-lookup"><span data-stu-id="1809e-180">Packaging: jar</span></span>
   * <span data-ttu-id="1809e-181">Nom : AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="1809e-181">Name: AzureWebDemo</span></span>
     
     <span data-ttu-id="1809e-182">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="1809e-182">Click **Finish**.</span></span>
3. <span data-ttu-id="1809e-183">Ouvrez le fichier de pom.xml de hello du nouveau projet dans l’Explorateur de projets.</span><span class="sxs-lookup"><span data-stu-id="1809e-183">Open hello new project's pom.xml file in Project Explorer.</span></span> <span data-ttu-id="1809e-184">Sélectionnez hello **dépendances** onglet. Comme il s’agit d’un nouveau projet, aucun package n’est encore répertorié.</span><span class="sxs-lookup"><span data-stu-id="1809e-184">Select hello **Dependencies** tab. As this is a new project, no packages are listed yet.</span></span>
4. <span data-ttu-id="1809e-185">Ouvrez hello Maven référentiels afficher.</span><span class="sxs-lookup"><span data-stu-id="1809e-185">Open hello Maven Repositories view.</span></span> <span data-ttu-id="1809e-186">**Cliquez sur Fenêtre &gt; Afficher la vue &gt; Autres &gt; Maven &gt; Référentiels Maven** , puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1809e-186">**Click Window > Show View > Other > Maven > Maven Repositories** and click **OK**.</span></span> <span data-ttu-id="1809e-187">Hello **Maven référentiels** affichage apparaîtra bas hello hello IDE.</span><span class="sxs-lookup"><span data-stu-id="1809e-187">hello **Maven Repositories** view will appear at hello bottom of hello IDE.</span></span>
5. <span data-ttu-id="1809e-188">Ouvrez **référentiels globaux**, avec le bouton hello **central** référentiel, puis sélectionnez **reconstruire l’Index**.</span><span class="sxs-lookup"><span data-stu-id="1809e-188">Open **Global Repositories**, right-click hello **central** repository, and select **Rebuild Index**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="1809e-189">Cette étape peut prendre plusieurs minutes selon la vitesse de hello de votre connexion.</span><span class="sxs-lookup"><span data-stu-id="1809e-189">This step can take several minutes depending on hello speed of your connection.</span></span> <span data-ttu-id="1809e-190">Lorsque les reconstructions d’index de hello, vous devez voir les packages de Microsoft Azure hello Bonjour **central** référentiel de Maven.</span><span class="sxs-lookup"><span data-stu-id="1809e-190">When hello index rebuilds, you should see hello Microsoft Azure packages in hello **central** Maven repository.</span></span>
6. <span data-ttu-id="1809e-191">Dans **Dépendances**, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1809e-191">In **Dependencies**, click **Add**.</span></span> <span data-ttu-id="1809e-192">Dans **Entrer l’ID de groupe...**, entrez `azure-management`.</span><span class="sxs-lookup"><span data-stu-id="1809e-192">In **Enter Group ID...** enter `azure-management`.</span></span> <span data-ttu-id="1809e-193">Sélectionnez les packages hello pour la gestion de base et la gestion de l’application de Service Web Apps :</span><span class="sxs-lookup"><span data-stu-id="1809e-193">Select hello packages for base management and App Service Web Apps management:</span></span>
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > <span data-ttu-id="1809e-194">**Remarque :** si vous mettez à jour les dépendances hello après une nouvelle version de version, vous devez toore-ajouter des dépendances de hello dans cette liste.</span><span class="sxs-lookup"><span data-stu-id="1809e-194">**Note:** If you are updating hello dependencies after a new version release, you need toore-add each of hello dependencies in this list.</span></span>
   > <span data-ttu-id="1809e-195">Après avoir cliqué sur **ajouter** et sélectionnez chaque dépendance, il s’affiche avec le nouveau numéro de version hello Bonjour **dépendances** liste.</span><span class="sxs-lookup"><span data-stu-id="1809e-195">After you click **Add** and select each dependency, it appears with hello new version number in hello **Dependencies** list.</span></span>
   > 
   > 

<span data-ttu-id="1809e-196">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1809e-196">Click **OK**.</span></span> <span data-ttu-id="1809e-197">Hello packages Azure, puis s’affichent dans hello **dépendances** liste.</span><span class="sxs-lookup"><span data-stu-id="1809e-197">hello Azure packages then appear in hello **Dependencies** list.</span></span>

### <a name="writing-java-code-toocreate-a-web-app-by-calling-hello-azure-sdk"></a><span data-ttu-id="1809e-198">Écrire du Code Java tooCreate une application Web à appeler hello Azure SDK</span><span class="sxs-lookup"><span data-stu-id="1809e-198">Writing Java Code tooCreate a Web App by Calling hello Azure SDK</span></span>
<span data-ttu-id="1809e-199">Ensuite, écrivez le code hello qui appelle des API Bonjour Azure SDK pour hello de toocreate Java application Service web d’application.</span><span class="sxs-lookup"><span data-stu-id="1809e-199">Next, write hello code that calls APIs in hello Azure SDK for Java toocreate hello App Service web app.</span></span>

1. <span data-ttu-id="1809e-200">Créer un point de code de Java classe toocontain hello entrée principal.</span><span class="sxs-lookup"><span data-stu-id="1809e-200">Create a Java class toocontain hello main entry point code.</span></span> <span data-ttu-id="1809e-201">Dans l’Explorateur de projets, avec le bouton droit sur le nœud de projet hello et sélectionnez **Nouveau > classe**.</span><span class="sxs-lookup"><span data-stu-id="1809e-201">In Project Explorer, right-click on hello project node and select **New > Class**.</span></span>
2. <span data-ttu-id="1809e-202">Dans **nouvelle classe Java**, nommez la classe hello `WebCreator` et vérifiez hello **principal de void statique publique** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="1809e-202">In **New Java Class**, name hello class `WebCreator` and check hello **public static void main** checkbox.</span></span> <span data-ttu-id="1809e-203">les sélections de Hello doivent apparaître comme suit :</span><span class="sxs-lookup"><span data-stu-id="1809e-203">hello selections should appear as follows:</span></span>
   
    ![][2]
3. <span data-ttu-id="1809e-204">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="1809e-204">Click **Finish**.</span></span> <span data-ttu-id="1809e-205">fichier de WebCreator.java Hello s’affiche dans l’Explorateur de projets.</span><span class="sxs-lookup"><span data-stu-id="1809e-205">hello WebCreator.java file appears in Project Explorer.</span></span>

### <a name="calling-hello-azure-api-toocreate-an-app-service-web-app"></a><span data-ttu-id="1809e-206">Appel de tooCreate des API Azure hello une application de Service d’applications Web</span><span class="sxs-lookup"><span data-stu-id="1809e-206">Calling hello Azure API tooCreate an App Service Web App</span></span>
#### <a name="add-necessary-imports"></a><span data-ttu-id="1809e-207">Ajout des importations nécessaires</span><span class="sxs-lookup"><span data-stu-id="1809e-207">Add necessary imports</span></span>
<span data-ttu-id="1809e-208">Dans WebCreator.java, ajoutez hello suivant importations ; ces importations fournissent des bibliothèques de gestion tooclasses accès Bonjour pour consommer des API Azure :</span><span class="sxs-lookup"><span data-stu-id="1809e-208">In WebCreator.java, add hello following imports; these imports provide access tooclasses in hello management libraries for consuming Azure APIs:</span></span>

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


#### <a name="define-hello-main-entry-point-class"></a><span data-ttu-id="1809e-209">Définir la classe de point d’entrée principal hello</span><span class="sxs-lookup"><span data-stu-id="1809e-209">Define hello main entry point class</span></span>
<span data-ttu-id="1809e-210">Car hello hello AzureWebDemo application vise toocreate une application de Service d’applications Web, nommez la classe principale hello pour cette application `WebAppCreator`.</span><span class="sxs-lookup"><span data-stu-id="1809e-210">Because hello purpose of hello AzureWebDemo application is toocreate an App Service Web App, name hello main class for this application `WebAppCreator`.</span></span> <span data-ttu-id="1809e-211">Cette classe fournit hello entrée principal point de code qui appelle l’application web hello API de gestion des services Azure toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="1809e-211">This class provides hello main entry point code that calls hello Azure Service Management API toocreate hello web app.</span></span>

<span data-ttu-id="1809e-212">Ajoutez hello suivant des définitions de paramètres de l’application web hello et espace Web.</span><span class="sxs-lookup"><span data-stu-id="1809e-212">Add hello following parameter definitions for hello web app and webspace.</span></span> <span data-ttu-id="1809e-213">Vous devez tooprovide vos propres informations de certificat et les ID d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="1809e-213">You will need tooprovide your own Azure subscription ID and certificate information.</span></span>

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

<span data-ttu-id="1809e-214">où :</span><span class="sxs-lookup"><span data-stu-id="1809e-214">where:</span></span>

* <span data-ttu-id="1809e-215">`<subscription-id>`est l’ID d’abonnement Azure hello dans lequel vous souhaitez que la ressource de hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="1809e-215">`<subscription-id>` is hello Azure subscription ID in which you want toocreate hello resource.</span></span>
* <span data-ttu-id="1809e-216">`<certificate-store-path>`est hello chemin d’accès et nom de fichier toohello JKS le fichier dans votre répertoire du magasin de certificats local.</span><span class="sxs-lookup"><span data-stu-id="1809e-216">`<certificate-store-path>` is hello path and filename toohello JKS file in your local certificate store directory.</span></span> <span data-ttu-id="1809e-217">Par exemple, `C:/Certificates/CertificateName.jks` pour Linux et `C:\Certificates\CertificateName.jks` pour Windows.</span><span class="sxs-lookup"><span data-stu-id="1809e-217">For example, `C:/Certificates/CertificateName.jks` for Linux and `C:\Certificates\CertificateName.jks` for Windows.</span></span>
* <span data-ttu-id="1809e-218">`<certificate-password>`est un mot de passe hello spécifié lorsque vous avez créé votre certificat JKS.</span><span class="sxs-lookup"><span data-stu-id="1809e-218">`<certificate-password>` is hello password you specified when you created your JKS certificate.</span></span>
* <span data-ttu-id="1809e-219">`webAppName`peut être n’importe quel nom que vous choisissez ; Cette procédure utilise le nom de hello `WebDemoWebApp`.</span><span class="sxs-lookup"><span data-stu-id="1809e-219">`webAppName` can be any name you choose; this procedure uses hello name `WebDemoWebApp`.</span></span> <span data-ttu-id="1809e-220">nom de domaine complet Hello est hello `webAppName` avec hello `domainName` ajouté, par conséquent, dans ce cas hello complète domaine est `webdemowebapp.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="1809e-220">hello full domain name is hello `webAppName` with hello `domainName` appended, so in this case hello full domain is `webdemowebapp.azurewebsites.net`.</span></span>
* <span data-ttu-id="1809e-221">`domainName` doit être spécifié comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="1809e-221">`domainName` should be specified as shown above.</span></span>
* <span data-ttu-id="1809e-222">`webSpaceName`doit être une des valeurs de hello définies dans hello [WebSpaceNames] [ WebSpaceNames] classe.</span><span class="sxs-lookup"><span data-stu-id="1809e-222">`webSpaceName` should be one of hello values defined in hello [WebSpaceNames][WebSpaceNames] class.</span></span>
* <span data-ttu-id="1809e-223">`appServicePlanName` doit être spécifié comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="1809e-223">`appServicePlanName` should be specified as shown above.</span></span>

> <span data-ttu-id="1809e-224">**Remarque :** chaque fois que vous exécutez cette application, vous devez la valeur hello toochange `webAppName` et `appServicePlanName` (ou supprimer l’application web de hello sur hello portail Azure) avant d’exécuter l’application hello.</span><span class="sxs-lookup"><span data-stu-id="1809e-224">**Note:** Each time you run this application, you need toochange hello value of `webAppName` and `appServicePlanName` (or delete hello web app on hello Azure Portal) before running hello application again.</span></span> <span data-ttu-id="1809e-225">Dans le cas contraire, l’exécution échoue car hello même ressource existe déjà dans Azure.</span><span class="sxs-lookup"><span data-stu-id="1809e-225">Otherwise, execution will fail because hello same resource already exists on Azure.</span></span>
> 
> 

#### <a name="define-hello-web-creation-method"></a><span data-ttu-id="1809e-226">Définir la méthode de création hello web</span><span class="sxs-lookup"><span data-stu-id="1809e-226">Define hello web creation method</span></span>
<span data-ttu-id="1809e-227">Définissez ensuite une application web de méthode toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="1809e-227">Next, define a method toocreate hello web app.</span></span> <span data-ttu-id="1809e-228">Cette méthode, `createWebApp`, spécifie les paramètres de hello de hello web app et espace Web de hello.</span><span class="sxs-lookup"><span data-stu-id="1809e-228">This method, `createWebApp`, specifies hello parameters of hello web app and hello webspace.</span></span> <span data-ttu-id="1809e-229">Il crée également et configure le client de gestion d’application Service Web Apps hello, qui est défini en hello [WebSiteManagementClient] [ WebSiteManagementClient] objet.</span><span class="sxs-lookup"><span data-stu-id="1809e-229">It also creates and configures hello App Service Web Apps management client, which is defined by hello [WebSiteManagementClient][WebSiteManagementClient] object.</span></span> <span data-ttu-id="1809e-230">client de gestion de Hello est toocreating clé des applications Web.</span><span class="sxs-lookup"><span data-stu-id="1809e-230">hello management client is key toocreating Web Apps.</span></span> <span data-ttu-id="1809e-231">Il fournit des services web RESTful qui autorisent des applications toomanage (exécution d’opérations telles que create, update et delete) des applications web en appelant l’API de gestion de service hello.</span><span class="sxs-lookup"><span data-stu-id="1809e-231">It provides RESTful web services that allow applications toomanage web apps (performing operations such as create, update, and delete) by calling hello service management API.</span></span>

    private static void createWebApp() throws Exception {

        // Specify configuration settings for hello App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path toohello JKS file
            keyStorePassword,  // Password for hello JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create hello App Service Web Apps management client toocall Azure APIs
        // and pass it hello App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for hello web app with hello specified parameters.
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
        // Note that hello server farm name takes hello Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define hello web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create hello web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output hello HTTP status code of hello response; 200 indicates hello request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output hello name of hello web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

<span data-ttu-id="1809e-232">le code Hello affiche l’état HTTP hello réponse hello indiquant la réussite ou l’échec et en cas de réussite, produira nom hello Hello créé l’application web.</span><span class="sxs-lookup"><span data-stu-id="1809e-232">hello code will output hello HTTP status of hello response indicating success or failure, and if successful, will output hello name of hello created web app.</span></span>

#### <a name="define-hello-main-method"></a><span data-ttu-id="1809e-233">Définir la méthode main() de hello</span><span class="sxs-lookup"><span data-stu-id="1809e-233">Define hello main() method</span></span>
<span data-ttu-id="1809e-234">Fournir le code de la méthode main() hello cette application web d’appels createWebApp() toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="1809e-234">Provide hello main() method code that calls createWebApp() toocreate hello web app.</span></span>

<span data-ttu-id="1809e-235">Enfin, appelez `createWebApp` à partir de `main` :</span><span class="sxs-lookup"><span data-stu-id="1809e-235">Finally, call `createWebApp` from `main`:</span></span>

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-hello-application-and-verify-web-app-creation"></a><span data-ttu-id="1809e-236">Exécutez l’application hello et vérifiez la création d’application web</span><span class="sxs-lookup"><span data-stu-id="1809e-236">Run hello application and verify web app creation</span></span>
<span data-ttu-id="1809e-237">tooverify votre application s’exécute, cliquez sur **exécuter > exécuter**.</span><span class="sxs-lookup"><span data-stu-id="1809e-237">tooverify that your application runs, click **Run > Run**.</span></span> <span data-ttu-id="1809e-238">Lors de l’application hello soit terminée, vous devez voir hello suivant la sortie dans la console hello Eclipse :</span><span class="sxs-lookup"><span data-stu-id="1809e-238">When hello application completes running, you should see hello following output in hello Eclipse console:</span></span>

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

<span data-ttu-id="1809e-239">Ouvrez une session hello portail Azure classic, puis cliquez sur **Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="1809e-239">Log into hello Azure classic portal and click **Web Apps**.</span></span> <span data-ttu-id="1809e-240">application web Hello doit apparaître dans la liste des applications Web hello dans quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="1809e-240">hello new web app should appear in hello Web Apps list within a few minutes.</span></span>

## <a name="deploying-an-application-toohello-web-app"></a><span data-ttu-id="1809e-241">Déploiement d’une application Web de toohello Application</span><span class="sxs-lookup"><span data-stu-id="1809e-241">Deploying an Application toohello Web App</span></span>
<span data-ttu-id="1809e-242">Une fois que vous avez exécuté AzureWebDemo et créées hello nouvelle application web, ouvrez une session sur le portail classique de hello, cliquez sur **Web Apps**, puis sélectionnez **WebDemoWebApp** Bonjour **Web Apps** liste.</span><span class="sxs-lookup"><span data-stu-id="1809e-242">After you have run AzureWebDemo and created hello new web app, log into hello classic portal, click **Web Apps**, and select **WebDemoWebApp** in hello **Web Apps** list.</span></span> <span data-ttu-id="1809e-243">Dans la page du tableau de bord de l’application hello web, cliquez sur **Parcourir** (ou cliquez sur l’URL de hello, `webdemowebapp.azurewebsites.net`) toonavigate tooit.</span><span class="sxs-lookup"><span data-stu-id="1809e-243">In hello web app's dashboard page, click **Browse** (or click hello URL, `webdemowebapp.azurewebsites.net`) toonavigate tooit.</span></span> <span data-ttu-id="1809e-244">Vous verrez une page de l’espace réservé vide, car aucun contenu n’a encore été toohello publié l’application web.</span><span class="sxs-lookup"><span data-stu-id="1809e-244">You will see a blank placeholder page, because no content has been published toohello web app yet.</span></span>

<span data-ttu-id="1809e-245">Ensuite vous créez une application « Hello World » et déployer l’application web toohello.</span><span class="sxs-lookup"><span data-stu-id="1809e-245">Next you will create a "Hello World" application and deploy it toohello web app.</span></span>

### <a name="create-a-jsp-hello-world-application"></a><span data-ttu-id="1809e-246">Création d’une application JSP Hello World</span><span class="sxs-lookup"><span data-stu-id="1809e-246">Create a JSP Hello World application</span></span>
#### <a name="create-hello-application"></a><span data-ttu-id="1809e-247">Créer l’application hello</span><span class="sxs-lookup"><span data-stu-id="1809e-247">Create hello application</span></span>
<span data-ttu-id="1809e-248">Dans toodemonstrate commande comment toodeploy web application toohello, hello procédure vous montre comment toocreate une application Java de « Hello World » simple et chargez-le toohello application Service d’applications Web créés par votre application.</span><span class="sxs-lookup"><span data-stu-id="1809e-248">In order toodemonstrate how toodeploy an application toohello web, hello following procedure shows you how toocreate a simple "Hello World" Java application and upload it toohello App Service Web App that your application created.</span></span>

1. <span data-ttu-id="1809e-249">Cliquez sur **Fichier > Nouveau > Projet Web dynamique**.</span><span class="sxs-lookup"><span data-stu-id="1809e-249">Click **File > New > Dynamic Web Project**.</span></span> <span data-ttu-id="1809e-250">Nommez-le `JSPHello`.</span><span class="sxs-lookup"><span data-stu-id="1809e-250">Name it `JSPHello`.</span></span> <span data-ttu-id="1809e-251">Il est inutile toochange tous les autres paramètres dans cette boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1809e-251">You do not need toochange any other settings in this dialog.</span></span> <span data-ttu-id="1809e-252">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="1809e-252">Click **Finish**.</span></span>
   
    ![][3]
2. <span data-ttu-id="1809e-253">Dans l’Explorateur de projets, développez hello **JSPHello** de projet, cliquez sur **WebContent**, puis cliquez sur **Nouveau > fichier JSP**.</span><span class="sxs-lookup"><span data-stu-id="1809e-253">In Project Explorer, expand hello **JSPHello** project, right-click **WebContent**, then click **New > JSP File**.</span></span> <span data-ttu-id="1809e-254">Dans la boîte de dialogue Nouveau fichier JSP hello, nommez le nouveau fichier de hello `index.jsp`.</span><span class="sxs-lookup"><span data-stu-id="1809e-254">In hello New JSP File dialog, name hello new file `index.jsp`.</span></span> <span data-ttu-id="1809e-255">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="1809e-255">Click **Next**.</span></span>
3. <span data-ttu-id="1809e-256">Bonjour **sélectionner un modèle JSP** boîte de dialogue, sélectionnez **nouveau fichier JSP (html)** et cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="1809e-256">In hello **Select JSP Template** dialog, select **New JSP File (html)** and click **Finish**.</span></span>
4. <span data-ttu-id="1809e-257">Dans index.jsp, ajoutez hello suivant code Bonjour `<head>` et `<body>` balise sections :</span><span class="sxs-lookup"><span data-stu-id="1809e-257">In index.jsp, add hello following code in hello `<head>` and `<body>` tag sections:</span></span>
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, hello time is <%= date %> 
        </body>

#### <a name="run-hello-hello-world-application-in-localhost"></a><span data-ttu-id="1809e-258">Exécutez l’application hello Hello World dans localhost</span><span class="sxs-lookup"><span data-stu-id="1809e-258">Run hello Hello World application in localhost</span></span>
<span data-ttu-id="1809e-259">Avant d’exécuter cette application, vous devez tooconfigure quelques propriétés.</span><span class="sxs-lookup"><span data-stu-id="1809e-259">Before you run this application, you need tooconfigure a few properties.</span></span>

1. <span data-ttu-id="1809e-260">Avec le bouton hello **JSPHello** de projet et sélectionnez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="1809e-260">Right-click hello **JSPHello** project and select **Properties**.</span></span>
2. <span data-ttu-id="1809e-261">Bonjour **propriétés** boîte de dialogue : sélectionnez **chemin d’accès de Build Java**, sélectionnez hello **de commande et d’exportation** onglet, vérifiez **bibliothèque de système de JRE**, puis cliquez sur **Des** toomove il haut toohello de liste de hello.</span><span class="sxs-lookup"><span data-stu-id="1809e-261">In hello **Properties** dialog: select **Java Build Path**, select hello **Order and Export** tab, check **JRE System Library**, then click **Up** toomove it toohello top of hello list.</span></span>
   
    ![][4]
3. <span data-ttu-id="1809e-262">Également dans hello **propriétés** boîte de dialogue : sélectionnez **ciblée des Runtimes** et cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="1809e-262">Also in hello **Properties** dialog: select **Targeted Runtimes** and click **New**.</span></span>
4. <span data-ttu-id="1809e-263">Bonjour **nouvel environnement d’exécution serveur** boîte de dialogue, sélectionnez un serveur comme **Apache Tomcat v7.0** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="1809e-263">In hello **New Server Runtime Environment** dialog, select a server such as **Apache Tomcat v7.0** and click **Next**.</span></span> <span data-ttu-id="1809e-264">Bonjour **serveur Tomcat** boîte de dialogue, définissez **nom** trop`Apache Tomcat v7.0`et la valeur **répertoire d’Installation de Tomcat** Active toohello dans lequel vous hello de version Tomcat serveur toouse.</span><span class="sxs-lookup"><span data-stu-id="1809e-264">In hello **Tomcat Server** dialog, set **Name** too`Apache Tomcat v7.0`, and set **Tomcat Installation Directory** toohello directory in which you installed hello version of Tomcat server you want toouse.</span></span>
   
    ![][5]
   
    <span data-ttu-id="1809e-265">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="1809e-265">Click **Finish**.</span></span>
5. <span data-ttu-id="1809e-266">Vous retournez puis toohello **ciblée des Runtimes** page Hello **propriétés** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1809e-266">You then return toohello **Targeted Runtimes** page of hello **Properties** dialog.</span></span> <span data-ttu-id="1809e-267">Sélectionnez **Apache Tomcat v7.0**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1809e-267">Select **Apache Tomcat v7.0**, then click **OK**.</span></span>
   
    ![][6]
6. <span data-ttu-id="1809e-268">Bonjour Eclipse **exécuter** menu, cliquez sur **exécuter**.</span><span class="sxs-lookup"><span data-stu-id="1809e-268">In hello Eclipse **Run** menu, click **Run**.</span></span> <span data-ttu-id="1809e-269">Bonjour **exécuter en tant que** boîte de dialogue, sélectionnez **s’exécutent sur le serveur**.</span><span class="sxs-lookup"><span data-stu-id="1809e-269">In hello **Run As** dialog, select **Run on Server**.</span></span> <span data-ttu-id="1809e-270">Bonjour **s’exécutent sur le serveur** boîte de dialogue, sélectionnez **Tomcat v7.0 serveur**:</span><span class="sxs-lookup"><span data-stu-id="1809e-270">In hello **Run on Server** dialog, select **Tomcat v7.0 Server**:</span></span>
   
    ![][7]
   
    <span data-ttu-id="1809e-271">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="1809e-271">Click **Finish**.</span></span>
7. <span data-ttu-id="1809e-272">Hello lorsque les exécutions de l’application, vous devez voir hello **JSPHello** page apparaît dans une fenêtre de localhost dans Eclipse (`http://localhost:8080/JSPHello/`), affichage hello message suivant :</span><span class="sxs-lookup"><span data-stu-id="1809e-272">When hello application runs, you should see hello **JSPHello** page appear in a localhost window in Eclipse (`http://localhost:8080/JSPHello/`), displaying hello following message:</span></span>
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-hello-application-as-a-war"></a><span data-ttu-id="1809e-273">Exporter l’application hello comme un WAR</span><span class="sxs-lookup"><span data-stu-id="1809e-273">Export hello application as a WAR</span></span>
<span data-ttu-id="1809e-274">Exporter des fichiers de projet web hello en tant que fichier d’archive (WAR) web afin que vous pouvez le déployer l’application web toohello.</span><span class="sxs-lookup"><span data-stu-id="1809e-274">Export hello web project files as a web archive (WAR) file so that you can deploy it toohello web app.</span></span> <span data-ttu-id="1809e-275">Hello fichiers projet web suivants se trouvent dans le dossier de contenu Web hello :</span><span class="sxs-lookup"><span data-stu-id="1809e-275">hello following web project files reside in hello WebContent folder:</span></span>

    META-INF
    WEB-INF
    index.jsp

1. <span data-ttu-id="1809e-276">Cliquez sur le dossier de contenu Web hello et sélectionnez **exporter**.</span><span class="sxs-lookup"><span data-stu-id="1809e-276">Right-click hello WebContent folder and select **Export**.</span></span>
2. <span data-ttu-id="1809e-277">Bonjour **exporter Sélectionnez** boîte de dialogue, cliquez sur **Web > WAR** de fichier, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="1809e-277">In hello **Export Select** dialog, click **Web > WAR** file, then click **Next**.</span></span>
3. <span data-ttu-id="1809e-278">Bonjour **WAR exporter** boîte de dialogue, sélectionnez le répertoire de src hello hello projet en cours et inclure le nom hello du fichier WAR de hello à fin de hello.</span><span class="sxs-lookup"><span data-stu-id="1809e-278">In hello **WAR Export** dialog, select hello src directory in hello current project, and include hello name of hello WAR file at hello end.</span></span> <span data-ttu-id="1809e-279">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="1809e-279">For example:</span></span>
   
    `<project-path>/JSPHello/src/JSPHello.war`

<span data-ttu-id="1809e-280">Pour plus d’informations sur le déploiement des fichiers WAR, consultez [ajouter un tooAzure d’application Java App Service Web Apps](web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="1809e-280">For more information on deploying WAR files, see [Add a Java application tooAzure App Service Web Apps](web-sites-java-add-app.md).</span></span>

### <a name="deploying-hello-hello-world-application-using-ftp"></a><span data-ttu-id="1809e-281">Déploiement hello Hello World Application à l’aide de FTP</span><span class="sxs-lookup"><span data-stu-id="1809e-281">Deploying hello Hello World Application Using FTP</span></span>
<span data-ttu-id="1809e-282">Sélectionnez une application hello de tiers FTP client toopublish.</span><span class="sxs-lookup"><span data-stu-id="1809e-282">Select a third-party FTP client toopublish hello application.</span></span> <span data-ttu-id="1809e-283">Cette procédure décrit les deux options : console de Kudu hello intégrée à Azure ; et FileZilla, un outil populaire avec une interface utilisateur graphique pratique.</span><span class="sxs-lookup"><span data-stu-id="1809e-283">This procedure describes two options: hello Kudu console built into Azure; and FileZilla, a popular tool with a convenient, graphical UI.</span></span>

> <span data-ttu-id="1809e-284">**Remarque :** hello boîte à outils Azure pour Eclipse prend en charge les comptes de déploiement toostorage et cloud services, mais ne prend pas actuellement en charge les applications tooweb de déploiement.</span><span class="sxs-lookup"><span data-stu-id="1809e-284">**Note:** hello Azure Toolkit for Eclipse supports deployment toostorage accounts and cloud services, but does not currently support deployment tooweb apps.</span></span> <span data-ttu-id="1809e-285">Vous pouvez déployer des comptes toostorage et services à l’aide d’un projet de déploiement Azure comme décrit dans le cloud [création d’une Application Hello World pour Azure dans Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), mais pas les applications tooweb.</span><span class="sxs-lookup"><span data-stu-id="1809e-285">You can deploy toostorage accounts and cloud services using an Azure Deployment Project as described in [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), but not tooweb apps.</span></span> <span data-ttu-id="1809e-286">Utilisez d’autres méthodes telles que FTP ou GitHub tootransfer fichiers tooyour l’application web.</span><span class="sxs-lookup"><span data-stu-id="1809e-286">Use other methods such as FTP or GitHub tootransfer files tooyour web app.</span></span>
> 
> <span data-ttu-id="1809e-287">**Remarque :** nous ne recommandons pas à l’aide de FTP à partir de l’invite de commandes Windows hello (hello FTP.EXE utilitaire qui est fourni avec Windows).</span><span class="sxs-lookup"><span data-stu-id="1809e-287">**Note:** We do not recommend using FTP from hello Windows command prompt (hello command-line FTP.EXE utility that ships with Windows).</span></span> <span data-ttu-id="1809e-288">Les clients FTP qui utilisent FTP actif, telles que FTP.EXE, souvent basculent toowork pare-feu.</span><span class="sxs-lookup"><span data-stu-id="1809e-288">FTP clients that use active FTP, such as FTP.EXE, often fail toowork over firewalls.</span></span> <span data-ttu-id="1809e-289">FTP actif spécifie une adresse interne basée sur le réseau local, toowhich FTP server risquent de ne tooconnect.</span><span class="sxs-lookup"><span data-stu-id="1809e-289">Active FTP specifies an internal LAN-based address, toowhich an FTP server will likely fail tooconnect.</span></span>
> 
> 

<span data-ttu-id="1809e-290">Pour plus d’informations sur le déploiement tooan application Service web d’application à l’aide de FTP, consultez hello rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="1809e-290">For more information on deployment tooan App Service web app using FTP, see hello following topics:</span></span>

* [<span data-ttu-id="1809e-291">Déployer à l’aide d’un utilitaire FTP</span><span class="sxs-lookup"><span data-stu-id="1809e-291">Deploy using an FTP utility</span></span>](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a><span data-ttu-id="1809e-292">Configurer les informations d'identification du déploiement</span><span class="sxs-lookup"><span data-stu-id="1809e-292">Set up deployment credentials</span></span>
<span data-ttu-id="1809e-293">Assurez-vous que vous avez exécuté hello **AzureWebDemo** application toocreate une application web.</span><span class="sxs-lookup"><span data-stu-id="1809e-293">Make sure you have run hello **AzureWebDemo** application toocreate a web app.</span></span> <span data-ttu-id="1809e-294">Vous souhaitez transférer l’emplacement des fichiers toothis.</span><span class="sxs-lookup"><span data-stu-id="1809e-294">You will transfer files toothis location.</span></span>

1. <span data-ttu-id="1809e-295">Connectez-vous au portail classique de hello et cliquez sur **Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="1809e-295">Log into hello classic portal and click **Web Apps**.</span></span> <span data-ttu-id="1809e-296">Assurez-vous que **WebDemoWebApp** apparaît dans la liste hello d’applications web et assurez-vous qu’il s’exécute.</span><span class="sxs-lookup"><span data-stu-id="1809e-296">Make sure **WebDemoWebApp** appears in hello list of web apps, and make sure that it is running.</span></span> <span data-ttu-id="1809e-297">Cliquez sur **WebDemoWebApp** tooopen son **tableau de bord** page.</span><span class="sxs-lookup"><span data-stu-id="1809e-297">Click **WebDemoWebApp** tooopen its **Dashboard** page.</span></span>
2. <span data-ttu-id="1809e-298">Sur hello **tableau de bord** sous **aperçu rapide**, cliquez sur **configurer vos informations d’identification de déploiement** (si vous avez déjà des informations d’identification de déploiement, il lit  **Réinitialiser vos informations d’identification de déploiement**).</span><span class="sxs-lookup"><span data-stu-id="1809e-298">On hello **Dashboard** page, under **Quick Glance**, click **Set up your deployment credentials** (if you already have deployment credentials, this reads **Reset your deployment credentials**).</span></span>
   
    <span data-ttu-id="1809e-299">Les informations d'identification du déploiement sont associées à un compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1809e-299">Deployment credentials are associated with a Microsoft account.</span></span> <span data-ttu-id="1809e-300">Vous devez toospecify un nom d’utilisateur et mot de passe que vous pouvez utiliser toodeploy à l’aide de Git et FTP.</span><span class="sxs-lookup"><span data-stu-id="1809e-300">You need toospecify a username and password that you can use toodeploy using Git and FTP.</span></span> <span data-ttu-id="1809e-301">Vous pouvez utiliser ces toodeploy informations d’identification tooany l’application web dans tous les abonnements Azure associés à votre compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1809e-301">You can use these credentials toodeploy tooany web app in all Azure subscriptions associated with your Microsoft account.</span></span> <span data-ttu-id="1809e-302">Fournissez les informations d’identification de la déploiement Git et FTP dans la boîte de dialogue hello et nom d’utilisateur de l’enregistrement hello et un mot de passe pour un usage ultérieur.</span><span class="sxs-lookup"><span data-stu-id="1809e-302">Provide Git and FTP deployment credentials in hello dialog, and record hello username and password for future use.</span></span>

#### <a name="get-ftp-connection-information"></a><span data-ttu-id="1809e-303">Obtention des informations de connexion FTP</span><span class="sxs-lookup"><span data-stu-id="1809e-303">Get FTP connection information</span></span>
<span data-ttu-id="1809e-304">toouse FTP toodeploy application fichiers toohello nouvellement créé l’application web, vous devez tooobtain les informations de connexion.</span><span class="sxs-lookup"><span data-stu-id="1809e-304">toouse FTP toodeploy application files toohello newly created web app, you need tooobtain connection information.</span></span> <span data-ttu-id="1809e-305">Il existe deux façons de tooobtain les informations de connexion.</span><span class="sxs-lookup"><span data-stu-id="1809e-305">There are two ways tooobtain connection information.</span></span> <span data-ttu-id="1809e-306">Est l’application web toovisit hello **tableau de bord** page ; hello autre manière consiste toodownload hello web application le profil de publication.</span><span class="sxs-lookup"><span data-stu-id="1809e-306">One way is toovisit hello web app's **Dashboard** page; hello other way is toodownload hello web app's publish profile.</span></span> <span data-ttu-id="1809e-307">profil de publication Hello est un fichier XML qui fournit des informations telles que les informations d’identification d’ouverture de session et de nom de hôte FTP pour vos applications web dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="1809e-307">hello publish profile is an XML file that provides information such as FTP host name and logon credentials for your web apps in Azure App Service.</span></span> <span data-ttu-id="1809e-308">Vous pouvez utiliser cette application web tooany de toodeploy nom d’utilisateur et mot de passe de tous les abonnements associés à hello compte Azure, pas uniquement celui-ci.</span><span class="sxs-lookup"><span data-stu-id="1809e-308">You can use this username and password toodeploy tooany web app in all subscriptions associated with hello Azure account, not only this one.</span></span>

<span data-ttu-id="1809e-309">les informations de connexion tooobtain FTP à partir du Panneau de l’application hello web Bonjour [Azure Portal][Azure Portal]:</span><span class="sxs-lookup"><span data-stu-id="1809e-309">tooobtain FTP connection information from hello web app's blade in hello [Azure Portal][Azure Portal]:</span></span>

1. <span data-ttu-id="1809e-310">Sous **Essentials**, recherchez et copiez hello **nom d’hôte FTP**.</span><span class="sxs-lookup"><span data-stu-id="1809e-310">Under **Essentials**, find and copy hello **FTP hostname**.</span></span> <span data-ttu-id="1809e-311">Ceci est un URI similaire trop`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="1809e-311">This is a URI similar too`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span></span>
2. <span data-ttu-id="1809e-312">Sous **Essentials**, recherchez et copiez le **Nom d’utilisateur FTP/déploiement**.</span><span class="sxs-lookup"><span data-stu-id="1809e-312">Under **Essentials**, find and copy **FTP/Deployment username**.</span></span> <span data-ttu-id="1809e-313">Cela aura un formulaire de hello *webappname\deployment-username*; par exemple `WebDemoWebApp\deployer77`.</span><span class="sxs-lookup"><span data-stu-id="1809e-313">This will have hello form *webappname\deployment-username*; for example `WebDemoWebApp\deployer77`.</span></span>

<span data-ttu-id="1809e-314">informations de connexion FTP tooobtain de hello profil de publication :</span><span class="sxs-lookup"><span data-stu-id="1809e-314">tooobtain FTP connection information from hello publish profile:</span></span>

1. <span data-ttu-id="1809e-315">Dans le panneau de l’application hello web, cliquez sur **obtenir le profil de publication**.</span><span class="sxs-lookup"><span data-stu-id="1809e-315">In hello web app's blade, click **Get publish profile**.</span></span> <span data-ttu-id="1809e-316">Il télécharge un disque tooyour fichier .publishsettings.</span><span class="sxs-lookup"><span data-stu-id="1809e-316">This will download a .publishsettings file tooyour local drive.</span></span>
2. <span data-ttu-id="1809e-317">Ouvrez le fichier .publishsettings de hello dans un éditeur XML ou un éditeur de texte et de recherche hello `<publishProfile>` élément contenant `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="1809e-317">Open hello .publishsettings file in an XML editor or text editor and find hello `<publishProfile>` element containing `publishMethod="FTP"`.</span></span> <span data-ttu-id="1809e-318">Il doit ressembler à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="1809e-318">It should look like hello following:</span></span>
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. <span data-ttu-id="1809e-319">Notez cette application web hello `publishProfile` paramètres mappent les paramètres du Gestionnaire de Site FileZilla toohello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1809e-319">Note that hello web app's `publishProfile` settings map toohello FileZilla Site Manager settings as follows:</span></span>

* <span data-ttu-id="1809e-320">`publishUrl`est de même que hello **nom d’hôte FTP**, hello valeur définie dans **hôte**.</span><span class="sxs-lookup"><span data-stu-id="1809e-320">`publishUrl` is hello same as **FTP host name**, hello value you set in **Host**.</span></span>
* <span data-ttu-id="1809e-321">`publishMethod="FTP"`signifie que vous définissez **protocole** trop**FTP - File Transfer Protocol**, et **chiffrement** trop**utiliser FTP brut**.</span><span class="sxs-lookup"><span data-stu-id="1809e-321">`publishMethod="FTP"` means that you set **Protocol** too**FTP - File Transfer Protocol**, and **Encryption** too**Use plain FTP**.</span></span>
* <span data-ttu-id="1809e-322">`userName`et `userPWD` sont des valeurs réelles du nom d’utilisateur et mot de passe spécifié lorsque vous réinitialisez les informations d’identification de déploiement hello clés pour hello.</span><span class="sxs-lookup"><span data-stu-id="1809e-322">`userName` and `userPWD` are keys for hello actual username and password values you specified when you reset hello deployment credentials.</span></span> <span data-ttu-id="1809e-323">`userName`est de même que hello **déploiement / FTP utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="1809e-323">`userName` is hello same as **Deployment / FTP user**.</span></span> <span data-ttu-id="1809e-324">Ils mappent trop**utilisateur** et **mot de passe** dans FileZilla.</span><span class="sxs-lookup"><span data-stu-id="1809e-324">They map too**User** and **Password** in FileZilla.</span></span>
* <span data-ttu-id="1809e-325">`ftpPassiveMode="True"`signifie que ce site hello FTP utilise le transfert FTP passif ; Sélectionnez **passif** sur hello **les paramètres de transfert** onglet.</span><span class="sxs-lookup"><span data-stu-id="1809e-325">`ftpPassiveMode="True"` means that hello FTP site uses passive FTP transfer; select **Passive** on hello **Transfer Settings** tab.</span></span>

#### <a name="configure-hello-web-app-toohost-a-java-application"></a><span data-ttu-id="1809e-326">Configurer l’application Web de hello toohost une application Java</span><span class="sxs-lookup"><span data-stu-id="1809e-326">Configure hello Web App toohost a Java application</span></span>
<span data-ttu-id="1809e-327">Avant de publier application hello, vous devez toochange quelques paramètres de configuration afin que hello application web peut héberger une application Java.</span><span class="sxs-lookup"><span data-stu-id="1809e-327">Before you publish hello application, you need toochange a few configuration settings so that hello web app can host a Java application.</span></span>

1. <span data-ttu-id="1809e-328">Dans le portail classique hello, accédez à l’application web de toohello **tableau de bord** page, puis cliquez sur **configurer**.</span><span class="sxs-lookup"><span data-stu-id="1809e-328">In hello classic portal, go toohello web app's **Dashboard** page and click **Configure**.</span></span> <span data-ttu-id="1809e-329">Sur hello **configurer** , spécifiez hello suivant les paramètres.</span><span class="sxs-lookup"><span data-stu-id="1809e-329">On hello **Configure** page, specify hello following settings.</span></span>
2. <span data-ttu-id="1809e-330">Dans **version Java** valeur par défaut hello est **hors**; sélectionnez une version Java hello votre application cible, par exemple 1.7.0_51.</span><span class="sxs-lookup"><span data-stu-id="1809e-330">In **Java version** hello default is **Off**; select hello Java version your application targets; for example 1.7.0_51.</span></span> <span data-ttu-id="1809e-331">Après cela, assurez-vous également que **conteneur Web** a la valeur version tooa du serveur Tomcat.</span><span class="sxs-lookup"><span data-stu-id="1809e-331">After you do this, also make sure that **Web container** is set tooa version of Tomcat Server.</span></span>
3. <span data-ttu-id="1809e-332">Dans **par défaut des Documents**, ajoutez index.jsp et déplacer vers le haut haut toohello de liste de hello.</span><span class="sxs-lookup"><span data-stu-id="1809e-332">In **Default Documents**, add index.jsp and move it up toohello top of hello list.</span></span> <span data-ttu-id="1809e-333">(le fichier par défaut de hello pour les applications web est hostingstart.html).</span><span class="sxs-lookup"><span data-stu-id="1809e-333">(hello default file for web apps is hostingstart.html.)</span></span>
4. <span data-ttu-id="1809e-334">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1809e-334">Click **Save**.</span></span>

#### <a name="publish-your-application-using-kudu"></a><span data-ttu-id="1809e-335">Publication de votre application à l’aide de Kudu</span><span class="sxs-lookup"><span data-stu-id="1809e-335">Publish your application using Kudu</span></span>
<span data-ttu-id="1809e-336">Application de hello toopublish unidirectionnelle est hello toouse que kudu déboguer console intégrée à Azure.</span><span class="sxs-lookup"><span data-stu-id="1809e-336">One way toopublish hello application is toouse hello Kudu debug console built into Azure.</span></span> <span data-ttu-id="1809e-337">Kudu est connu toobe stable et cohérent avec l’application applications de Service Web et serveur Tomcat.</span><span class="sxs-lookup"><span data-stu-id="1809e-337">Kudu is known toobe stable and consistent with App Service Web Apps and Tomcat Server.</span></span> <span data-ttu-id="1809e-338">Pour accéder à console hello pour l’application web de hello en parcourant les URL tooa Hello suivant du formulaire :</span><span class="sxs-lookup"><span data-stu-id="1809e-338">You access hello console for hello web app by browsing tooa URL of hello following form:</span></span>

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. <span data-ttu-id="1809e-339">Pour cette procédure, console de Kudu hello se trouve à hello suivant URL ; Rechercher l’emplacement de toothis :</span><span class="sxs-lookup"><span data-stu-id="1809e-339">For this procedure, hello Kudu console is located at hello following URL; browse toothis location:</span></span>
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. <span data-ttu-id="1809e-340">Dans le menu supérieur de hello, sélectionnez **Console de débogage > CMD**.</span><span class="sxs-lookup"><span data-stu-id="1809e-340">From hello top menu, select **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="1809e-341">Dans la ligne de commande de console hello, accédez trop`/site/wwwroot` (ou cliquez sur `site`, puis `wwwroot` dans la vue active de hello en hello haut hello) :</span><span class="sxs-lookup"><span data-stu-id="1809e-341">In hello console command line, navigate too`/site/wwwroot` (or click `site`, then `wwwroot` in hello directory view at hello top of hello page):</span></span>
   
    `cd /site/wwwroot`
4. <span data-ttu-id="1809e-342">Une fois que vous avez spécifié **Version Java**, Tomcat Server doit créer un répertoire webapps.</span><span class="sxs-lookup"><span data-stu-id="1809e-342">After you specify **Java version**, Tomcat server should create a webapps directory.</span></span> <span data-ttu-id="1809e-343">Dans la ligne de commande de console hello, accédez à toohello WebApp active :</span><span class="sxs-lookup"><span data-stu-id="1809e-343">In hello console command line, navigate toohello webapps directory:</span></span>
   
    `mkdir webapps`
   
    `cd webapps`
5. <span data-ttu-id="1809e-344">Faites glisser JSPHello.war de `<project-path>/JSPHello/src/` et déposez-le dans la vue de répertoire hello Kudu sous `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="1809e-344">Drag JSPHello.war from `<project-path>/JSPHello/src/` and drop it into hello Kudu directory view under `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="1809e-345">Ne faites pas glisser il toohello « Faites glisser ici tooupload et zip » zone, étant donné que Tomcat sera décompressez-le.</span><span class="sxs-lookup"><span data-stu-id="1809e-345">Do not drag it toohello "Drag here tooupload and zip" area, because Tomcat will unzip it.</span></span>
   
   ![][8]

<span data-ttu-id="1809e-346">Au premier JSPHello.war s’affiche dans la zone de répertoire hello par lui-même :</span><span class="sxs-lookup"><span data-stu-id="1809e-346">At first JSPHello.war appears in hello directory area by itself:</span></span>

  ![][9]

<span data-ttu-id="1809e-347">Dans une courte période (probablement inférieur à 5 minutes) serveur Tomcat sera décompresser le fichier WAR hello dans un répertoire JSPHello décompressé.</span><span class="sxs-lookup"><span data-stu-id="1809e-347">In a short time (probably less than 5 minutes) Tomcat Server will unzip hello WAR file into an unpacked JSPHello directory.</span></span> <span data-ttu-id="1809e-348">Cliquez sur toosee de répertoire racine hello si index.jsp a été décompressé et y copiés.</span><span class="sxs-lookup"><span data-stu-id="1809e-348">Click hello ROOT directory toosee whether index.jsp has been unzipped and copied there.</span></span> <span data-ttu-id="1809e-349">Dans ce cas, accédez toohello arrière WebApp Active toosee si hello décompressé JSPHello active a été créé.</span><span class="sxs-lookup"><span data-stu-id="1809e-349">If so, navigate back toohello webapps directory toosee whether hello unpacked JSPHello directory has been created.</span></span> <span data-ttu-id="1809e-350">Si vous ne voyez pas ces éléments, attendez et recommencez.</span><span class="sxs-lookup"><span data-stu-id="1809e-350">If you do not see these items, wait and repeat.</span></span>

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a><span data-ttu-id="1809e-351">Publication de votre application à l’aide de FileZilla (facultatif)</span><span class="sxs-lookup"><span data-stu-id="1809e-351">Publish your application using FileZilla (optional)</span></span>
<span data-ttu-id="1809e-352">Un autre outil, vous pouvez utiliser toopublish hello application est FileZilla, un client FTP tiers populaires avec une interface utilisateur graphique pratique.</span><span class="sxs-lookup"><span data-stu-id="1809e-352">Another tool you can use toopublish hello application is FileZilla, a popular third-party FTP client with a convenient, graphical UI.</span></span> <span data-ttu-id="1809e-353">Vous pouvez télécharger et installer FileZilla à partir de [http://filezilla-project.org/](http://filezilla-project.org/) si vous ne l’avez pas déjà.</span><span class="sxs-lookup"><span data-stu-id="1809e-353">You can download and install FileZilla from [http://filezilla-project.org/](http://filezilla-project.org/) if you do not already have it.</span></span> <span data-ttu-id="1809e-354">Pour plus d’informations sur l’utilisation hello client, consultez hello [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) et cette entrée de blog sur [les Clients FTP - partie 4 : FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span><span class="sxs-lookup"><span data-stu-id="1809e-354">For more information on using hello client, see hello [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) and this blog entry on [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span></span>

1. <span data-ttu-id="1809e-355">Dans FileZilla, cliquez sur **Fichier > Gestionnaire de Sites**.</span><span class="sxs-lookup"><span data-stu-id="1809e-355">In FileZilla, click **File > Site Manager**.</span></span>
2. <span data-ttu-id="1809e-356">Bonjour **Site Manager** boîte de dialogue, cliquez sur **nouveau Site**.</span><span class="sxs-lookup"><span data-stu-id="1809e-356">In hello **Site Manager** dialog, click **New Site**.</span></span> <span data-ttu-id="1809e-357">Un nouveau site FTP vide apparaît dans **sélectionner une entrée** vous invitant à tooprovide un nom.</span><span class="sxs-lookup"><span data-stu-id="1809e-357">A new blank FTP site will appear in **Select Entry** prompting you tooprovide a name.</span></span> <span data-ttu-id="1809e-358">Dans le cadre de cette procédure, nommez-le `AzureWebDemo-FTP`.</span><span class="sxs-lookup"><span data-stu-id="1809e-358">For this procedure, name it `AzureWebDemo-FTP`.</span></span>
   
    <span data-ttu-id="1809e-359">Sur hello **général** onglet, spécifiez hello suivant les paramètres :</span><span class="sxs-lookup"><span data-stu-id="1809e-359">On hello **General** tab, specify hello following settings:</span></span>
   
   * <span data-ttu-id="1809e-360">**Hôte :** entrée hello **nom d’hôte FTP** que vous avez copié à partir du tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="1809e-360">**Host:** Enter hello **FTP Host Name** that you copied from hello dashboard.</span></span>
   * <span data-ttu-id="1809e-361">**Port :** (laissez ce champ vide, car il s’agit d’un transfert passif et serveur de hello déterminera hello port toouse.)</span><span class="sxs-lookup"><span data-stu-id="1809e-361">**Port:** (Leave this blank, as this is a passive transfer and hello server will determine hello port toouse.)</span></span>
   * <span data-ttu-id="1809e-362">**Protocole :** FTP File Transfer Protocol</span><span class="sxs-lookup"><span data-stu-id="1809e-362">**Protocol:** FTP File Transfer Protocol</span></span>
   * <span data-ttu-id="1809e-363">**Chiffrement :** Utiliser un chiffrement FTP simple</span><span class="sxs-lookup"><span data-stu-id="1809e-363">**Encryption:** Use plain FTP</span></span>
   * <span data-ttu-id="1809e-364">**Type d'ouverture de session :** Normal</span><span class="sxs-lookup"><span data-stu-id="1809e-364">**Logon Type:** Normal</span></span>
   * <span data-ttu-id="1809e-365">**Utilisateur :** entrée hello déploiement / FTP utilisateur que vous avez copié à partir du tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="1809e-365">**User:** Enter hello Deployment / FTP user that you copied from hello dashboard.</span></span> <span data-ttu-id="1809e-366">Il s’agit d’utilisateur FTP complète hello, qui se présente sous forme de hello *webappname\username*.</span><span class="sxs-lookup"><span data-stu-id="1809e-366">This is hello full FTP username, which has hello form *webappname\username*.</span></span>
   * <span data-ttu-id="1809e-367">**Mot de passe :** Entrez le mot hello que vous avez spécifié lorsque vous définissez les informations d’identification de déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="1809e-367">**Password:** Enter hello password that you specified when you set hello deployment credentials.</span></span>
     
     <span data-ttu-id="1809e-368">Sur hello **les paramètres de transfert** onglet, sélectionnez **passif**.</span><span class="sxs-lookup"><span data-stu-id="1809e-368">On hello **Transfer Settings** tab, select **Passive**.</span></span>
3. <span data-ttu-id="1809e-369">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="1809e-369">Click **Connect**.</span></span> <span data-ttu-id="1809e-370">Si réussie, console de FileZilla affiche un `Status: Connected` message et émettre un `LIST` le contenu du répertoire toolist hello de commande.</span><span class="sxs-lookup"><span data-stu-id="1809e-370">If successful, FileZilla's console will display a `Status: Connected` message and issue a `LIST` command toolist hello directory contents.</span></span>
4. <span data-ttu-id="1809e-371">Bonjour **Local** Panneau de configuration de site, répertoire de source de hello Sélectionnez fichier dans lequel hello JSPHello.war réside ; c’est le chemin d’accès de hello similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="1809e-371">In hello **Local** site panel, select hello source directory in which hello JSPHello.war file resides; hello path will be similar toohello following:</span></span>
   
    `<project-path>/JSPHello/src/`
5. <span data-ttu-id="1809e-372">Bonjour **distant** Panneau de configuration de site, le dossier de destination sélectionnez hello.</span><span class="sxs-lookup"><span data-stu-id="1809e-372">In hello **Remote** site panel, select hello destination folder.</span></span> <span data-ttu-id="1809e-373">Vous allez déployer toohello de fichier WAR hello `webapps` répertoire sous la racine de l’application hello web.</span><span class="sxs-lookup"><span data-stu-id="1809e-373">You will deploy hello WAR file toohello `webapps` directory under hello web app's root.</span></span> <span data-ttu-id="1809e-374">Accédez trop`/site/wwwroot`, avec le bouton droit sur `wwwroot`, puis sélectionnez **créer le répertoire**.</span><span class="sxs-lookup"><span data-stu-id="1809e-374">Navigate too`/site/wwwroot`, right-click on `wwwroot`, and select **Create directory**.</span></span> <span data-ttu-id="1809e-375">Répertoire des noms hello `webapps` et entrez ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="1809e-375">Name hello directory `webapps` and enter that directory.</span></span>
6. <span data-ttu-id="1809e-376">Transfert de JSPHello.war trop`/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="1809e-376">Transfer JSPHello.war too`/site/wwwroot/webapps`.</span></span> <span data-ttu-id="1809e-377">Sélectionnez JSPHello.war Bonjour **Local** liste de fichiers, avec le bouton droit dessus et sélectionnez **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="1809e-377">Select JSPHello.war in hello **Local** file list, right-click on it and select **Upload**.</span></span> <span data-ttu-id="1809e-378">Il doit s’afficher dans `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="1809e-378">You should see it appear in `/site/wwwroot/webapps`.</span></span>
7. <span data-ttu-id="1809e-379">Après avoir copié le répertoire d’applications Web JSPHello.war toohello, serveur Tomcat sera automatiquement décompresser (décompresser) hello des fichiers dans le fichier WAR hello.</span><span class="sxs-lookup"><span data-stu-id="1809e-379">After you copy JSPHello.war toohello webapps directory, Tomcat Server will automatically unpack (unzip) hello files in hello WAR file.</span></span> <span data-ttu-id="1809e-380">Bien que le serveur Tomcat commence la décompression presque immédiatement, il peut prendre un certain délai éventuellement pour tooappear de fichiers hello dans le client de hello FTP.</span><span class="sxs-lookup"><span data-stu-id="1809e-380">Although Tomcat Server begins unpacking almost immediately, it might take a long time (possibly hours) for hello files tooappear in hello FTP client.</span></span>

#### <a name="run-hello-hello-world-application-on-hello-web-app"></a><span data-ttu-id="1809e-381">Exécuter l’application hello Hello World sur hello Web App</span><span class="sxs-lookup"><span data-stu-id="1809e-381">Run hello Hello World application on hello Web App</span></span>
1. <span data-ttu-id="1809e-382">Après avoir téléchargé le fichier WAR hello et vérifié que le serveur Tomcat a créé un décompressés `JSPHello` directory, parcourir trop`http://webdemowebapp.azurewebsites.net/JSPHello` application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="1809e-382">After you have uploaded hello WAR file and verified that Tomcat server has created an unpacked `JSPHello` directory, browse too`http://webdemowebapp.azurewebsites.net/JSPHello` toorun hello application.</span></span>
   
   > <span data-ttu-id="1809e-383">**Remarque :** si vous cliquez sur **Parcourir** à partir du portail classique de hello, vous obtiendrez de page Web par défaut de hello, indiquant que « cette application de web Java en fonction a été créée. »</span><span class="sxs-lookup"><span data-stu-id="1809e-383">**Note:** If you click **Browse** from hello classic portal, you might get hello default webpage, saying "This Java based web application has been successfully created."</span></span> <span data-ttu-id="1809e-384">Vous pouvez avoir toorefresh, hello page Web dans la sortie de commande tooview hello application au lieu de la page Web par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="1809e-384">You might have toorefresh hello webpage in order tooview hello application output instead of hello default webpage.</span></span>
   > 
   > 
2. <span data-ttu-id="1809e-385">Lors de l’application hello s’exécute, vous devez voir une page web avec hello suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="1809e-385">When hello application runs, you should see a web page with hello following output:</span></span>
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a><span data-ttu-id="1809e-386">Nettoyage des ressources Azure</span><span class="sxs-lookup"><span data-stu-id="1809e-386">Clean up Azure resources</span></span>
<span data-ttu-id="1809e-387">Cette procédure crée une application web App Service.</span><span class="sxs-lookup"><span data-stu-id="1809e-387">This procedure creates an App Service web app.</span></span> <span data-ttu-id="1809e-388">Vous serez facturé pour la ressource de hello aussi longtemps qu’il existe.</span><span class="sxs-lookup"><span data-stu-id="1809e-388">You will be billed for hello resource as long as it exists.</span></span> <span data-ttu-id="1809e-389">Si vous ne prévoyez toocontinue à l’aide de l’application web hello de test ou de développement, vous devez envisager l’arrêt ou la suppression.</span><span class="sxs-lookup"><span data-stu-id="1809e-389">Unless you plan toocontinue using hello web app for testing or development, you should consider stopping or deleting it.</span></span> <span data-ttu-id="1809e-390">Une application web qui a été arrêtée continuera à faire l’objet de frais réduits, mais vous pouvez la redémarrer à tout moment.</span><span class="sxs-lookup"><span data-stu-id="1809e-390">A web app that has been stopped will still incur a small charge, but you can restart it at any time.</span></span> <span data-ttu-id="1809e-391">Suppression d’une application web efface toutes les données que vous avez téléchargé tooit.</span><span class="sxs-lookup"><span data-stu-id="1809e-391">Deleting a web app erases all data you have uploaded tooit.</span></span>

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
