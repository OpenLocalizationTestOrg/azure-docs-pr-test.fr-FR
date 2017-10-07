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
# <a name="mydriving-iot-system-quick-start"></a>Système IoT MyDriving : démarrage rapide
MyDriving est un système qui illustre la conception de hello et l’implémentation d’un type [Internet of Things](iot-suite-overview.md) solution (IoT) qui collecte les données de télémétrie à partir d’appareils, traite ces données dans le cloud de hello et applique l’apprentissage automatique tooprovide une réponse adaptative. démonstration de Hello consigne les données sur vos trajets en voiture, en utilisant des données à partir de votre téléphone mobile et un adaptateur qui collecte des informations de système de contrôle de votre voiture. Il utilise ces commentaires tooprovide de données de votre style déterminant les utilisateurs tooother de comparaison.

Hello réel MyDriving vise tooget que vous avez démarrées dans la création de votre propre solution IoT. Mais avant cela, nous allons vous faire découvrir l’application de MyDriving hello lui-même en tant que membre de notre équipe d’utilisateur de test. Cela vous donne une expérience de l’application hello et système hello derrière lui en tant que consommateur, avant de vous plonger dans l’architecture de hello. Elle présente également tooHockeyApp, un moyen utile de la gestion des distributions de hello alpha et bêta de vos utilisateurs de tootest d’applications.

## <a name="use-hello-mobile-experience"></a>Utilisez l’expérience mobile de hello
Vous pouvez utiliser hello MyDriving application si vous avez un appareil Android, iOS ou Windows 10.

### <a name="android-and-windows-10-mobile-installation"></a>Installation sous Android et Windows 10 Mobile
Sur votre appareil :

1. Autoriser les applications de développement :
   
   * Android : sous **Paramètres** > **Sécurité**, autorisez les applications de **Sources inconnues**.
   * Windows 10 : sous **Paramètres** > **Mises à jour** > **Pour les développeurs**, sélectionnez **Mode développeur**.
2. Rejoignez notre équipe de bêta-testeurs en vous inscrivant ou en vous connectant à [HockeyApp](https://rink.hockeyapp.net). HockeyApp rend facile toodistribute premières versions de vos utilisateurs de tootest d’application.
   
   Si vous utilisez Windows 10, utilisez le navigateur Edge hello.
   
   Si vous étiez un participant de la Build 2016, connectez-vous à hello même e-mail du compte Microsoft que vous avez enregistré à l’aide d’un des boutons Microsoft de hello conférence hello. Vous êtes déjà inscrit à HockeyApp.
   
   ![Écran de connexion de HockeyApp](./media/iot-solution-get-started/image1.png)
3. Téléchargez et installez l’application hello à partir d’ici :
   
   * [Android](http://rink.io/spMyDrivingAndroid)
   * [Windows 10](http://rink.io/spMyDrivingUWP)
   
   Vous devez effectuer deux opérations. Installer le certificat hello dans **personnes**. Installez ensuite l’application hello.

*Les problèmes de démarrage de l’application de hello sur Windows 10 Mobile ?* Votre téléphone a peut-être une ou deux mises à jour de retard. Vérifiez que vous disposez des dernières mises à jour de hello ou installer :

* [Microsoft.NET.Native.Framework.1.2.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [Microsoft.NET.Native.Runtime.1.1.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [Microsoft.VCLibs.ARM.14.00.appx](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a>Installation sous iOS
Si vous avez assisté Build 2016, télécharger l’application hello en tant que membre de notre équipe de test sur HockeyApp :

1. Sur votre appareil iOS, connectez-vous trop[HockeyApp](https://rink.hockeyapp.net).
   Utilisez une des hello boutons de connexion Microsoft, connectez-vous à l’aide hello même e-mail du compte Microsoft que vous avez enregistré avec conférence de hello. (N’utilisez pas les champs par courrier électronique et le mot de passe hello).
   
   ![Écran de connexion de HockeyApp](./media/iot-solution-get-started/image1.png)
2. Dans le tableau de bord HockeyApp hello, sélectionnez MyDriving et téléchargez-le.
3. Autoriser la version bêta de hello de HockeyApp :
   
   a. Accédez trop**paramètres** > **général** > **profils et gestion des appareils.**
   
   b. Approbation hello **bits stade GmbH** certificat.

Si vous n’êtes pas allé 2016 de Build, vous pouvez générer et déployer application hello vous-même :

1. Télécharger le code de hello [à partir de GitHub].
2. Effectuez la génération et le déploiement [à l’aide de Xamarin].

Obtenir plus de détails dans hello [Guide de référence MyDriving](http://aka.ms/mydrivingdocs).

## <a name="get-an-obd-adapter-optional"></a>Obtenir un adaptateur OBD (facultatif)
Il s’agit de partie de hello qui en fait un système Internet of Things réel ! Vous pouvez utiliser application hello, mais il est plus amusant avec la réalité hello et ils ne sont pas coûteuses.

Diagnostics intégrés (OBD) est la fonctionnalité hello votre voiture hello tootune utilise de garage votre voiture et diagnostiquer les bruits impairs et feux de l’avertissement. Sauf si votre voiture est de grande antiquité, vous trouverez un socket quelque part dans une cabine hello, généralement derrière un rabat sous le tableau de bord hello. Avec le connecteur de droite hello, vous pouvez obtenir les métriques de performances du moteur hello et apporter certaines modifications. Vous pouvez acheter un connecteur OBD à moindre coût sur à partir d’emplacements habituels de hello. Il se connecte à l’aide des application tooan Bluetooth ou Wi-Fi sur votre téléphone.

Dans ce cas, nous allons tooconnect votre cloud toohello de voiture. connexion directe à partir de hello OBD par Hello est tooyour téléphone, mais notre application fonctionne comme un relais. Télémétrie de votre voiture est envoyé à droite toohello MyDriving IoT hub, où il est traité toolog allers-retours de votre feuille de route et évaluer votre style de conduite.

tooconnect un dispositif OBD :

1. Vérifiez que votre voiture est équipée d’un connecteur OBD.
2. Procurez-vous un adaptateur OBD :
   
   * Si vous utilisez un téléphone Android ou Windows, vous avez besoin d’un adaptateur OBD II Bluetooth. Nous avons utilisé le modèle [BAFX Products 34t5 Bluetooth OBDII Scan Tool].
   * Si vous utilisez un téléphone iOS, vous avez besoin d’un adaptateur OBD Wi-Fi. Nous avons utilisé le modèle [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner].
3. Suivez les instructions de hello fournis avec votre tooconnect d’adaptateur OBD tooyour phone. Gardez les points suivants hello à l’esprit :
   
   * Un adaptateur Bluetooth doit être associé à hello téléphone, sur hello **paramètres** page.
   * Une carte Wi-Fi doit avoir une adresse dans hello plage 192.168.xxx.xxx.
4. Si vous avez plusieurs voitures, vous pouvez vous procurer un adaptateur distinct pour chacune d’elles (trois au maximum).

Si vous n’avez pas un adaptateur OBD, application hello enverra emplacement et les données de vitesse de toohello du téléphone hello GPS récepteur précédent se terminent et vous demande si vous souhaitez toosimulate un OBD.

Vous trouverez plus d’informations sur l’application hello utilisation de données à partir de l’adaptateur OBD hello et sur les options pour la création de votre propre appareil OBD dans la section 2.1, « Appareils IoT, » Bonjour [Guide de référence MyDriving](http://aka.ms/mydrivingdocs).

## <a name="use-hello-app"></a>Utiliser l’application hello
Démarrez l’application hello. Il existe une initiale toowalk de démarrage rapide vous guide dans son fonctionnement.

### <a name="track-your-trips"></a>Suivez vos trajets
Appuyez sur le bouton d’enregistrement (cercle rouge big bas hello écran hello) de hello toostart un voyage, puis appuyez sur Nouveau tooend.

![Illustration du bouton d’enregistrement hello pour le voyage de suivi](./media/iot-solution-get-started/image2.png)

Chaque fois que vous démarrez un voyage, s’il n’existe aucun périphérique OBD, vous êtes invité si vous souhaitez que le simulateur de hello toouse.

À fin hello d’un voyage, bouton d’arrêt tap hello et que vous obtenez un résumé.

![Exemple de résumé d’un trajet](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a>Passez en revue vos trajets
![Exemple de trajet effectué](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a>Examinez votre profil
![Exemple de profil de style de conduite](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a>Envoyez-nous vos commentaires sur le test
Car nous avons créé des systèmes de votre propre IoT MyDriving toohelp jumpstart, nous voulons certainement toohear part sur le bon fonctionnement. Faites-nous savoir si :

* Vous rencontrez des difficultés ou des problèmes.
* Il existe un point d’extension qui peut la rendre plus adapté tooyour scénario.
* Vous trouverez un tooaccomplish de manière plus efficace de certains besoins.
* Vous avez des suggestions pour améliorer MyDriving ou cette documentation.

Au sein de l’application de MyDriving hello proprement dit, vous pouvez utiliser le mécanisme de commentaires HockeyApp intégré hello : sur iOS et Android, affectez simplement votre téléphone un secouer ou utilisez hello **commentaires** commande de menu. Cela a pour effet de joindre automatiquement une capture d’écran qui nous permet de comprendre ce dont vous parlez. Et si les pannes regrettable, HockeyApp collecte hello incident journaux tootell nous à leur sujet. Vous pouvez également donner des commentaires via hello [HockeyApp portal].

Vous pouvez également signaler un [problème sur GitHub] ou laisser un commentaire ci-dessous (édition en-us).

Nous attendons toohearing de votre part.

## <a name="next-steps"></a>Étapes suivantes
* Explorer hello [Guide de référence MyDriving](http://aka.ms/mydrivingdocs) toounderstand comment nous avons conçu et créé hello MyDriving ensemble du système.
* [Créez et déployez votre propre système](iot-solution-build-system.md) à l’aide de nos scripts Azure Resource Manager. Hello [Guide de référence MyDriving](http://aka.ms/mydrivingdocs) vous guide également dans les zones où vous apporterez hello la plupart des personnalisations.

[à partir de GitHub]: https://github.com/Azure-Samples/MyDriving
[à l’aide de Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[BAFX Products 34t5 Bluetooth OBDII Scan Tool]: http://www.amazon.com/gp/product/B005NLQAHS
[ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[HockeyApp portal]: https://rink.hockeyapp.org
[problème sur GitHub]: https://github.com/Azure-Samples/MyDriving/issues
