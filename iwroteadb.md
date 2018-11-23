# I wrote a database! Say what?
First of all, before you start imagine something like PostgreSQL or MongoDB, let me remind you that a database is _"an organized collection of data, generally stored and accessed electronically from a computer system."_ [source](https://en.wikipedia.org/wiki/Database)

## Why?
Because I wanted to. It's as simple as that. And well, because I wanted to put what I had learned in a C++ to use. I can't remember when, or why, I got the idea of writing my own database. If I can make a guess it was probably when I was diving into MongoDB and realising that working with databases doesn't always have to be cumbersome, but sometimes, it can actually be quite nice too.

## How?
I'm going to be honest, I've read a lot about writing programming languages and how to implement them, ([this tutorial](http://lisperator.net/pltut/) is great), and many of the concepts are the same, specifically the user input parsing and the corresponding code structure.

With the preamble quote about what a database is, together with my (scarce) knowledge of C++ and what I've previous read about programming language implementation, I set sail! The outcome? BedlamDB.

I decided early on that I wanted to keep it simple, so I started to implement a [key-value database](https://en.wikipedia.org/wiki/Key-value_database), to begin with. I diverted from that idea however, somewhere when I started to implement a format checker, and decided upon what one could call a key-less database, only storing values. Because why not? The user can fetch entries using the `print_entry` command, which will print all entries containing what the user is searching for. But what if I want one special, specific entry? Then I have to tell you that I'm sorry, BedlamDB doesn't believe in uniqueness as you can store the same data over and over again. I was on the verge of implementing a timestamp for each entry, but that would make each entry unique, wouldn't it?

## Insights?
It was easy, almost too easy, to reach an MVP level. Don't get me wrong, I'm not trying to sound like a know-it-all, only a couple of months ago I would have buckled beneath the task and moved on to something else. No one knows how many home projects I've stared only to quit them because I got stuck knowledge-wise, because I lost interest, or even both. But something kept me going this time, and I think a large portion of that "something" is the knowledge and experience I've collected during my failed projects.

## What is BedlamDB, and what isn't it?
Today, BedlamDB is a simple Windows application which can be run completely out of the box after build. There are no automatic tests however, all testing has been done by me manually. Automatic tests will be implemented in due course. I've also chosen to not implement any authentication at this time. Mostly because I wanted to keep the application as simple as possible. The code of BedlamDB will (hopefully) improve as I learn more about C++. If you who are reading this discover something I've missed, improvment suggestions etc. feel free to make a pedagogical merge request!

I have some ideas for the development including more commands, writing a driver for another language etc. But, only time will tell where this project end up! Also, if you have any feature suggestions or ideas of your own and want to contribute, feel free to [contact](mailto:beanilsson1@gmail.com) me!

### Technical perspective and design
The application consists of two modes (Overview and Single DB), each having their own commands. This results in the user having to enter Single DB mode for a specific database before they can perform operations like `insert` and `print_content`. The reason why I implemented this design, rather having one mode (or state perhaps?) of the application, is because the latter would require the user to type the database name every time they wanted to perform an action on it. Examples in pseudo code below.

With the different modes:
```
$ open database my_db
my db$ insert abc123
my db$ print_content
my_db$ delete_content
```

Without:
```
$ insert abc123 my_db
$ print_content my_db
$ delete_content my_db
```
You might not all agree, but to me it feels a bit repetetive to type the name of the database over and over, and as stated in the [Lisperator PL tutorial](http://lisperator.net/pltut/dream): _"The nice thing about writing your own language is that you can do it as you like it."_ And I think that goes for all things one make, at least on a personal/hobby basis. Don't constrain yourself to rules and standars if you don't like them. Implement to your own liking, which of course could lead to realising why the standars and rules are there in the first place :)

I also decided to create my own file extension, `.bedl` for the files where the databases are stored. Why? Well, in the beginning I stored the data in `.txt` files, but I wanted the databases to be associated by this application only. And yes, I know the "$" prompt might be more *nix than Windows-esque, but I prefer Ubuntu so ... There is also some inconsitencies between the usage of the `std::` prefix and where it is omitted due to the `using namespace std` declaration. I intend to clean this up eventually, but I'm torn between having to write `std::` infront of what feels like basically everything and deal with possible [ambiguites](https://stackoverflow.com/a/25538593/2750877).

The structure of a BedlamDB database looks like this:
```
{dataitem}{more data}{i am batman}{abc123}
```
Where each entry is saved within {} and the last entry is stored last, in this case `{abc123}`. There is currentyl no support for characters like ÅÄÖ.

## Where's the code?!
The source code for BedlamDB can be found (here)[https://github.com/beanilsson/BedlamDB].
