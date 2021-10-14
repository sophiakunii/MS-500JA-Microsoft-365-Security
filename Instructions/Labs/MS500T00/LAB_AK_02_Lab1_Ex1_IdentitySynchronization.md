# モジュール 2 - ラボ 1 - 演習 1 - ID 同期向けの組織設定 

あなたは、Adatum Corporation のセキュリティ管理者、Holly Dickson で、仮想化ラボ環境で Microsoft 365 がデプロイされています。このラボでは、Microsoft 365 テナント アカウントとローカルの Active Directory アカウントの間で ID 同期を実装します。

### タスク 1 - UPN サフィックスを構成する

1.	LON-DC1 で **Adatum\Administrator** として、ラボ ホスティング プロバイダーから割り当てられたパスワードを使ってログオンします。
2.	管理者として Windows PowerShell を使い、ドメインの UPN サフィックスを更新します。ドメイン名では “@zzzzzzz.onmicrosoft.com”  (zzzzzzz は一意の UPN 名) を使い、AD DS の各ユーザーで UPN を更新します。これを行うには、以下のコマンドを実行します (必ず zzzzzzz は一意の UPN 名に変更してください):

    	Set-ADForest -identity "adatum.com" -UPNSuffixes @{replace="zzzzzzz.onmicrosoft.com"}  
3.	次に以下のコマンドを入力します (必ず zzzzzzz を一意の UPN 名に変更してください): 

		Get-ADUser –Filter * -Properties SamAccountName | ForEach-Object { Set-ADUser $_ -UserPrincipalName ($_.SamAccountName + "@zzzzzzz.onmicrosoft.com" )}
4.	Windows PowerShell のプロンプトで以下のコマンドを入力してから Enter を押します:

		Set-ExecutionPolicy Unrestricted  
5.	実行ポリシーの変更を確定するには、「すべてにはい」と示唆するために 「**A**」 と入力し、Enter キーを押します。
 
### タスク 2 - ディレクトリ同期を有効にする

1.	ブラウザーを開き、`https://portal.office.com/` に移動します。   
2.	パスワード `Pa55w.rd` を使用し、**holly@M365xZZZZZZ.onmicrosoft.com** としてサインインします。    
3.	「**管理**」 をクリックして Microsoft 365 管理センターに移動します。
4.	**管理者の連絡先情報の更新**について尋ねられたら、「キャンセル」 ボタンをクリックして、この要求をスキップします。  
	**注:** Active Directory 同期が有効になっているという警告が表示されても、この時点では無視しますが、この演習では後ほどディレクトリ同期を実行できなくなります。ディレクトリ同期が有効になるまで待つ必要があります。ただし、警告が表示されても、以下の手順を完了することは可能です。  
5.	左側のナビゲーションで 「**ユーザー**」 アイコンを選択してから 「**アクティブなユーザー**」 を選択します。最上部のメニューで省略記号をクリックし、「**ディレクトリ同期**」 を選択します。   
6.	「**Go to the Download center to get the Azure AD Connect tool**」 をクリックします。   プロンプトで指示されたらダウンロードして実行します。
    
### タスク 3 - Azure AD Connect を実行する

1.	Microsoft Azure Active Directory Connect のセットアップ ウィザードの手順に従います。 
2.	ライセンス条項とプライバシーに関する声明に同意します。
3.	「**簡単設定を使う**」 をクリックします。   
4.	「**Azure AD に接続**」 画面で Office 365 管理者のユーザー名 
**holly@M365xZZZZZZ.onmicrosoft.com** とパスワード `Pa55w.rd` を入力し、「次へ」 をクリックします。   
5.	ポップアップ サイン イン ウィンドウ 「**AD DS に接続**」 画面がある場合は、ドメイン管理者 **Admin@M365xZZZZZZ.onmicrosoft.com** とパスワード `ycYoe＆L20a%%` を入力し、「**次へ**」 を選択します。   
6.	「**AD DS に接続**」 画面でドメイン管理者 **ADATUM\Administrator** とパスワード `Pa55w.rd` を入力して、「**次へ**」 を選択します。
7.	「**Continue without matching all UPN suffixes to verified domains**」 チェックボックスを選択します。Azure AD サインイン構成画面で 「**次へ**」 を選択します。   
8.	「**構成の準備完了**」 画面で 「**構成が完了したら、同期プロセスを開始**」 チェックボックスが選択されていることを確認してから 「**インストール**」 を選択します。   
9.	インストールが完了するのを待ちます (数分かかる可能性があります)。   
10.	「**終了**」 を選択します。   

### タスク 4 - ディレクトリ同期の結果を検証してユーザーにライセンスを付与する 

1.	作成した新しいユーザーを確認するにはブラウザーで Office 365 管理センターを開きます。アドレス バーに `https://portal.office.com` と入力してしてください。  
2.	以下の資格情報を使用し、Holly Dickson としてサインインします。  ユーザー名: **holly@M365xZZZZZZ.onmicrosoft.com**、パスワード: `Pa55w.rd`  
3.	「**アクティブなユーザー**」 に移動します。  
4.	ローカル Active Directory から同期された多くのユーザーが表示されるはずです。  「更新」 ボタンをクリックして、このページのデータを更新する必要があるかもしれません。  「Abbie Parsons」 を選択します。  Abbie は、同期前には AD DS ドメインにのみ含まれていたユーザーです。 
5.	Abbie Parsons の製品ライセンスを以下のように編集します。 
	- Location = United Kingdom
	- Product License = Enterprise Mobility + Security E5
6.	変更を行うには、「**変更の保存**」 をクリックします。ウィンドウを閉じます。

これでローカル ADATUM ユーザーが Office 365 に同期され、同期されたユーザー「Abbie Parsons」にライセンスが付与されました。

# ラボ終了  

 
