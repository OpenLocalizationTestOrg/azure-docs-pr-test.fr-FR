---
title: "Charger une application web Java personnalisée dans Azure"
description: "Ce didacticiel explique comment charger une application web Java personnalisée dans Azure App Service Web Apps."
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
ms.openlocfilehash: 9c8f9ee7780859f7640ac82d6ebce85082170ad7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-a-custom-java-web-app-to-azure"></a><span data-ttu-id="a9d0a-103">Charger une application web Java personnalisée dans Azure</span><span class="sxs-lookup"><span data-stu-id="a9d0a-103">Upload a custom Java web app to Azure</span></span>
<span data-ttu-id="a9d0a-104">Cette rubrique explique comment charger une application web Java personnalisée dans [Azure App Service] Web Apps.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-104">This topic explains how to upload a custom Java web app to [Azure App Service] Web Apps.</span></span> <span data-ttu-id="a9d0a-105">Vous y trouverez des informations s’appliquant à tous les sites web ou application web Java, ainsi que quelques exemples d’applications spécifiques.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-105">Included is information that applies to any Java website or web app, and also some examples for specific applications.</span></span>

<span data-ttu-id="a9d0a-106">Notez qu’Azure permet de créer des applications web Java en utilisant l’interface utilisateur de configuration du portail Azure ainsi qu’Azure Marketplace, comme décrit dans la page [Créer une application web Java dans Azure Web Service](web-sites-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a9d0a-106">Note that Azure provides a means for creating Java web apps using the Azure Portal's configuration UI, and the Azure Marketplace, as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md).</span></span> <span data-ttu-id="a9d0a-107">Ce didacticiel concerne les scénarios dans lesquels vous ne souhaitez pas utiliser l’interface utilisateur de configuration du portail Azure, ni Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-107">This tutorial is for scenarios in which you do not want to use the Azure Portal configuration UI or the Azure Marketplace.</span></span>  

## <a name="configuration-guidelines"></a><span data-ttu-id="a9d0a-108">Instructions de configuration</span><span class="sxs-lookup"><span data-stu-id="a9d0a-108">Configuration guidelines</span></span>
<span data-ttu-id="a9d0a-109">Voici les paramètres prévus pour les applications web Java personnalisées dans Azure :</span><span class="sxs-lookup"><span data-stu-id="a9d0a-109">The following describes the settings expected for custom Java web apps on Azure.</span></span>

* <span data-ttu-id="a9d0a-110">Le port HTTP utilisé par le processus Java est attribué dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-110">The HTTP port used by the Java process is dynamically assigned.</span></span>  <span data-ttu-id="a9d0a-111">Le processus doit utiliser le port à partir de la variable d’environnement `HTTP_PLATFORM_PORT`.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-111">The process must use the port from the environment variable `HTTP_PLATFORM_PORT`.</span></span>
* <span data-ttu-id="a9d0a-112">Tous les ports d'écoute autres que le seul écouteur HTTP doivent être désactivés.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-112">All listen ports other than the single HTTP listener should be disabled.</span></span>  <span data-ttu-id="a9d0a-113">Dans Tomcat, cela inclut le port d'arrêt ainsi que les ports HTTPS et AJP.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-113">In Tomcat, that includes the shutdown, HTTPS, and AJP ports.</span></span>
* <span data-ttu-id="a9d0a-114">Le conteneur doit être configuré pour le trafic IPv4 uniquement.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-114">The container needs to be configured for IPv4 traffic only.</span></span>
* <span data-ttu-id="a9d0a-115">La commande **startup** pour l'application doit être définie dans la configuration.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-115">The **startup** command for the application needs to be set in the configuration.</span></span>
* <span data-ttu-id="a9d0a-116">Les applications qui requièrent des répertoires accessibles en écriture doivent être situées dans le répertoire de contenu de l’application web Azure, soit **D:\home**.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-116">Applications that require directories with write permission need to be located in the Azure web app's content directory,  which is **D:\home**.</span></span>  <span data-ttu-id="a9d0a-117">La variable d’environnement `HOME` fait référence à D:\home.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-117">The environmental variable `HOME` refers to D:\home.</span></span>  

<span data-ttu-id="a9d0a-118">Vous pouvez définir les variables d'environnement comme requis dans le fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-118">You can set environment variables as required in the web.config file.</span></span>

## <a name="webconfig-httpplatform-configuration"></a><span data-ttu-id="a9d0a-119">Configuration de httpPlatform dans web.config</span><span class="sxs-lookup"><span data-stu-id="a9d0a-119">web.config httpPlatform configuration</span></span>
<span data-ttu-id="a9d0a-120">Les informations suivantes décrivent le format **httpPlatform** dans web.config :</span><span class="sxs-lookup"><span data-stu-id="a9d0a-120">The following information describes the **httpPlatform** format within web.config.</span></span>

<span data-ttu-id="a9d0a-121">**arguments** (Default="").</span><span class="sxs-lookup"><span data-stu-id="a9d0a-121">**arguments** (Default="").</span></span> <span data-ttu-id="a9d0a-122">Arguments de l’exécutable ou du script spécifiés dans le paramètre **processPath**.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-122">Arguments to the executable or script specified in the **processPath** setting.</span></span>

<span data-ttu-id="a9d0a-123">Exemples (avec **processPath** inclus) :</span><span class="sxs-lookup"><span data-stu-id="a9d0a-123">Examples (shown with **processPath** included):</span></span>

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


<span data-ttu-id="a9d0a-124">**processPath** : chemin d'accès à l'exécutable ou au script qui démarre un processus d'écoute des requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-124">**processPath** - Path to the executable or script that will launch a process listening for HTTP requests.</span></span>

<span data-ttu-id="a9d0a-125">Exemples :</span><span class="sxs-lookup"><span data-stu-id="a9d0a-125">Examples:</span></span>

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

<span data-ttu-id="a9d0a-126">**rapidFailsPerMinute** (par défaut = 10.) Nombre de fois par minute où le processus spécifié dans **processPath** est autorisé à se bloquer.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-126">**rapidFailsPerMinute** (Default=10.) Number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="a9d0a-127">Si cette limite est dépassée, **HttpPlatformHandler** arrête de démarrer le processus pendant le restant de la minute.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-127">If this limit is exceeded, **HttpPlatformHandler** will stop launching the process for the remainder of the minute.</span></span>

<span data-ttu-id="a9d0a-128">**requestTimeout** (par défaut = « 00:02:00 ») Durée pendant laquelle **HttpPlatformHandler** attend une réponse du processus à l’écoute sur `%HTTP_PLATFORM_PORT%`.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-128">**requestTimeout** (Default="00:02:00".) Duration for which **HttpPlatformHandler** will wait for a response from the process listening on `%HTTP_PLATFORM_PORT%`.</span></span>

<span data-ttu-id="a9d0a-129">**startupRetryCount** (par défaut = 10) Nombre de fois où **HttpPlatformHandler** tente de démarrer le processus spécifié dans **processPath**.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-129">**startupRetryCount** (Default=10.) Number of times **HttpPlatformHandler** will try to launch the process specified in **processPath**.</span></span> <span data-ttu-id="a9d0a-130">Pour plus d’informations, consultez la section **startupTimeLimit**.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-130">See **startupTimeLimit** for more details.</span></span>

<span data-ttu-id="a9d0a-131">**startupTimeLimit** (par défaut = 10 secondes) Durée pendant laquelle **HttpPlatformHandler** attend que l’exécutable/le script démarre un processus d’écoute du port.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-131">**startupTimeLimit** (Default=10 seconds.) Duration for which **HttpPlatformHandler** will wait for the executable/script to start a process listening on the port.</span></span>  <span data-ttu-id="a9d0a-132">Si cette limite de temps est dépassée, **HttpPlatformHandler** tue le processus et tente de le redémarrer **startupRetryCount** fois.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-132">If this time limit is exceeded, **HttpPlatformHandler** will kill the process and try to launch it again **startupRetryCount** times.</span></span>

<span data-ttu-id="a9d0a-133">**stdoutLogEnabled** (par défaut = « true ») Si true, **stdout** et **stderr** pour le processus spécifié dans le paramètre **processPath** sont redirigés vers le fichier spécifié dans **stdoutLogFile** (consultez la section **stdoutLogFile**).</span><span class="sxs-lookup"><span data-stu-id="a9d0a-133">**stdoutLogEnabled** (Default="true".) If true, **stdout** and **stderr** for the process specified in the **processPath** setting will be redirected to the file specified in **stdoutLogFile** (see **stdoutLogFile** section).</span></span>

<span data-ttu-id="a9d0a-134">**stdoutLogFile** (par défaut = « d:\home\LogFiles\httpPlatformStdout.log ») Chemin d’accès absolu au fichier pour lequel **stdout** et **stderr** sont journalisés à partir du processus spécifié dans **processPath**.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Absolute file path for which **stdout** and **stderr** from the process specified in **processPath** will be logged.</span></span>

> [!NOTE]
> <span data-ttu-id="a9d0a-135">`%HTTP_PLATFORM_PORT%` est un espace réservé spécial qui doit être spécifié soit dans les **arguments**, soit dans la liste **environmentVariables** de **httpPlatform**.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-135">`%HTTP_PLATFORM_PORT%` is a special placeholder which needs to specified either as part of **arguments** or as part of the **httpPlatform** **environmentVariables** list.</span></span> <span data-ttu-id="a9d0a-136">Un port généré en interne par **HttpPlatformHandler** le remplace afin que le processus spécifié par **processPath** puisse écouter ce port.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-136">This will be replaced by an internally generated port by **HttpPlatformHandler** so that the process specified by **processPath** can listen on this port.</span></span>
> 
> 

## <a name="deployment"></a><span data-ttu-id="a9d0a-137">Déploiement</span><span class="sxs-lookup"><span data-stu-id="a9d0a-137">Deployment</span></span>
<span data-ttu-id="a9d0a-138">Les applications web Java peuvent être déployées facilement via la plupart des outils utilisés pour les applications web IIS (Internet Information Services).</span><span class="sxs-lookup"><span data-stu-id="a9d0a-138">Java based web apps can be deployed easily through most of the same means that are used with the Internet Information Services (IIS) based web applications.</span></span>  <span data-ttu-id="a9d0a-139">Les mécanismes de déploiement FTP, Git et Kudu sont pris en charge, tout comme la fonctionnalité intégrée SCM pour les applications Web.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-139">FTP, Git and Kudu are all supported as deployment mechanisms, as is the integrated SCM capability for web apps.</span></span> <span data-ttu-id="a9d0a-140">WebDeploy fonctionne comme un protocole, mais étant donné que Java n’est pas développé dans Visual Studio, WebDeploy n’est pas adapté au déploiement d’applications web Java.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-140">WebDeploy works as a protocol, however, as Java is not developed in Visual Studio, WebDeploy does not fit with Java web app deployment use cases.</span></span>

## <a name="application-configuration-examples"></a><span data-ttu-id="a9d0a-141">Exemples de configuration d'application</span><span class="sxs-lookup"><span data-stu-id="a9d0a-141">Application configuration Examples</span></span>
<span data-ttu-id="a9d0a-142">Les applications suivantes utilisent un fichier web.config et la configuration de l’application comme exemples pour montrer comment activer votre application Java sur App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-142">For the following applications, a web.config file and the application configuration is provided as examples to show how to enable your Java application on App Service Web Apps.</span></span>

### <a name="tomcat"></a><span data-ttu-id="a9d0a-143">Tomcat</span><span class="sxs-lookup"><span data-stu-id="a9d0a-143">Tomcat</span></span>
<span data-ttu-id="a9d0a-144">Bien qu’il existe deux variantes Tomcat fournies avec App Service Web Apps, il est également possible de charger des instances spécifiques du client.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-144">While there are two variations on Tomcat that are supplied with App Service Web Apps, it is still quite possible to upload customer specific instances.</span></span> <span data-ttu-id="a9d0a-145">Voici un exemple d'installation de Tomcat avec une machine virtuelle Java (JVM) différente.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-145">Below is an example of an install of Tomcat with a different Java Virtual Machine (JVM).</span></span>

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
            <environmentVariable name="JRE_HOME" value="%HOME%\site\wwwroot\bin\java" /> <!-- optional, if not specified, this will default to %programfiles%\Java -->
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="a9d0a-146">Du côté de Tomcat, quelques modifications de configuration sont à effectuer.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-146">On the Tomcat side, there are a few configuration changes that need to be made.</span></span> <span data-ttu-id="a9d0a-147">server.xml doit être modifié pour définir :</span><span class="sxs-lookup"><span data-stu-id="a9d0a-147">The server.xml needs to be edited to set:</span></span>

* <span data-ttu-id="a9d0a-148">Port d'arrêt = -1</span><span class="sxs-lookup"><span data-stu-id="a9d0a-148">Shutdown port = -1</span></span>
* <span data-ttu-id="a9d0a-149">Port du connecteur HTTP = ${port.http}</span><span class="sxs-lookup"><span data-stu-id="a9d0a-149">HTTP connector port = ${port.http}</span></span>
* <span data-ttu-id="a9d0a-150">Adresse du connecteur HTTP = « 127.0.0.1 »</span><span class="sxs-lookup"><span data-stu-id="a9d0a-150">HTTP connector address = "127.0.0.1"</span></span>
* <span data-ttu-id="a9d0a-151">Placement des connecteurs HTTPS et AJP en commentaires</span><span class="sxs-lookup"><span data-stu-id="a9d0a-151">Comment out HTTPS and AJP connectors</span></span>
* <span data-ttu-id="a9d0a-152">Le paramètre IPv4 peut également être défini dans le fichier catalina.properties, où vous pouvez ajouter     `java.net.preferIPv4Stack=true`</span><span class="sxs-lookup"><span data-stu-id="a9d0a-152">The IPv4 setting can also be set in the catalina.properties file where you can add     `java.net.preferIPv4Stack=true`</span></span>

<span data-ttu-id="a9d0a-153">App Service Web Apps ne prend pas en charge les appels Direct3d.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-153">Direct3d calls are not supported on App Service Web Apps.</span></span> <span data-ttu-id="a9d0a-154">Pour les désactiver, ajoutez l’option Java suivante si votre application passe de tels appels : `-Dsun.java2d.d3d=false`</span><span class="sxs-lookup"><span data-stu-id="a9d0a-154">To disable those, add the following Java option should your application make such calls: `-Dsun.java2d.d3d=false`</span></span>

### <a name="jetty"></a><span data-ttu-id="a9d0a-155">Jetty</span><span class="sxs-lookup"><span data-stu-id="a9d0a-155">Jetty</span></span>
<span data-ttu-id="a9d0a-156">Comme pour Tomcat, les clients peuvent charger leurs propres instances pour Jetty.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-156">As is the case for Tomcat, customers can upload their own instances for Jetty.</span></span> <span data-ttu-id="a9d0a-157">En cas d'exécution de l'installation complète de Jetty, la configuration ressemblerait à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="a9d0a-157">In the case of running the full install of Jetty, the configuration would look like this:</span></span>

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

<span data-ttu-id="a9d0a-158">La configuration Jetty doit être changée dans le fichier start.ini pour définir `java.net.preferIPv4Stack=true`.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-158">The Jetty configuration needs to be changed in the start.ini to set `java.net.preferIPv4Stack=true`.</span></span>

### <a name="springboot"></a><span data-ttu-id="a9d0a-159">Springboot</span><span class="sxs-lookup"><span data-stu-id="a9d0a-159">Springboot</span></span>
<span data-ttu-id="a9d0a-160">Pour exécuter une application Springboot, vous devez télécharger votre fichier JAR ou WAR, puis ajoutez le fichier web.config suivant.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-160">In order to get a Springboot application running you need to upload your JAR or WAR file and add the following web.config file.</span></span> <span data-ttu-id="a9d0a-161">Le fichier web.config est placé dans le dossier wwwroot.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-161">The web.config file goes into the wwwroot folder.</span></span> <span data-ttu-id="a9d0a-162">Dans le fichier web.config, modifiez les arguments pour pointer vers votre fichier JAR. Dans l'exemple suivant, le fichier .jar se trouve également dans le dossier wwwroot.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-162">In the web.config adjust the arguments to point to your JAR file, in the following example the JAR file is located in the wwwroot folder as well.</span></span>  

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


### <a name="hudson"></a><span data-ttu-id="a9d0a-163">Hudson</span><span class="sxs-lookup"><span data-stu-id="a9d0a-163">Hudson</span></span>
<span data-ttu-id="a9d0a-164">Notre test a utilisé le war Hudson 3.1.2 et l'instance Tomcat 7.0.50 par défaut, mais pas l'interface utilisateur pour la configuration.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-164">Our test used the Hudson 3.1.2 war and the default Tomcat 7.0.50 instance but without using the UI to set things up.</span></span>  <span data-ttu-id="a9d0a-165">Comme Hudson est un outil de génération de logiciel, il est recommandé de l’installer sur des instances dédiées où l’indicateur **AlwaysOn** peut être défini sur l’application web.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-165">Because Hudson is a software build tool, it is advised to install it on dedicated instances where the **AlwaysOn** flag can be set on the web app.</span></span>

1. <span data-ttu-id="a9d0a-166">À la racine de votre application web, c’est-à-dire **d:\home\site\wwwroot**, créez un répertoire **webapps** (si ce n’est déjà fait), puis placez le fichier Hudson.war dans **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-166">In your web app’s root directory, i.e., **d:\home\site\wwwroot**, create a **webapps** directory (if not already present), and place Hudson.war in **d:\home\site\wwwroot\webapps**.</span></span>
2. <span data-ttu-id="a9d0a-167">Téléchargez apache maven 3.0.5 (compatible avec Hudson) et placez-le dans **d:\home\site\wwwroot**.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-167">Download apache maven 3.0.5 (compatible with Hudson) and place it in **d:\home\site\wwwroot**.</span></span>
3. <span data-ttu-id="a9d0a-168">Créez web.config dans **d:\home\site\wwwroot** et collez-y le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="a9d0a-168">Create web.config in **d:\home\site\wwwroot** and paste the following contents in it:</span></span>
   
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
   
    <span data-ttu-id="a9d0a-169">L’application web peut maintenant redémarrer pour prendre en compte les modifications.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-169">At this point the web app can be restarted to take the changes.</span></span>  <span data-ttu-id="a9d0a-170">Connectez-vous à http://yourwebapp/hudson pour démarrer Hudson.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-170">Connect to http://yourwebapp/hudson to start Hudson.</span></span>
4. <span data-ttu-id="a9d0a-171">Une fois que Hudson s'est configuré lui-même, l'écran suivant doit s'afficher :</span><span class="sxs-lookup"><span data-stu-id="a9d0a-171">After Hudson configures itself, you should see the following screen:</span></span>
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. <span data-ttu-id="a9d0a-173">Pour accéder à la page de configuration de Hudson, cliquez sur **Manage Hudson** puis **Configure System**.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-173">Access the Hudson configuration page: Click **Manage Hudson**, and then click **Configure System**.</span></span>
6. <span data-ttu-id="a9d0a-174">Configurez le JDK comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="a9d0a-174">Configure the JDK as shown below:</span></span>
   
    ![Configuration de Hudson](./media/web-sites-java-custom-upload/hudson2.png)
7. <span data-ttu-id="a9d0a-176">Configurez Maven comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="a9d0a-176">Configure Maven as shown below:</span></span>
   
    ![Configuration de Maven](./media/web-sites-java-custom-upload/maven.png)
8. <span data-ttu-id="a9d0a-178">Enregistrez les paramètres.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-178">Save the settings.</span></span> <span data-ttu-id="a9d0a-179">Hudson est désormais configuré et prêt à l'emploi.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-179">Hudson should now be configured and ready for use.</span></span>

<span data-ttu-id="a9d0a-180">Pour plus d'informations sur Hudson, consultez la page [http://hudson-ci.org](http://hudson-ci.org).</span><span class="sxs-lookup"><span data-stu-id="a9d0a-180">For additional information on Hudson, see [http://hudson-ci.org](http://hudson-ci.org).</span></span>

### <a name="liferay"></a><span data-ttu-id="a9d0a-181">Liferay</span><span class="sxs-lookup"><span data-stu-id="a9d0a-181">Liferay</span></span>
<span data-ttu-id="a9d0a-182">App Service Web Apps prend en charge Liferay.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-182">Liferay is supported on App Service Web Apps.</span></span> <span data-ttu-id="a9d0a-183">Étant donné que Liferay peut nécessiter une mémoire importante, l’application web doit s’exécuter sur un processus de travail dédié moyen ou important, capable de fournir une mémoire suffisante.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-183">Since Liferay can require significant memory, the web app needs to run on a medium or large dedicated worker, which can provide enough memory.</span></span> <span data-ttu-id="a9d0a-184">Le démarrage de Liferay prend également plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-184">Liferay also takes several minutes to start up.</span></span> <span data-ttu-id="a9d0a-185">Pour cette raison, il est recommandé de configurer l’application web sur **AlwaysOn**.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-185">For that reason, it is recommended that you set the web app to **Always On**.</span></span>  

<span data-ttu-id="a9d0a-186">En utilisant Liferay 6.1.2 Community Edition GA3 avec Tomcat, les fichiers suivants ont été modifiés après le téléchargement de Liferay :</span><span class="sxs-lookup"><span data-stu-id="a9d0a-186">Using Liferay 6.1.2 Community Edition GA3 bundled with Tomcat, the following files were edited after downloading Liferay:</span></span>

<span data-ttu-id="a9d0a-187">**Server.xml**</span><span class="sxs-lookup"><span data-stu-id="a9d0a-187">**Server.xml**</span></span>

* <span data-ttu-id="a9d0a-188">Modifiez le port d'arrêt sur -1.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-188">Change Shutdown port to -1.</span></span>
* <span data-ttu-id="a9d0a-189">Modifiez le connecteur HTTP sur `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span><span class="sxs-lookup"><span data-stu-id="a9d0a-189">Change HTTP connector to       `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span></span>
* <span data-ttu-id="a9d0a-190">Placez le connecteur AJP en commentaires.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-190">Comment out the AJP connector.</span></span>

<span data-ttu-id="a9d0a-191">Dans le dossier **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes**, créez un fichier nommé **portal-ext.properties**.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-191">In the **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** folder, create a file named **portal-ext.properties**.</span></span> <span data-ttu-id="a9d0a-192">Ce fichier doit contenir une ligne, comme illustrée ici :</span><span class="sxs-lookup"><span data-stu-id="a9d0a-192">This file needs to contain one line, as shown here:</span></span>

    liferay.home=%HOME%/site/wwwroot/liferay

<span data-ttu-id="a9d0a-193">Au même niveau d'arborescence que le dossier tomcat-7.0.40, créez un fichier nommé **web.config** avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="a9d0a-193">At the same directory level as the tomcat-7.0.40 folder, create a file named **web.config** with the following content:</span></span>

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

<span data-ttu-id="a9d0a-194">Sous le bloc **httpPlatform**, **requestTimeout** a la valeur « 00:10:00 ».</span><span class="sxs-lookup"><span data-stu-id="a9d0a-194">Under the **httpPlatform** block, the **requestTimeout** is set to “00:10:00”.</span></span>  <span data-ttu-id="a9d0a-195">Vous pouvez réduire cette valeur, mais certaines erreurs de délai d'attente sont alors susceptibles d'apparaître lors de l'amorçage de Liferay.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-195">It can be reduced but then you are likely to see some timeout errors while Liferay is bootstrapping.</span></span>  <span data-ttu-id="a9d0a-196">Si cette valeur est modifiée, **connectionTimeout** doit également être modifié dans tomcat server.xml.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-196">If this value is changed, then the **connectionTimeout** in the tomcat server.xml should also be modified.</span></span>  

<span data-ttu-id="a9d0a-197">Il est intéressant de remarquer que la variable d'environnement JRE_HOME est spécifiée dans web.config ci-dessus pour pointer vers le JDK 64 bits.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-197">It is worth noting that the JRE_HOME environnment varariable is specified in the above web.config to point to the 64-bit JDK.</span></span> <span data-ttu-id="a9d0a-198">Il est en 32 bits par défaut, mais étant donné que Liferay peut nécessiter d'importants niveaux de mémoire, il est recommandé d'utiliser le JDK 64 bits.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-198">The default is 32-bit, but since Liferay may require high levels of memory, it is recommended to use the 64-bit JDK.</span></span>

<span data-ttu-id="a9d0a-199">Une fois ces modifications effectuées, redémarrez votre application web qui exécute Liferay, puis ouvrez la page http://yourwebapp.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-199">Once you make these changes, restart your web app running Liferay, Then, open http://yourwebapp.</span></span> <span data-ttu-id="a9d0a-200">Le portail Liferay est disponible depuis la racine de l’application web.</span><span class="sxs-lookup"><span data-stu-id="a9d0a-200">The Liferay portal is available from the web app root.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a9d0a-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a9d0a-201">Next steps</span></span>
<span data-ttu-id="a9d0a-202">Pour plus d'informations sur Liferay, consultez la page [http://www.liferay.com](http://www.liferay.com).</span><span class="sxs-lookup"><span data-stu-id="a9d0a-202">For more information about Liferay, see [http://www.liferay.com](http://www.liferay.com).</span></span>

<span data-ttu-id="a9d0a-203">Pour plus d’informations sur Java, consultez [Azure pour les développeurs Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="a9d0a-203">For more information about Java, visit [Azure for Java developers](/java/azure).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
