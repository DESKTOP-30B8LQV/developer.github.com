---
タイトル：新しいウェブフックイベントアクションが来ています
AUTHOR_NAME：davidcelis
---

私たちは、すぐにいくつかの既存のウェブフックイベントのための新しい `action`値を導入開始します。あなたが現在ウェブフックに加入したが、ペイロードの `action`値をチェックしない場合は、この変更がリリースされた後に、誤ってイベントを処理するに終わる可能性があります。あなたのウェブフック処理は、これらの新しい `action`値によって影響されないことを確実にするために、**は** 4月15日、2016年までにあなたのウェブフック処理ロジックを監査する必要があります。

###のGitHubウェブフックアクションの概要

ウェブフックイベントは、複数のアクションを持つことができます。例えば、（https://developer.github.com/v3/activity/events/types/#issuesevent）いくつかの可能なアクションがあります。[`IssuesEvent`]これらは `問題が作成されopened`、`問題がクローズされclosed`、そして問題が誰かに割り当てられている `assigned`が含まれます。歴史的に、我々は1つのアクションだけを持つイベントをウェブフックする新しいアクションを追加していません。 GitHubのの機能セットが成長するにつれてしかし、我々は時折、既存のイベントタイプに新しいアクションを追加することができます。我々はいくつかの時間がかかるし、あなたのアプリケーションが明示的に任意の処理を実行する前にアクションをチェックしていることを確認することをお勧めします。

イベントアクションで作業するとき###何を避けるために、

ここでは `IssuesEvent`を処理しようとしたとき** **動作しません機能の例です。この例では、 `process_closed`方法は、` opened`または `assigned`ではない任意のイベントアクションのために呼び出されます。これは、 `process_closed`メソッドが` closed`アクションだけでなく、 `opened`またはウェブフックに配信されます` assigned`以外のアクションを持つ他のイベントとのイベントに対して呼び出されることを意味します。

`` `ルビー
＃以下は、将来性はありません！
ケースアクション
「開かれた」とき
Process_opened
ときに「割り当てられました」
Process_assigned
ほかに
Process_closed
終わり
```

###新しいイベント・アクションの操作方法

私たちは、あなたが明示的にイベントアクションを確認し、それに従って行動することを示唆しています。この例では、 `closed`アクションは` process_closed`メソッドを呼び出す前に、最初にチェックされています。さらに、未知の行動のために、私たちは何か新しいものが発生したことログインします。

`` `ルビー
＃以下を推奨します
ケースアクション
「開かれた」とき
Process_opened
ときに「割り当てられました」
Process_assigned
時「閉」
Process_closed
ほかに
「GitHubのから、Ooohh新しい何かを！」置きます
終わり
```

また、随時新しいウェブフックイベントタイプを追加することもできます。あなたのウェブフックが "** **すべてのものを私に送信する」ように設定されている場合、あなたのコードはまた、明示的に、我々は上記のアクション・タイプをチェックして行っているのと同様の方法で、イベントタイプをチェックする必要があります。より多くのヒントについては、私たちを見てみましょう。 [best-practices] [integrators best practices guide]

ご質問やご意見がありましたら、お願いします。 [get in touch] [get-in-touch]

[best-practices]: https://developer.github.com/guides/best-practices-for-integrators/
[get-in-touch] ：https://github.com/contact?form =新規+ウェブフック+アクション [subject]