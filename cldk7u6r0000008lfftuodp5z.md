# Data Visualization First Steps

## **Introduction**

### **What Is The Goal For This Post?**

The goal for this section is for you to be able to create the same chart from a local data source (csv file on your computer) and an external data source (csv file on the web).

### **What Data Do You Need?**

To get started, you’ll be using the `mpg` dataset which can be found [here](https://vincentarelbundock.github.io/Rdatasets/csv/ggplot2/mpg.csv). If you are unfamiliar with this dataset, you can read the [documentation](https://vincentarelbundock.github.io/Rdatasets/doc/ggplot2/mpg.html) which describes the MPG dataset and gives greater detail as to what each variable is.

Go ahead and download the MPG csv to a folder on your hard drive. It doesn't matter where you put it, just make sure you can get to it. You can then create a variable for the file location. For example:

```elm
mpg_file = "~Documents/data/mpg.csv"
```

## **Reading Local Data**

### **What is a DataFrame?**

Before you can work with your CSV file you will need to know what a DataFrame is. According to Databricks, DataFrames are “a data structure that organizes data into a 2-dimensional table of rows and columns.”. You can consider DataFrames to be a table in a spreadsheet without the GUI. Each column is a variable (or field) and each row is a record (or observation). DataFrames are the fundamental structure that Data Scientists use to work with, transform, and even model data.

### **How Can You Create a DataFrame?**

To work with DataFrames in Elixir, you will need to use the Explorer [package](https://hexdocs.pm/explorer/Explorer.html). Explorer allows you to read data from different formats (e.g., CSV, Text, Parquet, etc…) into a DataFrame for further work. Explorer is built upon the Rust package [Polars](https://pola-rs.github.io/polars-book/user-guide/), which is one of the fastest DataFrame libraries around. Here’s a quick table of stats to show you how Polars compares to many other DataFrame libraries.

![](https://user-images.githubusercontent.com/28072958/215755921-1f9e0715-eabf-4b18-9400-6a0ce173dfc0.png align="left")

> *Note: You can find more Polars benchmarks* [*here*](https://www.pola.rs/benchmarks.html)*.*

The point is, Explorer will give you plenty of horsepower to manipulate, change and edit your data however you see fit by building upon one of the most powerful DataFrame libraries around.

Like with most libraries in Elixir, you will probably want to `alias` in your package, so you don’t have to write `Explorer.DataFrame` or `Explorer.Series` every time. This can be accomplished with the following code:

```elm
alias Explorer.{DataFrame, Series}
```

Explorer makes creating DataFrames simple and straightforward. To create your MPG DataFrame, use the `from_csv!()` function and give it the `mpg_file` variable you created earlier.

```elm
mpg = DataFrame.from_csv!(mpg_file)
```

You should see a Livebook output something like this:

![](https://user-images.githubusercontent.com/28072958/215755943-143d085c-676b-4acf-b2d8-7ba80593948e.png align="left")

If your first column name happens to be blank, it will look like what is highlighted in the red box above. This no-named column is supposed to be the row ID. This shows up blank because Polars (and Explorer) is a column-oriented DataFrame rather than a row-oriented DataFrame where row IDs matter. You can read more about how Polars differs from the “typical” DataFrame libraries like Pandas [here](https://pola-rs.github.io/polars-book/user-guide/coming_from_pandas.html).

Since it is unnecessary going forward, you can add the following code to remove the column.

```elm
mpg =
  DataFrame.from_csv!(mpg_file)
  # Remove old row id column
  |> DataFrame.select([""], :drop)
```

Livebook should now output this:

![](https://user-images.githubusercontent.com/28072958/215755962-30e88ee8-e130-48b5-8d92-8ab26d994823.png align="left")

> *Note: Explorer automatically shows you the number of rows and columns in the top-left corner. For example, the MPG DataFrame above has 234 rows and 11 columns (234 × 11).*

## **Using Smart Cells to Create Plots**

### **What Are Smart Cells?**

Smart Cells are an option for you to create some predefined functionality in Livebook with no code. Where the `Code` button lets you write code and the `Block` button lets us write Markdown, the `Smart` button provides a GUI to create a Smart Cell.

![](https://user-images.githubusercontent.com/28072958/215755984-89490252-e626-4638-8b74-426eb00464c8.png align="left")

Smart Cells can do multiple things like create charts, connect to databases, create maps and generate SQL queries.

![](https://user-images.githubusercontent.com/28072958/215755997-9b200744-550a-4b87-8182-b0e184b852ab.png align="left")

For this use case, you’ll be using the `Chart` option.

### **How Do Smart Cells Work?**

As you begin to dig into the `mpg` DataFrame, say you want to understand the relationship between engine displacement and highway miles per gallon. To accomplish that, you’re going to want to create a Scatterplot that shows `displ` on the x-axis and `hwy` on the y-axis.

To get started, simply click on the `Chart` option is shown below.

![](https://user-images.githubusercontent.com/28072958/215756022-bb4a5ba3-08ab-47f7-be70-ba0a6b195c0f.png align="left")

You should be presented with a form that looks like this:

![](https://user-images.githubusercontent.com/28072958/215756041-b6814063-2a0f-41b1-b957-5a4314253a0a.png align="left")

To create the chart, simply change the x and y fields to `displ` and `hwy` as well as the types to `quantitative`, and click `Evaluate` in the top-left corner to generate the chart.

![](https://user-images.githubusercontent.com/28072958/215756064-3fa28793-189b-458a-b4b9-ad133cac7184.png align="left")

You should now see a chart below your Smart Cell like this:

![](https://user-images.githubusercontent.com/28072958/215756119-e8c9ce43-ff99-43ba-b816-c72b92d3f0dd.png align="left")

### **What Are The Benefits of Smart Cells?**

The beauty of Smart Cells is you don’t need to know anything about creating charts (or even writing Elixir) to start generating great-looking charts. In addition, Smart Cells have these cool buttons, on the top right, that, when clicked, will let you see the underlying code that was generated for you.

![](https://user-images.githubusercontent.com/28072958/215756144-b9c66101-a8a1-4e54-b924-5cbe210de007.mp4 align="left")

Playing around and seeing what code is generated is a great way to start learning how to use the VegaLite library.

> *Note: As of the time of this writing, Smart Cells require that your data must be saved on your computer. There is an* [*issue*](https://github.com/livebook-dev/kino_vega_lite/issues/17) *on the kino\_vega\_lite repository to add external data sources.*

## **Reading External Data**

External data sources are those that are not located directly on your computer. For instance, the R community has an excellent collection of datasets [here](https://vincentarelbundock.github.io/Rdatasets/datasets.html). Each dataset has a link to the CSV file and documentation that describes the data as well as defines what each variable is. For your next step, remake the same chart using the same dataset that is now located externally.

### **Step 0 — Setup**

You already brought VegaLite into your environment in the [last post](https://www.elixir4datascience.com/storytelling-with-elixir/) when you installed it. To save yourself from typing `VegaLite` every time you want to use a function you can `alias` the package as `Vl`. Your code will look like this:

```elm
alias VegaLite, as: Vl
```

### **Step 1 — Find the Data Source**

You’re going to create a variable, `mpg_url`, with the url for the MPG dataset from the collection R datasets mentioned above.

```elm
mpg_url = "https://vincentarelbundock.github.io/Rdatasets/csv/ggplot2/mpg.csv"
```

### **Step 2 — Create a New Chart**

When using VegaLite, the first step is always to define a new chart with the `Vl.new()` function.

> *Note: This is also where you can pass the width and height parameters to define the* `*width*` *and* `*height*` *of the chart.*

For this chart, your code should look like this:

```elm
VL.new()
```

### **Step 3 — Add Data**

Instead of downloading, you can let the VegaLite package handle that for you with the `Vl.data_from_url()` function. All you need to pass the `mpg_url` variable to where the data is hosted. When completed your code for this step should look like this:

```elm
 |> Vl.data_from_url(mpg_url)
```

### **Step 4 — Define the Chart Type**

No chart can be created without specifying the mark type. Marks are used for specifying the shapes to create any chart and can be created with the `Vl.mark()` function. There are a [multitude of marks](https://vega.github.io/vega-lite/docs/mark.html) you can use, but today the `:point` type is what we need. When completed, the code should look like this:

```elm
 |> Vl.mark(:point)
```

### **Step 5 — Encode Data to X**

For any encoding to work properly, you need to specify a variable from your dataset and what type that variable is. It is possible to ignore the type, but you may get some wonky results. This is due to Vega-Lite defaulting to a `:nominal` (string or category) data type. For this example, you want to define x as `displ` and define its data type as `:quantitative`. Your code should look like this:

```elm
|> Vl.encode_field(:x, "displ", type: :quantitative)
```

### **Step 6 — Encode Data to Y**

For Y you can follow the same process as X except that the variable you need to encode is `hwy`. Your code should look like this:

```elm
|> Vl.encode_field(:y, "hwy", type: :quantitative)
```

### **Step 7 — Put It All Together**

That’s it! Because Elixir is a functional language that uses pipes (`\|>`), you simply combine the steps much like you would a baking recipe. The whole thing should look like this:

```elm
Vl.new()
|> Vl.data_from_url(mpg_url)
|> Vl.mark(:point)
|> Vl.encode_field(:x, "displ", type: :quantitative)
|> Vl.encode_field(:y, "hwy", type: :quantitative)
```

> *Note: Elixir uses the pipe operator (*`*\|>*`*) to pass the output of one step to the input of the next step. This saves you from having to create intermediate variable names and makes your code more concise, and readable by showing the transformation of data from top to bottom.*

## **Vega-Lite Template to Follow**

VegaLite has a typical pattern it expects and follows. Below is an example showing the normal “recipe” used to create a chart.

```elm
 Vl.new() # Initialize a Vega-Lite Chart
|> Vl.data_from_*(data) # Read in data
|> Vl.transform() # Manipulate the data - optional
|> Vl.param() # Add interactivity - optional
|> Vl.mark(:mark) # Specify the shape used
|> Vl.encode_field(:var, "field_name", type: :quantitative) # Encode channels (:x, :y, etc...) with specific fields from the dataset
... # encode as many channels as you wish
```

## **Wrapping Up**

Congratulations! You just created your first DataFrame and Chart! Now that you know how to use Smart Cells, you can create great-looking charts without coding. This can be a great way to learn how the library works, and a great starting place to customize further. You finished up by creating your chart from scratch that used an external data source.

In the next section, you’ll learn how to work with encoding different [channels](https://vega.github.io/vega-lite/docs/encoding.html#channels) (i.e., x, y, color, size, etc…) in a chart.