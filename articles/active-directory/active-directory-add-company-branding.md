---
title: "marque tooyour se connecter et pages du volet d’accès de l’entreprise aaaAdd"
description: "Découvrez comment tooadd une page toohello connectez-vous Azure marque de société et hello accéder page du Panneau de configuration"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f74621b4-4ef0-4899-8c0e-0c20347a8c31
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/23/2017
ms.author: curtand
ms.openlocfilehash: b1c6442028393552bff3d380312c8cd1bfda5d31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-and-access-panel-pages"></a>Ajouter des logos tooyour se connecter et pages du volet d’accès de la société
tooavoid confusion, de nombreuses sociétés souhaitent tooapply une apparence cohérente sur tous les sites Web de hello et services qu’ils gèrent. Azure Active Directory offre cette possibilité en vous donnant l’apparence de hello toocustomize Hello suivant des pages web avec votre logo de l’entreprise et les jeux de couleurs personnalisés :

* **Page de connexion** -il s’agit page hello qui s’affiche lorsque vous vous connectez tooOffice 365 ou autres applications web qui utilisent Azure AD comme fournisseur d’identité. Vous interagissez avec cette page pendant une découverte d’accueil ou de tooenter vos informations d’identification. Découverte d’accueil de Hello permet STS local hello système tooredirect fédéré utilisateurs tootheir (par exemple, les services AD FS).
* **Page du volet d’accès** : hello volet d’accès est un portail web qui vous permet de tooview et lancement hello les applications cloud votre administrateur Azure AD vous a accordé l’accès à. tooaccess hello volet d’accès, hello utilisation suivant URL : [https://myapps.microsoft.com](https://myapps.microsoft.com).

Cette rubrique explique comment vous pouvez personnaliser hello-page de connexion et de la page du volet d’accès hello.

> [!NOTE]
> * Marque de société est une fonctionnalité est disponible uniquement si la mise à niveau toohello Premium ou édition de base d’Azure Active Directory ou un utilisateur d’Office 365. Pour plus d’informations, consultez la page [Éditions d’Azure Active Directory](active-directory-editions.md).
> * Azure Active Directory Premium et les éditions de base sont disponibles pour les clients en Chine utilisent hello instance mondiale d’Azure Active Directory. Azure Active Directory Premium et les éditions de base ne sont pas actuellement pris en charge dans le service Microsoft Azure hello géré par 21Vianet en Chine. Pour plus d’informations, veuillez nous contacter à hello [Forum Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/).
>
>

## <a name="customizing-hello-sign-in-page"></a>Personnalisation de hello-page de connexion
En règle générale, si vous avez besoin d’accès basé sur un navigateur tooyour applications et services cloud que votre organisation est abonnée à, vous utilisez hello-page de connexion.

Si vous avez appliqué les modifications tooyour-page de connexion, il peut prendre les horaires de tooan pour tooappear de modifications hello.

Une page de connexion personnalisée s’affiche uniquement lorsque vous accédez à un service avec une URL spécifique au client, telle que https://outlook.com/**contoso**.com, ou https://mail.**contoso**.com.

Lorsque vous visitez un service avec une URL non spécifique au client (par exemple : https://mail.office365.com), une page de connexion non personnalisée s’affiche. Dans ce cas, votre marque apparaît une fois que vous avez entré votre ID d’utilisateur ou que vous avez sélectionné une vignette utilisateur.

> [!NOTE]
> * Votre nom de domaine doit être « Actif » dans hello **Active Directory** > **active** > **domaines** section Hello portail Azure classic où vous avez effectué la personnalisation.
> * Personnalisation de la page de connexion n’est pas reflétée sur la page de Microsoft de connexion consommateur toohello. Si vous vous connectez avec un compte Microsoft personnel, vous pouvez voir une liste personnalisée de vignettes utilisateur rendues par Azure AD, mais toohello Microsoft compte-page de connexion ne s’applique pas hello de personnalisation de votre organisation.
>
>

Si vous souhaitez tooshow marque de votre société, les couleurs et les autres éléments personnalisables sur cette page, consultez hello suivant images toounderstand hello différence deux expériences de hello.

Hello capture d’écran affiche et l’exemple hello Office 365-page de connexion sur un ordinateur de bureau **avant** une personnalisation :

![Page de connexion Office 365 avant la personnalisation][1]

Hello capture d’écran affiche et l’exemple hello Office 365-page de connexion sur un ordinateur de bureau **après** une personnalisation :

![Page de connexion d’Office 365 après la personnalisation][2]

Hello capture d’écran suivante montre un exemple de page de connexion hello Office 365 sur un appareil mobile **avant** une personnalisation :

![Page de connexion Office 365 avant la personnalisation][3]

Hello capture d’écran suivante montre un exemple de page de connexion hello Office 365 sur un appareil mobile **après** une personnalisation :

![Page de connexion d’Office 365 après la personnalisation][4]

Lorsque vous redimensionnez une fenêtre de navigateur, hello grande Illustration, comme hello une indiqué précédemment, est souvent rognées tooaccommodate écran différentes proportions. Dans cet esprit, vous devez essayer tookeep hello principaux éléments visuels dans l’illustration de hello afin qu’ils apparaissent toujours dans l’angle supérieur gauche de hello (en haut à droite pour les langues de droite à gauche). Ceci est important, car le redimensionnement s’effectue généralement de passer en bas à droite de hello vers hello supérieur / gauche ou bas hello vers le haut de hello.

Hello image suivante montre comment les illustration hello est rognée lorsque le navigateur de hello est redimensionné toohello gauche :

![][6]

Voici comment il apparaît une fois que le navigateur de hello est redimensionné vers le haut de hello :

![][7]

## <a name="what-elements-on-hello-page-can-i-customize"></a>Les éléments sur la page de hello puis-je personnaliser ?
Vous pouvez personnaliser hello suivant d’éléments de hello-page de connexion :

![][5]

| Élément de la page | Emplacement sur la page de hello |
|:--- | --- |
| Logo de bannière |Affiché en haut à droite de hello de page de hello. Remplace le site de destination hello logo hello que vous vous connectez dans toodisplays (par exemple. Office 365 ou Azure). |
| Grande illustration/couleur d’arrière-plan |Affiché à gauche de hello de page de hello. Remplace le site de destination hello image hello que toodisplays vous vous connectez. Hello couleur d’arrière-plan peut s’afficher à la place de hello grande Illustration sur les connexions à faible bande passante, ou sur les écrans étroits. |
| Maintenir la connexion |Indiqué sous la zone de texte de mot de passe hello. |
| Texte de la page de connexion |Affiché au-dessus pied de page hello lorsque vous avez besoin des informations utiles tooconvey avant une connexion avec un compte professionnel ou scolaire. Par exemple, vous souhaiterez tooinclude hello phone numéro tooyour d’assistance ou une mention légale. |

> [!NOTE]
> Tous ces éléments sont facultatifs. Par exemple, si vous spécifiez un Logo de bannière mais aucune grande Illustration, hello-page de connexion affiche votre illustration hello et le logo pour le site de destination hello (autrement dit, image AutoRoute hello Californie d’Office 365).
>
>

Sur votre page de connexion, hello **maintenir la connexion** case à cocher permet un tooremain utilisateur connecté lorsqu’ils ferment et rouvrir leur navigateur. Elle n’a pas d’effet sur la durée de vie de session. Vous pouvez masquer la case à cocher hello sur hello Azure Active Directory-page de connexion.

Si la case à cocher hello est affiché en fonction de définition de hello de **KMSI de masquer**.

![][9]

toohide hello case à cocher, configurez ce paramètre trop**masqué**.

> [!NOTE]
> Certaines fonctionnalités de SharePoint Online et Office 2010 dépendent des utilisateurs en mesure de toocheck cette case. Si vous configurez ce paramètre toohidden, vos utilisateurs peuvent voir des invites de supplémentaires et inattendues dans toosign.
>
>

Vous pouvez également traduire tous les éléments de cette page. Une fois que vous avez configuré un jeu d’éléments de personnalisation « par défaut », vous pouvez configurer des versions supplémentaires avec différents paramètres régionaux. Vous pouvez également combiner différents éléments. Vous pouvez par exemple afficher :

* Créez une grande illustration par défaut adaptée à toutes les cultures, puis créez des versions spécifiques pour l’anglais et le français. Lorsque vous définissez votre tooone navigateurs de ces deux langues, image spécifique de hello s’affiche, tandis que l’illustration de hello par défaut s’affiche pour tous les autres langages.
* Configurez différents logos pour votre organisation (par exemple, des versions en japonais ou en hébreu).

## <a name="access-panel-page-customization"></a>Personnalisation de la page du volet d’accès
page du volet d’accès Hello est essentiellement une page de portail pour les applications de cloud toohello accès rapide que vous disposiez d’un accès tooby votre administrateur. Dans cette page, vos applications apparaissent comme des vignettes interactives.

Hello suivant capture d’écran montre un exemple d’une page de panneau d’accès après la personnalisation.

![][8]

## <a name="configure-your-directory-with-company-branding"></a>Ajout de la marque de votre société à votre annuaire
Vous pouvez configurer un ensemble par défaut des éléments personnalisables par répertoire Bonjour portail Azure classic. Une fois que les valeurs par défaut hello ont été enregistrés, un administrateur peut ajouter des versions localisées de chaque élément, pour différentes langues / paramètres régionaux. Tous les éléments personnalisables sont facultatifs.

Par exemple, si vous configurez un Logo de bannière par défaut, mais aucune grande Illustration, hello-page de connexion affiche votre logo dans le coin supérieur droit de hello. Illustration de valeur par défaut hello du site de hello est toutefois affichée.

Imaginez hello configuration suivante :

* Un logo de bannière par défaut et le texte de la page de connexion en anglais
* Un texte spécifique pour la page de connexion en allemand

Si votre préférence de langue est l’allemand, vous obtenez hello par défaut Logo de bannière mais hello texte en allemand.

Pendant que vous pourriez techniquement un ensemble différent pour chaque langue prise en charge par Azure AD, nous vous recommandons de conserver plusieurs variantes hello faible, pour des raisons de maintenance et les performances.

> [!IMPORTANT]
> Yammer ne pas afficher les hello Azure AD marque page de connexion jusqu'à ce qu’après que hello utilisateur se connecte. utilisateur de Hello voit hello tout d’abord de page de connexion Office 365 générique, et puis hello marque page après cela.   
 
 
**tooadd marque tooyour directory d’entreprise, effectuez les hello comme suit :**

1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com) en tant qu’administrateur du répertoire de hello souhaité toocustomize.
2. Sélectionnez le répertoire hello toocustomize.
3. Dans la barre d’outils de hello en haut de hello, cliquez sur **configurer**.
4. Cliquez sur **Personnaliser la marque**.
5. Modifier les éléments hello toocustomize. Tous les champs sont facultatifs.
6. Cliquez sur **Enregistrer**.

Il peut prendre les horaires tooan pour modification apportées toohello-page de connexion tooappear de personnalisation.

**tooadd spécifiques au langage marque de l’entreprise, effectuez hello comme suit :**

1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com) en tant qu’administrateur du répertoire de hello souhaité toocustomize.
2. Sélectionnez le répertoire hello toocustomize.
fs3. Dans la barre d’outils de hello en haut de hello, cliquez sur **configurer**.
4. Cliquez sur **Personnaliser la marque**.
5. Cliquez sur **Ajouter des paramètres de marque pour une langue spécifique**.
6. Sélectionnez hello langue souhaitée logo hello toocustomize, puis cliquez sur **suivant**.
7. Modifier uniquement les éléments hello pour lequel vous souhaitez les remplacements tooconfigure spécifiques au langage. Tous les champs sont facultatifs. Si un champ est laissé vide, puis par défaut personnalisée hello est affiché à la place (ou hello par défaut, si une valeur par défaut personnalisée n’est pas configuré).
8. Cliquez sur **Enregistrer**.

**tooremove marque de société de votre annuaire, effectuer hello comme suit :**

1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com) en tant qu’administrateur du répertoire de hello souhaité toocustomize.
2. Sélectionnez le répertoire hello toocustomize.
3. Dans la barre d’outils de hello en haut de hello, cliquez sur **configurer**.
4. Cliquez sur **Personnaliser la marque**.
5. Dans la page Personnaliser la marque de hello, sélectionnez **modifier les paramètres de marque existants** puis ouvrez la page suivante de toohello.
6. Selon les éléments auxquels vous souhaitez que tooremove, effectuez une ou plusieurs des éléments suivants de hello :

    a. Sous **Logo de bannière**, sélectionnez **Supprimer le logo téléchargé**.

    b. Sous **Logo de la mosaïque**, sélectionnez **Supprimer le logo téléchargé**.

    c. Supprimez le texte hello à partir de toutes les zones de texte.

    d. Cliquez sur **Suivant**.

    e. Supprimez le texte hello à partir de toutes les zones de texte.
7. Cliquez sur **enregistrer** éléments de hello tooremove.
8. Si nécessaire, cliquez sur **personnaliser la marque** à nouveau et répétez ces étapes pour tous les spécifiques au langage de personnalisation qui doit toobe supprimée.
    Tous les paramètres de personnalisation ont été supprimés lorsque vous cliquez sur **personnaliser la marque** et consultez hello **personnaliser la marque par défaut** formulaire sans aucun paramètre configuré.

## <a name="testing-and-examples"></a>Test et exemples
Nous vous recommandons d’effectuer un test avec un client test avant d’apporter des modifications à votre environnement de production.

**tooverify si votre marque a été appliqué :**

1. Ouvrez une session de navigateur InPrivate ou Incognito.
2. Permet de consulter https://outlook.com/contoso.com, en remplaçant contoso.com par domaine hello que vous avez personnalisé.

Cela fonctionne également avec les domaines qui ressemblent à contoso.onmicrosoft.com.

toohelp vous créez des ensembles de personnalisation efficaces, nous avons personnalisé hello suivant des pages de connexion fictives deux :

* [http://aka.ms/aaddemo001](http://aka.ms/aaddemo001)
* [http://aka.ms/aaddemo002](http://aka.ms/aaddemo002)

tootest les paramètres spécifiques au langage hello, vous devez les préférences de langue par défaut toomodify hello dans votre langue tooa du navigateur web que vous avez défini dans votre personnalisation. Dans Internet Explorer, vous configurer cela dans hello **Options Internet** menu.

## <a name="customizable-elements"></a>Éléments personnalisables
Certains éléments personnalisables d’Azure AD peuvent être utilisés de plusieurs manières. Vous pouvez configurer des logos de société une fois par répertoire et que vous êtes utilisé sur les deux, connectez-vous hello et pages du volet d’accès. Certains éléments personnalisables sont spécifiques uniquement toohello-page de connexion. Hello tableau suivant fournit des détails pour hello différents éléments personnalisables.

| Nom | Description | Contraintes | Recommandations |
| --- | --- | --- | --- |
| Logo de bannière |Hello Logo de bannière s’affiche sur hello-page de connexion et du volet d’accès hello. |<p>JPG ou PNG</p><p>60x280 pixels</p><p>10 Ko</p> |<p>Utilisez le logo complet de votre organisation (y compris le pictogramme et le logo)</p><p>Conserver les tooavoid haute sous 30 pixels présentation des barres de défilement sur les appareils mobiles</p><p>Ne doit pas dépasser 4 Ko</p><p>Utilisez un fichier PNG transparent (dites-vous que page de connexion hello a toujours un arrière-plan blanc)</p> |
| Logo de la mosaïque |(actuellement non utilisé dans la page de connexion hello) Bonjour future, ce texte peut être utilisé tooreplace hello générique « compte professionnel ou scolaire » pictogramme à différents endroits de l’expérience de hello. |<p>JPG ou PNG</p><p>120x120 pixels</p><p>10 Ko</p> |<p>Conserver simple (aucun texte de petite taille), cette image ne peut être redimensionné too50 % |
| </p> | | | |
| Étiquette du nom d’utilisateur de la page de connexion |(actuellement non utilisé dans la page de connexion hello) Bonjour future, ce texte peut être utilisé tooreplace hello chaîne générique « compte professionnel ou scolaire » à différents endroits de l’expérience de hello. Vous pouvez le définir toosomething comme « Compte Contoso » ou « ID Contoso » |<p>Texte Unicode, les caractères de too50</p><p>Texte brut uniquement (aucun lien ni balise HTML)</p> |<p>Court et simple</p><p>Demandez à vos utilisateurs comment ils désignent généralement toohello travail ou compte scolaire vous leur fournissez.</p> |
| Texte de la page de connexion |Ce texte « standard » s’affiche sous forme de page de connexion hello et peut être utilisé toocommunicate des instructions supplémentaires, ou où tooget aide et support. |<p>Texte Unicode, les caractères de too256</p><p>Texte brut uniquement (aucun lien ni balise HTML)</p> |Moins de 250 caractères (environ 3 lignes de texte) |
| Illustration de la page de connexion |illustration de Hello est une grande image s’affiche à gauche de toohello hello-page de connexion sous forme de page de connexion hello. |<p>JPG ou PNG</p><p>1420x1200</p><p>500 Ko</p> |<p>1420x1200 pixels</p><p>Important : la plus petite possible, idéalement moins de 200 Ko. Si cette image est trop volumineuse, les performances de hello de hello-page de connexion sont affectées lors de l’image de hello n’est pas mis en cache.</p><p>Cette image est souvent rognée, tooaccommodate différentes proportions d’écran. Conserver les éléments visuels principal hello dans hello angle supérieur gauche (en haut à droite pour les langues RTL), redimensionnement se hello bas/droite, pointant vers hello supérieur / gauche, comme la fenêtre de navigateur hello est réduit.</p> |
| Couleur d’arrière-plan de la page de connexion |couleur d’arrière-plan de page de connexion de Hello est utilisé dans gauche de toohello zone hello sous forme de page de connexion hello. |Il doit s’agir d’une couleur RVB au format hexadécimal (par exemple #FFFFFF) |<p>couleur d’arrière-plan Hello peut s’afficher à la place de hello grande Illustration sur les connexions à faible bande passante</p><p>Nous vous suggérons de sélection de couleur primaire de hello Hello Logo de bannière</p> |

## <a name="next-steps"></a>Étapes suivantes
* [Prise en main d’Azure Active Directory Premium (AD)](active-directory-get-started-premium.md)
* [Affichage de vos rapports d’accès et d’utilisation](active-directory-view-access-usage-reports.md)

<!--Image references-->
[1]: ./media/active-directory-add-company-branding/SignInPage_beforecustomization.png
[2]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization.png
[3]: ./media/active-directory-add-company-branding/SignInPage_mobile_beforecustomization.png
[4]: ./media/active-directory-add-company-branding/SignInPage_mobile_aftercustomization.png
[5]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_elements.png
[6]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_croppedleft.png
[7]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_croppedtop.png
[8]: ./media/active-directory-add-company-branding/APBranding.png
[9]: ./media/active-directory-add-company-branding/hidekmsi.png
