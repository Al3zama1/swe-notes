## Data Serialization
* Data serialization is the process of converting data into a standardized format/structure that can be stored (in a file) or transmitted (over a network) and reconstructed later (ie. by a different application).
	* This allows the data to be communicated between applications in a way both applications understand.
## JSON
* **JSON** (Javascript Object Notation) is an open standard **file format** and **data interchange format** that uses human-readable text to store and transmit data objects.
* It is standardized in RFC 8259
* It was derived from JavaScript, but it is language-independent and many modern programming languages are able to generate and read JSON data.
	* REST APIs often use JSON.
* *Whitespace* is insignificant.
* JSON can represent four primitive types:
	* string: A text value surrounded by double quotes.
	* number: A numeric value. It is not surrounded by quotes.
	* boolean: true/false
	* null: Represents the intentional absence of nay object value.
* JSON also has two data structures:
	* object: An unordered list of key-value pairs (variables).
		* Objects are surrounded by curly brackets {}.
		* They key is a string.
		* The value is any valid JSON data type (string, number, boolean, null, object, array).
		* They key and value are separated by colon : .
		* If there are multiple key-value pairs, each pair is separated by a comma.
	* array: a series of values separated by commas.
		* Not key-value pairs.
		* The values don't have to be the same data types.

```
{
  "name": "Alice",
  "age": 30,
  "isEmployee": true,
  "salary": null,
  "contactNumbers": [
    "123-456-7890",
    "098-765-4321"
  ],
  "address": {
    "street": "123 Main St",
    "city": "Anytown",
    "state": "CA",
    "postalCode": "12345"
  },
  "skills": [
    {
      "name": "Programming",
      "level": "Advanced"
    },
    {
      "name": "Data Analysis",
      "level": "Intermediate"
    },
    {
      "name": "Project Management",
      "level": "Beginner"
    }
  ]
}

```
## XML
* **XML** (Extensible Markup Language) was developed as a markup language, but is now used as a general data serialization language.
	* Markup languages (ie, HTML) are used to format text (font, size, color, headings, etc).
* XML is generally less human-readable than JSON.
* Whitespace is insignificant.
* Often used by REST APIs.
* The structure is `<key>value</key>`
## YAML
* **YAML** originally meant *Yet Another Markup Language*, but to distinguish its purpose as a data-serialization language rather than a markup language , it was repurposed to *YAML Aint Markup Language*
* YAML is used by the network automation tool Ansible.
* YAML is very human-readable.
* Whitespace is significant (unlike JSON and XML).
	* Indentation is very important.
* YAML files start with ---.
	* The `---` indicates the start of a new YAML document. This allows multiple documents to be included in a single file. When parsing the YAML, each document is treated as a separate entity. If there is only one document in the file, the `---` is optional but can be used for clarity.
* - is used to indicate a list.
* Keys and values are presented as `key:value`

```
# Example YAML with a list
shopping_list:
  - apples
  - bananas
  - oranges
  - grapes
  - strawberries

# Another example with a list of dictionaries
employees:
  - name: John Doe
    age: 30
    department: Sales
  - name: Jane Smith
    age: 25
    department: Marketing
  - name: Emily Johnson
    age: 28
    department: Development
```