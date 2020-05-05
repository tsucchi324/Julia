# Julia

## 勉強会のメモ

### 1. Installation ([参考](https://qiita.com/fkm_y/items/cde1f63dd5ff1cb2d051))
```
$ brew update
$ brew tap staticfloat/julia
$ brew install julia
###$ julia
```
めっちゃコンパイルに時間かかるくせにエラー出た。。。
```
In file included from ../src/debug.cpp:15:
../include/__hash_table:1132:43: error: exception specification in declaration does not match previous declaration
__hash_table<_Tp, _Hash, _Equal, _Alloc>::__hash_table()
```
（いつか対処するかも…xcodeを入れ直してもダメ）

黙って[ホームページ](https://julialang.org/downloads/)から`.dmg`インストールすればいいんだな。

juliaを起動すれば勝手にterminalからjulia内に入れる。

### 2. Jupyter notebookとの連携 ([参考](https://github.com/mitmath/6S083/blob/master/installation.md))
```
julia> using Pkg
julia> Pkg.add("IJulia")
julia> using IJulia
julia> notebook()
```
NewからJulia 1.4.1が選択できるのでセットアップ完了。以下は追加のセットアップ。
```
julia> Pkg.add("WebIO")
julia> using WebIO
julia> WebIO.install_jupyter_nbextension()
```
  
### 3. Jupyter Labとの連携([参考](https://qiita.com/kirikei/items/a1639954ce5ccaf7ac3c))

Jupyter notebookは開発が一旦止められていて，JupyterLabに移行予定とのことだったので，JupyterLabとも連携したよ。  
JupyterLabはanacondaとセットで入ってるらしく，自分も`jupyter lab`で起動できた。以下は追加のセットアップ。
```
julia> WebIO.install_jupyter_labextension()
```
上手く行かないんだが…(nbextensionと共存しない可能性？)
```
An error occured.
ValueError: 
"@webio/jupyter-lab-provider@0.8.13" is not compatible with the current JupyterLab
Conflicting Dependencies:
JupyterLab              Extension      Package
>=2.1.1 <2.2.0          >=1.0.1 <2.0.0 @jupyterlab/application
>=2.1.1 <2.2.0          >=1.0.1 <2.0.0 @jupyterlab/docmanager
>=2.1.1 <2.2.0          >=1.0.1 <2.0.0 @jupyterlab/notebook
>=2.1.0 <2.2.0          >=1.0.1 <2.0.0 @jupyterlab/rendermime
>=5.1.0 <5.2.0          >=4.0.1 <5.0.0 @jupyterlab/services
```
以下を実行したら上手くいったかも。
```
$ conda install -c conda-forge jupyterlab
julia> using Pkg
julia> Pkg.add("WebIO")
julia> using WebIO, IJulia
julia> WebIO.install_jupyter_labextension(force_conda_jupyter=true)
```
よくわからん。。（このせいで環境ぶっ壊した可能性あり）

【追記】  
昨日までjupyter notebook上でJuliaを動かせてたのにsetupをいじってたらKernel Errorが出るようになってしまった。  
conda, pip, pip3.8が共存してるのホント良くないっぽい。（→後日どうにかするかも。とりあえず動かせる必要があるのでDockerで構築）

### 4. Dockerで環境構築([参考](https://qiita.com/yoshikiri/items/683722701b57fa77aec1))

```
$ docker pull jupyter/datascience-notebook
$ docker run -p 8888:8888 -v ~/Desktop/Julia:/home/jovyan/work --user root --name mynotebook jupyter/datascience-notebook
$ docker start mynotebook
```
表示されたリンクをコピペすればok。  
簡単やん〜
