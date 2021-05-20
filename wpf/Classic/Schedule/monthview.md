---
layout: post
title: Month View in WPF SfSchedule Control | Syncfusion
description: Learn here all about Month View support in Syncfusion WPF Schedule (Classic) control, its elements and more details.
platform: wpf
control: SfSchedule
documentation: ug
---

# Month View in WPF Schedule (Classic)
Scheduler used to display entire dates of the specific month, current month will be displayed by default initially. `Month` view displays the month of dates similar to calendar and displays appointments for each day in a cell similar to outlook. 

## Change header date format
Scheduler supports to change header format of the month view by using [MonthHeaderDateFormat](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Schedule.SfSchedule.html#Syncfusion_UI_Xaml_Schedule_SfSchedule_MonthHeaderDateFormat) property.

{% tabs %}
{% highlight xaml %}
<Schedule:SfSchedule ScheduleType="Month" MonthHeaderDateFormat="dd/MM"/>
{% endhighlight %}
{% highlight c#%}
this.schedule.ScheduleType = ScheduleType.Month;
this.schedule.HeaderDateFormat = "dd/MM;
{% endhighlight %}
{% endtabs %}

![WPF Scheduler month view header date format](monthview_images/monthview-header-date-fromat.png)

## Change header background
Scheduler supports to change the header background by using [HeaderBackground](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Schedule.SfSchedule.html#Syncfusion_UI_Xaml_Schedule_SfSchedule_HeaderBackground) property.

{% tabs %}
{% highlight xaml %}
<Schedule:SfSchedule ScheduleType="Month" HeaderBackground="Cyan"/>
{% endhighlight %}
{% highlight c#%}
this.schedule.ScheduleType = ScheduleType.Month;
this.schedule.HeaderBackground = Brushes.Cyan;
{% endhighlight %}
{% endtabs %}

![WPF Scheduler month view header background](monthview_images/monthview-header-background.png)

## Change first day of week
Scheduler supports to change the first day of week by using [FirstDayOfWeek](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Schedule.SfSchedule.html#Syncfusion_UI_Xaml_Schedule_SfSchedule_FirstDayOfWeek) property.

{% tabs %}
{% highlight xaml %}
<Schedule:SfSchedule ScheduleType="Month" FirstDayOfWeek="Tuesday"/>
{% endhighlight %}
{% highlight c#%}
this.schedule.ScheduleType = ScheduleType.Month;
this.schedule.FirstDayOfWeek = DayOfWeek.Tuesday;
{% endhighlight %}
{% endtabs %}

![WPF Scheduler month view first day of week](monthview_images/monthview-first-day-of-week.png)

## Change active and inactive month dates background
Scheduler supports to change the active and inactive month background by using [FocusedMonth](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Schedule.SfSchedule.html#Syncfusion_UI_Xaml_Schedule_SfSchedule_FocusedMonth) and [NonFocusedMonth](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Schedule.SfSchedule.html#Syncfusion_UI_Xaml_Schedule_SfSchedule_NonFocusedMonth) property.

{% tabs %}
{% highlight xaml %}
<Schedule:SfSchedule ScheduleType="Month" FocusedMonth="AliceBlue" NonFocusedMonth = "SkyBlue"/>
{% endhighlight %}
{% highlight c#%}
this.schedule.ScheduleType = ScheduleType.Month;
this.schedule.FocusedMonth = Brushes.AliceBlue;
this.schedule.NonFocusedMonth = Brushes.SkyBlue;
{% endhighlight %}
{% endtabs %}

![WPF Scheduler month view acitve and inactive dates background](monthview_images/monthview-focused-nonfocused-background.png)

## Change the border color
Scheduler support to change the header items border color by using [MonthViewLineStroke](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Schedule.SfSchedule.html#Syncfusion_UI_Xaml_Schedule_SfSchedule_MonthViewLineStroke) property.

{% tabs %}
{% highlight xaml %}
<Schedule:SfSchedule ScheduleType="Month" MonthViewLineStroke="BlueViolet"/>
{% endhighlight %}
{% highlight c#%}
this.schedule.ScheduleType = ScheduleType.Month;
this.schedule.MonthViewLineStroke = Brushes.BlueViolet;
{% endhighlight %}
{% endtabs %}

![WPF Scheduler month view border color changes](monthview_images/monthview-border-color-changed.png)

## Change the selection background
Scheduler supports to change the selection background by using [CellSelectionBrush](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Schedule.SfSchedule.html#Syncfusion_UI_Xaml_Schedule_SfSchedule_CellSelectionBrush)

{% tabs %}
{% highlight xaml %}
<Schedule:SfSchedule ScheduleType="Month" CellSelectionBrush="SkyBlue"/>
{% endhighlight %}
{% highlight c#%}
this.schedule.ScheduleType = ScheduleType.Month;
this.schedule.CellSelectionBrush = Brushes.SkyBlue;
{% endhighlight %}
{% endtabs %}

![WPF Scheduler month view selection background](monthview_images/monthview-cell-selection-brush.png)

## Current day highlighting
Scheduler supports to change current day background and foreground for month view by using [CurrentDateBackground](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Schedule.SfSchedule.html#Syncfusion_UI_Xaml_Schedule_SfSchedule_CurrentDateBackground) and [CurrentDateForeground](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Schedule.SfSchedule.html#Syncfusion_UI_Xaml_Schedule_SfSchedule_CurrentDateForeground) property.

{% tabs %}
{% highlight xaml %}
<syncfusion:SfSchedule ScheduleType="Month" CurrentDateBackground="Brown" CurrentDateForeground="White"/>
{% endhighlight %}
{% highlight c# %}
this.schedule.ScheduleType = ScheduleType.Month;
this.schedule.CurrentDateBackground = Brushes.Brown;
this.schedule.CurrentDateForeground = Brushes.White;
{% endhighlight %}
{% endtabs %}

![WPF Scheduler month view current date background](monthview_images/monthview-currentdate-background.png)