---
title: "Configuration avancée et extensions des applications web Azure App Service"
description: "Utilisez les déclarations XDT (XML Document Transformation) pour transformer le fichier ApplicationHost.config dans votre application web Azure App Service et ajouter des extensions privées permettant d’effectuer des actions d’administration personnalisées."
author: cephalin
writer: cephalin
editor: mollybos
manager: erikre
services: app-service
documentationcenter: 
ms.assetid: b441a286-ef38-4abc-b102-cdb249baf5bc
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: 314d3a954e712b829e7cf5eb37b23b31670f976b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a><span data-ttu-id="21729-103">Configuration avancée et extensions des applications web Azure App Service</span><span class="sxs-lookup"><span data-stu-id="21729-103">Azure App Service web app advanced config and extensions</span></span>
<span data-ttu-id="21729-104">En utilisant les déclarations [XML Document Transformation](http://msdn.microsoft.com/library/dd465326.aspx) (XDT), vous pouvez transformer le fichier [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) de votre application web dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="21729-104">By using [XML Document Transformation](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) declarations, you can transform the [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) file in your web app in Azure App Service.</span></span> <span data-ttu-id="21729-105">Vous pouvez également utiliser les déclarations XDT pour ajouter des extensions privées autorisant des actions d’administration d’application web personnalisées.</span><span class="sxs-lookup"><span data-stu-id="21729-105">You can also use XDT declarations to add private extensions to enable custom web app administration actions.</span></span> <span data-ttu-id="21729-106">Le présent article inclut un exemple d’extension d’application web PHP Manager, qui permet de gérer les paramètres PHP par le biais d’une interface web.</span><span class="sxs-lookup"><span data-stu-id="21729-106">This article includes a sample PHP Manager web app extension that enables management of PHP settings through a web interface.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="21729-107"><a id="transform"></a>Configuration avancée via ApplicationHost.config</span><span class="sxs-lookup"><span data-stu-id="21729-107"><a id="transform"></a>Advanced configuration through ApplicationHost.config</span></span>
<span data-ttu-id="21729-108">La plateforme App Service apporte flexibilité et contrôle à la configuration de l’application web.</span><span class="sxs-lookup"><span data-stu-id="21729-108">The App Service platform provides flexibility and control for web app configuration.</span></span> <span data-ttu-id="21729-109">Bien que le fichier de configuration ApplicationHost.config IIS standard ne puisse pas être modifié directement dans App Service, la plateforme prend en charge un modèle de transformation ApplicationHost.config déclaratif basé sur XDT.</span><span class="sxs-lookup"><span data-stu-id="21729-109">Although the standard IIS ApplicationHost.config configuration file is not available for direct editing in App Service, the platform supports a declarative ApplicationHost.config transform model based on XML Document Transformation (XDT).</span></span>

<span data-ttu-id="21729-110">Pour tirer parti de cette fonctionnalité de transformation, vous créez un fichier ApplicationHost.xdt avec du contenu XDT et vous le placez à la racine du site (d:\home\site) dans la [console Kudu](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span><span class="sxs-lookup"><span data-stu-id="21729-110">To leverage this transform functionality, you create an ApplicationHost.xdt file with XDT content and place under the site root (d:\home\site) in the [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span></span> <span data-ttu-id="21729-111">Vous devrez peut-être redémarrer l’application web pour que les modifications soient appliquées.</span><span class="sxs-lookup"><span data-stu-id="21729-111">You may need to restart the Web App for changes to take effect.</span></span>

<span data-ttu-id="21729-112">L’exemple applicationHost.xdt suivant montre comment ajouter une nouvelle variable d’environnement personnalisée à une application web utilisant PHP 5.4.</span><span class="sxs-lookup"><span data-stu-id="21729-112">The following applicationHost.xdt sample shows how to add a new custom environment variable to a web app that uses PHP 5.4.</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <fastCgi>
      <application>
        <environmentVariables>
          <environmentVariable name="CONFIGTEST" value="TEST" xdt:Transform="Insert" xdt:Locator="XPath(/configuration/system.webServer/fastCgi/application[contains(@fullPath,'5.4')]/environmentVariables)" />
        </environmentVariables>
      </application>
    </fastCgi>
  </system.webServer>
</configuration>
```

<span data-ttu-id="21729-113">Un fichier journal avec le statut et les détails de transformation est disponible à la racine FTP sous LogFiles\Transform.</span><span class="sxs-lookup"><span data-stu-id="21729-113">A log file with transform status and details is available from the FTP root under LogFiles\Transform.</span></span>

<span data-ttu-id="21729-114">Pour d’autres exemples, consultez la page [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span><span class="sxs-lookup"><span data-stu-id="21729-114">For additional samples, see [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span></span>

<span data-ttu-id="21729-115">**Remarque :**</span><span class="sxs-lookup"><span data-stu-id="21729-115">**Note**</span></span><br />
<span data-ttu-id="21729-116">Les éléments de la liste de modules sous `system.webServer` ne peuvent pas être supprimés ni réorganisés, mais des ajouts à la liste sont possibles.</span><span class="sxs-lookup"><span data-stu-id="21729-116">Elements from the list of modules under `system.webServer` cannot be removed or reordered, but additions to the list are possible.</span></span>

## <span data-ttu-id="21729-117"><a id="extend"></a> Étendre votre application web</span><span class="sxs-lookup"><span data-stu-id="21729-117"><a id="extend"></a> Extend your web app</span></span>
### <span data-ttu-id="21729-118"><a id="overview"></a> Vue d’ensemble des extensions privées d’application web</span><span class="sxs-lookup"><span data-stu-id="21729-118"><a id="overview"></a> Overview of private web app extensions</span></span>
<span data-ttu-id="21729-119">App Service prend en charge les extensions d’application web comme point d’extensibilité des actions d’administration.</span><span class="sxs-lookup"><span data-stu-id="21729-119">App Service supports web app extensions as an extensibility point for administrative actions.</span></span> <span data-ttu-id="21729-120">En fait, certaines fonctionnalités de la plateforme App Service sont implémentées en tant qu’extensions préinstallées.</span><span class="sxs-lookup"><span data-stu-id="21729-120">In fact, some App Service platform features are implemented as pre-installed extensions.</span></span> <span data-ttu-id="21729-121">Bien qu’il ne soit pas possible de modifier ces dernières, vous pouvez créer et configurer des extensions privées pour vos propres applications web.</span><span class="sxs-lookup"><span data-stu-id="21729-121">While the pre-installed platform extensions cannot be modified, you can create and configure private extensions for your own web app.</span></span> <span data-ttu-id="21729-122">Cette fonctionnalité repose également sur les déclarations XDT.</span><span class="sxs-lookup"><span data-stu-id="21729-122">This functionality also relies on XDT declarations.</span></span> <span data-ttu-id="21729-123">Les principales étapes de création d’une extension d’application web privée sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="21729-123">The key steps for creating a private web app extension are the following:</span></span>

1. <span data-ttu-id="21729-124">**Contenu**de l’extension d’application web : créez une application web prise en charge par App Service.</span><span class="sxs-lookup"><span data-stu-id="21729-124">Web app extension **content**: create any web application supported by App Service</span></span>
2. <span data-ttu-id="21729-125">**Déclaration**de l’extension d’application web : créez un fichier ApplicationHost.xdt.</span><span class="sxs-lookup"><span data-stu-id="21729-125">Web app extension **declaration**: create an ApplicationHost.xdt file</span></span>
3. <span data-ttu-id="21729-126">**Déploiement** de l’extension d’application web : placez le contenu dans le dossier SiteExtensions de `root`.</span><span class="sxs-lookup"><span data-stu-id="21729-126">Web app extension **deployment**: place content in the SiteExtensions folder under `root`</span></span>

<span data-ttu-id="21729-127">Les liens internes de l’application web doivent pointer vers un chemin d’accès relatif au chemin d’accès de l’application spécifié dans le fichier ApplicationHost.xdt.</span><span class="sxs-lookup"><span data-stu-id="21729-127">Internal links for the web app should point to a path relative to the application path specified in the ApplicationHost.xdt file.</span></span> <span data-ttu-id="21729-128">Toute modification apportée au fichier ApplicationHost.xdt requiert un recyclage de l’application web.</span><span class="sxs-lookup"><span data-stu-id="21729-128">Any change to the ApplicationHost.xdt file requires a web app recycle.</span></span>

<span data-ttu-id="21729-129">**Remarque**: des informations supplémentaires sur ces éléments clés sont disponibles sur [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span><span class="sxs-lookup"><span data-stu-id="21729-129">**Note**: Additional information for these key elements is available at [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span></span>

<span data-ttu-id="21729-130">Un exemple détaillé est inclus pour illustrer les étapes de création et d’activation d’une extension d’application web privée.</span><span class="sxs-lookup"><span data-stu-id="21729-130">A detailed example is included to illustrate the steps for creating and enabling a private web app extension.</span></span> <span data-ttu-id="21729-131">Le code source de l'exemple PHP Manager suivant peut être téléchargé sur [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span><span class="sxs-lookup"><span data-stu-id="21729-131">The source code for the PHP Manager example that follows can be downloaded from [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span></span>

### <span data-ttu-id="21729-132"><a id="SiteSample"></a> Exemple d’extension d’application web : PHP Manager</span><span class="sxs-lookup"><span data-stu-id="21729-132"><a id="SiteSample"></a> Web app extension example: PHP Manager</span></span>
<span data-ttu-id="21729-133">PHP Manager est une extension d’application web permettant aux administrateurs d’application web d’afficher et de configurer facilement leurs paramètres PHP au moyen d’une interface web plutôt que d’avoir à modifier les fichiers .ini PHP directement.</span><span class="sxs-lookup"><span data-stu-id="21729-133">PHP Manager is a web app extension that allows web app administrators to easily view and configure their PHP settings using a web interface instead of having to modify PHP .ini files directly.</span></span> <span data-ttu-id="21729-134">Les fichiers de configuration communs pour PHP incluent le fichier php.ini situé sous Program Files et le fichier .user.ini situé dans le dossier racine de votre application web.</span><span class="sxs-lookup"><span data-stu-id="21729-134">Common configuration files for PHP include the php.ini file located under Program Files and the .user.ini file located in the root folder of your web app.</span></span> <span data-ttu-id="21729-135">Étant donné que le fichier php.ini ne peut pas être modifié directement sur la plateforme App Service, l’extension PHP Manager utilise le fichier .user.ini pour appliquer les changements de paramètres.</span><span class="sxs-lookup"><span data-stu-id="21729-135">Since the php.ini file is not directly editable on the App Service platform, the PHP Manager extension uses the .user.ini file to apply setting changes.</span></span>

#### <span data-ttu-id="21729-136"><a id="PHPwebapp"></a> Application web PHP Manager</span><span class="sxs-lookup"><span data-stu-id="21729-136"><a id="PHPwebapp"></a> The PHP Manager web application</span></span>
<span data-ttu-id="21729-137">Ceci est la page d’accueil du déploiement PHP Manager :</span><span class="sxs-lookup"><span data-stu-id="21729-137">The following is the home page of the PHP Manager deployment:</span></span>

![TransformSitePHPUI][TransformSitePHPUI]

<span data-ttu-id="21729-139">Comme vous pouvez le voir, une extension d’application web est similaire à une application web standard, à la différence près qu’un fichier ApplicationHost.xdt supplémentaire se trouve dans le dossier racine de l’application web (des informations supplémentaires sur le fichier ApplicationHost.xdt sont disponibles dans la section suivante de cet article).</span><span class="sxs-lookup"><span data-stu-id="21729-139">As you can see, a web app extension is just like a regular web application, but with an additional ApplicationHost.xdt file placed in the root folder of the web app (more details about the ApplicationHost.xdt file are available in the next section of this article).</span></span>

<span data-ttu-id="21729-140">L'extension PHP Manager a été créée au moyen du modèle d'application Web ASP.NET MVC 4 Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="21729-140">The PHP Manager extension was created using the Visual Studio ASP.NET MVC 4 Web Application template.</span></span> <span data-ttu-id="21729-141">L’affichage suivant de l’Explorateur de solutions illustre la structure de l’extension PHP Manager.</span><span class="sxs-lookup"><span data-stu-id="21729-141">The following view from Solution Explorer shows the structure of the PHP Manager extension.</span></span>

![TransformSiteSolEx][TransformSiteSolEx]

<span data-ttu-id="21729-143">La seule logique spéciale requise pour l’E/S de fichier consiste à indiquer où se trouve le répertoire wwwroot de l’application web.</span><span class="sxs-lookup"><span data-stu-id="21729-143">The only special logic needed for file I/O is to indicate where the wwwroot directory of the web app is located.</span></span> <span data-ttu-id="21729-144">Comme illustré dans l’exemple de code suivant, la variable d’environnement « HOME » indique le chemin d’accès de la racine de l’application web, et le chemin d’accès wwwroot peut être construit en ajoutant « site\wwwroot » :</span><span class="sxs-lookup"><span data-stu-id="21729-144">As the following code example shows, the environment variable "HOME" indicates the web app's root path, and the wwwroot path can be constructed by appending "site\wwwroot":</span></span>

```csharp
/// <summary>
/// Gives the location of the .user.ini file, even if one doesn't exist yet
/// </summary>
private static string GetUserSettingsFilePath()
{
  var rootPath = Environment.GetEnvironmentVariable("HOME"); // For use on Azure Websites
  if (rootPath == null)
  {
    rootPath = System.IO.Path.GetTempPath(); // For testing purposes
  };
  var userSettingsFile = Path.Combine(rootPath, @"site\wwwroot\.user.ini");
  return userSettingsFile;
}
```


<span data-ttu-id="21729-145">Une fois que vous disposez du chemin d'accès au répertoire, vous pouvez utiliser des opérations d'E/S de fichier pour accéder en lecture et écriture aux fichiers.</span><span class="sxs-lookup"><span data-stu-id="21729-145">After you have the directory path, you can use regular file I/O operations to read and write to files.</span></span>

<span data-ttu-id="21729-146">Il convient d’exprimer un avertissement par rapport aux extensions d’application web et à la gestion des liens internes.</span><span class="sxs-lookup"><span data-stu-id="21729-146">One point of caution with web app extensions regards the handling of internal links.</span></span>  <span data-ttu-id="21729-147">Si vos fichiers HTML contiennent des liens fournissant des chemins d’accès absolus vers des liens internes de votre application web, vous devez vous assurer que ces liens sont précédés de votre nom d’extension en tant que racine de votre application.</span><span class="sxs-lookup"><span data-stu-id="21729-147">If you have any links in your HTML files that give absolute paths to internal links on your web app, you must ensure those links are prepended with your extension name as your root.</span></span> <span data-ttu-id="21729-148">Ceci est nécessaire car la racine du site de votre extension est à présent « /`[your-extension-name]`/ » et non simplement « / ». Tous les liens internes doivent donc être mis à jour en conséquence.</span><span class="sxs-lookup"><span data-stu-id="21729-148">This is needed because the root for your extension is now "/`[your-extension-name]`/" rather than being just "/", so any internal links must be updated accordingly.</span></span> <span data-ttu-id="21729-149">Par exemple, supposons que votre code inclut un lien vers ceci :</span><span class="sxs-lookup"><span data-stu-id="21729-149">For example, suppose your code includes a link to the following:</span></span>

`"<a href="/Home/Settings">PHP Settings</a>"`

<span data-ttu-id="21729-150">Lorsque le lien fait partie d’une extension d’application web, il doit se présenter sous la forme suivante :</span><span class="sxs-lookup"><span data-stu-id="21729-150">When the link is part of a web app extension, the link must be in the following form:</span></span>

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

<span data-ttu-id="21729-151">Vous pouvez contourner cette obligation en n’utilisant que des chemins d’accès relatifs dans votre application web ou, pour les applications ASP.NET, en utilisant la méthode `@Html.ActionLink` qui crée les liens appropriés pour vous.</span><span class="sxs-lookup"><span data-stu-id="21729-151">You can work around this requirement by either using only relative paths within your web application, or in the case of ASP.NET applications, by using the `@Html.ActionLink` method which creates the appropriate links for you.</span></span>

#### <span data-ttu-id="21729-152"><a id="XDT"></a> Fichier applicationHost.xdt</span><span class="sxs-lookup"><span data-stu-id="21729-152"><a id="XDT"></a> The applicationHost.xdt file</span></span>
<span data-ttu-id="21729-153">Le code de votre extension d’application web figure sous %HOME%\SiteExtensions\[nom-votre-extension].</span><span class="sxs-lookup"><span data-stu-id="21729-153">The code for your web app extension goes under %HOME%\SiteExtensions\[your-extension-name].</span></span> <span data-ttu-id="21729-154">Nous appellerons cela la racine d'extension.</span><span class="sxs-lookup"><span data-stu-id="21729-154">We'll call this the extension root.</span></span>  

<span data-ttu-id="21729-155">Pour inscrire votre extension d’application web dans le fichier applicationHost.config, vous devez placer un fichier intitulé ApplicationHost.xdt à la racine de l’extension.</span><span class="sxs-lookup"><span data-stu-id="21729-155">To register your web app extension with the applicationHost.config file, you need to place a file called ApplicationHost.xdt in the extension root.</span></span> <span data-ttu-id="21729-156">Le contenu du fichier ApplicationHost.xdt doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="21729-156">The content of the ApplicationHost.xdt file should be as follows:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.applicationHost>
    <sites>
      <site name="%XDT_SCMSITENAME%" xdt:Locator="Match(name)">
        <!-- NOTE: Add your extension name in the application paths below -->
        <application path="/[your-extension-name]" xdt:Locator="Match(path)" xdt:Transform="Remove" />
        <application path="/[your-extension-name]" applicationPool="%XDT_APPPOOLNAME%" xdt:Transform="Insert">
          <virtualDirectory path="/" physicalPath="%XDT_EXTENSIONPATH%" />
        </application>
      </site>
    </sites>
  </system.applicationHost>
</configuration>
```

<span data-ttu-id="21729-157">Le nom que vous sélectionnez comme nom de votre extension doit être identique au dossier racine de votre extension.</span><span class="sxs-lookup"><span data-stu-id="21729-157">The name you select as your extension name should have the same name as your extension root folder.</span></span>

<span data-ttu-id="21729-158">Cela a pour effet d’ajouter un nouveau chemin d’application dans la liste de sites `system.applicationHost` sous le site SCM.</span><span class="sxs-lookup"><span data-stu-id="21729-158">This has the effect of adding a new application path to the `system.applicationHost` sites list under the SCM site.</span></span> <span data-ttu-id="21729-159">Ce dernier représente un point de terminaison d'administration de site avec des informations d'identification d'accès spécifiques.</span><span class="sxs-lookup"><span data-stu-id="21729-159">The SCM site is a site administration end point with specific access credentials.</span></span> <span data-ttu-id="21729-160">Son URL est `https://[your-site-name].scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="21729-160">It has the URL `https://[your-site-name].scm.azurewebsites.net`.</span></span>  

```xml
<system.applicationHost>
  ...       
  <sites>
    <site name="~1[your-website]" id="1716402716">
      <bindings>
        <binding protocol="http" bindingInformation="*:80: [your-website].scm.azurewebsites.net" />
        <binding protocol="https" bindingInformation="*:443: [your-website].scm.azurewebsites.net" />
      </bindings>
      <traceFailedRequestsLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles" />
      <detailedErrorLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles\DetailedErrors" />
      <logFile logSiteId="false" />
      <application path="/" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="D:\Program Files (x86)\SiteExtensions\Kudu\1.24.20926.5" />
      </application>
      <!-- Note the custom changes that go here -->
      <application path="/[your-extension-name]" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\SiteExtensions\[your-extension-name]" />
      </application>
    </site>
  </sites>
  ... 
</system.applicationHost>
```

### <span data-ttu-id="21729-161"><a id="deploy"></a> Déploiement d’extension d’application web</span><span class="sxs-lookup"><span data-stu-id="21729-161"><a id="deploy"></a> Web app extension deployment</span></span>
<span data-ttu-id="21729-162">Pour installer l’extension de votre application web, vous pouvez copier par FTP tous les fichiers de votre application web dans le dossier `\SiteExtensions\[your-extension-name]` de l’application web où vous souhaitez installer l’extension.</span><span class="sxs-lookup"><span data-stu-id="21729-162">To install your web app extension, you can use FTP to copy all the files of your web application to the `\SiteExtensions\[your-extension-name]` folder of the web app on which you want to install the extension.</span></span>  <span data-ttu-id="21729-163">Veillez à copier le fichier ApplicationHost.xdt à cet emplacement également.</span><span class="sxs-lookup"><span data-stu-id="21729-163">Be sure to copy the ApplicationHost.xdt file to this location as well.</span></span> <span data-ttu-id="21729-164">Redémarrez votre application web pour activer l’extension.</span><span class="sxs-lookup"><span data-stu-id="21729-164">Restart your web app to enable the extension.</span></span>

<span data-ttu-id="21729-165">Vous devez être en mesure de voir l’extension de votre application web à l’adresse :</span><span class="sxs-lookup"><span data-stu-id="21729-165">You should be able to see your web app extension at:</span></span>

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

<span data-ttu-id="21729-166">Notez que l’URL ressemble en tous points à l’URL de votre application web, sauf qu’elle utilise HTTPS et contient « .scm ».</span><span class="sxs-lookup"><span data-stu-id="21729-166">Note that the URL looks just like the URL for your web app, except that it uses HTTPS and contains ".scm".</span></span>

<span data-ttu-id="21729-167">Il est possible de désactiver toutes les extensions privées (non préinstallées) de votre application web pendant le développement et les tests en ajoutant les paramètres de l’application avec la clé `WEBSITE_PRIVATE_EXTENSIONS` et la valeur `0`.</span><span class="sxs-lookup"><span data-stu-id="21729-167">It is possible to disable all private (not pre-installed) extensions for your web app during development and investigations by adding an app settings with the key `WEBSITE_PRIVATE_EXTENSIONS` and a value of `0`.</span></span>

> [!NOTE]
> <span data-ttu-id="21729-168">Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="21729-168">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="21729-169">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="21729-169">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="21729-170">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="21729-170">What's changed</span></span>
* <span data-ttu-id="21729-171">Pour obtenir un guide présentant les modifications apportées dans le cadre de la transition entre Sites Web et App Service, consultez la page [Azure App Service et les services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="21729-171">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

