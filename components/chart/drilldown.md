---
title: Drilldown Charts
page_title: Drilldown Charts
description: The DrillDown Chart feature allows the users to explore hierarchical data by initially displaying summarized information and to "drill down" into specific categories or data points for more detailed insights.
slug: chart-drilldown
tags: telerik,blazor,chart,drill,down,drilldown
published: true
position: 55
---

# DrillDown Charts

The Telerik UI for Blazor Chart supports drilldown functionality for exploring data.

The drilldown function allows users to click on a point (bar, pie segment, etc.) in order to navigate to a different view. The new view usually contains finer grained data about the selected item, like breakdown by product of the selected category.

The view hierarchy can be displayed in a breadcrumb for easy navigation back to previous views.

## Configuring Drilldown Charts

To configure a chart series for drilldown:

1. Prepare the data in the appropriate format. Each series data that will be drilled down should contain a property of type `ChartSeriesDescriptor`. The descriptor includes all the parameters of the `ChartSeries` tag and acts as a container holding information about the series displayed upon user-initiated drilldown.
1. Specify the drilldown field (the `ChartSeriesDescriptor` field) of the series data by using the `ChartSeries.DrillDownField` or `ChartSeriesDescriptor.DrillDownField` property.

````CSHTML
@* Configuring Drilldown Charts *@

<TelerikChart>
    <ChartSeriesItems>
        <ChartSeries Type="ChartSeriesType.Column"
                     Name="Total Sales By Company"
                     Data="@Data"
                     Field="@nameof(CompanyModel.Sales)"
                     CategoryField="@nameof(CompanyModel.Name)"
                     DrilldownField="@nameof(CompanyModel.Details)">
        </ChartSeries>
    </ChartSeriesItems>
</TelerikChart>

@code {
    public List<CompanyModel> Data { get; set; } = new List<CompanyModel>();

    protected override Task OnInitializedAsync()
    {
        Data = GetSeriesData();
        return base.OnInitializedAsync();
    }

    public static List<CompanyModel> GetSeriesData()
    {
        var data = new List<CompanyModel>()
        {
            new CompanyModel()
            {
                Name = "Company A",
                Sales = 100M,
                Details = new ChartSeriesDescriptor()
                {
                    Name = "Company A Sales By Product",
                    Type = ChartSeriesType.Column,
                    Field = nameof(ProductModel.Sales),
                    CategoryField = nameof(ProductModel.Name),
                    Data = new List<ProductModel>()
                    {
                        new ProductModel() { Name = "Product 1", Sales = 10M },
                        new ProductModel() { Name = "Product 2", Sales = 20M },
                        new ProductModel() { Name = "Product 3", Sales = 30M },
                    }
                }
            },
            new CompanyModel()
            {
                Name = "Company B" ,
                Sales = 200M,
                Details = new ChartSeriesDescriptor()
                {
                    Name = "Company B Sales By Product",
                    Type = ChartSeriesType.Column,
                    Field = nameof(ProductModel.Sales),
                    CategoryField = nameof(ProductModel.Name),
                    Data = new List<ProductModel>()
                    {
                        new ProductModel() { Name = "Product 1", Sales = 30M },
                        new ProductModel() { Name = "Product 2", Sales = 20M },
                        new ProductModel() { Name = "Product 3", Sales = 10M },
                    }
                }
            }
        };
        return data;
    }

    public class CompanyModel
    {
        public string Name { get; set; }
        public decimal Sales { get; set; }
        public ChartSeriesDescriptor Details { get; set; }
    }

    public class ProductModel
    {
        public string Name { get; set; }
        public decimal Sales { get; set; }
    }
}

````

## DrillDown Chart Breadcrumb

Optionally you can display a breadcrumb that shows the drilldown levels. To add breadcrumb:

1. Declare a `TelerikChartBreadcrumb` component.
1. Set the `ChartId` parameter of the breadcrumb component. It should match the `Id` of the chart that will be associated with the breadcrumb.

````CSHTML
@* Configuring Drilldown Chart Breadcrumb *@

<TelerikChartBreadcrumb ChartId="@ChartId"></TelerikChartBreadcrumb>

<TelerikChart Id="@ChartId">
    <ChartSeriesItems>
        <ChartSeries Type="ChartSeriesType.Column"
                     Name="Total Sales By Company"
                     Data="@Data"
                     Field="@nameof(CompanyModel.Sales)"
                     CategoryField="@nameof(CompanyModel.Name)"
                     DrilldownField="@nameof(CompanyModel.Details)">
        </ChartSeries>
    </ChartSeriesItems>
</TelerikChart>

@code {
    public const string ChartId = "chart1";

    public List<CompanyModel> Data { get; set; } = new List<CompanyModel>();

    protected override Task OnInitializedAsync()
    {
        Data = GetSeriesData();
        return base.OnInitializedAsync();
    }

    public static List<CompanyModel> GetSeriesData()
    {
        var data = new List<CompanyModel>()
        {
            new CompanyModel()
            {
                Name = "Company A",
                Sales = 100M,
                Details = new ChartSeriesDescriptor()
                {
                    Name = "Company A Sales By Product",
                    Type = ChartSeriesType.Column,
                    Field = nameof(ProductModel.Sales),
                    CategoryField = nameof(ProductModel.Name),
                    Data = new List<ProductModel>()
                    {
                        new ProductModel() { Name = "Product 1", Sales = 10M },
                        new ProductModel() { Name = "Product 2", Sales = 20M },
                        new ProductModel() { Name = "Product 3", Sales = 30M },
                    }
                }
            },
            new CompanyModel()
            {
                Name = "Company B" ,
                Sales = 200M,
                Details = new ChartSeriesDescriptor()
                {
                    Name = "Company B Sales By Product",
                    Type = ChartSeriesType.Column,
                    Field = nameof(ProductModel.Sales),
                    CategoryField = nameof(ProductModel.Name),
                    Data = new List<ProductModel>()
                    {
                        new ProductModel() { Name = "Product 1", Sales = 30M },
                        new ProductModel() { Name = "Product 2", Sales = 20M },
                        new ProductModel() { Name = "Product 3", Sales = 10M },
                    }
                }
            }
        };

        return data;
    }

    public class CompanyModel
    {
        public string Name { get; set; }
        public decimal Sales { get; set; }
        public ChartSeriesDescriptor Details { get; set; }
    }

    public class ProductModel
    {
        public string Name { get; set; }
        public decimal Sales { get; set; }
    }
}
````

## See Also

* [Live Demo: Drilldown Charts](https://demos.telerik.com/blazor-ui/chart/drilldown)