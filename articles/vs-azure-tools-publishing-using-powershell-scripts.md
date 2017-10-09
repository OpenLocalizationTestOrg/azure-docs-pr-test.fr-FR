---
title: aaaUsing les environnements de Test et les Scripts Windows PowerShell tooPublish tooDev | Documents Microsoft
description: "Découvrez comment toouse Windows PowerShell scripts à partir d’environnements de test et de toodevelopment de toopublish de Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5fff1301-5469-4d97-be88-c85c30f837c1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 491a058f96255576afa74f6156f20ae9559bb9f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-powershell-scripts-toopublish-toodev-and-test-environments"></a>À l’aide de Windows PowerShell scripts des environnements de test et de toodev de toopublish
Lorsque vous créez une application web dans Visual Studio, vous pouvez générer un script Windows PowerShell que vous pouvez utiliser la publication hello tooautomate ultérieure de tooAzure de votre site Web comme une application Web dans Azure App Service ou une machine virtuelle. Vous pouvez modifier et étendre des besoins de votre script Windows PowerShell de hello dans toosuit de l’éditeur Visual Studio hello ou intégrer le script de hello avec la build existante, de test et des scripts de publication.

À l’aide de ces scripts, vous pouvez configurer des versions personnalisées (également connues comme environnements de développement et de test) de votre site pour une utilisation temporaire. Par exemple, vous pourrez configurer une version particulière de votre site Web sur une machine virtuelle Azure ou sur hello staging emplacement sur un site Web de toorun une suite de tests, reproduire un bogue, tester un correctif, évaluer une proposition de modification ou configurer un environnement personnalisé pour une démonstration ou une présentation. Une fois que vous avez créé un script qui publie votre projet, vous pouvez recréer des environnements identiques en réexécutant le script de hello en fonction des besoins, ou exécuter les script hello avec votre propre build de votre toocreate d’application web un environnement personnalisé pour le test.

## <a name="what-you-need"></a>Ce dont vous avez besoin
* Kit de développement logiciel (SDK) Azure 2.3 ou version ultérieure. Pour plus d’informations, consultez [Téléchargements Visual Studio](http://go.microsoft.com/fwlink/?LinkID=624384) .

Vous n’avez pas besoin de hello Azure SDK toogenerate hello des scripts pour les projets web. Cette fonctionnalité s’adresse aux projets web, et non aux rôles web dans les services cloud.

* Azure PowerShell 0.7.4 ou version ultérieure. Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations.
* [Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) ou version ultérieure.

## <a name="additional-tools"></a>Outils supplémentaires
Des outils et ressources supplémentaires sont disponibles pour l’utilisation de PowerShell dans Visual Studio pour le développement Azure. Consultez [Outils PowerShell pour Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).

## <a name="generating-hello-publish-scripts"></a>Génération de hello publier des scripts
Vous pouvez générer hello publier des scripts pour une machine virtuelle qui héberge votre site Web lorsque vous créez un nouveau projet en suivant [ces instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Vous pouvez également [Générer des scripts de publication pour les applications web dans Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).

## <a name="scripts-that-visual-studio-generates"></a>Scripts générés par Visual Studio
Visual Studio génère un dossier au niveau solution appelé **PublishScripts** qui contient deux fichiers de Windows PowerShell, un script de publication pour votre machine virtuelle ou site Web et un module qui contient les fonctions que vous pouvez utiliser Bonjour scripts. Visual Studio génère également un fichier au format JSON hello qui spécifie les détails de hello de projet que vous déployez hello.

### <a name="windows-powershell-publish-script"></a>Script de publication Windows PowerShell
Hello du script de publication contient des étapes de déploiement d’ordinateur virtuel ou le site Web de tooa de publication. Visual Studio propose la coloration de syntaxe pour le développement de Windows PowerShell. Aide pour les fonctions hello est disponible, et vous pouvez modifier librement les fonctions hello dans hello script toosuit vos besoins.

### <a name="windows-powershell-module"></a>Module Windows PowerShell
Hello Windows PowerShell module généré par Visual Studio contient les fonctions hello publier utilise de script. Ces sont des fonctions Azure PowerShell et ne sont pas prévu toobe modifié. Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations.

### <a name="json-configuration-file"></a>Fichier de configuration JSON
fichier JSON de Hello est créé dans hello **Configurations** dossier et contient des données de configuration qui spécifie exactement le tooAzure toodeploy de ressources. nom de Hello du fichier hello généré par Visual Studio est projet-nom-WAWS-dev.JSON si vous avez créé un site Web ou un projet nom-VM-dev.JSON si vous avez créé une machine virtuelle. Voici un exemple de fichier de configuration JSON généré lorsque vous créez un site web. La plupart des valeurs de hello est explicite. nom du site Web Hello est généré par Azure, qui peut correspondre pas à votre nom de projet.

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```
Lorsque vous créez une machine virtuelle, fichier de configuration JSON hello recherche similaire toohello suivant. Notez qu’un service cloud est créé en tant que conteneur pour la machine virtuelle de hello. machine virtuelle de Hello contient des points de terminaison habituels hello pour l’accès web via HTTP et HTTPS, ainsi que les points de terminaison pour Web Deploy, qui vous permet de publier le site Web de toohello à partir de votre ordinateur local, Bureau à distance et Windows PowerShell.

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

Vous pouvez modifier hello JSON configuration toochange que se passe-t-il lorsque vous exécutez hello publier des scripts. Hello `cloudService` et `virtualMachine` sections sont requises, mais vous pouvez supprimer hello `databases` section si vous n’avez pas besoin. propriétés Hello vides dans le fichier de configuration par défaut hello généré par Visual Studio sont facultatifs ; ceux qui ont des valeurs dans le fichier de configuration par défaut hello sont requis.

Si vous avez un site Web qui a plusieurs environnements de déploiement (ou emplacements) plutôt qu’un site de production unique dans Azure, vous pouvez inclure le nom d’emplacement hello dans nom hello du site Web de hello dans le fichier de configuration JSON hello. Par exemple, si vous avez un site Web nommé **monsite** et un emplacement correspondant se nomme **test** hello URI est monsite-test.cloudapp.net, mais toouse nom correct de hello dans le fichier de configuration hello est MySite (test) . Vous pouvez uniquement le faire si les emplacements et le site Web de hello existent déjà dans votre abonnement. Si elles n’existent pas, créer un site Web de hello en exécutant le script de hello sans spécifier l’emplacement de hello, puis créez emplacement hello Bonjour [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885), et avant d’exécuter les script hello avec le nom du site Web modifié hello. Pour plus d’informations sur les emplacements de déploiement pour les applications web, consultez [Configurer des environnements intermédiaires pour les applications web dans Azure App Service](app-service-web/web-sites-staged-publishing.md).

## <a name="how-toorun-hello-publish-scripts"></a>Comment toorun hello publier des scripts
Si vous n’avez jamais exécuté un script Windows PowerShell avant, vous devez d’abord définir hello exécution stratégie tooenable scripts toorun. Il s’agit d’un utilisateur de tooprevent fonctionnalité sécurité de l’exécution de scripts Windows PowerShell s’ils sont vulnérable toomalware ou virus impliquant l’exécution de scripts.

### <a name="run-hello-script"></a>Exécutez le script de hello
1. Créer un package de déploiement Web hello pour votre projet. Un package Web Deploy est une archive compressée (fichier .zip) qui contiennent les fichiers que vous souhaitez un ordinateur virtuel ou le site Web de tooyour toocopy. Vous pouvez créer des packages Web Deploy dans Visual Studio pour toute application web.

![Créer un package Web Deploy](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

Pour plus d’informations, consultez [Comment : créer un package de déploiement web dans Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx). Vous pouvez également automatiser la création de hello de votre package Web Deploy, comme décrit dans la section de hello **publier des scripts de personnalisation et extension hello** plus loin dans cette rubrique.

1. Dans **l’Explorateur de solutions**, ouvrez le menu contextuel de hello pour le script de hello, puis choisissez **ouvrir avec PowerShell ISE**.
2. S’il s’agit hello première fois que vous exécutez des scripts Windows PowerShell sur cet ordinateur, ouvrez une fenêtre d’invite de commandes avec des privilèges d’administrateur et hello type commande suivante :

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. Connexion tooAzure à l’aide de hello la commande suivante.

    ```powershell
    Add-AzureAccount
    ```

    Lorsque vous y êtes invité, indiquez votre nom d’utilisateur et votre mot de passe.

    Notez que cette méthode de fournir des informations d’identification Azure ne fonctionne pas lorsque vous automatisez le script de hello. Au lieu de cela, vous devez utiliser les informations d’identification du tooprovide fichier .publishsettings hello. Une fois seulement, vous utilisez commande hello **Get-AzurePublishSettingsFile** hello de toodownload à partir de Azure et par la suite utiliser **Import-AzurePublishSettingsFile** fichier de hello tooimport. Pour obtenir des instructions détaillées, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

4. (Facultatif) Si vous souhaitez toocreate Azure ressources telles que la machine virtuelle de hello, base de données et du site Web sans avoir à publier votre application web, utilisent hello **Publish-WebApplication.ps1** avec hello **-Configuration** argument défini toohello fichier de configuration JSON. Cette commande utilise toodetermine de fichier de configuration de JSON hello le toocreate de ressources. Car elle utilise les paramètres par défaut de hello pour les autres arguments de ligne de commande, il crée des ressources de hello, mais ne publie pas votre application web. Hello – Verbose vous donne plus d’informations sur ce qui se passe.

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. Hello d’utilisation **Publish-WebApplication.ps1** commande comme indiqué dans un des exemples tooinvoke hello script suivant de hello et publier votre application web. Si vous devez les paramètres par défaut toooverride hello des hello autres arguments, comme le nom de l’abonnement hello, nom du package, les informations d’identification de l’ordinateur virtuel ou les informations d’identification du serveur de base de données de publication, vous pouvez spécifier ces paramètres. Hello d’utilisation **– Verbose** option toosee plus d’informations sur la progression de hello Hello processus de publication.

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    Si vous créez une machine virtuelle, commande hello ressemble à hello suivant. Cet exemple montre également comment toospecify hello les informations d’identification pour plusieurs bases de données. Pour hello machines virtuelles créées par ces scripts, certificats SSL de hello n’est pas à partir d’une autorité racine approuvée. Par conséquent, vous devez toouse hello **– AllowUntrusted** option.

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    script de Hello peut créer des bases de données, mais il ne crée pas de serveurs de base de données. Si vous voulez toocreate un serveur de base de données, vous pouvez utiliser hello **New-AzureSqlDatabaseServer** fonction Bonjour module Azure.

## <a name="customizing-and-extending-hello-publish-scripts"></a>Personnalisation et extension hello publier des scripts
Vous pouvez personnaliser hello publier le script et le fichier de configuration JSON. Hello des fonctions dans le module Windows PowerShell de hello **AzureWebAppPublishModule.psm1** ne sont pas prévu toobe modifié. Simplement toospecify une autre base de données ou modifier certaines propriétés hello de machine virtuelle de hello, modifier le fichier de configuration JSON hello. Si vous souhaitez tooextend hello de hello script tooautomate génération et test de votre projet, vous pouvez implémenter les stubs de fonction dans **Publish-WebApplication.ps1**.

tooautomate création de votre projet, ajoutez le code appelant MSBuild trop`New-WebDeployPackage` comme indiqué dans cet exemple de code. chemin d’accès de Hello toohello commande MSBuild est différente selon la version hello de Visual Studio que vous avez installé. tooget hello chemin d’accès correct, vous pouvez utiliser la fonction de hello **Get-MSBuildCmd**, comme illustré dans cet exemple.

### <a name="tooautomate-building-your-project"></a>tooautomate générer votre projet
1. Ajouter hello `$ProjectFile` paramètre dans la section des paramètres globaux hello.

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. Copier la fonction hello `Get-MSBuildCmd` dans votre fichier de script.

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

3. Remplacez `New-WebDeployPackage` avec hello de code suivant et remplacez les espaces réservés de hello lors de la construction de ligne hello `$msbuildCmd`. Ce code est destiné à Visual Studio 2015. Si vous utilisez Visual Studio 2013, modifiez hello **VisualStudioVersion** propriété ci-dessous trop`12.0`.

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function toobuild and package your web application
    ```

    toobuild votre application web, utilisez MsBuild.exe. Pour obtenir de l’aide, reportez-vous à la section Référence de ligne de commande MSBuild à l’adresse : [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-hello-build-command"></a>Démarrer l’exécution de la commande de génération hello

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain hello project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct hello path tooweb deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get hello full path for hello web deploy zip package. This is required for MSDeploy toowork
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. Appelez hello `New-WebDeployPackage` fonction avant cette ligne : `$Config = Read-ConfigFile $Configuration` pour les applications web ou `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` pour les ordinateurs virtuels.

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. Appeler script hello personnalisé à partir de la ligne de commande à l’aide de passage hello `$Project` argument, comme dans hello suivant l’exemple de ligne de commande.

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    tooautomate test de votre application, ajoutez le code trop`Test-WebApplication`. Être toouncomment que les lignes hello dans **Publish-WebApplication.ps1** dans lesquelles ces fonctions sont appelées. Si vous ne fournissez pas d’implémentation, vous pouvez créer manuellement votre projet avec Visual Studio, et puis exécution hello publier tooAzure toopublish de script.

## <a name="publishing-function-summary"></a>Résumé de la fonction de publication
aide tooget pour les fonctions que vous pouvez utiliser à l’invite de commandes Windows PowerShell hello, utilisez la commande hello `Get-Help function-name`. aide de Hello inclut des exemples et l’aide du paramètre. Hello même aide figure également dans les fichiers sources de script hello **AzureWebAppPublishModule.psm1** et **Publish-WebApplication.ps1**. aide et script de hello est localisées dans votre langage de Visual Studio.

**AzureWebAppPublishModule**

| Nom de la fonction | Description |
| --- | --- |
| Add-AzureSQLDatabase |Crée une base de données SQL Azure. |
| Add-AzureSQLDatabases |Crée les bases de données SQL Azure à partir de valeurs hello hello fichier de configuration JSON généré par Visual Studio. |
| Add-AzureVM |Crée une machine virtuelle Azure et renvoie le QU'URL de hello Hello déployé la machine virtuelle. Hello fonction définit les conditions préalables de hello et puis hello d’appels **New-AzureVM** fonction (module Azure) toocreate un nouvel ordinateur virtuel. |
| Add-AzureVMEndpoints |Ajoute le nouvel ordinateur virtuel de tooa des points de terminaison d’entrée et retourne la machine virtuelle, hello avec nouveau point de terminaison hello. |
| Add-AzureVMStorage |Crée un nouveau compte de stockage Azure dans l’abonnement actif de hello. nom de Hello du compte de hello commence par « devtest » suivi d’une chaîne alphanumérique unique. fonction Hello retourne le nom hello du nouveau compte de stockage hello. Vous devez spécifier un emplacement ou un groupe d’affinités pour le nouveau compte de stockage hello. |
| Add-AzureWebsite |Crée un site Web avec l’emplacement et le nom spécifié de hello. Cette fonction appelle hello **New-AzureWebsite** fonction Bonjour module Azure. Si l’abonnement de hello n’inclut pas déjà un site Web avec le nom spécifié de hello, cette fonction crée le site Web de hello et retourne un objet de site Web. Sinon, la valeur renvoyée est `$null`. |
| Backup-Subscription |Enregistre hello abonnement Azure actuel Bonjour `$Script:originalSubscription` variable dans l’étendue du script. Cette fonction enregistre l’abonnement Azure hello (tels qu’obtenus par `Get-AzureSubscription -Current`) et son compte de stockage et abonnement hello modifié par ce script (stocké dans la variable de hello `$UserSpecifiedSubscription`) et son compte de stockage, dans l’étendue du script. En enregistrant les valeurs hello, vous pouvez utiliser une fonction, tels que `Restore-Subscription`, toorestore hello d’origine abonnement et stockage compte toocurrent état actuel si l’état actuel de hello a changé. |
| Find-AzureVM |Obtient hello spécifié de machine virtuelle Azure. |
| Format-DevTestMessageWithTime |Ajoute un message tooa date et l’heure d’appel. Cette fonction est conçue pour les messages écrits toohello des flux d’erreurs et de commentaires. |
| Get-AzureSQLDatabaseConnectionString |Assemble une base de données de connexion chaîne tooconnect tooan SQL Azure. |
| Get-AzureVMStorage |Retourne hello nom hello premier du compte de stockage avec le modèle de nom hello « devtest*» (la casse) dans le groupe hello emplacement ou d’affinités spécifié. Si hello « devtest*« compte de stockage ne correspond pas à groupe d’affinités ou emplacement de hello, hello fonction l’ignore. Vous devez spécifier un emplacement ou un groupe d’affinités. |
| Get-MSDeployCmd |Retourne un outil de commande toorun hello MsDeploy.exe. |
| New-AzureVMEnvironment |Recherche ou crée un ordinateur virtuel dans l’abonnement hello qui correspond aux valeurs hello dans le fichier de configuration JSON hello. |
| Publish-WebPackage |Utilise MsDeploy.exe et un site web publient le package. ZIP fichier toodeploy ressources tooa site Web. Cette fonction ne génère aucune sortie. Si hello appel tooMSDeploy.exe échoue, la fonction hello lève une exception. tooget plus les résultats détaillés, utilisez hello **-Verbose** option. |
| Publish-WebPackageToVM |Vérifie les valeurs de paramètre hello et appelle ensuite hello **Publish-WebPackage** (fonction). |
| Read-ConfigFile |Valide le fichier de configuration JSON hello et retourne une table de hachage des valeurs sélectionnées. |
| Restore-Subscription |Réinitialise l’abonnement d’origine hello actuel abonnement toohello. |
| Test-AzureModule |Retourne `$true` si hello installé Azure module version 0.7.4 ou une version ultérieure. Retourne `$false` si le module de hello n’est pas installé ou est une version antérieure. Cette fonction n’a pas de paramètres. |
| Test-AzureModuleVersion |Retourne `$true` si hello hello module Azure est 0.7.4 ou une version ultérieure. Retourne `$false` si le module de hello n’est pas installé ou est une version antérieure. Cette fonction n’a pas de paramètres. |
| Test-HttpsUrl |Convertit l’objet de hello d’entrée URL tooa System.Uri. Retourne `$True` si hello URL est absolue et son schéma est https. Retourne `$false` si hello URL est relative, son schéma n’est pas HTTPS ou hello la chaîne d’entrée doit être converti tooa URL. |
| Test-Member |Retourne `$true` si une propriété ou méthode est un membre d’objet de hello. Sinon, renvoie `$false`. |
| Write-ErrorWithTime |Écrit un message d’erreur hello précédé de l’heure actuelle. Cette fonction appelle hello **Format-DevTestMessageWithTime** fonction tooprepend durée hello time avant d’écrire le flux d’erreur hello message toohello. |
| Write-HostWithTime |Écrit un programme hôte de message toohello (**Write-Host**) hello précédé de l’heure actuelle. effet Hello de l’écriture de programme de l’hôte toohello varie. La plupart des programmes qui hébergent Windows PowerShell écrire ces messages toostandard sortie. |
| Write-VerboseWithTime |Écrit un message détaillé précédé de hello heure actuelle. Étant donné qu’il appelle **Write-Verbose**, message de type hello affiche uniquement lorsque le script de hello est exécuté avec hello **Verbose** paramètre ou lorsque hello **VerbosePreference** préférence est définir trop**continuer**. |

**Publish-WebApplication**

| Nom de la fonction | Description |
| --- | --- |
| New-AzureWebApplicationEnvironment |Crée des ressources Azure, comme un site web ou une machine virtuelle. |
| New-WebDeployPackage |Cette fonction n’est pas implémentée. Vous pouvez ajouter des commandes dans cette toobuild fonction votre projet. |
| Publish-AzureWebApplication |Publie un tooAzure d’application web. |
| Publish-WebApplication |Crée et déploie des applications web, des machines virtuelles, des bases de données SQL et des comptes de stockage pour un projet web Visual Studio. |
| Test-WebApplication |Cette fonction n’est pas implémentée. Vous pouvez ajouter des commandes dans cette tootest fonction votre application. |

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur les scripts PowerShell en lisant [écriture de scripts avec Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) et consultez les autres scripts Azure PowerShell à hello [centre de scripts](https://azure.microsoft.com/documentation/scripts/).
