# Statistics and R Cheat Sheet

## Basic R Operations

### Data Types and Structures
```r
# Vectors
x <- c(1, 2, 3, 4, 5)           # Numeric vector
y <- c("a", "b", "c")           # Character vector
z <- c(TRUE, FALSE, TRUE)       # Logical vector

# Matrices
matrix(1:9, nrow = 3, ncol = 3) # 3x3 matrix
rbind(x, y)                     # Combine by rows
cbind(x, y)                     # Combine by columns

# Data Frames
df <- data.frame(
  id = 1:3,
  name = c("John", "Jane", "Bob"),
  score = c(85, 92, 78)
)

# Lists
list_data <- list(
  numbers = 1:5,
  text = "hello",
  df = data.frame(x = 1:3, y = 4:6)
)
```

### Data Import/Export
```r
# Reading data
read.csv("file.csv")
read.table("file.txt", header = TRUE)
read_excel("file.xlsx")         # requires readxl

# Writing data
write.csv(df, "output.csv")
write.table(df, "output.txt")
saveRDS(object, "data.rds")     # Save R object
```

### Data Manipulation (dplyr)
```r
library(dplyr)

# Basic operations
select(df, col1, col2)          # Select columns
filter(df, col1 > 5)            # Filter rows
arrange(df, col1)               # Sort
mutate(df, new_col = col1 * 2)  # Create/modify columns
summarise(df, mean = mean(col1)) # Summarize data

# Grouping operations
df %>%
  group_by(category) %>%
  summarise(
    count = n(),
    mean_val = mean(value),
    sd_val = sd(value)
  )
```

## Descriptive Statistics

### Measures of Central Tendency
```r
# Mean
mean(x)
mean(x, trim = 0.1)             # Trimmed mean
weighted.mean(x, w)             # Weighted mean

# Median
median(x)

# Mode (custom function)
get_mode <- function(x) {
  unique_x <- unique(x)
  unique_x[which.max(tabulate(match(x, unique_x)))]
}

# Summary statistics
summary(x)
fivenum(x)                      # Tukey's five number summary
```

### Measures of Dispersion
```r
# Variance and Standard Deviation
var(x)                          # Variance
sd(x)                          # Standard deviation

# Range
range(x)                       # Min and max
IQR(x)                        # Interquartile range
diff(range(x))               # Range calculation

# Quantiles
quantile(x)                   # Default quantiles
quantile(x, probs = seq(0, 1, 0.1)) # Deciles
```

### Distributions

#### Normal Distribution
```r
# Probability density function
dnorm(x, mean = 0, sd = 1)

# Cumulative distribution function
pnorm(q, mean = 0, sd = 1)

# Quantile function
qnorm(p, mean = 0, sd = 1)

# Random generation
rnorm(n, mean = 0, sd = 1)

# Test for normality
shapiro.test(x)
```

#### Other Common Distributions
```r
# t-distribution
dt(x, df)
pt(q, df)
qt(p, df)
rt(n, df)

# Chi-square distribution
dchisq(x, df)
pchisq(q, df)
qchisq(p, df)
rchisq(n, df)

# F-distribution
df(x, df1, df2)
pf(q, df1, df2)
qf(p, df1, df2)
rf(n, df1, df2)
```

## Inferential Statistics

### Hypothesis Testing
```r
# t-tests
t.test(x)                      # One-sample t-test
t.test(x, y)                   # Two-sample t-test
t.test(x, y, paired = TRUE)    # Paired t-test

# ANOVA
aov(y ~ group)                 # One-way ANOVA
aov(y ~ group1 * group2)       # Two-way ANOVA
TukeyHSD(aov_model)           # Post-hoc test

# Chi-square tests
chisq.test(table(x, y))        # Independence test
chisq.test(x, p = p0)         # Goodness of fit

# Correlation tests
cor.test(x, y)                # Pearson correlation
cor.test(x, y, method = "spearman") # Spearman correlation
```

### Confidence Intervals
```r
# Mean confidence interval
t.test(x)$conf.int

# Proportion confidence interval
prop.test(x, n)$conf.int

# Custom confidence interval
mean(x) + c(-1, 1) * qt(0.975, df = length(x)-1) * sd(x)/sqrt(length(x))
```

## Regression Analysis

### Linear Regression
```r
# Simple linear regression
model <- lm(y ~ x)
summary(model)
coef(model)
confint(model)

# Multiple linear regression
model <- lm(y ~ x1 + x2 + x3)
summary(model)

# Model diagnostics
plot(model)                    # Diagnostic plots
anova(model)                   # ANOVA table
predict(model, newdata)        # Predictions
residuals(model)               # Residuals
```

### Logistic Regression
```r
# Binary logistic regression
model <- glm(y ~ x, family = binomial)
summary(model)

# Predictions
predict(model, type = "response")

# Model evaluation
library(pROC)
roc(y, fitted(model))
```

## Data Visualization

### Base R Graphics
```r
# Scatter plots
plot(x, y)
plot(x, y, type = "l")         # Line plot

# Histograms
hist(x)
hist(x, breaks = 20)

# Box plots
boxplot(x ~ group)

# Bar plots
barplot(table(x))

# Multiple plots
par(mfrow = c(2, 2))          # 2x2 plot layout
```

### ggplot2
```r
library(ggplot2)

# Scatter plot
ggplot(df, aes(x, y)) +
  geom_point()

# Line plot
ggplot(df, aes(x, y)) +
  geom_line()

# Box plot
ggplot(df, aes(group, value)) +
  geom_boxplot()

# Histogram
ggplot(df, aes(value)) +
  geom_histogram()

# Bar plot
ggplot(df, aes(category, value)) +
  geom_bar(stat = "identity")

# Facets
ggplot(df, aes(x, y)) +
  geom_point() +
  facet_wrap(~category)
```

## Time Series Analysis

### Basic Time Series Operations
```r
# Create time series object
ts_data <- ts(x, frequency = 12)

# Decomposition
decompose(ts_data)
stl(ts_data, s.window = "periodic")

# Forecasting (forecast package)
library(forecast)
fit <- auto.arima(ts_data)
forecast(fit, h = 12)
```

## Power Analysis
```r
library(pwr)

# t-test power analysis
pwr.t.test(n = NULL, d = 0.5, 
           sig.level = 0.05, power = 0.8)

# ANOVA power analysis
pwr.anova.test(k = 3, n = NULL, 
               f = 0.25, sig.level = 0.05, 
               power = 0.8)
```

## Machine Learning in R

### Data Preprocessing
```r
# Split data
library(caret)
split <- createDataPartition(y, p = 0.7, list = FALSE)
train <- df[split, ]
test <- df[-split, ]

# Scale features
preproc <- preProcess(train, method = c("center", "scale"))
train_scaled <- predict(preproc, train)

# Handle missing values
library(mice)
imputed_data <- mice(df, m = 5)
```

### Model Building
```r
# Random Forest
library(randomForest)
rf_model <- randomForest(y ~ ., data = train)

# Support Vector Machine
library(e1071)
svm_model <- svm(y ~ ., data = train)

# Cross-validation
ctrl <- trainControl(method = "cv", number = 10)
model <- train(y ~ ., data = train, 
              method = "rf", 
              trControl = ctrl)
```

## Useful R Functions

### Data Cleaning
```r
# Missing values
is.na(x)                      # Check for NA
na.omit(df)                   # Remove NA rows
complete.cases(df)            # Complete cases

# Duplicates
duplicated(df)                # Check duplicates
unique(df)                    # Remove duplicates

# Data type conversion
as.numeric(x)
as.character(x)
as.factor(x)
as.Date(x)
```

### String Operations
```r
library(stringr)
str_length(x)                 # String length
str_trim(x)                   # Remove whitespace
str_split(x, pattern)         # Split string
str_replace(x, pattern, replacement)
```

### Date/Time Operations
```r
library(lubridate)
ymd("2024-01-01")            # Parse date
now()                        # Current time
interval(start, end)         # Time interval
difftime(time1, time2)       # Time difference
```

### Apply Functions
```r
apply(matrix, margin, fun)    # Apply to matrix
lapply(list, fun)            # Apply to list
sapply(list, fun)            # Simplified lapply
tapply(vector, index, fun)    # Apply by group
```
