---
title: Overview
page_title: MultiColumnComboBox Overview
description: Discover the Blazor MultiColumnComboBox and explore the examples.
slug: multicolumncombobox-overview
tags: telerik,blazor,multicolumncombobox,combo,columns,overview
published: True
position: 0
---

# Blazor MultiColumnComboBox Overview

The <a href="https://www.telerik.com/blazor-ui/multicolumn-combobox" target="_blank">Blazor MultiColumnComboBox</a> allows the user to choose an option from a [predefined set of choices]({%slug multicolumncombobox-data-binding%}) in a dropdown grid structure. You can also allow them to enter [custom values]({%slug multicolumncombobox-custom-value%}), [filter]({%slug multicolumncombobox-filter%}) the available items, and [group]({%slug multicolumncombobox-group%}) the listed items in common categories. 

## Creating MultiColumnComboBox

1. Use the `TelerikMultiColumnComboBox` tag to add the component to your razor page.
1. Populate the `Data` property with the collection of items that you want to appear in the dropdown.
1. Set the `TextField` and `ValueField` properties to point to the corresponding names of the model
1. [Bind the value of the component]({%slug get-started-value-vs-data-binding %}#value-binding) to a variable of the same type as the type defined in the `ValueField` parameter.
1. Add `MultiColumnComboBoxColumn` instances under the `MultiColumnComboBoxColumns` tag. Each column, the `Field` must point to a property in the bound model property. Use `nameof()` or the plain field name.

>caption MultiColumnComboBox data binding with two-way value binding

````CSHTML
Selected value: @BoundValue
<br />

<TelerikMultiColumnComboBox Data="@MultiComboData"
                            @bind-Value="@BoundValue"
                            ValueField="@nameof(SampleData.Id)"
                            TextField="@nameof(SampleData.Name)">
    <MultiColumnComboBoxColumns>
        <MultiColumnComboBoxColumn Field="@nameof(SampleData.Id)" Title="The id" ></MultiColumnComboBoxColumn>
        <MultiColumnComboBoxColumn Field="@nameof(SampleData.Name)" Title="The name"></MultiColumnComboBoxColumn>
    </MultiColumnComboBoxColumns>
</TelerikMultiColumnComboBox>

@code {
    public int BoundValue { get; set; }

    public List<SampleData> MultiComboData { get; set; } = Enumerable.Range(0, 30).Select(x => new SampleData()
    {
        Id = x,
        Name = "Name " + x
    }).ToList();

    public class SampleData
    {
        public int Id { get; set; }
        public string Name { get; set; }
    }
}
````

## Component Reference

The MultiColumnComboBox is a generic component and its type is determined by the type of the model you pass to it, and the type of its value field. You can find examples in the [Data Bind - Considerations]({%slug multicolumncombobox-data-binding%}#considerations) article.

## Data Binding

The Blazor MultiColumnComboBox @[template](/_contentTemplates/dropdowns/features.md#data-binding) [Read more about the Blazor MultiColumnComboBox data binding...]({% slug multicolumncombobox-data-binding %}).

## Columns

The Blazor MultiColumnComboBox allows you to define one or more columns in the dropdown. [Read more about the Blazor MultiColumnComboBox columns...]({%slug multicolumncombobox-column-overview%})

## Filtering

The Blazor MultiColumnComboBox @[template](/_contentTemplates/dropdowns/features.md#filtering) [Read more about the Blazor ComboBox filter...]({% slug multicolumncombobox-filter %}).

## Grouping

The Blazor MultiColumnComboBox @[template](/_contentTemplates/dropdowns/features.md#grouping) [Read more about the Blazor MultiColumnComboBox grouping...]({% slug multicolumncombobox-group %}).

## Templates

@[template](/_contentTemplates/dropdowns/features.md#templates) [Read more about the Blazor MultiColumnComboBox templates...]({% slug multicolumncombobox-templates %}).

## Validation

@[template](/_contentTemplates/dropdowns/features.md#validation)

## Virtualization

@[template](/_contentTemplates/dropdowns/features.md#virtualization) [Read more about the Blazor MultiColumnComboBox virtualization...]({% slug multicolumncombobox-virtualization %})


## Parameters

>caption The MultiColumnComboBox provides various parameters that allow you to configure the component:

<style>
    article style + table {
        table-layout: auto;
        word-break: normal;
    }
</style>
| Parameter      | Type | Description
| ----------- | ----------- | -----------|
| `AllowCustom` | `bool` | whether the user can enter [custom values]({%slug multicolumncombobox-custom-value%}). If enabled, the `ValueField` must be a `string`.
| `ClearButton` | `bool` | whether the user will have the option to clear the selected value. When it is clicked, the `Value` will be updated to `default(TValue)`, so there must be no item in the `Data` that has such a `Value`. For example, if `TValue` is `int`, clearing the value will lead to a `0` `Value`, so if there is an Item with `0` in its `ValueField` - issues may arise with its selection. This feature can often go together with `AllowCustom`.
| `Data` | `IEnumerable<TItem>` | allows you to provide the data source. Required.
| `DebounceDelay` | `int` <br/> 150 | Time in milliseconds between the last typed symbol and the internal `oninput` event firing. Applies when the user types and filters. Use it to balance between client-side performance and number of database queries.
| `Enabled` | `bool` | whether the component is enabled.
|`Filterable` | `bool` | whether [filtering]({% slug multicolumncombobox-filter %}) is enabled for the end user.
| `FilterOperator` | `StringFilterOperator` <br /> (`StartsWith`) | the method of [filtering]({% slug multicolumncombobox-filter %}) the items.
| `Id` | `string` | renders as the `id` attribute on the `<input />` element, so you can attach a `<label for="">` to the input.
| `Placeholder` | `string` | the text the user sees as a hint when no item is selected. In order for it to be shown, the `Value` parameter should be set to a default value depending on the type defined in the `ValueField` parameter. For example, `0` for an `int`, and `null` for an `int?` or `string`. You need to make sure that it does not match the value of an existing item in the data source.
| `TItem` | `Type` | the type of the model to which the component is bound. Required if you can't provide `Data` or `Value`. Determines the type of the reference object.
| `TValue` | `Type` | the type of the value field from the model to which the component is bound. Required if you can't provide `Data` or `Value`. Determines the type of the reference object. The type of the values can be:<br /> - `number` (such as `int`, `double`, and so on)<br /> - `string`<br /> - `Guid`<br /> - `Enum`|
| `TextField` | `string` <br /> (`Text`)| the name of the field from the model that will be shown to the user.
| `ValueField` | `string` <br /> (`Value`) | the name of the field from the model that will be the underlying `value`.
| `Value` and `bind-Value` | `TValue` | get/set the value of the component, can be used for binding. If you set it to a value allowed by the model class value field, the corresponding item from the data collection will be pre-selected. Use the `bind-Value` syntax for two-way binding, for example, to a variable of your own.
| `TabIndex` | `int?` | maps to the `tabindex` attribute of the HTML element. You can use it to customize the order in which the inputs in your form focus with the `Tab` key.

### Styling and Appearance

The following parameters enable you to customize the appearance of the Blazor MultiColumnComboBox:

@[template](/_contentTemplates/dropdowns/features.md#styling)

You can find more options for customizing the MultiColumnComboBox styling in the [Appearance article]({%slug multicolumncombobox-appearance%}).


### Popup settings

The popup of the component can be additionally customized via nested tags:

````
<div class="skip-repl"></div>
<TelerikMultiColumnComboBox>
    <MultiColumnComboBoxSettings>
        <MultiColumnComboBoxPopupSettings Height="..." />
    </MultiColumnComboBoxSettings>
</TelerikMultiColumnComboBox>
````

The MultiColumnComboBox provides the following popup settings:

@[template](/_contentTemplates/dropdowns/features.md#popup-settings)


## Selected Item

By default, if no `Value` is provided, the MultiColumnComboBox will appear empty, or will display the `Placeholder` defined. If a `Value` is provided and `AllowCustom` is *not* set to `true`, the `Value` should match an item in the data source (see more in the [Value Out of Range]({%slug multicolumncombobox-data-binding%}#value-out-of-range) section. 

The MultiColumnComboBox will not always have a selected item, however, because it can act as an input. There will be no selected item in the following cases that depend on the settings of the component that the developer can control:

* the user clears the value through the Clear button,
* the user clears the value with `Backspace` or `Del` keys,
* `AllowCustom="false"` - when a custom value is typed, the MultiColumnComboBox input value will be automatically cleared on the change event (`blur` of the input or `Enter` keypress). See the table below.
* `AllowCustom="true"` - when the user starts typing a custom value.


Missing selection is most common when the initial value is `null` as data sources rarely have items with a `null` value, and/or when you want to let your users type in values that are not in your predefined set of options.

>caption If the user types text in the input, selection behaves according to the following table:


| User input matches | AllowCustom=`true`   | AllowCustom=`false`                      |
|----------------------------|----------------------|------------------------------------------|
|  The `TextField` of an item | Matched item is selected. The `Value` is taken from the item. | Matched item is selected. The `Value` is taken from the item. |
| The `ValueField` of an item | No item is selected. `Value` is updated to the custom one. | No item is selected. `Value` is updated to `default(typeof(Value))`. The `OnChange` event does not fire for the value clearing. |
| No match | No item is selected. `Value` is updated to the custom one. | No item is selected. `Value` is updated to `default(typeof(Value))`. The `OnChange` event does not fire for the value clearing. |


@[template](/_contentTemplates/common/get-model-from-dropdowns.md#get-model-from-dropdowns)

## Next Steps

* [Binding the MultiColumnComboBox to Data]({%slug multicolumncombobox-data-binding%})

## See Also

  * [Data Binding]({% slug multicolumncombobox-data-binding %})
  * [Live Demo: MultiColumnComboBox](https://demos.telerik.com/blazor-ui/multicolumncombobox/overview)
  * [Live Demo: MultiColumnComboBox Validation](https://demos.telerik.com/blazor-ui/multicolumncombobox/validation)
