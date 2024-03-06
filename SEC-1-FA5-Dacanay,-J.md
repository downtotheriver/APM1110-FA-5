APM1110 - FA 5 - Dacanay
================

### 1. An email message can travel through one of three server routes. The percentage of errors in each of the servers and the percentage of messages that travel through each route are shown in the following table. Assume that the servers are independent.

``` r
library(pander)

Servers <- c("Server 1", "Server 2", "Server 3")
df_email <- data.frame(
  Percentage_of_Messages = c(40, 25, 35),
  Percentage_of_Errors = c(1, 2, 1.5)
)
rownames(df_email) <- Servers

pander(df_email)
```

|              | Percentage_of_Messages | Percentage_of_Errors |
|:------------:|:----------------------:|:--------------------:|
| **Server 1** |           40           |          1           |
| **Server 2** |           25           |          2           |
| **Server 3** |           35           |         1.5          |

#### (a) What is the probability of receiving an email containing an error?

We can use the law of total probability. In this problem, we need to get
the product of the probability of messages and errors of each server and
solve for their sum.

``` r
# Assigning values for the probability of messages and errors
p_message_1 <- df_email[1, 1] / 100
p_message_2 <- df_email[2, 1] / 100
p_message_3 <- df_email[3, 1] /100

p_error_1 <- df_email[1, 2] / 100
p_error_2 <- df_email[2, 2] / 100
p_error_3 <- df_email[3, 2] / 100

# Product of message and error of each server
prod_server_1 <- p_message_1 * p_error_1
prod_server_2 <- p_message_2 * p_error_2
prod_server_3 <- p_message_3 * p_error_3

# Total sum of all servers
p_email_error <- prod_server_1 + prod_server_2 + prod_server_3
```

##### ANSWER

``` r
paste0(p_email_error, " or ", p_email_error * 100, "%")
```

    ## [1] "0.01425 or 1.425%"

The probability of receiving an email containing an error is $0.01425$
or $1.425$%

#### (b) What is the probability that a message will arrive without error?

We can use the complementary approach here, in which we will subtract
the probability of receiving an error in email from 1.

``` r
p_email_wo_error <- 1 - p_email_error
```

##### ANSWER

``` r
paste0(p_email_wo_error, " or ", p_email_wo_error * 100, "%")
```

    ## [1] "0.98575 or 98.575%"

The probability of receiving an email containing an error is $0.98575$
or $98.575$%

#### (c) If a message arrives without error, what is the probability that it was sent through server 1?

In this question, we will use the data from (b), which is the
probability of receiving an email without an error. We will use Bayes’
rule here.

``` r
p_email_wo_error_1 <- round(((p_message_1 * (1-p_error_1)) / p_email_wo_error), 4)
```

##### ANSWER

``` r
paste0(p_email_wo_error_1, " or ", p_email_wo_error_1*100, "%")
```

    ## [1] "0.4017 or 40.17%"

The probability of receiving an email without an error in server 1 is
$0.4017$ or $40.17$%

### 9. A software company surveyed managers to determine the probability that they would buy a new graphics package that includes three-dimensional graphics. About 20% of office managers were certain that they would not buy the package, 70% claimed that they would buy, and the others were undecided. Of those who said that they would not buy the package, only 10% said that they were interested in upgrading their computer hardware. Of those interested in buying the graphics package, 40% were also interested in upgrading their computer hardware. Of the undecided, 20% were interested in upgrading their computer hardware.

``` r
Decisions <- c("Not buying", "Buying", "Undecided")
df_company <- data.frame(
  Percentage_of_Managers = c(20, 70, 10),
  Percentage_of_Upgrading = c(10, 40, 20)
)
rownames(df_company) <- Decisions

pander(df_company)
```

|                | Percentage_of_Managers | Percentage_of_Upgrading |
|:--------------:|:----------------------:|:-----------------------:|
| **Not buying** |           20           |           10            |
|   **Buying**   |           70           |           40            |
| **Undecided**  |           10           |           20            |

Let ***A*** denote the intention of not buying, ***B*** the intention of
buying, ***C*** the undecided, ***G*** the intention of upgrading the
computer hardware, and ***H*** the complementary of ***G***.

#### (a) Calculate the probability that a manager chosen at random will not upgrade the computer hardware (P(H)).

We can use the complementary approach first of the event that the
managers will upgrade the computer hard, then, the law of total
probability. In this problem, we need to get the product of the
probability of managers and not upgrading for each decision and solve
for their sum.

``` r
# Probability of Manager's decision
p_managers_not_buying <- df_company[1, 1] / 100
p_managers_buying <- df_company[2, 1] / 100
p_managers_undecided <- df_company[3, 1] / 100

# Probability of Upgrading
p_upgrading_not_buying <- df_company[1, 2] / 100
p_upgrading_buying <- df_company[2, 2] / 100
p_upgrading_undecided <- df_company[3, 2] / 100

# Complementary of Upgrading
p_not_upgrading_not_buying <- 1 - p_upgrading_not_buying
p_not_upgrading_buying <- 1 - p_upgrading_buying
p_not_upgrading_undecided <- 1 - p_upgrading_undecided

# Product of the probability of each manager's decision and not upgrading
prod_not_buying <- p_managers_not_buying * p_not_upgrading_not_buying
prod_buying <- p_managers_buying * p_not_upgrading_buying
prod_undecided <- p_managers_undecided * p_not_upgrading_undecided

# Total sum of all servers
p_not_upgrading <- prod_not_buying + prod_buying + prod_undecided
```

##### ANSWER

``` r
paste0(p_not_upgrading, " or ", p_not_upgrading * 100, "%")
```

    ## [1] "0.68 or 68%"

The probability that a manager chosen at random will not upgrade the
computer hardware is $0.68$ or $68$%
