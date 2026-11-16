# Project – Training Log

**Individual Project Brief – Week 6 · u08**

Start: Monday, 16 November 2026. Show the working program on Monday, 23 November 2026.

## The Idea

You build a small training diary that reads itself. You keep your trainings in `training.csv` — date, activity, minutes, distance in kilometres — and the program reads the file, computes the pace of every training, adds up the weeks, finds your best and your slowest run, and draws the minutes per week as a PBM bar chart.

The program is small, but every line in it does real work: it converts text into numbers, divides one number by another, protects itself from a division by zero, and turns the totals into a picture. This is the first project where the file is not an exercise file but your own data.

## Why This Project Is Yours

You played football in a club, you train, and you built things with Arduino and Scratch, where a mistake is visible immediately — a motor does not turn, an LED does not light. A training log gives you the same feedback: a number in the file changes a bar in the picture. You have not written Python before this course, so this project deliberately uses only what the five weeks have already given you, plus careful thinking about numbers.

## What You Already Have

- Lists, indexing, `for` loops, conditions and comparisons.
- `int()` and `float()` conversions, `%s` and `%d` formatting.
- Reading files line by line with `strip()` and `split(",")`.
- The PBM format from last week: a `P1` header, then a grid of `0` and `1`.

## The New Thing

Two details decide whether this program is correct or only looks correct. Find out how to:

1. Read a decimal number from a file, and why `int("7.5")` fails while `float("7.5")` works.
2. Format a number with exactly two decimals, and what `%.2f` does with `7.0`.
3. Divide by a value that may be zero, and what error Python raises when it is.
4. Protect a division without hiding it: check the value, then decide what the program prints.
5. Compute minutes per kilometre from minutes and kilometres, and check that the unit of the result is what you think it is.
6. Sum a week of trainings when the dates are text, not dates.

**Write it down:** Create `notes.md` with `## The New Thing – dividing safely`. Write the rule in two sentences, give one example with real numbers from your file, and describe what your program does with a training that has `0` kilometres. Then add one sentence about the mistake you made first and how you found it.

## The Plan

### Milestone 1 – Your own data

Create `training.csv` by hand.

1. Four columns: `date,activity,minutes,km`. Use dates in the form `2026-11-02`.
2. At least fourteen rows, over three weeks, with three activities: `run`, `ride`, `gym`.
3. Include one row with `0` kilometres, and one row with a distance written with two decimals.
4. Keep a paper total of the minutes, so that you can check the program later.

### Milestone 2 – Read and print

Create `training_log.py`.

1. Read the file line by line, `strip()` every line and `split(",")` it.
2. Skip the header row.
3. Convert the minutes to an integer and the distance to a float.
4. Print each row as an aligned line: date, activity, minutes, distance.

At the end of this step the terminal shows your whole file as a readable table.

### Milestone 3 – One training, one pace

1. For every training with a distance above zero, compute minutes per kilometre.
2. Format it with two decimals and print it in a fifth column.
3. For a training with zero distance, print `--` instead of a number.
4. Check two rows by hand with a calculator and write the results in `notes.md`.

At the end of this step no row crashes the program, and the `--` row is a decision, not an accident.

### Milestone 4 – Totals and records

1. Sum the minutes, the kilometres and the number of trainings with loops. Do not use `sum()`.
2. Find the longest training and the fastest pace, keeping the whole row of the winner.
3. Count the trainings per activity with two parallel lists.
4. Print a summary with the count, the total time in hours and minutes, the total distance with one decimal and the average pace of the runs.

At the end of this step the totals agree with your paper total from Milestone 1.

### Milestone 5 – Weeks

1. Group the trainings by the week they belong to. Use the first ten characters of the date, or the week number if you prefer — but write down which rule you chose.
2. Count the trainings, the minutes and the kilometres per week.
3. Write `summary.txt` with one line per week and a final line for the whole period.
4. Print the same summary on the screen.

### Milestone 6 – The chart

1. Create `weeks.pbm` with one bar per week, eight rows tall, scaled so that the longest bar is at most two hundred pixels.
2. Draw the bars in black, one under the other, with one empty row between them.
3. Print the same bars to the terminal with `#` and `.`.
4. Compare the terminal picture with `summary.txt` and check that the tallest bar belongs to the week with the most minutes.

## Example

```text
Reading training.csv
date        activity  minutes   km    pace
2026-11-02  run          42.0   7.50   5.60
2026-11-03  gym          55.0   0.00     --
2026-11-05  ride         68.0  24.30   2.80
2026-11-07  run          38.0   6.80   5.59
...

14 trainings
Total time: 11 h 21 min
Total distance: 124.7 km
Average pace (runs): 5.55 min/km

by activity
run    7 trainings, 284 minutes
ride   4 trainings, 245 minutes
gym    3 trainings, 152 minutes

summary.txt
week        trainings  minutes   km
2026-11-02          5      245   44.6
2026-11-09          5      238   41.8
2026-11-16          4      198   38.3
total              14      681  124.7

Saved weeks.pbm (200x26)
```

## Requirements

- One program, `training_log.py`, started from the terminal with `python3 training_log.py`.
- Every number is converted explicitly, with `int()` or `float()`; nothing is compared as text.
- The average pace uses only the runs, and a training with zero distance does not stop the program.
- Totals, minimum and maximum are found with loops, not with `sum()`, `min()` or `max()`.
- `summary.txt` and the terminal output agree, line for line.
- `weeks.pbm` has a correct header and one bar per week, including a week with no trainings if one exists.
- The program reads the file from the same directory, so it runs after `cd training_log`.

## Files

```text
training_log/
├── training.csv
├── training_log.py
├── summary.txt
├── weeks.pbm
├── notes.md
└── check.py
```

Commit the whole directory to your repository and push it before the Monday session. A directory that exists only on your laptop cannot be checked.

Run `python3 check.py` in the project directory before you commit. It reads the files your program produced, not your code, and prints one line per requirement.


## How It Will Be Checked

- The total minutes and kilometres match the rows of the file.
- A row with `0` distance produces `--` and does not change the average pace.
- Changing one row in `training.csv` changes the totals and the bars, without editing the code.
- The number of trainings in the summary equals the number of data rows.
- `weeks.pbm` is a valid PBM file and its bars are proportional to the minutes.
- You can explain what happens in the program when a distance is zero.

**Hint:** Do the conversion once, when you read the row, and keep the converted values in a list. If you convert in one place and not in another, the same row will behave differently in two lines of the program — and that is where the crash will come from.

**Additional challenge:** Add a second file, `plan.csv`, with your planned trainings for next week, and compare the plan with the executed trainings: how many minutes are missing, which activity is behind. Write the comparison to `plan_check.txt` and say in `notes.md` which line of the comparison you would show a coach first.

## Suggested Learning Resources

- [Numbers in Python – `int`, `float` and conversions](https://docs.python.org/3/library/stdtypes.html#numeric-types-int-float-complex)
- [String formatting with `%` – `%.2f` and field widths](https://docs.python.org/3/library/stdtypes.html#printf-style-string-formatting)
- [Errors and exceptions – `ValueError` and `ZeroDivisionError`](https://docs.python.org/3/tutorial/errors.html)
- [Reading and writing files](https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files)
- [Netpbm – description of the PBM format](https://netpbm.sourceforge.net/doc/pbm.html)

**Final goal:** By the end of this project, you should have a program that reads your own training file, converts and protects its numbers, computes totals, records and paces, writes a weekly summary, and draws the weeks as a PBM chart — using loops, conditions, lists and file handling from the first five weeks.
