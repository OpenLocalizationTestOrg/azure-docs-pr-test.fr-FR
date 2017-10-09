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
# <a name="upload-a-custom-java-web-app-tooazure"></a><span data-ttu-id="04f37-103">Télécharger un tooAzure d’application web Java personnalisée</span><span class="sxs-lookup"><span data-stu-id="04f37-103">Upload a custom Java web app tooAzure</span></span>
<span data-ttu-id="04f37-104">Cette rubrique explique comment tooupload Java personnalisé web application trop[Azure App Service] les applications Web.</span><span class="sxs-lookup"><span data-stu-id="04f37-104">This topic explains how tooupload a custom Java web app too[Azure App Service] Web Apps.</span></span> <span data-ttu-id="04f37-105">Les informations qui s’applique tooany Java site Web ou application web et également des exemples d’applications spécifiques sont incluses.</span><span class="sxs-lookup"><span data-stu-id="04f37-105">Included is information that applies tooany Java website or web app, and also some examples for specific applications.</span></span>

<span data-ttu-id="04f37-106">Notez que Azure offre un moyen pour créer des applications web de Java à l’aide d’interface utilisateur de configuration du portail d’Azure hello et hello Azure Marketplace, comme décrit dans [créer une application de web Java dans Azure App Service](web-sites-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="04f37-106">Note that Azure provides a means for creating Java web apps using hello Azure Portal's configuration UI, and hello Azure Marketplace, as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md).</span></span> <span data-ttu-id="04f37-107">Ce didacticiel est pour les scénarios dans lesquels vous ne veulent interface de configuration du portail Azure hello toouse pas ou ne hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="04f37-107">This tutorial is for scenarios in which you do not want toouse hello Azure Portal configuration UI or hello Azure Marketplace.</span></span>  

## <a name="configuration-guidelines"></a><span data-ttu-id="04f37-108">Instructions de configuration</span><span class="sxs-lookup"><span data-stu-id="04f37-108">Configuration guidelines</span></span>
<span data-ttu-id="04f37-109">suivante de Hello décrit les paramètres hello attendus pour les applications web Java personnalisées sur Azure.</span><span class="sxs-lookup"><span data-stu-id="04f37-109">hello following describes hello settings expected for custom Java web apps on Azure.</span></span>

* <span data-ttu-id="04f37-110">le port HTTP Hello utilisé par hello processus Java est attribué dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="04f37-110">hello HTTP port used by hello Java process is dynamically assigned.</span></span>  <span data-ttu-id="04f37-111">processus de Hello doit utiliser des ports hello à partir de la variable d’environnement hello `HTTP_PLATFORM_PORT`.</span><span class="sxs-lookup"><span data-stu-id="04f37-111">hello process must use hello port from hello environment variable `HTTP_PLATFORM_PORT`.</span></span>
* <span data-ttu-id="04f37-112">Tous les écoutent les ports autres que le port d’écoute HTTP unique hello doit être désactivée.</span><span class="sxs-lookup"><span data-stu-id="04f37-112">All listen ports other than hello single HTTP listener should be disabled.</span></span>  <span data-ttu-id="04f37-113">Dans Tomcat, qui comprend l’arrêt hello, HTTPS et AJP ports.</span><span class="sxs-lookup"><span data-stu-id="04f37-113">In Tomcat, that includes hello shutdown, HTTPS, and AJP ports.</span></span>
* <span data-ttu-id="04f37-114">conteneur de Hello doit toobe configuré pour le trafic IPv4 uniquement.</span><span class="sxs-lookup"><span data-stu-id="04f37-114">hello container needs toobe configured for IPv4 traffic only.</span></span>
* <span data-ttu-id="04f37-115">Hello **démarrage** commande pour application hello doit toobe défini dans la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="04f37-115">hello **startup** command for hello application needs toobe set in hello configuration.</span></span>
* <span data-ttu-id="04f37-116">Les applications qui requièrent des répertoires avec l’autorisation en écriture doivent toobe situé dans le répertoire de contenu de l’application hello web Azure, qui est **D:\home**.</span><span class="sxs-lookup"><span data-stu-id="04f37-116">Applications that require directories with write permission need toobe located in hello Azure web app's content directory,  which is **D:\home**.</span></span>  <span data-ttu-id="04f37-117">variable d’environnement Hello `HOME` fait référence à tooD:\home.</span><span class="sxs-lookup"><span data-stu-id="04f37-117">hello environmental variable `HOME` refers tooD:\home.</span></span>  

<span data-ttu-id="04f37-118">Vous pouvez définir des variables d’environnement en fonction des besoins dans le fichier web.config de hello.</span><span class="sxs-lookup"><span data-stu-id="04f37-118">You can set environment variables as required in hello web.config file.</span></span>

## <a name="webconfig-httpplatform-configuration"></a><span data-ttu-id="04f37-119">Configuration de httpPlatform dans web.config</span><span class="sxs-lookup"><span data-stu-id="04f37-119">web.config httpPlatform configuration</span></span>
<span data-ttu-id="04f37-120">Hello informations suivantes décrivent hello **httpplatform du fichier** mise en forme dans le fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="04f37-120">hello following information describes hello **httpPlatform** format within web.config.</span></span>

<span data-ttu-id="04f37-121">**arguments** (Default="").</span><span class="sxs-lookup"><span data-stu-id="04f37-121">**arguments** (Default="").</span></span> <span data-ttu-id="04f37-122">Toohello arguments exécutable ou un script spécifié dans hello **processPath** paramètre.</span><span class="sxs-lookup"><span data-stu-id="04f37-122">Arguments toohello executable or script specified in hello **processPath** setting.</span></span>

<span data-ttu-id="04f37-123">Exemples (avec **processPath** inclus) :</span><span class="sxs-lookup"><span data-stu-id="04f37-123">Examples (shown with **processPath** included):</span></span>

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


<span data-ttu-id="04f37-124">**processPath** -toohello de chemin d’accès au fichier exécutable ou un script qui lance un processus d’écoute les requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="04f37-124">**processPath** - Path toohello executable or script that will launch a process listening for HTTP requests.</span></span>

<span data-ttu-id="04f37-125">Exemples :</span><span class="sxs-lookup"><span data-stu-id="04f37-125">Examples:</span></span>

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

<span data-ttu-id="04f37-126">**rapidFailsPerMinute** (par défaut = 10.) Nombre de fois où les processus hello spécifié dans **processPath** est autorisée toocrash par minute.</span><span class="sxs-lookup"><span data-stu-id="04f37-126">**rapidFailsPerMinute** (Default=10.) Number of times hello process specified in **processPath** is allowed toocrash per minute.</span></span> <span data-ttu-id="04f37-127">Si cette limite est dépassée, **HttpPlatformHandler** cesse de lancement du processus hello pour reste hello de minute de hello.</span><span class="sxs-lookup"><span data-stu-id="04f37-127">If this limit is exceeded, **HttpPlatformHandler** will stop launching hello process for hello remainder of hello minute.</span></span>

<span data-ttu-id="04f37-128">**requestTimeout** (par défaut = « 00:02:00 ») Durée pour laquelle **HttpPlatformHandler** attend une réponse à partir de processus hello qui écoute sur `%HTTP_PLATFORM_PORT%`.</span><span class="sxs-lookup"><span data-stu-id="04f37-128">**requestTimeout** (Default="00:02:00".) Duration for which **HttpPlatformHandler** will wait for a response from hello process listening on `%HTTP_PLATFORM_PORT%`.</span></span>

<span data-ttu-id="04f37-129">**startupRetryCount** (par défaut = 10) Nombre de fois **HttpPlatformHandler** va tenter de processus de hello toolaunch spécifié dans **processPath**.</span><span class="sxs-lookup"><span data-stu-id="04f37-129">**startupRetryCount** (Default=10.) Number of times **HttpPlatformHandler** will try toolaunch hello process specified in **processPath**.</span></span> <span data-ttu-id="04f37-130">Pour plus d’informations, consultez la section **startupTimeLimit**.</span><span class="sxs-lookup"><span data-stu-id="04f37-130">See **startupTimeLimit** for more details.</span></span>

<span data-ttu-id="04f37-131">**startupTimeLimit** (par défaut = 10 secondes) Durée pour laquelle **HttpPlatformHandler** attendra hello exécutable/script toostart un processus à l’écoute sur le port hello.</span><span class="sxs-lookup"><span data-stu-id="04f37-131">**startupTimeLimit** (Default=10 seconds.) Duration for which **HttpPlatformHandler** will wait for hello executable/script toostart a process listening on hello port.</span></span>  <span data-ttu-id="04f37-132">Si cette limite de temps est dépassée, **HttpPlatformHandler** sera tuer un processus de hello et essayez toolaunch nouveau **startupRetryCount** fois.</span><span class="sxs-lookup"><span data-stu-id="04f37-132">If this time limit is exceeded, **HttpPlatformHandler** will kill hello process and try toolaunch it again **startupRetryCount** times.</span></span>

<span data-ttu-id="04f37-133">**stdoutLogEnabled** (par défaut = « true ») Si la valeur est true, **stdout** et **stderr** pour les processus hello spécifié Bonjour **processPath** paramètre sera fichier redirigé toohello spécifié dans  **stdoutLogFile** (consultez **stdoutLogFile** section).</span><span class="sxs-lookup"><span data-stu-id="04f37-133">**stdoutLogEnabled** (Default="true".) If true, **stdout** and **stderr** for hello process specified in hello **processPath** setting will be redirected toohello file specified in **stdoutLogFile** (see **stdoutLogFile** section).</span></span>

<span data-ttu-id="04f37-134">**stdoutLogFile** (par défaut = « d:\home\LogFiles\httpPlatformStdout.log ») Chemin d’accès absolu pour lequel **stdout** et **stderr** à partir de processus hello spécifié dans **processPath** doivent être enregistrés.</span><span class="sxs-lookup"><span data-stu-id="04f37-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Absolute file path for which **stdout** and **stderr** from hello process specified in **processPath** will be logged.</span></span>

> [!NOTE]
> <span data-ttu-id="04f37-135">`%HTTP_PLATFORM_PORT%`est un espace réservé spécial qui doit toospecified en tant qu’élément de **arguments** ou dans le cadre de hello **httpplatform du fichier** **environmentVariables** liste.</span><span class="sxs-lookup"><span data-stu-id="04f37-135">`%HTTP_PLATFORM_PORT%` is a special placeholder which needs toospecified either as part of **arguments** or as part of hello **httpPlatform** **environmentVariables** list.</span></span> <span data-ttu-id="04f37-136">Il sera remplacé par un port généré en interne par **HttpPlatformHandler** afin que le processus de hello spécifié par **processPath** peuvent écouter sur ce port.</span><span class="sxs-lookup"><span data-stu-id="04f37-136">This will be replaced by an internally generated port by **HttpPlatformHandler** so that hello process specified by **processPath** can listen on this port.</span></span>
> 
> 

## <a name="deployment"></a><span data-ttu-id="04f37-137">Déploiement</span><span class="sxs-lookup"><span data-stu-id="04f37-137">Deployment</span></span>
<span data-ttu-id="04f37-138">Java en fonction des applications web peuvent être déployées facilement via la plupart des hello que même indique qui est utilisée avec les applications web Internet Information Services (IIS) en fonction hello.</span><span class="sxs-lookup"><span data-stu-id="04f37-138">Java based web apps can be deployed easily through most of hello same means that are used with hello Internet Information Services (IIS) based web applications.</span></span>  <span data-ttu-id="04f37-139">FTP, Git et Kudu est toutes prises en charge en tant que mécanisme de déploiement est hello fonctionnalités SCM intégrées pour les applications web.</span><span class="sxs-lookup"><span data-stu-id="04f37-139">FTP, Git and Kudu are all supported as deployment mechanisms, as is hello integrated SCM capability for web apps.</span></span> <span data-ttu-id="04f37-140">WebDeploy fonctionne comme un protocole, mais étant donné que Java n’est pas développé dans Visual Studio, WebDeploy n’est pas adapté au déploiement d’applications web Java.</span><span class="sxs-lookup"><span data-stu-id="04f37-140">WebDeploy works as a protocol, however, as Java is not developed in Visual Studio, WebDeploy does not fit with Java web app deployment use cases.</span></span>

## <a name="application-configuration-examples"></a><span data-ttu-id="04f37-141">Exemples de configuration d'application</span><span class="sxs-lookup"><span data-stu-id="04f37-141">Application configuration Examples</span></span>
<span data-ttu-id="04f37-142">Pourquoi suit les applications, un fichier web.config hello configuration de l’application est fournie en tant qu’exemples tooshow comment tooenable votre application Java sur l’application de Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="04f37-142">For hello following applications, a web.config file and hello application configuration is provided as examples tooshow how tooenable your Java application on App Service Web Apps.</span></span>

### <a name="tomcat"></a><span data-ttu-id="04f37-143">Tomcat</span><span class="sxs-lookup"><span data-stu-id="04f37-143">Tomcat</span></span>
<span data-ttu-id="04f37-144">Lorsqu’il existe deux variantes Tomcat qui sont fournis avec les applications Web App Service, il est tout à fait possible tooupload client des instances spécifiques.</span><span class="sxs-lookup"><span data-stu-id="04f37-144">While there are two variations on Tomcat that are supplied with App Service Web Apps, it is still quite possible tooupload customer specific instances.</span></span> <span data-ttu-id="04f37-145">Voici un exemple d'installation de Tomcat avec une machine virtuelle Java (JVM) différente.</span><span class="sxs-lookup"><span data-stu-id="04f37-145">Below is an example of an install of Tomcat with a different Java Virtual Machine (JVM).</span></span>

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

<span data-ttu-id="04f37-146">Sur le côté de Tomcat de hello, il existe quelques modifications de configuration qui doivent toobe effectuée.</span><span class="sxs-lookup"><span data-stu-id="04f37-146">On hello Tomcat side, there are a few configuration changes that need toobe made.</span></span> <span data-ttu-id="04f37-147">Hello server.xml doit toobe modifié tooset :</span><span class="sxs-lookup"><span data-stu-id="04f37-147">hello server.xml needs toobe edited tooset:</span></span>

* <span data-ttu-id="04f37-148">Port d'arrêt = -1</span><span class="sxs-lookup"><span data-stu-id="04f37-148">Shutdown port = -1</span></span>
* <span data-ttu-id="04f37-149">Port du connecteur HTTP = ${port.http}</span><span class="sxs-lookup"><span data-stu-id="04f37-149">HTTP connector port = ${port.http}</span></span>
* <span data-ttu-id="04f37-150">Adresse du connecteur HTTP = « 127.0.0.1 »</span><span class="sxs-lookup"><span data-stu-id="04f37-150">HTTP connector address = "127.0.0.1"</span></span>
* <span data-ttu-id="04f37-151">Placement des connecteurs HTTPS et AJP en commentaires</span><span class="sxs-lookup"><span data-stu-id="04f37-151">Comment out HTTPS and AJP connectors</span></span>
* <span data-ttu-id="04f37-152">Hello IPv4 peut également être défini dans le fichier catalina.properties de hello dans laquelle vous pouvez ajouter`java.net.preferIPv4Stack=true`</span><span class="sxs-lookup"><span data-stu-id="04f37-152">hello IPv4 setting can also be set in hello catalina.properties file where you can add     `java.net.preferIPv4Stack=true`</span></span>

<span data-ttu-id="04f37-153">App Service Web Apps ne prend pas en charge les appels Direct3d.</span><span class="sxs-lookup"><span data-stu-id="04f37-153">Direct3d calls are not supported on App Service Web Apps.</span></span> <span data-ttu-id="04f37-154">toodisable, ajoutez hello suivant option Java à votre application établisse ces appels :`-Dsun.java2d.d3d=false`</span><span class="sxs-lookup"><span data-stu-id="04f37-154">toodisable those, add hello following Java option should your application make such calls: `-Dsun.java2d.d3d=false`</span></span>

### <a name="jetty"></a><span data-ttu-id="04f37-155">Jetty</span><span class="sxs-lookup"><span data-stu-id="04f37-155">Jetty</span></span>
<span data-ttu-id="04f37-156">Comme hello pour Tomcat, les clients peuvent télécharger leurs propres instances pour Jetty.</span><span class="sxs-lookup"><span data-stu-id="04f37-156">As is hello case for Tomcat, customers can upload their own instances for Jetty.</span></span> <span data-ttu-id="04f37-157">Dans les cas de hello d’une installation en cours d’exécution hello complète de Jetty, configuration de hello ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="04f37-157">In hello case of running hello full install of Jetty, hello configuration would look like this:</span></span>

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

<span data-ttu-id="04f37-158">la configuration Jetty Hello doit toobe modifié dans hello start.ini tooset `java.net.preferIPv4Stack=true`.</span><span class="sxs-lookup"><span data-stu-id="04f37-158">hello Jetty configuration needs toobe changed in hello start.ini tooset `java.net.preferIPv4Stack=true`.</span></span>

### <a name="springboot"></a><span data-ttu-id="04f37-159">Springboot</span><span class="sxs-lookup"><span data-stu-id="04f37-159">Springboot</span></span>
<span data-ttu-id="04f37-160">Dans l’ordre tooget une application Springboot en cours d’exécution vous devez tooupload votre fichier JAR ou WAR et ajouter hello le fichier web.config suivant.</span><span class="sxs-lookup"><span data-stu-id="04f37-160">In order tooget a Springboot application running you need tooupload your JAR or WAR file and add hello following web.config file.</span></span> <span data-ttu-id="04f37-161">fichier web.config de Hello est placé dans le dossier wwwroot de hello.</span><span class="sxs-lookup"><span data-stu-id="04f37-161">hello web.config file goes into hello wwwroot folder.</span></span> <span data-ttu-id="04f37-162">Dans le fichier web.config de hello ajuster le fichier JAR tooyour hello arguments toopoint, Bonjour le fichier JAR exemple hello suivant se trouve dans le dossier wwwroot de hello également.</span><span class="sxs-lookup"><span data-stu-id="04f37-162">In hello web.config adjust hello arguments toopoint tooyour JAR file, in hello following example hello JAR file is located in hello wwwroot folder as well.</span></span>  

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


### <a name="hudson"></a><span data-ttu-id="04f37-163">Hudson</span><span class="sxs-lookup"><span data-stu-id="04f37-163">Hudson</span></span>
<span data-ttu-id="04f37-164">Notre test utilisé hello war de Hudson 3.1.2 et hello instance de Tomcat 7.0.50 par défaut, mais sans utiliser choses de tooset hello l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="04f37-164">Our test used hello Hudson 3.1.2 war and hello default Tomcat 7.0.50 instance but without using hello UI tooset things up.</span></span>  <span data-ttu-id="04f37-165">Hudson étant un outil de génération de logiciel, il est tooinstall conseillée sur dédié instances où hello **AlwaysOn** indicateur peut être défini sur l’application web de hello.</span><span class="sxs-lookup"><span data-stu-id="04f37-165">Because Hudson is a software build tool, it is advised tooinstall it on dedicated instances where hello **AlwaysOn** flag can be set on hello web app.</span></span>

1. <span data-ttu-id="04f37-166">À la racine de votre application web, c’est-à-dire **d:\home\site\wwwroot**, créez un répertoire **webapps** (si ce n’est déjà fait), puis placez le fichier Hudson.war dans **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="04f37-166">In your web app’s root directory, i.e., **d:\home\site\wwwroot**, create a **webapps** directory (if not already present), and place Hudson.war in **d:\home\site\wwwroot\webapps**.</span></span>
2. <span data-ttu-id="04f37-167">Téléchargez apache maven 3.0.5 (compatible avec Hudson) et placez-le dans **d:\home\site\wwwroot**.</span><span class="sxs-lookup"><span data-stu-id="04f37-167">Download apache maven 3.0.5 (compatible with Hudson) and place it in **d:\home\site\wwwroot**.</span></span>
3. <span data-ttu-id="04f37-168">Créer le fichier web.config situé dans **d:\home\site\wwwroot** et coller hello suivant contenu dans celui-ci :</span><span class="sxs-lookup"><span data-stu-id="04f37-168">Create web.config in **d:\home\site\wwwroot** and paste hello following contents in it:</span></span>
   
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
   
    <span data-ttu-id="04f37-169">À ce stade hello l’application web peut être redémarré tootake hello modifications.</span><span class="sxs-lookup"><span data-stu-id="04f37-169">At this point hello web app can be restarted tootake hello changes.</span></span>  <span data-ttu-id="04f37-170">Se connecter toohttp://yourwebapp/hudson toostart Hudson.</span><span class="sxs-lookup"><span data-stu-id="04f37-170">Connect toohttp://yourwebapp/hudson toostart Hudson.</span></span>
4. <span data-ttu-id="04f37-171">Une fois Hudson se configure lui-même, vous devez voir hello suivant d’écran :</span><span class="sxs-lookup"><span data-stu-id="04f37-171">After Hudson configures itself, you should see hello following screen:</span></span>
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. <span data-ttu-id="04f37-173">Hello d’accès page de configuration Hudson : cliquez sur **gérer les Hudson**, puis cliquez sur **configurer le système**.</span><span class="sxs-lookup"><span data-stu-id="04f37-173">Access hello Hudson configuration page: Click **Manage Hudson**, and then click **Configure System**.</span></span>
6. <span data-ttu-id="04f37-174">Configurer hello JDK, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="04f37-174">Configure hello JDK as shown below:</span></span>
   
    ![Configuration de Hudson](./media/web-sites-java-custom-upload/hudson2.png)
7. <span data-ttu-id="04f37-176">Configurez Maven comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="04f37-176">Configure Maven as shown below:</span></span>
   
    ![Configuration de Maven](./media/web-sites-java-custom-upload/maven.png)
8. <span data-ttu-id="04f37-178">Enregistrer les paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="04f37-178">Save hello settings.</span></span> <span data-ttu-id="04f37-179">Hudson est désormais configuré et prêt à l'emploi.</span><span class="sxs-lookup"><span data-stu-id="04f37-179">Hudson should now be configured and ready for use.</span></span>

<span data-ttu-id="04f37-180">Pour plus d'informations sur Hudson, consultez la page [http://hudson-ci.org](http://hudson-ci.org).</span><span class="sxs-lookup"><span data-stu-id="04f37-180">For additional information on Hudson, see [http://hudson-ci.org](http://hudson-ci.org).</span></span>

### <a name="liferay"></a><span data-ttu-id="04f37-181">Liferay</span><span class="sxs-lookup"><span data-stu-id="04f37-181">Liferay</span></span>
<span data-ttu-id="04f37-182">App Service Web Apps prend en charge Liferay.</span><span class="sxs-lookup"><span data-stu-id="04f37-182">Liferay is supported on App Service Web Apps.</span></span> <span data-ttu-id="04f37-183">Étant donné que Liferay peut nécessiter une mémoire importante, hello web application doit toorun un travailleur dédié moyenne ou grande, ce qui peut fournir suffisamment de mémoire.</span><span class="sxs-lookup"><span data-stu-id="04f37-183">Since Liferay can require significant memory, hello web app needs toorun on a medium or large dedicated worker, which can provide enough memory.</span></span> <span data-ttu-id="04f37-184">Liferay également prend plusieurs minutes toostart.</span><span class="sxs-lookup"><span data-stu-id="04f37-184">Liferay also takes several minutes toostart up.</span></span> <span data-ttu-id="04f37-185">Pour cette raison, il est recommandé de définir l’application web hello trop**Always On**.</span><span class="sxs-lookup"><span data-stu-id="04f37-185">For that reason, it is recommended that you set hello web app too**Always On**.</span></span>  

<span data-ttu-id="04f37-186">À l’aide de Liferay 6.1.2 que Community Edition GA3 fourni avec Tomcat, hello fichiers suivants ont été modifiées après le téléchargement Liferay :</span><span class="sxs-lookup"><span data-stu-id="04f37-186">Using Liferay 6.1.2 Community Edition GA3 bundled with Tomcat, hello following files were edited after downloading Liferay:</span></span>

<span data-ttu-id="04f37-187">**Server.xml**</span><span class="sxs-lookup"><span data-stu-id="04f37-187">**Server.xml**</span></span>

* <span data-ttu-id="04f37-188">Modifier un arrêt port trop-1.</span><span class="sxs-lookup"><span data-stu-id="04f37-188">Change Shutdown port too-1.</span></span>
* <span data-ttu-id="04f37-189">Modifier le connecteur HTTP trop`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span><span class="sxs-lookup"><span data-stu-id="04f37-189">Change HTTP connector too       `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span></span>
* <span data-ttu-id="04f37-190">Commentez connecteur AJP hello.</span><span class="sxs-lookup"><span data-stu-id="04f37-190">Comment out hello AJP connector.</span></span>

<span data-ttu-id="04f37-191">Bonjour **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** dossier, créez un fichier nommé **ext.properties-portail**.</span><span class="sxs-lookup"><span data-stu-id="04f37-191">In hello **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** folder, create a file named **portal-ext.properties**.</span></span> <span data-ttu-id="04f37-192">Ce fichier doit toocontain une seule ligne, comme illustré ici :</span><span class="sxs-lookup"><span data-stu-id="04f37-192">This file needs toocontain one line, as shown here:</span></span>

    liferay.home=%HOME%/site/wwwroot/liferay

<span data-ttu-id="04f37-193">À hello même niveau de répertoire comme dossier de tomcat-7.0.40 hello, créez un fichier nommé **web.config** avec hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="04f37-193">At hello same directory level as hello tomcat-7.0.40 folder, create a file named **web.config** with hello following content:</span></span>

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

<span data-ttu-id="04f37-194">Sous hello **httpplatform du fichier** bloquer, hello **requestTimeout** est défini trop « 00 : 10:00 ».</span><span class="sxs-lookup"><span data-stu-id="04f37-194">Under hello **httpPlatform** block, hello **requestTimeout** is set too“00:10:00”.</span></span>  <span data-ttu-id="04f37-195">Il peut être réduit mais, vous êtes probablement toosee des erreurs de délai d’attente lors de l’amorçage de Liferay.</span><span class="sxs-lookup"><span data-stu-id="04f37-195">It can be reduced but then you are likely toosee some timeout errors while Liferay is bootstrapping.</span></span>  <span data-ttu-id="04f37-196">Si cette valeur est modifiée, puis hello **connectionTimeout** Tomcat de hello server.xml doit également être modifié.</span><span class="sxs-lookup"><span data-stu-id="04f37-196">If this value is changed, then hello **connectionTimeout** in hello tomcat server.xml should also be modified.</span></span>  

<span data-ttu-id="04f37-197">Il est important de noter que varariable d’environnement JRE_HOME hello est spécifié dans hello ci-dessus web.config toopoint toohello JDK 64 bits.</span><span class="sxs-lookup"><span data-stu-id="04f37-197">It is worth noting that hello JRE_HOME environnment varariable is specified in hello above web.config toopoint toohello 64-bit JDK.</span></span> <span data-ttu-id="04f37-198">par défaut de Hello 32 bits, mais Liferay peut nécessiter des niveaux élevés de mémoire, il est recommandé de toouse hello JDK 64 bits.</span><span class="sxs-lookup"><span data-stu-id="04f37-198">hello default is 32-bit, but since Liferay may require high levels of memory, it is recommended toouse hello 64-bit JDK.</span></span>

<span data-ttu-id="04f37-199">Une fois ces modifications effectuées, redémarrez votre application web qui exécute Liferay, puis ouvrez la page http://yourwebapp.</span><span class="sxs-lookup"><span data-stu-id="04f37-199">Once you make these changes, restart your web app running Liferay, Then, open http://yourwebapp.</span></span> <span data-ttu-id="04f37-200">portail de Liferay Hello est disponible à partir de la racine de l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="04f37-200">hello Liferay portal is available from hello web app root.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="04f37-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="04f37-201">Next steps</span></span>
<span data-ttu-id="04f37-202">Pour plus d'informations sur Liferay, consultez la page [http://www.liferay.com](http://www.liferay.com).</span><span class="sxs-lookup"><span data-stu-id="04f37-202">For more information about Liferay, see [http://www.liferay.com](http://www.liferay.com).</span></span>

<span data-ttu-id="04f37-203">Pour plus d’informations sur Java, consultez [Azure pour les développeurs Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="04f37-203">For more information about Java, visit [Azure for Java developers](/java/azure).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
