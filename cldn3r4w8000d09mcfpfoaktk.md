# Breathe Life Into Your Data

Any chart, on its own, can be pretty boring and lifeless. This can lead to the reader not understanding your point. They need a splash of color or an explosion of size to start taking shape and bring understanding. In Vega-Lite, much of the look and feel of any graphic comes from adding data to channels. Doing this will breathe life into your data and help give it some shape. Great…but what are channels?

[Channels](https://vega.github.io/vega-lite/docs/encoding.html#channel-definition) are the visual properties of a chart (like size, shape, and color) you [encode](https://vega.github.io/vega-lite/docs/encoding.html) with your data. Said another way, channels are where you can customize your chart with your data. To aid you in this task, Vega-Lite provides you with numerous channels to use for chart creation.

In this chapter we will go over encoding data points in charts, to assist in communicating a more specific visual narrative, through manipulating channels, specifically:

To run these examples you will need to install the following Elixir packages:

* explorer
    
* vega\_lite
    
* kino
    
* kino\_vega\_lite
    

The typical code structure for a chart can be automated using Smart Charts in Elixir

![](https://user-images.githubusercontent.com/28072958/216326987-b7181661-dc9c-4061-8883-6922fe99b309.gif align="left")

This will leave you with the following chart:

![](https://user-images.githubusercontent.com/28072958/216327019-da47c7e9-c5bd-47fb-b1ab-d2f42be8e258.png align="left")

In this section, you will be focusing on changing the following line of code below that needs to be added to the template above:

...where the XXXX above is used to encode channels (i.e. Shape, Opacity, etc.).

> Note: Other types of marks can be found [here](https://vega.github.io/vega-lite/docs/mark.html#types)

## 1) Color

Smart Cells are a great way to create charts with minimal effort.  Once created, you can convert them to code to further customize.  The Chart Smart Cell is what you'll use below to color the `mpg` dataset by `class`.

![](https://user-images.githubusercontent.com/28072958/216327043-17657371-e245-4af0-b2a7-4c1ddb5fa88f.gif align="left")

Converting the above smart cell Chart will leave you with the following code:

```javascript
Vl.new(width: 400, title: "Color by Class")
|> Vl.data_from_values(mpg, only: ["displ", "hwy", "class"])
|> Vl.mark(:point)
|> Vl.encode_field(:x, "displ", type: :quantitative)
|> Vl.encode_field(:y, "hwy", type: :quantitative)
|> Vl.encode_field(:color, "class", type: :nominal)
```

![](https://user-images.githubusercontent.com/28072958/216327067-987762e1-16b3-4b5b-832b-38af6c445b58.png align="left")

There can also be times when you need to change all of the data points to a single color (i.e."black").  To do so, you will need to change the following line of code from...

```javascript
|> Vl.encode_field(:color, "class", type: :nominal)
```

...to

```javascript
|> Vl.encode(:color, value: "black")
```

Your code should now look like the code below.

```javascript
Vl.new(width: 400, title: "Color All Points Black")
|> Vl.data_from_values(mpg, only: ["displ", "hwy", "class"])
|> Vl.mark(:point)
|> Vl.encode_field(:x, "displ", type: :quantitative)
|> Vl.encode_field(:y, "hwy", type: :quantitative)
|> Vl.encode(:color, value: "black")
```

![](https://user-images.githubusercontent.com/28072958/216327079-43cef8ac-dd5e-4cb7-ab83-935a9228adb7.png align="left")

> Note: `Vl.encode_field` is changed to `Vl.encode()`.  The "\_field," part of the code is shorthand for the encode function that uses the field parameter. Since we are not using a field from the dataset to color the points black part of the code ("\_field") is not helpful. Use the more generic encode function by removing the "\_field," as shown above.  You can read more about it in the [documentation](https://hexdocs.pm/vega_lite/VegaLite.html#encode_field/4).

To create filled-in circles as opposed to hollow circles simply change the `:point` mark to `:circle`.  Your code will then look like this.

```javascript
Vl.new(width: 400, title: "Color Fill All Points Black")
|> Vl.data_from_values(mpg, only: ["displ", "hwy", "class"])
|> Vl.mark(:circle)
|> Vl.encode_field(:x, "displ", type: :quantitative)
|> Vl.encode_field(:y, "hwy", type: :quantitative)
|> Vl.encode(:color, value: "black")
```

![](https://user-images.githubusercontent.com/28072958/216327098-bd4eafea-d57f-47f9-8c97-c17358c486ff.png align="left")

## 2) Shape

Working from the chart created with the Smart Cells, you can change the `:shape` instead of `:color` by changing one line of code.  Change

```javascript
|> Vl.encode_field(:color, "class", type: :nominal)
```

to

```javascript
|> Vl.encode_field(:shape, "class", type: :nominal)
```

Your code should match the code below.

```javascript
Vl.new(width: 400, title: "Shape")
|> Vl.data_from_values(mpg, only: ["displ", "hwy", "class"])
|> Vl.mark(:point)
|> Vl.encode_field(:x, "displ", type: :quantitative)
|> Vl.encode_field(:y, "hwy", type: :quantitative)
|> Vl.encode_field(:shape, "class", type: :nominal)
```

![](https://user-images.githubusercontent.com/28072958/216329155-8f28a7e8-56e1-491c-a241-8579c59eb6b6.png align="left")

> Note: While there are many mark types to choose from, you must use the `:point` mark when encoding the `:shape`channel.

## 3) Size

Next up is Size. The only needed change, again, is the last line of code. You are removing `:shape` and replacing that with `:size`.

```javascript
Vl.new(width: 400, title: "Size")
|> Vl.data_from_values(mpg, only: ["displ", "hwy", "class"])
|> Vl.mark(:point)
|> Vl.encode_field(:x, "displ", type: :quantitative)
|> Vl.encode_field(:y, "hwy", type: :quantitative)
|> Vl.encode_field(:size, "class", type: :nominal)
```

![](https://user-images.githubusercontent.com/28072958/216327172-63e6e7f4-d251-4251-90c3-fc1f27c4c3fc.png align="left")

Again, to change the data points to filled vs. hollow circles, change the mark from `:point` to :`circle`.

```javascript
Vl.new(width: 400, title: "Size With Solid Points")
|> Vl.data_from_values(mpg, only: ["displ", "hwy", "class"])
|> Vl.mark(:circle)
|> Vl.encode_field(:x, "displ", type: :quantitative)
|> Vl.encode_field(:y, "hwy", type: :quantitative)
|> Vl.encode_field(:size, "class", type: :nominal)
```

![](https://user-images.githubusercontent.com/28072958/216327189-d2bc7e47-12a5-4ad9-bad4-eb9d0cd0634a.png align="left")

## 4) Opacity

You may have noticed that Vega\_lite defaults to include opacity in all of the exercises we have already completed. However, you can specify opacity in the last line of code, substituting `:size` for `:opacity`.

```javascript
Vl.new(width: 400, title: "Opacity")
|> Vl.data_from_values(mpg, only: ["displ", "hwy", "class"])
|> Vl.mark(:point)
|> Vl.encode_field(:x, "displ", type: :quantitative)
|> Vl.encode_field(:y, "hwy", type: :quantitative)
|> Vl.encode_field(:opacity, "class", type: :nominal)
```

![](https://user-images.githubusercontent.com/28072958/216327212-25326bf9-63ce-41ba-9382-b1c3abf0b633.png align="left")

## 5) Conditional Encoding

### How does conditional formatting work?

Vega-Lite’s conditions may look a little different but are simple if-then statements. Each [condition](https://vega.github.io/vega-lite/docs/condition.html) has a test, a value and a default value. The test checks to see if a condition is true. If it is, then the value is applied. Otherwise, apply the default value.

Looking at the Opacity chart above it appears that there are outliers in the dataset. If you look at the X and Y axis the outliers are grouped where: the y-axis is greater than 20 and the x-axis is greater than 5.

To visually show the outliers you can isolate them by changing colors, shape, size, etc. Let's try to isolate the outliers using color

```javascript
Vl.new(width: 400, title: "Conditional Encoding")
|> Vl.data_from_values(mpg, only: ["hwy", "displ", "class"])
|> Vl.mark(:circle)
|> Vl.encode_field(:y, "hwy", type: :quantitative)
|> Vl.encode_field(:x, "displ", type: :quantitative)
|> Vl.encode(:color,
  condition: %{test: "datum['hwy'] > 20 & datum['displ'] > 5", value: "red"},
  value: "black"
)
```

![](https://user-images.githubusercontent.com/28072958/216327231-fdb88612-5a42-4a11-8ed4-9b3a22377502.png align="left")

One thing to notice in the code above is the use of the datum variable in your conditional test.

The datum variable represents a row in your dataset passed into VegaLite. You can access any column within the row by typing datum\[column\_name\]. [datum](https://vega.github.io/vega-lite/docs/datum.html) is commonly used in conditional encoding to specify a constant instead of a variable. It can be used anywhere you need to change how a column is handled based on its value. You'll see it used more throughout other Data Visualization sections.

## Wrapping Up

Encoding channels with your data is what brings life to the charts you make. Channels provide you the flexibility to customize to your heart's content and to help your users better understand the story you’re sharing with them. Even though you covered seven different scenarios, you only just scratched the surface of all the different channels that Vega-Lite makes available to you. Check them out and start experimenting to see what you can come up with.

In the next section, you’ll learn how to use VegaLite to [transform](https://vega.github.io/vega-lite/docs/transform.html) data.