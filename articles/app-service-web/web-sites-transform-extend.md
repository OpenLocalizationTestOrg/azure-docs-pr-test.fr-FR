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
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a>Configuration avancée et extensions des applications web Azure App Service
À l’aide de [Transformation du Document XML](http://msdn.microsoft.com/library/dd465326.aspx) les déclarations (XDT), vous pouvez transformer hello [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) fichier dans votre application web dans Azure App Service. Vous pouvez également utiliser des actions administration des applications web personnalisées tooenable XDT déclarations tooadd extensions privées. Le présent article inclut un exemple d’extension d’application web PHP Manager, qui permet de gérer les paramètres PHP par le biais d’une interface web.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="transform"></a>Configuration avancée via ApplicationHost.config
Hello plateforme de Service d’applications fournit la flexibilité et contrôle pour la configuration d’application web. Bien que le fichier de configuration IIS ApplicationHost.config hello standard n’est pas disponible pour la modification directe dans le Service d’applications, hello prend en charge un modèle de transformation ApplicationHost.config déclaratif basé sur XML Document Transformation (XDT).

tooleverage cette fonctionnalité de transformation, vous créez un fichier ApplicationHost.xdt avec XDT contenu et placer sous la racine du site (d:\home\site) hello Bonjour [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console). Vous devrez peut-être toorestart hello Web App pour effet de tootake de modifications.

Hello suivant applicationHost.xdt exemple montre comment tooadd un tooa de variable d’environnement personnalisé nouveau web application qui utilise PHP 5.4.

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

Un fichier journal avec le statut de la transformation et de détails est disponible à partir de la racine de hello FTP LogFiles\Transform.

Pour d’autres exemples, consultez la page [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).

**Remarque :**<br />
Éléments de liste de hello des modules sous `system.webServer` ne peut pas être supprimés ou réorganisés, mais la liste des ajouts toohello sont possibles.

## <a id="extend"></a> Étendre votre application web
### <a id="overview"></a> Vue d’ensemble des extensions privées d’application web
App Service prend en charge les extensions d’application web comme point d’extensibilité des actions d’administration. En fait, certaines fonctionnalités de la plateforme App Service sont implémentées en tant qu’extensions préinstallées. Alors que les extensions de la plate-forme préinstallées hello ne peut pas être modifiées, vous pouvez créer et configurer les extensions privées pour votre application web. Cette fonctionnalité repose également sur les déclarations XDT. Hello principales étapes de création d’une extension d’application web privés sont les suivants de hello :

1. **Contenu**de l’extension d’application web : créez une application web prise en charge par App Service.
2. **Déclaration**de l’extension d’application web : créez un fichier ApplicationHost.xdt.
3. Extension de l’application Web **déploiement**: placer le contenu dans le dossier de SiteExtensions hello sous`root`

Les liens internes pour l’application web de hello doivent pointer tooa chemin d’accès relatif toohello application chemin d’accès spécifié dans le fichier de ApplicationHost.xdt hello. N’importe quel fichier de ApplicationHost.xdt toohello modification requiert un recyclage d’application web.

**Remarque**: des informations supplémentaires sur ces éléments clés sont disponibles sur [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).

Un exemple détaillé est étapes de hello tooillustrate inclus pour la création et l’activation d’une extension d’application web privée. code source pour un exemple de gestionnaire PHP hello qui suit peut être téléchargé à partir de Hello [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).

### <a id="SiteSample"></a> Exemple d’extension d’application web : PHP Manager
PHP Manager est une extension d’application web qui autorise les administrateurs d’application web tooeasily afficher et configurer leurs paramètres de PHP à l’aide d’une interface web au lieu d’avoir des fichiers .ini PHP toomodify directement. Les fichiers de configuration courants pour PHP incluent le fichier php.ini de hello situé sous Program Files et hello. fichier user.ini situé dans le dossier racine de hello de votre application web. Étant donné que le fichier php.ini de hello n’est pas directement modifiable sur hello plateforme de Service d’application, hello extension PHP Manager utilise hello. tooapply de fichier user.ini modifications apportées au paramètre.

#### <a id="PHPwebapp"></a>Hello application web PHP Manager
Hello Voici la page d’accueil hello Hello déploiement du Gestionnaire de PHP :

![TransformSitePHPUI][TransformSitePHPUI]

Comme vous pouvez le voir, une extension d’application web est comme une application web standard, mais avec un autre fichier ApplicationHost.xdt placé dans le dossier racine de hello de hello web app (plus de détails sur le fichier de ApplicationHost.xdt hello sont disponibles dans la section suivante de hello de ce article).

Hello extension PHP Manager a été créé à l’aide du modèle d’Application de Web Visual Studio ASP.NET MVC 4 hello. Hello suivantes à partir de l’Explorateur de solutions affiche structure hello Hello extension du Gestionnaire de PHP.

![TransformSiteSolEx][TransformSiteSolEx]

Bonjour uniquement une logique spéciale nécessaire pour le fichier d’e/s est tooindicate où hello répertoire wwwroot de l’application hello web se trouve. Comme le montre le code exemple suivant, hello hello environnement variable « HOME » indique hello du chemin d’accès racine de l’application web, et le chemin d’accès de hello wwwroot peut être construit en ajoutant « site\wwwroot » :

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


Une fois que vous avez le chemin d’accès du répertoire hello, vous pouvez utiliser des tooread des opérations d’e/s de fichier normal et écrire toofiles.

Un point de précautions avec les extensions d’application web ce qui concerne la gestion de hello des liens internes.  Si vous avez des liens dans vos fichiers HTML qui fournissent des chemins d’accès absolus toointernal liens sur votre application web, vous devez vérifier que ces liens sont précédées du nom de votre extension en tant que racine de votre. Cela est nécessaire car la racine hello pour votre extension est désormais « /`[your-extension-name]`/ » au lieu d’être simplement « / », par conséquent, toute internes liens doivent être mis à jour en conséquence. Par exemple, supposons que votre code inclut une suivant toohello de lien :

`"<a href="/Home/Settings">PHP Settings</a>"`

Lorsque le lien de hello fait partie d’une extension d’application web, lien de hello doit être Bonjour suivant du formulaire :

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

Vous pouvez contourner cette exigence en utilisant uniquement des chemins d’accès relatifs au sein de votre application web, ou dans hello cas des applications ASP.NET, à l’aide de hello `@Html.ActionLink` méthode qui crée les liens appropriés hello pour vous.

#### <a id="XDT"></a>fichier de applicationHost.xdt Hello
code Hello pour votre extension d’application web est mis sous %HOME%\SiteExtensions\[votre extension-name]. Nous vous appellerons pour cette racine d’extension hello.  

tooregister votre extension d’application web avec le fichier applicationHost.config de hello, vous devez tooplace un fichier appelé ApplicationHost.xdt dans la racine d’extension hello. Hello contenu du fichier de ApplicationHost.xdt hello doit être comme suit :

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

vous sélectionnez en tant que nom de votre extension de nom de Hello doit avoir hello même nom que votre dossier racine d’extension.

Cela a pour effet de hello d’ajout d’un nouveau toohello de chemin d’accès application `system.applicationHost` liste des sites sous le site SCM hello. site SCM Hello est un point de terminaison de site administration avec les informations d’identification d’accès spécifiques. Il a hello URL `https://[your-site-name].scm.azurewebsites.net`.  

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

### <a id="deploy"></a> Déploiement d’extension d’application web
tooinstall votre extension d’application web, vous pouvez utiliser FTP toocopy tous les fichiers hello de votre toohello d’application web `\SiteExtensions\[your-extension-name]` dossier de l’application hello web sur lequel vous souhaitez l’extension de hello tooinstall.  Être vraiment toocopy hello ApplicationHost.xdt toothis emplacement du fichier ainsi. Redémarrez votre extension d’hello tooenable application web.

Vous devez être en mesure de toosee votre extension d’application web à :

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

Notez que hello QU'URL ressemble à hello URL pour votre application web, sauf qu’elle utilise le protocole HTTPS contient « .scm ».

Extensions privées de toodisable possibles (ne pas préinstallé) pour votre application web est pendant le développement et aux enquêtes en ajoutant des paramètres de l’application avec la clé de hello `WEBSITE_PRIVATE_EXTENSIONS` et la valeur `0`.

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

