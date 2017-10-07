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
# <a name="using-java-command-line-app-tooaccess-an-api-with-azure-ad"></a>À l’aide de la ligne de commande d’application Java tooAccess une API avec Azure AD
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure AD rend très simple toooutsource gestion des identités de votre application web, en fournissant une seule connexion et déconnexion avec seulement quelques lignes de code.  Dans les applications web Java, vous pouvez parvenir à l’aide de l’implémentation Microsoft de hello communautaire ADAL4J.

  Ici, nous allons utiliser ADAL4J pour :

* Signe hello utilisateur dans l’application hello à l’aide d’Azure AD en tant que fournisseur d’identité hello.
* Affiche des informations sur l’utilisateur de hello.
* Signe hello utilisateur hors de l’application de hello.

Dans commande toodo cela, vous devez :

1. inscrire une application auprès d’Azure AD ;
2. Configurer votre bibliothèque de ADAL4J application toouse hello.
3. Utilisez hello ADAL4J bibliothèque tooissue connectez-vous et demandes de déconnexion tooAzure AD.
4. Imprimer les données sur l’utilisateur de hello.

tooget démarré, [télécharger squelette d’application hello](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) ou [télécharger l’exemple hello terminée](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).  Vous aurez également besoin un locataire Azure AD dans le tooregister votre application.  Si vous n’avez pas déjà, [apprendre comment tooget un](active-directory-howto-tenant.md).

## <a name="1--register-an-application-with-azure-ad"></a>1.  Inscrire une application auprès d’Azure AD
tooenable vos utilisateurs tooauthenticate d’application, vous devez tout d’abord tooregister une nouvelle application dans votre client.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Sur la barre supérieure de hello, cliquez sur votre compte et sous hello **répertoire** , sélectionnez le client Active Directory de hello où vous souhaitez tooregister votre application.
3. Cliquez sur **plus Services** dans hello de navigation de gauche, puis choisissez **Azure Active Directory**.
4. Cliquez sur **Inscriptions des applications**, puis sur **Ajouter**.
5. Suivez les invites hello et créer un nouveau **Application Web et/ou WebAPI**.
  * Hello **nom** Hello application décrivent tooend-utilisateurs de votre application
  * Hello **URL de connexion** est l’URL de base hello de votre application.  valeur par défaut du squelette Hello est `http://localhost:8080/adal4jsample/`.
6. Une fois l’inscription terminée, AAD affecte un ID d’application unique à votre application.  Vous aurez besoin de cette valeur dans les sections suivantes hello, par conséquent, copiez-le à partir de l’onglet de l’application hello.
7. À partir de hello **paramètres** -> **propriétés** page de votre application, la mise à jour de hello URI ID d’application. Hello **URI ID d’application** est un identificateur unique pour votre application.  convention de Hello est toouse `https://<tenant-domain>/<app-name>`, par exemple `http://localhost:8080/adal4jsample/`.

Une fois, dans le portail hello pour votre application, créez un **clé** de hello **paramètres** page de votre application et le copier vers le bas.  Vous en aurez besoin rapidement.

## <a name="2-set-up-your-app-toouse-adal4j-library-and-prerequisites-using-maven"></a>2. Configurer votre bibliothèque de ADAL4J toouse application et les conditions préalables à l’aide de Maven
Ici, nous allons configurer protocole d’authentification OpenID Connect ADAL4J toouse hello.  ADAL4J est utilisé tooissue les demandes de connexion et déconnexion, gérer la session de l’utilisateur hello et obtenir des informations sur l’utilisateur hello, entre autres.

* Dans le répertoire racine de hello de votre projet, créer/ouvrir `pom.xml` et recherchez hello `// TODO: provide dependencies for Maven` et remplacez par hello qui suit :

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



## <a name="3-create-hello-java-publicclient-file"></a>3. Créer le fichier de Java PublicClient hello
Comme indiqué ci-dessus, nous allons utiliser hello données tooget de l’API Graph sur hello à l’utilisateur connecté. Pour cette toobe facile pour nous nous devons créer à la fois un toorepresent fichier un **objet annuaire** et un hello toorepresent de fichier **utilisateur** afin que hello OO modèle de Java peut être utilisé.

* Créez un fichier appelé `DirectoryObject.java` que nous utiliserons toostore les données de base sur n’importe quel DirectoryObject (vous pouvez être toouse libre cela plus tard pour toutes les autres requêtes graphique vous pouvez le faire). Vous pouvez couper/coller ces éléments ci-dessous :

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


## <a name="compile-and-run-hello-sample"></a>Compiler et exécuter l’exemple hello
Modifiez arrière répertoire tooyour et exécutez hello suivant commande toobuild hello exemple vous venez de créer à l’aide de `maven`. Ce processus utilisera hello `pom.xml` fichier que vous avez écrit des dépendances.

`$ mvn package`

Vous devez maintenant disposer d’un fichier `adal4jsample.war` dans votre répertoire `/targets`. Vous pouvez déployer dans votre conteneur de Tomcat et accédez à hello URL 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> Il est très facile toodeploy un WAR avec les serveurs Tomcat dernière hello. Accédez simplement trop`http://localhost:8080/manager/` et suivez les instructions de hello sur le téléchargement votre '' adal4jsample.war' fichier. Il sera autodeploy pour vous avec un point de terminaison correct hello.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Félicitations ! Vous avez une application Java qui a des utilisateurs tooauthenticate hello capacité, en toute sécurité appelez des API Web à l’aide d’OAuth 2.0 et obtenez des informations de base sur l’utilisateur de hello.  Si vous n’avez pas encore, est à présent hello temps toopopulate votre locataire avec certains utilisateurs.

Pour référence, hello effectuée exemple (sans les valeurs de configuration) [est fournie en tant qu’un fichier zip ici](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), ou vous pouvez le cloner à partir de GitHub :

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

