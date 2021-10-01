---
layout: post
title: Custom Editor in WPF PropertyGrid control | Syncfusion
description: Learn about Custom Editor support in Syncfusion Essential Studio WPF PropertyGrid control, its elements and more.
platform: wpf
control: PropertyGrid 
documentation: ug
---

# Custom Editor in WPF PropertyGrid

The [PropertyGrid](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.PropertyGrid.html) control supports several built-in editors. Based on the property type, the built-in editors automatically assigned as value editor for the properties. You can assign own value editor(control) for the properties instead of default value editor by using the [Editor](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.editorattribute?view=netframework-4.8) attribute or [CustomEditorCollection](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.PropertyGrid.html#Syncfusion_Windows_PropertyGrid_PropertyGrid_CustomEditorCollection).

 For example, if you creates an `EmailID` property as a string type, `TextBox` is assigned as a value editor and all the text will be allowed. If you want to accept the input that is only in the mail id format, you can assign [SfMaskedEdit](https://www.syncfusion.com/wpf-ui-controls/maskedtextbox) control with email-id mask as the value editor for the `EmailID` property. 

## Best practice to follow
When using the [CustomEditorCollection](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.PropertyGrid.html#Syncfusion_Windows_PropertyGrid_PropertyGrid_CustomEditorCollection) property to assign a custom editor to multiple properties of the same data type in the `PropertyGrid`, it is recommended to use the [`EditorType`](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.CustomEditor.html#Syncfusion_Windows_PropertyGrid_CustomEditor_EditorType),[`PropertyType`](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.CustomEditor.html#Syncfusion_Windows_PropertyGrid_CustomEditor_PropertyType) and [`HasPropertyType`](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.CustomEditor.html#Syncfusion_Windows_PropertyGrid_CustomEditor_HasPropertyType) properties of the [`CustomEditor`](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.CustomEditor.html) class. Otherwise, for proper functionality, you must create a new `CustomEditor` class and assign it to each property using the `Properties` collection property.

## Creating the Custom Editor

To create [CustomEditor](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.CustomEditor.html), we need to implement [ITypeEditor](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.ITypeEditor.html) interface. Here, `SfMaskedEdit` control is assigned with mail id mask as `EmailEditor` and `UpDown` control is assigned with min, max value as `IntegerEditor`. `EmailEditor` and `IntegerEditor` are the custom editors.

{% tabs %}
{% highlight C# %}

//Custom Editor for the EmailId properties.
public class EmailEditor : ITypeEditor {
    SfMaskedEdit maskededit;
    public void Attach(PropertyViewItem property, PropertyItem info) {
        if (info.CanWrite) {
            var binding = new Binding("Value")
            {
                Mode = BindingMode.TwoWay,
                Source = info,
                ValidatesOnExceptions = true,
                ValidatesOnDataErrors = true
            };
            BindingOperations.SetBinding(maskededit, SfMaskedEdit.ValueProperty, binding);
        }
        else {
            maskededit.IsEnabled = false;
            var binding = new Binding("Value")
            {
                Source = info,
                ValidatesOnExceptions = true,
                ValidatesOnDataErrors = true
            };
            BindingOperations.SetBinding(maskededit, SfMaskedEdit.ValueProperty, binding);
        }
    }
    public object Create(PropertyInfo propertyInfo) {
        maskededit = new SfMaskedEdit();
        maskededit.MaskType = MaskType.RegEx;
        maskededit.Mask = "[A-Za-z0-9._%-]+@[A-Za-z0-9]+.[A-Za-z]{2,3}";
        return maskededit;
    }
    public void Detach(PropertyViewItem property) {

    }
}

//Custom Editor for the integer type properties.
public class IntegerEditor : ITypeEditor {
    UpDown upDown;
    public void Attach(PropertyViewItem property, PropertyItem info) {
        if (info.CanWrite) {
            var binding = new Binding("Value")
            {
                Mode = BindingMode.TwoWay,
                Source = info,
                ValidatesOnExceptions = true,
                ValidatesOnDataErrors = true
            };
            BindingOperations.SetBinding(upDown, UpDown.ValueProperty, binding);
        }
        else {
            upDown.IsEnabled = false;
            var binding = new Binding("Value")
            {
                Source = info,
                ValidatesOnExceptions = true,
                ValidatesOnDataErrors = true
            };
            BindingOperations.SetBinding(upDown, UpDown.ValueProperty, binding);
        }
    }
    public object Create(PropertyInfo propertyInfo) {
        upDown = new UpDown();
        upDown.ApplyZeroColor = false;
        upDown.MinValue = 0;
        upDown.MaxValue = 100;
        upDown.NumberDecimalDigits = 0;
        return upDown;
    }
    public void Detach(PropertyViewItem property) {

    }
}

{% endhighlight  %}
{% endtabs %}

N> To assign a created custom editor to a properties, refer the [Assigning a Custom Editor](https://help.syncfusion.com/wpf/propertygrid/customeditor-support#assigning-a-custom-editor-using-editor-attribute) topic.

## Creating Custom Editor for a dynamic property.

If the [SelectedObject](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.PropertyGrid.html#Syncfusion_Windows_PropertyGrid_PropertyGrid_SelectedObject) has a property of type `dynamic`, `ExpandoObject` or `ICustomTypeDescriptor`, we can create `CustomEditor` class by inheriting [BaseTypeEditor](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.BaseTypeEditor.html). You can initialize a new instance of the custom editor using the [BaseTypeEditor.Create(PropertyDescriptor)](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.BaseTypeEditor.html#Syncfusion_Windows_PropertyGrid_BaseTypeEditor_Create_System_ComponentModel_PropertyDescriptor_) function. Below example shows, how to get the value of dynamic properties using its PropertyDescriptor and apply the value in `ComboEditor` to ComboBox objects.

{% tabs %}

{% highlight C# %}

//Custom Editor for the List<string> type properties.
public class ComboEditor : BaseTypeEditor
{
    ComboBox comboBox;
      
    public override void Attach(PropertyViewItem property, PropertyItem info)
    {
        var binding = new Binding("Value")
        {
            Mode = BindingMode.TwoWay,
            Source = info,
            ValidatesOnExceptions = true,
            ValidatesOnDataErrors = true
        };
        BindingOperations.SetBinding(comboBox, ComboBox.SelectedItemProperty, binding);
    }

    // Create a custom editor for a normal property
    public override object Create(PropertyInfo PropertyInfo)
    {
        throw new NotImplementedException();
    }
    
    // Create a custom editor for a dynamic property
    public override object Create(PropertyDescriptor PropertyDescriptor)
    {
        comboBox = new ComboBox();
        // Getting the values of dynamic property
        dynamic comboBoxItemsList = PropertyDescriptor.GetValue(PropertyDescriptor.Name);
        foreach (dynamic items in comboBoxItemsList)
        {
            comboBox.Items.Add(items);
        }

        comboBox.SelectedIndex = 0;
        return comboBox;
    }

    public override void Detach(PropertyViewItem property)
    {
        comboBox = null;
    }
}

{% endhighlight  %}

{% endtabs %}

N> Download demo application from [GitHub](https://github.com/SyncfusionExamples/wpf-property-grid-examples/tree/master/Samples/CustomEditor/CustomEditor-dynamic-type-selected-object).

## Assigning a Custom Editor using Editor Attribute

We can assign the `CustomEditor` to any individual property by name of the property and to multiple properties based on the property type by using the `Editor` attribute.

{% tabs %}
{% highlight C# %}

//CustomEditor for the specfic(EmailID) property
[Editor("EmailID", typeof(EmailEditor))]

//Custom Editor for the multiple(Tnteger type) properties
[Editor(typeof(int), typeof(IntegerEditor))]
public class Employee {
    public string EmailID { get; set; }
    public string Name { get; set; }
    public int Age { get; set; }
    public int Experience { get; set; }
}

class ViewModel {
    public object SelectedEmployee { get; set; }
    public ViewModel() {
        SelectedEmployee = new Employee()
        {
            Age = 25,
            Name = "mark",
            Experience = 5,
            EmailID = "mark@gt"
        };
    }
}

{% endhighlight  %}
{% endtabs %}

{% tabs %}
{% highlight xaml %}

<syncfusion:PropertyGrid SelectedObject="{Binding SelectedEmployee}"
                         x:Name="propertyGrid1" >
    <syncfusion:PropertyGrid.DataContext>
        <local:ViewModel></local:ViewModel>
   </syncfusion:PropertyGrid.DataContext>
</syncfusion:PropertyGrid>

{% endhighlight  %}
{% highlight C# %}

PropertyGrid propertyGrid1 = new PropertyGrid();
propertyGrid1.DataContext = new ViewModel();
propertyGrid1.SetBinding(PropertyGrid.SelectedObjectProperty, new Binding("SelectedEmployee"));

{% endhighlight  %}
{% endtabs %}

Here, `EmailID` property value editor changed from `TextBox` to  `MaskedEdit` control with email id mask. Also, we assigned the `IntegerEditor` for the integer type properties, so it applied to the `Experience` and `Age` properties. Then, the value editors for the `Experience` and `Age` property is changed from `NumericTextBox` to `Updown` control.

![Property grid with specified custom editors](CustomEditor-support_images/CustomEditor-Attribute.png)

## Assigning a Custom Editor using Collection

We can assign the `CustomEditor` to any particular property and to multiple properties using the `CustomEditorCollection`. 

## Assigning a Custom Editor to the specific property

If we want to apply custom editor for any particular property, we need to create the `CustomEditor` instance, assign our own editor to the `CustomEditor.Editor` and add the property name to the `CustomEditor.Properties` collection. Then, add the `CustomEditor` instance to the `PropertyGrid.CustomEditorCollection`.

{% tabs %}
{% highlight C# %}

public class Employee {
    public string EmailID { get; set; }
    public string Name { get; set; }
    public int Age { get; set; }
    public int Experience { get; set; }
}

class ViewModel {
    public object SelectedEmployee { get; set; }
    public CustomEditorCollection customEditorCollection = new CustomEditorCollection();
    public CustomEditorCollection CustomEditorCollection
    {
        get { return customEditorCollection; }
        set { customEditorCollection = value; }
    }
    public ViewModel() {
        SelectedEmployee = new Employee() { Age = 25, Name = "mark", Experience = 5, EmailID = "mark@gt" };

        // EmailEditor added to the collection and will applied to the "EmailID" property
        CustomEditor editor1 = new CustomEditor();
        editor1.Editor = new EmailEditor();
        editor1.Properties.Add("EmailID");
        CustomEditorCollection.Add(editor1);
    }
}

{% endhighlight  %}
{% endtabs %}

{% tabs %}
{% highlight xaml %}

<syncfusion:PropertyGrid CustomEditorCollection="{Binding CustomEditorCollection}" 
                         SelectedObject="{Binding SelectedEmployee}"
                         x:Name="propertyGrid1" >
    <syncfusion:PropertyGrid.DataContext>
        <local:ViewModel></local:ViewModel>
   </syncfusion:PropertyGrid.DataContext>
</syncfusion:PropertyGrid>

{% endhighlight  %}
{% highlight C# %}

PropertyGrid propertyGrid1 = new PropertyGrid();
propertyGrid1.DataContext = new ViewModel();
propertyGrid1.SetBinding(PropertyGrid.CustomEditorCollectionProperty, new Binding("CustomEditorCollection"));
propertyGrid1.SetBinding(PropertyGrid.SelectedObjectProperty, new Binding("SelectedEmployee"));

{% endhighlight  %}
{% endtabs %}

Here, The `EmailID` is a string property, the `TextBox` is assigned as a default editor. We changed it as `SfMaskedEdit` textbox that accepts only inputs which are in the email id format.

![CustomEditor applied for EmailID property](CustomEditor-support_images/CustomEditor-Collection1.png)

## Assigning a Custom Editor based on the property type

If we want to apply custom editor for multiple properties which are all contains same type, we need to create the `CustomEditor` instance, assign our own editor to the `CustomEditor.Editor` and sets the `CustomEditor.HasPropertyType`  property  to `true`. Then, mention the property type to the `CustomEditor.PropertyType`.

{% tabs %}
{% highlight C# %}

public class Employee {
    public string EmailID { get; set; }
    public string Name { get; set; }
    public int Age { get; set; }
    public int Experience { get; set; }
}

class ViewModel {
    public object SelectedEmployee { get; set; }
    public CustomEditorCollection customEditorCollection = new CustomEditorCollection();
    public CustomEditorCollection CustomEditorCollection
    {
        get { return customEditorCollection; }
        set { customEditorCollection = value; }
    }
    public ViewModel() {
        SelectedEmployee = new Employee() { Age = 25, Name = "mark", Experience = 5, EmailID = "mark@gt" };

        // IntegerEditor added to the collection and will applied to the "int" type properties
        CustomEditor editor = new CustomEditor();
        editor.Editor = new IntegerEditor();
        editor.HasPropertyType = true;
        editor.PropertyType = typeof(int);
        CustomEditorCollection.Add(editor);
    }
}

{% endhighlight  %}
{% endtabs %}

{% tabs %}
{% highlight xaml %}

<syncfusion:PropertyGrid CustomEditorCollection="{Binding CustomEditorCollection}" 
                         SelectedObject="{Binding SelectedEmployee}"
                         x:Name="propertyGrid1" >
    <syncfusion:PropertyGrid.DataContext>
        <local:ViewModel></local:ViewModel>
   </syncfusion:PropertyGrid.DataContext>
</syncfusion:PropertyGrid>

{% endhighlight  %}
{% highlight C# %}

PropertyGrid propertyGrid1 = new PropertyGrid();
propertyGrid1.DataContext = new ViewModel();
propertyGrid1.SetBinding(PropertyGrid.CustomEditorCollectionProperty, new Binding("CustomEditorCollection"));
propertyGrid1.SetBinding(PropertyGrid.SelectedObjectProperty, new Binding("SelectedEmployee"));

{% endhighlight  %}
{% endtabs %}

![CustomEditor applied for integer type properties](CustomEditor-support_images/CustomEditor-Collection2.png)

Here, we assigned the `IntegerEditor` custom editor for the integer type properties, so it applied to the `Experience` and `Age` properties. Then, the value editors for the `Experience` and `Age` property is changed from `NumericTextBox` to `Updown` control.

Click [here](https://github.com/SyncfusionExamples/wpf-property-grid-examples/tree/master/Samples/CustomEditor) to download the sample that showcases the `CustomEditor` support.

## Assigning a Custom Editor by the editor type

By default, when we use the [CustomEditor.Editor](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.CustomEditor.html#Syncfusion_Windows_PropertyGrid_CustomEditor_Editor) to target multiple properties in `PropertyGrid`, the same custom editor instance is used for all those properties. To maintain a dedicated or separate instance of the custom editor for each property, use [CustomEditor.EditorType](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.CustomEditor.html#Syncfusion_Windows_PropertyGrid_CustomEditor_EditorType). The default value of the `EditorType` property is **null**. 

You can set the value for `EditorType` property when custom editor is initialized in `ViewModel` class as shown below.

{% tabs %}
{% highlight xaml %}

<syncfusion:PropertyGrid CustomEditorCollection="{Binding CustomEditorCollection}" 
                         SelectedObject="{Binding SelectedEmployee}"
                         x:Name="propertyGrid1" >
    <syncfusion:PropertyGrid.DataContext>
        <local:ViewModel></local:ViewModel>
   </syncfusion:PropertyGrid.DataContext>
</syncfusion:PropertyGrid>

{% endhighlight  %}
{% highlight C# %}

public class Employee
{
    public string Country { get; set; }
    public double Experience { get; set; }
    public string Name { get; set; }
    public double Age { get; set; }
}

class ViewModel 
{
    public object SelectedEmployee { get; set; }

    private CustomEditorCollection customEditorCollection = new CustomEditorCollection();
    public CustomEditorCollection CustomEditorCollection
    {
        get { return customEditorCollection; }
        set { customEditorCollection = value; }
    }

    public ViewModel()
    {
         SelectedEmployee = new Employee() { Age = 25, Name = "mark", Experience = 5, EmailID = "mark@gt.com" };
        CustomEditor editor1 = new CustomEditor()
        {
            EditorType = typeof(IntegerEditor),
            HasPropertyType = true,
            PropertyType = typeof(double)
        };

        CustomEditorCollection.Add(editor1);

    }
}

{% endhighlight  %}
{% endtabs %}

You can also set value for `CustomEditorType` property for `CustomEditor` class in the xaml file as shown below.

<syncfusion:PropertyGrid SelectedObject="{Binding SelectedEmployee}" 
                            x:Name="propertyGrid1" >
    <syncfusion:PropertyGrid.DataContext>
        <local:ViewModel></local:ViewModel>
    </syncfusion:PropertyGrid.DataContext>
    <syncfusion:PropertyGrid.CustomEditorCollection>
            <syncfusion:CustomEditorCollection>
                <syncfusion:CustomEditor  PropertyType="{x:Type a:Double}" HasPropertyType="True" EditorType="{x:Type local:IntegerEditor}" />
            </syncfusion:CustomEditorCollection>
        </syncfusion:PropertyGrid.CustomEditorCollection>
</syncfusion:PropertyGrid>

![CustomEditor applied for integer type properties](CustomEditor-support_images/CustomEditor-Collection2.png)

## Use constructor with parameters in custom editor

By default, [`PropertyGrid`](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid) control only invokes the constructor without parameter in custom editor. You can invoke and pass arguments to the constructors with any number of parameters in custom editor using the [ConstructorParameter](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.CustomEditor.html#Syncfusion_Windows_PropertyGrid_CustomEditor_ConstructorParameters) property of [CustomEditor](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.CustomEditor) class. The default value of `ConstructorParameter` is **null**. This can be achieved by following the below steps.

N> `ConstructorParameter` property will work only if a value is assigned for the `EditorType` property in the `CustomEditor` class.

1. Create a custom editor for the desired property item in `PropertyGrid`. Add constructor with parameters in the custom editor class.

{% tabs %}
{% highlight C# %}

public class IntegerEditor : ITypeEditor
{
    IntegerTextBox integerTextBox;
    bool ShowUpDown = false;

    public IntegerEditor()
    {

    }

    // Constructor with parameter in custom editor
    public IntegerEditor(bool showUpDown)
    {
        ShowUpDown = showUpDown;
    }

    public void Attach(PropertyViewItem property, PropertyItem info)
    {
        if (info.CanWrite)
        {
            var binding = new Binding("Value")
            {
                Mode = BindingMode.TwoWay,
                Source = info,
                ValidatesOnExceptions = true,
                ValidatesOnDataErrors = true
            };
            BindingOperations.SetBinding(integerTextBox, IntegerTextBox.ValueProperty, binding);
        }
        else
        {
            integerTextBox.IsEnabled = false;
            var binding = new Binding("Value")
            {
                Source = info,
                ValidatesOnExceptions = true,
                ValidatesOnDataErrors = true
            };
            BindingOperations.SetBinding(integerTextBox, IntegerTextBox.ValueProperty, binding);
        }
    }
    public object Create(PropertyInfo propertyInfo)
    {
        integerTextBox = new IntegerTextBox()
        {
            ApplyZeroColor = false,
            MinValue = 0,
            MaxValue = 50,
            ShowSpinButton = ShowUpDown,
        };
        return integerTextBox;
    }
    public void Detach(PropertyViewItem property)
    {

    }
}

{% endhighlight  %}
{% endtabs %}

2. Create `Employee` and `ViewModel` classes with required properties. Pass the required objects in an object array and assign it to the `ConstructorParameter` property of `CustomEditor` as shown below. 

{% tabs %}
{% highlight C# %}

public class Employee
{
    public string EmailID { get; set; }
    public double Experience { get; set; }
    public string Name { get; set; }
    public long Age { get; set; }
}


class ViewModel 
{
    public object SelectedEmployee { get; set; }

    private CustomEditorCollection customEditorCollection = new CustomEditorCollection();
    public CustomEditorCollection CustomEditorCollection
    {
        get { return customEditorCollection; }
        set { customEditorCollection = value; }
    }

    public int DecimalDigits { get; set; }
    public ViewModel()
    {
        SelectedEmployee = new Employee() { Age = 25, Name = "Mark Anthony", EmailID = "markanthony@syncfusion.com", Experience = 3 };
        CustomEditor editor1 = new CustomEditor()
        {
            EditorType = typeof(IntegerEditor),
            HasPropertyType = true,
            PropertyType = typeof(long),
            ConstructorParameters = new object [] {true}
        };

        CustomEditorCollection.Add(editor1);

    }
}

{% endhighlight  %}
{% highlight xaml %}
<syncfusion:PropertyGrid CustomEditorCollection="{Binding CustomEditorCollection}" SelectedObject="{Binding SelectedEmployee}" 
                         x:Name="propertyGrid1" >
    <syncfusion:PropertyGrid.DataContext>
        <local:ViewModel></local:ViewModel>
    </syncfusion:PropertyGrid.DataContext>
</syncfusion:PropertyGrid>

{% endhighlight  %}
{% endtabs %}

Since we have assigned the custom editor for property type **long(Int64)**, the custom editor will be applied for `Age` property item. You can also create custom editor and set value for `ConstructorParameter` property in xaml file as shown below.

{% tabs %}
{% highlight xaml %}

<syncfusion:PropertyGrid SelectedObject="{Binding SelectedEmployee}" 
                            x:Name="propertyGrid1" >
    <syncfusion:PropertyGrid.DataContext>
        <local:ViewModel></local:ViewModel>
    </syncfusion:PropertyGrid.DataContext>
    <syncfusion:PropertyGrid.CustomEditorCollection>
        <syncfusion:CustomEditorCollection>
            <syncfusion:CustomEditor  PropertyType="{x:Type a:Int64}" HasPropertyType="True" EditorType="{x:Type local:IntegerEditor}" >
                <syncfusion:CustomEditor.ConstructorParameters>
                    <x:Array Type="{x:Type a:Object}">
                        <a:Boolean>True</a:Boolean>
                    </x:Array>
                </syncfusion:CustomEditor.ConstructorParameters>
            </syncfusion:CustomEditor>
        </syncfusion:CustomEditorCollection>
    </syncfusion:PropertyGrid.CustomEditorCollection>
</syncfusion:PropertyGrid>

{% endhighlight  %}
{% endtabs %}

![ConstructorParameter passed in CustomEditor](CustomEditor-support_images/propertygrid-wpf-constructor-with-parameter-customeditor.png)

## Create custom editor control for the property item
The [`PropertyGrid`](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid) control allows users to create their editor controls using the [CustomEditor](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.CustomEditor.html) class and [CustomEditorCollection](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.PropertyGrid.html#Syncfusion_Windows_PropertyGrid_PropertyGrid_CustomEditorCollection) property for property items. The custom editors can be inherited from [ITypeEditor](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.ITypeEditor.html) and [BaseTypeEditor](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.BaseTypeEditor.html) interfaces. 

The [`Create`](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.ITypeEditor.html#Syncfusion_Windows_PropertyGrid_ITypeEditor_Create_System_Reflection_PropertyInfo_) method in the custom editor class can be used to create and assign the required editor controls for specific property items. The Create method's PropertyInfo parameter allows users to customize the editor control based on the value of [`PropertyInfo`](https://docs.microsoft.com/en-us/dotnet/api/system.reflection.propertyinfo?view=net-5.0) class.

{% tabs %}
{% highlight C# %}

public object Create(PropertyInfo propertyInfo)
{
    textBox = new IntegerTextBox();
    if (propertyInfo.Name == "Age")
    {
        textBox.MinValue = 20;
        textBox.MaxValue = 50;
    }
    if (propertyInfo.CanWrite)
        textBox.ShowSpinButton = true;
    
    return textBox;
}

{% endhighlight  %}
{% endtabs %}

![WPF PropertyGrid custom editor Create method](Editor_images/propertygrid_create_method.png)

N> If a [CustomEditor](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.CustomEditor.html) class is inherited from [BaseTypeEditor](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.BaseTypeEditor.html) interface, the Create method will have [`PropertyDescriptor`](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.propertydescriptor?view=net-5.0) parameter value which can be used as per requirement.

## Attach the custom editor with property item
The [`PropertyGrid`](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid) control control allows users to bind the essential properties of the custom editor control with the properties of the property items using the [`Attach`](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.ITypeEditor.html#Syncfusion_Windows_PropertyGrid_ITypeEditor_Attach_Syncfusion_Windows_PropertyGrid_PropertyViewItem_Syncfusion_Windows_PropertyGrid_PropertyItem_) method. You can also customize the property items using the [PropertyItem](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.PropertyItem.html) and [PropertyViewItem](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.PropertyViewItem.html) using the parameters in the `Attach` method.

{% tabs %}
{% highlight C# %}

public void Attach(PropertyViewItem property, PropertyItem info)
{
    if (info.CanWrite)
    {
        property.FontFamily = new FontFamily("Comic Sans MS");
        var binding = new Binding("Value")
        {
            Mode = BindingMode.TwoWay,
            Source = info,
            ValidatesOnExceptions = true,
            ValidatesOnDataErrors = true
        };
        BindingOperations.SetBinding(textBox, IntegerTextBox.ValueProperty, binding);
    }
}

{% endhighlight  %}
{% endtabs %}

![WPF PropertyGrid custom editor Attach method](Editor_images/propertygrid_attach_method.png)

## Dispose the custom editor
The [`PropertyGrid`](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid) control control allows you to dispose the custom editor control and it's dependent properties in CustomEditor class by using the [`Detach`](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.ITypeEditor.html#Syncfusion_Windows_PropertyGrid_ITypeEditor_Detach_Syncfusion_Windows_PropertyGrid_PropertyViewItem_) method. You can also dispose the [PropertyViewItem](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PropertyGrid.PropertyViewItem.html) which will be available from the parameter of `Detach` method.

{% tabs %}
{% highlight C# %}

public void Detach(PropertyViewItem property)
{
    if (property != null && this.textBox != null)
    {
        this.textBox = null;
        property.Dispose();
        property = null;
    }
}

{% endhighlight  %}
{% endtabs %}
