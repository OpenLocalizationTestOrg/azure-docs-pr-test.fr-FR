---
title: "Bien démarrer avec la ligne de commande Azure AD Java | Microsoft Docs"
description: "Comment créer une application de ligne de commande Java qui connecte les utilisateurs pour l’accès à une API."
services: active-directory
documentationcenter: java
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 51e1a8f9-6ff0-4643-a350-0ba794e26fd1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 01/23/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 91e4a7b2ac454465d5cce4948a4d5f0b542d2b55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="using-java-command-line-app-to-access-an-api-with-azure-ad"></a><span data-ttu-id="5d939-103">Utilisation d’une application en ligne de commande Java pour accéder à une API avec Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d939-103">Using Java Command Line App To Access An API with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="5d939-104">Azure AD simplifie l’externalisation de la gestion des identités de votre application web en fournissant une authentification unique avec seulement quelques lignes de code.</span><span class="sxs-lookup"><span data-stu-id="5d939-104">Azure AD makes it simple and straightforward to outsource your web app's identity management, providing single sign-in and sign-out with only a few lines of code.</span></span>  <span data-ttu-id="5d939-105">Dans les applications web Java, vous pouvez y parvenir en utilisant l’implémentation Microsoft d’ADAL4J communautaire.</span><span class="sxs-lookup"><span data-stu-id="5d939-105">In Java web apps, you can accomplish this using Microsoft's implementation of the community-driven ADAL4J.</span></span>

  <span data-ttu-id="5d939-106">Ici, nous allons utiliser ADAL4J pour :</span><span class="sxs-lookup"><span data-stu-id="5d939-106">Here we'll use ADAL4J to:</span></span>

* <span data-ttu-id="5d939-107">connecter l’utilisateur à l’application à l’aide d’Azure AD comme fournisseur d’identité ;</span><span class="sxs-lookup"><span data-stu-id="5d939-107">Sign the user into the app using Azure AD as the identity provider.</span></span>
* <span data-ttu-id="5d939-108">afficher des informations sur l’utilisateur ;</span><span class="sxs-lookup"><span data-stu-id="5d939-108">Display some information about the user.</span></span>
* <span data-ttu-id="5d939-109">déconnecter l’utilisateur de l’application.</span><span class="sxs-lookup"><span data-stu-id="5d939-109">Sign the user out of the app.</span></span>

<span data-ttu-id="5d939-110">Pour ce faire, vous devez :</span><span class="sxs-lookup"><span data-stu-id="5d939-110">In order to do this, you'll need to:</span></span>

1. <span data-ttu-id="5d939-111">inscrire une application auprès d’Azure AD ;</span><span class="sxs-lookup"><span data-stu-id="5d939-111">Register an application with Azure AD</span></span>
2. <span data-ttu-id="5d939-112">Configurez votre application pour utiliser la bibliothèque ADAL4J.</span><span class="sxs-lookup"><span data-stu-id="5d939-112">Set up your app to use the ADAL4J library.</span></span>
3. <span data-ttu-id="5d939-113">Utilisez la bibliothèque ADAL4J pour émettre des demandes de connexion et de déconnexion dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d939-113">Use the ADAL4J library to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="5d939-114">afficher les données relatives à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5d939-114">Print out data about the user.</span></span>

<span data-ttu-id="5d939-115">Pour commencer, téléchargez [la structure de l’application](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) ou [l’exemple terminé](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="5d939-115">To get started, [download the app skeleton](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) or [download the completed sample](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span></span>  <span data-ttu-id="5d939-116">Vous aurez également besoin d’un client Azure AD dans lequel inscrire votre application.</span><span class="sxs-lookup"><span data-stu-id="5d939-116">You'll also need an Azure AD tenant in which to register your application.</span></span>  <span data-ttu-id="5d939-117">Si ce n’est pas déjà fait, [découvrez comment en obtenir un](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="5d939-117">If you don't have one already, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1--register-an-application-with-azure-ad"></a><span data-ttu-id="5d939-118">1.  Inscrire une application auprès d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d939-118">1.  Register an Application with Azure AD</span></span>
<span data-ttu-id="5d939-119">Pour autoriser l’authentification des utilisateurs par votre application, vous devez tout d’abord inscrire une nouvelle application dans votre client.</span><span class="sxs-lookup"><span data-stu-id="5d939-119">To enable your app to authenticate users, you'll first need to register a new application in your tenant.</span></span>

1. <span data-ttu-id="5d939-120">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5d939-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5d939-121">Dans la barre supérieure, cliquez sur votre compte et, dans la liste **Répertoire**, choisissez le locataire Active Directory auprès duquel vous voulez inscrire votre application.</span><span class="sxs-lookup"><span data-stu-id="5d939-121">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="5d939-122">Cliquez sur **Autres services** dans le volet de navigation gauche et choisissez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5d939-122">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="5d939-123">Cliquez sur **Inscriptions des applications**, puis sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5d939-123">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="5d939-124">Suivez les invites et créez une **Application Web et/ou API Web**.</span><span class="sxs-lookup"><span data-stu-id="5d939-124">Follow the prompts and create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="5d939-125">Le **nom** de l’application doit décrire votre application aux utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="5d939-125">The **name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="5d939-126">L’ **URL de connexion** est l’URL de base de votre application.</span><span class="sxs-lookup"><span data-stu-id="5d939-126">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="5d939-127">La valeur par défaut de la structure est `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="5d939-127">The skeleton's default is `http://localhost:8080/adal4jsample/`.</span></span>
6. <span data-ttu-id="5d939-128">Une fois l’inscription terminée, AAD affecte un ID d’application unique à votre application.</span><span class="sxs-lookup"><span data-stu-id="5d939-128">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="5d939-129">Copiez cette valeur dans l’onglet de l’application, car vous en aurez besoin dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="5d939-129">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="5d939-130">À partir de la page **Paramètres** -> **Propriétés** de votre application, mettez à jour l’URI ID d’application.</span><span class="sxs-lookup"><span data-stu-id="5d939-130">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="5d939-131">Un **URI ID d’application** est un identificateur unique pour votre application.</span><span class="sxs-lookup"><span data-stu-id="5d939-131">The **App ID URI** is a unique identifier for your application.</span></span>  <span data-ttu-id="5d939-132">L’usage est d’utiliser `https://<tenant-domain>/<app-name>`, par exemple `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="5d939-132">The convention is to use `https://<tenant-domain>/<app-name>`, e.g. `http://localhost:8080/adal4jsample/`.</span></span>

<span data-ttu-id="5d939-133">Une fois dans le portail de votre application, créez une **clé** dans la page **Paramètres** pour votre application et notez-la quelque part.</span><span class="sxs-lookup"><span data-stu-id="5d939-133">Once in the portal for your app create a **Key** from the **Settings** page for your application and copy it down.</span></span>  <span data-ttu-id="5d939-134">Vous en aurez besoin rapidement.</span><span class="sxs-lookup"><span data-stu-id="5d939-134">You will need it shortly.</span></span>

## <a name="2-set-up-your-app-to-use-adal4j-library-and-prerequisites-using-maven"></a><span data-ttu-id="5d939-135">2. Configurer votre application pour utiliser la bibliothèque ADAL4J et la configuration requise à l’aide de Maven</span><span class="sxs-lookup"><span data-stu-id="5d939-135">2. Set up your app to use ADAL4J library and prerequisites using Maven</span></span>
<span data-ttu-id="5d939-136">Ici, nous allons configurer ADAL4J pour utiliser le protocole d’authentification OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="5d939-136">Here, we'll configure ADAL4J to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="5d939-137">ADAL4J sera utilisée pour émettre des demandes de connexion et de déconnexion, gérer la session utilisateur et obtenir des informations concernant l’utilisateur, entre autres.</span><span class="sxs-lookup"><span data-stu-id="5d939-137">ADAL4J will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

* <span data-ttu-id="5d939-138">Dans le répertoire racine de votre projet, ouvrez/créez `pom.xml`, recherchez `// TODO: provide dependencies for Maven` et remplacez cette portion par les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5d939-138">In the root directory of your project, open/create `pom.xml` and locate the `// TODO: provide dependencies for Maven` and replace with the following:</span></span>

```Java
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>public-client-adal4j-sample</artifactId>
    <packaging>jar</packaging>
    <version>0.0.1-SNAPSHOT</version>
    <name>public-client-adal4j-sample</name>
    <url>http://maven.apache.org</url>
    <properties>
        <spring.version>3.0.5.RELEASE</spring.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>adal4j</artifactId>
            <version>1.1.2</version>
        </dependency>
        <dependency>
            <groupId>com.nimbusds</groupId>
            <artifactId>oauth2-oidc-sdk</artifactId>
            <version>4.5</version>
        </dependency>
        <dependency>
            <groupId>org.json</groupId>
            <artifactId>json</artifactId>
            <version>20090211</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.0.1</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>1.7.5</version>
        </dependency>
</dependencies>
    <build>
        <finalName>public-client-adal4j-sample</finalName>
        <plugins>
                <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <version>1.2.1</version>
            <configuration>
                <mainClass>PublicClient</mainClass>
            </configuration>
        </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>1.7</source>
                    <target>1.7</target>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <executions>
                    <execution>
                        <id>install</id>
                        <phase>install</phase>
                        <goals>
                            <goal>sources</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-resources-plugin</artifactId>
                <version>2.5</version>
                <configuration>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
        <artifactId>maven-assembly-plugin</artifactId>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
              <goal>single</goal>
            </goals>
          </execution>
        </executions>
        <configuration>
          <descriptorRefs>
            <descriptorRef>jar-with-dependencies</descriptorRef>
          </descriptorRefs>
        </configuration>
      </plugin>
      <plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-assembly-plugin</artifactId>
  <configuration>
    <archive>
      <manifest>
        <mainClass>PublicClient</mainClass>
      </manifest>
    </archive>
  </configuration>
</plugin>
        </plugins>
    </build>

</project>


```



## <a name="3-create-the-java-publicclient-file"></a><span data-ttu-id="5d939-139">3. Créer le fichier PublicClient Java</span><span class="sxs-lookup"><span data-stu-id="5d939-139">3. Create the Java PublicClient file</span></span>
<span data-ttu-id="5d939-140">Comme indiqué ci-dessus, nous utiliserons l’API Graph pour obtenir les données relatives à l’utilisateur connecté.</span><span class="sxs-lookup"><span data-stu-id="5d939-140">As indicated above, we will be using the Graph API to get data about the logged in user.</span></span> <span data-ttu-id="5d939-141">Afin de nous faciliter la tâche, nous devons créer un fichier pour représenter un **objet répertoire** et un fichier individuel pour représenter **l’utilisateur** afin que le modèle OO de Java puisse être utilisé.</span><span class="sxs-lookup"><span data-stu-id="5d939-141">For this to be easy for us we should create both a file to represent a **Directory Object** and an individual file to represent the **User** so that the OO pattern of Java can be used.</span></span>

* <span data-ttu-id="5d939-142">Créez un fichier appelé `DirectoryObject.java` que nous utiliserons pour stocker les données de base sur n’importe quel objet répertoire (n’hésitez pas à l’utiliser ultérieurement pour toutes vos autres requêtes Graph éventuelles).</span><span class="sxs-lookup"><span data-stu-id="5d939-142">Create a file called `DirectoryObject.java` which we will use to store basic data about any DirectoryObject (you can feel free to use this later for any other Graph Queries you may do).</span></span> <span data-ttu-id="5d939-143">Vous pouvez couper/coller ces éléments ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5d939-143">You can cut/paste this from below:</span></span>

```Java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

import javax.naming.ServiceUnavailableException;

import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;

public class PublicClient {

    private final static String AUTHORITY = "https://login.microsoftonline.com/common/";
    private final static String CLIENT_ID = "2a4da06c-ff07-410d-af8a-542a512f5092";

    public static void main(String args[]) throws Exception {

        try (BufferedReader br = new BufferedReader(new InputStreamReader(
                System.in))) {
            System.out.print("Enter username: ");
            String username = br.readLine();
            System.out.print("Enter password: ");
            String password = br.readLine();

            AuthenticationResult result = getAccessTokenFromUserCredentials(
                    username, password);
            System.out.println("Access Token - " + result.getAccessToken());
            System.out.println("Refresh Token - " + result.getRefreshToken());
            System.out.println("ID Token - " + result.getIdToken());
        }
    }

    private static AuthenticationResult getAccessTokenFromUserCredentials(
            String username, String password) throws Exception {
        AuthenticationContext context = null;
        AuthenticationResult result = null;
        ExecutorService service = null;
        try {
            service = Executors.newFixedThreadPool(1);
            context = new AuthenticationContext(AUTHORITY, false, service);
            Future<AuthenticationResult> future = context.acquireToken(
                    "https://graph.windows.net", CLIENT_ID, username, password,
                    null);
            result = future.get();
        } finally {
            service.shutdown();
        }

        if (result == null) {
            throw new ServiceUnavailableException(
                    "authentication result was null");
        }
        return result;
    }
}


```


## <a name="compile-and-run-the-sample"></a><span data-ttu-id="5d939-144">Compiler et exécuter l’exemple</span><span class="sxs-lookup"><span data-stu-id="5d939-144">Compile and run the sample</span></span>
<span data-ttu-id="5d939-145">Revenez à votre répertoire racine et exécutez la commande suivante pour générer l’exemple que vous venez de créer à l’aide de `maven`.</span><span class="sxs-lookup"><span data-stu-id="5d939-145">Change back out to your root directory and run the following command to build the sample you just put together using `maven`.</span></span> <span data-ttu-id="5d939-146">L’opération utilisera le fichier `pom.xml` que vous avez écrit pour vos dépendances.</span><span class="sxs-lookup"><span data-stu-id="5d939-146">This will use the `pom.xml` file you wrote for dependencies.</span></span>

`$ mvn package`

<span data-ttu-id="5d939-147">Vous devez maintenant disposer d’un fichier `adal4jsample.war` dans votre répertoire `/targets`.</span><span class="sxs-lookup"><span data-stu-id="5d939-147">You should now have a `adal4jsample.war` file in your `/targets` directory.</span></span> <span data-ttu-id="5d939-148">Vous pouvez le déployer dans votre conteneur Tomcat et ouvrir l’URL</span><span class="sxs-lookup"><span data-stu-id="5d939-148">You may deploy that in your Tomcat container and visit the URL</span></span> 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> <span data-ttu-id="5d939-149">Il est très facile de déployer un fichier WAR avec les derniers serveurs Tomcat.</span><span class="sxs-lookup"><span data-stu-id="5d939-149">It is very easy to deploy a WAR with the latest Tomcat servers.</span></span> <span data-ttu-id="5d939-150">Accédez simplement à `http://localhost:8080/manager/` et suivez les instructions pour charger votre fichier adal4jsample.war.</span><span class="sxs-lookup"><span data-stu-id="5d939-150">Simply navigate to `http://localhost:8080/manager/` and follow the instructions on uploading your ``adal4jsample.war\` file.</span></span> <span data-ttu-id="5d939-151">Il se déploiera automatiquement pour vous avec le point de terminaison correct.</span><span class="sxs-lookup"><span data-stu-id="5d939-151">It will autodeploy for you with the correct endpoint.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="5d939-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5d939-152">Next Steps</span></span>
<span data-ttu-id="5d939-153">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="5d939-153">Congratulations!</span></span> <span data-ttu-id="5d939-154">Vous disposez désormais d’une application Java fonctionnelle capable d’authentifier les utilisateurs, d’appeler en toute sécurité les API web à l’aide d’OAuth 2.0 et d’obtenir des informations de base concernant l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5d939-154">You now have a working Java application that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="5d939-155">Si vous ne l’avez pas encore fait, il est maintenant temps de remplir votre client avec quelques utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5d939-155">If you haven't already, now is the time to populate your tenant with some users.</span></span>

<span data-ttu-id="5d939-156">Pour référence, l’exemple terminé (sans vos valeurs de configuration) [est fourni ici au format .zip](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip). Vous pouvez également le cloner à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="5d939-156">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

