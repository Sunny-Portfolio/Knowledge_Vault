
`\d`  stands for a digit character

Matching phone number:
`\d\d\d-\d\d\d-\d\d\d\d`
or
`\d{3}-\d{3}-\d{4}`

##### Pass a regex pattern to get a regex pattern object
```py
import re   # you need to import
>>> phoneNumRegex = re.compile(r'\d\d\d-\d\d\d-\d\d\d\d')
```

##### Regex pattern obj's search method
```py
>>> mo = phoneNumRegex.search('My number is 415-555-4242.')
```

if pattern found, `search()` returns Match object which has a `group()` method that returns the matched text from the original string.
```py
>>> print('Phone number found: ' + mo.group())
Phone number found: 415-555-4242
```


Adding `( )` to regex will create groups of the regex:
```py
>>> phoneNumRegex = re.compile(r'(\d\d\d)-(\d\d\d-\d\d\d\d)')
>>> mo = phoneNumRegex.search('My number is 415-555-4242.')
>>> mo.group(1)
'415'
>>> mo.group(2)
'555-4242'
>>> mo.group(0)     # 0 return entire matched text
'415-555-4242'
>>> mo.group()      # '' return entire matched text
'415-555-4242'
```

##### groups()
- retrieve all groups at once
- returns tuple of multiple values, can use to multiple-assignment
```py
>>> mo.groups()
('415', '555-4242')
>>> areaCode, mainNumber = mo.groups()
>>> print(areaCode)
415
>>> print(mainNumber)
555-4242
```

##### if you need to match a `( )` use a `\` escape character
```py
>>> phoneNumRegex = re.compile(r'(\(\d\d\d\)) (\d\d\d-\d\d\d\d)')
```

### Pipe
---
##### Pipe to match one of the expressions
```py
>>> heroRegex = re.compile (r'Batman|Tina Fey')
>>> mo1 = heroRegex.search('Batman and Tina Fey')
>>> mo1.group()
'Batman'
```

##### use a ( ) to match part of the string
```py
>>> batRegex = re.compile(r'Bat(man|mobile|copter|bat)')
>>> mo = batRegex.search('Batmobile lost a wheel')
>>> mo.group()
'Batmobile'
>>> mo.group(1)
'mobile'
```

##### use ? to match the preceding the ? optionally
the following will match either Batman or Batwoman
? matches 0 or 1 of the preceding group
```py
>>> batRegex = re.compile(r'Bat(wo)?man')
>>> mo1 = batRegex.search('The Adventures of Batman')
Pattern Matching with Regular Expressions   169
>>> mo1.group()
'Batman'
```

```py
>>> mo2 = batRegex.search('The Adventures of Batwoman')
>>> mo2.group()
'Batwoman'
```

##### match zero or more with * 
```py
>>> batRegex = re.compile(r'Bat(wo)*man')
>>> mo3 = batRegex.search('The Adventures of Batwowowowoman')
>>> mo3.group()
'Batwowowowoman'
```

##### match one or more with +
```py
>>> batRegex = re.compile(r'Bat(wo)+man')
>>> mo3 = batRegex.search('The Adventures of Batman')
>>> mo3 == None
True
```

##### match repetition pattern with {}
```py
(Ha){3}     # match HaHaHa
(Ha){3,}    # match 3 or more
(Ha){,5}    # match up to 5
(Ha){3,5}    # match 3 to 5 
```

##### Python's regex is greedy by default, which match the longest string
Lazy version matches the shortest string, do {3,5}?

```py
>>> greedyHaRegex = re.compile(r'(Ha){3,5}')
>>> mo1 = greedyHaRegex.search('HaHaHaHaHa')
>>> mo1.group()
'HaHaHaHaHa'
```

```py
>>> nongreedyHaRegex = re.compile(r'(Ha){3,5}?')
>>> mo2 = nongreedyHaRegex.search('HaHaHaHaHa')
>>> mo2.group()
'HaHaHa'
```

##### findall() method
`search()` finds first matched text, returns a Match Object with `group()`
`findall()` finds every match, note that it has no `group()` because it is a list

```py
>>> phoneNumRegex = re.compile(r'\d\d\d-\d\d\d-\d\d\d\d') # has no groups
>>> phoneNumRegex.findall('Cell: 415-555-9999 Work: 212-555-0000')
['415-555-9999', '212-555-0000']
```

If there are groups in the regex, then findall() returns list of tuples
```py
>>> phoneNumRegex = re.compile(r'(\d\d\d)-(\d\d\d)-(\d\d\d\d)') # has groups
>>> phoneNumRegex.findall('Cell: 415-555-9999 Work: 212-555-0000')
[('415', '555', '9999'), ('212', '555', '0000')]
```


### Other character class
```
/d      0-9
/D      not 0-9
/w      alphanumeric and _
/W      not alphanumeric and _
/s      Space, tab, /n
/S      not Space, tab, /n
```

```
[0-5]   0-5
[^0-5]  not 0-5
[a-zA-Z]    alphabets
[a-zA-Z0-9] alphanumeric
```

```py
>>> alphabets = re.compile(r'[a-zA-Z])
```

```py
>>> vowelRegex = re.compile(r'[aeiouAEIOU]')
>>> vowelRegex.findall('RoboCop eats baby food. BABY FOOD.')
['o', 'o', 'o', 'e', 'a', 'a', 'o', 'o', 'A', 'O', 'O']
```

##### Use ^ to search start with, $ for end with
```py
>>> beginsWithHello = re.compile(r'^Hello')
>>> endsWithNumber = re.compile(r'\d$')     # ends with number
>>> startsAndBegin = re.compile(r'^\d+$')   # starts and end with 1 or more num
The above basically means match only numbers
```

### Wildcard . dot
Match any except newline
```py
>>> atRegex = re.compile(r'.at')
>>> atRegex.findall('The cat in the hat sat on the flat mat.')
['cat', 'hat', 'sat', 'lat', 'mat']
```

Match anything with .*
```py
>>> nameRegex = re.compile(r'First Name: (.*) Last Name: (.*)')
>>> mo = nameRegex.search('First Name: Al Last Name: Sweigart')
>>> mo.group(1)
'Al'
>>> mo.group(2)
'Sweigart'
```

.* is greedy by default, use ？ for non-greedy
>>> nongreedyRegex = re.compile(r'<.*?>')
>>> mo = nongreedyRegex.search('<To serve man> for dinner.>')
>>> mo.group()
'<To serve man>'

>>> greedyRegex = re.compile(r'<.*>')
>>> mo = greedyRegex.search('<To serve man> for dinner.>')
>>> mo.group()
'<To serve man> for dinner.>'

Match .* dot character including newline \n
>>> newlineRegex = re.compile('.*', re.DOTALL)
>>> newlineRegex.search('Serve the public trust.\nProtect the innocent.
\nUphold the law.').group()
'Serve the public trust.\nProtect the innocent.\nUphold the law.'

----------------------------------

# To match exact text
>>> regex1 = re.compile('RoboCop')

# To match with case-insensitive
>>> regex1 = re.compile('RoboCop', re.IGNORECASE)
>>> robocop.search('RoboCop is part man, part machine, all cop.').group()
'RoboCop'
>>> regex1 = re.compile('RoboCop', re.I)
You can directly add .group() to the end to get the result

# sub() method to substitude text
>>> namesRegex = re.compile(r'Agent \w+')   # match 1 ore more of preceding
>>> namesRegex.sub('CENSORED', 'Agent Alice gave the secret documents to Agent Bob.')
'CENSORED gave the secret documents to CENSORED.'

# Match complex regexes with verbose mode
Instead of this:
phoneRegex = re.compile(r'((\d{3}|\(\d{3}\))?(\s|-|\.)?\d{3}(\s|-|\.)\d{4}
(\s*(ext|x|ext.)\s*\d{2,5})?)')

You can write this:
phoneRegex = re.compile(r'''(
(\d{3}|\(\d{3}\))?              # area code
(\s|-|\.)?                      # separator
\d{3}                           # first 3 digits
(\s|-|\.)                       # separator
\d{4}                           # last 4 digits
(\s*(ext|x|ext.)\s*\d{2,5})?    # extension
)''', re.VERBOSE)


# the re.compile() function can only take one value as second argument
# get around this by using | pipeline character (bitwise or operator)
>>> someRegexValue = re.compile('foo', re.IGNORECASE | re.DOTALL | re.VERBOSE)



