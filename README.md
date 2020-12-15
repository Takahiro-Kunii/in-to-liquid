# web-vr
　webブラウザ経由でVR体験を提供する方法。<br/>
　レンタルサーバーなどを用意し、そこに自分が用意したVR体験用のhtmlファイルを置いて、これをwebブラウザからアクセスしてもらうことで利用者にVR体験を提供する。<br/>
* LAN内にWebサーバーを用意しても良い。ここではMacを使う方法を例示する。
 
## VR体験に必要なハードウエア
　VRを体験するためには以下のいずれかのハードウエアが必須となる。
* PC[^1]と接続したVRヘッドセット
  * [Oculus Rift](https://www.oculus.com/rift-s/)
  * [Vive](https://www.vive.com/jp/product/#all)
* VRヘッドセット一体型Android端末
  * [Oculus Quest/Quest2](https://www.oculus.com/quest/)

[^1]:ここでいうPCはWindowsマシンを指す。MacとVRヘッドセットを接続することも可能だが、一般的ではない。

## VR体験に必要なソフトウエア
　VR体験を提供を受ける側は、webブラウザが必要となる。webブラウザはHTML5対応が必須であるが、現状のメジャーなwebブラウザなら対応している。
* HTML5対応ブラウザ(Egde, Safari, Chrome, Firefox,...)

## VR体験を提供するために必要なソフトウエア
　webブラウザ経由でVR体験を提供する側は、サーバー側に以下の追加ソフトウエアが必要となる。
* three.js
 
### three.js
　言語はJavasript。<br/>
　HTML5では3Dモデル表示APIとしてWebGLが提供される。このAPIだけで3D表示が可能だが、三角形平面を表示するといった、非常に基礎的な機能のために記述が膨大になる。これを簡素化するために利用する。

[https://threejs.org](https://threejs.org)

　最新ソースはGitHubで公開されているので、クローンして取り出せば良い。

[https://github.com/mrdoob/three.js/](https://github.com/mrdoob/three.js/)

　クローンしたリポジトリの容量は1GB近くになるが、最低限Webサーバー側に必要なのはリポジトリ(three.js)内の2つのフォルダとなる。
 
* build 
* examples/jsm
 
 これらをWebサーバーに置かれたVR体験用HTMLファイルから読み込める場所に置いて利用する。
 例えばVR体験用の処理を記述したHTMLファイルを
 
* vr.html

　とし、buildやexamples/jsmフォルダと共に、{Webサーバーが公開するフォルダ}下に、以下のように配置した場合
```
{Webサーバーが公開するフォルダ}/
  web-vr/
    vr.html
  three.js/
    build/
    examples/
      jsm/
```
　vr.html内部では以下のような記述でbuildやexamples/jsmフォルダ内の必要なファイルを読み込むことなる。
 
 ```
 <!DOCTYPE html>
<html lang="en">
	<head>
  ・・・
	</head>
	<body>
		<script type="module">
			import * as THREE from '../three.js/build/three.module.js';
			import { VRButton } from '../three.js/examples/jsm/webxr/VRButton.js';
　　  ・・・      
		</script>
	</body>
</html>
 ```
 
となる。

https://tetera.sakura.ne.jp/web-vr/vr.html
