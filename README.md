# oss
oss简单的图片上传
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
