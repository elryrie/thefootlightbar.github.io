# The `_data` folder

This folder contains [Jekyll data files](https://jekyllrb.com/docs/datafiles/), which are used for controlling certain contents in your website. This includes files for ordering the navigation menus, images in the gallery, and for working with and publishing event information to your Web pages and other applications. It contains a number of different types of files (see [§ Files in this folder](#files-in-this-folder)) including both published artifacts and work-in-progress.

1. [Files in this folder](#files-in-this-folder)
1. [Events](#events)
1. [Gallery](#gallery)
1. [Navigation menus](#navigation-menus)

## Files in this folder

* `README.md` - This help file. :)
* [`events.csv`](#events) - Event information, including the name of each event, its start and end times, whether and how it repeats, and many other details.
* `example-events.ods` - Example spreadsheet containing sample events. This file is an [OpenDocument Format (ODF)](https://en.wikipedia.org/wiki/OpenDocument) Spreadsheet. You must use a free software application such as [LibreOffice](https://en.wikipedia.org/wiki/LibreOffice) to open and to work with the file. Programs you must pay for, like Microsoft Excel, will not work.
* [`gallery.yml`](#gallery) - Description of which images to display on your site's gallery, and in what order.
* [`nav_menus.yml`](#navigation-menus) - Description of which pages to link to from the navigation menus.

## Events

To work with event information, your website uses the same industry standard digital calendaring specification used by programs like Google Calendar, called [iCalendar](https://en.wikipedia.org/wiki/ICalendar). The iCalendar specification defines a set of datum that describes calendars and the event information those calendars contain. This data can be easily represented as data in a plain text file, where the individual data elements (start time, event name, etcetera) are written in a [comma-separated values (CSV) file](https://simple.wikipedia.org/wiki/Comma-separated_values).

Each event published by your website is stored as a line in [the `events.csv` file](events.csv). You can have as many events as you want. In practice, however, it is a good idea to prune (i.e., delete) old events from your calendars so that they do not accumulate.

Editing CSV files by hand can be hard, so we recommend that you use the supplied ODF Spreadsheet (the file ending with `.ods`) to edit your calendar events data. The ODF Spreadsheet also contains data validation and integrity checks to help make sure you don't accidentally set an event to start at "50 PM" instead of "5 PM." Once you edit the data in the spreadsheet, however, you must save a *new* copy of the spreadsheet as a CSV file, replacing the existing CSV file so that your website will pick up on the new data.

The whole the process looks like this:

1. You start by downloading and opening the [`events.ods`](events.ods) spreadsheet file.
1. Next, you edit the data in the spreadsheet to your liking. In this case, that means entering or deleting event information into the columns of the spreadsheet. Remember to save the spreadsheet regularly so you don't lose any of your work.
1. When the spreadsheet contains the correct data, you save it one last time, and then you *also* save another copy of the spreadsheet as a CSV (comma-separated values) file, using the "Save As…" menu item in [LibreOffice Calc](https://help.libreoffice.org/Calc/Welcome_to_the_Calc_Help) or your ODF-compatible spreadsheet application of choice.
1. Upload the saved `events.csv` file you created using the spreadsheet back into this folder.
1. Delete the copy of the `events.csv` file on your local workstation so you can easily recreate a new copy when you come back later.

The remainder of this section describes the above process in more detail and provides links to additional information.

### Recurring events

If you have an event that happens "every week, on Monday at 10pm," you do not need to write out every occurrence of the event into the `events.csv` file. Instead, you can write the details of the first event in the recurring sequence and describe the pattern in which the event repeats using the various `Recurrence` fields (described below). This makes it easy to schedule weekly events, for instance, infinitely into the future.

### Field reference

The fields ("columns") in the `events.csv` data file correspond approximately to the iCalendar specification (RFCs [5545](https://tools.ietf.org/html/rfc5545), [5546](https://tools.ietf.org/html/rfc5546), [6868](https://tools.ietf.org/html/rfc6868), and [7529](https://tools.ietf.org/html/rfc7529)). A brief overview of the purpose of those fields is described here. In some cases, the field is an exact implementation, such as in the case of `Summary`. Other fields are approximations that are used in concert with one another to generate valid iCalendar data, such as `Start_Date` and `Start_Time`. (Together, `Start_Date` and `Start_Time` map to the [`DTSTART`](https://www.kanzaki.com/docs/ical/dtstart.html) property of an iCalendar event object.) Further information can be found in the relevant Internet Engineering Task Force (IETF) documentation, i.e., the aforementioned RFCs.

#### `Calendar`

The name of the calendar on which this event belongs. You can have as many calendars as you want. Each unique value in this field will be interpreted as a new calendar.

For example, if your venue has two different event spaces, say, "the Main Stage, and "the rooftop"), you might want to schedule events independently for each space. In this case, events scheduled for the main stage area should have `Main Stage` in this field, while events that occur on the roof would have `Rooftop` in the `Calendar` column. To be on the same calendar, each event must have its `Calendar` field written in *exactly* the same way.

If you leave this field blank, the event will only appear on your site's "All events" calendar.

#### `Summary`

The description of the event in a few words or a single, short sentence. This is often the event's title or name. For example:

```
Evening Pot-Luck sponsored by Widget, Co
```

This field is required; it cannot be left blank.

#### `Start_Date`

The year, month, and day that the event starts, or the year, month, and day of the first event in a recurring sequence.

The field value must be written to the CSV file in `YYYY-MM-DD` format. If you are editing your event data using the ODF spreadsheet, you can write in most natural language formats, such as "April 8, 2018," and your spreadsheet application will apply the correct formatting when you save the file in CSV format.

This field is required; it cannot be left blank.

#### `Start_Time`

The hour, minute, and second that the event starts, or the hour, minute, and second on the day of the first event in a recurring sequence.

The field value must be written to the CSV file in `HH:MM:SS` format. If you are editing your event data using the ODF spreadsheet, you can write in most natural language formats, such as "5 PM," and your spreadsheet application will apply the correct formatting when you save the file in CSV format.

This field is required; it cannot be left blank.

#### `End_Date`

The year, month, and day that the event ends, or the year, month, and day that the first event in a recurring sequence ends.

The field value must be written to the CSV file in `YYYY-MM-DD` format. If you are editing your event data using the ODF spreadsheet, you can write in most natural language formats, such as "April 8, 2018," and your spreadsheet application will apply the correct formatting when you save the file in CSV format.

This field is required; it cannot be left blank.

#### `End_Time`

The hour, minute, and second that the event ends, or the hour, minute, and second that the first event in a recurring sequence ends.

The field value must be written to the CSV file in `HH:MM:SS` format. If you are editing your event data using the ODF spreadsheet, you can write in most natural language formats, such as "5 PM," and your spreadsheet application will apply the correct formatting when you save the file in CSV format.

This field is required; it cannot be left blank.

#### `Recurrence`

Whether or not this event repeats and, if so, according to what pattern. Leave this field blank for a one-off event. If the event repeats, enter a valid value. Valid values are:

* `HOURLY` - (This value is ONLY PARTIALLY IMPLEMENTED.)
* `DAILY` - (This value is ONLY PARTIALLY IMPLEMENTED.)
* `WEEKLY`
* `MONTHLY` - (This value is ONLY PARTIALLY IMPLEMENTED.)
* `YEARLY` - (This value is NOT YET IMPLEMENTED.)

If you are editing your event data using the ODF spreadsheet, clicking into a cell in this column will reveal a drop-down menu of the valid values.

#### `Recurrence_Interval`

The numeric step by which to apply the `Recurrence` value. For instance, if the `Recurrence` field is set to `WEEKLY` and this field is set to `2`, the event will repeat "once, every two weeks." This field must contain a whole number (integer).

This field is ignored unless [`Recurrence`](#recurrence) also contains a valid value.

#### `Recurrence_Count`

Specifies the total number of times the event occurs. For instance, an event that repeats five times will have the value `5` in this field. This field must contain a whole number (integer).

This field is ignored unless [`Recurrence`](#recurrence) also contains a valid value.

#### `Location`

The full address for the event, separated by commas. A full address will contain the following parts:

1. Street address
1. Extended address (often the name of a neighborhood)
1. City or region
1. State or province
1. Postal code
1. Country

For example:

```
123 Main Street, Pleasant Hill Neighborhood, Anytown, NY, 12345, United States
```

If you leave this field blank, the value from `site.iCalendar.defaults.location` in [`_config.yml`](../README.md#icalendar-defaults) is used.

#### `Description`

A long(er) description for the event (than the [`Summary`](#summary)). You may write as much detail as you wish, but it is generally a good idea to limit yourself to one or two paragraphs. If you need to describe more details about the event, consider publishing a blog post about the event and setting this event's [`URL`](#url) field to the Web address of that blog post.

#### `Image`

The full, direct Web address of an image to associate with the event. This image is used on event pages and in supporting client applications. For example:

```
https://example.com/images/my-awesome-event.jpg
```

#### `Status`

The current planning stage of the event. Valid values are:

* `TENTATIVE`
* `CONFIRMED`
* `CANCELLED`

If you are editing your event data using the ODF spreadsheet, clicking into a cell in this column will reveal a drop-down menu of the valid values.

#### `URL`

The full, direct Web address to a Web page or other online resource that provides more detailed or supplementary information about the event. This could be the permanent link to a blog post about the event, an artist's homepage, or a page at which one can purchase tickets or submit an RSVP for the event. For example:

```
https://example.com/blog/2018/04/03/example-event.html
```

#### `Categories`

An optional, comma-separated list of categories by which to further distinguish this event from other events on the same calendar. For example, you may want to categorize a jazz show as:

```
Music, Jazz
```

You can supply as many categories as you want, but in practice it is a good idea to determine a generic taxonomy for your specific website and stick to those. Each unique sub-value will be interpreted as its own category.

## Gallery

> :construction: TK-TODO: Describe [YAML](https://en.wikipedia.org/wiki/YAML).

[The `gallery.yml` data file](gallery.yml) controls which images are published to your website's "Gallery" page, along with which gallery image is featured on the home page's horizontal image slider. It is a YAML file containing a single list. Each item in the list represents an image in the gallery.

In turn, each image in the gallery has, at a minimum, a `src` ("source") field, whose value should be the Web address of some image on the Web. The image may also contain the following optional fields:

* `alt` - Brief textual description of the image, usually no more than a sentence or two. For example, `Sunset on a sand beach over calm waters.` This text is usually not displayed visually but provides a [gracefully degrading fallback](https://en.wikipedia.org/wiki/Fault_tolerance) in case of a network error, as well as [important accessibility benefits](https://en.wikipedia.org/wiki/Wikipedia:Manual_of_Style/Accessibility/Alternative_text_for_images) for browsers with visual impairments, including humans as well as bots.
* `caption` - A caption for the image. This accompanies the image as visually rendered text somewhere near the image itself. HTML is allowed in this field.
* `link` - A Web address (URL) to link this image to. Omit this field if you do not want the image to be a link.
* `link_title` - The `title` attribute text of the image's link. This field is ignored unless `link` is also set.
* `featured` - Whether or not the image should be included on the home page's horizontal image slider. The only valid value is `true`; omit this field if you do not want to include the image on the front page.

## Navigation menus

> :construction: TK-TODO: Describe [YAML](https://en.wikipedia.org/wiki/YAML).

[The `nav_menus.yml` data file](nav_menus.yml) defines the name, order, and contents of your site's navigation menus.  Each menu has a name, such as `main` or `sidebar`. Each menu is a list of links that may also be an image. At a minimum, each menu item must include a `url` and a `text` field.

Optionally, menu items may also include the following fields:

* `title_text` - The `title` attribute's text for the link.
* `image_url` - The Web address to an image.
