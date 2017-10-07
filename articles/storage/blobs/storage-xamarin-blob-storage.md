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
ms.openlocfilehash: 688484fc560b5c89ed1692f5cbf5713aa8fc90a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-xamarin"></a><span data-ttu-id="04198-104">Comment toouse stockage d’objets Blob à partir de Xamarin</span><span class="sxs-lookup"><span data-stu-id="04198-104">How toouse Blob Storage from Xamarin</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a><span data-ttu-id="04198-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="04198-105">Overview</span></span>
<span data-ttu-id="04198-106">Xamarin permet aux développeurs toouse partagé c# codebase toocreate iOS, Android et applications du Windows Store avec leurs interfaces utilisateur natives.</span><span class="sxs-lookup"><span data-stu-id="04198-106">Xamarin enables developers toouse a shared C# codebase toocreate iOS, Android, and Windows Store apps with their native user interfaces.</span></span> <span data-ttu-id="04198-107">Ce didacticiel vous montre comment le stockage Blob Azure avec une application Xamarin de toouse.</span><span class="sxs-lookup"><span data-stu-id="04198-107">This tutorial shows you how toouse Azure Blob storage with a Xamarin application.</span></span> <span data-ttu-id="04198-108">Si vous souhaitez que toolearn plus d’informations sur le stockage Azure, avant de plonger dans le code de hello, consultez [Introduction tooMicrosoft Azure Storage](../common/storage-introduction.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="04198-108">If you'd like toolearn more about Azure Storage, before diving into hello code, see [Introduction tooMicrosoft Azure Storage](../common/storage-introduction.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a><span data-ttu-id="04198-109">Création d’une application Xamarin</span><span class="sxs-lookup"><span data-stu-id="04198-109">Create a new Xamarin Application</span></span>
<span data-ttu-id="04198-110">Pour ce didacticiel, nous allons créer une application qui cible Windows, iOS et Android.</span><span class="sxs-lookup"><span data-stu-id="04198-110">For this tutorial, we'll be creating an app that targets Android, iOS, and Windows.</span></span> <span data-ttu-id="04198-111">Cette application créera simplement un conteneur et chargera un objet blob dans ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="04198-111">This app will simply create a container and upload a blob into this container.</span></span> <span data-ttu-id="04198-112">Nous utiliserons Visual Studio sur Windows, mais hello apprentissages mêmes peuvent être appliqués lors de la création d’une application à l’aide de Xamarin Studio sur macOS.</span><span class="sxs-lookup"><span data-stu-id="04198-112">We'll be using Visual Studio on Windows, but hello same learnings can be applied when creating an app using Xamarin Studio on macOS.</span></span>

<span data-ttu-id="04198-113">Suivez ces étapes toocreate votre application :</span><span class="sxs-lookup"><span data-stu-id="04198-113">Follow these steps toocreate your application:</span></span>

1. <span data-ttu-id="04198-114">Si vous ne l’avez pas encore fait, téléchargez et installez [Xamarin pour Visual Studio](https://www.xamarin.com/download).</span><span class="sxs-lookup"><span data-stu-id="04198-114">If you haven't already, download and install [Xamarin for Visual Studio](https://www.xamarin.com/download).</span></span>
2. <span data-ttu-id="04198-115">Ouvrez Visual Studio et créez une application vide (native portable) : **Fichier > Nouveau > Projet > Multiplateforme > Application vide (native portable)**.</span><span class="sxs-lookup"><span data-stu-id="04198-115">Open Visual Studio, and create a Blank App (Native Portable): **File > New > Project > Cross-Platform > Blank App(Native Portable)**.</span></span>
3. <span data-ttu-id="04198-116">Avec le bouton droit de votre solution dans le volet de l’Explorateur de solutions hello et sélectionnez **gérer les Packages NuGet pour la Solution**.</span><span class="sxs-lookup"><span data-stu-id="04198-116">Right-click your solution in hello Solution Explorer pane and select **Manage NuGet Packages for Solution**.</span></span> <span data-ttu-id="04198-117">Recherchez **WindowsAzure.Storage** et d’installer des projets de tooall hello dernière version stable dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="04198-117">Search for **WindowsAzure.Storage** and install hello latest stable version tooall projects in your solution.</span></span>
4. <span data-ttu-id="04198-118">Créez et exécutez votre projet.</span><span class="sxs-lookup"><span data-stu-id="04198-118">Build and run your project.</span></span>

<span data-ttu-id="04198-119">Vous devez maintenant avoir une application qui vous permet de tooclick un bouton qui incrémente un compteur.</span><span class="sxs-lookup"><span data-stu-id="04198-119">You should now have an application that allows you tooclick a button which increments a counter.</span></span>

## <a name="create-container-and-upload-blob"></a><span data-ttu-id="04198-120">Créer un conteneur et télécharger un objet blob</span><span class="sxs-lookup"><span data-stu-id="04198-120">Create container and upload blob</span></span>
<span data-ttu-id="04198-121">Ensuite, sous votre `(Portable)` projet, vous allez ajouter du code trop`MyClass.cs`.</span><span class="sxs-lookup"><span data-stu-id="04198-121">Next, under your `(Portable)` project, you'll add some code too`MyClass.cs`.</span></span> <span data-ttu-id="04198-122">Ce code crée un conteneur et charge dans celui-ci un objet blob.</span><span class="sxs-lookup"><span data-stu-id="04198-122">This code creates a container and uploads a blob into this container.</span></span> <span data-ttu-id="04198-123">`MyClass.cs`doit ressembler à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="04198-123">`MyClass.cs` should look like hello following:</span></span>

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

<span data-ttu-id="04198-124">Assurez-vous que tooreplace « your_account_name_here » et « your_account_key_here » avec votre nom réel du compte et votre clé de compte.</span><span class="sxs-lookup"><span data-stu-id="04198-124">Make sure tooreplace "your_account_name_here" and "your_account_key_here" with your actual account name and account key.</span></span> 

<span data-ttu-id="04198-125">Votre iOS, Android et Windows Phone tous les projets de projet Portable références tooyour - ce qui signifie que vous pouvez écrire tout votre code partagé dans un Placez et l’utiliser dans l’ensemble de vos projets.</span><span class="sxs-lookup"><span data-stu-id="04198-125">Your iOS, Android, and Windows Phone projects all have references tooyour Portable project - meaning you can write all of your shared code in one place and use it across all of your projects.</span></span> <span data-ttu-id="04198-126">Vous pouvez maintenant ajouter hello suivant la ligne de code tooeach projet toostart en tirant profit :`MyClass.performBlobOperation()`</span><span class="sxs-lookup"><span data-stu-id="04198-126">You can now add hello following line of code tooeach project toostart taking advantage: `MyClass.performBlobOperation()`</span></span>

### <a name="xamarinappdroid--mainactivitycs"></a><span data-ttu-id="04198-127">XamarinApp.Droid > MainActivity.cs</span><span class="sxs-lookup"><span data-stu-id="04198-127">XamarinApp.Droid > MainActivity.cs</span></span>

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

### <a name="xamarinappios--viewcontrollercs"></a><span data-ttu-id="04198-128">XamarinApp.iOS > ViewController.cs</span><span class="sxs-lookup"><span data-stu-id="04198-128">XamarinApp.iOS > ViewController.cs</span></span>

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

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a><span data-ttu-id="04198-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="04198-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span></span>

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

## <a name="run-hello-application"></a><span data-ttu-id="04198-130">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="04198-130">Run hello application</span></span>
<span data-ttu-id="04198-131">Vous pouvez maintenant exécuter cette application dans un émulateur Android ou Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="04198-131">You can now run this application in an Android or Windows Phone emulator.</span></span> <span data-ttu-id="04198-132">Vous pouvez également exécuter cette application dans un émulateur iOS, mais cette opération nécessite un ordinateur Mac.</span><span class="sxs-lookup"><span data-stu-id="04198-132">You can also run this application in an iOS emulator, but this will require a Mac.</span></span> <span data-ttu-id="04198-133">Pour obtenir des instructions sur comment toodo, veuillez lire documentation hello pour [connexion Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span><span class="sxs-lookup"><span data-stu-id="04198-133">For specific instructions on how toodo this, please read hello documentation for [connecting Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span></span>

<span data-ttu-id="04198-134">Une fois que vous exécutez votre application, il va créer le conteneur de hello `mycontainer` dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="04198-134">Once you run your app, it will create hello container `mycontainer` in your Storage account.</span></span> <span data-ttu-id="04198-135">Elle doit contenir des objets blob hello, `myblob`, qui contient le texte de hello, `Hello, world!`.</span><span class="sxs-lookup"><span data-stu-id="04198-135">It should contain hello blob, `myblob`, which has hello text, `Hello, world!`.</span></span> <span data-ttu-id="04198-136">Vous pouvez le vérifier à l’aide de hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="04198-136">You can verify this by using hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="04198-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="04198-137">Next steps</span></span>
<span data-ttu-id="04198-138">Dans ce didacticiel, vous avez appris comment toocreate une application multiplateforme dans Xamarin qui utilise le stockage Azure, en particulier en mettant l’accent sur un seul scénario dans le stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="04198-138">In this tutorial, you learned how toocreate a cross-platform application in Xamarin that uses Azure Storage, specifically focusing on one scenario in Blob Storage.</span></span> <span data-ttu-id="04198-139">Toutefois, vous pouvez en faire beaucoup plus, non seulement avec le stockage Blob, mais également avec le stockage Table, le stockage Fichier et le stockage File d’attente.</span><span class="sxs-lookup"><span data-stu-id="04198-139">However, you can do a lot more with not only Blob Storage, but also with Table, File, and Queue Storage.</span></span> <span data-ttu-id="04198-140">Extrayez hello suivant toolearn articles plus :</span><span class="sxs-lookup"><span data-stu-id="04198-140">Please check out hello following articles toolearn more:</span></span>

* [<span data-ttu-id="04198-141">Prise en main d’Azure Blob Storage à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="04198-141">Get started with Azure Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="04198-142">Prise en main d’Azure Table Storage à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="04198-142">Get started with Azure Table storage using .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="04198-143">Prise en main du stockage de files d’attente Azure à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="04198-143">Get started with Azure Queue storage using .NET</span></span>](../queues/storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="04198-144">Prise en main d’Azure File Storage sur Windows</span><span class="sxs-lookup"><span data-stu-id="04198-144">Get started with Azure File storage on Windows</span></span>](../files/storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]
