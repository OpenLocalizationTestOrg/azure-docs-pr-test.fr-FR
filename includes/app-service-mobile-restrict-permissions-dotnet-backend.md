
Par défaut, les API d’un serveur principal Mobile Apps peuvent être appelées de manière anonyme. Ensuite, vous devez les clients toorestrict tooonly authentifié.  

* **Node.js retour de fin (via hello portail Azure)** :  

    Dans les paramètres Mobile Apps, cliquez sur **Tables faciles**, puis sélectionnez votre table. Cliquez sur **Modifier les autorisations**, sélectionnez **Accès authentifié uniquement** pour toutes les autorisations, puis cliquez sur **Enregistrer**.
* **Serveur principal .NET (C#)** :  

    Dans le projet de serveur hello, accédez trop**contrôleurs** > **TodoItemController.cs**. Ajouter hello `[Authorize]` attribut toohello **TodoItemController** de classe, comme suit. toorestrict accès seules toospecific les méthodes, vous pouvez également appliquer cette méthode de toothose tout attribut au lieu de la classe hello. Publiez de nouveau projet de serveur hello.

        [Authorize]
        public class TodoItemController : TableController<TodoItem>

* **Serveur principal Node.js (via le code Node.js)** :  

    authentification toorequire pour l’accès à la table, ajoutez hello ligne toohello Node.js serveur script suivant :

        table.access = 'authenticated';

    Pour plus d’informations, consultez [Comment : exiger l’authentification pour accès tootables](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-auth). toolearn projet de code de démarrage rapide de hello toodownload à partir de votre site, voir [Comment : téléchargement hello Node.js principal quickstart projet de code à l’aide de Git](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart).
