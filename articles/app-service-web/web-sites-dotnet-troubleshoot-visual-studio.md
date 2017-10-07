---
title: "aaaTroubleshoot une application web dans Azure App Service à l’aide de Visual Studio"
description: "Découvrez comment tootroubleshoot une application web Azure à l’aide de débogage distant, suivi et de journalisation des outils qui sont générés dans tooVisual Studio 2013."
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: 
ms.assetid: def8e481-7803-4371-aa55-64025d116c97
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/29/2016
ms.author: rachelap
ms.openlocfilehash: 8e3a8a58293f2ebcdc131fbf2534f8ff99b26730
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-web-app-in-azure-app-service-using-visual-studio"></a>Dépanner une application web dans le Service d’application Microsoft Azure à l’aide de Visual Studio
## <a name="overview"></a>Vue d'ensemble
Ce didacticiel montre comment les outils de Visual Studio toouse qui aident à déboguer une application web [du Service d’applications](http://go.microsoft.com/fwlink/?LinkId=529714), en exécutant dans [mode débogage](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) à distance ou en consultant les journaux des applications et les journaux du serveur web.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

Vous apprendrez ce qui suit :

* quelles sont les fonctions de gestion d’application web Microsoft Azure proposées par Visual Studio ;
* Comment à distance de Visual Studio toouse afficher toomake rapides modifications dans une application web à distance.
* Comment toorun en mode de débogage à distance lors d’un projet est en cours d’exécution dans Azure, à la fois pour une application web et une tâche Web.
* Comment les applications toocreate journaux de suivi et de les afficher lors de l’application hello est leur création.
* Comment les journaux du serveur web tooview, y compris les messages d’erreur détaillés et suivi de la requête ayant échoué.
* Comment toosend diagnostic enregistre le compte de stockage Azure tooan et il les afficher.

Si vous disposez de Visual Studio Ultimate, vous pouvez également utiliser [IntelliTrace](http://msdn.microsoft.com/library/vstudio/dd264915.aspx) à des fins de débogage. IntelliTrace n’est pas couvert dans ce didacticiel.

## <a name="prerequisites"></a>Configuration requise
Ce didacticiel fonctionne avec l’environnement de développement hello, projet web et application web Azure que vous avez configurée dans [prise en main Azure et ASP.NET][GetStarted]. Pour les sections de tâches Web hello, vous devez application hello que vous créez dans [prise en main hello Kit de développement logiciel Azure WebJobs][GetStartedWJ].

code Hello exemples indiqués dans ce didacticiel sont destinés à une application web de MVC c#, mais hello des procédures de dépannage sont hello même pour les applications Visual Basic et les Web Forms.

Hello est supposé à l’aide de Visual Studio 2015 ou 2013. Si vous utilisez Visual Studio 2013, hello tâches Web requièrent [mise à jour 4](http://go.microsoft.com/fwlink/?LinkID=510314) ou version ultérieure.

journaux de diffusion en continu Hello fonctionnalité fonctionne uniquement pour les applications qui ciblent .NET Framework 4 ou version ultérieure.

## <a name="sitemanagement"></a>Gestion et configuration de l’application Web
Visual Studio fournit le sous-ensemble de tooa d’accès de fonctions de gestion hello web app et les paramètres de configuration disponibles dans hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715). Cette section présente les éléments disponibles en cas d’utilisation de l’ **Explorateur de serveurs**. tester les dernières fonctionnalités d’intégration d’Azure des hello de toosee, **Cloud Explorer** également. Vous pouvez ouvrir les deux fenêtres de hello **vue** menu.

1. Si vous n’êtes pas déjà connecté tooAzure dans Visual Studio, cliquez sur hello **connecter tooAzure** situé dans **l’Explorateur de serveurs**.

    Une autre solution consiste à tooinstall un certificat de gestion active tooyour compte d’accès. Si vous choisissez tooinstall un certificat, cliquez sur hello **Azure** nœud **l’Explorateur de serveurs**, puis cliquez sur **gérer et filtrer les abonnements** dans le menu contextuel de hello. Bonjour **gérer les abonnements Azure** boîte de dialogue, cliquez sur hello **certificats** onglet, puis cliquez sur **importation**. Suivez toodownload de directions hello, puis importer un fichier d’abonnement (également appelé un *.publishsettings* fichier) pour votre compte Azure.

   > [!NOTE]
   > Si vous téléchargez un fichier d’abonnement, enregistrez-le dossier tooa en dehors de vos répertoires de code source (par exemple, dans le dossier Téléchargements de hello) et le supprimer puis une fois l’importation hello est terminée. Un utilisateur malveillant qui réussit le fichier d’abonnement accès toohello peut modifier, créer et supprimer vos services Azure.
   >
   >

    Pour plus d’informations sur la connexion des ressources de tooAzure à partir de Visual Studio, consultez [gérer les comptes, les abonnements et les rôles d’administrateur](http://go.microsoft.com/fwlink/?LinkId=324796#BKMK_AccountVCert).
2. Dans l’**Explorateur de serveurs**, développez **Azure**, puis **App Service**.
3. Développez le groupe de ressources hello qui inclut l’application hello web que vous avez créé dans [prise en main d’Azure et ASP.NET][GetStarted], puis cliquez sur le nœud d’application web hello et cliquez sur **paramètresd’affichage**.

    ![Afficher les paramètres dans l'Explorateur de serveurs](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewsettings.png)

    Hello **application Web Azure** onglet s’affiche et vous pouvez voir hello il les tâches de gestion et la configuration d’application web qui sont disponibles dans Visual Studio.

    ![Fenêtre Application web Microsoft Azure](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configtab.png)

    Dans ce didacticiel vous allez utiliser la journalisation hello et les zones déroulantes le suivi. Vous allez également utiliser le débogage distant, mais vous allez utiliser une autre méthode tooenable il.

    Pour plus d’informations à propos des zones de chaînes de connexion et les paramètres de l’application hello dans cette fenêtre, consultez [Azure Web Apps : manière dont les chaînes d’Application et de travail des chaînes de connexion](http://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).

    Si vous souhaitez tooperform une tâche de gestion d’application web qui ne peut pas être effectuée dans cette fenêtre, cliquez sur **ouvrir dans le portail de gestion** tooopen un toohello de fenêtre de navigateur portail Azure.

## <a name="remoteview"></a>Accès aux fichiers d’applications Web dans l’Explorateur de serveurs
Vous déployez en général d’un projet web avec hello `customErrors` indicateur Bonjour ensemble de fichiers Web.config trop`On` ou `RemoteOnly`, ce qui signifie que vous n’obtenez pas un message d’erreur utile lorsqu’un problème survient. Pour de nombreuses erreurs vous récupérer qu’une page comme hello ceux suivant.

**Erreur de serveur dans l’application « / » :**

![Page d’erreur inutile](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror.png)

**Nous avons rencontré une erreur :**

![Page d’erreur inutile](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror1.png)

**site Web de Hello ne peut pas afficher la page de hello**

![Page d’erreur inutile](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror2.png)

Hello plus simple façon toofind hello cause de hello erreur est souvent tooenable des messages d’erreur détaillés qui hello premier Hello précédant les captures d’écran explique comment toodo. Qui requiert qu'une modification de hello déployé le fichier Web.config. Vous pouvez modifier hello *Web.config* de fichier dans le projet de hello et redéployer hello projet ou de créer un [transformation Web.config](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) et déployer une version debug, mais il existe un moyen plus rapide : dans **Solution Explorer** vous pouvez directement afficher et modifier des fichiers dans l’application web à distance de hello, à l’aide de hello *vue distante* fonctionnalité.

1. Dans **l’Explorateur de serveurs**, développez **Azure**, développez **du Service d’applications**, développez le groupe de ressources hello que votre application web se trouve dans, puis développez le nœud hello pour votre application web.

    Vous consultez des nœuds qui vous donnent les fichiers de contenu et les fichiers journaux de l’application web accès toohello.
2. Développez hello **fichiers** nœud, puis double-cliquez sur hello *Web.config* fichier.

    ![Ouvrir Web.config](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfig.png)

    Visual Studio ouvre le fichier Web.config de hello à partir de l’application web à distance de hello et montre [distant] nom de fichier toohello suivant dans la barre de titre hello.
3. Ajouter hello suivant ligne toohello `system.web` élément :

    `<customErrors mode="Off"></customErrors>`

    ![Modifier Web.config](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfigedit.png)
4. Actualiser le navigateur hello qui affiche le message d’erreur inutile hello et maintenant, vous obtenez un message d’erreur détaillé, par exemple hello l’exemple suivant :

    ![Messages d’erreur détaillés](./media/web-sites-dotnet-troubleshoot-visual-studio/detailederror.png)

    (erreur hello indiqué a été créé en ajoutant la ligne hello indiqué en rouge trop*Views\Home\Index.cshtml*.)

Modification du fichier Web.config hello n'est qu’un exemple de scénarios dans quelle capacité hello tooread et modifier des fichiers sur votre application web Azure faciliter le dépannage.

## <a name="remotedebug"></a>Débogage à distance des applications Web
Si le message d’erreur détaillé hello ne fournit pas suffisamment d’informations, et vous ne pouvez pas recréer erreur hello localement, une autre façon tootroubleshoot est toorun en mode débogage à distance. Vous pouvez définir des points d’arrêt, manipuler directement de mémoire, parcourir le code et même modifier le chemin d’accès du code hello.

Le débogage à distance ne fonctionne pas avec les éditions Express de Visual Studio.

Cette section montre comment toodebug à distance à l’aide de hello project vous créez dans [prise en main d’Azure et ASP.NET][GetStarted].

1. Projet ouvert hello web que vous avez créé dans [prise en main d’Azure et ASP.NET][GetStarted].
2. Ouvrez *Controllers\HomeController.cs*.
3. Supprimer hello `About()` (méthode) et suivant de hello d’insertion de code à la place.

        public ActionResult About()
        {
            string currentTime = DateTime.Now.ToLongTimeString();
            ViewBag.Message = "hello current time is " + currentTime;
            return View();
        }
4. [Définir un point d’arrêt](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) sur hello `ViewBag.Message` ligne.
5. Dans **l’Explorateur de solutions**, cliquez sur le projet de hello, puis cliquez sur **publier**.
6. Bonjour **profil** liste déroulante, sélectionnez hello même profil que vous avez utilisée dans [prise en main d’Azure et ASP.NET][GetStarted].
7. Cliquez sur hello **paramètres** onglet et modifier **Configuration** trop**déboguer**, puis cliquez sur **publier**.

    ![Publier en mode débogage](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-publishdebug.png)
8. Après le déploiement terminé et votre navigateur s’ouvre, toohello URL Azure de votre application web, navigateur de fermer hello.
9. Dans l’**Explorateur de serveurs**, cliquez avec le bouton droit sur votre application web, puis cliquez sur **Attacher le débogueur**.

    ![Attacher le débogueur](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-attachdebugger.png)

    navigateur de Hello s’ouvre automatiquement la page d’accueil tooyour s’exécutant dans Azure. Peut avoir toowait 20 secondes ou par conséquent, tandis que Azure configure serveur hello pour le débogage. Ce retard produit uniquement hello première fois que vous exécutez en mode débogage sur une application web. Pour les fois suivantes au sein de hello 48 heures lorsque vous redémarrez le débogage il ne sont pas un délai.

    **Remarque :** si vous avez des problèmes pour démarrer le débogueur de hello, essayez toodo à l’aide de **Cloud Explorer** au lieu de **l’Explorateur de serveurs**.
10. Cliquez sur **sur** dans le menu de hello.

     Visual Studio s’arrête sur le point d’arrêt hello et code de hello s’exécute dans Azure, pas sur votre ordinateur local.
11. Placez le curseur sur hello `currentTime` valeur d’heure toosee variable hello.

     ![Afficher une variable en mode débogage sur Azure](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugviewinwa.png)

     fois que vous voyez Hello est heure du serveur Azure hello qui se trouve dans un fuseau horaire différent de votre ordinateur local.
12. Entrez une nouvelle valeur pour hello `currentTime` variable, par exemple « En cours d’exécution dans Azure ».
13. Appuyez sur F5 les toocontinue en cours d’exécution.

     Hello sur la page en cours d’exécution dans Azure affiche hello nouvelle valeur que vous avez entré dans la variable de currentTime hello.

     ![Page « À propos de » avec une nouvelle valeur](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugchangeinwa.png)

## <a name="remotedebugwj"></a> Débogage à distance de WebJobs
Cette section montre comment toodebug à distance à l’aide de hello projet et l’application web que vous créez dans [prise en main hello Azure WebJobs SDK](websites-dotnet-webjobs-sdk.md).

fonctionnalités de Hello présentées dans cette section sont uniquement disponibles dans Visual Studio 2013 avec Update 4 ou version ultérieure.

Le débogage à distance fonctionne uniquement avec les tâches Web en continu. Les tâches Web planifiées et à la demande ne prennent pas en charge le débogage.

1. Projet ouvert hello web que vous avez créé dans [prise en main hello Kit de développement logiciel Azure WebJobs][GetStartedWJ].
2. Dans le projet de ContosoAdsWebJob hello, ouvrez *Functions.cs*.
3. [Définir un point d’arrêt](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) sur la première instruction de hello Bonjour `GnerateThumbnail` (méthode).

    ![Définir le point d’arrêt](./media/web-sites-dotnet-troubleshoot-visual-studio/wjbreakpoint.png)
4. Dans **l’Explorateur de solutions**, avec le bouton droit hello web projet (pas hello la tâche Web), puis cliquez sur **publier**.
5. Bonjour **profil** liste déroulante, sélectionnez hello même profil que vous avez utilisée dans [prise en main hello Azure WebJobs SDK](websites-dotnet-webjobs-sdk.md).
6. Cliquez sur hello **paramètres** onglet et modifier **Configuration** trop**déboguer**, puis cliquez sur **publier**.

    Visual Studio déploie hello et projets de la tâche Web et votre navigateur s’ouvre toohello URL Azure de votre application web.
7. Dans l’**Explorateur de serveurs**, développez **Azure > App Service > votre groupe de ressources > WebJobs > Continu**, puis cliquez avec le bouton droit sur **ContosoAdsWebJob**.
8. Cliquez sur **Attacher le débogueur**.

    ![Attacher le débogueur](./media/web-sites-dotnet-troubleshoot-visual-studio/wjattach.png)

    navigateur de Hello s’ouvre automatiquement la page d’accueil tooyour s’exécutant dans Azure. Peut avoir toowait 20 secondes ou par conséquent, tandis que Azure configure serveur hello pour le débogage. Ce retard produit uniquement hello première fois que vous exécutez en mode débogage sur une application web. Hello prochaine fois que vous attachez le débogueur hello sera un délai, si vous le faites dans les 48 heures.
9. Dans le navigateur web hello qui est la page d’accueil Contoso publicités toohello ouvert, créez une nouvelle annonce.

    Création d’une annonce provoque une toobe de message de le file d’attente créé, qui est récupéré par la tâche Web de hello et traité. Lorsque hello WebJobs SDK appelle un message de file d’attente hello fonction tooprocess hello, code de hello accéderont à votre point d’arrêt.
10. Lorsque le débogueur de hello s’arrête au point d’arrêt, vous pouvez examiner et modifier les valeurs des variables pendant l’exécution du programme hello cloud de hello. Bonjour débogueur de hello illustration suivante montre le contenu hello d’objet blobInfo hello qui a été passé à toohello GenerateThumbnail (méthode).

     ![Objet blobInfo dans le débogueur](./media/web-sites-dotnet-troubleshoot-visual-studio/blobinfo.png)
11. Appuyez sur F5 les toocontinue en cours d’exécution.

     Hello GenerateThumbnail méthode termine la création de miniatures de hello.
12. Dans le navigateur de hello, page d’Index actualisation hello et que vous consultez miniature de hello.
13. Dans Visual Studio, appuyez sur MAJ + F5 toostop de débogage.
14. Dans **l’Explorateur de serveurs**, cliquez sur le nœud de ContosoAdsWebJob hello et cliquez sur **affichage tableau de bord**.
15. Connectez-vous avec vos informations d’identification Azure, puis cliquez sur le page toohello toogo hello la tâche Web nom pour votre tâche Web.

     ![Cliquer sur ContosoAdsWebJob](./media/web-sites-dotnet-troubleshoot-visual-studio/clickcaw.png)

     Hello du tableau de bord affiche cette fonction GenerateThumbnail exécutée récemment hello.

     (hello la prochaine fois que vous cliquez sur **affichage tableau de bord**, vous n’avez pas toosign dans et hello navigateur ouvre directement toohello page pour votre tâche Web.)
16. Cliquez sur hello fonction nom toosee plus d’informations sur l’exécution d’une fonction hello.

     ![Détails de la fonction](./media/web-sites-dotnet-troubleshoot-visual-studio/funcdetails.png)

Si votre fonction [a écrit des journaux](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs), vous pouvez cliquer sur **ToggleOutput** toosee les.

## <a name="notes-about-remote-debugging"></a>Notes à propos du débogage à distance
* Nous vous déconseillons d'exécuter le mode débogage en production. Si votre application web de production n’est pas mis à l’échelle des instances de serveur toomultiple, débogage empêchera serveur hello web répond tooother demandes. Si vous le faites plusieurs instances de serveur web, lorsque vous attachez le débogueur toohello vous obtenez une instance aléatoire et que vous n’avez aucun moyen tooensure ce navigateur suivant les demandes sortent toothat instance. En outre, vous généralement ne pouvez pas déployer une tooproduction de build de débogage et les optimisations du compilateur pour les versions release peuvent rendre impossible tooshow que se passe-t-il ligne par ligne dans votre code source. Pour résoudre les problèmes de production, la meilleure ressource est constituée des journaux de suivi d'application et de serveur Web.
* Évitez les arrêts longs aux points d'arrêt avec le débogage à distance. Azure considère qu'un processus arrêté pendant plus de quelques minutes ne répond pas, et l'arrête définitivement.
* Pendant que vous déboguez, hello serveur envoie des données tooVisual Studio, ce qui peut affecter les coûts de bande passante. Pour plus d'informations sur les tarifs de bande passante, consultez les [tarifs Azure](https://azure.microsoft.com/pricing/calculator/).
* Vérifiez que hello `debug` attribut Hello `compilation` élément Bonjour *Web.config* fichier a la valeur tootrue. Il a la valeur tootrue par défaut lorsque vous publiez une configuration de build de débogage.

        <system.web>
          <compilation debug="true" targetFramework="4.5" />
          <httpRuntime targetFramework="4.5" />
        </system.web>
* Si vous trouvez que ce débogueur hello n’est pas à pas dans le code que vous souhaitez toodebug, vous pouvez avoir le paramètre d’uniquement mon Code hello toochange.  Pour plus d’informations, consultez [restreindre l’exécution pas à pas tooJust mon Code](http://msdn.microsoft.com/library/vstudio/y740d9d3.aspx#BKMK_Restrict_stepping_to_Just_My_Code).
* Un minuteur démarre sur le serveur de hello lorsque vous activez la fonctionnalité de débogage distant de hello, et au bout de 48 heures hello est automatiquement décochée. Cette limite de 48 heures a été définie à des fins de sécurité et de performances. Vous pouvez facilement activer la fonctionnalité de hello en autant de fois que vous le souhaitez. Nous vous recommandons de la désactiver lorsque vous n'utilisez pas le débogage.
* Vous pouvez attacher manuellement le processus du débogueur tooany hello, non seulement hello web application processus (w3wp.exe). Pour plus d’informations sur la façon dont toouse mode débogage dans Visual Studio, consultez [débogage dans Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx).

## <a name="logsoverview"></a>Présentation des journaux de diagnostic
Une application ASP.NET qui s’exécute dans une application web Azure permettre créer hello suivant les types de journaux :

* **Journaux de suivi d’application**<br/>
  Hello application crée ces journaux en appelant des méthodes de hello [System.Diagnostics.Trace](http://msdn.microsoft.com/library/system.diagnostics.trace.aspx) classe.
* **Journaux des serveurs web**<br/>
  serveur web de Hello crée une entrée de journal pour chaque demande HTTP toohello l’application web.
* **Journaux détaillés des messages d’erreur**<br/>
  serveur web de Hello crée une page HTML avec des informations supplémentaires pour les requêtes HTTP ayant échoué (celles qui résultent de code d’état 400 ou supérieur).
* **Journaux de suivi de demandes ayant échoué**<br/>
  serveur web de Hello crée un fichier XML avec les informations de suivi détaillées pour les demandes HTTP ayant échouées. serveur web de Hello fournit également un hello XSL tooformat fichier XML dans un navigateur.

Journalisation affecte les performances application web, Azure vous offre hello tooenable de capacité ou de désactiver chaque type de journal en fonction des besoins. Vous pouvez définir un niveau minimal de gravité pour l'écriture des journaux d'application. Lorsque vous créez une application web, la fonction de journalisation est désactivée par défaut.

Toofiles les journaux sont écrits un *LogFiles* dossier hello système de fichiers de votre application web et le sont accessible via FTP. Journaux du serveur Web et les journaux des applications peuvent également être écrites compte de stockage Azure tooan. Vous pouvez conserver un plus grand nombre de journaux dans un compte de stockage que dans le système de fichiers hello. Vous êtes limité tooa au maximum 100 mégaoctets de journaux lorsque vous utilisez le système de fichiers hello. (il ne conserve pas les journaux très longtemps : Azure supprime les anciens fichiers journaux toomake de marge pour les nouveaux après que hello limite est atteinte.)  

## <a name="apptracelogs"></a>Création et affichage des journaux de suivi d’application
Dans cette section, vous effectuerez hello tâche suivantes :

* Ajouter le suivi les instructions toohello projet web que vous avez créé dans [prise en main Azure et ASP.NET][GetStarted].
* Afficher les journaux hello lorsque vous exécutez le projet de hello localement.
* Afficher les journaux de hello comme ils sont générés par l’application hello s’exécutant dans Azure.

Pour plus d’informations sur comment toocreate application consigne dans les tâches Web, consultez [comment toowork avec stockage de la file d’attente Azure à l’aide hello WebJobs SDK - mode toowrite de journalisation des](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs). Hello les instructions suivantes pour l’affichage des journaux et de contrôler la façon dont elles sont stockées dans Azure s’appliquent également les journaux tooapplication créés par les tâches Web.

### <a name="add-tracing-statements-toohello-application"></a>Ajouter une application de toohello instructions de traçage
1. Ouvrez *Controllers\HomeController.cs*et remplacez hello `Index`, `About`, et `Contact` méthodes avec hello suivant de code dans l’ordre tooadd `Trace` instructions et un `using` instruction pour `System.Diagnostics`:

        public ActionResult Index()
        {
            Trace.WriteLine("Entering Index method");
            ViewBag.Message = "Modify this template toojump-start your ASP.NET MVC application.";
            Trace.TraceInformation("Displaying hello Index page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Index method");
            return View();
        }

        public ActionResult About()
        {
            Trace.WriteLine("Entering About method");
            ViewBag.Message = "Your app description page.";
            Trace.TraceWarning("Transient error on hello About page at " + DateTime.Now.ToShortTimeString());
            Trace.WriteLine("Leaving About method");
            return View();
        }

        public ActionResult Contact()
        {
            Trace.WriteLine("Entering Contact method");
            ViewBag.Message = "Your contact page.";
            Trace.TraceError("Fatal error on hello Contact page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Contact method");
            return View();
        }        
2. Ajouter un `using System.Diagnostics;` haut de toohello d’instruction de fichier de hello.

### <a name="view-hello-tracing-output-locally"></a>Suivi de hello vue localement de sortie
1. Appuyez sur la touche application de F5 toorun hello en mode débogage.

    écouteur de trace par défaut Hello écrit tous les toohello de sortie de trace **sortie** fenêtre, ainsi que de l’autre sortie de débogage. Hello l’illustration suivante sortie hello hello instructions de trace que vous avez ajouté toohello `Index` (méthode).

    ![Suivi dans la fenêtre Débogage](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugtracing.png)

    Hello suit montrent comment tooview du résultat dans une page web, sans compiler en mode débogage.
2. Ouvrez le fichier Web.config de l’application hello (hello une situé dans le dossier du projet hello) et ajoutez un `<system.diagnostics>` élément à fin hello du fichier hello juste avant la fermeture de hello `</configuration>` élément :

          <system.diagnostics>
            <trace>
              <listeners>
                <add name="WebPageTraceListener"
                    type="System.Web.WebPageTraceListener,
                    System.Web,
                    Version=4.0.0.0,
                    Culture=neutral,
                    PublicKeyToken=b03f5f7f11d50a3a" />
              </listeners>
            </trace>
          </system.diagnostics>

    Hello `WebPageTraceListener` sortie de trace vous permet d’afficher en parcourant trop`/trace.axd`.
3. Ajouter un <a href="http://msdn.microsoft.com/library/vstudio/6915t83k(v=vs.100).aspx">élément trace</a> sous `<system.web>` dans le fichier Web.config hello, par exemple hello l’exemple suivant :

        <trace enabled="true" writeToDiagnosticsTrace="true" mostRecent="true" pageOutput="false" />
4. Appuyez sur la touche application de hello toorun CTRL + F5.
5. Dans la barre d’adresses hello hello fenêtre du navigateur, ajoutez *trace.axd* toohello URL, puis appuyez sur entrée (URL de hello sera toohttp://localhost:53370/trace.axd similaire).
6. Sur hello **Trace de l’Application** , cliquez sur **afficher les détails** de ligne de première hello (pas hello BrowserLink ligne).

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd1.png)

    Hello **détails de la demande** page s’affiche et Bonjour **les informations de traçage** section sortie hello à partir d’instructions de trace hello que vous avez ajouté toohello `Index` (méthode).

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd2.png)

    Par défaut, `trace.axd` est uniquement disponible localement. Si vous souhaitiez toomake il est disponible à partir d’une application web à distance, vous pouvez ajouter `localOnly="false"` toohello `trace` élément Bonjour *Web.config* de fichiers, comme indiqué dans hello l’exemple suivant :

        <trace enabled="true" writeToDiagnosticsTrace="true" localOnly="false" mostRecent="true" pageOutput="false" />

    Toutefois, l’activation `trace.axd` d’une production application web est généralement pas recommandée pour des raisons de sécurité, et dans les sections suivantes de hello, vous verrez un tooread de façon plus facile dans une application web Azure, les journaux de suivi.

### <a name="view-hello-tracing-output-in-azure"></a>Afficher la sortie de traçage hello dans Azure
1. Dans **l’Explorateur de solutions**, droit hello web projet, puis cliquez sur **publier**.
2. Bonjour **publier le site Web** boîte de dialogue, cliquez sur **publier**.

    Une fois que Visual Studio publie votre mise à jour, il ouvre une fenêtre d’Explorateur tooyour la page d’accueil (en supposant que vous n’avez pas effacer **URL de Destination** sur hello **connexion** onglet).
3. Dans l’**Explorateur de serveurs**, cliquez avec le bouton droit sur votre application web et sélectionnez **Afficher les journaux de streaming**.

    ![Afficher la diffusion de journaux en continu dans le menu contextuel](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewlogsmenu.png)

    Hello **sortie** fenêtre montre que vous êtes connecté toohello journal de diffusion en continu de service et ajoute une ligne notification chaque minute qui passe sans une toodisplay de journal.

    ![Afficher la diffusion de journaux en continu dans le menu contextuel](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-nologsyet.png)
4. Dans la fenêtre de navigateur hello qui affiche la page d’accueil de votre application, cliquez sur **Contact**.

    Dans quelques secondes hello de sortie de trace de niveau d’erreur hello, vous avez ajouté toohello `Contact` méthode s’affiche dans hello **sortie** fenêtre.

    ![Suivi d'erreur dans la fenêtre Sortie](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-errortrace.png)

    Visual Studio affiche seulement les traces de niveau d’erreur, car c’est le paramètre par défaut de hello lorsque vous activez le service de surveillance du journal de hello. Lorsque vous créez une nouvelle application web Azure, tout enregistrement est désactivé par défaut, que vous avez vu lors de l’ouverture de page de paramètres hello précédemment :

    ![Journalisation d'application désactivée](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-apploggingoff.png)

    Toutefois, si vous avez sélectionné **afficher les journaux de diffusion en continu**, Visual Studio automatiquement modifiée **Application Logging(File System)** trop**erreur**, ce qui signifie que les journaux de niveau d’erreur obtenir signalée. Dans commande toosee tous vos journaux de suivi, vous pouvez modifier ce paramètre trop**Verbose**. Lorsque vous sélectionnez un niveau de gravité inférieur à l'erreur, tous les journaux correspondant aux niveaux de gravité supérieurs sont également signalés. Donc, lorsque vous sélectionnez Commentaires, vous pouvez également consulter des informations, des avertissements et des journaux d'erreurs.  

1. Dans **l’Explorateur de serveurs**, avec le bouton droit de l’application hello web, puis cliquez sur **afficher les paramètres** comme vous l’avez fait précédemment.
2. Modification **journalisation des applications (système de fichiers)** trop**Verbose**, puis cliquez sur **enregistrer**.

    ![Paramètre tooVerbose de niveau de trace](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-applogverbose.png)
3. Dans la fenêtre du navigateur hello qui s’affiche maintenant votre **Contact** , cliquez sur **accueil**, puis cliquez sur **sur**, puis cliquez sur **Contact**.

    Après quelques secondes, hello **sortie** fenêtre affiche tous les de la sortie de traçage.

    ![Sortie de suivi des commentaires](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-verbosetraces.png)

    Dans cette section, vous avez activé et désactivé la journalisation à l’aide des paramètres d’application web Microsoft Azure. Vous pouvez également activer et désactiver des écouteurs de suivi en modifiant le fichier Web.config de hello. Toutefois, la modification du fichier Web.config de hello entraîne toorecycle de domaine d’application de hello, alors que l’activation de la journalisation via la configuration de l’application hello web qui ne. Si le problème de hello prend un tooreproduce beaucoup de temps, ou est intermittent, le recyclage de domaine d’application hello peut « corriger » et vous forcer toowait jusqu'à ce qu’il se produit à nouveau. L'activation des diagnostics dans Azure n'entraîne pas cela, vous pouvez donc commencer tout de suite à saisir des informations sur une erreur.

### <a name="output-window-features"></a>Fonctionnalités de la fenêtre Sortie
Hello **journaux Azure** onglet Hello **sortie** fenêtre comporte plusieurs boutons et une zone de texte :

![Boutons de l'onglet Journaux](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-icons.png)

Ils effectuent hello suivant des fonctions :

* Désactivez hello **sortie** fenêtre.
* Activation ou désactivation du retour automatique à la ligne
* Démarrage ou arrêt de la surveillance des journaux
* Spécifier les journaux toomonitor.
* Téléchargement de journaux
* Filtrage des journaux en fonction d'une chaîne de recherche ou d'une expression régulière
* Fermer hello **sortie** fenêtre.

Si vous entrez une chaîne de recherche ou d’une expression régulière, Visual Studio filtre les informations de journalisation sur le client de hello. Cela signifie que vous pouvez entrer des critères de hello après hello journaux sont affichés dans hello **sortie** fenêtre et que vous pouvez modifier les critères de filtrage sans avoir tooregenerate hello journaux.

## <a name="webserverlogs"></a>Affichage des journaux de serveur Web
Journaux du serveur Web enregistrent toute l’activité HTTP pour l’application web de hello. Dans l’ordre toosee dans hello **sortie** fenêtre que vous avez tooenable pour hello web app et indiquer à Visual Studio que vous souhaitez toomonitor les.

1. Bonjour **Configuration de l’application Web Azure** onglet que vous avez ouvert à partir de **l’Explorateur de serveurs**, modifier la journalisation du serveur Web trop**sur**, puis cliquez sur **enregistrer**.

    ![Activer la journalisation de serveur Web](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-webserverloggingon.png)
2. Bonjour **sortie** fenêtre, cliquez sur hello **spécifier quels toomonitor journaux Azure** bouton.

    ![Spécifiez le toomonitor journaux Azure](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-specifylogs.png)
3. Bonjour **des Options de journalisation Azure** boîte de dialogue, sélectionnez **Web journaux du serveur**, puis cliquez sur **OK**.

    ![Surveiller les journaux de serveur Web](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorwslogson.png)
4. Dans la fenêtre du navigateur hello qui montre l’application hello web, cliquez sur **accueil**, puis cliquez sur **sur**, puis cliquez sur **Contact**.

    journaux d’application Hello généralement s’affichent en premier, suivie de journaux du serveur web hello. Vous pouvez avoir toowait un certain temps pour hello consigne tooappear.

    ![Journaux de serveur Web dans la fenêtre Sortie](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-wslogs.png)

Par défaut, lorsque vous activez tout d’abord les journaux du serveur web à l’aide de Visual Studio, Azure écrit le système de fichiers toohello hello journaux. En guise d’alternative, vous pouvez utiliser hello Azure toospecify portail qui web journaux du serveur doit être écrits tooa conteneur d’objets blob dans un compte de stockage.

Si vous utilisez hello tooenable portail web server journalisation compte de stockage Azure tooan et désactivez la journalisation dans Visual Studio, lorsque vous réactivez journalisation dans Visual Studio, vos paramètres de compte de stockage sont restaurés.

## <a name="detailederrorlogs"></a>Affichage des journaux de messages d’erreur détaillés
Les journaux d'erreur détaillés fournissent des informations supplémentaires sur les requêtes HTTP ayant pour résultat des codes de réponse d'erreur (400 ou au-delà). Dans l’ordre toosee dans hello **sortie** , vous devez tooenable pour hello web app et indiquer à Visual Studio que vous souhaitez toomonitor les.

1. Bonjour **Configuration de l’application Web Azure** onglet que vous avez ouvert à partir de **l’Explorateur de serveurs**, modifiez **Messages d’erreur détaillés** trop**sur**, et puis cliquez sur **enregistrer**.

    ![Activer les messages d'erreur détaillés](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailedlogson.png)
2. Bonjour **sortie** fenêtre, cliquez sur hello **spécifier quels toomonitor journaux Azure** bouton.
3. Bonjour **des Options de journalisation Azure** boîte de dialogue, cliquez sur **tous les journaux**, puis cliquez sur **OK**.

    ![Surveiller tous les journaux](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorall.png)
4. Dans la barre d’adresses hello hello fenêtre du navigateur, ajoutez une toocause d’URL caractère supplémentaire toohello une 404 erreur (par exemple, `http://localhost:53370/Home/Contactx`), puis appuyez sur ENTRÉE.

    Après quelques secondes, journal des erreurs détaillé hello apparaît dans hello Visual Studio **sortie** fenêtre.

    ![Journal d'erreur détaillé dans la fenêtre Sortie](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorlog.png)

    Touche CTRL enfoncée et cliquez sur sortie hello link toosee hello journal mis en forme dans un navigateur :

    ![Journal d'erreur détaillé dans la fenêtre du navigateur](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorloginbrowser.png)

## <a name="downloadlogs"></a>Téléchargement de journaux du système de fichiers
Tous les journaux que vous pouvez surveiller Bonjour **sortie** fenêtre peut aussi être téléchargé en tant qu’un *.zip* fichier.

1. Bonjour **sortie** fenêtre, cliquez sur **télécharger les journaux de diffusion en continu**.

    ![Boutons de l'onglet Journaux](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadicon.png)

    L’Explorateur de fichiers s’ouvre tooyour *télécharge* dossier avec hello téléchargé le fichier sélectionné.

    ![Fichier téléchargé](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadedfile.png)
2. Extraire hello *.zip* fichier et que vous consultez hello suivant la structure de dossiers :

    ![Fichier téléchargé](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilefolders.png)

   * Journaux de suivi d’application se trouvent dans *.txt* fichiers Bonjour *LogFiles\Application* dossier.
   * Journaux du serveur Web se trouvent dans *.log* fichiers Bonjour *LogFiles\http\RawLogs* dossier. Vous pouvez utiliser un outil tel que [Log Parser](http://www.microsoft.com/download/details.aspx?displaylang=en&id=24659) tooview et de manipuler ces fichiers.
   * Journaux de messages d’erreur détaillés se trouvent dans *.html* fichiers Bonjour *LogFiles\DetailedErrors* dossier.

     (hello *déploiements* est de dossier pour les fichiers créés par le contrôle de source de publication ; il n’est pas la publication Studio tooVisual connexes n’est pas défini. Hello *Git* dossier concerne les traces connexes toosource contrôle publication hello fichier journal et de service de diffusion en continu.)  

## <a name="storagelogs"></a>Affichage des journaux de stockage
Journaux de suivi d’application peuvent également être envoyés à tooan compte de stockage Azure, et vous pouvez les afficher dans Visual Studio. toodo que vous allez créer un compte de stockage et activer les journaux de stockage dans le portail classique de hello et les afficher dans hello **journaux** onglet Hello **application Web Azure** fenêtre.

Vous pouvez envoyer des journaux tooany ou l’ensemble des trois destinations :

* système de fichiers Hello.
* les tables de compte de stockage ;
* les objets blob de compte de stockage.

Vous pouvez définir un niveau de gravité distinct pour chaque destination.

Tables rendent tooview facilement les détails des journaux en ligne, et ils prennent en charge la diffusion en continu ; Vous pouvez interroger les journaux dans les tables et voir les nouveaux journaux lors de leur création. Objets BLOB rendre facile toodownload journaux dans les fichiers et tooanalyze les à l’aide de HDInsight, car HDInsight sait comment toowork avec le stockage d’objets blob. Pour plus d’informations, consultez la section **Hadoop et MapReduce** de la page [Options de stockage de données (développement d’applications cloud concrètes avec Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options).

Vous avez actuellement des fichiers journaux tooverbose niveau du système ; Hello étapes suivantes décrivent la configuration des tableaux compte des informations sur les journaux de niveau toogo toostorage. « Au niveau de l’information » signifie que tous les journaux créés en appelant `Trace.TraceInformation`, `Trace.TraceWarning` et `Trace.TraceError` seront affichés, mais pas les journaux créés en appelant `Trace.WriteLine`.

Comptes de stockage offrent que plus de stockage et de rétention plus longue durée pour les journaux de système de fichiers toohello comparées. Un autre avantage de l’application émettrice toostorage des journaux de suivi est que vous obtenez des informations supplémentaires avec chaque journal que vous n’obtenez pas de système de fichiers journaux.

1. Avec le bouton droit **stockage** sous hello nœud Azure, puis cliquez sur **créer un compte de stockage**.

![Créer un compte de stockage](./media/web-sites-dotnet-troubleshoot-visual-studio/createstor.png)

1. Bonjour **créer un compte de stockage** boîte de dialogue, entrez un nom pour le compte de stockage hello.

    nom de Hello doit être unique (aucun autre compte de stockage Azure ne peut avoir hello même nom). Si le nom hello que vous entrez est déjà en cours d’utilisation, vous obtiendrez une chance toochange il.

    Hello tooaccess URL votre compte de stockage sera *{nom}*. core.windows.net.
2. Ensemble hello **région ou groupe d’affinités** tooyou le plus proche de liste déroulante toohello région.

    Ce paramètre spécifie le centre de données Azure qui hébergera votre compte de stockage. Pour ce didacticiel, votre choix ne sont pas rendre une différence notable, mais pour une application web de production que votre serveur web et votre toobe de compte de stockage Bonjour même latence toominimize de région et les données des frais de sortie. Hello web application (vous allez créer une version ultérieure) doit s’exécuter dans une région aussi près que les navigateurs toohello possible l’accès à votre application web de latence toominimize de commande.
3. Ensemble hello **réplication** déroulante liste trop**localement redondant**.
   
    Lors de la géo-réplication est activée pour un compte de stockage, contenu de hello stocké est répliqué tooa centre de données secondaire tooenable basculement toothat emplacement en cas de sinistre majeur dans l’emplacement principal de hello. La géo-réplication peut engendrer des coûts supplémentaires. Pour les comptes de test et de développement, généralement non désirés toopay pour la géo-réplication. Pour plus d’informations, consultez [Création, gestion ou suppression d’un compte de stockage](../storage/common/storage-create-storage-account.md).
4. Cliquez sur **Create**.

    ![New storage account](./media/web-sites-dotnet-troubleshoot-visual-studio/newstorage.png)    
5. Bonjour Visual Studio **application Web Azure** fenêtre, cliquez sur hello **journaux** onglet, puis cliquez sur **configurer la journalisation dans le portail de gestion**.

    <!-- todo:screenshot of new portal if hello VS page link goes toonew portal -->
    ![Configuration de la journalisation](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configlogging.png)

    Cette opération ouvre hello **configurer** portail classique de hello pour votre application web.
6. Dans le portail hello classic **configurer** onglet, faites défiler la liste toohello section de diagnostics d’application et modifiez **journalisation des applications (stockage de tables)** trop**sur**.
7. Modification **au niveau de journalisation** trop**informations**.
8. Cliquez sur **Manage Table Storage**.

    ![Cliquer sur Manage Table Storage](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-stgsettingsmgmtportal.png)

    Bonjour **gérer le stockage de table pour application diagnostics** zone, vous pouvez choisir votre compte de stockage si vous avez plusieurs. Vous pouvez créer une table ou utiliser une table existante.

    ![Manage Table Storage](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-choosestorageacct.png)
9. Bonjour **gérer le stockage de table pour application diagnostics** boîte boîte de hello tooclose hello case à cocher, cliquez sur.
10. Dans le portail hello classic **configurer** , cliquez sur **enregistrer**.
11. Dans la fenêtre du navigateur hello qui affiche l’application hello application web, cliquez sur **accueil**, puis cliquez sur **sur**, puis cliquez sur **Contact**.

     compte de stockage toohello seront écrit les informations de journalisation Hello produites par navigation ces pages web.
12. Bonjour **journaux** onglet Hello **application Web Azure** fenêtre dans Visual Studio, cliquez sur **Actualiser** sous **résumé de Diagnostic**.

     ![Cliquer sur Actualiser.](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-refreshstorage.png)

     Hello **résumé de Diagnostic** section affiche les journaux pour hello des 15 dernières minutes par défaut. Vous pouvez modifier toosee de période hello davantage de journaux.

     (Si vous obtenez une erreur « table introuvable », vérifiez que vous avez accédé pages toohello hello suivi une fois que vous avez activé **journalisation des applications (stockage)** et une fois que vous avez cliqué sur **enregistrer**.)

     ![Journaux de stockage](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-storagelogs.png)

     Notez que dans cette vue consultez **ID de processus** et **ID de Thread** pour chaque journal, vous n’obtenez pas dans les journaux système de fichier hello. Vous pouvez voir des champs supplémentaires en consultant le tableau de stockage Azure hello directement.
13. Cliquez sur **View all application logs**.

     table de journal de trace Hello s’affiche dans la visionneuse de table de stockage Azure hello.

     (Si vous obtenez une erreur « séquence ne contient aucun élément », ouvrez **l’Explorateur de serveurs**, développez le nœud hello pour votre compte de stockage sous hello **Azure** nœud et avec le bouton droit puis **Tables**sur **Actualiser**.)

     ![Journaux de stockage dans la vue Table](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracelogtableview.png)

     Cette vue affiche des champs supplémentaires que vous ne pouvez pas consulter ailleurs. Cette vue vous permet également toofilter journaux à l’aide de l’interface utilisateur du Générateur de requête spécial pour la construction d’une requête. Pour plus d'informations, consultez les sections « Utilisation des ressources de tables » et « Filtrage d'entités » de la page [Consultation des ressources de stockage avec l'Explorateur de serveurs](http://msdn.microsoft.com/library/ff683677.aspx).
14. toolook détails hello pour une seule ligne, double-cliquez sur une des lignes de hello.

     ![Table de suivi dans l'Explorateur de serveurs](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracetablerow.png)

## <a name="failedrequestlogs"></a>Affichage des journaux de suivi de demandes ayant échoué
Journaux de suivi des demandes ayant échoué est utiles lorsque vous avez besoin des détails de hello toounderstand de la façon dont IIS traite une demande HTTP, dans des scénarios tels que les problèmes d’authentification ou de réécriture d’URL.

Azure web apps utilisez hello Échec de la même demande de fonctionnalité de traçage qui a été disponible avec IIS 7.0 et versions ultérieures. Vous n’avez toohello accès paramètres IIS qui configurent les erreurs sont consignés, toutefois. Lorsque vous activez le suivi des demandes ayant échoué, toutes les erreurs sont récupérées.

Vous pouvez activer le suivi des demandes ayant échoué en utilisant Visual Studio, mais vous ne pouvez pas les afficher dans Visual Studio. Ces journaux sont des fichiers XML. Hello service journal uniquement de diffusion en continu vérifie les fichiers qui sont considérées comme accessible en lecture en mode texte brut : *.txt*, *.html*, et *.log* fichiers.

Vous pouvez afficher les journaux de suivi des demandes ayant échoué dans un navigateur directement via FTP ou localement après un toodownload d’outil FTP à l’aide de leur ordinateur local de tooyour. Dans cette section, nous les afficherons directement dans un navigateur.

1. Bonjour **Configuration** onglet Hello **application Web Azure** fenêtre que vous avez ouvert à partir de **l’Explorateur de serveurs**, modifiez **Échec de suivi des demandes**trop**sur**, puis cliquez sur **enregistrer**.

    ![Activer le suivi des demandes ayant échoué](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequeston.png)
2. Dans la barre d’adresses hello de fenêtre du navigateur hello qui montre l’application hello web, ajoutez une URL toohello de caractère supplémentaire et cliquez sur entrée toocause une erreur 404.

    Cela provoque une toobe de journal de suivi des demandes ayant échoué créé et hello étapes suivantes montrent comment tooview ou téléchargement hello journal.
3. Dans Visual Studio, Bonjour **Configuration** onglet Hello **application Web Azure** fenêtre, cliquez sur **ouvrir dans le portail de gestion**.
4. Bonjour [Azure Portal](https://portal.azure.com) **paramètres** panneau pour votre application web, cliquez sur **informations d’identification de déploiement**, puis entrez un nouveau nom d’utilisateur et un mot de passe.

    ![Nouveaux nom d'utilisateur et mot de passe FTP](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-enterftpcredentials.png)

    ** Lorsque vous vous connectez, vous avez toouse hello nom d’utilisateur complet avec hello web application le préfixe de nom tooit. Par exemple, si vous entrez « MonID » comme nom d’utilisateur et le site de hello est « myexample », vous connecter en tant que « myexample\myid ».
5. Dans une nouvelle fenêtre de navigateur, accédez à toohello URL qui est affiché sous **nom d’hôte FTP** ou **nom d’hôte FTPS** Bonjour **Web App** panneau pour votre application web.
6. Connectez-vous en utilisant les informations d’identification hello FTP que vous avez créé précédemment (y compris le préfixe du nom application hello web hello nom d’utilisateur).

    navigateur de Hello affiche le dossier racine de hello de hello web app.
7. Ouvrez hello *LogFiles* dossier.

    ![Ouvrir le dossier LogFiles](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilesfolder.png)
8. Ouvrez le dossier hello nommé W3SVC ainsi qu’une valeur numérique.

    ![Ouvrir le dossier W3SVC](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfolder.png)

    dossier de Hello contient les fichiers XML pour les erreurs qui ont été consignés une fois que vous avez activé le suivi des demandes ayant échoué et un fichier XSL qu’un navigateur peut utiliser tooformat hello XML.

    ![Dossier W3SVC](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfoldercontents.png)
9. Cliquez sur le fichier XML de hello pour les demandes ayant échoué hello souhaité pour les informations de traçage toosee pour.

    Hello l’illustration suivante montre une partie des informations de traçage hello pour un exemple d’erreur.

    ![Suivi d'une demande ayant échoué dans le navigateur](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequestinbrowser.png)

## <a name="nextsteps"></a>Étapes suivantes
Vous avez vu comment Visual Studio le rend facile tooview journaux créés par une application web Azure. Hello sections suivantes fournissent des liens toomore ressources sur les rubriques connexes :

* Dépannage des applications web Microsoft Azure
* Débogage dans Visual Studio
* Débogage distant dans Azure
* Suivi dans les applications ASP.NET
* Analyse de journaux de serveur Web
* Analyse des journaux de suivi des demandes ayant échoué
* Débogage de Cloud Services

### <a name="azure-web-app-troubleshooting"></a>Dépannage des applications web Microsoft Azure
Pour plus d’informations sur le dépannage des applications web dans Azure App Service, consultez hello suivant des ressources :

* [Comment les applications web toomonitor](/manage/services/web-sites/how-to-monitor-websites/)
* [Étude des fuites de mémoire dans les applications Web Microsoft Azure avec Visual Studio 2013](http://blogs.msdn.com/b/visualstudioalm/archive/2013/12/20/investigating-memory-leaks-in-azure-web-sites-with-visual-studio-2013.aspx). Article sur le blog ALM de Microsoft concernant les fonctionnalités de Visual Studio prévues pour l'analyse de problèmes de mémoire gérés.
* [Les outils en ligne des applications Web Microsoft Azure que vous devez connaître](https://azure.microsoft.com/blog/2014/03/28/windows-azure-websites-online-tools-you-should-know-about-2/). Article de blog par Amit Apple.

Pour une aide à poser une question de résolution des problèmes spécifique, démarrer un thread de hello suivant forums :

* [Hello forum Azure sur le site d’ASP.NET hello](http://forums.asp.net/1247.aspx/1?Azure+and+ASP+NET).
* [Hello forum Azure sur MSDN](http://social.msdn.microsoft.com/Forums/windowsazure/).
* [StackOverflow.com](http://www.stackoverflow.com).

### <a name="debugging-in-visual-studio"></a>Débogage dans Visual Studio
Pour plus d’informations sur la façon dont toouse mode débogage dans Visual Studio, consultez hello [débogage dans Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx) rubrique MSDN et [conseils de débogage avec Visual Studio 2010](http://weblogs.asp.net/scottgu/archive/2010/08/18/debugging-tips-with-visual-studio-2010.aspx).

### <a name="remote-debugging-in-azure"></a>Débogage distant dans Azure
Pour plus d’informations sur le débogage distant d’applications web Azure et les tâches Web, consultez hello suivant des ressources :

* [Introduction tooRemote débogage Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/).
* [Introduction tooRemote débogage Azure App Service Web Apps partie 2 - à l’intérieur de débogage distant](https://azure.microsoft.com/blog/2014/05/07/introduction-to-remote-debugging-azure-web-sites-part-2-inside-remote-debugging/)
* [Introduction tooRemote débogage sur Azure App Service Web Apps 3ème partie-environnement d’instances multiples et GIT](https://azure.microsoft.com/blog/2014/05/08/introduction-to-remote-debugging-on-azure-web-sites-part-3-multi-instance-environment-and-git/)
* [Débogage de WebJobs (vidéo)](https://www.youtube.com/watch?v=ncQm9q5ZFZs&list=UU_SjTh-ZltPmTYzAybypB-g&index=1)

Si votre application web utilise une API Web Azure ou des Services mobiles principale et que vous devez toodebug qui, consultez [débogage de service principal .NET dans Visual Studio](http://blogs.msdn.com/b/azuremobile/archive/2014/03/14/debugging-net-backend-in-visual-studio.aspx).

### <a name="tracing-in-aspnet-applications"></a>Suivi dans les applications ASP.NET
Il n’y a aucune tooASP.NET complète et à jour des vues d’ensemble de suivi disponibles sur Internet de hello. Hello meilleures que vous pouvez effectuer est prise en main des matériaux introduction ancien écrits pour Web Forms étant donné que MVC n’existe encore et qui complètent avec la plus récente blog valide qui se concentrent sur des problèmes spécifiques. Certains toostart bon point de départ sont hello suivant des ressources :

* [Surveillance et télémétrie (développement d’applications cloud concrètes avec Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry).<br>
  Chapitre de livre électronique contenant des recommandations pour le suivi dans les applications de cloud Azure.
* [Suivi ASP.NET](http://msdn.microsoft.com/library/ms972204.aspx)<br/>
  Ancien, mais toujours une bonne ressource pour un objet de toohello présentation générale.
* [Écouteurs de suivi](http://msdn.microsoft.com/library/4y5y10s7.aspx)<br/>
  Pour plus d’informations sur les écouteurs de traçage, mais ne mentionnent pas hello [WebPageTraceListener](http://msdn.microsoft.com/library/system.web.webpagetracelistener.aspx).
* [Procédure pas à pas : intégration du suivi ASP.NET avec le suivi System.Diagnostics](http://msdn.microsoft.com/library/b0ectfxd.aspx)<br/>
  Cela trop ancien, mais inclut des informations supplémentaires non traités dans cet article Introduction hello.
* [Suivi dans les vues d’ASP.NET MVC Razor](http://blogs.msdn.com/b/webdev/archive/2013/07/16/tracing-in-asp-net-mvc-razor-views.aspx)<br/>
  Outre le suivi dans les vues Razor, post de hello explique également comment toocreate une erreur filtrer dans l’ordre toolog non prise en charge toutes les exceptions dans une application MVC. Pour plus d’informations sur comment non gérée toolog toutes les exceptions dans une application Web Forms, consultez l’exemple de Global.asax de hello dans [exemple complet pour les gestionnaires d’erreurs](http://msdn.microsoft.com/library/bb397417.aspx) sur MSDN. Dans MVC ou Web Forms, si vous souhaitez toolog certaines exceptions mais que vous permettent de framework par défaut de hello gestion prennent effet, vous pouvez intercepter et lever de nouveau comme hello l’exemple suivant :

        try
        {
           // Your code that might cause an exception toobe thrown.
        }
        catch (Exception ex)
        {
            Trace.TraceError("Exception: " + ex.ToString());
            throw;
        }
* [Diffusion en continu de la journalisation du suivi de diagnostic à partir de hello de ligne de commande Azure (plus aperçu !)](http://www.hanselman.com/blog/StreamingDiagnosticsTraceLoggingFromTheAzureCommandLinePlusGlimpse.aspx)<br/>
  Comment toouse hello toodo de ligne de commande quel ce indique didacticiel comment toodo dans Visual Studio. [Glimpse](http://www.hanselman.com/blog/IfYoureNotUsingGlimpseWithASPNETForDebuggingAndProfilingYoureMissingOut.aspx) est un outil pour le débogage d'applications ASP.NET.
* [Utilisation des fonctions de journalisation et de diagnostic des applications web - avec David Ebbo](/documentation/videos/azure-web-site-logging-and-diagnostics/) et [Journaux de streaming dans Web Apps - avec David Ebbo](/documentation/videos/log-streaming-with-azure-web-sites/)<br>
  par Scott Hanselman et David Ebbo.

Pour la journalisation de l’erreur, un autre toowriting votre propre code de traçage est toouse open source les fonctionnalités de journalisation comme [ELMAH](http://nuget.org/packages/elmah/). Pour plus d'informations, consultez les [billets du blog de Scott Hanselman sur ELMAH](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx).

Notez également que vous n’avez pas toouse ASP.NET ou les journaux de suivi System.Diagnostics si vous souhaitez tooget de diffusion en continu à partir d’Azure. Hello le service de journalisation de diffusion en continu de l’application web Azure est diffusés les *.txt*, *.html*, ou *.log* fichier qu’il trouve Bonjour *LogFiles* dossier. Par conséquent, vous pouvez créer votre propre système de journalisation qui écrit le système de fichiers toohello de hello web app, et votre fichier être diffusé en continu et automatiquement téléchargé. Tout ce que vous avez toodo est d’écrire du code application qui crée des fichiers Bonjour *d:\home\logfiles* dossier.

### <a name="analyzing-web-server-logs"></a>Analyse de journaux de serveur Web
Pour plus d’informations sur l’analyse des journaux de serveur web, consultez hello suivant des ressources :

* [LogParser](http://www.microsoft.com/download/details.aspx?id=24659)<br/>
  Un outil pour afficher les données des journaux de serveur Web (fichiers*.log* ).
* [Dépannage des problèmes de performances IIS ou des erreurs d’application à l’aide de LogParser ](http://www.iis.net/learn/troubleshoot/performance-issues/troubleshooting-iis-performance-issues-or-application-errors-using-logparser)<br/>
  Un outil d’analyseur de journal toohello présentation que vous pouvez utiliser le serveur web de tooanalyze se connecte.
* [Billets du blog de Robert McMurray sur l’utilisation de LogParser](http://blogs.msdn.com/b/robert_mcmurray/archive/tags/logparser/)<br/>
* [Hello, code d’état HTTP dans IIS 7.0, IIS 7.5 et IIS 8.0](http://support.microsoft.com/kb/943891)

### <a name="analyzing-failed-request-tracing-logs"></a>Analyse des journaux de suivi des demandes ayant échoué
site Web de Microsoft TechNet Hello inclut un [à l’aide d’Échec de suivi des demandes](http://www.iis.net/learn/troubleshoot/using-failed-request-tracing) section qui peut être utile pour comprendre comment toouse ces journaux. Toutefois, cette documentation se concentre principalement sur la configuration du suivi des demandes ayant échoué dans IIS, ce que vous ne pouvez pas faire dans les applications web Microsoft Azure.

[GetStarted]: app-service-web-get-started-dotnet.md
[GetStartedWJ]: websites-dotnet-webjobs-sdk.md
