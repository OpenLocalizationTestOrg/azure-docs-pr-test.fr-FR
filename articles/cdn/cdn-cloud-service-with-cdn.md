---
title: aaaIntegrate un service cloud Azure avec Azure CDN | Documents Microsoft
description: "Découvrez comment toodeploy un service cloud qui fait Office de contenu à partir d’un point de terminaison CDN Azure intégrée"
services: cdn, cloud-services
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: tysonn
ms.assetid: b3c0108f-9ec5-43a8-8fd0-40eafbd32637
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f20d60b0b5edc133adf06d010633a15f62e2b8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="intro"></a> Intégration d’un service cloud à Azure CDN
Un service cloud peut être intégré à Azure CDN, servant le contenu de l’emplacement du service de cloud hello. Cela donne approche vous hello suivants avantages :

* Facilité de déploiement et de mise à jour des images, scripts et feuilles de style dans les annuaires de projet du service cloud
* Mettre à niveau facilement les packages NuGet hello dans votre service cloud, tels que jQuery ou versions d’amorçage
* Gérer votre application Web et votre CDN-pris en charge de contenu à partir d’hello même interface de Visual Studio
* Flux de travail unifié pour le déploiement de votre application web et de votre contenu CDN
* Intégration du regroupement et de la minimisation d'ASP.NET avec Azure CDN

## <a name="what-you-will-learn"></a>Contenu
Ce didacticiel vous apprendra à effectuer les opérations suivantes :

* [Intégration d'un point de terminaison Azure CDN à votre service cloud et traitement du contenu statique dans vos pages Web depuis Azure CDN](#deploy)
* [Configuration des paramètres du cache pour le contenu statique de votre service cloud](#caching)
* [Distribution du contenu à partir d'actions de contrôleur via Azure CDN](#controller)
* [Serve groupée et réduire le contenu via le CDN Azure tout en conservant le script hello débogage dans Visual Studio](#bundling)
* [Configuration de secours de vos scripts et feuilles de style CSS quand votre service Azure CDN est hors connexion](#fallback)

## <a name="what-you-will-build"></a>Ce que vous allez créer
Vous déployez un rôle Web de service cloud à l’aide de la valeur par défaut de hello modèle ASP.NET MVC, ajouter du contenu de tooserve de code à partir d’un CDN Azure intégré, comme une image, les résultats d’action de contrôleur et les fichiers JavaScript et CSS par défaut hello et également écrire hello tooconfigure de code mécanisme de secours pour les groupes pris en charge dans les événements hello que hello CDN est hors connexion.

## <a name="what-you-will-need"></a>Éléments requis
Ce didacticiel n’hello suivant des conditions préalables :

* Un [compte Microsoft Azure](/account/)
* Visual Studio 2015 avec le [Kit SDK Azure](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)

> [!NOTE]
> Vous avez besoin une toocomplete compte Azure ce didacticiel :
> 
> * Vous pouvez [ouvrir un compte Azure gratuitement](https://azure.microsoft.com/pricing/free-trial/) -vous obtenez des crédits vous pouvez utiliser tootry à payer des services Azure et même après qu’ils soient utilisés jusqu'à vous pouvez conserver le compte de hello et libérer de l’utilisation des services Azure, comme les sites Web.
> * Vous pouvez [activer les avantages de l'abonnement MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) : votre abonnement MSDN vous donne droit chaque mois à des crédits dont vous pouvez vous servir pour les services Azure payants.
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a>Déploiement d'un service cloud
Dans cette section, vous déploie la valeur par défaut de hello modèle d’application ASP.NET MVC dans le rôle du service Web de Visual Studio 2015 tooa cloud et puis l’intégrer à un point de terminaison CDN. Suivez les instructions de hello ci-dessous :

1. Dans Visual Studio 2015, créez un nouveau service cloud Azure à partir de la barre de menus hello en accédant trop**fichier > Nouveau > projet > Cloud > Azure Cloud Service**. Attribuez-lui un nom et cliquez sur **OK**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. Sélectionnez **rôle Web ASP.NET** et cliquez sur hello  **>**  bouton. Cliquez sur OK.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. Sélectionnez **MVC** et cliquez sur **OK**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. À présent, publier cette tooan de rôle Web service cloud Azure. Cliquez sur le projet de service cloud hello et sélectionnez **publier**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. Si vous n’êtes pas encore inscrit dans Microsoft Azure, cliquez sur hello **ajouter un compte...**  hello de liste déroulante et cliquez sur **ajouter un compte** élément de menu.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. Dans la page de connexion hello, connectez-vous à hello compte Microsoft que vous avez utilisé tooactivate votre compte Azure.
7. Une fois que vous êtes connecté, cliquez sur **Suivant**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. En supposant que vous n'avez pas créé de compte de service cloud ou de stockage, Visual Studio vous aide à créer les deux. Bonjour **créer un Service Cloud et compte** boîte de dialogue, nom de service désiré de type hello et la région souhaités hello select. Cliquez sur **Créer**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. Bonjour une page de paramètres de publication, vérifiez la configuration de hello, cliquez sur **publier**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > processus de publication Hello pour les services de cloud prend beaucoup de temps. Hello activer Web Deploy pour l’option de tous les rôles peut rendre le débogage de votre service cloud beaucoup plus rapide en fournissant des mises à jour rapide (mais temporaire) tooyour rôles Web. Pour plus d’informations sur cette option, consultez [publication d’un Service Cloud à l’aide des outils d’Azure hello](http://msdn.microsoft.com/library/ff683672.aspx).
   > 
   > 
   
    Hello lorsque **journal des activités Microsoft Azure** indique que l’état de publication est **terminé**, vous allez créer un point de terminaison CDN est intégré à ce service cloud.
   
   > [!WARNING]
   > Si, après la publication, le service de cloud computing hello déployé affiche un écran d’erreur, il est probable que vous avez déployé le service cloud hello utilise un [invité du système d’exploitation qui n’inclut pas de .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).  Vous pouvez contourner ce problème en [déployant .NET 4.5.2 en tant que tâche de démarrage](../cloud-services/cloud-services-dotnet-install-dotnet.md).
   > 
   > 

## <a name="create-a-new-cdn-profile"></a>Créer un profil CDN
Un profil CDN est une collection de points de terminaison CDN.  Chaque profil contient un ou plusieurs points de terminaison CDN.  Vous souhaiterez peut-être toouse plusieurs profils tooorganize vos points de terminaison CDN par domaine internet, application web ou d’autres critères.

> [!TIP]
> Si vous avez déjà un profil CDN que vous souhaitez toouse pour ce didacticiel, passez trop[créer un nouveau point de terminaison CDN](#create-a-new-cdn-endpoint).
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a>Créer un point de terminaison CDN
**toocreate un nouveau point de terminaison CDN pour votre compte de stockage**

1. Bonjour [portail de gestion Azure](https://portal.azure.com), accédez tooyour le profil CDN.  Vous pouvez avoir épinglée toohello le tableau de bord à l’étape précédente de hello.  Si vous ne vous le trouverez en cliquant sur **Parcourir**, puis **profils CDN**, et en cliquant sur le profil de hello vous prévoyez de tooadd votre point de terminaison.
   
    Panneau de profil CDN Hello s’affiche.
   
    ![Profil CDN][cdn-profile-settings]
2. Cliquez sur hello **ajouter le point de terminaison** bouton.
   
    ![Bouton Ajouter un point de terminaison][cdn-new-endpoint-button]
   
    Hello **ajouter un point de terminaison** panneau s’affiche.
   
    ![Panneau Ajouter un point de terminaison][cdn-add-endpoint]
3. Entrez un **nom** pour ce point de terminaison CDN.  Ce nom sera utilisé tooaccess vos ressources mises en cache au niveau du domaine de hello `<EndpointName>.azureedge.net`.
4. Bonjour **type d’origine** liste déroulante, sélectionnez *service de cloud computing*.  
5. Bonjour **nom d’hôte d’origine** liste déroulante, sélectionnez votre service cloud.
6. Laisser les valeurs par défaut hello pour **chemin d’origine**, **en-tête hôte d’origine**, et **port de protocole/origine**.  Vous devez spécifier au moins un protocole (HTTP ou HTTPS).
7. Cliquez sur hello **ajouter** bouton toocreate hello nouveau point de terminaison.
8. Une fois que le point de terminaison hello est créé, il apparaît dans une liste de points de terminaison pour le profil de hello. Hello liste affiche hello URL toouse tooaccess mis en cache le contenu, ainsi que le domaine d’origine hello.
   
    ![Point de terminaison CDN][cdn-endpoint-success]
   
   > [!NOTE]
   > point de terminaison Hello pas immédiatement sera disponible pour utilisation.  Il peut prendre jusqu'à minutes too90 toopropagate d’inscription hello via réseau CDN de hello. Les utilisateurs qui essaient de nom de domaine CDN toouse hello immédiatement peuvent recevoir le code d’état 404 jusqu'à ce que le contenu hello est disponible via hello CDN.
   > 
   > 

## <a name="test-hello-cdn-endpoint"></a>Hello de test point de terminaison CDN
Lorsque l’état de publication de hello est **terminé**, ouvrez une fenêtre de navigateur et accédez trop**http://<cdnName>*.azureedge.net/Content/bootstrap.css**. Dans ma configuration, cette URL est la suivante :

    http://camservice.azureedge.net/Content/bootstrap.css

Qui correspond à toohello suivant l’URL d’origine au point de terminaison CDN hello :

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

Lorsque vous accédez trop**http://*&lt;cdnName >*.azureedge.net/Content/bootstrap.css**, en fonction de votre navigateur, vous serez toodownload demandée ou ouvrez hello bootstrap.css qui fournie à partir de votre application Web publiée.

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

De même, vous pouvez accéder à toute URL accessible publiquement à l’adresse **http://*&lt;nom_service>*.cloudapp.net/**, directement à partir de votre point de terminaison CDN. Par exemple :

* Un fichier .js à partir du chemin d’accès de hello /Script
* N’importe quel fichier de contenu à partir de hello/Content chemin d’accès
* un contrôleur/une action ;
* Si la chaîne de requête hello est activé au point de terminaison CDN, n’importe quelle URL avec des chaînes de requête

En fait, avec hello au-dessus de configuration, vous pouvez héberger service cloud entière hello  **http://*&lt;cdnName >*.azureedge.net/**. Si vous accédez trop**http://camservice.azureedge.net/ **, je reçois résultat d’action hello de Home/Index.

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

Cela ne signifie pas, toutefois, qu’il s’agit toujours d’un tooserve conseillé un service cloud entière via le CDN Azure. 

Un CDN avec optimisation de la remise statique ne pas nécessairement accélérer la remise de ressources dynamiques qui ne sont pas destinés toobe mis en cache ou sont mis à jour très fréquemment, étant donné que hello CDN doit extraire une nouvelle version de l’élément multimédia de hello à partir du serveur d’origine hello très souvent. Pour ce scénario, vous pouvez activer [accélération de Site dynamique](cdn-dynamic-site-acceleration.md) optimisation (DSA) sur votre point de terminaison CDN qui utilise différents toospeed techniques paramétrer la livraison de ressources dynamiques non mise en cache. 

Si vous avez un site avec un mélange de contenu statique et dynamique, vous pouvez choisir tooserve votre contenu statique de distribution de contenu avec un type de l’optimisation statique (par exemple, la remise de web général) et le contenu dynamique tooserve directement à partir de serveur d’origine hello, ou via un réseau CDN point de terminaison avec l’optimisation de DSA activée sur un cas par cas. fin de toothat, vous avez déjà vu comment tooaccess le contenu des fichiers à partir du point de terminaison CDN hello. Je vous montrera comment tooserve une action de contrôleur spécifique via un point de terminaison CDN spécifique dans servir contenu à partir d’actions de contrôleur via le CDN Azure.

Hello consiste toodetermine qui tooserve à partir d’Azure CDN sur un cas par cas dans votre service cloud de contenu. fin de toothat, vous avez déjà vu comment tooaccess le contenu des fichiers à partir du point de terminaison CDN hello. Je vous montrera comment tooserve une action de contrôleur spécifique via hello point de terminaison CDN dans [traiter du contenu à partir d’actions de contrôleur via Azure CDN](#controller).

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a>Configuration des options de mise en cache des fichiers statiques dans votre service cloud
Avec l’intégration d’Azure CDN dans votre service cloud, vous pouvez spécifier comment vous souhaitez que statique toobe contenu mis en cache dans le point de terminaison CDN hello. toodo, ouvrez *Web.config* à partir de votre rôle Web de projet (par exemple, WebRole1) et ajoutez un `<staticContent>` élément trop`<system.webServer>`. Hello XML ci-après configure hello cache tooexpire dans les 3 jours.  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

Une fois que vous faites cela, tous les fichiers statiques dans votre service cloud observera hello même règle dans le cache du CDN. Pour un contrôle plus granulaire des paramètres du cache, ajoutez un fichier *Web.config* dans un dossier et ajoutez-lui vos paramètres. Par exemple, ajouter un *Web.config* toohello de fichiers *\Content* dossier et remplacer hello contenu par hello XML suivant :

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

Avec ce paramètre, tous les fichiers statiques à partir de hello *\Content* toobe dossier mis en cache pendant 15 jours.

Pour plus d’informations sur la façon de tooconfigure hello `<clientCache>` élément, consultez [cache du Client &lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).

Dans [traiter du contenu à partir d’actions de contrôleur via Azure CDN](#controller), je vous montrera également comment vous pouvez configurer les paramètres de cache pour les résultats d’action de contrôleur Bonjour cache du CDN.

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a>Distribution du contenu à partir d'actions de contrôleur via Azure CDN
Lorsque vous intégrez un rôle Web de service cloud avec Azure CDN, il est relativement facile tooserve le contenu à partir d’actions de contrôleur via hello Azure CDN. Autre que desservant votre cloud service directement par le biais d’Azure CDN (illustré ci-dessus), [Maarten Balliauw](https://twitter.com/maartenballiauw) vous montre comment toodo avec un fun contrôleur MemeGenerator [ce qui réduit la latence sur le web hello avec hello CDN Azure ](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN). Je reproduis simplement cette page ici.

Supposons que votre service cloud, vous souhaitez memes toogenerate basée sur une image Chuck Norris jeune (photo par [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) comme suit :

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

Vous avez un simple `Index` qui permet aux clients de hello superlatifs de hello toospecify dans l’image de hello, puis génère hello MIME une fois qu’ils publient toohello action. Dans la mesure où il s’agit de Chuck Norris, vous vous attendez toobecome de cette page grandement populaires globalement. Cet exemple illustre bien la distribution de contenu semi-dynamique avec Azure CDN.

Suivez les étapes ci-dessus toosetup, hello cette action de contrôleur :

1. Bonjour *\Controllers* dossier, créez un nouveau fichier .cs appelé *MemeGeneratorController.cs* et hello remplacer avec hello après le code. Être vraiment partie en surbrillance tooreplace hello avec le nom de votre CDN.  
   
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;
   
        namespace WebRole1.Controllers
        {
            public class MemeGeneratorController : Controller
            {
                static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();
   
                public ActionResult Index()
                {
                    return View();
                }
   
                [HttpPost, ActionName("Index")]
                public ActionResult Index_Post(string top, string bottom)
                {
                    var identifier = Guid.NewGuid().ToString();
                    if (!Memes.ContainsKey(identifier))
                    {
                        Memes.Add(identifier, new Tuple<string, string>(top, bottom));
                    }
   
                    return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
                }
   
                [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
                public ActionResult Show(string id)
                {
                    Tuple<string, string> data = null;
                    if (!Memes.TryGetValue(id, out data))
                    {
                        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
                    }
   
                    if (Debugger.IsAttached) // Preserve hello debug experience
                    {
                        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                    else // Get content from Azure CDN
                    {
                        return Redirect(string.Format("http://<yourCdnName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                }
   
                [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
                public ActionResult Generate(string top, string bottom)
                {
                    string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
                    Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);
   
                    using (Graphics graphics = Graphics.FromImage(bitmap))
                    {
                        SizeF size = new SizeF();
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                        }
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                        }
                    }
   
                    MemoryStream ms = new MemoryStream();
                    bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    return File(ms.ToArray(), "image/png");
                }
   
                private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
                {
                    // Compute actual size, shrink if needed
                    while (true)
                    {
                        size = g.MeasureString(text, font);
   
                        // It fits, back out
                        if (size.Height < i.Height &&
                             size.Width < i.Width) { return font; }
   
                        // Try a smaller font (90% of old size)
                        Font oldFont = font;
                        font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                        oldFont.Dispose();
                    }
                }
            }
        }
2. Avec le bouton droit dans la valeur par défaut hello `Index()` action et sélectionnez **ajouter une vue**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. Acceptez les paramètres hello ci-dessous et cliquez sur **ajouter**.
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. Ouvrez hello nouvelle *Views\MemeGenerator\Index.cshtml* et remplacez le contenu hello hello suivant HTML simple pour l’envoi de superlatifs de hello :
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. Publiez de nouveau service de cloud computing hello et accédez trop**http://*&lt;serviceName >*.cloudapp.net/MemeGenerator/Index** dans votre navigateur.

Lorsque vous envoyez des valeurs de formulaire hello trop`/MemeGenerator/Index`, hello `Index_Post` méthode d’action renvoie un lien de toohello `Show` méthode d’action avec l’identificateur d’entrée de hello respectifs. Lorsque vous cliquez sur le lien de hello, vous atteignez hello suivant de code :  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve hello debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

Si votre débogueur local est connecté, vous obtiendrez expérience de débogage normal hello avec une redirection locale. Si elle est en cours d’exécution dans le service cloud hello, elle sera rediriger vers :

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

Qui correspond à toohello suivant l’URL d’origine au point de terminaison CDN :

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


Vous pouvez ensuite utiliser hello `OutputCacheAttribute` attribut sur hello `Generate` toospecify méthode comment résultat d’action hello doit être mise en cache, qui respecte Azure CDN. code Hello ci-dessous spécifient une expiration du cache de 1 heure (3 600 secondes).

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

De même, vous pouvez traiter le contenu à partir d’une action de contrôleur dans votre service cloud via le CDN Azure, avec l’option de mise en cache hello souhaité.

Dans la section suivante de hello, je vous indiquera comment tooserve hello groupée et réduire les scripts et CSS via le CDN Azure.

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a>Intégration du regroupement et de la minimisation d'ASP.NET avec Azure CDN
Feuilles de style CSS et des scripts changent peu souvent et sont des candidats idéaux pour hello du cache du CDN Azure. Service hello ensemble Web du rôle via le CDN Azure est toointegrate de façon plus simple de hello groupement et la minimisation avec Azure CDN. Toutefois, comme vous ne voulez pas toodo cela, je vous indiquera comment toodo qu’il tout en conservant hello souhaité expérience de programme de groupement d’ASP.NET et la minimisation, telles que :

* Mode débogage puissant
* Facilité de déploiement
* Tooclients mises à jour immédiate des mises à niveau de version de script/CSS
* Mécanisme de secours en cas de défaillance de votre point de terminaison CDN
* Modifications minimales du code

Bonjour **WebRole1** projet que vous avez créé dans [intégrer un point de terminaison CDN Azure avec votre site Web Azure et du contenu statique dans vos pages Web à partir d’Azure CDN](#deploy), ouvrez *App_Start\ BundleConfig.cs* et examinez hello `bundles.Add()` les appels de méthode.

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

Hello tout d’abord `bundles.Add()` instruction ajoute un regroupement de script au répertoire virtuel de hello `~/bundles/jquery`. Ensuite, ouvrez *Views\Shared\_Layout.cshtml* toosee la balise de regroupement de script hello est rendu. Vous devez être hello toofind en mesure de la ligne de code Razor suivante :

    @Scripts.Render("~/bundles/jquery")

Lorsque ce code Razor est exécuté dans le rôle Web Azure de hello, il affichera une `<script>` hello balise de script suivant toohello similaire de regroupement :

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

Toutefois, lors de son exécution dans Visual Studio en tapant `F5`, il doit rendre individuellement chaque fichier de script dans une offre groupée de hello (dans le cas de hello ci-dessus, uniquement un fichier de script est dans le groupe de hello) :

    <script src="/Scripts/jquery-1.10.2.js"></script>

Cela vous permet du code JavaScript dans votre environnement de développement toodebug hello lors de la réduction des connexions clientes simultanées (regroupement) et l’amélioration de fichier téléchargement performances (minimisation) en production. Il s’agit d’un toopreserve fonctionnalité intéressante avec intégration d’Azure CDN. En outre, étant donné que le groupe de hello rendu contient déjà une chaîne de version généré automatiquement, vous souhaitez tooreplicate fonctionnalité hello par conséquent, lorsque vous mettez à jour votre version de jQuery via NuGet, il peut être mis à jour côté client de hello dès que possible.

Suivez les étapes de hello ci-dessous groupement de ASP.NET de toointegration et la minimisation avec votre point de terminaison CDN.

1. Dans les *App_Start\BundleConfig.cs*, modifier hello `bundles.Add()` toouse méthodes une autre [constructeur d’offre groupée](http://msdn.microsoft.com/library/jj646464.aspx), qui spécifie une adresse CDN. toodo, hello remplacer `RegisterBundles` définition de méthode par hello suivant de code :  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            bundles.UseCdn = true;
            var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
                .GetName().Version.ToString();
            var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?v=" + version;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                        "~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                        "~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you're
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    Être vraiment tooreplace `<yourCDNName>` nom hello de votre CDN Azure.
   
    Clairement, vous définissez `bundles.UseCdn = true` et ajouté un regroupement de tooeach URL du CDN élaborées avec soin. Par exemple, hello premier constructeur dans le code hello :
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    est hello identique :
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    Ce constructeur indique à ASP.NET groupement et la minimisation toorender des fichiers de script individuels lors du débogage localement, mais utilisez hello spécifié CDN tooaccess hello un script adresses en question. Cependant, notez deux caractéristiques importantes avec cette URL CDN correctement formatée :
   
   * l’origine de cette URL CDN Hello est `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, qui est réellement hello répertoire virtuel du regroupement de script hello dans votre service cloud.
   * Étant donné que vous utilisez le constructeur CDN, hello balise de script CDN pour le regroupement de hello contient ne sont plus chaîne de version de hello généré automatiquement Bonjour rendu d’URL. Vous devez générer manuellement une chaîne de version unique chaque fois que regroupement de script hello est modifié tooforce un cache manquent à votre Azure CDN. AT hello même temps, cette chaîne de version unique doit rester constante via vie hello hello déploiement toomaximize d’accès du cache à votre Azure CDN après le regroupement de hello est déployé.
   * chaîne de requête v de Hello = extrait < W.X.Y.Z > à partir de *Properties\AssemblyInfo.cs* dans votre projet de rôle Web. Vous pouvez avoir un flux de travail de déploiement qui inclut l’incrémentation de version de l’assembly hello chaque fois que vous publiez tooAzure. Ou bien, vous pouvez simplement modifier *Properties\AssemblyInfo.cs* dans votre chaîne de version de projet tooautomatically incrément hello chaque fois que vous générez, à l’aide de caractère générique de hello ' *'. Par exemple :
     
        [assembly: AssemblyVersion("1.0.0.*")]
     
     Toutes les autres toostreamline stratégie générant une chaîne unique pour la durée de vie hello d’un déploiement fonctionne ici.
2. Republier hello cloud service et l’accès hello page d’accueil.
3. Hello vue code HTML de la page de hello. Vous devez être en mesure de toosee hello URL du CDN rendu, avec une chaîne de version unique chaque fois que vous republiez le service de cloud de tooyour de modifications. Par exemple :  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. Dans Visual Studio, déboguer le service de cloud computing hello dans Visual Studio en tapant `F5`.,
5. Hello vue code HTML de la page de hello. Vous voyez chaque fichier de script restitué individuellement de façon à effectuer un débogage cohérent dans Visual Studio.  
   
        ...
   
            <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
   
            <script src="/Scripts/modernizr-2.6.2.js"></script>
   
        ...
   
            <script src="/Scripts/jquery-1.10.2.js"></script>
   
            <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
   
        ...   

<a name="fallback"></a>

## <a name="fallback-mechanism-for-cdn-urls"></a>Mécanisme de secours pour les URL CDN
Lorsque votre point de terminaison CDN Azure échoue pour une raison quelconque, vous souhaitez que votre toobe page Web actives suffisamment tooaccess votre serveur Web d’origine comme solution de secours hello pour charger JavaScript ou amorçage. Il est suffisamment graves toolose des images sur votre site Web en raison de tooCDN indisponibilité, mais beaucoup plus grave fonctionnalité de page cruciale toolose fournie par vos scripts et les feuilles de style.

Hello [groupe](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) classe contient une propriété appelée [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) qui vous permet de mécanisme de secours hello tooconfigure de l’échec CDN. toouse cette propriété, hello suivez les étapes ci-dessous :

1. Dans votre projet de rôle Web, ouvrez *App_Start\BundleConfig.cs*, où vous avez ajouté une URL du CDN dans chaque [constructeur d’offre groupée](http://msdn.microsoft.com/library/jj646464.aspx)et suit hello mis en surbrillance change tooadd mécanisme de secours toohello lots de la valeur par défaut :  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
                .GetName().Version.ToString();
            var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
            bundles.UseCdn = true;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
                        { CdnFallbackExpression = "window.jquery" }
                        .Include("~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval"))
                        { CdnFallbackExpression = "$.validator" }
                        .Include("~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer"))
                        { CdnFallbackExpression = "window.Modernizr" }
                        .Include("~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                        { CdnFallbackExpression = "$.fn.modal" }
                        .Include(
                                  "~/Scripts/bootstrap.js",
                                  "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    Lorsque `CdnFallbackExpression` est non null, script injecter hello HTML tootest si l’offre groupée de hello est chargée avec succès et dans le cas contraire, accéder hello regroupement directement à partir de serveur Web d’origine hello. Cette propriété doit toobe ensemble expression tooa JavaScript qui teste si l’offre groupée de hello respectif CDN est chargée correctement. expression de Hello requise tootest chaque lot diffère en fonction toohello contenu. Pour les offres de valeur par défaut hello ci-dessus :
   
   * `window.jquery` est défini dans jquery-{version}.js
   * `$.validator` est défini dans jquery.validate.js
   * `window.Modernizr` est défini dans modernizer-{version}.js
   * `$.fn.modal` est défini dans bootstrap.js
     
     Vous avez peut-être remarqué que vous n’avez pas défini CdnFallbackExpression pour hello `~/Cointent/css` offre groupée. Il s’agit, car il n’y a un [bogue dans System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) qui injecte un `<script>` balise pour hello attendu de secours CSS au lieu de hello `<link>` balise.
     
     Il existe néanmoins un bon [mécanisme de secours pour les styles](https://github.com/EmberConsultingGroup/StyleBundleFallback) proposé par [Ember Consulting Group](https://github.com/EmberConsultingGroup).
2. solution de contournement toouse hello pour CSS, créer un nouveau fichier .cs dans votre projet de rôle Web *App_Start* dossier appelé *StyleBundleExtensions.cs*et remplacez son contenu hello [à partir de code GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).
3. Dans *App_Start\StyleFundleExtensions.cs*, renommez le nom du rôle Web hello espace de noms tooyour (par exemple, **WebRole1**).
4. Revenir en arrière trop`App_Start\BundleConfig.cs` et modifier hello dernière `bundles.Add` instruction avec hello suivant le code en surbrillance :  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    Cette nouvelle méthode d’extension utilise hello même idée tooinject script hello HTML toocheck hello DOM pourquoi un nom de classe correspondant, nom de la règle et valeur de la règle définie dans hello CSS lot et se situe toohello précédent serveur Web d’origine en cas d’échec de correspondance de hello toofind.
5. Publier à nouveau le service cloud hello et la page d’accueil access hello.
6. Hello vue code HTML de la page de hello. Vous devez rechercher les scripts injecté similaire toohello suivantes :    
   
        ...
   
        <link href="http://az632148.azureedge.net/Content/css?v=1.0.0.25474" rel="stylesheet"/>
        <script>(function() {
                        var loadFallback,
                            len = document.styleSheets.length;
                        for (var i = 0; i < len; i++) {
                            var sheet = document.styleSheets[i];
                            if (sheet.href.indexOf('http://camservice.azureedge.net/Content/css?v=1.0.0.25474') !== -1) {
                                var meta = document.createElement('meta');
                                meta.className = 'sr-only';
                                document.head.appendChild(meta);
                                var value = window.getComputedStyle(meta).getPropertyValue('width');
                                document.head.removeChild(meta);
                                if (value !== '1px') {
                                    document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                                }
                            }
                        }
                        return true;
                    }())||document.write('<script src="/Content/css"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25474"></script>
        <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
   
        ...
   
            <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25474"></script>
        <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25474"></script>
        <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
   
        ...

    Notez que script injecté hello CSS regroupement contient encore restante exempte de malintentionné hello de hello `CdnFallbackExpression` propriété dans la ligne de hello :

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    Mais depuis la première partie de hello Hello || expression retourne toujours true (sur ligne hello directement au-dessus), la fonction de hello document.Write () ne sera jamais exécuté.

## <a name="more-information"></a>Informations complémentaires
* [Vue d’ensemble de hello réseau de distribution contenu (CDN) Azure](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [Utilisation d’Azure CDN](cdn-create-new-endpoint.md)
* [Regroupement et minimisation d’ASP.NET](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
