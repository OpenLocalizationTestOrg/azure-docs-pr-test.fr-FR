---
title: "aaaSetting accès conditionnel en local à l’aide de l’inscription de périphérique Azure Active Directory | Documents Microsoft"
description: "Un guide pas à pas tooenabling l’accès conditionnel tooon applications locales à l’aide des Services de fédération Active Directory (AD FS) dans Windows Server 2012 R2."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6ae9df8b-31fe-4d72-9181-cf50cfebbf05
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 808e3b96873102aebae667153f588dcdb205e884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-on-premises-conditional-access-by-using-azure-active-directory-device-registration"></a>Configuration d’un accès conditionnel en local à l’aide du service Azure Active Directory Device Registration
Lorsque vous avez besoin des utilisateurs tooworkplace-jointure leur appareils personnels de toohello service d’inscription de périphérique Azure Active Directory (Azure AD), leurs appareils peuvent être marqués en tant qu’organisation de tooyour connus. Voici un guide pas à pas pour activer des applications de tooon local d’accès conditionnel à l’aide des Services de fédération Active Directory (AD FS) dans Windows Server 2012 R2.

> [!NOTE]
> Une licence Office 365 ou Azure AD Premium est nécessaire pour utiliser des appareils enregistrés dans les stratégies d’accès conditionnel du service Azure Active Directory Device Registration. Ces stratégies se composent notamment de celles qui sont appliquées par AD FS dans les ressources locales.
> 
> Pour plus d’informations sur les scénarios d’accès conditionnel hello pour les ressources locales, consultez [joindre tooworkplace à partir de n’importe quel appareil pour l’authentification unique et une authentification multifacteur transparente entre les applications d’entreprise](https://technet.microsoft.com/library/dn280945.aspx).

Ces fonctionnalités sont disponibles toocustomers qui achètent une licence Azure Active Directory Premium.

## <a name="supported-devices"></a>Appareils pris en charge
* Appareils Windows 7 joints à un domaine
* Appareils Windows 8.1 personnels et joints à un domaine
* iOS 6 et versions ultérieures pour le navigateur Safari hello
* Android 4.0 ou versions ultérieures, téléphones Samsung GS3 ou versions ultérieures, Samsung Galaxy Note 2 ou tablettes plus récentes

## <a name="scenario-prerequisites"></a>Configuration requise pour le scénario
* Abonnement tooOffice 365 ou Azure Active Directory Premium
* Un client Azure Active Directory
* Windows Server Active Directory (Windows Server 2008 ou versions ultérieures)
* Schéma mis à jour dans Windows Server 2012 R2
* Une licence Azure Active Directory Premium
* Windows Server 2012 R2 Federation Services, configuré pour l’authentification unique tooAzure AD
* Proxy d’application web Windows Server 2012 R2 
* Microsoft Azure Active Directory Connect (Azure AD Connect) [(Télécharger Azure AD Connect)](http://www.microsoft.com/en-us/download/details.aspx?id=47594)
* Domaine vérifié

## <a name="known-issues-in-this-release"></a>Problèmes connus dans cette version
* Stratégies d’accès conditionnel appareil nécessitent tooActive de l’écriture différée objet périphérique active à partir d’Azure Active Directory. Il peut prendre jusqu'à heures toothree toobe d’objets périphériques tooActive active de l’écriture.
* les appareils iOS 7 invitent toujours hello utilisateur tooselect un certificat lors de l’authentification de certificat client.
* Certaines versions d’iOS8 antérieures à iOS 8.3 ne fonctionnent pas.

## <a name="scenario-assumptions"></a>Hypothèses de scénario
Ce scénario suppose que vous disposez d’un environnement hybride comprenant un locataire Azure AD et une instance Active Directory locale. Ces locataires doivent être connectés avec Azure AD Connect, un domaine vérifié et AD FS pour l’authentification unique. Utilisez hello suivant toohelp de liste de vérification vous configurer votre environnement en fonction des exigences de toohello.

## <a name="checklist-prerequisites-for-conditional-access-scenario"></a>Liste de vérification : prérequis pour un scénario d’accès conditionnel
Connectez votre locataire Azure AD avec votre instance Active Directory locale.

## <a name="configure-azure-active-directory-device-registration-service"></a>Configurer le service Azure Active Directory Device Registration
Utilisez ce guide toodeploy et configurer hello Azure Active Directory device registration service pour votre organisation.

Ce guide suppose que vous avez configuré Windows Server Active Directory et que vous êtes abonné tooMicrosoft Azure Active Directory. Voir les conditions préalables de hello décrits précédemment.

toodeploy hello device registration service Active Directory de Azure avec Azure Active Directory du client, les tâches hello complète Bonjour suit la liste de vérification dans l’ordre. Lorsqu’un lien de référence vous redirige rubrique conceptuelle de tooa, retournent toothis la liste de vérification par la suite, vous pouvez poursuivre hello les tâches restantes. Certaines tâches incluent une étape de validation de scénario qui peut vous aider à confirmer si les étape hello sont terminée avec succès.

## <a name="part-1-enable-azure-active-directory-device-registration"></a>1ère partie : Activer le service Azure Active Directory Device Registration
Suivez les étapes de hello dans tooenable de liste de vérification hello et configurer hello Azure Active Directory device registration service.

| Task | Référence | 
| --- | --- |
| Activer l’inscription de périphérique dans votre entreprise de hello Azure Active Directory locataire tooallow périphériques toojoin. Par défaut, l’authentification multifacteur Azure n’est pas activée pour le service de hello. Cependant, nous vous recommandons d’utiliser l’authentification multifacteur pendant l’inscription d’un appareil. Avant d’activer l’authentification multifacteur dans le service d’inscripton Active Directory, vérifiez que les services AD FS sont configurés pour un fournisseur d’authentification multifacteur. |[Activer le service Azure Active Directory Device Registration](active-directory-device-registration-get-started.md)| 
|Les appareils détectent votre service Azure Active Directory Device Registration en recherchant des enregistrements DNS connus. Configurez le DNS de votre entreprise de sorte que les appareils puissent détecter le service Azure Active Directory Device Registration. |[Configurer la découverte du service Azure Active Directory Device Registration](active-directory-device-registration-get-started.md)| 


## <a name="part-2-deploy-and-configure-windows-server-2012-r2-active-directory-federation-services-and-set-up-a-federation-relationship-with-azure-ad"></a>2ème partie : Déployer et configurer Windows Server 2012 R2 Active Directory Federation Services et configurer une relation de fédération avec Azure AD

| Task | Référence |
| --- | --- |
| Déployer des Services de domaine Active Directory avec les extensions de schéma Windows Server 2012 R2 hello. Il est inutile tooupgrade un de vos tooWindows de contrôleurs de domaine Server 2012 R2. mise à niveau du schéma Hello est la seule exigence de hello. |[Mettre à niveau le schéma Active Directory Domain Services](#upgrade-your-active-directory-domain-services-schema) |
| Les appareils détectent votre service Azure Active Directory Device Registration en recherchant des enregistrements DNS connus. Configurez le DNS de votre entreprise de sorte que les appareils puissent détecter le service Azure Active Directory Device Registration. |[Préparation de votre Active Directory à la prise en charge d'appareils](#prepare-your-active-directory-to-support-devices) |

## <a name="part-3-enable-device-writeback-in-azure-ad"></a>3ème partie : Activer l'écriture différée des appareils dans Azure AD
| Task | Référence |
| --- | --- |
| Terminez la 2ème partie de l’activation de l’écriture différée des appareils dans Azure AD Connect. Une fois que vous avez terminé, retour toothis guide. |[Activation de l’écriture différée des appareils dans Azure AD Connect](#upgrade-your-active-directory-domain-services-schema) |

## <a name="optional-part-4-enable-multi-factor-authentication"></a>[Facultatif] 4ème partie : Activer l’authentification multifacteur
Nous recommandons vivement que vous configurez l’un des hello plusieurs options pour l’authentification multifacteur. Si vous souhaitez toorequire l’authentification multifacteur, consultez [choisir la solution de sécurité de l’authentification multifacteur hello vous](../multi-factor-authentication/multi-factor-authentication-get-started.md). Il inclut une description de chaque solution et lie toohelp vous configurez la solution hello de votre choix.

## <a name="part-5-verification"></a>5ème partie : Vérification
Hello déploiement est maintenant terminé, et vous pouvez essayer de certains scénarios. Utilisez hello suivant lie tooexperiment avec le service de hello et vous familiariser avec ses fonctionnalités.

| Task | Référence |
| --- | --- |
| Joindre des espace de travail tooyour périphériques à l’aide du service d’inscription de périphérique Azure Active Directory. Vous pouvez joindre des appareils iOS, Windows et Android. |[Joindre l’espace de travail tooyour périphériques avec Azure Active Directory device registration service](#join-devices-to-your-workplace-using-azure-active-directory-device-registration) |
| Afficher et activer ou désactiver les appareils inscrits à l’aide du portail d’administration hello. Dans cette tâche, vous permet d’afficher certains appareils inscrits à l’aide du portail d’administration hello. |[Vue d’ensemble du service Azure Active Directory Device Registration](active-directory-device-registration-get-started.md) |
| Vérifiez que les objets périphériques sont réécrits à partir d’Azure Active Directory tooWindows Server Active Directory. |[Vérifiez que les appareils inscrits sont réécrits tooActive Active](#verify-registered-devices-are-written-back-to-active-directory) |
| Maintenant que les utilisateurs peuvent inscrire leurs appareils, vous pouvez créer des stratégies d'accès à l'application dans AD FS qui autorisent uniquement les appareils inscrits. Cette tâche consiste à créer une règle d’accès à l’application et un message personnalisé d’accès refusé. |[Créer une stratégie d’accès à une application et un message personnalisé de refus d’accès](#create-an-application-access-policy-and-custom-access-denied-message) |

## <a name="integrate-azure-active-directory-with-on-premises-active-directory"></a>Intégration d’Azure Active Directory au répertoire Active Directory local
Cette étape vise à vous faire intégrer votre locataire Azure AD à votre instance Active Directory locale à l’aide d’Azure AD Connect. Bien que les étapes de hello sont disponibles dans hello portail Azure classic, notez les instructions spéciales qui sont répertoriées dans cette section.

1. Se connecter toohello portail Azure classic à l’aide d’un compte qui est un administrateur global dans Azure AD.
2. Dans le volet gauche de hello, sélectionnez **Active Directory**.
3. Sur hello **répertoire** , sélectionnez votre annuaire.
4. Sélectionnez hello **intégration d’annuaire** onglet.
5. Sous hello **déployer et gérer des** section, suivez les étapes 1 à 3 toointegrate Azure Active Directory avec votre annuaire local.
   
   1. Ajoutez des domaines.
   2. Installer et exécuter Azure AD Connect à l’aide d’instructions hello à [installation personnalisée d’Azure AD Connect](connect/active-directory-aadconnect-get-started-custom.md).
   3. Vérifiez et gérez la synchronisation des répertoires. Les instructions de l'authentification unique sont disponibles dans cette étape.
   
   Par ailleurs, configurez la fédération avec AD FS comme indiqué dans [Installation personnalisée d’Azure AD Connect](connect/active-directory-aadconnect-get-started-custom.md).

## <a name="upgrade-your-active-directory-domain-services-schema"></a>Mettre à niveau le schéma des services de domaine Active Directory
> [!NOTE]
> Une fois que vous mettez à niveau votre schéma Active Directory, les processus hello ne peut pas être annulée. Nous vous recommandons d’abord effectuer la mise à niveau de hello dans un environnement de test.
> 

1. Connectez-vous tooyour contrôleur de domaine avec un compte disposant des droits d’administrateur de schéma et d’administrateur d’entreprise.
2. Hello de copie **[media] \support\adprep** tooone de répertoire et les sous-répertoires de vos contrôleurs de domaine Active Directory (où **[media]** est le support d’installation de Windows Server 2012 R2 hello chemin d’accès toohello ).
4. À partir d’une invite de commandes, accédez à toohello **adprep** répertoire et exécutez **adprep.exe /forestprep**. Suivez la mise à niveau du schéma de hello toocomplete hello instructions à l’écran.

## <a name="prepare-your-active-directory-toosupport-devices"></a>Préparer vos appareils toosupport de Active Directory
> [!NOTE]
> Il s’agit d’une opération unique que vous devez exécuter tooprepare vos appareils toosupport de forêt Active Directory. toocomplete cette procédure, vous devez être connecté avec des autorisations d’administrateur d’entreprise et votre forêt Active Directory doit posséder le schéma de Windows Server 2012 R2 de hello.
> 


### <a name="prepare-your-active-directory-forest"></a>Préparer votre forêt Active Directory
1. Sur votre serveur de fédération, ouvrez une fenêtre de commande Windows PowerShell, puis tapez **Initialize-ADDeviceRegistration**. 
2. Lorsque vous y êtes invité pour **ServiceAccountName**, entrez le nom hello hello du compte de service vous avez sélectionné comme compte de service hello pour AD FS. S’il est un compte de service administré de groupe, entrez le compte de hello Bonjour **domain\accountname$** format. Pour un compte de domaine, utilisez le format de hello **domain\accountname**.

### <a name="enable-device-authentication-in-ad-fs"></a>Activer l’authentification d’appareils dans AD FS
1. Sur votre serveur de fédération, ouvrez la console de gestion de hello AD FS et accédez trop**AD FS** > **des stratégies d’authentification**.
2. Sur hello **Actions** volet, sélectionnez **modifier l’authentification principale globale**.
3. Cochez **Activer l’authentification des appareils**, puis sélectionnez **OK**.
4. Par défaut, AD FS supprime régulièrement les appareils non utilisés d’Active Directory. Désactivez cette tâche quand vous utilisez le service Azure Active Directory Device Registration pour permettre la gestion des appareils dans Azure.

### <a name="disable-unused-device-cleanup"></a>Désactiver le nettoyage des appareils non utilisés
Sur votre serveur de fédération, ouvrez une fenêtre de commande Windows PowerShell, puis tapez **Set-AdfsDeviceRegistration -MaximumInactiveDays 0**.

### <a name="prepare-azure-ad-connect-for-device-writeback"></a>Préparation d'Azure AD Connect pour l'écriture différée des appareils
Terminez la partie 1 : Préparer Azure AD Connect.

## <a name="join-devices-tooyour-workplace-by-using-azure-active-directory-device-registration-service"></a>Joindre un espace de travail tooyour périphériques à l’aide du service d’inscription de périphérique Azure Active Directory

### <a name="join-an-ios-device-by-using-azure-active-directory-device-registration"></a>Joindre un appareil iOS à l’aide du service Azure Active Directory Device Registration
L’inscription de périphérique Azure Active Directory utilise le processus d’inscription de profil de l’air hello pour les appareils iOS. Ce processus commence lorsque les utilisateur hello connecte toohello profil d’inscription URL avec Safari. format d’URL Hello est comme suit :

    https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/"yourdomainname"

Dans ce cas, `yourdomainname` est le nom de domaine hello que vous avez configuré avec Azure Active Directory. Par exemple, si votre nom de domaine est contoso.com, URL de hello est comme suit :

    https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/contoso.com

Nombreuses façons toocommunicate cette URL tooyour utilisateurs est. Par exemple, l’une des méthodes que nous recommandons consiste à publier cette URL dans un message personnalisé de refus d’accès à l’application dans AD FS. Cette information est décrite dans section à venir de hello [créer une stratégie d’accès application et le message d’accès refusé personnalisé](#create-an-application-access-policy-and-custom-access-denied-message).

### <a name="join-a-windows-81-device-by-using-azure-active-directory-device-registration"></a>Joindre un appareil Windows 8.1 à l’aide du service Azure Active Directory Device Registration
1. Sur votre appareil Windows 8.1, sélectionnez **Paramètres du PC** > **Réseau** > **Lieu de travail**.
2. Entrez votre nom d’utilisateur au format UPN (par exemple, **dan@contoso.com**).
3. Sélectionnez **Joindre**.
4. Quand vous y êtes invité, connectez-vous avec vos informations d’identification. Hello appareil est maintenant joint.

### <a name="join-a-windows-7-device-by-using-azure-active-directory-device-registration"></a>Joindre un appareil Windows 7 à l’aide du service Azure Active Directory Device Registration
tooregister Windows 7 joints à un domaine des appareils, vous devez le package logiciel d’inscription toodeploy hello appareil. Hello package logiciel est appelé Workplace Join for Windows 7 et ses disponible pour téléchargement à l’adresse hello [site Web Microsoft Connect](https://connect.microsoft.com/site1164). 

Des instructions sur la façon dont toouse hello package sont disponibles dans [comment tooconfigure l’inscription automatique de Windows appartenant au domaine des appareils avec Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).

## <a name="verify-that-registered-devices-are-written-back-tooactive-directory"></a>Vérifiez que les appareils inscrits sont réécrits tooActive Active
Vous pouvez afficher et vérifier que vos objets d’appareil ayant été réécrits dans tooyour Active Directory à l’aide de LDP.exe ou ADSI Edit. Les deux sont disponibles avec les outils d’administration Active Directory hello.

Par défaut, les objets d’appareil sont réécrits à partir d’Azure Active Directory sont placés dans hello même domaine que votre batterie AD FS.

    CN=RegisteredDevices,defaultNamingContext

## <a name="create-an-application-access-policy-and-custom-access-denied-message"></a>Créer une stratégie d’accès à une application et un message personnalisé de refus d’accès
Envisagez de hello scénario : vous créez une application de confiance dans AD FS et configurer une règle d’autorisation d’émission qui autorise uniquement les appareils inscrits. Maintenant que les périphériques qui sont inscrits sont autorisés application hello de tooaccess. 

toomake facilement votre application de toohello utilisateurs toogain access, vous configurez un message de refus d’accès personnalisé qui fournit des instructions de toojoin leur appareil. Maintenant vos utilisateurs disposent d’un tooregister de manière transparente leurs appareils afin qu’ils peuvent accéder à une application.

Hello étapes suivantes vous montrent comment tooimplement ce scénario.

> [!NOTE]
> Cette section part du principe que vous avez déjà configuré une approbation de partie de confiance pour votre application dans AD FS.
> 

1. Ouvrez hello outil MMC AD FS, puis **AD FS** > **relations d’approbation** > **confiance**.
2. Recherchez toowhich d’application hello que cette nouvelle règle d’accès s’applique. Application hello d’avec le bouton droit et sélectionnez **modifier les règles de revendication**.
3. Sélectionnez hello **les règles d’autorisation d’émission** onglet, puis sélectionnez **ajouter une règle**.
4. À partir de hello **règle de revendication** la liste déroulante modèle, sélectionnez **autoriser ou refuser les utilisateurs en fonction d’une revendication entrante**. Sélectionnez ensuite **Suivant**.
5. Bonjour **nom de règle de revendication** , tapez **autoriser l’accès aux appareils inscrits**.
6. À partir de hello **type de revendication entrante** la liste déroulante, sélectionnez **est un utilisateur inscrit**.
7. Bonjour **valeur de revendication entrante** , tapez **true**.
8. Sélectionnez hello **toousers d’accès Autoriser avec cette revendication entrante** case d’option.
9. Sélectionnez **Terminer**, puis **Appliquer**.
10. Supprimer toutes les règles qui sont plus permissives que la règle hello que vous avez créé. Par exemple, supprimez la règle par défaut de hello **tooall d’autoriser l’accès aux utilisateurs**.

Votre application est maintenant configuré tooallow accéder uniquement lorsque l’utilisateur de hello provient d’un appareil qu’ils inscrit et joints à un espace de travail toohello. Pour des stratégies d’accès plus avancées, consultez [Gérer les risques avec une authentification multifacteur supplémentaire pour les applications sensibles](https://technet.microsoft.com/library/dn280949.aspx).

Configurez ensuite un message d’erreur personnalisé pour votre application. message d’erreur Hello informe les utilisateurs qu’ils doivent joindre leur espace de travail toohello appareil avant qu’ils puissent accéder à application hello. Vous pouvez créer un message personnalisé de refus d’accès à l’application en utilisant du code HTML personnalisé et PowerShell.

Sur votre serveur de fédération, ouvrez une fenêtre de commande PowerShell, puis tapez Bonjour commande suivante. Remplacer des parties de la commande hello avec les éléments qui sont spécifiques tooyour système :

    Set-AdfsRelyingPartyWebContent -Name "relying party trust name" -ErrorPageAuthorizationErrorMessage
Vous devez inscrire votre appareil avant d'accéder à cette application.

**Si vous utilisez un appareil iOS, sélectionnez ce toojoin lien votre appareil**:

    a href='https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/yourdomain.com

Joignez cet espace de travail tooyour de périphérique iOS.

Si vous utilisez un appareil Windows 8.1, vous pouvez joindre votre appareil en sélectionnant **Paramètres du PC**> **Réseau** > **Espace de travail**.

Bonjour précédant les commandes, **nom d’approbation de partie de confiance tiers** est le nom hello votre objet de l’application de confiance dans AD FS.
Et **votredomaine.com** est le nom de domaine hello que vous avez configuré avec Azure Active Directory (par exemple, contoso.com).
Être tooremove que les sauts de ligne (le cas échéant) à partir de hello HTML contenu que vous passez toohello **Set-AdfsRelyingPartyWebContent** applet de commande.

Maintenant lorsque les utilisateurs accèdent à votre application à partir d’un périphérique qui n’est pas inscrit avec hello service d’inscription de périphérique Azure Active Directory, ils voient une page similaire toohello suivant capture d’écran de recherche.

![Capture d’écran d’une erreur qui s’affiche quand les utilisateurs n’ont pas enregistré leur appareil auprès d’Azure AD](./media/active-directory-conditional-access/error-azureDRS-device-not-registered.gif)


