# Add event to google calendar

### Basic URL

`https://calendar.google.com/calendar/render`

```

$baseUrl = 'https://calendar.google.com/calendar/render?';

$paremetersList = [
    'action' => 'TEMPLATE'
    'text' => 'Birthday',
    'dates' => '20220421T193000/20201231T223000',
    'details' => 'With clowns and stuff',
];

$queryParameters = http_build_query($parametersList);

echo $baseUrl . $queryParameters;

Output: https://calendar.google.com/calendar/u/0/r/eventedit?text=Birthday&dates=20220422T160000/20220422T19000&details=With+clowns+and+stuff
```


Reference: https://interactiondesignfoundation.github.io/add-event-to-calendar-docs/services/google.html
