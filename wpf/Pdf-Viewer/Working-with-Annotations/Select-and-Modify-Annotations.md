---
layout: post
title: Select and Modify annotations in WPF Pdf Viewer control | Syncfusion
description: Learn about Select and Modify annotations programmatically support in WPF Pdf Viewer, its elements and more.
platform: wpf
control: PDF Viewer
documentation: ug
---

# Select and Modify annotations programmatically

## Select an annotation

### Select an annotation with the annotation's name 

PDF Viewer allows the users to select the annotation programmatically using [SelectAnnotation](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PdfViewer.PdfViewerControl.html#Syncfusion_Windows_PdfViewer_PdfViewerControl_SelectAnnotation_System_String_) method. The annotation’s name should pass as a parameter which needs to be selected. This method returns true, if any annotation is found to be selected. Otherwise, it returns false. 

The following code snippet explains how to select ink annotation and similarly, we can implement it for all other annotation.

{% tabs %}
{% highlight C# %}

//Selecting ink annotation with annotation’s name 
private void SelectAnnotation1(object sender, RoutedEventArgs e)
{ 
    bool isSelected = pdfViewer.SelectAnnotation(inkAnnotationName);
}

{% endhighlight %}
{% endtabs %}

### Select an annotation with the annotation's name and page number 

PDF Viewer also allows the users to select the annotation programmatically using [SelectAnnotation](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PdfViewer.PdfViewerControl.html#Syncfusion_Windows_PdfViewer_PdfViewerControl_SelectAnnotation_System_String_System_Int32_) method with page number overload. The annotation’s name and its page number should pass as a parameter which needs to be selected. This method returns true, if any annotation is found to be selected. Otherwise, it returns false. 

N> For better performance, we can use the method [SelectAnnotation](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PdfViewer.PdfViewerControl.html#Syncfusion_Windows_PdfViewer_PdfViewerControl_SelectAnnotation_System_String_System_Int32_) with page number overload.

The following code snippet explains how to select ink annotation with page number overload and similarly, we can implement it for all other annotation.

{% tabs %}
{% highlight C# %}

//Selecting ink annotation with annotation’s name and page number
private void SelectAnnotation(object sender, RoutedEventArgs e)
{ 
    bool isSelected = pdfViewer.SelectAnnotation(inkAnnotationName, 1);
}

{% endhighlight %}
{% endtabs %}

### How to obtain the name of an annotation

Annotation’s name can be obtained either for newly added annotation or the annotation which already exist. In the following sections, the ink annotation was explained brevity and similarly, we can obtain names for all other annotations.

#### Getting annotation’s name while adding annotation
Added annotation’s name can be obtained from respective annotation changed event. The following code snippet explains how to get the annotation’s name while adding the annotation to the document.

{% tabs %}
{% highlight C# %}

//Getting annotation’s name while adding the annotation
private void PdfViewer_InkAnnotationChanged(object sender, InkAnnotationChangedEventArgs e)
{
    if (e.Action == AnnotationChangedAction.Add)
    {
        string inkAnnotationName = e.Name;
    }
}

{% endhighlight %}
{% endtabs %}


#### Getting annotation’s name for existing annotation

The existing annotation’s name can be obtained from [LoadedDocument]( https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PdfViewer.PdfViewerControl.html#Syncfusion_Windows_PdfViewer_PdfViewerControl_LoadedDocument). The following code snippet explains how to get the existing annotation’s name. 

{% tabs %}
{% highlight C# %}
//Getting existing annotation’s name
private void PdfViewer_DocumentLoaded(object sender, EventArgs args)
{
     PdfLoadedDocument loadedDocument = pdfViewer.LoadedDocument;
     PdfPageBase page = loadedDocument.Pages[0];
     string annotationName = page.Annotations[0].Name;
}

{% endhighlight %}
{% endtabs %}

## Modify an annotation

Annotation’s properties can be modified programmatically through `Settings` in respective annotation changed event. 

The following code snippet explains how to modify the selected ink annotation’s properties. Similarly, we can implement for all other annotations.

{% tabs %}
{% highlight C# %}

//Modifying the selected annotation’s properties.
private void PdfViewer_InkAnnotationChanged(object sender, InkAnnotationChangedEventArgs e)
{
    if (e.Action == AnnotationChangedAction.Select)
    {
		PdfViewerInkSettings pdfViewerInkSettings = (e.Settings as PdfViewerInkSettings);
		pdfViewerInkSettings.InkColor = System.Windows.Media.Color.FromArgb(255, 0, 0, 255);
		pdfViewerInkSettings.Opacity = 1f;
		pdfViewerInkSettings.Thickness = 5;
    }
}

{% endhighlight %}
{% endtabs %}
