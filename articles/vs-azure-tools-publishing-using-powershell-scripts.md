---
title: "Utilisation de scripts Windows PowerShell pour publier dans des environnements de développement et de test | Microsoft Docs"
description: "Découvrez comment utiliser les scripts Windows PowerShell à partir de Visual Studio pour la publication dans des environnements de développement et de test."
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
ms.openlocfilehash: 4e9409aac836a60e7ea01261840c084ff09e954e
ms.sourcegitcommit: f847fcbf7f89405c1e2d327702cbd3f2399c4bc2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2017
---
# <a name="using-windows-powershell-scripts-to-publish-to-dev-and-test-environments"></a>Utilisation de scripts Windows PowerShell pour publier des environnements de développement et de test

Lorsque vous créez une application web dans Visual Studio, vous pouvez générer un script Windows PowerShell que vous pouvez utiliser ultérieurement pour automatiser la publication de votre site web sur Azure en tant qu’application web dans Azure App Service ou dans une machine virtuelle. Vous pouvez modifier et étendre le script Windows PowerShell dans l’éditeur Visual Studio, conformément à vos besoins, ou intégrer le script à la build, aux tests et aux scripts de publication existants.

À l’aide de ces scripts, vous pouvez configurer des versions personnalisées (également connues comme environnements de développement et de test) de votre site pour une utilisation temporaire. Par exemple, vous pouvez configurer une version particulière de votre site web sur une machine virtuelle Azure ou sur l’emplacement intermédiaire d’un site web pour exécuter une suite de tests, reproduire un bogue, tester un correctif, évaluer une proposition de modification ou configurer un environnement personnalisé pour une démonstration ou une présentation. Une fois que vous avez créé un script qui publie votre projet, vous pouvez recréer des environnements identiques en réexécutant le script en fonction des besoins, ou en exécutant le script avec votre propre build de votre application web pour créer un environnement personnalisé de test.

## <a name="prerequisites"></a>Composants requis

* Kit de développement logiciel (SDK) Azure 2.3 ou version ultérieure. Voir [Téléchargements Visual Studio](http://go.microsoft.com/fwlink/?LinkID=624384). (Vous n’avez pas besoin du kit de développement logiciel (SDK) Azure pour générer les scripts pour les projets web. Cette fonctionnalité s’adresse aux projets web, et non aux rôles web dans les services cloud.)
* Azure PowerShell 0.7.4 ou version ultérieure. Consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).
* [Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) ou version ultérieure.

## <a name="additional-tools"></a>Outils supplémentaires

Des outils et ressources supplémentaires sont disponibles pour l’utilisation de PowerShell dans Visual Studio pour le développement Azure. Consultez [Outils PowerShell pour Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).

## <a name="generating-the-publish-scripts"></a>Génération de scripts de publication

Vous pouvez générer des scripts de publication pour une machine virtuelle qui héberge votre site web lorsque vous créez un projet en suivant [ces instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Vous pouvez également [Générer des scripts de publication pour les applications web dans Azure App Service](app-service/app-service-web-get-started-dotnet.md).

## <a name="scripts-that-visual-studio-generates"></a>Scripts générés par Visual Studio

Visual Studio génère un dossier au niveau solution appelé **PublishScripts** qui contient deux fichiers Windows PowerShell, un script de publication pour votre machine virtuelle ou votre site web et un module qui contient des fonctions que vous pouvez utiliser dans les scripts. Visual Studio génère également un fichier au format JSON qui spécifie les détails du projet que vous déployez.

### <a name="windows-powershell-publish-script"></a>Script de publication Windows PowerShell

Le script de publication contient des étapes de publication spécifiques pour le déploiement sur un site web ou une machine virtuelle. Visual Studio propose la coloration de syntaxe pour le développement de Windows PowerShell. Vous pouvez bénéficier d’une aide sur les fonctions et modifier librement les fonctions dans le script en fonction de l’évolution de vos besoins.

### <a name="windows-powershell-module"></a>Module Windows PowerShell

Le module Windows PowerShell généré par Visual Studio contient des fonctions que le script de publication utilise. Ces fonctions Azure PowerShell ne sont pas destinées à être modifiées. Consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).

### <a name="json-configuration-file"></a>Fichier de configuration JSON
Le fichier JSON est créé dans le dossier **Configurations** et contient des données de configuration qui spécifient exactement les ressources à déployer sur Azure. Le nom du fichier généré par Visual Studio est projet-nom-WAWS-dev.json, si vous avez créé un site web, ou projet-nom-VM-dev.json, si vous avez créé une machine virtuelle. Voici un exemple de fichier de configuration JSON généré lorsque vous créez un site web. La plupart des valeurs sont explicites. Le nom du site web est généré par Azure ; il peut donc ne pas correspondre au nom de votre projet.

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

Lorsque vous créez une machine virtuelle, le fichier de configuration JSON ressemble à ce qui suit. Un service cloud est créé comme un conteneur pour la machine virtuelle. La machine virtuelle contient les points de terminaison habituels pour l’accès web via HTTP et HTTPS, ainsi que les points de terminaison pour Web Deploy, ce qui vous permet de publier sur le site web à partir de votre ordinateur local, de la connexion Bureau à distance et de Windows PowerShell.

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

Vous pouvez modifier la configuration JSON pour changer ce qui se passe lorsque vous exécutez les scripts de publication. Les sections `cloudService` et `virtualMachine` sont obligatoires, mais vous pouvez supprimer la section `databases` si vous n’en avez pas besoin. Les propriétés qui sont vides dans le fichier de configuration par défaut généré par Visual Studio sont facultatives ; celles qui ont des valeurs dans le fichier de configuration par défaut sont obligatoires.

Si vous possédez un site web qui compte plusieurs environnements de déploiement (appelés emplacements) au lieu d’un site de production unique dans Azure, vous pouvez inclure le nom de l’emplacement dans le nom du site web dans le fichier de configuration JSON. Par exemple, si votre site web est nommé **monsite** et que son emplacement est nommé **test**, l’URI est `mysite-test.cloudapp.net`, mais le nom correct à utiliser dans le fichier de configuration est monsite(test). Vous pouvez uniquement effectuer cette opération si le site web et les emplacements existent déjà dans votre abonnement. S’ils n’existent pas, créez le site web en exécutant le script sans spécifier l’emplacement, puis créez l’emplacement dans le [portail Azure](https://portal.azure.com/). Ensuite, exécutez le script avec le nom de site web modifié. Pour plus d’informations sur les emplacements de déploiement pour les applications web, consultez [Configurer des environnements intermédiaires pour les applications web dans Azure App Service](app-service/web-sites-staged-publishing.md).

## <a name="how-to-run-the-publish-scripts"></a>Exécution de scripts de publication

Si vous n’avez jamais exécuté de script Windows PowerShell auparavant, vous devez d’abord définir la stratégie d’exécution pour permettre l’exécution de scripts. Cette stratégie est une fonctionnalité de sécurité visant à empêcher les utilisateurs d’exécuter des scripts Windows PowerShell s’ils sont vulnérables aux programmes malveillants ou aux virus impliquant l’exécution de scripts.

### <a name="run-the-script"></a>Exécutez le script

1. Créez le package Web Deploy pour votre projet. Un package Web Deploy est une archive compressée (fichier .zip) contenant les fichiers que vous souhaitez copier sur votre site web ou sur votre machine virtuelle. Vous pouvez créer des packages Web Deploy dans Visual Studio pour toute application web.

![Créer un package Web Deploy](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

Pour plus d’informations, consultez [Comment : créer un package de déploiement web dans Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx). Vous pouvez également automatiser la création de votre package Web Deploy, comme décrit dans la section [Personnalisation et extension des scripts de publication[(#customizing-and-extending-publish-scripts)]

1. Dans l’**Explorateur de solutions**, ouvrez le menu contextuel du script, puis choisissez **Ouvrir avec PowerShell ISE**.
2. Si vous exécutez des scripts Windows PowerShell sur cet ordinateur pour la première fois, ouvrez une fenêtre d’invite de commandes avec des privilèges d’administrateur et tapez la commande suivante :

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. Connectez-vous à Azure en utilisant la commande suivante.

    ```powershell
    Add-AzureAccount
    ```

    Lorsque vous y êtes invité, indiquez votre nom d’utilisateur et votre mot de passe.

    Notez que lorsque vous automatisez le script, cette méthode de renseignement des informations d’identification Azure ne fonctionne pas. À la place, vous devez utiliser le fichier `.publishsettings` pour fournir des informations d’identification. Une fois seulement, vous utilisez la commande **Get-AzurePublishSettingsFile** pour télécharger le fichier à partir d’Azure. Ensuite, vous utilisez **Import-AzurePublishSettingsFile** pour importer le fichier. Pour des instructions détaillées, consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).

4. (Facultatif) Si vous souhaitez créer des ressources Azure telles que la machine virtuelle, la base de données et le site web sans publier votre application web, utilisez la commande **Publish-WebApplication.ps1** avec l’argument **-Configuration** défini dans le fichier de configuration JSON. Cette ligne de commande utilise le fichier de configuration JSON pour déterminer les ressources à créer. Étant donné qu’elle utilise les paramètres par défaut pour les autres arguments de ligne de commande, elle crée les ressources, mais ne publie pas votre application web. L’option –Verbose vous donne plus d’informations sur ce qui se passe.

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. Utilisez la commande **Publish-WebApplication.ps1** comme indiqué dans l’un des exemples suivants pour appeler le script et publier votre application web. Si vous souhaitez remplacer les paramètres par défaut de tout autre argument, comme le nom de l’abonnement, le nom du package de publication, les informations d’identification de la machine virtuelle ou les informations d’identification du serveur de base de données, vous pouvez spécifier ces paramètres. Utilisez l’option **–Verbose** pour afficher plus d’informations sur la progression du processus de publication.

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    Si vous créez une machine virtuelle, la commande ressemble à ce qui suit. Cet exemple montre également comment spécifier les informations d’identification pour plusieurs bases de données. Pour les machines virtuelles créées par ces scripts, le certificat SSL n’est pas d’une autorité racine de confiance. Par conséquent, vous devez utiliser l’option **–AllowUntrusted** .

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

    Le script peut créer des bases de données, mais il ne crée pas de serveurs de base de données. Si vous souhaitez créer un serveur de base de données, vous pouvez utiliser la fonction **New-AzureSqlDatabaseServer** du module Azure.

## <a name="customizing-and-extending-the-publish-scripts"></a>Personnalisation et extension des scripts de publication
Vous pouvez personnaliser le script de publication et le fichier de configuration JSON. Les fonctions dans le module Windows PowerShell **AzureWebAppPublishModule.psm1** ne sont pas destinées à être modifiées. Si vous souhaitez simplement spécifier une autre base de données ou modifier certaines propriétés de la machine virtuelle, modifiez le fichier de configuration JSON. Si vous souhaitez étendre la fonctionnalité de script pour automatiser la création et le test de votre projet, vous pouvez implémenter les stubs de fonction dans **Publish-WebApplication.ps1**.

Pour automatiser la création de votre projet, ajoutez le code appelant MSBuild sur `New-WebDeployPackage` , comme illustré dans cet exemple de code. Le chemin d’accès à la commande MSBuild est différent selon la version de Visual Studio que vous avez installée. Pour obtenir le chemin d’accès correct, vous pouvez utiliser la fonction **Get-MSBuildCmd**, comme illustré dans cet exemple.

### <a name="to-automate-building-your-project"></a>Pour automatiser la création de votre projet
1. Ajoutez le paramètre `$ProjectFile` dans la section des paramètres globaux.

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. Copiez la fonction `Get-MSBuildCmd` dans votre fichier de script.

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

3. Remplacez `New-WebDeployPackage` avec le code suivant et remplacez les espaces réservés dans la ligne créant `$msbuildCmd`. Ce code est destiné à Visual Studio 2017. Si vous utilisez Visual Studio 2015, remplacez la propriété **VisualStudioVersion** par `14.0` (`12.0` pour Visual Studio 2013).

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function to build and package your web application
    ```

    Pour générer votre application web, utilisez MsBuild.exe. Pour obtenir de l’aide, reportez-vous à la section Référence de ligne de commande MSBuild à l’adresse : [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=15.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-the-build-command"></a>Démarrez l’exécution de la commande build

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain the project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct the path to web deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get the full path for the web deploy zip package. This is required for MSDeploy to work
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. Appelez la fonction `New-WebDeployPackage` avant cette ligne : `$Config = Read-ConfigFile $Configuration` pour les applications web ou `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` pour les machines virtuelles.

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. Appelez le script personnalisé à partir de la ligne de commande à l’aide de la transmission de l’argument `$Project`, comme dans l'exemple suivant :

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    Pour automatiser le test de votre application, ajoutez le code à `Test-WebApplication`. Veillez à supprimer les marques de commentaire des lignes dans **Publish-WebApplication.ps1** où ces fonctions sont appelées. Si vous ne fournissez pas d’implémentation, vous pouvez créer votre projet manuellement avec Visual Studio, puis exécuter le script de publication pour publier dans Azure.

## <a name="publishing-function-summary"></a>Résumé de la fonction de publication
Pour obtenir de l’aide pour les fonctions que vous pouvez utiliser à l’invite de commande Windows PowerShell, utilisez la commande `Get-Help function-name`. L’aide inclut de l’aide sur les paramètres et des exemples. Le même texte d’aide figure également dans les fichiers sources du script, **AzureWebAppPublishModule.psm1** et **Publish-WebApplication.ps1**. Le script et l’aide sont localisés dans votre langue Visual Studio.

**AzureWebAppPublishModule**

| Nom de la fonction | Description |
| --- | --- |
| Add-AzureSQLDatabase |Crée une base de données SQL Azure. |
| Add-AzureSQLDatabases |Crée des bases de données SQL Azure à partir des valeurs du fichier de configuration JSON généré par Visual Studio. |
| Add-AzureVM |Crée une machine virtuelle Azure et renvoie l’URL de la machine virtuelle déployée. La fonction définit les conditions préalables, puis appelle la fonction **New-AzureVM** (module Azure) pour créer une machine virtuelle. |
| Add-AzureVMEndpoints |Ajoute de nouveaux points de terminaison d’entrée à une machine virtuelle et renvoie la machine virtuelle avec le nouveau point de terminaison. |
| Add-AzureVMStorage |Crée un compte de stockage Azure dans l’abonnement actif. Le nom du compte commence par « devtest » et est suivi d’une chaîne alphanumérique unique. La fonction renvoie le nom du nouveau compte de stockage. Spécifiez un emplacement ou un groupe d’affinités pour le nouveau compte de stockage. |
| Add-AzureWebsite |Crée un site web avec le nom et l’emplacement spécifiés. Cette fonction appelle la fonction **New-AzureWebsite** dans le module Azure. Si l’abonnement ne contient pas déjà un site web avec le nom spécifié, cette fonction crée le site web et renvoie un objet de site web. Sinon, la valeur renvoyée est `$null`. |
| Backup-Subscription |Enregistre l’abonnement Azure actif dans la variable `$Script:originalSubscription` dans la portée du script. Cette fonction enregistre l’abonnement Azure actif (tel qu’obtenu par `Get-AzureSubscription -Current`) et son compte de stockage, ainsi que l’abonnement modifié par ce script (stocké dans la variable `$UserSpecifiedSubscription`) et son compte de stockage, dans la portée de script. En enregistrant les valeurs, vous pouvez utiliser une fonction telle que `Restore-Subscription` pour restaurer l’abonnement actif d’origine et son compte de stockage à l’état actif, si ce dernier a changé. |
| Find-AzureVM |Obtient la machine virtuelle Azure spécifiée. |
| Format-DevTestMessageWithTime |Indique la date et l’heure avant un message. Cette fonction est conçue pour les messages écrits dans les flux Error et Verbose. |
| Get-AzureSQLDatabaseConnectionString |Assemble une chaîne de connexion pour se connecter à une base de données SQL Azure. |
| Get-AzureVMStorage |Renvoie le nom du premier compte de stockage avec le modèle de nom devtest *(non sensible à la casse) dans l’emplacement ou le groupe d’affinités spécifié. Si le compte de stockage devtest* ne correspond pas à l’emplacement ou au groupe d’affinités, la fonction l’ignore. Spécifiez un emplacement ou un groupe d’affinités. |
| Get-MSDeployCmd |Renvoie une commande pour exécuter l’outil MsDeploy.exe. |
| New-AzureVMEnvironment |Recherche ou crée une machine virtuelle dans l’abonnement qui correspond aux valeurs dans le fichier de configuration JSON. |
| Publish-WebPackage |Utilise MsDeploy.exe et un fichier. zip de package de publication web pour déployer des ressources sur un site web. Cette fonction ne génère aucune sortie. Si l’appel de MSDeploy.exe échoue, la fonction lève une exception. Pour obtenir une sortie plus détaillée, utilisez l’option **-Verbose**. |
| Publish-WebPackageToVM |Vérifie les valeurs des paramètres, puis appelle la fonction **Publish-WebPackage** . |
| Read-ConfigFile |Valide le fichier de configuration JSON et renvoie une table de hachage des valeurs sélectionnées. |
| Restore-Subscription |Réinitialise l’abonnement actif sur l’abonnement d’origine. |
| Test-AzureModule |Renvoie `$true` si la version du module Azure installé est 0.7.4 ou une version ultérieure. Renvoie `$false` si le module n’est pas installé ou s’il s’agit d’une version antérieure. Cette fonction n’a pas de paramètres. |
| Test-AzureModuleVersion |Renvoie `$true` si la version du module Azure est 0.7.4 ou une version ultérieure. Renvoie `$false` si le module n’est pas installé ou s’il s’agit d’une version antérieure. Cette fonction n’a pas de paramètres. |
| Test-HttpsUrl |Convertit l’URL d’entrée en un objet System.Uri. Renvoie `$True` si l’URL est absolue et que son schéma est https. Renvoie `$false` si l’URL est relative, que son schéma n’est pas HTTPS ou que la chaîne d’entrée ne peut pas être convertie en URL. |
| Test-Member |Renvoie `$true` si une propriété ou méthode est un membre de l’objet. Sinon, renvoie `$false`. |
| Write-ErrorWithTime |Écrit un message d’erreur préfixé avec l’heure actuelle. Cette fonction appelle la fonction **Format-DevTestMessageWithTime** à indiquer l’heure avant d’écrire le message dans le flux Error. |
| Write-HostWithTime |Écrit un message dans le programme hôte (**Write-Host**) préfixé avec l’heure actuelle. L’effet de l’écriture dans le programme hôte varie. La plupart des programmes qui hébergent Windows PowerShell écrivent ces messages dans la sortie standard. |
| Write-VerboseWithTime |Écrit un message détaillé préfixé avec l’heure actuelle. Étant donné qu’il appelle **Write-Verbose**, le message s’affiche uniquement lorsque le script s’exécute avec le paramètre **Verbose** ou lorsque la préférence **VerbosePreference** est définie sur **Continuer**. |

**Publish-WebApplication**

| Nom de la fonction | Description |
| --- | --- |
| New-AzureWebApplicationEnvironment |Crée des ressources Azure, comme un site web ou une machine virtuelle. |
| New-WebDeployPackage |Cette fonction n’est pas implémentée. Vous pouvez ajouter des commandes à cette fonction pour créer votre projet. |
| Publish-AzureWebApplication |Publie une application web dans Azure. |
| Publish-WebApplication |Crée et déploie des applications web, des machines virtuelles, des bases de données SQL et des comptes de stockage pour un projet web Visual Studio. |
| Test-WebApplication |Cette fonction n’est pas implémentée. Vous pouvez ajouter des commandes à cette fonction pour tester votre application. |

## <a name="next-steps"></a>Étapes suivantes
Pour en savoir plus sur l’écriture de scripts PowerShell lisez [Écriture de scripts avec Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) et consultez d’autres scripts Azure PowerShell sur le [Centre de scripts](https://azure.microsoft.com/documentation/scripts/).
