# Storytelling With Elixir

## What is Data Visualization?

Storytelling is at the heart of Data Visualization. Regardless of the type of information or data, there is always a tale to tell. Thus, Data Visualization could be defined as the art of using graphics encoded with data to convey some unseen insight or understanding. Below are a few examples of types of visualizations you might create.

* [Outliers](https://observablehq.com/@rreusser/online-outlier-detection) — Outliers identify data that is outside the "norm" of what you'd expect to see.  Using different colors is a great way to highlight potential outlier data points.
    

![](https://user-images.githubusercontent.com/28072958/215350976-8a7bf0b5-c83e-424f-99b4-201ca9f5a3b5.png align="left")

* [Trends or Relationships](https://vega.github.io/vega-lite/examples/layer_point_line_regression.html) — Regressions lines (red below) help the reader understand how strong or weak the relationship between two variables is.
    

![](https://user-images.githubusercontent.com/28072958/215350982-d725a0d3-d244-40ac-a172-7ca9dfad5f7d.png align="left")

* [Groups or Clusters](https://vega.github.io/vega-lite/examples/geo_circle.html) - Clusters help you identify sub-groups within your datasets.  Color can provide clarity where you may not have seen it before by showing how information is grouped.
    

![](https://user-images.githubusercontent.com/28072958/215350985-446c856d-f558-4ae1-857b-b08a87c77a8b.png align="left")

* [Rankings](https://observablehq.com/@jlmborges/rank-plot_vega-lite) — Line charts can be used to help show how the order of data may change over time.
    

![](https://user-images.githubusercontent.com/28072958/215350999-1479d087-e3d1-45bd-95e9-cf6ed8d5bcb3.png align="left")

* [Interactions](https://vega.github.io/vega-lite/examples/interactive_layered_crossfilter.html) — Interactivity is a great way to allow your end user to engage with the data and ask their questions.
    

![](https://user-images.githubusercontent.com/28072958/215351010-d9cbda4c-68b5-49a4-8a9a-7336a36165a8.mp4 align="left")

## What is the purpose of Data Visualization?

Visualizing data is built around the idea of simplifying the complex. Have you ever tried explaining how something technical works to anyone else? It rarely goes well. The best way to share your technical idea with anyone else is by creating a visual representation of what you’re describing, so it’s easier for their brains to digest it. We’re trying to convey ideas and if they don’t get it, then you’ve missed an opportunity to share what you’ve learned. A picture, or in this case, a chart, is worth a thousand words.

## How does Data Visualization fit within Data Science?

While it may appear that Data Visualization primarily falls within the Communicate section of the Data Science flow diagram in [R4DS](https://r4ds.had.co.nz/introduction.html) (seen below), it is used throughout the whole process. The only different thing is the audience. You will want to see what you are doing along the way, while your end user will typically care about the end product.

![](https://user-images.githubusercontent.com/28072958/215351711-cd803135-6791-4a96-8524-e6dfd28db315.png align="left")

Below are 3 scenarios for visualizing data throughout the Data Science process.

1). Before we can build cool charts, we must first get familiar with our data. Below are a few questions you may need to answer first:

1. How many blanks or nulls are in each column?
    
2. What types are in a particular column (i.e., string, int, float, etc…)?
    
3. What data is missing?
    
4. Is there enough data in a column to even use it?
    

2). When you’re working with models, you will want to see how well the models represent the data. Below are 2 different types of regressions that work slightly differently.

* Linear Regression
    

![](https://user-images.githubusercontent.com/28072958/215351037-7ffda771-7a67-4a79-a745-953dad9e781f.png align="left")

* Loess Regression
    

![](https://user-images.githubusercontent.com/28072958/215351047-15668465-312b-4642-b713-cd586684ba20.png align="left")

3). After you’ve selected a model, you will want to know how well it is performing at predicting future events.

1. For regressions, you may want the R2, as shown in the linear regression above.
    
2. For classification, you may want to see the ROC (Receiver Operating Characteristic) curve.
    

![](https://user-images.githubusercontent.com/28072958/215351077-d2f81c5e-f2b8-4f3c-be2b-4a41cf30cd13.png align="left")

## What library are we going to use?

As we move forward, we’ll be using the Vega-Lite library to create all our charts and graphics. Vega-Lite describes itself as “A High-Level Grammar of Interactive Graphics”. What does that mean? Let’s break it down into 3 sections.

1). What is High-Level?

High-level is in relation to Vega or D3.js. Both are libraries that Vega-Lite is built upon. The “level” refers to the detail and code needed to generate a graph. Vega-Lite requires far less code than either of the other libraries.

2). What is the "Grammar of Graphics"?

It is a framework to approach the creation of graphics by breaking every chart down into its most basic building blocks. The framework was originally popularized by Leeland Wilkinson in his book titled “The Grammar of Graphics”.

Below is an image depicting the primary layers used to create a chart using the Grammar of Graphics framework.

![](https://user-images.githubusercontent.com/28072958/215351148-81bf730d-f8ae-44fa-a2be-c893e406ad90.jpeg align="left")

The benefit here is that instead of describing how to create your chart (i.e., calculating where to position each element). You describe what you want to see. Simply pass the data and tell the framework what to visualize. For example, there is no need to figure out how to calculate different coordinate types.

* [Linear](https://vega.github.io/vega-lite/examples/point_color_with_shape.html)
    

![](https://user-images.githubusercontent.com/28072958/215351156-d0c9218f-8639-4f45-8edc-525196c5ce97.png align="left")

* [Circular](https://vega.github.io/vega-lite/examples/arc_radial.html)
    

![](https://user-images.githubusercontent.com/28072958/215351174-2085ac5f-d279-45f6-8ac7-d37ebe0eab87.png align="left")

* [Map](https://vega.github.io/vega-lite/examples/geo_choropleth.html)
    

![](https://user-images.githubusercontent.com/28072958/215351185-dcbdbf43-c5a8-4dfc-98ee-69cb0fc6c7a6.png align="left")

3). What About Interactivity?

The Vega-Lite team has extended the original Grammar of Graphics to include a layer for interactivity. They define their building blocks for interaction as [Parameters](https://vega.github.io/vega-lite/docs/parameter.html). Parameters can be either simple variables that change a specific feature or complex selections as shown below.

* Simple Variable
    

![](https://user-images.githubusercontent.com/28072958/215351197-c18e7fdb-19e6-4206-849b-6eb83196e6de.mp4 align="left")

* Complex Selection
    

![](https://user-images.githubusercontent.com/28072958/215351206-11d8ac64-d666-4c02-982f-eab1e40f7bc1.mp4 align="left")

5 of the most common building blocks you’ll use in VegaLite are:

1. Data — Read information in
    
2. Scales — Transform the data into the right domain
    
3. Axes — Define the lines, ticks, and labels
    
4. Legends — Provide context to the visuals
    
5. Marks — Specify the shape to be displayed
    

## How do you get started?

Before you can get started, you will need to first install a few packages for Elixir.

* VegaLite — Create charts
    
* Kino\_Vega\_Lite — Makes VegaLite render in Livebook
    
* Kino — Interactive Livebook widgets
    
* Explorer — Manipulate and clean data with DataFrames
    

With Livebook, installation is simple. All you need to do is search for the packages you want and click the “Setup” button to install them.

![](https://user-images.githubusercontent.com/28072958/215351227-0d1fdc00-2f6c-4e61-b85b-4080afba67bb.mp4 align="left")

> Note: The [VegaLite](https://hexdocs.pm/vega_lite/VegaLite.html) package is a simple wrapper around the original [Vega-Lite](https://vega.github.io/vega-lite/) JavaScript library so that the Elixir community didn’t have to re-create it from scratch.

## Wrapping Up

Data Visualization is an important process for simplifying complex ideas and allows us to communicate our findings with others and ourselves. It is not simply for generating reports, but for communication along the whole Data Science process. In the next section, we’ll be looking at how to get started with reading data into Livebook and then making a basic chart.