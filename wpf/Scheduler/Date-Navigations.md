---
layout: post
title: Date navigations in WPF Scheduler control | Syncfusion
description: Learn here all about to use Date Navigations in Syncfusion WPF Scheduler (SfScheduler) control and more.
platform: wpf
control: SfScheduler
documentation: ug
---

# Date Navigations in WPF Scheduler (SfScheduler)

## Range for visible dates
Visible dates can be restricted between certain range of dates, using [MaximumDate](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Scheduler.SfScheduler.html#Syncfusion_UI_Xaml_Scheduler_SfScheduler_MaximumDate) and [MinimumDate](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Scheduler.SfScheduler.html#Syncfusion_UI_Xaml_Scheduler_SfScheduler_MinimumDate) properties in [SfScheduler](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Scheduler.SfScheduler.html). It is applicable in all the schedule views.

### Minimum display date
`MinimumDate` will restrict date navigations features of backward, also cannot swipe the control using touch gesture beyond the minimum date range. The dates before the minimum date will be disabled in the schedule.

{% tabs %}
{% highlight xaml %}
<syncfusion:SfScheduler x:Name="Schedule"
                        MinimumDate="2020-05-05 10:0:0">
</syncfusion:SfScheduler>
{% endhighlight %}
{% highlight c#%}
this.Schedule.MinimumDate = new DateTime(2020, 05, 05, 10, 0, 0);
{% endhighlight %}
{% endtabs %}

### Maximum display date
`MaximumDate` will restrict date navigations features of forward, and also cannot swipe the control using touch gesture beyond the maximum date range. The dates beyond the maximum date will be disabled in the schedule.

{% tabs %}
{% highlight xaml %}
<syncfusion:SfScheduler x:Name="Schedule"
                        MaximumDate="2020-10-05 10:0:0">
</syncfusion:SfScheduler>
{% endhighlight %}
{% highlight c#%}
this.Schedule.MaximumDate = new DateTime(2020, 10, 05, 10, 0, 0);
{% endhighlight %}
{% endtabs %}

## Programmatic date navigation
You can programmatically navigate the dates in scheduler by using the [DisplayDate](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Scheduler.SfScheduler.html#Syncfusion_UI_Xaml_Scheduler_SfScheduler_DisplayDate) property of SfScheduler.

{% tabs %}
{% highlight xaml %}
<syncfusion:SfScheduler x:Name="Schedule"
                        DisplayDate="2020-07-05 10:0:0">
</syncfusion:SfScheduler>
{% endhighlight %}
{% highlight c#%}
this.Schedule.DisplayDate = new DateTime(2020, 07, 05, 10, 0, 0);
{% endhighlight %}
{% endtabs %}

N>Date navigation before the minimum date will be reset to the scheduler minimum date and date navigation beyond the maximum date will be reset to the scheduler maximum date.

## Programmatic date selection
You can programmatically select the dates in scheduler by using the [SelectedDate](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Scheduler.SfScheduler.html#Syncfusion_UI_Xaml_Scheduler_SfScheduler_SelectedDate) property of SfScheduler.

{% tabs %}
{% highlight xaml %}
<syncfusion:SfScheduler x:Name="Schedule"
                        SelectedDate="2020-07-10 10:0:0">
</syncfusion:SfScheduler>
{% endhighlight %}
{% highlight c#%}
this.Schedule.SelectedDate = new DateTime(2020, 07, 10, 10, 0, 0);
{% endhighlight %}
{% endtabs %}

N>Selection before minimum dates and beyond maximum dates using the `SelectedDate` is not possible.

## Programmatically change to adjacent dates
By default, the date can be navigated to next and previous views using touch gesture, by swiping the control from right to left and left to right direction. The view can be also changed programmatically using the [Forward](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Scheduler.SfScheduler.html#Syncfusion_UI_Xaml_Scheduler_SfScheduler_Forward) and [Backward](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Scheduler.SfScheduler.html#Syncfusion_UI_Xaml_Scheduler_SfScheduler_Backward) methods available in SfScheduler.

### Forward
You can use the `Forward` method of SfScheduler for viewing the next immediate visible dates in the scheduler. It will move to next month if the scheduler view is month, similarly it will move to next week for week view and next day for day view.

{% tabs %}
{% highlight xaml %}
<syncfusion:SfScheduler x:Name="Schedule"
                        MaximumDate="2020-10-05 10:0:0">
</syncfusion:SfScheduler>

<Button x:Name="Forward"
        Content="fwd" 
        Click="Forward_Click">
</Button>
{% endhighlight %}
{% highlight c#%}
private void Forward_Click(object sender, RoutedEventArgs e)
{
    Schedule.Forward();
}
{% endhighlight %}
{% endtabs %}

### Backward
You can use the `Backward` method of SfScheduler for viewing the previous immediate visible dates in the scheduler. It will move to previous month if the scheduler view is month, similarly it will move to previous week for week view and previous day for day view.

{% tabs %}
{% highlight xaml %}
<syncfusion:SfScheduler x:Name="Schedule"
                        MinimumDate="2020-05-05 10:0:0">
</syncfusion:SfScheduler>

<Button x:Name="Backward"
        Content="bwd" 
        Click="Backward_Click">
</Button>
{% endhighlight %}
{% highlight c#%}
private void Backward_Click(object sender, RoutedEventArgs e)
{
    Schedule.Backward();
}
{% endhighlight %}
{% endtabs %}