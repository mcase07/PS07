Distribution of the Majors at Smith College
================

## Smih Majors Data Set

The data for these plots comes from the Smith Common Data Set provided
by the College. The data used is from the years 2020-21. The first plot
uses data about the divisions of majors[1] and the second plor uses data
about the distribution of the top five majors[2].

This is an R Markdown format used for publishing markdown documents to
GitHub. When you click the **Knit** button all R code chunks are run and
a markdown file (.md) suitable for publishing to GitHub is generated.

## Creating a New Data Set and Wrangling

Taking information from the Smith Common Data Set and turning it into
two data sets:

``` r
major <- c("Social Science", "Computer and information sciences", "Area, ethnic, and gender studies", 
           "Engineering", "Foreign languages, literatures, and linguistics", "English", 
           "Biological/life sciences", "Mathematics and statistics", "Physical sciences", 
           "Psychology", "Visual and performing arts", "History", "Natural resources and conservation", 
           "Education", "Interdisciplinary", "Philosophy and religious studies", "Architecture")
percentage <- c(14.99, 6.31, 7.67, 5.52, 5.64, 5.41, 12.18, 4.96, 5.86, 
                7.22, 7.55, 2.71, 3.04, 2.37, 5.64, 2.03, 0.9)

major_division <- c("Humanities", "Social Science", "Natural Science", "Interdivisional/Self-Designed")
division_percentage <- c(23, 18, 42, 17)

# Creating a new data frame of the top 5 majors
smith_major.data <- data.frame(major, percentage) %>% 
  arrange(desc(percentage))

# Creating a new data frame of major divisions
smith_major_division.data <- data.frame(major_division, division_percentage)
```

Wrangling the top five majors at Smith!

``` r
# taking the top 5 majors
smith_major_top <- smith_major.data %>%
   top_n(n = 5, wt = percentage)
```

## Barplots Illustrating the Data

Barplot of the distribution of students in the four divisions of majors
at the time of graduation:

``` r
ggplot(data = smith_major_division.data, aes(fct_reorder(major_division,
                                                         division_percentage),
                                             division_percentage,
                                             fill = major_division)) + 
                                             
  geom_col() +
  labs(title = "Distribution of the major divisions at Smith College", 
       x = "major division", 
       y = "% of students in major division") +
  scale_fill_brewer(palette = "OrRd",
                    name = "Major divisions") +
  theme(axis.text.x = element_blank())
```

![](README_files/figure-gfm/division_plot-1.png)<!-- -->

Barplot of the distribution of students in the top five majors awarded:

``` r
ggplot(data = smith_major_top, aes(x = major, 
                                   y = percentage, 
                                   fill = major)) + 
  geom_col() +
  labs(title = "Distribution of the majors at Smith College",
       subtitle = "Includes top 5 majors",
       x = "major",
       y = "% of students majoring") +
  scale_fill_brewer(palette = "YlGnBu") +
  theme(axis.text.x = element_blank())
```

![](README_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

[1] via
<https://www.smith.edu/sites/default/files/media/Documents/Registrar/MAJORSatGraduation.pdf>

[2] via
<https://www.smith.edu/sites/default/files/media/Smith_CDS_2020-2021_update%204-7-21.pdf>
