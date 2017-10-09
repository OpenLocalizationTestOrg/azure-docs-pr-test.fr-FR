## <a name="prerequisites"></a>Composants requis
Nous pouvons écrire le code de gestion CDN, nous devons toodo certains tooenable préparation notre toointeract code avec hello Azure Resource Manager.  toodo, vous devez :

* Créer un ordinateur ressource groupe toocontain hello profil CDN que nous avons créé dans ce didacticiel
* Configurer l’authentification Azure Active Directory tooprovide pour notre application
* Appliquer des autorisations de groupe de ressources toohello afin que seules les utilisateurs à partir de notre client Azure AD peut interagir avec notre profil CDN

### <a name="creating-hello-resource-group"></a>Création du groupe de ressources hello
1. Ouvrez une session sur hello [Azure Portal](https://portal.azure.com).
2. Cliquez sur hello **nouveau** bouton dans le coin supérieur gauche de hello, puis **gestion**, et **groupe de ressources**.

    ![Création d’un groupe de ressources](./media/cdn-app-dev-prep/cdn-new-rg-1-include.png)
3. Attribuez à votre groupe de ressources le nom *CdnConsoleTutorial*.  Sélectionnez votre abonnement et choisissez un emplacement près de chez vous.  Si vous le souhaitez, vous pouvez cliquer sur hello **toodashboard du code confidentiel** case à cocher toopin hello ressource groupe toohello tableau de bord de portail de hello.  Cela rend plus facile toofind plus tard.  Une fois vos sélections effectuées, cliquez sur **Créer**.

    ![Groupe de ressources d’affectation de noms hello](./media/cdn-app-dev-prep/cdn-new-rg-2-include.png)
4. Une fois le groupe de ressources hello est créé, si vous n’avez pas l’épinglez tooyour le tableau de bord, vous pouvez le trouver en cliquant sur **Parcourir**, puis **groupes de ressources**.  Cliquez sur tooopen de groupe de ressources hello il.  Notez votre **ID d’abonnement**.  Vous en aurez besoin ultérieurement.

    ![Groupe de ressources d’affectation de noms hello](./media/cdn-app-dev-prep/cdn-subscription-id-include.png)

### <a name="creating-hello-azure-ad-application-and-applying-permissions"></a>Création d’application hello Azure AD et appliquer des autorisations
Il existe deux approches de l’authentification avec Azure Active Directory tooapp : des utilisateurs individuels ou un principal de service. Un principal de service est un compte service tooa similaire dans Windows.  Au lieu d’accorder un toointeract d’autorisations utilisateur particulier avec des profils de CDN hello, nous à la place accorder les autorisations hello toohello principal du service.  Les principaux de service s’utilisent généralement pour des processus automatisés et non interactifs.  Bien que ce didacticiel est l’écriture d’une application console interactive, nous allons nous concentrer sur l’approche de hello service principal.

La création d’un principal de service comprend plusieurs étapes, dont la création d’une application Azure Active Directory.  toodo, nous allons trop[suivez ce didacticiel](../articles/resource-group-create-service-principal-portal.md).

> [!IMPORTANT]
> Être toofollow que toutes les étapes hello hello [didacticiel lié](../articles/resource-group-create-service-principal-portal.md).  Il est *primordial* de suivre la procédure à la lettre.  Assurez-vous que toonote votre **ID de locataire**, **nom de domaine client** (généralement un *. onmicrosoft.com* domaine, sauf si vous avez spécifié un domaine personnalisé), **ID client** , et **clé d’authentification client**, comme nous aurez besoin ultérieurement.  Être très prudent tooguard votre **ID client** et **clé d’authentification client**, car ces informations d’identification peuvent être utilisée par tout le monde tooexecute opérations en tant que principal du service hello.
>
> Lorsque vous obtenez l’étape toohello nommé configurer une application mutualisée, sélectionnez **non**.
>
> Si vous obtenez les toohello étape [affecter l’application toorole](../articles/azure-resource-manager/resource-group-create-service-principal-portal.md#assign-application-to-role), groupe de ressources utiliser hello créée précédemment, *CdnConsoleTutorial*, mais au lieu de hello **lecteur** rôle, affecter Hello **collaborateur de profil CDN** rôle.  Après avoir attribué hello d’application hello **collaborateur de profil CDN** rôle sur votre groupe de ressources, retour toothis didacticiel. 
>
>

Une fois que vous avez créé votre hello de service principal et affectés **collaborateur de profil CDN** rôle, hello **utilisateurs** panneau pour votre groupe de ressources doit ressembler toothis similaire.

![Panneau Utilisateurs](./media/cdn-app-dev-prep/cdn-service-principal-include.png)

### <a name="interactive-user-authentication"></a>Authentification interactive des utilisateurs
Si, au lieu d’un principal de service, vous préférez que l’authentification d’utilisateur interactif, processus de hello est très similaire toothat pour un principal de service.  En fait, vous devez toofollow hello la même procédure, mais apporter quelques modifications mineures.

> [!IMPORTANT]
> Procédez comme suit uniquement si vous choisissez l’authentification utilisateur individuel toouse au lieu d’un service principal.
>
>

1. Lors de la création de votre application, au lieu de choisir **Application web**, sélectionnez **Application native**.

    ![Application native](./media/cdn-app-dev-prep/cdn-native-application-include.png)
2. Sur la page suivante de hello, vous serez invité pour un **URI de redirection**.  Hello URI ne sont pas validés, mais rappelez-vous que vous avez entrés.  Vous en aurez besoin ultérieurement.
3. Il n’existe aucun besoin toocreate un **clé d’authentification client**.
4. Au lieu d’affecter un toohello de principal du service **collaborateur de profil CDN** rôle, nous allons tooassign utilisateurs ou groupes individuels.  Dans cet exemple, vous pouvez voir que j’ai attribué *CDN démonstration utilisateur* toohello **collaborateur de profil CDN** rôle.  

    ![Accès d’utilisateurs individuels](./media/cdn-app-dev-prep/cdn-aad-user-include.png)
