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

You will need to create a local database called `expenses` before executing this program, using syntax similar to this:
```
createdb expenses
```
The program will take care of creating requisite tables if they don't exist.

Once you have the correct gem versions and Postgres installed, you can use the `./expense` command in your terminal of choice. You can use the following commands:
- `./expense list`: This will list all the expenses contained in the database so far.
- `./expense add AMT, "MEMO"`, where `AMT` is a `FLOAT` type less than `10000` and `MEMO` is a `STRING` type, which should be surrounded by double quotes `"`. This allows the user to add an expense to the database.
- `./expense delete ID`, will delete specific rows from the `expense` table, where `ID` is the primary key for the table.
- `./expense clear` will delete all expenses, after user validation.
- `./expense search TERM` will search for an expense where `TERM` (case insensitive) is found in the `memo` field for that expense.

### Design Choices
I made use of two main classes here:
1. The CLI class, which handles formatting the input and arguments from the CLI
2. The ExpenseData class, which handles the communication with the database and formatting and displaying results

I chose this split of responsibilities since we can have a class that completely handles the conversion __to__ Ruby (`CLI`) and another class that handles everything __in__ Ruby (`ExpenseData`). While I could split off another class to handle the formatting and displaying of results, for a program this small, I think it's fine. I might choose to refactor this later on.

### Challenges
The design of the application is always hard - I'm not entirely sure what classes and responsibilities those classes should have ahead of time, and I feel like I'm adjusting on the fly to figure out where methods should live, and what objects should interact with other objects.

There was some fiddliness towards collecting input from the CLI, eventually settling on `$stdin`. I initially tried to pull user input via `gets`, but if the `ARGV` constant (which captures any arguments passed as part of the program execution, in an `Array`) has any values in it (which must have in order to execute commands, in our implementation), then the `Kernel#gets` method tries to treat the first value in the `ARGV` array as a file, which in our case, never is.
