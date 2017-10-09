[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister votre API web, utilisez les paramètres de hello spécifiés dans la table de hello.

![Exemples de paramètres d’inscription pour les nouvelles API web](./media/active-directory-b2c-register-web-api/b2c-new-web-api-settings.png)

| Paramètre      | Exemple de valeur  | Description                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Nom** | API de Contoso B2C | Entrez un **nom** pour l’application hello qui décrit votre tooconsumers API. | 
| **Inclure une application/API web** | Oui | Sélectionnez **Oui** pour une API web. |
| **Autoriser le flux implicite** | Oui | Choisissez **Oui** si votre application doit utiliser une [connexion OpenID Connect](../articles/active-directory-b2c/active-directory-b2c-reference-oidc.md). |
| **URL de réponse** | `https://localhost:44316/` | Les URL de réponse sont des points de terminaison auxquels Azure AD B2C renvoie les jetons demandés par votre application. Entrez une URL [appropriée](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-web-app-or-api-reply-url) comme **URL de réponse**. Dans cet exemple, votre API web est locale et à l’écoute sur le port 44316. |
| **URI ID d’application** | api | Hello URI ID d’application est l’identificateur hello pour votre API web. Bonjour identificateur complet URI, y compris le domaine de hello est généré pour vous. |

Cliquez sur **créer** tooregister votre application.

Votre application qui vient d’être enregistrée s’affiche dans la liste des applications pour le client de B2C hello hello. Sélectionnez votre API web à partir de la liste de hello. volet de propriétés de l’API de Hello s’affiche.

![Propriétés de l’API Web](./media/active-directory-b2c-register-web-api/b2c-web-api-properties.png)

Notez hello globalement unique **identifiant Client d’Application**. Vous utilisez hello ID dans le code de votre application.
