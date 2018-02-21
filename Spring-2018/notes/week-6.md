# Parsing html with Open Refine

1) Start OpenRefine and select Create Project


* Under “Get Data From”, click Clipboard, and paste this URL into the text box:

https://programminghistorian.org/assets/fetch-and-parse-data-with-openrefine/pg1105.html

Add the project name “Sonnets” at the top right and click Create project. 

2) Click on the menu arrow of Column 1 > Edit column > Add column by fetching urls.

* Name the new column “fetch”. 

3) click on the URL in Column 1 to open the link in a new tab, then right click on the page to “View Page Source”.

* On the fetch column, click on the menu arrow > edit column > Add column based on this column. 
Give the new column the name “parse”, then click in the Expression text box.

value.parseHtml().select("p")

value.parseHtml().select("p")[0]

value.parseHtml().select("p")[37]

value.parseHtml().select("p")[-1]

Add the slice() function to the expression to preview the sub-set: 

value.parseHtml().select("p").slice(37,-2)

value.parseHtml().select("p").slice(37,-2).join("|")

Click OK to create the new column using the expression.

## Split the Cells

* Click the menu arrow on the parse column > Edit cells > Split multi-valued cells. Enter the separator |

After this operation, the top of the project table should now read 154 rows. 
Below the number is an option toggle “Show as: rows records”.

Click on the parse column and select Edit cells > Transform. 

value.parseHtml()

value.parseHtml().select("p")[0].innerHtml()

## Getting rid of unwanted tags

On the parse column, select Edit cells > Transform and type the following in the expression box:

value.unescape('html')

Create two new columns from the parse column using these names and expressions:

“number”, value.split("<br />")[0].trim()
“first”, value.split("<br />")[1].trim()


From the parse column, create a new column named “text”, and click in the Expression box

forEach(value.split("<br />"), line, line.trim()).slice(1).join("\n")

characters”, value.length()

“lines”, value.split(/\n/).length()
