---
title: "Exemple Azure IoT MyDriving : Démarrage rapide | Microsoft Docs"
description: "Prise en main une application qui est une démonstration complète de la tooarchitect un système IoT à l’aide de Microsoft Azure, notamment les flux Analytique, Machine Learning et concentrateurs d’événements."
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: f40ea71b-5721-4a6b-a886-53c2e9dffe8f
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 03/25/2016
ms.author: harikm
ms.openlocfilehash: 411b9a992deb22b915f8291d8559e2917d976b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="mydriving-iot-system-quick-start"></a><span data-ttu-id="5f8cf-103">Système IoT MyDriving : démarrage rapide</span><span class="sxs-lookup"><span data-stu-id="5f8cf-103">MyDriving IoT system: Quick start</span></span>
<span data-ttu-id="5f8cf-104">MyDriving est un système qui illustre la conception de hello et l’implémentation d’un type [Internet of Things](iot-suite-overview.md) solution (IoT) qui collecte les données de télémétrie à partir d’appareils, traite ces données dans le cloud de hello et applique l’apprentissage automatique tooprovide une réponse adaptative.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-104">MyDriving is a system that demonstrates hello design and implementation of a typical [Internet of Things](iot-suite-overview.md) (IoT) solution that gathers telemetry from devices, processes that data in hello cloud, and applies machine learning tooprovide an adaptive response.</span></span> <span data-ttu-id="5f8cf-105">démonstration de Hello consigne les données sur vos trajets en voiture, en utilisant des données à partir de votre téléphone mobile et un adaptateur qui collecte des informations de système de contrôle de votre voiture.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-105">hello demonstration logs data about your car trips, by using data from both your mobile phone and an adapter that collects information from your car’s control system.</span></span> <span data-ttu-id="5f8cf-106">Il utilise ces commentaires tooprovide de données de votre style déterminant les utilisateurs tooother de comparaison.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-106">It uses this data tooprovide feedback on your driving style in comparison tooother users.</span></span>

<span data-ttu-id="5f8cf-107">Hello réel MyDriving vise tooget que vous avez démarrées dans la création de votre propre solution IoT.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-107">hello real purpose of MyDriving is tooget you started in creating your own IoT solution.</span></span> <span data-ttu-id="5f8cf-108">Mais avant cela, nous allons vous faire découvrir l’application de MyDriving hello lui-même en tant que membre de notre équipe d’utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-108">But before that, let’s get you going with hello MyDriving app itself--as a member of our test user team.</span></span> <span data-ttu-id="5f8cf-109">Cela vous donne une expérience de l’application hello et système hello derrière lui en tant que consommateur, avant de vous plonger dans l’architecture de hello.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-109">This gives you an experience of hello app and hello system behind it as a consumer, before you delve into hello architecture.</span></span> <span data-ttu-id="5f8cf-110">Elle présente également tooHockeyApp, un moyen utile de la gestion des distributions de hello alpha et bêta de vos utilisateurs de tootest d’applications.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-110">It also introduces you tooHockeyApp, a cool way of managing hello alpha and beta distributions of your apps tootest users.</span></span>

## <a name="use-hello-mobile-experience"></a><span data-ttu-id="5f8cf-111">Utilisez l’expérience mobile de hello</span><span class="sxs-lookup"><span data-stu-id="5f8cf-111">Use hello mobile experience</span></span>
<span data-ttu-id="5f8cf-112">Vous pouvez utiliser hello MyDriving application si vous avez un appareil Android, iOS ou Windows 10.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-112">You can use hello MyDriving app if you have an Android, iOS, or Windows 10 device.</span></span>

### <a name="android-and-windows-10-mobile-installation"></a><span data-ttu-id="5f8cf-113">Installation sous Android et Windows 10 Mobile</span><span class="sxs-lookup"><span data-stu-id="5f8cf-113">Android and Windows 10 Mobile installation</span></span>
<span data-ttu-id="5f8cf-114">Sur votre appareil :</span><span class="sxs-lookup"><span data-stu-id="5f8cf-114">On your device:</span></span>

1. <span data-ttu-id="5f8cf-115">Autoriser les applications de développement :</span><span class="sxs-lookup"><span data-stu-id="5f8cf-115">Allow development apps:</span></span>
   
   * <span data-ttu-id="5f8cf-116">Android : sous **Paramètres** > **Sécurité**, autorisez les applications de **Sources inconnues**.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-116">Android: In **Settings** > **Security**, allow apps from **Unknown sources**.</span></span>
   * <span data-ttu-id="5f8cf-117">Windows 10 : sous **Paramètres** > **Mises à jour** > **Pour les développeurs**, sélectionnez **Mode développeur**.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-117">Windows 10: In **Settings** > **Updates** > **For Developers**, set **Developer mode**.</span></span>
2. <span data-ttu-id="5f8cf-118">Rejoignez notre équipe de bêta-testeurs en vous inscrivant ou en vous connectant à [HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="5f8cf-118">Join our beta test team by signing up with, or signing in to, [HockeyApp](https://rink.hockeyapp.net).</span></span> <span data-ttu-id="5f8cf-119">HockeyApp rend facile toodistribute premières versions de vos utilisateurs de tootest d’application.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-119">HockeyApp makes it easy toodistribute early releases of your app tootest users.</span></span>
   
   <span data-ttu-id="5f8cf-120">Si vous utilisez Windows 10, utilisez le navigateur Edge hello.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-120">If you’re using Windows 10, use hello Edge browser.</span></span>
   
   <span data-ttu-id="5f8cf-121">Si vous étiez un participant de la Build 2016, connectez-vous à hello même e-mail du compte Microsoft que vous avez enregistré à l’aide d’un des boutons Microsoft de hello conférence hello.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-121">If you were a Build 2016 attendee, sign in with hello same Microsoft account email that you registered for hello conference, by using one of hello Microsoft buttons.</span></span> <span data-ttu-id="5f8cf-122">Vous êtes déjà inscrit à HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-122">You’re already signed up with HockeyApp.</span></span>
   
   ![Écran de connexion de HockeyApp](./media/iot-solution-get-started/image1.png)
3. <span data-ttu-id="5f8cf-124">Téléchargez et installez l’application hello à partir d’ici :</span><span class="sxs-lookup"><span data-stu-id="5f8cf-124">Download and install hello app from here:</span></span>
   
   * [<span data-ttu-id="5f8cf-125">Android</span><span class="sxs-lookup"><span data-stu-id="5f8cf-125">Android</span></span>](http://rink.io/spMyDrivingAndroid)
   * [<span data-ttu-id="5f8cf-126">Windows 10</span><span class="sxs-lookup"><span data-stu-id="5f8cf-126">Windows 10</span></span>](http://rink.io/spMyDrivingUWP)
   
   <span data-ttu-id="5f8cf-127">Vous devez effectuer deux opérations.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-127">There are two items.</span></span> <span data-ttu-id="5f8cf-128">Installer le certificat hello dans **personnes**.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-128">Install hello certificate in **Trusted People**.</span></span> <span data-ttu-id="5f8cf-129">Installez ensuite l’application hello.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-129">Then install hello app.</span></span>

<span data-ttu-id="5f8cf-130">*Les problèmes de démarrage de l’application de hello sur Windows 10 Mobile ?*</span><span class="sxs-lookup"><span data-stu-id="5f8cf-130">*Any issues starting hello app on Windows 10 Mobile?*</span></span> <span data-ttu-id="5f8cf-131">Votre téléphone a peut-être une ou deux mises à jour de retard.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-131">Your phone might be an update or two behind.</span></span> <span data-ttu-id="5f8cf-132">Vérifiez que vous disposez des dernières mises à jour de hello ou installer :</span><span class="sxs-lookup"><span data-stu-id="5f8cf-132">Make sure you've got hello latest updates, or install:</span></span>

* [<span data-ttu-id="5f8cf-133">Microsoft.NET.Native.Framework.1.2.appx</span><span class="sxs-lookup"><span data-stu-id="5f8cf-133">Microsoft.NET.Native.Framework.1.2.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [<span data-ttu-id="5f8cf-134">Microsoft.NET.Native.Runtime.1.1.appx</span><span class="sxs-lookup"><span data-stu-id="5f8cf-134">Microsoft.NET.Native.Runtime.1.1.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [<span data-ttu-id="5f8cf-135">Microsoft.VCLibs.ARM.14.00.appx</span><span class="sxs-lookup"><span data-stu-id="5f8cf-135">Microsoft.VCLibs.ARM.14.00.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a><span data-ttu-id="5f8cf-136">Installation sous iOS</span><span class="sxs-lookup"><span data-stu-id="5f8cf-136">iOS installation</span></span>
<span data-ttu-id="5f8cf-137">Si vous avez assisté Build 2016, télécharger l’application hello en tant que membre de notre équipe de test sur HockeyApp :</span><span class="sxs-lookup"><span data-stu-id="5f8cf-137">If you attended Build 2016, download hello app as a member of our test team on HockeyApp:</span></span>

1. <span data-ttu-id="5f8cf-138">Sur votre appareil iOS, connectez-vous trop[HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="5f8cf-138">On your iOS device, sign in too[HockeyApp](https://rink.hockeyapp.net).</span></span>
   <span data-ttu-id="5f8cf-139">Utilisez une des hello boutons de connexion Microsoft, connectez-vous à l’aide hello même e-mail du compte Microsoft que vous avez enregistré avec conférence de hello.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-139">Use one of hello Microsoft sign-in buttons, and sign in with hello same Microsoft account email that you registered with hello conference.</span></span> <span data-ttu-id="5f8cf-140">(N’utilisez pas les champs par courrier électronique et le mot de passe hello).</span><span class="sxs-lookup"><span data-stu-id="5f8cf-140">(Don’t use hello email and password fields.)</span></span>
   
   ![Écran de connexion de HockeyApp](./media/iot-solution-get-started/image1.png)
2. <span data-ttu-id="5f8cf-142">Dans le tableau de bord HockeyApp hello, sélectionnez MyDriving et téléchargez-le.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-142">In hello HockeyApp dashboard, select MyDriving and download it.</span></span>
3. <span data-ttu-id="5f8cf-143">Autoriser la version bêta de hello de HockeyApp :</span><span class="sxs-lookup"><span data-stu-id="5f8cf-143">Authorize hello beta release from HockeyApp:</span></span>
   
   <span data-ttu-id="5f8cf-144">a.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-144">a.</span></span> <span data-ttu-id="5f8cf-145">Accédez trop**paramètres** > **général** > **profils et gestion des appareils.**</span><span class="sxs-lookup"><span data-stu-id="5f8cf-145">Go too**Settings** > **General** > **Profiles and Device Management.**</span></span>
   
   <span data-ttu-id="5f8cf-146">b.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-146">b.</span></span> <span data-ttu-id="5f8cf-147">Approbation hello **bits stade GmbH** certificat.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-147">Trust hello **Bit Stadium GmbH** certificate.</span></span>

<span data-ttu-id="5f8cf-148">Si vous n’êtes pas allé 2016 de Build, vous pouvez générer et déployer application hello vous-même :</span><span class="sxs-lookup"><span data-stu-id="5f8cf-148">If you didn’t attend Build 2016, you can build and deploy hello app yourself:</span></span>

1. <span data-ttu-id="5f8cf-149">Télécharger le code de hello [à partir de GitHub].</span><span class="sxs-lookup"><span data-stu-id="5f8cf-149">Download hello code [from GitHub].</span></span>
2. <span data-ttu-id="5f8cf-150">Effectuez la génération et le déploiement [à l’aide de Xamarin].</span><span class="sxs-lookup"><span data-stu-id="5f8cf-150">Build and deploy by [using Xamarin].</span></span>

<span data-ttu-id="5f8cf-151">Obtenir plus de détails dans hello [Guide de référence MyDriving](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="5f8cf-151">Find more details in hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="get-an-obd-adapter-optional"></a><span data-ttu-id="5f8cf-152">Obtenir un adaptateur OBD (facultatif)</span><span class="sxs-lookup"><span data-stu-id="5f8cf-152">Get an OBD adapter (optional)</span></span>
<span data-ttu-id="5f8cf-153">Il s’agit de partie de hello qui en fait un système Internet of Things réel !</span><span class="sxs-lookup"><span data-stu-id="5f8cf-153">This is hello part that makes this a real Internet of Things system!</span></span> <span data-ttu-id="5f8cf-154">Vous pouvez utiliser application hello, mais il est plus amusant avec la réalité hello et ils ne sont pas coûteuses.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-154">You can use hello app without one, but it’s more fun with hello real thing, and they aren’t expensive.</span></span>

<span data-ttu-id="5f8cf-155">Diagnostics intégrés (OBD) est la fonctionnalité hello votre voiture hello tootune utilise de garage votre voiture et diagnostiquer les bruits impairs et feux de l’avertissement.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-155">On-board diagnostics (OBD) is hello feature of your car that hello garage uses tootune up your car and diagnose odd noises and warning lamps.</span></span> <span data-ttu-id="5f8cf-156">Sauf si votre voiture est de grande antiquité, vous trouverez un socket quelque part dans une cabine hello, généralement derrière un rabat sous le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-156">Unless your car is of great antiquity, you’ll find a socket somewhere in hello cabin, typically behind a flap under hello dashboard.</span></span> <span data-ttu-id="5f8cf-157">Avec le connecteur de droite hello, vous pouvez obtenir les métriques de performances du moteur hello et apporter certaines modifications.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-157">With hello right connector, you can get metrics of hello engine’s performance and make certain adjustments.</span></span> <span data-ttu-id="5f8cf-158">Vous pouvez acheter un connecteur OBD à moindre coût sur à partir d’emplacements habituels de hello.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-158">An OBD connector can be purchased cheaply from hello usual places.</span></span> <span data-ttu-id="5f8cf-159">Il se connecte à l’aide des application tooan Bluetooth ou Wi-Fi sur votre téléphone.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-159">It connects by using Bluetooth or Wi-Fi tooan app on your phone.</span></span>

<span data-ttu-id="5f8cf-160">Dans ce cas, nous allons tooconnect votre cloud toohello de voiture.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-160">In this case, we’re going tooconnect your car toohello cloud.</span></span> <span data-ttu-id="5f8cf-161">connexion directe à partir de hello OBD par Hello est tooyour téléphone, mais notre application fonctionne comme un relais.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-161">hello direct connection from hello OBD is tooyour phone, but our app works as a relay.</span></span> <span data-ttu-id="5f8cf-162">Télémétrie de votre voiture est envoyé à droite toohello MyDriving IoT hub, où il est traité toolog allers-retours de votre feuille de route et évaluer votre style de conduite.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-162">Your car's telemetry is sent straight toohello MyDriving IoT hub, where it's processed toolog your road trips and assess your driving style.</span></span>

<span data-ttu-id="5f8cf-163">tooconnect un dispositif OBD :</span><span class="sxs-lookup"><span data-stu-id="5f8cf-163">tooconnect an OBD device:</span></span>

1. <span data-ttu-id="5f8cf-164">Vérifiez que votre voiture est équipée d’un connecteur OBD.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-164">Check that your car has an OBD socket.</span></span>
2. <span data-ttu-id="5f8cf-165">Procurez-vous un adaptateur OBD :</span><span class="sxs-lookup"><span data-stu-id="5f8cf-165">Obtain an OBD adapter:</span></span>
   
   * <span data-ttu-id="5f8cf-166">Si vous utilisez un téléphone Android ou Windows, vous avez besoin d’un adaptateur OBD II Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-166">If you're using an Android or Windows phone, you need a Bluetooth-enabled OBD II adapter.</span></span> <span data-ttu-id="5f8cf-167">Nous avons utilisé le modèle [BAFX Products 34t5 Bluetooth OBDII Scan Tool].</span><span class="sxs-lookup"><span data-stu-id="5f8cf-167">We used [BAFX Products 34t5 Bluetooth OBDII Scan Tool].</span></span>
   * <span data-ttu-id="5f8cf-168">Si vous utilisez un téléphone iOS, vous avez besoin d’un adaptateur OBD Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-168">If you're using an iOS phone, you need a Wi-Fi-enabled OBD adapter.</span></span> <span data-ttu-id="5f8cf-169">Nous avons utilisé le modèle [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner].</span><span class="sxs-lookup"><span data-stu-id="5f8cf-169">We used [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner].</span></span>
3. <span data-ttu-id="5f8cf-170">Suivez les instructions de hello fournis avec votre tooconnect d’adaptateur OBD tooyour phone.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-170">Follow hello instructions that come with your OBD adapter tooconnect it tooyour phone.</span></span> <span data-ttu-id="5f8cf-171">Gardez les points suivants hello à l’esprit :</span><span class="sxs-lookup"><span data-stu-id="5f8cf-171">Keep hello following in mind:</span></span>
   
   * <span data-ttu-id="5f8cf-172">Un adaptateur Bluetooth doit être associé à hello téléphone, sur hello **paramètres** page.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-172">A Bluetooth adapter must be paired with hello phone, on hello **Settings** page.</span></span>
   * <span data-ttu-id="5f8cf-173">Une carte Wi-Fi doit avoir une adresse dans hello plage 192.168.xxx.xxx.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-173">A Wi-Fi adapter must have an address in hello range 192.168.xxx.xxx.</span></span>
4. <span data-ttu-id="5f8cf-174">Si vous avez plusieurs voitures, vous pouvez vous procurer un adaptateur distinct pour chacune d’elles (trois au maximum).</span><span class="sxs-lookup"><span data-stu-id="5f8cf-174">If you have several cars, you can get a separate adapter for each (maximum of three).</span></span>

<span data-ttu-id="5f8cf-175">Si vous n’avez pas un adaptateur OBD, application hello enverra emplacement et les données de vitesse de toohello du téléphone hello GPS récepteur précédent se terminent et vous demande si vous souhaitez toosimulate un OBD.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-175">If you don’t have an OBD adapter, hello app will still send location and speed data from hello phone's GPS receiver toohello back end and will ask if you want toosimulate an OBD.</span></span>

<span data-ttu-id="5f8cf-176">Vous trouverez plus d’informations sur l’application hello utilisation de données à partir de l’adaptateur OBD hello et sur les options pour la création de votre propre appareil OBD dans la section 2.1, « Appareils IoT, » Bonjour [Guide de référence MyDriving](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="5f8cf-176">You can find out more about how hello app uses data from hello OBD adapter and about options for creating your own OBD device in section 2.1, "IoT Devices," in hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="use-hello-app"></a><span data-ttu-id="5f8cf-177">Utiliser l’application hello</span><span class="sxs-lookup"><span data-stu-id="5f8cf-177">Use hello app</span></span>
<span data-ttu-id="5f8cf-178">Démarrez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-178">Start hello app.</span></span> <span data-ttu-id="5f8cf-179">Il existe une initiale toowalk de démarrage rapide vous guide dans son fonctionnement.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-179">There’s an initial Quickstart toowalk you through how it works.</span></span>

### <a name="track-your-trips"></a><span data-ttu-id="5f8cf-180">Suivez vos trajets</span><span class="sxs-lookup"><span data-stu-id="5f8cf-180">Track your trips</span></span>
<span data-ttu-id="5f8cf-181">Appuyez sur le bouton d’enregistrement (cercle rouge big bas hello écran hello) de hello toostart un voyage, puis appuyez sur Nouveau tooend.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-181">Tap hello record button (big red circle at hello bottom of hello screen) toostart a trip, and tap again tooend.</span></span>

![Illustration du bouton d’enregistrement hello pour le voyage de suivi](./media/iot-solution-get-started/image2.png)

<span data-ttu-id="5f8cf-183">Chaque fois que vous démarrez un voyage, s’il n’existe aucun périphérique OBD, vous êtes invité si vous souhaitez que le simulateur de hello toouse.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-183">Each time you start a trip, if there’s no OBD device, you’ll be asked if you want toouse hello simulator.</span></span>

<span data-ttu-id="5f8cf-184">À fin hello d’un voyage, bouton d’arrêt tap hello et que vous obtenez un résumé.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-184">At hello end of a trip, tap hello stop button, and you get a summary.</span></span>

![Exemple de résumé d’un trajet](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a><span data-ttu-id="5f8cf-186">Passez en revue vos trajets</span><span class="sxs-lookup"><span data-stu-id="5f8cf-186">Review your trips</span></span>
![Exemple de trajet effectué](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a><span data-ttu-id="5f8cf-188">Examinez votre profil</span><span class="sxs-lookup"><span data-stu-id="5f8cf-188">Review your profile</span></span>
![Exemple de profil de style de conduite](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a><span data-ttu-id="5f8cf-190">Envoyez-nous vos commentaires sur le test</span><span class="sxs-lookup"><span data-stu-id="5f8cf-190">Send us your test feedback</span></span>
<span data-ttu-id="5f8cf-191">Car nous avons créé des systèmes de votre propre IoT MyDriving toohelp jumpstart, nous voulons certainement toohear part sur le bon fonctionnement.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-191">Because we created MyDriving toohelp jumpstart your own IoT systems, we certainly want toohear from you about how well it works.</span></span> <span data-ttu-id="5f8cf-192">Faites-nous savoir si :</span><span class="sxs-lookup"><span data-stu-id="5f8cf-192">Let us know if:</span></span>

* <span data-ttu-id="5f8cf-193">Vous rencontrez des difficultés ou des problèmes.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-193">You run into difficulties or challenges.</span></span>
* <span data-ttu-id="5f8cf-194">Il existe un point d’extension qui peut la rendre plus adapté tooyour scénario.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-194">There is an extension point that would make it more suitable tooyour scenario.</span></span>
* <span data-ttu-id="5f8cf-195">Vous trouverez un tooaccomplish de manière plus efficace de certains besoins.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-195">You find a more efficient way tooaccomplish certain needs.</span></span>
* <span data-ttu-id="5f8cf-196">Vous avez des suggestions pour améliorer MyDriving ou cette documentation.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-196">You have any other suggestions for improving MyDriving or this documentation.</span></span>

<span data-ttu-id="5f8cf-197">Au sein de l’application de MyDriving hello proprement dit, vous pouvez utiliser le mécanisme de commentaires HockeyApp intégré hello : sur iOS et Android, affectez simplement votre téléphone un secouer ou utilisez hello **commentaires** commande de menu.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-197">Within hello MyDriving app itself, you can use hello built-in HockeyApp feedback mechanism: on iOS and Android, just give your phone a shake, or use hello **Feedback** menu command.</span></span> <span data-ttu-id="5f8cf-198">Cela a pour effet de joindre automatiquement une capture d’écran qui nous permet de comprendre ce dont vous parlez.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-198">This will automatically attach a screenshot, so that we’ll know what you’re talking about.</span></span> <span data-ttu-id="5f8cf-199">Et si les pannes regrettable, HockeyApp collecte hello incident journaux tootell nous à leur sujet.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-199">And if there are any unfortunate crashes, HockeyApp collects hello crash logs tootell us about them.</span></span> <span data-ttu-id="5f8cf-200">Vous pouvez également donner des commentaires via hello [HockeyApp portal].</span><span class="sxs-lookup"><span data-stu-id="5f8cf-200">You can also give feedback through hello [HockeyApp portal].</span></span>

<span data-ttu-id="5f8cf-201">Vous pouvez également signaler un [problème sur GitHub] ou laisser un commentaire ci-dessous (édition en-us).</span><span class="sxs-lookup"><span data-stu-id="5f8cf-201">You can also file an [issue on GitHub], or leave a comment below (en-us edition).</span></span>

<span data-ttu-id="5f8cf-202">Nous attendons toohearing de votre part.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-202">We look forward toohearing from you!</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f8cf-203">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5f8cf-203">Next steps</span></span>
* <span data-ttu-id="5f8cf-204">Explorer hello [Guide de référence MyDriving](http://aka.ms/mydrivingdocs) toounderstand comment nous avons conçu et créé hello MyDriving ensemble du système.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-204">Explore hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) toounderstand how we’ve designed and built hello entire MyDriving system.</span></span>
* <span data-ttu-id="5f8cf-205">[Créez et déployez votre propre système](iot-solution-build-system.md) à l’aide de nos scripts Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-205">[Create and deploy a system of your own](iot-solution-build-system.md) by using our Azure Resource Manager scripts.</span></span> <span data-ttu-id="5f8cf-206">Hello [Guide de référence MyDriving](http://aka.ms/mydrivingdocs) vous guide également dans les zones où vous apporterez hello la plupart des personnalisations.</span><span class="sxs-lookup"><span data-stu-id="5f8cf-206">hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) also guides you through areas where you’ll make hello most customizations.</span></span>

[à partir de GitHub]: https://github.com/Azure-Samples/MyDriving
[à l’aide de Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[BAFX Products 34t5 Bluetooth OBDII Scan Tool]: http://www.amazon.com/gp/product/B005NLQAHS
[ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[HockeyApp portal]: https://rink.hockeyapp.org
[problème sur GitHub]: https://github.com/Azure-Samples/MyDriving/issues
