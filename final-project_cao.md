Final Project
================

Introduction

For the past decade, U.S. colleges and universities have been increasing tuition costs at an average rate of 3.2% per year beyond inflation (College Board, 2017), causing a heavier financial burden for Americans than ever before. However, education spending doesn’t rise at the same pace. According to Delta Cost Project data, from 2003 to 2013, the growth rates of median instructional spending per full-time equivalent (FTE) student were much lower than a number of other expenses, such as academic support, student services, and institutional supports, regardless of institutional types.Considering the limited public funding and multiple possible institutional spending pattern, this project is trying to explore if any particular spending strategies would benefit institutions best regarding to its degree production.

Data

This project uses data from the Delta Cost Project Database. Considering the different focuses of different type of institutions, I excluded for-profit and two-year sectors in this project. Also, based on statistical analysis concerns, institutions with 5 or less bachelor degrees per year as well as institutions with less than 100 undergraduates enrolled in total are excluded in the analysis. All institutions with more bachelor degrees produced than the undergraduate enrollment are excluded in the analysis.

Load Data
---------

For the purpose of this project, several new variables are generated. Instead of using actual expenses for each category, share of different expenses are calculated. This aligns with the purpose of finding the most efficient spending strategy. Overall revenue will be included as a control variable in the final regression model. Previous research shows that selectivity is positively related with institutional performance, so it is also calculated to be included in the models. Insitution sizes are calculated according the categories in IPEDS database.

Descriptive Statistics

|      |  Public|  Private|
|------|-------:|--------:|
| 2000 |     459|      885|
| 2001 |     464|      907|
| 2002 |     468|      914|
| 2003 |     472|      926|
| 2004 |     474|      928|
| 2005 |     476|      934|
| 2006 |     474|      932|
| 2007 |     476|      939|
| 2008 |     485|      942|
| 2009 |     486|      939|
| 2010 |     488|      945|
| 2011 |     488|      949|
| 2012 |     487|      952|
| 2013 |     486|      953|
| 2014 |     483|      959|
| 2015 |     482|      959|

|             |  Public|  Private|
|-------------|-------:|--------:|
| 0-999       |     105|     2845|
| 1000-4999   |    1853|     9574|
| 5000-9999   |    2101|     1447|
| 10000-19999 |    1701|      809|
| 20000+      |    1886|      275|

|                                          |  Public|  Private|
|------------------------------------------|-------:|--------:|
| Associate's Colleges                     |       0|      134|
| Research/Doctorate-granting Universities |    2540|     1619|
| Master’s Colleges and Universities       |    3776|     5559|
| Baccalaureate Colleges                   |    1332|     7651|

Associate's Colleges include institutions where all degrees are at the associate's level, or where bachelor's degrees account for less than 10 percent of all undergraduate degrees. Excludes Special Focus Institutions and Tribal Colleges.

Research/Doctorate-granting Universities includes institutions that award at least 20 doctoral degrees per year (excluding doctoral-level degrees that qualify recipients for entry into professional practice, such as the JD, MD, PharmD, DPT, etc.) Excludes Special Focus Institutions and Tribal Colleges.

Master’s Colleges and Universities includes institutions that award at least 50 master's degrees per year. Excludes Special Focus Institutions and Tribal Colleges.

Baccalaureate Colleges includes institutions where baccalaureate degrees represent at least 10 percent of all undergraduate degrees and that award fewer than 50 master's degrees or fewer than 20 doctoral degrees per year. Excludes Special Focus Institutions and Tribal Colleges.

![](final-project_cao_files/figure-markdown_github-ascii_identifiers/Descriptive%20Stats%20Cond1-1.png)![](final-project_cao_files/figure-markdown_github-ascii_identifiers/Descriptive%20Stats%20Cond1-2.png)

    ## Warning: The labeller API has been updated. Labellers taking `variable`and
    ## `value` arguments are now deprecated. See labellers documentation.

![](final-project_cao_files/figure-markdown_github-ascii_identifiers/Descriptive%20Stats%20Cond1-3.png)

Instruction - A functional expense category that includes expenses of the colleges, schools, departments, and other instructional divisions of the institution and expenses for departmental research and public service that are not separately budgeted. Includes general academic instruction, occupational and vocational instruction, community education, preparatory and adult basic education, and regular, special, and extension sessions. Also includes expenses for both credit and non-credit activities. Excludes expenses for academic administration where the primary function is administration (e.g., academic deans). Information technology expenses related to instructional activities are included if the institution separately budgets and expenses information technology resources (otherwise these expenses are included in academic support). Operations and maintenance and interest amounts attributed to the instruction function have been subtracted from the total instructional expenditure amount at FASB reporting institutions. Operations and maintenance amounts (and interest in the aligned form beginning in 2009) attributed to the instruction function have been subtracted from the total amount at public Aligned form reporting institutions.

Academic support - A functional expense category that includes expenses of activities and services that support the institution's primary missions of instruction, research, and public service. It includes the retention, preservation, and display of educational materials (for example, libraries, museums, and galleries); organized activities that provide support services to the academic functions of the institution (such as a demonstration school associated with a college of education or veterinary and dental clinics if their primary purpose is to support the instructional program); media such as audiovisual services; academic administration (including academic deans but not department chairpersons); and formally organized and separately budgeted academic personnel development and course and curriculum development expenses. Also included are information technology expenses related to academic support activities; if an institution does not separately budget and expense information technology resources, the costs associated with the three primary programs will be applied to this function and the remainder to institutional support. Operations and maintenance and interest amounts attributed to the academic support function have been subtracted from the total academic support expenditure amount at FASB reporting institutions. Operations and maintenance amounts (and interest in the aligned form beginning in 2009) attributed to the academic support function have been subtracted from the total academic support expenditure amount at public Aligned Form reporting institutions.

Student services - A functional expense category that includes expenses for admissions, registrar activities, and activities whose primary purpose is to contribute to students emotional and physical well-being and to their intellectual, cultural, and social development outside the context of the formal instructional program. Examples include student activities, cultural events, student newspapers, intramural athletics, student organizations, supplemental instruction outside the normal administration, and student records. Intercollegiate athletics and student health services may also be included except when operated as self - supporting auxiliary enterprises. Also may include information technology expenses related to student service activities if the institution separately budgets and expenses information technology resources(otherwise these expenses are included in institutional support.) Operations and maintenance and interest amounts attributed to the student sevices function have been subtracted from the total student services expenditure amount at FASB reporting institutions. Operations and maintenance (and interest in the aligned form beginning in 2009) amounts attributed to the student services function have been subtracted from the total student services expenditure amount at public Aligned Form reporting institutions.

Institutional support - A functional expense category that includes expenses for the day-to-day operational support of the institution. Includes expenses for general administrative services, central executive-level activities concerned with management and long range planning, legal and fiscal operations, space management, employee personnel and records, logistical services such as purchasing and printing, and public relations and development. Also includes information technology expenses related to institutional support activities. Operations and maintenance and interest amounts attributed to the institutional support function have been subtracted from the total institutional support expenditure amount at FASB reporting institutions. Operations and maintenance amounts (and interest in the aligned form beginning in 2009) attributed to the institutional support function have been subtracted from the total institutional support expenditure amount at public Aligned Form reporting institutions.

    ## Warning: Removed 3517 rows containing non-finite values (stat_boxplot).

    ## Warning: Removed 3691 rows containing non-finite values (stat_boxplot).

    ## Warning: Removed 3474 rows containing non-finite values (stat_boxplot).

    ## Warning: Removed 3581 rows containing non-finite values (stat_boxplot).

![](final-project_cao_files/figure-markdown_github-ascii_identifiers/Descriptive%20Stats%20Cond2-1.png)

    ## TableGrob (2 x 2) "arrange": 4 grobs
    ##   z     cells    name           grob
    ## 1 1 (1-1,1-1) arrange gtable[layout]
    ## 2 2 (1-1,2-2) arrange gtable[layout]
    ## 3 3 (2-2,1-1) arrange gtable[layout]
    ## 4 4 (2-2,2-2) arrange gtable[layout]

Using one-year sample from 2015 to explore possible models

![](final-project_cao_files/figure-markdown_github-ascii_identifiers/data%20for%202015%20predict%20DV%20using%20conditional%20means-1.png)

    ## Warning: The labeller API has been updated. Labellers taking `variable`and
    ## `value` arguments are now deprecated. See labellers documentation.

    ## Warning: Removed 4 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 4 rows containing missing values (geom_point).

![](final-project_cao_files/figure-markdown_github-ascii_identifiers/data%20for%202015%20predict%20DV%20using%20conditional%20means-2.png)

    ## Warning: The labeller API has been updated. Labellers taking `variable`and
    ## `value` arguments are now deprecated. See labellers documentation.

    ## Warning: Removed 4 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 4 rows containing missing values (geom_point).

![](final-project_cao_files/figure-markdown_github-ascii_identifiers/data%20for%202015%20predict%20DV%20using%20conditional%20means-3.png)

    ## 
    ## Call:
    ## lm(formula = log(bachelordegrees + 1) ~ p_instruct + p_acadsupp + 
    ##     p_studserv + p_instsupp + as.factor(control) + as.factor(hbcu) + 
    ##     as.factor(insttype) + select + log(fall_total_undergrad + 
    ##     1) + log(tot_rev_wo_auxother_sum + 1), data = delta_4_2015, 
    ##     na.action = na.exclude)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -1.47107 -0.10511  0.02313  0.12362  1.04514 
    ## 
    ## Coefficients:
    ##                                    Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)                      -6.225e+00  2.026e-01 -30.731  < 2e-16
    ## p_instruct                        6.007e-03  1.053e-03   5.707 1.43e-08
    ## p_acadsupp                        5.851e-03  1.644e-03   3.559 0.000386
    ## p_studserv                        1.067e-02  1.391e-03   7.674 3.29e-14
    ## p_instsupp                        3.576e-03  1.347e-03   2.654 0.008046
    ## as.factor(control)2              -5.612e-02  2.482e-02  -2.261 0.023909
    ## as.factor(hbcu)2                  1.712e-01  3.266e-02   5.242 1.86e-07
    ## as.factor(insttype)2              1.488e+00  6.810e-02  21.844  < 2e-16
    ## as.factor(insttype)3              1.520e+00  6.268e-02  24.245  < 2e-16
    ## as.factor(insttype)4              1.434e+00  6.158e-02  23.287  < 2e-16
    ## select                           -7.271e-05  3.898e-04  -0.187 0.852061
    ## log(fall_total_undergrad + 1)     7.553e-01  1.689e-02  44.715  < 2e-16
    ## log(tot_rev_wo_auxother_sum + 1)  2.453e-01  1.468e-02  16.710  < 2e-16
    ##                                     
    ## (Intercept)                      ***
    ## p_instruct                       ***
    ## p_acadsupp                       ***
    ## p_studserv                       ***
    ## p_instsupp                       ** 
    ## as.factor(control)2              *  
    ## as.factor(hbcu)2                 ***
    ## as.factor(insttype)2             ***
    ## as.factor(insttype)3             ***
    ## as.factor(insttype)4             ***
    ## select                              
    ## log(fall_total_undergrad + 1)    ***
    ## log(tot_rev_wo_auxother_sum + 1) ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.2348 on 1276 degrees of freedom
    ##   (152 observations deleted due to missingness)
    ## Multiple R-squared:  0.959,  Adjusted R-squared:  0.9587 
    ## F-statistic:  2490 on 12 and 1276 DF,  p-value: < 2.2e-16

    ##                                      GVIF Df GVIF^(1/(2*Df))
    ## p_instruct                       1.558519  1        1.248407
    ## p_acadsupp                       1.223454  1        1.106098
    ## p_studserv                       2.482984  1        1.575749
    ## p_instsupp                       2.312269  1        1.520615
    ## as.factor(control)               3.185306  1        1.784743
    ## as.factor(hbcu)                  1.193812  1        1.092617
    ## as.factor(insttype)              2.741971  3        1.183070
    ## select                           1.201031  1        1.095916
    ## log(fall_total_undergrad + 1)    7.890558  1        2.809014
    ## log(tot_rev_wo_auxother_sum + 1) 7.623900  1        2.761141

    ## [1] 1.263217

    ## [1] 1.275323

Cross validation not working

Models

    ## Warning in log(tot_rev_wo_auxother_sum + 1): NaNs produced

    ## Pooling Model
    ## 
    ## Call:
    ## plm(formula = log(bachelordegrees + 1) ~ p_instruct + p_acadsupp + 
    ##     p_studserv + p_instsupp + as.factor(control) + as.factor(hbcu) + 
    ##     as.factor(insttype) + select + log(tot_rev_wo_auxother_sum + 
    ##     1) + log(fall_total_undergrad + 1), data = delta_4, model = "pooling")
    ## 
    ## Unbalanced Panel: n=13, T=515-1291, N=15731
    ## 
    ## Residuals :
    ##    Min. 1st Qu.  Median 3rd Qu.    Max. 
    ## -2.4300 -0.1120  0.0268  0.1470  1.9800 
    ## 
    ## Coefficients :
    ##                                     Estimate  Std. Error  t-value
    ## (Intercept)                      -6.02381340  0.06749771 -89.2447
    ## p_instruct                        0.00367477  0.00032565  11.2845
    ## p_acadsupp                        0.00413793  0.00052229   7.9227
    ## p_studserv                        0.00867826  0.00045225  19.1891
    ## p_instsupp                        0.00160156  0.00041813   3.8303
    ## as.factor(control)2               0.04312514  0.00768932   5.6084
    ## as.factor(hbcu)2                  0.21047029  0.01040926  20.2195
    ## as.factor(insttype)2              1.73994927  0.03483777  49.9443
    ## as.factor(insttype)3              1.74984823  0.03394464  51.5501
    ## as.factor(insttype)4              1.65754696  0.03377713  49.0731
    ## select                           -0.00052190  0.00012612  -4.1383
    ## log(tot_rev_wo_auxother_sum + 1)  0.20183346  0.00401207  50.3066
    ## log(fall_total_undergrad + 1)     0.80818513  0.00494929 163.2930
    ##                                   Pr(>|t|)    
    ## (Intercept)                      < 2.2e-16 ***
    ## p_instruct                       < 2.2e-16 ***
    ## p_acadsupp                       2.478e-15 ***
    ## p_studserv                       < 2.2e-16 ***
    ## p_instsupp                       0.0001285 ***
    ## as.factor(control)2              2.076e-08 ***
    ## as.factor(hbcu)2                 < 2.2e-16 ***
    ## as.factor(insttype)2             < 2.2e-16 ***
    ## as.factor(insttype)3             < 2.2e-16 ***
    ## as.factor(insttype)4             < 2.2e-16 ***
    ## select                           3.518e-05 ***
    ## log(tot_rev_wo_auxother_sum + 1) < 2.2e-16 ***
    ## log(fall_total_undergrad + 1)    < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Total Sum of Squares:    20463
    ## Residual Sum of Squares: 1091.5
    ## R-Squared:      0.94666
    ## Adj. R-Squared: 0.94662
    ## F-statistic: 23245.9 on 12 and 15718 DF, p-value: < 2.22e-16

    ## Warning in log(tot_rev_wo_auxother_sum + 1): NaNs produced

    ## Oneway (individual) effect Within Model
    ## 
    ## Call:
    ## plm(formula = log(bachelordegrees + 1) ~ p_instruct + p_acadsupp + 
    ##     p_studserv + p_instsupp + as.factor(control) + as.factor(hbcu) + 
    ##     as.factor(insttype) + select + log(tot_rev_wo_auxother_sum + 
    ##     1) + log(fall_total_undergrad + 1), data = delta_4, model = "within", 
    ##     index = c("unitid", "academicyear"))
    ## 
    ## Unbalanced Panel: n=1390, T=1-13, N=15731
    ## 
    ## Residuals :
    ##      Min.   1st Qu.    Median   3rd Qu.      Max. 
    ## -1.430000 -0.058800  0.000377  0.061400  1.100000 
    ## 
    ## Coefficients :
    ##                                     Estimate  Std. Error t-value  Pr(>|t|)
    ## p_instruct                        4.9947e-04  3.8348e-04  1.3025   0.19278
    ## p_acadsupp                       -6.3164e-05  6.6188e-04 -0.0954   0.92397
    ## p_studserv                        1.1086e-03  5.2951e-04  2.0937   0.03631
    ## p_instsupp                       -1.6617e-03  4.0541e-04 -4.0988 4.177e-05
    ## as.factor(insttype)3              8.0713e-02  8.9395e-02  0.9029   0.36660
    ## select                           -6.0912e-04  1.0706e-04 -5.6897 1.298e-08
    ## log(tot_rev_wo_auxother_sum + 1)  8.2823e-02  4.2262e-03 19.5975 < 2.2e-16
    ## log(fall_total_undergrad + 1)     7.2390e-01  9.0177e-03 80.2749 < 2.2e-16
    ##                                     
    ## p_instruct                          
    ## p_acadsupp                          
    ## p_studserv                       *  
    ## p_instsupp                       ***
    ## as.factor(insttype)3                
    ## select                           ***
    ## log(tot_rev_wo_auxother_sum + 1) ***
    ## log(fall_total_undergrad + 1)    ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Total Sum of Squares:    431.66
    ## Residual Sum of Squares: 257.35
    ## R-Squared:      0.40381
    ## Adj. R-Squared: 0.3457
    ## F-statistic: 1213.48 on 8 and 14333 DF, p-value: < 2.22e-16

    ## These series are constants and have been removed: sector_revised, control

    ## Oneway (individual) effect Within Model
    ## 
    ## Call:
    ## plm(formula = log(bachelordegrees + 1) ~ p_instruct + p_acadsupp + 
    ##     p_studserv + p_instsupp + as.factor(hbcu) + as.factor(insttype) + 
    ##     select + log(tot_rev_wo_auxother_sum + 1) + log(fall_total_undergrad + 
    ##     1), data = delta_4_public, model = "within", index = c("unitid", 
    ##     "academicyear"))
    ## 
    ## Unbalanced Panel: n=458, T=1-13, N=5533
    ## 
    ## Residuals :
    ##      Min.   1st Qu.    Median   3rd Qu.      Max. 
    ## -1.360000 -0.048500 -0.000349  0.047000  0.889000 
    ## 
    ## Coefficients :
    ##                                     Estimate  Std. Error t-value  Pr(>|t|)
    ## p_instruct                        0.00195540  0.00062470  3.1302  0.001757
    ## p_acadsupp                        0.00097112  0.00104299  0.9311  0.351850
    ## p_studserv                        0.00412269  0.00136214  3.0266  0.002485
    ## p_instsupp                       -0.00320371  0.00079048 -4.0528 5.136e-05
    ## select                           -0.00122942  0.00015227 -8.0742 8.414e-16
    ## log(tot_rev_wo_auxother_sum + 1)  0.26448036  0.01004712 26.3240 < 2.2e-16
    ## log(fall_total_undergrad + 1)     0.66953665  0.01794473 37.3110 < 2.2e-16
    ##                                     
    ## p_instruct                       ** 
    ## p_acadsupp                          
    ## p_studserv                       ** 
    ## p_instsupp                       ***
    ## select                           ***
    ## log(tot_rev_wo_auxother_sum + 1) ***
    ## log(fall_total_undergrad + 1)    ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Total Sum of Squares:    124.52
    ## Residual Sum of Squares: 59.587
    ## R-Squared:      0.52147
    ## Adj. R-Squared: 0.47765
    ## F-statistic: 788.955 on 7 and 5068 DF, p-value: < 2.22e-16

    ## These series are constants and have been removed: sector_revised, control, flagship

    ## Warning in log(tot_rev_wo_auxother_sum + 1): NaNs produced

    ## Oneway (individual) effect Within Model
    ## 
    ## Call:
    ## plm(formula = log(bachelordegrees + 1) ~ p_instruct + p_acadsupp + 
    ##     p_studserv + p_instsupp + as.factor(hbcu) + as.factor(insttype) + 
    ##     select + log(tot_rev_wo_auxother_sum + 1) + log(fall_total_undergrad + 
    ##     1), data = delta_4_private, model = "within", index = c("unitid", 
    ##     "academicyear"))
    ## 
    ## Unbalanced Panel: n=932, T=1-13, N=10198
    ## 
    ## Residuals :
    ##    Min. 1st Qu.  Median 3rd Qu.    Max. 
    ## -1.3700 -0.0614  0.0023  0.0667  1.1000 
    ## 
    ## Coefficients :
    ##                                     Estimate  Std. Error t-value  Pr(>|t|)
    ## p_instruct                       -0.00012133  0.00047534 -0.2552    0.7985
    ## p_acadsupp                       -0.00191775  0.00083204 -2.3049    0.0212
    ## p_studserv                        0.00053255  0.00060405  0.8816    0.3780
    ## p_instsupp                       -0.00198421  0.00047990 -4.1346 3.587e-05
    ## as.factor(insttype)3              0.08019839  0.09562999  0.8386    0.4017
    ## select                           -0.00019809  0.00013949 -1.4201    0.1556
    ## log(tot_rev_wo_auxother_sum + 1)  0.05434163  0.00482858 11.2542 < 2.2e-16
    ## log(fall_total_undergrad + 1)     0.70232716  0.01073042 65.4520 < 2.2e-16
    ##                                     
    ## p_instruct                          
    ## p_acadsupp                       *  
    ## p_studserv                          
    ## p_instsupp                       ***
    ## as.factor(insttype)3                
    ## select                              
    ## log(tot_rev_wo_auxother_sum + 1) ***
    ## log(fall_total_undergrad + 1)    ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Total Sum of Squares:    307.14
    ## Residual Sum of Squares: 190.18
    ## R-Squared:      0.38081
    ## Adj. R-Squared: 0.31801
    ## F-statistic: 711.735 on 8 and 9258 DF, p-value: < 2.22e-16

    ## These series are constants and have been removed: hbcu, instsize

    ## Warning in log(tot_rev_wo_auxother_sum + 1): NaNs produced

    ## Oneway (individual) effect Within Model
    ## 
    ## Call:
    ## plm(formula = log(bachelordegrees + 1) ~ p_instruct + p_acadsupp + 
    ##     p_studserv + p_instsupp + as.factor(insttype) + select + 
    ##     log(tot_rev_wo_auxother_sum + 1) + log(fall_total_undergrad + 
    ##     1), data = delta_4_large, model = "within", index = c("unitid", 
    ##     "academicyear"))
    ## 
    ## Unbalanced Panel: n=155, T=1-13, N=1570
    ## 
    ## Residuals :
    ##      Min.   1st Qu.    Median   3rd Qu.      Max. 
    ## -0.296000 -0.036800  0.000243  0.036500  0.397000 
    ## 
    ## Coefficients :
    ##                                     Estimate  Std. Error t-value  Pr(>|t|)
    ## p_instruct                       -0.00015276  0.00086600 -0.1764 0.8600051
    ## p_acadsupp                        0.00682555  0.00142448  4.7916 1.830e-06
    ## p_studserv                        0.00989873  0.00226096  4.3781 1.286e-05
    ## p_instsupp                       -0.00022401  0.00113845 -0.1968 0.8440394
    ## select                           -0.00086015  0.00022705 -3.7883 0.0001581
    ## log(tot_rev_wo_auxother_sum + 1)  0.14040505  0.01012856 13.8623 < 2.2e-16
    ## log(fall_total_undergrad + 1)     0.89822958  0.02621647 34.2620 < 2.2e-16
    ##                                     
    ## p_instruct                          
    ## p_acadsupp                       ***
    ## p_studserv                       ***
    ## p_instsupp                          
    ## select                           ***
    ## log(tot_rev_wo_auxother_sum + 1) ***
    ## log(fall_total_undergrad + 1)    ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Total Sum of Squares:    20.324
    ## Residual Sum of Squares: 6.2048
    ## R-Squared:      0.69471
    ## Adj. R-Squared: 0.6598
    ## F-statistic: 457.721 on 7 and 1408 DF, p-value: < 2.22e-16

    ## These series are constants and have been removed: flagship, instsize

    ## Warning in log(tot_rev_wo_auxother_sum + 1): NaNs produced

    ## Oneway (individual) effect Within Model
    ## 
    ## Call:
    ## plm(formula = log(bachelordegrees + 1) ~ p_instruct + p_acadsupp + 
    ##     p_studserv + p_instsupp + as.factor(hbcu) + as.factor(insttype) + 
    ##     select + log(tot_rev_wo_auxother_sum + 1) + log(fall_total_undergrad + 
    ##     1), data = delta_4_small, model = "within", index = c("unitid", 
    ##     "academicyear"))
    ## 
    ## Unbalanced Panel: n=245, T=1-13, N=1724
    ## 
    ## Residuals :
    ##     Min.  1st Qu.   Median  3rd Qu.     Max. 
    ## -1.16000 -0.10200  0.00669  0.10800  1.20000 
    ## 
    ## Coefficients :
    ##                                     Estimate  Std. Error t-value  Pr(>|t|)
    ## p_instruct                       -0.00295511  0.00144786 -2.0410  0.041427
    ## p_acadsupp                       -0.00788029  0.00265438 -2.9688  0.003038
    ## p_studserv                        0.00170170  0.00165289  1.0295  0.303398
    ## p_instsupp                       -0.00341907  0.00122922 -2.7815  0.005480
    ## as.factor(insttype)3              0.09647027  0.14045386  0.6868  0.492288
    ## select                           -0.00061000  0.00041341 -1.4755  0.140279
    ## log(tot_rev_wo_auxother_sum + 1)  0.03369883  0.01532019  2.1996  0.027988
    ## log(fall_total_undergrad + 1)     0.68182268  0.03364071 20.2678 < 2.2e-16
    ##                                     
    ## p_instruct                       *  
    ## p_acadsupp                       ** 
    ## p_studserv                          
    ## p_instsupp                       ** 
    ## as.factor(insttype)3                
    ## select                              
    ## log(tot_rev_wo_auxother_sum + 1) *  
    ## log(fall_total_undergrad + 1)    ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Total Sum of Squares:    88.53
    ## Residual Sum of Squares: 64.845
    ## R-Squared:      0.26754
    ## Adj. R-Squared: 0.14206
    ## F-statistic: 67.1629 on 8 and 1471 DF, p-value: < 2.22e-16

    ## Warning in log(tot_rev_wo_auxother_sum + 1): NaNs produced

    ## Oneway (individual) effect Within Model
    ## 
    ## Call:
    ## plm(formula = log(bachelordegrees + 1) ~ p_instruct + p_acadsupp + 
    ##     p_studserv + p_instsupp + as.factor(hbcu) + as.factor(insttype) + 
    ##     select + log(tot_rev_wo_auxother_sum + 1) + log(fall_total_undergrad + 
    ##     1), data = delta_4_med, model = "within", index = c("unitid", 
    ##     "academicyear"))
    ## 
    ## Unbalanced Panel: n=1147, T=1-13, N=12435
    ## 
    ## Residuals :
    ##      Min.   1st Qu.    Median   3rd Qu.      Max. 
    ## -1.45e+00 -5.75e-02 -7.51e-05  5.95e-02  1.02e+00 
    ## 
    ## Coefficients :
    ##                                     Estimate  Std. Error t-value  Pr(>|t|)
    ## p_instruct                        0.00122335  0.00041314  2.9611  0.003072
    ## p_acadsupp                        0.00168320  0.00070700  2.3808  0.017294
    ## p_studserv                        0.00182625  0.00060208  3.0332  0.002425
    ## p_instsupp                       -0.00100043  0.00046734 -2.1407  0.032322
    ## select                           -0.00055009  0.00011456 -4.8017 1.594e-06
    ## log(tot_rev_wo_auxother_sum + 1)  0.08938553  0.00452403 19.7580 < 2.2e-16
    ## log(fall_total_undergrad + 1)     0.68718362  0.01060477 64.7995 < 2.2e-16
    ##                                     
    ## p_instruct                       ** 
    ## p_acadsupp                       *  
    ## p_studserv                       ** 
    ## p_instsupp                       *  
    ## select                           ***
    ## log(tot_rev_wo_auxother_sum + 1) ***
    ## log(fall_total_undergrad + 1)    ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Total Sum of Squares:    272.89
    ## Residual Sum of Squares: 171.86
    ## R-Squared:      0.3702
    ## Adj. R-Squared: 0.30584
    ## F-statistic: 947.31 on 7 and 11281 DF, p-value: < 2.22e-16

    ## These series are constants and have been removed: flagship, insttype

    ## Warning in log(tot_rev_wo_auxother_sum + 1): NaNs produced

    ## Oneway (individual) effect Within Model
    ## 
    ## Call:
    ## plm(formula = log(bachelordegrees + 1) ~ p_instruct + p_acadsupp + 
    ##     p_studserv + p_instsupp + as.factor(hbcu) + select + log(tot_rev_wo_auxother_sum + 
    ##     1) + log(fall_total_undergrad + 1), data = delta_4_ba, model = "within", 
    ##     index = c("unitid", "academicyear"))
    ## 
    ## Unbalanced Panel: n=549, T=1-13, N=5913
    ## 
    ## Residuals :
    ##     Min.  1st Qu.   Median  3rd Qu.     Max. 
    ## -1.42000 -0.06770  0.00251  0.07520  1.10000 
    ## 
    ## Coefficients :
    ##                                     Estimate  Std. Error t-value  Pr(>|t|)
    ## p_instruct                       -0.00013628  0.00068433 -0.1991   0.84216
    ## p_acadsupp                       -0.00290873  0.00129164 -2.2520   0.02436
    ## p_studserv                        0.00076180  0.00085307  0.8930   0.37189
    ## p_instsupp                       -0.00330079  0.00067002 -4.9264 8.626e-07
    ## select                           -0.00084011  0.00019528 -4.3020 1.722e-05
    ## log(tot_rev_wo_auxother_sum + 1)  0.04812347  0.00644404  7.4679 9.460e-14
    ## log(fall_total_undergrad + 1)     0.74708513  0.01508032 49.5404 < 2.2e-16
    ##                                     
    ## p_instruct                          
    ## p_acadsupp                       *  
    ## p_studserv                          
    ## p_instsupp                       ***
    ## select                           ***
    ## log(tot_rev_wo_auxother_sum + 1) ***
    ## log(fall_total_undergrad + 1)    ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Total Sum of Squares:    220.01
    ## Residual Sum of Squares: 137.43
    ## R-Squared:      0.37536
    ## Adj. R-Squared: 0.31065
    ## F-statistic: 459.878 on 7 and 5357 DF, p-value: < 2.22e-16

    ## These series are constants and have been removed: flagship, insttype

    ## Warning in log(tot_rev_wo_auxother_sum + 1): NaNs produced

    ## Oneway (individual) effect Within Model
    ## 
    ## Call:
    ## plm(formula = log(bachelordegrees + 1) ~ p_instruct + p_acadsupp + 
    ##     p_studserv + p_instsupp + as.factor(hbcu) + select + log(tot_rev_wo_auxother_sum + 
    ##     1) + log(fall_total_undergrad + 1), data = delta_4_ma, model = "within", 
    ##     index = c("unitid", "academicyear"))
    ## 
    ## Unbalanced Panel: n=566, T=1-13, N=6735
    ## 
    ## Residuals :
    ##      Min.   1st Qu.    Median   3rd Qu.      Max. 
    ## -0.875000 -0.057200 -0.000405  0.058400  0.632000 
    ## 
    ## Coefficients :
    ##                                     Estimate  Std. Error t-value  Pr(>|t|)
    ## p_instruct                        0.00175245  0.00052477  3.3395 0.0008443
    ## p_acadsupp                        0.00083503  0.00089668  0.9312 0.3517649
    ## p_studserv                       -0.00189597  0.00075980 -2.4954 0.0126089
    ## p_instsupp                       -0.00133274  0.00058073 -2.2949 0.0217711
    ## select                           -0.00022397  0.00014122 -1.5860 0.1127964
    ## log(tot_rev_wo_auxother_sum + 1)  0.17510081  0.00776208 22.5585 < 2.2e-16
    ## log(fall_total_undergrad + 1)     0.61105068  0.01326760 46.0559 < 2.2e-16
    ##                                     
    ## p_instruct                       ***
    ## p_acadsupp                          
    ## p_studserv                       *  
    ## p_instsupp                       *  
    ## select                              
    ## log(tot_rev_wo_auxother_sum + 1) ***
    ## log(fall_total_undergrad + 1)    ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Total Sum of Squares:    153.3
    ## Residual Sum of Squares: 83.67
    ## R-Squared:      0.45421
    ## Adj. R-Squared: 0.40354
    ## F-statistic: 732.568 on 7 and 6162 DF, p-value: < 2.22e-16

    ## These series are constants and have been removed: has_all, insttype

    ## Warning in log(tot_rev_wo_auxother_sum + 1): NaNs produced

    ## Oneway (individual) effect Within Model
    ## 
    ## Call:
    ## plm(formula = log(bachelordegrees + 1) ~ p_instruct + p_acadsupp + 
    ##     p_studserv + p_instsupp + as.factor(hbcu) + select + log(tot_rev_wo_auxother_sum + 
    ##     1) + log(fall_total_undergrad + 1), data = delta_4_phd, model = "within", 
    ##     index = c("unitid", "academicyear"))
    ## 
    ## Unbalanced Panel: n=257, T=1-13, N=3021
    ## 
    ## Residuals :
    ##      Min.   1st Qu.    Median   3rd Qu.      Max. 
    ## -0.487000 -0.042900 -0.000195  0.043700  0.429000 
    ## 
    ## Coefficients :
    ##                                     Estimate  Std. Error t-value  Pr(>|t|)
    ## p_instruct                        0.00149968  0.00065768  2.2802   0.02267
    ## p_acadsupp                        0.00554016  0.00094071  5.8894 4.346e-09
    ## p_studserv                        0.01490114  0.00128950 11.5557 < 2.2e-16
    ## p_instsupp                        0.00415391  0.00083892  4.9515 7.808e-07
    ## select                           -0.00078325  0.00018512 -4.2310 2.403e-05
    ## log(tot_rev_wo_auxother_sum + 1)  0.07438532  0.00660485 11.2622 < 2.2e-16
    ## log(fall_total_undergrad + 1)     0.76927206  0.01838784 41.8359 < 2.2e-16
    ##                                     
    ## p_instruct                       *  
    ## p_acadsupp                       ***
    ## p_studserv                       ***
    ## p_instsupp                       ***
    ## select                           ***
    ## log(tot_rev_wo_auxother_sum + 1) ***
    ## log(fall_total_undergrad + 1)    ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Total Sum of Squares:    44.38
    ## Residual Sum of Squares: 18.203
    ## R-Squared:      0.58983
    ## Adj. R-Squared: 0.55071
    ## F-statistic: 566.381 on 7 and 2757 DF, p-value: < 2.22e-16

Key Takeways

1.  Institutional spending patterns do relate to its degree production.
2.  The relationships vary across institutions with different focuses, sizes, and types.
3.  It is unclear whether it is just a concurrent phenomenon or a casual effect. If it is a casual effect, it needs further research to unreveal the mechanism underlying as well as the cause of variation among different institutions.
