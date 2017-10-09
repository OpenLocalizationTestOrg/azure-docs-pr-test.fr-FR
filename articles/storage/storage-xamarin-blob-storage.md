---
title: "aaaHow toouse stockage d’objets Blob à partir de Xamarin | Documents Microsoft"
description: "Hello bibliothèque cliente de stockage Azure pour Xamarin permet aux développeurs toocreate iOS, Android et applications du Windows Store avec leurs interfaces utilisateur natives. Ce didacticiel montre comment toouse Xamarin toocreate une application qui utilise le stockage d’objets Blob Azure."
services: storage
documentationcenter: xamarin
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 44cb845d-cf78-4942-95b8-952da4f9a2c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 751f66d1d2392c8bcf6e5f8d1b185af73582fab3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-xamarin"></a>Comment toouse stockage d’objets Blob à partir de Xamarin
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a>Vue d'ensemble
Xamarin permet aux développeurs toouse partagé c# codebase toocreate iOS, Android et applications du Windows Store avec leurs interfaces utilisateur natives. Ce didacticiel vous montre comment le stockage Blob Azure avec une application Xamarin de toouse. Si vous souhaitez que toolearn plus d’informations sur le stockage Azure, avant de plonger dans le code de hello, consultez [Introduction tooMicrosoft Azure Storage](storage-introduction.md).

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a>Création d’une application Xamarin
Pour ce didacticiel, nous allons créer une application qui cible Windows, iOS et Android. Cette application créera simplement un conteneur et chargera un objet blob dans ce conteneur. Nous utiliserons Visual Studio sur Windows, mais hello apprentissages mêmes peuvent être appliqués lors de la création d’une application à l’aide de Xamarin Studio sur macOS.

Suivez ces étapes toocreate votre application :

1. Si vous ne l’avez pas encore fait, téléchargez et installez [Xamarin pour Visual Studio](https://www.xamarin.com/download).
2. Ouvrez Visual Studio et créez une application vide (native portable) : **Fichier > Nouveau > Projet > Multiplateforme > Application vide (native portable)**.
3. Avec le bouton droit de votre solution dans le volet de l’Explorateur de solutions hello et sélectionnez **gérer les Packages NuGet pour la Solution**. Recherchez **WindowsAzure.Storage** et d’installer des projets de tooall hello dernière version stable dans votre solution.
4. Créez et exécutez votre projet.

Vous devez maintenant avoir une application qui vous permet de tooclick un bouton qui incrémente un compteur.

## <a name="create-container-and-upload-blob"></a>Créer un conteneur et télécharger un objet blob
Ensuite, sous votre `(Portable)` projet, vous allez ajouter du code trop`MyClass.cs`. Ce code crée un conteneur et charge dans celui-ci un objet blob. `MyClass.cs`doit ressembler à hello suivantes :

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using System.Threading.Tasks;

namespace XamarinApp
{
    public class MyClass
    {
        public MyClass ()
        {
        }

        public static async Task performBlobOperation()
        {
            // Retrieve storage account from connection string.
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here");

            // Create hello blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference tooa previously created container.
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Create hello container if it doesn't already exist.
            await container.CreateIfNotExistsAsync();

            // Retrieve reference tooa blob named "myblob".
            CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

            // Create hello "myblob" blob with hello text "Hello, world!"
            await blockBlob.UploadTextAsync("Hello, world!");
        }
    }
}
```

Assurez-vous que tooreplace « your_account_name_here » et « your_account_key_here » avec votre nom réel du compte et votre clé de compte. 

Votre iOS, Android et Windows Phone tous les projets de projet Portable références tooyour - ce qui signifie que vous pouvez écrire tout votre code partagé dans un Placez et l’utiliser dans l’ensemble de vos projets. Vous pouvez maintenant ajouter hello suivant la ligne de code tooeach projet toostart en tirant profit :`MyClass.performBlobOperation()`

### <a name="xamarinappdroid--mainactivitycs"></a>XamarinApp.Droid > MainActivity.cs

```csharp
using Android.App;
using Android.Widget;
using Android.OS;

namespace XamarinApp.Droid
{
    [Activity (Label = "XamarinApp.Droid", MainLauncher = true, Icon = "@drawable/icon")]
    public class MainActivity : Activity
    {
        int count = 1;

        protected override async void OnCreate (Bundle bundle)
        {
            base.OnCreate (bundle);

            // Set our view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Get our button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);

            button.Click += delegate {
                button.Text = string.Format ("{0} clicks!", count++);
            };

            await MyClass.performBlobOperation();
            }
        }
    }
}
```

### <a name="xamarinappios--viewcontrollercs"></a>XamarinApp.iOS > ViewController.cs

```csharp
using System;
using UIKit;

namespace XamarinApp.iOS
{
    public partial class ViewController : UIViewController
    {
        int count = 1;

        public ViewController (IntPtr handle) : base (handle)
        {
        }

        public override async void ViewDidLoad ()
        {
            int count = 1;

            public ViewController (IntPtr handle) : base (handle)
            {
            }

            public override async void ViewDidLoad ()
            {
                base.ViewDidLoad ();
                // Perform any additional setup after loading hello view, typically from a nib.
                Button.AccessibilityIdentifier = "myButton";
                Button.TouchUpInside += delegate {
                    var title = string.Format ("{0} clicks!", count++);
                    Button.SetTitle (title, UIControlState.Normal);
                };

                await MyClass.performBlobOperation();
            }

            public override void DidReceiveMemoryWarning ()
            {
                base.DidReceiveMemoryWarning ();
                // Release any cached data, images, etc that aren't in use.
            }
        }
    }
}
```

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a>XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs

```csharp
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

// hello Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=391641

namespace XamarinApp.WinPhone
{
    /// <summary>
    /// An empty page that can be used on its own or navigated toowithin a Frame.
    /// </summary>
    public sealed partial class MainPage : Page
    {
        int count = 1;

        public MainPage()
        {
            this.InitializeComponent();

            this.NavigationCacheMode = NavigationCacheMode.Required;
        }

        /// <summary>
        /// Invoked when this page is about toobe displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.
        /// This parameter is typically used tooconfigure hello page.</param>
        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            int count = 1;

            public MainPage()
            {
                this.InitializeComponent();

                this.NavigationCacheMode = NavigationCacheMode.Required;
            }

            /// <summary>
            /// Invoked when this page is about toobe displayed in a Frame.
            /// </summary>
            /// <param name="e">Event data that describes how this page was reached.
            /// This parameter is typically used tooconfigure hello page.</param>
            protected override async void OnNavigatedTo(NavigationEventArgs e)
            {
                // TODO: Prepare page for display here.

                // TODO: If your application contains multiple pages, ensure that you are
                // handling hello hardware Back button by registering for the
                // Windows.Phone.UI.Input.HardwareButtons.BackPressed event.
                // If you are using hello NavigationHelper provided by some templates,
                // this event is handled for you.
                Button.Click += delegate {
                    var title = string.Format("{0} clicks!", count++);
                    Button.Content = title;
                };

                await MyClass.performBlobOperation();
            }
        }
    }
}
```

## <a name="run-hello-application"></a>Exécutez l’application hello
Vous pouvez maintenant exécuter cette application dans un émulateur Android ou Windows Phone. Vous pouvez également exécuter cette application dans un émulateur iOS, mais cette opération nécessite un ordinateur Mac. Pour obtenir des instructions sur comment toodo, veuillez lire documentation hello pour [connexion Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)

Une fois que vous exécutez votre application, il va créer le conteneur de hello `mycontainer` dans votre compte de stockage. Elle doit contenir des objets blob hello, `myblob`, qui contient le texte de hello, `Hello, world!`. Vous pouvez le vérifier à l’aide de hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez appris comment toocreate une application multiplateforme dans Xamarin qui utilise le stockage Azure, en particulier en mettant l’accent sur un seul scénario dans le stockage Blob. Toutefois, vous pouvez en faire beaucoup plus, non seulement avec le stockage Blob, mais également avec le stockage Table, le stockage Fichier et le stockage File d’attente. Extrayez hello suivant toolearn articles plus :

* [Prise en main d’Azure Blob Storage à l’aide de .NET](storage-dotnet-how-to-use-blobs.md)
* [Prise en main d’Azure Table Storage à l’aide de .NET](storage-dotnet-how-to-use-tables.md)
* [Prise en main du stockage de files d’attente Azure à l’aide de .NET](storage-dotnet-how-to-use-queues.md)
* [Prise en main d’Azure File Storage sur Windows](storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

