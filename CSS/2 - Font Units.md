## REM
* Good for text.
## EM
* Good for padding, margin, and width.
* When it isn't applied to the font size property, it becomes relative to the font size of its own element.
* Not good for font size because it becomes relative to the font size of the parent element.
## Percentages
* They are always relative to their parent.
## VW, VH
* Use VW if you don't want the width to be relative to their parent. It is relative to the viewport width instead.
* VH is the same as VW, but for height instead of width.
## CH
* It measures the width of the character 0 on your font.
* It can be used to set a max width on a paragraph.
* It works better than rem and em for setting text width because it lets you specifically specify the number of characters per line.
	* As a rule of thumb, paragraphs should have a length per line of around 54 to 75 characters.