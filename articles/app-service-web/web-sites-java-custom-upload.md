---
title: "aaaUpload un tooAzure d’application web Java personnalisée"
description: "Ce didacticiel vous montre comment tooupload Java personnalisé web application tooAzure App Service Web Apps."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: eb2ccd83-e5c6-444e-a0fc-08fd5cc8326c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 0cb4a682bb25d86ff08bfd03628c89795c58451e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-java-web-app-tooazure"></a>Télécharger un tooAzure d’application web Java personnalisée
Cette rubrique explique comment tooupload Java personnalisé web application trop[Azure App Service] les applications Web. Les informations qui s’applique tooany Java site Web ou application web et également des exemples d’applications spécifiques sont incluses.

Notez que Azure offre un moyen pour créer des applications web de Java à l’aide d’interface utilisateur de configuration du portail d’Azure hello et hello Azure Marketplace, comme décrit dans [créer une application de web Java dans Azure App Service](web-sites-java-get-started.md). Ce didacticiel est pour les scénarios dans lesquels vous ne veulent interface de configuration du portail Azure hello toouse pas ou ne hello Azure Marketplace.  

## <a name="configuration-guidelines"></a>Instructions de configuration
suivante de Hello décrit les paramètres hello attendus pour les applications web Java personnalisées sur Azure.

* le port HTTP Hello utilisé par hello processus Java est attribué dynamiquement.  processus de Hello doit utiliser des ports hello à partir de la variable d’environnement hello `HTTP_PLATFORM_PORT`.
* Tous les écoutent les ports autres que le port d’écoute HTTP unique hello doit être désactivée.  Dans Tomcat, qui comprend l’arrêt hello, HTTPS et AJP ports.
* conteneur de Hello doit toobe configuré pour le trafic IPv4 uniquement.
* Hello **démarrage** commande pour application hello doit toobe défini dans la configuration de hello.
* Les applications qui requièrent des répertoires avec l’autorisation en écriture doivent toobe situé dans le répertoire de contenu de l’application hello web Azure, qui est **D:\home**.  variable d’environnement Hello `HOME` fait référence à tooD:\home.  

Vous pouvez définir des variables d’environnement en fonction des besoins dans le fichier web.config de hello.

## <a name="webconfig-httpplatform-configuration"></a>Configuration de httpPlatform dans web.config
Hello informations suivantes décrivent hello **httpplatform du fichier** mise en forme dans le fichier web.config.

**arguments** (Default=""). Toohello arguments exécutable ou un script spécifié dans hello **processPath** paramètre.

Exemples (avec **processPath** inclus) :

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


**processPath** -toohello de chemin d’accès au fichier exécutable ou un script qui lance un processus d’écoute les requêtes HTTP.

Exemples :

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

**rapidFailsPerMinute** (par défaut = 10.) Nombre de fois où les processus hello spécifié dans **processPath** est autorisée toocrash par minute. Si cette limite est dépassée, **HttpPlatformHandler** cesse de lancement du processus hello pour reste hello de minute de hello.

**requestTimeout** (par défaut = « 00:02:00 ») Durée pour laquelle **HttpPlatformHandler** attend une réponse à partir de processus hello qui écoute sur `%HTTP_PLATFORM_PORT%`.

**startupRetryCount** (par défaut = 10) Nombre de fois **HttpPlatformHandler** va tenter de processus de hello toolaunch spécifié dans **processPath**. Pour plus d’informations, consultez la section **startupTimeLimit**.

**startupTimeLimit** (par défaut = 10 secondes) Durée pour laquelle **HttpPlatformHandler** attendra hello exécutable/script toostart un processus à l’écoute sur le port hello.  Si cette limite de temps est dépassée, **HttpPlatformHandler** sera tuer un processus de hello et essayez toolaunch nouveau **startupRetryCount** fois.

**stdoutLogEnabled** (par défaut = « true ») Si la valeur est true, **stdout** et **stderr** pour les processus hello spécifié Bonjour **processPath** paramètre sera fichier redirigé toohello spécifié dans  **stdoutLogFile** (consultez **stdoutLogFile** section).

**stdoutLogFile** (par défaut = « d:\home\LogFiles\httpPlatformStdout.log ») Chemin d’accès absolu pour lequel **stdout** et **stderr** à partir de processus hello spécifié dans **processPath** doivent être enregistrés.

> [!NOTE]
> `%HTTP_PLATFORM_PORT%`est un espace réservé spécial qui doit toospecified en tant qu’élément de **arguments** ou dans le cadre de hello **httpplatform du fichier** **environmentVariables** liste. Il sera remplacé par un port généré en interne par **HttpPlatformHandler** afin que le processus de hello spécifié par **processPath** peuvent écouter sur ce port.
> 
> 

## <a name="deployment"></a>Déploiement
Java en fonction des applications web peuvent être déployées facilement via la plupart des hello que même indique qui est utilisée avec les applications web Internet Information Services (IIS) en fonction hello.  FTP, Git et Kudu est toutes prises en charge en tant que mécanisme de déploiement est hello fonctionnalités SCM intégrées pour les applications web. WebDeploy fonctionne comme un protocole, mais étant donné que Java n’est pas développé dans Visual Studio, WebDeploy n’est pas adapté au déploiement d’applications web Java.

## <a name="application-configuration-examples"></a>Exemples de configuration d'application
Pourquoi suit les applications, un fichier web.config hello configuration de l’application est fournie en tant qu’exemples tooshow comment tooenable votre application Java sur l’application de Service Web Apps.

### <a name="tomcat"></a>Tomcat
Lorsqu’il existe deux variantes Tomcat qui sont fournis avec les applications Web App Service, il est tout à fait possible tooupload client des instances spécifiques. Voici un exemple d'installation de Tomcat avec une machine virtuelle Java (JVM) différente.

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat" 
            arguments="">
          <environmentVariables>
            <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
            <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\bin\tomcat" />
            <environmentVariable name="JRE_HOME" value="%HOME%\site\wwwroot\bin\java" /> <!-- optional, if not specified, this will default too%programfiles%\Java -->
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

Sur le côté de Tomcat de hello, il existe quelques modifications de configuration qui doivent toobe effectuée. Hello server.xml doit toobe modifié tooset :

* Port d'arrêt = -1
* Port du connecteur HTTP = ${port.http}
* Adresse du connecteur HTTP = « 127.0.0.1 »
* Placement des connecteurs HTTPS et AJP en commentaires
* Hello IPv4 peut également être défini dans le fichier catalina.properties de hello dans laquelle vous pouvez ajouter`java.net.preferIPv4Stack=true`

App Service Web Apps ne prend pas en charge les appels Direct3d. toodisable, ajoutez hello suivant option Java à votre application établisse ces appels :`-Dsun.java2d.d3d=false`

### <a name="jetty"></a>Jetty
Comme hello pour Tomcat, les clients peuvent télécharger leurs propres instances pour Jetty. Dans les cas de hello d’une installation en cours d’exécution hello complète de Jetty, configuration de hello ressemble à ceci :

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httppPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe" 
             arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP_PLATFORM_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"
            startupTimeLimit="20"
          startupRetryCount="10"
          stdoutLogEnabled="true">
        </httpPlatform>
      </system.webServer>
    </configuration>

la configuration Jetty Hello doit toobe modifié dans hello start.ini tooset `java.net.preferIPv4Stack=true`.

### <a name="springboot"></a>Springboot
Dans l’ordre tooget une application Springboot en cours d’exécution vous devez tooupload votre fichier JAR ou WAR et ajouter hello le fichier web.config suivant. fichier web.config de Hello est placé dans le dossier wwwroot de hello. Dans le fichier web.config de hello ajuster le fichier JAR tooyour hello arguments toopoint, Bonjour le fichier JAR exemple hello suivant se trouve dans le dossier wwwroot de hello également.  

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
            arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\my-web-project.jar&quot;">
        </httpPlatform>
      </system.webServer>
    </configuration>


### <a name="hudson"></a>Hudson
Notre test utilisé hello war de Hudson 3.1.2 et hello instance de Tomcat 7.0.50 par défaut, mais sans utiliser choses de tooset hello l’interface utilisateur.  Hudson étant un outil de génération de logiciel, il est tooinstall conseillée sur dédié instances où hello **AlwaysOn** indicateur peut être défini sur l’application web de hello.

1. À la racine de votre application web, c’est-à-dire **d:\home\site\wwwroot**, créez un répertoire **webapps** (si ce n’est déjà fait), puis placez le fichier Hudson.war dans **d:\home\site\wwwroot\webapps**.
2. Téléchargez apache maven 3.0.5 (compatible avec Hudson) et placez-le dans **d:\home\site\wwwroot**.
3. Créer le fichier web.config situé dans **d:\home\site\wwwroot** et coller hello suivant contenu dans celui-ci :
   
        <?xml version="1.0" encoding="UTF-8"?>
        <configuration>
          <system.webServer>
            <handlers>
              <add name="httppPlatformHandler" path="*" verb="*" 
        modules="httpPlatformHandler" resourceType="Unspecified" />
            </handlers>
            <httpPlatform processPath="%AZURE_TOMCAT7_HOME%\bin\startup.bat"
        startupTimeLimit="20"
        startupRetryCount="10">
        <environmentVariables>
          <environmentVariable name="HUDSON_HOME" 
        value="%HOME%\site\wwwroot\hudson_home" />
          <environmentVariable name="JAVA_OPTS" 
        value="-Djava.net.preferIPv4Stack=true -Duser.home=%HOME%/site/wwwroot/user_home -Dhudson.DNSMultiCast.disabled=true" />
        </environmentVariables>            
            </httpPlatform>
          </system.webServer>
        </configuration>
   
    À ce stade hello l’application web peut être redémarré tootake hello modifications.  Se connecter toohttp://yourwebapp/hudson toostart Hudson.
4. Une fois Hudson se configure lui-même, vous devez voir hello suivant d’écran :
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. Hello d’accès page de configuration Hudson : cliquez sur **gérer les Hudson**, puis cliquez sur **configurer le système**.
6. Configurer hello JDK, comme indiqué ci-dessous :
   
    ![Configuration de Hudson](./media/web-sites-java-custom-upload/hudson2.png)
7. Configurez Maven comme indiqué ci-dessous :
   
    ![Configuration de Maven](./media/web-sites-java-custom-upload/maven.png)
8. Enregistrer les paramètres de hello. Hudson est désormais configuré et prêt à l'emploi.

Pour plus d'informations sur Hudson, consultez la page [http://hudson-ci.org](http://hudson-ci.org).

### <a name="liferay"></a>Liferay
App Service Web Apps prend en charge Liferay. Étant donné que Liferay peut nécessiter une mémoire importante, hello web application doit toorun un travailleur dédié moyenne ou grande, ce qui peut fournir suffisamment de mémoire. Liferay également prend plusieurs minutes toostart. Pour cette raison, il est recommandé de définir l’application web hello trop**Always On**.  

À l’aide de Liferay 6.1.2 que Community Edition GA3 fourni avec Tomcat, hello fichiers suivants ont été modifiées après le téléchargement Liferay :

**Server.xml**

* Modifier un arrêt port trop-1.
* Modifier le connecteur HTTP trop`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`
* Commentez connecteur AJP hello.

Bonjour **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** dossier, créez un fichier nommé **ext.properties-portail**. Ce fichier doit toocontain une seule ligne, comme illustré ici :

    liferay.home=%HOME%/site/wwwroot/liferay

À hello même niveau de répertoire comme dossier de tomcat-7.0.40 hello, créez un fichier nommé **web.config** avec hello suivant le contenu :

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
    <add name="httpPlatformHandler" path="*" verb="*"
         modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\tomcat-7.0.40\bin\catalina.bat" 
                      arguments="run" 
                      startupTimeLimit="10" 
                      requestTimeout="00:10:00" 
                      stdoutLogEnabled="true">
          <environmentVariables>
      <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
      <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\tomcat-7.0.40" />
            <environmentVariable name="JRE_HOME" value="D:\Program Files\Java\jdk1.7.0_51" /> 
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

Sous hello **httpplatform du fichier** bloquer, hello **requestTimeout** est défini trop « 00 : 10:00 ».  Il peut être réduit mais, vous êtes probablement toosee des erreurs de délai d’attente lors de l’amorçage de Liferay.  Si cette valeur est modifiée, puis hello **connectionTimeout** Tomcat de hello server.xml doit également être modifié.  

Il est important de noter que varariable d’environnement JRE_HOME hello est spécifié dans hello ci-dessus web.config toopoint toohello JDK 64 bits. par défaut de Hello 32 bits, mais Liferay peut nécessiter des niveaux élevés de mémoire, il est recommandé de toouse hello JDK 64 bits.

Une fois ces modifications effectuées, redémarrez votre application web qui exécute Liferay, puis ouvrez la page http://yourwebapp. portail de Liferay Hello est disponible à partir de la racine de l’application web hello. 

## <a name="next-steps"></a>Étapes suivantes
Pour plus d'informations sur Liferay, consultez la page [http://www.liferay.com](http://www.liferay.com).

Pour plus d’informations sur Java, consultez [Azure pour les développeurs Java](/java/azure).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
