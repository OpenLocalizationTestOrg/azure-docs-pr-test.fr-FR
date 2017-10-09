[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister votre application web, utiliser les paramètres hello spécifiés dans la table de hello.

![Exemples de paramètres d’inscription pour les nouvelles applications web](./media/active-directory-b2c-register-web-app/b2c-new-app-settings.png)

| Paramètre      | Exemple de valeur  | Description                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Nom** | Application de Contoso B2C | Entrez un **nom** pour l’application hello qui décrit votre tooconsumers d’application. | 
| **Inclure une application/API web** | Oui | Sélectionnez **Oui** pour une application web. |
| **Autoriser le flux implicite** | Oui | Choisissez **Oui** si votre application doit utiliser une [connexion OpenID Connect](../articles/active-directory-b2c/active-directory-b2c-reference-oidc.md). |
| **URL de réponse** | `https://localhost:44316` | Les URL de réponse sont des points de terminaison auxquels Azure AD B2C renvoie les jetons demandés par votre application. Entrez une URL [appropriée](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-web-app-or-api-reply-url) comme **URL de réponse**. Dans cet exemple, votre application web est locale et à l’écoute sur le port 44316. |

Cliquez sur **créer** tooregister votre application.

Votre application qui vient d’être enregistrée s’affiche dans la liste des applications pour le client de B2C hello hello. Sélectionnez votre application web à partir de la liste de hello. volet des propriétés de l’application Hello web s’affiche.

![Propriétés de l’application web](./media/active-directory-b2c-register-web-app/b2c-web-app-properties.png)

Notez hello globalement unique **identifiant Client d’Application**. Vous utilisez hello ID dans le code de votre application.
