---
layout: post
title: Header in WPF Scheduler control | Syncfusion
description: Learn here all about Header support in Syncfusion WPF Scheduler (SfScheduler) control, its elements and more.
platform: wpf
control: SfScheduler
documentation: ug
---

# Header in WPF Scheduler (SfScheduler)
Change the header height, date format and appearance of [SfScheduler](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Scheduler.SfScheduler.html).

## Header height
Change the scheduler header height by using [HeaderHeight](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Scheduler.SfScheduler.html#Syncfusion_UI_Xaml_Scheduler_SfScheduler_HeaderHeight) property of SfScheduler. By default, the header height is 50.

{% tabs %}
{% highlight xaml %}
<syncfusion:SfScheduler x:Name="Schedule"
                        HeaderHeight="100" >
</syncfusion:SfScheduler>
{% endhighlight %}
{% highlight c#%}
this.Schedule.HeaderHeight = 100;
{% endhighlight %}
{% endtabs %}

![WPF Scheduler header ViewHeaderHeight](Header_Images/HeaderHeight.png)

## Header date format
Change the Scheduler header date format of scheduler by using the  [HeaderDateFormat](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Scheduler.SfScheduler.html#Syncfusion_UI_Xaml_Scheduler_SfScheduler_HeaderDateFormat) property of SfScheduler. By default, the header date format is `MMMM yyyy`.

{% tabs %}
{% highlight xaml %}
<syncfusion:SfScheduler x:Name="Schedule"
                        HeaderDateFormat="MMM/yyyy">   
</syncfusion:SfScheduler>
{% endhighlight %}
{% highlight c#%}
this.Schedule.HeaderDateFormat = "MMM/yyyy";
{% endhighlight %}
{% endtabs %}

![WPF Scheduler header HeaderDateFormat](Header_Images/HeaderDateFormat.png)

## Appearance customization

### Customize header appearance using Style
Style the Scheduler header appearance using [SchedulerHeaderControl](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Scheduler.SchedulerHeaderControl.html) in scheduler. Change the background color, textStyle, and borderBrush etc. by setting style property for `SchedulerHeaderControl`.

{% tabs %}
{% highlight xaml %}
<Style TargetType="syncfusion:SchedulerHeaderControl">
    <Setter Property="Background" Value="LightCyan"/>
    <Setter Property="Foreground" Value="Red"/>
    <Setter Property="FontStyle" Value="Italic"/>
    <Setter Property="BorderBrush" Value="LightCoral"/>
    <Setter Property="BorderThickness" Value="2"/>
</Style>
{% endhighlight %}
{% endtabs %}

![WPF Scheduler header CustomizedHeader](Header_Images/CustomizedHeader.png)

### Customize header appearance using DataTemplate
Customize header appearance of scheduler by using [HeaderTemplate](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Scheduler.SfScheduler.html#Syncfusion_UI_Xaml_Scheduler_SfScheduler_HeaderTemplate) property of SfScheduler.

{% tabs %}
{% highlight xaml %}
<syncfusion:SfScheduler x:Name="Schedule">
    <syncfusion:SfScheduler.HeaderTemplate>
        <DataTemplate >
                <TextBlock FontStyle="Italic"
                           Foreground="Blue"
                           FontSize="25"
                           Text="{Binding}"/>
        </DataTemplate>
    </syncfusion:SfScheduler.HeaderTemplate>
</syncfusion:SfScheduler>
{% endhighlight %}
{% endtabs %}

![WPF Scheduler header HeaderTemplate](Header_Images/HeaderTemplate.png)

N> You can refer to our [WPF Scheduler](https://www.syncfusion.com/wpf-controls/scheduler) feature tour page for its groundbreaking feature representations. You can also explore our [WPF Scheduler example](https://github.com/syncfusion/wpf-demos) to knows how to schedule and manage appointments through an intuitive user interface, similar to the Outlook calendar.