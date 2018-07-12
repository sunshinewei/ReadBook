#### android 多渠道打包

<pre><code>
build.gradle的配置：
buildTypes {
        release {
            minifyEnabled true
//            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.txt'
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
            debuggable true
            signingConfig signingConfigs.config
            shrinkResources true//去除无用资源
            // 自定义输出配置
            applicationVariants.all { variant ->
                variant.outputs.each { output ->
                    def outputFile = output.outputFile
                    if (outputFile != null && outputFile.name.endsWith('.apk')) {
                        // 输出apk名称为wooyun_v1.0_wandoujia.apk
                        def fileName = "ryhui_v5.0.3_${variant.productFlavors[0].name}.apk"
                        output.outputFile = new File(outputFile.parent, fileName)
                    }
                }
            }

        }
        debug {
            debuggable true
            signingConfig signingConfigs.config
            minifyEnabled false
        }
    }

    productFlavors {
        kuan {}
        xiaomi {}
        qh360 {}
        baidu {}
        wandoujia {}
        Umeng {}
        huawei {}
        yingyongbao {}
        vivo {}
        oppo {}
    }
</code></pre>
在manifest.xml文件中配置：
value="UMENG_CHANNEL_VALUE"