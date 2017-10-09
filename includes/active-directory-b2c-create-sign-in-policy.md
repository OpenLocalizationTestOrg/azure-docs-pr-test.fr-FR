Connectez-vous tooenable sur votre application, vous devez toocreate un signe de stratégie. Cette stratégie décrit les expériences hello qui parcourt les consommateurs pendant la connexion et de contenu hello de jetons qui hello application recevra sur les connexions réussies.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)] Cliquez sur **Stratégies de connexion**.

Cliquez sur **+ ajouter** haut hello du Panneau de hello.

Hello **nom** détermine le nom de la stratégie d’authentification hello utilisée par votre application. Par exemple, entrez **SiIn**.

Cliquez sur **Fournisseurs d’identité** et sélectionnez **Connexion du compte local**. Si vous le souhaitez, vous pouvez également sélectionner des fournisseurs d'identité sociaux, s'ils sont déjà configurés. Cliquez sur **OK**.

Cliquez sur **Revendications d’application**. Vous choisissez ici les revendications que vous souhaitez renvoyer dans les jetons hello envoyées application tooyour précédent après une expérience de connexion réussie. Par exemple, sélectionnez **Nom d’affichage**, **Fournisseur d’identité**, **Code postal** et **ID d’objet de l’utilisateur**. Cliquez sur **OK**.

Cliquez sur **Créer**. Notez que la stratégie hello venez de créer s’affiche en tant que **B2C_1_SiIn** (hello **B2C\_1\_**  fragment est automatiquement ajouté) Bonjour **stratégies d’authentification**panneau.

Ouvrez la stratégie de hello en cliquant sur **B2C_1_SiIn**.

Sélectionnez **Contoso B2C application** Bonjour **Applications** liste déroulante et `https://localhost:44321/` Bonjour **URL de réponse / URI de redirection** liste déroulante.

Cliquez sur **Exécuter maintenant**. Un nouvel onglet de navigateur s’ouvre et vous pouvez exécuter via une expérience de consommateur hello de se connecter à votre application.

> [!NOTE]
> Il occupe minute tooa pour la création de stratégies et met à jour tootake effet.
>