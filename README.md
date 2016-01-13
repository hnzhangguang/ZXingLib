# ZXingLib

博客地址：http://blog.csdn.net/q4878802/article/details/50440807


#Android二维码扫描、生成
> 现在使用二维码作为信息的载体已经越来越普及，那么二维码的生成以及扫描是如何实现的呢
> google为我们提供了zxing开源库供我们使用

[zxing GitHub源码地址](https://github.com/zxing/zxing)

> But！But！But！仅仅是源码！我第一次看也有点懵。
> 现如今已经有人对其做了封装，用了好多，这个还不错，在我的GitHub

[我的zxing库](https://github.com/kongqw/ZXingLib)

##效果图
###二维码生成

![P1](http://img.blog.csdn.net/20151231115131330)

###二维码扫描
![P2](http://img.blog.csdn.net/20151231115148954)

##使用
###1. 下载libzxing
![P3](http://img.blog.csdn.net/20151231115216041)

###2. 将库导入工程
####1. 将libzxing放入工程
![P4](http://img.blog.csdn.net/20151231115234867)

![P5](http://img.blog.csdn.net/20151231115251873)

####2. 让libzxing“成为一个库”
> 仅仅将libzxing放入工程目录，他只是个文件，想让工程知道它是一个库，要在**settings.gradle**添加如下配置

```
include ':app', ':libzxing'
```

![P6](http://img.blog.csdn.net/20151231115416045)

> 配置完以后，**Sync** 同步下工程


####3. 给工程真正意义上的添加libzxing库

![P7](http://img.blog.csdn.net/20151231115517567)

![P8](http://img.blog.csdn.net/20151231115533438)

> 到此，准备工作就已经就绪啦

###3. 使用
####1. 二维码生成

```
// 生成二维码图片
String text = editText.getText().toString().trim();
if (!TextUtils.isEmpty(text)) {
    Bitmap qrCodeBitmap = EncodingUtils.createQRCode(text, 400, 400,
            checkBox.isChecked() ?
                    BitmapFactory.decodeResource(getResources(), R.mipmap.ic_launcher) : null);
    imageView.setImageBitmap(qrCodeBitmap);
}
```

![P9](http://img.blog.csdn.net/20151231115615106)

####2. 二维码扫描
#####1. 打开扫描页面
> 安卓6.0以后，需要动态获取权限，不然会报错，可以参考之前的博客

[Android6.0动态获取权限](http://blog.csdn.net/q4878802/article/details/50419004)

```
//打开扫描界面扫描条形码或二维码
Intent openCameraIntent = new Intent(MainActivity.this, CaptureActivity.class);
startActivityForResult(openCameraIntent, 0);
```

#####2. 扫描成功后的回掉

```
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (resultCode == RESULT_OK) {
        Bundle bundle = data.getExtras();
        String scanResult = bundle.getString("result");
        Toast.makeText(MainActivity.this, scanResult, Toast.LENGTH_SHORT).show();
    }
}
```

![P](http://img.blog.csdn.net/20151231115808552)
