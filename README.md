# Ruby Database
A repo building a database backed Ruby CLI application (WIP).

### Basic Overview
This is an expense tracking CRUD program written in Ruby that allows users to:
1) List 
2) Add
3) Delete individual and all
4) Search

Expenses through the CLI, and uses the `pg` gem to connect with a Postgres database.

### How to Run
This program is intended to run locally. Once you've cloned the repo, please run `bundle install` to make sure you've got the appropriate gems installed. You will also need to have Postgres installed locally so that expenses can be saved to a database - you can see [how to do this here](https://wiki.postgresql.org/wiki/Homebrew).

Once you have the correct gem versions and Postgres installed, you can use the `./expense` command in your terminal of choice. You can use the following commands:
- `./expense list`: This will list all the expenses contained in the database so far.
- `./expense add amt, "memo"`, where `amt` is a `FLOAT` type less than `10000` and `memo` is a `STRING` type, which should be surrounded by double quotes `"`. This allows the user to add an expense to the database.

### Design Choices
I made use of two main classes here:
1. The CLI class, which handles formatting the input and arguments from the CLI
2. The ExpenseData class, which handles the communication with the database and formatting and displaying results

I chose this split of responsibilities since we can have a class that completely handles the conversion __to__ Ruby (`CLI`) and another class that handles everything __in__ Ruby (`ExpenseData`). While I could split off another class to handle the formatting and displaying of results, for a program this small, I think it's fine. I might choose to refactor this later on.

### Challenges
The design of the application is always hard - I'm not entirely sure what classes and responsibilities those classes should have ahead of time, and I feel like I'm adjusting on the fly to figure out where methods should live, and what objects should interact with other objects.
