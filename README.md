# CPP_HTTP_GET_AND_POST
c++ Socket实现的http get和post请求

post分为普通post和post携带文件信息，其实普通post也可以直接发送GetFileContext读出来的16进制文件流过去，不过服务器那边的处理不同，(django为例)不能从request.FILES.get(x)获取，而直接从body，用request.body获取流，然后写入文件

django的处理：   
          
     if request.method == "POST":  # 请求方法为POST时，进行处理
     # myFile = request.body    位置处替换
     # destination.write(myFile)
        myFile = request.FILES.get("myfile", None)  # 获取上传的文件，如果没有文件，则默认为None
        if not myFile:
            return HttpResponse("no files for upload!")
        destination = open(os.path.join("F:\\upload", myFile.name), 'wb+')  # 打开特定的文件进行二进制的写操作
        for chunk in myFile.chunks():  # 分块写入文件
            destination.write(chunk)
        destination.close()
