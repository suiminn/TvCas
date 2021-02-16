# CAS 処理用 tvcas プラグイン

by Logue, modified by tsukumi

TVTest の CasProcessor プラグインで CAS 処理を呼び出すためのライブラリ。再配布規定に基づき、オリジナルと出力ファイル名その他が異なります。

TVTest 0.9.0 未満では動作確認していません。

言うまでもありませんが、スクランブル解除などといった機能はありません。

## このフォークの変更点

Logue 氏版 TvCas の SPHD.tvcas は、実際にはメタデータを変更し名前を変えただけの B25.tvcas になっており、その結果スカパー！プレミアムサービス (SPHD) では利用できない SPHD.tvcas が生成されてしまっていました。  
そこで、tvcas_attachment_20120915 用の [TVCAS_B25_SPHD.diff.txt](http://www2.wazoku.net/2sen/dtvvup/source/TVCAS_B25_SPHD.diff.txt) を適用し、スカパー！プレミアムサービスで利用できる B1.tvcas を生成できるように変更しました。

私は SPHD の受信環境がないのでテストできていませんが、SPHD の受信環境がある方にテストしてもらったところ動いたとのことなので、おそらく使えるはずです。  
 
B1.tvcas を生成できるようにするにあたり、TVCAS_25/ を TVCAS_B25/ へ移動し、TVCAS_B1/ には TVCAS_B25/ 以下のファイルを前述のパッチを当てた上で追加しています。  
また、便宜的に TVCAS_B1/ 以下のファイルの「TVCAS_B25」の記述やファイル名を全て「TVCAS_B1」へ置換しました。TVCAS_B1.h では B1.tvcas 用のメタデータが定義されています。

これにともないプロジェクト設定も変更し、DebugSPHD/ReleaseSPHD を廃止し、Debug/Release に統一しました。ソリューションのビルド 1 回で B25.tvcas と B1.tvcas の両方が生成されるはずです。TVCAS_B25 プロジェクトは B25.tvcas を、TVCAS_B1 プロジェクトは B1.tvcas を生成します。

スカパー！プレミアムサービス向け tvcas プラグインのファイル名は、B1Decoder などとの統一の観点から SPHD.tvcas から B1.tvcas に変更しました。B25 の名称は [ARIB STD-B25](https://www.arib.or.jp/kikaku/kikaku_hoso/std-b25.html) 標準規格、B1 の名称は [ARIB STD-B1](https://www.arib.or.jp/kikaku/kikaku_hoso/std-b1.html) 標準規格にそれぞれ由来しているものと思われます。

また、tvcas_attachment_20120915 用の [TVCAS_B25.diff.txt](http://www2.wazoku.net/2sen/dtvvup/source/TVCAS_B25.diff.txt) を適用し、BonCasClient を利用できるようにしました。B25.tvcas (TVCAS_B25) 、B1.tvcas (TVCAS_B1) 両方に適用しています。   
このほか、プロジェクトの Visual Studio 2019 へのアップグレードを行いました。

オリジナルの tvcas_attachment_20120915 内の TVCAS_B25.tvcas はこのフォークでの B25.tvcas に対応します。  
EMM ロギング機能（注：コンパイル時に EMMLOG フラグが必要）と、[TVCAS_B25.diff.txt](http://www2.wazoku.net/2sen/dtvvup/source/TVCAS_B25.diff.txt) を適用して BonCasClient 対応を追加したこと以外は TVCAS_B25.tvcas との機能上の差異はありません。

オリジナルの tvcas_attachment_20120915 に [TVCAS_B25_SPHD.diff.txt](http://www2.wazoku.net/2sen/dtvvup/source/TVCAS_B25_SPHD.diff.txt) を適用した TVCAS_B1.tvcas はこのフォークでの B1.tvcas に対応します。  
EMM ロギング機能（注：コンパイル時に EMMLOG フラグが必要）と、[TVCAS_B25.diff.txt](http://www2.wazoku.net/2sen/dtvvup/source/TVCAS_B25.diff.txt) を適用して BonCasClient 対応を追加したこと以外は TVCAS_B1.tvcas との機能上の差異はありません。

## 使用方法

* ビルドしたファイルを TVTest ディレクトリ内に入れて、Plugins ディレクトリ内に [CasProcessor.tvtp](https://github.com/logue/CasProcessor) を設置します。
* TVTest を起動して CasProcessor.tvtp が起動していることを確認したら設定画面を開き、\[TSプロセッサー\] に移動します。
* \[TSプロセッサー\] で CasProcessor を選択し、\[デフォルトモジュール\] から 地デジ・BS・CS110 の場合は B25.tvcas を、スカパー！プレミアムサービスの場合は B1.tvcas を読み込むようにします。
* \[デフォルトデバイス\] で CAS 処理を行いたいデバイスを選びます。
* \[デフォルトフィルター\] で利用する B-CAS カードまたはスカパー！カードを選択します。

## リンク

* [TVTest](https://github.com/DBCTRADO/TVTest)
* [CasProcessor](https://github.com/logue/CasProcessor)

## 謝辞

* [追加ファイル置き場](http://www2.wazoku.net/2sen/dtvvup/)
* [TVTest0.9.0(2014/12/1以降)のビルド方法](http://dtv.air-nifty.com/sphd/2015/03/tvtest-09020141.html)

## 以下オリジナル

>本プログラムは、デジタル放送における CAS 処理の試験又は研究のために公開されています。
>
>以下の条項に同意する場合にのみ利用することができます。
>
>・試験又は研究の目的に限り利用することができます。
>・使用又は使用不能によって生じたいかなる損害も補償しません。
>・正規のカード以外で利用することはできません。
>
>改変する場合、以下の条件に従ってください。
>
>・ファイル名をオリジナルと異なるものにすること。
>・著作権表記を書き換えること。
>・原著作者が一切関わっていないことを明確にすること。
>・正規のカード以外で利用するための改変をしないこと。
>
>
>2012 デジタル放送総合技術研究開発機構