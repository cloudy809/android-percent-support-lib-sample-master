# android-percent-support-lib-sample-master
修改官方23版百分比布局


看例子发现会出现空隙，查看源码最终发现，在像素转换时会丢失1个像素，稍微做了下修改，将源代码抽出单独弄了一个库。

1.主要修改地方
```android
 public void fillLayoutParams(LayoutParams params, int widthHint, int heightHint) {
            this.mPreservedParams.width = params.width;
            this.mPreservedParams.height = params.height;
            if(this.widthPercent >= 0.0F) {
//                params.width = (int)((float)widthHint * this.widthPercent);
                params.width=Math.round((float)widthHint * this.widthPercent);
            }

            if(this.heightPercent >= 0.0F) {
//                params.height = (int)((float)heightHint * this.heightPercent);
                params.height = Math.round((float)heightHint * this.heightPercent);
            }

            if(Log.isLoggable("PercentLayout", 3)) {
                Log.d("PercentLayout", "after fillLayoutParams: (" + params.width + ", " + params.height + ")");
            }

        }
```
2.官方库例子https://github.com/JulienGenoud/android-percent-support-lib-sample
![image](https://github.com/cwenlu/android-percent-support-lib-sample-master/blob/master/screenshots/1.png)
![image](https://github.com/cwenlu/android-percent-support-lib-sample-master/blob/master/screenshots/2.png)
