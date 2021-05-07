---
layout: post
title: Settings in WPF Digital Gauge control | Syncfusion
description: Learn here all about Settings support in Syncfusion WPF Digital Gauge (SfDigitalGauge) control and more.
platform: wpf
control: SfDigitalGauge
documentation: ug
---

# Settings in WPF Digital Gauge (SfDigitalGauge)

There are some other elements/behavior in SfDigitalGauge also can be customized. 

They are:

* Character Spacing
* Segment Thickness
* RTL (Right to Left) support
* Character Stroke
* Dimmed Brush stroke
* Dimmed Brush opacity

## Character Spacing

The distance between the characters can be set by using the [`CharacterSpacing`](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Gauges.SfDigitalGauge.html#Syncfusion_UI_Xaml_Gauges_SfDigitalGauge_CharactersSpacing) property.

{% tabs %}
{% highlight xaml %}

    <syncfusion:SfDigitalGauge  Value="SYNCFUSION" CharactersSpacing="50"/>

{% endhighlight %}

{% highlight c# %}

    SfDigitalGauge digitalgauge = new SfDigitalGauge();
    digitalgauge.Value = "SYNCFUSION";
    digitalgauge.CharacterSpacing = 50;
    this.Grid.Children.Add(digitalgauge);      

{% endhighlight %}
{% endtabs %}

![Digital Gauge Value with CharacterSpacing](Settings_images/Settings_img1.png)

## Character Stroke

The Stroke of the character can be changed by [`CharacterStroke`](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Gauges.SfDigitalGauge.html#Syncfusion_UI_Xaml_Gauges_SfDigitalGauge_CharacterStroke) property.

{% tabs %}
{% highlight xaml %}

    <syncfusion:SfDigitalGauge  Value="SYNCFUSION"   CharacterType="SegmentFourteen" 
                                CharacterStroke="Blue" />

{% endhighlight %}

{% highlight c# %}

    SfDigitalGauge digitalgauge = new SfDigitalGauge();
    digitalgauge.Value = "SYNCFUSION";
    digitalgauge.CharacterStroke = new SolidColorBrush(Colors.Blue);
    digitalgauge.CharacterType = CharacterType.SegmentFourteen;
    this.Grid.Children.Add(digitalgauge);
    
{% endhighlight %}
{% endtabs %}

![Digital Gauge Value with CharacterStroke](Settings_images/Settings_img2.png)

## Segment Thickness

Using [`SegmentThickness`](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Gauges.SfDigitalGauge.html#Syncfusion_UI_Xaml_Gauges_SfDigitalGauge_SegmentThickness) property, you can adjust the thickness of the segment.

{% tabs %}
{% highlight xaml %}

    <syncfusion:SfDigitalGauge  Value="SYNCFUSION"  CharacterType="SegmentFourteen”  
                                SegmentThickness="5"/>
    
{% endhighlight %}

{% highlight c# %}

    SfDigitalGauge digitalgauge = new SfDigitalGauge();
    digitalgauge.Value = "SYNCFUSION";
    digitalgauge.SegmentThickness = 5;
    digitalgauge.CharacterType = CharacterType.SegmentFourteen;
    this.Grid.Children.Add(digitalgauge);

{% endhighlight %}
{% endtabs %}

![Digital Gauge Value with SegmentThickness](Settings_images/Settings_img3.png)

## RTL (Right to Left) support

The Characters are aligned using [`EnableRTLFormat`](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Gauges.SfDigitalGauge.html#Syncfusion_UI_Xaml_Gauges_SfDigitalGauge_EnableRTLFormat) property. The default value of `EnableRTLFormat` is `false`.

{% tabs %}
{% highlight xaml %}

    <syncfusion:SfDigitalGauge  Value="SYNCFUSION"  CharacterType="SegmentFourteen"   
                                EnableRTLFormat="True" />

{% endhighlight %}

{% highlight c# %}

    SfDigitalGauge digitalgauge = new SfDigitalGauge();
    digitalgauge.Value = "SYNCFUSION";
    digitalgauge.EnableRTLFormat= true;
    digitalgauge.CharacterType = CharacterType.SegmentFourteen;
    this.Grid.Children.Add(digitalgauge);

{% endhighlight %}
{% endtabs %}

![Digital Gauge Value with RTL](Settings_images/Settings_img4.png)

## Dimmed Brush stroke

[`DimmedBrush`](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Gauges.SfDigitalGauge.html#Syncfusion_UI_Xaml_Gauges_SfDigitalGauge_DimmedBrush) property is used to apply brushes to the dimmed segment. This property is used to suit the background of the Digital gauge

{% tabs %}
{% highlight xaml %}

    <syncfusion:SfDigitalGauge  Value="SYNCFUSION" CharacterType="SegmentFourteen"  
                                DimmedBrush="SkyBlue" />

{% endhighlight %}

{% highlight c# %}

    SfDigitalGauge digitalgauge = new SfDigitalGauge();
    digitalgauge.Value = "SYNCFUSION";
    digitalgauge.DimmedBrush = new SolidColorBrush(Colors.SkyBlue);
    digitalgauge.CharacterType = CharacterType.SegmentFourteen;
    this.Grid.Children.Add(digitalgauge);

{% endhighlight %}
{% endtabs %}

![Digital Gauge Value with DimmedBrush](Settings_images/Settings_img5.png)

## Dimmed Brush opacity

[`DimmedBrushOpacity`](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Gauges.SfDigitalGauge.html#Syncfusion_UI_Xaml_Gauges_SfDigitalGauge_DimmedBrushOpacity) property is used to set the opacity of the brushes to the dimmed segment.

{% tabs %}
{% highlight xaml %}

    <syncfusion:SfDigitalGauge  Value="SYNCFUSION" DimmedBrush="Blue"  
                                DimmedBrushOpacity="20" CharacterType="SegmentFourteen" />

{% endhighlight %}

{% highlight c# %}

    SfDigitalGauge digitalgauge = new SfDigitalGauge();
    digitalgauge.Value = "SYNCFUSION";
    digitalgauge.DimmedBrush = new SolidColorBrush(Colors.Blue);
    digitalgauge.CharacterType = CharacterType.SegmentFourteen;
    digitalgauge.DimmedBrushOpacity = 20;
    this.Grid.Children.Add(digitalgauge);

{% endhighlight %}
{% endtabs %}

![Digital Gauge Value with DimmedBrushOpacity](Settings_images/Settings_img6.png)
