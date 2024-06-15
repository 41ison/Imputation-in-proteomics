# Imputation-in-proteomics
Steps to impute multiple columns in a data frame using recursive partitioning and regression trees method

Important considerations:
  Usually, we have an abundance matrix. Here we are going to use a data frame;
  This strategy is dependent on the {dlookr} package. I'm using the version dlookr_0.6.3;
  You already know something about the missing values in your dataset, that is, whether they are distributed at random or not;
  It is highly recommended to reduce the sparsity before imputing, regardless of the quality of the method.
