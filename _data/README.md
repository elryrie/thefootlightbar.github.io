# Data for Calendars

This folder contains files for working with and publishing event information to your website and other applications. It contains a number of different types of files (see [§ Files in this folder](#files-in-this-folder)). This includes both published artifacts and work-in-progress.

In general, the process looks like this:

1. You start by downloading and opening a spreadsheet, which is a file in this folder that ends in `.ods`.
1. Next, you edit the data in the spreadsheet to your liking. In this case, that means entering or deleting event information into the columns of the spreadsheet. Remember to save the spreadsheet regularly so you don't lose any of your work.
1. When the spreadsheet contains the correct data, you save it one last time, and then you *also* save another copy of the spreadsheet as a CSV (comma-separated values) file, using the "Save As…" menu item.
1. Upload the CSV file you prepared from the spreadsheet back into this folder.

The remainder of this document describes the above process in more detail and provides links to additional information.

## Files in this folder

* `README.md` - This help file. :)
* `example-calendar.ods` - Example spreadsheet containing sample events. This file is an [OpenDocument Format (ODF)](https://en.wikipedia.org/wiki/OpenDocument) Spreadsheet. You must use a free software application such as [LibreOffice](https://en.wikipedia.org/wiki/LibreOffice) to open and to work with the file. Programs you must pay for, like Microsoft Excel, will not work.
* Other files ending in `.csv` - Calendar data published by your website.

## Spreadsheets as Calendars

To work with event information, your website uses the same industry standard digital calendaring specification used by programs like Google Calendar, called [iCalendar](https://en.wikipedia.org/wiki/ICalendar). The iCalendar specification defines a set of datum that describes calendars and the event information those calendars contain. This data can be easily represented as data in a plain text file, where the individual data elements (start time, event name, etcetera) are written in a comma-separated values (CSV) file.

Each calendar published by your website is stored here as a CSV file. Each line in the CSV file is an event on that calendar. You can have as many calendars (CSV files) as you want. Similarly, you can have as many events in a calendar as you want. In practice, however, it is a good idea to prune old events from your calendars so that they do not accumulate.

Editing CSV files by hand can be hard, so instead we recommend that you use the supplied ODF Spreadsheet (the file ending with `.ods` but otherwise with the same name as the CSV file) to edit your calendar data. The ODF Spreadsheet also contains data validation and integrity checks to help make sure you don't accidentally set an event to start at "50 PM" instead of "5 PM." Once you edit the data in the spreadsheet, however, you must save the spreadsheet as a CSV file and replace the existing CSV file so that your website will pick up on the new data.

## Recurring events

If you have an event that happens "every week, on Monday at 10pm," you do not need to write out every occurrence of the event into your calendars. Instead, you can describe the pattern in which the event repeats.

## Field reference

The fields ("columns") in the CSV data file correspond approximately to the iCalendar specification (RFCs [5545](https://tools.ietf.org/html/rfc5545), [5546](https://tools.ietf.org/html/rfc5546), [6868](https://tools.ietf.org/html/rfc6868), and [7529](https://tools.ietf.org/html/rfc7529)). A brief overview of the purpose of those fields is described here. In some cases, the field is an exact implementation, such as in the case of `Summary`. Other fields are approximations that are used in concert with one another to generate valid iCalendar data, such as `Start_Date` and `Start_Time`. (Together, `Start_Date` and `Start_Time` map to the [`DTSTART`](https://www.kanzaki.com/docs/ical/dtstart.html) property of an iCalendar event object.) Further information can be found in the relevant Internet Engineering Task Force (IETF) documentation.

### `Summary`

### `Start_Date`

### `Start_Time`

### `End_Date`

### `End_Time`

### `Recurrence`

Valid values are:

* `HOURLY`
* `WEEKLY`
* `MONTHLY`
* `YEARLY` (This value is NOT YET IMPLEMENTED.)

### `Recurrence_Interval`

### `Recurrence_Count`

Specifies the number of times the event occurs. For instance, an event that repeats five times will have the value `5` in this field.

This field is ignored unless [`Recurrence`](#recurrence) also contains a valid value.

### `Location`

### `Description`

### `Image`

### `Status`

### `URL`

### `Categories`
