# web-vr
　webブラウザ経由でVR体験を提供する方法。<br/>
　一般的にはレンタルサーバーなどを用意し、そこに自分が用意したVR体験用のhtmlファイルを置いて、これをwebブラウザからアクセスしてもらうことで利用者にVR体験を提供する。<br/>
  ただし、ここではレンタルサーバーの契約などはせずに、Macを使い、LAN内にWebサーバーを用意し、同じLAN内からOculus Questのwebブラウザ経由でVR体験を提供する方法を紹介する。
 
## VR体験に必要なハードウエア
　VRを体験するためには以下のいずれかのハードウエアが必須となる。
* PCとモニタおよびVRヘッドセット
* Oculus Quest/Quest2

## VR体験に必要なソフトウエア
　VR体験を提供を受ける側は、webブラウザが必要となる。webブラウザはHTML5対応が必須であるが、現状のメジャーなwebブラウザなら対応している。
* HTML5対応ブラウザ

## VR体験を提供するために必要なソフトウエア
　webブラウザ経由でVR体験を提供する側は、サーバー側に以下の追加ソフトウエアが必要となる。
* three.js

　言語はJavasript。
 
## three.js
　HTML5では3Dモデル表示APIとしてWebGLが提供される。このAPIだけで3D表示が可能だが、三角形平面を表示するといった、非常に基礎的な機能のために記述が膨大になる。これを簡素化するために利用する。

[https://threejs.org](https://threejs.org)

　最新ソースはGitHubで公開されているので、クローンして取り出せば良い。

[https://github.com/mrdoob/three.js/](https://github.com/mrdoob/three.js/)

　クローンしたリポジトリ内で最低限必要なのは
 
* build
 
 であり、これに基本的な機能を網羅した
 
* examples/jsm
 
 の2つのフォルダを、WebサーバーのVR体験用のHTMLファイルから読み込める場所に置いて利用する。
 例えばVR体験用の処理を記述したHTMLファイルを
 
* vr.html

　とした場合、vr.html内部では以下のような記述でbuildやexamples/jsmフォルダ内の必要なファイルを読み込むことなる。
 
 ```
 <!DOCTYPE html>
<html lang="en">
	<head>
  ・・・
	</head>
	<body>
		<script type="module">
			import * as THREE from './build/three.module.js';
			import { VRButton } from './examples/jsm/webxr/VRButton.js';
　　  ・・・      
		</script>
	</body>
</html>
 ```
 
 　上述のソースの場合、ファイルの配置は以下のようになる。
  
```
{Webサーバーが公開するフォルダ}/
  vr.html
  build/
  examples/
    jsm/
```
 
 この公開されたフォルダを示すURLが仮に
 
```
https://localhost/
```

とすると、vr.htmlにアクセスするURLは

```
https://localhost/vr.html
```

となる。
