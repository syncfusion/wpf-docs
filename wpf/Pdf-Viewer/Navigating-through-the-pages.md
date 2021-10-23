---
layout: post
title: Page Navigation in WPF Pdf Viewer control | Syncfusion
description: Learn about Page Navigation support in Syncfusion Essential Studio WPF Pdf Viewer control, its elements and more.
platform: wpf
control: PDF Viewer
documentation: ug
---

# Page Navigation in WPF Pdf Viewer

PDF Viewer allows you to navigate through the pages of the PDF document using the [GotoPage](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PdfViewer.PdfViewerControl.html#Syncfusion_Windows_PdfViewer_PdfViewerControl_GotoPage_System_Int32_) method. The following code example illustrates the navigation to page 2 of the PDF document.

{% tabs %}
{% highlight C# %}

//Initialize PDF Viewer.
PdfViewerControl pdfViewer1 = new PdfViewerControl();

//Load the PDF.
pdfViewer1.Load("Sample.pdf");

//Navigate to page 2
pdfviewer1.GotoPage(2);

{% endhighlight %}

{% highlight vbnet %}

'Initialize PDF Viewer.
Private pdfViewer1 As New PdfViewerControl()

'Load the PDF.
pdfViewer1.Load("Sample.pdf")

'Navigate to page 2
pdfviewer1.GotoPage(2)

{% endhighlight %}
{% endtabs %}

## Navigate to the horizontal and vertical offset
You can now scroll to the given horizontal and vertical offset of the PDF document programmatically using the [ScrollTo](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PdfViewer.PdfViewerControl.html#Syncfusion_Windows_PdfViewer_PdfViewerControl_ScrollTo_System_Double_) method of [PdfViewerControl](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PdfViewer.PdfViewerControl.html). Refer to the following code to scroll the PDF document to the horizontal and vertical offset of 160 and 400 respectively.

N> When the [ZoomTo](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PdfViewer.PdfViewerControl.html#Syncfusion_Windows_PdfViewer_PdfViewerControl_ZoomTo_System_Int32_) method is used along with the [ScrollTo](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PdfViewer.PdfViewerControl.html#Syncfusion_Windows_PdfViewer_PdfViewerControl_ScrollTo_System_Double_System_Double_) method, the zoom operation will be executed first.

{% tabs %}
{% highlight C# %}

//Initialize PDF Viewer.
PdfViewerControl pdfViewerControl = new PdfViewerControl();

//Load the PDF.
pdfViewerControl.Load("Sample.pdf");

//Navigate to the horizontal and vertical offset of 160 and 400 respectively
pdfViewerControl.ScrollTo (160, 400);

{% endhighlight %}

{% highlight vbnet %}

'Initialize PDF Viewer.
Private pdfViewerControl As New PdfViewerControl()

'Load the PDF.
pdfViewerControl.Load("Sample.pdf")

'Navigate to the horizontal and vertical offset of 160 and 400 respectively
pdfViewerControl.ScrollTo (160, 400)

{% endhighlight %}
{% endtabs %}

N> You can refer to our [WPF PDF Viewer](https://www.syncfusion.com/wpf-controls/pdf-viewer) feature tour page for its groundbreaking feature representations. You can also explore our [WPF PDF Viewer example](https://github.com/syncfusion/wpf-demos) to know how to render and configure the pdfviewer.