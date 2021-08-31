---
layout: post
title: Map Shape Labels in WPF Maps control | Syncfusion
description: Learn here all about Map Shape Labels support in Syncfusion WPF Maps (SfMap) control, its elements and more details.
platform: wpf
control: SfMap
documentation: ug
---

# Map Shape Labels in WPF Maps (SfMap)

Labels for map shapes can be displayed by using the [`LabelPath`](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Maps.ShapeFileLayer.html#Syncfusion_UI_Xaml_Maps_ShapeFileLayer_LabelPath) of ShapeFileLayer. The value of LabelPath must be a field name specified in the .dbf file corresponding to the shapefile. 


<table>
<tr>
<th>
Property</th><th>
Type</th><th>
Description</th></tr>
<tr>
<td>
LabelPath</td><td>
string</td><td>
Gets or sets the field name in the database (.dbf) file.</td></tr>
</table>

{% tabs %}

{% highlight xaml %}

      <syncfusion:SfMap>
            <syncfusion:SfMap.Layers>
                <syncfusion:ShapeFileLayer x:Name="shapeFileLayer"   
                                       Uri="DataMarkers.ShapeFiles.world1.shp"  
                                       LabelPath="NAME" FontSize="14">
                </syncfusion:ShapeFileLayer>
            </syncfusion:SfMap.Layers>
        </syncfusion:SfMap>

{% endhighlight %}

{% highlight c# %}

            SfMap map = new SfMap();          
            ShapeFileLayer shapeFileLayer = new ShapeFileLayer();
            shapeFileLayer.LabelPath = "NAME";
            shapeFileLayer.FontSize = 14;
            shapeFileLayer.Uri = "DataMarkers.ShapeFiles.world1.shp";
            map.Layers.Add(shapeFileLayer);
            this.Content = map;

{% endhighlight %}

{% endtabs %}

The labels can also be customized by modifying the [`ItemsTemplate`](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Maps.ShapeFileLayer.html#Syncfusion_UI_Xaml_Maps_ShapeFileLayer_ItemsTemplate) of ShapeFileLayer. The labels can be accessed by using DBFData as follows:

{% tabs %}

{% highlight xaml %}

      <Grid.Resources>
            <DataTemplate x:Key="itemtemplate">
                <Grid >
                    <TextBlock Text="{Binding DbfData[NAME]}"
                                       FontSize="14" Margin="10 5"/>
                </Grid>
            </DataTemplate>
        </Grid.Resources>

         <syncfusion:SfMap>
            <syncfusion:SfMap.Layers>
                <syncfusion:ShapeFileLayer Uri="DataMarkers.ShapeFiles.world1.shp"
                                       LabelPath="NAME" ItemsTemplate="{StaticResource itemtemplate}">
                   
                </syncfusion:ShapeFileLayer>
            </syncfusion:SfMap.Layers>
        </syncfusion:SfMap>

{% endhighlight %}

{% highlight c# %}

            SfMap map = new SfMap();          
            ShapeFileLayer shapeFileLayer = new ShapeFileLayer();
            shapeFileLayer.LabelPath = "NAME";
            shapeFileLayer.Uri = "DataMarkers.ShapeFiles.world1.shp";
            shapeFileLayer.ItemsTemplate = grid.Resources["itemTemplate"] as DataTemplate;
            map.Layers.Add(shapeFileLayer);
            this.Content = map;

{% endhighlight %}

{% endtabs %}


![Maps control Shape labels](Map-Shape-Labels_images/Map-Shape-Labels_img1.png)

N> You can refer to our [WPF Map](https://www.syncfusion.com/wpf-controls/map) feature tour page for its groundbreaking feature representations. You can also explore our [WPF Map example](https://github.com/syncfusion/wpf-demos/tree/master/map) to know how to render and configure the map.
