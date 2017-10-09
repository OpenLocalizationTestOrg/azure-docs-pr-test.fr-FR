## <a name="prepare-for-akv-integration"></a>Préparation pour AKV Integration
toouse Azure Key Vault Integration tooconfigure votre machine virtuelle SQL Server, il existe plusieurs conditions préalables : 

1. [Installation d'Azure Powershell](#install-azure-powershell)
2. [Création d'un Azure Active Directory](#create-an-azure-active-directory)
3. [Création d’un coffre de clés](#create-a-key-vault)

Hello sections suivantes décrivent ces conditions préalables et les informations hello applets de commande PowerShell toocollect toolater exécuter hello.

### <a name="install-azure-powershell"></a>Installation d'Azure PowerShell
Vérifiez que vous avez installé hello la dernière version du SDK de PowerShell Azure. Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs).

### <a name="create-an-azure-active-directory"></a>Création d'un Azure Active Directory
Tout d’abord, vous devez toohave une [Azure Active Directory](https://azure.microsoft.com/trial/get-started-active-directory/) (AAD) dans votre abonnement. Parmi les nombreux avantages, cela vous permet toogrant autorisation tooyour coffre de clés pour certaines applications et les utilisateurs.

Inscrivez ensuite une application auprès d'ADD. Cela vous donnera un compte de Principal du Service qui a accès tooyour coffre de clés dont votre machine virtuelle a besoin. Dans l’article de coffre de clés Azure hello, vous pouvez trouver ces étapes Bonjour [inscrire une application avec Azure Active Directory](../articles/key-vault/key-vault-get-started.md#register) section, ou vous pouvez voir les étapes de hello avec des captures d’écran Bonjour **obtenir une identité pour l’application hello section** de [ce billet de blog](http://blogs.technet.com/b/kv/archive/2015/01/09/azure-key-vault-step-by-step.aspx). Avant d’effectuer ces étapes, notez que vous devez hello toocollect informations au cours de cette inscription est nécessaire ultérieurement, lorsque vous activez Azure Key Vault Integration sur votre VM SQL suivantes.

* Une fois l’application hello est ajoutée, recherche hello **ID CLIENT** sur hello **configurer** onglet.   ![ID de Client Azure Active Directory](./media/virtual-machines-sql-server-akv-prepare/aad-client-id.png)
  
    ID de client Hello est attribué toohello ultérieure **$spName** paramètre (nom Principal de Service) dans tooenable de script PowerShell hello Azure Key Vault Integration. 
* En outre, lors de ces étapes lorsque vous créez votre clé, copier hello la clé secrète pour votre clé comme indiqué dans hello suivant capture d’écran. Cette clé secrète est attribué ultérieure toohello **$spSecret** paramètre (secret Principal du Service) de script PowerShell hello.  
    ![Secret Azure Active Directory](./media/virtual-machines-sql-server-akv-prepare/aad-sp-secret.png)
* Vous devez autoriser cette nouvelle ID toohave messages hello du client les autorisations d’accès suivantes : **chiffrer**, **déchiffrer**, **wrapKey**, **unwrapKey**, **signe**, et **vérifier**. Cette opération s’effectue par hello [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/azure/mt603625.aspx) applet de commande. Pour plus d’informations, consultez [Authorize hello application toouse hello clé ou le secret](../articles/key-vault/key-vault-get-started.md#authorize).

### <a name="create-a-key-vault"></a>Création d’un coffre de clés
Dans toouse Azure Key Vault toostore hello clés de commande que vous allez utiliser pour le chiffrement dans votre machine virtuelle, vous avez besoin d’un coffre de clés tooa accès. Si vous n’avez pas déjà configuré votre coffre de clés, créez-le en suivant les étapes de hello Bonjour [prise en main d’Azure Key Vault](../articles/key-vault/key-vault-get-started.md) rubrique. Avant d’effectuer ces étapes, notez qu’il existe certaines informations que vous devez toocollect au cours de ce qui sont nécessaire ultérieurement lorsque vous activez Azure Key Vault Integration sur votre VM SQL.

Lorsque vous obtenez toohello créer une étape de coffre de clés, hello de Remarque retourné **vaultUri** propriété, qui est l’URL de coffre de clés hello. Dans l’exemple hello fournie dans cette étape, illustrée ci-dessous, nom de coffre de clés hello est ContosoKeyVault, par conséquent, les URL de coffre de clés hello serait https://contosokeyvault.vault.azure.net/.

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

URL de coffre de clés Hello est attribué ultérieure toohello **$akvURL** paramètre hello PowerShell script tooenable Azure Key Vault Integration.

