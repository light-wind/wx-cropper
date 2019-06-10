# wx-cropper
通用微信小程序图片裁剪组件，简单易用，帮助快速开发图片裁剪功能，支持自定义约束宽高，适用于头像或其他需要特定长宽比图片的场景。
# 裁剪效果预览图
![image](https://github.com/light-wind/wx-cropper/blob/master/screenshot.gif)

# 用法
下载源码，pages/cropper/目录拷贝到项目中。
## 1、在json文件中添加cropper组件
```
{
  "usingComponents": {
    "cropper":"/pages/cropper/cropper"
  },
  "disableScroll": true
}
```

## 2、wxml页面文件中
```
<view class='body'>

  <cropper id='cropper' class='stage'></cropper>
  
  <view class='bar'>
    <view class='btn btn-cancel ripple' bindtap='fnCancel'>取消</view>
    <view class='btn btn-submit ripple' bindtap='fnSubmit'>确定</view>
  </view>

</view>
```

## 3、在onLoad中初始化组件
```
    cropper = this.selectComponent('#cropper');
    cropper.fnInit({
      imagePath:'/assets/test.jpg',       //*必填
      debug: true,                        //可选。是否启用调试，默认值为false。true：打印过程日志；false：关闭过程日志
      outputFileType: 'jpg',              //可选。目标文件的类型。默认值为jpg，jpg：输出jpg格式图片；png：输出png格式图片
      quality: 1,                         //可选。图片的质量。默认值为1，即最高质量。目前仅对 jpg 有效。取值范围为 (0, 1]，不在范围内时当作 1.0 处理。
      aspectRatio: 1.25,                  //可选。裁剪的宽高比，默认null，即不限制剪裁宽高比。aspectRatio需大于0
      minBoxWidthRatio: 0.2,              //可选。最小剪裁尺寸与原图尺寸的比率，默认0.15，即宽度最小剪裁到原图的0.15宽。
      minBoxHeightRatio: 0.2,             //可选。同minBoxWidthRatio，当设置aspectRatio时，minBoxHeight值设置无效。minBoxHeight值由minBoxWidth 和 aspectRatio自动计算得到。
      initialBoxWidthRatio: 0.6,          //可选。剪裁框初始大小比率。默认值0.6，即剪裁框默认宽度为图片宽度的0.6倍。
      initialBoxHeightRatio: 0.6          //可选。同initialBoxWidthRatio，当设置aspectRatio时，initialBoxHeightRatio值设置无效。initialBoxHeightRatio值由initialBoxWidthRatio 和 aspectRatio自动计算得到。
      });
```

## 4、在点击事件中裁剪图片，获取裁剪后的图片路径
```
    cropper.fnCrop({
      //裁剪成功的回调
      success:function(res){
        console.log(res)
         //生成文件的临时路径
        console.log(res.tempFilePath);
        wx.previewImage({
          urls: [res.tempFilePath],
        })
      },
      //裁剪失败的回调
      fail:function(res){
        console.log(res);
      },
      //裁剪结束的回调
      complete:function(){
        //complete
      }
    });
```
