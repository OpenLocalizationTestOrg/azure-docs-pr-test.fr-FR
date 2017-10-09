tooenable mot de passe affinées réinitialiser sur votre application, vous devez toocreate une stratégie de réinitialisation de mot de passe. Notez que ce mot de passe à l’échelle du locataire hello réinitialiser l’option spécifiée [ici](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md). Cette stratégie décrit les expériences hello qui parcourt les consommateurs hello lors de la réinitialisation de mot de passe et le contenu hello de jetons qui hello application recevra de réussite.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Dans section de stratégies hello des paramètres, sélectionnez **réinitialise les stratégies de mot de passe** et cliquez sur **+ ajouter**.

![Sélectionner des stratégies d’inscription ou de la connexion et cliquez sur le bouton Ajouter de hello](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

Entrez une stratégie **nom** pour tooreference de votre application. Par exemple, entrez : `SSPR`.

Cliquez sur **Fournisseurs d’identité** et sélectionnez **Réinitialiser le mot de passe à l’aide de l’adresse e-mail**. Cliquez sur **OK**.

![Sélectionnez la réinitialisation de mot de passe à l’aide d’adresse de messagerie en tant que fournisseur d’identité et cliquez sur hello OK](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

Cliquez sur **Revendications de l’application**. Choisissez les revendications à renvoyer dans les jetons d’autorisation hello envoyées arrière tooyour application après la réinitialisation d’un mot de passe réussie expérience. Par exemple, sélectionnez **ID d’objet de l’utilisateur**.

![Sélectionnez des revendications d’application et cliquez sur le bouton OK](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

Cliquez sur **créer** stratégie de hello tooadd. stratégie de Hello est répertorié en tant que **B2C_1_SSPR**. Hello **B2C_1_** préfixe est ajouté toohello nom.

Ouvrez la stratégie de hello en sélectionnant **B2C_1_SSPR**. Vérifiez les paramètres de hello spécifiés dans la table de hello, puis cliquez sur **exécuter maintenant**.

![Sélectionner la stratégie et l’exécuter](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| Paramètre      | Valeur  |
| ------------ | ------ |
| **Applications** | Application de Contoso B2C |
| **Sélectionner l’URL de réponse** | `https://localhost:44316/` |

Un nouvel onglet de navigateur s’ouvre et vous pouvez vérifier l’expérience des utilisateurs dans votre application de réinitialisation de mot de passe hello.

> [!NOTE]
> Il occupe minute tooa pour la création de stratégies et met à jour tootake effet.
>
