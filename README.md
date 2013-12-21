#OpenCvSharp
Cross platform wrapper of OpenCV for .NET Framework

OpenCvSharpは、OpenCVを.NET Frameworkから利用するためのクロスプラットフォームで動作するラッパーです。

## Installation
### NuGet
If you use Visual Studio 2012 or later, search 'opencvsharp' on the NuGet Package Manager.
* [x86 package](https://www.nuget.org/packages/OpenCvSharp-x86/) - for 32-bit OS
* [x64 package](https://www.nuget.org/packages/OpenCvSharp-x64/) - for 64-bit OS

### Downloads


## Requirements
* [OpenCV 2.4.5](http://opencv.org/)
* [Visual C++ 2012 Redistributable Package](http://www.microsoft.com/ja-jp/download/details.aspx?id=30679)
* .NET Framework 2.0 or later / Mono
    * OpemCvSharp runs not just on Windows but on Linux, MacOSX, etc.

## Features
* OpenCvSharp wraps more OpenCV's functions than SharperCV and OpenCVDotNet.
* Many classes of OpenCvSharp implement IDisposable. There is no need to manage unsafe resources. 
* OpenCvSharp does not force object-oriented programming style on you. You can also call native-style OpenCV functions.
* OpenCvSharp provides functions for converting from IplImage into Bitmap(GDI+) or WriteableBitmap(WPF).
* OpenCvSharp can work on Mono. It can run on any platform which Mono supports (e.g. Linux and MacOSX). 

-----

* OpenCvSharpはSharperCVやOpenCVDotNetといった他のOpenCVのラッパーよりも多くの関数を実装しています。
* 多くのクラスがIDisposableインターフェイスを実装しているので、ネイティブリソース管理の心配が軽減されます。
* オブジェクト指向な書き方を強制しません。OpenCVのネイティブの関数をそのままの形式で呼べます。
* GDI+やWPFとの相互利用が可能です。OpenCVのIplImageとGDI+のBitmapやWPFのWriteableBitmapとの変換機能があります。
* Monoに対応しています。LinuxやMacOSX等のクロスプラットフォームで動作します。
    　

## Usage
### C-style
```C#
// Edge detection by Canny algorithm
using OpenCvSharp;

class Program 
{
    static void Main() 
    {
        IplImage src = Cv.LoadImage("lenna.png", LoadMode.GrayScale);
        IplImage dst = Cv.CreateImage(new CvSize(src.Width, src.Height), BitDepth.U8, 1);
        Cv.Canny(src, dst, 50, 200);
        Cv.NamedWindow("src image");  
        Cv.ShowImage("src image", src);
        Cv.NamedWindow("dst image");  
        Cv.ShowImage("dst image", dst);
        Cv.WaitKey();
        Cv.DestroyAllWindows();
        Cv.ReleaseImage(src);
        Cv.ReleaseImage(dst);          
    }
}
```

### Wrapper-style

```C#
// Edge detection by Canny algorithm
using OpenCvSharp;

class Program 
{
    static void Main() 
    {
        using (IplImage src = new IplImage("lenna.png", LoadMode.GrayScale))
        using (IplImage dst = new IplImage(src.Size, BitDepth.U8, 1)) 
        {
            src.Canny(dst, 50, 200);
            using (new CvWindow("src image", src)) 
            using (new CvWindow("dst image", dst)) 
            {
                CvWindow.WaitKey();
            }
        }
    }
}
```

For more details, see the xxx page.

