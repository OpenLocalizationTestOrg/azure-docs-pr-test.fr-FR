---
title: "aaaTranslate des liens et Proxy d’application d’URL Azure AD | Documents Microsoft"
description: "Traite des principes de base hello des connecteurs de Proxy d’Application Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7ec2b9fb01617067cf5d676037877bf72c19217b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="redirect-hardcoded-links-for-apps-published-with-azure-ad-application-proxy"></a>Rediriger les liens codés en dur pour les applications publiées avec le Proxy d’application Azure AD

Proxy d’Application Azure AD rend votre toousers de disponible localement les applications qui sont distants ou sur leurs propres appareils. Toutefois, certaines applications, développées avec liens locaux incorporés dans hello HTML. Ces liens ne fonctionnent pas correctement lors de l’application hello est utilisée à distance. Lorsque vous avez plusieurs locaux applications point tooeach autres, vos utilisateurs souhaitent tookeep de liens hello fonctionne lorsqu’ils ne sont pas au bureau de hello. 

toomake moyen Hello meilleures assurer que les liens fonctionnels hello identique à l’intérieur et en dehors de votre réseau d’entreprise sont tooconfigure hello des URL externes de votre toobe applications hello même si leur URL interne. Utilisez [des domaines personnalisés](active-directory-application-proxy-custom-domains.md) tooconfigure votre toohave URL externe, nom de votre domaine d’entreprise au lieu du domaine de proxy application hello par défaut.

Si vous ne pouvez pas utiliser des domaines personnalisés dans votre locataire, fonctionnalité de traduction de lien de hello du Proxy d’Application conserve vos liens de travail quel que soit l’où vos utilisateurs. Lorsque vous avez des applications qui pointent directement des ports ou des points de terminaison toointernal, vous pouvez mapper ces toohello URL interne publié URL de Proxy d’Application externe. Lorsque la traduction de liens est activée et que le Proxy d’application procède à des recherches via des balises HTML, CSS et JavaScript sélectionnées pour les liens internes publiées. Puis hello service Proxy d’Application les traduit afin que vos utilisateurs obtiennent une expérience sans interruption.

>[!NOTE]
>Bonjour fonctionnalité de traduction de lien est pour les clients qui, pour une raison quelconque, ne peut pas utiliser des domaines personnalisés toohave hello mêmes URL internes et externes pour leurs applications. Avant d’activer cette fonctionnalité, consultez si [des domaines personnalisés dans le Proxy d’application Azure AD](active-directory-application-proxy-custom-domains.md) peuvent vous être utiles.
>
>Ou, si l’application hello vous devez tooconfigure avec la traduction de lien est SharePoint, consultez [configurer les mappages des accès de substitution pour SharePoint 2013](https://technet.microsoft.com/library/cc263208.aspx) pour les liens de toomapping une autre approche.

## <a name="how-link-translation-works"></a>Comment fonctionnement la traduction de lien

Après l’authentification, lorsque le serveur de proxy hello passe utilisateur toohello de données l’application hello, le Proxy d’Application analyse application hello pour les liens de codé en dur et les remplace par respectives, publié des URL externes.

Le Proxy d’application part du principe que les applications sont encodées en UTF-8. Si tel n’est pas le cas de hello, spécifier type de codage hello dans un en-tête de réponse http, tel que `Content-Type:text/html;charset=utf-8`.

### <a name="which-links-are-affected"></a>Quels sont les liens qui sont affectés ?

fonctionnalité de traduction de lien de Hello recherche uniquement les liens qui se trouvent dans les balises de code dans le corps de hello d’une application. Le Proxy d’application dispose d’une fonctionnalité distincte pour traduire les URL ou les cookies dans les en-têtes. 

Il existe deux types de liens internes communs dans des applications locales :

- **Les liens internes relatifs** tooa de ce point partagé de ressource dans une structure de fichiers local, comme `/claims/claims.html`. Ces liens fonctionnent automatiquement dans les applications qui sont publiées via le Proxy d’Application et continuer toowork avec ou sans traduction de lien. 
- **Les liens internes sont codées en dur** tooother localement les applications telles que `http://expenses` ou publié les fichiers `http://expenses/logo.jpg`. fonctionnalité de traduction de lien de Hello fonctionne sur les liens internes sont codées en dur et modifie les URL externes toopoint toohello nécessitant des utilisateurs distants toogo via.

### <a name="how-do-apps-link-tooeach-other"></a>Comment les applications lier tooeach autres ?

Traduction de lien est activée pour chaque application, afin que vous contrôlez l’expérience utilisateur hello au niveau de hello par application. Activer traduction de liens pour une application lorsque vous souhaitez que les liens de hello *de* toobe de cette application traduite, pas les liens *à* cette application. 

Par exemple, supposons que vous disposez de trois applications publiées via le Proxy d’Application que tout lien tooeach autres : avantages et les dépenses de voyage. Il existe une quatrième application, Commentaires, qui n’est pas publiée via le Proxy d’application.

Lorsque vous activez la traduction de lien pour l’application des avantages hello, hello liens tooExpenses et déplacement sont redirigés toohello des URL externes pour ces applications, mais hello lien tooFeedback n’est pas redirigée, car il n’existe aucune URL externe. Liens à partir des dépenses et de déplacement ne fonctionnent pas tooBenefits différés, car la traduction de lien n’a pas été activée pour ces deux applications.

![Liens à partir d’applications de tooother avantages lors de la traduction de liens est activée.](./media/application-proxy-link-translation/one_app.png)

### <a name="which-links-arent-translated"></a>Quels sont les liens qui ne sont pas traduits ?

tooimprove performances et sécurité, certains liens ne sont pas traduits :

- Les liens non inclus dans des balises de code. 
- Liens hors de HTML, CSS et JavaScript. 
- Liens internes ouverts à partir d’autres programmes. Les liens envoyés par e-mail ou message instantané ou inclus dans d’autres documents, ne sont pas traduits. les utilisateurs de Hello doivent URL externe de tooknow toogo toohello.

Si vous devez toosupport un de ces deux scénarios, utilisez hello même URL internes et externes au lieu de la traduction de lien.  

## <a name="enable-link-translation"></a>Activer la traduction de lien

Bien démarrer avec la traduction de lien est aussi simple que cliquer sur un bouton :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) en tant qu’administrateur.
2. Accédez trop**Azure Active Directory** > **des applications d’entreprise** > **toutes les applications** > application hello sélectionnez toomanage > **Le proxy d’application**.
3. Activer **traduire les URL dans le corps de l’application** trop**Oui**.

   ![Sélectionnez Oui tootranslate URL dans le corps de l’application](./media/application-proxy-link-translation/select_yes.png).
4. Sélectionnez **enregistrer** tooapply vos modifications.

Désormais, lorsque les utilisateurs accèdent à cette application, proxy de hello recherchera automatiquement les URL internes qui ont été publiés via le Proxy d’Application sur votre client.

## <a name="send-feedback"></a>Envoyer des commentaires

Nous souhaitons votre toomake de l’aide de cette fonctionnalité fonctionne pour toutes vos applications. Nous rechercher des balises plus de 30 en HTML et CSS et que vous envisagez du toosupport de cas de JavaScript. Si vous disposez d’un exemple de liens générés qui ne sont pas en cours de traduction, envoyez un extrait de code trop[commentaires de Proxy d’Application](mailto:aadapfeedback@microsoft.com). 

## <a name="next-steps"></a>Étapes suivantes
[Utiliser des domaines personnalisés avec le Proxy d’Application Azure AD](active-directory-application-proxy-custom-domains.md) toohave hello même URL interne et externe

[Configurer les mappages d’accès alternatifs dans SharePoint 2013](https://technet.microsoft.com/library/cc263208.aspx)
