---
title: "aaaAzure application web App Service Configuration avancée et extensions"
description: "Utilisez Transformation(XDT) du Document XML déclarations tootransform hello le fichier ApplicationHost.config dans vos Azure App Service web app et tooadd extensions privées tooenable administration personnalisées actions."
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
ms.openlocfilehash: 873347ac13113d1ac989cba29128382c81dcfcca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a><span data-ttu-id="d8556-103">Configuration avancée et extensions des applications web Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d8556-103">Azure App Service web app advanced config and extensions</span></span>
<span data-ttu-id="d8556-104">À l’aide de [Transformation du Document XML](http://msdn.microsoft.com/library/dd465326.aspx) les déclarations (XDT), vous pouvez transformer hello [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) fichier dans votre application web dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="d8556-104">By using [XML Document Transformation](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) declarations, you can transform hello [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) file in your web app in Azure App Service.</span></span> <span data-ttu-id="d8556-105">Vous pouvez également utiliser des actions administration des applications web personnalisées tooenable XDT déclarations tooadd extensions privées.</span><span class="sxs-lookup"><span data-stu-id="d8556-105">You can also use XDT declarations tooadd private extensions tooenable custom web app administration actions.</span></span> <span data-ttu-id="d8556-106">Le présent article inclut un exemple d’extension d’application web PHP Manager, qui permet de gérer les paramètres PHP par le biais d’une interface web.</span><span class="sxs-lookup"><span data-stu-id="d8556-106">This article includes a sample PHP Manager web app extension that enables management of PHP settings through a web interface.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="d8556-107"><a id="transform"></a>Configuration avancée via ApplicationHost.config</span><span class="sxs-lookup"><span data-stu-id="d8556-107"><a id="transform"></a>Advanced configuration through ApplicationHost.config</span></span>
<span data-ttu-id="d8556-108">Hello plateforme de Service d’applications fournit la flexibilité et contrôle pour la configuration d’application web.</span><span class="sxs-lookup"><span data-stu-id="d8556-108">hello App Service platform provides flexibility and control for web app configuration.</span></span> <span data-ttu-id="d8556-109">Bien que le fichier de configuration IIS ApplicationHost.config hello standard n’est pas disponible pour la modification directe dans le Service d’applications, hello prend en charge un modèle de transformation ApplicationHost.config déclaratif basé sur XML Document Transformation (XDT).</span><span class="sxs-lookup"><span data-stu-id="d8556-109">Although hello standard IIS ApplicationHost.config configuration file is not available for direct editing in App Service, hello platform supports a declarative ApplicationHost.config transform model based on XML Document Transformation (XDT).</span></span>

<span data-ttu-id="d8556-110">tooleverage cette fonctionnalité de transformation, vous créez un fichier ApplicationHost.xdt avec XDT contenu et placer sous la racine du site (d:\home\site) hello Bonjour [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span><span class="sxs-lookup"><span data-stu-id="d8556-110">tooleverage this transform functionality, you create an ApplicationHost.xdt file with XDT content and place under hello site root (d:\home\site) in hello [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span></span> <span data-ttu-id="d8556-111">Vous devrez peut-être toorestart hello Web App pour effet de tootake de modifications.</span><span class="sxs-lookup"><span data-stu-id="d8556-111">You may need toorestart hello Web App for changes tootake effect.</span></span>

<span data-ttu-id="d8556-112">Hello suivant applicationHost.xdt exemple montre comment tooadd un tooa de variable d’environnement personnalisé nouveau web application qui utilise PHP 5.4.</span><span class="sxs-lookup"><span data-stu-id="d8556-112">hello following applicationHost.xdt sample shows how tooadd a new custom environment variable tooa web app that uses PHP 5.4.</span></span>

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

<span data-ttu-id="d8556-113">Un fichier journal avec le statut de la transformation et de détails est disponible à partir de la racine de hello FTP LogFiles\Transform.</span><span class="sxs-lookup"><span data-stu-id="d8556-113">A log file with transform status and details is available from hello FTP root under LogFiles\Transform.</span></span>

<span data-ttu-id="d8556-114">Pour d’autres exemples, consultez la page [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span><span class="sxs-lookup"><span data-stu-id="d8556-114">For additional samples, see [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span></span>

<span data-ttu-id="d8556-115">**Remarque :**</span><span class="sxs-lookup"><span data-stu-id="d8556-115">**Note**</span></span><br />
<span data-ttu-id="d8556-116">Éléments de liste de hello des modules sous `system.webServer` ne peut pas être supprimés ou réorganisés, mais la liste des ajouts toohello sont possibles.</span><span class="sxs-lookup"><span data-stu-id="d8556-116">Elements from hello list of modules under `system.webServer` cannot be removed or reordered, but additions toohello list are possible.</span></span>

## <span data-ttu-id="d8556-117"><a id="extend"></a> Étendre votre application web</span><span class="sxs-lookup"><span data-stu-id="d8556-117"><a id="extend"></a> Extend your web app</span></span>
### <span data-ttu-id="d8556-118"><a id="overview"></a> Vue d’ensemble des extensions privées d’application web</span><span class="sxs-lookup"><span data-stu-id="d8556-118"><a id="overview"></a> Overview of private web app extensions</span></span>
<span data-ttu-id="d8556-119">App Service prend en charge les extensions d’application web comme point d’extensibilité des actions d’administration.</span><span class="sxs-lookup"><span data-stu-id="d8556-119">App Service supports web app extensions as an extensibility point for administrative actions.</span></span> <span data-ttu-id="d8556-120">En fait, certaines fonctionnalités de la plateforme App Service sont implémentées en tant qu’extensions préinstallées.</span><span class="sxs-lookup"><span data-stu-id="d8556-120">In fact, some App Service platform features are implemented as pre-installed extensions.</span></span> <span data-ttu-id="d8556-121">Alors que les extensions de la plate-forme préinstallées hello ne peut pas être modifiées, vous pouvez créer et configurer les extensions privées pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="d8556-121">While hello pre-installed platform extensions cannot be modified, you can create and configure private extensions for your own web app.</span></span> <span data-ttu-id="d8556-122">Cette fonctionnalité repose également sur les déclarations XDT.</span><span class="sxs-lookup"><span data-stu-id="d8556-122">This functionality also relies on XDT declarations.</span></span> <span data-ttu-id="d8556-123">Hello principales étapes de création d’une extension d’application web privés sont les suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="d8556-123">hello key steps for creating a private web app extension are hello following:</span></span>

1. <span data-ttu-id="d8556-124">**Contenu**de l’extension d’application web : créez une application web prise en charge par App Service.</span><span class="sxs-lookup"><span data-stu-id="d8556-124">Web app extension **content**: create any web application supported by App Service</span></span>
2. <span data-ttu-id="d8556-125">**Déclaration**de l’extension d’application web : créez un fichier ApplicationHost.xdt.</span><span class="sxs-lookup"><span data-stu-id="d8556-125">Web app extension **declaration**: create an ApplicationHost.xdt file</span></span>
3. <span data-ttu-id="d8556-126">Extension de l’application Web **déploiement**: placer le contenu dans le dossier de SiteExtensions hello sous`root`</span><span class="sxs-lookup"><span data-stu-id="d8556-126">Web app extension **deployment**: place content in hello SiteExtensions folder under `root`</span></span>

<span data-ttu-id="d8556-127">Les liens internes pour l’application web de hello doivent pointer tooa chemin d’accès relatif toohello application chemin d’accès spécifié dans le fichier de ApplicationHost.xdt hello.</span><span class="sxs-lookup"><span data-stu-id="d8556-127">Internal links for hello web app should point tooa path relative toohello application path specified in hello ApplicationHost.xdt file.</span></span> <span data-ttu-id="d8556-128">N’importe quel fichier de ApplicationHost.xdt toohello modification requiert un recyclage d’application web.</span><span class="sxs-lookup"><span data-stu-id="d8556-128">Any change toohello ApplicationHost.xdt file requires a web app recycle.</span></span>

<span data-ttu-id="d8556-129">**Remarque**: des informations supplémentaires sur ces éléments clés sont disponibles sur [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span><span class="sxs-lookup"><span data-stu-id="d8556-129">**Note**: Additional information for these key elements is available at [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span></span>

<span data-ttu-id="d8556-130">Un exemple détaillé est étapes de hello tooillustrate inclus pour la création et l’activation d’une extension d’application web privée.</span><span class="sxs-lookup"><span data-stu-id="d8556-130">A detailed example is included tooillustrate hello steps for creating and enabling a private web app extension.</span></span> <span data-ttu-id="d8556-131">code source pour un exemple de gestionnaire PHP hello qui suit peut être téléchargé à partir de Hello [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span><span class="sxs-lookup"><span data-stu-id="d8556-131">hello source code for hello PHP Manager example that follows can be downloaded from [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span></span>

### <span data-ttu-id="d8556-132"><a id="SiteSample"></a> Exemple d’extension d’application web : PHP Manager</span><span class="sxs-lookup"><span data-stu-id="d8556-132"><a id="SiteSample"></a> Web app extension example: PHP Manager</span></span>
<span data-ttu-id="d8556-133">PHP Manager est une extension d’application web qui autorise les administrateurs d’application web tooeasily afficher et configurer leurs paramètres de PHP à l’aide d’une interface web au lieu d’avoir des fichiers .ini PHP toomodify directement.</span><span class="sxs-lookup"><span data-stu-id="d8556-133">PHP Manager is a web app extension that allows web app administrators tooeasily view and configure their PHP settings using a web interface instead of having toomodify PHP .ini files directly.</span></span> <span data-ttu-id="d8556-134">Les fichiers de configuration courants pour PHP incluent le fichier php.ini de hello situé sous Program Files et hello. fichier user.ini situé dans le dossier racine de hello de votre application web.</span><span class="sxs-lookup"><span data-stu-id="d8556-134">Common configuration files for PHP include hello php.ini file located under Program Files and hello .user.ini file located in hello root folder of your web app.</span></span> <span data-ttu-id="d8556-135">Étant donné que le fichier php.ini de hello n’est pas directement modifiable sur hello plateforme de Service d’application, hello extension PHP Manager utilise hello. tooapply de fichier user.ini modifications apportées au paramètre.</span><span class="sxs-lookup"><span data-stu-id="d8556-135">Since hello php.ini file is not directly editable on hello App Service platform, hello PHP Manager extension uses hello .user.ini file tooapply setting changes.</span></span>

#### <span data-ttu-id="d8556-136"><a id="PHPwebapp"></a>Hello application web PHP Manager</span><span class="sxs-lookup"><span data-stu-id="d8556-136"><a id="PHPwebapp"></a> hello PHP Manager web application</span></span>
<span data-ttu-id="d8556-137">Hello Voici la page d’accueil hello Hello déploiement du Gestionnaire de PHP :</span><span class="sxs-lookup"><span data-stu-id="d8556-137">hello following is hello home page of hello PHP Manager deployment:</span></span>

![TransformSitePHPUI][TransformSitePHPUI]

<span data-ttu-id="d8556-139">Comme vous pouvez le voir, une extension d’application web est comme une application web standard, mais avec un autre fichier ApplicationHost.xdt placé dans le dossier racine de hello de hello web app (plus de détails sur le fichier de ApplicationHost.xdt hello sont disponibles dans la section suivante de hello de ce article).</span><span class="sxs-lookup"><span data-stu-id="d8556-139">As you can see, a web app extension is just like a regular web application, but with an additional ApplicationHost.xdt file placed in hello root folder of hello web app (more details about hello ApplicationHost.xdt file are available in hello next section of this article).</span></span>

<span data-ttu-id="d8556-140">Hello extension PHP Manager a été créé à l’aide du modèle d’Application de Web Visual Studio ASP.NET MVC 4 hello.</span><span class="sxs-lookup"><span data-stu-id="d8556-140">hello PHP Manager extension was created using hello Visual Studio ASP.NET MVC 4 Web Application template.</span></span> <span data-ttu-id="d8556-141">Hello suivantes à partir de l’Explorateur de solutions affiche structure hello Hello extension du Gestionnaire de PHP.</span><span class="sxs-lookup"><span data-stu-id="d8556-141">hello following view from Solution Explorer shows hello structure of hello PHP Manager extension.</span></span>

![TransformSiteSolEx][TransformSiteSolEx]

<span data-ttu-id="d8556-143">Bonjour uniquement une logique spéciale nécessaire pour le fichier d’e/s est tooindicate où hello répertoire wwwroot de l’application hello web se trouve.</span><span class="sxs-lookup"><span data-stu-id="d8556-143">hello only special logic needed for file I/O is tooindicate where hello wwwroot directory of hello web app is located.</span></span> <span data-ttu-id="d8556-144">Comme le montre le code exemple suivant, hello hello environnement variable « HOME » indique hello du chemin d’accès racine de l’application web, et le chemin d’accès de hello wwwroot peut être construit en ajoutant « site\wwwroot » :</span><span class="sxs-lookup"><span data-stu-id="d8556-144">As hello following code example shows, hello environment variable "HOME" indicates hello web app's root path, and hello wwwroot path can be constructed by appending "site\wwwroot":</span></span>

```csharp
/// <summary>
/// Gives hello location of hello .user.ini file, even if one doesn't exist yet
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


<span data-ttu-id="d8556-145">Une fois que vous avez le chemin d’accès du répertoire hello, vous pouvez utiliser des tooread des opérations d’e/s de fichier normal et écrire toofiles.</span><span class="sxs-lookup"><span data-stu-id="d8556-145">After you have hello directory path, you can use regular file I/O operations tooread and write toofiles.</span></span>

<span data-ttu-id="d8556-146">Un point de précautions avec les extensions d’application web ce qui concerne la gestion de hello des liens internes.</span><span class="sxs-lookup"><span data-stu-id="d8556-146">One point of caution with web app extensions regards hello handling of internal links.</span></span>  <span data-ttu-id="d8556-147">Si vous avez des liens dans vos fichiers HTML qui fournissent des chemins d’accès absolus toointernal liens sur votre application web, vous devez vérifier que ces liens sont précédées du nom de votre extension en tant que racine de votre.</span><span class="sxs-lookup"><span data-stu-id="d8556-147">If you have any links in your HTML files that give absolute paths toointernal links on your web app, you must ensure those links are prepended with your extension name as your root.</span></span> <span data-ttu-id="d8556-148">Cela est nécessaire car la racine hello pour votre extension est désormais « /`[your-extension-name]`/ » au lieu d’être simplement « / », par conséquent, toute internes liens doivent être mis à jour en conséquence.</span><span class="sxs-lookup"><span data-stu-id="d8556-148">This is needed because hello root for your extension is now "/`[your-extension-name]`/" rather than being just "/", so any internal links must be updated accordingly.</span></span> <span data-ttu-id="d8556-149">Par exemple, supposons que votre code inclut une suivant toohello de lien :</span><span class="sxs-lookup"><span data-stu-id="d8556-149">For example, suppose your code includes a link toohello following:</span></span>

`"<a href="/Home/Settings">PHP Settings</a>"`

<span data-ttu-id="d8556-150">Lorsque le lien de hello fait partie d’une extension d’application web, lien de hello doit être Bonjour suivant du formulaire :</span><span class="sxs-lookup"><span data-stu-id="d8556-150">When hello link is part of a web app extension, hello link must be in hello following form:</span></span>

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

<span data-ttu-id="d8556-151">Vous pouvez contourner cette exigence en utilisant uniquement des chemins d’accès relatifs au sein de votre application web, ou dans hello cas des applications ASP.NET, à l’aide de hello `@Html.ActionLink` méthode qui crée les liens appropriés hello pour vous.</span><span class="sxs-lookup"><span data-stu-id="d8556-151">You can work around this requirement by either using only relative paths within your web application, or in hello case of ASP.NET applications, by using hello `@Html.ActionLink` method which creates hello appropriate links for you.</span></span>

#### <span data-ttu-id="d8556-152"><a id="XDT"></a>fichier de applicationHost.xdt Hello</span><span class="sxs-lookup"><span data-stu-id="d8556-152"><a id="XDT"></a> hello applicationHost.xdt file</span></span>
<span data-ttu-id="d8556-153">code Hello pour votre extension d’application web est mis sous %HOME%\SiteExtensions\[votre extension-name].</span><span class="sxs-lookup"><span data-stu-id="d8556-153">hello code for your web app extension goes under %HOME%\SiteExtensions\[your-extension-name].</span></span> <span data-ttu-id="d8556-154">Nous vous appellerons pour cette racine d’extension hello.</span><span class="sxs-lookup"><span data-stu-id="d8556-154">We'll call this hello extension root.</span></span>  

<span data-ttu-id="d8556-155">tooregister votre extension d’application web avec le fichier applicationHost.config de hello, vous devez tooplace un fichier appelé ApplicationHost.xdt dans la racine d’extension hello.</span><span class="sxs-lookup"><span data-stu-id="d8556-155">tooregister your web app extension with hello applicationHost.config file, you need tooplace a file called ApplicationHost.xdt in hello extension root.</span></span> <span data-ttu-id="d8556-156">Hello contenu du fichier de ApplicationHost.xdt hello doit être comme suit :</span><span class="sxs-lookup"><span data-stu-id="d8556-156">hello content of hello ApplicationHost.xdt file should be as follows:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.applicationHost>
    <sites>
      <site name="%XDT_SCMSITENAME%" xdt:Locator="Match(name)">
        <!-- NOTE: Add your extension name in hello application paths below -->
        <application path="/[your-extension-name]" xdt:Locator="Match(path)" xdt:Transform="Remove" />
        <application path="/[your-extension-name]" applicationPool="%XDT_APPPOOLNAME%" xdt:Transform="Insert">
          <virtualDirectory path="/" physicalPath="%XDT_EXTENSIONPATH%" />
        </application>
      </site>
    </sites>
  </system.applicationHost>
</configuration>
```

<span data-ttu-id="d8556-157">vous sélectionnez en tant que nom de votre extension de nom de Hello doit avoir hello même nom que votre dossier racine d’extension.</span><span class="sxs-lookup"><span data-stu-id="d8556-157">hello name you select as your extension name should have hello same name as your extension root folder.</span></span>

<span data-ttu-id="d8556-158">Cela a pour effet de hello d’ajout d’un nouveau toohello de chemin d’accès application `system.applicationHost` liste des sites sous le site SCM hello.</span><span class="sxs-lookup"><span data-stu-id="d8556-158">This has hello effect of adding a new application path toohello `system.applicationHost` sites list under hello SCM site.</span></span> <span data-ttu-id="d8556-159">site SCM Hello est un point de terminaison de site administration avec les informations d’identification d’accès spécifiques.</span><span class="sxs-lookup"><span data-stu-id="d8556-159">hello SCM site is a site administration end point with specific access credentials.</span></span> <span data-ttu-id="d8556-160">Il a hello URL `https://[your-site-name].scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="d8556-160">It has hello URL `https://[your-site-name].scm.azurewebsites.net`.</span></span>  

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
      <!-- Note hello custom changes that go here -->
      <application path="/[your-extension-name]" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\SiteExtensions\[your-extension-name]" />
      </application>
    </site>
  </sites>
  ... 
</system.applicationHost>
```

### <span data-ttu-id="d8556-161"><a id="deploy"></a> Déploiement d’extension d’application web</span><span class="sxs-lookup"><span data-stu-id="d8556-161"><a id="deploy"></a> Web app extension deployment</span></span>
<span data-ttu-id="d8556-162">tooinstall votre extension d’application web, vous pouvez utiliser FTP toocopy tous les fichiers hello de votre toohello d’application web `\SiteExtensions\[your-extension-name]` dossier de l’application hello web sur lequel vous souhaitez l’extension de hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="d8556-162">tooinstall your web app extension, you can use FTP toocopy all hello files of your web application toohello `\SiteExtensions\[your-extension-name]` folder of hello web app on which you want tooinstall hello extension.</span></span>  <span data-ttu-id="d8556-163">Être vraiment toocopy hello ApplicationHost.xdt toothis emplacement du fichier ainsi.</span><span class="sxs-lookup"><span data-stu-id="d8556-163">Be sure toocopy hello ApplicationHost.xdt file toothis location as well.</span></span> <span data-ttu-id="d8556-164">Redémarrez votre extension d’hello tooenable application web.</span><span class="sxs-lookup"><span data-stu-id="d8556-164">Restart your web app tooenable hello extension.</span></span>

<span data-ttu-id="d8556-165">Vous devez être en mesure de toosee votre extension d’application web à :</span><span class="sxs-lookup"><span data-stu-id="d8556-165">You should be able toosee your web app extension at:</span></span>

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

<span data-ttu-id="d8556-166">Notez que hello QU'URL ressemble à hello URL pour votre application web, sauf qu’elle utilise le protocole HTTPS contient « .scm ».</span><span class="sxs-lookup"><span data-stu-id="d8556-166">Note that hello URL looks just like hello URL for your web app, except that it uses HTTPS and contains ".scm".</span></span>

<span data-ttu-id="d8556-167">Extensions privées de toodisable possibles (ne pas préinstallé) pour votre application web est pendant le développement et aux enquêtes en ajoutant des paramètres de l’application avec la clé de hello `WEBSITE_PRIVATE_EXTENSIONS` et la valeur `0`.</span><span class="sxs-lookup"><span data-stu-id="d8556-167">It is possible toodisable all private (not pre-installed) extensions for your web app during development and investigations by adding an app settings with hello key `WEBSITE_PRIVATE_EXTENSIONS` and a value of `0`.</span></span>

> [!NOTE]
> <span data-ttu-id="d8556-168">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="d8556-168">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d8556-169">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="d8556-169">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="d8556-170">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="d8556-170">What's changed</span></span>
* <span data-ttu-id="d8556-171">Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="d8556-171">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

