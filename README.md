# onlyofficeFileReviewDemo


OnlyOffice前端示例说明:

示例为静态页面(`fileViewer.html`),可以将静态页面部署到web目录下(tomcat/nginx等),以供预览
  
  
## 需要修改几处 

1）. js地址需要替换为实际部署的地址

``` js
<script type="text/javascript" src="http://10.10.38.44:8089/web-apps/apps/api/documents/api.js"></script>
```

2). 静态页面(`fileViewer.html`)url传参,如:

``` 
http://localhost:8088/onlyOffice/fileViewer.html?fileURL=http://10.10.38.44:8888/api/v1/uploads/73MB20190103221507216.docx&fileType=docx&fileName=73MB.docx
``` 

3). 文件类型`fileType`或`fileName`如果包含中文，路径需要进行url编码,如:


``` js 
const fileName = '73MB20190103221507216.docx';
const fileType = 'docx';
const name = '73MB.docx'
//需要注意: 文件地址不能为localhost/127.0.0.1,可以是局域网地址或公网地址
const path = 'http://10.10.38.44:8888/api/v1/uploads/' + model.fileName;
//判断后缀是否支持,若支持则调用onlyoffice,否则直接调用浏览器打开
if (this.containdeFileType('.doc|.docx|.docm|.dot|.dotx|.dotm|.odt|.fodt|.ott|.rtf|.txt|.html|.htm|.mht|.pdf|.djvu|.fb2|.epub|.xps|.xls|.xlsx|.xlsm|.xlt|.xltx|.xltm|.ods|.fods|.ots|.csv|.pps|.ppsx|.ppsm|.ppt|.pptx|.pptm|.pot|.potx|.potm|.odp|.fodp|.otp', path)){
    const pathx = `http://localhost:8088/onlyOffice/fileViewer.html?fileURL=${path}&fileType=${fileType}&fileName=${name}`;
    //防止文件乱码,将路径进行编码
    window.open(encodeURI(encodeURI(pathx)));
} else{
    window.open(path, '_blank');
}
``` 

onlyoffice更多参数配置请查阅[官方文档](https://api.onlyoffice.com/editors/advanced)

