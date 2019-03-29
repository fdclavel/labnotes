Lab1 Rmarkdown 10 Jan 2019
================
Fred Clavel
January 15, 2019

<a href="https://github.com/fdclavel" target="_blank" class="github-corner" aria-label="View source on GitHub"><svg width="80" height="80" viewBox="0 0 250 250" style="fill:#FD6C6C; color:#fff; position: absolute; top: 0; border: 0; right: 0;" aria-hidden="true"><path d="M0,0 L115,115 L130,115 L142,142 L250,250 L250,0 Z"></path><path d="M128.3,109.0 C113.8,99.7 119.0,89.6 119.0,89.6 C122.0,82.7 120.5,78.6 120.5,78.6 C119.2,72.0 123.4,76.3 123.4,76.3 C127.3,80.9 125.5,87.3 125.5,87.3 C122.9,97.6 130.6,101.9 134.4,103.2" fill="currentColor" style="transform-origin: 130px 106px;" class="octo-arm"></path><path d="M115.0,115.0 C114.9,115.1 118.7,116.5 119.8,115.4 L133.7,101.6 C136.9,99.2 139.9,98.4 142.2,98.6 C133.8,88.0 127.5,74.4 143.8,58.0 C148.5,53.4 154.0,51.2 159.7,51.0 C160.3,49.4 163.2,43.6 171.4,40.1 C171.4,40.1 176.1,42.5 178.8,56.2 C183.1,58.6 187.2,61.8 190.9,65.4 C194.5,69.0 197.7,73.2 200.1,77.6 C213.8,80.2 216.3,84.9 216.3,84.9 C212.7,93.1 206.9,96.0 205.4,96.6 C205.1,102.4 203.0,107.8 198.3,112.5 C181.9,128.9 168.3,122.5 157.7,114.1 C157.9,116.9 156.7,120.9 152.7,124.9 L141.0,136.5 C139.8,137.7 141.6,141.9 141.8,141.8 Z" fill="currentColor" class="octo-body"></path></svg></a><style>.github-corner:hover .octo-arm{animation:octocat-wave 560ms ease-in-out}@keyframes octocat-wave{0%,100%{transform:rotate(0)}20%,60%{transform:rotate(-25deg)}40%,80%{transform:rotate(10deg)}}@media (max-width:500px){.github-corner:hover .octo-arm{animation:none}.github-corner .octo-arm{animation:octocat-wave 560ms ease-in-out}}</style>

<style>
div.blue { background-color:#e6f0ff; border-radius: 5px; padding: 20px;}
div.green { background-color:#e6ffd0; border-radius: 5px; padding: 20px;}
div.red { background-color:#ffe6f0; border-radius: 5px; padding: 20px;}
div.warn { background-color:#ee1111; color:#ffffff; font-weight:bold; border-radius: 5px; padding: 20px; font-variant:small-caps}
div.safe { background-color:#00bb00; color:#ffffff; border-radius: 5px; padding: 20px; font-family:tahoma; line-height:150%}
div.data {background-color:#ddddee; border-radius: 5px; padding: 20px; font-family:monospace}
</style>
Use ctrl+alt+i to start a new code chunk in R markdown.

``` r
#while inside a code chunk, you still need to use hashtags to insert comments, as you would during a standard R script.

#the basic act of creating an object uses the arrow sign <-.
thing1 <-5

#once you run the line above, you will have an object named thing1 in your environment, and it will be equal to 5.

#you can add more objects and then use them in tandem.
thing2 <-2

#adding them will give you a value in the console.
thing1+thing2
```

    ## [1] 7

``` r
#you can save the added value as a new object too.
thing3 <- thing1+thing2

#it's a good idea to clear your environment after you are done coding, and then re-run your entire script, to make sure you didn't overwrite anything along the way. It's easy to accidentally change objects along the way.
```

R is made up of packages and functions. Both make common actions easier to repeat.

Examples of functions include:

``` r
#if you need a list of numbers from 1 to 15, you can hard code it like this:
number_list <-c(1,2,3,4,5,6,7,8,9,10,11,12,13,14,15)

#this can get tedious, but fortunately there is a function that already does this - the seq() function.

#to see what seq() is (or any other function), just search for info using the  question mark and the name, like this:
?seq()

#we can use tihs to create another list, from 1 to 1000, in increments of 5).
number_list2<-seq(from=1, to=1000, by =5)

#if you need a function but don't have the package, you can install it as long as you are connected to the internet. use the install.packages() command.
?install.packages()

#some other helpful functions include standard descriptive statistics, such as finding means, meadians, and SDs.

mean(number_list2)
```

    ## [1] 498.5

``` r
median(number_list2)
```

    ## [1] 498.5

``` r
sd(number_list2)
```

    ## [1] 289.3959

``` r
#you can randomly sample from a Z distribution using the rnorm() function.
rnorm(25, mean=0, sd=1)
```

    ##  [1]  1.07990652 -1.10733962  0.01216996 -0.83653185  0.64516742
    ##  [6] -0.11254119 -0.24906934  0.53297538 -2.19770195 -0.64444973
    ## [11] -0.89065708  0.79455059  0.42620103 -0.04163298  0.08941915
    ## [16] -1.34280873  0.74761022 -0.68897648 -1.47518460  0.91180169
    ## [21]  0.73294791 -0.94856961 -2.23830921  1.24487349 -0.27729768

``` r
#you can also generate random matrices with placeholder values, using the matrix() command.
m <-matrix(NA, 50,3) #creates a matrix of "NA"s with 50 rows and 3 columns

#sample() is a useful way to randomly draw from a pre-existing data array, matrix, list, etc., either with replacement or without.

sample(number_list2,8,replace=T) #sample 8 values from number list 2, with replacement.
```

    ## [1] 276 111 106 716 116 156 946 571

Writing your own Functions.

This is a great way to steamline your code and check that it is doing what you think it is doing.

``` r
#writing a function.

#this is a simple function to calculate means. Give it a name and define it using the function() command.
Fred_mean <-function(x) {sum(x)/length(x)} #add all Xs and divide by the length (i.e., the number of elements in the list).

#now you can call your function and use it with any vector of numbers that you have in your environment.
Fred_mean(x=number_list2)
```

    ## [1] 498.5

``` r
Fred_mean(x=c(1,3,6,22,5,3,6,7,88,30))
```

    ## [1] 17.1

``` r
Fred_mean(x=5)
```

    ## [1] 5

You might also want to iterate something across multiple values. You can write a function for this as well, using For loops. They can be very useful, but can process REALLY slowly if you have a larger array (say 50 observations or more).

``` r
#lets say we want to calculate means for multiple columns.

#create a new matrix 3x3, sampling from number list 2, using the cbind() function. cbind() will bind multiple columns together in sequence.
number_list3 <-cbind(sample(number_list2,8,replace=T),sample(number_list2,8,replace=T),sample(number_list2,8,replace=T))

#now use a for loop to calculate means for each column in number list 3.
#for loops need a place to put the values they calculate, so we create an empty vector of NAs.
means_numlist3 <-c(NA,NA,NA)

for(i in 1:nrow(number_list3)){
  means_numlist3[i] <-Fred_mean(number_list3[i,])
}

#the above tells R to loop i times, where i goes from 1 to the number of rows in the matrix we want to calculate means for. We calculate the means using the custom function Fred_mean() we created above [telling it how many rows and columns to create]!

#calling the object will show us the means we want to see.
means_numlist3
```

    ## [1] 102.6667 412.6667 789.3333 661.0000 224.3333 692.6667 581.0000 346.0000

&nbsp;
<hr />
<p style="text-align: center;">A lab note sheet by <a href="http://www.clavelresearch.wordpress.com/" target="_blank">Fred Clavel, Ph.D.</a></p>
<p style="text-align: center;">TWITTER: <a href="http://twitter.com/FDClavel" target="_blank">@FDClavel</a></p>
<p style="text-align: center;"><span style="color: #808080;"><em>E-MAIL: clavelresearch [at] gmail [dot] com</em></span></p>
&nbsp;
