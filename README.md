# vaccineproject
A descriptive analysis school vaccinations.
---
title: "Class Exercises"
date: "January 19, 2023"
output:
  word_document: default
  html_document:
    df_print: paged
---

```{r include = FALSE}
knitr::opts_chunk$set(comment = "")
```

# Introduction to R

These exercises are intended to guide you through your first experience with R and RStudio. You will explore a dataset containing vaccination rates for all kindergartners in the state of California from the school year 2011-12. The codebook is also provided for this dataset. Be sure to download the data on your computer. Note, all of the questions below can be answered by writing a line or two of R code.

1. Read in the California vaccination rate `2011-2012 Vaccination Data.csv` data file and save it as a new object called `CA_vacc`.  
HINT: You may save the R Markdown file and data file in the same folder, and then open the Markdown folder from that location. Or, you can specify the file path to the location of where you saved the data file.

```{r}
getwd()
CA_vacc<-read.csv("/Users/sindoos/Downloads/2011-2012_vaccination_data.csv",stringsAsFactors = TRUE)
```

2. Ensure that you have read in the data correctly by looking at the structure of `CA_vacc` using the `str()` function.

```{r}
str(CA_vacc)
```

3. Use the `summary()` and `hist()` functions to understand the distribution of the `uptodate` variable.

```{r}
summary(CA_vacc$uptodate)
hist(CA_vacc$uptodate)
hist(CA_vacc$uptodate_percent)
````

4. Calculate the total number of students that were up-to-date on their vaccines.

```{r}
sum(CA_vacc$uptodate, na.rm = TRUE)
```

5. Find the mean percent of students (across schools) who did not meet all vaccination requirements, and save it as a variable called `mean_cond_pct`. Call this object to output the results in the console window (or R Markdown file).

```{r}
mean_cond_pct <- (CA_vacc$conditional_percent/7327)
head(mean_cond_pct)
summary(mean_cond_pct)
```

6. Use the `table()` function to find the number of schools who reported their vaccination information versus the number of schools who did not report.

```{r}
table(CA_vacc$REPORTED)
```

7. Find the mean rate of kindergartners who received the Hepatitis-B vaccine in Alameda county and the mean rate who received the Polio vaccine in Alameda county.

```{r}
AC_county <- subset(CA_vacc, COUNTY == "ALAMEDA")
mean(AC_county$HEPB [AC_county$ENROLLMENT], na.rm = TRUE)
mean(AC_county$Polio [AC_county$ENROLLMENT], na.rm = TRUE)
```

8. Report the mean rate of kindergartners who received the Hepatitis-B vaccine in private schools versus in public schools for Alameda county.

```{r}
AC_priv <- subset(AC_county, PUBPRIV == "PRIVATE")
AC_pub <- subset(AC_county, PUBPRIV == "PUBLIC")
mean(AC_pub$HEPB [AC_pub$ENROLLMENT], na.rm = TRUE)
mean(AC_priv$HEPB [AC_pub$ENROLLMENT], na.rm = TRUE)
```
