    | COPYDISK EXEC    | Copy disk with ``FLASHCOPY`` if not ``DDR``     |
    | MAN      EXEC    | Give help on CMS/CP/XEDIT commands              |
    | QA       EXEC    | Run ``QUERY ACCESSED``                          |
    | SSICMD   EXEC    | Run CP commands on multiple SSI members         |
    | WHICH    EXEC    | Resolve CMS/CP/XEDIT commands                   |
    | WHO      EXEC    | Show who is logged on and allow a pattern       |
To search for strings with spaces, the pattern has to be escaped with triple double-quotes.  For example:

```
grep """parse upper arg""" * exec
```
