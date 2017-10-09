---
title: journalisation des diagnostics aaaEnable pour les applications web dans Azure App Service
description: "Découvrez comment tooenable journalisation des diagnostics et ajouter une application de tooyour instrumentation, ainsi que la manière dont tooaccess hello informations consignées par Azure."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: c9da27b2-47d4-4c33-a3cb-1819955ee43b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2016
ms.author: cephalin
ms.openlocfilehash: 4b2903ff31cc93180552cf51196c33505ffbaf07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-logging-for-web-apps-in-azure-app-service"></a>Activer la journalisation des diagnostics pour les applications web dans Azure App Service
## <a name="overview"></a>Vue d'ensemble
Azure fournit tooassist diagnostics intégrés avec débogage un [application web App Service](http://go.microsoft.com/fwlink/?LinkId=529714). Dans cet article, vous allez apprendre comment tooenable journalisation des diagnostics et ajouter une application de tooyour instrumentation, ainsi que la manière dont tooaccess hello informations consignées par Azure.

Cet article utilise hello [Azure Portal](https://portal.azure.com), Azure PowerShell et toowork d’Interface de ligne de commande de Azure (Azure CLI) hello avec les journaux de diagnostic. Pour plus d’informations sur l’utilisation de journaux de diagnostic avec Visual Studio, consultez [Résolution des problèmes Azure dans Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="whatisdiag"></a>Diagnostics de serveur Web et diagnostics d’application
Applications de Service d’applications web fournissent des fonctionnalités de diagnostic enregistrées les informations de serveur web de hello et application web de hello. Ces informations sont réparties, en toute logique, en **diagnostics de serveur web** et en **diagnostics d’application**.

### <a name="web-server-diagnostics"></a>Diagnostics de serveur web
Vous pouvez activer ou désactiver hello suivant les types de journaux :

* **Messages d’erreur détaillés** : informations d’erreur détaillées pour les codes d’état HTTP qui indiquent un échec (code d’état 400 ou supérieur). Il peut contenir des informations qui peuvent aider à déterminer pourquoi les serveur hello a renvoyé un code d’erreur hello.
* **Échec de l’outil suivi des demandes** -des informations détaillées sur les demandes ayant échoué, y compris une trace de hello IIS composants utilisés tooprocess hello demande et de durée hello dans chaque composant. Cela peut être utile si vous essayez de performances de site tooincrease ou Isolez la cause une toobe d’erreur HTTP spécifique retourné.
* **Journalisation du serveur Web** -informations sur les transactions HTTP à l’aide de hello [format de fichier journal étendu W3C](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx). Cela est utile lors de la détermination des métriques d’un site global comme nombre hello de demandes traitées ou nombre de requêtes qui proviennent d’une adresse IP spécifique.

### <a name="application-diagnostics"></a>diagnostics d’application
Application diagnostics vous permet de toocapture les informations produites par une application web. Applications ASP.NET peuvent utiliser hello [System.Diagnostics.Trace](http://msdn.microsoft.com/library/36hhw2t6.aspx) classe toolog informations toohello application diagnostics se connecter. Par exemple :

    System.Diagnostics.Trace.TraceError("If you're seeing this, something bad happened");

Lors de l’exécution, vous pouvez récupérer ces toohelp journaux de résolution des problèmes. Pour plus d’informations, consultez la page [Résolution des problèmes des applications web Azure dans Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md).

Applications de Service d’applications web également enregistrer les informations relatives au déploiement que lorsque vous publiez l’application web de contenu tooa. Cela est effectué automatiquement et il n'existe aucun paramètre de configuration pour la journalisation du déploiement. Journalisation de déploiement vous permet de toodetermine pourquoi un déploiement a échoué. Par exemple, si vous utilisez un script de déploiement personnalisé, vous pouvez utiliser toodetermine de journalisation de déploiement pourquoi hello script échoue.

## <a name="enablediag"></a>Comment tooenable diagnostics
diagnostics tooenable Bonjour [Azure Portal](https://portal.azure.com), accédez panneau toohello pour votre application web, cliquez sur **Paramètres > journaux de diagnostic**.

<!-- todo:cleanup dogfood addresses in screenshot -->
![Partie des journaux](./media/web-sites-enable-diagnostic-log/logspart.png)

Lorsque vous activez **diagnostics d’application** vous choisissez également hello **niveau**. Ce paramètre vous permet de toofilter hello informations trop**d’information**, **avertissement** ou **erreur** plus d’informations. La définition de cette trop**verbose** enregistre les informations de tous les produits par l’application hello.

> [!NOTE]
> Contrairement à la modification du fichier web.config de hello fichier, l’activation des diagnostics de l’Application ou la modification des niveaux de journalisation de diagnostic n’est pas recyclé domaine d’application hello application hello s’exécutant dans.
>
>

Bonjour [portail classique](https://manage.windowsazure.com) application Web **configurer** onglet, vous pouvez sélectionner **stockage** ou **système de fichiers** pour **serveur web journalisation**. En sélectionnant **stockage** vous permet de tooselect un compte de stockage, puis un conteneur d’objets blob pour les journaux de hello seront conservés. Tous les autres journaux pour **diagnostics de site** sont écrites toohello le système de fichiers uniquement.

Hello [portail classique](https://manage.windowsazure.com) application Web **configurer** onglet comprend également des paramètres supplémentaires pour application diagnostics :

* **Système de fichiers** -magasins hello de système de fichiers application diagnostics informations toohello web app. Ces fichiers peuvent être accédées par FTP, ou téléchargés sous la forme d’une archive Zip à l’aide de hello Azure PowerShell ou l’Interface de ligne de commande de Azure (Azure CLI).
* **Stockage de table** -magasins hello des informations de diagnostic d’application par le nom de compte de stockage Azure et de table spécifié hello.
* **Stockage d’objets BLOB** -magasins hello des informations de diagnostics de l’application dans le conteneur spécifié de compte de stockage Azure et blob hello.
* **Période de rétention** : par défaut, les journaux ne sont pas automatiquement supprimés du **Stockage Blob**. Sélectionnez **de rétention définie est** et entrez le nombre de hello de jours pendant lesquels les journaux tookeep si vous le souhaitez tooautomatically supprimer les journaux.

> [!NOTE]
> Si vous [régénérer les clés d’accès de votre compte de stockage](../storage/common/storage-create-storage-account.md), vous devez réinitialiser les clés de hello journalisation respectifs configuration toouse hello mis à jour. toodo cela :
>
> 1. Bonjour **configurer** onglet, définissez trop de fonctionnalité de journalisation respectifs de hello**hors**. Enregistrez votre paramètre.
> 2. Activer la journalisation toohello stockage compte blob ou table à nouveau. Enregistrez votre paramètre.
>
>

N’importe quelle combinaison de système de fichiers, de stockage de table ou de stockage d’objets blob peut être activé à hello en même temps et ont des configurations au niveau de journal. Par exemple, vous souhaiterez avertissements et erreurs de toolog tooblob stockage comme une solution de journalisation à long terme, tout en activant la journalisation du système de fichiers avec un niveau de commentaires.

Tandis que les trois emplacements de stockage fournissent hello mêmes informations de base pour les événements enregistrés, **stockage de table** et **stockage d’objets blob** consigner des informations supplémentaires telles que l’ID d’instance hello, ID de thread et plus horodatage précis (format de battement) à celui de la journalisation trop**système de fichiers**.

> [!NOTE]
> Les informations stockées dans le **stockage table** ou le **stockage blob** ne sont accessibles qu’à l’aide d’un client de stockage ou d’une application capable d’utiliser directement ces systèmes de stockage. Par exemple, Visual Studio 2013 contient un Explorateur de stockage qui peuvent être de stockage de table ou un objet blob utilisé tooexplore et HDInsight permettre accéder aux données stockées dans le stockage d’objets blob. Vous pouvez également écrire une application qui accède au stockage Azure à l’aide d’une des hello [kits de développement logiciel Azure](/downloads/#).
>
> [!NOTE]
> Diagnostics peut également être activées à partir d’Azure PowerShell à l’aide de hello **Set-AzureWebsite** applet de commande. Si vous n’avez pas installé Azure PowerShell ou que vous le n'avez pas configuré toouse votre abonnement Azure, consultez [comment tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).
>
>

## <a name="download"></a> Téléchargement de journaux
Système de fichiers des informations de diagnostic stockées toohello web application est accessible directement à l’aide de FTP. Il peut aussi être téléchargé en tant qu’une archive Zip à l’aide d’Azure PowerShell ou hello Interface de ligne de commande de Azure.

structure de répertoires Hello hello journaux sont stockés dans est la suivante :

* **Journaux d'application** : /LogFiles/Application/. Ce dossier contient un ou plusieurs fichiers texte contenant des informations générées dans le cadre de la journalisation des applications.
* **Suivi des demandes ayant échoué** : /LogFiles/W3SVC#########/. Ce dossier contient un fichier XSL et un ou plusieurs fichiers XML. Assurez-vous de télécharger le fichier XSL de hello en hello même répertoire que hello que fichier (s) XML, car le fichier XSL de hello fournit des fonctionnalités de mise en forme et le filtrage de contenu hello Hello XML fichier (s) lors de son affichage dans Internet Explorer.
* **Journaux d'erreurs détaillés** : /LogFiles/DetailedErrors/. Ce dossier contient un ou plusieurs fichiers .htm fournissant des informations détaillées sur toute erreur HTTP qui s'est produite.
* **Journaux des serveurs Web** : /LogFiles/http/RawLogs. Ce dossier contient un ou plusieurs fichiers de texte formatés à l’aide de hello [format de fichier journal étendu W3C](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).
* **Journaux de déploiement** : /LogFiles/Git. Ce dossier contient les journaux générés par les processus de déploiement interne hello utilisés par les applications web Azure, ainsi que les journaux pour les déploiements Git.

### <a name="ftp"></a>FTP
tooaccess des informations de diagnostic à l’aide de FTP, visitez hello **tableau de bord** de votre application web Bonjour [portail classic](https://manage.windowsazure.com). Bonjour **coup de œil rapide** section, utilisez hello **journaux de Diagnostic FTP** lier les fichiers de journaux hello tooaccess à l’aide de FTP. Hello **utilisateur déploiement/FTP** entrée indique le nom d’utilisateur hello qui doit être utilisé tooaccess hello FTP site.

> [!NOTE]
> Si hello **utilisateur déploiement/FTP** entrée n’est pas définie, ou vous avez oublié le mot de passe hello pour cet utilisateur, vous pouvez créer un nouvel utilisateur et un mot de passe à l’aide de hello **réinitialiser les informations d’identification de déploiement** lien Bonjour **coup de œil rapide** section Hello **tableau de bord**.
>
>

### <a name="download-with-azure-powershell"></a>Téléchargement avec Azure PowerShell
fichiers toodownload hello, démarrez une nouvelle instance d’Azure PowerShell et utilisez hello de commande suivante :

    Save-AzureWebSiteLog -Name webappname

Cette action va enregistrer les journaux hello pour l’application web de hello spécifié par hello **-nom** fichier tooa de paramètre nommé **logs.zip** hello répertoire en cours.

> [!NOTE]
> Si vous n’avez pas installé Azure PowerShell ou que vous le n'avez pas configuré toouse votre abonnement Azure, consultez [comment tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).
>
>

### <a name="download-with-azure-command-line-interface"></a>Téléchargement avec l’interface de ligne de commande Azure
journaux toodownload hello à l’aide de hello Interface de ligne de commande Azure, ouvrez une nouvelle invite de commandes, PowerShell, un interpréteur de commandes ou une session Terminal Server, puis entrez hello de commande suivante :

    azure site log download webappname

Cette action va enregistrer les journaux hello pour l’application web de hello nommé 'webappname' tooa nommé **diagnostics.zip** hello répertoire en cours.

> [!NOTE]
> Si vous n’avez pas installé hello Azure Interface de ligne (Azure), ou le n'avez pas configuré toouse votre abonnement Azure, consultez [comment tooUse CLI d’Azure](../cli-install-nodejs.md).
>
>

## <a name="how-to-view-logs-in-application-insights"></a>Affichage des journaux dans Application Insights
Visual Studio Application Insights fournit des outils de filtrage et de recherche de journaux et pour la corrélation des journaux de hello avec les requêtes et d’autres événements.

1. Ajouter un projet de tooyour Application Insights SDK hello dans Visual Studio.
   * Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet, puis sélectionnez Ajouter Application Insights. Vous serez guidé tout au long de la création de la ressource Application Insights. [En savoir plus](../application-insights/app-insights-asp-net.md)
2. Ajoutez le package tooyour projet hello écouteur de suivi.
   * Cliquez avec le bouton droit sur votre projet et choisissez Gérer les packages NuGet. Sélectionnez `Microsoft.ApplicationInsights.TraceListener` [En savoir plus](../application-insights/app-insights-asp-net-trace-logs.md)
3. Téléchargez votre projet et l’exécuter toogenerate les données de journal.
4. Bonjour [Azure Portal](https://portal.azure.com/), accédez tooyour ressource Application Insights et **recherche**. Vous pouvez voir vos données de journal, ainsi que la requête, l’utilisation et les autres mesures de télémétrie. Certaines données de télémétrie peuvent prendre quelques minutes tooarrive : cliquez sur Actualiser. [En savoir plus](../application-insights/app-insights-diagnostic-search.md)

[En savoir plus sur le suivi des performances avec Application Insights](../application-insights/app-insights-azure-web-apps.md)

## <a name="streamlogs"></a> Diffusion en continu des journaux
Lors du développement d’une application, il est souvent utile toosee les informations de journalisation dans quasiment en temps réel. Cela est possible en environnement de développement tooyour informations journalisation à l’aide d’Azure PowerShell ou hello Azure une Interface de ligne de la diffusion en continu.

> [!NOTE]
> Certains types de mémoire tampon de journalisation d’écrire le fichier de journal toohello, ce qui peut entraîner des événements en désordre dans le flux de hello. Par exemple, une entrée de journal d’application qui se produit lorsqu’un utilisateur visite une page peut affichera dans le flux hello avant l’entrée de journal HTTP correspondante hello pour la demande de page hello.
>
> [!NOTE]
> Journal de diffusion en continu sera également transmettre en continu informations écrites tooany fichier de texte stocké dans hello **D:\\domestique\\LogFiles\\**  dossier.
>
>

### <a name="streaming-with-azure-powershell"></a>Diffusion d'informations en continu avec Azure PowerShell
informations de journalisation de toostream, démarrez une nouvelle instance d’Azure PowerShell et utilisez les hello de commande suivante :

    Get-AzureWebSiteLog -Name webappname -Tail

Cela se connecte à l’application web toohello spécifiée par hello **-nom** paramètre et commencer la diffusion en continu de fenêtre de PowerShell toohello informations comme le journal des événements se produisent sur l’application web hello. Toutes les informations écrites toofiles se terminant par .txt, .log ou .htm qui sont stockés dans le répertoire de /LogFiles hello (accueil/d:/logfiles) seront diffusées console locale de toohello.

toofilter des événements spécifiques, telles que les erreurs, utilisent hello **-Message** paramètre. Par exemple :

    Get-AzureWebSiteLog -Name webappname -Tail -Message Error

les types de journaux spécifiques de toofilter, tels que HTTP, utilisent hello **-chemin d’accès** paramètre. Par exemple :

    Get-AzureWebSiteLog -Name webappname -Tail -Path http

toosee une liste de chemins d’accès disponibles, utilisez hello - ListPath paramètre.

> [!NOTE]
> Si vous n’avez pas installé Azure PowerShell ou que vous le n'avez pas configuré toouse votre abonnement Azure, consultez [comment tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).
>
>

### <a name="streaming-with-azure-command-line-interface"></a>Diffusion d’informations en continu avec l’interface de ligne de commande Azure
les informations de journalisation toostream, ouvrez une nouvelle invite de commandes, PowerShell, un interpréteur de commandes ou une session Terminal Server, puis entrez hello de commande suivante :

    azure site log tail webappname

Cela se connecter à l’application web toohello nommée « webappname » et commencer la diffusion en continu de la fenêtre toohello d’informations comme le journal des événements se produisent sur l’application web hello. Toutes les informations écrites toofiles se terminant par .txt, .log ou .htm qui sont stockés dans le répertoire de /LogFiles hello (accueil/d:/logfiles) seront diffusées console locale de toohello.

toofilter des événements spécifiques, telles que les erreurs, utilisent hello **--filtre** paramètre. Par exemple :

    azure site log tail webappname --filter Error

les types de journaux spécifiques de toofilter, tels que HTTP, utilisent hello **: chemin d’accès** paramètre. Par exemple :

    azure site log tail webappname --path http

> [!NOTE]
> Si vous n’avez pas installé hello Interface de ligne de commande de Azure, ou le n'avez pas configuré toouse votre abonnement Azure, consultez [comment tooUse Interface de ligne de commande Azure](../cli-install-nodejs.md).
>
>

## <a name="understandlogs"></a> Présentation des journaux de diagnostic
### <a name="application-diagnostics-logs"></a>Journaux de diagnostic d'application
Diagnostics de l’application stocke des informations dans un format spécifique pour les applications .NET, selon que vous stockez le système de fichiers journaux toohello, le stockage de table, ou un stockage d’objets blob. jeu de données stockées de base Hello est hello identiques sur tous les trois types de stockage hello date et heure hello événement, ID de processus hello qui a généré le message d’événement hello, type d’événement hello (informations, avertissement, erreur) et d’événements de hello.

**Système de fichiers**

Chaque ligne connecté toohello système de fichiers ou reçus à l’aide de la diffusion en continu sera Bonjour suivant le format :

    {Date}  PID[{process id}] {event type/level} {message}

Par exemple, un événement d’erreur s’affiche semblable toohello suivantes :

    2014-01-30T16:36:59  PID[3096] Error       Fatal error on hello page!

Journalisation du système de fichiers toohello fournit des informations de base de hello de hello trois méthodes disponibles, en fournissant des temps de hello, id de processus, niveau d’événement et message uniquement.

**Stockage Table**

Lors de la connexion de stockage tootable, des propriétés supplémentaires sont utilisé toofacilitate recherche hello les données stockées dans la table de hello, ainsi que des informations plus précises sur les événements hello. Hello propriétés suivantes (colonnes) sont utilisées pour chaque entité (lignes) stockée dans la table de hello.

| Nom de la propriété | Valeur/format |
| --- | --- |
| PartitionKey |Date/heure de l’événement hello Aaaammjjhh format |
| RowKey |Valeur GUID qui identifie cette entité de façon unique |
| Timestamp |Hello date et heure hello événement s’est produite |
| EventTickCount |Hello date et heure hello événement s’est produite, dans le format de battement (précision supérieure) |
| ApplicationName |nom de l’application Hello web |
| Level |Niveau d'événement (erreur, avertissement ou information, par exemple) |
| EventId |ID d’événement Hello de cet événement<p><p>Par défaut too0 si aucun n’est spécifié |
| InstanceId |Instance de l’application web hello hello même s’est produite sur |
| Pid |ID du processus |
| Tid |Hello ID de thread de hello qui a produit l’événement de hello |
| Message |Message détaillé sur l'événement |

**Stockage d’objets blob**

Quand vous vous connectez tooblob stockage, les données sont stockées au format de valeurs séparées par des virgules (CSV). Stockage de tootable similaire, des champs supplémentaires sont journalisée tooprovide des informations plus précises sur l’événement hello. Hello propriétés suivantes sont utilisées pour chaque ligne de hello CSV :

| Nom de la propriété | Valeur/format |
| --- | --- |
| Date |Hello date et heure hello événement s’est produite |
| Level |Niveau d'événement (erreur, avertissement ou information, par exemple) |
| ApplicationName |nom de l’application Hello web |
| InstanceId |Instance de l’application web hello qui hello événement s’est produite sur |
| EventTickCount |Hello date et heure hello événement s’est produite, dans le format de battement (précision supérieure) |
| EventId |ID d’événement Hello de cet événement<p><p>Par défaut too0 si aucun n’est spécifié |
| Pid |ID du processus |
| Tid |Hello ID de thread de hello qui a produit l’événement de hello |
| Message |Message détaillé sur l'événement |

données Hello stockées dans un objet blob serait similaire toohello suivantes :

    date,level,applicationName,instanceId,eventTickCount,eventId,pid,tid,message
    2014-01-30T16:36:52,Error,mywebapp,6ee38a,635266966128818593,0,3096,9,An error occurred

> [!NOTE]
> Hello première ligne du journal de hello contiendra alors des en-têtes de colonne hello comme représenté dans cet exemple.
>
>

### <a name="failed-request-traces"></a>Suivi des demandes ayant échoué
Le suivi des demandes ayant échoué est stocké dans des fichiers XML nommés **fr######.xml**. toomake il plus facile d’informations hello connecté tooview, une feuille de style XSL nommé **freb.xsl** est fourni dans hello même répertoire comme hello des fichiers XML. Ouverture d’un des fichiers XML de hello dans Internet Explorer utilise tooprovide de feuille de style XSL hello affichage mis en forme des informations de trace hello. Cela apparaîtra similaire toohello suivantes :

![demandes ayant échoué dans hello navigateur](./media/web-sites-enable-diagnostic-log/tws-failedrequestinbrowser.png)

### <a name="detailed-error-logs"></a>Journaux d'erreurs détaillés
Les journaux d'erreurs détaillés sont des documents HTML qui fournissent des informations plus détaillées sur les erreurs HTTP qui se sont produites. Puisqu'il s'agit simplement de documents HTML, ils peuvent être consultés à l'aide d'un navigateur Web.

### <a name="web-server-logs"></a>Journaux des serveurs Web
Hello journaux du serveur web sont mis en forme à l’aide de hello [format de fichier journal étendu W3C](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx). Ces informations peuvent être lues à l'aide d'un éditeur de texte ou analysées à l'aide d'utilitaires tels que [Log Parser](http://go.microsoft.com/fwlink/?LinkId=246619).

> [!NOTE]
> Hello journaux générés par les applications web Azure ne prennent pas charge hello **s-computername**, **s-ip**, ou **cs-version** champs.
>
>

## <a name="nextsteps"></a> Étapes suivantes
* [Comment tooMonitor les applications Web](http://docs.microsoft.com/en-us/azure/app-service-web/web-sites-monitor)
* [Résolution des problèmes des applications web Azure dans Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md)
* [Analyse des journaux d’application Web dans HDInsight (en anglais)](http://gallery.technet.microsoft.com/scriptcenter/Analyses-Windows-Azure-web-0b27d413)

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
>
>

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)
* Pour un toohello guide consultez Modification de l’ancien portail du nouveau portail toohello hello : [référence pour parcourir les hello portail Azure](http://go.microsoft.com/fwlink/?LinkId=529715)
