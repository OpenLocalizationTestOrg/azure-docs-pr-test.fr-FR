[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister votre application mobile ou native, utiliser les paramètres hello spécifiés dans la table de hello.

![Exemples de paramètres d’inscription pour une nouvelle application mobile ou native](./media/active-directory-b2c-register-mobile-native-app/b2c-new-mobile-native-app-settings.png)

| Paramètre      | Exemple de valeur  | Description                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Nom** | Application de Contoso B2C | Entrez un **nom** pour l’application hello qui décrit votre tooconsumers d’application. |
| **Client natif** | Oui | Sélectionnez **Oui** pour une application mobile ou native. |
| **Obtenir un URI de redirection personnalisé** | `com.onmicrosoft.contoso.appname://redirect/path` | Entrez un URI de redirection avec un schéma personnalisé. Prenez soin de choisir un [URI de redirection approprié](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-native-application-redirect-uri) et de ne pas y inclure de caractères spéciaux tels que des traits de soulignement. |

Cliquez sur **créer** tooregister votre application.

Votre application qui vient d’être enregistrée s’affiche dans la liste des applications pour le client de B2C hello hello. Sélectionnez votre application mobile ou native à partir de la liste de hello. volet de propriétés de l’application Hello s’affiche.

![Propriétés de l’application](./media/active-directory-b2c-register-mobile-native-app/b2c-mobile-native-app-properties.png)

Notez hello globalement unique **identifiant Client d’Application**. Vous utilisez hello ID dans le code de votre application.

Si votre application native appelle une API web sécurisée par Azure AD B2C, procédez comme suit :
   1. Créer un secret d’application en accédant de toohello **clés** lame et en cliquant sur hello **générer une clé** bouton. Prenez note de hello **clé application** valeur. Vous utilisez les valeur hello en tant que secret d’application hello dans le code de votre application.
   2. Cliquez sur **Accès d’API**, cliquez sur **Ajouter**, puis sélectionnez votre API web et les étendues (autorisations).

> [!NOTE]
> Une **Clé secrète d’application** est une information d’identification de sécurité importante, qui doit être correctement sécurisée.
> 
