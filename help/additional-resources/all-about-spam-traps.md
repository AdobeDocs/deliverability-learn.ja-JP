---
title: スパムトラップに関するすべて
description: 配信品質を管理する際に、スパムトラップを理解し、識別し、回避する方法を説明します。
topics: Deliverability
doc-type: article
activity: understand
team: ACS
exl-id: 45cdcda0-70e4-47f4-8713-a834500e7881
source-git-commit: d6094cd2ef0a8a7741e7d8aa4db15499fad08f90
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 100%

---

# スパムトラップに関するすべて

[スパムトラップ](/help/metrics/spam-traps.md)は有効なアドレスで、電子メールの送信時にエラーメッセージは表示されません。スパムトラップには、データの衛生処理を行わずにスパムの発信者または送信者を特定するという主な使命があります。

## スパムトラップアドレスを管理するのは誰か

最初のタイプのスパムトラップアドレスは、SpamHaus、Sorbs、SpamCop などの IP およびドメインのブロックリスト会社です。これらの会社は、web サイトやブログ、フォーラムなどの様々なインターネットページに送信されるアドレスの膨大なネットワークを持っており、スパムの発信者がそのアドレスを収集します。

2 つ目のタイプのスパムトラップは、アクティブな古い ISP アドレスに基づいています。これらの ISP には、トラップで再変換された非アクティブなアドレスに基づいて構築された独自のスパムトラップネットワークがあり、ヒットのたびに送信者の IP とドメインの評判に影響を与えます。

## 仕組み

**エンドユーザーのいない電子メールアドレス**：これらのアドレスにはニュースレターや他の種類の通信に登録できるエンドユーザーは存在せず、今後も存在することはありません。

**ユーザーによって破棄された電子メールアドレス**：使用されていない状態が続くと、アドレスは ISP によって無効にされます。この新しいステータスについての通知を送信者に送信するために、バウンスメッセージが送信されます。送信者は、これらのアドレスを強制隔離するか、今後の通信から削除する必要があります。ISP は、「スパムトラップ」に変換されたこれらのアドレスを使用して、不正な慣行に従う送信者を監視します。

## スパムトラップを認識または特定する方法

スパムトラップを特定するのは難しい作業です。これらのアドレスは悪質な送信者の特定に使用されるため、匿名のままである必要があります。ISP のほとんどには、悪質な送信者のヒットを監視するための簡単なシステムがありません。以前の定義によれば、不審なアドレスのセットを特定し、セットを選択する効率をテストすることが可能です。

## データベースがスパムトラップに感染している理由

電子メールアドレスデータベースにスパムトラップが含まれています。これはどうして可能なのでしょうか。2 つの主な理由は、データベース衛生処理の欠如と収集機能障害です。

以下のいくつかのポイントは、プロセスの確認に役立ちます。

* 収集機能障害：
   * メールアドレスの送信元はどこですか。これらのアドレスの収集にはいくつのソースが使用されていますか。ソースを特定できますか。内部／共登録ですか。
   * オプトインシステムは正常に動作していますか。
   * アドレスのドメインとエイリアスを確認しましたか。下の表に従ってください。
* データベースの衛生プロセス：
   * 過去 12 か月間非アクティブなアドレスに関するプロセスは何ですか。
   * ソフトバウンスの強制隔離を「非アクティブなユーザー」として処理していますか。
   * 最後にデータベースの処理を実行し、クリーンアップを試みたのはいつですか。定期的に実行してください。

## 回避対象のエイリアスとドメイン

**エイリアス**

![](../../help/assets/aliases.png)

**ドメイン**

![](../../help/assets/domains.png)
