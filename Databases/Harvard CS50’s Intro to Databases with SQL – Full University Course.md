---
title: Harvard CS50’s Intro to Databases with SQL – Full University Course
source: https://www.youtube.com/watch?v=WXk7yDqsKxs
author:
  - "[[freeCodeCamp.org]]"
published: 2025-10-09
created: 2026-05-26
description: This is CS50’s introduction to databases using a language called SQL. You'll learn how to create, read, update, and delete data with relational databases, wh...
tags:
  - "#sql"
---
![](https://www.youtube.com/watch?v=WXk7yDqsKxs)

## Transcript

**0:00** · This course is CS50's introduction to databases using a language called SQL.

**0:04** · This course is from Harvard University and is taught by Carter Zeni with help from Dr. David J. Men. In this course, you'll master the fundamentals of SQL, including how to create, read, update, and delete data. You'll learn to model real world scenarios by designing tables, normalizing data to reduce redundancy, and joining tables using primary and foreign keys. The course also covers how to automate queries with views, accelerate searches, with indexes, and connect your database to languages like Python.

### Introduction

**0:36** · The curriculum begins with the portability of SQLite before introducing the scalable power of PostQL and MySQL all through assignments inspired by realworld data sets.

**0:53** · \[Music\] Hello world. This is CS50's introduction to databases with SQL or SQL. My name is David Mailen and my name is Carter Zeni.

**1:15** · CS50 itself is an introduction to computer science and along the way you learn about SQL and more. This course dives all the more deeply into SQL specifically and you can take it before, during, or after CS50 itself, whether you're a computer scientist, data scientist, programmer, or simply someone who's interested in databases. Now, we'll begin with a software called SQL light, which you can use to query a table of data, maybe a table of books, for instance. You will then graduate and work not just with one table, but multiple and see how to define relationships among them.

**1:46** · Afterwards, you'll figure out how to design your very own database from scratch, learning about schemas and data types. And then you'll see how to add data to that database, how to insert, update, and delete some data all together. Soon after, you'll see how to write alternate views for your data, new ways of simplifying your data for yourself and for others. And then towards the end of the course, you'll see how to optimize your queries, how to reduce the time that they take, although at the cost of some space.

**2:17** · And then finally, to cap it all off, you'll learn other DBMS's, database management systems like MySQL and Postgress that you can use to do all of this and more at a much bigger scale. Now, this is CS50. \[Music\] Well, hello one and all and welcome to CSA's introduction to databases with SQL.

### Querying

**2:58** · My name is Carter Zeni and in this course you'll learn how to represent, how to organize and manage, and how to ask questions of the data that's around you in your everyday life. But why learn those skills? Well, you may have heard it. So, we're living in the information age where we generate so much information, so much data by virtue of interaction with computers and with each other over the internet. Uh, you might think of, let's say, uh, Google keeping track of the sites you click on or the sites you search for.

**3:26** · You could think of maybe the smartphone in your pocket or the smartwatch on your wrist, keeping track of health information, emails, text messages, and so on. You might even think of YouTube where you might be watching this same video keeping track of all the videos on their platform, the creators of those videos and even the comment you might leave on this video.

**3:48** · So although we're living in this information age where there is so much data, so much information, we can use these new tools like database and SQL to interact with that information to store it and manage it. And although we're using some of these new tools, some of the other concepts we'll learn aren't actually so new. So here is a diagram from literally a few thousand years ago.

**4:10** · And notice how this diagram has rows and columns. And this seems to store the uh stipens for workers at a temple some few thousand years ago. So given what you know based on your prior knowledge, what kind of name might you give this diagram with rows and with columns? What could we give a name to for this? So I'm seeing some ideas of a table, perhaps a spreadsheet as well.

**4:37** · For our purposes, we'll call this a table where a table stores some set of information and every row in that table stores one item in that set where every column has some piece of information about that item, some attribute of that item. So here for example, we do have a table of workers at a temple. every row is one worker and every column is their stipend for a particular month. So I could take this idea of a table, this very ancient idea, and apply it to a more modern context.

**5:11** · So let's say I'm a librarian for instance, and I want to organize my library. Well, here I have book titles and authors, and I could certainly use a table to store this information, but how might you propose I store this information? What could I do with my rows and with my columns if I have book titles and book authors?

**5:34** · I see one thing I could do is probably organize my titles and my authors kind of next to each other like this. I could take my titles and my authors, put them right next to each other. So, I have Song of Solomon by Tony Morrison, Good Night Moon by Margaret Wise Brown. And notice here how each book is one row, but every row has two columns where two pieces of information for each book. I have a title for one column and an author for the other.

**6:00** · And so together I have a table of books where every column tells me one piece of information and every row tells me one book in this data set.

**6:12** · So thankfully now that we're living in this information age, we no longer have to use no longer have to use like stone tablets or perhaps pencil and paper to store our tables. We have software now like Apple numbers, Google Sheets and Microsoft Excel, but this isn't a course on Apple Numbers or Microsoft Excel or so on. It's actually a course on databases and on SQL. So feel free to raise your hand if you'd like.

**6:37** · But why would we decide to move along from these spreadsheet softwares towards a database? What might that database give us that a spreadsheet might not give us?

**6:50** · So I'm seeing a few ideas here and among them are some simplicity, some ability to organize some data. Um but there are a few other ideas we think about too for why move beyond spreadsheets and go towards databases. Now one of these is this idea of scale. So let's say you are a Google or an Instagram. You're trying to store not just tens of thousands of users or hundreds of thousands but literally millions of users or billions of users. And with that kind of scale, you might be better served by a database to store that much information.

**7:22** · Another reason to move from spreadsheets to databases is this idea of being able to update data more frequently. Maybe you're a Twitter of the world. You're trying to have others tweet multiple times per second. Well, a database can handle that kind of capacity much better than a spreadsheet could alone. And a third reason to move beyond this might be speed. Let's say I'm trying to look up some piece of information in my database. Well, I could do that much faster with a database than I could with a spreadsheet.

**7:50** · You could think of yourself using command F or control F to find a piece of information in your spreadsheet, kind of going one by one through the rows. A database gives you access to more kinds of algorithms you could use to search this data much faster ultimately. So these three reasons among others are those you might want to move beyond spreadsheets and start using databases.

**8:12** · Now it's worth thinking first what is a database? We'll be talking about databases throughout this course. So what is a database? Well, a database is simply some way to organize your data such that you can actually create data, update data, read data, and delete data.

**8:30** · And often these are our four interactions that we'll do with a database, like adding some data, looking at data, deleting data, and even updating it along the way. But the database isn't the only thing in our picture here. We also have a database management system, way to interact with our database. So you might think of perhaps writing a um program on your computer. You have some interface with which to write that program like VS code for instance or you might think of your own desktop on your own computer. You have icons such that interact with the underlying operating system.

**9:01** · In the same way we can use this software called a database management system or a DBMS for short to interact with the database perhaps using a graphical interface or using a textual language too. Now there

**9:17** · are a few uh varieties of database management softwares and these are a few of them here my SQL Oracle Postgress SQL and SQLite but this is a non-exhaustive list so let me also ask again what kinds of other database management systems have you perhaps heard of in this case I'm seeing one for Microsoft Access perhaps um MongoDB there are other kinds of software other companies out there that make these ways to interact act with a database. This is again a non-exhaustive list.

**9:47** · Now, if you are a database administrator or maybe you're somebody who's making a choice of which software to use, you have a few trade-offs to consider. Let's say you might think of one being proprietary, for instance, costing money to work with. What you get for that money is additional support to actually implement your own database. On the other hand, you might have open-source software or free software to use stuff like Postgress SQL, MySQL, and SQLite. But the downside is you are then responsible for actually implementing that database.

**10:21** · Another uh thing to consider too is that maybe some are going to be heavier weight than others more fully featured as a consequence but perhaps heavier weight requiring more computation to run. You could think of those like my SQL or post SQL being a little bit heavier weight but being more fully featured. Whereas SQLite down below will be a little lighter weight as the name might imply, but allow you to do most of the same work that these other softwares could allow you to do as well.

**10:46** · And in this course, we'll actually be using SQLite for you to work with your own databases, but gradually we'll move on to MySQL and Postgress SQL too.

**11:00** · So let me go ahead and talk about then SQL in this case. You might notice that in each of these MySQL and Postgress SQL and SQLite each of them have this idea of SQL in them and SQL is that language that we'll use to interact with our database. Now let me ask what does SQL stand for? Perhaps we talk about SQL or SQL but what might SQL stand for?

**11:22** · So I'm seeing it might stand for structured query language which is good if you already know this but not to worry if you don't. So SQL does stand for structured query language. As we'll see in this course, it is structured. It does have some keywords you can use to interact with a database. And it is a query language. It can be used to ask questions of data inside a database.

**11:48** · We'll see that this is the language we can use to create data, to read data, to update data, and delete data all with SQL in this case. And our next thing will be to talk about this idea of querying. So SQL is a query language. But what can we do with SQL? Well, the first thing we can do we'll focus on first in this course is writing queries.

**12:13** · Trying to ask questions of data using SQL. Well, what kinds of questions could we ask? Well, you might imagine perhaps working at an Instagram or a Facebook trying to work as an engineer to figure out what kinds of posts are the most liked on your platform. That's a question you can answer with databases and with SQL. You might also think of um whether your numbers of daily users are growing or shrinking if you're working at a startup for instance.

**12:37** · Even maybe might be working for something company like Spotify that could ask how could we play songs that are like those a user just played. This too is a question you can answer with databases and with SQL.

**12:53** · Now, today we'll be focusing on this database of books and in particular books that have been long listed quote unquote for the International Booker Prize. The International Booker Prize, if you're not familiar, is a award given to books written around the world by authors from many countries. And it's designed to uh award uh books of fiction are particularly good in some cases. And every year the committee selects 13 books to include on a long list for consideration for this prize.

**13:20** · And our database then has 5 years worth of long lists for the International Booker Prize inside of it. We could use this database perhaps if we were a librarian trying to find books for our library or even as a a book reader, an avid reader myself, trying to find books to read that I could put on my own shelf overall. So, we'll look at this database, but we'll need a few tools in our toolkit, metaphorically, to actually interact with this database. And one of them is going to be Visual Studio Code.

**13:50** · Visual Studio Code is an IDE, integrated development environment to write code and to edit files with. It's also often called VS Code. Now in VS Code, we'll also be able to use SQLite, this database management system or a DBMS for short to actually interact with that database. So we'll be using these two tools combined to work with this database of long listed books for the International Booker Prize.

**14:18** · And although we'll be using it here, SQLite is not uh just used in this course. It's used in a variety of applications. You could think too of phone applications or SQLite is often used on those um devices that have much lower memory. You could think too of it being used on desktop applications to simplify the process of storing data there too. You could even think of it being used on websites to help store information the user submits via a form for example.

**14:48** · So we'll jump into using SQLite but keep in mind that uh not just in this course you'll use it but also it's used in a variety of applications here too.

**14:59** · So why don't we just jump right into things start using our uh environment and start using SQLite. So I'll go over here to my computer and I will open up let's say VS Code where here you can see I have my terminal environment and if you're familiar you can type things like ls to see the files that are in your current folder. So I'll type ls right here and I'll see this database called longlist db. Again working with books that have been long listed or considered for the international booker prize.

**15:28** · So if I want to open up this file, I can use this command. Then this command is going to be called SQLite 3 or I can take some file that I have like long list.db and open it using this program called SQLite 3. Well, it's called SQLite 3 because this is the third version of the SQLite software. So let's try this in our terminal. I'll go back over here and I'll say SQLite 3. SQLite 3 long list db. And now I'll hit enter.

**16:05** · And notice how my terminal prompt changes. It's no longer a dollar sign. It now says SQLite in front. This means I'm inside of my SQLite environment.

**16:15** · So to clear things up, let me just clear my terminal. I can use L for this. And now I have just that prompt up top. And now a question I want to answer in this case first is what data do I actually have in my database? What data is actually here for me to look at and to ask questions about? Now for this question, I can use my very first SQL keyword which will be called select. So select is a way for me to select some rows in a table inside of my database.

**16:49** · Using select I can get back certain rows or in this case perhaps all of them just to get a taste of what's inside. So let's try using select on this database to understand what rows we have in our table here. Let me go back to my computer into my SQLite environment and I will try this very first SQL keyword. I'll say select and I can use this star operator here to say select everything.

**17:15** · I want every row and every column from this table.

**17:21** · Now, it's not enough for me to simply say select star and end my query. I have to tell SQL which table do I want to select rows from. In this case, I know a table is called long list. So, I'll say select star from long list quote unquote. And to end my query, I'll say semicolon. And then finally, I can hit enter. And notice how I get a lot of data back, right? This is a lot of data all at once. But it's because my terminal is a little bit small. There's a lot of rows and columns here.

**17:51** · So I could probably simplify this just a little bit. Instead of saying select star, I could also select a particular column from my table. I could say for instance, select let's say just the title column from my database from my table like this. I just know already that there is a column called title. So now I'll try this instead. Not select star, but select title instead. I'll hit enter. And now this looks a little bit better.

**18:21** · I can see the titles inside of this table from top to bottom. Now the neat thing here is I can select more than one column, too. Let's say I don't want just the titles. I want titles and authors in my search. Well, I could do that as well. Let me try this.

**18:41** · Select not just title quote unquote, but then I'll say comma and some new column to select. I'll select also the authors from this table. And I'll select them from the long list table like this. Now I'll hit semicolon to end my query. Hit enter. And now I'll see a variety of columns here. In particular, the title and the author column.

**19:07** · Now, this is going to back all of my columns so far, and there is a way for me to get back just some of them later on that we'll see. But for now, let's ask what questions do you have on this SQL select statement and how we're getting back these rows.

**19:22** · Do I need to use the quotes around the words like you are?

**19:26** · Yeah, great question. Do I have to use quotes around the words like I am? In general, it's a good practice to use these double quotes around your table names and your column names. These are called SQL identifiers. Later on, we'll see we'll also have strings in SQL.

**19:43** · Strings being collections of characters we can use. For those, we'll simply single quote them to note the difference between a string and an actual column name. So, good style convention here to use double quotes for column names and single quotes for string names.

**19:59** · Other questions, too?

**20:01** · Okay, I wanted to know uh where did we take all this information from? Like uh this data I don't know this list of book where did we take all this information from?

**20:13** · Yeah, great question. Where do we take this information from? So some of this data is publicly available. In fact, if you look at the Booker Prize website, you can find a set of long listed books over the years. In this case, we have books from 2018 to 2023. We'll also see later on this table has data on the ratings of those books and the number of votes that were given to those books.

**20:35** · That data is from Goodreads, this site that aggregates reviews from people like you, people like me who rate books online. So, we've taken data from a variety of sources and combined it into one here. Let's take one more question too from Vinak.

**20:50** · Yeah.

**20:50** · So, I wanted to ask regarding the syntax of what you used in the terminal.

**20:56** · So is the whole SQL light tree is case sensitive because while using the syntax you used capital letters whereas can we use like small case letter as well?

**21:08** · A great question. So here I used capital letters for SQL keywords and lowercase for my table names and column names. Do I have to do that? I in some cases do some cases don't. I think I could use lowercase for these SQL keywords but it's not very good style for instance.

**21:24** · So let me just show you an example of this while I go back to my computer. So the question again was can I use lowercase for SQL keywords? I think I could but the question is should I and and probably not. So let me try this. I'll say select let's say title from I'm in the habit of uppercasing it. So I'll say from and lowercase long list like this semicolon hit enter.

**21:48** · And that still works. But the problem you might run into is someone who's reading your query, particularly a long one, might want to know what are the SQL keywords and what are your column names and other identifiers here. By capitalizing your SQL keywords, you can make it clear that this is a SQL keyword and not some other name overall.

**22:11** · Okay, so let's keep going. And we saw just a little bit ago that we could select title from long list and we would get back a whole list of titles.

**22:20** · Literally all the titles that are in this database. But it's often maybe good practice for me to not look at all the data. Like imagine if we had millions of rows in this in this column, but only to get back some take like a peak of what's inside this database. And for that I could use this other SQL keyword, this one called limit. So limit as its name might imply limits the number of queries or the number of rows I get back from my query.

**22:48** · I could say limit three for instance or limit five to get back only the top three or the top five rows from my table. And let me ask folks if I wanted to peak in this data set how many rows should I try to limit it to?

**23:03** · I could say select title from let's say long list but limit to what number?

**23:10** · I'm seeing 10. So, let's try 10 first. I'll go back to my computer. I'll come back over here and I'll say why don't I select title, select title from long list. But now, instead of hitting semicolon, I will instead say limit 10 semicolon and I'll hit enter. Now, I see only the first 10 rows in my data set. Handy for peeking in at the top of my data set here too.

**23:39** · Let me try not just 10 but five. So I'll say select title from long list limit five semicolon. This then gives me just the top five titles in my database just in whatever order they were added to my table. I'll see them in that order here too.

**24:01** · So using limit we can actually um try to get back a certain number of rows. But this isn't quite that interesting. It's good for peing your data set. I think we've answered that question of what data do we have. But let's say we want to make more advanced queries. We want to find the books that were nominated in 2023 or perhaps books by a certain author. Well, for that we could use this next SQL keyword. This one called where.

**24:26** · So where allows me to get back not all rows but only some rows where some condition is true. So where is often combined with other conditions to make sure I only get back some rows where that condition is true. Let's try looking at that in SQLite to get a feel for what it can do for us here.

**24:47** · So I'll go back to my where and I will then go back to SQLite here uh control L to clear my terminal and I'll then try this query. I'll say select title. Select title. And why don't we also select author along the way. Two columns here. And I'll select them from my long list table. But I don't want all rows. I only want let's say those titles and authors that were long listed in 2023.

**25:21** · So I'll do this. I'll say where the year column is equal to 2023. And notice here how 2023 is not in quotes because it is an actual number, an integer. So I don't need to quote it like I would a string, some collection of characters, or a table or column name. So I'll hit enter here. And what do I see? Well, I see only those books that were nominated in 2023.

**25:48** · Let's try this again. I might try not just 2023. I might try 2022.

**25:55** · Like this. Hit semicolon. Now I'll see those books nominated in 2022. I could keep going. I could say why not 2022?

**26:04** · Why not 2021? Now I have all those books nominated in 2021.

**26:10** · So this is handy. We can set things equal to or not equal to to make some condition here. And we also have others we could use. We saw equals just now, but we similarly have not equals. And we have this kind of obscure operator down here. This one being also equivalent to not equals as we'll see in just a minute. But let me first ask now what questions do we have on how to use where or using select so far?

**26:38** · What are the subsets of SQL?

**26:41** · A good question. Are there subsets of SQL? So um there are in fact SQL or SQL was defined by the I believe it's the ANZI like standard corporation. They have a whole set of the SQL language that is like the official version of it. you might be able to use some subset of that version with the database management system that you actually use.

**27:00** · So for SQLite, we're using a subset of SQL that works with SQLite. Similarly, if you were using another software like Postgress SQL or MySQL, you could use another subset there too. Let's take another question from Teaos perhaps.

**27:16** · Sir, I want to know that can we add 2022 and 2021 in a terminal?

**27:22** · Yeah, good question. Could I um perhaps try to filter by both and by 2021 and 2022? I could do that and we'll see that in just a moment here. So let's keep going and exploring some other options with not equals and then we'll see how we can combine conditions using where to. So let's go back and let's focus first on trying to use these not equal operators. We saw the exclamation point equals and this greater than less than sign put together. So let's try a few of those. Let's say I want to find books that are written by um a certain author.

**27:55** · Well, I could use equals for that. But let's say I also want to find books that are not written in a hardcover format.

**28:02** · They kind of tend to be more expensive and so on. So, I don't want hardcover books. Well, I could try a query like this. I could say select title and format where format is either hard coverver or paperback from my long list table. And now I'll say where the format is not equal to hard cover semicolon. So notice here I'm using single quotes for hard cover. This is a string. It's not a table name or a column name. It is just a string.

**28:33** · So I'm using single quotes here. Everything else though like format, long list, title, etc. Those are all table names or column names. So again I'll hit enter. And now I'll see that these are all in paperback according to my table. I've omitted those that are hard cover. Well, I could also use in this case the kind of greater than or less than sign put together to say not equals as well. Let me just hit the up arrow on my computer to sort of reveal what I just previously typed.

**29:04** · I'll then tab back over and say not exclamation point equals but less than and then greater than. Hit enter now and I should see the very same results. But all I did was change this operator from exclamation point equals to less than and greater than. It tends to be that the exclamation point equals is the more common operator in this case, but they do the very same thing.

**29:31** · Now, one more keyword I could use here that's worth mentioning is this keyword called not. So here I was able to use exclamation point equals or the less than or greater than sign to say not equals. But I could also negate a condition using not. So let's try using this one in our SQLite terminal too.

**29:51** · I'll go back over here and I'll bring back my SQLite terminal. I'll say let's do not this operator here but instead use not. So I might in front of where say where not format equals hard cover. So I have a condition format equals hard cover. But now I'm going to negate it. Take the opposite of it and get back the very same results here too.

**30:22** · Okay.

**30:24** · So to the question earlier how we can combine these conditionals. Let's try that here in just a minute. So, let's say I wanted to find the books that were not just written in 2022 or 2023 alone, but all the books together. Well, for this, I could use a few other SQL keywords that might be a little familiar to you, too. Let's try looking at some of these over here. So, here we have these called and, or these parentheses here, too.

**30:55** · So, using and and or I can change condition. I can chain conditionals. I can put them together to make a more complex conditional, a compound condition. And I could also use these parentheses to symbolize that this condition should come first and then some condition should come afterwards as well. So let's try these in SQLite as well. I'll go back to my computer and again our goal is to find not just books in 2022 or 2023, but books that work across those years as well.

**31:24** · So I'll in this case say select let's go for title and author from my long list table. Now I'll say where the year is 2022 as we did before or perhaps the year is 2023.

**31:46** · And notice how my query is kind of wrapping around my terminal. I could leave it like this or if I backspace just a little bit I could hit enter and now I'm on a new line to continue my query. So here I'll say or the year is 2023 and now my query is done. So I'll hit semicolon and I should see those books published in or nominated in 2022 or 2023.

**32:18** · Let's try a few more here. Let's try using our parenthesis as well. Maybe I want not just these books, but also those that are formatted in a hard coverver format. So I'll say clear my terminal, control L again, and select title as well as let's say format from my long list table. And now I'll hit my new line to sort of extend my query without wrapping it around my terminal.

**32:46** · I'll hit enter and I'll say where the year is 2022 or the year is 2023. That's one condition and I can denote that with a single set of parenthesis here. I also want it to be true that the format is not hard cover. So now I'm adding another condition in here. Now I'll say semicolon, hit enter, and I'll get back only those books are published in the paperback format in 2022 and 2023.

**33:25** · Okay, so let me pause again and ask if there are any questions so far on how we've been using where and select and other conditions as well.

**33:36** · I would like to know about uh the uh we can able to list out the top titles available database like you have mentioned the title order where we can know about it uh what are the titles available in the database using command to know yeah so here I've been using these column names called title and author and I think the question is how would I know that I have these columns well as we'll see in future times together I'll be able to actually look at the schema of my database.

**34:07** · What columns are inside of it. For now, just take it on, you know, you know, my my own word that I knew what was inside this database before I actually started querying it. We'll see later on how you can take a database, understand the columns you have there, too. A good question. Let's jump into some more queries. Then I'll go back to my computer and let's see what else we could do with these conditions. Well, not only could I try to make compound conditions, I could also try to find, let's say, which data is missing.

**34:35** · So, I know in this table I have not just authors of books, but translators of those books. Often books for the international book of Prize were translated from some other language into English. But some weren't, or at least they didn't have a translator that was separate from the author. So to think about what data is missing from our table, we should introduce this new idea. This one called null.

**35:00** · So I'll walk over here and we'll see that we have this type called null where this means that this value doesn't exist. It's not in our database. We can actually put together a condition around this idea of null, something not being there. We could use is null to figure out if a value is null. It's not there. It's missing from our database. or is not null, meaning that it actually is there.

**35:30** · So, I'll go back to SQLite and show you what we could do with some of these um concepts here. Let me go back to my terminal and let's say I do want to find those translators that don't exist in my database. Well, I could use select, let's say, title and translator from my long list. And I want to make sure that these translators are null. they don't exist. So I'll say where translator is null semicolon.

**35:59** · Now I'll hit enter and I should see two books titles are the perfect nine and the enlightenment of the green gauge tree. But notice how over here this value is null. It doesn't exist in my table. I could conversely find those books that do have translators using is not null. And I will try this one again. But in this case, I'll say where translator is not null semicolon.

**36:29** · And I'll hit enter. And now let me just zoom out just a little bit. I can see that I have both titles on the left hand side and translators on the right hand side. All of these actually exist. These are books that did have translators in this case. So a good way to find data that's missing in your table using null or is not null. So let's come back over here and figure out what more we could do with some of these queries.

**36:56** · We've kind of exhausted our work with um some of our you know conditions like chaining them together and using null and so on.

**37:05** · But one more thing we could do is trying to use this idea of matching some kind of pattern in my database. So maybe I'm a uh you know book reader and I want to find a book with the word love somewhere in the title. Well, for this I could use another keyword. This one called like.

**37:25** · So like is a good keyword to use when I want to roughly match some string in my database. Let's say I want to look at book titles and find if some word exists in that title. I could use like for that. And like becomes powerful when you combine it with these other operators, namely this percent sign and this underscore. The percent sign can match any character around a string I give it.

**37:51** · And the underscore can match any single character that I pass in with my string. It's probably best shown with an example. So let me show you some in my terminal here. I'll walk back and again we'll try to find these books that have love somewhere in the title. So I'll say in this case select let's say title from long list. But I don't want all titles.

**38:15** · I only want those that have love somewhere in this title. So I'll say where title like let's say percent love percent semicolon. Now before I run this let me explain what this is doing. I have here a select query asking for the title column from my long list table. But I'll only get back those rows where title is like percent love percent.

**38:47** · Well, what does that mean? Well, the percent remember matches any string of characters. It could match ABC 1 2 3. As long as it some any string of characters comes after and has love, I could match that uh value here. Similarly, the percent sign after says anything can come after love as long as love is somewhere in the middle. So, anything before, anything after, but so long as love is just somewhere in there, I'll get it back. So, let me try running this query then and come back over here.

**39:15** · I will hit enter on my query and I'll see I get back four books, Love in the Big City, More Than Love My Life, and so on. So notice how if I come back over here that each of these titles has love somewhere in it. For this one, I matched love up front and then had any string of characters coming after it like this.

**39:38** · For this one, I had more than I love my life. Uh some string before it and then afterwards any string after it. Love is somewhere in the middle. Let me show you another example too where we use percent in a different way. Let's say I want to find only those books that have the at the very beginning of the title. Let me try this. I'll say select title from long list. Then where let's say the title is like the percent semicolon.

**40:15** · Now I've changed something up. I have not percent in front and behind but only after the 'the'. So in this case I'll get back not anything that has the in the title wherever but now the at the very beginning of this string and I see perhaps a a style mistake. Let me ask the audience what style mistake did I just make when I typed in this query. So I'm seeing maybe I used double quotes when I should have used single quotes.

**40:45** · So let me come back and fix that first. I'll come back over here and again by convention we tend to use single quotes for our strings. So let me fix that right here. And now let me run this query to see what we get back. I'll hit enter and I'll see only those books that begin with the. Now let me show this query again though.

**41:08** · This was our query here. Knowing what we know about the percent sign, what other titles might I accidentally get back by running this query? I have the percent, but what other words might actually begin these book titles? If I were to run this query here, we saw only those with 'the', but if I had other book titles, what might I get back? So I might get back those book titles that have not just the at the beginning but also let's say there or they or so on.

**41:42** · There are many uh words that begin with th e. And if I have the percent sign right after it, I might match one of those words like y or re e or so on. So I didn't have any of those titles in this database, but you could imagine a different database where I have that kind of data.

**41:58** · Let's fix this then. I say I want to match not just 'the' butthe' in a space and match any characters after that to make this query better designed in this instance. Okay. So let me pause here then and ask what questions we have on using percent along with like.

**42:19** · Can we use 2% signs for between two words?

**42:24** · Yeah, I think so. So let me go back to my kernel here and let me try to answer this question. So, can we use two percent signs to say something's between two words? So, let me say this. I'll go with um select let's say title from long list where maybe the title has something like maybe it begins with 'the'.

**42:45** · So I'll say where title like uh title like 'the' and then I'll take any set of characters afterwards but I want to have love also in here too. So I'll say love and then I'll take any other characters after it percent again single quote semicolon.

**43:06** · Now I don't know if I have any books that actually fit this search but I could say the percent love percent to mean give me back any title that has the at the beginning then any words or characters then love then any words or characters after that. I'll hit enter and I see I don't have any books that fit that kind of description, but I if I did, I would see them here with 'the' at the beginning and love somewhere in the title.

**43:37** · All right, so let's keep going. Let's focus not just on this percent sign, but also on this underscore. So if I want to find let's say I don't know what a particular character is in my title I could use this underscore to match any particular character not any string of characters but any single character too.

**43:56** · So let's try this in our terminal and there is a book uh this one called py and I actually keep forgetting how it's spelled. I don't know whether it's p i e or p y r e. It could be either one but I want to find it in my database. So let me try this.

**44:13** · I'll say select let's say title from long list where in this case title is like well I know that it starts with a P and I don't know if this is an I or a Y but I'll at least leave it as an underscore now to say it could be any character here. Then I'll say re sing single quote semicolon. And now I could try hitting enter and I'll see I get back this title called py.

**44:41** · So notice in this case that the underscore is matching literally any single character. This could be a y, it could be an i, but in this case I have this y here. Okay, let me go back and let's actually ask in this case what questions we have on using like with these single underscores if any.

**45:04** · Yeah.

**45:04** · So Carter, I wanted to ask you that as you use the underscore sign here, so can we for multiple characters, can we use multiple underscores in order to find something in the database?

**45:16** · A great question. Could we use more than one underscore to try to find some characters in our database? You absolutely could. So let me try that myself. I'll go back to my terminal and let me try to find a book title this could work with. I'll say maybe select title from long list to get back all the books in this table. I'll hit semicolon and maybe I will go with h um let's try this one uh called till.

**45:44** · Well, maybe I want to just find the titles that have a Y or an I in here, but I also don't know if it's one L or maybe two L's for instance. Let me go back and try this. I'll say select let's say title from long list where my title is like I know it begins with a T. I don't know if this is a Y or an I. And maybe I know that it has maybe one or two characters after it. So I'll try this one. Now I have three underscores, single underscores.

**46:15** · So match any book title that has T and then any three individual characters after it. I'll hit enter. And I'll see I get back till this is the only title that has T and then three characters after it. I could try to get better with this. I could say maybe I'll accept you know five or six characters like that. Hit enter and I'll see whoops I didn't complete my query here. Let me just try it from the top again. I'll say select title from long list where title is like let's say ty hit semicolon. And now I get no matches.

**46:54** · So there is no book in this database that has TY and then let's say three or four underscores for any character after it. Okay, so this covers our use of like, but let's keep going and building more complex conditions to find even more um answers to questions we might have about this data. Over here, let me think what we should show next. We've seen like we've seen some compound conditionals.

**47:22** · Well, let's go back to trying to find books that are in a certain year. So, we saw earlier we had this kind of query.

**47:30** · We could say select title and year from, let's say, our long list. Now, I could try to find those books that are written or nominated in 2022 and 2023. But let's say I want to go further. I want those from 2019 to 2022. A span of multiple years here. So I could try it like this. Where year equals let's go ahead and say 2019 or year is 2020 or year is 2021.

**48:04** · And let me make a new line again. Or year is 2022 semicolon. Now before I run this query, let me ask our audience, what strikes you as being not very well designed about this query? What could I be doing better here? So I'm seeing maybe one improvement is that I don't need to write out or year is this or year is that. I could probably do better with this.

**48:33** · And let's introduce some new keywords for working with ranges in terms of our conditions. So here we can see some new operators to use. We have this greater than sign, this less than sign, greater than or equal to, and less than or equal to. And we can use these to build ranges inside of our queries to say I want something to be greater than this number or less than this number two.

**48:59** · And we can combine these with our and and our or we saw before to get back in this case some set of of rows that match our what we intend to find. So let me go back and try some of these out. I'll try to improve the design of this query. Let me first run it and we'll see. We do get back 2019 to 2022.

**49:22** · But I could probably do better. So let's try using our new operators here that can give us some range capabilities.

**49:29** · I'll say select title and also select year from long list. But now I want those rows where the year is greater than or equal to 2019 and the year is less than or equal to 2022 semicolon. I'll hit enter. Notice how I get the very same results. So I get all those same rows, but now my query is much smaller. It's making use of these range operators I've seen so far. I could even further improve this.

**50:02** · I could make this a little better designed too. Let me go back to some slides and show you. We could use these keywords between blank and blank where this can be some condition or some number. In this case, I could say between let's say 2019 and 2022. This is inclusive. So if I say 2019 and 2022, I'll get back a query that includes 2019 and 2022. So let me try this one.

**50:32** · I'll go back over here and I will now try select title from year from long list where the year is between between 2019 and 2022. Same results now, but just a different way of writing this same query.

**50:54** · Now, what else could we do with these ranges? Well, as we've said before, these books actually have some ratings involved. These ratings are crowdsourced from Goodreads, the site you can review books online. And I want to find maybe the books that have a rating of 4.0 or higher. Well, I could do that now with my ranges. I could say select title and rating from my long list and I could say where the rating is greater than 4.0 semicolon.

**51:23** · I'll hit enter and I'll see now only those books that have a rating of 4.0 or higher like this. I could even combine conditions. So I know that these books have a certain rating, but how many votes did they really get? Well, let's take a peek. I'll come back over here and let me try this one. I could say select title. Oops. Let me clear my terminal again.

**51:51** · So, it's back up top. Select title and uh rating and the number of votes that these books got from let's say our long list table. Now, I want to find those that have a rating of greater than 4.0 you know, and let's say a number of votes, a number of votes is greater than at least, let's go with 10,000.

**52:19** · So, at least we know a good number of folks actually voted on these books to find the best among them. I'll hit enter. And now I'll see we're only down to a few books, four in fact, where each one has a rating higher than 4.0. And indeed each every the vote every every vote row has a vote total greater than 10,000 in this case. So a good way to try to find the top books in our data set here.

**52:47** · Let's keep going with these ranges and let's think about one more thing we could do. Maybe I want to find books that are less than a certain length. So I'll try that as well. I'll say select let's say title and pages from my long list. And now I can make a condition based on pages. I'll say where pages is less than 300. Hit enter. And now I should see that I have all these books that are less than 300 pages long when they were first published.

**53:19** · So let's pause here and ask what questions we have on these range conditions. I just wanted to check if um for a for a proper query in this case um to be able to run operations they have to be integers in the database. Um and I my second question is for when we're matching a string um is it case sensitive or not?

**53:42** · Yeah, two great questions. So the first one here is going to be do I have to use integers in this case and what types maybe should I use and the second one being could I match strings like case insensitively. So for the first one um in this case it'll depend on the design of your database. So we'll see later on in the course how we can choose the types for our columns and how that might impact the types we actually use in our queries. Um for now I made this database so I just know that my my year column is an integer.

**54:11** · My ratings column is a is a real number or a float if you're familiar and my votes is an integer. So I just know to use those numbers there.

**54:19** · to the question of uh matching things case insensitively. Let's actually revisit like just briefly here to show you what that can do. So I'll go back to my terminal and let's say uh I want to find just a book title and I want to type it in kind of sloppily. I don't want to capitalize it like capital books are. So I'll say select let's say title from um long list and maybe I'll want to find that book p again. So I could say where title is like py but all in lowercase.

**54:52** · Now I'll hit enter and I'll see I do get back p. So even though I said where title is like lowercase p y r e I got back capital p yre e. Now this is in contrast to saying where title equals lowercase p. Let's try that. I'll come back over here and I'll say again select title from long list but now where oops where title equals quote

**55:25** · unquote p semicolon I'll hit enter and now I see no results so in this case the equals is going to be case sensitive case matters in this case but like is case insensitive Okay, why don't we keep going then and let's take a look at a few other things we can do with these SQL keywords for querying.

**55:51** · Well, earlier we were trying to find a way to find the best books in our data set. And we did that by filtering them based on some ranges, but we could probably do that a little bit more methodically. In this case, using a new keyword, this one called order by. So order by allows us to take the results of our query and order them as it suggests by some column itself.

**56:15** · So we could put them in alphabetical order or in order by number of votes or in order by number of ratings. And let's just try an example of this to see how order by works for us. But in the end we'll see it can arrange columns, arrange rows for us in a resulting query. So, I'll go back to my my computer and let's try this question here. I want to try to find the top 10 books in my table. So, I'll say select title and rating from long list. Enter.

**56:53** · Not on my query yet though. Now, I'll say order by the rating. And let's only take the top 10. So I'll say limit 10 in this instance semicolon.

**57:07** · So now I've combined some of my prior keywords. I'm using select, I'm using order by, and I'm still using our old friend limit. So let me hit enter here and I'll get back. Well, not quite the top 10. I see rating of 3.05 here and rating of 3.42 down here.

**57:28** · So based on this, what do you think the default ordering of order by is? See it might be from least to greatest. So we saw here that we have rating being pretty small, but we said order by rating. So it starts from small and goes down to large. So we need to fix this in some way. Let's introduce a new addition to order by to have us um fix this query overall. So let me show you that order by does by default sort from least to greatest.

**58:00** · But let's try some addition here. We have not just order by but order by some column and then ascending or descending. So ascending is the default. It means from least to greatest. Descending we can specify meaning from greatest to smallest. So let's try using order by but now with this other keyword called deesc for descending. Here I'll go back to my terminal and let's rewrite this query to include deesc.

**58:31** · I'll say select title and rating from long list. And let me before I run this query let me just clear my terminal so it's back up at the top.

**58:42** · I'll backspace this and then a moment here I'll press ctr L. Now I'm back at the top. I'll say select title, select title and rating from long list where actually not where we're not filtering yet. I'll say order by rating but not by ascending by default for going from least to greatest. I want greatest to least. So I'll say deesc here. Now I can say limit 10 semicolon hit enter. And now I'll see the top 10 books.

**59:16** · Here I have The Eighth Life coming in at 4.52 and the Books of Jacob coming in at 4.06. So now we're going from greatest to smallest. Well, I could order by not just these ratings, but also by the number of votes. Like it seems there's a tie to break here. If I look at Stillborn and When We Cease to Understand the World, those both have a rating of 4.14.

**59:43** · But presumably one book has maybe more votes than the other. So I could try to break this tie by ordering not just by rating but also by votes. The number of votes this book actually received on Goodreads. So let's try that then to break this tie. I'll come back over here and I'll try this query now. I'll say again select title and rating from long list. Now I'll order by first the rating column in descending order.

**1:00:15** · But I also want to order by the number of votes after I order by rating. So I'm saying first order by rating but afterwards followed by a comma let's order by the number of votes also in descending order from greatest to smallest. Now I'll just continue my query on the next line and I'll say limit 10 semicolon.

**1:00:37** · This then gives me, let's see, the books, but now they're going to be in the order that allows us to see the number of votes. Let me just actually refine this. Let me say not just select title and rating.

**1:00:52** · Let's make sure we can see the votes here, too. So, select title and rating and votes from long list. Hit enter on my query. Now, I'll say order by rating and votes. Then I'll say limit 10. And here I'm just hitting the up arrow on my computer. I'll hit enter and now I'll see the votes included. So let me show you this on the big screen. Here we see that the tie is broken. So when we cease to understand the world, these both have 4.14 along with um stillborn.

**1:01:19** · But here this book has more votes and so is higher in our order now that we've ordered by multiple columns. So let me pause here and ask what questions we have on ordering with data. ordering by one column or multiple and how we can sort data like this.

**1:01:43** · Sir, I want to know that can we write rating to 4.93 to uh 4.9?

**1:01:50** · Yeah, good question. So, I think if I understand correctly, how can we select a rating or try to find a rating that's like equal to 4, you know, 92 or things like that? Let's try that here. So, if I want to find a particular rating, I could simply use my uh wear friend from before. I could say select let's say title and rating and maybe I could try to find a particular rating for a book from long list.

**1:02:13** · I could say then where this rating is equal to let's say 4.932 semicolon this if this book exists it'll get it back here. So I'll hit enter and I see there's no book with this particular rating 4.392. But good question for how to find particular ratings for our books here.

**1:02:37** · Okay, other questions too on how we've been able to sort our data and use order by. Will desend work on a string on an alphabetic basis or do we need to have a special conditions for alphabetic characters?

**1:02:54** · Yeah, great question. So, how could we use order by with some characters or strings or some text in our database?

**1:03:00** · Let's try that one out too and see how that works with ASC for ascending and DEESC for descending. So I'll go back to my terminal and I'll demonstrate here how we can use this for some text. So let's try simply sorting our books alphabetically for let's say our library. I'll say select title from long list. Enter. And I want to order by title just plain and simple. And then hit semicolon. Let's see what happens.

**1:03:28** · I'll hit enter. And now I'll see that these books are ordered but they seem to be ordered alphabetically. So here we have some uh titles lower in the alphabet and up here we have titles earlier in the alphabet. So by default order by seems to order alphabetically. If I change that default though from ascending to descending. Let's see what happens. I'll go back over here and I'll try the same query but now using DEESC.

**1:03:58** · Select title from long list order by title now in descending order. Hit enter. And now I'll see these titles in reverse alphabetical order. So notice how earlier on we have titles that are lower in the alphabet, but down below we have titles that are earlier in the alphabet here. So you can use order by with these texts but you then have to specify whether you want it in alphabetical order or in reverse alphabetical order.

**1:04:29** · Okay. So let's show a few um other uh uh you know concepts here we can use alongside of these orderings. One thing we could also do is try to find uh more information about the ratings of these books. So let's say I want not just to order these books but try to find the average rating or to try to find the number of books or try to find let's say maybe the sum of my total votes on each of my books. Well for this we could in we could introduce some new concepts.

**1:05:00** · These ones called SQL's aggregate functions. These allow us to take a whole set of rows and return not each of those rows individually but instead in this case one number based on the values in those rows. You could imagine trying to count the number of rows you have or take the average of the number of rows or take the average of let's say a rating for instance finding the minimum rating or the maximum rating or finding the sum of some votes and we'll see each of these in action here.

**1:05:31** · Let's go back to our terminal. Try some of these out. I will try in this case first um trying to find the average rating from my long list. Well, I know just from experience and as you now know too, I can try to find the average of some column by using the AVG aggregate function. So, I'll say select not just rating in this case, but select the average rating from long list.

**1:06:03** · Notice how in this case I'm using this kind of syntax where I take rating my column I want to aggregate or to sum up or to average like this and I apply the function by saying its name followed by some parenthesis around that column name. So this will return to me not all of the rating rows but the average of the rating rows in one single cell. Let me try this. I'll come back and I will then hit enter. And I'll see this is the average rating. We have 3.7537179471795.

**1:06:42** · So average rating for all of these books. But of course, this isn't great. What might I want to do if I was going to show this to somebody else? I could probably improve the presentation of this in some way. So I could probably round this result.

**1:06:58** · Like I have 3.75 371. We could probably stop after two decimal points, right?

**1:07:04** · Just simply like 3.75. So I could introduce some new keyword here. This one to round the results. Let me show you this one in action. I'll come back and I'll try not just select average rating, but select the rounded average rating. So I'll say select round and then take average of rating and round to two decimal points from long list semicolon.

**1:07:31** · So now this query decides to first find the average of the rating column then take the result and round it using two decimal points.

**1:07:46** · Notice how round takes two inputs or two arguments. The first one being the rating, the average rating. The second one being number of decimal points to round to. And we complete our query in the way we usually do by saying from this table. So let's try this one to figure this out. I'll come back and I'll hit enter. And now we'll see we do get back 3.75.

**1:08:08** · But there is still one thing to improve here. When I write this query, I see this ugly title name, round, average, rating, 2. I wouldn't send this to my boss or somebody else who I work for, maybe even a friend, right? I want to make sure it's pretty so they can read it correctly. So, what could I do then to try to make this prettier?

**1:08:29** · I could maybe rename this column. I could try to take this and make it not just this ugly mess of SQL keywords, but to give it some name I could use instead. So, for this, we'll introduce a brand new one. new brand new keyword called as. Let's try this one too. I'll come back and I'll say select again round average rating, 2. But now I'll select it as let's say average rating.

**1:08:56** · And now before I actually finish this query, let me try to bring it to the top of my terminal. We can see it all in one go.

**1:09:06** · I'll backspace this and I'll say select select um the rounded version of the average rating rounded to two decimal points as let's go ahead and call this one average rating. Now I'll hit enter and I'll say from my long list table semicolon. Now I see it's much prettier overall. I have no longer these SQL keywords but instead just average rating as my column name. Okay.

**1:09:34** · So let me pause here and ask questions then on using average or using um round or using as in these cases.

**1:09:48** · I'm wondering do these sort of commands have like a function like are these commands called something like data type called something are these commands also do have a name?

**1:10:00** · Yeah.

**1:10:00** · And can I ask are you referring to like the AVG like count like sum those kinds of things or Yeah. So these functions do have a name. They are called aggregate functions and aggregate means to combine to bring together. So they're called aggregate functions because they take some number of rows like all my ratings for instance and bring it down to one single cell like the average or the sum or the count. So if you look up or read more about SQL aggregate functions, you'll see all of these and perhaps some more depending on the software you're using.

**1:10:33** · Okay, so let's keep going then and try to start counting um some other rows and use our other aggregate functions here. I'll go back to my terminal and so far we've seen average as well as um we have seen round and so on but why don't I try to find the maximum or the minimum rating in my table I'll say select let's say the max rating from my long list

**1:11:00** · semicolon hit enter now I see the highest rated book was had a rating of 4.52 well what about the minimum rating I could use min here too I could say I select let's say min of my rating column from my long list table I'll hit semicolon and I'll see 3.05 05 that is the lowest rated book I have in this in this set. Well, as we've seen, let me try to um view this for you all. I could say select um title and votes from my long list.

**1:11:33** · It's like title and votes for my long list. Here I have many books with many user generated votes. Maybe people on the internet decided to rate this book out of five and maybe uh go Went Gone got about let's say 592 votes.

**1:11:50** · So I'm curious then how many total votes do I have in my data set? Well for that I could use the sum aggregate function try to count up each one of these rows and return it back to me in a single cell. So I'll use sum here. I'll come back and I'll say I want to find the sum of my votes column. I'll say select let's say um the sum of my votes column from my long list table and then I'll just hit enter semicolon enter.

**1:12:21** · And I'll see over 600,000 people offered a vote for each of these books that were long listed for the International Booker Prize. Now that' be a few more here. So let's check out what else we have left to do in our aggregate functions. We could also try to count up just the number of books in our data set. So why don't I try to find the number of rows I have.

**1:12:47** · For that I could use count. And often to find the number of rows in your data set, you might use count and star as we saw a little earlier. I could say select count star from long list. And this means again star means give me every row and every column give me basically my whole table right and if I say count star that means count up the number of rows that I have in my database. So I'll say count star from long list and I get back 78 books in this database.

**1:13:17** · Well let me try counting up the number of translators here. I'll say select let's say count of translators from long list semicolon hit enter and now I see 76.

**1:13:36** · So I have 78 books but if I count translators I have 76 of them. So why might that be? If you were to raise your hand and try to guess at this. Why do I have 78 rows but 76 translators?

**1:13:55** · Um, hello. I actually had raised my hand for a question.

**1:13:58** · Yeah, go ahead.

**1:13:59** · Also, I wanted to know whether the max and the min function can be used for finding the longest or the shortest string as well or do you have a different command for that?

**1:14:08** · Ah, good question. Could we use max and min to find the longest or shortest string? That's a a good question. So, let's actually pause on this counting here and try that out real quick. So, I'll come back to my terminal and let me try to use max and min with some book titles. So, I'll say select um let's select the max um title. And at the same time, why don't we select the min title as well and I'll select these from my long list table. I'll hit semicolon. And now, let me try this out. I'll get back wretchedness and a new name.

**1:14:42** · Septology 6 through 7. Now, there's a few hypotheses here. It does seem that our max title is shorter than our min title. So, it's probably not that max gives us the length of the string. But what do you notice? Well, I see min is really early on in the alphabet. It has an A here, whereas max has a W, pretty low in the alphabet.

**1:15:09** · And I would bet if we ordered these book titles, we would see a new name up at the very top and a wretchedness the the book here down at the bottom. So max seems to give us the lowest alphabetically which is kind of contradictory with um titles here or strings and min gives us the earliest in the alphabet using this a as well.

**1:15:34** · Okay, so good question. Let's come back to our counting here. So let's go back to my terminal and again we had in this case 78 rows but only 76 translators. So again if I did select count star from let's say long list then semicolon I got back 78. But if I do select count of translators translator from long list I get back 76.

**1:16:01** · Let me ask again. Why do we have 78 rows but 76 translators? You're free to say it. Okay. So, I'm seeing maybe we have some number of rows 78. But for our translators, you remember two of those were null values. They didn't exist in our table. So, it seems like if we use count star, we're counting all the rows.

**1:16:26** · But if we use count translator, some column that has null values, we're only getting back those rows or those values that aren't null. So count when given a column counts only those that are not null or that exist in our table. Okay, let's look at one more example here for counting. And let's try this.

**1:16:47** · Let's say I want to find all of the publishers in this database. I'll say select count of publisher from my long list and I'll hit semicolon.

**1:17:00** · So you might think that I have 78 publishers in this long list, but would it be accurate if I were to say I have 78 different publishers in this long list? Could I say that?

**1:17:16** · I'm seeing no, right? I couldn't try to count up these publishers and then say I have 78 different ones. I might double count a publisher along the way. And let me show you what we mean here. So I'll go back to my table and let me try to select from publishers or select the publisher column from long list. I'll select publisher from long list. Hit semicolon.

**1:17:39** · Whoops. And now I see something a little odd. Let me scroll back up and maybe ask for a raised hand here.

**1:17:49** · Why might I get this odd result?

**1:17:55** · Because of the quotes.

**1:17:57** · Yeah.

**1:17:57** · So I I think I mistyped some of my query here. I said uh it looks like publisher instead of publisher. And in this case, SQL will give me kind of what I asked for. I said select pubser from long list. And says okay, here it is.

**1:18:11** · But that column doesn't exist. So it kind of creates this data for me. So let me try this again. I'll go back and I'll hopefully type this correctly. Now I'll say select let's say publisher this one from long list semicolon. And now I'll see all of the publishers that I have in my table. But what do you see?

**1:18:34** · Well, some repeat, right? I have uh Harville secker multiple times here. I have similarly uh Macose press multiple times as well. So if I counted up these publishers, I would get each one counted one time. But if I want to find the distinct ones, the different ones, I need a new keyword for this. And for this, we'll use this keyword indeed called distinct. Trying to find unique values from our column. So let's try this. I'll go back over here and I will now select not just publishers but distinct publishers.

**1:19:06** · I'll say select distinct publisher from long list semicolon. Now if I scroll through here I should see each publisher in here only one time. If they have the same name they've been filtered out and now they're only the same publisher here too. So I will then try to say select let's say count of publisher select count of publisher from uh count

**1:19:37** · of distinct publisher for instance count distinct publisher oh typo publisher from long list semicolon and I'll see I have 33 distinct publishers.

**1:19:55** · Okay, so this just about brings us to the conclusion of all of these new SQL keywords here. We've seen so far we have several here to use, but let's figure out how to actually exit this prompt. So you might be in your SQLite prompt right now. If you want to leave it, you could also use this commandquit.

**1:20:15** · Dotquit is not a SQL keyword. It's a SQLite keyword to leave your terminal and go back to where you started. So just to review then what we've seen so far is how to select data from our table. We can use select column to take some column from our table and give us back all of those rows from that table for that column. We've seen we can apply some aggregate functions to take maybe the count of our columns or the average or so on.

**1:20:43** · And we could get back not just all of our rows but only some of them using our wear clause here along with a condition. We could have multiple conditions having not just one but perhaps two like uh like let's say here condition zero and condition one and we could also use we saw before this idea of equals and like to match some pattern or to make something exactly equal over here. We could again use and and or we saw later on how we could order our data and use our limit function to get back only some number of rows.

**1:21:14** · Now, this then is our introduction to querying. And so far, we've seen this world of books. And the table we've had so far really just has books inside of it. But next time, what we'll see is how to take this world of books and split it into multiple tables. How do we find information on publishers or books or authors, too, and how do we try to put that in a table that can represent the relationships among all of these different entities?

**1:21:43** · We'll talk about all that and more when we come back next time, and we'll see you there. \[Music\] Well, hello one and all and welcome back to CSG's introduction to databases with SQL. My name is Carter Zeni and last we left off, we learned all about querying, how to ask questions of data in a single table.

### Relating

**1:22:20** · Today though, we'll take one step forward and we'll have databases that have not just one table inside of them, but actually multiple tables. Tables for authors, tables for books and for publishers and so on to represent all these people who are part of the book industry. And you too can apply these same skills for whatever you want to represent as well. So let's pick up where we last left off, which was with this database of books. I'll come back to my computer over here.

**1:22:46** · And if you recall, we had this data set that was the books that were long listed for the international booker prize. To be longlisted means to be nominated for some prize in a given year. And the international booker prize is awarded every year to one book, but 13 are nominated. So in this data set, we have 13 books for the past five years that were nominated for this prize. Now, I'll go ahead and open up this database once more.

**1:23:16** · And if you remember, we used this command last time to open this data set. SQLite 3 space the file name where our file name was long list. DB. And this is one example of our database management system. This one called SQLite and this one being the third version of SQLite.

**1:23:35** · So let's reopen this database and let me show you what we have now in store. I'll type SQLite. Oops. So I'll type SQLite sqlite 3 and then long list db and I'll hit enter. Now my prompt changes. I no longer have this dollar sign. I now have the SQLite prompt. And here's where we saw last time I could write my SQL queries. Well, before we start, let's see the changes to this database.

**1:24:01** · So if I want to get a feel for the tables that are inside of this database, I can use a command. this one called tables. Notice this is not a SQL keyword. This is a command particular to SQLite to show me what tables are inside this database. So I'll type enter here. And now I see I have more than one table. I have a table for authors, a table for books, for publishers, and even more.

**1:24:29** · And now that we're working with not just one table, but multiple, we're actually moving into this idea of a relational database. So no longer do we have a database with only one table inside of it. We now have multiple. And these tables presumably have some kind of relationship among them. You could think, for instance, of an author writing a book or a publisher publishing a book or even a translator translating a book.

**1:24:58** · So we'll have these tables and these relationships among them. So let's look at one example of this kind of relationship among tables.

**1:25:08** · I could have a table of authors and a table of books. This simplified for now to one column in every table. Well, my author's table I have names. In my book uh table I have titles. And we seem to be moving in the right direction. I could store more information about authors and books. But I've also created some problem like how do I know now who wrote which book?

**1:25:30** · Like earlier we saw that you know maybe Eva is right next to Boulder in a single table for authors and books and we know that Eva wrote Boulder that way. But now if I look at authors I only see Eva and no information about books. So we seem to have this problem here. Well one solution uh might be something like the honor system. I mean, I'm honest and so are you. We could say that, well, maybe the first row in authors will always correspond to the first row in books.

**1:26:02** · So, we always know Eva wrote Boulder because Eva is first in the author's table and Boulder is first in the books table. Similarly, let's say Han wrote the white book because Han is in the second row and the white book is in the second row in books.

**1:26:18** · But I have to imagine, I mean, as good as I am at being honest and transparent, maybe I make a mistake. Maybe I add a row to books but not to authors. Or maybe I add a row to authors and not to books. I could change data and not update it to adhere to that standard. So let's actually take a step back and maybe think, well, is it better then to have this kind of situation where we did have one table with authors and books?

**1:26:45** · It might be. But let's think. I mean, this could work for a while. But let's say Olga is a prolific author. They like to write not just one book, but two. They wrote not just flights, but also the books of Jacob. Well, let's say Olga writes another book or another one too.

**1:27:03** · What might be the problem with this arrangement now? And feel free to raise your hand too with your ideas. Why run into some issues here? If we only have one table of authors and books, there is some redundancy, some repetition.

**1:27:20** · Yeah, a good idea. So, you might notice there's some redundancy here. I mean, Olga is in here twice, which is maybe okay if Olga wrote two books, but again, let's say Olga wrote three or four or five. Olga will be in here that many times. And so, we could probably do a bit better than this. And let's actually just say this isn't going to be the most efficient idea for us, let's go back to these multiple tables here and think about how we could relate these two tables one to the other.

**1:27:46** · Now, before we get into the details of how we might do this technically, let's think about the kinds of relationships we could have between authors and books. Well, maybe in our world, we have one author that writes one book. And maybe we could say every author only writes one book. And similarly, one book is always written by one author. This could be true for some books and some authors. But arguably, it's not the best assumption, right?

**1:28:16** · We probably have authors writing more than one book or books being written by more than one author. So, as it stands now, we could call this kind of relationship a oneto-one relationship. If this is our idea of authors and books, one author writes one book and one book is written by one author. This is a oneto-one relationship.

**1:28:40** · Well, as we know, authors can write more than one book. Olga, for example, didn't write just flights, they also wrote another book. And so, we could say, well, Olga wrote not just this book up top, they also wrote this book down below. And now we're moving from a one to one relationship to what we'll call a one to many relationship. There are many books that one author could write.

**1:29:08** · But of course, is this the full picture, too? I mean, some books are only written by one author, but presumably some books are written by multiple authors. So, we need to enhance our picture even further. Let's try that. Let me add another author into the mix here. This author wrote this book along with Olga, let's say. So notice how here we have one author writing more than one book.

**1:29:36** · And we also have one book being written by more than one author. Well, this is called a many to many relationship. And it's called that because we have many books that could be written by many authors. So these in general are the kinds of relationships we'll have amongst our tables in a relational database. One to one, one to many, and many to many.

**1:30:03** · Now thankfully there are some tools we can use to visualize these kinds of relationships. We have at our disposal something called an entity relationship diagram. Something a bit like this. It's also called an ER diagram for short. And let me propose just for now that this is the diagram for our database. We have authors and publishers and translators, books and ratings. These are our entities in our database. The things we're trying to represent.

**1:30:35** · Now, you'll notice though that there's something more than just these boxes that have author, publisher, translator, and so on. There are all these lines among them and they have verbs like wrote and published and translated. And maybe that makes sense to you, but at first glance, like there's one line here that has three lines coming off of it, one line going across. This one has a circle on it. I mean, what does all that mean, right? This is kind of confusing at first glance. Well, this actually has some order to it, some rules that we can use.

**1:31:06** · And let me show you what those rules are. So here we have what's called a crow's foot notation. A way of trying to represent one to one, one to many or many to many relationships using just lines and in some cases circles. So here if you ever see this line with a circle on it, you could think of zero. This doesn't have to have anything related to it. You could think of this one with a bar going perpendicular as one.

**1:31:34** · something with this arrow has to have at least one thing that relates to it in some other table. And this one down below, the one that looks like a crow's foot, well, this one means that some entity has many that could be related to it in some other table. So, let's try this with an example. Here we have again our authors and our books. And here we can say that an author wrote one book.

**1:32:00** · We read this left to right. In this case, one author can have one book associated with them. We know it's one because we see this bar over our line here. Now, we know too that books, at least in our world, could be written by one author. They must be written by at least one author. So, let's try this.

**1:32:19** · I'll include that arrow on the other side, too. And I'll read this right to left. A book has to have at least one author.

**1:32:30** · Now I could add in more symbols too. We know that books could have more than one author and an author could write more than one book. So let's try enhancing our diagram even further. I could say adding in these crows foot notation with the multiple multiple lines here. Now I could read it like this. An author going from left to right can write at least one book but they could write many books. They could write one or many books. And similarly, a book could be written by at least one author, but certainly also multiple too.

**1:33:05** · So this is one example of an er diagram for our database. And hopefully now you can see uh a bit more of this making sense to you. So we see that authors here could write many books. Book could be written by many authors. Books actually don't need to have a translator. They could have zero to many translators for their book here. But in general, a translator should write or should translate at least one book or possibly many of them too.

**1:33:32** · So let me pause here and ask what questions do you have on these table relationships and these diagrams that we call ER entity relationship diagrams?

**1:33:48** · Yeah.

**1:33:48** · So K I want to ask that for any given database how can we predetermine whether how the relationship between the tables are going to be because here we know that the author has some relationship to the books but how can we determine whether those relationships are existent in the for first place a great question if we have some database how do we know the relationships among those entities or those things that are stored inside of it well part of this is really up to you I mean when you're designing designing a database.

**1:34:18** · As we'll see in a future week of this course, you have decisions to make. Do you want an author to be able to write only one book or multiple? For instance, often when I design a database, I might write a diagram like this. So, I could show this to somebody else who can know what tables I have and how they're related to one another. So if you're designing, you have the choice. But if you're taking data from someone else, you could ask for a diagram like this that could show you those relationships among those tables.

**1:34:48** · Let's see what other questions do we have too on these tables and their relationships.

**1:34:55** · How do we determine that relationship? I mean we know that it exists but how we assign which author wrote which book or multiple books or which book were written by what authors.

**1:35:09** · Yeah, great question. So how do we try to assign then these relationships perhaps in our database? Like we know that an author could write multiple books but how do we present that in our table? Let's say um well for this let me just transition to the next part of what we'll talk about which is going to be this idea of a key. So keys are this fundamental idea in databases that can help us relate tables one to the other.

**1:35:32** · And for this, let's actually do a bit of a an example, a bit of a roleplay here. So I will be your librarian today. And let's say that you're looking for a book. This one is called The Birthday Party. And I say, "Okay, I'll find you this book. I'll go to my computer here and I will try to find you the birthday party." Here though, I have two options.

**1:35:54** · I seem to have The Birthday Party by Wendy Danfield and The Birthday Party by Lauren Movenier. So, let me ask you, if we're on the phone perhaps, which one do you want?

**1:36:07** · Hearing feel free to to vote. Which book should we search for? The one by Wendy or the one by Laurent?

**1:36:16** · I'm hearing maybe going for Laurent. So, let's try Laurent over here. We'll search for the one by Lauren. So, The Birthday Party by Lauren Movenier. Okay.

**1:36:24** · Okay. Let me find you that book. But, well, now there are still two books I could choose from. Do you want it in hardcover or paperback? And so, I could ask you again, well, which one do you want? Do you want it in hard coverver or paperback? And again, feel free to vote.

**1:36:40** · Which book do you want?

**1:36:44** · Okay, I'm hearing we're going for I think closer to paperback. Let's try that one. So, I'll search for The Birthday Party by Laurent Movenier in paperback. And there are still two of them. Like, which one do you want? We have first edition and we have second edition. So, I would ask you again, which book do you really want?

**1:37:06** · And you could keep voting here, but for the sake of just keeping this going, I mean, let's pause here and think of a better way to do this, right? My life as a librarian would be much easier if you had given me a simple number. This number is called an ISBN. And it turns out that every book has a unique identifier called an ISBN.

**1:37:32** · Now, what is an ISBN really? Well, if it's the case that every book has a unique ISBN and I can only find one book if I have an ISBN, this is what we call in database terms a primary key, something that is going to be unique for our book or for any item that we have in our table. Now, here's one example of an ISBN. Notice how we have 978-1-840, whatever it is.

**1:38:00** · We could use this to uniquely identify at least our books, but we could extract this away and use this in more than one place. Not just for books, but for publishers, for translators, for authors as well, giving them each some ID that uniquely identifies them. So, here's one example of our table. Let's say that I have a table of books and I used to only have titles, but now I actually have more than a title. have an ISBN to uniquely identify each of these books.

**1:38:29** · And this is handy for me if I wanted to look up some book and know exactly which one I was talking about. Now, these are all fine and good in tables. They're very helpful. But we could do a little more with them. We could get to this question of how do we actually relate these tables together? We could use these primary keys for that. Now a primary key becomes useful for that kind of work when we treat it as a foreign key let's call it. Well what is a foreign key?

**1:39:00** · Well a foreign key is simply taking a primary key from one table and including it in the the column of some other table. So here we have in the ratings table the ISBN column still this is the primary key for the books table but now notice how it's inside the ratings table. This is now a foreign key because it is outside of this books table and inside the ratings table. And what could I do with this?

**1:39:28** · Well, I now see if I want to find all of the individual users ratings for for Boulder, I could look what is the ISBN of Boulder and then which ratings correspond to that ISBN in some other table. So this is an example how I could represent these one to many relationships.

**1:39:48** · I have here a table that has an ISBN or a list of ISBNs and I have another table that can tell me which ratings correspond to this ISBN this primary key in this other table here.

**1:40:04** · Well, that solves one picture here. How can I represent these one to many relationships? But we could also think about how we do the many to many relationships as well. And for this we'll need to think about how do we can improve our primary key here. So let me ask this is an ISBN but if I want to put this inside of a computer like over and over and over again as a primary key the unique identifier what problems do you think I might run into here if any?

**1:40:37** · What problems would I get by using this ISBN as my primary key? you would like run out of memory.

**1:40:44** · Run out of memory. It's a good guess.

**1:40:45** · Like if I had a lot of ISBNs, let's say I had not just 78 books, but I had literally millions of books. I mean, this is a lot of data to store. If you treated each of these as an individual character, that's about one bite, eight bits per character. That's, let's say, 13 plus four dashes, 17 bytes per per ISBN, which takes up a lot a lot of space. So, what if I instead said I'll remove the dashes like we did before and I'll treat it as a number. Well, in that case, I might also have a problem.

**1:41:16** · Like, let's say an ISBN begins with zero. And if I convert that to a number, I'll lose that beginning zero because it doesn't really mean anything in the context of being a number. And now I've lost my unique identifier. So, we could improve this even further and we could actually construct our very own primary key. This one, let's just say, will be called one for this book. And some other book we could call it uh two. Some other book maybe three.

**1:41:45** · And it doesn't quite matter what number we choose so long as this number uniquely identifies the book that we choose. And we don't use that number for any other book as well. So let's actually rethink this relationship of one to many here. Let's say let's not just use ISBN. This is a lot of space to use. to someone point earlier. Let's go ahead and use the ID. Let's make our own primary key in our books table and use that as the foreign key in ratings. So, we freed up a good amount of space here.

**1:42:19** · And notice, too, that maybe Boulder has the primary key, the ID of 1. The white book has the ID of 74. Well, doesn't matter if it's 1 2 3 or four. It doesn't. As long as 74 uniquely identifies the white book, we're okay. So here we have an example of a one to many relationship, but now improved.

**1:42:43** · And with this improvement, we could then think about many to many relationships as well. I could take the same idea and use it to relate authors and books. So let's think about this relationship. Now here too let's say I have a table of authors and a table of books and notably each has a primary key. So I could use that primary key for authors and for books and perhaps put it in some new table.

**1:43:11** · This one let's say is called authored and I'll have one column for author ID and one column for book ID. And based on the context clues here, what might it mean if I looked at the authored table and saw 23 next to one where 23 is in the author ID column and one is in the book ID column to raise your hand. What would it mean for me to see those two numbers next to each other?

**1:43:44** · Yeah, it would mean that uh the author that is that has the ID of 21 uh 23 has authored the book one.

**1:43:52** · Yeah, a great instinct here. So if I look at author ID, I see 23. Well, I could consider that maybe the author with the ID of 23 wrote the book with the ID of one. And I'll concede there's some extra work here. Like I have to figure out now who has this author ID of 23. Well, turns out if you look in the author's table, it's Eva. Similarly, for the book ID, I now have to go through the process of figuring out, okay, well, the book ID is one. What then is the book title? And I'll look for that in my books table over here.

**1:44:24** · So, it brings in a bit more work for me, but ultimately I think we've solved our problem from the very beginning of lecture trying to relate authors and books. We can now do that using both primary keys and foreign keys. So let me ask then what questions do we have on these keys and how to use them?

**1:44:46** · So if the I can the ID of the author and the book ID be the same? For example, can there be a author ID of one and a book ID of one or will they be mixed together?

**1:44:59** · A really good question and good thinking here. So let's consider that maybe an author ID matches a book's ID like both authors both the author and the book have this ID of one that's actually I would say okay in our case because we know that at least one refers to authors and one refers to books as we'll see in

**1:45:22** · future lectures too when I make this join table also called a joint table or junction table an associative entity I could claim that this column called author ID references the primary key column in authors and that primary key only. I could do the same thing for the book side. I could say the numbers in here reference the primary keys in the books table and those IDs only.

**1:45:45** · So I could actually have authors and books with the same ID so long as my tables know that if I have this column I'm looking for author IDs. This column I'm looking for book IDs. Great question.

**1:46:00** · Let's go to one more here. Um, I was wondering, it feels like having more and more tables because once you do this on a big scale, it adds up would use up a lot of space as well. How does it uh how do you deal with the tediousness of it adding up?

**1:46:17** · Yeah, good question here. So, if we had a lot of these kinds of tables, wouldn't that take more space? And I think your answer the answer to that question is it would, but we do gain some things by being able to do it this way. Okay, so for example, let me go back to my authors and books table. Um, in our database, we'll see we have not just author names, but also the year they were born, the city they were born in, the place that they were um, living in certain periods of their life and so on.

**1:46:42** · So, we could have much more information in these tables that we couldn't store as one table earlier because of these redundancies we saw a little bit earlier. So I think although this might take up a little more space, use a little more um tables, we can get around that as we'll see later on with some creativeness with our queries too to um address that that downside. But a good question, a good thought for trade-offs here. Let's go to one more here.

**1:47:10** · Uh so my question is that can the ID be updated and if so does it automatically get updated in the one that has both the ids together?

**1:47:20** · Yeah, good question. So, maybe we want to change the ID of some book or author. Could we do that? Uh, I would say you could, but it's kind of a dangerous game. I mean, if I changed Eva from 23, let's say, to uh let's so we change 27.

**1:47:37** · Well, I could get EVA confused with gauze. And I need to be doubly sure that when I'm changing these IDs, I'm making sure that I'm not making an ID nonique.

**1:47:50** · I'm not making it an ID that somebody else already has. And so for that reason, we very rarely change IDs. In fact, we tend to just abstract them away. So we don't actually know the ID of any particular author or the ID of a particular book. We just use them in our queries as we'll see in just a moment.

**1:48:07** · So wonderful questions here. What we'll do is take a very short break and come back to see how we can use these same tools of keys to not just relate tables, but to query them too and find answers to our questions across these tables.

**1:48:22** · We'll be back in just a minute. Well, we're back and what we saw before was how to relate our tables using keys. We saw that we could have tables of authors and translators and books related to each other using primary keys and foreign keys. So what we'll do now is figure out how we can query these tables using different techniques to that in this case might actually use primary keys and foreign keys within those same queries.

**1:48:49** · Now one technique we could use is this one called sub queries also called nested queries too that basically put one SQL query inside of another. And they're useful in a few different cases but let's say I have one case of a one to many relationship. Maybe I have publishers that are publishing many books, for instance. Well, I could use sub queries to help me answer questions about these kinds of relationships in my table.

**1:49:16** · To make it more concrete, let's say I have a table of books and I want to figure out which of these books were published by Fitz Caraldo editions, my favorite publisher. Let's say what's the problem here? I want to find the books published by Fitz Auto editions, but what am I missing? Feel free to raise your hand and answer.

**1:49:42** · Well, we don't have the name of the publisher in the same table and we haven't made the relationship with the other table to know the name of publisher.

**1:49:51** · Yeah, good observation. So, I want to find the books that are published by Fitz Caraldo editions. And as you noted, well, there's no publisher name. There's just the ID. So, I need to have some way of knowing what these IDs correspond to. And and thankfully, I do have a way of knowing that. I have a table called publishers. And this has a a column called ID and a column called publisher.

**1:50:15** · And what do I notice? Well, I notice that Fitz Caraldo editions has the ID of five. So, I could probably solve this problem. But let me ask again, what queries might I need to answer this question? And there are two queries that I need to do to answer the question of which books were published by Fitz Carlo auditions. What two queries are they?

**1:50:40** · I think it's select and where did you mean keywords or queries?

**1:50:46** · Yeah.

**1:50:46** · So keywords would be great. So I need to have some kind of select involved. I need to probably select something from publishers and something from books. So could I ask you what would I select from publishers and what would I select from books then let's take either another hand or following up here.

**1:51:06** · Okay.

**1:51:06** · So we would take the publisher. So select publisher ID from uh where publisher equals the publisher name we're looking for. And then uh we would nest this query inside the other one. So we can find the the name of the book published by this publisher since we found the ID.

**1:51:26** · Yeah, some good ideas here. And let me propose to do it a bit visually here first. So I want to figure out first what is the ID of Fitz Caraldo editions?

**1:51:36** · Well, I could write a query to find that and I'll say get back five for Fitz Caraldo editions. Well, that's one step.

**1:51:43** · But my next step is then to say what books fit that publisher ID. So I'll write another query this one to determine which titles have a publisher ID of five and I'll get back let's say minor detail and paradus. So let's make this more concrete as you were doing yourself John Paul and let's write these queries out. Let's say I have this first one to determine what is the ID of Fitz Caraldo editions.

**1:52:08** · I could say select ID from publishers where the publisher is Fitz Caraldo additions and I'll get back from this query the number five. Well, I could use that number in my next query.

**1:52:24** · As we saw visually here, I could then say select title from books where the publisher ID is five and I would get back many titles here. But here's another question. Why is this not very well designed? At least in the query I have here, what could I improve about it or what kind of smells wrong about it for you?

**1:52:50** · They are not connected.

**1:52:51** · Yeah.

**1:52:51** · So, Jean Paul, as you said too, they're not connected. And here I have this ID of five, but I mean I don't want to remember this number. I mean, I don't want to have to keep it in my mind and like use it later on in my queries. I ideally could use some other query to find this number for me more dynamically. And so SQL supports this idea of writing a sub query, a query within a query. For example, I'll take this and I'll convert it to the query we had before.

**1:53:21** · I'll select title from books where the publisher ID is equal to well the result of this query here. And notice how I have parenthesis. This means the query furthest inside the parentheses will be run first. So first this query is run. I get back five. Then I could finish out my query and say select title from books where publisher ID is equal to five.

**1:53:50** · So let me pause here before we do some practice in our SQLite terminal. What questions do we have on these kinds of sub queries so far?

**1:54:02** · I was wondering what would happen with um those records that don't match in the subquery.

**1:54:07** · Yeah, good question. So if the ID doesn't match, is that what you're asking?

**1:54:15** · Yeah, I'm hearing yes. So if the ID doesn't match, um that's a good question. So we can treat it as we would a regular old SQL query that we learned about um in last week. So we said select title from books where publisher ID is equal to let's say some value and we'll then filter out all of those that don't have that particular value. So if we have a publisher ID of six or of three those won't be included anymore because we said where publisher ID is equal to five. And now looking at this query too.

**1:54:48** · Well, let's say I might write select ID from publishers where publisher is or equal to Fitz Caraldo editions. Maybe that publisher doesn't exist. There's no publisher with that name. Well, in that case, this query would return nothing and therefore the next would also return nothing. So, we have queries dependent on the results of the other queries here. So let's actually try this using our SQLite terminal to get a better feel for what we can do with this kind of um structure for our queries.

**1:55:17** · I'll go back to my computer and I'll hop into my SQLite environment. Let's say here I want to do a similar query but I want to find those books that were published by Maclo editions or Maclo press rather. So let me try to attempt this one by one going one step of the way and then finally combining my queries into one I could use more dynamically. So to our point earlier we have to first find the ID of Macose press. Let me try to find that.

**1:55:49** · I'll say select let's say ID from publisher where the publisher is equal to none other than Macose press like this. and my quotes semicolon hit enter and hopefully oh I will see see an error and based on this error let me ask our group here what did I do wrong

**1:56:19** · judging by the error I think you just mistyped the table name yeah so I probably mistyped the table name and we could probably parse this if I look at the error itself so it says parse error no such table publisher and that's true there is no table called publisher so let me fix this and run it again I'll say select let's say ID from the publishers table plural and we'll say um where the

**1:56:50** · publisher is equal to Macly hose press like this and I'll hit a semicolon here and now fingers crossed this should work I do see an ID of 12. Okay, so Macose press the ID is 12. Now I want to find the books that were published by this ID. So let me go to my book table. I will say select title from books in this case where the publisher ID is equal to 12 as we saw before semicolon.

**1:57:22** · Now I'll hit enter and I'll see these are the books that Maclost Press has published.

**1:57:31** · But again as we saw before I could improve this. I could make this better, more dynamic by nesting my queries having a subquery a query inside of a query. So let's redo this. I'll start at the end. Essentially, I'll say select title. Select title from my book table where the publisher ID is or is equal to what? Well, let's say I don't know it's 12. I have to write another query here.

**1:58:02** · So, to do that, I could open up some parenthesis. Is equal to a parenthesis. And then I'll hit enter to continue my query. I'll uh indent four spaces. space space space space just a style convention to keep things clean for me to show this query is inside of this other query. What I'll then do is finish out this query.

**1:58:23** · I want to select I want to select the ID from the publishers table where let me just indent again where the publisher is equal to uh not fit scroll auditions is equal to Mac leos press end quote and now let me close my parenthesis I have an open one here that I should close to show this subquery is done I'll hit enter close my parenthesis.

**1:58:54** · And now my entire query is done. I can hit semicolon, hit enter again, and now I'll see the very same results, but more dynamic. No longer do I have to hardcode the ID. I can make it more dynamic, and I can actually find it using my very own query here. Let's try a different context, too. Maybe I want to find all of the ratings for this book called In Memory of Memory. Well, maybe I'll try it step by step.

**1:59:22** · And what I'll first do is try to find the ID for in memory of memory. I'll say select ID from uh let's go from the books table and let's say where the title is in memory of memory memory of memory end quote semicolon. Hit enter and we'll see 33. So this book has the ID 33.

**1:59:53** · Okay. Let's now look in our ratings table for this ID. I'll say select let's go for select rating from my ratings table where the book ID is equal to 33 I believe it was. So now I'll hit enter.

**2:00:10** · And now I should see all of the ratings for this book. And there are quite a few that people have left on this book on the Goodreads website. So let me again try to improve this and make it just a little bit better. I'll be more dynamic about it and try to nest these queries. I'll say select rating from ratings.

**2:00:30** · We'll start at the beginning. We ultimately want ratings. Well, I want those ratings where the book ID is equal to some number, but I don't know what number yet. So I have to write my own nested query. I'll I'll create a parenthesis like this. Enter. I'll indent four spaces. Space space space.

**2:00:52** · And then I'll say I want to find the ID from the books table. From the books table um where this title is equal to in is equal to in memory of memory. And that is my sub query now. So, I'll close this out. I'll hit enter. Close my parenthesis. Now have a semicolon and hit enter. And I see those very same ratings. Well, I could probably not get back the individual ratings.

**2:01:22** · I want to kind of average them over time. So, let's try that, too. I'll say the same thing. Select rating from ratings. But now, no longer do I want to select all the ratings. I want to average them. So, I'll say select the average rating of this book from ratings. And now let me go back over to my nested query and I will hit enter again and I will hit the up arrow to get back access to my earlier parts of my um my SQLite environment. I'll hit enter here. Close it out. Semicolon. And now I should see the average rating for this book.

**2:01:58** · Okay. So this is very handy for us. We're able to kind of replicate those queries we would have done with a single table but now using sub queries. And so far we've seen this working for a relationship that is one to many. We could also use sub queries with many to many relationships. These tables that have many items over here and many items over there that relate in some way.

**2:02:22** · Let's try it let's say with authors and books. And I want to figure out let's say which author wrote flights. Which author wrote flights? So, let me ask what should I figure out along the way to get to the author who wrote flights?

**2:02:41** · Could you walk me through what I might need to know for that query?

**2:02:46** · Uh, you need to know ID of author and of that book and based based on that relation you have to join all three tables together.

**2:02:59** · Yeah, I have to know ids and I have to kind of walk across these three tables as you're saying. So, let's go back to our tables and I want to know who wrote flights. Well, a good place to start to your point is to say let's start at flights and find the ID. Well, the ID of this seems to be 78. Okay, let me then look in our authored table and let me try to find the author ID that corresponds with 78. Well, I find 78 here. What's next to it? Well, 58.

**2:03:27** · Okay, so the author ID who wrote flights is 58. Well, who is 58? I'll look in the author's table and I'll see this is none other than Olga. Okay, so let's walk through trying to make this query happen, but now using SQL keywords. I'll start first with trying to find the ID of flights. I'll select the ID from the books table where the title is equal to flights. Okay, that's fair enough.

**2:03:55** · Now, I could nest this query, put it inside another query to find the author ID of the person who wrote flights. I'll do a bit like this. I'll select author ID from authored where the book ID is equal to my prior query. Select ID from flights where title is equal to or from books where title is equal to flights.

**2:04:21** · And now I could go one step further. I could say I want to find the name of the person who has this author ID. Let me nest again. Let me put this query select name from authors where ID equals and put all the rest of it inside of the uh nested query here. So to be clear, I'll start from the middle, find the ID of flights, then I'll find the author ID for that book ID, and then I'll find the name of the author who wrote that book.

**2:04:52** · Okay, so a good number of steps here, but let's try it out ourselves in our SQLite terminal. I'll come back to my computer and here maybe I want to find all of those books or maybe not all those books. I want to find the author of a particular book you might be familiar with called the birthday party from our librarian conversation a little earlier. Let me say I want to first find the ID of the birthday party. I'll say select ID from books where title is equal to the birthday party semicolon enter. Now the ID is 8.

**2:05:26** · Okay, let me keep that in mind and actually I don't quite need to know this. Let me try to nest this query inside some other query to keep going towards my goal of finding the author of the birthday party. So the next thing to figure out as we saw before is finding the author ID. I'll say select let's say the author ID from the authored table.

**2:05:52** · That table of authors who have written books and I'll say where the book ID where the book ID is none other than the one I got back from this prior query. Let me indent and say select ID from books where title is equal to the birthday party quote not a semicolon yet my parenthesis semicolon hit enter and now I see 44.

**2:06:22** · So we're getting there but now I have to figure out who has the ID of 44 in my author's table. Let's keep going. Let's clear our terminal using control L. And I will then say select the name from the author's table. We're going to start at the be or going to yeah start at the beginning the place we want to actually get to. Then I'll say where the ID or the ID of that author is equal to the result of this query. What is the author ID associated with the book I want to find?

**2:06:53** · So I'll select author ID from authored from authored and I'll say where the book ID is equal to another subquery here I'll indent four times and four again. Now I'm nesting twice. Right? So I'll then say select ID from books and I'll hit enter just to kind of keep me on um some good style here.

**2:07:18** · I'll indent eight times total or and then I'll say um where where let me make sure I'm doing the right thing. Where the title is the birthday party.

**2:07:32** · Okay, that was a lot. Now we'll close out our queries. I'll hit enter space again semicolon or uh parenthesis enter again parenthesis semicolon. And hopefully after all this typing we'll get back what we want. we see our friend Lauren Movenier. So this is an example of trying to find the author who wrote a particular book although it's a bit long-winded using these kinds of subqueries.

**2:07:57** · So let me pose questions then we've seen how to use these subqueries for one to many relationships and also many to many. What questions do you have about how to use these queries?

**2:08:12** · I remember you talking about books with the same name and fact they can have different versions and etc. How would you get the ID for the different versions if they are titled the same as I'm guessing you wouldn't I I'm guessing you would set the for you wouldn't set the foreign key to a title instead of be primary or is it done differently?

**2:08:32** · A good question here. So you could imagine a database that has um more than one edition of a book inside of it. like maybe I have two editions of the birthday party or the hard coverver and the paperback and all these other editions, right? Well, in that case, what I might do is try to actually this is a good segue. I might have multiple IDs that I'm searching for. Like let's say I don't care if it's the um hard cover or paperback version. Well, I could look for the ID of like 55 and 56 and try to find um the author of both of those. So, let's actually keep going here.

**2:09:04** · Let me show you a new keyword to use for those kinds of questions if you don't mind. Um, let me come back to my computer and let's introduce this new keyword that can help us find the author of not just one book but perhaps multiple books or different versions of the same book. Let me introduce this one. This one is called in. Very simple, just i. And I can use in to say well maybe some key or some column is in some set of values not just equal to one but in some set of values.

**2:09:36** · So let's see an example here. We're back at our authors books and authored tables. And maybe I want to find the books written by these two authors gauze and Olga. Well I could select their IDs. I could say get back 27 and 58. Now I have two ids. So I could look in authored and I could say give me back all of the book IDs that have an author ID of 27 and 58.

**2:10:04** · Okay, I'll look here and I'll get back both four and 78. So notice how earlier I was asking show me the book IDs where author ID is equal to some single value. Here I'm asking find me the book ids where book ID has where the author ID is in some set of values more than one. Now and similarly let me look at my books table. Let me say okay I want to find the titles for these books.

**2:10:35** · Well I'll find the titles that have that have book ids in this set of ids four and 78. So let's see this in action in our SQL terminal. I'll come back over here and I'll write this query to find all of the books by a particular author named Fernanda Melor. So I'll go back to my terminal and Fernanda is more prolific than most. She's written actually two books that are on the long list for the Booker Prize.

**2:11:06** · So I'll say select ID from authors where the name is equal to Fernanda Fernanda Melor semicolon and this now is Fernanda's ID 24. Okay, let me find the ids of books that Fernanda has written. I will now say select uh book ID. Select book ID.

**2:11:31** · If I can type like book ID from the authored table where the author ID is equal to the result of this query 1 2 3 four spaces here and I'll say select ID from authors where the name is equal to Fernanda Melor parenthesis semicolon and I'll hit enter and I'll get back not one book ID but two.

**2:12:00** · So if I want to find these titles, I should say find me the titles where the book ID is not equal to but is in this set of ids. So let's try that. Let me say select title from books where the ID is in some set of values is in those two ids we saw earlier.

**2:12:23** · So I'll say in enter 1 2 3 four spaces and then I'll say select the book ID from authored where let me actually um space this again where the author ID is equal to the result of this subquery.

**2:12:42** · We can use equals here because there's only one author ID we care about. I'll hit enter. Then I'll do space space space four spaces for one indentation and now four more spaces 1 2 3 four to indent again to my next nested query.

**2:12:59** · I'll then say select let's say the ID from authors from authors where the name is equal to Fernanda Melor. And now let me close out my queries. I'll hit enter space space again. And now I'll use parenthesis to close out my middle subquery. I'll do the same. I'll hit enter and then I'll do another parenthesis and then semicolon here. Hit enter. And now I should see finally Fernandanda's two books.

**2:13:31** · Okay. So this is one example of using in.

**2:13:37** · What questions do you have on how to use this syntax? Actually my question was not regarding n but actually the indentation you use regarding the subqueries because while you were using the subqueries you mentioned that you are giving four spaces. Is there any necessity of using like such kind of indentation while we are using subqueries?

**2:13:59** · Yeah

**2:13:59** · great question about style here and let me try to pull up some slides that have um an example of that style so we can talk about it. Let me try to find an example of our nested query. I'll pull this one up. And as you might remember, we had three queries here. And I tried to keep track of them by indenting them more and more and more. This isn't required. You could um I mean, don't do this, but you could put it all on one line, which would just be crazy long to read.

**2:14:29** · What we do instead is we'll often try to hit enter when it feels nice to have a break in the reading um length and we'll then indent some spaces to show that this query is a subquery of the prior one. The exact amount to indent might vary but the idea of trying to break up your lines and trying to indent is going to be a good one for your own sake and for those who read your code.

**2:14:55** · Let's take one more too. when do we need to use in in wear clause when we are doing you know subquerying I suppose that we can also use subquerying without in as well you're right so we saw an example using equals and we also saw an example using in general if you want just a you know rule of thumb to follow if you're looking to see if some ID is part of a

**2:15:21** · list of IDs or part of a set of ids that is more than one you should use in in is good for checking if something is inside of more than one um item. Let's say equals though is good if you know you have only one ID. Let's say I have an ID equal to 23 or equal to 25. That's a good place for equals. If though I had 23 or 25, I might use in to match either or of those in that set. But good question. Let's take one more here too.

**2:15:52** · We have seen many to one to many relationships. one to one relationships and many to many relationships. So how would many to one relationships be tackled? Suppose one book has three authors. Then how would that be represented in the tables?

**2:16:08** · Yeah, let's look at the example of one book having three authors for instance and let's look at our authored table. So let me pull up that slide for you and we'll talk about it in just a minute.

**2:16:18** · I'll come back over here and I will pull up our example of having authors and books and the authored table in the middle. And to your question of how could I have let's say a book written by three authors. Well, we could imagine that this table um let's say um let's talk about Boulder for instance. So Boulder has the ID of one. Let's say three people wrote Boulder. Well, in this case we could adjust this. I could say this is no longer 74. This is one.

**2:16:47** · And same thing here. This is not four.

**2:16:49** · This is one. We have the book ID one in here more than once. It's in here 1 2 3 times. But what we're saying each time is that well 23 was an author of one. 31 was an author of one as well. And so was 27. So I would not be afraid to have multiple um instances of your foreign key inside of this table. What I wouldn't do is have it more than once in your primary key here. Here it actually has some information who authored which book.

**2:17:21** · Here it is strictly a unique ID that should be only a one to one relationship. Every key has to be unique for the items in that table.

**2:17:31** · Good questions.

**2:17:34** · Okay, so we've seen sub queries, but there is one more technique we could use to solve some of these problems of quering across tables. And this one is going to be called a join. So let's dive into joins. And the whole idea behind joins is trying to take a table and combine it with some other table. And actually for this we have uh some I don't know maybe guests for our class.

**2:18:00** · We have these very cute sea lions. And we'll use a database of sea lions to understand how joins actually work. So, if you're not familiar, sea lions are sometimes native to the coast of California, and they like to travel.

**2:18:12** · They like to travel really far. They go from the southern part of California all the way up to Washington State. This is many, many miles of traveling for these adorable sea lions. So, there are data sets that involve sea lions and their migration patterns. Here's one, for example. Here we have a table of sea lions. And here we have a table of their migrations. A distance column tells us how far they went in miles. And a days column tells us how long it took them to travel, of course, in days.

**2:18:44** · Well, here, if we're researchers, maybe we're keeping track of some number of sea lions. We're keeping track of Ya and Spot and Tiger, Mabel, Rick, and Jolie, but we have data on many sea lions, perhaps some we aren't even tracking anymore. This would be our migrations table. Now, it could come to pass that I want to figure out, well, how far did Spot travel and how far did Tiger travel? And what I could do is I could use nested queries for this.

**2:19:13** · But perhaps better yet, I could try to join these tables to see the data all in one table.

**2:19:21** · Now, to do that, how could I try to take a row from this side and kind of attach it to or extend the row here? What idea could I use to put the right rows together in this case?

**2:19:40** · Could you use the uh primary key, the ID to kind of join them together using the primary key and the foreign key?

**2:19:46** · Yeah, a good idea. So, you might notice that we actually have two columns here, both called ID, which is handy for us.

**2:19:54** · And notice how we have them kind of sort of matching. and matching in the sense that some of these IDs are actually inside of this column too. So we could use the primary key in really both tables here and try to match it together to figure out how these rows could be extended to add more columns. We could join these tables together to make this table ultimately showing us where ya has um traveled and how long it took them to get there.

**2:20:23** · So the keyword for doing these kinds of manipulations with data in SQL is called join. Kind of straightforward. But let's take a peek at what join can do for us inside of this database. So I'll go to my computer here and I'll pull up this database of C lines that I prepared for us today. I will clear my terminal. I'll typ and I'll get out of my long list database. To do that I can typequit a SQLite command to leave this environment. I'll hit enter.

**2:20:55** · And then what I can do is I can type SQLite 3 space C\_lions. DB. That is just the name of this database. Okay. I'll hit enter. Now to make sure I'm in the right place, I could type to see what tables are inside of this environment. Tables. Enter. I see both tables, migrations and sea lions, which is promising for me here.

**2:21:24** · So, we could see what data is inside of these tables. I could say select star from C Lions, uh, semicolon, hit enter. Now, I see all of these adorable sea lions inside of this lovely table. What if I wanted to find migrations? Well, I could do that, too. I could say select star from migrations semicolon enter. Now I see my data on migrations. And notice how again some sea lions are in the sea lions table.

**2:21:55** · And we have some ids in our migrations table that actually aren't in our sea lions table. So we're keeping track of only a subset of sea lions. And this might have some uh seions we keep track of in the past. So not all of them as well. Okay. So let's try joining these tables to determine where have our sea lions been in our sea lions table.

**2:22:16** · I'll say select uh star from sea lions. But now I don't want to end this query here. I want to expand this table with the data inside of the migrations table. So what could I do? I'll hit enter just as as a style thing here to now consider how I can make a query a bit longer. I'll want to join the migrations table to the sea lions table. And to do that, I can type join. I'll say join then space. And I want to say the table I want to join.

**2:22:48** · In this case, the table is called migrations. I'll say migrations. And I have to tell it one more thing. I have to tell it what we saw visually earlier, which is that the ID column in sea lions matches the ID column in migrations. I have to tell SQL which two columns to try to join these tables by. So let me do that. I'll say join migrations on which is a SQL keyword what two columns should correspond.

**2:23:19** · I'll now say migrations. ID. This means the ID column inside of migrations table is equal to or is going to be joined with this sea lions table and the ID column within that. Again, these two columns should have some matching values that we could use to make these rows longer with more columns. Let me then hit semicolon here and hopefully we'll see all of our data now combined.

**2:23:51** · I can tell you how far Tiger went and how many days it took them to do it because I've joined these two tables together. So in doing this kind of join, just regular old join, what we're really doing is part of this family of joins are called an inner join. You may have seen this idea of an inner join or an outer join. The usual join, at least in SQLite, is going to be an inner join.

**2:24:20** · And what do we mean by inner join? Well, let's visualize it a little more slowly here and see the process of which we might use to understand this join. I'll have again my two tables, but now simplified. I have name and ID and just distance and ID. And to join these, I could literally kind of nudge them together and draw a line down the middle a bit like this. But what do you notice?

**2:24:48** · I mean, this one seems to match this ID.

**2:24:51** · And this ID seems to match this ID. But these two, well, they don't match. I mean, poor Jolie down here. We don't know how far Jolie went. And if we don't know this data, if these IDs don't match, if we can't find a match for this ID or for this ID, well, let's sadly just get rid of the row. Like, it's not part of our join table anymore. It's gone from our memory. We now have only these tables or these rows that we could actually join together with the row and the other table here.

**2:25:25** · So this is our example then of an inner join. Let me ask what questions do you have on these joins so far?

**2:25:35** · So the confusion for me right now is where were the IDs generated? Was it on the C lion table or on the migration table? And what kind of problem can that pose like maybe in real world? So that's the question I have maybe not directly to joint itself.

**2:25:48** · No, that's a great question and good to clarify. So um we have sea lions with some ID and we see here that you know one ID is 10484 another ID is 11728 and to your good question which is how do we get these IDs? Well, these actually came to us from researchers perhaps who are researching sea lions. And if you're not familiar, let me go back to our slide with sea lion migrations on it.

**2:26:13** · Researchers might often want to keep track of where sea lions have been. And to do so, they will aum non-invasively apply some tag to this animal that has some unique ID on it. And they'll track where that tag goes to understand where this particular sea lion went. So they will make up their very own primary keys, their very own unique IDs to identify these sea lions. We can then use those same IDs in our table to understand where these sea lions are going.

**2:26:43** · And just to be clear, too, let me find our full data set here. Here we have those sea lions that we're now interested in. Those were now tracking.

**2:26:53** · But you could imagine that we also have some sea lions that, you know, we no longer track. and you know maybe they've you know gone on they're doing something else now they're not part of our data set so that's why we might see some over here but not over here I hope that helps answer your question about the sources of this data so let's take one more when

**2:27:14** · we join together the two migration and seell the ID table is repeating so I just want uh days and the travel distance I don't want to repeat the table of ID is that possible Yeah. And I think if I'm understanding correctly, we want to try to um not just join these tables, but maybe remove the duplicate ID in them. Like if I showed you this joined table right here, ID appears in here twice. There is a way to do this, and we'll see it towards the end of our exploration of joins.

**2:27:45** · We'll come back to that in just a minute. Okay. So, we've seen inner joins so far.

**2:27:53** · are this way of combining tables and only keeping the data that actually matches between them. Well, let's try a new uh way of joining. This one that might not be so strict. We have a few options here. We have what we're going to call a left join, a right join, and a full join. And you could imagine based on the names here, what each one might do.

**2:28:18** · You could think of our tables, one being on the left, one being on the right, and trying to join them, prioritizing either the left table or the right table, or maybe even both per a full join. So, let's get a feel for what kinds of tables we get back from these different commands, and we'll talk about we'll visualize how this is actually happening underneath the hood.

**2:28:42** · Let's go back to our computer here and let's try to do a left join using our two data sets. Now, a left join will prioritize, so to speak, the data on my left table. Left being quote unquote because there is no left or right in a database, but left here means the first table that I start with. So, let's try this. I'll say select um star. Select star. And let me just make sure I'm typing the right things here. Let me try select star from the sea lions table.

**2:29:17** · And now I don't want to just do a regular old join. I want to do a left join. I want to no matter what always have the data on my left table. This sea lions table here. Left join. And I'll join migrations. I have to say the same thing. Which column in migrations corresponds to which column in se lines?

**2:29:40** · I'll say left join migrations on migrations id equals sea lions id as well. Now I think that's just about it for my join. So I'll say semicolon enter. And notice the difference here. Let me walk to this board so we can see it in its entirety. I have all of my sea lions now in this table. where we left off Jolie earlier.

**2:30:06** · We've now kept Jolie in even though Jolie doesn't have a distance or number of days. We actually haven't tracked that data yet for Jolie, but we still see them in this table. Let's now try a right join to see the difference between this and the right join. I'll come back over here and let's try prioritizing our rightmost table.

**2:30:30** · This one perhaps being the migrations table. So I'll say select star from sea lions. This will again be our left quote unquote table just because it comes first. Now I'll say join uh not just join I'll say write join migrations on again migrations ID equals let's say sea lions.

**2:30:55** · I semicolon. Now let's see the difference here. Well, what have we done? We've actually left off a few sea lions. Now, we only have those whose ids were in the right table. Again, the right table being that second one we used. And even if we don't have any names for these sea lions, we'll still include them in our data set. We can see though that this data is missing and that as we'll see, it has some special value called null. So, we have a left join and a right join.

**2:31:27** · A full join though allows us to see the entirety of both tables and which values are missing. Let's try that now. I'll come back over here and I'll do a full join.

**2:31:40** · I'll say select star from sea lions full join migrations on full join migrations on migrations migrations. ID is equal to sea lions do ID semicolon enter. And now what do we see? Well, we see both tables in their entirety. We have Jolie in here still even though Jolie doesn't have a distance or some number of days.

**2:32:11** · We also have our sea lions, our mystery sea lions down below who don't have any name but are still included in our migration table too. So left join, full join and right join. So let's then visualize this to understand what's happening along the way. I'll go back to some slides here.

**2:32:31** · Let's look first at these um left joins as well. So really all of these left join, right join and full join. These are all part of this family called an outer join. An outer join lets you keep some data even if the join is not going to quite work out for you as much as you would want it to in an inner join. By that I mean you might have some null or empty values in this join after you run it. So let's visualize it. Here I have a left outer join and I want to combine this left table with this right table.

**2:33:07** · I'll do a left outer join. I'll put them together. And notice how these two don't match. Well, because they don't match, I'll fill in these values with the value that signifies empty or null. In this case, it is literally null. There's nothing here. So, because I did a left join, what I should do is prioritize this left table's data. Even if this doesn't have any match here, I'll still keep this row. But notice down below that this ID has no match in the left table.

**2:33:39** · I'll omit that and in the end I'll delete this bottom row but be left with Jolie who might or may not have data in the right table. Let's try the right join. Right outer join. I'll do the same thing. Combine them and they'll do the same exact kind of orientation. I have some null values here that I don't quite know how to match up. What I can do instead is say, well, I want to prioritize the data on this rightmost table, even though this ID has no match.

**2:34:10** · I want to keep it because it's inside this right table. Okay, let me delete this row because it has no match in my right table. And I'll be back to this type of join, keeping every ID in the right table. A full join, a bit more simple. I'll take the same data, join it together, and I'll simply say I don't care if there are null values involved. I'll leave them be.

**2:34:35** · Okay, so this is a lot of visualizing.

**2:34:38** · Let me ask what questions do we have on these joins?

**2:34:44** · Could I somehow work with multiple tables? Uh is there, you know, if I have like three tables, which one is the left one, which one is the right one, and what's the third one?

**2:34:54** · Yeah.

**2:34:54** · A good question. So, we've seen two tables so far and this was deliberate kind of pedagogically. It' be a lot to see three joins all at once.

**2:35:02** · Um, if you're thinking about joining three tables though and you're asking which one is your left table, which one is your right table, always it will be that the table that comes first before your join command, your keyword will be the left table and the table that's involved in your join keyword like join migrations, let's say, that will be your right table. And so you can imagine three tables um where for like the first two, the first one's on the left, the first one's on the right. For the next two though, the middle one's on the left and the next one's on the right.

**2:35:31** · If that helps you visualize without having much on the board here. Good question. Let's take one more. When we perform the join function, do we get under the hood, do we have like a separate table that's created which we can reference later down in the code or like do we need to write that entire join command again? Yeah, good question.

**2:35:52** · And so I believe you're asking, do we get back a separate table that we could use? Um, for this I might want to doublech check myself, but just to kind of show you what we've been doing so far, go back to my um SQLite terminal here and I will ask like select star from um let's say sea lions and let's uh do a full join with migrations on migrations. ID is equal to um sea lions id.

**2:36:23** · And I think what you're asking is do we get back like a separate kind of table here. Um we could consider it as a kind of separate table like if I hit enter here is this is kind of something we're going to call a temporary table which you could also call a result set. We can use this table for the duration of our query. What we haven't done though is made this table accessible in our database itself. like this is only there for the duration of this query.

**2:36:50** · So hopefully that helps answer it with a bit of um factchecking if you need to as well.

**2:36:58** · Okay, let's show one final type of join here. This one called a natural join. A natural join kind of allows me to omit the part of the my previous joins where I was saying migrations ID equals sea lions id like natural join says both these columns are called ID. I could just assume that I want you to join by these two columns. So, let's try a natural join and see what we get back.

**2:37:24** · I'll come back over here and we'll try a natural join with our sea lions table and our migrations table. I'll say select let's say star from sea lions. Then I'll natural join migrations here. And I no longer need to say migrations ID equals sea lions do ID. I can just hit semicolon. And now I can hit enter.

**2:37:50** · So we'll see that the join worked just as we wanted it to. And we didn't even specify which ID column corresponded to which other ID column because these were named the same column name ID. Notice too, we don't get a duplicate ID column.

**2:38:08** · In some prior joins, we had an ID column here and an ID column here. Now, we've just combined them into one single column or really only kept one column among this join here. So, many kinds of joins to use, many ways to query our tables. What we've seen so far is how to organize our data, build connections between them, and now how to query this data using both subqueries and joins.

**2:38:37** · We'll take a quick break here and come back to see how we can use sets and groups to again kind of refine our queries and ask more interesting questions too. Well, we're back and now we're going to focus on this idea of sets in SQL. So, when you run a query, you get back some results and those results are often called a result set.

**2:38:59** · Some set of values that you've gotten back from your table. So let's take a look at what sets are and how we could use them to refine our queries and to find relationships among different groups of people, places or even things.

**2:39:13** · So let me ask a question of you. Maybe in this world we have authors and we have translators at least in the publishing industry, right? If you're in this set, you are an author. If you are in this set, then you're a translator.

**2:39:30** · But what would it be then if you were in this set? What does this set mean?

**2:39:39** · It means that uh you are both the author and the other one. So translator.

**2:39:44** · Yeah, you're right. So this means you are both an author and a translator. You're in the middle of these two overlapping circles. In SQL, we could represent this kind of relationship using our intersect operator, which we'll see in just a moment. We'll take authors perhaps and intersect them with those who are translators and find those who are both authors and translators.

**2:40:08** · Let's do another one then. Let's think of this set. Who are you? Or at least what does the set represent as a whole?

**2:40:18** · It means that you're either an author or a translator.

**2:40:21** · Nice. You're either an author or a translator. You could be both, too, but you're in either camp. You're either an author or a translator. And for this, we could use a SQL keyword called union.

**2:40:34** · I'll take my set of authors and combine them with my set of translators and get back, in this case, the entirety of these two sets. Let's look at this one, too. If you are in this set, who's included there?

**2:40:53** · Only authors will be included. Authors which are also translators will not be included here.

**2:40:59** · Yeah, good. So here only authors are included. We see that those who are also translators aren't included. In fact, if you are an author and only an author, then you are in this set. And to get this kind of result, we would use our SQL keyword called accept. I'll take my set of authors but subtract or remove or accept my set of translators. Similarly, I could say take my set of translators and accept the set of authors. Subtract them, remove them.

**2:41:30** · And I could do that with translators except authors. We'll see these keywords in just a moment.

**2:41:38** · Now, I have one final question here, which is how could you represent this one? I mean, who are you if you are in either this set or this set? And how would you get that kind of set? I'll actually save that one for you to do as homework, if I may, before we move on to seeing these in our actual terminal environment. So, let's take this idea of sets and apply it to authors and translators this time in our database.

**2:42:06** · I'll come back over to our SQLite terminal and let me now leave our database of C lines. Sadly, I'll typequit and go back to my regular old terminal. Now, I want to open back up our longlist db database. Long list db.

**2:42:23** · Hit enter. And now I'm back in the place where I have authors and books and publishers inside of this database. I'll type L to clear my terminal. And let's first try to find all of those who are either translators or authors. Well, what could I do? I could try this. Let me try select select name from translators like this or my translators table. Semicolon enter. These are all of my translators.

**2:42:54** · Now I want to find authors. I could then say select name from select name from authors semicolon. Hit enter. Now I have all of my authors. If I wanted though to combine these results, these result sets, I could do so using union. So let's try it. I'll say select name.

**2:43:19** · Select name from translators and not finish my query yet. I'll hit enter just for style sake. And I'll say union union with some other result I'll get back from some separate query. I'll hit enter. Now I'll say select let's say name from let's go for authors now end quote semicolon hit enter and now I'll see both authors and translators and we should see here that every author and every translator is in here only once.

**2:43:55** · We can assume that we have unique names for these authors and translators. And I could scroll through and figure out who is either an author or a translator. Actually see them both in the same set. If I wanted, I could distinguish between authors and translators by adjusting my query just a little bit. I could say select um let's go for select uh author the string as profession and also select name from the author's table semicolon.

**2:44:29** · This will give me back not just one column of names but also a another column called profession that has just author inside of it. I'll hit enter and I'll see I indeed have this column if I scroll all the way up called profession and I have the value being author. Okay, let's combine these. Let's union this set with the set of translators and give them their profession too.

**2:44:52** · I'll say select author as profession and then also name from the author's table and now I'll hit enter and I'll say union that set with the set of translators. I'll say select translator the string as the column profession. Then I'll say name from the translators name from the translators table quote unquote semicolon. Hit enter.

**2:45:25** · And now I could actually see who is a translator and who is an author. If I scroll through here I'll see translators and now I'll also see author. So I've combined these two sets into one that works for me here. Okay.

**2:45:41** · So this is how to union or combine our sets. But what if we wanted to find only those who are authors and translators?

**2:45:49** · Kind of a unique niche group of folks. But who is part of this set? Well, let's try to find out. I could select names from the author's table as I did before. Now, instead of union, let me intersect these names with those that will be in the translators column. I'll say intersect. intersect and select name from translators.

**2:46:16** · And now I'll hit semicolon enter. I'll see one his name is Goi who is both an author and a translator. They translated their own book into English for the international booker prize. Okay. So let's try now to find those who aren't just translators and authors but only those who are perhaps translators or only those who are um authors. So let's try this. I'll say select name from authors. Hit enter.

**2:46:46** · And now I want to exclude those who are also translators. I'll say except in this case select name from select name from translators. Hit semicolon. And now I should see if I pay close enough attention that Goi is not in this list. They are an author and they were in the author set of names, but because they're also a translator, they're not inside this set of list.

**2:47:19** · So this is fine and good for finding who's in one list, who's in some other list, and who's in between them. But it's also nice for trying to find books people have collaborated on, let's say.

**2:47:30** · Maybe I want to find the books that both Sophie Hughes and Margaret Costa have written together jointly. So I could try to find first the books that Sophie Hughes has translated. Let's say select um select book ID from the translated table. This table that has translated has translators and books inside of it. And then I'll say where the translator where the translator ID is equal to this subquery.

**2:48:03** · I'll find Sophie Hughes's ID as a translator. I'll say select ID from translators from translators where the name is Sophie Hughes. Okay. Semicolon to end. And these are the book IDs that Sophie Hughes has translated because Sophie Hughes is a translator. Well, let's see. Maybe they have translated some books with Margaret Costa as well. I could try to find out.

**2:48:33** · I'll say select say select book ID. We'll try to find um Sophie's books again. I'll say select book ID uh from trans from translated where the translator ID is equal to again Sophie Hughes's translator ID select ID from translators where let's say the name is Sophie Hughes like this now I'll close out this

**2:49:05** · part of my query but I want to find the intersection the set of book ID keys that are the same between Sophie Hughes's translated works and Margaret Costa's translated works too. So I'll continue. I'll say intersect intersect this result with some other query. All right. Now let me select the book ids from the translated table where the translator the translator ID is equal to a different kind of query. This one will get back the ID for Margaret Costa.

**2:49:36** · I'll say select ID from translators and where the name is equal to and I believe in this particular case they go by Margaret Ule Costa like this. Now I'll hit enter close out this subquery and finally I can hit semicolon. This is the end of my query. Semicolon here and now I'll see the book ID they have collaborated on.

**2:50:05** · You could imagine going beyond this to find the title of this book ID using another nested query, but I won't spend time on that at least for now because I have to write all this text back out for you. So, we've seen union, we've seen except, we've seen intersect. What questions do you have on these sets and how they work?

**2:50:29** · You've got three joints. I just wondered if there was a default that you chose if you didn't know what the situation was like which one to use.

**2:50:35** · Yeah.

**2:50:35** · So we saw different kinds of joins. Um we saw uh we saw left join, right join, full join, right? And the default as we saw a little before is just a simple join. And that join is an example of an inner join. It'll only take those rows where the ids actually match up. You could get more specific and have a left or right join or a full join, but we'll leave that um for you to try out on your own and see the results of as we did before too. But great question.

**2:51:02** · You mentioned that the ids from both tables were used automatically to merge the two tables and we didn't have to bother with the duplicate um duplicate column for an ID. So I was wondering in a situation whereby the primary key are actually like foreign keys. Let's say you're trying to join with another table where your ID is actually like a foreign key. How would you go about doing that?

**2:51:24** · Because it seems we didn't specify the ids where wanted to like make the joins on with a natural join. So I just wanted to needed some clarification on that front.

**2:51:33** · Yeah.

**2:51:33** · And let me make sure I'm understanding correctly. So I think you're trying to think about how you would um join a table that has a different kind of column name from the other one. Um, and for that you could use the equals there and you could say um, we said migrations id equals sea lionsid. But let's say the sea lions ID was actually called um, sea lions ID like the full thing spelled out. I could say join um, migrations on migrations equals sea lions. Lions ID to spell out the column name for SQL.

**2:52:04** · Good question too. Can I use intersect and the union together between more than two tables, three tables or four tables? Yeah, could you use intersect more than once? Let's say to intersect more than one set. You absolutely could. And here I don't have a good example planned for this, but you could have one query that does one thing. Gives you some set and you type intersect after it. Then you get back the next query and you find the intersection of that. You could then type intersect again to get the intersection of all of these three sets.

**2:52:37** · you keep going going as you'd like to. The key thing here though is that in your intersects or in your unions or in your excepts, you always have to have the same number and the same type of columns. So if I was trying to combine, let's say, author names with um book titles, I can't intersect or union those quite well because they have different kind of meanings, right? They're different kinds of things.

**2:53:02** · So if you're trying to join multiple thing, trying to join multiple tables or interact multiple tables, make sure you always have those same column names and those same column types, the type of data that's stored inside.

**2:53:17** · Okay, so we've seen sets now and we're going to conclude by looking at this idea of groups. Well, groups will allow us to recreate some of what we tried to do a little bit of last week, trying to um understand the average rating of some books. Let's take a look at groups now.

**2:53:36** · Well, you could imagine that I have my ratings table. And in this ratings table, I have book IDs and I also have ratings. Here, I see that the book ID of one has several ratings for people who gave the book a rating. It has four, three and four. And similarly, book ID with two has two ratings from folks two and three. Now I want to find the average rating across these ratings for each book ID. So let me try that in my terminal.

**2:54:08** · Come back over here and let me first try to find the average rating for each of these books. So I'll go back and I'll say why don't I select the average average rating. It's like the average rating from my ratings table. And I think this should be good enough. So I'll hit semicolon. And I'll see well 3.83644.

**2:54:32** · And this seems to be an average, but I wanted the average of each book. So what did I do wrong here? What am I actually seeing in this case?

**2:54:46** · Is that an average of all books in the entire table?

**2:54:51** · Yeah, good instinct. So, let me try to put back our table here. We can see what's actually going on. I'll come back over here and I will show us again this table. So, we had a table of ratings, right? And we had the rating column that has individual ratings inside of it.

**2:55:08** · When I say select the average rating from this table, well, what am I getting? I'm getting the average of all of these ratings, not grouped by book ID. So, if I want to find the average rating for each book, I need to employ this idea of groups. And I mean, wouldn't it be nice if I could do something like this? I could kind of highlight the rows that are part of each group and then try to average those. I could say, take all the books with ID 1 and all the books with ID2 and just collapse their ratings like this.

**2:55:40** · And once you do that, find the average for me and give me that back as a table. That'd be kind of nice. And luckily, we actually have the capacity to do that with SQL using this group by keyword. So, we'll see this in action. I'll come back over here and let's try to redo this query to find the right answer.

**2:56:03** · I'll come back and I'll say let's select let's select in this case the book IDs and also their average rating. I'll select book ID that's one column I want and I also want the average rating from this column from this table. Now I'll say let me title this perhaps as average rating. So, I'll get the average rating and just title that column average rating. Exactly. I want to select this from the ratings table.

**2:56:38** · Okay. But now I don't want to simply hit enter. I'll get back the same thing I did before, which is the average of all the ratings in the ratings table. What I want is for these ratings, the average ratings to be grouped by the book ID. So I'll say group by book ID semicolon hit enter. And now I should be able to see the results I wanted.

**2:57:03** · Let me scroll to the top and notice how using group by I was able to take each book ID collapse the rows the ratings were associated with this book and find the average of that rating 3.77 3.97 3.04 4 for each book. So, kind of handy here. Let me try to improve this and show you one additional thing we could do as well.

**2:57:32** · I'll come back and why don't I try to replicate what we did last time, which was find the books that have a certain rating or higher. Let's try that. I'll say select let's say the um book ID and let's get now the rounded rating the rounded average rating. I'll round the average rating to two decimal places and I'll call this average rating as a column.

**2:58:02** · Okay, I'm going to select this from my books table from my ratings table, sorry. And now I want to group by the book ID to find the average rating for each book ID.

**2:58:20** · Now though, let's say I only want those books that are pretty well rated, greater than 4.0 out of five stars. To include a wear clause, I could try following up on this group by. And you might think I could say, well, where the average where um average rating that new column I created is greater than or equal to 4.0.

**2:58:43** · But I can't because these are now not individual rows, they are groups. SQL uses a different keyword for conditions on groups than for conditions on individual rows. And this keyword is called having. H A V I N G. Let me try that. H A V I N G. I want to group by the book ID and only keep those that have an average rating of greater than 4.0. I will scroll over here and I'll hit enter. And now I should see a much smaller list.

**2:59:14** · I see book ID 5 has a 4.06, 10 has a 4.04 and so on. And now the next step is you could imagine me perhaps joining these book IDs with another table that has titles inside of it too to find the average rating given some title as well. So groups allow us to take these columns collapse some rows and find aggregate statistics across each of those groups. Let me ask then what questions we have on groups.

**2:59:48** · What if I don't want to see the rate the average rating of a book, but how many ratings does it have?

**2:59:56** · Oh, good one. So, I want to know not the average rating, but the number of reviews. Let's say the number of ratings it was given in my table. Well, for that, I could just modify my query a little bit. I could change average to count because count counts up the number of rows that I have. So, let me try that here. I'll come back to my laptop and let me try this one.

**3:00:16** · I will select book ID and I will also select the count of book ID um in my no also select the count of ratings how many ratings there are inside my ratings table. Count of rating from let's say the um ratings table like this. Now I want to group this data group the counting by book ID. So I'll say group by book ID. Give me a count of the ratings for each book ID.

**3:00:49** · And now I could just hit semicolon and enter. And now I'll see how many ratings each book actually has. Let me go to the top here. And I'll see book ID 1 has 2779 ratings. Book ID 2 has 175 ratings and so on. A good question. Let's take one more too.

**3:01:12** · So considering this new having syntax, how could we couple that with the order by?

**3:01:18** · Yeah, where does it fit in with order by? Like let's say I want to sort this data to at the end of the day. Well, I could do that as well. Let me show you one example. I'll come back to my terminal and I could try this. Let me come back to uh finding average ratings.

**3:01:34** · So I'll say select book ID and the rounded average rating to two decimal places calling that column average rating. And I'll select this from the ratings table. Well, now we want not just to find the average rating, we also want to sort by that column too. And in fact use having to only find those books that have 4.0 know or higher. Well, let's try this. I'll say from ratings and I'll still group by book ID.

**3:02:11** · Now, I'll say I only want to filter to those groups that have a average rating of greater than 4.0. And finally, after I've filtered out all of these rows, I want to order them. I want to sort them. So, I'll order them by average rating.

**3:02:31** · this column I made up top and I'll say order them descending order. I want biggest to smallest and fingers crossed I'll hit enter and we'll see our ratings sorted for us. So great question here to reimplement much of what we did last time. And now indeed we've kind of come full circle here. We've taken these ideas and we've seen them in single tables as we did last week.

**3:02:58** · We this week took our tables and expanded them into multiple tables, different authors, different publishers, different ratings and so on. And we learned how to query those tables using subqueries and using joins. What we'll see next time is putting you in the driver's seat, having you actually create your own tables, define your own relationships, and build a database to your own liking. So, all that and more next time. We'll see you there.

### Designing

**3:03:28** · \[Music\] Well, hello one and all and welcome back to CS50's introduction to databases with SQL. My name is Carter Zeni and last we left off we learned about relating.

**3:03:53** · That is how to have multiple tables in our database for people, places, and things and how to have them relate to one another in the way we might do in the real world. Now today we'll take a step forward and we'll talk about how to put you in the driver's seat designing your very own database schemas to organize your data. Now we'll pick up where we last left off which was with this database of books. So we had this database that was full of books that have been long listed for the international booker prize.

**3:04:23** · To be long listed means to be nominated for some prize let's say. So we had the past five years of books in this database and we worked on improving this database over time from week zero to week one. Now this week we'll actually take a look underneath the hood and see what commands we had used to create these very databases. So let's reveal now what we had done all along. I'll go back to my terminal here.

**3:04:51** · And if you remember, I could use a command to open up a database file, which was this command here, SQLite 3, and then the name of the file I want to open. So, let's try this.

**3:05:04** · I'll go back to week zero to my week zero folder like this, and I'll open up my longlist database, week zero longlist. DB. Okay, I'll hit enter. Now I'm in my SQLite prompt. So I could work on typing some SQL commands, SQL statements or queries inside of this uh terminal prompt here. So if I want to get a feel for what's inside this database, we saw I could use a command called select. So I'll select now some rows from this table.

**3:05:34** · I'll say select let's say the title and also the author columns from my long list table semicolon and enter. Now I'll see all the titles and all the authors that were inside of this long list table. But I only want to peak here. I only want to see roughly what kind of data is inside.

**3:06:01** · So I could probably improve this command here. I could instead say select the author and title columns from long list from long list but limit now to the first five rows we saw before semicolon and I'll hit enter on this query and now I'll see only the top five rows. So I'm able now to see what kind of data is inside my database.

**3:06:31** · But what I can't yet see is what command was used to create this table and what kind of data could be stored inside of it. So let's reveal now what was going on underneath the hood all this time.

**3:06:44** · I'll say this new command a SQLite command not a SQL keyword but a SQLite command called schema schema. Now if I hit enter, I'll see the following. The command, the statement, the query that was used to create this long list table. And notice how I have many columns inside this table. I have an ISBN column, a title column, an author column, and so on.

**3:07:09** · And each column seems to have some kind of data that could be stored inside of it like text or integers or real for floatingoint values or decimals if you're familiar.

**3:07:24** · So this is how we created the very first version of longlist db. But let's also see how we created the second. So I'll type doquit to leave this version of longlist db. And now let me open up the next version we had created which is more relational. It had tables inside of it that could relate to one another. So let me type SQLite 3 then long list the SQLite 3 and go to week one and then type long list db. I'll hit enter. Now in my next version of long list db.

**3:07:56** · Well what could I do? I could type select and look at some of the uh tables in here to see what kind of data is inside. I could perhaps say select maybe the names from the author's table here from the author's table and hit semicolon. Now I'll see all the names of authors that are inside of the author's table. I could do the same thing for books. I could maybe look at the titles of books.

**3:08:26** · I could say select title from the books table semicolon and enter. Now I see all of the titles that are inside my books table. But what I haven't seen yet is the schema of this database. It is the way it is organized and the commands that were used to create these tables.

**3:08:48** · So let me work on that. Now I'll clear my terminal using ctr L. And now let me type dots schema again. I'll type dots schema to see what commands were used to create this database. Hit enter. And I can see I mean there are quite a lot of commands here. Now this feels overwhelming. I mean I'd be right there with you, right? This is a lot of commands to parse through and read. So there's probably a better way to do this. And one way to try is to type schema and then give it some table name.

**3:09:24** · Let's say I want to understand the schema for just the books table like just that for now. So I'll say dots schema and then the table name books in this case. Then I can hit enter. Now I'll see the schema, the organization, the command that we used to create the books table in this case. And notice again we have several columns ID, ISBN, title, publisher ID and so on. Each one has their own kind of data they could support or take into this column like integers, text and so on.

**3:09:56** · So again, what we'll do today is have you all learn how to write your very own create table commands to build your very own databases that represent what you want to represent in the real world. So, let me exit this prompt here and let me propose that we'll have a bit of a design challenge today to actually try to represent a real world entity with some database here.

**3:10:23** · And if you're not already familiar, uh Boston is perhaps famous for being among the first cities to have a subway system in the United States. So, here is a picture from the late 1800s of a subway being built in Boston's city streets. underneath the streets here. There would be trolley cars would go and transport people across Boston. Here's another picture of a trolley actually working underneath the streets. So, people would go down underneath. They would hop on a trolley.

**3:10:53** · They'll be able to go to different parts of Boston, perhaps from Harvard to MIT or downtown up to, let's say, Brainree or down to Brainree, which is more south of Boston, for example. One of the famous stops is the Park Street stop which is right down in the middle of Boston, one of the central hubs of this subway system. And now these photos are all from, let's say, the early 1900s, late 1800s, and so on. But the subway's gotten a lot more modern since then. And actually now we have several lines that span the entire city and beyond.

**3:11:24** · So here we have the red line of which Harvard and MIT are a part. We have the green line which brings you kind of west to east, the blue line, the uh orange line and so on. So many more lines and stations have been added to this system.

**3:11:43** · It's a big design challenge to represent all of these stations, all of these lines and all these people who might ride this subway too. So the question then becomes how can we create a schema for this data? And again by schema we mean what kinds of tables should we have? What kinds of columns might those tables have? And what kind of data should we put in each of those columns for instance? So let me propose this.

**3:12:14** · Let's say we start just first with names and stations. So Charlie here, our very first rider on this system is going to be at the Kendall and MIT station. So this is what this table represents now. But what more could we have? Well, we might also want to have maybe what Charlie is doing at that station. Maybe he's entering the station, for instance.

**3:12:37** · And if you're familiar with the subway system, you often have to pay to get onto a a train or get onto the station itself. So, let's say Charlie pays some fair to enter into the Kendall MIT station. Well, back in the mid 1900s, the fair was only about a dime. It was 10 cents. So, we'll say Charlie paid 10 cents to enter the Kendall MIT station.

**3:13:02** · And now, this seems pretty good, but if I am the transit authority, the person who runs the subway system, I probably want to know, does Charlie have enough money to get on the train? And if so, I want to make sure that, okay, well, Charlie actually could get on this train. So, let's say not only does Charlie pay a fair, he has some remaining balance afterwards. So Charlie here has gotten onto the Kendall MIT stop. He's paid the fair of 10 cents and has five cents left.

**3:13:33** · Okay. So here's a bit of a table. We probably add more information to it.

**3:13:39** · Let's say Charlie then leaves at the Jamaica plane stop. And the fair to leave is about a nickel, 5 cents. And now Charlie has no cents left over. So again, Charlie paid 10 cents to get on, had 5 cents left, paid 5 cents to get off, and now has no remaining balance here anymore. Okay, so that's Charlie's story. Let's look at Alice, though.

**3:14:04** · Let's say Alice gets on at the Harvard stop. They too pay 10 cents to get on at the Harvard stop, and they have a remaining balance of 20 cents. Alice will go, let's say, to Park Street, get off at Park Street, pay the nickel to leave, and now they'll have a balance of 15 cents at the end. Let's go to Bob.

**3:14:25** · Bob enters the alewife station. They pay 10 cents. They have a remaining balance of 30 cents. And let's say they leave at Park Street and have a fair of 10 cents to leave because it's a further distance. Now, they'll have a remaining balance of 20 cents overall.

**3:14:42** · So this table is okay, I might admit. I mean, last time we learned about having we called primary keys and foreign keys. So seems like that's missing here. Let's go ahead and add that here. I'll give each row a unique ID so I can know who entered, who exited, and so on. And give that a unique ID here. But I might even say that this table could really be improved substantially. And I want to ask you, what redundancies or inefficiencies do you see here?

**3:15:16** · We're trying to represent riders and stations. What could we improve about this design?

**3:15:25** · Hello. So, uh probably the redundancy will be the names and the stations too.

**3:15:30** · For example, the Charlie will uh go to the train daily. Then he will become most of the names in the data. Yeah, good point. If I'm hearing what you're saying, Lauren, let me show you some examples that I highlighted here. You know, one example could be to your point about these names. Like these names seem to be telling us the name of a person.

**3:15:53** · But here we have only three names, Charlie, Alice, and Bob. Well, my name is Carter. And what if somebody else named Carter also tried to get on and leave at some stop? Well, I wouldn't be able to know which Carter was which or which Charlie was which or which Alice was which and so on. So, we probably need a way to represent people and their names a little better here too.

**3:16:18** · What other ideas do we have for how to improve the design of this table?

**3:16:24** · Yes, I think we can have uh a singular ID for a singular person. That way, we'll be better able to track their activities.

**3:16:31** · Nice. So, we could probably have an ID for each person. A bit of what we learned about last week, right? Putting people in their own table and giving them their own unique ID, a primary key.

**3:16:43** · Let's show that here. I'll go to some slides and I'll pick out one that shows us just riders. So, to your point, Sukanya, we could try to have maybe a table for just riders. And maybe to simplify, this table has only two columns. It has a column for ID and a column for name. So here we have Charlie, Alice, and Bob all in their own table. Well, let me pros too. We could do the same thing for stations. Like let's say we have a table of stations now and we give each one their very own ID as well.

**3:17:15** · Our own primary key for this table. We have Harvard, Kendall, and Park Street. We can differentiate between them using their IDs here. So a few improvements could be made. And as we're making these improvements, splitting one table into many and debating what kind of data to store in each table, the process we're going through is one called normalizing. We're normalizing our data.

**3:17:40** · To normalize means to reduce redundancies effectively to take a table uh take one table for instance, split up into multiple and have each entity be part of its very own table. Some academics in the world have named different normal forms quote unquote. There's like first normal form, second normal form, third normal form.

**3:18:04** · This progression of making your data more and more efficient. You can use those as heruristics. At the end of the day, a few principles might apply.

**3:18:12** · First, take your entities like in this case stations and riders and put them each in their own table. And if you add more data, make sure that if I were to add a column, let's say to riders, it is only a data point about riders, not about stations, not about fairs, only about riders. And that process can help us make a data set that is more dynamic, more easy to reproduce and more easy to write queries on. So that is the process here of normalizing.

**3:18:46** · Okay. So if we have now riders and stations, we want to represent them in our table. Well, we could use what we learned about relating last week to ask how could we actually represent these riders and these stations. So let's say here I again have riders and stations. I want to make sure that I have the right relationship between them. Well, if you're familiar with subways, we might say that a rider goes to one station.

**3:19:14** · And this big T here is the symbol for a station here in Boston for the T's that we call it for the subway. So a rider might go to one station, but of course that might not be the full picture. A rider also gets off at some station later on. So a rider could be associated with not just one station, but multiple.

**3:19:35** · And if you're familiar, at least with any subway system, really the Boston one too, it can often get pretty busy. And so riders might not just go to of course one station or two stations could also have multiple riders that are on a particular station here. So to recap, one rider might be associated with more than one station. They might get on at this first one and get off at this later one. But each station could presumably have more than one rider.

**3:20:03** · Each station here could have rider A or rider B, the rider up here or the rider down below and even many more than that as well. So to put it in the language of our ER diagrams, our entity relation diagrams from last week, we could look at a bit like this where we have riders and stations. Riders visit stations and they're associated like this. A rider must have at least one station associated with them.

**3:20:35** · That's what this horizontal line means. If they aren't at a station, they aren't really a rider, right? A rider though could have many stations associated with them. That's what this three prongs down here means. They could have one, two, three, four.

**3:20:50** · They could have many stations they get on and get off of. Now, a station could have anywhere between zero riders, if it's maybe out of commission or isn't very popular, upwards to many. It could have two, three, four, five, even hundreds of riders associated with this particular station. So, here is our entity relation diagram for these particular riders and these stations here.

**3:21:17** · So let me ask what questions do we have on these relationship between riders and stations and how to design this table so far.

**3:21:28** · Sir I want to ask that you have used the safe ID for stations and riders. So uh that maybe uh give us problem in coding.

**3:21:37** · Yeah

**3:21:37** · a good observation. And so you might have noticed that in the riders table and in the stations table I gave the same kind of ID like I had 1 2 3 for each of them. And let me just show you that again here. I'll come back to some slides and I'll show you again the riders table where we had Charlie, Alice, and Bob ID 1 2 3. Same for the stations. We had stations Harvard, Kendall, Park Street, ID 1, 2, 3. And to your question, isn't that a problem?

**3:22:08** · Well, I would argue in this case it's not so long as we keep clear that these ids are for stations and these IDs are for riders. And we'll see how to do that using our SQL keywords later on. But again, so long as we have an ID just for our riders and an ID just for our stations, we can keep these separate even if they might have the same values.

**3:22:34** · But a great question here. Let's take just one more.

**3:22:38** · Uh regarding the entity relationship diagram, how is it possible for stations to have uh a possibility of zero writers, but writers must compulsorily have at least one station?

**3:22:49** · Yeah, good question. So, this might be up to you and how you formulate it, but for me, let me show the diagram again.

**3:22:56** · I'll go back to over here. Uh in my mind, to be a rider, you have to have visited a station. If you aren't visiting a station, you aren't really a rider right now. Presumably, there are stations that were built but aren't really being used right now or aren't really uh in service yet. That could be a station that has no visitors. So, you could argue let's make sure every station has at least one rider and every rider may or not have to visit a station.

**3:23:24** · For that, I would say let's kind of we could probably reasonably disagree there and talk about how we could represent the diagram here too. But a great observation and a good um other critique of this this system here. All right. So let's now turn to representing this in our database. I'll go back to my computer and we'll learn about this new SQL uh keyword SQL statement. This one called create table.

**3:23:54** · Create table allows us to as the name suggests create a brand new table. So, let's do just that in our new database to represent riders and stations. I'll go into my terminal and I want to make a brand new database. I'll call this one MBTA. DB because MBTA stands for the Massachusetts Bay Transportation Authority, the people who run the subway essentially. So, I'll do SQLite 3 MBTA.

**3:24:23** · DB hit enter and I'll type Y to say yes I want to create this brand new database.

**3:24:31** · Okay. Now if I type schema I see nothing but that's expected. I don't have any tables yet. I have nothing inside this database. It's up to me to create these tables myself. So what I'll do is clear my terminal and let's start first with riders. I might create a table for riders. So I'll say create table and now I have to give that table some name.

**3:24:56** · I might call it riders here and then in parenthesis like this I can specify what columns should be part of this table. So let's start first. I'll hit enter here and continue this query. Now I'll by convention just indent four spaces. One, two, three, four. And I'll give an ID to each of these riders as we saw before. I'll say ID here is one of my columns.

**3:25:26** · Now to create a new column, I'll follow this up with a comma and hit enter. I'll again by convention for style just indent four spaces. And what's my next column? Perhaps a name for these riders.

**3:25:40** · I'll give this column the name name and I'll leave it at that. Once I'm done adding columns, I no longer need to have a comma. I could simply close out this query, this statement. I could hit enter here, say close parenthesis to close the top parenthesis here, semicolon, hit enter, and now nothing seems to happen.

**3:26:05** · But that's actually a good sign. So let me type dots schema hit enter and I'll see the result of that statement before create table if it doesn't already exist riders and riders has inside of it two columns ID and name. Okay, let's keep going. Let's make one for stations too.

**3:26:25** · I'll clear my terminal and I'll say create me a table called stations and include actually not station uh if you ever want to uh let's say fix this kind of table here let me try closing semi closing the parentheses hit semicolon enter I'll get a syntax error I can restart I'll do L now I'll do create table stations plural open parenthesis enter I'll indent by four spaces 1 2 3 4

**3:26:56** · and now I'll similarly include an ID for each of these stations. I'll say ID, comma, and then what else should I have?

**3:27:04** · Well, stations tend to have a name like the Kendall MIT station, the Harvard station, the Park Street station. So, I'll say I'll give each of these their very own name, what else do stations have? Well, they might also have a line that they're on.

**3:27:22** · Let's say it's the red line or the blue line or the green line and so on. I'll have a space for them to write in their line that they're a part of. Okay. And maybe I'll leave it at that to keep it simple. I'll say stations have an ID, a name, and a line. Now I'll close this out. I'll say end parenthesis semicolon. Hit enter. And nothing seems to happen.

**3:27:43** · But if I type dos schema, I'll now see my riders and my stations tables inside of my database. Now one more step here. We have riders.

**3:27:56** · We have stations. But we have to relate them. We have to relate them using this many to many relationship as we saw last week. So let me try making a table to implement this many to many relationship. And if you remember we might call this kind of table a junction table, an associative entity, a join table. has a lot of names, but it looks a bit like this. I'll create this new table to represent, let's say, visits. A rider visits a station.

**3:28:27** · So, I'll call this table visits. And inside, I'll make sure it has two columns. One for a rider ID to represent a rider and one let's say for a station ID to represent a station. Now, when I see a rider ID next to a station ID in this table, I'll know the rider with that certain ID visited the station with that certain ID. So, I'll close this out.

**3:28:58** · I'll say end parenthesis here semicolon enter. And finally clear my terminal type dot schema and I can see I have riders stations and visits between riders and stations in this associative entity this junction table or a join table up to you what you might want to call it in this case. Now what questions do we have why we have not use the primary key and the secondary key in this table?

**3:29:29** · Uh good question. So we're going to get there in just a minute. But if I look back at my uh terminal here, my schema, I'll see I really just have column names. And we saw before when we typed schema on our long list db, we had more than just column names. We had column names, we had perhaps data types, we had primary keys and foreign keys. So we'll get to that in just a minute, but suffice to say for now, we're going to keep improving this over time. Let's take one more.

**3:29:58** · Is it required to put spaces the four spaces the indents or that's just for the visual look?

**3:30:06** · Yeah, great question. Is it required to have these four spaces before each column name? And in fact, no, it's not. But it makes the code more readable. So if I I I could put this all on one line. I shouldn't, but I could. uh if I have um instead this new line followed by four spaces, I can make this more um readable for myself and for my colleagues too. Good question.

**3:30:30** · Okay, so to our earlier point, there are things that are missing from this schema. Like we have column names, but as we saw before, we should ideally specify what kind of data should be able to go into each of these columns. And for that, we'll need some new ideas to talk about here. So let's focus now on this idea of data types and storage classes.

**3:30:56** · Data types and storage classes are two very similar but distinct ideas and they're uh distinct in a way we'll talk about in just a minute. Now SQLite has five storage classes five kind of storage five kind of types so to speak of values that can values that can hold. So let's talk about the first one null for instance null in this case means nothing. There's nothing that actually is inside of this value. It's kind of a sentent value to mean nothing is here.

**3:31:28** · Integer means a whole number like one two three four five. Real talks about decimals like floating points like 1.2 or 2.4 and so on. Text is used for characters and blob kind of a funny one.

**3:31:44** · Blob stands for binary large object and it represents the data exactly as I give it to this value. If I tell it to store 1 0 1 0 1 0, it'll store exactly 1 0 1 0 1 0 in binary. So useful for storing in this case like images and video files and audio files, things that have some structure we don't want to mess around with. Now let's focus on this idea of a storage class.

**3:32:11** · These I'll say are storage classes and not data types in SQLite. Now a storage class like integer can comprise can hold several data types. Notice how there are seven different data types that could be stored under this integer storage class.

**3:32:33** · We have a six byte integer two byte integer uh eight and zero and so on. It could be any of these particular types but each of these types is under the umbrella of this integer storage class and SQLite itself will take care of making sure uh it uses the appropriate data type.

**3:32:53** · Like if I give a very large number like let's say 4 billion or 6 billion or even bigger than that it'll probably use a longer that is a bigger bite integer to store that kind of value. If I give it a smaller one like 1 2 3 or four, it'll probably use a one bite or a two byte integer for that. But SQLite's idea is that I as a programmer shouldn't have to care if I use an 8 byt or a one bite or a two byte integer.

**3:33:21** · I just care that I'm using integers, whole numbers. And they give me a storage class to use any of these up to their choice here as well. Now let's look at a few examples of values in SQLite that we could store.

**3:33:39** · Well, we have perhaps the red line as some text. And because this is characters, it's quoted. We could use the text storage class to represent this particular value here. We could have maybe an image. To the earlier point, we could say, well, this image might be best represented using a blob, a binary large object to keep all of these pixels exactly as they are in this image. But we do get some choice, some interesting design challenges. We look at the idea of fairs.

**3:34:11** · So let's say to our point earlier, fairs are 10 cents back in the 1950s or so. Well, 10 cents we could store as an integer, which seems just fine. But this could get confused. I'm talking about dollars here or cents. Maybe it would be better, let's say, if I did this. A dollar sign 0.10.

**3:34:36** · And what might that be stored as? Well, probably text, right? I could say this dollar sign isn't really a number, but now I have to include it. So I'll say this will be quoted essentially as dollar sign0. Now there's some downsides here too. Like let's say I have uh I want to add these up. Well, I can't add up text. Like what does it mean to say dollar sign plus dollar sign.20.

**3:35:01** · I can't do math with text. So maybe it would be better after all if I used a real or a decimal like this 0.1.

**3:35:12** · But I mean even here you run into some problems. If you are familiar with um how these are represented in binary you might know that decimal values or floatingoint values can't be perfectly precisely represented. And if I talk talk about 010 the computer might store 0.100000005679 it could get very wonky out to the many many decimal digits down below here. So tradeoffs and challenges overall. Let's look at these three though. I have the first one to store as an integer.

**3:35:43** · I'm trying to store fairs here. Second one as text and the third one as a floating point or a real in this case. Let me ask for some opinions here. Which one would you use and why? We're trying to represent fairs in this case.

**3:36:04** · Thank you. I prefer using integers because of course I need to get the calculation very accurately. Uh that's my point of view. Well, sometimes I can use float but you know like you said before it can get very wonky if I get you know if I really need that kind of precision I don't really recommend using floats.

**3:36:28** · Yeah, good point. So let me go back to some slides here. You might argue for the integer because you know you can precisely represent integers. And let's say I want to add up fairs over a lot a lot of riders. This might be useful for me because I know that each number will be perfectly precisely represented. I can do lots of big kind of math with this number here. To your point, this decimal might kind of as you should get wonky later on towards later decimal points. I might get some unexpected results if we add up these overall.

**3:36:56** · Let me ask though are there any proponents of this floating point value or a real value?

**3:37:08** · Okay.

**3:37:08** · So I think the uh I think this float is uh in the the number of for example for each pair like the uh like the answer that like uh truncation probably suggest one of the comments there.

**3:37:27** · Yeah

**3:37:27** · good point. Right? So if we talk about using this float value, I mean one thing we could say for it is that this decimal could be, you know, it's it's more accurate to say like we're working with dollars now and we could have maybe 10 cents which is only 0.1 of a dollar.

**3:37:41** · I totally hear that point as well. And the point we're making here is that they're really just tradeoffs among these data uh storage classes to use. Whether you're using integers or real values, it just depends on your use case and what you're designing for. So be sure to read up on trade-offs among these data types and determine for yourself which one should you best use.

**3:38:03** · Okay. So we have now these storage classes to store values. And it turns out that columns can be made to store certain storage classes or prioritize certain classes. And the key distinction here is that columns in SQLite don't always store one particular type.

**3:38:26** · Instead, they have type affinities, meaning that they'll try to convert some value you insert into a given cell or given row to the type they have the affinity for. Now, there are let's say five type affinities in SQLite. text columns can be of the type affinity text meaning they store just characters at the end of the day. There's also numeric which stores either integer values or real values depending on which one seems best to convert to.

**3:38:57** · You have integer type affinity which means it'll store whole numbers real to store floating points or decimal values and we have blob here again our old friend to store binary exactly as we get it. So whereas before we were talking about storage classes, those are associated with individual values, type affinities are now associated with individual columns.

**3:39:19** · So let's see some example of might how this might work in SQLite. Let's say I have this table of fairs and we've decided to store fairs as integers.

**3:39:31** · Well, if I said that this column called amount has the affinity for the text storage class, what would happen is if I insert this integer 10, it would look a bit like this later on. It would be converted to text be quoted in a sense to represent is now been converted to some set of characters. Let's say I insert this value 25. Well, 25 has a storage class right now of an integer.

**3:39:59** · It is a whole number. But if I insert this into a column that has the text affinity, it'll be converted into in this case text at the end of day. Let's do the opposite. Let's say I have my fair as a string, some text. In this case, I want to insert it into this column called amount. But now amount has the integer type affinity.

**3:40:24** · Well, if I insert 10 quote unquote into the column amount, I'll get back not 10 the text, but 10 the integer because again amount this column here has an affinity for the integer storage class. Let's try this 25 some text again. I'll insert it into this table. Now I'll have 25 as an integer.

**3:40:53** · So this is how SQLite allows us to give certain columns an affinity for certain types that they'll try to store values of that type so long as we insert values that could be feasibly converted to that type here. So let's go back to our schema and try to improve it now to use not just column names but also type affinities to store certain data of a certain type. go back to my computer here and let's improve this once more.

**3:41:26** · So I'll go over to my table. And now I probably want to improve the design here. And often if I want to improve this, I might just need to erase what I've already done. So let me introduce this new keyword, this new statement uh called drop table. To drop a table means to delete it, to remove it as effectively. So let me try doing this for riders stations and visits. I'll type drop table riders semicolon enter. Nothing seems to happen.

**3:41:58** · But if I type dot schema or riders is gone. I'll try drop table stations. Then semicolon hit enter and type uh let's see dots schema again. No more stations. I'll try drop table visits semicolon. enter and then dots schema and our table our database is really gone. There are no more tables inside of it.

**3:42:24** · So let me propose that instead of working inside of the SQLite prompt like typing out again and again and again create table riders, create table stations, create table visits, let me be a bit more efficient about this and create myself a schema file that I could reuse throughout this lesson and also wait it on while I'm working on this database on my own. To do that, let me quit my um SQLite prompt here and let me type something like code schema.sql.

**3:42:55** · I'm just creating this file called schema.sql.

**3:43:00** · Now, aSQL file allows me to type in SQL keywords and have them be syntax highlighted so I know what's going on inside of this file. So, let's just try this once more. I'll type create table riders and inside I'll say it has the ID column of what type ofity? IDs are whole numbers. So perhaps integer in this case I could say ID has the integer type affinity. Now let me say that writers also have a name.

**3:43:32** · And how could names be best represented? Maybe text, right?

**3:43:37** · Characters here. So I'll say name and text. Now I'll include a semicolon to say this is the end of my create table statement. And before remember how I had to kind of error out or I had to like backspace and so on to improve the design. Here I can literally just point and click and edit this file to improve my schema. And I'll later on apply this in my um database using a command that we'll see a bit later. So let's keep going here.

**3:44:06** · I'll say create table stations and inside of this stations table I'll make sure it has an ID column of type integer a name column that probably stores some text and a line column that also stores some text where name is the name of the station like Kendall MIT Harvard and line is blue line or green line what line it's part of in our subway let me try now visits

**3:44:35** · I'll say create table visits and then I'll do rider ID which has what type affinity probably integer and then I'll do station ID which has this same type ofinity it's we're talking about integers whole numbers here for ids semicolon to finish this statement now this is my schema as a whole I have riders stations and visits but now I want to apply this schema to my database so what could I I could reopen it.

**3:45:05** · Let's say I'll do SQLite 3 mbta.db in my terminal. And now I want to read in this schema.sql file. That is run the commands that are inside of this file.

**3:45:19** · So what could I do? I could say read schema.sql where readad is a command that says take whatever file you give me like schema.sql SQL and read it into this database running any SQL keywords you come across there. I'll hit enter and now nothing seems to happen. But if I type schema, I now see my schema improved.

**3:45:45** · And this is helpful for me because I what I could do now is I could just edit my schema.sql file and rerun it and rerun it to make sure I now have these tables being improved over time.

**3:45:58** · Okay, so this then is our new representation of our database. We have riders, of course, their own entity, and stations. They have an ID and a name, and stations have an ID, a name, and a line. We've also now included these type affinities integer text integer text to tell SQL what kinds of storage classes could be put inside of each of these columns.

**3:46:28** · Now before we keep improving this, let me ask what questions we have on these storage classes and type affinities.

**3:46:39** · Sir, you were using uh when you were creating the table, the table was not uh in the line. So when uh we search for the authors or books, so it comes with a perfect table. So how can we make a perfect table in the SQL?

**3:46:54** · Yeah. Do you mind um clarifying what you mean by like the the perfect table?

**3:46:58** · Uh sir, I mean that uh it was arranged in something like in boxes block boxes.

**3:47:05** · Ah good question. So um before we're able to see the results of our queries inside some boxes in our terminal and that is actually a mode of SQL light. I think you type like do mode table to see results in that version. Um here though we have no data inside of our tables. So we can't really select anything from them. Like if I go to my terminal here and I try to select some data from this riders table. Let me say select star from riders semicolon. I won't get anything back.

**3:47:37** · Next week though, we'll see how to insert and add and update and delete data inside of these tables. At which point you could write select star from riders and see some data you've inserted yourself. Great question. Let's take one more here.

**3:47:56** · Yes. Uh I would like to know if you have a column data type uh boolean.

**3:48:01** · Yeah.

**3:48:01** · Do we have a a boolean type affinity? Let's say so here we don't at least in SQLite. Some other DBMS's database management systems might have bool or boolean true or false. Right?

**3:48:15** · Let me show you this instead. If I go to my terminal, I can see if I type schema, I haven't used boolean. There's no need for me in this case, but I have used integer. And integer for SQL I can kind of for uh serve the same purpose. I could have the integer zero or the integer one to be true or to be false or true respectively. Zero being false and true being one I believe in this case.

**3:48:39** · But good question.

**3:48:42** · Okay. So to the earlier question like we've improved our tables. We now have type affinities for our columns but we don't yet have this idea we talked about last week which was primary keys and foreign keys. this idea of trying to uniquely represent each item in our own table using primary keys and trying to reference that primary key from some other table using foreign keys. So let's try to work on that now.

**3:49:09** · And for this we'll need this new idea called a table constraint. In SQLite you can apply what's called a constraint to your entire table. A constraint means that some values have to be a certain way.

**3:49:27** · Like let's say for a primary key, primary keys must be unique. They can't repeat and they must be at least in our cases going to be integers to be able to uh for quickly like add on to them over time. Similarly for foreign keys, well a constraint is that if you have a foreign key, you better find that value in some other table. Otherwise you violated this constraint of having a foreign key.

**3:49:52** · So we have two kinds of table constraints among others but two of these are primary key and foreign key and we can apply these to our table by applying them underneath the columns we tend to say will be inside of our table. Let's try these two here now. So let me come back to my terminal here so we can implement our very own primary key and foreign key constraints. We'll go back to my SQLite terminal and clear my screen. And let's then pull up our schema.sql file.

**3:50:22** · So we can keep modifying our schema. I can now see I have the writers table stations and visits. And I have some columns that could be primary keys or foreign keys, but I need to declare them as such. So here in the riders table, what was our primary key? Well, it was ID. Every rider should have their own unique ID that should not be duplicated across any two riders. So to ensure that constraint is applied, I could follow this up with a comma and then say primary key ID just like this.

**3:50:56** · Now ID is the primary key of this rider's table. I can go down to stations and ask what was my primary key? Well, similarly, it was ID, this ID column on line 8. So I'll type a comma followed up with primary key ID. And now that ID column is a primary key. It has that constraint applied in stations. But now if I get down to visits, I have a few more options.

**3:51:23** · Visits here actually doesn't have its own ID column that I created. I instead have a rider ID and a station ID column. So a few options here. One option is actually to make a joint primary key. I could have a primary key composed of two columns, both rider ID and station ID. If I applied that constraint, that would mean that if I were to ever insert a row that had the same rider ID and the same station ID as another row, I would trigger a constraint violation.

**3:51:55** · Every row that has a rider ID and a station ID has to be unique in their combination of those two values. to write that kind of scenario. I could follow this up and I could say similarly the primary key of this table is not just rider ID like this but it's also station ID. Now this is a joint primary key constraint.

**3:52:17** · But if we think about this logically I mean it kind of stands to reason that somebody would visit a station more than once and I don't want to make sure that every combination of rider and station ID should be unique. I want people to be able to visit a station more than once.

**3:52:34** · So maybe not the best design for this table, but I could certainly use it in other cases or other contexts. One other option would be to uh do what you did before and to have maybe the ID column here of type integer and then down below make that our primary key a bit like this. And now visits has its own ID column. But actually SQLite by default will give me its very own primary key one called row ID. It's implicit. I can't see it.

**3:53:05** · But I actually could query it. I could query for row ID all one word and get back a unique primary key for this table. SQLite is automatically created for me. Now we have seen the primary key options. What are our foreign key options? Well, it seems like rider ID and station ID are the foreign keys of this table where rider ID references the ID column in riders and station ID references the ID column in stations. So to codify that to make that a reality in our schema, I could follow this up with the foreign key.

**3:53:37** · The foreign key of this table is rider ID and it references it references the riders table and the ID column inside of it using this syntax here.

**3:53:51** · Now I could keep going. I could say I have more than one foreign key. I also have a foreign key foreign key called station ID and that references as we said before the stations table and the ID column inside of it. So now here I have my completed schema. I have a primary key for the tables I've declared an explicit column for a primary key and now I also have foreign key constraints for those columns that should be foreign keys.

**3:54:18** · So now let me ask what questions do we have on the schema or on primary keys and foreign keys.

**3:54:27** · Uh so yeah I just noticed that whenever before we hadn't added the affinities and the keys we were not applying commas after each column name. So what is the difference there?

**3:54:40** · Yeah, a good catch. Let me um kind of show you what this looks like in my terminal so you can see it live. Um you I think had noticed that before we had let's say this primary key ID um constraint in writers we had done something like this. Let me just copy paste that. And we had removed this last column or comma from the name column. Is that right? And if that's the case well it's um just convention just style here.

**3:55:06** · So if I want to keep adding some constraint or like a new line to my table, I should include a comma here.

**3:55:14** · This name column was the last um portion of my table I had specified. I have a column called name that has type affinity text, right? But now if I add this new constraint, we'll have to follow it up with followed up after a comma from this new column here. Notice now this constraint primary key ID is the last um let's say attribute of my table I specified. I no longer need to include a comma at the end of it.

**3:55:42** · So whatever is the last portion I should have a uh I should not have a comma after but everything else I should. Let's take one more question here too.

**3:55:54** · Would it be okay for the visits table to have an ID column as well?

**3:55:58** · Yeah, a good question. It would be okay for the visits table to have an ID column as well. It certainly would be.

**3:56:04** · We could define our very own primary key for this table, too. So, let me go back and show you how that could work. I'll go to my visits table here, and I could try to add my own primary key to this table. I could say ID, make a new column here, make it of type affinity integer like this. Let me scroll up. And now, let me add some new constraint. I could say because I've made my very own primary key, I'll say primary key id.

**3:56:34** · Now this table has a primary key that I've created called ID. And this will be in place of SQL lights that it would have made called row ID itself, but hidden from my own view.

**3:56:50** · Okay, let's keep going then. We've seen table constraints. We've seen type affinities, but we could probably do more to improve the design of this table or this database. So let's introduce one more kind of constraint. This one called a column constraint. So whereas a table constraint applies to the table as a whole, a column constraint applies to a particular column. Let's say maybe I want a column to have certain uh data inside of it.

**3:57:19** · I maybe I want to make sure it doesn't have null values and so on. I could do that with column constraints. There are four in SQLite. Check, default, not null, and unique. And each one does something different.

**3:57:36** · Check allows me to make my very own check. Like check to be sure that this amount is greater than zero. Or I could use default. Default means if I don't supply a value, when I add a new row, it'll just use a default value instead.

**3:57:52** · Not null means I can't insert null or empty values into this column. In fact, it's required. Unique means I want to make sure that every row in this column is a unique value. It doesn't appear twice in my data set. So, let's try applying a few of these to our schema here. Go back to my terminal. And now, let me check out this.

**3:58:17** · Well, I could try applying the notnull constraint when I know I want a column to be required effectively. Now, where could I best apply that? Maybe I could apply that to the name column in stations. Like stations must have a name. So, I'll say the name column cannot be null. It cannot be empty in here. Line also should probably be not null. A station must be part of some line. I can't have an empty value for line.

**3:58:48** · So I'll say too this should be not null. Now I could apply this up at name. I could say riders must have a name too. Let me try that. I'll say text not null. Or I could leave it optional. I could say maybe text just on its own and let writers choose to supply a name or not.

**3:59:11** · Now the question here is should I apply not null to my primary key columns like ID not null or ID not null here you might think that you should for thoroughess sake. Well it turns out that when you apply the primary key table constraint down below here this already ensures that there are several constraints applied to this particular column called ID. among them being that ID cannot be null.

**3:59:39** · So no need to duplicate this and say that this ID cannot be null when I already have it specified down below that ID is a primary key.

**3:59:51** · Let me check others here. You might also think could I do it for rider ID and station ID? Should I include not null here? Rider ID not null. Station ID not null. Well, that would be a good thought, but again, we're taken care of by our table constraint using our foreign key here. Again, this constraint will say if rider ID doesn't already exist in the ID column of riders, I can't insert that value.

**4:00:20** · And we could probably presume that if riders ID is a primary key, well, null will not be part of this column. And therefore I already can't insert null for rider ID or station ID. This would be in this case redundant. So not null is good when you have columns that are neither primary keys nor foreign keys and you want to make sure that they have all they always have a value that they are never uh null effectively.

**4:00:52** · Okay. So that is not null and we could keep going here. We also had one called unique that makes sure every um every value every row in this column is unique. Where could we apply this? I could try to apply it let's say to the name of a station like station should have unique names. So I'll say not null and unique. Now this column has two constraints. The first not null. It should always have a value.

**4:01:20** · The second unique the value shouldn't repeat throughout this column. line I might leave without this constraint. I could imagine two stations being on the same line like both on blue. I'll allow that in this case. Now again, we could try to apply unique to our primary keys or our foreign keys as I just did here, but it's already taken care of for us using this primary key constraint. A primary key again is always going to be unique and never null.

**4:01:51** · So we'll take advantage of that already using our primary key and foreign key constraints here. Okay. So we've seen unique and not null. And I might argue we're at the point where this schema seems to be fairly optimized at least using our column constraints, our table constraints, our type affinities and so on. So let's ask then what questions do we have on not null and unique if any.

**4:02:23** · So basically to recap if I understood correctly it's not precisely about not null and unique but about the concept of the key uh labeling a key immediately give us the attribute of not null unique and to be referenced. Right?

**4:02:38** · That is true. So when you use a primary key or a foreign key constraint, there are other constraints that go along with that constraint. A primary key for instance must not be null. Um it must be unique and so on. So it would be redundant to apply that again to say that this primary key should be unique or not null. Good clarification there.

**4:02:59** · Okay. So I think we're at the point where this schema is pretty well set for us. And we're going to need to think about though how we use this in the real world. Like if this is our schema here, we have riders and stations. Well, what could we do? I mean, riders tend to I mean, they could register for the subway. And riders, well, they do visit stations, but I think if we applied this to the real world, we'd see that this isn't quite how it's actually done. Like riders don't really register that often.

**4:03:34** · if uh a rider who's new to the city comes in, they want to ride the subway, they should be able to ride, too. So, it turns out, at least here in Boston, the MBTA doesn't really track riders, per se, but they do track what we call Charlie Cards. If you want to ride the subway, you get a Charlie Card. Charlie card allows you access to the subway, keeps track of your fair, your balance, and so on. Allows you to swipe in to certain stations.

**4:03:58** · So, and when we come back from a break here, we'll see how we can actually implement these Charlie cards instead of riders to make our system more efficient and more in line with what happens in the real world. We'll see you all in just a few.

**4:04:13** · And we're back. So, we saw last time this challenge of designing a system for the Massachusetts Bay Transportation Authority to represent riders and stations, people who get on a subway to go around Boston. But as we also saw, we learned that the MBTA doesn't keep track of riders themselves. They keep track of Charlie cards, this card that a rider might carry in their pocket.

**4:04:38** · And they can scan this card at a station to enter or even to exit in some cases to make sure that their fair is counted as they enter that station. So let's think now how to improve our schema to represent not just riders like me but Charlie cars themselves people might carry around when they enter the subway station. Well we saw before we had riders and cards.

**4:05:05** · But our goal now is to remove riders from the picture. Focus only on cards.

**4:05:11** · Well cards as we've seen might make us swipe at a station. If I enter Harvard station, I might swipe my Charlie card to enter that station. And we could see that a card would have maybe many swipes involved. Like if I swipe at Harvard, I might also swipe at MIT or swipe at Park Street and so on. We could see that a swipe can only happen at a single station at a time, though. Like if I swipe at Park Street, I'm only swiping at Park Street here.

**4:05:42** · And similarly, a swipe might only involve one single card. So if we think about these entities and how they relate, we could also think about what kinds of columns we should have inside of each entity. In this case, I would argue we should have something a bit like this. We could say that a card has a ID for its primary key in this case.

**4:06:03** · Similarly, this card makes a swipe and this swipe has itself an ID as well as a type, some time that that swipe happened and an amount or a transaction that is involved. So, for example, let's say I swipe in at the Harvard Square station. That type of swipe might be to enter the station at some certain time. Now, associated with that swipe is also some amount in dollars that happened to be subtracted from my card.

**4:06:34** · Like, let's say the fair nowadays is $2.40. Well, that amount is subtracted from my card from this swipe.

**4:06:44** · Now, of course, I do all of this at a station which has our same columns from before, ID, name, and line. So, a similar idea now, but we're replacing riders with cards and adding more information to these visits. They're instead swipes that could be maybe entering the station, exiting the station, or just adding funds to my balance, for instance. So, let's see how we could improve our schema now using some new SQL keywords to alter our tables and add some new ones, too.

**4:07:13** · I'll go back to my computer and let's see how we could try to alter the tables that we've already created. Like we already have a riders table, a visits table, and a station's table, but we could learn some new statements, some new queries to actually update and alter these tables as well. The first one, as we saw a little bit before, is this one called drop table. Arguably the most dramatic thing you can do to a table is just drop it, delete it like this. So, let's try deleting the writers table from our database.

**4:07:45** · I'll go back to my uh go back to my database here. I'll type SQLite3 MBTA. DB to pull up this database again. And now, if I type schema, I'll see I have a riders, stations, and visits table. But no longer do I want to have the riders table. I want to remove that. So I'll say drop table riders semicolon. Now I'll hit enter. No more riders table. If I type dots schema, that's gone for my database.

**4:08:21** · Well, what could I do now? I've dropped the table, but I'd still need to maybe update visits to instead be swipes. I could probably leave stations as is. But I want to update a table or alter its schema. I can use some new commands as well. I'll use this one called alter table. Alter table looks a bit like this.

**4:08:43** · I can use the alter table um statement here and give it some table name like let's say alter table visits and then inside uh this visits table I get to ask what do I want to do? Do I want to let's say rename the table? I could do that. I could also decide to add a column, rename a column or drop a column algether. Let's try first looking at rename to.

**4:09:09** · I want to rename this visits table to a swipes table representing not just a visit to the station, but a swipe of a card. So, let's try this one here. I'll go back to my computer and I'll go back to SQLite and I'll say I no longer want visits to be called visits. I ideally want visits to actually be called swipes. So let me try this. I'll say alter table. So we saw before visits rename to swipes like this semicolon. Now I'll hit enter.

**4:09:44** · And now if I type dots schema again I see oops kind of strange. I'll type dots schema again. I'll see swipes. no longer called visits, but now called swipes.

**4:10:01** · Well, we saw I'd ideally like to add a type of the swipe. Maybe I'm entering the station. Maybe I'm exiting. Maybe I'm just adding funds or depositing some funds. So, let me try adding let's say a new column to swipes. I'll say alter table add column alter table swipes.

**4:10:22** · Going to name that table swipes like this. And then let's add a column. Add a column called type. And this will have the type affinity text. I'll hit semicolon. Enter. And now if I type schema, I'll see well I have a column called TTP. So clearly I made a typo here. I had rider ID, station ID, this new column down below called TTP.

**4:10:52** · I kind of want to fix this, right? I don't want TTP. I want type. So probably a good chance to use my rename column. I'll come back here and I'll try that. I'll instead do alter table alter table swipes and I will rename a column. Now I'll say rename the column TTP to type spelled correctly. Now hit semicolon.

**4:11:21** · Go my terminal type.s schema. And now I see over here that type has been added to my table of swipes. I see rider ID, station ID, and now a new column called type. So through alter table, can we go ahead and add new columns, rename them even, or if I wanted to just drop the column al together. Let's say I add this column type and I change my mind. I don't want it here anymore. I go back to my computer and I could try dropping a particular column.

**4:11:51** · Let me try in this case alter table swipes. And now let me drop column type semicolon. Hit enter. And now if I type schema, I'm back to where I began. So these are the commands we can use to alter our tables to improve them if we make a mistake during our first create table command or if we want to add more functionality later down the line.

**4:12:21** · So ideally I could keep using you know alter table, add table, create table, drop table and so on. But what I want to do here is just probably start from scratch. Like I have, you know, stations and swipes and so on. Why don't I just go back to my schema file and use that instead? So what I'll do is I'll drop table for stations and oop semicolon. I will drop table for uh swipes now.

**4:12:44** · Semicolon. I'll type schema. And now I'll see nothing in here. I'll quit and I'll type code schema.sql. Let me just start from scratch using this schema.sql.

**4:12:59** · So we no longer want to have riders. We only want to have cards. So I could just rename this table here. I'll call it cards. Crate table cards. Now cards don't have a name. They only have some unique ID in this case. Now I'll leave stations just as it is. This seems perfectly fine to me. Stations have an ID, a name, and a line with these constraints applied to the name and line columns. But now the visits table. Well, the visits table is no longer a visit to the station per se.

**4:13:32** · It's more a swipe of the card at that station. So let's now say visits becomes swipes. And among these new columns to add are the following. I want to have not just an ID for each swipe, not just an ID for rider ID and station ID and so on, but also I want to have a type of swipe. Am I entering the station, exiting or depositing some funds?

**4:13:57** · So I'll say the type of this uh is going to be a new column and the data type this holds will be text enter, exit or deposit for some funds. Now let me try another column too. I'll include a date time. A date time is like a time stamp. What time did this swipe actually happen? And I'll make this type numeric. Numeric can store all kinds of dates and times for me in this table. Now let me add one final column.

**4:14:30** · This one will be an amount. I'll also use numeric for this kind of uh column here. And I'll say that this column uh called amount can store in this case integers or real numbers like floats and so on. I'll probably decide on that when I actually add some data to this table. Okay. So here we've updated our schema to represent that diagram we saw before.

**4:14:55** · I have cards, I have stations, and I have swipes that have some type associated with them. enter, exit, deposit, some date, time, and some amount that was charged to me while I made this swipe. Either I added some funds, which case amount is positive, or I subtracted some fun entering or exiting, in this case, uh, from the station.

**4:15:18** · All right, so I have these tables now, and now I want to probably apply some of those same column constraints we saw before. like here it's fine but I also want to make sure I'm not adding some data that I don't want to add to this table. So I could go back to my old friends these column constraints and we saw before we had uh default and not null unique and check we've used not null and unique but we haven't used check or default.

**4:15:47** · So let's start using more than just not null and unique and also focus on check and default what they can do for us here. I'll go back to my schema and let me just make sure that I'm making all the columns that I want to be required actually required. I'll go into my swipes table and I'll say that type I mean this should be required. I should I I should know whether I entered, exited or deposited some funds. So I'll say text not null.

**4:16:17** · Similarly for the timestamp the time this swipe happened I want that to be not null as well. So, I must know what time I swiped the card. And also, it makes sense for there to always be some amount associated with this swipe. Either I added some funds to my balance or I removed some funds overall. So, I'll make this not null as well.

**4:16:39** · Well, let's see what we could do here with default. default gives me some default value, some initial value to add to this column if I don't specify what kind of value to add. Well, this could be good for date time. Date time here is again the timestamp, the time I swiped this card to enter, let's say, Harvard station. Well, if I want this to always have the current time, I could use default.

**4:17:09** · I could say the default value for this column is this special value here. Current timestamp in all caps. Current timestamp will show me the year, the month, the day, the hour, the minute, and second all in one value and insert that into my table. So as soon as I add new row, if I don't supply a time for this datetime column, I'll instead get back the current time exactly as it is represented in SQLite.

**4:17:44** · Now what could I do further than this? I could also try to add a my very own check. Maybe I want to make sure that the amounts here are never equal to zero. Like nobody should ever be able to make a Z transaction or Z swipe. they're always being charged some money or they're always depositing some money in this case. So I could say amount here has my very own check on this column and inside check I could actually write my very own expression to check for.

**4:18:12** · I could say for example amount is not equal to zero using those same operators we saw back in week zero. This will ensure that any value inside amount will not be equal to zero.

**4:18:30** · Let's try it also for type. I mean type can only have a few values. We saw enter exit deposit some funds. I could make sure that only those values are included inside my type column. I could say check that type is in some list of values.

**4:18:48** · Going back to week one here we talked about in I could say maybe the type is in enter exit or is in deposit. So now when I have this table called swipes I'm representing what I'm actually doing when I go to Harvard station. I have here a visit for myself. My very own ID here which I'll update in just a second.

**4:19:12** · I have a station ID where I'm actually going to visit. I have a type that I'm going to use to enter, exit, or deposit some funds at this station. I'm doing at a certain time, and I have an amount associated with this transaction.

**4:19:28** · Now, there's one thing to fix here, which is that we're still talking about riders inside our swipes table. So, let's fix that here, too. I'll go back to my computer, and let's try fixing this. I have a rider ID inside of my swipes table, but no longer do I have riders, I have cards. So, let me say that this is now a card ID. And down below in my foreign key, I'll say that this card ID column references the ID column in cards.

**4:19:58** · And I think this should represent everything I want to represent about swipes at the station. So let me ask now what questions we have about this new schema and the constraints we've applied.

**4:20:15** · I wonder how how could you delete or drop table riders when you use uh ID as a foreign key. I tried to do that but I got an error.

**4:20:28** · Ah yeah. So you're getting into some more advanced stuff here. And suffice to say for now, my foreign key constraints aren't actually being checked right now, but yours might be. If you try to drop a table that has actually has some data is referenced by a foreign key, SQLite will warn you, perhaps just tell you you can't do that because this ID is referenced from this table over there.

**4:20:50** · So in that case, best to delete the value that has that foreign key and then proceed with dropping that table al together. Good question there. Yeah, let's take one more.

**4:21:03** · How much this syntax uh same the other SQL languages same as SQ uh same as SQL like SQL languages.

**4:21:13** · How much the syntax same?

**4:21:15** · Yeah, good question. So here we're using the SQLite database management system.

**4:21:20** · It is similar to but distinct in some ways from others like my SQL or Postgress SQL. I would say that most of what you're doing here could also be ported to MySQL and Postgress SQL with a few exceptions you might need to treat on a case- by case basis. In fact, the developers of SQLite built things so that it would be easy to port their database schemas to another schema like my SQL or Postgress SQL as well. But good question there.

**4:21:49** · All right, let's take one more question here. Imagine if we put in the ID, we don't put any data type, it's going to give us in the schema, it's going to give us a text or Yeah, great question. So, you're asking if I didn't tell SQLite what kind of type affinity a column had, what type affinity would it actually have? A great question.

**4:22:15** · In this case, by default, SQL light gives the numeric type affinity where numeric can store integers or real values. But if you give it like a string of text like let's say red line, it will store that for you too. Um kind of uh non-intuitively, but it will. But the default uh type is numeric in this case if you don't otherwise specify. Good question.

**4:22:40** · Okay, let's come back then and let's focus on wrapping up on a final few pieces here. So, we've seen some table constraints which we applied primary keys and foreign keys. We saw column constraints where we could make sure that certain values were given to us through not null. We could also make sure that the uh uh let's say the value is in some list of values using check or making sure that it's not some value also using check as well. default allows us to specify a given value for every new insertion of rows here.

**4:23:11** · And this is actually pretty important to have not just you know schemas that have column names and um let's say you know type affinities as well but also constraints to make sure the data we insert works well for us. And there actually a story behind this person who's on the Charlie card. Uh, this person who's on the subway, his name is Charlie, and he's perhaps the most famous subway rider in all of Boston.

**4:23:40** · Back in the 19, let's say mid1 1900s, the uh band called the Kingston Trio wrote a song about this man named Charlie. Charlie supposedly got on at the Kendall Square station where MIT is, and he made for Jamaica plane. But once he got Jamaica plane, the guy asked him for one more nickel.

**4:24:00** · And well, he didn't have that nickel. So he got stuck on the train for years and years and years and couldn't get off of the subway. So keep in mind Charlie when you're adding your own database constraints, making sure that if you get the train, you're able to get off of it at some point, right? Don't end up like Charlie in this case. So with this in mind, you're able to design your very own database schemas that keep not just certain columns involved, but also type affinities for those columns. Types that those data types types of columns can store.

**4:24:29** · You're also able to apply constraints to those columns to make sure that the data you're inserting is data you actually want to have in that column. Next time we'll focus on actually adding data to our columns to actually write data to a database file to insert, update and delete that data all together. So with that in mind, we'll see you next time.

### Writing

**4:24:52** · \[Music\] Well, hello one and all and welcome back to CS50's introduction to databases with SQL. My name is Carter Zeni and last we left off we learned how to create our very own database schemas. It is a way to organize data in our database.

**4:25:21** · Today we'll learn how to actually add data to our databases to insert to update and delete data. We'll do all of this in the context of Boston's very own Museum of Fine Arts or the MFA for short. So, the MFA here in Boston is a century, well maybe about a century old museum that has many artifacts and artwork inside of it, both historical and contemporary.

**4:25:46** · And it's worth asking, I mean, how do they keep track of the thousands of items that are in their collections?

**4:25:52** · What could they possibly use? Well, chances are they're likely using some kind of database. And on that database, they want to do four actions we learned about back in week zero. They could perhaps create data to add data or insert data to the database when they get some new piece of artwork for instance. They might want to query their database to read from it. They could also update data, change the artist, change the artwork in some way. And they could also just delete data to remove it all together.

**4:26:22** · But if we think about these creating, reading, updating, and deleting, we'll notice that reading, updating, and deleting, we can't do those if we don't actually have data in our database. And so today, we'll see how to create data, how to insert data into our very own database. Now, let's think about the MFA's collections. They're collection of art and artifacts. And let me propose they have a database looks a bit like this.

**4:26:51** · It's a single table and it has a title column, an accession number, which is a fancy way of saying a unique ID internal to the museum and also a date it was acquired. We have of course a primary key on this table called ID. And let's think, well, the museum might want to acquire this piece here, this one called profusion of flowers. Well, how could they log that this artwork is inside of their database? They could maybe just add a new row.

**4:27:21** · They could say, "Let's put Profusion of Flowers as the first item in our collections here. We'll give it a title, an accession number, which again is just unique ID internal to the museum, and the date it was acquired.

**4:27:34** · And that row then has its own primary key to identify this row uniquely in our database." Now, let's say they get another piece of artwork. They get this one called Farmers Working at Dawn. And they want to add this one to their table, too. Well, they could do the very same thing. They could just add a new row. They could say, "Let's make a title, an extension number, and a date it was acquired in this brand new row here for that piece of artwork." And maybe they get another one, too. Same thing. Maybe they'll get back spring outing and they want to add this to their collection.

**4:28:04** · They could simply add another row like this.

**4:28:09** · Now, it turns out that the database administrator behind the MFA might be running a SQL statement that looks a bit like this. Insert into. We can use insert into to add a new row to any given table. And notice how insert into needs to know a few pieces of information. The first is what table to insert into. What is the name of that table? Second, it needs to know what columns are we adding data to inside of this table.

**4:28:42** · We give it a list of those columns here. Then, of course, it needs to know what new values should go into this new row. For each of these columns like we saw before, is it profusion of flowers? Is it spring outing? etc. Here we can see that we have this list of values. And notice how value zero, the first value in this list, corresponds to the new value that will be inserted to this first column. And we can keep having value one or column one, value two and column two, each one aligning with that particular column there.

**4:29:14** · So let's see an example of this actually in code to understand it a bit more concretely. I'll go back to my computer here. Let's actually create our very own database that involves this schema of having our very own table which we can keep artists and artwork and um artifacts as well. So I'll type SQLite 3 MFAD db to create a database for the Museum of Fine Arts abbreviated as MFA.

**4:29:47** · I'll hit enter here and notice how I can now have access to my very own MFA. DB inside my SQLite environment. Well, now I can type schema to see the schema of this database. So, if I hit enter here, well, nothing's there because I just made this database. There's nothing in it yet. Well, it turns out I do actually have a schema file prepared for me already in schema.sql.

**4:30:14** · Here, I propose we make a table called collections. And like our table visually, it has, let's say, four columns. one as an ID, the primary key of this table, one for a title, one for the accession number, the unique ID internal to the museum, and finally the date it was acquired. And notice here that title has to be actually added to our database. It can't be null. It can't have an empty value. Same thing for accession number. And further, accession number has to be unique.

**4:30:46** · I can't have two items with a different accession number. Otherwise, I might get them confused in my database or inside my museum archives as well. So, let me then add this schema to my database. And I can do so with this command right here.

**4:31:04** · This is a SQLite command called read that we saw a little bit last week as well. I could type read and then the name of this file I want to read. So I'll say read schema schema.SQL hit enter. And now if I type let's say dots schema I can see that same SQL schema same database schema now inside of my terminal.

**4:31:31** · Okay. So now, as promised, let's try adding some rows to this table because right now, if I do select star from collections semicolon, I don't see anything because nothing is inside yet.

**4:31:45** · But I could add something using insert into. So let's try that. I'll say insert into the collections table. And now I have to ask what columns inside of collections do I want to add data to?

**4:32:00** · Well, I probably want to add to the first the ID column, that primary key column. Then maybe I want to add a title to this row and also an accession number and also of course the date this piece was acquired. So now I have the table I'm inserting into along with the columns I'm adding values for. So for style sake, I'll hit enter here. And now I could type a list of values to insert into this new row. I could say values and then inside parenthesis the values I want to insert.

**4:32:32** · Maybe the first primary key that I give to this item is going to be just one. Start at one and add up as we add new items. For the title, I'll say let's call this one profusion of flowers. This is the piece we recently acquired into our collection. The accession number that we gave it was 56.257 257 and the date it was acquired was back in 1956 0412.

**4:32:58** · Now I have all these values here. I'll type semicolon hit enter and nothing seems to happen. But if I type, let's say select star from collections semicolon, what do I see but this new row inside. Let's do it again to get a hang of this.

**4:33:16** · I want to now add farmers working at dawn to my collection. So I'll do the same thing. I'll say let's insert into the collections table and let's add values for the ID column, the uh title column, the accession number, and also the acquired column like this. Again, for style sake, I'll hit enter. Now I give some list of values to add into this new row. I'll say values here. Then this list of values to add for each column. Well, the first column I have to give a value for is ID.

**4:33:47** · If you remember, our last ID was one. So, what should this ID be? Maybe two. So, I'll type two here as the next uh increment of my primary key. Then I'll give it a title.

**4:34:01** · And this title was farmers. Farmers working at dawn. We gave it an accession number to keep track of it in our own internal museum records, our own archives here. So, I'll say 11.615 one 6.5 6.152 is the accession number for this particular item. Then I'll say we acquired it back in 1911 on 0803. Now I'll hit a semicolon here. Hit enter. And now I should be able to see if I type select star from collections.

**4:34:32** · Select star from collections semicolon. I now have these two items inside of my collection. Now let's do one more here, but let's focus in particular on this primary key.

**4:34:47** · Like notice here how we've been actually inserting our very own primary key one and then two. But maybe that's not the best design. Like if I let me try this again. I'll say insert into uh let's go for collections is our table name. And maybe I'll try again to add to the ID column, the title column, the accession number, and the acquired column here.

**4:35:14** · What could go wrong, do you think, if I try to specify the primary key myself? Let me ask this as an audience question here. Feel free to raise your hand. What might go wrong if I try to make the primary key myself and insert a value myself?

**4:35:34** · Uh let's go to Sakiva.

**4:35:37** · Yeah.

**4:35:37** · what we could do when we had to uh you know load a lot of values like maybe uh like big data or something. Is there a way to add it through a CSV file or something rather than typing insert into tables?

**4:35:52** · A good question. I think you're on to something here which is we're inserting one row at a time which could get easily repetitive. So let me hold that thought for just a minute here and focus on the primary keys before we see some more efficient ways to actually add data to our tables. So, I'm with you on this idea of maybe we don't want to duplicate this primary key, right? Maybe we could do a little better than that. So, I'll come back to my computer here. And if I specify the primary key, I might actually add a value that's already in there. So, I could thankfully leave it up to SQLite to actually increment this value for me. Let me try leaving off ID.

**4:36:27** · In this case, I'll omit the ID altogether, which seems at first like a bit of a bad thought. Like shouldn't every row have its own ID? Well, let's just try and figure what happens. I'll hit enter here. And now I'll say let me give the values. Well, now the first column is the title column. So I'll go ahead and say that this one will be called spring outing. We're going to add this one to our collection here. The accession number in this case is 14.76.

**4:36:53** · And we acquired this one all the way back in 1914 0108 semicolon. So I'll hit enter here. And notice how there's no ID that I have specified. But now if I hit enter, seems to work. I'll type select star from collections. And what do I see? But the new primary key of three. So it seems like SQLite actually increments the primary key for me.

**4:37:20** · If I add some new row, it looks what is the current highest primary key and adds one to that automatically for me. And I've gotten that by specifying in my schema this primary key constraint down on line six. So pretty handy for me here. I see a few other questions too. So let's take those before we move on as well.

**4:37:46** · Let's go to Andre. I just want to ask if I delete uh the let's say the third uh record and type again will it uh number it of the fourth number or or the third one?

**4:37:59** · Uh great question. We'll see this a little bit later on too. But if I delete some row, let's say I deleted the row with primary key of one. Well, what SQLite will do at least by default is actually take the highest value. Let's say the highest value is still three in my database. It'll add one to that. And when I insert that new row, it'll have the ID of four in this case. Okay. So let's explore a bit more some of these constraints on tables.

**4:38:24** · Like here we're talking about the primary key constraint, but we also have as we saw before the notnull constraint and the unique constraint. So let's try inserting given those constraints here.

**4:38:37** · I'll go back to my computer and again notice in my schema I specified that this title column should always be not null. It should never have a null value inside of it. And similarly accession number should also be not null. It should also be unique. I should have no two rows that have the same accession number. And maybe kind of uh playfully subversively here, let's try to run against this constraint. Let's actually try to add the same accession number and see what happens.

**4:39:07** · So I'll come back to my terminal. Let me just reinsert let's say spring outing. Notice how if I select star from collections, it's already in here. But I'll try to add it yet again with the same accession number. So I'll say insert into collections. And by now this is what becoming a little more familiar. I now want to say the row the columns I want to add data to. So I'll say the title column, the uh accession number accession accession number column and also the acquired date.

**4:39:38** · I'll hit enter and now I'll say the values again. Let's reinsert spring outing. I'll say spring outing as a title. The accession number is 14.76 and the date it was acquired was again 191408 semicolon. Now if I hit enter, what do we see?

**4:40:01** · runtime error unique constraint failed.

**4:40:04** · So it seems we ran against this constraint here that we specified on line four here. Excession number should always be unique. But by trying to add a new row that had that same accession number, we run into this runtime error and our operation was not completed. If I say in this case select star from collections. Notice how I guarded myself from adding spring outing more than once with the same accession number. So some usefulness here to these kinds of constraints.

**4:40:35** · Let's try violating not null too. I'll try adding a title that is actually null, non-existent. Try to add a painting without a title itself. Let's try this. I might try insert into the collections table and I'll add to the title columns, the accession number and also the acquired column. Now I'll say the values here. But remember this null value. Null meaning nothing. This value doesn't exist. I could insert that into my table or at least try to. I'll say null is a title.

**4:41:07** · And similarly null is the accession number. And let's say just playfully we got this painting uh back in 1900 on January 10th like this. Okay.

**4:41:19** · Now semicolon. I'll hit enter. And we see the same runtime error. Constraint failed. In this case, the notnull constraint. So notice again how in my schema I specified title should be not null. But here when I try to insert a null value, I run into that constraint and I can't insert that value. If I try to select star from collections, I should see in this case that insert didn't work.

**4:41:47** · So these constraints are really guard rails against me, against other users to adding values that we really shouldn't add to our table. Okay. So presumably here, you know, we're on to something by adding some rows. But if the museum acquires more than one item, maybe 100 at a time, I don't want to be the programmer who's sitting there writing 100 insert into. That's like not what I want to do.

**4:42:14** · There's probably a better way to do this. And let me show you one way to do this. One way is to instead of inserting one row like this to instead insert multiple separated by commas. So here I might say this is my first row for each of these columns. This is my second row again for each of these columns and so on and so forth. And it's worth noting this is not just a matter of convenience.

**4:42:40** · Like if I tried to insert a 100 rows, this is certainly convenient for me, but it's also most often in most cases going to be faster for me to insert 100 rows in one go than to insert one row 100 times. So this is both a convenience thing for programmers and also an efficiency thing to actually optimize your database as well. So let's try this syntax now to avoid me sitting there for hours and hours writing many insert into.

**4:43:09** · I'll go back to my computer and this time let's say we got two paintings at once. We got two. So I'll try to add both of them. I'll say insert into the collections table. And again, I want to keep adding to my title column, my accession number column, and even my acquired column like this. Now, I want to add in some values. So, I'll type values here. And as a matter of style, let me just say I'll make a new line.

**4:43:40** · I'll hit enter here. And now, I can type each of my new rows on their very own line. So, again, I'll type all of the values that I want in my first row. I might call this one imaginative landscape. We got this one back in. Actually, we don't quite know when we got this one. If I type 56.496 is the exception number like here. 56.496.

**4:44:04** · The MFA actually doesn't know when they got this painting. So, if they don't know, let's just insert null. This is intentionally left blank. Okay, this is my first row. Now, I want to add a second one in one go. I'll follow this up with a comma. And now I'll type out my next set of values. This next one we required is called pianies and butterfly. Now I'll say the succession number is 0681899 and the date we got this one was back in 1906 on January 1st.

**4:44:35** · Now I'll hit semicolon here. And now if I hit enter, nothing happens. But if I type select star from collections semicolon, what do we see? But now two new rows being inserted. So a handy way to insert more than one value. And also if you have a lot of values, a more efficient way as well.

**4:45:01** · So let me pause here and ask what questions we have on insert into whether adding one row or adding multiple. Let's go to teas. Sir, imagine you are writing a code or inserting a row. So by mistake you have entered the uh wrong spelling of the title. So how will we uh rename it?

**4:45:23** · Uh a great question too and often is the case with me. I make typos all the time.

**4:45:28** · I might add the uh artwork title and misspell it for instance. Well in that case I can't use insert into to correct it. But I can use a new statement we'll see a little later called update. And so with update can actually change the spellings of things and we'll see that a little later today. But great question to peek ahead as well.

**4:45:49** · Okay, so let's keep going here. Let's think about how we can keep adding values to our data set. And so far we've seen insert into with one row and with multiple. But one more way to keep in mind is you might already have your data perhaps in some other format. And one common format looks a bit like this on our screen over here. This file is called a CSV for commaepparated values. Now why commaepparated values?

**4:46:24** · Well, let's just look at it here. We see some presumably column or column names like ID, title, accession number and acquired. But what separates these column names? Well, looks like commas. ID, title, title, comma, accession number, and so on. Every row is still its own row. That makes sense here. But now those row values are also separated by commas. Notice here the first value before the first comma corresponds to the first column. This id is one.

**4:46:57** · Similarly the next commaepparated value profusion of flowers belongs to that next column here title as well and so on and so forth. You could if you wanted to kind of draw a snaky line to see how these columns correspond down our file here. Now you might often have data already in this format and it's actually pretty convenient to try to import this data into SQLite into your very own table so you can use SQL on it. So let's try doing that here. Taking a CSV like this and adding it to our database.

**4:47:29** · I'll come back to my computer and at this point I want to start over. Let's say I didn't use insert at all. I actually got a CSV from the MFA of all the items in our collection. So I'll typequit to leave this database. And now I'll type rm MFA. DB to remove this file al together. Now let me show you mfa.csv.

**4:47:56** · This CSV file I have that looks exactly like what we just saw. I'll type code MFA. CSV. And now I can indeed see I have an ID column, a title column, an accession number, and the date these pieces were acquired, all separated by commas. So let's say I want to quickly import this data into its very own database to run SQL queries on it. As it stands, I can't use SQL queries on this table because it's not inside of a SQLite database. But let me add one.

**4:48:29** · I'll type SQLite 3 MFA. DB to remake MFA down below. Let me now introduce this new command that is not a SQL keyword but is actually a SQL like command. And this command is called import.imp import lets you take a file like a CSV and automatically insert it row by row into a table of your own making or one that you can let SQLite create for you. Let's actually create the table ourselves and then insert this CSV using import.

**4:49:01** · So I'll go back to SQLite. Let me recreate this schema.

**4:49:08** · Right now there's no tables inside this database. But let me create one. I'll instead type read schema.sql to read in that old schema. SQL file. So I can have my own table here. I'll type that schema again. And now I see I have that table back. But if I type select star from collections semicolon, nothing is inside. Well, I could fix this. I could try to import this CSV into collections to insert all at once from this own from the CSV file we have right here.

**4:49:40** · So to do this, let me type.imp import. Now before I finish this off, there are a few arguments or options I can give to.imp import to make sure it works properly. The ones for this look as follows. I should type.imp import and then dash d-csv to say I'm importing a CSV. If I don't type dash d- CSV, SQLite might assume something about this file that just isn't true.

**4:50:10** · It should know that file that numbers are here separated by commas. Numbers or values, whatever's inside my table are separated by commas.

**4:50:19** · And then d- skip one. Well, let's take a look. If I go back to this file here, let's see. I have the first row, the second row, the third row, the fourth row. Are there any rows I probably shouldn't insert into my table here? Let me ask the audience. You're free to raise your hand. Are there any rows I shouldn't insert into this table?

**4:50:45** · Let's go to Sukana.

**4:50:46** · Yes, I think we shouldn't include the first row because it doesn't give us any value that we need.

**4:50:52** · Yeah, you're right. Right. So if I look at this header row as we call it, I see ID, title, accession number, and acquired the names for my columns. But notice in my schema, I already have those column names existing. So I shouldn't insert the value ID into my ID column. I want to just skip that row and only do the next one. So here by typing d- skip one, I'll skip that header row.

**4:51:18** · So let's try this now. I'll say.imp import- CSV. I'm going to import a CSV now. D-s skip. How many rows should I skip? Well, just one, the header row there. Now, I say the file to import. So, I'll type mfa.csv, the CSV file to import into my database.

**4:51:37** · Now, I type the name of the table I'm importing into, collections in this case. And notice how I no longer need to quote collections or quote MFA.CSV CSV because this is not a SQL statement. This is a SQL light statement. So I can get away with not quoting anything here.

**4:51:56** · Now I'll hit enter. And again, nothing seems to happen, but it's probably a good sign. Let me try selecting star from collections. Semicolon enter. And now all my data is just magically in there. It's went from my CSV into my very own table. Okay, so that's a pretty nice step forward. Like no longer do we have to use just single line inserts or even bulk inserts, those multi-line inserts.

**4:52:25** · We can now just import an entire table from a CSV. But I think I've been showing you a bit of a inaccuracy here, at least something that's not often going to happen to you. Like if I go back to this uh file here, the CSV, what you might notice is that I specified the primary key. I said ID of one, ID of two, ID of three.

**4:52:47** · But if we heard before, this might not be the best design because what if I import this CSV and there's already an item that has the ID of one or the ID of two. Ideally, I could let SQLite create its very own primary keys for each of these rows. And more often than not, you'll likely have a database or a CSV that looks a bit more like this without the primary key, but you'll still want to have a primary key when you import into your database.

**4:53:17** · So, let's try working with this kind of CSV now and having SQLite generate some of those primary keys for us. Come back to my computer and let's update our MFA.csv just to remove those primary key column here. So I will open up again MFA.CSV and let me try to just delete this column al together. I'll remove ID, remove one and two and three and four and five. Let me save it.

**4:53:46** · And now that ID column is gone but now there's a problem. Like if I go to my schema and I type dot schema, notice how there are four columns in this table. ID, title, accession number, and acquired. Well, now my CSV only has three columns. So, if I try to import this CSV into this table, I'm going to run into trouble because I have different numbers of columns between my CSV and my table.

**4:54:19** · What could I do instead? It turns out that I could actually import this data into a temporary table and then take that data and insert that data in that temporary table into my real one called collections. Here I can use both.imp import and insert into to accomplish that task for me. So let's try this. I'll say import I want to import a CSV now. D-csv.

**4:54:46** · Which one? Well, MFA.csv in this case. Now though, I want to create a brand new table that doesn't yet exist. So I'll type the name of the table. I might just call it temp for now to temporarily import this data into a brand new table. And notice how here I'm not using dash skip one because now I want to take advantage of those header rows. SQLite if I import into a new table.

**4:55:11** · Well, notice I have a header row and make my columns the very same names that are in my header row. title, accession number, and acquired. I don't want to skip them. I want SQLite to see them and create this table using those header rows. So now I'll hit enter.

**4:55:30** · Nothing seems to happen. But but if I type schema, what do I see? But a brand new table called temp that SQLite has just made automatically. And notice how it used that header row. I have title, accession number, and acquired as my column names.

**4:55:46** · Okay, let's now look inside the temp table. I'll say select star from temp semicolon. Oh, and now I see all the data in there, but I don't have primary keys yet. So, my goal is really to take all this data and insert it into my collections table to give it that primary key I've been wanting. Here, again, if I type select star from collections, uh, well, nothing. Oh, something is still there. Let me actually just delete this for demonstration.

**4:56:15** · I'll say delete from collections to remove it all together. We'll get that done in just a minute. And now let me try select star from collections. And I should see nothing inside of collections. So what could I do? I could insert into collections using the data from my temp table. So I'll try that. I'll say insert into collections and choose those columns yet again. I'll say the title and the accession number.

**4:56:46** · And now let's go for the acquired column as well. I'll hit enter. But instead of typing many new lines of values, I actually have a way to dynamically select all the values I want to insert.

**4:57:02** · And it looks a bit like this. I could say insert into some table and some columns of that table. But I want to insert the results of this select down below. So I'll select some columns from some separate table. And so long as these columns align, I'll be able to actually take the results of that select and insert all of them into this new table using insert into. So let me finish my statement here and we can see the results.

**4:57:31** · Come back to my computer and here I'll type a select to get back all the items from uh my temp table.

**4:57:39** · I'll say select in this case select um let's go for the title column the accession number column and the acquired column from my temp table. Now if I hit semicolon I should see well nothing at first but if I type select star from collections I see all my data now in there selected from my temporary table and now if I

**4:58:09** · type dots schema I still see temp but what can I do now I could just delete that table altogether I could say drop table temp as we saw last week semicolon hit enter dots schema again and Now we're back where we want to be with a single table. And now we've import our data from our CSV with primary keys. If I type collections here, we see it all in this table.

**4:58:36** · Okay. So we've seen several versions of import. One to import into an existing table and one to import into a brand new table. Let me ask then what questions we have on how to use import or how to insert more data into our database.

**4:58:55** · Let's go. Luis, can we ask the insert into command to uh place a column in a specific position?

**4:59:02** · Ah, good question. Can we ask insert into to place a column in a certain position? Um, there's a few ways of getting at what I think you're asking here. So, let me show you a few of those here. I'll come back to my computer and let me pull up the syntax for insert into again. I will choose this and I'll show it on the screen over here. So I'll say insert into some table given some columns. And notice how down below I actually have values to insert into those columns.

**4:59:32** · I could to your question rearrange these values. So I might have um this first value here is some value that goes into this column. This second column here is a value into that column and that would rearrange the values I insert into those columns. If you're asking though if I can reorder the columns that is up to create table and create table only. And in general I encourage you think not so much about an ordering of your columns because it could be in any order whatsoever. But you could just rearrange your selection of columns here to insert the data you want to insert.

**5:00:06** · Okay, let's take one more question here.

**5:00:09** · What happens if one of the rows you're trying to insert violates a constraint on the table?

**5:00:14** · Yeah, so here we're inserting multiple rows and if one actually violates some constraint, then we won't actually insert any of those rows. This is because this insert is bundled inside of a transaction which we'll learn more about later on in the course. Let's take another one.

**5:00:32** · I noticed that when you did select star from collections that one of the acquired dates was just blank. It didn't say no. Is that because the CSV itself just had an empty value next to the comma?

**5:00:43** · Yeah, great observation. So, let me try this again so we can see the results of this select. I'll come back to my computer here and let me show you again.

**5:00:52** · If I say select star from collections semicolon, notice how this acquired um col this acquired cell here, if I go back to my uh screen is just blank. But we saw before that if I selected star, I would have seen null there if this value was truly null. Well, it turns out one downside of importing from a CSV is that all of your data is imported initially as text. And if I have just a blank cell in my CSV, it won't be converted to null automatically.

**5:01:25** · I need to do that myself, perhaps using an update statement that we'll see in just a bit. So be wary of this. If you do want to keep track of null values and so on, if you don't actually manually make this value a null, it'll appear as just a blank value, not a null, which is different in this respect.

**5:01:44** · Okay, so here we've seen how to insert not just one row, but multiple and also how to import data from a CSV. When we come back, we'll see how to actually update our data altogether and even delete it too. So, we'll come back in just a few and talk about how to delete data from our tables. And we're back.

**5:02:04** · So, we just saw how to insert some rows into our database and also to import some data. But presumably, we also want to be able to delete some data from our table as well. You can imagine the MFA, the Museum of Fine Arts, maybe they're selling a piece of artwork or maybe they've lost one or maybe it was stolen.

**5:02:23** · But either way, they want to remove the row from their table. Well, let's see here. We could go back to our schema with a table of artifacts and artwork that is inside of the MFA. Now, if I want to delete a particular piece, you could visually think of it a bit like this. I could first identify that row I want to delete. Let's say it's spring outing here. We've sold this piece.

**5:02:47** · Well, I could visually just remove this row so it's no longer there and shift the remaining ones up metaphorically.

**5:02:54** · And it turns out that to do this in SQL, we have our very own statement we can use. This one reads delete from some table where a condition is true. So we see our old friend where back again and where is vitally important to this delete from. If I say delete from table with no where, what do you think is going to happen? We might drop everything from our table, right? But if I instead say where some condition is true, I can select the rows I want to delete and only delete those rows.

**5:03:27** · So let's try this here. I'll try to delete some artwork from our collections table. For example, maybe we've sold it and we want to get rid of it. I'll come back to my computer over here and I will open up our SQLite database. I'll say SQLite 3 mfa.db.

**5:03:46** · And now I can type select star from collections. And I see a few more items than last time now all inside of our table. But per the visual, I want to delete spring outing to remove it from this table. So what could I do? I could try delete from and then the table I want to delete from. In this case, I'll use the let's say collections name delete from collections. But I don't want to do this.

**5:04:14** · I don't want to say delete from collections semicolon end of statement because then all delete every row. What I should instead do is this delete from collections where some condition is true. Maybe the title in this case is a title I'm trying to remove. So I'll say title equals spring outing just like this. Semicolon enter.

**5:04:40** · Now nothing seems to happen. But if I do select star from collections semicolon, we no longer see spring outing. And notice here how the ID column, the ID of three is now gone. If I were to insert some new row here, I would start over with the highest number, which is seven in this case, going from seven to eight.

**5:05:02** · But three is no longer part of our database. Let me try this again. Notice how this one called imaginative landscape, the acquired date is null. We don't know when we got it. Well, let's say that we eventually sell it. It's no longer part of our database. We could use a condition based on null to remove this particular artwork. So, I'll say this. Let me try to delete from collections where title equals not spring outing, but uh where the acquired date, sorry, the acquired date is null semicolon.

**5:05:32** · I could also use is not null where acquired is not null, but that would delete all the pieces of artwork that actually have an acquired date. Here I want to delete only those that do not have an acquired date. So I'll say where acquired is null. Now I'll hit enter.

**5:05:54** · Nothing seems to happen, but I'll say select star from collections semicolon. And I'll see that that piece of artwork is now gone. I only have those that have an acquired date. Okay. So, similar to insert, we've been able to delete one row at a time, but it would probably be helpful for us to delete multiple rows at a time as well. Let's look again at our table. Here we have our artwork as it currently stands.

**5:06:27** · And maybe let's say we want to delete those pieces that we acquired before 1909. Uh here in Boston, the MFA actually moved locations in 1909 to a new place still in Boston, but a brand new building altogether. So let's say that perhaps they left some items at their old location. They're no longer part of their collections. via what condition do you think could I select these three rows for my delete from?

**5:06:56** · What could I put in my condition to delete these three rows? Let me ask the audience here. What might you propose for delete from here? Delete those three particular rows. Let's go to shiv greater than five. ID equals than five.

**5:07:18** · That's a good observations. We could look at our table here. We see the ID could be greater than or equal to five. That would remove these three rows.

**5:07:27** · Certainly, there's probably another way to do this, too. Any other ideas besides the ID? What else could we use?

**5:07:41** · Let's go to Yoshvi. Uh so we could compare the dates and use greater than or less than sign with the acquired dates.

**5:07:50** · Ah so you're proposing to use the date column too. That makes sense to me as well. We could see acquired here. Perhaps we could see is the acquired value less than 1909 that year that we move locations. We could also probably use the title, the accession number, and so on. And each has their own tradeoffs.

**5:08:09** · Remember though, for this particular query, which is deleting those items that were part of the museum, acquired before 1909, probably best to use the acquired date to actually delete those rows. What if, for instance, our IDs are actually not like this, but they're kind of interspersed around. I couldn't really do a query like if the ID is greater than equal to five because I could also include those that were maybe acquired 1911 1956 and so on. Probably ideal for me to use this date if it's the date that I ultimately care about.

**5:08:44** · So let's try this. I'll go back to my environment and I'll try to delete these three particular rows. I'll try delete from collections as we saw before. But now here comes my condition. I'll say where the acquired column is less than some date that I'll give. And here I'll give 1909 January 1st. It turns out that SQLite has a few ways to represent dates.

**5:09:12** · One of which is this format that follows the YY or the year four digits and then dash and then MM or the month with two digits and then dash again dd in this case the day in two digits. So 1909-01-01 means January 1st, 1909. And I can use these same operators with dates. I could say greater than or less than or equal to this particular date.

**5:09:43** · And SQLite will be able to parse this for me to understand what I mean, which is earlier than 1909. So let's try this. Then I'll hit enter and nothing seems to happen. But if I do select star from collections, I now see I'm down to two paintings, two pieces of artwork that were required only after 1909.

**5:10:07** · Okay. So given this uh part on delete, we're able to delete one row or even multiple rows at a time, but there are still instances where we might want to think about should we delete something or can we delete something. We'll talk about those in just a minute in terms of constraints.

**5:10:27** · Be back in a few. And we're back. So, we just saw how to delete one row, even multiple rows. We haven't yet talked about whether we should delete some data or whether we should delete some data.

**5:10:40** · And particularly in the context of these constraints where you might have maybe a piece of data you actually shouldn't delete to maintain the integrity of your table. Now, one example of this is a foreign key constraint, which means that you have some table with a primary key that is referenced by some other table.

**5:11:00** · And we'll get concrete about this just a minute, but it might mean that if you were to delete that primary key, that other table would have nothing to reference. So, let's update our schema here for the MFA, the Museum of Fine Arts, and let's say that they have not just a collection now, but also artists involved. And there exists a many to many relationship among artists and items in the collection. We could say that an artist might make more than one piece of art in the collection. And a piece of art might be created by more than one artist.

**5:11:32** · Now, concretely in our database, this might look as follows. I could have a table for artists and a table for collections. And notice how each has their own primary key. Artist has an ID column called our primary key column. Collections too has an ID called our primary key column. Here now in the middle is this table created that symbolizes that represents the relationship among artists and items in the collection.

**5:12:02** · Here on the first row we see the artist ID of one created the piece of art with the collection ID of two. So who did what here? Well, we can see that the artist with the ID of one is Lee Yin. Lee Yin created this piece of art with the ID of two, which is imaginative landscape. So, we can kind of relate in this case artists with collections as we saw just a few weeks ago. But let's say we decide to delete a particular artist.

**5:12:32** · Maybe we delete unidentified artists down here. Well, we could just delete from the artist table.

**5:12:40** · Maybe we find a condition to select this row and we delete from artists. We'll do that here. Remove that row. But what have we done wrong? If we look at our created table in particular, what have we now done wrong? What kind of problem might we run into?

**5:13:04** · Let's go to Kareem. The third row with ID three was only deleted from the artist table without the other table.

**5:13:13** · Yeah, good point. We only deleted the uh artist with the ID of three from the artist's table. Now, if I look at the created table and I look for the artist with ID of three, well, do you see them?

**5:13:26** · I don't exist anymore. So, I can't understand this relationship. I don't know the artist with the ID of three. So let's try this now with a new kind of schema now in our database. I'll go back to my computer and let me open up our new version of our database. I'll type SQLite 3 in this case uh MFA. DB same name but now different schema. If I type dot schema, notice a few things here. I have those same tables we saw visually.

**5:14:01** · I have collections, artists and a created table. Let me focus in particular on this created table. If I say do schema in this case created enter, I'll see I have a foreign key constraint on my artist ID column and my collection ID column. So if I tried to delete an artist that is referenced in my created table, I would probably raise a constraint error, a foreign key constraint error.

**5:14:33** · So let's just try this and see what happens. Let me try delete from the artist table. Delete from artists where let's say the name of that artist is literally unidentified artist. This is the name they have in the Museum of Fine Arts collections.

**5:14:55** · Unidentified artist. So now I want to delete them from that table. Well, if I hit enter, I do get that foreign key constraint error. So, does this mean I just can't delete this artist? Or is there a workaround? Let's look at it visually again. I'll go back to what we had before as our table. And let me ask the audience here, what's the solution?

**5:15:21** · Like, if I can't delete unidentified artist because they have an ID referenced by this table. What should I maybe do first? What should I do instead? Yeah, I want to say that first we can delete the ID that is being referenced by this ID that we want to delete. Then we can delete it. In fact, if we want to delete from the artist, first we have to delete from the created table or to other table which it is referencing, then we can delete from the artist table.

**5:15:50** · Yeah, I like your I like your thinking here. So if we look at the created table, you notice that we can't delete unidentified artist because it's referenced in the created table. What we should maybe first do is delete this row, delete their affiliation with their work and then delete the artist so we don't run into this foreign key constraint. So let's try this in our SQLite environment. Come back to that computer and again our plan was to first delete the artist's affiliation with their work from the created table.

**5:16:21** · So let me show you first the created table. I'll say select select star from created and see how it's exactly like the table we just visualized. Now let me try to delete this artist affiliation with their work. I'm not deleting the artist.

**5:16:40** · I'm deleting their affiliation with their authorship, their artistship, whatever you want to call it for their work. Now I'll say delete delete from let's say delete from artists where the artist ID is equal to or equals three.

**5:17:02** · Well I could do this but there's probably a better way. Like I know the ID and that's fine but we could also use what we saw a little bit ago which were sub queries. a way to write a query that returns me the result and that result gets included in another query altogether. So let's try that instead. Let's say I don't know the artist ID.

**5:17:23** · What I could do is make a sub query. I could say inside of this let me select the ID from oh the artist's table where in this case the name equals unidentified artist. And then let me close out this query. hit a semicolon. And I already see a typo in this, but I'm just going to try it anyway. I will go ahead and hit enter. And let's see if I type select star from artists. Enter. I still see unidentified artists.

**5:17:56** · And I think my typo here was as follows. If I look up my query using the up arrow on my keyboard, I see delete from artists where the artist ID equals some value here. But do I want delete from artists?

**5:18:11** · I don't I actually can't delete from artists. What I should do instead is delete from the created table. So, let's try this. I'll say delete from created making sure I only have double quotes around created. Then I'll say where the artist ID equals let's say either three, but it could also be the result of this subquery.

**5:18:32** · I'll say 1 2 3 4 and then select the ID from the artists from the artist table where the name equals unidentified artist then I'll close this sub query hitting semicolon hit enter and now if I say select star from created semicolon I should see that this artist's affiliation with their work no longer exists. artists.

**5:19:02** · And because it no longer exists, I can now delete them from the artist table. I don't have this foreign key, artist ID, referencing the primary key of this artist. So, let's now try that. I could say select star from artists. I see that unidentified artist is still in here, but let's delete them now. I'll say delete from let's say artists where the name equals unidentified artist. Closing my quotes, semicolon, hit enter.

**5:19:34** · And now if I select star from artists, semicolon, I should see they're no longer in this table to our earlier example. This becomes a two-step process. First, delete their affiliation, then delete their name.

**5:19:51** · Okay, so let's try this yet again, but now using some additional uh tools that we have at our disposal. So let's look back at this foreign key constraint that existed in this table. If you remember, it looked a bit like this. In my created table, I had this line foreign key.

**5:20:15** · Artist ID references the ID column in artists. Well, if that is the case, I can't delete the artist with the ID referenced by this foreign key. But it turns out that I could specify some alternative action that happens when I try to delete the ID that is referenced by this foreign key. I can specify that using a keyword called ondee.

**5:20:44** · So after foreign key reference artist ID, I could say afterwards ondee and then specify some action I want to actually happen when I try to delete the primary key referenced by this foreign key. One thing I could use would be restrict, which is kind of like what we saw before. If I try to delete a primary key that is referenced by this foreign key, I will not be allowed to do it. That action is restricted.

**5:21:11** · I could also decide to take no action.

**5:21:15** · In this case, I could delete the primary key referenced by this foreign key and nothing would happen. I would actually be allowed to do that, which may be unwise in some cases, but I could give myself that power. I could also decide to set null. That is, if I delete the primary key that is referenced by this foreign key, what I'll do is set the foreign key to be null, meaning that value no longer exists.

**5:21:42** · I could alternatively set it to a default value for that column. Or perhaps most compellingly, I could try to cascade the deletion. Where cascade means if I delete the artist, for instance, let's also delete their affiliation with their artwork all in one go. This converts our two-step process into a onestep process.

**5:22:08** · So let's visualize this. Let's say we have now applied this constraint ondee cascade. So if I delete the artist, I'll also delete their affiliation with their work. We'll have the same two tables, artists, collections, and created. Now again, artist ID references this primary key in artists. Now I'm going to try I want to delete unidentified artist here.

**5:22:35** · Well, I could do that. I could just delete their row. And now instead of a foreign key constrainted error, what I get is the following. I see and created that this row is also gone. The row that had the artist ID of three gets removed. We've cascaded the deletion onward to the created table. So let's try this now with a new database schema. I'll go back to my computer here.

**5:23:06** · So I'm back at in my terminal here and I can type SQLite 3 MFA. DB to reopen this database. And notice how if I type dots schema, I've updated this schema to now have ondelete cascade. Let me show you over here on the screen here on the created table, I now have the very same kind of table schema, but now my only difference is I've applied this ondee action to my foreign key constraints. In particular, I'm going to cascade the delete from the artist's table to the created table.

**5:23:37** · So let's try that out in SQLite. I'll come back over here and I will now try just delete from the artists table where the name equals unidentified artist. Unidentified artist semicolon.

**5:23:54** · Now I'll hit enter and I don't get a foreign key constraint anymore. But if I say select star from created semicolon, notice how I've also deleted the artist's affiliation with their work. So that is wherever in the artist ID column I saw the ID for the artist I deleted, I would too delete that row. So I have no references to that primary key which is now gone from my table.

**5:24:23** · So let me ask here we've seen how to delete single rows, how to delete multiple rows and now how to delete data among some constraints like our foreign key constraints. What questions do we have on those techniques?

**5:24:43** · Let's go to Han.

**5:24:44** · I have a question regarding deleting. Um since the uh the ID numbers have been um removed while we removing the record I was wondering if do we have to clean it up somehow later or will they be populated with the new data as it comes along?

**5:25:00** · Yeah

**5:25:00** · great question. So the question is what happens to our primary keys when we delete our data. So for this one let me show you the visual again that we had before of our tables nicely printed on the on the slide. So I'll come back here and I will go back to our idea of these um joint tables where we had an artists table, a collections table and a created table. And we saw before that we're going to delete this artist called unidentified artist. So I'll delete them. And to your point, well the ID of three no longer exists in this case.

**5:25:32** · Now by default at least in SQL light if I insert a new row what I'll do is take the highest ID value and I will then make that the new primary key for the new row that I insert. That is the default situation.

**5:25:51** · I could if I wanted to get more specific and if I had done in my um ID integer col my ID integer column here in my create table if I had also said this keyword called auto increment all one word what would happen instead is I would actually reinsert an

**5:26:14** · ID that is not used so in this case three is not used I could insert that one here so up to you what you want to do in general General SQLite by default will take the highest ID, add one from there. If you specify this constraint called auto increment, you will instead take whatever ID is not being used and use that in your insert afterwards.

**5:26:38** · Okay, so now we've seen how to insert and how to delete data. But of course, we make mistakes when we add data or even when we delete data. So, we'll see in just a minute how to update our values as well to correct typos and even to update associations between artists and artwork.

**5:26:57** · And we're back. So, we've so far seen how to insert some data into our tables and how to delete it. But sometimes we don't want to fully delete something. We just want to change its value to correct some typo or correct some association.

**5:27:12** · So let's think to our MFA example where the Museum of Fine Arts has some tables that look like this. They have artists in their collection and they also have artwork in their collection. They also have a created table to associate artists with their artwork. Now in this case we know that I have this unidentified artist and we can see that they authored this item in the collections farmers working at Dawn. But let's say that later on we find out it wasn't an unidentified artist.

**5:27:45** · It was instead Lee Yin who created Farmers Working at Dawn. How could we update our tables to make sure it's Lee Yin who we have creating Farmers Working at Dawn?

**5:28:02** · So uh what we could do is like uh we know that in created we have our artist ID and the collection ID. So we could update it there but somehow we need to cascade it over to the artists table because now this unidentified artist row I think we probably don't need it.

**5:28:25** · Yeah.

**5:28:25** · Yeah. So, a good point here where we could actually probably change the created table to reassociate an artist with some new artwork here. So, let's visualize this. I go to my created table and here the artist ID is currently three, but I want it really to be one. I want Lee Yin to be associated with this piece called Farmers Working at Dawn. So, I could update the created table to instead of having three here, have one.

**5:28:53** · Now we see Lee Yin created Farmers Working at Dawn. And to your concern about this unidentified artist here, I think it's okay to have an artist in our table who may or may not have an item in collections. We'll say that's okay, at least for now. So if we can update our associations between artists and collections like this, let's actually try to do that in our very own database here. I'll go back to my SQLite environment. And now let me try to uh open it. First I'll do SQLite 3 MFA. DB.

**5:29:27** · And now let me type dots schema to show you I have the very same schema from before. So I want to update the artist association between Lee Yin and farmers working at dawn. So let's say I'll select star from created like this.

**5:29:42** · Semicolon. Here I have my artist ids and my collection IDs. I see that we have the unidentified artist ID of three creating uh farmers working at dawn with the ID of one our collection here. So now let's try to update the artist who created this particular painting here. I have three associated with one but I want one associated with one where one is the ID for Lee Yin and one my collection ID is the ID for this artwork here. So let me try this.

**5:30:14** · I'll say update created and set let's say artist ID equal to some particular value. Well, what value should I set it to? I could try to set it to Lein's ID, which we know is just one. But let me try instead to use a sub query here. Let me try to say parenthesis and then write some query to update this value. I'll say select ID from artists like this. Enter again where the name equals Lee Yin.

**5:30:46** · And then let me close this sub query. Well, if I try to run this query, what might happen? I'm updating the created table. I'm setting the artist ID equal to the ID for Lee Yin. But what I've forgotten is this where to only choose some rows to update. So let me not close it yet.

**5:31:15** · I'll instead say where in this case the collection ID the piece of artwork in our collection is equal to well the ID for this painting. I'll say select ID from collections and then I'll say where the title equals farmers working at dawn. Now I'll close this subquery and hit semicolon. And here we've seen our first example of an update query.

**5:31:43** · I'm trying to update the artist ID column in created to be the ID for Lee Yin. I only want to do that though on the row where collection ID is equal to the ID for this particular painting we want to change the attribution for.

**5:32:00** · So now I'll hit enter and if I select star from created I should hopefully see in this case that the artist ID associated with this painting is two and also down below here is one as well. So I have Lein associated with now two paintings overall. So let's get a grasp on what this update uh syntax really looks like in general. And for that let's show this slide here.

**5:32:30** · We have this update keyword update statement in SQL to take uh a table name and update the columns inside of it. I say update then the name of the table I want to update. Then I say set some column equal to some value. I could if I wanted to have more than one column here. I could say maybe title and even um maybe if we're talking about authors, authors over here or even acquired date.

**5:32:59** · I could update more than one column in my set portion here. Then comes this where portion where some condition is true. I want to make sure I don't update all of my rows. I only update those where some condition is actually true.

**5:33:16** · So this is your syntax for updating some columns. Let's say if you want to change an artist attribution or if you want to change a typo you've made. So let's see this now not just in terms of changing artists and their attributions. Let's see a use case for update. we've made some mistakes in our data and let's say the museum decides to host some kind of um event where people vote on their favorite piece of artwork. They kind of handwrite or type it into some online form.

**5:33:46** · Well, we might get back a CSV of those responses, some commaepparated values, one line for each vote from our people who've attended this convention. Let's go back over here and I'll show you that CSV. Let me go to my environment and I'll type code MFA.csv to open this CSV that I already have. And here actually it's not called MFA.csv, it's called code votes.csv.

**5:34:14** · And now here we can see I have a table of one column that has several votes inside of it. Let's see we have maybe 20 votes to be exact. So the first row is the header row. I have in this CSV one column called title and each line here is one vote for a museum goer's favorite piece of artwork. We see farmers working at dawn. We see imaginative landscape profusion of flowers and our goal is to count up these votes to see which is the most popular.

**5:34:45** · Well, let's try using import again to actually turn this CSV into our very own SQLite database. Let me go back to my terminal and I'll type SQLite 3 votes.db to create a votes database. I'll hit enter. And now I can use import. I could say import a CSV called votes.csv into a table also called votes. I'll hit enter now.

**5:35:14** · And now if I select star from votes semicolon, I'll see all of my votes now in a single table. So, I want to tally these votes. We could do that using a technique we learned back in the week on querying and relating. What if I wanted to group by my titles and count up those groups? I could do that. I could say select, let's say, title and also the count of title. Let me count up the votes for each title from, in this case, my votes table like this.

**5:35:50** · Now I want to count not just each vote individually but I want to group them. I want to count group votes by group where that group is in this case the title itself. So let me try running this query and hitting enter. Well I'll see I've started to count some votes like I have imaginative landscape here. Spring outing farmers working at dawn. Spring outing down below here too.

**5:36:17** · But I seem to be missing something. Like I shouldn't have this many groups. I should only have four groups. Why do I have so many? Well, it seems like there's some typos here. What typos do you see? Feel free to raise your hand.

**5:36:32** · So, uh I think that it is title is uh when you count it is uh case sensitive. So maybe it is counting one by one.

**5:36:41** · Yeah, a good idea. So maybe it's case sensitive our group by is. And you'd be correct if you said that group by is in this case sensitive. So if we see here we see farmers working at dawn all capitalized at least the farmers working and dawn capitalized. Well that won't be part of the same group as uh let's say farmers working at dawn all cap properly capitalized in this case with lowercase working and lowercase dawn as it is in the MFA collections. So we could probably fix some capitalization here.

**5:37:13** · What other things could we fix? Let's hear from one more person. Let's go to Laurens.

**5:37:18** · The uh the count on each typo.

**5:37:22** · There are some typos in here.

**5:37:23** · Absolutely. So, if I look at some of these, I see uh not farmers but famers working at dawn. Um I might see instead of imaginative landscape, I just see imaginative landscape. So, definitely some typos in here to fix as well. So, let's start working on using our update tool, our update keyword to fix some of this data, to clean it up, so to speak, so we can count up our votes for these artworks. Come back to my terminal. And now, let's try updating to at least remove some of this white space here.

**5:37:56** · Like, you might notice that imaginative landscape has a space before it. And so does spring outing here. That space counts as part of the title and I want to remove it. So, what could I do? I could try using a function in SQLite, one called trim. Trim takes a string and just removes leading and trailing whites space, giving back only the characters in the middle. So, let me try that. I'll say update votes my table here and set the title column equal to what?

**5:38:26** · Well, the trimmed version of title. Trim looks like this. trim and then some parenthesis to say the input to this function. I'll give it the title column.

**5:38:42** · Now I'll hit semicolon and this query will run as follows. It will update the votes table and inside the votes table set the title column equal to the trimmed version of whatever values are inside that column. Trimming here means remove trailing and leading whites space. I don't need to apply any condition. I don't need to say say where dot dot dot because I want to apply to all rows in my data set. Now I'll hit enter and let me try running this again.

**5:39:13** · I'll say up arrow to get back my old query. Now I'll try counting again and I think we're making some progress. Like I can see that I've removed removed quote unquote those um titles that had leading or trailing whites space. They're now part of a group because their titles now match those groups. Let's keep going. We noticed before we had some capitalization issues. So, let's fix those as well. I can go back to my terminal and we could introduce this other function, one called upper.

**5:39:42** · Upper converts a string like farmers working at dawn to be all in uppercase kind of shouted out. And that's useful for us here because we could kind of force everything to uppercase thereby removing any inconsistencies in capitalization.

**5:39:59** · So, let me try that. I'll say update again the votes table and this time I'll set title equal to the uppercase version of title. So upper here is a function in SQLite that takes some values associated with a column and uppercases the entire thing to remove any consistencies and capitalization. Again no condition here because I want to apply this to all rows. I'll hit enter.

**5:40:26** · And now if I select select star from collections semicolon oops select star from votes in this case no longer a collections table. I'll say select star from votes semicolon. I should see all of my titles capitalized. But now I want to group by.

**5:40:45** · So let's try this. I'll go up arrow to get back to my old query that grouped by title. Hit enter. And now we're still making some more progress. I'm reducing my number of groups until I get to four.

**5:40:58** · But there's still some typos like we see famers working at dawn or farmers working or farmser working at dawn. We want these to be included as part of this group. Farmers working at dawn. So we should fix some of these typos here. Let me go back to my terminal and let's try this out. I could in this case just manually correct these. Like you could imagine me doing something like this.

**5:41:23** · update votes and set the title equal to all caps farmers working at dawn. Now including a condition where the title presently is is equal to far famers

**5:41:39** · working like this semicolon or not famous work uh I think it's farmers working just all in two words that was one title we saw I could manually update it a bit like this let me hit enter and let me do the same query by hitting the up arrow on my keyboard me find this one hit enter and now we can see that that title Farmers working is now just part of the main group farmers working at dawn. I could keep going here.

**5:42:08** · I could try to convert famers working at dawn to farmers working at dawn. Let me try it. I could say select let's say um not select let me update let me update in this case votes and set title equal to farmers working at dawn where the title equals

**5:42:29** · in this case famers working at dawn semicolon enter let me hit up arrow to go back to my old query to group by and now we're getting somewhere I'm seeing now only two groups for farmers working at dawn on but one more to fix. Now, we'd be here for a while if I spend all this time like one by one fixing these typos. So, there's probably a better way. There is. This one's going to be using the like keyword. We don't have to say equal so much.

**5:43:01** · We can just say like now I could try to match any title that looks like Farmers Working at Dawn and update it to be the correct title. So, let's try that here. I could now try update votes and set title equal to farmers working at dawn. Farmers working at dawn where the title is like where the title is like some pattern I could give.

**5:43:33** · Now for this data set it turns out that the only artwork that begins with FA is farmers working at dawn. So to match any title with FA and then anything afterwards, I could use FA percent and then close out that pattern. Notice how I don't have to have consistent capitalization like is case insensitive. And notice how too the percent matches anything that comes after FA.

**5:44:04** · Now in this data set, this is okay. But in a larger data set, you'd probably want to avoid this kind of query because you could match much more than farmers working at dawn. You'd match anything that begins with FA. So be careful with this and think through what pattern should you use to fix up your titles.

**5:44:24** · Let me just hit enter here. And now let me try hitting up arrow again to show you the result. And now we're in a pretty good place. I see all of my titles like farmers working at dawn are correctly capitalized, consistently spelled, and all in one place.

**5:44:42** · Okay, let's try the others here. I also have imaginative landscape which could be a little bit better designed here, a little bit better grouped as well by fixing some of these typos. Well, here I could try to match on to maybe imaginative. That seems like a long enough word that it could be useful for me here. So I'll say something like select not select I'll do update votes and set the title equal to imaginative landscape.

**5:45:11** · Now I want to match any rows that have a title like imaginative space percent end quote semicolon. Now I'll match any title that has imaginative as a full word at the very beginning of this phrase. This is I would say a better query than FA because FA could match much more than this painting name here.

**5:45:36** · If we have only one painting that begins with imaginative, this could work for us now. So I'll try this. I'll say enter.

**5:45:44** · And now let me rerun the query group by. And we're so close. There's still one more imaginative landscape. So for this one, I might just need to manually update that piece. I could say let's do update votes and set title equal to in this case imaginative landscape where of course the title currently is imaginative landscape without the a in there. Now I'll hit semicolon to run this query. I'll show you the results.

**5:46:15** · And now I think we're really almost there. There's only one more to do. Profusion of flowers. Let's fix that one. Now I could say select votes not not select update I'm always updating here update votes and then we want to set the title column to be equal to profusion profusion of flowers like this then

**5:46:42** · where the title is like in this case profusion at the beginning notice how I can't use profusion space and then percent afterwards because we have one title that is literally just profusion plain and simple. No spaces afterwards, no spaces at the beginning. To match that, I should just say profusion at the beginning. Now I can hit enter. And if I do my usual query to show you the group, the votes group by title, I see I'm finally at my correctly formatted data set.

**5:47:13** · Farmers working at dawn has six votes. Imaginative landscape has five and so on down the row. So here we've seen update being used not just to associate artists with new paintings but also to clean our data to make sure we can actually tally votes up in a way that's consistent and clean in this case. What questions do we have on update? Now let's go to Vixay.

**5:47:42** · Yes.

**5:47:42** · So uh what I wanted to ask is if there is a specific function for like lower case. So there's a there's a function for upper and there are the one for like all lowercase.

**5:47:52** · Yeah, a good corresponding question here. We used upper, but is there lower?

**5:47:56** · Turns out there is a lower function.

**5:47:57** · It's spelled um L O W E R and is an all lower case like upper was. So I could use that as well. There is a whole list of what SQLite calls these scalar functions. Functions that take in some set of values and return to you some modified version of those values. So if you do some googling look for SQLite scalar functions you can find all those functions in one place in the SQLite documentation.

**5:48:22** · Let's take one more question here. Let's go to Rupender.

**5:48:25** · So yeah my question is so instead of updating all the titles is it possible to create a new column with the four categories that we want to have actually.

**5:48:37** · Yeah

**5:48:37** · I could see that working too. So there's a few ways to fix this data. You could for imagine adding a new column and maybe you assign values to the rows in that column based on what you see in the um title that they've given you. So if you can match something like imaginative and you'd know that all your paintings associated with imaginative have the same title, you could group them into the one category, the two category and so on.

**5:49:02** · Um here you wouldn't be modifying those titles. you just be trying to strategically apply different categories which could also work as a solution here too. So good thinking.

**5:49:14** · Okay, so we've seen now how to insert data, how to update data and previously how to delete data. What we can still do though are learn how to have other SQL uh command other SQL statements that can run after we make our very own SQL statements as well. We'll come back and talk about these things called triggers.

**5:49:36** · And we're back. So, we've seen now a whole collection of ways to write data to a database. We've seen how to insert data, how to update data, and even delete data. What we'll see now, though, is this idea of a trigger, a way of writing a SQL statement to run in response to some other SQL statement like an insert, an update, or a delete.

**5:50:00** · Let's consider our museum yet again. And let's say they have a schema a bit like this one. Now they have items in their collections, but they also have a transactions table. Now, wouldn't it be nice if whenever I deleted something from the collections table, it would show up in transactions as sold, having been sold from the museum's collections.

**5:50:25** · Well, I could use a trigger to do just that. Let's see it visually first though. I'll say let's try to delete spring outing from our collections table. Well, if I do that, I could pretty easily do it with delete from.

**5:50:39** · Right now, it's no longer part of my database. But if I have created a trigger to run and insert whenever I hear or have listened to a a delete on my collections table, I could then see that same title in my transactions table as sold all automatically.

**5:51:00** · Let's think too maybe the museum acquires some piece of artwork. Maybe they actually add something new to their collection. We want that to show up in our transactions as well with the action of bought. Well, let's try it. I could probably add a new row here. I could say let's add pianies and butterfly to my collection here.

**5:51:19** · Now, if I have the appropriate trigger, I could run an insert into on transactions automatically that would insert this same title with the action of bought, thereby keeping a log of all of our sold pieces of artwork and all of our bought pieces of artwork. Now, to create what we're calling a trigger here, we can use the following syntax. I could say first create trigger and then some name.

**5:51:46** · So I tend to give triggers names to identify them among all of my database schemata like my tables and so on. Here after I say create trigger I have to specify should this trigger this statement run after or before some other SQL statement. Let's keep going with before here. Maybe it runs before an insert on some table. That's fine.

**5:52:13** · It could also run before an update of a column on some table. It could even run before a delete on some table. And then keep in mind this could be before or after any of these kinds of SQL statements. In this case we have insert, update and delete.

**5:52:35** · Now after we say this, we should say too is for each row. for each row means that if I were to maybe delete multiple rows, I should run my SQL statement for each row that I delete. If I delete two rows, I should run this statement coming soon two times. Okay, so now we've set up our trigger, at least kind of the data, the the the setup for it here.

**5:53:00** · What we haven't done yet is specified what statement should run whenever we see a delete on particular table. Well, let's try this here. I could say begin. Begin means here comes my statement I want to run whenever I hear a delete on this table. Now I'll write that query down below that statement inside my begin.

**5:53:25** · And I'll finish it off with an end to say this is the end of my statement. And my entire trigger looks like all of this lines of code here to say listen for a delete and run this statement in here for each row that I delete or update or insert.

**5:53:42** · So let's try actually implementing in this case the museum's collections where they're trying to sell or buy pieces of artwork and automatically add them to their transaction table whenever they create or delete some piece of data from their collections. go back to my terminal here. Let me pull up a database. I'll do SQLite 3 MFA. DB. And you'll notice that this is the same schema that we've had before. We have collections, artists, and the created table. What's missing here though is our transactions table.

**5:54:15** · So, let me make that for us here. I'll say let me go create table transactions. And now let me give it an ID column of type integer.

**5:54:28** · Now I'll also give it a title column as we saw before called text. It's in this column I'll store the title of the piece we either bought or sold. Now let me also include the action column also of type text to say whether we bought or sold this piece. Okay. Finally, I'll make the ID column my primary key. And if I say semicolon here and hit enter, I now have created this table.

**5:54:56** · So if I say dots schema, notice how I can now see my transactions table down below and I'm safe to run insert on this table to add some data to it. Well, let's try now creating our very first trigger. We're going to try to create a trigger that whenever an item is deleted from our collections table, we actually add it to our transactions table with the action of sold, meaning we sold this particular item.

**5:55:24** · So let me say create trigger as we saw before and give it some name to identify it. I'll call this one sell.

**5:55:33** · Now I'll say I want to run this trigger before I delete on the collections table. So before I run the delete query on my collections table, I want to run this statement instead. I'll say for each row begin, I want to now give you some statement to run for each row that I delete from collections. Let's make it this query here.

**5:55:59** · I'll do one, two, three, four spaces to indent and make sure this is clearly the query I want to run after I uh run the delete on collections. I'll say I want to insert into transactions and I want to insert into the title and action columns. What value should I insert? Well, I should insert the old title. And actually in triggers, you get access to this keyword called old. This is the title that we've just deleted from our collection.

**5:56:31** · So, old.title gives me access to the old row, the row we deleted, it's title column in particular. Now, let me add in the action which is just plain and simple sold. So, this is the query to run before I delete on collections. I will take the title of the row I'm about to delete and insert it into transactions along with the action sold. Let me type a semicolon here to say this is my entire query. Hit enter again.

**5:57:00** · And now I can end that particular statement I want to run after I hear a delete on collections. So I'll hit enter now and let me type dot schema. I can actually see this trigger is part of my schema. I can see create trigger cell before delete on transactions underneath the transactions table. Okay, let's try putting this into action here. Let me try actually deleting something from our collections table.

**5:57:31** · I'll say delete from collections where the title equals profusion of flowers. I want to sell this particular piece of artwork from our collection. I'll hit semicolon here. And now nothing seems to happen as usual. But if I select star from collections from collections, I see that piece is gone. It's no longer in here. And if I select star from transactions, select star from transactions, I actually see it's been sold.

**5:58:02** · So automatically I added profusion of flowers with the action of sold to my transactions table. I did not type insert myself. I instead created a trigger to run this statement. Insert into whenever I deleted on collections.

**5:58:21** · Let's try one more. We want to not to be able to sell artwork but also add it to our collection by buying it. So I could create a trigger called buy. Let me type create trigger buy. And now I want to run this statement forthcoming after an insert on collections. So I want to first insert a new item to collections. And when I do after I do I want to run this query coming next.

**5:58:52** · Now I want to for each row begin the statement I want to run. So as we said before I want to insert into the transactions table. I want to insert into the title and action columns just like this. Now I want to insert some values. The values I want to insert well I want to insert the new title the new row I've just added. So in addition to old we also have new when I'm top when I'm using a trigger on an insert.

**5:59:23** · So I'll say new.title title where again new is the new row or rows I'm inserting and thetitle is their column is a column called title. Now here I'll say the action was bought. We bought this artwork. I'll hit semicolon here and now I'll say end to say this is the end of my statement I want to run for every row I insert on collections. Let me hit enter here. I've created this trigger.

**5:59:51** · I can type schema to see it in my actual schema. Now let's try inserting. I'll say insert into collections. I want to insert into the title and accession number as well as the acquired columns. Here I want to insert some new artwork. Maybe I sold profusion of flowers but now I want to just buy it back. So I'll say I'll insert profusion. Profusion of flowers is the title. The accession number was 56.257.

**6:00:27** · And the date we acquired it, well, that was in 1956412. Let's hit semicolon here. Now I'll insert and I'll say select star from collections.

**6:00:40** · I should see profusion of flowers back in my table. Now though, if I say select star from transactions, select star from transactions, I should see I previously sold provision of flowers and later bought it back. So again, I didn't run this insert myself. I instead triggered it by making my very own insert on the collections table. So this is the power of triggers to be able to run statements that I myself didn't create in response to statements that I actually did.

**6:01:12** · So let me ask here what questions do we have on these triggers and what they can do for us?

**6:01:23** · Let's go to Simon. I'd like to know um uh if uh there are only there is only one SQL query that uh that you can write in trigger or multiple queries.

**6:01:38** · Yeah.

**6:01:38** · So we saw begin and end in our triggers here where begin indicates the start of our statement and end indicates the end. You actually can have multiple statements inside of the begin and end separated by of course that usual semicolon that we have.

**6:01:55** · Okay. So, one final idea here that we're getting at, we're kind of touching out with this transactions table is this idea of having a soft deletion. So, when I dropped something from my collections table, it actually ended up in my transactions table. So, it wasn't fully deleted in the sense that I'm keeping a record of it somewhere else. There's also one more way among many others to implement this idea of soft deletions.

**6:02:23** · that is not quite fully deleting something from my database, but instead keeping it around with a log that we've removed it in some way. Let's look at this table here. I have collections, but I also have this column called deleted.

**6:02:37** · And by default, the value here will be zero. That is, by default, I'll add some artwork to my collections table and deleted will be zero. If I want to delete a piece of artwork though, what could I do? Instead of deleting it fully from my table, removing the row, I could mark it as deleted. I could change the deleted column from a zero to a one.

**6:03:02** · Let's say I want to delete farmers working at dawn. Instead of writing literally delete from collections where title equals farmers working at dawn, I could say update the deleted column of collections where the title is farmers working at dawn and make it not zero but one. Now I've marked this item as deleted. I could run a query that excludes deleted items, but this row is still around in my table.

**6:03:27** · So let's try implementing this idea of a soft deletion inside of our collections table. so that we don't lose records of things we've actually had in our collection. I'll come back to my computer here and let's work on altering our table for collections here. If I type dots schema collections schema collections, you should see I have the table collections and also the triggers associated with it. What I don't have yet in collections.

**6:03:59** · If I go over here and show you, I don't have a deleted column. I have ID, title, accession number, and acquired, but I don't have deleted. So, as we learned last week, we can use alter table to add a column to our collections table and by default make the value zero. So, let's try that.

**6:04:21** · I'll go back to my environment and now I'll run alter table. I might say alter table and a table I want to alter which is collections. Now I want to add the column deleted deleted to collections and I want to make this type integer should store whole numbers whether positive or negative and the default value will be zero in this case. Now I'll hit enter.

**6:04:48** · And if I type dots schema collections, I should see I have my very own deleted column inside of collections. If I type for instance select star from collections from collection semicolon, I'll see that by default all of these values are zero in my new deleted column.

**6:05:12** · So instead of trying to delete, literally delete from collections, I could instead just update it. I could say take the updated column and flip it from a zero to a one. Let me try update collections and set the deleted the deleted column equal to one where let's say the title equals farmers working at dawn. And my query wraps here, but it should still work just fine. I'll hit semicolon enter. Now I didn't use delete from I used update.

**6:05:45** · If I select star from collections semicolon here I'll see well farmers working at dawn is in this table but technically at least we marked it as deleted. So it seems now I don't want to use just select star from collections to see what's inside my collection. I want to apply a filter to remove those that have a deleted value that's not equal to zero. Let's try this.

**6:06:14** · I'll say select star from collections where deleted does not equal one. If I hit semicolon here, what do I see? Only those values that are not deleted. I could go ahead and find them. I could say maybe select star from collections where deleted actually is one or deleted equals one like this. And now I see all those rows that I marked as deleted.

**6:06:45** · Now this has some advantages. One of them is we keep data around. We don't actually formally delete it. We can still recover it later on. But it also has some tricky ethical questions too.

**6:06:57** · Like it's okay if we're talking about artwork here, but if you're talking about user data, is it right to only soft delete it if they ask you to delete it? And particularly in conversation with um new frameworks like GDPR and the right to be forgotten and so on. It's up to you as a programmer to make the right decision here. When should you find data that's sensitive enough and actually delete it or when is it better to just soft delete it and keep it around in case you need it for later.

**6:07:23** · So we'll end here on this note where if I say select star from collections and I want to find those only where deleted is not equal to zero like this or not equal to one. This gives me back all of the items that are not deleted. But wouldn't it be nice if I could actually run a query on some brand new temporary table that actually only will ever have those items that are not soft deleted. Turns out we can do that with an idea called views.

**6:07:54** · And we'll see those in much more depth next week. We'll see you then. \[Music\] Well, hello one and all and welcome back to CS introduction to databases with SQL. My name is Carter Zeni and up until now you've been learning how to design databases and how to add data to them like how to insert, update, and delete some values all together.

**6:08:34** · Now along the way we've added some complexity that is we went from one table to multiple and we had relationships too among all those tables as well. Now what we'll introduce today is a way to simplify some of that complexity and give you a way to see your data all the more clearly. This tool called a view. Now we'll begin with a familiar data set this data set of books. And we learned about this data set of books back in week zero.

**6:09:00** · If you remember, we had a table of 78 books that had all been nominated for the International Booker Prize. It was a single table just of these books. Now, quickly in week one, we introduced more than just this single table. We actually had multiple tables. A table for books, a table for authors, for example, and also some relationship between those authors and those books.

**6:09:25** · We said that an author could write not just one book but multiple books and similarly a book could be written by not just one author but multiple as well. This is what we called a many to many relationship. Now we also saw this not just visually but in our database in terms of tables as well.

**6:09:47** · We had this kind of schema where we had a table for authors, a table for books, and then a table in the middle to talk about the relationship between authors and books. Which author wrote which book? We could see this in the authored table. Looking at these IDs here. And now to recap, if I wanted to find the book that Han here has written, let me ask how could I do that?

**6:10:12** · How could I find the book that Han in the author's table has written over here in the books table? And feel free to raise your hand.

**6:10:25** · By looking at the author ID, 31.

**6:10:28** · Nice. So start by looking at the author ID. That's a great idea. So here we see that Han's author ID is 31. And we could make this link between the author's table and the authored table. So I'll highlight this here so we can see it visually. Han has the ID 31. And here in the author table we see the author ID of 31 next to actually some book ID. This book ID is 74. Well, what book has that ID 74? Turns out it's the white book all the way over here. Now this is adding some complexity to our queries.

**6:11:02** · If I want to find who wrote what book, I have to go through the author's table, then the authored table, and then the books table. That's just a lot of steps to go through. And we could though try to simplify this to have a better view of this data to see it with just a single column for authors and a single column for titles. So let's try to visualize this together. What I might do first is try to flip around this primary key of authors, this ID column.

**6:11:32** · Let's put it closer to the author table just visually, metaphorically here. Now I might see that these ids line up one to another. And we saw in a previous lecture that I could use a join in SQL to put these tables into a single table.

**6:11:52** · And what a join does if you remember is take the primary key in one table and the foreign key in another and just find which ones match to put the rows of each table together. A bit like touching your fingertips together like this. So I'll then visually move these together, join these tables into a single table. And notice how if I now just get rid of these IDs metaphorically, just visually here, I now have a much more simple table, a simple view of this data.

**6:12:19** · And if I want to find which book Han has written, well, I could do that. Look at a single row here. Look at the name column and then the title column here.

**6:12:33** · Now what we're doing by creating this new view of our data set is actually creating well a view and a view is defined by this here a virtual table that is itself defined by a query. Now what does this mean? What is a virtual table? What is a query? Let's go back a few steps and see this in action. So we started with in this case three tables authors, books and authored. And presumably there's some query here that gets us from point A, these three tables, to point B, this single table.

**6:13:09** · That query might involve some selects, some joins we talked about earlier. But there's some query we can write to get us from point A to point B. And notice here that the result of this query is itself a table. Like this has rows and columns. And what we can do is see all of those in terms of a table we could later on query. So a view is a way of writing some query to see our data in a new way and then saving this view of our data so we can query it later on.

**6:13:46** · Now why might you want to build a view?

**6:13:48** · Well, you might want to do it for a few reasons here. You could use it to simplify your data as we just saw here.

**6:13:54** · You could use it to aggregate your data to try to sum up some values and store that in a single table. You could use it to partition your data or divide it into logical pieces. And you could even use it to secure your data to perhaps hide some columns you don't want somebody to see. There are more reasons too to use views, but we'll focus on these for today. And let's begin by focusing on simplifying. So we saw earlier a way to simplify these multiple tables down in to one.

**6:14:24** · If I go back here, we'll see we got from this set of three tables to a single table that had both author names and author titles. So let's see here exactly how much we're reducing complexity by trying out different queries and then adding in a view to see all the benefits of this new view we have here. So we'll go back and we'll see in this case our three tables authors books and authored and let's say I want to find the books a particular author has written.

**6:14:56** · I could write a query to do just that. Let's go back to SQLite here to run that query ourselves. I'll come back to my computer here in SQLite and my goal will be to find which author wrote which particular books. So if I go to my database here, I can go to my terminal and type SQLite 3 long list.

**6:15:17** · DB to reopen this database. And now I should see if I type schema all the tables that are inside of it. I have a table for authors. If I scroll up a little bit, a table for books and a table for authored, that is relationships between authors and books.

**6:15:35** · Now, let's say I want to write a query to find which books Fernanda Melor wrote. Well, I probably first need to find Fernandanda's ID as we just saw visually in our earlier example. So, let's find Fernandanda's ID. I could say select let's say ID from the author's table where the name equals Fernanda Melor. So, I'll say select ID from authors. Then where the name equals Fernanda Fernanda Melor semicolon. So it seems Fernanda's ID is 24.

**6:16:08** · And I could use this ID in the rest of my query, but I could probably do better than this. I could use what we saw before something called a sub query to take this query I just wrote and put it inside some other one here. So let's take the next step and find the book ids that Fernando wrote. So let's try looking at the authored table for that which has author ids and book ids side by side.

**6:16:35** · Okay, I'll say select in this case the book ID from the author table where in this case the author ID is equal to well I could say 24 but I want to do better. I could actually have a my very own subquery here to find Fran's ID dynamically.

**6:16:53** · I could put uh parenthesis here, then hit 1 2 3 four spaces and say select ID, select ID from the author's table where the name equals Fernanda Melor, that same query from before. I'll close this out. Close out my sub query. And then if I hit enter, I should see now the book IDs that Fernanda has written. But there's still one more step here. What do I now need to do?

**6:17:24** · I have book IDs that Fernando wrote. But how do you think I could find the titles from those book IDs?

**6:17:34** · You could select the title from the books.

**6:17:37** · Nice. We need to select title from that books table. So if you remember, we have titles inside of our books table, but we still need to link those titles through their ID to the book ids Fernanda has written. So let's do one last step here.

**6:17:52** · I'll come back to my terminal and I'll write the query in full now. So I know I want to end up with titles. I'll say select in this case title from the books table. Now I want to find particular titles where the ID is in that list of books Fernanda has written. So I'll say where the ID is in some subquery, the query we actually just wrote. So let me write it again. I'll say 1 2 3 four spaces here to indent for style.

**6:18:21** · Then I'll say select the book ID from the author table. in this case where the author ID is equal to some number in this case Fernand's ID. But what is Fernand's ID? Let's find out. I'll make another subquery here to find Fernand's ID indenting four times just for style here. Then I'll say select ID from the author's table and then again indent where the name equals Fernanda Melor.

**6:18:58** · Then I'll close out all my queries to create this single long query to find all the books Fernanda has written. And again the order here is first find Fernandanda's ID, then find the book IDs associated with that ID, then find the titles associated with those book IDs themselves. Now I'll hit enter and I should see all those books that Fernanda has written. Now, as we talked about, this is a lot of complexity, a lot of tables to go through, and there's probably a better way to do this.

**6:19:29** · Let me open up a new terminal and try out a different way of going about this. I'll make a new connection to my database.

**6:19:39** · I'll make a new terminal and I'll say SQLite 3 long list. DB. Hit enter. Now, I should see that I have a brand new connection to my database. And I could try to find a better way to do this. Let me try to do what we did visually and like join these tables together. Well, I could try select name and title from the author's table. But notice how author's table doesn't have titles in it.

**6:20:08** · It does have the name of the author, but it doesn't have book titles. So to get titles, I have to join in some new table here. I'll hit enter and I'll say join let's say the author table on author's dot id equals author do aauthor ID and

**6:20:32** · all I'm doing here is saying I'll take first the author's table and then why don't I try to combine this table with the authored table linking it up by looking at the author's do ID column and the authorauthor ID column And visually, let's take a look at what we're doing here in this join. If I look at this in my slides here, I should see I started with my author's table here. I had names of those authors and I had an ID column in that author table.

**6:21:02** · Now, I'm trying to join the author table by telling SQL that these two columns, author ID and ID, should align. They should line up like this. So, their rows are all together, but there's still one more step. I've joined the author table and the author table, but what's the next step to find book titles? I still have to join the books table. So, let's try that here.

**6:21:33** · I'll come back over and instead of joining just the auth table, let me now try to also join let me hit enter to also join the books table. I'll join books on books.

**6:21:50** · ID equals in this case authored dotbook ID. And to be clear, this line here means that what I'm trying to do is now join this books table which is over here with this author table aligning it so that their ids match up into a single row as we see here with 74 and 74 one and one and so on.

**6:22:16** · I'll come back and now let me try this. come back over here and I'll just try hitting enter to see what I can see from this query.

**6:22:29** · Okay, let me zoom out a little bit and you'll see I actually do have author names next to book titles all in one table just as we thought we would. So, this is useful to me. But what if I wanted to have this stored as a way to see my tables? I want to be able to query this kind of table I see right here. Well, for that I could try to introduce a view. Now, a view starts with a query as we just saw.

**6:23:02** · I wrote a query to select names and titles from three different tables joining them together. But if I want to save the results of that query so I can query them later on, I could use this syntax here. create a view that has a name that I can give to it as this query down below here. So create view given some name as the result of this query gives me a view that is then saved and part of my schema.

**6:23:35** · So let's try that here to create a view by which we can see both author and book titles side by side. I'll come back to SQL light here and I am already in this brand new terminal.

**6:23:50** · So I could try to remake this view and save it now for later usage. I'll say create a view and call it long list. The same name we gave our single table back in week zero. Now I'll say this view is

**6:24:08** · the result of this following query as let's say select name and title from the author's table but not just the author's table join let's say the author table join authorred on author's do ID equals author do aauthor ID and then join again our books table as we saw visually here.

**6:24:36** · Join books join books on books dot id equals authored dotbook id. Now that is the query I used before to see author names and book titles side by side. If I create this as a view hitting semicolon and enter nothing quite happens.

**6:24:59** · But now if I type dots schema and hit enter, I should see a view called long list that has two columns, name and title. And I actually see the query I used to create this view. So let me think now I want to see what's inside this view. And to query a view, I can use it exactly as I would a table.

**6:25:25** · I could say select star from long list semicolon hit enter and now I should see author names and book titles side by side. So if I have this kind of table with authors and book titles side by side, what then does my query become to find the books written by Fernanda?

**6:25:49** · Let me ask our audience here. What query could I use now on this view to find the books written by Fernanda?

**6:25:59** · Thank you, Mr. Carter. We cannot query uh the book or the all of the books using her specific name.

**6:26:07** · A good idea. I can use particular name in this case and perhaps just use a simple where. So let's try that here. I go back to my terminal and if I want to find the books written by Fernanda, well, I could just query for them in this single table that I created called long list or not really a table but now a view. I'll say in this case select the title from select title from long list where to Muhammad's point I could just say name equals Fernanda meernanda Melor semicolon.

**6:26:40** · I'll hit enter here and I see those same books Fernanda has written. Paradus and Hurricane season.

**6:26:49** · So let's see where we started here. We started with this kind of query long multiple lines many sub queries involved just to find the answer to which books Fernanda had written. Now though that we have a new view, I can simplify this query to just this here. select title from long list where the name equals Fernanda. And I can do all of this without using much if any more disk space. A view, remember, is a virtual table, not a real one.

**6:27:21** · And I can then have the results organized like this, while still being in those underlying tables stored essentially elsewhere.

**6:27:32** · So, let me ask what questions we have on how views can simplify our data. Um, can we then somehow manipulate the views to uh maybe order the results or display them just differently?

**6:27:48** · A great idea. So, if I wanted to maybe order these books, I could absolutely do that in the same way I would do in a table. So, let me go back and show you how to do that. Let's say I want to organize these books alphabetically by title. So, if you remember using our regular old table, we could use order by. I could do the same thing here. I could say select both the name and title columns from my long list table. And now let me try to order by order by the title column in this case.

**6:28:19** · And I'll hit semicolon. Now if I hit enter, I should see the book titles organized alphabetically. Now, the view itself does not have these titles automatically alphabetically sorted for me, but I could make it do that. If I had when I was making this view included order by let's say title at the end of that query, I would then have those titles saved in this view automatically as a toz.

**6:28:50** · So very powerful if you want to not just find particular ways of seeing your data, but also organizing it or ordering it too. So with that note, we've seen how to simplify one example of having multiple tables down into one. We'll come back in just a few and see what we can aggregate data too, putting that data into a single table for us to see some statistics and such as well. Come back in a few.

**6:29:16** · And we're back. So we just saw how to simplify some data, how to take multiple tables and see them as one. What we'll do now is think about how we can aggregate data. That is to take many individual data points and summarize them to find an average or a min or a max but see those results inside of a view. So if you remember in our long list database we had a table of ratings and in this case books had individual ratings from individual people.

**6:29:46** · Like maybe I gave book ID one a four out of five stars, but David gave it only a three. Now we store these individual ratings in our database. But ultimately, I don't care so much what I rated it or maybe what David rated it. I care about the average rating, let's say, for each book. But if we care about those averages, why then would we store all the individual ratings? Let's think of this as a design question here.

**6:30:15** · Can you think of a reason we might want to actually have these individual ratings stored in our database? What does that give us at the end of the day?

**6:30:26** · Perhaps reliability to know uh how many persons rated a book.

**6:30:31** · Nice. So, it's nice to have some more data. I could know how, let's say, I rated a book or how you rated a book.

**6:30:36** · That's good here too. And I would argue that from having this additional data, we could compute more statistics. I could find not just the average rating but also the minimum rating or the maximum rating or the median rating and so on. So these individual results allow us to find and compute more statistics like averages, mins and maxes as opposed to just storing the average. Now if I wanted to find the average of these results, what could I do?

**6:31:05** · Well, we saw before I could try to group ratings by individual book IDs. Let's say I want to find the ratings for book ID 1 and book ID 2. I could group by the book ID column, turning these into individual groups. And let's say I want to find the average here using a SQL query. I could say find me the average of the rating column when I have groups by book ID.

**6:31:33** · that effectively takes my table like this and says, "Okay, I'll combine all the ratings for each individual book ID and find for you the average. I'll first kind of compress this data together, literally putting it maybe one on top of the other here. And then find the average of all those results. Let's say 3.67 for book one and 2.5 for book two."

**6:31:56** · Kind of compressing all of our data into a single result. In this case, the average. So let's walk through then how we found the average using a SQL query and then we'll turn that into a view. So I'll come back over here to my computer and I'll open up long list db. I'm already here. So I can type dots schema ratings to see the schema for this ratings table. And you'll see it does have a book ID column and a rating column as well.

**6:32:26** · So if I want to find the average rating for each individual book ID, what could I do? I could try to select the book ID column and the rating column like this. But I don't want to select just the rating column itself. That gives me individual values. I want to find the average rating instead. I could instead say find me the average rating from this table.

**6:32:57** · Now let me give this a new name. I'll say as rating calling the average rating now newly in this case rating. And I'll select this from the ratings table. And finally I need to group by something. I need to group by book ID. That means I'll calculate the average rating for each book ID. I'll hit semicolon here and enter. And I should see all of these book IDs top to bottom with their own rating.

**6:33:31** · But here it doesn't look so pretty. What could I do to try to make this not so long? Like 3.774019431. There's a better way to do this. And we saw it before. What could I do to enhance this view of my ratings table? I see some suggestions about rounding the ratings, but I was also going to suggest adding the book titles of course.

**6:33:57** · Ah, good uh point here too. So, we first want to add the first want to probably add the book titles to see what titles we're talking about, not just in this case individual book IDs, but also a good point to say, let's try rounding these so we don't see 3.7740194.

**6:34:13** · Let's try to round that maybe to two decimal places just to be safe. So let's first try rounding this and then we'll try adding in some book titles to your suggestion here. I'll come back over and let me just try rounding it first. So I will come back to my terminal and I'll say I want to find the average rating for each book ID and I want to select not just the average rating as we did before but the rounded average rating.

**6:34:40** · So I can use round and say take the average rating and round it to two decimal places. And I'll call this column just rating in the final result. I'll select this from the ratings table.

**6:34:55** · And now I can group by in this case book ID. Enter. I should see I have rounded ratings now. A little more pretty than before. Now to your point, let's try to add in not just book IDs but also book titles. Like what does it mean for a book ID to have some rating? I want to see titles here in the end. So let's do that.

**6:35:17** · I'll say select book ID and also select title and maybe even select the year that book was nominated for the Booker Prize. I'll then select the rounded average rating to two decimal places as rating. And I want to select this from the ratings table from ratings. But what do you notice? If I were to select just from ratings, what data am I missing? And where could I find it?

**6:35:51** · Hey, you're missing the titles from the books uh table. Yeah, I have to have titles and those are stored in the books table. So, what should we do? Probably just join in the books table matching up that primary key with some foreign keys.

**6:36:06** · So, I'll come back over here and we'll do that. I want to select from ratings of course, but I also want to join in in this case the books table. So, I'll hit enter. And now I'll say join as well the books table. Now, how can I match up the books table with the rating table? Well, I know that the rating table has a foreign key called book ID and the book table has a primary key called ID. So, I'll tell SQL I want to match these two up a bit like this.

**6:36:34** · I'll say join books on ratings.book ID, that foreign key that's inside of ratings equals in this case books.

**6:36:47** · ID.

**6:36:49** · Now, there's one more step which is to group by book ID. still. So, I'll hit enter and group by book ID, but now I should be able to hit semicolon and enter. And I should see not just book IDs, but now titles and the years those books were nominated as well. So, this view is getting better and better. And I might say we actually go ahead and just add this to our schema. We could create a view that returns to us the results of this query. So, let's try that.

**6:37:19** · I'll say create a view called maybe average book ratings. Average book ratings for people to come in and do analysis on if they'd like. Then I could say um I want to create this view as that query we wrote before. So I'll say again select the book ID the um title and the uh let's say the year column the rounded average rating to two decimal places and then I want to select it as rating.

**6:37:54** · I'll select this from the ratings table from ratings and then I'll join as we did before the book table from ratings and then join books on that primary key and that foreign key. So I'll say on ratings dotbook id that foreign key in ratings and set that equal to books ID that primary key we're going to use to join these tables together. Then I'll say group by book ID.

**6:38:23** · And I should have if I hit enter my very own view called average book ratings that I can use to then see the averages for each of these books. I'll say select let's say star from average book ratings semicolon. And now I should see all of those results just as we had before. Now, notably, because this is in a view, I'm not using much if any additional space in my database.

**6:38:55** · I still have underlying this view individual ratings. But because I saved this query and the results it created in a view, I can actually have access to the a rounded average ratings for each of these and I can query that view as well. So let me ask then what questions we have on how we've used views to aggregate some data so far.

**6:39:21** · Actually I have a question can we use both uh uh same name like we before use long list and here we using for average something can we use long list for this both of them.

**6:39:37** · Yeah.

**6:39:37** · So if you remember before we had this view called long list and long list had book titles and authors inside of it. And I think you're asking could we try to join let's say the long list table with our ratings to get book titles and so on. We couldn't do that because we don't have the ID column in that long list view. Um we could though perhaps write some queries that involve that long list view as well.

**6:40:04** · Okay, let's keep going here and seeing what advantages this view might give us.

**6:40:09** · So, I'll come back over here. And one more advantage is that if I were to add in some new rating to my ratings column, I could just requery this view to find the updated average. So, let's say we use some insert into statement here and I update some books ratings. Well, if I'm a data analyst and I come back in a little later and I want to find the updated rating, I can do it just again by selecting from selecting star from average book ratings like this. Average book ratings. Hit enter.

**6:40:42** · And now I see perhaps some updated averages as well. Every time I query this view, I'll rerun essentially that query from before. And now I'll see the updated averages for each book.

**6:40:59** · Now sometimes as a data analyst I might want to create a view but not store it longterm as part of my schema. Like here if I type schema I see both our prior view called long list right here and I also see our average book ratings view.

**6:41:19** · But if I am somebody who comes in and I maybe want to find the average book ratings not by each book but by each year I could do that but then not store that view long term. Maybe I don't want others to see this view or maybe it's just for my own u analysis on this given day.

**6:41:37** · Well, to do that, I could move beyond just create view and I could also enhance this to be create temporary view where a temporary view exists only for the duration of my connection with database. So to be clear, that means if I type SQLite 3 long list db, I'm opening a connection to the database. If I then typequit, I would then lose that connection, quit that connection, and that view would no longer be there. So, let's try this.

**6:42:10** · I'll come back to my terminal, and we'll create a temporary view that shows us the average ratings for the books by the year they were nominated, not by every individual book here. So I could try doing the same query from before like select um let's say the rating average rating select it from the ratings table join books and titles and so on but what do I have already to build on top of if I wanted to find a view that has a title

**6:42:41** · a rating and even let's say the year that book was published what do I already have in my schema for that? Uh, so we could use the view that we just created.

**6:42:54** · Yeah, nice idea. So we could actually use the same view we just created to create ourselves a brand new view. So just because something is a view doesn't mean we can't use it to then create another view as well. So we'll do exactly that. We'll come back over here and I can type uh dots schema to see I still have this view called average book ratings and in it I have book ids their

**6:43:20** · title the year they were nominated and their average rating but now I want to find let's say the average rating for each individual year not for each individual book so what could I do I could say select the year column and the rounded average rating in this case from the rating column in average average book ratings and I'll wrap this query here. Let me zoom out so you can see it all online. Now I'll say I want to group by the year column.

**6:43:53** · So here I'm now saying find me the average rating of each book of each book's average rating for each individual year. I'll hit enter and we should see if I zoom back in for 2018 we have 3.75 for 2019 we have 3.64. So this means that apparently in 2023 the average rating for books that were long listed for the international booker prize was 3.78 and same for 2022 3.87 2021 was 3.69.

**6:44:26** · So I have this new view here. I could store this temporarily inside of a view that I could use while I'm doing some analysis on this given day. So I'll say create a temporary view and I'll call this one average ratings by year. How were the books rated each individual year on average? And I'll say this is the query that I just did before.

**6:44:49** · Select in this case the year and the rounded average rating to two decimal places as the rating column from average book ratings. That same view from before. Now I'm creating a view from my view. I'll group by here. Group by year. And then I'll hit enter. And I should see nothing popping up.

**6:45:16** · But now if I wanted to query this view, I could say select star from average ratings by year and I'll see the results of that view. Now though, here's the catch and why it's temporary. If I were to typequit now.quit and try it again, SQLite 3 long list db. Oops, let me retype that. SQLite 3 long list.db.

**6:45:47** · If I now try to select star from average ratings by year semicolon, I'll get no such table and really no such view. I don't have a view called average ratings by year anymore because this was temporary.

**6:46:05** · So let me ask what questions do we have on temporary tables if any temporary views rather? Right. So thank you. So the the first thing that I notic is that it just you know helps us to do some kind of testing when we use you know temporary views. Basically you know uh the views will not be saved in the database. Uh but again it's just you know a good way to you know just to test the query whether it is usable or not.

**6:46:38** · That's a great use case for them. And in general, if you are working on a database and you want to organize the data in some way, but you don't want to store that organization long term, a temporary view is great for that. If though you are a developer and you want to ingrain this view as part of your database, you might just use create view, plain and simple, to have it always be in your database for you wherever you connect to it and whenever you connect to it. Great question.

**6:47:06** · Okay, let's keep going and let's introduce now something called a common table expression or a CT. And a common table expression is simply a view that exists for the duration of a single query. So a regular view, as we saw before, exists forever in my schema.

**6:47:26** · A temporary view exists for a single connection, but a CTE exists for a single query. And the syntax looks just a bit different. With a CTE, I can write a single query, but at the beginning of that query, define the CTE, the common table expression. To do so, I would say with and give it some name as and then inside these parenthesis say the query I want to be this CTE here.

**6:47:52** · I could then optionally follow it up with more CTE for this same query or I could omit the comma and then use just select from the name of my CTE up above. This is useful if you want to have some very temporary view that you don't want to store in your schema but you do want to use for this particular query. So let's see an example now recreating our average ratings by year but now using a CTE.

**6:48:22** · So I'll come back to my computer and I'm already in my SQLite terminal. What I should do though is try to drop the prior view. I want to remove that view called average book ratings to create room to have now a CTE with that very same name.

**6:48:42** · So I'll say drop view and the name of the view I want to drop average book ratings average book ratings semicolon and now I should see that that view is no longer in my schema. So I want to recreate though what we did before which was finding the average ratings of books year overyear. So let me try to write this query.

**6:49:09** · But it would be handy if in that query I had access to a view that gave me the average rating for each book. So I'll write the query like this. I'll use a CTE and I'll say with average book ratings average book ratings as now this query I'll write now inside. And this query should be familiar. It's the same query we use to find the average rating for each book.

**6:49:38** · I'll say here I want to select I want to select the book ID column, the title column, the year column, and the rounded average rating to two decimal places. Calling it rating calling it rating in this case from my ratings table like this.

**6:50:04** · Now what do I need to do? I also need to you saw before join in my books table join books on the primary and foreign keys aligning. So I'll say the book ID column that foreign key in the ratings table should equal books. ID that primary key column in books. Then I will group by the book ID to find the average rating for each book. And now let me close out this CTE.

**6:50:34** · I'll close my parenthesis. And because I'm only using one CTE, I don't need a comma. I can then just write the rest of my query.

**6:50:47** · I'll hit enter for style sake. And now with this CTE called average book ratings, I want to find the average rating yearover-year grouping not by book but by year. So I'll say select in this case year and then select the rounded average rating still to two decimal places as a new rating column.

**6:51:12** · Then I'll select this from in this case my CTE. So I'll hit enter here as well from average book ratings that same CTE I defined earlier in my query. Now finally to find the average rating across individual years I'll say group by year semicolon and now hopefully if I hit enter I should see the average rating for each year in my database.

**6:51:44** · Okay, so the CTE is useful when you have sub queries you don't want to repeat or when you want to make a view that only exists for the duration of a query. And it's with all of these tools like views, temporary views, and CTE that we can get away with storing statistics about some data in our data set and not storing them uh in the actual um database, but

**6:52:09** · only inside this view we might have here. we'll do next is see how we can use views to create not just these aggregations but also partitions of our data. A way to split our data up into logical pieces for use for our own sake or even for application sake as well.

**6:52:26** · We'll come back in just a few. And we're back. So we've seen so far how to use views to simplify and also aggregate our data. What we'll see now though is how to use views to partition our data. that is to break it into smaller pieces that be useful to us or to some application.

**6:52:45** · Now on the international booker prize website they have a page for each year of long listed books. But in our table we have all the books together regardless of their year. Well maybe it will be useful in the application even for me personally to have a table one for each year of books that have been nominated for this prize. But before I create that view, I should ask how do I try to find the books nominated in 2023?

**6:53:16** · If my table looks like this, I have a table of books with ID, title, and year columns. What query could I use to find only those books nominated in 2023?

**6:53:29** · Use the wear clause with the year.

**6:53:33** · Yeah, I could use the wear clause and try to search for a given year. Like I could try to say where in this case the year is 2023 or equal to 2023 and that would give me back these two rows. If only two books were nominated in 2023.

**6:53:47** · In reality it's 13. If I wanted to find the next ones from 2022, what could I do? I could just change the wear clause to say where year equals 2022. And then same thing for 2021. I could say where year equals 2021. Now each of these segments of my data is what we'll call a partition a certain uh breaking down of my data into smaller pieces in this case organized by year.

**6:54:17** · So let's now create smaller tables one for each year that might be in our data set here. Come back to my terminal and let's think about writing this query from before. So, if I wanted to find the books that were nominated in 2022, I could say select the ID column and the title column from my books table. And then I want to find only those books where the year equals 2022.

**6:54:49** · Then semicolon and then enter. And I should see only those books that were nominated in 2022. But now I want to create a view that might actually store the results of this query more long-term. I could say create view and call this let's say 2022 as now same query from before select ID and title from my books table from my books table in this case where the year equals 2022 semicolon.

**6:55:26** · Now, if I ever want to find only those books nominated in 2022, I could now use my view. I could say select star from 2022 semicolon or uh quote and then semicolon. Hit enter. And now I should see those very same books. So, what could I do now? Maybe I want those books from 2021 as well. Let me ask the audience, what could you do to create the view for the books in 2021 based on what we've just seen now?

**6:55:58** · We could just change the year from 2022 to 2021.

**6:56:04** · Yeah, just change the year. And what would you propose we call this new view?

**6:56:08** · If you had to take the the reigns on naming this view, what would you name it?

**6:56:12** · Books that were written in 2021. Yeah, we could we could call it books that were nominated in 2021, but I would argue that might be a bit of a long view title. So, let's shorten it just a little bit and maybe keep in keeping with our current naming, we'll say 2021 instead. So, I'll come back over here and let's try this. I'll say create a view. Create a view. And we could by all accounts and purposes, we could say um books nominated books nominated in 2021.

**6:56:43** · And that's totally okay. But if I were to pass this view on to a new programmer, a new database analyst, well, I kind of want to shorten it for them, make it more simple for them to read. So, I could just call this 2021.

**6:56:56** · Of course, this title is kind of ambiguous. Like, if I pass you a view called 2021, are you automatically going to know what's inside that view?

**6:57:06** · Probably not. So, it's actually a balance between how descriptive you want to be with your names here. We'll stick though with 2021 to our earlier example here. Now I'll say create view 2021 as select ID title from books and to Vavian's point I'll say where the year equals 2021 semicolon enter and now I could say select star from sect star from 2021 semicolon.

**6:57:38** · So this is a good way to break apart a large table into logical pieces. It's useful both for both you as a programmer and also for applications that might only need to access some subset of your data where some condition is true. So based on what we've seen so far, what questions do we have on partitioning data with views?

**6:58:02** · We have created few views for 2021 and 2022. uh rather than creating two views, is it possible to uh you know uh simplify it as one and then use it rather like uh where is simply change that alone?

**6:58:19** · Yeah, I mean it's a trade-off here. So you could imagine trying to do let's say a single view that maybe has just titles and just years in it, but then you have to rewrite the query later on to find only those books for a certain year.

**6:58:33** · Here, what we're trying to do is just like break up this big table into smaller pieces. And you can imagine this being particularly useful if you had not just 78 books, but even like thousands or tens of thousands or millions of books. Could be useful to have a view for each logical segment of those 10,000 or more books. Let's take one more question here.

**6:58:54** · I uh would like to ask about uh updating the view itself. If I update the single table, any element in each table, the view can be updated automatically or maybe it needs some involvement.

**6:59:12** · Okay, a good forward thinking question here. Uh, you can, you're right, update a table. You can say update the table and set some column to some value. What you can't do actually is update a view.

**6:59:25** · And that's because a view doesn't have any underlying actually doesn't have any data inside of it exactly. It only pulls data from underlying tables. So let me show you how I could update this view or at least try to update this view. I'll come back to my computer and let's say we wanted to change a book in the 2021 view. I could say select star from 2021 semicolon. And maybe it turns out that there's a typo in here. So instead of uh minor detail, it's called something like the minor detail.

**6:59:56** · This um book on ID34 here, I could try to update this view. I could say update 2021 and set the title equal to the minor detail. The minor detail where the title currently is the title currently is minor detail like this minor detail. Then I'll hit semicolon. And if I do this, I get this error. Cannot modify 2021 because it is a view. Now, why can't we modify a view?

**7:00:33** · Well, recall that a view is simply the um combination of data from underlying tables. I've assembled data from different pieces of my database and put them into a single view. But I can't then update that data because that data is located in multiple individual tables around my database. What I should instead do is try to update the underlying table which I can do as we saw before with just update and set to.

**7:01:00** · Okay. So more on how we can update or at least uh try to update views a little bit later. We'll take a break and come back to talk about how we can secure data using views as well. And we're back. So, one more use case for views is being able to secure the data that's in your database. You might imagine having a table, but some columns in that table you don't want to share with somebody else. Well, a common practice in security is to only give someone the information they need to know. With views, you could do that very principle.

**7:01:35** · You could accomplish that by taking a table and reducing the number of columns somebody else might see. So let's consider here some ride share company. And ride share companies keep track of a lot of information about us. They keep track of where we're going, where we're coming from, who's in the car with us and who drove us there. Even sometimes.

**7:01:55** · Let's say that a ride share company has a table called rides. And inside this table is the origin of several rides and the destination along with the rider who took that ride. Now, if I were to ask you here, let's say I want to give this data to an analyst to figure out which rides are most popular or which rides are highly rated. What data should I probably omit if I wanted to share this data with somebody else? What should I remove from this table?

**7:02:28** · The data you could remove would be the rider.

**7:02:34** · Yeah, good point. So if I look at this table and I think of what information is personally identifiable P II personally identifiable information it seems like this rider column could identify somebody who took a ride from let's say goodday good galaxy to Honeyhive Galaxy and we don't want to leak that information if I gave this to some analyst.

**7:02:55** · Well, with a view, I could keep this underlying table, but I could create a view that only has the origin and the destination that omits the rider column. And I could more confidently share this view with an analyst, not the underlying table. So, let me try to implement this view so we can see it in action inside this database here. I'll come back to my computer. And in this case, I have a new database. I have one called rid share. DB.

**7:03:25** · I'll type SQLite 3 ridshare. DB to open up this database.

**7:03:33** · And if I type dots schema to see the schema of this database, I should see I have one table called rides where each ride has an ID, an origin, a destination, and a rider. Now I'll select star from the rides table. Select star from rides. Hit semicolon. And I should see the very same data we just saw in our slides where Peach is going from good galaxy to Honeyhive Galaxy, Mario going from Castle Courtyard to Cascade Kingdom and so on.

**7:04:03** · So now I know I don't want to share this data with somebody else. What could I do? Instead of selecting everything, I could try to omit this rider column to the point before. So let's try that. I'll select just ID and just origin and just destination from rides. I'll deliberately omit that rider column.

**7:04:26** · Now I'll hit enter and I should see the origin and destination, but I actually don't see the rider column. So this is a decent view, but I could probably improve this even more. It turns out that in SQLite, if I want to fill a column with some arbitrary value, I can do that a bit like this.

**7:04:49** · Why don't I try to select ID and select origin and destination, but I also want to let somebody know that this data has been anonymized. There is rider information in the underlying table, but you don't have access to it. What I'll do instead is say, let me make this new column that's filled with this value anonymous as a string. I'll say quote unquote anonymous as this column name called rider.

**7:05:20** · I'll select all of this from the rides table semicolon. Now I've more helpfully indicated that there is a rider column, but you deliberately don't have access to see who those riders are.

**7:05:36** · So my last step here is probably to turn this into a view. I have a good query, but I want to save it so I could query it later on. Well, I could type select or not select. I could type create view first. I'll create a view. This one just called analysis. I'll give this to my data analysts here. Create view analysis.

**7:05:54** · And then I'll say as let's go for select ID origin and destination as well as the anonymous the anonymous column as in this case the rider and I'll select all of this from my rides table semicolon hit enter now if I type schema I see my new view analysis and if I say select star from analysis is from analysis semicolon. I should see that I've anonymized quote unquote this data.

**7:06:34** · But to the extent this is helpful, I'd argue it's not very secure, at least in SQL light. And if you're thinking adversarially here, what might you be able to do still if I gave you access to this database?

**7:06:51** · What could you do to deanonymize this data and to see the data I didn't want you to see?

**7:06:57** · You can just uh query the writers table and find what are the riders values in the writers column.

**7:07:04** · Okay, so you're correct that we could still see the rides table. Maybe I look at the ID column in the analysis view and I see those IDs. I might be able to link those IDs with the IDs in the rides table. And nothing's stopping me, at least in SQLite, from saying select star from the rides table. So I'll come back over here and I'll try that. I'll say in this case, select star from rides. Hit semicolon. And now I see all that ride information although I hid it in this view called analysis. And this is a downside of SQLite.

**7:07:36** · In SQLite, we can't set access controls. Meaning I either give you the entire database or nothing at all. In other DBMS's though, I could set access controls. I could give David access only to the analysis view. I can give myself access to both the rides table and the analysis view. So keep that in mind when you're working with SQLite.

**7:08:03** · Okay, so we've seen here how to secure some data using SQLite and using views in this as well. Let's come back in just a minute and see how we could actually use SQLite and views to not just secure our data but also to work on soft deletions which you saw just a bit ago.

**7:08:20** · And we're back for one final application of views. We saw just a little week a few weeks ago how we could implement soft deletions. That is not fully deleting something in our database but only marking it as deleted. And we saw this in the context of Boston's own Museum of Fine Arts, keeping track of items inside their collection. So let's say we had this table called collections full of items in the MFA, the Museum of Fine Arts in Boston. Here I have four items currently in our collections. ID 1, ID2, 3, and four.

**7:08:52** · But I also have this deleted column which is either zero or one depending on whether an item has been deleted or not. So, I want to delete, let's say, farmers working at dawn. This first piece here, instead of deleting it from the table fully, I could set this deleted column from a zero to a one, just like this. And now it's only soft deleted. I still have the data here. I still have the title, but now instead of being a zero, it's marked as a one.

**7:09:23** · Now, this is useful, but what could I do to only see now the items that have not been deleted? Like, if I show you this database collections here, the table here, I have titles and the deleted column. But if I only want to see those items that are not deleted, what query could I use for that?

**7:09:48** · Would you use the wear statement?

**7:09:50** · I could use a select statement and I could use probably a wear clause as well. I could say select star where perhaps deleted equals zero because in this case when deleted is zero we know this item is still supposed to be in our table. So here's that query here select star from collections where deleted equals zero. Now we could try to convert this query into a view. So we could always only see the items in our current collection not those we have marked as deleted.

**7:10:22** · So, I'll come back over here and we'll see we have our collections table, but we also have now perhaps a new view of this table called current collections. Well, if I set current collections to be the result of this query, I should see when I update deleted to be one for some of these items here, it should be removed from this current collections table. So, let's try that. I could take farmers working at dawn and delete it. I could see this correspondence between this row here and this row here.

**7:10:54** · It's in both our collections table and current collections. But if I set deleted from zero to one, I should see that item removed from current collections, thus updating my view and keeping track of my items that are not currently in my collection. So let's come back here and implement this in terms of our own database. come back over here and I will open up MFA. DB, that old database from a few weeks ago. I'll say SQLite 3 MFA.

**7:11:29** · DB. And now if I type dots schema, I should see the tables inside of this database. Collections, artists, and created. We'll focus in particular on the collections table. So if I say select star from collections, I should see that I have the title, the accession number, and the date this piece was acquired by the MFA.

**7:11:49** · Now though, if I want to add a deleted column, I could do so by using alter table, I could say, let's alter table collections, alter table collections, and add a column called deleted. I'll say this column has the type integer. It stores whole numbers and the default number is zero semicolon.

**7:12:18** · Now if I say select star from collections select star from collections semicolon I should see there's this new deleted column where all the values are zero at first. So if I want to delete something, I could instead of typing delete from as we saw before, I could just update this deleted value. I could say maybe update update collections and set deleted equal to one where a certain title is present.

**7:12:51** · I'll say this that the title is equal to farmers title equals farmers working at dawn semicolon. So now I've soft deleted this item. It's still in my table at least the title is but now I've marked it as being deleted. It should not long be in my ultimate view. Hit enter here and I'll say select star from collections.

**7:13:20** · I'll see that in this case I still see farmers working at dawn. But what do I want? I want a view that only removes that only shows me those items that have not been deleted. So I'll try this. I'll say select star from collections and apply a condition to it to our earlier um point before. So I'll say where in this case deleted equals zero semicolon hit enter. And now I should see only those items that are not marked as deleted.

**7:13:51** · But I want to turn this into a view which I could. I could say maybe create a view called current collections. And then I'll make this the following query as select ID select title accession number and acquired. But now I'll actually omit that deleted column. I don't want this column to show up in my current collections. I only want it to be in the underlying table.

**7:14:18** · So I'll select all these columns from the collections table and then I'll say where deleted equals zero to apply this condition and only get those items that are not marked as deleted. Now I'll hit enter and I should be able to do this. Select star from current collections semicolon. And now I'll see only those items that have not been deleted.

**7:14:48** · So this seems worthwhile. I'm now able to view the items that are currently in my collection. But a problem remains. Like if I tried to update this table and insert something into it, what might happen? Let me ask our audience here.

**7:15:08** · Based on what we saw before, what would happen if tried to insert into this table here, this view perhaps?

**7:15:15** · I think we cannot uh update the view itself as we saw before.

**7:15:22** · Yeah, we can't update the view itself.

**7:15:24** · We can't insert new data. We can't even delete data. So, let me try first to delete data and then we'll see how to insert some data a little bit later.

**7:15:32** · I'll come back over to my terminal and what if I wanted to delete imaginative landscape I could say delete from delete from current collections where the title equals let me make a new line here where the title equals imaginative landscape imaginative landscape semicolon now I'll see that same error we got before we tried to update some view I can't modify this because it is a view.

**7:16:04** · Well, it turns out there is a way to work around this. We can't modify the view, but we can modify the underlying table. So to do this, we need rank from old friends. In this case, those called triggers. So if you remember, a trigger is a way to specify some SQL statement I want to run when some other SQL statement is run. we saw before. We could use before or after to say run this SQL statement either before or after some other SQL statement here.

**7:16:36** · What we didn't see until now is this instead of trigger. I can create a trigger that has a name and I can run it instead of some other SQL statement. So I could say instead of deleting on this view, let me give you the other the proper query to run in this case. So instead of deleting on this view, I will for each row run this other statement.

**7:17:02** · I'll say begin. This is the same I want you to run instead. And in this statement, we could have something that actually updates not the view but the underlying table. And we then end that query here.

**7:17:16** · So based on what we know about our view and the underlying table called collections, what query should we put in here to actually delete something from our table? Let me ask our audience instead of deleting from our view, what should we instead do to our table?

**7:17:38** · Yeah, you should update the deleted column in the collections table.

**7:17:42** · Yeah.

**7:17:42** · Uh, so instead of deleting from our view, what I really want to do is update that table. So let's write a trigger to do just that. Come back to my computer here and I'll start on this trigger. To our point, I want to create a trigger that runs instead of deleting on this view. And what I want to instead happen is an update on the underlying table. So I'll say create a trigger.

**7:18:08** · This one called delete. And then I'll say instead of delete on current collections that is whenever SQL hears or listens and hears a delete on the current collections view I don't want that to happen. I instead want this other statement to happen. I'll say for each row affected by that delete. For each row I asked delete on current collections run instead this other statement. I'll say begin. Here is that statement 1 2 3 4 indents for style sake.

**7:18:40** · And now I'll say I want to update collections. Update collections and set deleted set deleted equal to one.

**7:18:52** · But I don't want to leave this just as is. If I say update collections set deleted equal to one. What's the problem with that statement if I end it there?

**7:19:04** · Uh so yeah it will update all the columns whether it is we want it to be deleted or not.

**7:19:11** · Yeah

**7:19:11** · with no condition it'll update all the columns here. So I want to apply a condition to make sure it only affects the particular row I'm working with.

**7:19:20** · Well what unique identifies each row?

**7:19:22** · The ID does. So let's try using the ID here. I'll come back and I'll say I want to update collections set deleted equal to one but only when some condition is true. I'll indent again four times and say where in this case the ID the ID column is equal to the old ID. Now old here is a special keyword that means the row we just deleted or that we would have deleted from current collections.

**7:19:50** · I want to update that same row with that same ID in the underlying collections table. So I'll put a semicolon here to end and then I'll say end this statement. This is the entire statement I want to run after I try to delete on my current collections table. Now I'll hit enter and I'll see nothing changes.

**7:20:15** · But if I say dots schema, I should then see down below here I have a trigger called delete that will instead run an update when I try to delete from this view. So let's try that. What I can do now is try again to delete from current collections. I'll say delete from current collections. Current collections where in this case the title equals imaginative landscape. Let's say we sold this painting. It's no longer part of our collection. Imaginative landscape semicolon.

**7:20:47** · And now it actually seemed to work. I get no error here. So it seems like it went okay. Okay. Well, if I select star from current collections, I actually see that it's gone. But is it really gone? If I try select star from collections, not current collections.

**7:21:09** · The underlying table for current collections semicolon, what do I see?

**7:21:14** · That the ID column has been updated from a zero now to a one. So a good way of trying to use triggers here to update our views by instead modifying the underlying table. Now there might be one more issue we encounter here which is the following.

**7:21:34** · Let's say I'm at this current state in my tables. I have collections where farmers working at dawn is deleted. It has a one right here and we thus can't see it inside of current collections. Well, let's say I want to not delete from current collections, but also add to current collections. I could try to insert into this view, but I probably actually won't be able to do that because it is a view. Let's think then.

**7:22:01** · If I wanted to insert into this view, what should I really do instead?

**7:22:08** · You should add it to the collections table instead of the view.

**7:22:13** · I like that idea. So, I should add this row to the collections table instead of the view. But now, here's a bit of a trick. Let's say I add farmers working at dawn. We reacquired it. What should I do in that case? When I'm adding a painting I previously deleted.

**7:22:33** · So uh what we could do is we know that the deleted we we can check if the deleted column is one and then uh based on that we could like uh update that particular column or if the if uh the there is no uh title in the connections table you can just add it inside there.

**7:22:59** · Yeah, I like your thinking there of first trying to check, do we have this item already in our table or do we not? If we do already have it in our table, we should just flip this bit from a zero from a one to a zero. If we don't though, let's add a brand new row as we heard before.

**7:23:19** · So, let's think. What could we use to conditionally run some code on this collections table? Well, it turns out that you can use some other aspects of triggers. In this case, triggers have not just um unconditional uh use cases, but also conditional ones too. So, let's try this. I could try to insert to on this view and then run some code down below. But to our discussion a little bit earlier, I don't want to unconditionally do this.

**7:23:48** · I want to check is this item in my table or is it not already? So, for that, I could use this keyword called when. I could say for each row when some condition is true, run this trigger. And you can imagine having two triggers to insert into our view. One that runs when the item is already in our table. We could then flip that bit from a one to a zero. We could also have a different trigger to actually insert a new item.

**7:24:17** · In that case, actually inserting a brand new row to our underlying collections table. So let's work on this now to finish off and polish our collections view. Come back to our terminal here. And what we'll try to do is now insert into this table.

**7:24:37** · I'll create a new trigger this case called insert when exists. I'll say create trigger. Create trigger. Insert when exists. So this trigger will run when an item we're trying to insert is already in our collections table. I'll say instead of insert on the current collections table I want this to happen instead I'll say for each row now I'll

**7:25:06** · hit enter again and say when just for style sake when new accession number new accession number is in my table already well I want to find which accession numbers I already have and if you Excession number is a unique ID for the museum. It's not the ID column in my table, but a unique ID to keep track of items in the museum. So if I've already given this item an exception number, I should already see it in my table already. So I'll say then enter enter for style sake.

**7:25:37** · Select accession number.

**7:25:42** · Select accession number from collections. So this sub query tells me what accession numbers do I already have and this condition tells me is the new row I'm inserting does that have the same accession number or not. Now I'll close this sub query and I'll continue my trigger. I'll say begin. Well in the case that this item already exists in my collections table I just want to update.

**7:26:14** · I want to flip that integer from a one back down to a zero. So I'll say update collections update collections and set deleted deleted equal to zero.

**7:26:28** · Now I want to do this not on my entire table but only where the accession number is equal to the new accession number. That is the accession number I'm inserting here as well. I'll then end like this. And now I have my entire trigger. I'll say instead of inserting into my view, I want to run this instead. Check if I've already added this item and if I have changed that deleted column from a one to a zero.

**7:26:56** · Now I'll hit enter and let me hit enter again and let me check. I needed to have a semicolon after my where. So let me try to run this again. I'll do control D to restart and I'll say SQLite 3. Um let's do MFA. DB and I'll restart this trigger. So here I'll say create trigger create trigger insert when exists we gave the name before.

**7:27:29** · Then I'll say instead of insert on current collections what I want to do is run this. I'll say for each row I insert check some condition when the new accession number that is the unique ID the museum has for this item is in my already available accession numbers. I'll say select in this case select accession number from from collections and then I'll close the subquery.

**7:28:04** · Now I'll say I want to begin the same thing I want to run begin. Now update in this case my collections table and set the deleted column from a one back down to a zero. Update collections and set deleted equals zero where in this case the accession number is equal to the new accession number only modifying that particular row. Now I'll hit semicolon to close this statement.

**7:28:36** · And then I'll say end below a second semicolon enter. And now if I type dot schema, I should see my new trigger to insert into my collections table when I try to insert into my view.

**7:28:49** · So let's try this. I'll say maybe I want to insert into my collections my current collections. Insert into well let me try this. I'll say select star from select star from collections. And let's say I want to reinsert in this case profusion of flowers. So I'll say insert into um my current collections. Actually reinsert into current collections. I want to insert imaginative landscape.

**7:29:18** · So I'll say insert into current collections some set of values along with some columns. I'll say the title is profusion of flowers. There's imaginative landscape later on. then accession number then the date it was acquired like this now hit enter and provide the values I'll say the title is imaginative landscape like this number is 56.496 496 and the acquired date is going to be null in this case. We don't know when we got it.

**7:29:49** · I'll hit semicolon here and enter. So if I select star from collections now, select star from collections. Semicolon. I should see that I didn't actually insert a new row.

**7:30:01** · I only flipped that deleted value from a one back down to a zero. Now, there's certainly more to do here. I could write a trigger to actually add a brand new row to this table here. I could also try to update this data, change, for example, the acquired date from null to date we actually do know. For now, though, we'll leave all that up to you and we'll see you next time.

### Optimizing

**7:30:27** · \[Music\] Well, hello one and all and welcome back to CSF's introduction to databases with SQL. My name is Carter Zeni and today we'll focus on optimizing trying to reduce the time our queries take as well as the storage space our database might use.

**7:30:59** · We'll also see how to handle concurrency that is many queries all at once. Now, we'll do all of this in the context of a new database. This one, the Internet Movies Database, or IMDb for short. If you've been to imdb.com, you may have seen this whole big database of movies and we've compiled that into our very own SQLite database for us today. Now, this database is big.

**7:31:26** · It is much bigger than anything we've seen so far. In fact, it has over 200,000 movie ratings, over 400,000 movies, and 1.4 million stars or people who have acted in some movie. And the goal of this database is to represent movies, the people in them, and the average ratings for each of those movies. Now, we have ourselves an entity relationship diagram to describe this database. And it looks a bit like this.

**7:31:54** · We have people in one table, movies in another, and ratings in a separate table down here. Notice that people have a name and a birthday along with an ID, the primary key for that table. Movies too have a title and the year they were released as well as their own primary key ID here. rating down here has the average rating for a given movie as well as the number of votes that went into calculating that average rating here.

**7:32:24** · And notice too that the movie and people table has a many to many relationship.

**7:32:30** · That is a person can star in more than one movie in the same way a movie can have multiple stars. So if we want to implement this many to many relationship, we've seen one way to do that. Let me actually ask the audience here. How have we implemented a many to many relationship historically? What kind of tables do we need for this do you think? All right. So, not to worry if you don't have an idea of what we're going to use here. Let's take a peek at what tables we can actually use.

**7:32:58** · So, here as we've seen historically, we might have two tables. One for people and one for movies. And notice here in the people table, we have names along with a primary key called ID. And similarly in our movies table we also have a title column along with movies's own primary key and ID column over there. Now to implement the relationship between people and movies we have to have some table in the middle of these two.

**7:33:29** · One that relates people ids or person IDs with movie ids. And if we look at this table, I could see that if I see person ID next to some given movie ID, well, it means that the person with this ID has starred in played a role in this movie here. We see person 158.

**7:33:48** · Let's see, Tom Hanks was in the movie ID with 11479 or Toy Story as we see in the movies table. And now knowing this, how could we figure out which movies Kristen Bell has starred in? If we know Christian Bell's ID, what should we then do to find the movies Christian Bell has starred in?

**7:34:10** · Uh, you could select the ID of the people, then look it into the stars table, then look it into the movies table.

**7:34:19** · Yeah, I like your thinking. So, there's multiple steps here. We have to go through each table to find ultimately the movie that Kristen Bell has starred in. The first step might be to ask, what is Kristen Bell's ID? Well, it seems to be 68338. Then, to your point, we could look at the stars table and find out what movie IDs correspond to that ID here. So, it seems like 2294629 corresponds with Kristen Bell's ID here.

**7:34:45** · Then, finally, we look up in the movies table. Well, what title corresponds with 2294629?

**7:34:51** · It seems to be the movie Frozen. So, visually, we have this relationship among these tables here. So, let's now dive into our movies database to actually get a sense of what data is inside of this. And for that, I'll go back to my computer so we can open this database up in SQLite. Come back over here and I'll open up my own environment where I can type SQLite 3 movies. DB movies. DB.

**7:35:15** · And now, if I zoom in just a bit, I can then type schema to show you all the tables that exist in this database. I see up top I do have a movies table that has a primary key called ID, a column called title, and a column called year. I have that same people table with names and birthdays.

**7:35:39** · And I also have this stars table that corresponds with person IDs and movie IDs relating in this case people and movies. Okay, so let's try selecting then from our movies table to see what movies we have. Take a peek at our data.

**7:35:56** · what we saw just a little bit ago. We could try to take a peek at our data using a certain SQL keyword. I could select star from movies to see all columns from movies. But if I have, let's say, 400,000 rows, I don't want to print all those to the screen. So, what could I use instead? Certain SQL keyword. I'm hearing limit. So, let's try that. I'll say limit five. I only want the first five results here. I'll hit enter. And here I'll see those first five movies in my movies table.

**7:36:25** · They each have their own unique ID, a primary key. They have a title and the year that they were published. But if you've been to imdb.com, you may have wanted to search for a particular movie. Maybe you wanted to find your favorite movie among all the possible movies in their database. And we can simulate that kind of query by querying the database here.

**7:36:48** · Whenever you type in IMDb's browser, let's like the search for a movie called um Frozen, for example, it odds are that behind the scenes, a database is actually running that same query to return to you what movies have that title called Frozen.

**7:37:03** · Now, for me, uh my favorite movie since I was a kid is one called cars. So, let me try to search for cars here. I'll try to find select star from movies where the title equals cars. And you could imagine me going to IMDb, typing in cars in the search bar, and behind the scenes, this cql query gets run to find what movies have the title cars. So, let me hit enter here. And now I'll see that one movie has that title. Cars came out in 2006 and the ID is 317219.

**7:37:38** · But this is a lecture on optimizing. So, it's worth asking how much time did it take for this query to run? Let's find out. Well, I can use a SQL light command here called timer. I'll say dot timer on to make sure that I time my future queries. I'll hit enter now. And now if I try selecting again, I'll hit the up arrow twice to get back my old query. I can type enter and I'll see not just the results, but the time it took to run that query.

**7:38:11** · Now notice we have several different measures of time here. I have the quote unquote real time, which is essentially the stopwatch time, meaning from the time I pressed enter to the time I saw these results. How long did that take?

**7:38:24** · But of course, if you're familiar with computers, you know that there's more involved than just this query running. I also have to wait for the operating system, other processes as well. That's where user and system time come in. User time is how much time this query particularly took on the CPU. System time is how long I spent waiting around for other processes to finish before I could run this query. For us, we'll focus on real time. What was the wall clock time, the stopwatch time, so to speak, between the time I pressed enter and the time I saw these results.

**7:38:53** · Okay, so here we have a query taking 0.084 seconds. I mean, that is pretty good. If I only wait around for less than a tenth of a second, like I'm not complaining.

**7:39:08** · But if I'm the engineer at IMDb, why might I be concerned about a query that takes 0.084 seconds? Particular if I have lots and lots of users. What's the problem there?

**7:39:22** · Users, the database might be overwhelmed by the queries. And you should also consider like how much time the application takes to form the query to the database too.

**7:39:36** · Yeah.

**7:39:36** · Yeah. So the basic idea here is that when I have a single query that takes maybe less than ten of a second, that's fine. But if I have many many users running those queries all at once, like that time is going to add up. And so if I'm an engineer or even somebody in finance, I want to reduce that time because I'm paying per second that I run this database on some other server. So we can optimize these queries. But let's first get a sense of how they're presently running. Like what is SQLite doing underneath the hood? defined this movie called Cars.

**7:40:07** · Well, for that I'll bring up a certain visual here of our titles column. So imagine here that we have a uh sort of smaller database called movies that just has titles in this case. And now I want to search these titles. But I'm a computer. I'm not a human. Meaning I can only look at one item at a time. I can only look at one row and check its title.

**7:40:30** · Now, if I want to find the row or the rows that have cars in them, what's the best I could do? If my titles are not sorted, what's the best approach I could take here? If I can only look at one row at a time, how might I search this column?

**7:40:52** · You should use a linear search then, right?

**7:40:55** · So, I like your intuition. There is an algorithm, a step-by-step process called linear search where we look at one element at a time or in this case one row at a time. That's exactly what we can do for this table. I can look at one row at a time to find is this title in this column or is it not. So here to visualize I could take this title column. I can only look at one at a time. But if this data is not sorted, I can do no better than looking at every row exactly once.

**7:41:25** · So here we start with Toy Story. We ask, is Toy Story equal to Cars? It's not. So we'll keep going. Here I'll check Cars 3. Is Cars 3 strictly equal to Cars? I mean, it has Cars in it, but it's not Cars exactly. So I'll keep going. I'll look at Frozen. And Frozen is not cars either. So I'll keep going again. And here I see cars. So maybe I could stop here.

**7:41:53** · But why couldn't I? Well, if I need to find not just the one row that has cars, but all the rows that have cars, I have to keep going to see is cars elsewhere in this column. Is it not just here, but also in other rows, too? So, I'll keep going. I'll look at Wall-E, Ratatouille, Soul turning red until I get to the end of this column. And this process is called a scan of the table.

**7:42:18** · We're scanning our column top to bottom looking for the result that we need to find. But it turns out we can actually optimize this search. We can do a bit better than going one by one by one by one. And for this we need a bit of a a metaphor to think about how we can search our table. So if you have ever seen a kind of textbook, you might have seen something a bit like this here.

**7:42:44** · This is a handbook of education research. And maybe I want to find which pages correspond to how students learn computer science. So one thing I could do is open to the start of the book. I could go kind of page by page looking for which pages have how students learn computer science. I keep going here. And if I want to find all the pages that have how students learn computer science on them, I can do no better than going through everyone one by one by one until I'm at the end of this textbook. But chances are you yourself don't do this.

**7:43:20** · You do something better. And there's some built-in structure in this book that could help you find what you're looking for. What might you use to find something in a textbook or some other book, too? We can use the index of the book.

**7:43:38** · You can use the index. So often a book like a textbook has something at the very back of the book that tells me all the subjects that are inside this book but in alphabetical order. So I can see here there's a subject index in the back of the book here that lists the subjects in alphabetical order A to Z. And if I want to find how students learn computer science, I could perhaps search for computer science in this index. I could find A B C. Oh, there's C. And here I see computer science.

**7:44:04** · Now I know all the pages I need to look at inside this book without going through each of them one by one by one. So in the same way that books have an index, so too can databases and tables have an index as well. So let's see a definition here for what an index is. Well, an index is a structure that we can use. It's built into our database to help us speed up the retrieval of rows from that table.

**7:44:30** · I first search my index, find out what rows my given search term is in, and then look those rows up in my table. Now, if I want to create an index on a table, I can use some SQL syntax. I can say create index and give it some name. But I need to also specify a few other things like similar to my books index.

**7:45:00** · That index has some content. It's an index by subject or an index by author.

**7:45:06** · So I need to have tell this index what to include. So I should also say create index give it a name on some table and some columns in that table telling my index what data from my table it should include. So let's create our very own index in the movies table to identify how we can make this query just a bit faster overall. So I'll come back to my computer here and let's now try to create this index.

**7:45:34** · I will open up a new tab here, a new tab and then I'll log back into my database. I'll say SQLite 3 movies. DB. And now I want to first create some index here. So, I'll turn my timer back on. And now I'll type the syntax we just learned. I want to create an index. And if I'm searching my title column in movies, I should probably include the title column in this index.

**7:46:05** · So, I'll say call this the title index here. It'll be on the movies table and it'll contain the data in the title column of movies. A bit like this. Now I'll hit enter and I'll see this index took some time to be created. There's some stuff going on underneath the hood where I'm putting this data in a new structure. We're calling the index here.

**7:46:28** · But now if I rerun this query, if I say select star from movies, select star from movies where the title equals cars semicolon. It's a lot faster. Here I see 0.01. 01 seconds real time compared to 0.084 seconds. That's a savings of almost eight times like almost eight times faster now that we have this index. Now, it took some time to create the index.

**7:47:01** · If I run just a few queries, I much easily make that time up in terms of the time I'm using on my server to look up these kinds of pieces of information.

**7:47:13** · Okay, so let's actually take a look at how we can ensure a query is using some index. Here I just kind of taking it on my word like here it was faster so it used the index but there is a way for you to know whether an index was used. I could use a SQL statement called explain query plan.

**7:47:32** · Other DBMS's might call this just simply explain but in SQL write it's explain query plan and then after explain query plan I can type the query that I want to learn the plan for that is how does SQLite plan to find me this information how does it plan to execute this query so now I'll type select star from movies where title equals cars like this semicolon I'll hit Enter.

**7:48:01** · And now I don't get the results, but I do get the plan SQLite intends to use to find me this result. And take a look here. I see query plan. And underneath I see what SQLite intends to do. It will search the movies table, but it will do so using the index that we called title index.

**7:48:25** · And it will do so given some value for title here. So we can actually see SQLite does plan to use the index to speed up this query. We can confirm that this is exactly what's happening. But let me try now to remove this index and see what SQLite would have done when we didn't have this index. I'll come back over here and I'll go back to my other connection to my database. This one over here. And now I'll remove the index we just created. To remove an index I can drop it.

**7:48:57** · I can say drop index title index semicolon. And now that took it just a small amount of time, but now I don't have that index anymore. I can type dos schema and I'll see that that index is not part of my schema. But now if I try explain query plan select star from movies where title equals cars semicolon.

**7:49:25** · I'll see that the plan is not to use the index. The plan is to scan movies where scan we saw before means to go top to bottom through that title column and find me all the rows that have cars in them. So we can see here the optimization we're already making by using this index here.

**7:49:46** · Okay, so let's take a moment here and pause. What questions do we have about indexes and how they're used in this case? Doesn't uh databases have implicit algorithms to optimize search?

**7:50:01** · Yeah, good question. Do databases have implicit algorithms to optimize search?

**7:50:06** · They do for some columns. So if we saw in our table earlier, we had a primary key column like ID in SQLite and most other DBMS's. If I specify that a column is a primary key, then that database management system will automatically create an index v which I can search for a primary key. If though I have a regular old column like title or like year or so on, it doesn't go through the process of automatically optimizing that search for me. I have to do that myself as we're doing here.

**7:50:39** · Let's take one more.

**7:50:40** · Would it be advisable to create a different index for every column in case we need it? Yeah, I mean it seems like indexes are so good. They speed up queries for us. Why not create an index on every column we have? Well, as we'll see in just a moment, there are some tradeoffs involving space and also the time it later takes us to insert or add new data. So, good questions. I'll come back to my laptop where we can continue on. So, we've seen how uh indexes can speed up queries and we've we're searching for one column here, but they could also speed up queries across multiple tables.

**7:51:12** · So, let's try a different kind of query here. What I might do now is try to find all of those movies that Tom Hanks starred in. And we did a bit of a um example of this a little earlier visually, but my goal is to find all of those titles that Tom Hanks played a role in. Well, if my goal is to end up with titles of movies, I could try selecting title from the movies column like this.

**7:51:38** · But if I look at that movies table, I'll know I only have titles, year, and the ID of those movies. I don't have anything related to Tom Hanks. Well, Tom Hanks, though, is probably showing up in the stars table where I could correspond Tom Hanks's ID with the movie IDs that Tom Hanks played a role in. So, let me try filtering these movies by an ID. I'll say where the ID of that movie is in some list of movie IDs that also correspond with Tom Hanks's person ID.

**7:52:09** · So I'll make a subquery here to find exactly those films. Now I'll say select movie ID from stars where the person ID is equal to well I don't know Tom Hanks's person ID. I could try to hardcode it here, but I could do better by having another subquery to find what is Tom Hanks's ID.

**7:52:33** · Now I'll indent not just four times, but eight to show this is my next level of a subquery. Here I'll now select ID from people where the name equals Tom Hanks.

**7:52:46** · Tom Hanks like this. And now I can close out my sub queries. I've found the ID of Tom Hanks. I've found those movie IDs that correspond with the person ID of Tom Hanks. And then I found the titles that correspond to those movie IDs. Now I'll hit a semicolon here, press enter, and I should see I get back all of Tom Hanks's movies, all of those that he played a role in, and I'll also see the time that it took. The real time for this query was about 0.197 seconds.

**7:53:17** · So getting a little bit slower now that we're looking across multiple tables and having multiple sub queries. Well, an index could speed this up as well. I can make a um new terminal here.

**7:53:31** · And let me open up the connection in my database. Again, I'll say SQLite 3 movies. DB. And now I should figure out what columns do I need to index to speed up this query. Well, one thing I could do is try explain query plan. Again, I want to understand what SQLite plans to do to execute this query. So, I'll explain query plan and I'll type in the same query from before.

**7:53:55** · I'll say select the title from movies where the ID is in those movies that Tom Hanks played a role in. So I'll select in this case movie ID movie ID from the stars table where the person ID equals Tom Hanks's ID. Now I'll find that I'll indent eight times to show this is my next level subquery. I'll select ID from people where name equals Tom Hanks. And I'll wrap the line just a little bit.

**7:54:28** · Let me zoom out so you can see it all in one go. And now I'll close out these sub queries just like this. Hit enter. And I should see if I zoom back in the plan SQLite intends to use to find me the results of this query.

**7:54:44** · Now let's take a look here. I'm planning to first scan people. To understand the structure of this, I need to first go all the way in to this bottom part here.

**7:54:53** · I'm going to scan people to find presumably Tom Hanks's ID. Then after I do that, I'm going to scan stars presumably to find all the movie IDs that have Tom Hanks's ID. But then up here, I'm finally going to search movies using integer primary key. Some index is automatically created for me as we saw before for my primary keys. So it seems like the optimization here could be in the people table and the stars table.

**7:55:27** · Now let me ask if I wanted to create an index on either the people table or the stars table. What do you think I should include? Which column should I include in this index given my query here?

**7:55:43** · What column should I include in this index given this previous query?

**7:55:48** · We could index the uh ID and the name of the person.

**7:55:54** · Yeah, a good idea. index the ID and the name of the person. So if we look at this query again, we'll see that our wear clause here is um searching by the name in the people table. And up here, this wear clause is searching by the person ID column in our stars table. So it would stand a reason that I should actually create an index that includes the name column in people and the person ID column in stars. Perhaps two separate indexes, one for each here. So let's go ahead and create those.

**7:56:23** · Now I'll come back to my computer and here I will try to create this index. I'll say first create an index. Create index called person index. And I'll create it on stars and the person ID column in stars as we just discussed. Now if I hit enter, I should let it take some time to build up this index. But now I can also create my next one.

**7:56:52** · I'll say create index and then I'll choose name index on the people uh on people table and I'll include the name column here. So now I'll hit enter. That too will take some time to run. But now if I try to explain the query plan again I'll clear my screen try explain query plan and then I'll type in this query again.

**7:57:18** · I'll say select title from movies where the ID is in those movies that Tom Hanks played a role in that have the person ID next to it. Then I'll say um which is Tom Hanks's ID. And I'll close out this subquery here just like this.

**7:57:35** · And now if I explain the plan yet again I should see I'm now optimizing this query even further. I can see down below here, my plan is to search the people table. Not to scan it, but to search it using what we call a covering index called name index, the one we just created. We'll explain covering index in just a little bit. Next though, I'm going to search stars using the index we just created called person index given some person ID.

**7:58:03** · And then finally, I'll search movies using an integer primary key index, the one that's automatically created for me here. So here we see some new vocabulary, not just using index, but using a covering index. What is a covering index? A covering index, it turns out, is is still an index. It's the same kind of idea, but it is one in which we have all the data we need inside the index itself.

**7:58:31** · It's one in which the query data can be found only by searching the index. There's no need for me to go from the index to the table. I can just look it up in the index. It's similar to me searching this textbook and getting to the index and not then needing to actually go back in the book's pages, I can find everything I'm looking for in the index itself.

**7:58:53** · And this is good because if I need to not just find the items in my index, but then look them up in my table, like that look up in the table takes some time. So if I instead have a covering index, one that includes all data I want to find exactly right there in it, that's going to be faster for me than a regular old index. So let's try then turning one more index into a covering index.

**7:59:19** · I'll come back over here and we saw before that we had the um index on the stars table using just a regular old index using index person index. But what are we trying to find from this index? We're trying to find the movie ID column. So I could create an index that includes the movie ID column as well. I can have indexes that span multiple columns. So let's try that here.

**7:59:49** · I'll come back over and I'll create this new index that intends to cover our search here. I want to include not just the person ID column but also the movie ID column so I can quickly find that data inside the index itself. Let me drop our current implementation of the of the person index like this. I'll hit semicolon here. And now that index is gone.

**8:00:13** · But if I type now create index I'll also call this person index on stars. and I'll say let's include not just the person ID column, let's also include in this case the movie ID column like this. Now I'll hit semicolon enter and that'll take a bit of time to run but once it's done I can probably try to explain the query plan again and see if we have our covering index. I'll go back up top here.

**8:00:45** · I'll explain query plan and I'll choose to recreate this query from before just like this. going to select the uh movie ID from stars and then find Tom Hanks's ID and then close out these subqueries here just like this.

**8:01:03** · And now once I explain query plan, we've optimized even further. Now I have two covering indexes. I can find all the information I need just by looking in these indexes, not by doing a table lookup. So let's now run this query and see just how much faster it might be.

**8:01:24** · Come back to my laptop here and let's get rid of explain query plan. Let's now turn our timer on. I'll turn timer on like this and I'll rerun this query.

**8:01:33** · I'll say we select title for movies where the ID is in the stars table. So long as the movie ID aligns with the person ID. Then I'll find Tom Hanks's person ID here. I'll close out my sub queries and I should be able to find that this query is just a little bit there's an understatement here a lot faster. So if I go back to my old query here I'll see this one took 0.197 seconds. This one with two covering indexes takes 0.004 seconds.

**8:02:04** · This is an order of magnitude faster than my prior query because I've used indexes now. So let's see if we have all these benefits of indexes, we must be paying something like if I have this book here and I'm trying to find some data inside of it. What might the tradeoffs be? If I want to create an index, maybe think first about this database on my computer. What am I giving up?

**8:02:35** · I'm making sure my query is faster. What am I losing? Do you think space we required for indexing also the more index we would have the more space and more memory we would have to consume for that?

**8:02:49** · Yeah.

**8:02:49** · Uh so it's a general theme that when I try to speed up something in computer science I have to pay some cost which is often in terms of space that when I create an index I'm using more space in my database and this similarly applies to a oldfashioned textbook like if I have an index in here I'm literally paying in pages to print so people can find content better. This is some extra money I have to spend, extra pages I have to print in order to make my queries faster either on this book or in my database.

**8:03:19** · So let's understand why indexes take up so much space by looking at the underlying data structure they use to store information. Well, it turns out that the part of the reason indexes take up so much space is because they use a certain data structure, a way of organizing data called a B tree or a balanced tree structure. So, not to worry if you don't know what a tree structure is.

**8:03:45** · Here's a visual to keep in mind as you think about using trees in computer science and in indexes in particular. A tree might look a bit like this. And notice how it's similar to a family tree with grandparents and parents and children and so on. You could, if you wanted to, kind of do a 180 on this diagram, flip it right side up. And now you might see more of a tree structure going from top to bottom.

**8:04:08** · You could see down here, what we might call the trunk of the tree, followed by some branches, these over here, and then the leaves, these up top, kind of the edge of this tree diagram. And there's a few vocabulary words you might want to know when you talk about trees. One of them is this idea of a node. So this right here is a single node in our tree. A tree is made up of a collection of nodes. And each of these nodes stores some value.

**8:04:39** · Maybe it's a value in the column we're trying to index, for example. But in addition to that value, this node also stores pointers, kind of arrows metaphorically, to other nodes to tell us where in memory these nodes are.

**8:04:58** · And by stringing these nodes together, we can build up this treel like structure. Now, this node here points to three other nodes. And some new vocabulary here is that this node has three children. Going back to that family tree example, we see that this node here has three children, which are these right here. But these nodes themselves also have three children of their own.

**8:05:22** · So if I were to go down to the next level of our tree, well, if I'm referring to this node here, these nodes down below are that node's grandchildren, the children of its children. Now, these nodes here also have another name. We saw it before.

**8:05:39** · They're often called leaf nodes. or the edge of our tree. And we know a node is a leaf node when there are no other nodes it points to. So this is the general idea of what an index looks like. But let's get a little more concrete and try to build an index from our title column in our movies table here. So let's assume we have a table of ids and titles here. And I want to create an index on this title column to search it more efficiently.

**8:06:08** · Well, we saw before that the best I can do when this data is unsorted is to go top to bottom.

**8:06:16** · First look at Toy Story, then look at Cars 3, then look at Frozen, all the way down to the bottom. I can only scan this column, so to speak. But I know I could probably do a little better if the data is sorted. If the data is sorted, I could look roughly in the middle and if I've gone too far, go back a little bit.

**8:06:34** · or if I haven't gone far enough, go forward a little bit and do a fewer number of lookups to find the I'm looking for. So, let me sort this title column. I'll put it like this.

**8:06:46** · What have I done wrong?

**8:06:49** · First, I had this. Then, I wanted to sort my title column to make it faster to search.

**8:06:57** · But what did I what rule did I break here by sorting this title column like that?

**8:07:03** · Yes, Carter. The thing is that by sorting only the movie's name and not the ID, you will break uh the entire other databases that relates to that one. So for example, let's look for a movie in which I don't know Johnny Depp is working or has work done and the result may be I don't know Titanic.

**8:07:23** · Yeah, I love that example that really drives it home here. And in more general terms like I had this primary key called ID and in the prior state I had Toy Story with the ID of 114709. A primary key means that Toy Story should be consistently identified with this number 114709. But to your point Matteo, if I sort only the title column, well now cars has that ID 11479, I've broken that relationship.

**8:07:56** · particularly if other tables are relying on uh Toy Story being identified by 1 14709. So I can't do this. This is bad. I need some other way to sort my title column. So let's bring this back to what it was here. Let me focus just on the title column. Well, I can't sort this title column because it's part of my table and the ordering of that table does matter.

**8:08:24** · What I could do though is create a copy of this column and maybe sort that copy.

**8:08:29** · So I'll literally create a copy of this title column elsewhere in memory. And let me just remove this title column identifier here. So I have just the data, just the data in this column somewhere else in memory. And now I could sort this data like this. So let's say I now want to find cars. Well, now that my data is sorted, what could I do?

**8:08:51** · I could look first in the middle at Ratatouille, for instance, and then realize, well, cars comes before Ratatouille. Maybe I'll go a little higher in my index here. I'll search in the middle of this first half. I'll look at, in this case, Frozen. And cars, well, it still comes before Frozen. So, let me look up at the first half of this first half. I'll then go up here and I'll have spotted cars. So, a much faster way to search for information now once I have it sorted.

**8:09:21** · But I don't think we're quite there yet.

**8:09:23** · Like if I wanted to find the year that cars was released. I found that it's in my title column. But what am I not able to do at this point? I've copied the data somewhere else. But now I want to find some other data in my table. What can't I do?

**8:09:43** · We need to point to index. Yeah, I need to be able to find some way to relate this index with the rows in my table. So here, this is elsewhere in memory. It's good that I can find that cars is in my title column. But if I want to find the other data in this row, like the year that cars was released, well, I have to have some way of linking this uh this data here, cars, to my table.

**8:10:07** · So often in an index, we not just copy the data to some new location and sort it. will also have some link between these index pieces of data over here and our rows in our table back here. So for instance, here is cars and cars appears to be in row four. Similarly, cars three looks to be in row two in my table and I could metaphorically visually draw some lines between cars over here in my index and cars in my table.

**8:10:40** · I could draw one that looks a bit like this. Going from cars, my index to actually cars in my table. I could draw one for cars three going from this index place here to row two in my title column. So that is the way I can link my index with my table data. I could do the rest of these two for all of my other pieces of data in my index.

**8:11:06** · So let's focus on this now like just to check for understanding. I have this index. That index has my sorted title data and also the row number in which I found that piece of data. So let's say here I want to find the movie soul. I want to find the movie soul. How could I find soul in my index?

**8:11:31** · Yeah, since it is already sorted, I believe you could use binary search.

**8:11:36** · Yeah, I could use algorithm called binary search. which if you're not familiar simply means start in the middle and if I've gone too far look in either the left half or the right half and repeat that process over and over. So here is my index again. I'll go roughly to the middle and I'll look at Ratatouille here. Well, soul I know comes after Ratatouille alphabetically.

**8:11:56** · So what should I do? I should now look in this second half here. I might go to Toy Story. Well, once I see Toy Story, I know I've gone a little bit too far. like soul comes before Toy Story alphabetically. So I'll look in the first half of this second half and what do I see? I see soul right there. Okay, so our index seems to be working. It allows me to more efficiently find data.

**8:12:22** · I no longer have to look through every single row. I can simply use a more efficient algorithm like binary search.

**8:12:30** · But now there's one more catch, which is if I had many, many, many rows, not just nine, but literally thousands or hundreds of thousands or millions of rows in this index, like that's a lot of data to store in one location in memory or even to load into my computer's RAM, so to speak. It's random access memory, so it can do all this jumping around.

**8:12:54** · Ideally, what I would do is break this index up into smaller pieces. So, I don't have to load all of this at once.

**8:13:01** · And in reality, our index is not a single column like this, but often individual nodes where each of these 1 2 3 might be some node scattered about the computer's memory. But what problem have I introduced now? If these are around the computer's memory, I can't actually jump between them anymore. I can't go maybe one space above Toy Story and find Soul. This node might be elsewhere in memory.

**8:13:29** · And so, we'll need some other nodes to actually help us find what we're looking for in this index. I might have one more over here that tells me what kind of data is in each of these nodes. Maybe I have one here that has both frozen and soul. Notice how here frozen is the furthest down alphabetically in this node up here. And notice down below here, soul is the furthest down alphabetically in this node here.

**8:13:59** · That is, if what I'm looking for comes before frozen, I should look at this node. If what I'm looking for comes after frozen but before soul, I should look in this node. Or if what I'm looking for comes before none of these, it comes after soul, I should look at this node down here. So let's find an example. Let's say I want to find cars now. Well, I'd start in this root node, the face of this tree we're building here that I've turned kind of right side this way. Let's say frozen.

**8:14:30** · I'll go here. And does cars come before Frozen?

**8:14:36** · Well, it does. So I'll look in this node now. I'll come up here and I'll find cars in that node. Let's see here. Maybe I want to find Ratatouille. I'll go back to the beginning and I'll look through this par this root node. I'll say, does Ratatouille come before Frozen?

**8:14:54** · It doesn't. It comes after Frozen. So, I'll look and check soul. Does Ratatouille come before Soul? Well, it does. So, I'll look in this node now.

**8:15:03** · I'll go find Luca. And not quite there yet, but I will see Ratatouille. So I know that I've now found Ratatouille in my index. And now for one more, let me check for understanding here. How could I find turning red? What steps would I follow to find turning red? I might start at that root node, but then what questions should I ask from um frozen or so? We can see uh rather two to the right.

**8:15:33** · So that we move in the direction of so and once we get there we find the middle elements and we can see two ways to the right of um the middle element. So that's how we find it. Divide the list into two halves and look into the half that the element is found.

**8:15:55** · Yeah, I like what you're thinking here.

**8:15:56** · So you're talking about traversing this tree we've built and turned on its side here. And let's visualize that search here. So, first we'll start at Frozen and ask, does Turning Red come before Frozen? It doesn't. It comes after. So, I'll keep looking. I'll look at Soul.

**8:16:12** · Does Turning Red come before Soul? Well, it doesn't. It comes after Soul. So, I know I need to look at this node down here. I'll go find Toy Story. Not quite there yet. But now I'll see Turning Red. I'm able to find what I'm looking for.

**8:16:27** · And not just that, I can find what row number Turning Red is actually in. in my table. So when you use an index, SQL or SQLite is using some algorithm a bit like this. It creates some tree structure a bit like this here with individual nodes that has your column data. It then uses this kind of algorithm to search that index and find whether or not that piece of data is in your index. And if it is, it will go ahead and look up that piece of data in your table.

**8:16:57** · So see here, although this is turned on its side, the relationship between a kind of tree, we had a root node or a a trunk node here pointing to some of these leaf nodes, the edges of our graph right here. And you can see some relationship between these nodes here and our tree as well right here with arrows pointing across these individual nodes.

**8:17:23** · So let me pause here and ask what questions do we have on this structure and how we've searched it.

**8:17:30** · Uh is that related to linked lists or arrays?

**8:17:35** · Uh good question. Is this related to linked lists or arrays? So if you're familiar, a linked list is some set of nodes that have been linked together in memory using these arrows like we saw on our diagram here. It is the case that sometimes an index will include a linked list.

**8:17:54** · Let's take one more here. I want to know uh covering index what how is the create covering index and uh what I mean if we just first we saw example index and then we saw covering index how SQL automatically get that covering index

**8:18:16** · that's yeah we're asking how is the index created like what is the process for doing that well it turns out that just as we saw here in the slides SQLite or whatever DBMS you're using will take a copy of the data that should be in that index and organize it into a tree structure like we saw here. It may or may not be similar to the structure we saw just a little earlier with nodes that have different pieces of um row data in them. But good question there.

**8:18:44** · Okay, so we've seen now the tradeoff that we get with index which is they're very fast to look up some data but they take up a lot more space. There's a lot of redundancy to them here. There's also one more trade-off, which is if I want to insert something into this structure, it'll take me more time. I have to navigate this structure here. I have to figure out should it come before this v this this value or after this value and I'll have to traverse this tree every time.

**8:19:13** · Versus without an index, I could just add something to the end of this list. But with a B tree with an index I need to traverse all these nodes to figure out where should that piece of data go. So these trade something you should keep in mind as you build indexes and optimize your queries.

**8:19:30** · Okay. There are ways though to actually optimize the space that we use using a tree like this. We can use a structure called not an index but a partial index.

**8:19:42** · And if you're concerned about space, a partial index might be good for you. A partial index only includes a subset of the data from a given column, thus making your index smaller overall. You can think of a partial index being useful when you know that your users will only query a subset, only a small number of rows from that table.

**8:20:03** · And for example, in IMDb, maybe we know people are more likely to search for a movie that came out this year versus someone that came out in like 15 years ago or so. So, we could create an index that focuses on those movies that came out this year versus 15 years ago or so. And we'll do just that. If I want to create a partial index, I can use this syntax here. I could say create an index and give it some name.

**8:20:32** · Then include some data from this table and this column here or list of columns I can provide. But then what I need to do is add a condition where some condition is true.

**8:20:46** · These are the rows I want to include in this index. Before we had just create index name on table, some list of columns. Now we can add in this wear clause that says only include those rows where this condition is true. So let's try that now. I'll come back to my computer and why don't we try creating a partial index to help speed up the um lookup of movies that came out this year. I could come back to my terminal and I could remove let's say this one over here.

**8:21:18** · Now I'll try to create this partial index. I'll say uh create an index called recents to indicate this will help us search for recent movies. Now I'll make this movie uh recents on movies and the title column. I want to look up titles ultimately. But now I only want to create an index for those rows where the year equals 2023. I only want to include those titles in my index that were released in 2023.

**8:21:54** · So I'll hit enter now and I'll see I created this index for myself here. Now let me try searching for those. I'll select title from movies where the year equals 2023. Enter. And I'll see a lot of movies came out in 2023. Almost one uh almost taking 1.3 seconds here. But now I could prove to you that we are using some index. I could say explain explain query plan.

**8:22:21** · And now type select title from movies where the year equals 2023. Hit enter. And now we'll see what are we doing. We're going to we'll st scan movies, but we're still going to use the index we just created called recents. So it's helping speed us up just a little bit overall. Now, let me try dropping this index and showing you the opposite. I'll come back over here.

**8:22:50** · And I could try dropping it. Actually, before I do that, let me show you what would happen if I didn't search for movie in 2023. I would try explain query plan. And let me try select title from movies where the year equals 1998 like this. And see now I'm only back to scanning movies. So before in my prior query I was able to use the index because my wear clause included 2023.

**8:23:22** · Now though I'm using 1998 which were rows that were not included in this partial index. Okay. So let me ask now what questions we have on these partial index which we can use to optimize some of the space these indexes take up.

**8:23:40** · Why index is not saved in schema?

**8:23:43** · A good question. Are indexes saved in the schema in SQLite. If I type schema I can actually see them in my schema. So let me go back here and show you. If I now type something like let me turn timer off here. Dot schema. You can see down below here that I actually have these indexes as part of my schema. I'll see the create index statements I used down below here. Create an index called name index called person index called recents. And all that I use to create these indexes now inside my schema.

**8:24:13** · If I drop some index, it'll then be just removed from my schema altogether.

**8:24:22** · Good question.

**8:24:24** · Okay, so speaking of dropping indexes, one other way we can more efficiently use space is to a bit of vacuuming, so to speak. So let's introduce this idea of vacuuming up our database. Let me show you a slide here. And um this one involves this idea of trying to clean up unused space in our database. Often when we delete something, either a rows or an index, we don't actually delete those bits that were being used by those rows or that index.

**8:24:55** · We just mark them as being available for whatever we next insert. They can be overwritten, so to speak. But if I want to actually reduce the size of my database after I delete something, I should use something like vacuum in SQLite or optimize in some other DBMS. Vacuuming is a bit like taking those unused bits and just like sucking them up, taking them back in so we can give them back to the operating system. And the keyword we can use for vacuum is just simply vacuum. So let's try this.

**8:25:27** · So, I'll come back to my computer over here and let me open up a new terminal, one that I can use to find the current size of movies. DB. So, I'll hit this plus button here. And now I could type a command, not a SQL command or SQLite command, but actually a Unix command. I could type du-b for the disk usage in bytes. How many bytes is a particular file? I could then say movies. DB here. And if I hit enter, I should see movies. DB is something like 158 million bytes or 158 megabytes.

**8:26:04** · So let's see what happens if I were to delete an index, which you know takes up some amount of space in our database. I'll go back to my terminal here and let me try to drop an index that we had recently created. I'll say drop index person index to remove the person index.

**8:26:21** · In this case, I'll hit enter. And now I see that person index is dropped. If I type dot schema here, I no longer see it in my schema down below. So now let me check the disk usage in bytes and see if it's any smaller. I'll hit the up arrow to get access to that same command. Hit enter. And it seems like it's the same size. It's still 158 megabytes. So let me try dropping something more here.

**8:26:47** · I'll go back to my terminal here. And now I'll try what other do I have? So I have um I have name index. So I'll say let's drop index name index like this.

**8:26:57** · I'll hit enter and I'll see that that index is now gone. Well now I'll also try dropping recent. I'll drop index drop index recents. And now I believe all of my indexes should be gone. If I type dos schema, I don't see any more indexes. So now let's check on the disk usage in bytes. I'll go back to my other terminal. Hit du-b again and it's still 158 megabytes.

**8:27:25** · Well, what could we do to clean this up?

**8:27:28** · We could run vacuum. If you remember here, when we delete an index, we drop the index. We don't actually shrink our database file. We just mark those bits that were part of the index as being available for reuse. So, let's now vacuum and compress our file to give back those bites, those bits to the operating system. I'll come back to my terminal here and type vacuum semicolon.

**8:27:53** · Hit enter and I'll wait for it to find those bits and bytes. Wait for it to give them back to deallocate them to go back to the operating system. And now if I come back and I type du-b again, hit enter, I should see a much smaller file. So before we had about 158 million bytes. We're down to in this case 100 million after dropping our indexes and using vacuum.

**8:28:20** · So let me ask now what questions do we have on vacuuming?

**8:28:25** · Can we do vacuuming in a faster way?

**8:28:27** · Can you vacuum in a faster way? Uh so I think it depends on the size of the vacuum that you're trying to implement here. If you have a lot of bits and bites you're trying to deallocate that could take more time. I mean the process here is the computer has to find those bits and byes you're no longer using and then give each of those back to the operating system. So it could depend on the size and how long they take to find.

**8:28:51** · Let's take another question here.

**8:28:53** · Initially you said once we drop a database we don't lose the the data is not deleted. It's just uh the space is just uh reallocated right if if I got you right. So, does that mean um the queries we run today, are they locked somewhere that let's say you mistakenly did a a query, you can go back and pull that data back? Is it is that possible?

**8:29:19** · Kind of like a reversal of a a query.

**8:29:22** · Yeah.

**8:29:22** · So, you're talking about some forensics here, like could we mark something as deleted but still find it later? Um there actually are uh people who are trained in this in forensics to find pieces of data that you thought were deleted but are actually still on your computer just kind of um forgotten if you will. In this case in SQLite it would take a lot of work to go ahead and find all of those bits and bites we've removed.

**8:29:44** · Um but once we vacuum once we actually give them back to the operating system we can no longer find those in the database because they're not just marked as being deallocated they actually have been given back and they're no longer part of our database.

**8:29:58** · Good question there. Okay, so we've seen here how we can optimize our queries by reducing the time that they take, although at the cost of some space. When we come back, we'll see how we can handle not just one query at a time, but many all at once. See you in a bit. And we're back. So we've seen so far how to optimize individual queries, ensuring they take less time and also to ensure our databases use as little space as possible.

**8:30:27** · What we'll focus on now is trying to ensure we can handle not just one query at a time but multiple all at once. And this is this idea of concurrency. Concurrency is when I get multiple queries, multiple interactions all at roughly the same time and my computer system, my database needs to figure out how to handle all of those at once. This is particularly important for websites get a lot of traffic or even for the financial sector. People are constantly making trades, placing orders, exchanging money and so on.

**8:30:58** · So let's see one example here of a bank.

**8:31:05** · Let's say here I have a table of accounts and each account has a name and some balance to it. Well, we decide here that uh maybe Alice wants to pay Bob $10. So, what should I do to update the balances here? Maybe the first thing I should do is make sure that Bob receives that money. I could update Bob's account to have a balance not of 20, but of 30.

**8:31:30** · Now, from 20 to 30. But here's the thing. If at this moment somebody looks at this table, what will they see that's wrong?

**8:31:42** · What will they see that they might not get the right picture of? At this point, I'm hearing they might not see the correct balance for Alice. Like Bob has gotten some money. He's gotten he's gone from 20 here to 30. But now I have not just let's see $60 in the bank. I now have 70 it looks like. So somebody looks at this transaction in this moment, they'll see some incorrect information.

**8:32:10** · What I should then do is update Alice's balance subtracting 10. So we're at the right amount of dollars across our bank accounts here. So this is an issue. When I have one ongoing transaction like this and somebody else wants to look at that data, they really shouldn't be able to until this transaction is complete in its entirety. So ideally, let's go back to what we had before with Alice at 10, Bob at 20. Ideally, if Alice wants to pay Bob, this should happen to an outside observer all at once.

**8:32:41** · Bob should get those $10 and Alice should lose those $10 at the same exact moment. So nobody can look and see that Bob has more money while Alice doesn't have less money. Now we can implement this idea of this transaction using a very similarly named idea in databases called a transaction. Now a transaction in the world of databases is an individual unit of work. That means a transaction can't be broken down into smaller pieces.

**8:33:14** · It happens all at once or not at all. And in fact, a transaction has several properties and helps implement several properties of a database. Among these are ACID, AC, CI, D. You may have heard of these if you've looked up some about databases. But each one stands for some principle of ensuring a consistent and reliable database. In fact, A stands for atomicity, which means I can't break a transaction down into smaller pieces.

**8:33:43** · I can't break a transaction between Alice and Bob into Bob's update and then Alice's update. It's just update both accounts at the same time. Consistency means a transaction help me ensure that I don't violate some database constraint. Let's say I try to pay Bob from Alice's account, but Alice doesn't have the money. If that is the case, a transaction will revert, undo. So I go back to being in this consistent state for my database.

**8:34:14** · Isolation means if I have more than one person trying to access this database, their queries, their transactions won't interfere with each other. And then finally, durability means if I were to unplug this database were to encounter a power failure or the server were to crash, all that data would still be there from the time we committed our transaction or saved the results there. So transactions do a lot for us, but they have some very simple syntax.

**8:34:45** · I can simply use begin transaction and then follow it up with some statements I want to include in that transaction. And once I'm sure I want to save the results of these statements, I can then say commit, meaning save these changes thus far. And it's using this kind of syntax we can ensure that nobody sees incorrect balances. Let's say for this bank account um table here.

**8:35:10** · So let's try this out and implement a payment between Alice and Bob, but now using a transaction. Come back to my computer here and let me show you a new database. I'll type SQLite 3 bank. DB. I'll hit enter and I'll SQLite 3, sorry, bank.db.

**8:35:32** · I'll hit enter. And now let me type dot schema to see the schema of this database. I'll see here a few different columns that I have an ID column, my primary key, a name column like we saw in our slides that is text and can't be null. And then a balance column. There's an integer, a whole number of dollars that also must have a value can't be null. And I have a check constraint here saying the balance must be at all times greater than or equal to zero.

**8:36:00** · So this is our implementation of a table of bank accounts. Let me try querying here to see what our account balances look like. I'll say select star from accounts semicolon. And now I'll see that very same arrangement we saw in our slides. Alice has $10, Bob has $20, and Charlie has $30. So let me try then processing this transaction between Alice and Bob.

**8:36:31** · Well, at this moment, I might try to update Bob's account. At the first bat, I'll say, uh, let's try update and update the accounts table. Set the balance equal to balance + 10, where the ID equals 2. Remember, Bob's accounts ID is two. So now, if I hit enter here, Bob should have gotten just 10 more dollars. But there's a problem. If I also connect to this database to another connection here, SQLite 3 bankdb.

**8:37:04** · Maybe I'm somebody who's checking on the balances of the bank. I say select star from accounts.

**8:37:11** · What do I see? But an incorrect total balance. We should have $60, but here I see 70. So I need to complete this transaction to ensure that I actually have the right amount of balances across the board. Let me go back here and let me try to run the next part here. I'll change let me update this. I'll say update accounts and I'll set balance equal to balance minus 10 minus 10 where the ID equals in this case 1 where Alice's bank account ID is one.

**8:37:43** · Now if I hit enter, I should be able to go back to my other terminal and check on the balances again. And now I'll see the right balances all together. But there is a way to avoid me looking at this table and seeing an incorrect state. And that's the way to do that is called a transaction. So let's go back here and I will reset my terminals. I'll now also give back Alice's money. I'll say um let me give back Bob the $10. Let me go back give Alice back $10.

**8:38:15** · I say where ID equals one here. Now Alice will have 10 more dollars. And I'll go back and I'll update accounts. I'll set um the balance equal to balance um minus 10 where the ID equals 2. So I'm giving Bob back the $10 that they just gave to Alice. Now if I select star from accounts, we're back to where we began.

**8:38:39** · So ideally I should be able to complete this transaction between Alice and Bob without somebody seeing the intermediate process of Bob having more money than Alice. So let's try this. I'll say begin transaction semicolon. Enter. And now I can include what I want to have happen in this transaction. First I want to update Bob's account.

**8:39:04** · I'll say update accounts and set balance equal to balance + 10 where the ID in this case equals let's see two because Bob's account ID is two. Now I'll hit enter. And now I'm in the middle of this transaction. But if I go to my other terminal, let's say I'm somebody new and I check on the balances of the bank. I say select star from accounts.

**8:39:33** · What do I see? I don't see any change from before. Alice still has $10, Bob has $20, and Charlie has 30. And even though in this terminal, I've been able to update the account balance, I haven't committed those changes. I haven't saved them to the database just yet. So, let me try now removing money from Alice's account. I'll say update accounts and set balance equal to balance minus 10 where the ID equals 1. Now I'll remove $10 from Alice's account. Hit enter.

**8:40:05** · And still if I go back to this other perspective here from somebody else checking on the bank balances, I see well everything is still the same. But the moment I then go to this transaction and finish it by typing commit, meaning save these changes, I'll commit here. I can go back and I'll see all in one moment that it appears Alice has paid Bob $10.

**8:40:33** · So this is the atomicity part of transactions. I don't see the intermediate steps in the transaction. I only see that it happened all at once or not at all. Okay. So this is one example here of a transaction. Let me ask what questions we have so far on the transactions we've made and how they can be used.

**8:40:58** · uh I mean you are searching based on ID like ID is equal to question mark but uh in a real world scenario how they will search maybe like using the transaction ID or basing the account number like uh good question so here I'm searching by ID I'm saying that I want to update the balance of account with ID 1 or ID2 for instance and this is similar in spirit to how your bank account likely has some unique number an account number so to speak so here In this table, I'm updating balances by referring to the account number.

**8:41:30** · You could imagine me using names, but there might be in some world multiple Alice, multiple Bobs. So, I should uniquely identify each account using its ID in this case. Okay. So, let's come back and think through more kinds of transactions here.

**8:41:47** · And let's think through a transaction we actually don't want to complete. So, let's go back to our balance sheet where we have Alice at $0 and Bob at 30. And let's say Alice wants to pay Bob $10 more. Well, if I go through this transaction, what's going to happen?

**8:42:07** · Alice will have $10 and Bob will have 40. That violates our check constraint that we saw in our schema. The balance of Alice's account must always be at least $0.

**8:42:20** · So if I were to complete this transaction that would bring our database to an inconsistent state. It violates some uh constraint that we have. But what I can do is undo these changes, revert them so that we go back to the original state if we ever violate some constraint like we just did.

**8:42:41** · There's a technical name for this which is rolling back. So if I ever want to not save the changes in this transaction, I can say roll back. Go back to the beginning. Think about it as if this transaction never even happened at all. So let's try this. I'll come back to my computer and what I'll do is try to implement this idea first without a transaction. I'll go back to let's say this first terminal here and I'll select star from accounts like this. Notice how Alice has zero dollars and Bob has 30.

**8:43:17** · Well, I want to pay Bob 10 more dollars from Alice. So, I'll update Bob's account. I'll find here my prior um my prior statement. Update accounts set balance equal to balance plus 10 where the ID equals 2. And recall that Bob's account ID is two. I'll hit enter. And now if I select star from accounts, we're looking somewhere else. Select star from accounts.

**8:43:42** · I'll see Bob has 10 more dollars. But now I need to subtract money from Alice's account. So I'll use the same thing, but now I'll say minus 10 where the ID equals 1. Alice's account ID is one. Now I'll try to subtract $10 from Alice. But I get a constraint failure here. My check constraint failed on the balance column. Well, why did it do that? because I now have less than $0 in that balance column. So, I need to undo this.

**8:44:16** · But I don't have a transaction here. What could I do instead to undo what I've just done?

**8:44:25** · So, we can roll back.

**8:44:26** · We could roll back. But here's the thing. A roll back only works while we're inside of a transaction. And a transaction begins when we say begin transaction. So here I actually didn't say begin transaction. What I have to do instead is run another update statement.

**8:44:43** · I have to update um let's see uh Bob's account to remove the $10 that Alice paid Bob. So let's try that. I'll come back to my computer and I will then revert back. I'll say let's undo this.

**8:44:56** · Let's subtract $10 now from Bob's account where the ID is two. Now we're back to where we began. If I check in from some other detection here, I'll see we're back to Alice having zero and Bob having 30. But we ideally want to use roll back to undo some changes that we had made in a transaction. So for that, let me now use a transaction. I'll say begin begin transaction like this. Hit enter. Now I want to update Bob's balance.

**8:45:28** · I'll say update accounts set balance equal to balance plus 10 where the ID where the ID equals 2. Bob's account ID is two. Now let me subtract $10 from Alice like this minus 10. I'll go back here and say where the ID equals 1 for Alice's account. Hit enter. But now I get that same constraint failure.

**8:45:51** · Alice has less than $0 which can't be possible. So what do we do? Instead of having another update, we could just roll back. We could undo all of these previous statements here. Roll back like this. Hit enter. And now I should see from another perspective here my table exactly as it was before with no intermediate step of Bob having money but Alice having -10.

**8:46:17** · So let me ask now we've seen commit and roll back. What questions do we have on transactions? now. Okay, seeing none so far. So, let's keep going. Um, transactions are helpful for ensuring that our data is consistent like we just saw and that they're also we have atomic transactions. We can't break things down into smaller pieces.

**8:46:46** · But there is a case that transactions can help guard against some adversarial kind of attack where we run into what we call race condition. A race condition is when we have multiple people, multiple processes trying to access some value and also making a decision based on that value. If unressed, it can lead to a scenario that's inconsistent in our database. And actually hackers can exploit race conditions to bring our database to an inconsistent state in a way that benefits them.

**8:47:16** · So let's say our friends uh Charlie and Alice here, they decide to rob our bank. They decide to take money from it by exploiting race conditions. And here are the logs of what Charlie and Alice actually did. We see here that Charlie and Alice executed three concurrent transactions with our bank. On the one hand, Charlie opened up his bank account on two different computers. He logged in and he said, "Let me transfer $30 to Alice."

**8:47:45** · He at the same time clicked transfer on both computers. Knowing just well he had only $30 to give to Alice, but he was going to send her 60. In this case, he was hoping that we weren't guarding against race conditions that he could send $30 on both accounts to Alice. Now, at the same time, Alice is at the ATM, and they're hoping that at the same time Charlie Price's transfer, Alice hits confirm on their transaction to withdraw $60 from the ATM.

**8:48:15** · And when all of these happen at once, we might run into some inconsistent states in our database. Let's say first we run this transaction here. Let's focus on this one. The first step is to check Charlie's balance. Does Charlie have $30? It seems like Charlie does. We continue. We might say, "Okay, let me add $30 to Alice's account like this. Then let me subtract $30 from Al from Charlie's account down below here."

**8:48:42** · And finally, that's the end of our transaction. We checked Charlie's balance. We added $30 to Alice and subtracted $30 from Charlie.

**8:48:52** · But now, at the same time, we're also processing the other transfer of $30 to Alice. So here, we check in terms of our time top to bottom here. We check Charlie's balance at this point. It's still $30. Knowing this, this process goes ahead and says, "Let's add $30 to Alice's account." And now, only later, let's subtract $30 like this. Now, Charlie will appears to have no money in his account.

**8:49:21** · But at this time up above, we've already sent $30 to Alice's account two times. And if Alice is waiting at the ATM over here and they press confirm on that withdrawal, what might happen is something like this. At that moment that Alice has $60 in their account, they check and they see it.

**8:49:39** · They could then withdraw that $60 and now that money is gone from our bank, even if we realize Charlie shouldn't have been able to make that transaction happen.

**8:49:50** · So what logically is a solution here? It seems these transactions happened all at the same time. But what would you do to reorder these statements to make it clear that we can only do one at a time? What would you do in this case to update this table to fix this problem?

**8:50:12** · I would group um the withdrawal and the debit as um one transaction. So the subtraction is done and the addition is done as one unit of work in order for the double transfer not to happen.

**8:50:29** · Yeah.

**8:50:29** · So ideally we should treat each of these as a separate transaction literally a transaction in the database sense where if I go back to this table if Charlie transfers $30 to Alice at roughly the same time I should handle these sequentially. I should first do this one, then I should do this one, and only after that should Alice be able to withdraw their $60, or at least try to in this case. So, we need to make these transactions sequential. And the word for this is isolating our transactions.

**8:50:59** · Here, they are not isolated. They're working at the same time, but in reality, I want them to be isolated, happen one after another after another.

**8:51:08** · So, ideally, our table looks more like this. Charlie hits transfer at the exact same time on two laptops, but because we're working in transactions, we only process one first. We start with this one here. We check the balance. We say, let's add 30 to Charlie to Alice's account and subtract 30 from Charlie's.

**8:51:29** · Once we're sure that is okay, we'll commit the transaction. And that is a done deal. Now though, we'll go down below. We'll say begin transaction.

**8:51:39** · We'll then say Charlie's balance is $0 because we're doing this after we did our first transaction. Charlie has no more money to give Alice. At that point, what we'll do is try to add 30 to Alice, but subtract 30 from Charlie. And we'll realize, well, we made a mistake. We should roll back and undo what we just did here. So, these now are separate transactions happening sequentially. And we avoid our error of giving Alice $60 when she shouldn't have that money at all. And then only after this is done do we let Alice try to withdraw $60.

**8:52:11** · We'll go over here and see. Alice tries to have a balance of $60. Withdraw 60 and commit it. But at this point she wouldn't actually have that money there.

**8:52:23** · So let's see now what questions do we have on the way transactions are sequential. In this case in practically I want to ask that there millions of transactions are going on the practically also is it like that that sequentially this is these transactions are being handled for example financial transaction or any other because you know there are a number of banks in a single country or international transactions are they handled sequentially or there is some parallel handling mechanism also exist if you may please clarify.

**8:52:55** · Yeah

**8:52:55** · good question. And so here visually we see these transactions are actually sequential in the operation here. And I think your question is are they literally sequential like one after another after another. In reality they are very much just sequential like this.

**8:53:09** · A database can get creative with the use of locks we'll see in just a minute. But by and large they are sequential one after the other. And it's the job of a database module to ensure that these transactions are executed sequentially in an isolated way. Good question.

**8:53:25** · Okay, so let's see now how if a database is able to make these sequential, it must be using something underneath the hood to ensure that these transactions don't interfere. And in SQL light and other DBMS's we use this idea of a lock on database to ensure people can't access data when they really shouldn't be able to. So here let's take an idea of what SQLite has as different kinds of locks on this database. We have a few different kinds, unlocked, shared, and exclusive among some others here.

**8:53:57** · Each one has a different meaning for different processes. Let's take a look here at our bank account table. Let's say two computers want to access this accounts table. Well, at this time, because nobody is accessing our database, it is unlocked. Anyone could read from the database that is see what's inside or write to it, add some data, or update some data. But let's say we have one computer here who wants to read from this database. They want to see what data is inside.

**8:54:27** · Well, that database in SQLite would acquire what's called a shared lock like this. They're able to read the database, but also still allow others to read as well. A shared lock means I'm only reading. You too could read as well. So, let's say this computer comes in. they decide to read from this table, they could acquire the same shared lock. And because we're only reading, not updating, multiple transactions can read all at once.

**8:54:59** · We don't have to make these sequential. But if we have a transaction that's hoping to write to the base to update some value, well, that's when things get a little weird. I can't let somebody else read my data while I'm updating it.

**8:55:18** · So what I need is for this process here if it's writing to acquire an exclusive lock meaning this is the only computer only transaction that can read and write to this database. All others must hold off in order to be sequential. So we've seen transactions then are sequential and they use this idea of a lock to ensure other folks can't read when they make something sensitive like writing the database.

**8:55:49** · Let me ask now what questions we have on locks and how they work for us here. Okay. My question is that uh suppose uh uh one computer means for what amount we will should we should allow to do the exclusive log. Maybe uh if the time if the time stamp is larger then some other computers will get time out exception and all the things right because it's

**8:56:14** · not allowed to do but exclusively it's a locked how we going to decide those things for what time one instance is going to be put the exclusive lock on the resource so the question is at what point does a transaction actually get an exclusive lock and how do we decide how to prioritize different transactions here well there are a two algorithms you could use. One of which is simply taking the transaction that just came first.

**8:56:38** · If at this point I receive a request for an exclusive lock, I might just wait for others to finish reading and allow that one to proceed. I could also use a process called timestamping which is similar to this where I look at the timestamp the time a database tried to write to the log and use the one that is earliest in that case. Now it's important to note that an exclusive lock does block others from running their own transactions.

**8:57:06** · If I have an exclusive lock, no one else can run their transaction. That is kind of a necessary necessary downside in this case to ensure that I don't make mistakes in updating my table.

**8:57:21** · Let's take one more here. What's the granularity on locking? I mean, you seem to say you lock the table uh database, but that's craziness. Do you lock a table or would you lock a record on a table?

**8:57:32** · Yeah, it might depend on the DBMS itself. So, um, at the very at the very coursest, a lock might just lock the entire database. I can't actually see anything inside of it. And I might be able to demonstrate that for you in a minute here. Let me go back to my computer. Let me try to deliberately lock this database. If I go to my terminal, I can begin a transaction that automatically has an exclusive lock. In SQLite, the statement is begin exclusive again exclusive transaction. I'll hit enter like this.

**8:58:02** · And now I'm in the middle of this transaction is exclusive has an exclusive lock. Nobody else can read. If I go back to my um other terminal here, connect to my database. I could try select star from accounts just to read from this table. And now I see runtime error. Database is locked. the entire database cannot be read from at the very coarsest level of an exclusive lock. Now, because these locks are so coarse, I have to lock the entire database.

**8:58:33** · SQLite has its own module, a way of prioritizing transactions and ensuring that a transaction only has an exclusive lock for the duration absolutely needs to because otherwise you would slow down substantially if I had to wait and wait and wait for somebody to finish with their transaction. Okay, so this then is how we can handle not just one query at a time, but multiple.

**8:58:59** · And today we've seen how to optimize our databases from making sure queries are faster to also making sure our databases use as little space as possible. We'll see next time how to actually scale up our databases using other DBMS's like my SQL besides SQLite. We'll see you next time.

### Scaling

**8:59:19** · \[Music\] Okay. Well, hello one and all and welcome back to CS50's introduction to databases with SQL. My name is Carter Zeni and this week is the culmination of all you've learned over the past several weeks in the course.

**8:59:48** · Today we'll give you the tools to do all that you've done in the past, but now just at a bigger scale. Now, while we're talking about scale, it's worth defining what scale is and what it means for some application to have scalability. For an application to be scalable or to have scalability, it means it can take some number of requests and handle those. whether that request is small or large. And so to kick things off here, let me ask a question.

**9:00:16** · What are some famous tech companies you've seen that have needed to scale over time? Let's brainstorm here. Which ones are you familiar with that have needed to scale over time to handle more users, more data? What have you seen?

**9:00:33** · Any social media sites such as Facebook?

**9:00:35** · Yeah, any social media sites. You could think of things like Facebook, now Meta, uh Instagram, and similar. And these kinds of sites might have some really large number of users that are always accessing their data. But even though they have a constantly large number of users, there might even be spikes in the number of requests that they get. Maybe during the World Cup, for example, everyone is on Facebook, everyone's on Instagram. That would be a spike our application should be able to handle if it is truly scalable. Let's take one more idea here.

**9:01:09** · What other kinds of companies tech prominently have needed to scale? So I think uh for banking systems who they might start locally but if you consider national and international level banking so you're right a banking system might need to scale as they gain more users or more accounts or they want to process more transactions.

**9:01:31** · Now today we'll introduce you to a few new DBMS's or database management systems like MySQL and PostgresQL or just Postgress for short and developers often reach to these when they want to scale some application or some database because whereas SQLite was a embedded database

**9:01:54** · MySQL and Postgress these are database servers that means they often run on their own dedicated hardware that you connect to over the internet to run your SQL queries. And now being a database server, they have a few advantages. They can store data not just on disk, like on an SSD or a hard drive, but in RAM or random access memory, which often allows for faster querying.

**9:02:19** · They also have a full feature set to take advantage of ways you could scale like replication and sharding that we'll talk about later on today. Now before then we'll actually compare MySQL and Postgress with SQLite paying attention in particular to types but later on we'll focus on their features for scaling as well. Now we'll do all of this in the context of the MBTA or the Massachusetts Bay Transportation Authority. This is the subway system here in Boston.

**9:02:50** · And if you're ever in town and you want to get around, you might use one of these subway lines. You could enter under the ground, get on a train and go across town on either, let's say, the red line on which Harvard and MIT are apart, the green line, the orange line, or the blue line. And if you recall in our week on designing, we talked about how to represent all of the riders and stations on MBTA here. Now, one thing we discussed was that the MBTA doesn't keep track of individual people.

**9:03:22** · You often don't register your name with them. you instead get your very own Charlie card that you might swipe when you enter some station. Uh often if I'm getting on the Harvard Square stop, I'll take out my Charlie card and to enter that station, I'll swipe it against some counter and that will log my fair. I could also swipe my card to deposit some funds to pay my fair in the future. And in some stops, I might actually swipe to leave the station and pay some extra fair there.

**9:03:54** · Now we decided then to represent in this case cards, swipes and stations own table for each of them. Cards just had their own unique ID and those cards made some swipe and like we just mentioned this swipe has a certain type.

**9:04:11** · Did I swipe it to let's say enter the station? Did I swipe it to exit the station? Or did I swipe my card to deposit some funds into my account? And each swipe has as well its own date and time it occurred as well as some amount associated with it. Did I pay some money to enter or did I deposit some money to actually uh add to the funds in my account?

**9:04:34** · And then finally, this all happens at individual stations with their own IDs, their own names like the Harvard Square stop or the Kendall MIT stop and their own line like the red, green, blue or orange lines. So our goal will be to first compare MySQL with SQLite, seeing how we can translate a schema like this from SQLite to MySQL.

**9:04:59** · Okay, let me come back to my computer here and open up our very first instance of a MySQL server. So to connect to this server here, I can run some command that begins with MySQL. This is a command line program I can run to connect to the server over the internet. Now unlike SQLite, MySQL actually has individual user accounts to log into the database.

**9:05:22** · And here I want to log in as the root user or the admin for this database. Now to say the user I want to log in as I can type dash u where u is in lowercase here followed by the name of the user I'm logging in as in this case root. And again, root is just some synonym uh for the admin of some database. Now I connect to this database over the internet and I might often include the IP address of the computer, the unique identifier of that computer on the internet.

**9:05:53** · For my sake though, I mean this database is on my very own computer here. So for the host where I type H or H is in lowercase, I can say 127.0.0.1 0.1 which if you're familiar is the IP address for my own home computer also known as localhost.

**9:06:13** · Now I can keep going and I should tell my SQL what the uh port I'm connecting to is. In this case I'll type dashp where p is an uppercase and then the port number 336 by default. And then I want to be prompted for the root password. So I'll type -ashp where p is lowercase. And finally, I'll hit enter to connect. I'll type in my password and I should see that I'm connected to my MySQL server.

**9:06:43** · Now, this is a full database server and as such, it could have multiple databases inside of it. In fact, there are a few here already. If I type show databases just like this, you should see by default on your own MySQL installation on your own server a few default databases like information schema or MySQL or performance schema or CIS.

**9:07:07** · And these are tables or databases that have some um meta information on the server like the user accounts, how performance is configured, and other details that you might care about if you're a system administrator. So, we've seen here how to log in to a MySQL server and some of these default databases. Now, let me ask what questions do we have on MySQL so far.

**9:07:32** · Uh, what's hyphen new room?

**9:07:34** · Yeah, let me go back to my computer. I can show you what that looked like so we can refresh our memories on that. So, if you recall, let me open up a new terminal here. To connect to this server, I typed MySQL u root or u root.

**9:07:49** · And what this means is when I want to connect to my server, I have to connect to it using some user account. Unlike SQLite where I could just kind of log in without any users, MySQL has users. So the dash u says here comes the user I want to log in as and root in this case is a name for the admin. Just some uh geek historical term for the admin of some a system.

**9:08:13** · I could also very well use dash u carter if my username was just carter but here we're using root to get access to some administrative privileges. Okay, good question and good to clarify that. So let's keep going. And right now we have access to our database server with the databases inside of it. But our goal is to design the MBTA system and create our very own database now in MySQL.

**9:08:44** · So let me try creating some new database. I'll say create database like this. And now I'll give it some name. And in MySQL I don't use double quotes like I did in SQLite. I use back ticks like this. Create database back tick. MBTA for the title. Back tick again to close that all out. Now I'll hit enter and I'll see the query was okay. One row affected. If I now type show databases.

**9:09:12** · show databases.

**9:09:15** · I should see that MBTA is now part of this server. And if I want to run my future queries on this database, I could use another command, another statement here, use. I'll say use MBTA semicolon, hit enter, and I see database changed. So now all my future queries will be run on this MBTA database that I just made.

**9:09:41** · So presently our database is empty and it's up to us to add in some tables. So let's think through how we could add tables to our very own database we've just made here. Well, one thing we should focus on is this idea of the types for our columns. Like I think we know already what tables we'll have, what names we'll give them, but it remains to be seen what kind of columns should we add? And actually in MySQL, we get a lot more control over types.

**9:10:08** · We no longer have just text and numeric and integer. We have a lot more control and a lot more variety. So let's look here at our cards table. We want to recreate this now in MySQL. And this is from SQL light here. Recall how we had a table called cards that had an ID column with the type affinity of integer. And that was our primary key down here. So our goal is now to think about how do we translate this from SQLite to MySQL.

**9:10:42** · So we should think what kind of types might MySQL have for integers. Well, it turns out there's more than just one.

**9:10:50** · There actually several here. We have tiny int, small int, medium int, in int, and then big int. So lots of choices over our integers. And these vary just based on their size. I mean they all store whole numbers but they do vary based on their size. So a tiny int is only a single bite. It's about eight bits. But a big int that's eight bytes or 64 bits. Now why do we have so many of these?

**9:11:20** · Like why can't we just have one? Well, let me ask you all to use your own intuition. I mean what does using more bytes and more bits get me when I'm trying to represent an integer?

**9:11:34** · So basically it depends on the need of the DB or you know the organization. If the data requires much more storage then it means we need to have you know a bigger data type but if you know uh currently if we need smaller sizes then it means we need to use smaller data types.

**9:11:57** · Yeah.

**9:11:57** · So, I like your thinking and I think um kind of behind that is this idea that if we used more bits, we'd be able to count higher like just as I have on my hands like 10 fingers. If I had more fingers, I could count higher in unary notation, right? Or if I had more digits, I could count higher using decimal. So, it's the same thing in binary here where I could count higher the more bits that I have. So if I take a look at this table here, each data type has a range of values that it could possibly store.

**9:12:27** · If I'm talking about both negative and positive values, here's the range for each of these data types. You could see for a tiny int, we can only count up to 127. And that is it. We cannot count higher using a single bite. But if I used a big int, well, I could count all the way up to 2 to the 63rd power minus one. That is almost unpronouncably big.

**9:12:52** · It's something like a quintilion uh, you know, number of options that you might have between these two minimum values and the maximum values here. So all trade-offs what you want to represent.

**9:13:07** · But our goal here is to translate a primary key. Like a primary key doesn't be it isn't negative. So, we could perhaps use something called an unsigned integer. An unsigned integer has no negative values, starts at zero, but can then go to a higher positive value because we're now using some of those combinations of ones and zeros that represented negative numbers now for positive numbers, too. So, here an int can go up to almost 4.2 2 billion values between 0ero and 4.2 billion.

**9:13:41** · So an int is already pretty darn big. So with these in mind, tiny int, small int, medium int, in int and big int, let's go back to our SQLite create table statement. And let me actually ask you all like what would you substitute in place here? We no longer have integer for our primary key. But which of these do you think seems the best substitute for our primary key on cards? Tiny, small, medium, int, or big int.

**9:14:18** · So, uh, in case we know that it's not going to be really huge, we can just use a int. But if it's going to be very large, like say a timestamp, we could use a big int.

**9:14:32** · Yeah, I like your thinking. So if it's if it's big but not too big, maybe an int would be good. If we know for sure though that it's going to be huge, well, a big int is probably best. And let me um offer some intuition here. So, if there are fewer than 4 billion people on this earth, which I believe is a true fact, and we're using one of these IDs to represent one card, well, if everyone on Earth visited Boston and got their own Charlie card, we wouldn't run out of values using an int here. So, it seems like that's a pretty safe bet.

**9:15:04** · Unless unless we knew that everyone in Boston was going to have like 10 Charlie cards or 20 or more, then we could use a big int. But in this case, an int seems pretty safe. So let's update this. Let's go from SQLite now to MySQL. So here I had the ID column with type affinity integer. And my first step in converting should probably be to get rid of these double quotes. I no longer need to use double quotes. I should use back ticks as a matter of style in MySQL.

**9:15:35** · But now I should update this type from integer perhaps to a plain old int. As we discussed before, some intuition for that is we'll probably never have more than 4 billion Charlie cards in our table. Now there's one more thing to add to which is this auto increment. So SQLite for free gave us a primary key that if I inserted some value and didn't provide a value for the primary key, SQLite would generate that for me.

**9:16:06** · But in MySQL, I have to actually say auto increment. If I add some new row, make sure you take the highest primary key right now, increase it by one and assign it to that new value. So you'll often see primary keys being defined with the name ID and the type int and the auto increment property of that column there.

**9:16:32** · So let me ask now what questions do we have on these integers and types so far for for ID we have using integer type why we know that ID cannot be negative it will always start from one or and go onward so we should use here unsigned

**9:16:50** · nice so here we didn't include it um partly for slide's sake but you could if you wanted to make sure that the ID is unsigned so unsigned means going from zero all the way up to some larger number whereas not unsigned or just assigned integer goes from negative to some positive value. Absolutely right.

**9:17:09** · Okay, let's keep going then and let's think through our next table here. So our next table is not just the cards table, it's also the stations table.

**9:17:19** · Actually before we do that, let's actually try to add in our cards table to our server. So I'll go to MySQL here and now let me try to create this table to store it inside of our server before we move on to stations. So I'll say create table cards and then I'll follow some very similar syntax what you've seen before. Create table cards. Now let me add an ID column int and auto increment like this. And now I'll make the primary key ID like this.

**9:17:50** · Now I'll close out my create table with a semicolon. Hit enter. And I should see the query is okay. Now if I use the MBTA database as I did before, I typed use MBTA. I could show tables like this. Semicolon. Hit enter.

**9:18:14** · And now I'll see I have a cards table inside the MBTA database. So kind of like for example typing schema or tables in this instance in my in SQLite to see what tables I had. Now though let me try this. Let me try describe cards. Describe is a bit more like schema to show me the schema of this table. I'll describe cards and I'll see a few different columns here.

**9:18:42** · Let me come over to this this uh board here and we'll see that this table cards has one column, one field called ID. The type of this column is an integer as we said it was before in our create table statement. Now this null here, this is whether this column can accept a null value, yes or no. Yes means it can accept a null value. can hold null. No means it should never hold a null value.

**9:19:14** · So this ID should always should never include a null value.

**9:19:19** · Now the key the key column tells us what role this column plays in terms of the keys of this table. Pry here PRI stands for primary key. This is the primary key of our table. Default means the initial value given to any um value. If we inserted some, if we inserted some row with no value, we'd get back this default value here, null. And the extra is what we included auto increment. It should increase by one every time we add some new row.

**9:19:48** · So using describe and show tables, can you actually see what you're creating along the way?

**9:19:58** · So now let's keep going. Let's actually focus on creating our stations table. And for that we'll pull up our SQL lights syntax we used to create that table. So here here was what we used to create the stations table in SQLite. We gave each station an ID that was an integer. The primary key of this table.

**9:20:21** · We then gave them each a name and a line. Like the name could be uh the Harvard Square station or the Kendall MIT station. And the line could be red, green, blue, whatever line this station is a part of. And of course the uh primary key is our ID column as we just said. Now here we've seen how to handle this integer type, but we haven't yet seen how to handle text. Like could we do better than this in MySQL compared to SQLite? Turns out that we can.

**9:20:48** · We have a variety of options for representing strings. Basically this collection of text here. And two of the more popular ones are going to be char and var.

**9:21:02** · So char is a fixed width string, a string that only has and will ever have the same number of characters. You could think of, for example, in the US we abbreviate state names using two letters like ma for Massachusetts or VA for Virginia. You might do the same thing with countries as well.

**9:21:23** · Now, that would be useful for a char because this char will always hold only two characters, but often you're not sure how long the string is. You're going to add to your column. Like, let's say you're trying to store names of people. Well, my name is Carter, but yours could be longer or shorter. So a varchchar works well for that scenario where a varchchar can accept a variable length string up to some number of characters.

**9:21:55** · And when you use these, my SQL will ask you to provide how much space this type should take up using m here. So I could say char parenthesis 2 to get back a fixed width string of two characters. For varchar I could say varchchar and then put in the middle here like let's say 16 or 32 or 64 and that would be the maximum size of the string that I could represent using varchchar.

**9:22:27** · So good here for strings that are going to be a bit shorter in length. What if though you want to store the text of a book or something a bit longer than that? Well, you could use another type.

**9:22:39** · this one called text. And this is different than SQL lights text. In SQL lights text, I could store short strings, long strings, etc. In MySQL, text is good for longer chunks of text, paragraphs, pages of books, and so on.

**9:22:56** · And you actually have some options for the length or the size of this text. You could use tiny text, medium text, or long text. Each just uses some variable amount of space on your computer to store in this case characters that are going to be longer than any particular string like a name and more like some page in a book.

**9:23:20** · Now besides text we do have our old friend blob and blob still stores binary exactly as you give it. And more interestingly though we also have enum and set and these are brand new. These are not in SQL light, but they're very useful for us. If you remember back in our week on designing, we introduced constraints. Maybe a constraint is that this column should only have a certain uh certain values.

**9:23:48** · Like let's say for calculating t-shirt sizes, I should only have xs for extra small, s for small, m for medium. There's some fixed range of values this column could hold. Well, I could use enum for that where enum lets me enumerate the possible options I could put into this column like xsm if I'm doing t-shirt sizes or something else altogether.

**9:24:19** · Now set complements enum. Enum means I can only have one of these options. If I had XS, XX Sm and so on for t-shirt sizes, I can only choose one. But a set would allow me to choose more than one to store in that same cell. You could think of, for example, um movie genres.

**9:24:42** · A movie isn't just uh horror or fiction or it isn't just comedy. It could be all of those together. And so set would allow you to choose not just one option from your list, but multiple and put it inside of that single cell there.

**9:24:59** · So let's go back to our SQLite create table statement and let's update this for MySQL. Well, the first thing to do is what? Change these double quotes to back tick. So I'll do that here. And now let's update this ID. We saw before we could use just regular old int and auto increment like this. But now we have some more choice like for this name field that should store the name of a station.

**9:25:27** · Let me actually ask you all what do you think is the best type to use when we're storing the name of some station?

**9:25:35** · Um it would be a varchar simply because you don't know how long the station name actually is.

**9:25:41** · Yeah, good point. So, um, we're always creating new stations and maybe some station name is pretty long or maybe it's short. We can't really tell, right?

**9:25:50** · So, a var is good if we have some variable amount of characters inside the text we're trying to store. And notice how a station name isn't paragraphs of text. It's just, you know, maybe a few words. So, that's good for a varchchar. And in general here, I could say, well, let's try to use a varchchar and say we could use up to 32 characters including spaces. I think that'll cover us pretty well for names of stations.

**9:26:19** · Now, let's talk about the line. Now, in Boston, there are a few lines. There's the blue line, the green line, the red line, um even the silver line. But what what type should we use for storing lines then that these stations are a part of?

**9:26:38** · In this case, I could believe that there can be two options where it would be a a small integer number uh and pointed to another table uh storing the colors. Another one will be a limited chart taking into account that perhaps the longest uh color name will be like aquamarine or something like that and truncated it just to that size will be another option as well.

**9:27:03** · Yeah, I love you're thinking through multiple options here and indeed there's usually more than one option for any given type of a table here. So for this one, I mean, you could actually have line be a foreign key and reference some other table to your point of those colors. So line might then be an integer. We could also make line another varchchar. Maybe this one's a little shorter, like it's always going to be just blue, green, red, or so on. So a pretty short string, but still variable length nonetheless.

**9:27:33** · So we could say varchchar maybe nine, for instance, to represent a color here. One other option though exists, one that kind of constrains us, but that might still be a good fit.

**9:27:49** · Um, maybe it would be good to use a set to use set. Yeah, you could use set as well. So, you could say that a station might be on the blue line and the green line as exists in the real world. You could certainly use set for that. For our purposes, I might just go ahead and simplify things and just say enum. A station will only be on one line at a time for simplicity. But if you wanted a station on more than one line, you could use set as well. And in this enum or in this set, we could include the possible lines that currently exist in the MBTA.

**9:28:22** · So great reasoning through some different data types here. Let's now build this into our MySQL server here.

**9:28:30** · I'll come back and I will create this table. So we saw before I could simply use create table. I could say create table and then I could say give it a name called stations and inside I'll make sure to include let me indent four spaces here 1 2 3 4 give it an ID which has the type integer and auto increment.

**9:28:56** · Then afterwards we also want to include the name of our station which could be a varchchar up to size 32. It could include up to 32 characters. And this should also be not null and unique. Those same kind of column constraints. So they're still here in MySQL.

**9:29:15** · Now I could also include the line column. And for simplicity, I could just assume every station is part of only one line. So I'll say enum here. And I'll choose blue and green and orange and red. These are four lines for the subway that exist here in Boston. And I'll make sure this has to be uh have a value. It can't be null that not null constraint here. Then I'll say my primary key is the ID column.

**9:29:45** · And I will go ahead and close this out. Hit semicolon and enter.

**9:29:51** · And I'll see query. Okay. So now if I show tables enter, I'll see both cards and stations. And if I were to describe describe stations, what do I see here?

**9:30:05** · Let's take a look. I'll come back over here and I'll see I have three columns, ID, name, and line. And each of these has their very own type as I see in this column of my describes output. I see here that the type of ID is an integer.

**9:30:22** · The type of name is a var 32. And the type of line is an enum. Blue, green, orange, or red are the possible values for that column. Now, none of these columns can have a null value inside of them. But here's the interesting part. I see ID has a key prior. That means ID is my primary key. But I also see uni where uni stands for unique.

**9:30:47** · Now we saw before this name column I applied a unique constraint meaning there can only be a given station with a unique name. I can't duplicate station names and then of course over here we also saw the extra column auto increment that I applied to the ID column here. So let me ask we've seen now uh some new types for text some new types for enum and set and so on.

**9:31:18** · What questions do we have on these new types and how we've used them?

**9:31:24** · I was wondering if if it would be perhaps possible to include a table as the argument to enum.

**9:31:30** · Oh, a good question. I actually am not sure. I could imagine the possibility of using a um nested select for that. But I mean, let's reason through this here. If I had a table that was growing, would I want to use those table results in my create table statement? I would argue probably not because then things are going to change over time. So, probably worth just enumerating one at a time explicitly what might go into that enum.

**9:32:04** · But I encourage you to just try that out too and see what happens. Let's take one more. Is it a problem for the database if I for example I have no idea how long uh could be the name of the station and if I write a v chart for example 100 or 300.

**9:32:21** · Yeah.

**9:32:21** · So maybe you're think of a scenario where you don't know how long it's going to be. So you'd be kind of extra safe. You say like varchchar 300 for instance just accommodate anything you could put in there. that is okay, but the trade-off is you're then using up to 300 bytes every time you store a smaller string. Like if I use varchchar 300 and I only ever use let's say like 10 characters on my longest string, well, I'm wasting some space. So, it's worthwhile to think through beforehand what should I actually use here.

**9:32:52** · And um something to keep in mind is you can always expand a varchar using MySQL's alter table statements. So, we'll see that in just a bit. How to use alter table, but you could always expand if you need to. Okay, good questions here. Let's keep going then. And our next table is going to be the table that represents swipes.

**9:33:15** · We have cards and stations, but now we have to represent swipes at those stations. Well, let's come back to our schema for swipes in SQLite. Here I had this table called swipes that had some columns up top and some primary foreign keys down below. But the important part for us now is going to be these three columns. Type, date, time, and amount.

**9:33:43** · And remember that on the MBTA, I can take my Charlie card. I can make a swipe when I enter, exit, or deposit some money at a station. That's that type column here. It could be either enter, exit or deposit. Now, date time is the time and date. I swipe that card to enter, exit, or deposit some funds. And amount is the amount in dollars associated with that transaction. Now, the fair nowadays is like $2.40.

**9:34:15** · Back in the 50s, it was maybe like a dime or so.

**9:34:20** · It changes over time, so it's worth keeping track of in our table here. So let's think through some options that MySQL gives us. Among them are options for dates and times. So whereas in SQL light we had numeric for dates and times in MySQL we actually have explicit date and time types. For instance we have all these here date which is just a date like the year the month the day. Time which is the uh actual time like hours, minutes and seconds.

**9:34:51** · We then have date time which combines those timestamp which is similar but used with a bit more precision often for logging events on your own software and then year which is just 2023 or 2020 for instance in a single column. Now you can get more particular about how precise you want to be with these times.

**9:35:13** · For time, date, time, and time stamp, I can specify how many decimal digits I want to keep track of after the decimal point. Do I want to keep track of tenths of seconds, hundreds, or thousands? I could specify that using this uh parenthesis FSP. In this case, I could say 1, two, three, four up to, I believe, six to figure out how precisely do I want to keep track of time where more digits means more precision.

**9:35:49** · So, I could use these for dates and times that could get us through part of our table migration here. But I should also think about how to represent real numbers. That is numbers with a decimal point in them.

**9:36:04** · Now you might think back to SQLite and remember the real data type affinity and we have some similar options here. We have float and double precision where the only difference is float stores um a number in size four bytes whereas double precision stores that number in eight bytes. And you might be thinking, well, if they both store a decimal number, a real number, why would I choose one over the other?

**9:36:38** · Or why would I use more space when float does the same thing for me in fewer bytes? Well, it turns out that in computer science, we run into this problem of floating point imprecision where there are an infinite number of real numbers. Like if I asked you to find me all of the decimal numbers between one and two, you would be here for literally an eternity.

**9:37:03** · And if we have so many numbers to represent but so few bits, it goes to say that we can only represent some of them and not all of them. So at the end of the day, floatingoint numbers, decimals, uh real numbers will be imprecisely represented. Now, a double precision could get us more could get us um more of the way there.

**9:37:28** · We could use more bits to more precisely represent some number, which you might use if you're a scientist, someone who wants to keep track of things very precisely. If you don't care as much though, you could use a float and just use a little bit less space.

**9:37:45** · Now, thankfully, this trade-off isn't um isn't quite so salient in MySQL because you also get access to fixed precision types where fixed precision means I can specify I want to always have two places after decimal precisely represented. And one type for this will be the decimal type where I can use a decimal and then say I want to store a certain number of digits with some number coming after the decimal point.

**9:38:19** · Now for example I could say decimal 5,2 and I could store any number between99.99 up to 999.99 so long as there are only two places after the decimal here. Now I could increase this. I could say I want to go beyond this range. I want to have more digits. I could increase this first parameter here from five, let's say, to six. And now I have a wider range.

**9:38:51** · I have 9,999 all the way down to 9,999 in both cases.99. Two decimal digits after this decimal point.

**9:39:08** · Now I keep going. I could say seven and get an even bigger range. But if I want to represent something precisely after this decimal point, what could I do? I could change this one too from two, let's say, to three or even to four. I could keep going, but notice how my range shrinks. What I get in return is just more digits after that decimal point precisely represented.

**9:39:31** · I don't have to worry about floating point imprecision so long as I'm using decimal and telling my SQL how many I want and how many come after the decimal point. Okay, so let's try this here. I want to migrate this table from SQLite to MySQL. The first thing to do change these quotes from double quotes to back ticks. I could then update uh my primary key and so on. Let's focus now on this type.

**9:40:03** · This type column should only have some set of values like enter, exit or deposit. And when you see that, you could think I should probably use an enum to only store some piece some data types that are some uh values that are inside of this list. So I'll make this now an enum. But the question then becomes, what should I use for datetime?

**9:40:27** · What type have we seen so far that could be useful for storing the date and time?

**9:40:33** · I swiped my Charlie card.

**9:40:35** · Yes, I believe we can use the date time uh data type.

**9:40:39** · I could use date time. So, kind of self-explanatory here. I mean, the column is called date time. And coincidentally, MySQL also has a type called date time that stores both a date year year year mm dd and then the hour along with that. I could say date time here to get both day and time.

**9:40:59** · Now the next one amount. Now it's worth noting I want to be precise with this amount. Like if I'm going to sum up many many amounts, many fairs. I want it to be accurate. So I don't want to deal with let's say float or double precision. I want to specify how precise I should be. Let me ask what data type might be good for storing the amount of some given fair.

**9:41:28** · Uh I believe we can use the decimal data type.

**9:41:31** · Yeah, you could absolutely use decimal data type here. So decimal was part of MySQL's fixed um precision kinds of types. So we could use that here to precisely represent the amount column here. I could change this from numeric in SQLite to decimal now where decimal I could say takes five possible digits like um five total and two now could come after the decimal point.

**9:41:55** · So I could have um amounts or fairs that go up to hundreds of dollars which often isn't going to happen but I could be safe here if I need to be.

**9:42:06** · Okay, let's go ahead and combine this and put this inside of our MySQL server here. I'll come back to my computer here and my goal is to run this create table statement to create this table on our server. I'll say create a table called swipes like this. And I'll include a few columns we didn't show on the slides just for simplicity. I'll first include the ID column with type int. And I also want to make sure this auto increments as I add to it.

**9:42:36** · I'll then go on and I will also include a card ID column that has a type int. And then I'll include a station ID column which also has type int. So now I can see which card ID is swiped at which station. Now when they swipe here at the MBTA, a swipe can mean a few different things. It can have a different type. One type we might care about is the enter type.

**9:43:04** · When I swipe to enter some station, I could also swipe to exit some station or to deposit to deposit some funds into my account. And a type should never be null. It has the not null constraint here.

**9:43:24** · Now, a type a a swipe happens at some particular date and time. So, I'll include the date time column and say that this is of type date time. I want to make sure that this uh column always has some value. So it's not null. And the default when I insert some new row will be this special value here. Current timestamp, the current date and time.

**9:43:51** · Now I'll go on and I'll include the amount of some swipe. I'll hit enter space and then I'll say amount here.

**9:43:58** · This is the amount associated with that swipe. Was I charged money? Was I adding money? Here I'll say I want this to be a decimal type because you said we want this to be precise and decimal is a fixed precision type. I'll say I want five decimal digits with two after the decimal point. Now this similar should be not null and I'll include our same check constraint. I'll check that amount with back ticks here does not equal zero. And if that's the case, I'll be able to insert some new swipe.

**9:44:30** · Now I'll assign my table constraints like primary keys and foreign keys. I'll say my primary key my primary key is the ID column like this. And then if I hit enter again my foreign key my foreign key in this case card ID should reference it references cards table and the ID column in cards bit like this.

**9:44:58** · So that card ID column references the ID column in the cards table. Now I'll include my last foreign key. The foreign key station ID. Station ID references the stations table and the ID column in stations. And now to quickly review to make sure I've typed everything in correctly here. So we have the ID column, the card ID column, station ID, type of enum, date time, amount. I think we'll be good here.

**9:45:31** · So if I hit enter and then use parenthesis semicolon, I should see query. Okay, zero rows affected. Now if I type in this case show tables enter, I'll see I have a new swipes table. And if I type describe describe swipes like this, I should see some familiar output. If I go back to um my screen over here, we can take a look.

**9:46:00** · We have again our fields ID, card ID and so on. Types int, enum, date, time, decimal. Some can have null values, some should not. We have a primary key here. But now the interesting thing is this mul.

**9:46:17** · Well, if I look at card ID and station ID, what do we call those two columns?

**9:46:26** · What kind of constraints did I apply to card ID and station ID?

**9:46:31** · So, we use the foreign key constraints.

**9:46:34** · The foreign key, so it's referencing the stations and the card key.

**9:46:38** · You're exactly right. We applied the foreign key constraint to the card ID and station ID columns. So, this mul here is referring to the fact that these are foreign keys. And mul stands for something like multiple or multi. It means I could have um in this case multiple um of the same value because it is a foreign key in this table.

**9:46:59** · Now the default here we now see current timestamp when I insert some value into this table and I insert some row sorry into this table and don't supply a value for the date time column I'll instead make that default value the current date and the current time. And here we see some extras like auto increment that we saw before and now default generated meaning this is a generated column that will automatically create some value for me when I insert some new row.

**9:47:33** · Okay. So let me ask what questions do we have then on these new types dates and times and more.

**9:47:41** · Yes.

**9:47:41** · Um I wanted to know the precedence in which the um the attributes the specific constraints to attributes are added. So is it in the format of the describe table you know in the describe table there's a certain format in which the data is is that the priority in which you do it let's say an integer before let's say a unique constraint before um a not what's the precedent and

**9:48:12** · secondly is there any type affinity in MySQL yeah both good questions I'll answer the first one first so the first one is what's the prec precedence I believe of these constraints we're applying. If I look at this um output of describe swipes here, I see that I applied some constraints. Among them are the foreign key constraint, the primary key constraint. Some I made sure that I couldn't have some null value in here.

**9:48:39** · Uh in effect, they all combine to um work for me here. So when I made that create table statement, I applied multiple constraints like not null and unique and I could put those in any order. MySQL is designed so I can do it in any order and get the same result forwards or backwards. When I read this table, I might just read it right or left to right here and kind of get a feel for which constraints are being applied in no particular order in this case.

**9:49:10** · Okay.

**9:49:10** · Yeah. The second question has to do with type affinity and you know with SQL like we had something like a type affinity where a particular value is appropriate for a particular row. So is there anything like that in MySQL?

**9:49:26** · Yes

**9:49:26** · there is. So in SQLite you're right we had type affinities where we defined a table and said that this column should store values of this type. We're doing the very same thing in MySQL when we say ID of type int or the the name of a station of type varchchar 16 for instance. Um, one difference though is that SQLite will allow you to add in some value that doesn't actually have the type of that given column.

**9:49:56** · So if I had a SQL like column of type text or of type let's say um let's say type numeric and I added some text it would try to convert but if it couldn't it would actually just store text. MySQL is more strict than that. It will make sure you have the proper type when you insert some new rows at least by default.

**9:50:21** · Okay, great questions here. Let's keep going and show some more features of MySQL. So, one of them is the ability to uh alter tables in a more fundamental way. So, let me zoom back in here. In SQLite, we had some options to alter tables, but at the end of the day, they just weren't all that powerful. With my SQL though, we're actually able to alter tables a little bit more um a little bit more fundamentally.

**9:50:50** · So, let's say that the MBTA adds in a new line, a new subway line. And actually, the silver line, if you can see it here, is currently a bus line, but it was planned to be a subway line. So, if I wanted to add in a subway line called the silver line, well, I can't currently do that because my type for the um lines is an enum. It only has red, green, blue, and orange, not silver.

**9:51:21** · So I should actually edit this create table to now be able to include the silver line as a possible value among that enum. So I'll come back over here and I'll introduce you to MySQL's alter table syntax. So in MySQL, we have still alter table similar to SQLite. They're all based on the SQL standard, but now we have modify where modify can take some column definition and change it on the fly.

**9:51:51** · So I'll go to MySQL here and let me just uh let me describe again the stations table. I'll hit enter now and we'll see that the line is an enum and it has a few options, blue, green, orange, and red.

**9:52:09** · But now I want to add silver here. So what could I do? I could do this. I could use alter table and I could say I want to alter table. I want to alter the stations table and I want to modify I want to modify the line column to be this. I want it to be an enum with these options. Blue, blue, green, orange, red, and silver like this. Now I have more options in my enum.

**9:52:43** · I could also include not null too. Hit enter and I should see Oops. I think I might have forgotten a quote somewhere. I believe I did. Let me fix this. I will finish the quote. hit semicolon. And let me show you how I noticed that. If I go back to my screen here, see in MySQL, it's kind of helpful.

**9:53:04** · If I finish a line and I haven't closed this quote here, like I did in red, it will alert me on this next line with this single quote here saying, "Hey, you didn't close that thing that you probably thought you were going to." So, let me restart. I'll come back over here and I will try this again. I will alter table stations and then I will modify the line column as we said before to be an enum with a few different values. Blue, green, orange, red, closing both quotes now.

**9:53:36** · And then silver again closing both quotes. And let me double check. Believe we're all set. I'll then say not null semicolon. Enter. And I'll see the query is okay. Now, if I do describe describe stations like this semicolon and zoom out just a bit, I see I've added to my possible values for this enum. I have blue, green, orange, red, and silver.

**9:54:06** · So, this is one example of using alter table to adjust a column definition. To an earlier question, you could also use this to expand the size of varchars or to change your table altogether. you can do so a little bit more powerfully than you can with SQLite just because MySQL decided to focus on this particular feature. So let me ask now what questions we have on altering tables in MySQL.

**9:54:33** · This is uh regarding to generally regarding to MySQL and Postgress. Can you use those applications instead of VS code? I mean that uh user interface.

**9:54:43** · Yeah, good question. So I think you're asking what would be the difference or how could I use like MySQL and Postgress compared with VS code. Um in fact there are kind of different use cases. So VS code as you might know is an IDE an integrated development environment allows you to write code in a file to run that code and to edit it and see it all in one place. Whereas MySQL and PostgreSQL those allow you to write SQL statements on a command line talking to some underlying server. So a bit different.

**9:55:14** · You could for example use VS code and connect to a MySQL or PostgresQL server to run your SQL queries you're creating in VS Code. A good question there for workflows. Okay. So what we'll do is take a quick break here and we'll come back and talk about stored procedures. Some functions we can define to run over and over and over again. We'll see you in a few.

**9:55:43** · Okay, and we're back. Now, we'll next talk about stored procedures, which are a way to automate the running of SQL statements over and over and over again.

**9:55:54** · This is useful as you're scaling because if you have some process you often call, you can put it inside of a stored procedure and run it all the more simply. So to demonstrate stored procedures, what we'll do is go back to our example of the Museum of Fine Art, one of Boston's oldest museums, also called the MFA. And if you remember in the MFA, we had a certain number of tables where one of these tables was a collections table.

**9:56:24** · It is the items the MFA has in their collection, the items they put on display. For instance, here we had a few pieces. Farmers working at dawn. imaginative landscape and so on.

**9:56:37** · Each had their own ID and they also had a deleted column to implement what we called a soft delete where to delete something we wouldn't remove the row. We would instead just mark this deleted column from a zero to a one sort of hiding it or marking it as having been deleted to keep data around without removing it all together.

**9:56:59** · Now to find all of the items that weren't marked as deleted, we could use this query select star from collections where deleted equals zero, at least in SQLite.

**9:57:16** · Now we then created a view. We said maybe I want to just always be able to view those items that have not been marked as deleted. one table called current collections or one virtual table of view called current collections. If I were to update farmers working at dawn to be marked as deleted, what would happen? This deleted column would become a one and I would not see it in current collection. So our goal then is to reimplement something like this.

**9:57:45** · But now not using a view in this case using a stored procedure we could simply call to find all the items that have not been marked as deleted. So to create a stored procedure we have some syntax we can use that syntax looks a bit like this. We could say create procedure and give it some name.

**9:58:12** · Well, this procedure we could call maybe current collections being able to view what is inside our collection and not marked as deleted. We could then similar to a trigger say begin after which we say the SQL statements we want to run as part of this procedure. So begin we then type the SQL statements we want to run and finally say end. This is the end of our procedure.

**9:58:42** · And then later on, we could use a statement called call to call this procedure over and over again. So let's work on creating our very first stored procedure to find all the items in our collection that have not been deleted.

**9:59:00** · Well, I'll go back to my MySQL server and I'll show you a new database I've made. Here I can type show databases semicolon. And now I should see I have not just the default MySQL databases, I also have the MFA database. So if I type use use MFA semicolon, I should see database changed. Now all my future queries will run on this MFA database.

**9:59:31** · And so I could type show tables to see all the tables inside of this database. Hit enter and I'll see I have artists, collections, and created. I could even if I wanted to describe the collections table. Describe collections semicolon.

**9:59:48** · And now I'll see the description for this collections table here. I have an ID, title, accession number column, and an acquired column too. But what am I missing? I want to be able to implement soft deletes. If you were to look at this describe output, what am I missing?

**10:00:09** · If I want to implement soft deletes, you're missing the deleted column.

**10:00:15** · Yeah, the deleted column is not yet in this table. I know because I used describe here. So, I don't have deleted yet. But I can add it using alter table.

**10:00:23** · So, I'll come back to my computer and let me use alter table to add in this particular column. I could say alter table collections like this. And then I could use add column. Modify was good for modifying a column that already existed. Add column is good for adding a brand new column. I'll call this one deleted. And its type will actually be a tiny int. A tiny int. Why? Well, it's only ever going to be one or zero. I should use as few bits as possible, and tiny int gives that to me.

**10:00:55** · Now I'll say the default value is zero for not deleted. And I'll hit enter. And now if I describe collections again, describe collections. I should see that I'm back to having a deleted column of type tiny int with a default value of zero. Okay.

**10:01:16** · So now we saw I could select everything from collections that's not deleted by saying something like select star from collections where deleted equals zero. I could implement the same thing here, but now using a stored procedure, something I could call again and again and again to speed up this process just a little bit. So I'll say I want to create this procedure current collections. But there's something a little interesting about the MySQL syntax here.

**10:01:44** · If you remember, if I go back to some slides here, in the middle of begin and end, we're going to put our very own SQL statements to run as part of this procedure. Well, to end a SQL statement, we have to have a semicolon. But MySQL might actually prematurely end this statement. If I type create procedure name begin some statement, then a semicolon, it'll say, "Okay, you're done." But I'm actually not. I might want to add more statements.

**10:02:16** · I might want to conclude with this end down here. So a workaround is to temporarily declare a different delimiter. Instead of ending my queries with semicolon here, I'll end them with let's say slash slash. And we'll see that in just a moment here. I'll come back to my computer and for the sake of writing this procedure, I'll change my delimiter. that is what icon represents the end of my query to slash slash like this. Then I'll hit enter.

**10:02:47** · Now I can start creating my procedure. I'll say create procedure and I'll call this one current current collections with a open and close parenthesis after this. This is common for names here. Then I'll say begin this procedure. And in this procedure I want to select the title accession accession number and acquired columns.

**10:03:14** · I want to do it from the collections table where deleted equals zero. And now I can safely include a semicolon because my delimiter for this entire query is a slash slash. So this is the end of this particular query inside my procedure.

**10:03:38** · It's also the end of my procedure in general. And now to declare the end of this procedure, the end of this overarching statement, I could say slash slash instead of semicolon. Now if I hit enter, I'll see query. Okay. And now I should change back to in this case semicolon. So I can get back to what I'm used to using to end my queries. I'll hit enter. And now let's see what we can do. Well, I could say call current collection.

**10:04:09** · I think we called it collection singular. And I'll say this semicolon there. Now I should see all of the items that are marked as not deleted. So using call, can I then call this procedure I've made and stored?

**10:04:27** · Let's try deleting something. I'll try maybe deleting farmers working at dawn. I could say update in this case collections and set deleted set deleted equal to one where the title equals farmers working at dawn. Farmers working at dawn semicolon. I'll hit enter again.

**10:04:49** · I'll see one row has changed. If I call current collection again like this semicolon enter I'll see that that particular artwork is now gone is not returned to me by the query that was part of my procedure.

**10:05:07** · So this then is one example of a stored procedure. One way of saving a query and calling it again and again if I might use it very often. But what questions do we have so far on stored procedures and how we can use them?

**10:05:22** · I have a question that just like in other languages do we have the provisioning that we can pass some parameters and arguments in the function in the procedure as well in MySQL. And secondly, can we call other procedures also in one procedure like in other languages we have one function call from other?

**10:05:37** · Yeah, a great question about the power of stored procedures. So the first question, could I add parameters or arguments to this procedure and could I change what I do based on that input?

**10:05:46** · The answer is absolutely yes, you can in MySQL and I'll show you that in just a minute here. The next one, which is can I call other procedures inside my procedure? Yes to that as well. Any statement you might write, you could probably put in a procedure too. Okay, let's take one more.

**10:06:06** · Yes, I have a question. uh there is any way that I can add any note or comment to the table.

**10:06:13** · Ah could you add any note or comment to your table? Um a good intuition like it's good to include notes to yourself or to include notes to others. To my knowledge you would best do that in something like a schema.sql file. If you have a um a text editor you could make a SQL file and store your schema inside of that. at which point you could leave comments to other developers to make them know what you were thinking as you were building this. There might be a way to leave comments in MySQL, but I don't personally know what that is.

**10:06:43** · You could do some research to look that up, too.

**10:06:48** · Okay, great question. Let's keep going then into our question about procedures and trying to make sure they could have inputs. Let's see that as well. Well, we saw too that I might want to mark some particular item as sold as soon as I mark it as being deleted. So, for that, I'll need a new table here. If I type um show tables semicolon, I'll see artists, collections, and created.

**10:07:15** · But back in our week on um the MFA, we also had a table to keep track of transactions when we might buy and sell some piece of artwork. So let's recreate that table here. I'll create a table called transactions. Create table transactions like this. And then I'll give it an ID column with the type int and auto increment. Then I'll give it a title to mark as being sold or bought.

**10:07:46** · Let's say the title is a var of size up to 64 and it can't be null. Then I'll say the action which can be either bought or sold. Do we buy or sell this piece of artwork with this particular title? So I'll say this is an enum with the possibility of bought or sold. Then I'll say this is not null. And I'll then say the primary key, primary key of this table is ID.

**10:08:17** · And I'll close out this create table statement here. Hitting enter. Now I can see I have a transactions table to log the buying and selling of pieces of artwork.

**10:08:31** · Well, it stands to reason that when I update my uh my collections table and I set some item to be deleted from a zero to a one that deleted column I want to add it to the transactions table and also mark it as sold. So normally that is two steps updating the table and also adding it to transactions. With a procedure though I could give that entire sequence one name. So let's try that here. I'll say I want to make a my delimiter slash.

**10:09:04** · I'm going to create some procedure here. I'm going to end it with slash. So I'll say create procedure and I'll call this one cell like this. But now instead of open parenthesis and close parenthesis, I actually want to give some input to this function. And let me actually ask you all here like what kind of input should I give to this cell function so I can identify the painting I want to sell.

**10:09:36** · Uh should we like uh do a primary key and refer to the name of the painting probably.

**10:09:42** · Yeah, I like your thinking. We could think about what identifies this artwork. Maybe it's the ID or the title.

**10:09:48** · In this case, I like your intuition for the ID which is unique, will never change. So let's actually use the ID here of an item in the collections table to mark it as sold. So I'll come back to my computer and I'll say that cell actually takes an input and I can say in here to note a um value as an input.

**10:10:09** · I'll say the input is something called sold sold ID the item we're selling and the type of this is an int like this. So now I have a procedure that takes in some value, an integer called sold ID. Now I'll say let's begin this procedure.

**10:10:28** · Let's begin down below. And the first thing I should do is update update collections like this and set deleted equal to one under what condition or perhaps under the condition where the ID is equal to our input which is called sold ID. So I'm using the input of sold ID to find in collections which artwork I'm marking now as deleted.

**10:10:55** · But the next step I'll say semicolon here to end that step is to then insert into the transactions table. I've marked it as being deleted but now I need to insert into transactions. I'll say then I want to insert into insert into transactions in the title in the title and action columns some values here. Well, what values?

**10:11:22** · The first value is actually the title of this artwork and I only have the ID right now. But I could use the ID to get back the title. I could say write a subquery that is select in this case title from collections where the ID equals sold sold ID like this. That is a subquery that gives me back the title of this artwork.

**10:11:50** · Now I'll also log sold here like this and then I think that's the end for that particular query there. I'll hit let me just double check this. Insert in transactions title action value select title from collections where id equals sold ID sold. Okay, I think we're good. I'll hit enter on that. And then I think I can safely end my procedure. I'll say end here. Slash enter again. I see everything was okay.

**10:12:21** · So now if I change my delimiter, change my delimter back to a semicolon, I can call sell on some particular ID like let's say I now want to sell the particular item. I could say maybe select star from collections to see what I have. And now I want to sell imaginative landscape which has the ID of two. Well, I could try call cell. And now pass in that value two. Call cell two.

**10:12:52** · And if I now hit enter, I should see some rows were affected. This procedure worked. Let me check. I'll say select star from collections semicolon.

**10:13:04** · And I'll see that that piece now has been updated. This value was zero, but now it's one for the deleted column. Now if I say select star from transactions semicolon I'll then see imaginative landscape being sold here as well. So good check here. Let me actually just check on this. So I think this was the ID was two and that actually makes sense here. So the ID we're thinking about and it is different here.

**10:13:33** · So this is the ID of the transaction which is different than the ID of the painting which is two just to clarify that.

**10:13:42** · Okay. So what other questions then do we have on stored procedures? We've seen some without inputs now some with inputs. What else are you wondering?

**10:13:54** · Is it possible to pass in multiple inputs to a store procedure?

**10:13:58** · Yeah, could it have multiple inputs? It absolutely could. separated by some commas inside of those parentheses. So you could imagine in sold ID int, some other input as well. And a procedure can also um output some value. You could say I want to store the result in some variable I could keep track of in the server too.

**10:14:19** · Let's keep going then and we'll f we'll kind of end store procedures on this note here which is I seem to if I go back to what I um had discussed before I was able to update some item in my collections table and then add it to the uh transactions table too. So if I say select star from collections, there is some danger here.

**10:14:43** · Like if I try to sell something that has already been sold, I might run the procedure and mark something as being sold twice. Now I'll actually leave this up to you as your own exercise, but I want to give you a few tools to think about for writing your own procedures.

**10:15:00** · Among them are some constructs you might be familiar with if you've programmed before. So here you might notice a stored procedure can actually uh be compatible with some familiar programming syntax like conditions for example if else if and else and also loops like the ability to do something more than once or to repeat something over and over and over again. So you can use these to really build up your own store procedures to combine statements and automate processes that you're going to do very frequently on your database at large scale.

**10:15:31** · So we've seen here some options for stored procedures. What we'll do is come back and talk next about Postgress. See you in a few. And we're back. So we've seen so far MySQL which is a new DBMS that allows you to do just a bit more than SQLite at a larger scale. It's worth also taking a brief detour into Postgress just to get a taste for what it looks like and get an understanding for how it can represent some of these same tables in a different environment.

**10:16:01** · So we'll talk here about Postgress and our goal will be to do the same thing we did with MySQL converting our tables from SQLite over to Postgress taking advantage of some new types and some new affordances it might offer that are particular to Postgress itself. So here then is our table we used for cards in SQLite just to remind you again we had an ID column of type integer and that was our primary key.

**10:16:31** · Well, we saw in MySQL we had a variety of integers and here we actually have the same thing in Postgress but they just look a little bit slightly different. So here I have a table of integers in Postgress the signed and signed values over here going from negative to positive. So unlike MySQL which had tiny int, uh medium int and so on, in Postgress we only have small int, int and big int.

**10:16:59** · Just a little bit fewer options because the developers thought you might not need a tiny int or a medium int just give you three particular options. Now although there are fewer integer options, we also get something a little bit different. I can also use a serial type, small serial, serial or big serial.

**10:17:20** · Now a serial is still an integer, a whole number, but it actually does what we try to do in MySQL for me, which was try to include an auto increment attribute. A serial will automatically increment for me, making it good for primary keys.

**10:17:39** · So here, if I go back to my cars table and I had this ID column of type integer, I could update that to now be a serial where a serial means some whole integer number that will increase as I add more and more data to my table. Now what else do you notice here? Well, it seems like these double quotes are back in Postgress. So in MySQL, you had back ticks. In SQLite, you had double quotes.

**10:18:11** · Well, in Postgress, you have double quotes for your identifiers here. So, this then is how we've changed our cards table. And now, let's actually do this inside of Postgress. I'll log in and create my very own database and my own table. So, I'll come back to my computer here. And now, let me do this. I will log into Postgress using this command right here.

**10:18:37** · I'm going to open PSQL which is essentially the command line interface like MySQL but now just for Postgress. I'll hit enter here and I'll log in as the default Postgress user.

**10:18:52** · This is the admin for Postgress. Now I'll type in my password and I'll see a prompt look just a little bit different but the same kind of spirit here. If I want to list all databases I don't type show databases. I just type back slashl for list and now I'll hit enter here and now I'll see a collection of default databases that come with the Postgress installation. Similar to MySQL, these are databases that contain configuration information metadata on this installation of Postgress.

**10:19:23** · But now I want to create my own database one called MBTA. So I'll say create database same as before and call it MBTA. now using double quotes. If I hit enter now, I should see create database. It's confirming this statement. And if I type back slashl, I'll now see MBTA is included in my list of databases.

**10:19:51** · So if I want to connect to a database in MySQL, I used use in Postgress, I'll use back slash C. So I'll say back slash C and then MBTA. Hit enter. And now I'm connected to the database MBTA as this user whose name is Postgress.

**10:20:14** · And now if I want to see what tables I already have, I could type back slashdt, hit enter, and I'll see no relations, no tables, but just another way of figuring out this is an empty database.

**10:20:29** · So we've seen so far how to log in to Postgress and some basic navigational statements we can use to work our way around this database. But it turns out there is some stuff that's familiar here. Like if I want to create a new table, I can do it the very same way I did it before. I could use create table.

**10:20:49** · I could say create table. Let's say cards. And then let me include in this case an ID column of type serial which means an integer that auto increments for me. Then I'll apply the primary key constraint. Familiar old friend here.

**10:21:10** · Then I'll close out cards like this. Hit enter. And I should see it confirms I created this table. If I now type slashdt to list my tables, I'll see I have a table called cards. And if I want to look at this table in particular to understand its schema, I could type slashd and then the name of that table cards like this. Hit enter. And now I should see some more information on this cards table.

**10:21:42** · It has a column called ID, a type called integer, and some more information like we saw in MySQL, but now just in a different format.

**10:21:54** · So, not to worry if these commands come uh a little bit seem maybe arcane to you at first glance. You'll get used to it with some practice if you choose to learn either MySQL or Postgress here. So let me pause before we go any further and just ask what questions so far do we have on Postgress if any?

**10:22:14** · What's the sort of thing that indicates it's an error?

**10:22:18** · Um a good question. So similar to SQLite or MySQL, you'll know you have an error when you hit enter and it doesn't say either query okay or repeat to you that um command you just used. It might give you a particular error like maybe you forgot a comma, maybe you forgot a quote somewhere. It should kind of give you an idea of what you didn't do correctly with the syntax. The best way to see it is just to try it and figure out what it tells you as you go.

**10:22:46** · Okay, let's keep going then and we'll see a few differences between Postgress and MySQL 2. So, we have our cards table, but our other goal was to create a stations table. So, let me pull up what we did for this one. Let me find stations here. So this was our stations table with Postgress or sorry with SQLite we had an ID a name and a line column integer text and text for those types.

**10:23:15** · Now we've seen in Postgress I could change this integer for my primary key to be a serial that's a little more apt for this use case here. And it turns out that in Postgress I also have varchars I could use inside of this station's table. I could make name a varchchar here up to size 32 characters.

**10:23:35** · And for simplicity though we used an enum earlier. I'll now use a varchchar for line as well just to keep things simple. So here we've updated our stations table using what postgress might offer us. The real differences though come not in our stations table but actually inside of our other table. This one called swipes. So this here was our swipe table or some section of it.

**10:24:01** · We had ids up top and primary key and foreign key constraints down below. Now remember we had type of text, date time of numeric and amount of numeric as well. Well, Postgress offers some other types we could use to update these as well. Among them are enum, our old friend again, but we use enum a little bit differently. So instead of including enum inside of our column definition, we actually create our very own type.

**10:24:34** · Postgress supports something like this.

**10:24:37** · Create a type and give it some name. And then I could say what that type actually is. So here I've created some type and called it swipe type and then said this type can have the following values enter exit or deposit and I can then use this name swipe type as my very own type in future create table statement. So something that Postgress has that my SQL might not in this form let's consider then dates and times.

**10:25:08** · So dates and times largely similar. I have timestamp, date, time, and interval. A particular type representing the distance between times.

**10:25:19** · How long did something take? But we still have our old friends date and time for dates and times respectively. And also time stamp to combine these two into one. And then we also have precision with these. I could say I want to represent to the hundreds place, the thousand's place or so on for each of time stamp, time and interval.

**10:25:42** · Continuing on, we could also work with real numbers which are largely the same amenities between MySQL and Postgress with a few differences. One is that at least in Postgress we call decimal numeric. So numeric in this case can specify some precision that is the number of digits and the scale that is the number that come after the decimal point and new word to postgress is a

**10:26:08** · type particularly for money which depending on your settings in your database will put to you either a certain number of decimal points and include perhaps a dollar sign or a euro sign or a pound sign whatever it is you're using and whatever it is you've configured in your database. So let's update now. Let's go ahead and improve this statement in swipes from SQLite to Postgress. Here I had type well that could now be our very own swipe type.

**10:26:38** · Notice here I defined up above as an enum. Now I'm going to use it down below in my swipes table. This type column has the type swipe type and it cannot be null. Then I'll keep going and I'll make datetime just timestamp. timestamp is the newer version in Postgress of what um MySQL had called datetime and what

**10:27:02** · SQLite called numeric and then instead of let's say current time stamp postgress just uses this function called now the current time stamp it will get for you as you add some new row and then finally amount we could use money we could use uh numeric we'll stick in this case to just numeric like we did for mysql and say numeric IC up to five digits, two of which come after the decimal point. So a whirlwind tour of some differences in types between MySQL and Postgress.

**10:27:34** · What questions do we have on these? Not seeing too many here. Let me keep going. Come back to my computer here. So it's worth um showing that we're able to create a table. We can then show it and describe it like this.

**10:27:52** · But then the question remains how do you get out of Postgress? Well, for that you can use let me clear my screen simply slash Q whereas in MySQL you could use quit in Postgress it's slash Q. So I'll hit enter on this and we'll say goodbye to Postgress for now but after the break we'll come back and keep working with MySQL and focus on actually what features we can use to scale up our applications. What does MySQL and Postgress offer to serve more users more frequently? Back in a few.

**10:28:24** · And we're back. So, we've gotten a taste so far of both MySQL and Postgress, but now it's time to think through the features each offers up to scale up our application. So, let's envision a sample application here, one that starts off pretty small. We have users trying to read from this database about a hundred times per minute, but they're also writing to the databases, adding new data about 50 times per minute.

**10:28:52** · And maybe this application over time, it grows a little bit. Maybe instead of a 100 reads, it goes up to a thousand. It multiplies by 10. And same thing for our rights, they also multiply on average by about 10. And this application, it gets even more popular, increases by tenfold again. Now we have 10,000 reads per minute, 5,000 writes per minute, and then finally it keeps growing another tenfold.

**10:29:22** · And now we're at a 100,000 reads per minute and 50,000 writes per minute. What might be the problem? If I had a single server like this, why might my application start to slow down?

**10:29:41** · Uh so yeah, I would like to say that whenever the requests are increasing with that the time to which the server would reply would also increase and the list would seem to grow on and on. So yeah.

**10:29:55** · Yeah, I like your thinking there. So you can think of the time that each query takes. As we saw in our optimizing lecture, we could time our queries. And if I have many, many, many of those queries running all at one time. I mean, that could add up substantially. So it's worth thinking about whether one computer can really handle all of these reads and all of these writes. So if you find yourself writing some application and it per behaves a little bit slower than you want it to at particularly at scale, you have a few options.

**10:30:25** · And I want to ask you just to use your own intuition here. Like if you encounter this problem of your application slowing down, what might you try to do to solve that problem? Uh, you could try to you could try to optimize your queries.

**10:30:48** · Yeah, try to optimize your queries. Make sure they take a little less time than they did before. Or you could even try to throw more hardware at the problem. Like maybe you have optimized your queries to the maximum you think you can and it's just still not fast enough.

**10:31:02** · Well, one approach might be what's called vertical scaling. trying to make this single server all the more um quicker at replying to your queries. So vertical scaling is about increasing your application's capacity by increasing the capacity of a single server, the computing power of that server.

**10:31:23** · So whereas this was our regular old server, you could imagine trying to vertically scale this server, just make it more powerful, optimize your queries and have them run on this server faster than they did before. But there's also another approach you could take. Here we focused on one server, but what else could you logically do to just have more resources at your disposal? Actually, we can horizontally scale up our server.

**10:31:52** · We can add two or three more servers so we can manage it.

**10:31:59** · Yeah, I like your thinking. So, maybe we buy a fancier server like this. But if we ever run out of this server's capacity, well, the only logical thing is to buy more servers. Like, let's have not just one but three, for instance.

**10:32:14** · And this is an example of horizontal scaling. So horizontal scaling is increasing your application's capacity not by increasing a single server's computing power but by spreading it out buying more servers to handle that load across more in this case individual people who can do work on those queries.

**10:32:35** · So horizontal scaling might look a bit more like this. We have not just one server but now three overall. So this process of having not just one server but multiple. It's a process called replication. So replication is keeping copies of your database not just on one server but on multiple. And this seems like a good idea. Like wouldn't it be great to have a copy of your data not just in one place but in multiple.

**10:33:04** · Maybe you yourself have made a backup of your own data on your computer. This is not a dissimilar idea, but it turns out there are some challenges with this. Like it's very complicated to have servers communicate with themselves to keep track of who has the most recent updates. Uh who should I follow, who should lead and so on. And so for that reason, there are a few models of replication that you should at least know about.

**10:33:33** · Among them are single leader replication, multiler replication and leaderless replication. So single leader means that there is a single database server out there that takes in the incoming rights to an application, the updates to some data and that single server passes them on to some copy to take care of making sure it's redundant that this data is stored not just in one place but multiple places too.

**10:34:05** · Multile means there's not just one server listening for updates. There are multiple. And suffice to say, it gets a lot more complicated when there are more than one leader trying to listen for updates and process them. And finally, there are some other ones like leader lists and some more that actually just do away with leaders altogether and do something totally different. But today, we'll focus on single leader. One of the most basic replication strategies you could try and one that is built into MySQL. So let's focus on this one here.

**10:34:36** · You could imagine in this case that you have a computer and you're trying to connect to some social network. Well, here are two databases. One is a leader and one is a follower. And just to check for understanding here, let's say I want to upload a profile photo. I'm updating some data to which server would I send that data? If I want to change something on the server, who's listening for that request?

**10:35:07** · I think that we will send to the leader because the other data servers would get data from the leader. They will get updated from the leader, but the I will send to the leader because it will have the latest data for other servers and other users.

**10:35:21** · Yeah, exactly right. So if I want to change some piece of data, I know by definition the leader has the most recent copy of that data and is also the designated server to process updates to my database, changes to its data like insertions or updates or deletions. So if I'm uploading some profile photo, I'll send this photo of of me right here to my leader and that leader will then take that profile photo and store it on the database.

**10:35:50** · But before long the leader will also talk to communicate with the follower make sure that the follower has a copy of this data elsewhere. So it will forward on this update to the follower who will then process it in turn. And now that both the leader and the follower have this data. Well, who could I ask to see the latest profile photo for Carter Zeni? Which server might have that? Both the server also has the data.

**10:36:21** · So I could ask either server for information on this profile photo. I could ask either the leader or the follower because each is storing a copy of this photo or rather a copy of its location on the server itself. Now let's say here I ask the follower for this profile photo so I can see it on my own browser. Here I'll ask the follower and get back that image inside of my own browser. But I could have asked either one to distribute that load across both of these servers.

**10:36:54** · Now this follower is what's known as a read replica. A read replica is a server from which we would only ever read data. If I ever wanted to update some photo or insert some new rows, I would never ask the follower. I would always ask the leader who's in charge so to speak of handling these updates and these rights to that database.

**10:37:20** · So the next step is to think about um not just the types of leaders that we have but also how they communicate. And in general there are two options for communication both synchronous and asynchronous. So synchronous means that the leader will wait for the follower to get the data and process it before doing anything else. It synchronizes with that follower.

**10:37:47** · Asynchronous though means the leader sends that data to the follower and doesn't wait for the follower to finish processing. It just keeps going and going hoping the follower is keeping up. So let's focus first on a few of these in particular on synchronous. Now in this diagram I have a client and a server. My client is my computer. The server is some database. And on this xaxis here left to right. I have time.

**10:38:18** · Well, if I want to make a request to this server, I might denote that with a line like this. My client sends some requests to my server. Maybe it asks for data or tries to update some photo. then that takes some time to get the request from my client to the server down here.

**10:38:38** · And the response itself also takes some time. Maybe the server responds, hey, everything's okay. I got your photo, here's your data, etc. It'll take some time for that to get back to me. So, between here and here, that's how long it took for me to receive some data from this server. Now let's focus on synchronous replication here where the leader and the follower are always in sync. So this might look a bit like this.

**10:39:06** · If I add in the follower and I have a leader and a follower, I might send that profile photo to the leader a bit like this. The leader then sends it to the follower down below and waits. It waits until the follower has confirmed they have received that photo. they have added to the database and now they send back a request saying look I got it everything is okay and now only at this

**10:39:33** · point once the leader has received the okay from the follower does it then communicate with me it then says everything's okay we got your photo this is great because it's redundant like I know for sure that my photo is on both the leader and the follower but there is a downside and looking at this diagram here. What do you think that downside might be?

**10:39:59** · Maybe it's too slow.

**10:40:00** · Yeah, exactly. It could be just too slow. Like if I have to wait for the follower to get the okay back to the leader and then back to me, that's just more time for me to wait. And maybe my application shouldn't wait around that long. You might use this though if you're working in finance or healthcare where you have to be doubly sure you have data stored exactly as you want it to be. But if you're like a social media site like a Facebook or a Twitter, I mean maybe you don't care if you lose a tweet every once in a while. It's okay.

**10:40:34** · So maybe synchronous isn't the best most ideal scenario for that as well. So let's think through now asynchronous. So we'll go back to asynchronous here and think through our diagram again. Well, in asynchronous, the leader doesn't wait around for the follower to get the data.

**10:40:51** · So to visualize, my client could send this to the leader. Maybe a photo update, for example. Then simultaneously, the leader tells me, I got your photo, everything's okay. And then send the photo to the follower. The follower might later on tell the leader that everything's okay, but the leader already told me, "Look, all good. We got your photo." So, there's nothing more to do after this. Now, this admittedly is faster. Like, this amount of time is much shorter.

**10:41:21** · But again, there is some downside here. Why might I not want to use asynchronous replication? At least in some cases, I would guess that it's um an issue with data being corrupted possibly.

**10:41:37** · So, you're right. There could be some data corruption here where let's say the leader sends some data to the follower and they confirm for me that that data has been received across all instances of these servers. Well, I mean later on maybe the follower encounters some problem and they don't actually follow through. Well, at that point I have had a bad contract with my leader. It told me that everything was okay, but actually it wasn't. So, there are all kinds of trade-offs here.

**10:42:02** · Um, whether in terms of the time that things take or redundancy, but it's up to you to decide which one might work best for your own use case, synchronous replication or asynchronous. Now, in addition to replication, there is some other strategy for scaling you should be at least familiar with, and this is a process known as sharding.

**10:42:24** · Now, sharding is great for really large data sets on the order of many, many, many gigabytes or terabytes of data that you just can't fit on a single server or a single computer. Sharding involves taking some data set like that and essentially splitting it up in some logical way across multiple servers like this. Maybe for simplicity, you have some database of names, and you decide that all of those names that begin with, let's say, A to I end up on this server here, this first one.

**10:42:55** · But then all those names J through R, well, they get stored on this server here. And S through Z, they get stored on this third server here. So our data has been split or sharded across multiple instances of some database server. And this is helpful because if I had a really large data set, it now is smaller on every individual database server. You could also organize your data by, let's say, primary key. Maybe you have 3,000 rows or 3,000 records.

**10:43:26** · And the first one through a,000, those go on this first server. The second, 101 to 2,000 inclusive, those go on the second server. And 2001 to 30,000 also inclusive, those go on that third server. Now, there's a lot of thought that goes behind the best way to shard your data. The goal is to really to avoid what we call um a hot spot wherein one database server becomes more frequently accessed or requested than others.

**10:43:57** · Like let's say for some reason the data in 101 to 2000 gets um accessed quite a lot. Well, now we're actually uh trying to um run into a problem here wherein one server gets overload. The same problem we're trying to guard against using sharding. So, it's important then to think about what's the best most logical way to distribute data. So, you don't have one server being accessed much more than another.

**10:44:27** · There's another problem here too, which is if I'm not using replication, I'm only using sharding. Well, let's say that one server goes down. What do we have now? Maybe we're missing all the names that went in the middle of um our partition. Or maybe we're missing all of those rows. Uh let's see, 101 to 2,00 for instance. And that would be what we call a single point of failure. If one system goes down, our entire system is now not usable.

**10:44:57** · So something to keep in mind as you work on sharding is also you could combine it with some strategies from replication to keep copies of your data across servers too.

**10:45:10** · So these are some features built into MySQL and Postgress for scaling but they also give user accounts and we can perhaps enhance our security by taking advantage of some of those user accounts. So let's talk now about this idea of access control trying to have users and only grant some of them certain permissions. So here we saw before I was logging into MySQL using the root user. The root user is the admin.

**10:45:39** · But I could just as easily create a new user perhaps one called Carter for myself. So I will open up MySQL again.

**10:45:49** · And in this case I will create a new user one named Carter. So to do so I can use this command here this statement here create a user whose name is Carter in single quotes. Now I can say they are identified by the password and this password is literally password P A S W D. It is one of unfortunately the most popular passwords. do not use his password.

**10:46:18** · So I will hit enter here and now I have created some new user named Carter and I can log in using that Carter username. So I'll create myself a new terminal here and I will try to log in to my SQL again. I will run this statement here.

**10:46:38** · I'll say MySQL which is the command line interface for the MySQL server and I will say I want to connect using this user carter before we used root but now I'll use Carter the host the place the server is located is 127.0.0.1 0.1 my own computer here. This is the IP for this very computer. I can then say dash P capital P for the port number 3306 by default. And finally P means prompt me for my password.

**10:47:10** · I'll type it in here. So I'll hit enter. And now I get prompted for the password. I'll type that in here. And now oh wait, I typed in my password. So let me try this again. So, I'll go back up and I will type in my password, which was password. Hit enter. And now I'm logged in as Carter. So, by default, if I try something like this, show databases.

**10:47:36** · Enter. I'll only see a few. Like, I'm pretty sure I had MBTA, MFA in here, and a few others, but I just can't see them. So when I create this new user, by default it has very few privileges, very few ways of accessing this database, but I could decide to grant some privileges. And just to show you, let me be root again for a second. Here I'm the admin.

**10:48:04** · I can do most anything I want. And notice how in here I have a new database. I can type show databases.

**10:48:11** · Enter. And I'll see I have a new database called ride share which is similar from a prior week on viewing and security. So if I say use ride share semicolon enter I could say select star from ride share semicolon. Now whoops sorry the table isn't rid share. Se star from rides then I'll hit enter here. And now I'll see all of the rides in the rides table which is part of the ride share database.

**10:48:42** · And if I look at this table in our week on viewing, we talked about eliminating some PII, personally identifiable information.

**10:48:55** · What was that PII here?

**10:48:59** · Seems it was the rider column, like the names of those riders. We know where each rider is going. But ideally, we should make a new view. One that allows us to see not the riders, but only their origins and destinations. Removing this pi of individuals names.

**10:49:18** · So, by default, Carter can't see this data, but neither can Carter see the view I made called analysis. If I go back to my computer here, I could type select star from analysis. Hit semicolon enter. And now I'll see the view I had made the virtual table that removes that PII. But here I'm logged in as root. If Carter wants to see this, I go over here, show databases. I can't even see the ride share database.

**10:49:49** · So the root user needs to grant access to Carter to see this particular view. Now for that I can use some syntax looks a bit like this here. I can use both grant and revoke. Grant means to give some privilege like select or update or delete on some table to a particular user. Revoke means simply to remove that permission. If I gave you select before, I'll now revoke it down below like this.

**10:50:22** · And there are many privileges you can use. You could use all like everything. Allow Carter to do literally everything he could do. There's create to create tables and views and so on. There's insert to add data, select to read, and all the way down this list. Look at documentation to figure out what you can use here.

**10:50:42** · So I want to give Carter, it seems like a select privilege on the view I created for analysis in this database. So I'll come back over here and I'll try that. I will log in as root here and I will try to grant the um let's see grant the

**10:51:03** · select permission privilege on the ride share database in particular the analysis table inside of it and I'll grant that to Carter like this semicolon and enter now I'll see the query is okay If I log back in as Carter down here and now type show databases, enter, I should see I can now see the ride share database. So I'll type use ride share semicolon database changed.

**10:51:35** · I could say show tables and what do I see but that virtual table that view called analysis. So now as Carter I can select I can uh select star from analysis semicolon and see that same data but I can't see the ride data. If I say select star from rides that table that's currently hidden to me I get back you don't have permission.

**10:52:07** · So this is the benefit of MySQL's users and privileges to make sure I could have multiple users accessing this database and then only allowing some to access confidential data. So let me ask now what questions we have on access control in MySQL and Postgress. uh if we have to like ask for everything, do we grant uh is there any like particular syntax for that or should we type on all the uh like select right and everything?

**10:52:41** · Yeah, a great question here. Like if you want to give somebody multiple privileges, what could you do? One approach is you could say grant and then say the privilege and then have a comma afterwards. I could grant select, comma, insert, comma, etc. including the tables that I this user can insert, update, delete on, etc. You could also use all like if I say grant all on star.star to Carter, that means grant all permissions on everything to this user named Carter.

**10:53:13** · So you can absolutely do either of those approaches, but best to be more fine grained, particularly in a production environment.

**10:53:23** · Okay, great questions here. So let's keep going. So this then was how to uh use access controls. Um but it's also worth thinking about ways we can prevent other kinds of attacks and harden the security of our database. Like here I have users and passwords which works well. But if I were to expose my application to the outside world, I should also be concerned about a few other attacks here. Now, one of these attacks is a SQL injection attack.

**10:53:55** · SQL injection means I have some query and somebody else adds in some malicious code to finish that query for me. So, for example, maybe I have a query like this select ID from the users table where the username equals someone's username and the password equals somebody's password.

**10:54:21** · And if I find a user matching this username and password, if I get back an ID, I'll log that user in. Now, in a regular website, if someone was actually behaving nicely, they could type in their username like this, and they could type in their password a bit like this. This is kind of what I did before. I logged in as Carter and gave the password of password.

**10:54:46** · And when you are entering your own username and your own password on some website, something similar to this is likely happening. There might be some SQL query that takes your username and takes your password and inserts them into a SQL query to figure out are you who you say you are. But let's think a bit more maliciously about this.

**10:55:07** · Like here, if I gave you permission to add anything to this dot dot dot here, anything at all, what could you do to try to hack this database to log in as Carter? Keep in mind that this is selecting an ID from users where some condition is true. What might you be able to add to this dot dot dot to log in as me?

**10:55:35** · Yes, you could use some u kind of statements like union or with or delete something, etc.

**10:55:47** · Yeah, I could really put most anything I want in here. But the SQL injection attack comes about when I deliberately put some SQL statement that I think will give me access to some data I shouldn't have access to. So you could imagine maybe I type in my password but then I type you know a single quote followed by or 1 equals 1. Now what would that do?

**10:56:10** · Well notice that 1 equals 1 that condition will always be true. And so this condition where username equals Carter and password equals password.

**10:56:20** · Well, in that case, I have access to Carter's account because I modified the condition to just always be true whether or not the password is correct. Let's see one more example here. Maybe I'm logging into my bank account and I want to check my balance. We could maybe assume that the bank has some table of balances or has some people of accounts that have balances. And I could type in my account number like this. you know, 1 2 3 4 all the way up to number nine here. And that will give me access to my accounts balance.

**10:56:53** · But now let's take a look at this query here. Select balance from accounts where ID equals the account number. What kinds of SQL statements could you include in this ID value here to get access to everyone's account balances? So we basically have a where which does some ID. If we just commented that part out then it would be a sort of a problem.

**10:57:22** · Or if we just did the similar example to the last time like putter or one is equal to one that could also trigger it. So there are multiple options.

**10:57:35** · Yeah

**10:57:35** · I like your thinking here. There's definitely more than one option. I like your thinking of maybe we include some comment that kind of messes up this query. Maybe it removes the condition.

**10:57:46** · So I just get select balance from accounts. That could be one strategy. I could maybe include um an or that maybe makes sure that this wear is just always true. Give me back all balances from this account. I could also use as well a union like this. I could say make sure I add my own account ID. But then union some other query like this union select ID from accounts.

**10:58:12** · Now I have all the account ids from this table and I could then query them one at a time for their balance. So let's try this out in MySQL to see some of the dangers of these injection attacks. Go back to my computer here and I'll show you how I already have a database set up for this.

**10:58:35** · If I type show databases, hit enter. I see bank is one database here. Well, I want to use that database. I'll say use bank and then hit enter semicolon. Um, and now I can say show tables where I see an accounts table and I'll select star from accounts. Enter semicolon here to see some familiar users and some familiar balances.

**10:59:05** · So let's actually complete this injection attack we just saw on the slides. Maybe this bank has some feature where I can choose some ID. I can enter in my own account ID to see my balance.

**10:59:20** · So on the website they complete this query for me. I give them let's say the ID one. I am Alice in this case. They might finish this. They might say select star from accounts where the ID equals 1. And they might automatically run this SQL query. I'll hit enter. And now I'll see the balance for this account. Well, now what else could I do? I could try to deliberately mess up this query to run my own SQL injection attack.

**10:59:51** · I could select let's say star from accounts and then let me try where the id equals 1. I give them one but I also give them some SQL statements they unwittingly execute.

**11:00:07** · I say union and then select uh star from accounts bit like this. Now I'll hit enter. And if I complete this query, I see not just my own, I see everyone's balances and their names, too. So, this is one demo of how SQL injection attacks can show and leak data that isn't intended to be leaked. And sadly, these are fairly common today among people who just aren't familiar with how to prevent them.

**11:00:39** · So let me ask now what questions we have on these attacks before we get to how to guard against them.

**11:00:48** · Can we use some regular expressions also?

**11:00:52** · Ah could you use regular expressions? So if you're familiar a regular expression is some pattern of characters that can match some text and find values within some text. I personally haven't seen regular expressions being used for injection attacks but that doesn't mean they can't be. So always do your research on what you can and can't use for an injection attack. But a good question here.

**11:01:16** · Okay. So we've seen now SQL injection attacks, but how do we prevent them?

**11:01:21** · Well, one strategy is using what we call a prepared statement. A prepared statement is kind of what it sounds like. A prepared statement is a pre-prepared statement. Is a statement that we will later on insert some values into. We might treat it like a fill-in- thelank, like here is my select and I'll let you fill in what you want me to select, but I'll make sure to clean your input before actually adding it in. So, let's think through a few of these here.

**11:01:51** · Here I have prepare name from statement. This is a SQL statement I can use to prepare some statement to take some user input to make sure that when I add in that user input nothing malicious will happen. And in particular I can make sure the statement looks something a bit like this. Select balance from accounts where ID equals question mark.

**11:02:16** · This question mark is just a question mark, but syntactically it stands for the ability of this statement to clean whatever I put inside of it to make sure it doesn't inadvertently run SQL code. I don't want it to run. So, let's try making our very own prepared statement to guard against these kinds of insertions here. I'll go back to my computer and let's try this one out.

**11:02:46** · I could go back to MySQL and let me prepare some statement. I could say let's prepare a statement called balance check like we had before.

**11:03:02** · And now if I try to prepare this statement from the following select star from accounts where the ID equals question mark end quote semicolon. So in single quotes I have the query I'm trying to prepare to take user input and I'm giving it some name like balance check. So I'll hit enter now and I'll see the query is okay. Statement prepared.

**11:03:30** · Now if I want to run this statement to check on somebody's balance, I can go through a few steps. I could first set my own variable. Like let's say I get some user input from the user. They type in one underneath the hood in SQL. I could say set this variable called ID equal to one. this at symbol. It's just a uh convention for variables in MySQL.

**11:04:01** · Now I'll hit enter. So the user input is stored separately in some variable, not inside of my SQL query like we saw before. Now I can execute I can say execute in this case the balance check statement using that same variable at id. So that question mark I had before, I will then take whatever the user typed in and clean it and then substitute in that value into this.

**11:04:32** · So I'll say using ID and now I get back Alice's balance.

**11:04:41** · And just to be clear here, let me try to make this deliberately malicious. I want to see everyone's accounts. Well, we saw before that I completed this query by typing in let's see set at id equal to one, but then union select star from accounts. This was what I added to that query to show me everyone's account balances. And I'll try to do the same here. I'll say this is what I'm trying to substitute into this prepared statement. I'll hit enter.

**11:05:11** · Now execute again. I'll say execute balance check using at id which has an ID but also some malicious SQL statements. Now if I hit enter, what do I see? Only Alice's balance. So it seems that the prepared statement cleans up my input, ensures that if I have SQL statements, they don't get run.

**11:05:36** · So we've seen now SQL injection attacks and how to guard against them. What questions do we have?

**11:05:47** · So for this previous example you shown us, does the prepare statement only take into account the first uh the first acceptable condition or how does it work?

**11:05:57** · Yeah, good question. So here, let me show you again the ID that I had um put inside of here. So if I say select at ID like that, I'll see this is the value of ID one union select star from accounts.

**11:06:12** · And what happens is this paired statement does a process called escaping. It finds all of the SQL keywords, all of the values that could be malicious and escapes them. So they don't actually get executed. So it seems like in this case what actually happened was type in the query again. Balance check was select star from accounts where id equals 1. It seems like it just did the equals one part to give me back in this case the account balance while cleaning up the rest of it overall.

**11:06:46** · Okay, let's take one more question here.

**11:06:49** · So, uh is this the same reason why we shouldn't use a formatted string in Python to execute a SQL query?

**11:06:58** · Yeah.

**11:06:58** · So if you're familiar with Python format strings, it's a similar kind of pitfall which is you can add in any possible value for this variable you're substituting into and that can lead to some unintended consequences. So similarly, should we create um prepared statements that can actually clean and um escape the data that we might want to insert into our queries or our statements over there too? Good question.

**11:07:26** · Okay, so we've seen here SQL injection attacks and also how to guard against them. And actually by now you're pretty well equipped to go off into the world of databases. And even though this is our last week, I hope you think back on how far you have come. So you began by querying a single table, a table of books in this case. You then graduated into tables that were related of books and authors and publishers and so on and querying those as well.

**11:07:56** · Afterwards, you saw how to design your own databases, learn about types and create table statements to build something up from scratch. Finally, you saw how to write, how to add data to those databases you had designed. And then you kept going.

**11:08:14** · You saw how to view databases, how to see them in a more simplified light, how to optimize those queries, and finally today, how to scale up all of this so we can serve more and more users. So, I hope after all these weeks that you are proud of how much you've grown. We are certainly proud of you all, too. Now, go off and continue your learning. We'll see you later.