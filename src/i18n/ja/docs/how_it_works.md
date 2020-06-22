# 🛠 仕組み

Parcel は**バンドル**のツリーを**アセット**のツリーに変換します。

他の多くのバンドラーは基本的に JavaScript のアセットをベースにして、他のフォーマットのアセットを追跡しています。（たとえば、JS ファイルに文字列としてのインライン化など。）
Parcel はファイルタイプにとらわれず、どんなタイプのアセットでもコンフィギュレーションなしに期待通りの方法で動作します。

Parcel のバンドリングプロセスには 3 つのステップがあります。

### 1. アセットツリーの構築

Parcel は入力として 1 つのエントリーアセットを取ります。エントリーアセットは任意のタイプで、JS ファイル、HTML、CSS、画像などです。特定のファイルタイプを処理するために、Parcel にはさまざまな[アセットタイプ](asset_types.html)が定義されています。アセットの解析、依存関係の抽出がされ、最終的にコンパイルされた形式に変換されます。これによりアセットのツリーが作成されます。

### 2. バンドルツリーの構築

アセットツリーが構築されると、バンドルツリーにアセットが配置されます。エントリーアセット用のバンドルが作成され、動的な`import()`用の子バンドルが作成されます。これによりコード分割が発生します。

兄弟バンドルは、JavaScript から CSS ファイルをインポートした場合など、異なるタイプのアセットがインポートされると作成され、対応する JavaScript の兄弟バンドルに配置されます。

アセットが複数のバンドルで必要とされる場合、そのアセットはバンドルツリー内で最も近い共通の上位の階層まで引き上げられるため、複数回含まれることはありません。

### 3. パッケージング

バンドルツリーが構築された後、各バンドルはファイルタイプ固有の[パッケージャ](packagers.html)によってファイルに書き込まれます。パッケージャは、各アセットのコードをブラウザによってロードされる最終ファイルにまとめます。