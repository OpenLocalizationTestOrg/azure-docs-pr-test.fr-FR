---
title: "aaaSmooth didacticiel d’application de diffusion en continu Windows Store | Documents Microsoft"
description: "Découvrez comment toouse Azure Media Services toocreate une application du Windows Store en c# avec un MediaElement XML contrôler tooplayback Smooth diffuser du contenu."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0fa5d8c5-3d5f-4886-ae55-fb6de4f5256d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: juliako
ms.openlocfilehash: b02aa2c7f68fe22a23ea846d72fdd23bfba2b19c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobuild-a-smooth-streaming-windows-store-application"></a>Comment tooBuild un Smooth Streaming Application du Windows Store

Hello Smooth Streaming Client SDK pour Windows 8 permet les applications du Windows Store les développeurs toobuild qui peuvent lire le contenu de diffusion en continu lisse à la demande et en direct. En outre lecture de base toohello de Smooth Streaming également de contenu, hello SDK fournit des fonctionnalités puissantes comme la protection de Microsoft PlayReady, restriction de niveau de qualité, Live magnétoscope numérique, le flux audio commutation, à l’écoute des mises à jour de l’état (telles que les modifications au niveau de qualité ) et les événements d’erreur et ainsi de suite. Pour plus d’informations des fonctionnalités de hello pris en charge, consultez hello [notes de publication](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes). Pour plus d’informations, consultez [Player Framework for Windows 8](http://playerframework.codeplex.com/). 

Le didacticiel se compose de quatre leçons :

1. Création d'une application Windows Store de diffusion en continu lisse de base
2. Ajouter un barre tooControl hello Media progression du curseur
3. Sélection des flux de diffusion en continu lisse
4. Sélection des pistes de diffusion en continu lisse

## <a name="prerequisites"></a>Conditions préalables
* Windows 8 32 bits ou 64 bits. Vous pouvez télécharger la [version d'évaluation de Windows 8 Entreprise](http://msdn.microsoft.com/evalcenter/jj554510.aspx) sur MSDN.
* Visual Studio 2012 ou Visual Studio Express 2012 (ou une version ultérieure). Vous pouvez obtenir la version d’évaluation à partir de hello [ici](http://www.microsoft.com/visualstudio/11/downloads).
* [Kit de développement logiciel (SDK) du client Microsoft de diffusion en continu lisse pour Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).

solution Hello terminé pour chaque leçon peut être téléchargée à partir d’exemples de Code pour développeurs MSDN (Code Gallery) : 

* [Leçon 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) : un lecteur multimédia Smooth Streaming pour Windows 8, 
* [Leçon 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) : un lecteur multimédia simple Smooth Streaming pour Windows 8 doté d’une fonction de contrôle avec barre de curseur, 
* [Leçon 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) : un lecteur multimédia Smooth Streaming pour Windows 8 avec sélection de flux,  
* [Leçon 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907) : un lecteur multimédia Smooth Streaming pour Windows 8 avec sélection des pistes.

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a>Leçon 1 : créer une application Windows Store de diffusion en continu lisse de base

Dans cette leçon, vous créerez une application du Windows Store avec un contrôle MediaElement tooplay contenu Smooth Streaming contenu.  exécution de l’application Hello ressemble à ceci :

![Exemple d'application Windows Store de diffusion en continu lisse][PlayerApplication]

Pour plus d'informations sur le développement d'une application Windows Store, consultez la rubrique [Développement d'applications fantastiques pour Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx). Cette leçon contient hello procédures suivantes :

1. Création d'un projet Windows Store
2. Interface utilisateur du concepteur hello (XAML)
3. Modifier hello fichier code-behind
4. Compiler et tester l’application hello

**toocreate un projet Windows Store**

1. Exécutez Visual Studio 2012 ou une version ultérieure.
2. À partir de hello **fichier** menu, cliquez sur **nouveau**, puis cliquez sur **projet**.
3. À partir de la boîte de dialogue Nouveau projet hello, type ou sélectionnez hello suivant des valeurs :

| Nom | Valeur |
| --- | --- |
| Groupe de modèles |Installed/Templates/Visual C#/Windows Store |
| Modèle |Application vide (XAML) |
| Nom |SSPlayer |
| Lieu |C:\SSTutorials |
| Nom de la solution |SSPlayer |
| Créer un répertoire pour la solution |(sélectionné) |

1. Cliquez sur **OK**.

**tooadd un toohello référence SDK de Client de diffusion en continu lisse**

1. Dans l'Explorateur de solutions, cliquez avec le bouton droit sur **SSPlayer**, puis cliquez sur **Ajouter une référence**.
2. Tapez ou sélectionnez hello valeurs suivantes :

| Nom | Valeur |
| --- | --- |
| Groupe de référence |Windows/Extensions |
| Référence |Sélectionnez le Kit de développement logiciel (SDK) du client de diffusion en continu lisse pour Windows 8 et le package Runtime Microsoft Visual C++ |

1. Cliquez sur **OK**. 

Après avoir ajouté des références de hello, vous devez sélectionner la plate-forme hello ciblé (x64 ou x86), ajout de références ne fonctionne pas pour la configuration de la plateforme Any CPU.  Dans l'Explorateur de solutions, un symbole d'avertissement jaune s'affiche pour indiquer les références ajoutées.

**interface utilisateur de toodesign hello lecteur**

1. Dans l’Explorateur de solutions, double-cliquez sur **MainPage.xaml** tooopen dans la conception de hello afficher.
2. Recherchez hello  **&lt;grille&gt;**  et  **&lt;/Grid&gt;**  balises hello fichier XAML et de code suivant de hello de coller entre les balises de hello deux :

         <Grid.RowDefinitions>

            <RowDefinition Height="20"/>    <!-- spacer -->
            <RowDefinition Height="50"/>    <!-- media controls -->
            <RowDefinition Height="100*"/>  <!-- media element -->
            <RowDefinition Height="80*"/>   <!-- media stream and track selection -->
            <RowDefinition Height="50"/>    <!-- status bar -->
         </Grid.RowDefinitions>

         <StackPanel Name="spMediaControl" Grid.Row="1" Orientation="Horizontal">
            <TextBlock x:Name="tbSource" Text="Source :  " FontSize="16" FontWeight="Bold" VerticalAlignment="Center" />
            <TextBox x:Name="txtMediaSource" Text="http://ecn.channel9.msdn.com/o9/content/smf/smoothcontent/elephantsdream/Elephants_Dream_1024-h264-st-aac.ism/manifest" FontSize="10" Width="700" Margin="0,4,0,10" />
            <Button x:Name="btnSetSource" Content="Set Source" Width="111" Height="43" Click="btnSetSource_Click"/>
            <Button x:Name="btnPlay" Content="Play" Width="111" Height="43" Click="btnPlay_Click"/>
            <Button x:Name="btnPause" Content="Pause"  Width="111" Height="43" Click="btnPause_Click"/>
            <Button x:Name="btnStop" Content="Stop"  Width="111" Height="43" Click="btnStop_Click"/>
            <CheckBox x:Name="chkAutoPlay" Content="Auto Play" Height="55" Width="Auto" IsChecked="{Binding AutoPlay, ElementName=mediaElement, Mode=TwoWay}"/>
            <CheckBox x:Name="chkMute" Content="Mute" Height="55" Width="67" IsChecked="{Binding IsMuted, ElementName=mediaElement, Mode=TwoWay}"/>
         </StackPanel>

         <StackPanel Name="spMediaElement" Grid.Row="2" Height="435" Width="1072"
                    HorizontalAlignment="Center" VerticalAlignment="Center">
            <MediaElement x:Name="mediaElement" Height="356" Width="924" MinHeight="225"
                          HorizontalAlignment="Center" VerticalAlignment="Center" 
                          AudioCategory="BackgroundCapableMedia" />
            <StackPanel Orientation="Horizontal">
                <Slider x:Name="sliderProgress" Width="924" Height="44"
                        HorizontalAlignment="Center" VerticalAlignment="Center"
                        PointerPressed="sliderProgress_PointerPressed"/>
                <Slider x:Name="sliderVolume" 
                        HorizontalAlignment="Right" VerticalAlignment="Center" Orientation="Vertical" 
                        Height="79" Width="148" Minimum="0" Maximum="1" StepFrequency="0.1" 
                        Value="{Binding Volume, ElementName=mediaElement, Mode=TwoWay}" 
                        ToolTipService.ToolTip="{Binding Value, RelativeSource={RelativeSource Mode=Self}}"/>
            </StackPanel>
         </StackPanel>

         <StackPanel Name="spStatus" Grid.Row="4" Orientation="Horizontal">
            <TextBlock x:Name="tbStatus" Text="Status :  " 
               FontSize="16" FontWeight="Bold" VerticalAlignment="Center" HorizontalAlignment="Center" />
            <TextBox x:Name="txtStatus" FontSize="10" Width="700" VerticalAlignment="Center"/>
         </StackPanel>
   
   Hello contrôle MediaElement est un support tooplayback utilisé. contrôle de curseur Hello nommé sliderProgress servira en cours du support hello prochaine leçon toocontrol hello.
3. Appuyez sur **CTRL + S** fichier hello de toosave.

Hello contrôle MediaElement ne prend pas en charge la diffusion en continu lisse contenu out-of-box. tooenable hello Smooth Streaming prise en charge, vous devez inscrire le gestionnaire hello octet-stream diffusion en continu par l’extension de nom de fichier et le type MIME.  tooregister, vous utilisez (méthode MediaExtensionManager.RegisterByteStremHandler hello) de l’espace de noms Windows.Media hello.

Dans ce fichier XAML, certains gestionnaires d’événements sont associés à des contrôles de hello.  Vous devez définir les gestionnaires d'événements en question.

**toomodify hello fichier code-behind**

1. Dans l'Explorateur de solutions, cliquez avec le bouton droit sur **MainPage.xaml**, puis cliquez sur **Afficher le code**.
2. Haut hello du fichier de hello, ajoutez hello qui suit à l’aide d’instruction :
   
        using Windows.Media;
3. Au début de hello Hello **MainPage** de classe, ajoutez hello suivant du membre de données :
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. À fin hello Hello **MainPage** constructeur, ajoutez hello deux lignes suivantes :
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. À fin hello Hello **MainPage** de classe, collez hello suivant de code :
   
         # region UI Button Click Events
         private void btnPlay_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Play();
         txtStatus.Text = "MediaElement is playing ...";
         }
         private void btnPause_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Pause();
         txtStatus.Text = "MediaElement is paused";
         }
         private void btnSetSource_Click(object sender, RoutedEventArgs e)
         {

         sliderProgress.Value = 0;
         mediaElement.Source = new Uri(txtMediaSource.Text);

         if (chkAutoPlay.IsChecked == true)
         {
             txtStatus.Text = "MediaElement is playing ...";
         }
         else
         {
             txtStatus.Text = "Click hello Play button tooplay hello media source.";
         }
         }
         private void btnStop_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Stop();
         txtStatus.Text = "MediaElement is stopped";
         }
         private void sliderProgress_PointerPressed(object sender, PointerRoutedEventArgs e)
         {

         txtStatus.Text = "Seek tooposition " + sliderProgress.Value;
         mediaElement.Position = new TimeSpan(0, 0, (int)(sliderProgress.Value));
         }
         # endregion

Gestionnaire d’événements sliderProgress_PointerPressed Hello est défini ici.  Il existe plusieurs tooget de toodo fonctionne qu’il fonctionne, qui seront abordée dans la leçon suivante de hello de ce didacticiel.
6. Appuyez sur **CTRL + S** fichier hello de toosave.

Hello hello terminé fichier code-behind doit ressembler à ceci :

![Codeview dans Visual Studio d'une application Windows Store de diffusion en continu lisse][CodeViewPic]

**application de hello toocompile et de test**

1. À partir de hello **générer** menu, cliquez sur **Configuration Manager**.
2. Modification **plateforme de solution Active** toomatch votre plateforme de développement.
3. Appuyez sur **F6** projet hello de toocompile. 
4. Appuyez sur **F5** application hello de toorun.
5. Haut hello du application hello, vous pouvez utiliser la valeur par défaut de hello URL de diffusion en continu lisse ou entrez un nom différent. 
6. Cliquez sur **Définir la source**. Étant donné que **lecture Auto** est activée par défaut, hello la lecture du média est automatiquement.  Vous pouvez contrôler les média hello à l’aide de hello **lire**, **Pause** et **arrêter** boutons.  Vous pouvez contrôler le volume de support hello à l’aide du curseur vertical de hello.  Toutefois, hello curseur horizontal pour le contrôle hello progression de média n’est pas entièrement encore implémentée. 

Vous avez terminé la leçon 1.  Dans cette leçon, vous utilisez un tooplayback de contrôle MediaElement contenu Smooth Streaming.  Dans la leçon suivante de hello, vous allez ajouter une progression de hello curseur toocontrol Hello contenu Smooth Streaming.

## <a name="lesson-2-add-a-slider-bar-toocontrol-hello-media-progress"></a>Leçon 2 : Ajouter un barre tooControl hello Media progression du curseur

Dans la leçon 1, vous avez créé une application du Windows Store avec un tooplayback de contrôle MediaElement XAML diffusion en continu le contenu du média.  Elle offre des fonctions de lecture multimédia de base, comme le démarrage, l'arrêt et la pause.  Dans cette leçon, vous allez ajouter une application de toohello contrôle slider barre.

Dans ce didacticiel, nous allons utiliser un minuteur tooupdate hello curseur en fonction de la position actuelle de hello Hello contrôle MediaElement.  curseur de Hello commencer et se terminer temps également toobe besoin de mettre à jour en cas de contenu en direct.  Cela peut être mieux gérée dans les événements de mise à jour source adaptive hello.

Les sources multimédias sont des objets qui produisent des données multimédias.  programme de résolution de source Hello prend un flux d’URL ou d’octets et crée la source de média approprié hello pour ce contenu.  programme de résolution de source Hello consiste hello standard pour des sources de médias toocreate hello applications. 

Cette leçon contient hello procédures suivantes :

1. Inscrire le Gestionnaire de diffusion en continu lisse hello 
2. Ajoutez des gestionnaires d’événements de niveau hello source adaptive manager
3. Ajoutez des gestionnaires d’événements au niveau source adaptive hello
4. Ajout de gestionnaires d'événements MediaElement
5. Ajout du code lié à la barre de curseur
6. Compiler et tester l’application hello

**propertyset hello tooregister hello flux d’octets de diffusion en continu lisse gestionnaire et passez**

1. Dans l'Explorateur de solutions, cliquez avec le bouton droit sur **MainPage.xaml**, puis cliquez sur **Afficher le code**.
2. Au début de hello du fichier de hello, ajoutez hello à l’aide d’instruction :

        using Microsoft.Media.AdaptiveStreaming;
3. Au début de hello Hello classe MainPage, ajoutez hello suivant des membres de données :

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. À l’intérieur hello **MainPage** constructeur, ajoutez hello après le code après hello **cela. Initialiser Components() ;**  ligne et les lignes de code hello d’enregistrement écrits dans la leçon précédente de hello :

        // Gets hello default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value tooAdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. À l’intérieur hello **MainPage** constructeur, modifier hello de hello deux RegisterByteStreamHandler méthodes tooadd les deux paramètres :

         // Registers Smooth Streaming byte-stream handler for ".ism" extension and, 
         // "text/xml" and "application/vnd.ms-ss" mime-types and pass hello propertyset. 
         // http://*.ism/manifest URI resources will be resolved by Byte-stream handler.
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "text/xml", 
            propertySet );
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "application/vnd.ms-sstr+xml", 
         propertySet);
6. Appuyez sur **CTRL + S** fichier hello de toosave.

**Gestionnaire d’événements de niveau tooadd hello source adaptive manager**

1. Dans l'Explorateur de solutions, cliquez avec le bouton droit sur **MainPage.xaml**, puis cliquez sur **Afficher le code**.
2. À l’intérieur hello **MainPage** de classe, ajoutez hello suivant du membre de données :
   
     private AdaptiveSource adaptiveSource = null;
3. À fin hello Hello **MainPage** de classe, ajoutez hello suivant du Gestionnaire d’événements :
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. À fin hello Hello **MainPage** constructeur, ajoutez hello suivant ligne toosubscribe toohello adaptative source ouvert événement :
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. Appuyez sur **CTRL + S** fichier hello de toosave.

**gestionnaires d’événements au niveau source adaptive tooadd**

1. Dans l'Explorateur de solutions, cliquez avec le bouton droit sur **MainPage.xaml**, puis cliquez sur **Afficher le code**.
2. À l’intérieur hello **MainPage** de classe, ajoutez hello suivant du membre de données :
   
     private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;
3. À fin hello Hello **MainPage** de classe, ajoutez hello suivant des gestionnaires d’événements :

         # region Adaptive Source Level Events
         private void mediaElement_ManifestReady(AdaptiveSource sender, ManifestReadyEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
            manifestObject = args.AdaptiveSource.Manifest;
         }

         private void mediaElement_AdaptiveSourceStatusUpdated(AdaptiveSource sender, AdaptiveSourceStatusUpdatedEventArgs args)
         {

            adaptiveSourceStatusUpdate = args;
         }

         private void mediaElement_AdaptiveSourceFailed(AdaptiveSource sender, AdaptiveSourceFailedEventArgs args)
         {

            txtStatus.Text = "Error: " + args.HttpResponse;
         }

         # endregion Adaptive Source Level Events
4. À fin hello Hello **mediaElement AdaptiveSourceOpened** (méthode), ajouter hello après les événements de code toosubscribe toohello :
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. Appuyez sur **CTRL + S** fichier hello de toosave.

Hello mêmes événements sont disponibles sur Adaptive Gestionnaire niveau de la Source, qui peut être utilisé pour la gestion des fonctionnalités tooall media éléments communs application hello. Chaque AdaptiveSource inclut ses propres événements et tous les événements AdaptiveSource sont affichés en cascade dans AdaptiveSourceManager.

**gestionnaires d’événements tooadd élément multimédia**

1. Dans l'Explorateur de solutions, cliquez avec le bouton droit sur **MainPage.xaml**, puis cliquez sur **Afficher le code**.
2. À fin hello Hello **MainPage** de classe, ajoutez hello suivant des gestionnaires d’événements :

         # region Media Element Event Handlers
         private void MediaOpened(object sender, RoutedEventArgs e)
         {

            txtStatus.Text = "MediaElement opened";
         }

         private void MediaFailed(object sender, ExceptionRoutedEventArgs e)
         {

            txtStatus.Text= "MediaElement failed: " + e.ErrorMessage;
         }

         private void MediaEnded(object sender, RoutedEventArgs e)
         {

            txtStatus.Text ="MediaElement ended.";
         }

         # endregion Media Element Event Handlers
3. À fin hello Hello **MainPage** constructeur, ajoutez hello après les événements de code toosubscript toohello :

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. Appuyez sur **CTRL + S** fichier hello de toosave.

**curseur tooadd connexe code barres**

1. Dans l'Explorateur de solutions, cliquez avec le bouton droit sur **MainPage.xaml**, puis cliquez sur **Afficher le code**.
2. Au début de hello du fichier de hello, ajoutez hello à l’aide d’instruction :
      
        using Windows.UI.Core;
3. À l’intérieur hello **MainPage** de classe, ajoutez hello suivant des membres de données :
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. À fin hello Hello **MainPage** constructeur, ajoutez hello suivant de code :
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. À fin hello Hello **MainPage** de classe, ajoutez hello suivant de code :

         # region sliderMediaPlayer
         private double SliderFrequency(TimeSpan timevalue)
         {

            long absvalue = 0;
            double stepfrequency = -1;

            if (manifestObject != null)
            {
                absvalue = manifestObject.Duration - (long)manifestObject.StartTime;
            }
            else
            {
                absvalue = mediaElement.NaturalDuration.TimeSpan.Ticks;
            }

            TimeSpan totalDVRDuration = new TimeSpan(absvalue);

            if (totalDVRDuration.TotalMinutes >= 10 && totalDVRDuration.TotalMinutes < 30)
            {
               stepfrequency = 10;
            }
            else if (totalDVRDuration.TotalMinutes >= 30 
                     && totalDVRDuration.TotalMinutes < 60)
            {
                stepfrequency = 30;
            }
            else if (totalDVRDuration.TotalHours >= 1)
            {
                stepfrequency = 60;
            }

            return stepfrequency;
         }

         void updateSliderPositionoNTicks(object sender, object e)
         {

            sliderProgress.Value = mediaElement.Position.TotalSeconds;
         }

         public void setupTimer()
         {

            sliderPositionUpdateDispatcher = new DispatcherTimer();
            sliderPositionUpdateDispatcher.Interval = new TimeSpan(0, 0, 0, 0, 300);
            startTimer();
         }

         public void startTimer()
         {

            sliderPositionUpdateDispatcher.Tick += updateSliderPositionoNTicks;
            sliderPositionUpdateDispatcher.Start();
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderStartTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.StartTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Minimum = absvalue;
            });
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderEndTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Maximum = absvalue;
            });
         }

         # endregion sliderMediaPlayer
      
>[!NOTE]
>CoreDispatcher est modifications toomake utilisé toohello l’interface utilisateur de thread non thread d’interface utilisateur. En cas de goulot d’étranglement sur le thread dispatcher, développeur peut choisir toouse répartiteur fournie par l’élément d’interface utilisateur qu'il envisage de tooupdate.  Par exemple :
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. À fin hello Hello **mediaElement_AdaptiveSourceStatusUpdated** (méthode), ajouter hello suivant de code :

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. À fin hello Hello **MediaOpened** (méthode), ajouter hello suivant de code :

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. Appuyez sur **CTRL + S** fichier hello de toosave.

**application de hello toocompile et de test**

1. Appuyez sur **F6** projet hello de toocompile. 
2. Appuyez sur **F5** application hello de toorun.
3. Haut hello du application hello, vous pouvez utiliser la valeur par défaut de hello URL de diffusion en continu lisse ou entrez un nom différent. 
4. Cliquez sur **Définir la source**. 
5. Barre de défilement test hello.

Vous avez terminé la leçon 2.  Dans cette leçon, vous avez ajouté une tooapplication de curseur. 

## <a name="lesson-3-select-smooth-streaming-streams"></a>Leçon 3 : sélectionner les flux de diffusion en continu lisse
Smooth Streaming est contenu toostream compatibles avec plusieurs pistes audio langage sont sélectionnables par les visionneuses hello.  Dans cette leçon, vous allez activer le flux de données tooselect visionneuses. Cette leçon contient hello procédures suivantes :

1. Modifier le fichier XAML de hello
2. Modifier le fichier de behand code hello
3. Compiler et tester l’application hello

**fichier XAML de hello toomodify**

1. Dans l'Explorateur de solutions, cliquez avec le bouton droit sur **MainPage.xaml**, puis cliquez sur **Concepteur de vues**.
2. Recherchez &lt;Grid.RowDefinitions&gt;et modifier hello RowDefinitions afin qu’ils ressemble à :
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. À l’intérieur hello &lt;grille&gt;&lt;/Grid&gt; ajouter des balises, hello de code suivant toodefine un contrôle listbox, donc les utilisateurs peuvent voir liste hello de flux de données disponibles et sélectionnez le flux de données :

         <Grid Name="gridStreamAndBitrateSelection" Grid.Row="3">
            <Grid.RowDefinitions>
                <RowDefinition Height="300"/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="250*"/>
                <ColumnDefinition Width="250*"/>
            </Grid.ColumnDefinitions>
            <StackPanel Name="spStreamSelection" Grid.Row="1" Grid.Column="0">
                <StackPanel Orientation="Horizontal">
                    <TextBlock Name="tbAvailableStreams" Text="Available Streams:" FontSize="16" VerticalAlignment="Center"></TextBlock>
                    <Button Name="btnChangeStreams" Content="Submit" Click="btnChangeStream_Click"/>
                </StackPanel>
                <ListBox x:Name="lbAvailableStreams" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                    ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
                    <ListBox.ItemTemplate>
                        <DataTemplate>
                            <CheckBox Content="{Binding Name}" IsChecked="{Binding isChecked, Mode=TwoWay}" />
                        </DataTemplate>
                    </ListBox.ItemTemplate>
                </ListBox>
            </StackPanel>
         </Grid>
4. Appuyez sur **CTRL + S** modifications de hello toosave.

**toomodify hello fichier code-behind**

1. Dans l'Explorateur de solutions, cliquez avec le bouton droit sur **MainPage.xaml**, puis cliquez sur **Afficher le code**.
2. Au sein de l’espace de noms SSPlayer hello, ajoutez une nouvelle classe :
   
        #region class Stream
   
        public class Stream
        {
            private IManifestStream stream;
            public bool isCheckedValue;
            public string name;
   
            public string Name
            {
                get { return name; }
                set { name = value; }
            }
   
            public IManifestStream ManifestStream
            {
                get { return stream; }
                set { stream = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    // mMke hello video stream always checked.
                    if (stream.Type == MediaStreamType.Video)
                    {
                        isCheckedValue = true;
                    }
                    else
                    {
                        isCheckedValue = value;
                    }
                }
            }
   
            public Stream(IManifestStream streamIn)
            {
                stream = streamIn;
                name = stream.Name;
            }
        }
        #endregion class Stream
3. Au début de hello Hello classe MainPage, ajoutez hello suivant des définitions de variables :
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. Au sein de hello classe MainPage, ajoutez hello suivant région :
   
        #region stream selection
        ///<summary>
        ///Functionality tooselect streams from IManifestStream available streams
        /// </summary>
   
        // This function is called from hello mediaElement_ManifestReady event handler 
        // tooretrieve hello streams and populate them toohello local data members.
        public void getStreams(Manifest manifestObject)
        {
            availableStreams = new List<Stream>();
            availableVideoStreams = new List<Stream>();
            availableAudioStreams = new List<Stream>();
            availableTextStreams = new List<Stream>();
   
            try
            {
                for (int i = 0; i<manifestObject.AvailableStreams.Count; i++)
                {
                    Stream newStream = new Stream(manifestObject.AvailableStreams[i]);
                    newStream.isChecked = false;
   
                    //populate hello stream lists based on hello types
                    availableStreams.Add(newStream);
   
                    switch (newStream.ManifestStream.Type)
                    {
                        case MediaStreamType.Video:
                            availableVideoStreams.Add(newStream);
                            break;
                        case MediaStreamType.Audio:
                            availableAudioStreams.Add(newStream);
                            break;
                        case MediaStreamType.Text:
                            availableTextStreams.Add(newStream);
                            break;
                    }
   
                    // Select hello default selected streams from hello manifest.
                    for (int j = 0; j<manifestObject.SelectedStreams.Count; j++)
                    {
                        string selectedStreamName = manifestObject.SelectedStreams[j].Name;
                        if (selectedStreamName.Equals(newStream.Name))
                        {
                            newStream.isChecked = true;
                            break;
                        }
                    }
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function set hello list box ItemSource
        private async void refreshAvailableStreamsListBoxItemSource()
        {
            try
            {
                //update hello stream check box list on hello UI
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableStreams.ItemsSource = availableStreams; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function creates a selected streams list
        private void createSelectedStreamsList(List<IManifestStream> selectedStreams)
        {
            bool isOneVideoSelected = false;
            bool isOneAudioSelected = false;
   
            // Only one video stream can be selected
            for (int j = 0; j<availableVideoStreams.Count; j++)
            {
                if (availableVideoStreams[j].isChecked && (!isOneVideoSelected))
                {
                    selectedStreams.Add(availableVideoStreams[j].ManifestStream);
                    isOneVideoSelected = true;
                }
            }
   
            // Select hello frist video stream from hello list if no video stream is selected
            if (!isOneVideoSelected)
            {
                availableVideoStreams[0].isChecked = true;
                selectedStreams.Add(availableVideoStreams[0].ManifestStream);
            }
   
            // Only one audio stream can be selected
            for (int j = 0; j<availableAudioStreams.Count; j++)
            {
                if (availableAudioStreams[j].isChecked && (!isOneAudioSelected))
                {
                    selectedStreams.Add(availableAudioStreams[j].ManifestStream);
                    isOneAudioSelected = true;
                    txtStatus.Text = "hello audio stream is changed too" + availableAudioStreams[j].ManifestStream.Name;
                }
            }
   
            // Select hello frist audio stream from hello list if no audio steam is selected.
            if (!isOneAudioSelected)
            {
                availableAudioStreams[0].isChecked = true;
                selectedStreams.Add(availableAudioStreams[0].ManifestStream);
            }
   
            // Multiple text streams are supported.
            for (int j = 0; j < availableTextStreams.Count; j++)
            {
                if (availableTextStreams[j].isChecked)
                {
                    selectedStreams.Add(availableTextStreams[j].ManifestStream);
                }
            }
        }
   
        // Change streams on a smooth streaming presentation with multiple video streams.
        private async void changeStreams(List<IManifestStream> selectStreams)
        {
            try
            {
                IReadOnlyList<IStreamChangedResult> returnArgs =
                    await manifestObject.SelectStreamsAsync(selectStreams);
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
        #endregion stream selection
5. Recherchez hello mediaElement_ManifestReady méthode, ajoutez hello suivant du code à la fin de hello de fonction hello :
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    Par conséquent, lorsque le manifeste de MediaElement est prêt, hello code obtient une liste de flux de données disponible hello et remplit la zone de liste de l’interface utilisateur de hello avec la liste de hello.
6. À l’intérieur de hello classe MainPage, recherchez hello UI boutons cliquez sur la région d’événements et ajoutez hello après la définition de fonction :
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on hello presentation
            changeStreams(selectedStreams);
        }

**application de hello toocompile et de test**

1. Appuyez sur **F6** projet hello de toocompile. 
2. Appuyez sur **F5** application hello de toorun.
3. Haut hello du application hello, vous pouvez utiliser la valeur par défaut de hello URL de diffusion en continu lisse ou entrez un nom différent. 
4. Cliquez sur **Définir la source**. 
5. langue par défaut de Hello est audio_eng. Essayez tooswitch entre audio_eng et audio_es. Chaque fois que vous, vous sélectionnez un flux de données, vous devez cliquer sur bouton d’envoi hello.

Vous avez terminé la leçon 3.  Dans cette leçon, vous ajoutez des flux toochoose hello fonctionnalité.

## <a name="lesson-4-select-smooth-streaming-tracks"></a>Leçon 4 : sélectionner les pistes de diffusion en continu lisse
Une présentation de diffusion en continu lisse peut contenir plusieurs fichiers vidéo encodés comportant des niveaux de qualité (débit) et des résolutions différents. Dans cette leçon, vous allez activer les utilisateurs tooselect pistes. Cette leçon contient hello procédures suivantes :

1. Modifier le fichier XAML de hello
2. Modifier le fichier de behand code hello
3. Compiler et tester l’application hello

**fichier XAML de hello toomodify**

1. Dans l'Explorateur de solutions, cliquez avec le bouton droit sur **MainPage.xaml**, puis cliquez sur **Concepteur de vues**.
2. Recherchez hello &lt;grille&gt; balise avec le nom de hello **gridStreamAndBitrateSelection**, ajouter hello suivant du code à fin hello de balise de hello :
   
         <StackPanel Name="spBitRateSelection" Grid.Row="1" Grid.Column="1">
         <StackPanel Orientation="Horizontal">
             <TextBlock Name="tbBitRate" Text="Available Bitrates:" FontSize="16" VerticalAlignment="Center"/>
             <Button Name="btnChangeTracks" Content="Submit" Click="btnChangeTrack_Click" />
         </StackPanel>
         <ListBox x:Name="lbAvailableVideoTracks" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                  ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
             <ListBox.ItemTemplate>
                 <DataTemplate>
                     <CheckBox Content="{Binding Bitrate}" IsChecked="{Binding isChecked, Mode=TwoWay}"/>
                 </DataTemplate>
             </ListBox.ItemTemplate>
         </ListBox>
         </StackPanel>
3. Appuyez sur **CTRL + S** toosave il change.

**toomodify hello fichier code-behind**

1. Dans l'Explorateur de solutions, cliquez avec le bouton droit sur **MainPage.xaml**, puis cliquez sur **Afficher le code**.
2. Au sein de l’espace de noms SSPlayer hello, ajoutez une nouvelle classe :
   
        #region class Track
        public class Track
        {
            private IManifestTrack trackInfo;
            public string _bitrate;
            public bool isCheckedValue;
   
            public IManifestTrack TrackInfo
            {
                get { return trackInfo; }
                set { trackInfo = value; }
            }
   
            public string Bitrate
            {
                get { return _bitrate; }
                set { _bitrate = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    isCheckedValue = value;
                }
            }
   
            public Track(IManifestTrack trackInfoIn)
            {
                trackInfo = trackInfoIn;
                _bitrate = trackInfoIn.Bitrate.ToString();
            }
            //public Track() { }
        }
        #endregion class Track
3. Au début de hello Hello classe MainPage, ajoutez hello suivant des définitions de variables :
   
        private List<Track> availableTracks;
4. Au sein de hello classe MainPage, ajoutez hello suivant région :
   
        #region track selection
        /// <summary>
        /// Functionality tooselect video streams
        /// </summary>
   
        /// This Function gets hello tracks for hello selected video stream
        public void getTracks(Manifest manifestObject)
        {
            availableTracks = new List<Track>();
   
            IManifestStream videoStream = getVideoStream();
            IReadOnlyList<IManifestTrack> availableTracksLocal = videoStream.AvailableTracks;
            IReadOnlyList<IManifestTrack> selectedTracksLocal = videoStream.SelectedTracks;
   
            try
            {
                for (int i = 0; i < availableTracksLocal.Count; i++)
                {
                    Track thisTrack = new Track(availableTracksLocal[i]);
                    thisTrack.isChecked = true;
   
                    for (int j = 0; j < selectedTracksLocal.Count; j++)
                    {
                        string selectedTrackName = selectedTracksLocal[j].Bitrate.ToString();
                        if (selectedTrackName.Equals(thisTrack.Bitrate))
                        {
                            thisTrack.isChecked = true;
                            break;
                        }
                    }
                    availableTracks.Add(thisTrack);
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = e.Message;
            }
        }
   
        // This function gets hello video stream that is playing
        private IManifestStream getVideoStream()
        {
            IManifestStream videoStream = null;
            for (int i = 0; i < manifestObject.SelectedStreams.Count; i++)
            {
                if (manifestObject.SelectedStreams[i].Type == MediaStreamType.Video)
                {
                    videoStream = manifestObject.SelectedStreams[i];
                    break;
                }
            }
            return videoStream;
        }
   
        // This function set hello UI list box control ItemSource
        private async void refreshAvailableTracksListBoxItemSource()
        {
            try
            {
                // Update hello track check box list on hello UI 
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableVideoTracks.ItemsSource = availableTracks; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }        
        }
   
        // This function creates a list of hello selected tracks.
        private void createSelectedTracksList(List<IManifestTrack> selectedTracks)
        {
            // Create a list of selected tracks
            for (int j = 0; j < availableTracks.Count; j++)
            {
                if (availableTracks[j].isCheckedValue == true)
                {
                    selectedTracks.Add(availableTracks[j].TrackInfo);
                }
            }
        }
   
        // This function selects hello tracks based on user selection 
        private void changeTracks(List<IManifestTrack> selectedTracks)
        {
            IManifestStream videoStream = getVideoStream();
            try
            {
                videoStream.SelectTracks(selectedTracks);
            }
            catch (Exception ex)
            {
                txtStatus.Text = ex.Message;
            }
        }
        #endregion track selection
5. Recherchez hello mediaElement_ManifestReady méthode, ajoutez hello suivant du code à la fin de hello de fonction hello :
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. À l’intérieur de hello classe MainPage, recherchez hello UI boutons cliquez sur la région d’événements et ajoutez hello après la définition de fonction :
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on hello presentation
            changeStreams(selectedStreams);
         }

**application de hello toocompile et de test**

1. Appuyez sur **F6** projet hello de toocompile. 
2. Appuyez sur **F5** application hello de toorun.
3. Haut hello du application hello, vous pouvez utiliser la valeur par défaut de hello URL de diffusion en continu lisse ou entrez un nom différent. 
4. Cliquez sur **Définir la source**. 
5. Par défaut, toutes les pistes hello du flux vidéo de hello sont sélectionnées. tooexperiment hello bit de taux de change, vous pouvez sélectionnez hello plus faible vitesse de transmission disponible, puis hello plus haute vitesse de transmission disponible. Vous devez cliquer sur Envoyer après chaque modification.  Vous pouvez voir les modifications de la qualité vidéo hello.

Vous avez terminé la leçon 4.  Dans cette leçon, vous ajoutez hello fonctionnalité toochoose pistes.

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a>Autres ressources :
* [Comment toobuild une application Smooth Streaming Windows 8 JavaScript avec les fonctionnalités avancées](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [Présentation technique de la diffusion en continu lisse](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

