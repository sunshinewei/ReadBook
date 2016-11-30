##density
##scaledDensity
##减少Bitmap的使用：
~对于jpg和png两种图片来说，jpg会比png小一些一般，因为·jpg是一种有损压缩的图片存储格式，而png是一种无损压缩的图片格式。但是jpg没有alpha通道。~
1.使用SampleSize:对于图片资源本身太大，对图片进行压缩。
使用 BitmapFactory.Options options= new BitmapFactory.Options();加载图片，选择自己要压缩的大小。
2.合理选择Bitmap的像素格式：
~ARGB8888，ARGB4444,ARGB565~
3.使用矩阵
~对于Bitmap来说，Bitmap就是像素点阵，就是矩阵，如何使用，可以说~**大图小用用采样，小图大用用矩阵。**
4.索引位图
~每个像素只占1byte,同时支持RGB和alpha,但官方不支持。所以在xml文件中不能配置，也不可以当画布。~
try {
   BitmapFactory.Options options = new Options();
   options.inPreferredConfig = Config.RGB_565;
Bitmap bitmap = BitmapFactory.decodeStream(getResources().getAssets().open("index.png"), null, options);
   Log.d(TAG, "bitmap.getConfig() = " + bitmap.getConfig());
   Log.d(TAG, "scaled bitmap.getByteCount() = " + bitmap.getByteCount());
   imageView.setImageBitmap(bitmap);
} catch (IOException e) {
    e.printStackTrace();
}

