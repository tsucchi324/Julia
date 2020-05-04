# Julia

## 勉強会のメモ

1. Installation ([参考](https://qiita.com/fkm_y/items/cde1f63dd5ff1cb2d051))
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
（いつか対処するかも）

黙って[ホームページ](https://julialang.org/downloads/)から`.dmg`インストールすればいいんだな。

juliaを起動すれば勝手にterminalからjulia内に入れる。

2. Jupyter Notebookとの連携 ([参考](https://github.com/mitmath/6S083/blob/master/installation.md))
```
julia> using Pkg
julia> Pkg.add("IJulia")
julia> using IJulia
julia> notebook()
```
NewからJulia 1.4.1が選択できるのでセットアップ完了。

