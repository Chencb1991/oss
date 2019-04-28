# oss
oss简单的图片上传

> 单张图片

```

<!DOCTYPE html>
<html>
<script src="http://libs.baidu.com/jquery/2.0.0/jquery.min.js"></script>
<script src="http://gosspublic.alicdn.com/aliyun-oss-sdk-4.4.4.min.js"></script>
<head>
	<title>oss</title>
</head>
<body>
<img id="imgd" src="">
<input type="file" name="" id="file" value="" />
<script type="text/javascript">
	const date = new Date();
	const time = ''+date.getFullYear()+date.getMonth()+'1'+date.getDate();
	const objename = Math.random(0,1).toFixed(4)*10000;
	const storeAs = 'app/'+time+'/'+date.getTime()+objename+'.'+'jpeg';//
	var client = new OSS.Wrapper({
            region: 'oss-cn-hangzhou',
            accessKeyId: '填写keyid',
            accessKeySecret: '填写KeySecret',
            bucket: 'jinqianbao-test'
          });
         
         $("#file").change(function(){
            console.log("change");
            client.multipartUpload(storeAs, this.files[0]).then(function (result) {
                console.log(result.url);
                //result.url是返回图片地址
		$("#imgd").attr('src',result.url); 
              }).catch(function (err) {
                console.log(err);
              });
          });
</script>
</body>
</html>
```

> 多张图片

```
<!DOCTYPE html>
<html>
<script src="http://libs.baidu.com/jquery/2.0.0/jquery.min.js"></script>
<script src="http://gosspublic.alicdn.com/aliyun-oss-sdk-4.4.4.min.js"></script>
<head>
	<title>oss</title>
   <link rel="stylesheet" href="https://g.alicdn.com/de/prismplayer/2.8.1/skins/default/aliplayer-min.css" />
  <script type="text/javascript" charset="utf-8" src="https://g.alicdn.com/de/prismplayer/2.8.1/aliplayer-min.js"></script>
</head>
<body>

<div class="uploadImgBtn" id="uploadImgBtn">
    <input class="uploadImg" type="file" name="file" multiple id="file">
</div>



<script type="text/javascript">
	const date = new Date();
	const time = ''+date.getFullYear()+date.getMonth()+'1'+date.getDate();

	var client = new OSS.Wrapper({
             region: 'oss-cn-hangzhou',
            accessKeyId: '填写keyid',
            accessKeySecret: '填写KeySecret',
            bucket: 'jinqianbao-test'
          });
            
         $(".uploadImg").on('change',function(){
            let dataurl = [];
            for(let i=0;i<this.files.length;i++){
              let storeAs = 'app/'+time+'/'+date.getTime()+ Math.random(0,1).toFixed(4)*10000+'.'+'jpg';//
                client.multipartUpload(storeAs, this.files[i]).then(function (result) {
                console.log('第'+i+'张'+result.url);
                dataurl.push({'imgurl':result.url})
              }).catch(function (err) {
                console.log(err);
              });
              console.log(dataurl);
            }           
          });
</script>

</body>
</html>

```


