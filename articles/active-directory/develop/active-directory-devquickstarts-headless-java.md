---
title: "ligne de commande AD Java prise en main d’aaaAzure | Documents Microsoft"
description: Comment toobuild Java commande application de ligne qui signe les utilisateurs de tooaccess une API.
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
ms.openlocfilehash: 9ba1d1e794928a39ca1f091bd0e6eba57ce3d6aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-java-command-line-app-tooaccess-an-api-with-azure-ad"></a><span data-ttu-id="86484-103">À l’aide de la ligne de commande d’application Java tooAccess une API avec Azure AD</span><span class="sxs-lookup"><span data-stu-id="86484-103">Using Java Command Line App tooAccess An API with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="86484-104">Azure AD rend très simple toooutsource gestion des identités de votre application web, en fournissant une seule connexion et déconnexion avec seulement quelques lignes de code.</span><span class="sxs-lookup"><span data-stu-id="86484-104">Azure AD makes it simple and straightforward toooutsource your web app's identity management, providing single sign-in and sign-out with only a few lines of code.</span></span>  <span data-ttu-id="86484-105">Dans les applications web Java, vous pouvez parvenir à l’aide de l’implémentation Microsoft de hello communautaire ADAL4J.</span><span class="sxs-lookup"><span data-stu-id="86484-105">In Java web apps, you can accomplish this using Microsoft's implementation of hello community-driven ADAL4J.</span></span>

  <span data-ttu-id="86484-106">Ici, nous allons utiliser ADAL4J pour :</span><span class="sxs-lookup"><span data-stu-id="86484-106">Here we'll use ADAL4J to:</span></span>

* <span data-ttu-id="86484-107">Signe hello utilisateur dans l’application hello à l’aide d’Azure AD en tant que fournisseur d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="86484-107">Sign hello user into hello app using Azure AD as hello identity provider.</span></span>
* <span data-ttu-id="86484-108">Affiche des informations sur l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="86484-108">Display some information about hello user.</span></span>
* <span data-ttu-id="86484-109">Signe hello utilisateur hors de l’application de hello.</span><span class="sxs-lookup"><span data-stu-id="86484-109">Sign hello user out of hello app.</span></span>

<span data-ttu-id="86484-110">Dans commande toodo cela, vous devez :</span><span class="sxs-lookup"><span data-stu-id="86484-110">In order toodo this, you'll need to:</span></span>

1. <span data-ttu-id="86484-111">inscrire une application auprès d’Azure AD ;</span><span class="sxs-lookup"><span data-stu-id="86484-111">Register an application with Azure AD</span></span>
2. <span data-ttu-id="86484-112">Configurer votre bibliothèque de ADAL4J application toouse hello.</span><span class="sxs-lookup"><span data-stu-id="86484-112">Set up your app toouse hello ADAL4J library.</span></span>
3. <span data-ttu-id="86484-113">Utilisez hello ADAL4J bibliothèque tooissue connectez-vous et demandes de déconnexion tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="86484-113">Use hello ADAL4J library tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="86484-114">Imprimer les données sur l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="86484-114">Print out data about hello user.</span></span>

<span data-ttu-id="86484-115">tooget démarré, [télécharger squelette d’application hello](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) ou [télécharger l’exemple hello terminée](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="86484-115">tooget started, [download hello app skeleton](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) or [download hello completed sample](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span></span>  <span data-ttu-id="86484-116">Vous aurez également besoin un locataire Azure AD dans le tooregister votre application.</span><span class="sxs-lookup"><span data-stu-id="86484-116">You'll also need an Azure AD tenant in which tooregister your application.</span></span>  <span data-ttu-id="86484-117">Si vous n’avez pas déjà, [apprendre comment tooget un](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="86484-117">If you don't have one already, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1--register-an-application-with-azure-ad"></a><span data-ttu-id="86484-118">1.  Inscrire une application auprès d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="86484-118">1.  Register an Application with Azure AD</span></span>
<span data-ttu-id="86484-119">tooenable vos utilisateurs tooauthenticate d’application, vous devez tout d’abord tooregister une nouvelle application dans votre client.</span><span class="sxs-lookup"><span data-stu-id="86484-119">tooenable your app tooauthenticate users, you'll first need tooregister a new application in your tenant.</span></span>

1. <span data-ttu-id="86484-120">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="86484-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="86484-121">Sur la barre supérieure de hello, cliquez sur votre compte et sous hello **répertoire** , sélectionnez le client Active Directory de hello où vous souhaitez tooregister votre application.</span><span class="sxs-lookup"><span data-stu-id="86484-121">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="86484-122">Cliquez sur **plus Services** dans hello de navigation de gauche, puis choisissez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="86484-122">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="86484-123">Cliquez sur **Inscriptions des applications**, puis sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="86484-123">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="86484-124">Suivez les invites hello et créer un nouveau **Application Web et/ou WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="86484-124">Follow hello prompts and create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="86484-125">Hello **nom** Hello application décrivent tooend-utilisateurs de votre application</span><span class="sxs-lookup"><span data-stu-id="86484-125">hello **name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="86484-126">Hello **URL de connexion** est l’URL de base hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="86484-126">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="86484-127">valeur par défaut du squelette Hello est `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="86484-127">hello skeleton's default is `http://localhost:8080/adal4jsample/`.</span></span>
6. <span data-ttu-id="86484-128">Une fois l’inscription terminée, AAD affecte un ID d’application unique à votre application.</span><span class="sxs-lookup"><span data-stu-id="86484-128">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="86484-129">Vous aurez besoin de cette valeur dans les sections suivantes hello, par conséquent, copiez-le à partir de l’onglet de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="86484-129">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="86484-130">À partir de hello **paramètres** -> **propriétés** page de votre application, la mise à jour de hello URI ID d’application.</span><span class="sxs-lookup"><span data-stu-id="86484-130">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="86484-131">Hello **URI ID d’application** est un identificateur unique pour votre application.</span><span class="sxs-lookup"><span data-stu-id="86484-131">hello **App ID URI** is a unique identifier for your application.</span></span>  <span data-ttu-id="86484-132">convention de Hello est toouse `https://<tenant-domain>/<app-name>`, par exemple `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="86484-132">hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `http://localhost:8080/adal4jsample/`.</span></span>

<span data-ttu-id="86484-133">Une fois, dans le portail hello pour votre application, créez un **clé** de hello **paramètres** page de votre application et le copier vers le bas.</span><span class="sxs-lookup"><span data-stu-id="86484-133">Once in hello portal for your app create a **Key** from hello **Settings** page for your application and copy it down.</span></span>  <span data-ttu-id="86484-134">Vous en aurez besoin rapidement.</span><span class="sxs-lookup"><span data-stu-id="86484-134">You will need it shortly.</span></span>

## <a name="2-set-up-your-app-toouse-adal4j-library-and-prerequisites-using-maven"></a><span data-ttu-id="86484-135">2. Configurer votre bibliothèque de ADAL4J toouse application et les conditions préalables à l’aide de Maven</span><span class="sxs-lookup"><span data-stu-id="86484-135">2. Set up your app toouse ADAL4J library and prerequisites using Maven</span></span>
<span data-ttu-id="86484-136">Ici, nous allons configurer protocole d’authentification OpenID Connect ADAL4J toouse hello.</span><span class="sxs-lookup"><span data-stu-id="86484-136">Here, we'll configure ADAL4J toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="86484-137">ADAL4J est utilisé tooissue les demandes de connexion et déconnexion, gérer la session de l’utilisateur hello et obtenir des informations sur l’utilisateur hello, entre autres.</span><span class="sxs-lookup"><span data-stu-id="86484-137">ADAL4J will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

* <span data-ttu-id="86484-138">Dans le répertoire racine de hello de votre projet, créer/ouvrir `pom.xml` et recherchez hello `// TODO: provide dependencies for Maven` et remplacez par hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="86484-138">In hello root directory of your project, open/create `pom.xml` and locate hello `// TODO: provide dependencies for Maven` and replace with hello following:</span></span>

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



## <a name="3-create-hello-java-publicclient-file"></a><span data-ttu-id="86484-139">3. Créer le fichier de Java PublicClient hello</span><span class="sxs-lookup"><span data-stu-id="86484-139">3. Create hello Java PublicClient file</span></span>
<span data-ttu-id="86484-140">Comme indiqué ci-dessus, nous allons utiliser hello données tooget de l’API Graph sur hello à l’utilisateur connecté.</span><span class="sxs-lookup"><span data-stu-id="86484-140">As indicated above, we will be using hello Graph API tooget data about hello logged in user.</span></span> <span data-ttu-id="86484-141">Pour cette toobe facile pour nous nous devons créer à la fois un toorepresent fichier un **objet annuaire** et un hello toorepresent de fichier **utilisateur** afin que hello OO modèle de Java peut être utilisé.</span><span class="sxs-lookup"><span data-stu-id="86484-141">For this toobe easy for us we should create both a file toorepresent a **Directory Object** and an individual file toorepresent hello **User** so that hello OO pattern of Java can be used.</span></span>

* <span data-ttu-id="86484-142">Créez un fichier appelé `DirectoryObject.java` que nous utiliserons toostore les données de base sur n’importe quel DirectoryObject (vous pouvez être toouse libre cela plus tard pour toutes les autres requêtes graphique vous pouvez le faire).</span><span class="sxs-lookup"><span data-stu-id="86484-142">Create a file called `DirectoryObject.java` which we will use toostore basic data about any DirectoryObject (you can feel free toouse this later for any other Graph Queries you may do).</span></span> <span data-ttu-id="86484-143">Vous pouvez couper/coller ces éléments ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="86484-143">You can cut/paste this from below:</span></span>

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


## <a name="compile-and-run-hello-sample"></a><span data-ttu-id="86484-144">Compiler et exécuter l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="86484-144">Compile and run hello sample</span></span>
<span data-ttu-id="86484-145">Modifiez arrière répertoire tooyour et exécutez hello suivant commande toobuild hello exemple vous venez de créer à l’aide de `maven`.</span><span class="sxs-lookup"><span data-stu-id="86484-145">Change back out tooyour root directory and run hello following command toobuild hello sample you just put together using `maven`.</span></span> <span data-ttu-id="86484-146">Ce processus utilisera hello `pom.xml` fichier que vous avez écrit des dépendances.</span><span class="sxs-lookup"><span data-stu-id="86484-146">This will use hello `pom.xml` file you wrote for dependencies.</span></span>

`$ mvn package`

<span data-ttu-id="86484-147">Vous devez maintenant disposer d’un fichier `adal4jsample.war` dans votre répertoire `/targets`.</span><span class="sxs-lookup"><span data-stu-id="86484-147">You should now have a `adal4jsample.war` file in your `/targets` directory.</span></span> <span data-ttu-id="86484-148">Vous pouvez déployer dans votre conteneur de Tomcat et accédez à hello URL</span><span class="sxs-lookup"><span data-stu-id="86484-148">You may deploy that in your Tomcat container and visit hello URL</span></span> 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> <span data-ttu-id="86484-149">Il est très facile toodeploy un WAR avec les serveurs Tomcat dernière hello.</span><span class="sxs-lookup"><span data-stu-id="86484-149">It is very easy toodeploy a WAR with hello latest Tomcat servers.</span></span> <span data-ttu-id="86484-150">Accédez simplement trop`http://localhost:8080/manager/` et suivez les instructions de hello sur le téléchargement votre '' adal4jsample.war' fichier.</span><span class="sxs-lookup"><span data-stu-id="86484-150">Simply navigate too`http://localhost:8080/manager/` and follow hello instructions on uploading your ``adal4jsample.war\` file.</span></span> <span data-ttu-id="86484-151">Il sera autodeploy pour vous avec un point de terminaison correct hello.</span><span class="sxs-lookup"><span data-stu-id="86484-151">It will autodeploy for you with hello correct endpoint.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="86484-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="86484-152">Next Steps</span></span>
<span data-ttu-id="86484-153">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="86484-153">Congratulations!</span></span> <span data-ttu-id="86484-154">Vous avez une application Java qui a des utilisateurs tooauthenticate hello capacité, en toute sécurité appelez des API Web à l’aide d’OAuth 2.0 et obtenez des informations de base sur l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="86484-154">You now have a working Java application that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="86484-155">Si vous n’avez pas encore, est à présent hello temps toopopulate votre locataire avec certains utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="86484-155">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>

<span data-ttu-id="86484-156">Pour référence, hello effectuée exemple (sans les valeurs de configuration) [est fournie en tant qu’un fichier zip ici](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), ou vous pouvez le cloner à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="86484-156">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

