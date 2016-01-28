[vim](#vim) 


<h5 id="vim">vim</h5> 

		gconf-editor       # 配置编辑器
		/etc/vimrc         # 配置文件路径
		vim +24 file       # 打开文件定位到指定行
		vim file1 file2    # 打开多个文件	
		vim -O2 file1 file2    # 垂直分屏
		vim -on file1 file2    # 水平分屏
		sp filename        # 上下分割打开新文件
		vsp filename       # 左右分割打开新文件
		Ctrl+W [操作]      # 多个文件间操作  大写W  # 操作: 关闭当前窗口c  屏幕高度一样=  增加高度+  移动光标所在屏 右l 左h 上k 下j 中h  下一个w  
		:n                 # 编辑下一个文件
		:2n                # 编辑下二个文件
		:N                 # 编辑前一个文件
		:rew               # 回到首文件
		:set nu            # 打开行号
		:set nonu          # 取消行号
		200G               # 跳转到200
		:nohl              # 取消高亮
		:set autoindent    # 设置自动缩进
		:set ff            # 查看文本格式
		:set binary        # 改为unix格式
		ctrl+ U            # 向前翻页
		ctrl+ D            # 向后翻页
		%s/字符1/字符2/g   # 全部替换	
		X                  # 文档加密
	
