# dday.ical migration

Migrating from [dday.ical](https://www.nuget.org/packages/DDay.iCal) to [ical.net](https://github.com/rianjs/ical.net/wiki/Migrating-from-dday.ical)

## productId serialize issue

when migrate dday.ical to ical.net, we use the `Ical.Net.Calendar.ProductId` to replace dday.ical `ProductID`, but we got a error ProductId.

```cs
var calendar = new Ical.Net.Calendar
{
    ProductId = "-//dotnet-migration.pages.dev///RemoteAPI/EN"
};
calendar.Events.Add(ev);
var serializer = new CalendarSerializer(new SerializationContext());
```

but we got `PRODID:-//github.com/rianjs/ical.net//NONSGML ical.net 4.0//EN`

https://github.com/rianjs/ical.net/issues/408

use ComponentSerializer instead of CalendarSerializer

### Solution

use `ComponentSerializer` to replace `CalendarSerializer`.

```
val icalStr = (new ComponentSerializer()).SerializeToString(calendar);
```

## calendar parameter serialize issue

After migrate to [ical.net](https://github.com/rianjs/ical.net/wiki/Migrating-from-dday.ical), we got a unexpected string when use `CalendarSerializer.SerializeToString(calendar)`. I use AddParameter to add key-value pair("FMTTYPE", "text/html") to property object, but the result lost key-value pair.

### Solution

so we add the parameter to Property name.

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
