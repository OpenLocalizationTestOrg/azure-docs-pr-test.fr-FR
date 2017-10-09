profil de tooenable modification sur votre application, vous devez toocreate un stratégie de modification du profil. Cette stratégie décrit les expériences hello qui parcourt les consommateurs pendant contenu hello et de modification du profil de jetons application hello recevra de réussite.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Dans section de stratégies hello des paramètres, sélectionnez **modification des stratégies de profil** et cliquez sur **+ ajouter**.

![Sélectionnez les stratégies de modification de profil et cliquez sur le bouton Ajouter de hello](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

Entrez une stratégie **nom** pour tooreference de votre application. Par exemple, entrez : `SiPe`.

Cliquez sur **Fournisseurs d’identité** et sélectionnez **Connexion du compte local**. Si vous le souhaitez, vous pouvez également sélectionner des fournisseurs d'identité sociaux, s'ils sont déjà configurés. Cliquez sur **OK**.

![Sélectionnez la connexion de compte Local comme fournisseur d’identité et cliquez sur hello OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

Cliquez sur **Attributs de profil**. Choisissez le consommateur de hello attributs peut afficher et modifier leur profil. Par exemple, vérifiez **Pays/région**, **Nom d’affichage** et **Code postal**. Cliquez sur **OK**.

![Sélectionnez certains attributs et cliquez sur le bouton de hello OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

Cliquez sur **Revendications de l’application**. Choisissez les revendications à renvoyer dans les jetons d’autorisation hello envoyées application tooyour précédent après une expérience de modification de profil réussie. Par exemple, sélectionnez **Nom d’affichage** et **Code postal**.

![Sélectionnez des revendications d’application et cliquez sur le bouton OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

Cliquez sur **créer** stratégie de hello tooadd. stratégie de Hello est répertorié en tant que **B2C_1_SiPe**. Hello **B2C_1_** préfixe est ajouté toohello nom.

Ouvrez la stratégie de hello en sélectionnant **B2C_1_SiPe**. Vérifiez les paramètres de hello spécifiés dans la table de hello, puis cliquez sur **exécuter maintenant**.

![Sélectionner la stratégie et l’exécuter](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| Paramètre      | Valeur  |
| ------------ | ------ |
| **Applications** | Application de Contoso B2C |
| **Sélectionner l’URL de réponse** | `https://localhost:44316/` |

Un nouvel onglet de navigateur s’ouvre et vous pouvez vérifier le profil de hello édition consommateur tel que configuré.

> [!NOTE]
> Il occupe minute tooa pour la création de stratégies et met à jour tootake effet.
>