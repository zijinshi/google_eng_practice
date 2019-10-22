book.json: 

for 1920 x 1080

    "pdf": {      
        "pageNumbers": true,
        "fontSize": 18,
        "paperSize": "a4",
        "margin": {
            "right": 62,
            "left": 62,
            "top": 36,
            "bottom": 36
        },  
        "headerTemplate": null,
        "footerTemplate": null
    }

for 1366 * 768
    "pdf": {      
        "pageNumbers": true,
        "fontSize": 15,
        "paperSize": "a4",
        "margin": {
            "right": 44,
            "left": 44,
            "top": 26,
            "bottom": 26
        },  
        "headerTemplate": null,
        "footerTemplate": null
    }
    
   生成pdf文件注意事项：
   使用gitbook pdf 命令生成pdf文件时，需要本机安装 calibre，用到ebook-convert.exe。
   在windows 7电脑上，如果安装 calibre 4.2，那么生成的pdf文件比较大，嵌入了很多字体，并且目录（左边的书签）无法正确定位到文档中正确的位置。在calibre的官网上（https://calibre-ebook.com/download_windows64）找到如下文字：If you are using Windows 7 or Vista please, use calibre 3.48, which works with all Windows 7/Vista machines, from here. Simply un-install calibre and install 3.48, doing so will not affect your books/settings。
   于是卸载4.2，安装3.48。再生成pdf文件，文件变小了（没有嵌入太多字体），并且左边的书签可以正确定位到文件中正确的位置。
