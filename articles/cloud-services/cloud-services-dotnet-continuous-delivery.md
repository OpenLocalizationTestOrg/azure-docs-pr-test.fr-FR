---
title: remise aaaContinuous pour cloud services avec TFS dans Azure | Documents Microsoft
description: "Découvrez comment les applications cloud tooset de livraison continue pour Azure. Exemples de code pour les instructions en ligne de commande MSBuild et les scripts PowerShell."
services: cloud-services
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4f3c93c6-5c82-4779-9d19-7404a01e82ca
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/12/2017
ms.author: kraigb
ms.openlocfilehash: c0e5e72ffbd3c05b84ce1733068e92c528bcc4b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a>Remise continue pour Cloud Services dans Azure
Hello est décrite dans cet article vous montre comment tooset de livraison continue pour les applications de cloud Azure. Ce processus vous permet de créer automatiquement des packages et de déployer hello package tooAzure après chaque archivage de code. processus de génération de package décrit dans cet article Hello est équivalent toohello **Package** commande dans Visual Studio et la procédure de publication est équivalent toohello **publier** dans Visual Studio.
Hello article couvre hello méthodes que vous utiliseriez toocreate un serveur de builds avec les instructions de ligne de commande MSBuild et scripts Windows PowerShell et également montre comment toooptionally configurer Visual Studio Team Foundation Server - définitions de Build d’équipe commandes de MSBuild toouse hello et scripts PowerShell. processus de Hello est personnalisable pour votre environnement de génération et les environnements cibles Azure.

Vous pouvez également utiliser Visual Studio Team Services, une version de TFS qui est hébergé dans Azure, toodo cela plus facilement. 

Avant de commencer, vous devez publier votre application à partir de Visual Studio.
Cela permet de garantir que toutes les ressources de hello sont disponibles et initialisé lors du processus de publication tooautomate hello.

## <a name="1-configure-hello-build-server"></a>1 : configurer hello serveur Build
Avant de pouvoir créer un package Azure à l’aide de MSBuild, vous devez installer les logiciels requis de hello et les outils sur le serveur de builds hello.

Visual Studio n’est pas requis toobe installé sur le serveur de builds hello. Si vous souhaitez toouse Service Team Foundation Build toomanage de votre serveur de builds, suivez les instructions de hello Bonjour [Service Team Foundation Build] [ Team Foundation Build Service] documentation.

1. Sur le serveur de builds hello, installez hello [.NET Framework 4.5.2][.NET Framework 4.5.2], qui inclut MSBuild.
2. Installer hello dernières [outils de création de Azure pour .NET](https://azure.microsoft.com/develop/net/).
3. Installer hello [bibliothèques Azure pour .NET](http://go.microsoft.com/fwlink/?LinkId=623519).
4. Serveur de builds de copier le fichier Microsoft.WebApplication.targets hello à partir d’un toohello d’installation de Visual Studio.

   Sur un ordinateur avec Visual Studio est installé, ce fichier se trouve dans le répertoire hello C:\\Files(x86)%\\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications. Vous devez le copier toohello même répertoire sur le serveur de builds hello.
5. Installer hello [Azure Tools pour Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).

## <a name="2-build-a-package-using-msbuild-commands"></a>2 : Génération d'un package à l'aide des commandes MSBuild
Cette section décrit comment tooconstruct un MSBuild commande qui crée un package Azure. Exécutez cette étape sur hello build server tooverify que tout est configuré correctement et qui exécute la commande de MSBuild hello ce que vous souhaitez toodo. Vous pouvez ajouter cette ligne de commande de tooexisting générer des scripts sur le serveur de builds hello, ou vous pouvez utiliser la ligne de commande hello dans une définition de Build TFS, comme décrit dans la section suivante de hello. Pour plus d’informations sur les paramètres de ligne de commande et MSBuild, consultez la page [Référence de la ligne de commande MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).

1. Si Visual Studio est installé sur le serveur de builds hello, recherchez et sélectionnez **invite de commandes Visual Studio** Bonjour **Visual Studio Tools** dossier dans Windows.

   Si Visual Studio n’est pas installé sur le serveur de builds hello, ouvrez une invite de commandes et assurez-vous que le MSBuild.exe est accessible sur le chemin d’accès. MSBuild est installé avec hello .NET Framework dans hello chemin d’accès % Windir%\\Microsoft.NET\\Framework\\*Version*. Par exemple, pour ajouter la variable d’environnement PATH MSBuild.exe toohello lorsque vous avez installé .NET Framework 4, tapez Bonjour commande à l’invite de commandes hello suivante :

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. À l’invite de commandes hello accédez dossier toohello contenant le fichier de projet Windows Azure que vous souhaitez toobuild.
3. Exécuter MSBuild avec hello /target : publier l’option comme hello l’exemple suivant :

       MSBuild /target:Publish

   Cette option peut être abrégée en /t:Publish. option de /t:Publish Hello dans MSBuild ne doit pas être confondue avec les commandes de publication hello disponibles dans Visual Studio lorsque vous avez hello Qu'azure SDK installé. Hello /t : option de publication uniquement les builds hello packages Azure. Il ne déploie pas les packages hello comme les commandes de publication hello dans Visual Studio.

   Si vous le souhaitez, vous pouvez spécifier le nom du projet hello comme paramètre de MSBuild. Si non spécifié, le répertoire actuel de hello est utilisé. Pour plus d’informations sur les options de ligne de commande MSBuild, consultez la page [Référence de la ligne de commande MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).
4. Recherchez la sortie de hello. Par défaut, cette commande crée un répertoire dans la relation toohello racine dossier hello projet, tel que *Répertoireprojet*\\bin\\*Configuration* \\ App.Publish\\. Lorsque vous générez un projet Windows Azure, vous générez deux fichiers, fichier de package hello lui-même et hello qui accompagne le fichier de configuration :

   * Project.cspkg
   * ServiceConfiguration.*TargetProfile*.cscfg

   Par défaut, tous les projets Azure comprennent un fichier de configuration de service (.cscfg file) pour les versions locales (débogage) et un autre pour les versions cloud (intermédiaire ou de production), mais vous pouvez ajouter ou supprimer les fichiers de configuration de service selon vos besoins. Lorsque vous créez un package dans Visual Studio, vous devez le tooinclude de fichier de configuration de service en même temps que le package de hello.
5. Spécifiez le fichier de configuration de service hello. Lorsque vous générez un package à l’aide de MSBuild, le fichier de configuration de service local hello est inclus par défaut. tooinclude un fichier de configuration de service différent, définissez la propriété de Profilcible de la commande MSBuild hello, comme dans hello l’exemple suivant :

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. Spécifiez l’emplacement hello pour la sortie de hello. Chemin d’accès de hello jeu à l’aide de la/p : PublishDir =*active* \\ option, y compris hello à droite du séparateur barre oblique inverse, hello l’exemple suivant :

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   Une fois que vous avez construit et testé un MSBuild appropriée toobuild de ligne de commande de vos projets et les associer dans un package d’Azure, vous pouvez ajouter cette ligne de commande tooyour des scripts de build. Si votre serveur de builds utilise des scripts personnalisés, ce processus dépend des particularités de votre processus de génération personnalisé. Si vous utilisez TFS comme un environnement de génération, vous pouvez suivre les instructions hello hello prochaine étape tooadd hello package Azure build tooyour processus de génération.

## <a name="3-build-a-package-using-tfs-team-build"></a>3 : Génération d’un package avec TFS Team Build
Si vous avez configuré comme serveur de création d’un contrôleur de build et le hello Team Foundation Server (TFS) configuré comme un ordinateur de build TFS, puis vous pouvez éventuellement configurer une génération automatique de votre package d’Azure. Pour plus d’informations sur comment tooset haut et utiliser Team Foundation server comme un système de génération, consultez [montée en charge votre système de génération][Scale out your build system]. En particulier, la procédure suivante suppose que vous avez configuré votre serveur de builds comme décrit dans [déployer et configurer un serveur de builds][Deploy and configure a build server], et que vous avez créé un projet d’équipe créé un cloud projet de service dans le projet d’équipe hello.

tooconfigure TFS toobuild Azure packages, effectuer hello comme suit :

1. Dans Visual Studio sur votre ordinateur de développement sur le menu Affichage de hello, choisissez **Team Explorer**, ou choisissez Ctrl +\\, Ctrl + M. Dans la fenêtre Team Explorer, développez hello **génère** nœud ou choisissez hello **génère** page, puis choisissez **nouvelle définition de Build**.

   ![Option Nouvelle définition de build][0]
2. Choisissez hello **déclencheur** onglet et spécifier hello souhaitées conditions lorsque vous souhaitez hello toobe package généré. Par exemple, spécifier **intégration continue** package de hello toobuild chaque fois qu’un contrôle de source de vérification se produit.
3. Choisissez hello **paramètres Source** onglet et vérifiez que votre dossier de projet est répertorié dans hello **dossier de contrôle de code Source** colonne, et l’état hello est **Active**.
4. Choisissez hello **générer les valeurs par défaut** onglet et sous contrôleur de Build, vérifiez le nom de hello du serveur de builds hello.  Choisissez également hello option **dossier de dépôt suivant de toohello de sortie de build copie** et spécifiez l’emplacement de dépôt hello souhaité.
5. Choisissez hello **processus** onglet. Sous l’onglet processus de hello, choisissez un modèle par défaut de hello, sous **générer**, choisissez le projet de hello si elle n’est pas déjà sélectionnée et développez hello **avancé** section Bonjour **générer**section de la grille de hello.
6. Choisissez **Arguments MSBuild**et définissez les arguments de ligne de commande MSBuild hello appropriés comme décrit à l’étape 2 ci-dessus. Par exemple, entrez **/t : publier/p : PublishDir =\\\\myserver\\supprime\\**  toobuild un package hello du package et copie les fichiers toohello emplacement \\ \\myserver\\supprime\\:

   ![Arguments MSBuild][2]

   > [!NOTE]
   > Copie hello fichiers tooa partage public rend plus facile toomanually déployer des packages de hello à partir de votre ordinateur de développement.
7. Réussite hello de votre étape de génération de test en vérifiant dans un projet de tooyour de modification ou d’une nouvelle build en file d’attente. tooqueue d’une nouvelle build, dans Team Explorer, cliquez sur **toutes les définitions de Build,** , puis **file d’attente une nouvelle Build**.

## <a name="4-publish-a-package-using-a-powershell-script"></a>4 : Publication d'un package à l'aide d'un script PowerShell
Cette section décrit comment tooconstruct un script Windows PowerShell qui publiera le package d’application Cloud hello sortie tooAzure à l’aide des paramètres facultatifs. Ce script peut être appelé une fois l’étape de génération de hello dans votre automatisation de génération personnalisée. Il peut également être appelé depuis les activités de workflow du modèle de processus dans Visual Studio TFS Team Build.

1. Installer hello [applets de commande Azure PowerShell] [ Azure PowerShell cmdlets] (v0.6.1 ou une version ultérieure).
   Pendant la phase d’installation hello applet de commande, choisissez tooinstall comme un composant logiciel enfichable. Notez que cette version officiellement pris en charge remplace la version antérieure de hello proposée via CodePlex, bien que les versions précédentes de hello numéro 2.x.x.
2. Démarrez PowerShell Azure à l’aide du menu Démarrer de hello ou page de démarrage. Si vous démarrez de cette façon, hello applets de commande PowerShell de Azure est chargé.
3. À l’invite de PowerShell hello, vérifiez que les applets de commande PowerShell hello sont chargées en entrant la commande partielle hello `Get-Azure` et en appuyant sur hello touche Tab pour la saisie semi-automatique des instructions.

   Si vous appuyez sur TAB. hello à plusieurs reprises, vous devez voir les différentes commandes Azure PowerShell.
4. Vérifiez que vous pouvez vous connecter tooyour abonnement Azure en important les informations de votre abonnement à partir du fichier .publishsettings de hello.

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   Puis entrez la commande hello

   `Get-AzureSubscription`

   Ceci affiche les informations sur votre abonnement. Vérifiez que tout est correct.
5. Enregistrer le modèle de script hello fourni à fin hello de cet article dans votre dossier de scripts en tant que c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.
6. Passez en revue la section des paramètres de script de hello hello. Ajoutez des valeurs ou modifiez les valeurs par défaut. Ces valeurs peuvent de toute manière être ignorées en indiquant des paramètres explicites.
7. Vérifiez contient le service cloud valide des comptes de stockage créés dans votre abonnement qui peut être ciblé par hello du script de publication. Le compte de stockage (stockage d’objets blob) sera être utilisé tooupload et stocker temporairement les fichier de package et de configuration de déploiement hello pendant le déploiement est en cours de création.

   * toocreate un nouveau service cloud, vous pouvez appeler cette hello script ou utilisez [portail Azure](https://portal.azure.com). nom de service de cloud Hello sera utilisé en tant que préfixe dans un nom de domaine complet, et par conséquent, il doit être unique.

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * toocreate un compte de stockage, vous pouvez appeler cette hello script ou utilisez [portail Azure](https://portal.azure.com). nom de compte de stockage Hello sera utilisé en tant que préfixe dans un nom de domaine complet, et par conséquent, il doit être unique. Vous pouvez essayer à l’aide de hello même nom que le service cloud.

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. Appeler le script de hello directement à partir d’Azure PowerShell ou associer cette toooccur automation de script tooyour hôte build après génération du package hello.

   > [!IMPORTANT]
   > script de Hello sera toujours supprimer ou remplacer vos déploiements existants par défaut si elles sont détectées. Ceci est nécessaire pour permettre la remise continue automatique là où il n'est pas possible de demander à l'utilisateur d'intervenir.
   >
   >

   **Exemple de scénario 1 :** toohello déploiement continu environnement d’un service intermédiaire :

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   Cette opération est normalement suivie d'un test de vérification et d'un échange d'adresses IP virtuelles. permutation de Hello adresse IP virtuelle peut être effectuée via hello [portail Azure](https://portal.azure.com) ou en utilisant l’applet de commande Move-déploiement de hello.

   **Exemple de scénario 2 :** environnement de production toohello déploiement continu d’un service de test dédié

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   **Bureau à distance :**

   Si le Bureau à distance est activé dans votre projet Windows Azure, vous devez étapes supplémentaires à usage unique tooperform hello tooensure que bon certificat de Service Cloud est téléchargés les services de cloud computing tooall ciblées par ce script.

   Recherchez les valeurs d’empreinte numérique du certificat hello attendus par vos rôles. Les valeurs de l’empreinte numérique sont visibles dans la section certificats de hello du fichier de configuration de cloud (c'est-à-dire ServiceConfiguration.Cloud.cscfg). Il est également visible dans la boîte de dialogue hello Configuration Bureau à distance dans Visual Studio vous afficher les Options et afficher hello sélectionné de certificat.

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   Télécharger des certificats de bureau à distance en tant qu’une étape d’installation unique à l’aide de hello script de l’applet de commande suivant :

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   Par exemple :

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   Vous pouvez également exporter le fichier de certificat PFX hello avec la clé privée et le téléchargement des certificats tooeach cible cloud service à l’aide de la [portail Azure](https://portal.azure.com).

   <!---
   Fixing broken links for Azure content migration from ACOM tooDOCS. I'm unable toofind a replacement links, so I'm commenting out this reference for now. hello author can investigate in hello future. "Read hello following article toolearn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   **Mise à niveau du déploiement et suppression du déploiement -\> Nouveau déploiement**

   Hello script par défaut effectue un déploiement de mise à niveau ($enableDeploymentUpgrade = 1) lorsque aucun paramètre n’est passé ou la valeur 1 est passée de manière explicite. Pour les instances uniques, ceci présente l'avantage de prendre moins de temps qu'un déploiement complet. Pour les instances qui nécessitent une haute disponibilité, qu'il présente également l’avantage de hello de laisser des instances en cours d’exécution tandis que d’autres sont mis à niveau (parcours de votre domaine de mise à jour), ainsi que votre adresse IP virtuelle n’est pas supprimé.

   Déploiement de mise à niveau peut être désactivé dans le script de hello ($enableDeploymentUpgrade = 0) ou en passant *enableDeploymentUpgrade - 0* en tant que paramètre, ce qui modifie la suppression de toofirst de comportement de script tout déploiement existant, puis créer un nouveau déploiement.

   > [!IMPORTANT]
   > script de Hello sera toujours supprimer ou remplacer vos déploiements existants par défaut si elles sont détectées. Ceci est nécessaire pour permettre la remise continue automatique là où il n'est pas possible de demander à l'utilisateur ou à l'opérateur d'intervenir.
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a>5 : Publication d’un package avec TFS Team Build
Cette étape facultative connecte à TFS Team Build toohello script créé à l’étape 4, qui gère la publication de tooAzure de génération de package hello. Cela implique la modification hello de modèle de processus utilisé par votre définition de build pour qu’il exécute une activité de publier à fin hello du flux de travail hello. Hello publication s’exécute la commande PowerShell en passant les paramètres de génération de hello. Sortie de hello MSBuild cible et un script de publication sera redirigé dans la sortie de génération standard de hello.

1. Modifier hello responsable de la définition de Build en continu déployer.
2. Sélectionnez hello **processus** onglet.
3. Suivez [ces instructions](http://msdn.microsoft.com/library/dd647551.aspx) tooadd un projet d’activité pour hello générer le modèle de processus, téléchargez le modèle par défaut de hello, ajoutez-le au projet de hello et archivez-le. Renommer le modèle de processus de génération hello, telles que AzureBuildProcessTemplate.
4. Retourner toohello **processus** onglet et utiliser **afficher les détails** tooshow une liste des modèles de processus de génération disponibles. Choisissez hello **nouveau...**  bouton, puis accédez de projet toohello vous venez d’ajouter et archivé. Recherchez le modèle hello vous venez de créer et choisissez **OK**.
5. Ouvrez hello sélectionné de modèle de processus à modifier. Vous pouvez ouvrir directement dans le Concepteur de flux de travail hello ou dans toowork de l’éditeur XML hello avec hello XAML.
6. Ajoutez hello suivant de la liste des nouveaux arguments en tant que lignes séparées dans l’onglet des arguments hello du Concepteur de flux de travail hello. Tous ces arguments doivent avoir direction=In et type=String. Il s’agit des paramètres tooflow utilisé à partir de la définition de build hello dans le flux de travail hello, quels hello de toocall utilisé get puis publier le script.

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Liste des arguments][3]

   Hello que XAML correspondant se présente comme suit :

       <Activity  _ />
         <x:Members>
           <x:Property Name="BuildSettings" Type="InArgument(mtbwa:BuildSettings)" />
           <x:Property Name="TestSpecs" Type="InArgument(mtbwa:TestSpecList)" />
           <x:Property Name="BuildNumberFormat" Type="InArgument(x:String)" />
           <x:Property Name="CleanWorkspace" Type="InArgument(mtbwa:CleanWorkspaceOption)" />
           <x:Property Name="RunCodeAnalysis" Type="InArgument(mtbwa:CodeAnalysisOption)" />
           <x:Property Name="SourceAndSymbolServerSettings" Type="InArgument(mtbwa:SourceAndSymbolServerSettings)" />
           <x:Property Name="AgentSettings" Type="InArgument(mtbwa:AgentSettings)" />
           <x:Property Name="AssociateChangesetsAndWorkItems" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateWorkItem" Type="InArgument(x:Boolean)" />
           <x:Property Name="DropBuild" Type="InArgument(x:Boolean)" />
           <x:Property Name="MSBuildArguments" Type="InArgument(x:String)" />
           <x:Property Name="MSBuildPlatform" Type="InArgument(mtbwa:ToolPlatform)" />
           <x:Property Name="PerformTestImpactAnalysis" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateLabel" Type="InArgument(x:Boolean)" />
           <x:Property Name="DisableTests" Type="InArgument(x:Boolean)" />
           <x:Property Name="GetVersion" Type="InArgument(x:String)" />
           <x:Property Name="PrivateDropLocation" Type="InArgument(x:String)" />
           <x:Property Name="Verbosity" Type="InArgument(mtbw:BuildVerbosity)" />
           <x:Property Name="Metadata" Type="mtbw:ProcessParameterMetadataCollection" />
           <x:Property Name="SupportedReasons" Type="mtbc:BuildReason" />
           <x:Property Name="SubscriptionName" Type="InArgument(x:String)" />
           <x:Property Name="StorageAccountName" Type="InArgument(x:String)" />
           <x:Property Name="CloudConfigLocation" Type="InArgument(x:String)" />
           <x:Property Name="PackageLocation" Type="InArgument(x:String)" />
           <x:Property Name="Environment" Type="InArgument(x:String)" />
           <x:Property Name="SubscriptionDataFileLocation" Type="InArgument(x:String)" />
           <x:Property Name="PublishScriptLocation" Type="InArgument(x:String)" />
           <x:Property Name="ServiceName" Type="InArgument(x:String)" />
         </x:Members>

         <this:Process.MSBuildArguments>
7. Ajoutez une nouvelle séquence à fin hello de s’exécuter sur l’Agent :

   1. Commencez par ajouter un toocheck d’activité instruction If pour un fichier de script valide. Valeur des toothis de condition hello :

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. Bonjour puis les cas de hello instruction If, ajouter une nouvelle activité de séquence. Ensemble hello affichage nom too'Start publier '
   3. Hello début publier la séquence étant toujours sélectionnée, ajouter la liste suivante de nouvelles variables en tant que lignes séparées dans l’onglet variables de Concepteur de workflow hello. Toutes les variables doivent comporter type =String et Scope=Start publish. Il s’agit des paramètres tooflow utilisé à partir de la définition de build hello dans le flux de travail, le hello de toocall utilisé get puis publier le script.

      * SubscriptionDataFilePath, de type String
      * PublishScriptFilePath, de type String

        ![Nouvelles variables][4]
   4. Si vous utilisez TFS 2012 ou version antérieure, ajoutez une activité ConvertWorkspaceItem début de hello de hello nouvelle séquence. Si vous utilisez TFS 2013 ou version ultérieure, ajoutez une activité GetLocalPath début de hello de nouvelle séquence de hello. Pour un ConvertWorkspaceItem, définissez les propriétés de hello comme suit : Direction = ServerToLocal, DisplayName = 'Convert publish nom de fichier de script', entrée = 'PublishScriptLocation', résultat = 'PublishScriptFilePath', espace de travail = 'Espace de travail'. Pour une activité GetLocalPath, définissez hello propriété IncomingPath too'PublishScriptLocation », et hello too'PublishScriptFilePath de résultat '. Cette toohello de chemin d’accès hello activité convertit un script à partir d’emplacements de serveur TFS de publication (le cas échéant) le chemin d’accès de tooa standard disque local.
   5. Si vous utilisez TFS 2012 ou version antérieure, ajoutez une autre activité ConvertWorkspaceItem à fin hello de hello nouvelle séquence. Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'. Si vous utilisez TFS 2013 ou version ultérieure, ajoutez un autre GetLocalPath. IncomingPath='SubscriptionDataFileLocation' et Result='SubscriptionDataFilePath.'
   6. Ajouter une activité InvokeProcess à fin hello Hello nouvelle séquence.
      Cette activité d’appels PowerShell.exe avec des arguments de hello transmis par hello la définition de Build.

      + Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)
      + DisplayName = Execute publish script
      + Nom de fichier = « PowerShell » (en incluant les guillemets hello)
      + OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)
   7. Bonjour **Handle Standard Output** section zone de texte de la InvokeProcess, définissez too'data de valeur de zone de texte hello ». Il s’agit d’une variable toostore les données de sortie standard salutation.
   8. Ajouter une activité WriteBuildMessage juste en dessous de hello **Handle Standard Output** section. Définir l’Importance de hello = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' et hello Message = « données ». Cela garantit la sortie standard de hello du script sera écrite toohello sortie de la génération.
   9. Bonjour **Handle Error Output** section zone de texte de la InvokeProcess, définissez too'data de valeur de zone de texte hello ». Il s’agit d’une les données de variable toostore salutation erreur standard.
   10. Ajouter une activité WriteBuildError juste en dessous de hello **Handle Error Output** section. Définir hello Message = « données ». Ainsi, les erreurs de types hello du script de hello sera écrite toohello sortie d’erreur de build.
   11. Corrigez toutes les erreurs, indiquées par des points d'exclamation bleus. Placez le curseur sur le points d’exclamation tooget une indication de l’erreur de hello. Enregistrer le workflow hello pour effacer des erreurs.

   résultat final de Hello Hello publier des activités doit ressembler à ceci dans le Concepteur de hello un flux de travail :

   ![Activités de workflow][5]

   résultat final de Hello Hello publier des flux de travail activités doit ressembler à ceci en XAML :

       <If Condition="[Not String.IsNullOrEmpty(PublishScriptLocation)]" sap2010:WorkflowViewState.IdRef="If_1">
           <If.Then>
             <Sequence DisplayName="Start Publish" sap2010:WorkflowViewState.IdRef="Sequence_4">
               <Sequence.Variables>
                 <Variable x:TypeArguments="x:String" Name="SubscriptionDataFilePath" />
                 <Variable x:TypeArguments="x:String" Name="PublishScriptFilePath" />
               </Sequence.Variables>
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert publish script filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_1" Input="[PublishScriptLocation]" Result="[PublishScriptFilePath]" Workspace="[Workspace]" />
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert subscription filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_2" Input="[SubscriptionDataFileLocation]" Result="[SubscriptionDataFilePath]" Workspace="[Workspace]" />
               <mtbwa:InvokeProcess Arguments="[String.Format(&quot; -File &quot;&quot;{0}&quot;&quot; -serviceName {1}&#xD;&#xA;            -storageAccountName {2} -packageLocation &quot;&quot;{3}&quot;&quot;&#xD;&#xA;            -cloudConfigLocation &quot;&quot;{4}&quot;&quot; -subscriptionDataFile &quot;&quot;{5}&quot;&quot;&#xD;&#xA;            -selectedSubscription {6} -environment &quot;&quot;{7}&quot;&quot;&quot;,&#xD;&#xA;            PublishScriptFilePath, ServiceName, StorageAccountName,&#xD;&#xA;            PackageLocation, CloudConfigLocation,&#xD;&#xA;            SubscriptionDataFilePath, SubscriptionName, Environment)]" DisplayName="'Execute Publish Script'" FileName="[PowerShell]" sap2010:WorkflowViewState.IdRef="InvokeProcess_1">
                 <mtbwa:InvokeProcess.ErrorDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildError Message="{x:Null}" sap2010:WorkflowViewState.IdRef="WriteBuildError_1" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.ErrorDataReceived>
                 <mtbwa:InvokeProcess.OutputDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildMessage sap2010:WorkflowViewState.IdRef="WriteBuildMessage_2" Importance="[Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High]" Message="[data]" mva:VisualBasic.Settings="Assembly references and imported namespaces serialized as XML namespaces" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.OutputDataReceived>
               </mtbwa:InvokeProcess>
             </Sequence>
           </If.Then>
         </If>
       </Sequence>
8. Enregistrer le workflow de modèle de processus de génération hello et archiver ce fichier.
9. Modifier la définition de build hello (fermer si elle est déjà ouverte) et sélectionnez hello **nouveau** bouton si vous ne voyez pas encore hello nouveau modèle dans hello liste des modèles de processus.
10. Définissez les valeurs de propriété de paramètre hello Bonjour section divers comme suit :

    1. CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *Cette valeur est dérivée de : ($PublishDir)ServiceConfiguration.Cloud.cscfg*
    2. PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *Cette valeur est dérivée de : ($PublishDir)($ProjectName).cspkg*
    3. PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'
    4. ServiceName = 'mycloudservicename' *utilisation hello approprié nom du service cloud ici*
    5. Environment = 'Staging'
    6. StorageAccountName = 'mystorageaccountname' *utilisation hello approprié nom compte de stockage ici*
    7. SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'
    8. SubscriptionName = 'default'

    ![Valeurs de propriétés des paramètres][6]
11. Enregistrer les modifications de hello toohello la définition de Build.
12. File d’attente d’un tooexecute de Build à la fois hello build du package et de publication. Si vous avez un déclencheur défini tooContinuous intégration, vous allez exécuter ce comportement sur chaque archivage.

### <a name="publishcloudserviceps1-script-template"></a>Modèle de script PublishCloudService.ps1
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy too$servicename",
        $timeStampFormat = "g",
        $alwaysDeleteExistingDeployments = 1,
        $enableDeploymentUpgrade = 1,
        $selectedsubscription = "default",
        $subscriptionDataFile = ""
     )


function Publish()
{
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot -ErrorVariable a -ErrorAction silentlycontinue
    if ($a[0] -ne $null)
    {
        Write-Output "$(Get-Date -f $timeStampFormat) - No deployment is detected. Creating a new deployment. "
    }
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according too$alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
    if ($deployment.Name -ne $null)
    {
        switch ($alwaysDeleteExistingDeployments)
        {
            1
            {
                switch ($enableDeploymentUpgrade)
                {
                    1  #Update deployment inplace (usually faster, cheaper, won't destroy VIP)
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Upgrading deployment."
                        UpgradeDeployment
                    }
                    0  #Delete then create new deployment
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Deleting deployment."
                        DeleteDeployment
                        CreateNewDeployment

                    }
                } # switch ($enableDeploymentUpgrade)
            }
            0
            {
                Write-Output "$(Get-Date -f $timeStampFormat) - ERROR: Deployment exists in $servicename.  Script execution cancelled."
                exit
            }
        } #switch ($alwaysDeleteExistingDeployments)
    } else {
            CreateNewDeployment
    }
}

function CreateNewDeployment()
{
    write-progress -id 3 -activity "Creating New Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: In progress"

    $opstat = New-AzureDeployment -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Creating New Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: Complete, Deployment ID: $completeDeploymentID"

    StartInstances
}

function UpgradeDeployment()
{
    write-progress -id 3 -activity "Upgrading Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: In progress"

    # perform Update-Deployment
    $setdeployment = Set-AzureDeployment -Upgrade -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName -Force

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Upgrading Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: Complete, Deployment ID: $completeDeploymentID"
}

function DeleteDeployment()
{

    write-progress -id 2 -activity "Deleting Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: In progress"

    #WARNING - always deletes with force
    $removeDeployment = Remove-AzureDeployment -Slot $slot -ServiceName $serviceName -Force

    write-progress -id 2 -activity "Deleting Deployment: Complete" -completed -Status $removeDeployment
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: Complete"

}

function StartInstances()
{
    write-progress -id 4 -activity "Starting Instances" -status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: In progress"

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $runstatus = $deployment.Status

    if ($runstatus -ne 'Running')
    {
        $run = Set-AzureDeployment -Slot $slot -ServiceName $serviceName -Status Running
    }
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $oldStatusStr = @("") * $deployment.RoleInstanceList.Count

    while (-not(AllInstancesRunning($deployment.RoleInstanceList)))
    {
        $i = 1
        foreach ($roleInstance in $deployment.RoleInstanceList)
        {
            $instanceName = $roleInstance.InstanceName
            $instanceStatus = $roleInstance.InstanceStatus

            if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
            {
                $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
                Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
            }

            write-progress -id (4 + $i) -activity "Starting Instance '$instanceName'" -status "$instanceStatus"
            $i = $i + 1
        }

        sleep -Seconds 1

        $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    }

    $i = 1
    foreach ($roleInstance in $deployment.RoleInstanceList)
    {
        $instanceName = $roleInstance.InstanceName
        $instanceStatus = $roleInstance.InstanceStatus

        if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
        {
            $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
            Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
        }

        $i = $i + 1
    }

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $opstat = $deployment.Status

    write-progress -id 4 -activity "Starting Instances" -completed -status $opstat
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: $opstat"
}

function AllInstancesRunning($roleInstanceList)
{
    foreach ($roleInstance in $roleInstanceList)
    {
        if ($roleInstance.InstanceStatus -ne "ReadyRole")
        {
            return $false
        }
    }

    return $true
}

#configure powershell with Azure 1.7 modules
Import-Module Azure

#configure powershell with publishsettings for your subscription
$pubsettings = $subscriptionDataFile
Import-AzurePublishSettingsFile $pubsettings
Set-AzureSubscription -CurrentStorageAccountName $storageAccountName -SubscriptionName $selectedsubscription
Select-AzureSubscription $selectedsubscription

#set remaining environment variables for Azure cmdlets
$subscription = Get-AzureSubscription $selectedsubscription
$subscriptionname = $subscription.subscriptionname
$subscriptionid = $subscription.subscriptionid
$slot = $environment

#main driver - publish & write progress tooactivity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a>Étapes suivantes
débogage distant tooenable lors de l’utilisation de la livraison continue, consultez [activer le débogage distant lors de l’utilisation de livraison continue toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[hello .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
