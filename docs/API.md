# Simple Calendar API

There are the functions that other modules, systems and macros can access and what they can do. Most of these are for advanced interfacing with Simple Calendar and not something everyone needs to worry about.

Simple Calendar exposes a variable called `SimpleCalendar`, all of these API functions exist the property api on that variable `SimpleCalendar.api`

## Properties
- [Calendars](#simplecalendarapicalendars)
- [LeapYearRules](#simplecalendarapileapyearrules)
- [MoonIcons](#simplecalendarapimoonicons)
- [MoonYearResetOptions](#simplecalendarapimoonyearresetoptions)
- [YearNamingRules](#simplecalendarapiyearnamingrules)

## Functions
- [changeDate](#simplecalendarapichangedateinterval)
- [chooseRandomDate](#simplecalendarapichooserandomdatestartdate-enddate)
- [clockStatus](#simplecalendarapiclockstatus)
- [configureCalendar](#simplecalendarapiconfigurecalendarconfig)
- [dateToTimestamp](#simplecalendarapidatetotimestampdate)
- [getAllSeasons](#simplecalendarapigetallseasons)
- [getCurrentSeason](#simplecalendarapigetcurrentseason)
- [isPrimaryGM](#simplecalendarapiisprimarygm)
- [secondsToInterval](#simplecalendarapisecondstointervalseconds)
- [setDate](#simplecalendarapisetdatedate)
- [showCalendar](#simplecalendarapishowcalendardate-compact)
- [timestamp](#simplecalendarapitimestamp)
- [startClock](#simplecalendarapistartclock)
- [stopClock](#simplecalendarapistopclock)
- [timestampPlusInterval](#simplecalendarapitimestampplusintervaltimestamp-interval)
- [timestampToDate](#simplecalendarapitimestamptodatetimestamp)

## Types
- [Calendar Configuration Object](#calendar-configuration-object)
- [Current Date Object](#current-date-object)
- [Date Object](#date-object)
- [Date Display Object](#date-display-object)
- [Date Time Object](#date-time-object)
- [First New Moon Object](#first-new-moon-object)
- [Interval Time Object](#interval-time-object)
- [Leap Year Object](#leap-year-object)
- [Month Object](#month-object)
- [Moon Object](#moon-object)
- [Moon Phase Object](#moon-phase-object)
- [Note Category Object](#note-category-object)
- [Season Object](#season-object)
- [Time Object](#time-object)
- [Weekday Object](#weekday-object)
- [Year Object](#year-object)

# Properties

## `SimpleCalendar.api.Calendars`

This is an enum that contains a list of all available predefined calendars within Simple Calendar.

**Important**: This is a list of keys used internally to determine which Predefined calendar should be used it does not return an object containing the configuration for a predefined calendar.

## `SimpleCalendar.api.LeapYearRules`

This is an enum that contains the options for how leap years are calculated. Options are:
 - **None**: No leap year rules
 - **Gregorian**: Follow the Gregorian leap year rules
 - **Custom**: Set up custom leap year rules

## `SimpleCalendar.api.MoonIcons`

This is an enum that contains a list of all available icons for moon phases.

## `SimpleCalendar.api.MoonYearResetOptions`

This is an enum that contains the options for when a moons first new moon year should be reset. Options are:

- **None**: The moons first new moon year is never reset.
- **Leap Year**: The moons first new moon year is reset every leap year.
- **X Years**: The moons first new moon year is reset every X years.

## `SimpleCalendar.api.YearNamingRules`

This is an enum that contains the options for how year names are applied to years. Options are:

- **Default**: From the year name starting year the names will be applied in order. When names run out no names will be used.
- **Repeat**: From the year name starting year the names will be applied in order. When names run out the list will repeat from the beginning.
- **Random**: Every year will be giving a random year name from the list.

# Functions

## `SimpleCalendar.api.changeDate(interval)`

Changes the current date of Simple Calendar.

**Important**: This function can only be run by users who have permission to change the date in Simple Calendar.

### Parameters

Parameter|Type|Default Value|Description
---------|-----|-------------|-----------
interval|[Interval Time Object](#interval-time-object)|No Default|The interval objects properties are all optional so only those that are needed have to be set.<br/>Where each property is how many of that interval to change the current date by.

### Returns

This function will return true if the date change was successful and false if it was not.

### Examples
```javascript
//Assuming a date of June 1, 2021 and user has permission to change the date
SimpleCalendar.api.changeDate({day: 1}); // Will set the new date to June 2, 2021

//Assuming a date of June 1, 2021 and user has permission to change the date
SimpleCalendar.api.changeDate({day: -1}); // Will set the new date to May 31, 2021

//Assuming a date of June 1, 2021 10:00:00 and user has permission to change the date
SimpleCalendar.api.changeDate({year: 1, month: 1, day: 1, hour: 1, minute: 1, second: 1}); // Will set the new date to July 2, 2022 11:01:01

//Assuming a date of June 1, 2021 10:00:00 and user has permission to change the date
SimpleCalendar.api.changeDate({second: 3600}); // Will set the new date to June 1, 2021 11:00:00
```

## `SimpleCalendar.api.chooseRandomDate(startDate, endDate)`

Will choose a random date between the 2 passed in dates, or if no dates are passed in will choose a random date.

### Parameters

Parameter|Type|Default Value|Description
---------|-----|-------------|-----------
startDate|[Date Time Object](#date-time-object)|{}|The start date objects properties are all optional so only those needed have to be set.<br/>Where each property is the earliest date to be chosen when randomly selecting a date.<br/>The month and day properties are both index's so January would be 0 and the first day of the month is also 0.
endDate|[Date Time Object](#date-time-object)|{}|The end date objects properties are all optional so only those needed have to be set.<br/>Where each property is the latest date to be chosen when randomly selecting a date.<br/>The month and day properties are both index's so January would be 0 and the first day of the month is also 0.

### Returns
The [Date Time Object](#date-time-object) returned has the following properties

Property|Type|Default Value|Description
---------|-----|-------------|-----------
year|Number|0|The randomly selected year
month|Number|0|The randomly selected month index
day|Number|0|The randomly selected day index
hour|Number|0|The randomly selected hour
minute|Number|0|The randomly selected minute
second|Number|0|The randomly selected second

### Examples

```javascript
SimpleCalendar.api.chooseRandomDate({year: 2021, month: 3, day: 0},{year: 2021, month: 5, day: 1})
/*
{
    day: 1
    hour: 12
    minute: 5
    month: 4
    second: 41
    year: 2021
}
 */

SimpleCalendar.api.chooseRandomDate({year: 1900, month: 3},{year: 2021, month: 5})
/*
{
    day: 19
    hour: 8
    minute: 16
    month: 3
    second: 25
    year: 1982
}
*/

SimpleCalendar.api.chooseRandomDate();
/*
{
    day: 11
    hour: 0
    minute: 49
    month: 8
    second: 37
    year: 3276
}
 */
```

## `SimpleCalendar.api.clockStatus()`

Will get the current status of the built-in clock in Simple Calendar

### Returns

The returned object has the following properties:

Property|Type|Description
---------|-----|-----------
started|Boolean|If the clock has started and is running.
stopped|Boolean|If the clock is stopped and not running.
paused|Boolean|If the clock has paused. The clock will be paused when the game is paused or the active scene has an active combat.

### Examples

```javascript
const status = SimpleCalendar.api.clockStatus();
console.log(status); // {started: false, stopped: true, paused: false}
```

## `SimpleCalendar.api.configureCalendar(config)`

Sets up the current calendar to match the passed in configuration. This function can only be run by GMs.

### Parameters

Parameter|Type|Default Value|Description
---------|-----|-------------|-----------
config|`SimpleCalendar.api.Calendar` or [Calendar Configuration](#calendar-configuration-object)|undefined|The configuration to set the current year to. It can be one of the predefined calendars or an [Calendar Configuration object](#calendar-configuration-object) representing a custom calendar.


### Returns

Returns a promise that resolves to a boolean value, true if the change was successful and false if it was not.

### Examples

```javascript

//Set the calendar configuration to the Gregorian calendar
const result = await SimpleCalendar.api.configureCalendar(SimpleCalendar.api.Calendars.Gregorian);

//Set the calendar configuration to a custom calendar
const custom = {};

const result = await SimpleCalendar.api.configureCalendar(custom);

```

## `SimpleCalendar.api.dateToTimestamp(date)`

Will convert that passed in date object to a timestamp.

### Parameters

Parameter|Type|Default Value|Description
---------|-----|-------------|-----------
date|[Date Time Ojbect](#date-time-object) or null|null|A date object (eg `{year:2021, month: 4, day: 12, hour: 0, mintue: 0, second: 0}`) with the parameters set to the date that should be converted to a timestamp. Any missing parameters will default to the current date value for that parameter.<br>**Important**: The month and day are index based so January would be 0 and the first day of the month will also be 0.

### Returns

Returns the timestamp for that date.


### Examples

```javascript
SimpleCalendar.api.dateToTimestamp({}); //Returns the timestamp for the current date

SimpleCalendar.api.dateToTimestamp({year: 2021, month: 0, day: 0, hour: 1, minute: 1, second: 0}); //Returns 1609462860
```

## `SimpleCalendar.api.getAllSeasons()`

Gets all the seasons for the calendar.

### Returns

This function returns an array of [Season objects](#season-object).

### Examples
```javascript
SimpleCalendar.api.getAllSeasons();
/*
    Returns an array like this, assuming the Gregorian Calendar
    [
        {
            color: "#fffce8",
            name: "Spring",
            startingDay: 19,
            startingMonth: 2
        },
        {
            color: "#f3fff3",
            name: "Summer",
            startingDay: 19,
            startingMonth: 5
        },
        {
            color: "#fff7f2",
            name: "Fall",
            startingDay: 21,
            startingMonth: 8
        },
        {
            color: "#f2f8ff",
            name: "Winter",
            startingDay: 20,
            startingMonth: 11
        }
    ]
 */
```

## `SimpleCalendar.api.getCurrentSeason()`

Gets the details about the season for the current date of the calendar.

### Returns

This function returns a [Season Object](#season-object).

### Examples

```javascript
SimpleCalendar.api.getCurrentSeason();
/* Returns an object like this
{
    name: "Summer",
    color:"#f3fff3",
    startingDay: 19,
    startingMonth: 5
}
*/
```

## `SimpleCalendar.api.isPrimaryGM()`

Returns if the current user is considered the primary GM or not.

### Examples

```javascript

SimpleCalendar.api.isPrimaryGM(); //True or Flase depending on if the current user is primary gm

```

## `SimpleCalendar.api.secondsToInterval(seconds)`

Will attempt to parse the passed in seconds into larger time intervals that make it up.

### Parameters

Parameter|Type|Default Value|Description
---------|-----|-------------|-----------
seconds|Number|No Default|The number of seconds to convert to different intervals.

### Returns

Returns an [Interval Time Object](#interval-time-object).

### Examples

```javascript
//Assuming a Gregorian Calendar
SimpleCalendar.api.secondsToInterval(3600); //Returns {year: 0, month: 0, day: 0, hour: 1, minute: 0, second 0}
SimpleCalendar.api.secondsToInterval(3660); //Returns {year: 0, month: 0, day: 0, hour: 1, minute: 1, second: 0}
SimpleCalendar.api.secondsToInterval(86400); //Returns {year: 0, month: 0, day: 1, hour: 0, minute: 0, second: 0}
SimpleCalendar.api.secondsToInterval(604800); //Returns {year: 0, month: 0, day: 7, hour: 0, minute: 0, second: 0}
SimpleCalendar.api.secondsToInterval(2629743); //Returns {year: 0, month: 1, day: 0, hour: 10, minute: 29, second: 3}
SimpleCalendar.api.secondsToInterval(31556926); //Returns {year: 1, month: 0, day: 0, hour: 5, minute: 48, second: 46}
```

## `SimpleCalendar.api.setDate(date)`

Will set the current date to the passed in date.

**Important**: This function can only be run by users who have permission to change the date in Simple Calendar.

### Parameters

Parameter|Type|Default Value|Description
---------|-----|-------------|-----------
date|[Date Time Object](#date-time-object) or null|null|A date object (eg `{year:2021, month: 4, day: 12, hour: 0, mintue: 0, second: 0}`) with the parameters set to the date that the calendar should be set to. Any missing parameters will default to the current date value for that parameter.<br>**Important**: The month and day are index based so January would be 0 and the first day of the month will also be 0.

### Returns

This function will return true if the date was set successfully, false if it was not.

### Examples

```javascript
//To set the date to December 25th 1999 with the time 00:00:00
SimpleCalendar.setDateTime(1999, 11, 24);

//To set the date to December 31st 1999 and the time to 11:59:59pm
SimpleCalendar.setDateTime(1999, 11, 30, 23, 59, 59);
```

## `SimpleCalendar.api.showCalendar(date, compact)`

Will open up Simple Calendar to the current date, or the passed in date.

### Parameters

Parameter|Type|Default Value|Description
---------|-----|-------------|-----------
date|[Date Time Object](#date-time-object) or null|null|A date object (eg `{year:2021, month: 4, day: 12}`) with the year, month and day set to the date to be visible when the calendar is opened.<br>**Important**: The month is index based so January would be 0.
compact|boolean|false|If to open the calendar in compact mode or not.

### Examples
```javascript
//Assuming a Gregorian Calendar
SimpleCalendar.api.showCalendar(); // Will open the calendar to the current date.
SimpleCalendar.api.showCalendar({year: 1999, month: 11, day: 25}); // Will open the calendar to the date December 25th, 1999
SimpleCalendar.api.showCalendar(null, true); // Will opent the calendar to the current date in compact mode.
```

## `SimpleCalendar.api.timestamp()`

Return the timestamp (in seconds) of the calendars currently set date.

### Examples
```javascript
const timestamp = SimpleCalendar.api.timestamp();
console.log(timestamp); // This will be a number representing the current number of seconds passed in the calendar.
```

## `SimpleCalendar.api.startClock()`

Starts the real time clock of Simple Calendar. Only the primary GM can start a clock.

### Returns

Will return true if the clock started, false if it did not.

### Examples

```javascript
SimpleCalendar.api.startClock();
```

## `SimpleCalendar.api.stopClock()`

Stops the real time clock of Simple Calendar.

### Returns

Will return true if the clock stopped, false if it did not.

### Examples

```javascript
SimpleCalendar.api.stopClock();
```

## `SimpleCalendar.api.timestampPlusInterval(timestamp, interval)`

Returns the current timestamp plus the passed in interval amount.

### Parameters

Parameter|Type|Default Value|Description
---------|-----|-------------|-----------
timestamp|Number| No Default |The timestamp (in seconds) to have the interval added too.
interval|[Interval Time Object](#interval-time-object)|No Default|The interval objects properties are all optional so only those needed have to be set.<br/>Where each property is how many of that interval to increase the passed in timestamp by.

### Examples

```javascript
let newTime = SimpleCalendar.api.timestampPlusInterval(0, {day: 1});
console.log(newTime); // this will be 0 + the number of seconds in 1 day. For most calendars this will be 86400

// Assuming Gregorian Calendar with the current date of June 1, 2021
newTime = SimpleCalendar.api.timestampPlusInterval(1622505600, {month: 1, day: 1});
console.log(newTime); // This will be the number of seconds that equal July 2nd 2021
```

## `SimpleCalendar.api.timestampToDate(timestamp)`

Takes in a timestamp (in seconds) and will return that as a Simple Calendar date object.

### Parameters

Parameter|Type|Default Value|Description
---------|-----|-------------|-----------
timestamp|Number| No Default |The timestamp (in seconds) to convert into a date object.

### Returns

A [Date Object](#date-object) is returned.



### Examples

```javascript
// Assuming Gregorian Calendar with the current date of June 1, 2021
let scDate = SimpleCalendar.api.timestampToDate(1622505600);
console.log(scDate);
/* This is what the returned object will look like
{
    currentSeason: {color: "#fffce8", startingMonth: 3, startingDay: 20, name: "Spring"},
    day: 0,
    dayDisplay: "1",
    dayOfTheWeek: 2,
    dayOffset: 0,
    display: {
        day: "1",
        daySuffix: "st",
        month: "6",
        monthName: "June",
        time: "21:03:35",
        weekday: "Tuesday",
        year: "2021",
        yearName: "",
        yearPostfix: "",
        yearPrefix: "",
    },
    hour: 0,
    minute: 0,
    month: 5,
    monthName: "June",
    second: 0,
    showWeekdayHeadings: true,
    weekdays: (7) ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"],
    year: 2021,
    yearName: "",
    yearPostfix: "",
    yearPrefix: "",
    yearZero: 1970
}
*/
```

# Types

## Calendar Configuration Object

This type contains all information for configuring a calendar.

Property|Type|Optional|Default|Description
--------|-----|-------|------|-----------
currentDate|[Current Date Object](#current-date-object)|Yes|{}|The current date of the calendar.
leapYearSettings|[Leap Year Object](#leap-year-object)|Yes|{}| The leap year settings for the calendar.
monthSettings|Array<[Month Object](#month-object)>|Yes|[]| An array of month settings for the calendar.
moonSettings|Array<[Moon Object](#moon-object)>|Yes|[]| An array of moon settings for the calendar.
noteCategories|Array<[Note Cateogry Object](#note-category-object)>|Yes|[]| An array of note categories for the calendar.
seasonSettings|Array<[Season Object](#season-object)>|Yes|[]|An array of season for the calendar.
timeSettings|[Time Object](#time-object)|Yes|{}| The time settings for the calendar.
weekdaySettings|Array<[Weekday Object](#weekday-object)>|Yes|[]| An array of weekday settings for the calendar.
yearSettings|[Year Object](#year-object)|Yes|{}| The year settings for the calendar.

## Current Date Object

This type contains information on the current date.

Property|Type|Optional|Default|Description
--------|-----|-------|------|-----------
year|Number|No|0|The current year.
month|Number|No|1|The current month's numeric representation.
day|Number|No|1|The current day's numeric representation.
seconds|Number|No|0|The current number of seconds passed in the current day.

## Date Object

This type contains the current date information

Property|Type|Default Value|Description
---------|-----|-------------|-----------
currentSeason|[Season Object](#season-object)|{}|The information for the season of the date, properties include "name" for the seasons name and "color" for the color associated with the season.
day|Number|0|The index of the day of the month represented in the timestamp.
dayDisplay|String|""|**Depreciated** Please use display.day instead. This will be removed when Foundry v9 Stable is released.
dayOfTheWeek|Number|0|The day of the week the day falls on.
dayOffset|Number|0|The number of days that the months days are offset by.
display|[Date Display Object](#date-display-object)|{}|All of the strings associated with displaying the date are put here
hour|Number|0|The hour represented in the timestamp.
isLeapYear|Boolean|false|If this date falls on a leap year.
minute|Number|0|The minute represented in the timestamp.
month|Number|0|The index of the month represented in the timestamp.
monthName|String|""|**Depreciated** Please use display.monthName instead. This will be removed when Foundry v9 Stable is released.
second|Number|0|The seconds represented in the timestamp.
showWeekdayHeadings|Boolean|true|If to show the weekday headings for the month.
sunrise|Number|0|The timestamp of when the sun rises for this date.
sunset|Number|0|The timestamp of when the sun sets for this date.
weekdays|String Array|[]|A list of weekday names.
year|Number|0|The year represented in the timestamp.
yearName|String|""|**Depreciated** Please use display.yearName instead. This will be removed when Foundry v9 Stable is released.
yearPostfix|String|""|**Depreciated** Please use display.yearPostfix instead. This will be removed when Foundry v9 Stable is released.
yearPrefix|String|""|**Depreciated** Please use display.yearPrefix instead. This will be removed when Foundry v9 Stable is released.
yearZero|Number|0|What is considered as year zero when doing timestamp calculations.


## Date Display Object

This type contains the formatted strings used to display the current date and time.

Property|Type|Default Value|Description
---------|-----|-------------|-----------
day|String|""|How the day is displayed, generally its number on the calendar.
daySuffix|String|""|The Ordinal Suffix associated with the day number (st, nd, rd or th)
month|String|""|The month number.
monthName|String|""|The name of the month.
time|String|''|The hour, minute and seconds.
weekday|String|""|The name of the weekday this date falls on.
year|String|""|The year number
yearName|String|""|The name of the year, if year names have been set up.
yearPostfix|String|""|The postfix value for the year
yearPrefix|String|""|The prefix value for the year

## Date Time Object

This type is used to indicate dates and times.

Property|Type|Optional|Default|Description
--------|-----|-------|------|-----------
year|Number|Yes|0|The year for the date time.
month|Number|Yes|0|The month for the date time. **Importat**: The month is index based, meaning the first month of a year will have a value of 0.
day|Number|Yes|0|The day for the date time. **Important**: The day is index based, meaning the first day of the month will have a value of 0.
hour|Number|Yes|0|The hour for the date time.
minute|Number|Yes|0|The minute for the date time.
second|Number|Yes|0|The second for the date time.

## First New Moon Object

This type is used to configure when the first new moon for a moon was.

Property|Type|Optional|Default|Description
--------|-----|-------|------|-----------
yearReset|[MoonYearResetOptions](#simplecalendarapimoonyearresetoptions)|No|`SimpleCalendar.api.MoonYearResetOptions.None`|If and when the year of the new moon should be reset.
yearX|Number|No|0|Reset the new moon year every X years.
year|Number|No|0|The year of the first new moon.
month|Number|No|1|The month of the first new moon.
day|Number|No|1|The day of the first new moon.

## Leap Year Object

This type contains information about leap year rules.

Property|Type|Optional|Default|Description
--------|-----|-------|------|-----------
rule|[LeapYearRules](#simplecalendarapileapyearrules)|No|`SimpleCalendar.api.LeapYearRules.None`|This is the leap year rule to follow.
customMod|Number|No|0|The number of years that a leap year happens when the rule is set to 'custom'.

## Interval Time Object

This type is used to indicate intervals of time.

Property|Type|Optional|Default|Description
--------|-----|-------|------|-----------
year|Number|Yes|0|The number of years making up the interval.
month|Number|Yes|0|The number of months making up the interval.
day|Number|Yes|0|The number of days making up the interval.
hour|Number|Yes|0|The number of hours making up the interval.
minute|Number|Yes|0|The number of minutes making up the interval.
second|Number|Yes|0|The number of seconds making up the interval.

## Month Object

This type contains information about a month.

Property|Type|Optional|Default|Description
--------|-----|-------|------|-----------
name|String|No|""|The name of the month.
numericRepresentation|Number|No|1|The number associated with the display of this month.
numericRepresentationOffset|Number|No|0|The amount to offset day numbers by for this month.
numberOfDays|Number|No|0|The number of days this month has during a non leap year.
numberOfLeapYearDays|Number|No|0|The number of days this month has during a leap year.
intercalary|Boolean|No|False|If this month is an intercalary month.
intercalaryInclude|Boolean|No|False|If this month is intercalary then if its days should be included in total day calculations.
startingWeekday|Number or Null|No|Null|The day of the week this month should always start on.

## Moon Object

This type contains information about a moon.

Property|Type|Optional|Default|Description
--------|-----|-------|------|-----------
color|String|No|"#FFFFFF"|The color associated with the moon.
currentPhase|[Moon Phase Object](#moon-phase-object)|Yes|{}|The moon phase for the current date. This option is present only in results from the [DateTimeChange hook](Hooks.md#datetime-change)
cycleDayAdjust|Number|No|0|A way to nudge the cycle calculations to align with correct dates.
cycleLength|Number|No|0|How many days it takes the moon to complete 1 cycle.
firstNewMoon|[First New Moon Object](#first-new-moon-object)|Yes|{}|When the first new moon was. This is used to calculate the current phase for a given day.
name|String|No|""|The name of the moon.
phases|Array<[Moon Phase Object](#moon-phase-object)>|Yes|[]|The different phases of the moon.

## Moon Phase Object

This type contains information about a moon phase.

Property|Type|Optional|Default|Description
--------|-----|-------|------|-----------
icon|[MoonIcons](#simplecalendarapimoonicons)|No|``|The icon to associate with this moon phase.
length|Number|No|0|How many days of the cycle this phase takes up.
name|String|No|""|The name of the phase.
singleDay|Boolean|No|False|If this phase should only take place on a single day.


## Note Category Object

This type contains information about a note category.

Property|Type|Optional|Default|Description
--------|-----|-------|------|-----------
name|String|No|""|The name of the note category.
color|String|No|""|The background color assigned to the note category.
textColor|String|No|"#FFFFFF"|The color of the text assigned to the note category.

## Season Object

This type contains information about a season.

Property|Type|Default Value|Description
---------|-----|-------------|-----------
name|String|''|The name of the season.
color|String|#ffffff|The color associated with this season.
startingDay|Number|1|The day index of the month that the season starts on.
startingMonth|Number|1|The month index that the season starts on.
sunrise|Number|0|The number of seconds into the starting day of the season that the sun rises. EG. a value of 3600 would be 1:00am in a Gregorian Calendar.
sunset|Number|0|The number of seconds into the starting day of the season that the sun sets. EG. a value of 82800 would be 11:00pm in a Gregorian Calendar.

## Time Object

This type contains information about how time is configured.

Property|Type|Optional|Default|Description
--------|-----|-------|------|-----------
hoursInDay|Number|No|24|The number of hours in a single day.
minutesInHour|Number|No|60|The number of minutes in a single hour.
secondsInMinute|Number|No|60|The number of seconds in a single minute.
gameTimeRatio|Number|No|1|When running the clock for every second that passes in the real world how many seconds pass in game.
unifyGameAndClockPause|Boolean|No|False|If to start/stop the clock when the game is unpaused/paused.
updateFrequency|Number|No|1|How often (in real world seconds) to update the time while the clock is running.

## Weekday Object

This type contains information about a weekday.

Property|Type|Optional|Default|Description
--------|-----|-------|------|-----------
name|String|No|""|The name of the weekday.
numericRepresentation|Number|No|0|The number representing the weekday.

## Year Object

This type contains information about a year.

Property|Type|Optional|Default|Description
--------|-----|-------|------|-----------
numericRepresentation|Number|No|0|The number representing the year.
prefix|String|No|""|A string to append to the beginning of a year's number.
postfix|String|No|""|A string to append to the end of a year's number.
showWeekdayHeadings|Boolean|No|True|If to show weekday headings on the calendar.
firstWeekday|Number|No|0|The day of the week the first day of the first month of year zero starts on.
yearZero|Number|No|0|What is considered to be the first year when calculating timestamps.
yearNames|Array<String>|No|[]|A list of names to use for years.
yearNamingRule|[YearNamingRule](#simplecalendarapiyearnamingrules)|No|`SimpleCalendar.api.YearNamingRule.Default`|How to calculate what year name to give to a year.
yearNamesStart|Number|No|0|The year to start applying the year names.