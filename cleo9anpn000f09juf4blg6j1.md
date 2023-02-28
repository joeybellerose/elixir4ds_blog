# Whittling Down Your Data

It is easy to get distracted by the sheer volume of data you will need to wade through. Most datasets include far more columns than you will end up needing for your analysis. A perfect example of this would be an `id` column. You would rarely want to include this column as part of your modeling effort.

`Select` gives you the ability to choose a subset of columns.  `Select` works for columns in the same way `Filter` works for rows. This step becomes more useful when you are dealing with more than 100 columns or 10s of millions of rows. This has a twofold effect:

1. Being efficient with your computer memory when working with larger datasets.
    
2. Focusing on the information you need to answer the question driving your analysis.
    

# How Can You Keep Columns?

Keeping any list of columns is as simple as using the `select` function.  Start by keeping only the `year`, `month`, and `day` columns.

```javascript
df
|> DataFrame.select(["year", "month", "day"])
```

![](https://user-images.githubusercontent.com/28072958/221857467-5c143835-fcf9-4bd5-8bd9-39dff7d2abf5.png align="left")

> Note: Selecting Single Column – You can pass the name of the column name (e.g., `select("year")`).  Selecting Multiple Columns – You will need to pass a list of column names (e.g., `select(\["year", "month", "day"\])`)

# How Can You Remove Columns?

One useful option for the `select` function is the `keep_or_drop` parameter. By default, this parameter is set to `:keep`, but you can use `:drop` to remove the columns specified as shown in the example below.

Notice how the columns' `year`, `month`, and `day` do not show up in the results.

```javascript
df
|> DataFrame.select(["year", "month", "day"], :drop)
```

![](https://user-images.githubusercontent.com/28072958/221857694-2f655bc8-d63d-4297-84bc-f9bcfd474f52.png align="left")

# How Can You Select Adjacent Columns?

As of the time of this writing, it is not possible to select multiple adjacent columns with the names of the first and last columns like R does (e.g., `year:day`). One workaround is to specify the numbers for the first and last column that you want, as shown below.

```javascript
df
|> DataFrame.select(0..2)
```

![](https://user-images.githubusercontent.com/28072958/221857934-d2c3c831-a91b-45e4-8b7a-6aec43ee864b.png align="left")

...and you can also `:drop` to remove adjacent columns as well.

```javascript
df
|> DataFrame.select(0..2, :drop)
```

![](https://user-images.githubusercontent.com/28072958/221858043-8653f4a0-8492-42c0-88d6-e7bd054ecff0.png align="left")

# How Can You Select With String Functions?

In addition to lists (`\["year", "month", "day"\]`) and ranges (`0..2`), you can use standard Elixir String functions for more flexible ways to `select` columns as shown in the examples below.

1. `String.starts_with` searches all the column names to see which ones **exactly** begin with the letters you supply. Below will find all the column names that start with the letter "d".
    

```javascript
df
|> DataFrame.select(&String.starts_with?(&1, "d"))
```

![](https://user-images.githubusercontent.com/28072958/221858199-9dea003d-a901-438f-9950-660d111e6d51.png align="left")

2\.   `String.ends_with` searches all the column names to see which ones **exactly** end with the letters you supply. Below will find all the columns names that end with the letter "e".

```javascript
df
|> DataFrame.select(&String.ends_with?(&1, "e"))
```

![](https://user-images.githubusercontent.com/28072958/221858270-e25b1c76-990f-45e7-934f-ddb44b645ea6.png align="left")

3\.    `String.contains` searches all the column names to see which ones contain anywhere the letters you supply. Below will find any column name that contains the letter "a".

```javascript
df
|> DataFrame.select(&String.contains?(&1, "a"))
```

![](https://user-images.githubusercontent.com/28072958/221858415-6a733f0f-7d22-41ad-84fe-f936008de2ca.png align="left")

4\.    `String.match` matches the column names based on the regular expression you provide. Below, will show you all the columns that have `_arr` in their name.

```javascript
df
|> DataFrame.select(&String.match?(&1, ~r/_[arr]/))
```

![](https://user-images.githubusercontent.com/28072958/221858475-fa110b82-83f2-46a6-9a4e-c8107727f369.png align="left")

As you can see, there is a lot of flexibility that Elixir natively gives you for selecting columns. But there's even more options that what you've seen above. Refer to check out the Elixir String [docs](https://hexdocs.pm/elixir/1.13/String.html) to see what else you can use.