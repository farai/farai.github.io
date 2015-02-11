---
layout: post
title: "Qualities of clean code - Naming of things"
date: 2015-02-11 16:44:23 +0000
comments: true
categories: 
---

Over the course of the months to come, Im going to be focusing on the topic of clean code and noting all the qualities that constitute clean code through reading and re-factoring code, discussions with fellow developers, and drawing from insight gained through Robert C Martin's book, [Clean Code - A handbook of agile software craftsmenship](http://www.amazon.co.uk/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882).
As a reminder to myself of the main attributes to always keep in mind and to share with anyone interested in becoming better developers through improving their own code quality; I will be writing a series of posts detailing the main attributes of clean code and their importance.  
Firstly, what is the definition of clean code? My interpretation of clean code is code that is:

   1.. Simple and easy to understand

   2.. Can easily be modified/enhanced by other developers

   3.. Testable

To kick off the series of posts, I'm going to start with highlighting the importance of how you name things.
Naming is one of the hardest things in software development. Considering how we come to easily understanding some logic is partly hinged on how things were named; it is important we name things properly. By sticking to the following points as rule of thumb we are never going to be far off the mark of attaining clean code.

## Be Descriptive
There is nothing more frustrating than realising time spent while trying to work out what some code does through dumping variables or stepping through with debuggers before you can actually make your code change all because of some cryptic class, function and variable names. The names you choose should be able to quickly highlight purpose and shed light on how an item is being used in a particular context. Avoid single letter variable names and ensure that the names you have chosen are pronounceable . Keep in mind that being descriptive doesn't mean use long names. If the name cannot be noted at a glance then it's most likely too long. 
Consider the following piece of code:

``` php
public function getBlockedItems($dataSet)
{
    $data = [];
    foreach ($dataSet as $key => $value) {
        if ($value['status'] === 'blocked') {
            $data[] = $dataSet[$key];
        }
    }
    return $data;
}
```

Its not complicated having taken a close at the code to understand what it is doing but there is totally no context to what is going on here. Had things been named in a more descriptive manner you would have clearly understood its purpose in half the time. So how could the code have been written in a clearer more descriptive way?

``` php
public function getBlockedAccounts($accounts)
{
    $blockedAccounts = [];
    foreach ($accounts as $accountNumber => $accountDetails) {
        if ($accountDetails['status'] === 'blocked') {
            $blockedAccounts[] = $accounts[$accountNumber];
        }
    }
    return $blockedAccounts;
}
```

With just a few descriptive names, at a glance you can now quickly work out the purpose of the logic and notice what a difference that makes.

## Be Consistent
Try be as consistent as possible in your use of the names. Ensure your choice of names for concepts is clearly distinguishable from other procceses.
Its confusing to have fetch, get, retrieve littered all over the code in an inconsistent manner. With inconsistency it would make it difficult to quickly work out which function will return data with the attributes you are after.

## Avoid abbreviation
Abbreviations are dangerous. Personal interpretation of abbreviations can lead to misunderstanding. You should really avoid using these unless its really unavoidable because extremely long names as mentioned before can also be bad when people are trying to read your code. I would say the only case it might be acceptable is when referring to domain specific phrases.

## Avoid Hungarian notation
If still using Hungarian notion you should have stopped a long time ago. Its a dated concept which doesn’t provide any real benefit these days and most of the time is misused. Attempting to use it will most likely only make it harder to understand and follow what your code is doing. 
To this date a good article still worthwhile reading is Joel Spolsky's ["Making Wrong Code Look Wrong"](http://www.joelonsoftware.com/articles/Wrong.html). His article goes into more detail about the origins of the notation and how the abuse and misunderstanding of it has created issues.

## Avoid misleading names
Avoid using names that in the domain of our language choice and field of computer science could mean something else. Using such names could lead to bad assumptions and false conclusion.

## *Parting words*
As general rule of thumb, take time to think about your names and if you need to add comments to explain the purpose of a variable or function internal in your code, you've probably already messed up. In that scenario revist your code and reconsider your implementation to see if it can be further simplified in such a way the code expresses itself and the author.