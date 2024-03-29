# モジュール 11 - ラボ 1 - 演習 1 - DLP ポリシーを管理する  


Adatum のセキュリティ管理者、Holly Dickson としてのロールで、Microsoft 365 を仮想ラボ環境でデプロイしました。Microsoft 365 パイロット プロジェクトを進めているのですが、次のステップでは Adatum でデータ損失防止 (DLP) ポリシーを実装します。まず、カスタム DLP を作成してから、メール メッセージのアーカイブと機密データが含まれているメールに関連した DLP ポリシーをテストします。 

### タスク 1 - カスタム設定で DLP ポリシーを作成する

この演習では、 セキュリティ/コンプライアンス センターでデータ損失防止ポリシーを作成し、ユーザーが機密データを共有することを防止します。作成する DLP ポリシーでは、ユーザーが米国社会保障番号の含まれたコンテンツを共有できないようにします。

1. まだ、クライアント 1 VM (**LON-CL1**) に **LON-CL1\Admin** アカウントとしてログインし、Microsoft 365 に **Holly Dickson** としてログインしているはずです。 

2. **Microsoft Edge** で、「Office 365 コンプライアンス センター」 タブがまだ開いているはずです。その場合は、それを選択して次の手順に進みます。閉じている場合は、新しいタブで `https://protection.office.com` に移動します。

3. **セキュリティ/コンプライアンス センター**の左側のナビゲーション ペインで 「**データ損失防止**」 を選択してから 「**ポリシー**」 を選択します。

4. 「**ポリシー**」 ウィンドウで 「**+ ポリシーを作成**」 を選択し、新しいデータ損失防止ポリシーを作成するウィザードを起動します。

5. 「**テンプレートの利用またはカスタム ポリシーの作成**」 ページの左側のペインで 「**カスタム**」、真ん中のペインで 「**カスタム ポリシー**」 を選択します。ただし、既定でどちらのオプションもすでに選択されています (そうでない場合は、ここで選択します)。「**次へ**」 を選択します。

6. 「**DLP ポリシーの名前の設定**」 ページで 「**名前**」 フィールドに `Social Security DLP Policy` と入力し、「**説明**」 フィールドには `Protect social security numbers from being shared` と入力します。「**次へ**」 を選択します。

7. 「**ポリシーを適用する場所の選択**」 ページで **Exchange のメール、Teams のチャットとチャネル メッセージ、OneDrive、SharePoint サイト**」 オプションを選択し、「**次へ**」 を選択します。

8. **「ポリシー設定の定義」** で、**「詳細な DLP ルールを作成またはカスタマイズします」** を選択し、「**次へ**」 を選択します。

8. **「詳細な DLP ルールのカスタマイズ」** ページで 「**ルールを作成**」 を選択します。

9. 「**ルールの作成**」 ウィンドウで 「**名前**」 フィールドには `U.S. Social Security Number` と入力します。

10. 「**条件**」 フィールドで 「**条件の追加**」 ドロップダウン フィールドを選択し、ドロップダウン メニューで  「**コンテンツに含まれている**」 を選択します。

11. 「**コンテンツに含まれている**」 フィールドで 「**追加**」 ドロップダウン フィールドを選択し、ドロップダウン メニューで 「**機密情報の種類**」 を選択します。

12. 「**機密情報の種類**」 ウィンドウで、検索フィールドに `social` と入力し、検索結果が表示されるまで待ちます。

13. 検索結果のリストで 「**U.S. Social Security Number (SSN)**」 チェックボックスを選択し、「**追加**」 を選択します。

14. 「**U.S. Social Security Number (SSN)**」 フィールドで「**インスタンス数**」 が 「**1～500**」となるように入力します。

17. 「**条件**」 フィールドで 「**条件の追加**」 ドロップダウン フィールドを選択し、ドロップダウン メニューで  「**コンテンツが Microsoft 365 から共有されている**」 を選択します。

19. 「**コンテンツが Microsoft 365 から共有されている**」 フィールドでドロップダウン矢印を選び、「**組織内の連絡先のみ**」 を選択します。

19. 「**アクション**」 フィールドで 「**処理を追加**」 ドロップダウン フィールドを選択し、ドロップダウン メニューで  「**Microsoft 365 の場所にあるコンテンツへのアクセスを制限またはコンテンツを暗号化する**」を選択します。

20. 「**Microsoft 365 の場所にあるコンテンツへのアクセスを制限またはコンテンツを暗号化する**」フィールドで「**Microsoft 365 の場所にあるコンテンツへのアクセスを制限またはコンテンツを暗号化する**」チェックボックスを選択し、「**すべてのユーザーをブロックします**」を選択します。

21. 「**インシデント レポート**」 フィールドで 「**ルールの一致が発生した場合に管理者にアラートを送信します**」をオンにします。 この構成により、Microsoft DLP がメールに 2 つ以上の米国社会保障番号が含まれていることを検出した場合、メールは配信されず、レポートがグローバル管理者に送信されます。  これらの設定を確定した後、「**保存**」 を選択します。

21. 「**詳細な DLP ルールのカスタマイズ**」 ページで 「**次へ**」 を選択します。

22. 「**テストを行うかポリシーを有効にする**」 ページで 「**すぐに有効にする**」 を選択してから 「**次へ**」 を選択します。

22. 「**ポリシーの確認と作成**」 ページで、設定を修正する必要があれば 「**戻る**」 を選択し、満足できる設定になったら 「**送信**」 を選択します。

これで、組織内で送信または共有されるメールとドキュメントで米国の社会保障番号をスキャンする DLP ポリシーが作成されました。


# 演習 2 に進みます。 
