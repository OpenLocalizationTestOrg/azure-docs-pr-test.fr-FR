tooenable d’inscription de votre application, vous devez toocreate une stratégie d’inscription. Cette stratégie décrit des expériences hello consommateurs traversent pendant l’inscription et un contenu hello de jetons qui hello application reçoit les inscriptions réussies.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Cliquez sur **Stratégies d'inscription**.

Cliquez sur **+ ajouter** haut hello du Panneau de hello.

Hello **nom** détermine le nom de stratégie d’inscription hello utilisée par votre application. Par exemple, entrez **SiUp**.

Cliquez sur **Fournisseurs d’identité** et sélectionnez **Inscription par e-mail**. Si vous le souhaitez, vous pouvez également sélectionner des fournisseurs d'identité sociaux, s'ils sont déjà configurés. Cliquez sur **OK**.

Cliquez sur **Attributs d’inscription**. Vous choisissez ici les attributs que vous souhaitez toocollect consommateur de hello pendant l’inscription. Par exemple, sélectionnez **Pays/région**, **Nom d’affichage** et **Code postal**. Cliquez sur **OK**.

Cliquez sur **Revendications d’application**. Vous choisissez ici les revendications que vous souhaitez renvoyer dans les jetons hello envoyées application tooyour précédent après une expérience d’inscription. Par exemple, sélectionnez **Nom d’affichage**, **Fournisseur d’identité**, **Code postal**, **Nouvel utilisateur** et **ID d’objet de l’utilisateur**.

Cliquez sur **Créer**. stratégie Hello créée apparaît sous la forme **B2C_1_SiUp** (hello **B2C\_1\_**  fragment est automatiquement ajouté) Bonjour **des stratégies d’inscription** panneau.

Ouvrez la stratégie de hello en cliquant sur **B2C_1_SiUp**.

Sélectionnez **Contoso B2C application** Bonjour **Applications** liste déroulante et `https://localhost:44321/` Bonjour **URL de réponse / URI de redirection** liste déroulante.

Cliquez sur **Exécuter maintenant**. Un nouvel onglet de navigateur s’ouvre et vous pouvez exécuter via une expérience de consommateur hello de s’inscrire à votre application.

> [!NOTE]
> Il occupe minute tooa pour la création de stratégies et met à jour tootake effet.
>