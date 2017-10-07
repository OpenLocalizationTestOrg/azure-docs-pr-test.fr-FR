---
title: "aaaProblem configuration de mot de passe l’authentification unique pour une application non-galerie | Documents Microsoft"
description: "Comprendre le cadran de personnes hello courantes des problèmes lors de la configuration de mot de passe Single Sign-on pour les applications non-galerie personnalisées qui ne sont pas répertoriées dans hello Galerie d’applications Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 3aee0a4c525bb3da338da2da0882ec572cf0e5e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a>Problème de configuration de l’authentification unique avec mot de passe pour une application non issue de la galerie

Cet article vous a-t-il face de personnes toounderstand hello courantes des problèmes lors de la configuration **mot de passe l’authentification unique sur** avec une application non-galerie.

## <a name="how-toocapture-sign-in-fields-for-an-application"></a>Comment se connecter toocapture dans des champs pour une application

La capture des champs de connexion est uniquement prise en charge pour les pages de connexion HTML et **n’est pas prise en charge pour les pages de connexion non standard** comme celles qui utilisent Flash ou d’autres technologies non HTML.

Deux options s’offrent à vous pour capturer des champs de connexion dans vos applications personnalisées :

-   La capture de champs de connexion automatique

-   La capture de champs de connexion manuelle

**Capture de champ de connexion automatique** fonctionne bien avec la plupart des compatible HTML pages de connexion, s’ils utilisent **ID DIV connus pour le nom d’utilisateur hello et un mot de passe d’entrée** champ. Hello que cela fonctionne consiste par frottement hello HTML sur la page de hello toofind ID DIV qui correspondent à certains critères et en enregistrant ensuite que les métadonnées pour cette application afin de nous pouvons relire ultérieurement les mots de passe tooit.

**Capture de champ de connexion manuelle** peut être utilisé dans le cas de hello hello application **n’affecte pas un fournisseur** hello d’entrée des champs utilisés pour la connexion. Capture de champ de connexion manuelle peut également servir dans les cas de hello lorsque hello **fournisseur restitue plusieurs champs** qui ne peut pas être détecté automatiquement. Azure AD peut stocker les données pour que la page, de nombreux champs de hello connexion tant que vous nous dire où ces champs se trouvent sur la page de hello.

En règle générale, **si la capture de champ de connexion automatique ne fonctionne pas, nous suggérons toujours lors de l’option manuelle de hello.**

### <a name="how-tooautomatically-capture-sign-in-fields-for-an-application"></a>Comment tooautomatically capturer les champs de connexion pour une application

tooconfigure **mot de passe Single Sign-on** pour une application en utilisant **capture du champ de connexion automatique**, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

  * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello tooconfigure l’authentification unique.

7.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

8.  Mode de sélection hello **mot de passe de session.**

9.  Entrez hello **URL de connexion**. Il s’agit d’URL de hello où les utilisateurs entrent leur nom d’utilisateur et mot de passe des toosign dans pour. **Assurez-vous que connexion hello dans les champs est visibles à l’URL de hello vous fournissez**.

10. Cliquez sur hello **enregistrer** bouton.

11. Une fois que vous le faire, nous allons capturer automatiquement cette URL pour un nom d’utilisateur et mot de passe zone d’entrée vous permettre de transmettre des toouse Azure AD toosecurely application toothat de mots de passe à l’aide d’extension du navigateur hello accès Panneau de configuration.

## <a name="how-toomanually-capture-sign-in-fields-for-an-application"></a>Comment toomanually capturer les champs de connexion pour une application

toomanually capture champs de connexion, vous devez disposer d’extension de navigateur de panneau d’accès hello installée et **ne pas être en cours d’exécution en mode privé, inPrivate ou incognito.** extension du navigateur tooinstall hello, suivez les étapes hello Bonjour [comment tooinstall hello extension du navigateur de panneau d’accès](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.

tooconfigure **mot de passe Single Sign-on** pour une application en utilisant **capture du champ de connexion manuelle**, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

   * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello tooconfigure l’authentification unique.

7.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

8.  Mode de sélection hello **mot de passe de session.**

9.  Entrez hello **URL de connexion**. Il s’agit d’URL de hello où les utilisateurs entrent leur nom d’utilisateur et mot de passe des toosign dans pour. **Assurez-vous que connexion hello dans les champs est visibles à l’URL de hello vous fournissez**.

10. Cliquez sur hello **enregistrer** bouton.

11. Une fois que vous le faire, nous allons capturer automatiquement cette URL pour un nom d’utilisateur et mot de passe zone d’entrée vous permettre de transmettre des toouse Azure AD toosecurely application toothat de mots de passe à l’aide d’extension du navigateur hello accès Panneau de configuration. En cas de hello que cette opération échoue, vous pouvez **hello mode connexion toouse champ de connexion manuelle capture des modifications** en continuant toostep 12.

12. Cliquez sur **Configurer les paramètres d’authentification unique par mot de passe de** &lt;nom de l’application&gt;.

13. Sélectionnez hello **détecter manuellement les champs de connexion** option de configuration.

14. Cliquez sur **OK**.

15. Cliquez sur **Enregistrer**.

16. Suivez hello sur l’écran des instructions toouse hello panneau d’accès.

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a>Une erreur « Nous n’avons trouvé aucun champ de connexion à cette URL. » s’affiche

Vous obtenez cette erreur en cas d’échec de la détection automatique des champs de connexion. tooresolve les étapes de ce problème, essayez la détection champ de connexion manuelle en suivant les hello Bonjour [comment toomanually capturer les champs de connexion pour une application](#how-to-manually-capture-sign-in-fields-for-an-application) section.

## <a name="i-see-an-unable-toosave-single-sign-on-configuration-error"></a>Je vois une erreur « Impossible de toosave Single Sign-on configuration »

Dans certains cas rares, la mise à jour de la configuration de l’authentification unique de l’hello peut échouer. tooresolve cela réessayez hello seule configuration de l’authentification à nouveau.

Si le problème persiste toofail de manière cohérente, ouvrez une demande de support et fournissent des informations hello collectées Bonjour [comment toosee les détails de hello d’une notification de portail](#i-cannot-manually-detect-sign-in-fields-for-my-application) et [comment tooget aider en envoyant la notification détails tooa ingénieur de support](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a>Impossible de détecter manuellement les champs de connexion de mon application

Vous pouvez voir lorsque détection manuelle ne fonctionne pas de comportements de hello sont les suivantes :

-   processus de capture manuelle de Hello est apparue toowork, mais les champs hello capturées n’étaient pas correctes

-   champs de droite Hello ne sont soulignés lors de l’exécution du processus de capture hello

-   processus de capture Hello me prend page de connexion de l’application toohello comme prévu, mais rien ne se produit

-   Capture manuelle apparaît toowork, mais l’authentification unique ne se produit lorsque mes utilisateurs accèdent toohello application hello panneau d’accès.

Vérifiez les éléments suivants de hello si vous rencontrez l’une de ces problèmes :

-   Assurez-vous d’avoir hello dernière version d’extension du navigateur hello accès panneau **installé** et **activé** en suivant les étapes de hello Bonjour [comment tooinstall hello navigateur de panneau d’accès extension](#how-to-install-the-access-panel-browser-extension) section.

-   Assurez-vous que vous n’essayez pas de processus de capture hello lors de votre navigateur **mode privé, inPrivate ou incognito**. extension de panneau d’accès Hello n’est pas pris en charge dans ces modes.

-   Assurez-vous que vos utilisateurs n’essaient pas de toosign dans l’application toohello à partir du panneau d’accès hello lors de **mode privé, inPrivate ou incognito**. extension de panneau d’accès Hello n’est pas pris en charge dans ces modes.

-   Réessayez le processus de capture manuelle de hello, la vérification des marqueurs de hello rouge sont sur des champs de hello correct.

-   Si le processus de capture manuelle de hello semble toohang ou page de connexion hello ne rien (cas 3 ci-dessus), essayez à nouveau les processus de capture manuelle de hello. Mais, cette fois après avoir effectué le processus hello, appuyez sur hello **F12** bouton tooopen console de développement de votre navigateur. Une fois, il, ouvrez hello **console** et type **window.location= »&lt;entrez hello signe dans l’url que vous avez spécifié lors de la configuration d’application hello&gt;»** , puis appuyez sur  **Entrez**. Cette force une page de redirection qui terminer le processus de capture hello et stocker hello les champs qui ont été capturées.

Si aucune de ces approches ne fonctionne pour vous, nous pouvons vous aider. Ouvrez un cas de prise en charge avec les détails de ce que vous avez essayé de, ainsi que les informations de hello collectées Bonjour hello [comment toosee les détails de hello d’une notification de portail](#i-cannot-manually-detect-sign-in-fields-for-my-application) et [comment tooget aider en envoyant des détails de la notification prise en charge tooa ingénieur](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (le cas échéant).

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Comment tooinstall hello extension du navigateur de panneau d’accès

tooinstall hello extension du navigateur de panneau d’accès, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [volet d’accès](https://myapps.microsoft.com) dans un des navigateurs de hello pris en charge et vous connecter en tant qu’un **utilisateur** dans Azure AD.

2.  Cliquez sur un **application d’authentification unique du mot de passe** Bonjour panneau d’accès.

3.  Dans hello invite vous demandant tooinstall hello logiciel, sélectionnez **installer maintenant**.

4.  En fonction de votre navigateur vous être lien de téléchargement toohello dirigée. **Ajouter** navigateur de tooyour extension hello.

5.  Si votre navigateur vous invite à sélectionner tooeither **activer** ou **autoriser** hello extension.

6.  Une fois l’extension installée, **redémarrez** votre session de navigateur.

7.  Connectez-vous en hello volet d’accès et de voir si vous pouvez **lancer** vos applications SSO de mot de passe.

Vous pouvez également télécharger l’extension de hello pour Chrome et Firefox à partir de liens directs de hello ci-dessous :

-   [Extension du volet d’accès pour Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Extension du volet d’accès pour Firefox](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-toosee-hello-details-of-a-portal-notification"></a>Comment toosee les détails de hello d’une notification de portail

Vous pouvez voir les détails de hello toute notification portail en suivant les étapes de hello ci-dessous :

1.  Cliquez sur hello **Notifications** icône (clochette hello) dans hello coin supérieur droit de hello portail Azure

2.  Sélectionnez une notification dans un **erreur** état (celles avec un toothem suivant rouge ( !)).

  >!NOTE] Vous ne pouvez pas cliquer sur les notifications affichant l’état **Réussi** ou **En cours**.
  >
  >

3.  Cette hello ouvrir **détails de la Notification** panneau.

4.  Utilisez ces informations vous-même toounderstand plus des détails sur le problème de hello.

5.  Si vous avez toujours besoin d’aide, vous pouvez également partager ces informations avec une prise en charge ingénieur ou hello groupe tooget aide produit avec votre problème.

6.  Cliquez sur hello **copie** **icône** toohello à droite de hello **copiez erreur** toocopy de zone de texte tous les hello tooshare détails de notification avec un ingénieur du groupe de produit ou de la prise en charge.

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a>Comment tooget aider en envoyant l’ingénieur du support de notification détails tooa

Il est très important que vous partagez **tous hello détails ci-dessous** avec un ingénieur du support, si vous avez besoin d’aide, afin qu’ils peuvent vous aider à rapidement. Vous pouvez facilement en cela **prendre une capture d’écran,** ou en cliquant sur hello **icône d’erreur de copie**, trouvé toohello Hello **erreur de copie** zone de texte.

## <a name="notification-details-explained"></a>Explication des détails de la notification

Hello ci-dessous explique plus la fonction de chacun des éléments de notification hello et donne des exemples de chacun d’eux.

### <a name="essential-notification-items"></a>Éléments essentiels de la notification

-   **Titre** : hello titre descriptif de la notification de hello

    -   Exemple : **Paramètres de proxy d’application**

-   **Description** – hello description de ce qui s’est produite en raison de l’opération de hello

    -   Exemple : **L’URL interne entrée est déjà utilisée par une autre application**

-   **Id de notification** – id unique de hello de notification de hello

    -   Exemple : **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**

-   **Id de demande client** – id de demande spécifique hello effectuée par votre navigateur

    -   Exemple : **302fd775-3329-4670-a9f3-bea37004f0bc**

-   **Heure UTC de marqueur** – hello horodatage au cours de laquelle hello notification s’est produite, en heure UTC

    -   Exemple : **2017-03-23T19:50:43.7583681Z**

-   **Id de Transaction interne** – hello ID interne, nous pouvons utiliser des erreurs de hello toolook dans nos systèmes

    -   Exemple : **71a2f329-ca29-402f-aa72-bc00a7aca603**

-   **UPN** – utilisateur hello qui a effectué l’opération de hello

    -   Exemple : **tperkins@f128.info**

-   **Id de locataire** – ID unique de hello du client, hello dont hello utilisateur qui a effectué l’opération de hello était membre

    -   Exemple : **7918d4b5-0442-4a97-be2d-36f9f9962ece**

-   **L’Id d’objet utilisateur** – hello ID unique de l’utilisateur hello qui a effectué l’opération de hello

    -   Exemple : **17f84be4-51f8-483a-b533-383791227a99**

### <a name="detailed-notification-items"></a>Éléments détaillés de la notification

-   **Nom d’affichage** – **(peut être vide)** un nom d’affichage plus détaillé pour l’erreur de hello

    -   Exemple *: **Paramètres de proxy d’application**

-   **État** – hello état spécifique de la notification de hello

    -   Exemple *: **Échec**

-   **Id d’objet** – **(peut être vide)** hello ID d’objet sur le hello opération a été effectuée

    -   Exemple : **8e08161d-f2fd-40ad-a34a-a9632d6bb599**

-   **Détails** – hello description détaillée de ce qui s’est produite en raison de l’opération de hello

    -   Exemple : **l’URL interne 'http://bing.com/' n’est pas valide car elle est déjà en cours d’utilisation**

-   **Erreur de copie** – cliquez sur hello **icône de copie** toohello à droite de hello **copiez erreur** toocopy de zone de texte tous les hello tooshare détails de notification avec un ingénieur du groupe de support ou de produit

    -   Exemple : ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```

## <a name="next-steps"></a>Étapes suivantes
[Fournissent des applications de tooyour de l’authentification unique avec le Proxy d’Application](active-directory-application-proxy-sso-using-kcd.md)

