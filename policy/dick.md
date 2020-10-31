## 
[MAC driver](https://github.com/adrianmihalko/ch340g-ch34g-ch34x-mac-os-x-driver)


function gdrive_download () {
  CONFIRM=$(wget --quiet --save-cookies /tmp/cookies.txt --keep-session-cookies --no-check-certificate "https://docs.google.com/uc?export=download&id=$1" -O- | sed -rn 's/.*confirm=([0-9A-Za-z_]+).*/\1\n/p')
  wget --load-cookies /tmp/cookies.txt "https://docs.google.com/uc?export=download&confirm=$CONFIRM&id=$1" -O $2
  rm -rf /tmp/cookies.txt
}

gdrive_download 1d_fu0rIJP83nE84XzEoYeYZSXo8ry7-T mon10Sessions.zip
gdrive_download 1pE0GlrH9pCJlgu-KhYnvlbAugGST5N2M mon10SessionsTest.zip
unzip -l mon10Sessions.zip  | head

https://drive.google.com/file/d/1pE0GlrH9pCJlgu-KhYnvlbAugGST5N2M/view?usp=sharing
aws s3 cp ./mon10Sessions.zip s3://open-bot/other/
aws s3 cp ./mon10SessionsTest.zip s3://open-bot/other/

aws s3 cp 表情识别数据.zip s3://dy-ml-data/表情识别数据.zip --region us-east-1 --endpoint-url http://s3-accelerate.amazonaws.com


https://open-bot.s3-accelerate.amazonaws.com/other/mon10Sessions.zip
https://open-bot.s3-accelerate.amazonaws.com/other/mon10SessionsTest.zip



git clone git@github.com:intel-isl/OpenBot.git



cd android/app/
aws s3 cp build/outputs/apk/release/app-release.apk s3://edu-app-release-jp/openbot.apk --region=ap-northeast-1
aws s3api put-object-acl --bucket edu-app-release-jp --key openbot.apk --acl public-read --region=ap-northeast-1



## auto pilot
CameraActivity.onPreviewFrame(final byte[] bytes, final Camera camera)  # Callback for android.hardware.Camera API
    NetworkActivity.processImage() # 处理图片
        CameraActivity.getRgbBytes()
            CameraActivity.imageConverter.run()
                env/ImageUtils.ImageUtils.convertYUV420SPToARGB8888(bytes, previewWidth, previewHeight, rgbBytes)  # convert bytes into rgbBytes


CameraActivity.onImageAvailable(final ImageReader reader)  # Callback for Camera2 API
    NetworkActivity.processImage() # 处理图片
        CameraActivity.getRgbBytes()
            CameraActivity.imageConverter.run()
                env/ImageUtils.ImageUtils.ImageUtils.convertYUV420ToARGB8888(
                  yuvBytes[0],
                  yuvBytes[1],
                  yuvBytes[2],
                  previewWidth,
                  previewHeight,
                  yRowStride,
                  uvRowStride,
                  uvPixelStride,
                  rgbBytes);  # convert bytes into rgbBytes
        rgbFrameBitmap.setPixels(getRgbBytes(), 0, previewWidth, 0, 0, previewWidth, previewHeight)  # rgbFrameBitmap for output log
        final Canvas canvas = new Canvas(croppedBitmap);                                             # this 2 lines of codes will use rgbFrameBitmap to override the croppedBitmap
        canvas.drawBitmap(rgbFrameBitmap, frameToCropTransform, null);                               # this 2 lines of codes will use rgbFrameBitmap to override the croppedBitmap
        final List<Detector.Recognition> results = detector.recognizeImage(croppedBitmap)            #    预测-追踪
        vehicleControl = autoPilot.recognizeImage(croppedBitmap, vehicleIndicator)                   # or 预测-自动驾驶




  

