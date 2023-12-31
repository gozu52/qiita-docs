<!--
title:   App Engine Studioを使ったPlaybookの統合
tags:    ServiceNow
id:      db00d6016d74868ac78e
private: false
-->
# Playbookの統合 in App Engine Studio

Process Automation Designerで作成したPlaybookをWorkspaceに統合する過程で少し詰まったので備忘録的にまとめていきます。

1. Workspaceの作成
2. Playbookの作成・統合
3. おまけ（何故この記事を用意したのか）

上記３ステップで実際にアプリケーションの作成から統合までの流れを記載します。

前提条件

    必要なアプリケーション
       - App Engine Studio
       - Playbook Experience

    必要な作業
       - App Engine Studio上でアプリケーションの作成

## 1.Workspaceの作成

My App (App Engine Studio) > Experience > Workspace

Name: 自由に設定可能
Description:
URL: Nameに連携して自動入力されるが、個人で設定可能。
Roles: アクセス権限の設定

![PADImageStartScreen.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3630262/a84d8e0d-bb7a-61d9-4efa-54c006b99284.png)
<!-- ![PlaybookStartCreenImage](PADImageStartScreen.png)
 -->

上記画面でContinueするだけで基本的な構成がされたWorkspaceが出来上がります。
Homeや分析機能を効果的に利用するには設定が必要ですが、趣旨と異なるので割愛します。

## 2.Playbookの作成・統合

### Playbookの作成

Playbookの作成はProcess Automation Designer上で可能です。
２箇所からアクセスできます。

    1. App Engine Studioで作成したApplication > Logic and Automation > PAD - Process Creation Wizard Template
    2. Filter Navigator Menu > Process Automation > Process Automation Designer

双方に大きな違いはないので、今回は１のAppEngineのアプリ上のもので作成していきます。

![PADImageCreateNew.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3630262/c82483d9-0137-e66f-eb0c-bbe591daeaea.png)
<!-- ![CreateNewPADImage](PADImageCreateNew.png) -->

こちらの画面でPlaybookの名前、Application Scopeを選択します。
PlaybookのTriggerは次の画面で選択できます。

![PADImageDefineTrigger.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3630262/e14af813-3bf0-7195-1a91-fc6c1edfd7a6.png)
<!-- ![DefinePADTriggerImage](PADImageDefineTrigger.png) -->

Trigger typeだけでなく、該当Tableや詳細の条件も設定できます。

この画面で、ステージとアクティビティを追加していきます。
ActivateでPlaybookの準備が完了します。

![PADImageCompletePlaybook.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3630262/e3928b2f-222c-f0bb-7cb5-1fa1255f0bda.png)
<!-- ![CompletePADImage](PADImageCompletePlaybook.png) -->

### Playbookの統合

PlaybookのActivateが完了したら１で作成したWorkspaceに戻ります。
Workspaceの編集を開くとNavigation Configurationの画面が表示されます。

![PADImageIntegratePAD.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3630262/cfc5f860-5d09-6373-2ab7-03e2097f467a.png)
<!-- ![IntegratePADImage](PADImageIntegratePAD.png) -->

Record pagesからレコードを表示する画面に移動し、左側メニューからRecord detailsに移動し、右側メニューのAdd a playbookから追加します。

![PADImageAddName.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3630262/77ba201e-211d-6f0c-91bf-9b07527b50c4.png)
<!-- ![AddNameImage](PADImageAddName.png) -->

メニューを進むと、Tab nameとPlaybook experienceを設定する画面が表示されます。Tab nameはWorkspaceのPlaybookを表示するためのTabの名前であり、Playbook experienceはカスタムレイアウト用のモジュラーのことを指しています（こちらをカスタムする必要はほとんどなく、公式Docs上にも多く記載されていません。Global Playbook Experienceを選択しておけば基本的に問題なく動作し、新たな空のExperienceを作成して選択しても同じ挙動をします。詳細は私も理解が甘いので割愛させていただきます）。
今回はPlaybook experienceに既存のGlobal Playbook Experienceを選択し、Tab名は任意ものに設定します。

![PADImageRealScreen.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3630262/7379b1cf-3652-19da-b2fb-5cc78a8090ff.png)
<!-- ![RealScreenImage](PADImageRealScreen.png) -->

設定後、１つ以上のレコードを作成後、レコードに移動すると上記のように表示されます。
こちらで統合作業は終了です。

## おまけ（何故この記事を用意したのか）

機能の使い方で充足する方は飛ばして問題ないです。
Utah versionにてPlaybookを初めて統合しようとした際に、Docsを見てもどのように統合するのか、統合に必要なものがどれかがわからずネット上にも統合プロセスを記載した記事が見当たらず、時間をかなり無駄にしてしまいました。
その時に参照したDocsが下記です。
いずれもPlabookの公式Docsですが、UI Builderでの統合やContextual Side Panel、Related Itemsを追加することでPlaybookの統合を行う方法が記載されているのみで、今回紹介した一番簡単と思われる統合方法が記載されていませんでした。
外部サイトやNow Community、Now Support、Youtube上にも見つけられず、App Engineを使用してWorkspaceに統合する際、大きく遠回りする必要ができてしまいます。
その解消として参照していただければ幸いです。

[Playbook][PlaybookDoc]

[Get started with custom layouts][PlaybookCustomLayoutDoc]

[Integrate Playbook with Workspace][IntegratePlaybookWithWOrkspace]

[PlaybookDoc]: <https://docs.servicenow.com/bundle/vancouver-build-workflows/page/administer/workspace/concept/playbook-ui.html>

[PlaybookCustomLayoutDoc]: <https://docs.servicenow.com/bundle/vancouver-build-workflows/page/administer/workspace/task/playbook-get-started-custom-layouts.html>

[IntegratePlaybookWithWOrkspace]: <https://docs.servicenow.com/bundle/vancouver-platform-user-interface/page/administer/workspace/task/integrate-playbook-workspace.html>
