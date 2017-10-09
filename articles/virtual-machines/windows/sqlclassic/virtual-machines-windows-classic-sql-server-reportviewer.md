---
title: aaaUse ReportViewer dans un Site Web | Documents Microsoft
description: "Cette rubrique décrit comment toobuild un site Web Microsoft Azure avec le contrôle ReportViewer Visual Studio hello qui affiche un rapport stocké sur une Machine virtuelle Microsoft Azure."
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 78b76318-d9bf-48ef-9d9e-d1b7d8cf3042
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: 8e0729d6657f96c32a9ac7dffdff7745ff92b48d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-reportviewer-in-a-web-site-hosted-in-azure"></a>Utilisation de ReportViewer sur un site web hébergé dans Azure
> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../azure-resource-manager/resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.

Vous pouvez créer un site Web Microsoft Azure avec hello du contrôle Visual Studio ReportViewer qui affiche un rapport stocké sur une Machine virtuelle Microsoft Azure. Hello contrôle ReportViewer est dans une application Web que vous créez à l’aide de hello modèle d’application Web ASP.NET.

> [!IMPORTANT]
> modèles d’Application Web ASP.NET MVC Hello ne prennent pas en charge contrôle ReportViewer de hello.

tooincorporate ReportViewer dans votre site Web Microsoft Azure, vous devez hello toocomplete tâches suivantes.

* **Ajouter** assemblys toohello Package de déploiement
* **Configuration** de l’authentification et de l’autorisation
* **Publier** hello tooAzure d’application Web ASP.NET

## <a name="prerequisites"></a>Composants requis
Passez en revue la section « instructions générales et meilleures pratiques » de hello dans [SQL Server Business Intelligence dans des Machines virtuelles Azure](../classic/ps-sql-bi.md).

> [!NOTE]
> Les contrôles ReportViewer sont fournis avec Visual Studio Standard Edition ou une version supérieure. Si vous utilisez hello Web Developer Express Edition, vous devez installer hello [MICROSOFT REPORT VIEWER 2012 RUNTIME](https://www.microsoft.com/download/details.aspx?id=35747) fonctionnalités du runtime toouse hello ReportViewer.
> 
> ReportViewer configuré en mode de traitement local n’est pas pris en charge dans Microsoft Azure.

## <a name="adding-assemblies-toohello-deployment-package"></a>Ajout d’assemblys toohello Package de déploiement
Lorsque vous hébergez votre ASP.NET application sur site, les assemblys ReportViewer hello sont généralement installés directement dans hello global assembly cache (GAC) du serveur IIS de hello lors de l’installation de Visual Studio et sont accessibles directement par l’application hello. Toutefois, lorsque vous hébergez votre application ASP.NET dans le cloud hello, Microsoft Azure n’autorise aucune toobe installé dans hello GAC, donc vous devez vous assurer que les assemblys ReportViewer hello sont disponibles localement pour votre application. Vous pouvez ajouter des références toothem dans votre projet et configurez-les toobe copié localement.

En mode de traitement distant, hello contrôle ReportViewer utilise hello suivant des assemblys :

* **Microsoft.ReportViewer.WebForms.dll**: contient le code hello ReportViewer dont vous avez besoin de toouse ReportViewer dans votre page. Une référence pour cet assembly est ajoutée tooyour projet lorsque vous supprimez un contrôle ReportViewer dans une page ASP.NET dans votre projet.
* **Microsoft.ReportViewer.Common.dll**: contient des classes utilisées par hello contrôle ReportViewer au moment de l’exécution. Il n’est pas automatiquement ajouté tooyour projet.

### <a name="tooadd-a-reference-toomicrosoftreportviewercommon"></a>tooadd un tooMicrosoft.ReportViewer.Common de référence
* Avec le bouton droit de votre projet **références** nœud et sélectionnez **ajouter une référence**, sélectionnez l’assembly hello dans l’onglet .NET de hello, puis cliquez sur **OK**.

### <a name="toomake-hello-assemblies-locally-accessible-by-your-aspnet-application"></a>assemblys de hello toomake localement accessibles par votre application ASP.NET
1. Bonjour **références** dossier, cliquez sur assembly Microsoft.ReportViewer.Common de hello afin que ses propriétés s’affichent dans le volet de propriétés hello.
2. Dans le volet de propriétés hello, définissez **copie locale** tooTrue.
3. Répétez les étapes 1 et 2 pour Microsoft.ReportViewer.WebForms.

### <a name="tooget-reportviewer-language-pack"></a>tooget linguistique ReportViewer
1. Installer hello Microsoft Report Viewer 2012 Runtime redistributable package approprié à partir de [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=317386).
2. Langage hello SELECT à partir de la liste déroulante de hello et page de hello obtient toohello redirigé page du centre de téléchargement correspondant.
3. Cliquez sur **télécharger** télécharger hello toostart ReportViewerLP.exe.
4. Après avoir téléchargé ReportViewerLP.exe, cliquez sur **exécuter** tooinstall immédiatement, ou cliquez sur **enregistrer** toosave il tooyour ordinateur. Si vous cliquez sur **enregistrer**, n’oubliez pas de nom hello du dossier hello où vous enregistrez le fichier de hello.
5. Recherchez le dossier hello où vous avez enregistré le fichier de hello. Cliquez avec le bouton droit sur ReportViewerLP.exe, cliquez sur **Exécuter en tant qu’administrateur**, puis sur **Oui**.
6. Après avoir exécuté ReportViewerLP.exe, vous verrez hello c:\windows\assembly a des fichiers de ressources hello **Microsoft.ReportViewer.Webforms.Resources** et **Microsoft.ReportViewer.Common.Resources** .

### <a name="tooconfigure-for-localized-reportviewer-control"></a>tooconfigure pour le contrôle ReportViewer localisé
1. Téléchargez et installez le package redistribuable Microsoft Report Viewer 2012 Runtime de hello en hello suivante au-dessus des instructions spécifiées.
2. Créer <language> dossier Bonjour de projet et copiez hello associés il les fichiers d’assembly de ressources. Hello toobe de fichiers d’assembly ressources copiée sont : **Microsoft.ReportViewer.Webforms.Resources.dll** et **Microsoft.ReportViewer.Common.Resources.dll**. Sélectionnez les fichiers d’assembly de ressources hello et dans le volet de propriétés hello, définissez **copier tooOutput active** trop «**toujours copier**».
3. Définir hello Culture et UICulture pour le projet web de hello. Pour plus d’informations sur la façon dont tooset hello Culture et la Culture d’interface utilisateur pour une page Web ASP.NET, consultez [Comment : ensemble hello Culture et la Culture d’interface utilisateur pour la globalisation de Page Web ASP.NET](http://go.microsoft.com/fwlink/?LinkId=237461).

## <a name="configuring-authentication-and-authorization"></a>Configuration de l’authentification et de l’autorisation
Hello ReportViewer doit tooauthenticate des informations d’identification appropriées toouse avec le serveur de rapports hello et informations d’identification hello doivent être autorisées par les rapports hello hello report server tooaccess souhaité. Pour plus d’informations sur l’authentification, consultez le livre blanc hello [serveurs de rapports basé sur les machines virtuelles Microsoft Azure et de contrôle de visionneuse de rapports Reporting Services](https://msdn.microsoft.com/library/azure/dn753698.aspx).

## <a name="publish-hello-aspnet-web-application-tooazure"></a>Publier hello tooAzure d’application Web ASP.NET
Pour obtenir des instructions sur la publication d’un tooAzure d’application Web ASP.NET, consultez [Comment : migrer et publier un tooAzure d’Application Web à partir de Visual Studio](../../../vs-azure-tools-migrate-publish-web-app-to-cloud-service.md) et [prise en main des applications Web et ASP.NET](../../../app-service-web/app-service-web-get-started-dotnet.md).

> [!IMPORTANT]
> Si hello commande Ajouter un projet de déploiement Azure ou ajouter un projet Azure Cloud Service n’apparaît pas dans le menu contextuel de hello dans l’Explorateur de solutions, vous devrez peut-être toochange hello cible de .NET framework pour hello projet too.NET Framework 4.
> 
> Hello deux commandes fournissent essentiellement hello les mêmes fonctionnalités. Un ou hello autre commande apparaîtra dans le menu contextuel de hello, selon la version de hello Microsoft Azure SDK, vous avez installé.
> 
> 

## <a name="resources"></a>Ressources
[Rapports Microsoft](http://go.microsoft.com/fwlink/?LinkId=205399)

[Business Intelligence de SQL Server dans les machines virtuelles Azure](../classic/ps-sql-bi.md)

[Utilisez PowerShell tooCreate un Azure VM avec un serveur en Mode natif rapport](../classic/ps-sql-report.md)

