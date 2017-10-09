Connectez-vous tooenable sur votre application, vous devez toocreate un signe de stratégie. Cette stratégie décrit les expériences hello qui parcourt les consommateurs pendant la connexion et de contenu hello de jetons qui hello application recevra sur les connexions réussies.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Dans section de stratégies hello des paramètres, sélectionnez **les stratégies d’inscription ou connectez-vous** et cliquez sur **+ ajouter**.

![Sélectionnez des stratégies d’inscription ou de connexion et cliquez sur Ajouter.](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

Entrez une stratégie **nom** pour tooreference de votre application. Par exemple, entrez : `SiUpIn`.

Cliquez sur **Fournisseurs d’identité**, puis sélectionnez **Inscription par e-mail**. Si vous le souhaitez, vous pouvez également sélectionner des fournisseurs d'identité sociaux, s'ils sont déjà configurés. Cliquez sur **OK**.

![Sélectionnez l’inscription de la messagerie comme fournisseur d’identité et cliquez sur hello OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

Sélectionnez **Attributs d’inscription**. Choisissez les attributs souhaités toocollect consommateur de hello pendant l’inscription. Par exemple, vérifiez **Pays/région**, **Nom d’affichage** et **Code postal**. Cliquez sur **OK**.

![Sélectionnez certains attributs et cliquez sur le bouton de hello OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

Cliquez sur **Revendications de l’application**. Choisissez les revendications à renvoyer dans les jetons d’autorisation hello envoyées application tooyour précédent après une expérience d’inscription ou de la connexion. Par exemple, sélectionnez **Nom d’affichage**, **Fournisseur d’identité**, **Code postal**, **Nouvel utilisateur** et **ID d’objet de l’utilisateur**.

![Sélectionnez des revendications d’application et cliquez sur le bouton OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

Cliquez sur **créer** stratégie de hello tooadd. stratégie de Hello est répertorié en tant que **B2C_1_SiUpIn**. Hello **B2C_1_** préfixe est ajouté toohello nom.

Ouvrez la stratégie de hello en sélectionnant **B2C_1_SiUpIn**. Vérifiez les paramètres de hello spécifiés dans la table de hello, puis cliquez sur **exécuter maintenant**.

![Sélectionner la stratégie et l’exécuter](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| Paramètre      | Valeur  |
| ------------ | ------ |
| **Applications** | Application de Contoso B2C |
| **Sélectionner l’URL de réponse** | `https://localhost:44316/` |

Un nouvel onglet de navigateur s’ouvre, et vous pouvez vérifier expérience du consommateur de s’inscrire ou connectez-vous hello tel que configuré.

> [!NOTE]
> Il occupe minute tooa pour la création de stratégies et met à jour tootake effet.
>