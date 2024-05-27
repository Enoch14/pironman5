.. _set_up_rpi:

4. Raspberry Piのセットアップ
=====================================

この章では、Raspberry Piへのログイン方法を学びます。画面がある場合は、接続してRaspberry Piのデスクトップを表示してください。

画面がない場合は、リモートでRaspberry Piにログインする必要があります。また、VNC Viewerを使用してRaspberry Piのデスクトップにアクセスすることもできます。

.. note::

    すでにRaspberry Piの操作に慣れている場合、この章をスキップできます。

画面を使ったセットアップ
---------------------------

画面があると、Raspberry Piの作業が簡単になります。

 **必要なコンポーネント** 

* |link_pironman5|
* 電源アダプター
* Micro SDカード
* 画面用電源アダプター
* HDMIケーブル
* 画面
* マウス
* キーボード

手順:

#. Raspberry Pi OSがインストールされたMicro SDカードを |link_pironman5| に挿入します。

#. マウスとキーボードを |link_pironman5| に接続します。

#. HDMIケーブルを使用して、画面を |link_pironman5| のHDMIポートに接続します。画面が電源に接続され、電源が入っていることを確認してください。

#. 電源アダプターを使用して |link_pironman5| に電源を供給します。数秒後にRaspberry Pi OSのデスクトップが画面に表示されるはずです。

    .. image:: img/bookwarm.png
        :align: center

#. ターミナルを開いてコマンドを入力できます。

画面なしでのセットアップ
------------------------------

モニターがない場合は、リモートログインが可能です。

SSHを使用して、Raspberry PiのBashシェルにアクセスできます。BashはデフォルトのLinuxシェルで、さまざまなタスクを実行するためのコマンドラインインターフェースを提供します。

グラフィカルユーザーインターフェース（GUI）を好む場合、リモートデスクトップ機能を使用してファイルや操作を管理することが便利です。

 **必要なコンポーネント** 

* |link_pironman5| 
* 電源アダプター
* Micro SDカード

手順:

#. Raspberry Pi OSがインストールされたMicro SDカードを |link_pironman5| に挿入します。

#. 電源アダプターを使用して |link_pironman5| に電源を供給します。

#. 使用しているオペレーティングシステムに基づく詳細なセットアップチュートリアルについては、以下のセクションを参照してください：

.. toctree::

    remote_macosx
    remote_windows
    remote_linux
    remote_desktop

