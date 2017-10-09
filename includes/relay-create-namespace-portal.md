1. Ouvrez une session sur toohello [portail Azure][Azure portal].
2. Dans le volet de navigation gauche hello du portail de hello, cliquez sur **nouveau**, puis cliquez sur **intégration**, puis cliquez sur **relais**.
3. Bonjour **créer l’espace de noms** boîte de dialogue, entrez un nom d’espace de noms. système de Hello vérifie immédiatement toosee si le nom hello est disponible.
4. Bonjour **abonnement** champ, choisissez un abonnement Azure dans l’espace de noms toocreate hello.
5. Bonjour  **[groupe de ressources](../articles/azure-resource-manager/resource-group-portal.md)**  champ, choisissez un groupe de ressources existant dans le hello espace de noms dynamique, ou créer un nouveau.      
6. Dans **emplacement**, choisissez hello pays ou une région dans laquelle votre espace de noms doit être hébergé.
   
    ![Créer un espace de noms][create-namespace]
7. Cliquez sur **Créer**. système de Hello maintenant crée votre espace de noms et active. Après quelques minutes, hello système configure des ressources pour votre compte.

### <a name="obtain-hello-management-credentials"></a>Obtenir des informations d’identification de gestion hello
1. Dans hello d’espaces de noms, cliquez sur hello nouvellement créée le nom de l’espace de noms.
2. Dans le panneau espace de noms de hello, cliquez sur **les stratégies d’accès partagé**.
3. Bonjour **les stratégies d’accès partagé** panneau, cliquez sur **RootManageSharedAccessKey**.
   
    ![informations de connexion][connection-info]
4. Bonjour **stratégie : RootManageSharedAccessKey** panneau, cliquez sur bouton hello suivant trop**la clé de chaîne – primary connexion**, toocopy hello connexion chaîne tooyour le Presse-papiers pour une utilisation ultérieure. Copiez cette valeur dans le Bloc-notes ou un autre emplacement temporaire.
   
    ![connection-string][connection-string]

5. Étape précédente hello répétition, copier et coller la valeur hello **clé primaire** tooa les emplacement temporaire pour une utilisation ultérieure.  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
