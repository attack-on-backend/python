# Attack on Python - å­ç¬¦ä¸² ð














<extoc></extoc>

## ä»ç»

å­ç¬¦ä¸²æ¯ `Python` ä¸­æåºæ¬çæ°æ®ç±»åä¹ä¸ , å®æ¯ä¸ä¸ªå®é¿å¯¹è±¡ , è¿æå³çå®çä¸æ¦åå»º , åä¹æ æ³æ¹åé¿åº¦

æä»¥å³äºå­ç¬¦ä¸²çæä½ , é½ä¼è¿åä¸ä¸ªæ°çå­ç¬¦ä¸² , èæ æ³å¨åæ¥çå­ç¬¦ä¸²ä¸ç´æ¥æä½

å­ç¬¦ä¸²çä½¿ç¨éè¦ç¨å¼å·æ¬èµ·æ¥ , ä¾å¦ : `name = "Lyon"` ; è¿énameå°±æ¯ä¸ä¸ªåéå , èå¼å·éé¢ç`Lyon` åå°±æ¯è¯¥åéç»å®çå¼ , è¯¥å¼çç±»åä¸º " str" ç±»å , æä»¬å¯ä»¥å©ç¨`type()` å½æ°è¿è¡æ¥ç : 

```python
>>> name = "Lyon"
>>> type(name)
<class 'str'>
>>>
```

è¿å°±æ¯å­ç¬¦ä¸²ç±»å , å½ç¶å¦ä¸ä½¿ç¨çæ¯åå¼å· , è¿éå¶å®è¿å¯ä»¥ä½¿ç¨åå¼å·`'Lyon'`ä»¥åä¸å¼å·`'''Lyon'''`(æèæ¯`"""Lyon"""`  , åå¼å·åå¼å·é½å¯ä»¥) , ä¸è¿å¯¹äºä¸å¼å· , æä»¬éå¸¸æ¯è¡¨ç¤ºå¤è¡å­ç¬¦ä¸² , è¿æ ·æä»¬å°±ä¸éè¦å©ç¨ " \n " ï¼æ¢è¡ç¬¦ï¼æ¥è¿è¡æ¯ä¸è¡çæ¢è¡äº

å¯¹äºåµå¥å¼å·çæ¶åè¦æ³¨æ , éè¦ç¨ä¸åçå¼å·æ¥é¿åæ­§ä¹ , æ¯å¦ : `'I am "Lyon"'`  , ä¹å¯ä»¥ `"I am 'Lyon'"` 

å¯¹äºææçåºæ¬æ°æ®ç±»å , æä»¬é½åºè¯¥çæå¶ç¹æ§ä»¥åæä½

å­ç¬¦ä¸²æä½ä¸»è¦æ **æ·è´ãæ¼æ¥ãæ¥æ¾ãæ¯è¾ãç»è®¡ãåçãæµè¯ãå¤§å°åç­**

## æ·è´

```python
>>> a = "Lyon"
>>> b = a
>>> print(a,b)
Lyon Lyon
```

## æ¼æ¥

```python
>>> a = "Hello"
>>> b = "Lyon"
>>> print(a + b)
HelloLyon
```

å° `Tips` : ç±äºå­ç¬¦ä¸²æ¯å®é¿å¯¹è±¡ , è¿å°±å¯¼è´æä»¬å¦æå `+` è¿ç® , ä¸¤ä¸¤ç¸å é½ä¼çæä¸ä¸ªæ°çå­ç¬¦ä¸² , äºæ¯å¦æä½ è¿æ ·æä½ `a + a + a + a + a` é¤äºæåçç»æ , å¨åå­ä¸­è¿ä¼åå»º 3 ä¸ªå¨è¿ç®è¿ç¨ä¸­éè¦çå­ç¬¦ä¸² , æä»¥å¦ææ¼æ¥æä½è¿å¤ , æä»¬æ­£ç¡®çæ¹å¼åºè¯¥æ¯ä½¿ç¨ `''.join(list())` , ä¹å°±æ¯éè¿ `join` æ¹æ³

```python
>>> a = "Lyon"
>>> b = "Hello"
>>> print(a.join(b)) 
HLyoneLyonlLyonlLyono  #HLyon eLyon lLyon lLyon o
```

## æ¥æ¾

```python
>>> name = "Lyon"
# è¿åLå­ç¬¦æå¨çä¸æ ,ä¸æ æ¯ä»0å¼å§çæ´æ°
>>> name.index('L')
0 
# å¦æä¸å­å¨å°±ä¼æ¥é
>>> name.index('N') 
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: substring not found  
# ä¹å¯ä»¥ç¨in,not inæ¥è¿è¡å¤æ­
>>>'L' in name
>>>
```

## æ¯è¾

æ¬æ¥ `Python 2` ä¸­æä¸ª `str.cmp()` æ¹æ³æ¥æ¯è¾ä¸¤ä¸ªå¯¹è±¡ , å¹¶æ ¹æ®ç»æè¿åä¸ä¸ªæ´æ° , æ´æ°çæ­£è´å°±æ¯æ°å¼çå¤§å°äº , ä½æ¯å¨ `Python 3` ä¸­å°±æ²¡æè¿ä¸ªæ¹æ³äº , å®æ¹ææ¡£å¦ä¸ : 

```The cmp() function should be treated as gone, and the __cmp__() special method is no longer supported. Use __lt__() for sorting, __eq__() with __hash__(), and other rich comparisons as needed. (If you really need the cmp() functionality, you could use the expression (a > b) - (a < b) as the equivalent for cmp(a, b).)
The cmp() function should be treated as gone, and the __cmp__() special method is no longer supported. Use __lt__() for sorting, __eq__() with __hash__(), and other rich comparisons as needed. (If you really need the cmp() functionality, you could use the expression (a > b) - (a < b) as the equivalent for cmp(a, b).)
```

å¤§è´çææå°±æ¯cmp()å½æ°å·²ç»èµ°äº , å¦æä½ ççéè¦cmpå½æ° , ä½ å¯ä»¥ç¨è¡¨è¾¾å¼`(a>b)-(a<b)ä»£æ¿cmp(a,b)`  , çä¸é¢ `2.7` çä»£ç  : 

```python
>>> a = "100"
>>> b = "50"
>>> cmp(a,b)   # a>b  è´æ°
-1
>>> cmp(b,a)   # b<a  æ­£æ°
1
```

## ç»è®¡

```python
>>> name = "Lyon"
 # nameä¸­"L"çä¸ªæ°
>>> name.count("L")     
1
```

## åç

```python
>>> name = "i like Lyon"
# ååç¬¬7ä¸ªå°ç¬¬9ä¸ªå­ç¬¦,æ³¨æç©ºæ ¼ä¹æ¯ä¸ä¸ªå­ç¬¦
>>> name[7:10]     
'Lyo'
>>> name = "i like Lyon"
# ç¬¬7å°ç¬¬10å,é¡¾å¤´ä¸é¡¾å°¾
>>> name[7:11]
'Lyon'
```

## æ£æµ

```python
>>> name = "Lyon"
# æ£æµ"L"æ¯å¦å¨nameä¸­,è¿åboolå¼
>>> "L" in name     
True
>>> num = "3412313"
# æ£æµnuméé¢æ¯å¦å¨é½æ¯æ´æ°
>>> num.isdigit()    
True
>>> name = "Lyon"
# æ£æµnameæ¯å¦å¯ä»¥è¢«å½ä½æ æ å¿ç¬¦,å³æ¯å¦ç¬¦ååéå½åè§å 
>>> name.isidentifier()
Trueã
# æ£æµnameéé¢ææ²¡æ"L",æå°±è¿åä¸æ 
>>> name.find('L')    
0
# æ£æµnameéé¢ææ²¡æ"N",æ²¡æå°±è¿å-1
>>> name.find('N')   
-1    
```

æ£æµç¸å³

```python
str.startswith(prefix[,start[,end]]) # æ¯å¦ä»¥prefixå¼å¤´ 
str.endswith(suffix[,start[,end]])   # ä»¥suffixç»å°¾ 
str.isalnum()    # æ¯å¦å¨æ¯å­æ¯åæ°å­,å¹¶è³å°æä¸ä¸ªå­ç¬¦ 
str.isalpha()    # æ¯å¦å¨æ¯å­æ¯,å¹¶è³å°æä¸ä¸ªå­ç¬¦ 
str.isdigit()    # æ¯å¦å¨æ¯æ°å­,å¹¶è³å°æä¸ä¸ªå­ç¬¦ 
str.isspace()    # æ¯å¦å¨æ¯ç©ºç½å­ç¬¦,å¹¶è³å°æä¸ä¸ªå­ç¬¦ 
str.islower()    # æ¯å¦å¨æ¯å°å 
str.isupper()    # æ¯å¦ä¾¿æ¯å¤§å 
str.istitle()    # æ¯å¦æ¯é¦å­æ¯å¤§åç
```

æ³¨ : è¿åå¼å¨ä¸º `bool` å¼

## å¤§å°å

```python
>>> name = "I am Lyon"
# å¤§å°åäºæ¢
>>> name.swapcase()   
'i AM lYON'
# é¦å­æ¯å¤§å,å¶å®é½å°å
>>> name.capitalize()     
'I am lyon'
# è½¬æ¢ä¸ºå¤§å
>>> name.upper()          
'I AM LYON'
# è½¬æ¢ä¸ºå°å
>>> name.lower()           
'i am lyon'
```

## æ´å¤

```python
 |  capitalize(...)
 |      S.capitalize() -> str
 |
 |      Return a capitalized version of S, i.e. make the first character
 |      have upper case and the rest lower case.
 |
 |  casefold(...)
 |      S.casefold() -> str
 |
 |      Return a version of S suitable for caseless comparisons.
 |
 |  center(...)
 |      S.center(width[, fillchar]) -> str
 |
 |      Return S centered in a string of length width. Padding is
 |      done using the specified fill character (default is a space)
 |
 |  count(...)
 |      S.count(sub[, start[, end]]) -> int
 |
 |      Return the number of non-overlapping occurrences of substring sub in
 |      string S[start:end].  Optional arguments start and end are
 |      interpreted as in slice notation.
 |
 |  encode(...)
 |      S.encode(encoding='utf-8', errors='strict') -> bytes
 |
 |      Encode S using the codec registered for encoding. Default encoding
 |      is 'utf-8'. errors may be given to set a different error
 |      handling scheme. Default is 'strict' meaning that encoding errors raise
 |      a UnicodeEncodeError. Other possible values are 'ignore', 'replace' and
 |      'xmlcharrefreplace' as well as any other name registered with
 |      codecs.register_error that can handle UnicodeEncodeErrors.
 |
 |  endswith(...)
 |      S.endswith(suffix[, start[, end]]) -> bool
 |
 |      Return True if S ends with the specified suffix, False otherwise.
 |      With optional start, test S beginning at that position.
 |      With optional end, stop comparing S at that position.
 |      suffix can also be a tuple of strings to try.
 |
 |  expandtabs(...)
 |      S.expandtabs(tabsize=8) -> str
 |
 |      Return a copy of S where all tab characters are expanded using spaces.
 |      If tabsize is not given, a tab size of 8 characters is assumed.
 |
 |  find(...)
 |      S.find(sub[, start[, end]]) -> int
 |
 |      Return the lowest index in S where substring sub is found,
 |      such that sub is contained within S[start:end].  Optional
 |      arguments start and end are interpreted as in slice notation.
 |
 |      Return -1 on failure.
 |
 |  format(...)
 |      S.format(*args, **kwargs) -> str
 |
 |      Return a formatted version of S, using substitutions from args and kwargs.
 |      The substitutions are identified by braces ('{' and '}').
 |
 |  format_map(...)
 |      S.format_map(mapping) -> str
 |
 |      Return a formatted version of S, using substitutions from mapping.
 |      The substitutions are identified by braces ('{' and '}').
 |
 |  index(...)
 |      S.index(sub[, start[, end]]) -> int
 |
 |      Like S.find() but raise ValueError when the substring is not found.
 |
 |  isalnum(...)
 |      S.isalnum() -> bool
 |
 |      Return True if all characters in S are alphanumeric
 |      and there is at least one character in S, False otherwise.
 |
 |  isalpha(...)
 |      S.isalpha() -> bool
 |
 |      Return True if all characters in S are alphabetic
 |      and there is at least one character in S, False otherwise.
 |
 |  isdecimal(...)
 |      S.isdecimal() -> bool
 |
 |      Return True if there are only decimal characters in S,
 |      False otherwise.
 |
 |  isdigit(...)
 |      S.isdigit() -> bool
 |
 |      Return True if all characters in S are digits
 |      and there is at least one character in S, False otherwise.
 |
 |  isidentifier(...)
 |      S.isidentifier() -> bool
 |
 |      Return True if S is a valid identifier according
 |      to the language definition.
 |
 |      Use keyword.iskeyword() to test for reserved identifiers
 |      such as "def" and "class".
 |
 |  islower(...)
 |      S.islower() -> bool
 |
 |      Return True if all cased characters in S are lowercase and there is
 |      at least one cased character in S, False otherwise.
 |
 |  isnumeric(...)
 |      S.isnumeric() -> bool
 |
 |      Return True if there are only numeric characters in S,
 |      False otherwise.
 |
 |  isprintable(...)
 |      S.isprintable() -> bool
 |
 |      Return True if all characters in S are considered
 |      printable in repr() or S is empty, False otherwise.
 |
 |  isspace(...)
 |      S.isspace() -> bool
 |
 |      Return True if all characters in S are whitespace
 |      and there is at least one character in S, False otherwise.
 |
 |  istitle(...)
 |      S.istitle() -> bool
 |
 |      Return True if S is a titlecased string and there is at least one
 |      character in S, i.e. upper- and titlecase characters may only
 |      follow uncased characters and lowercase characters only cased ones.
 |      Return False otherwise.
 |
 |  isupper(...)
 |      S.isupper() -> bool
 |
 |      Return True if all cased characters in S are uppercase and there is
 |      at least one cased character in S, False otherwise.
 |
 |  join(...)
 |      S.join(iterable) -> str
 |
 |      Return a string which is the concatenation of the strings in the
 |      iterable.  The separator between elements is S.
 |
 |  ljust(...)
 |      S.ljust(width[, fillchar]) -> str
 |
 |      Return S left-justified in a Unicode string of length width. Padding is
 |      done using the specified fill character (default is a space).
 |
 |  lower(...)
 |      S.lower() -> str
 |
 |      Return a copy of the string S converted to lowercase.
 |
 |  lstrip(...)
 |      S.lstrip([chars]) -> str
 |
 |      Return a copy of the string S with leading whitespace removed.
 |      If chars is given and not None, remove characters in chars instead.
 |
 |  partition(...)
 |      S.partition(sep) -> (head, sep, tail)
 |
 |      Search for the separator sep in S, and return the part before it,
 |      the separator itself, and the part after it.  If the separator is not
 |      found, return S and two empty strings.
 |
 |  replace(...)
 |      S.replace(old, new[, count]) -> str
 |
 |      Return a copy of S with all occurrences of substring
 |      old replaced by new.  If the optional argument count is
 |      given, only the first count occurrences are replaced.
 |
 |  rfind(...)
 |      S.rfind(sub[, start[, end]]) -> int
 |
 |      Return the highest index in S where substring sub is found,
 |      such that sub is contained within S[start:end].  Optional
 |      arguments start and end are interpreted as in slice notation.
 |
 |      Return -1 on failure.
 |
 |  rindex(...)
 |      S.rindex(sub[, start[, end]]) -> int
 |
 |      Like S.rfind() but raise ValueError when the substring is not found.
 |
 |  rjust(...)
 |      S.rjust(width[, fillchar]) -> str
 |
 |      Return S right-justified in a string of length width. Padding is
 |      done using the specified fill character (default is a space).
 |
 |  rpartition(...)
 |      S.rpartition(sep) -> (head, sep, tail)
 |
 |      Search for the separator sep in S, starting at the end of S, and return
 |      the part before it, the separator itself, and the part after it.  If the
 |      separator is not found, return two empty strings and S.
 |
 |  rsplit(...)
 |      S.rsplit(sep=None, maxsplit=-1) -> list of strings
 |
 |      Return a list of the words in S, using sep as the
 |      delimiter string, starting at the end of the string and
 |      working to the front.  If maxsplit is given, at most maxsplit
 |      splits are done. If sep is not specified, any whitespace string
 |      is a separator.
 |
 |  rstrip(...)
 |      S.rstrip([chars]) -> str
 |
 |      Return a copy of the string S with trailing whitespace removed.
 |      If chars is given and not None, remove characters in chars instead.
 |
 |  split(...)
 |      S.split(sep=None, maxsplit=-1) -> list of strings
 |
 |      Return a list of the words in S, using sep as the
 |      delimiter string.  If maxsplit is given, at most maxsplit
 |      splits are done. If sep is not specified or is None, any
 |      whitespace string is a separator and empty strings are
 |      removed from the result.
 |
 |  splitlines(...)
 |      S.splitlines([keepends]) -> list of strings
 |
 |      Return a list of the lines in S, breaking at line boundaries.
 |      Line breaks are not included in the resulting list unless keepends
 |      is given and true.
 |
 |  startswith(...)
 |      S.startswith(prefix[, start[, end]]) -> bool
 |
 |      Return True if S starts with the specified prefix, False otherwise.
 |      With optional start, test S beginning at that position.
 |      With optional end, stop comparing S at that position.
 |      prefix can also be a tuple of strings to try.
 |
 |  strip(...)
 |      S.strip([chars]) -> str
 |
 |      Return a copy of the string S with leading and trailing
 |      whitespace removed.
 |      If chars is given and not None, remove characters in chars instead.
 |
 |  swapcase(...)
 |      S.swapcase() -> str
 |
 |      Return a copy of S with uppercase characters converted to lowercase
 |      and vice versa.
 |
 |  title(...)
 |      S.title() -> str
 |
 |      Return a titlecased version of S, i.e. words start with title case
 |      characters, all remaining cased characters have lower case.
 |
 |  translate(...)
 |      S.translate(table) -> str
 |
 |      Return a copy of the string S in which each character has been mapped
 |      through the given translation table. The table must implement
 |      lookup/indexing via __getitem__, for instance a dictionary or list,
 |      mapping Unicode ordinals to Unicode ordinals, strings, or None. If
 |      this operation raises LookupError, the character is left untouched.
 |      Characters mapped to None are deleted.
 |
 |  upper(...)
 |      S.upper() -> str
 |
 |      Return a copy of S converted to uppercase.
 |
 |  zfill(...)
 |      S.zfill(width) -> str
 |
 |      Pad a numeric string S with zeros on the left, to fill a field
 |      of the specified width. The string S is never truncated.
 |
 |  ----------------------------------------------------------------------
```
