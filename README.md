# academic-calendars

Single source of truth for academic calendars of universities across the US

This document outlines the algorithmic location of these calendars for known universities.

## Overview

Currently organized by the following regions:

```
WEST: ["WA", "OR", "CA", "ID", "NV", "MT", "WY", "UT", "CO", "AZ", "NM", "AK", "HI"],
MIDWEST: ["ND", "SD", "NE", "KS", "MN", "IA", "MO", "WI", "MI", "IL", "IN", "OH"],
NORTHEAST: ["PA", "NY", "NJ", "CT", "RI", "MA", "VT", "NH", "ME", "MD", "DE", "DC"],
SOUTH: ["OK", "TX", "AR", "LA", "MS", "AL", "TN", "KY", "GA", "FL", "SC", "NC", "VA", "WV"],
```

The points of interest are a list of first and last day of instruction, including any final examination week.

Variables:

| Variable | Description                      | Example for 2020-21 academic year |
| -------- | -------------------------------- | --------------------------------- |
| `Y1`     | first calendar year              | 2020                              |
| `y1`     | half of the first calendar year  | 20                                |
| `Y2`     | second calendar year             | 2021                              |
| `y2`     | half of the second calendar year | 21                                |

Constants:

- `NUM_QUARTERS` = 4
- `NUM_SEMESTERS` = 3

## Per-college details

### West Coast

#### University of Washington

1. URL: `https://www.washington.edu/students/reg/${y1}${y2}cal.html`
2. Dates:

```
def get_date(num):
    return document.querySelector(`#QS+table > tbody > tr:nth-child(2) > td:nth-child(${num})`).parse("MMMM D, YYYY")

for i in range NUM_QUARTERS:
    start = get_date(2)
    end = get_date(4) if it isn't empty, else get_date(3)
```

#### Stanford University

1. URL:
   1. https://registrar.stanford.edu/academic-calendar
   2. https://registrar.stanford.edu/future-academic-calendars
   3. https://registrar.stanford.edu/academic-calendar-${Y1}-${y2}
1. Dates:
   1. Open links in the following order and look for an `h2` element with the content `${Y1}-${y2} First Day of Classes and End of Term`:
      1. Link #3
      2. Link #1
      3. Link #2
   2. If not found, abort.
   3. 4 bullets, each has the quarter description, a colon, and then `MMMM D and MMMM D.*`. Parse out the dates.
