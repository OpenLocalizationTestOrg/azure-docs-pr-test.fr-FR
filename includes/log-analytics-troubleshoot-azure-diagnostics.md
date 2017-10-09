### <a name="troubleshoot-azure-diagnostics"></a>Résoudre les problèmes d’Azure Diagnostics

Si vous recevez hello message d’erreur suivant, le fournisseur de ressources Microsoft.insights hello n’est pas enregistrée :

`Failed tooupdate diagnostics for 'resource'. {"code":"Forbidden","message":"Please register hello subscription 'subscription id' with Microsoft.Insights."}`

fournisseur de ressources tooregister hello, effectuer hello Bonjour portail Azure comme suit :

1.  Dans le volet de navigation hello hello gauche, cliquez sur *abonnements*
2.  Sélectionnez l’abonnement hello identifié dans le message d’erreur hello
3.  Cliquez sur *Fournisseurs de ressources*
4.  Recherche hello *Microsoft.insights* fournisseur
5.  Cliquez sur hello *inscrire* lien

![Enregistrez le fournisseur de ressources microsoft.insights](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

Une fois hello *Microsoft.insights* fournisseur de ressources est enregistré, puis réessayez la configuration des diagnostics.


Dans PowerShell, si vous recevez hello après le message d’erreur, vous devez tooupdate votre version de PowerShell :

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

Mettre à jour votre version de PowerShell toohello novembre 2016 (v2.3.0) ou une version plus récente, à l’aide des instructions de hello Bonjour [prise en main des applets de commande Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) l’article.
