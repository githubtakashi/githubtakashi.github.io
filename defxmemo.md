# defxの設定メモ

defxの設定についてのメモ

- Nerd Fontをインストールすることでフォルダなどにアイコンが使えるようになる。

- windowsの場合はchocoでNerd Fontをインストールが楽。

- windows terminalの設定ファイルのfontにフォント名を指定するとフォントが適用される。

- 画面の左側にファイルをツリー表示する使い方のときはvimrcファイルに書くキーマッピングのopenをdropに変更する。

<br />

```
" Defx
" Defx起動時のレイアウト含む設定
call defx#custom#option('_', {
      \ 'winwidth': 40,
      \ 'split': 'vertical',
      \ 'direction': 'topleft',
      \ 'show_ignored_files': 1,
      \ 'buffer_name': 'exlorer',
      \ 'toggle': 1,
      \ 'resume': 1,
      \ })
let g:python3_host_prog = 'C:\Python39\Pythonw.exe'

" キーマッピング
	autocmd FileType defx call s:defx_my_settings()
	function! s:defx_my_settings() abort
	  " Define mappings
	  nnoremap <silent><buffer><expr> <CR>
	  \ defx#do_action('drop')
	  nnoremap <silent><buffer><expr> c
	  \ defx#do_action('copy')
	  nnoremap <silent><buffer><expr> m
	  \ defx#do_action('move')
	  nnoremap <silent><buffer><expr> p
	  \ defx#do_action('paste')
	  nnoremap <silent><buffer><expr> l
	  \ defx#do_action('drop')
	  nnoremap <silent><buffer><expr> E
	  \ defx#do_action('drop', 'vsplit')
	  nnoremap <silent><buffer><expr> P
	  \ defx#do_action('preview')
	  nnoremap <silent><buffer><expr> o
	  \ defx#do_action('open_tree', 'toggle')
	  nnoremap <silent><buffer><expr> K
	  \ defx#do_action('new_directory')
	  nnoremap <silent><buffer><expr> N
	  \ defx#do_action('new_file')
	  nnoremap <silent><buffer><expr> M
	  \ defx#do_action('new_multiple_files')
	  nnoremap <silent><buffer><expr> C
	  \ defx#do_action('toggle_columns',
	  \                'mark:indent:icon:filename:type:size:time')
	  nnoremap <silent><buffer><expr> S
	  \ defx#do_action('toggle_sort', 'time')
	  nnoremap <silent><buffer><expr> d
	  \ defx#do_action('remove')
	  nnoremap <silent><buffer><expr> r
	  \ defx#do_action('rename')
	  nnoremap <silent><buffer><expr> !
	  \ defx#do_action('execute_command')
	  nnoremap <silent><buffer><expr> x
	  \ defx#do_action('execute_system')
	  nnoremap <silent><buffer><expr> yy
	  \ defx#do_action('yank_path')
	  nnoremap <silent><buffer><expr> .
	  \ defx#do_action('toggle_ignored_files')
	  nnoremap <silent><buffer><expr> ;
	  \ defx#do_action('repeat')
	  nnoremap <silent><buffer><expr> h
	  \ defx#do_action('cd', ['..'])
	  nnoremap <silent><buffer><expr> ~
	  \ defx#do_action('cd')
	  nnoremap <silent><buffer><expr> q
	  \ defx#do_action('quit')
	  nnoremap <silent><buffer><expr> <Space>
	  \ defx#do_action('toggle_select') . 'j'
	  nnoremap <silent><buffer><expr> *
	  \ defx#do_action('toggle_select_all')
	  nnoremap <silent><buffer><expr> j
	  \ line('.') == line('$') ? 'gg' : 'j'
	  nnoremap <silent><buffer><expr> k
	  \ line('.') == 1 ? 'G' : 'k'
	  nnoremap <silent><buffer><expr> <C-l>
	  \ defx#do_action('redraw')
	  nnoremap <silent><buffer><expr> <C-g>
	  \ defx#do_action('print')
	  nnoremap <silent><buffer><expr> cd
	  \ defx#do_action('change_vim_cwd')
	endfunction
```
<br />

| option名 | 意味 |
| -- | -- |
| winwidth | エクスプローラーの表示幅 |
| split | defxウィンドウの分割表示の型式 |
| direction | エクスプローラの位置、topleft か botright |
| show_ignored_files | dotfileを表示するかどうか、1でtrue |
| buffer_name | defx起動時のバッファの名前を付けれる |
| toggle | 1にすると:DefxコマンドでDefxを開くだけでなく閉じることもできる |
| resume | 1にするとdefxを閉じてまた開いても閉じる前の状態でdefxを起動できる |

<br />

表示はこんな感じになります。

![defx](https://user-images.githubusercontent.com/43819429/141695905-cd4fdeb1-752b-4f82-b0ea-5f1b379ea478.png)



