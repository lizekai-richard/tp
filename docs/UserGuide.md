---
layout: page
title: User Guide
---

ProfNUS is a **desktop application which helps SOC Professors who have many modules with many students/TAs to manage.** It is optimized for users who prefer CLI over GUI so that frequent tasks can be done faster by typing in commands.

* Table of Contents
{:toc}

--------------------------------------------------------------------------------------------------------------------

## Quick start

1. Ensure you have Java `11` or above installed in your Computer.

1. Download the latest `addressbook.jar` from [here](https://github.com/se-edu/addressbook-level3/releases).

1. Copy the file to the folder you want to use as the _home folder_ for your AddressBook.

1. Double-click the file to start the app. The GUI similar to the below should appear in a few seconds. Note how the app contains some sample data.<br>
   ![Ui](images/Ui.png)

1. Type the command in the command box and press Enter to execute it. e.g. typing **`help`** and pressing Enter will open the help window.<br>
   Some example commands you can try:

   * **`list`** : Lists all contacts.

   * **`add`**`n/John Doe p/98765432 e/johnd@example.com a/John street, block 123, #01-01` : Adds a contact named `John Doe` to the Address Book.

   * **`delete`**`3` : Deletes the 3rd contact shown in the current list.

   * **`clear`** : Deletes all contacts.

   * **`exit`** : Exits the app.

1. Refer to the [Features](#features) below for details of each command.

--------------------------------------------------------------------------------------------------------------------

## Features

<div markdown="block" class="alert alert-info">

**:information_source: Notes about the command format:**<br>

* Words in `UPPER_CASE` are the parameters to be supplied by the user.<br>
  e.g. in `add n/NAME`, `NAME` is a parameter which can be used as `add n/John Doe`.

* Items in square brackets are optional.<br>
  e.g `n/NAME [t/TAG]` can be used as `n/John Doe t/friend` or as `n/John Doe`.

* Items with `…`​ after them can be used multiple times including zero times.<br>
  e.g. `[t/TAG]…​` can be used as ` ` (i.e. 0 times), `t/friend`, `t/friend t/family` etc.

* Parameters can be in any order.<br>
  e.g. if the command specifies `n/NAME p/PHONE_NUMBER`, `p/PHONE_NUMBER n/NAME` is also acceptable.

* If a parameter is expected only once in the command but you specified it multiple times, only the last occurrence of the parameter will be taken.<br>
  e.g. if you specify `p/12341234 p/56785678`, only `p/56785678` will be taken.

* Extraneous parameters for commands that do not take in parameters (such as `help`, `list`, `exit` and `clear`) will be ignored.<br>
  e.g. if the command specifies `help 123`, it will be interpreted as `help`.

</div>

### Viewing help : `help`

Shows a message explaning how to access the help page.

![help message](images/helpMessage.png)

Format: `help`


### Adding a person: `add`

Adds a person to the address book.

Format: `add n/NAME p/PHONE_NUMBER e/EMAIL a/ADDRESS [t/TAG]…​`

<div markdown="span" class="alert alert-primary">:bulb: **Tip:**
A person can have any number of tags (including 0)
</div>

Examples:
* `add n/John Doe p/98765432 e/johnd@example.com a/John street, block 123, #01-01`
* `add n/Betsy Crowe t/friend e/betsycrowe@example.com a/Newgate Prison p/1234567 t/criminal`

### Listing all students : `list`

Shows a list of all the students in the module with their contact information in the application.

Format: `list MODULE_NAME [MORE_MODULE_NAMES]`
- The module name is case-insensitive. e.g CS1101S will match cs1101s
- Students matching at least one module will be returned
- Only exact module matches will be returned. e.g. CS1231 will not match CS1231S

Examples:
- `list CS1101S returns` Alex Yeoh and Bernice Yu
- `list CS1101S CS1231S` returns Bernice Yu only`

![list](images/userguide/list.png)


### Viewing list of modules : `mlist`

Shows a list of all modules in the address book.

![mlist](images/userguide/mlist.png)

Format: `mlist`


### Editing a person : `edit`

Edits an existing person in the address book.

Format: `edit INDEX [n/NAME] [p/PHONE] [e/EMAIL] [a/ADDRESS] [t/TAG]…​`

* Edits the person at the specified `INDEX`. The index refers to the index number shown in the displayed person list. The index **must be a positive integer** 1, 2, 3, …​
* At least one of the optional fields must be provided.
* Existing values will be updated to the input values.
* When editing tags, the existing tags of the person will be removed i.e adding of tags is not cumulative.
* You can remove all the person’s tags by typing `t/` without
    specifying any tags after it.

Examples:
*  `edit 1 p/91234567 e/johndoe@example.com` Edits the phone number and email address of the 1st person to be `91234567` and `johndoe@example.com` respectively.
*  `edit 2 n/Betsy Crower t/` Edits the name of the 2nd person to be `Betsy Crower` and clears all existing tags.

### Locating persons by name: `find`

Finds persons whose names contain any of the given keywords.

Format: `find KEYWORD [MORE_KEYWORDS]`

* The search is case-insensitive. e.g `hans` will match `Hans`
* The order of the keywords does not matter. e.g. `Hans Bo` will match `Bo Hans`
* Only the name is searched.
* Only full words will be matched e.g. `Han` will not match `Hans`
* Persons matching at least one keyword will be returned (i.e. `OR` search).
  e.g. `Hans Bo` will return `Hans Gruber`, `Bo Yang`

Examples:
* `find John` returns `john` and `John Doe`
* `find alex david` returns `Alex Yeoh`, `David Li`<br>
  ![result for 'find alex david'](images/findAlexDavidResult.png)

### Deleting a person : `delete`

Deletes the specified person from the address book.

Format: `delete INDEX`

* Deletes the person at the specified `INDEX`.
* The index refers to the index number shown in the displayed person list.
* The index **must be a positive integer** 1, 2, 3, …​

Examples:
* `list` followed by `delete 2` deletes the 2nd person in the address book.
* `find Betsy` followed by `delete 1` deletes the 1st person in the results of the `find` command.

### Clearing all entries : `clear`

Clears all entries from the address book.

Format: `clear`

### Exiting the program : `exit`

Exits the program.

Format: `exit`

### Saving the data

AddressBook data are saved in the hard disk automatically after any command that changes the data. There is no need to save manually.

### Editing the data file

AddressBook data are saved as a JSON file `[JAR file location]/data/addressbook.json`. Advanced users are welcome to update data directly by editing that data file.

<div markdown="span" class="alert alert-warning">:exclamation: **Caution:**
If your changes to the data file makes its format invalid, AddressBook will discard all data and start with an empty data file at the next run.
</div>
### Add a teaching schedule `sadd`

Adds a schedule of a module in the adressbook. 

**Format**: `sadd m/MODULE_CODE w/WEEKDAY ct/PERIOD cc/CLASS_TYPE cv/VENUE `

- Adds a schedule with the module it belongs to, the weekday, the time period, the type of the class, and the venue.
- `MODULE_CODE` needs to abide by the [Module Code Format of NUS ](https://www.nus.edu.sg/registrar/docs/info/nusbulletin/AY201213_GeneralInformation.pdf) 
- The `WEEKDAY` should be one of `Monday`, `Tuesday`, `Wednesday`, `Thursday`, `Friday`, `Saturday` and `Sunday`.
- The `PERIOD` includes the start time and the end time which are both in the format of the *modern 24-hour clock*.
- The `CLASS_TYPE` should be one of `lec`, `tut`, `lab`, and `rec`, which represent lecture, tutorial, laborartory, and reflection respectively.

<div markdown="span" class="alert alert-warning">:exclamation: **Caution:**
Please make sure you have added the module with `MODULE_CODE` before you add any schedules with `MODULE_CODE`. Otherwise, address book will consider the command to be invalid.
</div>

<div markdown="span" class="alert alert-warning">:exclamation: **Caution:**
If the schedule to be added conflicts with any existing schedule, the address book will not perform any operation.
</div>

**Example**: `sadd m/CS2103T w/Friday ct/16:00-18:00 cc/lec cv/I3-AUD`



### View your teaching schedule: `view schedule`

Views the teaching schedule that have been added to the address book.

**Format**: `view schedule [-w WEEKDAY] [-m MODULE_CODE] [-d DATE] [-h] [-v]`

- `-w WEEKDAY` option shows your schedule on the `WEEKDAY`. `WEEKDAY` should be one of `Monday`, `Tuesday`, `Wednesday`, `Thursday`, `Friday`, `Saturday` and `Sunday`.
- `-m MODULE_NAME` option shows your weekly schedule of `MODULE_CODE`.
- `-d DATE` option shows your schedule on the `DATE`. `DATE` should comply with the format `yyyy-mm-dd`
- `-h` option shows your schedule table in a horizontal mode (time will be columns and weekdays will be rows).
- `-v` options shows your schedule table in a vertical mode (weekdays will be columns and time will be rows).
- The result will be a timetable in vertical mode by default if no option is specified.

**Notes about the syntax**:

- `-w WEEKDAY` option and `-d DATE` option cannot be used at the same time.
- If either `-w WEEKDAY`, `-m MODULE_NAME` or `-d DATE` is used, the result won't be a timetable. Instead, it will be shown as a list of slots.
- `-h` and `-v` options can only be used when the result is shown as a timetable.
- `-h` option and `-v` option cannot be used at the same time.

**Examples**:

- `view schedule -w Monday -m CS2103T`

  <div align=center><img src="./images/view schedule -w Monday -m CS2103T.png" width=300px></div>

- `view schedule -d 2022-09-12`

  <div align=center><img src="./images/view schedule -d 2022-09-12.png" width=300px></div>

- `view schedule -h` 

  <div align=center><img src="./images/view schedule -h.png" width=500px height=250px></div>



### Archiving data files `[coming in v2.0]`

_Details coming soon ..._

--------------------------------------------------------------------------------------------------------------------

## FAQ

**Q**: How do I transfer my data to another Computer?<br>
**A**: Install the app in the other computer and overwrite the empty data file it creates with the file that contains the data of your previous AddressBook home folder.

--------------------------------------------------------------------------------------------------------------------

## Command summary

Action | Format, Examples
--------|------------------
**Add** | `add n/NAME p/PHONE_NUMBER e/EMAIL a/ADDRESS [t/TAG]…​` <br> e.g., `add n/James Ho p/22224444 e/jamesho@example.com a/123, Clementi Rd, 1234665 t/friend t/colleague`
**Clear** | `clear`
**Delete** | `delete INDEX`<br> e.g., `delete 3`
**Edit** | `edit INDEX [n/NAME] [p/PHONE_NUMBER] [e/EMAIL] [a/ADDRESS] [t/TAG]…​`<br> e.g.,`edit 2 n/James Lee e/jameslee@example.com`
**Find** | `find KEYWORD [MORE_KEYWORDS]`<br> e.g., `find James Jake`
**List** | `list`
**Help** | `help`
