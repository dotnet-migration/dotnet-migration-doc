Migrating from dday.ical to ical.net

[ical.net](https://github.com/rianjs/ical.net/wiki/Migrating-from-dday.ical)

## productId serialize issue
https://github.com/rianjs/ical.net/issues/408

use ComponentSerializer instead of CalendarSerializer

```
val icalStr = (new ComponentSerializer()).SerializeToString(calendar);
```

## calendar parameter serialize issue
```cs
eventDescription = $"<html><body>{eventDescription}</body></html>";
var cProperty = new CalendarProperty("X-ALT-DESC");
cProperty.AddParameter("FMTTYPE", "text/html");
cProperty.Value = eventDescription;
calendarEvent.AddProperty(altDesc);
```
change to

```cs
eventDescription = $"<html><body>{eventDescription}</body></html>";
var cProperty = new CalendarProperty("X-ALT-DESC;FMTTYPE=text/html");
cProperty.Value = eventDescription;
calendarEvent.AddProperty(altDesc);
```
