---
title: "aaaCreate une API REST dans Azure avec ASP.NET et la base de données SQL | Documents Microsoft"
description: "Un didacticiel qui vous apprend de comment toodeploy une application qui utilise hello tooan de l’API Web ASP.NET application web Azure à l’aide de Visual Studio."
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
writer: Rick-Anderson
manager: erikre
editor: 
ms.assetid: f4916fc0-ea08-41f7-846b-73e41bc88149
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: riande
ms.openlocfilehash: 1ef45dd1582bfda367e53c39f863164422ad678b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a>Créer un service REST à l’aide de l’API Web ASP.NET et de Base de données SQL dans Azure App Service
Ce didacticiel montre comment toodeploy ASP.NET web application tooan [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) en utilisant l’Assistant de publication Web hello dans Visual Studio 2013 ou Visual Studio 2013 Community Edition. 

Vous pouvez ouvrir un compte Azure gratuit, et si vous ne disposez pas de Visual Studio 2013, hello SDK installe automatiquement Visual Studio 2013 pour Web Express. Vous pouvez donc commencer vos développements Azure gratuitement.

Ce didacticiel part du principe que vous n'avez pas d'expérience en tant qu'utilisateur d'Azure. Une fois ce didacticiel, vous avez une application web simple haut et en cours d’exécution dans le cloud de hello.

Vous apprendrez ce qui suit :

* Comment tooenable votre ordinateur pour le développement Azure en installant hello Azure SDK.
* Comment toocreate un Visual Studio ASP.NET MVC 5 du projet et publiez-le tooan application Azure.
* Appels d’API Restful comment toouse hello tooenable de l’API Web ASP.NET.
* Toouse SQL base de données toostore dans Azure.
* Comment toopublish application met à jour tooAzure.

Vous allez générer une application web de liste de contacts simple qui repose sur ASP.NET MVC 5 et utilise hello ADO.NET Entity Framework pour l’accès de la base de données. Hello suivant illustration montre hello terminé l’application :

![capture d’écran du site Web][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-hello-project"></a>Créer le projet de hello
1. Démarrez Visual Studio 2013.
2. À partir de hello **fichier** menu, cliquez sur **nouveau projet**.
3. Bonjour **nouveau projet** boîte de dialogue, développez **Visual C#** et sélectionnez **Web** , puis sélectionnez **Application Web ASP.NET**. Nommez l’application hello **ContactManager** et cliquez sur **OK**.
   
    ![Boîte de dialogue Nouveau projet](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. Bonjour **nouveau projet ASP.NET** boîte de dialogue, sélectionnez hello **MVC** modèle, cocher **API Web** puis cliquez sur **modifier l’authentification**.
5. Bonjour **modifier l’authentification** boîte de dialogue, cliquez sur **aucune authentification**, puis cliquez sur **OK**.
   
    ![Aucune authentification](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    exemple d’application Hello que vous créez ne sont pas ont des fonctionnalités qui nécessitent des toolog d’utilisateurs dans. Pour plus d’informations sur la façon tooimplement des fonctionnalités d’authentification et d’autorisation, consultez hello [étapes](#nextsteps) section à fin hello de ce didacticiel. 
6. Bonjour **nouveau projet ASP.NET** boîte de dialogue, vérifiez les hello que **hôte Bonjour Cloud** est activée et cliquez sur **OK**.

Si vous n’êtes pas déjà inscrit dans tooAzure, vous serez invité à toosign dans.

1. Assistant de configuration Hello suggère un nom unique basé sur *ContactManager* (voir l’image hello ci-dessous). Sélectionnez une région proche de chez vous. Vous pouvez utiliser [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") centre de données de latence la plus faible toofind hello. 
2. Si vous n’avez pas créé de serveur de base de données, sélectionnez **Créer un serveur**, entrez un nom d’utilisateur et un mot de passe de base de données.
   
    ![Configuration du site Web Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

Si vous avez un serveur de base de données, utilisez ce toocreate une base de données. Les serveurs de base de données sont une ressource précieuse, et que vous souhaitez généralement toocreate plusieurs bases de données sur hello même serveur de test et développement au lieu de créer un serveur de base de données par base de données. Assurez-vous que votre site web et la base de données sont Bonjour même région.

![Configuration du site Web Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-hello-page-header-and-footer"></a>Page hello en-tête et pied de page
1. Dans **l’Explorateur de solutions**, développez hello *Views\Shared* dossier et ouvrez hello *_Layout.cshtml* fichier.
   
    ![_Layout.cshtml dans l'Explorateur de solutions][newapp004]
2. Remplacez le contenu hello Hello *Views\Shared_Layout.cshtml* fichier avec hello suivant de code :

        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="utf-8" />
            <title>@ViewBag.Title - Contact Manager</title>
            <link href="~/favicon.ico" rel="shortcut icon" type="image/x-icon" />
            <meta name="viewport" content="width=device-width" />
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
        </head>
        <body>
            <header>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p class="site-title">@Html.ActionLink("Contact Manager", "Index", "Home")</p>
                    </div>
                </div>
            </header>
            <div id="body">
                @RenderSection("featured", required: false)
                <section class="content-wrapper main-content clear-fix">
                    @RenderBody()
                </section>
            </div>
            <footer>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p>&copy; @DateTime.Now.Year - Contact Manager</p>
                    </div>
                </div>
            </footer>
            @Scripts.Render("~/bundles/jquery")
            @RenderSection("scripts", required: false)
        </body>
        </html>

balisage de Hello au-dessus de nom de l’application hello modifications à partir de « My ASP.NET App » trop « Contact Manager » et il supprime les liens hello trop**accueil**, **sur** et **Contact**.

### <a name="run-hello-application-locally"></a>Exécutez hello application localement
1. Appuyez sur la touche application de hello toorun CTRL + F5.
   page d’accueil application Hello s’affiche dans le navigateur par défaut de hello.
    ![page d’accueil liste tooDo](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)

Cela est que nécessaire pour l’application de hello toocreate maintenant que vous allez déployer tooAzure toodo. Après cela, vous allez ajouter les fonctionnalités de base de données.

## <a name="deploy-hello-application-tooazure"></a>Déployer hello application tooAzure
1. Dans Visual Studio, cliquez sur projet hello dans **l’Explorateur de solutions** et sélectionnez **publier** à partir du menu contextuel de hello.
   
    ![Publier dans le menu contextuel du projet][PublishVSSolution]
   
    Hello **publier le site Web** Assistant s’ouvre.
2. Cliquez sur **Publier**.

![Onglet Paramètres](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

Visual Studio commence le processus hello hello fichiers toohello serveur Azure à copier. Hello **sortie** fenêtre affiche les actions de déploiement ont été effectuées et signale la réussite du déploiement de hello.

1. navigateur par défaut de Hello ouvre automatiquement toohello les URL du site de hello déployé.
   
   application Hello que vous avez créé est en cours d’exécution dans le cloud de hello.
   
   ![page d’accueil liste tooDo s’exécutant dans Azure][rxz2]

## <a name="add-a-database-toohello-application"></a>Ajouter une application toohello de base de données
Ensuite, vous allez mettre à jour hello MVC application tooadd hello capacité toodisplay et mettre à jour contacts stocker les données de hello dans une base de données. application Hello utilise tooread et la base de données hello Entity Framework toocreate hello et mettre à jour des données dans la base de données hello.

### <a name="add-data-model-classes-for-hello-contacts"></a>Ajouter des classes de modèle de données pour les contacts de hello
Commencez par créer un modèle de données simple dans le code.

1. Dans **l’Explorateur de solutions**, cliquez sur le dossier de modèles hello, cliquez sur **ajouter**, puis **classe**.
   
    ![Menu contextuel Ajouter une classe aux modèles][adddb001]
2. Bonjour **ajouter un nouvel élément** boîte de dialogue, le fichier de classe nom hello *Contact.cs*, puis cliquez sur **ajouter**.
   
    ![Boîte de dialogue Ajouter un nouvel élément][adddb002]
3. Remplacez contenu hello du fichier de Contacts.cs hello hello suivant de code.
   
        using System.Globalization;
        namespace ContactManager.Models
        {
            public class Contact
               {
                public int ContactId { get; set; }
                public string Name { get; set; }
                public string Address { get; set; }
                public string City { get; set; }
                public string State { get; set; }
                public string Zip { get; set; }
                public string Email { get; set; }
                public string Twitter { get; set; }
                public string Self
                {
                    get { return string.Format(CultureInfo.CurrentCulture,
                         "api/contacts/{0}", this.ContactId); }
                    set { }
                }
            }
        }

Hello **contactez** classe définit les données de hello que vous souhaitez stocker pour chaque contact, plus une clé primaire, ContactID, qui est requise par la base de données hello. Vous pouvez obtenir plus d’informations sur les modèles de données Bonjour [étapes](#nextsteps) section à fin hello de ce didacticiel.

### <a name="create-web-pages-that-enable-app-users-toowork-with-hello-contacts"></a>Créer des pages web qui permettent de toowork d’utilisateurs d’application avec des contacts de hello
Hello fonctionnalité de génération de modèles automatique ASP.NET MVC hello peut générer automatiquement le code qui effectue créer, lire, mettre à jour et supprimer des actions (CRUD).

## <a name="add-a-controller-and-a-view-for-hello-data"></a>Ajouter un contrôleur et une vue de données de salutation
1. Dans **l’Explorateur de solutions**, développez le dossier de contrôleurs hello.
2. Générez le projet de hello **(Ctrl + Maj + B)**. (Vous devez générer le projet de hello avant d’utiliser le mécanisme de génération de modèles automatique.) 
3. Cliquez sur le dossier de contrôleurs hello, sur **ajouter**, puis cliquez sur **contrôleur**.
   
    ![Ajouter un contrôleur dans le menu contextuel du dossier Contrôleurs][addcode001]
4. Bonjour **ajouter une vue de structure** boîte de dialogue, sélectionnez **contrôleur MVC avec vues, utilisant Entity Framework** et cliquez sur **ajouter**.
   
   ![Ajouter un contrôleur](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. Définir le nom du contrôleur hello trop**HomeController**. Sélectionnez **Contact** comme classe de modèle. Cliquez sur hello **nouveau contexte de données** bouton et acceptez la valeur par défaut de hello « ContactManager.Models.ContactManagerContext » pour hello **nouveau type de contexte de données**. Cliquez sur **Add**.

    Une boîte de dialogue vous invite à vous : « un fichier portant le nom de hello HomeController existe déjà. Voulez-vous vraiment tooreplace il ? ». Cliquez sur **Oui**. Nous sommes remplacement hello contrôleur Home qui a été créé avec un nouveau projet de hello. Nous allons utiliser hello nouvelle accueil contrôleur pour notre liste de contacts.

    Visual Studio crée des méthodes de contrôleur et des vues pour les opérations de base de données CRUD des objets **Contact** .

## <a name="enable-migrations-create-hello-database-add-sample-data-and-a-data-initializer"></a>Activer les Migrations, créer la base de données hello, ajouter un initialiseur de données et des exemples de données
la tâche suivante Hello est tooenable hello [Migrations Code First](http://curah.microsoft.com/55220) fonctionnalité dans la base de données de commandes toocreate hello en fonction de modèle de données hello vous avez créé.

1. Bonjour **outils** menu, sélectionnez **Gestionnaire de Package de bibliothèque** , puis **Package Manager Console**.
   
    ![Console du Gestionnaire de package dans le menu Outils][addcode008]
2. Bonjour **Package Manager Console** fenêtre, entrez hello de commande suivante :
   
        enable-migrations 
   
    Hello **enable-migrations** commande crée un *Migrations* dossier et qu’il place dans ce dossier un *Configuration.cs* fichier que vous pouvez modifier les Migrations tooconfigure. 
3. Bonjour **Package Manager Console** fenêtre, entrez hello de commande suivante :
   
        add-migration Initial
   
    Hello **Initial de la migration ajouter** commande génère une classe nommée  **&lt;date_stamp&gt;initiale** qui crée la base de données hello. Hello du premier paramètre ( *initiale* ) nom de hello toocreate arbitraire et utilisé du fichier de hello. Vous pouvez voir les nouveaux fichiers de classe hello dans **l’Explorateur de solutions**.
   
    Bonjour **initiale** classe hello **des** méthode crée la table Contacts de hello et hello **vers le bas** dépose (méthode) (utilisé lorsque vous souhaitez que l’état précédent de tooreturn toohello).
4. Ouvrez hello *Migrations\Configuration.cs* fichier. 
5. Ajoutez hello suivant des espaces de noms. 
   
         using ContactManager.Models;
6. Remplacez hello *Seed* méthode avec hello suivant de code :
   
        protected override void Seed(ContactManager.Models.ContactManagerContext context)
        {
            context.Contacts.AddOrUpdate(p => p.Name,
               new Contact
               {
                   Name = "Debra Garcia",
                   Address = "1234 Main St",
                   City = "Redmond",
                   State = "WA",
                   Zip = "10999",
                   Email = "debra@example.com",
                   Twitter = "debra_example"
               },
                new Contact
                {
                    Name = "Thorsten Weinrich",
                    Address = "5678 1st Ave W",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "thorsten@example.com",
                    Twitter = "thorsten_example"
                },
                new Contact
                {
                    Name = "Yuhong Li",
                    Address = "9012 State st",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "yuhong@example.com",
                    Twitter = "yuhong_example"
                },
                new Contact
                {
                    Name = "Jon Orton",
                    Address = "3456 Maple St",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "jon@example.com",
                    Twitter = "jon_example"
                },
                new Contact
                {
                    Name = "Diliana Alexieva-Bosseva",
                    Address = "7890 2nd Ave E",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "diliana@example.com",
                    Twitter = "diliana_example"
                }
                );
        }
   
    Ce code ci-dessus initialisera la base de données de hello avec les informations de contact hello. Pour plus d’informations sur la base de données hello l’amorçage, consultez [les bases de données Entity Framework (EF) débogage](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).
7. Bonjour **Package Manager Console** Entrez la commande hello :
   
        update-database
   
    ![Commandes de la Console du Gestionnaire de package][addcode009]
   
    Hello **mise à jour de la base de données** séries hello première migration qui crée la base de données hello. Par défaut, la base de données de hello est créée en tant qu’une base de données SQL Server Express LocalDB.
8. Appuyez sur la touche application de hello toorun CTRL + F5. 

application Hello affiche les données de valeur initiale hello et fournit les modifier, détails et les liens de suppression.

![Affichage MVC des données][rxz3]

## <a name="edit-hello-view"></a>Modifier hello vue
1. Ouvrez hello *Views\Home\Index.cshtml* fichier. Dans l’étape suivante de hello, nous remplaçons balisage de hello généré par le code qui utilise [jQuery](http://jquery.com/) et [Knockout.js](http://knockoutjs.com/). Ce nouveau code récupère la liste des contacts hello d’à l’aide des API web et JSON, puis lie hello contactez données toohello l’interface utilisateur à l’aide de knockout.js. Pour plus d’informations, consultez hello [étapes](#nextsteps) section à fin hello de ce didacticiel. 
2. Remplacez contenu hello du fichier de hello hello suivant de code.
   
        @model IEnumerable<ContactManager.Models.Contact>
        @{
            ViewBag.Title = "Home";
        }
        @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                function ContactsViewModel() {
                    var self = this;
                    self.contacts = ko.observableArray([]);
                    self.addContact = function () {
                        $.post("api/contacts",
                            $("#addContact").serialize(),
                            function (value) {
                                self.contacts.push(value);
                            },
                            "json");
                    }
                    self.removeContact = function (contact) {
                        $.ajax({
                            type: "DELETE",
                            url: contact.Self,
                            success: function () {
                                self.contacts.remove(contact);
                            }
                        });
                    }
   
                    $.getJSON("api/contacts", function (data) {
                        self.contacts(data);
                    });
                }
                ko.applyBindings(new ContactsViewModel());    
        </script>
        }
        <ul id="contacts" data-bind="foreach: contacts">
            <li class="ui-widget-content ui-corner-all">
                <h1 data-bind="text: Name" class="ui-widget-header"></h1>
                <div><span data-bind="text: $data.Address || 'Address?'"></span></div>
                <div>
                    <span data-bind="text: $data.City || 'City?'"></span>,
                    <span data-bind="text: $data.State || 'State?'"></span>
                    <span data-bind="text: $data.Zip || 'Zip?'"></span>
                </div>
                <div data-bind="if: $data.Email"><a data-bind="attr: { href: 'mailto:' + Email }, text: Email"></a></div>
                <div data-bind="ifnot: $data.Email"><span>Email?</span></div>
                <div data-bind="if: $data.Twitter"><a data-bind="attr: { href: 'http://twitter.com/' + Twitter }, text: '@@' + Twitter"></a></div>
                <div data-bind="ifnot: $data.Twitter"><span>Twitter?</span></div>
                <p><a data-bind="attr: { href: Self }, click: $root.removeContact" class="removeContact ui-state-default ui-corner-all">Remove</a></p>
            </li>
        </ul>
        <form id="addContact" data-bind="submit: addContact">
            <fieldset>
                <legend>Add New Contact</legend>
                <ol>
                    <li>
                        <label for="Name">Name</label>
                        <input type="text" name="Name" />
                    </li>
                    <li>
                        <label for="Address">Address</label>
                        <input type="text" name="Address" >
                    </li>
                    <li>
                        <label for="City">City</label>
                        <input type="text" name="City" />
                    </li>
                    <li>
                        <label for="State">State</label>
                        <input type="text" name="State" />
                    </li>
                    <li>
                        <label for="Zip">Zip</label>
                        <input type="text" name="Zip" />
                    </li>
                    <li>
                        <label for="Email">E-mail</label>
                        <input type="text" name="Email" />
                    </li>
                    <li>
                        <label for="Twitter">Twitter</label>
                        <input type="text" name="Twitter" />
                    </li>
                </ol>
                <input type="submit" value="Add" />
            </fieldset>
        </form>
3. Cliquez sur le dossier de contenu hello, sur **ajouter**, puis cliquez sur **un nouvel élément...** .
   
    ![Ajouter une feuille de style dans le menu contextuel du dossier Contenu][addcode005]
4. Bonjour **ajouter un nouvel élément** boîte de dialogue, entrez **Style** dans hello de zone de recherche du volet supérieur droit, puis sélectionnez **feuille de Style**.
    ![Boîte de dialogue Ajouter un nouvel élément][rxStyle]
5. Nom de fichier hello *Contacts.css* et cliquez sur **ajouter**. Remplacez contenu hello du fichier de hello hello suivant de code.
   
        .column {
            float: left;
            width: 50%;
            padding: 0;
            margin: 5px 0;
        }
        form ol {
            list-style-type: none;
            padding: 0;
            margin: 0;
        }
        form li {
            padding: 1px;
            margin: 3px;
        }
        form input[type="text"] {
            width: 100%;
        }
        #addContact {
            width: 300px;
            float: left;
            width:30%;
        }
        #contacts {
            list-style-type: none;
            margin: 0;
            padding: 0;
            float:left;
            width: 70%;
        }
        #contacts li {
            margin: 3px 3px 3px 0;
            padding: 1px;
            float: left;
            width: 300px;
            text-align: center;
            background-image: none;
            background-color: #F5F5F5;
        }
        #contacts li h1
        {
            padding: 0;
            margin: 0;
            background-image: none;
            background-color: Orange;
            color: White;
            font-family: Trebuchet MS, Tahoma, Verdana, Arial, sans-serif;
        }
        .removeContact, .viewImage
        {
            padding: 3px;
            text-decoration: none;
        }
   
    Nous allons utiliser cette feuille de style pour la mise en page hello, couleurs et styles utilisés dans l’application du Gestionnaire de contacts hello.
6. Ouvrez hello *App_Start\BundleConfig.cs* fichier.
7. Ajouter hello suivant hello tooregister de code [Knockout](http://knockoutjs.com/index.html "KO") plug-in.
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    Cet exemple à l’aide de knockout toosimplify dynamique du code JavaScript qui gère les modèles d’écran hello.
8. Modifier hello de hello contenu/css entrée tooregister *contacts.css* feuille de style. Modifier hello ligne suivante :
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   Par :
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. Dans la Console du Gestionnaire de Package de hello, exécutez hello suivant commande tooinstall Knockout.
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-hello-web-api-restful-interface"></a>Ajouter un contrôleur pour l’interface Web API Restful de hello
1. Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur Contrôleurs, cliquez sur **Ajouter**, puis sur **Contrôleur...** 
2. Bonjour **ajouter une vue de structure** boîte de dialogue, entrez **Web API 2 contrôleur avec actions, utilisant Entity Framework** puis cliquez sur **ajouter**.
   
    ![Ajouter un contrôleur API](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. Bonjour **ajouter un contrôleur** boîte de dialogue, entrez « ContactsController » comme nom de votre contrôleur. Sélectionnez « Contact (ContactManager.Models) » pour hello **classe de modèle**.  Conserver la valeur par défaut de hello pour hello **classe de contexte de données**. 
4. Cliquez sur **Add**.

### <a name="run-hello-application-locally"></a>Exécutez hello application localement
1. Appuyez sur la touche application de hello toorun CTRL + F5.
   
    ![Page d'index][intro001]
2. Entrez un contact, puis cliquez sur **Ajouter**. application Hello retourne la page d’accueil toohello et affiche le contact hello que vous avez entré.
   
    ![Page d'index avec éléments de liste des tâches][addwebapi004]
3. Dans le navigateur de hello, ajoutez **/api/contacts** toohello URL.
   
    les URL qui en résulte Hello ressemblera http://localhost:1234/api/contacts. web RESTful de Hello API que vous avez ajouté retourne les contacts stockée hello. Firefox et Chrome affiche les données de salutation au format XML.
   
    ![Page d'index avec éléments de liste des tâches][rxFFchrome]

    Internet Explorer est vous invite tooopen ou enregistrer les contacts de hello.

    ![Boîte de dialogue Enregistrer de l'API Web][addwebapi006]


    Vous pouvez ouvrir hello retourné de contacts dans le bloc-notes ou un navigateur.

    Ce résultat peut être utilisé par une autre application, comme une page Web ou une application mobile.

    ![Boîte de dialogue Enregistrer de l'API Web][addwebapi007]

    **Avertissement de sécurité**: À ce stade, votre application est non sécurisé et vulnérable tooCSRF attaque. Plus loin dans le didacticiel de hello, nous allons supprimer cette vulnérabilité. Pour plus d’informations, consultez la page [Prévention des falsifications de requête intersites][prevent-csrf-attacks].
## <a name="add-xsrf-protection"></a>Ajouter une protection XSRF
Falsification de requête (également appelé XSRF ou CSRF) est une attaque contre les applications hébergées par le web dans laquelle un site Web malveillant peut influencer interaction hello entre un navigateur client et un site Web approuvé par ce navigateur. Ces attaques sont possible parce que les navigateurs web envoie des jetons d’authentification automatiquement avec tous les sites Web tooa demande. exemple Hello est un cookie d’authentification, tels que ASP. Ticket d’authentification par formulaire de NET. Cependant, les sites Web utilisant un mécanisme d'authentification persistant (comme l'authentification Windows, Basic, etc.) peuvent être visés par ces attaques.

Une attaque XSRF est différente d'une attaque par hameçonnage (ou « phishing »). Des attaques d’hameçonnage requièrent une interaction à partir de la victime de hello. Dans une attaque par hameçonnage, un site Web malveillant reflétera le site Web cible de hello et victime de hello est croyez fournissant les intrus de toohello des informations sensibles. Dans une attaque XSRF, aucune interaction n’est souvent nécessaire de victime de hello. Au lieu de cela, les intrus hello repose sur navigateur hello envoyer automatiquement le site Web de destination toohello tous les cookies pertinentes.

Pour plus d’informations, consultez hello [ouvrir un projet Web Application sécurité](https://www.owasp.org/index.php/Main_Page) (OWASP avoir) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).

1. Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le projet **ContactManager**, cliquez sur **Ajouter**, puis sur **Classe**.
2. Nom de fichier hello *ValidateHttpAntiForgeryTokenAttribute.cs* et ajoutez hello suivant de code :
   
        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Helpers;
        using System.Web.Http.Controllers;
        using System.Web.Http.Filters;
        using System.Web.Mvc;
        namespace ContactManager.Filters
        {
            public class ValidateHttpAntiForgeryTokenAttribute : AuthorizationFilterAttribute
            {
                public override void OnAuthorization(HttpActionContext actionContext)
                {
                    HttpRequestMessage request = actionContext.ControllerContext.Request;
                    try
                    {
                        if (IsAjaxRequest(request))
                        {
                            ValidateRequestHeader(request);
                        }
                        else
                        {
                            AntiForgery.Validate();
                        }
                    }
                    catch (HttpAntiForgeryException e)
                    {
                        actionContext.Response = request.CreateErrorResponse(HttpStatusCode.Forbidden, e);
                    }
                }
                private bool IsAjaxRequest(HttpRequestMessage request)
                {
                    IEnumerable<string> xRequestedWithHeaders;
                    if (request.Headers.TryGetValues("X-Requested-With", out xRequestedWithHeaders))
                    {
                        string headerValue = xRequestedWithHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(headerValue))
                        {
                            return String.Equals(headerValue, "XMLHttpRequest", StringComparison.OrdinalIgnoreCase);
                        }
                    }
                    return false;
                }
                private void ValidateRequestHeader(HttpRequestMessage request)
                {
                    string cookieToken = String.Empty;
                    string formToken = String.Empty;
                    IEnumerable<string> tokenHeaders;
                    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
                    {
                        string tokenValue = tokenHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(tokenValue))
                        {
                            string[] tokens = tokenValue.Split(':');
                            if (tokens.Length == 2)
                            {
                                cookieToken = tokens[0].Trim();
                                formToken = tokens[1].Trim();
                            }
                        }
                    }
                    AntiForgery.Validate(cookieToken, formToken);
                }
            }
        }
3. Ajoutez hello suivant *à l’aide de* toohello d’instruction contrats contrôleur afin que vous ayez accès toohello **[ValidateHttpAntiForgeryToken]** attribut.
   
        using ContactManager.Filters;
4. Ajouter hello **[ValidateHttpAntiForgeryToken]** toohello des méthodes de publication de hello d’attribut **ContactsController** tooprotect à partir de menaces XSRF. Vous allez l’ajouter toohello « PutContact », « PostContact » et **DeleteContact** méthodes d’action.
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. Hello de mise à jour *Scripts* section Hello *Views\Home\Index.cshtml* les jetons XSRF hello tooinclude code tooget de fichiers.
   
         @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                @functions{
                   public string TokenHeaderValue()
                   {
                      string cookieToken, formToken;
                      AntiForgery.GetTokens(null, out cookieToken, out formToken);
                      return cookieToken + ":" + formToken;                
                   }
                }
   
               function ContactsViewModel() {
                  var self = this;
                  self.contacts = ko.observableArray([]);
                  self.addContact = function () {
   
                     $.ajax({
                        type: "post",
                        url: "api/contacts",
                        data: $("#addContact").serialize(),
                        dataType: "json",
                        success: function (value) {
                           self.contacts.push(value);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
                     });
   
                  }
                  self.removeContact = function (contact) {
                     $.ajax({
                        type: "DELETE",
                        url: contact.Self,
                        success: function () {
                           self.contacts.remove(contact);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
   
                     });
                  }
   
                  $.getJSON("api/contacts", function (data) {
                     self.contacts(data);
                  });
               }
               ko.applyBindings(new ContactsViewModel());
            </script>
         }

## <a name="publish-hello-application-update-tooazure-and-sql-database"></a>Publier tooAzure de mise à jour d’application hello et la base de données SQL
application de hello toopublish, vous répétez procédure hello que vous avez suivi le plus haut.

1. Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le projet hello et sélectionnez **publier**.
   
    ![Publier][rxP]
2. Cliquez sur hello **paramètres** onglet.
3. Sous **ContactsManagerContext(ContactsManagerContext)**, cliquez sur hello **v** icône toochange *chaîne de connexion à distance* toohello chaîne de connexion pour le contact de hello base de données. Cliquez sur **ContactDB**.
   
    ![Paramètres](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. Case de hello pour **exécuter fonctionnalité Migrations Code First (s’exécute sur le démarrage de l’application)**.
5. Cliquez sur **Suivant**, puis sur **Aperçu**. Visual Studio affiche une liste de fichiers hello qui seront ajoutés ou mis à jour.
6. Cliquez sur **Publier**.
   Après déploiement de hello, navigateur de hello ouvre toohello page d’accueil de l’application hello.
   
    ![Page d'index sans contacts][intro001]
   
    Hello Visual Studio publier la chaîne de connexion de processus configuré automatiquement hello Bonjour déployé *Web.config* base de données de fichier toopoint toohello SQL. Elle également configurée Migrations Code First tooautomatically hello mise à niveau de base de données toohello version la plus récente hello première heure hello application accède à des base de données hello après le déploiement.
   
    À la suite de cette configuration, Code First créé hello base de données en exécutant du code de hello Bonjour **initiale** classe que vous avez créé précédemment. Après le déploiement, il a cette hello première hello application a tenté de tooaccess hello de base de données.
7. Entrez un contact comme vous l’avez fait lors de l’exécution d’application hello localement, tooverify le déploiement de la base de données a réussi.

Lorsque vous voyez cet élément hello que vous entrez est enregistré et s’affiche sur la page du Gestionnaire de contacts hello, vous savez qu’elle a été stockée dans la base de données hello.

![Page d'index avec contacts][addwebapi004]

application Hello est en cours d’exécution dans le cloud de hello, à l’aide de la base de données SQL toostore ses données. Une fois que vous avez terminé de tester l’application hello dans Azure, supprimez-le. application Hello est publique et n’a pas un mécanisme toolimit.

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Une autre façon dont les données toostore dans une application Windows Azure sont toouse le stockage Azure, qui permettent de stocker des données non relationnelles sous forme de hello d’objets BLOB et tables. Hello suivant liens fournit plus d’informations sur les API Web, ASP.NET MVC et Windows Azure.

* [Mise en route d’Entity Framework avec MVC (en anglais)][EFCodeFirstMVCTutorial]
* [Introduction tooASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [Votre première API Web ASP.NET (en anglais)](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [Débogage de WAWS](web-sites-dotnet-troubleshoot-visual-studio.md)

Cet exemple d’application didacticiel et hello a été écrit par [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) avec l’assistance de Tom Dykstra et Barry Dorrans (Twitter [ @blowdart ](https://twitter.com/blowdart)). 

Veuillez laisser des commentaires sur ce que vous avez aimé ou ce que vous voulez toosee améliorée, non seulement sur didacticiel hello lui-même, mais également sur les produits de hello il montre. Vos commentaires nous aideront à orienter nos améliorations. Nous intéressent particulièrement savoir combien intérêt il est en plus d’automation pour les processus hello de configuration et de déploiement de base de données d’appartenance hello. 

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles toohello Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update hello Membership Database]:#ppd2
[setupdbenv]: #bkmk_setupdevenv
[setupwindowsazureenv]: #bkmk_setupwindowsazure
[createapplication]: #bkmk_createmvc4app
[deployapp1]: #bkmk_deploytowindowsazure1
[adddb]: #bkmk_addadatabase
[addcontroller]: #bkmk_addcontroller
[addwebapi]: #bkmk_addwebapi
[deploy2]: #bkmk_deploydatabaseupdate

<!-- links -->
[EFCodeFirstMVCTutorial]: http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
[dbcontext-link]: http://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx


<!-- images-->
[rxE]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxE.png
[rxP]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxP.png
[rx22]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/
[rxb2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxb2.png
[rxz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz.png
[rxzz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxzz.png
[rxz2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz2.png
[rxz3]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz3.png
[rxStyle]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxStyle.png
[rxz4]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz4.png
[rxz44]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz44.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxPrevDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPrevDB.png
[rxOverwrite]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxOverwrite.png
[rxPWS]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPWS.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxAddApiController]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxAddApiController.png
[rxFFchrome]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxFFchrome.png
[intro001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobil-intro-finished-web-app.png
[rxCreateWSwithDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxCreateWSwithDB.png
[setup007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-setup-azure-site-004.png
[setup009]: ../Media/dntutmobile-setup-azure-site-006.png
[newapp002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-002.png
[newapp004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-004.png
[firsdeploy007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-005.png
[firsdeploy009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-007.png
[adddb001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-001.png
[adddb002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-002.png
[addcode001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-context-menu.png
[addcode002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-controller-dialog.png
[addcode004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-index-context.png
[addcode005]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-contents-context-menu.png
[addcode007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-bundleconfig-context.png
[addcode008]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-menu.png
[addcode009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-console.png
[addwebapi004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-added-contact.png
[addwebapi006]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-save-returned-contacts.png
[addwebapi007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-contacts-in-notepad.png
[Add XSRF Protection]: #xsrf
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[Add XSRF Protection]: #xsrf
[ImportPublishSettings]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishSettings.png
[ImportPublishProfile]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishProfile.png
[PublishVSSolution]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/PublishVSSolution.png
[ValidateConnection]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ValidateConnection.png
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[prevent-csrf-attacks]: http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-(csrf)-attacks

