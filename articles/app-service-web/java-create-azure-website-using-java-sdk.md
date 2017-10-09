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
# <a name="create-a-web-app-in-azure-app-service-using-hello-azure-sdk-for-java"></a>Créer une application Web dans Azure App Service à l’aide de hello SDK Azure pour Java
<!-- Azure Active Directory workflow is not yet available on hello Azure Portal -->

## <a name="overview"></a>Vue d'ensemble
Cette procédure pas à pas vous montre comment toocreate un kit de développement logiciel Azure pour une application Java qui crée une application Web [Azure App Service][Azure App Service], puis déployer une application tooit. Elle comprend deux parties :

* Partie 1 montre comment toobuild une application Java qui crée une application web.
* Partie 2 illustre comment toocreate un JSP simple « Hello World » application, puis utiliser FTP client toodeploy code tooApp Service.

## <a name="prerequisites"></a>Composants requis
### <a name="software-installations"></a>Installations de logiciels
Hello AzureWebDemo code de l’application dans cet article a été écrit à l’aide du SDK Azure Java 0.7.0, que vous pouvez installer à l’aide de hello [Web Platform Installer] [ Web Platform Installer] (WebPI). En outre, assurez-vous que toouse hello version la plus récente de hello [boîte à outils Azure pour Eclipse][Azure Toolkit for Eclipse]. Après avoir installé hello SDK, mettre à jour les dépendances hello dans votre projet Eclipse en exécutant **mettre à jour l’Index** dans **Maven référentiels**, puis rajoutez la version la plus récente de chaque package Bonjour hello  **Dépendances** fenêtre. Vous pouvez vérifier la version de hello de logiciels installés dans Eclipse en cliquant sur **aide > Détails de l’Installation**; vous doit avoir au moins hello suivants versions :

* Package pour les bibliothèques Microsoft Azure pour Java 0.7.0.20150309
* Environnement de développement intégré (IDE) Eclipse pour développeurs Java EE 4.4.2.20150219

### <a name="create-and-configure-cloud-resources-in-azure"></a>Création et configuration de ressources de cloud dans Azure
Avant de commencer cette procédure, vous devez toohave un abonnement Azure actif et configuré par défaut Active Directory (AD) sur Azure.

### <a name="create-an-active-directory-ad-in-azure"></a>Création d’un annuaire Active Directory (AD) dans Azure
Si vous n’avez pas déjà un Active Directory (AD) sur votre abonnement Azure, connectez-vous à hello [portail Azure classic] [ Azure classic portal] avec votre compte Microsoft. Si vous avez plusieurs abonnements, cliquez sur **abonnements** et le répertoire par défaut de select hello pour l’abonnement de hello souhaité toouse pour ce projet. Puis cliquez sur **appliquer** tooswitch toothat une vue d’abonnement.

1. Sélectionnez **Active Directory** à partir du menu hello située à gauche. **Cliquez sur Nouveau &gt; Annuaire &gt; Création personnalisée**.
2. Dans **Ajouter un annuaire**, sélectionnez **Créer un nouvel annuaire**.
3. Dans **Nom**, entrez un nom d’annuaire.
4. Dans **Domaine**, entrez un nom de domaine. Il s’agit d’un nom de domaine de base qui est inclus par défaut dans votre répertoire ; Il présente sous forme de hello `<domain_name>.onmicrosoft.com`. Vous pouvez nommer en fonction de nom de répertoire hello ou un autre nom de domaine que vous possédez. Par la suite, vous pouvez ajouter un autre nom de domaine que votre organisation utilise déjà.
5. Dans **Pays ou région**, sélectionnez votre paramètre régional.

Pour plus d'informations sur AD, consultez la page [Qu'est-ce qu'un annuaire Azure AD][What is an Azure AD directory]?

### <a name="create-a-management-certificate-for-azure"></a>Création d’un certificat de gestion pour Azure
Hello SDK Azure pour Java utilise tooauthenticate de certificats de gestion avec des abonnements Azure. Il s’agit d’utiliser de tooauthenticate une application cliente qui utilise tooact des API de gestion hello pour le compte de ressources d’abonnement toomanage hello abonnement propriétaire de certificats X.509 v3.

code Hello dans cette procédure utilise un certificat auto-signé de tooauthenticate avec Azure. Pour cette procédure, vous devez toocreate un certificat et le télécharger toohello [portail Azure classic] [ Azure classic portal] au préalable. Cette opération implique hello comme suit :

* Générer un fichier PFX représentant votre certificat client et l’enregistrer en local
* Générer un certificat de gestion (fichier CER) dans le fichier PFX hello.
* Téléchargez tooyour de fichier CER hello abonnement Azure.
* Convertir le fichier PFX hello JKS, étant donné que Java utilise ce tooauthenticate de format à l’aide de certificats.
* Écrire du code d’authentification de l’application hello, qui fait référence le fichier JKS toohello local.

Lorsque vous effectuez cette procédure, certificat CER hello résidera dans votre abonnement Azure et certificat JKS hello doit résider sur votre disque local. Pour plus d’informations sur les certificats de gestion, consultez la page [Créer et télécharger un certificat de gestion pour Microsoft Azure][Create and Upload a Management Certificate for Azure].

#### <a name="create-a-certificate"></a>Création d’un certificat
toocreate votre propre certificat auto-signé, ouvrez une console de commande sur votre système d’exploitation et exécutez hello suivant les commandes.

> **Remarque :** ordinateur hello sur lequel vous exécutez cette commande doit avoir hello JDK installé. En outre, hello chemin d’accès toohello keytool dépend de l’emplacement hello dans lequel vous installez hello JDK. Pour plus d’informations, consultez [clé et l’outil de gestion de certificat (keytool)] [ Key and Certificate Management Tool (keytool)] dans la documentation en ligne de hello Java.
> 
> 

fichier .pfx de hello toocreate :

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

toocreate de fichier .cer hello :

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

où :

* `<java-install-dir>`est hello chemin d’accès toohello répertoire dans lequel vous avez installé Java.
* `<keystore-id>`est l’identificateur de l’entrée keystore hello (par exemple, `AzureRemoteAccess`).
* `<cert-store-dir>`est hello chemin toohello répertoire dans lequel vous souhaitez toostore certificats (par exemple `C:/Certificates`).
* `<cert-file-name>`est le nom hello hello du fichier de certificat (par exemple `AzureWebDemoCert`).
* `<password>`mot de passe hello vous choisissez tooprotect hello certificat ; Il doit être au moins 6 caractères. Vous avez la possibilité de n’entrer aucun mot de passe, même si cela n’est pas recommandé.
* `<dname>`est toobe de nom unique X.500 hello associée alias et est utilisé en tant que l’émetteur de hello et d’objet dans le certificat auto-signé de hello.

Pour plus d'informations, consultez [Create and upload a management certificate for Azure][Create and Upload a Management Certificate for Azure].

#### <a name="upload-hello-certificate"></a>Télécharger le certificat de hello
tooupload tooAzure un certificat auto-signé, accédez toohello **paramètres** dans le portail classique de hello, puis cliquez sur hello **certificats de gestion** onglet. Cliquez sur **télécharger** bas hello hello page et naviguer emplacement toohello du fichier CER de hello vous avez créé.

#### <a name="convert-hello-pfx-file-into-jks"></a>Convertir le fichier PFX hello JKS
Bonjour invite de commandes Windows (en cours d’exécution en tant qu’administrateur), cd toohello répertoire contenant hello certificats et exécutez hello suivant de commande, où `<java-install-dir>` est le répertoire hello dans lequel vous avez installé Java sur votre ordinateur :

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. Lorsque vous y êtes invité, entrez le mot de passe du magasin de clés de destination hello ; Il s’agit d’un mot de passe hello pour le fichier JKS hello.
2. Lorsque vous y êtes invité, entrez le mot de passe du magasin de clés du source de hello ; Il s’agit d’un mot de passe hello que vous avez spécifié pour le fichier PFX hello.

deux mots de passe Hello n’ont pas de toobe hello identiques. Vous avez la possibilité de n’entrer aucun mot de passe, même si cela n’est pas recommandé.

## <a name="build-a-web-app-creation-application"></a>Création d’une application de création d’application web
### <a name="create-hello-eclipse-workspace-and-maven-project"></a>Créer hello d’espace de travail Eclipse et Maven projet
Dans cette section, vous créez un espace de travail et un projet Maven pour l’application de la création de hello web app, nommé AzureWebDemo.

1. Créez un projet Maven. Cliquez sur **Fichier > Nouveau > Projet Maven**. Dans **Nouveau projet Maven**, sélectionnez **Créer un projet simple** et **Utiliser l’emplacement de l’espace de travail par défaut**.
2. Sur la deuxième page de hello de **nouveau projet Maven**, spécifiez hello qui suit :
   
   * ID de groupe : `com.<username>.azure.webdemo`
   * ID d’artefact : AzureWebDemo
   * Version : 0.0.1-SNAPSHOT
   * Packaging : ar
   * Nom : AzureWebDemo
     
     Cliquez sur **Terminer**.
3. Ouvrez le fichier de pom.xml de hello du nouveau projet dans l’Explorateur de projets. Sélectionnez hello **dépendances** onglet. Comme il s’agit d’un nouveau projet, aucun package n’est encore répertorié.
4. Ouvrez hello Maven référentiels afficher. **Cliquez sur Fenêtre &gt; Afficher la vue &gt; Autres &gt; Maven &gt; Référentiels Maven** , puis cliquez sur **OK**. Hello **Maven référentiels** affichage apparaîtra bas hello hello IDE.
5. Ouvrez **référentiels globaux**, avec le bouton hello **central** référentiel, puis sélectionnez **reconstruire l’Index**.
   
    ![][1]
   
    Cette étape peut prendre plusieurs minutes selon la vitesse de hello de votre connexion. Lorsque les reconstructions d’index de hello, vous devez voir les packages de Microsoft Azure hello Bonjour **central** référentiel de Maven.
6. Dans **Dépendances**, cliquez sur **Ajouter**. Dans **Entrer l’ID de groupe...**, entrez `azure-management`. Sélectionnez les packages hello pour la gestion de base et la gestion de l’application de Service Web Apps :
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > **Remarque :** si vous mettez à jour les dépendances hello après une nouvelle version de version, vous devez toore-ajouter des dépendances de hello dans cette liste.
   > Après avoir cliqué sur **ajouter** et sélectionnez chaque dépendance, il s’affiche avec le nouveau numéro de version hello Bonjour **dépendances** liste.
   > 
   > 

Cliquez sur **OK**. Hello packages Azure, puis s’affichent dans hello **dépendances** liste.

### <a name="writing-java-code-toocreate-a-web-app-by-calling-hello-azure-sdk"></a>Écrire du Code Java tooCreate une application Web à appeler hello Azure SDK
Ensuite, écrivez le code hello qui appelle des API Bonjour Azure SDK pour hello de toocreate Java application Service web d’application.

1. Créer un point de code de Java classe toocontain hello entrée principal. Dans l’Explorateur de projets, avec le bouton droit sur le nœud de projet hello et sélectionnez **Nouveau > classe**.
2. Dans **nouvelle classe Java**, nommez la classe hello `WebCreator` et vérifiez hello **principal de void statique publique** case à cocher. les sélections de Hello doivent apparaître comme suit :
   
    ![][2]
3. Cliquez sur **Terminer**. fichier de WebCreator.java Hello s’affiche dans l’Explorateur de projets.

### <a name="calling-hello-azure-api-toocreate-an-app-service-web-app"></a>Appel de tooCreate des API Azure hello une application de Service d’applications Web
#### <a name="add-necessary-imports"></a>Ajout des importations nécessaires
Dans WebCreator.java, ajoutez hello suivant importations ; ces importations fournissent des bibliothèques de gestion tooclasses accès Bonjour pour consommer des API Azure :

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


#### <a name="define-hello-main-entry-point-class"></a>Définir la classe de point d’entrée principal hello
Car hello hello AzureWebDemo application vise toocreate une application de Service d’applications Web, nommez la classe principale hello pour cette application `WebAppCreator`. Cette classe fournit hello entrée principal point de code qui appelle l’application web hello API de gestion des services Azure toocreate hello.

Ajoutez hello suivant des définitions de paramètres de l’application web hello et espace Web. Vous devez tooprovide vos propres informations de certificat et les ID d’abonnement Azure.

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

où :

* `<subscription-id>`est l’ID d’abonnement Azure hello dans lequel vous souhaitez que la ressource de hello de toocreate.
* `<certificate-store-path>`est hello chemin d’accès et nom de fichier toohello JKS le fichier dans votre répertoire du magasin de certificats local. Par exemple, `C:/Certificates/CertificateName.jks` pour Linux et `C:\Certificates\CertificateName.jks` pour Windows.
* `<certificate-password>`est un mot de passe hello spécifié lorsque vous avez créé votre certificat JKS.
* `webAppName`peut être n’importe quel nom que vous choisissez ; Cette procédure utilise le nom de hello `WebDemoWebApp`. nom de domaine complet Hello est hello `webAppName` avec hello `domainName` ajouté, par conséquent, dans ce cas hello complète domaine est `webdemowebapp.azurewebsites.net`.
* `domainName` doit être spécifié comme indiqué ci-dessus.
* `webSpaceName`doit être une des valeurs de hello définies dans hello [WebSpaceNames] [ WebSpaceNames] classe.
* `appServicePlanName` doit être spécifié comme indiqué ci-dessus.

> **Remarque :** chaque fois que vous exécutez cette application, vous devez la valeur hello toochange `webAppName` et `appServicePlanName` (ou supprimer l’application web de hello sur hello portail Azure) avant d’exécuter l’application hello. Dans le cas contraire, l’exécution échoue car hello même ressource existe déjà dans Azure.
> 
> 

#### <a name="define-hello-web-creation-method"></a>Définir la méthode de création hello web
Définissez ensuite une application web de méthode toocreate hello. Cette méthode, `createWebApp`, spécifie les paramètres de hello de hello web app et espace Web de hello. Il crée également et configure le client de gestion d’application Service Web Apps hello, qui est défini en hello [WebSiteManagementClient] [ WebSiteManagementClient] objet. client de gestion de Hello est toocreating clé des applications Web. Il fournit des services web RESTful qui autorisent des applications toomanage (exécution d’opérations telles que create, update et delete) des applications web en appelant l’API de gestion de service hello.

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

le code Hello affiche l’état HTTP hello réponse hello indiquant la réussite ou l’échec et en cas de réussite, produira nom hello Hello créé l’application web.

#### <a name="define-hello-main-method"></a>Définir la méthode main() de hello
Fournir le code de la méthode main() hello cette application web d’appels createWebApp() toocreate hello.

Enfin, appelez `createWebApp` à partir de `main` :

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-hello-application-and-verify-web-app-creation"></a>Exécutez l’application hello et vérifiez la création d’application web
tooverify votre application s’exécute, cliquez sur **exécuter > exécuter**. Lors de l’application hello soit terminée, vous devez voir hello suivant la sortie dans la console hello Eclipse :

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

Ouvrez une session hello portail Azure classic, puis cliquez sur **Web Apps**. application web Hello doit apparaître dans la liste des applications Web hello dans quelques minutes.

## <a name="deploying-an-application-toohello-web-app"></a>Déploiement d’une application Web de toohello Application
Une fois que vous avez exécuté AzureWebDemo et créées hello nouvelle application web, ouvrez une session sur le portail classique de hello, cliquez sur **Web Apps**, puis sélectionnez **WebDemoWebApp** Bonjour **Web Apps** liste. Dans la page du tableau de bord de l’application hello web, cliquez sur **Parcourir** (ou cliquez sur l’URL de hello, `webdemowebapp.azurewebsites.net`) toonavigate tooit. Vous verrez une page de l’espace réservé vide, car aucun contenu n’a encore été toohello publié l’application web.

Ensuite vous créez une application « Hello World » et déployer l’application web toohello.

### <a name="create-a-jsp-hello-world-application"></a>Création d’une application JSP Hello World
#### <a name="create-hello-application"></a>Créer l’application hello
Dans toodemonstrate commande comment toodeploy web application toohello, hello procédure vous montre comment toocreate une application Java de « Hello World » simple et chargez-le toohello application Service d’applications Web créés par votre application.

1. Cliquez sur **Fichier > Nouveau > Projet Web dynamique**. Nommez-le `JSPHello`. Il est inutile toochange tous les autres paramètres dans cette boîte de dialogue. Cliquez sur **Terminer**.
   
    ![][3]
2. Dans l’Explorateur de projets, développez hello **JSPHello** de projet, cliquez sur **WebContent**, puis cliquez sur **Nouveau > fichier JSP**. Dans la boîte de dialogue Nouveau fichier JSP hello, nommez le nouveau fichier de hello `index.jsp`. Cliquez sur **Suivant**.
3. Bonjour **sélectionner un modèle JSP** boîte de dialogue, sélectionnez **nouveau fichier JSP (html)** et cliquez sur **Terminer**.
4. Dans index.jsp, ajoutez hello suivant code Bonjour `<head>` et `<body>` balise sections :
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, hello time is <%= date %> 
        </body>

#### <a name="run-hello-hello-world-application-in-localhost"></a>Exécutez l’application hello Hello World dans localhost
Avant d’exécuter cette application, vous devez tooconfigure quelques propriétés.

1. Avec le bouton hello **JSPHello** de projet et sélectionnez **propriétés**.
2. Bonjour **propriétés** boîte de dialogue : sélectionnez **chemin d’accès de Build Java**, sélectionnez hello **de commande et d’exportation** onglet, vérifiez **bibliothèque de système de JRE**, puis cliquez sur **Des** toomove il haut toohello de liste de hello.
   
    ![][4]
3. Également dans hello **propriétés** boîte de dialogue : sélectionnez **ciblée des Runtimes** et cliquez sur **nouveau**.
4. Bonjour **nouvel environnement d’exécution serveur** boîte de dialogue, sélectionnez un serveur comme **Apache Tomcat v7.0** et cliquez sur **suivant**. Bonjour **serveur Tomcat** boîte de dialogue, définissez **nom** trop`Apache Tomcat v7.0`et la valeur **répertoire d’Installation de Tomcat** Active toohello dans lequel vous hello de version Tomcat serveur toouse.
   
    ![][5]
   
    Cliquez sur **Terminer**.
5. Vous retournez puis toohello **ciblée des Runtimes** page Hello **propriétés** boîte de dialogue. Sélectionnez **Apache Tomcat v7.0**, puis cliquez sur **OK**.
   
    ![][6]
6. Bonjour Eclipse **exécuter** menu, cliquez sur **exécuter**. Bonjour **exécuter en tant que** boîte de dialogue, sélectionnez **s’exécutent sur le serveur**. Bonjour **s’exécutent sur le serveur** boîte de dialogue, sélectionnez **Tomcat v7.0 serveur**:
   
    ![][7]
   
    Cliquez sur **Terminer**.
7. Hello lorsque les exécutions de l’application, vous devez voir hello **JSPHello** page apparaît dans une fenêtre de localhost dans Eclipse (`http://localhost:8080/JSPHello/`), affichage hello message suivant :
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-hello-application-as-a-war"></a>Exporter l’application hello comme un WAR
Exporter des fichiers de projet web hello en tant que fichier d’archive (WAR) web afin que vous pouvez le déployer l’application web toohello. Hello fichiers projet web suivants se trouvent dans le dossier de contenu Web hello :

    META-INF
    WEB-INF
    index.jsp

1. Cliquez sur le dossier de contenu Web hello et sélectionnez **exporter**.
2. Bonjour **exporter Sélectionnez** boîte de dialogue, cliquez sur **Web > WAR** de fichier, puis cliquez sur **suivant**.
3. Bonjour **WAR exporter** boîte de dialogue, sélectionnez le répertoire de src hello hello projet en cours et inclure le nom hello du fichier WAR de hello à fin de hello. Par exemple :
   
    `<project-path>/JSPHello/src/JSPHello.war`

Pour plus d’informations sur le déploiement des fichiers WAR, consultez [ajouter un tooAzure d’application Java App Service Web Apps](web-sites-java-add-app.md).

### <a name="deploying-hello-hello-world-application-using-ftp"></a>Déploiement hello Hello World Application à l’aide de FTP
Sélectionnez une application hello de tiers FTP client toopublish. Cette procédure décrit les deux options : console de Kudu hello intégrée à Azure ; et FileZilla, un outil populaire avec une interface utilisateur graphique pratique.

> **Remarque :** hello boîte à outils Azure pour Eclipse prend en charge les comptes de déploiement toostorage et cloud services, mais ne prend pas actuellement en charge les applications tooweb de déploiement. Vous pouvez déployer des comptes toostorage et services à l’aide d’un projet de déploiement Azure comme décrit dans le cloud [création d’une Application Hello World pour Azure dans Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), mais pas les applications tooweb. Utilisez d’autres méthodes telles que FTP ou GitHub tootransfer fichiers tooyour l’application web.
> 
> **Remarque :** nous ne recommandons pas à l’aide de FTP à partir de l’invite de commandes Windows hello (hello FTP.EXE utilitaire qui est fourni avec Windows). Les clients FTP qui utilisent FTP actif, telles que FTP.EXE, souvent basculent toowork pare-feu. FTP actif spécifie une adresse interne basée sur le réseau local, toowhich FTP server risquent de ne tooconnect.
> 
> 

Pour plus d’informations sur le déploiement tooan application Service web d’application à l’aide de FTP, consultez hello rubriques suivantes :

* [Déployer à l’aide d’un utilitaire FTP](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a>Configurer les informations d'identification du déploiement
Assurez-vous que vous avez exécuté hello **AzureWebDemo** application toocreate une application web. Vous souhaitez transférer l’emplacement des fichiers toothis.

1. Connectez-vous au portail classique de hello et cliquez sur **Web Apps**. Assurez-vous que **WebDemoWebApp** apparaît dans la liste hello d’applications web et assurez-vous qu’il s’exécute. Cliquez sur **WebDemoWebApp** tooopen son **tableau de bord** page.
2. Sur hello **tableau de bord** sous **aperçu rapide**, cliquez sur **configurer vos informations d’identification de déploiement** (si vous avez déjà des informations d’identification de déploiement, il lit  **Réinitialiser vos informations d’identification de déploiement**).
   
    Les informations d'identification du déploiement sont associées à un compte Microsoft. Vous devez toospecify un nom d’utilisateur et mot de passe que vous pouvez utiliser toodeploy à l’aide de Git et FTP. Vous pouvez utiliser ces toodeploy informations d’identification tooany l’application web dans tous les abonnements Azure associés à votre compte Microsoft. Fournissez les informations d’identification de la déploiement Git et FTP dans la boîte de dialogue hello et nom d’utilisateur de l’enregistrement hello et un mot de passe pour un usage ultérieur.

#### <a name="get-ftp-connection-information"></a>Obtention des informations de connexion FTP
toouse FTP toodeploy application fichiers toohello nouvellement créé l’application web, vous devez tooobtain les informations de connexion. Il existe deux façons de tooobtain les informations de connexion. Est l’application web toovisit hello **tableau de bord** page ; hello autre manière consiste toodownload hello web application le profil de publication. profil de publication Hello est un fichier XML qui fournit des informations telles que les informations d’identification d’ouverture de session et de nom de hôte FTP pour vos applications web dans Azure App Service. Vous pouvez utiliser cette application web tooany de toodeploy nom d’utilisateur et mot de passe de tous les abonnements associés à hello compte Azure, pas uniquement celui-ci.

les informations de connexion tooobtain FTP à partir du Panneau de l’application hello web Bonjour [Azure Portal][Azure Portal]:

1. Sous **Essentials**, recherchez et copiez hello **nom d’hôte FTP**. Ceci est un URI similaire trop`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.
2. Sous **Essentials**, recherchez et copiez le **Nom d’utilisateur FTP/déploiement**. Cela aura un formulaire de hello *webappname\deployment-username*; par exemple `WebDemoWebApp\deployer77`.

informations de connexion FTP tooobtain de hello profil de publication :

1. Dans le panneau de l’application hello web, cliquez sur **obtenir le profil de publication**. Il télécharge un disque tooyour fichier .publishsettings.
2. Ouvrez le fichier .publishsettings de hello dans un éditeur XML ou un éditeur de texte et de recherche hello `<publishProfile>` élément contenant `publishMethod="FTP"`. Il doit ressembler à hello suivantes :
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. Notez cette application web hello `publishProfile` paramètres mappent les paramètres du Gestionnaire de Site FileZilla toohello comme suit :

* `publishUrl`est de même que hello **nom d’hôte FTP**, hello valeur définie dans **hôte**.
* `publishMethod="FTP"`signifie que vous définissez **protocole** trop**FTP - File Transfer Protocol**, et **chiffrement** trop**utiliser FTP brut**.
* `userName`et `userPWD` sont des valeurs réelles du nom d’utilisateur et mot de passe spécifié lorsque vous réinitialisez les informations d’identification de déploiement hello clés pour hello. `userName`est de même que hello **déploiement / FTP utilisateur**. Ils mappent trop**utilisateur** et **mot de passe** dans FileZilla.
* `ftpPassiveMode="True"`signifie que ce site hello FTP utilise le transfert FTP passif ; Sélectionnez **passif** sur hello **les paramètres de transfert** onglet.

#### <a name="configure-hello-web-app-toohost-a-java-application"></a>Configurer l’application Web de hello toohost une application Java
Avant de publier application hello, vous devez toochange quelques paramètres de configuration afin que hello application web peut héberger une application Java.

1. Dans le portail classique hello, accédez à l’application web de toohello **tableau de bord** page, puis cliquez sur **configurer**. Sur hello **configurer** , spécifiez hello suivant les paramètres.
2. Dans **version Java** valeur par défaut hello est **hors**; sélectionnez une version Java hello votre application cible, par exemple 1.7.0_51. Après cela, assurez-vous également que **conteneur Web** a la valeur version tooa du serveur Tomcat.
3. Dans **par défaut des Documents**, ajoutez index.jsp et déplacer vers le haut haut toohello de liste de hello. (le fichier par défaut de hello pour les applications web est hostingstart.html).
4. Cliquez sur **Enregistrer**.

#### <a name="publish-your-application-using-kudu"></a>Publication de votre application à l’aide de Kudu
Application de hello toopublish unidirectionnelle est hello toouse que kudu déboguer console intégrée à Azure. Kudu est connu toobe stable et cohérent avec l’application applications de Service Web et serveur Tomcat. Pour accéder à console hello pour l’application web de hello en parcourant les URL tooa Hello suivant du formulaire :

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. Pour cette procédure, console de Kudu hello se trouve à hello suivant URL ; Rechercher l’emplacement de toothis :
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. Dans le menu supérieur de hello, sélectionnez **Console de débogage > CMD**.
3. Dans la ligne de commande de console hello, accédez trop`/site/wwwroot` (ou cliquez sur `site`, puis `wwwroot` dans la vue active de hello en hello haut hello) :
   
    `cd /site/wwwroot`
4. Une fois que vous avez spécifié **Version Java**, Tomcat Server doit créer un répertoire webapps. Dans la ligne de commande de console hello, accédez à toohello WebApp active :
   
    `mkdir webapps`
   
    `cd webapps`
5. Faites glisser JSPHello.war de `<project-path>/JSPHello/src/` et déposez-le dans la vue de répertoire hello Kudu sous `/site/wwwroot/webapps`. Ne faites pas glisser il toohello « Faites glisser ici tooupload et zip » zone, étant donné que Tomcat sera décompressez-le.
   
   ![][8]

Au premier JSPHello.war s’affiche dans la zone de répertoire hello par lui-même :

  ![][9]

Dans une courte période (probablement inférieur à 5 minutes) serveur Tomcat sera décompresser le fichier WAR hello dans un répertoire JSPHello décompressé. Cliquez sur toosee de répertoire racine hello si index.jsp a été décompressé et y copiés. Dans ce cas, accédez toohello arrière WebApp Active toosee si hello décompressé JSPHello active a été créé. Si vous ne voyez pas ces éléments, attendez et recommencez.

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a>Publication de votre application à l’aide de FileZilla (facultatif)
Un autre outil, vous pouvez utiliser toopublish hello application est FileZilla, un client FTP tiers populaires avec une interface utilisateur graphique pratique. Vous pouvez télécharger et installer FileZilla à partir de [http://filezilla-project.org/](http://filezilla-project.org/) si vous ne l’avez pas déjà. Pour plus d’informations sur l’utilisation hello client, consultez hello [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) et cette entrée de blog sur [les Clients FTP - partie 4 : FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).

1. Dans FileZilla, cliquez sur **Fichier > Gestionnaire de Sites**.
2. Bonjour **Site Manager** boîte de dialogue, cliquez sur **nouveau Site**. Un nouveau site FTP vide apparaît dans **sélectionner une entrée** vous invitant à tooprovide un nom. Dans le cadre de cette procédure, nommez-le `AzureWebDemo-FTP`.
   
    Sur hello **général** onglet, spécifiez hello suivant les paramètres :
   
   * **Hôte :** entrée hello **nom d’hôte FTP** que vous avez copié à partir du tableau de bord hello.
   * **Port :** (laissez ce champ vide, car il s’agit d’un transfert passif et serveur de hello déterminera hello port toouse.)
   * **Protocole :** FTP File Transfer Protocol
   * **Chiffrement :** Utiliser un chiffrement FTP simple
   * **Type d'ouverture de session :** Normal
   * **Utilisateur :** entrée hello déploiement / FTP utilisateur que vous avez copié à partir du tableau de bord hello. Il s’agit d’utilisateur FTP complète hello, qui se présente sous forme de hello *webappname\username*.
   * **Mot de passe :** Entrez le mot hello que vous avez spécifié lorsque vous définissez les informations d’identification de déploiement hello.
     
     Sur hello **les paramètres de transfert** onglet, sélectionnez **passif**.
3. Cliquez sur **Connecter**. Si réussie, console de FileZilla affiche un `Status: Connected` message et émettre un `LIST` le contenu du répertoire toolist hello de commande.
4. Bonjour **Local** Panneau de configuration de site, répertoire de source de hello Sélectionnez fichier dans lequel hello JSPHello.war réside ; c’est le chemin d’accès de hello similaire toohello suivantes :
   
    `<project-path>/JSPHello/src/`
5. Bonjour **distant** Panneau de configuration de site, le dossier de destination sélectionnez hello. Vous allez déployer toohello de fichier WAR hello `webapps` répertoire sous la racine de l’application hello web. Accédez trop`/site/wwwroot`, avec le bouton droit sur `wwwroot`, puis sélectionnez **créer le répertoire**. Répertoire des noms hello `webapps` et entrez ce répertoire.
6. Transfert de JSPHello.war trop`/site/wwwroot/webapps`. Sélectionnez JSPHello.war Bonjour **Local** liste de fichiers, avec le bouton droit dessus et sélectionnez **télécharger**. Il doit s’afficher dans `/site/wwwroot/webapps`.
7. Après avoir copié le répertoire d’applications Web JSPHello.war toohello, serveur Tomcat sera automatiquement décompresser (décompresser) hello des fichiers dans le fichier WAR hello. Bien que le serveur Tomcat commence la décompression presque immédiatement, il peut prendre un certain délai éventuellement pour tooappear de fichiers hello dans le client de hello FTP.

#### <a name="run-hello-hello-world-application-on-hello-web-app"></a>Exécuter l’application hello Hello World sur hello Web App
1. Après avoir téléchargé le fichier WAR hello et vérifié que le serveur Tomcat a créé un décompressés `JSPHello` directory, parcourir trop`http://webdemowebapp.azurewebsites.net/JSPHello` application hello de toorun.
   
   > **Remarque :** si vous cliquez sur **Parcourir** à partir du portail classique de hello, vous obtiendrez de page Web par défaut de hello, indiquant que « cette application de web Java en fonction a été créée. » Vous pouvez avoir toorefresh, hello page Web dans la sortie de commande tooview hello application au lieu de la page Web par défaut de hello.
   > 
   > 
2. Lors de l’application hello s’exécute, vous devez voir une page web avec hello suivant de sortie :
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a>Nettoyage des ressources Azure
Cette procédure crée une application web App Service. Vous serez facturé pour la ressource de hello aussi longtemps qu’il existe. Si vous ne prévoyez toocontinue à l’aide de l’application web hello de test ou de développement, vous devez envisager l’arrêt ou la suppression. Une application web qui a été arrêtée continuera à faire l’objet de frais réduits, mais vous pouvez la redémarrer à tout moment. Suppression d’une application web efface toutes les données que vous avez téléchargé tooit.

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
