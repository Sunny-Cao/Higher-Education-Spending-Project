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

From this table, we could see that over years, the number of institutions in public and private sectos keeps relatively steady, suggesting that institutions are measured year by year by large chances.

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

Notes:

Associate's Colleges include institutions where all degrees are at the associate's level, or where bachelor's degrees account for less than 10 percent of all undergraduate degrees. Excludes Special Focus Institutions and Tribal Colleges.

Research/Doctorate-granting Universities includes institutions that award at least 20 doctoral degrees per year (excluding doctoral-level degrees that qualify recipients for entry into professional practice, such as the JD, MD, PharmD, DPT, etc.) Excludes Special Focus Institutions and Tribal Colleges.

Master’s Colleges and Universities includes institutions that award at least 50 master's degrees per year. Excludes Special Focus Institutions and Tribal Colleges.

Baccalaureate Colleges includes institutions where baccalaureate degrees represent at least 10 percent of all undergraduate degrees and that award fewer than 50 master's degrees or fewer than 20 doctoral degrees per year. Excludes Special Focus Institutions and Tribal Colleges.

So we can see that a lot of variation exist in the size and type of institutions, suggesting that we need to classify institutions when we try to find out patterns.

![](final-project_cao_files/figure-markdown_github-ascii_identifiers/Descriptive%20Stats%20Cond2-1.png)

This graph shows the growing trend of enrollment and bachelor degree production. Enrollment data here includes all students enroll rather than the incoming cohort. Thus the gap between enrollment and degree production appears to be a little wide. We can see that total enrollment in public institutions has been growing rapidly, while other index also grew over years but on a slower pace.

![](final-project_cao_files/figure-markdown_github-ascii_identifiers/Descriptive%20Stats%20Cond3-1.png)

From this box plot, we could see that bachelor degree production is increasing over years (the graph is on a log scale, so the growth is not that obvious), but there is large variation among institutions.

    ## Warning: The labeller API has been updated. Labellers taking `variable`and
    ## `value` arguments are now deprecated. See labellers documentation.

![](final-project_cao_files/figure-markdown_github-ascii_identifiers/Descriptive%20Stats%20Cond4-1.png)

Instructional expenditure still account for the largest portion of institutional expenses regardless of institutional types. However, while public institutions have witnessed a slight growth in instructional expenses over the past fifteen years, private institutions have cut down their instructional expenditure by a large portion. Besides, private institutions also gradually decrease their expenditure on academic support. All these money saved are used in student services and institutional support, which align with the fierce enrollment management nowadays.

Notes:

Instruction - A functional expense category that includes expenses of the colleges, schools, departments, and other instructional divisions of the institution and expenses for departmental research and public service that are not separately budgeted. Includes general academic instruction, occupational and vocational instruction, community education, preparatory and adult basic education, and regular, special, and extension sessions. Also includes expenses for both credit and non-credit activities. Excludes expenses for academic administration where the primary function is administration (e.g., academic deans). Information technology expenses related to instructional activities are included if the institution separately budgets and expenses information technology resources (otherwise these expenses are included in academic support). Operations and maintenance and interest amounts attributed to the instruction function have been subtracted from the total instructional expenditure amount at FASB reporting institutions. Operations and maintenance amounts (and interest in the aligned form beginning in 2009) attributed to the instruction function have been subtracted from the total amount at public Aligned form reporting institutions.

Academic support - A functional expense category that includes expenses of activities and services that support the institution's primary missions of instruction, research, and public service. It includes the retention, preservation, and display of educational materials (for example, libraries, museums, and galleries); organized activities that provide support services to the academic functions of the institution (such as a demonstration school associated with a college of education or veterinary and dental clinics if their primary purpose is to support the instructional program); media such as audiovisual services; academic administration (including academic deans but not department chairpersons); and formally organized and separately budgeted academic personnel development and course and curriculum development expenses. Also included are information technology expenses related to academic support activities; if an institution does not separately budget and expense information technology resources, the costs associated with the three primary programs will be applied to this function and the remainder to institutional support. Operations and maintenance and interest amounts attributed to the academic support function have been subtracted from the total academic support expenditure amount at FASB reporting institutions. Operations and maintenance amounts (and interest in the aligned form beginning in 2009) attributed to the academic support function have been subtracted from the total academic support expenditure amount at public Aligned Form reporting institutions.

Student services - A functional expense category that includes expenses for admissions, registrar activities, and activities whose primary purpose is to contribute to students emotional and physical well-being and to their intellectual, cultural, and social development outside the context of the formal instructional program. Examples include student activities, cultural events, student newspapers, intramural athletics, student organizations, supplemental instruction outside the normal administration, and student records. Intercollegiate athletics and student health services may also be included except when operated as self - supporting auxiliary enterprises. Also may include information technology expenses related to student service activities if the institution separately budgets and expenses information technology resources(otherwise these expenses are included in institutional support.) Operations and maintenance and interest amounts attributed to the student sevices function have been subtracted from the total student services expenditure amount at FASB reporting institutions. Operations and maintenance (and interest in the aligned form beginning in 2009) amounts attributed to the student services function have been subtracted from the total student services expenditure amount at public Aligned Form reporting institutions.

Institutional support - A functional expense category that includes expenses for the day-to-day operational support of the institution. Includes expenses for general administrative services, central executive-level activities concerned with management and long range planning, legal and fiscal operations, space management, employee personnel and records, logistical services such as purchasing and printing, and public relations and development. Also includes information technology expenses related to institutional support activities. Operations and maintenance and interest amounts attributed to the institutional support function have been subtracted from the total institutional support expenditure amount at FASB reporting institutions. Operations and maintenance amounts (and interest in the aligned form beginning in 2009) attributed to the institutional support function have been subtracted from the total institutional support expenditure amount at public Aligned Form reporting institutions.

Next, I made four box plots for each type of expenses. There is huge variation cross instituions.

    ## Warning: Removed 3517 rows containing non-finite values (stat_boxplot).

    ## Warning: Removed 3691 rows containing non-finite values (stat_boxplot).

    ## Warning: Removed 3474 rows containing non-finite values (stat_boxplot).

    ## Warning: Removed 3581 rows containing non-finite values (stat_boxplot).

![](final-project_cao_files/figure-markdown_github-ascii_identifiers/Descriptive%20Stats%20Cond5-1.png)

    ## TableGrob (2 x 2) "arrange": 4 grobs
    ##   z     cells    name           grob
    ## 1 1 (1-1,1-1) arrange gtable[layout]
    ## 2 2 (1-1,2-2) arrange gtable[layout]
    ## 3 3 (2-2,1-1) arrange gtable[layout]
    ## 4 4 (2-2,2-2) arrange gtable[layout]

Using one-year sample from 2015 to explore possible models

    ## Warning: The labeller API has been updated. Labellers taking `variable`and
    ## `value` arguments are now deprecated. See labellers documentation.

    ## Warning: Removed 4 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 4 rows containing missing values (geom_point).

![](final-project_cao_files/figure-markdown_github-ascii_identifiers/data%20for%202015%20predict%20DV%20using%20conditional%20means-1.png)

For small (0-999) and large (20000+), instructional spending seems to be negatively related to degree production. The correlations are positive for median-size institutions (1000-19999), though public and private institutions seem to have different patterns.

    ## Warning: The labeller API has been updated. Labellers taking `variable`and
    ## `value` arguments are now deprecated. See labellers documentation.

    ## Warning: Removed 4 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 4 rows containing missing values (geom_point).

![](final-project_cao_files/figure-markdown_github-ascii_identifiers/data%20for%202015%20predict%20DV%20using%20conditional%20means%20cond-1.png)

There are obviously positive relationships between instructional spending and bachelor degree production in Baccalaureate Colleges (both private and public) and public Master's College and University.

Based on these finding, institutional types should be included in the regression models.

    ## 
    ## ===============================================
    ##                                   Model 1      
    ## -----------------------------------------------
    ## (Intercept)                         -6.2254 ***
    ##                                     (0.2026)   
    ## p_instruct                           0.0060 ***
    ##                                     (0.0011)   
    ## p_acadsupp                           0.0059 ***
    ##                                     (0.0016)   
    ## p_studserv                           0.0107 ***
    ##                                     (0.0014)   
    ## p_instsupp                           0.0036 ** 
    ##                                     (0.0013)   
    ## as.factor(control)2                 -0.0561 *  
    ##                                     (0.0248)   
    ## as.factor(hbcu)2                     0.1712 ***
    ##                                     (0.0327)   
    ## as.factor(insttype)2                 1.4876 ***
    ##                                     (0.0681)   
    ## as.factor(insttype)3                 1.5197 ***
    ##                                     (0.0627)   
    ## as.factor(insttype)4                 1.4339 ***
    ##                                     (0.0616)   
    ## select                              -0.0001    
    ##                                     (0.0004)   
    ## log(fall_total_undergrad + 1)        0.7553 ***
    ##                                     (0.0169)   
    ## log(tot_rev_wo_auxother_sum + 1)     0.2453 ***
    ##                                     (0.0147)   
    ## -----------------------------------------------
    ## R^2                                  0.9590    
    ## Adj. R^2                             0.9587    
    ## Num. obs.                         1289         
    ## RMSE                                 0.2348    
    ## ===============================================
    ## *** p < 0.001, ** p < 0.01, * p < 0.05

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

Notes: RMSE is on a log scale.

This model fits well and doesn't have a problem of multicollinearity.

I tested this model on the 2014 data and got a similar RMSE, suggesting the patterns might be similar over years.

RMSE when testing on 2014 data:

    ## [1] 0.2431998

I tried to apply cross validation to this dataset, but because of missing data, I failed to make it work.

Models

Based on the previous, I did a pooling model for all-year data and a fixed-effect model.

    ## Warning in log(tot_rev_wo_auxother_sum + 1): NaNs produced

    ## Warning in log(tot_rev_wo_auxother_sum + 1): NaNs produced

    ## 
    ## ====================================================================
    ##                                   Pooling Model   Fixed Effect Model
    ## --------------------------------------------------------------------
    ## (Intercept)                          -6.0238 ***                    
    ##                                      (0.0675)                       
    ## p_instruct                            0.0037 ***      0.0005        
    ##                                      (0.0003)        (0.0004)       
    ## p_acadsupp                            0.0041 ***     -0.0001        
    ##                                      (0.0005)        (0.0007)       
    ## p_studserv                            0.0087 ***      0.0011 *      
    ##                                      (0.0005)        (0.0005)       
    ## p_instsupp                            0.0016 ***     -0.0017 ***    
    ##                                      (0.0004)        (0.0004)       
    ## as.factor(control)2                   0.0431 ***                    
    ##                                      (0.0077)                       
    ## as.factor(hbcu)2                      0.2105 ***                    
    ##                                      (0.0104)                       
    ## as.factor(insttype)2                  1.7399 ***                    
    ##                                      (0.0348)                       
    ## as.factor(insttype)3                  1.7498 ***      0.0807        
    ##                                      (0.0339)        (0.0894)       
    ## as.factor(insttype)4                  1.6575 ***                    
    ##                                      (0.0338)                       
    ## select                               -0.0005 ***     -0.0006 ***    
    ##                                      (0.0001)        (0.0001)       
    ## log(tot_rev_wo_auxother_sum + 1)      0.2018 ***      0.0828 ***    
    ##                                      (0.0040)        (0.0042)       
    ## log(fall_total_undergrad + 1)         0.8082 ***      0.7239 ***    
    ##                                      (0.0049)        (0.0090)       
    ## --------------------------------------------------------------------
    ## R^2                                   0.9467          0.4038        
    ## Adj. R^2                              0.9466          0.3457        
    ## Num. obs.                         15731           15731             
    ## ====================================================================
    ## *** p < 0.001, ** p < 0.01, * p < 0.05

Some institutions (probably one or two) changed their carniege type. We could temporarily ignore this part.

All three control variables (selectivity, total revenue, total enrollment) are significant in both models. However, instructional expenses and academic support expenses become insignificant when we control for institutional characteristics. Expenditure on student services become less significant and the coefficient drops quite a lot. Expenditure on institutional support is still significant, but the relationship changes from positively related to negatively related.

All these changes suggests that there is huge variation across different institutions, so the pooling model can't really represent any institutions.

Considering that, I did several fixed-effect models for different types of universities.

    ## These series are constants and have been removed: sector_revised, control

    ## These series are constants and have been removed: sector_revised, control, flagship

    ## Warning in log(tot_rev_wo_auxother_sum + 1): NaNs produced

    ## These series are constants and have been removed: hbcu, instsize

    ## Warning in log(tot_rev_wo_auxother_sum + 1): NaNs produced

    ## These series are constants and have been removed: flagship, instsize

    ## Warning in log(tot_rev_wo_auxother_sum + 1): NaNs produced

    ## Warning in log(tot_rev_wo_auxother_sum + 1): NaNs produced

    ## These series are constants and have been removed: flagship, insttype

    ## Warning in log(tot_rev_wo_auxother_sum + 1): NaNs produced

    ## These series are constants and have been removed: flagship, insttype

    ## Warning in log(tot_rev_wo_auxother_sum + 1): NaNs produced

    ## These series are constants and have been removed: has_all, insttype

    ## Warning in log(tot_rev_wo_auxother_sum + 1): NaNs produced

    ## 
    ## ==========================================================================================================================================================================
    ##                                   All             Public         Private         Large          Small          Median          Baccalaureate  Master         PhD          
    ## --------------------------------------------------------------------------------------------------------------------------------------------------------------------------
    ## p_instruct                            0.0005         0.0020 **      -0.0001        -0.0002        -0.0030 *        0.0012 **     -0.0001         0.0018 ***     0.0015 *  
    ##                                      (0.0004)       (0.0006)        (0.0005)       (0.0009)       (0.0014)        (0.0004)       (0.0007)       (0.0005)       (0.0007)   
    ## p_acadsupp                           -0.0001         0.0010         -0.0019 *       0.0068 ***    -0.0079 **       0.0017 *      -0.0029 *       0.0008         0.0055 ***
    ##                                      (0.0007)       (0.0010)        (0.0008)       (0.0014)       (0.0027)        (0.0007)       (0.0013)       (0.0009)       (0.0009)   
    ## p_studserv                            0.0011 *       0.0041 **       0.0005         0.0099 ***     0.0017          0.0018 **      0.0008        -0.0019 *       0.0149 ***
    ##                                      (0.0005)       (0.0014)        (0.0006)       (0.0023)       (0.0017)        (0.0006)       (0.0009)       (0.0008)       (0.0013)   
    ## p_instsupp                           -0.0017 ***    -0.0032 ***     -0.0020 ***    -0.0002        -0.0034 **      -0.0010 *      -0.0033 ***    -0.0013 *       0.0042 ***
    ##                                      (0.0004)       (0.0008)        (0.0005)       (0.0011)       (0.0012)        (0.0005)       (0.0007)       (0.0006)       (0.0008)   
    ## as.factor(insttype)3                  0.0807                         0.0802                        0.0965                                                                 
    ##                                      (0.0894)                       (0.0956)                      (0.1405)                                                                
    ## select                               -0.0006 ***    -0.0012 ***     -0.0002        -0.0009 ***    -0.0006         -0.0006 ***    -0.0008 ***    -0.0002        -0.0008 ***
    ##                                      (0.0001)       (0.0002)        (0.0001)       (0.0002)       (0.0004)        (0.0001)       (0.0002)       (0.0001)       (0.0002)   
    ## log(tot_rev_wo_auxother_sum + 1)      0.0828 ***     0.2645 ***      0.0543 ***     0.1404 ***     0.0337 *        0.0894 ***     0.0481 ***     0.1751 ***     0.0744 ***
    ##                                      (0.0042)       (0.0100)        (0.0048)       (0.0101)       (0.0153)        (0.0045)       (0.0064)       (0.0078)       (0.0066)   
    ## log(fall_total_undergrad + 1)         0.7239 ***     0.6695 ***      0.7023 ***     0.8982 ***     0.6818 ***      0.6872 ***     0.7471 ***     0.6111 ***     0.7693 ***
    ##                                      (0.0090)       (0.0179)        (0.0107)       (0.0262)       (0.0336)        (0.0106)       (0.0151)       (0.0133)       (0.0184)   
    ## --------------------------------------------------------------------------------------------------------------------------------------------------------------------------
    ## R^2                                   0.4038         0.5215          0.3808         0.6947         0.2675          0.3702         0.3754         0.4542         0.5898    
    ## Adj. R^2                              0.3457         0.4777          0.3180         0.6598         0.1421          0.3058         0.3106         0.4035         0.5507    
    ## Num. obs.                         15731           5533           10198           1570           1724           12435           5913           6735           3021         
    ## ==========================================================================================================================================================================
    ## *** p < 0.001, ** p < 0.01, * p < 0.05

We could see that the coefficients, significance, and the model fits vary largely across different sample. Thus, I would be extremely careful to explain any of these as a causal effect. Also, when we control for other factors, the positive effect of instructional expenditure on bachelor degree production in baccalaureate college disappeared. This makes me think about if spending patterns really influence institutional bachelor degree producing efficiency.

Key Takeways

1.  Institutional spending patterns do relate to its degree production.
2.  The relationships vary across institutions with different focuses, sizes, and types.
3.  It is unclear whether it is just a concurrent phenomenon or a casual effect. If it is a casual effect, it needs further research to unreveal the mechanism underlying as well as the cause of variation among different institutions.
