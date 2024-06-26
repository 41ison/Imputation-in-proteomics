# Imputation for proteomics
Steps to impute multiple columns in a data frame using recursive partitioning and regression trees method implemented in R {dlookr} package

## Important considerations
1. Usually, we have an abundance matrix. Here we are going to use a data frame, so use the `tibble::rownames_to_column()` function to have the id column in your dataset;
2. This strategy is dependent on the {dlookr} package. I'm using the version **dlookr_0.6.3**;
3. You already know something about the missing values in your dataset, that is, whether they are distributed at random or not;
4. It is highly recommended to reduce the sparsity in your data before imputing, regardless of the quality of the method;
5. Please, take a look at the **{dlookr}** R package [documentation](https://choonghyunryu.github.io/dlookr/).

## What our function is doing?
1. We create a list to store the imputed columns;
2. Loop through the columns to be imputed by applying the `dlookr::imputate_na` function from **{dlookr}** package to each column;
3. Return the list with the imputed columns

## Our function to impute multiple columns requires the following arguments:
1. data = a data frame containing the columns to be imputed and the id column;
2. columns = the columns to be imputed. Here we use the column names from the second column to the last one;
   - Here you can use the argument `colnames(your_dataframe)[2:ncol(your_dataframe)]` to iterate over the column names.
4. id_column = the column to be used as id (e.g., gene, protein, phosphosite, etc.);
5. method = the method to be used for imputation. Here we use the **rpart** method, but you can use any other method available in the **{dlookr}** package.

```
imputate_multiple_columns <- function(data, columns,
                                      id_col, method = "rpart") {
  imputation_list <- list()
  for (i in columns) {
    imputation_list[[i]] <- dlookr::imputate_na(data,
                                         i, id_col,
                                         method = method)
  }
  return(imputation_list)
}
```
