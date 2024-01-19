---
layout: single 
title: "How to remove ASCII control characters from a string" 
classes: wide
last_modified_at:
---

Recently, I have been working on text files from different sources such as DOCX and PDF. Reading the text file into Python environment often leaves ASCII control characters. Many times, it gives better results when removing these ASCII control characters for text cleaning and processing or Natural Language Processing (NLP) tasks.

### What are the ASCII control characters
ASCII control characters are non-printable characters within the ASCII character set that are designed to control devices or data flow rather than represent visible symbols. There are total 33 characters from 0 to 31 and 127. 
While some control characters are still used in modern computing (like tabs, line feeds, and carriage returns), many are obsolete due to advancements in device control and data handling.

The ASCII control chart from [Wikipedia](https://en.wikipedia.org/wiki/ASCII#ASCII_control_characters) are below.

| [Dec](https://en.wikipedia.org/wiki/Decimal "Decimal") | [Hex](https://en.wikipedia.org/wiki/Hexadecimal "Hexadecimal") | Abbreviation | Escape sequence | Name |
| ---- | ---- | ---- | ---- | ---- |
| 0 | 00 | NUL | \0 | [Null](https://en.wikipedia.org/wiki/Null_character "Null character") |
| 1 | 01 | SOH |  | [Start of Heading](https://en.wikipedia.org/wiki/Start_of_Heading "Start of Heading") |
| 2 | 02 | STX |  | [Start of Text](https://en.wikipedia.org/wiki/Start_of_Text "Start of Text") |
| 3 | 03 | ETX |  | [End of Text](https://en.wikipedia.org/wiki/End-of-Text_character "End-of-Text character") |
| 4 | 04 | EOT |  | [End of Transmission](https://en.wikipedia.org/wiki/End-of-Transmission_character "End-of-Transmission character") |
| 5 | 05 | ENQ |  | [Enquiry](https://en.wikipedia.org/wiki/Enquiry_character "Enquiry character") |
| 6 | 06 | ACK |  | [Acknowledgement](https://en.wikipedia.org/wiki/Acknowledge_character "Acknowledge character") |
| 7 | 07 | BEL | \a | [Bell](https://en.wikipedia.org/wiki/Bell_character "Bell character") |
| 8 | 08 | BS | \b | [Backspace](https://en.wikipedia.org/wiki/Backspace "Backspace") |
| 9 | 09 | HT | \t | [Horizontal Tab](https://en.wikipedia.org/wiki/Horizontal_Tab "Horizontal Tab") |
| 10 | 0A | LF | \n | [Line Feed](https://en.wikipedia.org/wiki/Line_Feed "Line Feed") |
| 11 | 0B | VT | \v | [Vertical Tab](https://en.wikipedia.org/wiki/Vertical_Tab "Vertical Tab") |
| 12 | 0C | FF | \f | [Form Feed](https://en.wikipedia.org/wiki/Form_Feed "Form Feed") |
| 13 | 0D | CR | \r | [Carriage Return](https://en.wikipedia.org/wiki/Carriage_Return "Carriage Return") |
| 14 | 0E | SO |  | [Shift Out](https://en.wikipedia.org/wiki/Shift_Out "Shift Out") |
| 15 | 0F | SI |  | [Shift In](https://en.wikipedia.org/wiki/Shift_In "Shift In") |
| 16 | 10 | DLE |  | [Data Link Escape](https://en.wikipedia.org/wiki/Data_Link_Escape "Data Link Escape") |
| 17 | 11 | DC1 |  | [Device Control 1](https://en.wikipedia.org/wiki/Device_Control_1 "Device Control 1") (often [XON](https://en.wikipedia.org/wiki/XON "XON")) |
| 18 | 12 | DC2 |  | [Device Control 2](https://en.wikipedia.org/wiki/Device_Control_2 "Device Control 2") |
| 19 | 13 | DC3 |  | [Device Control 3](https://en.wikipedia.org/wiki/Device_Control_3 "Device Control 3") (often [XOFF](https://en.wikipedia.org/wiki/XOFF "XOFF")) |
| 20 | 14 | DC4 |  | [Device Control 4](https://en.wikipedia.org/wiki/Device_Control_4 "Device Control 4") |
| 21 | 15 | NAK |  | [Negative Acknowledgement](https://en.wikipedia.org/wiki/Negative-acknowledge_character "Negative-acknowledge character") |
| 22 | 16 | SYN |  | [Synchronous Idle](https://en.wikipedia.org/wiki/Synchronous_Idle "Synchronous Idle") |
| 23 | 17 | ETB |  | [End of Transmission Block](https://en.wikipedia.org/wiki/End-of-Transmission-Block_character "End-of-Transmission-Block character") |
| 24 | 18 | CAN |  | [Cancel](https://en.wikipedia.org/wiki/Cancel_character "Cancel character") |
| 25 | 19 | EM |  | [End of Medium](https://en.wikipedia.org/wiki/End_of_Medium "End of Medium") |
| 26 | 1A | SUB |  | [Substitute](https://en.wikipedia.org/wiki/Substitute_character "Substitute character") |
| 27 | 1B | ESC | \e | [Escape](https://en.wikipedia.org/wiki/Escape_character "Escape character") |
| 28 | 1C | FS |  | [File Separator](https://en.wikipedia.org/wiki/File_Separator "File Separator")\| |
| 29 | 1D | GS |  | [Group Separator](https://en.wikipedia.org/wiki/Group_Separator "Group Separator") |
| 30 | 1E | RS |  | [Record Separator](https://en.wikipedia.org/wiki/Record_Separator "Record Separator") |
| 31 | 1F | US |  | [Unit Separator](https://en.wikipedia.org/wiki/Unit_Separator "Unit Separator") |
| 127 | 7F | DEL |  | [Delete](https://en.wikipedia.org/wiki/Delete_character "Delete character") |

### How to remove
We can remove all those control characters using `re` library.

```python
import re

def remove_ctrl_chars(text):
"""Removes all ASCII control characters from a string.""" 
    return re.sub(r'[\x00-\x1F\x7F]', '', text)
```

The explanation of regex expression:
 - `\x00-\x1F` :Matches any character with a hexadecimal code between 0x00 (null) and 0x1F (US), covering the first 32 control characters.
 -  `\x7F`: Matches the DEL character (0x7F), the last control character in the ASCII table.

```python
text = '1.\tThis is the first line of \x07string.\n\x0C2.\tThis is the \x08second line of string.'
cleaned_text = remove_ctrl_chars(text)
print(cleaned_text)
# output: 
# 1.This is the first line of string.2.This is the second line of string.
```

Optionally, we can preserve some characters such as tab `\t` and newlines `\n`.

```python
import re

def remove_ctrl_chars_except_tab_newline(text):
"""Removes all ASCII control characters except tab and newline from a string.""" 
    return re.sub(r'[\x00-\x1F\x7F](?<![\x0A\x09])', '', text)
```
where, `\x09` and  `\x0A` matches tab and newline characters.

```python
text = '1.\tThis is the first line of \x07string.\n\x0C2.\tThis is the \x08second line of string.'
cleaned_text = remove_ctrl_chars_except_tab_newline(text)
print(cleaned_text)
# output: 
# 1.    This is the first line of string. 
# 2.    This is the second line of string.
```
