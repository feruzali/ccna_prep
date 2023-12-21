---
description: JSON, XML, & YAML
---

# Day 60

**Data serialization** is the process of converting data into a serialized format/structure that can be stored or transmitted and reconstructed later. This allows the data to be communicated between applications in a way both applications understand. Data serialization languages allow us to represent variables with text. **Variables** are containers that store values.&#x20;

<figure><img src=".gitbook/assets/image (7).png" alt="data serialization demo" width="563"><figcaption></figcaption></figure>

### JSON

**JSON** (JavaScript Object Notation) is an open standard file format and data interchange format that uses human-readable text to store and transmit data objects. REST APIs often use JSON. In JSON, whitespace is insignificant.

JSON primitive data types:

* **String** - a text value. It is surrounded by double quotes (`" "`).
* **Number** - a numeric value.&#x20;
* **Boolean** - data type that has only two possible values (true or false).
* **Null** - represents the intentional absence of any object value (`null`).

JSON structured data types:

*   **Object** - an unordered list of key-value pairs (variables). Objects are surrounded by curly brackets (`{}`). The **key** is a string and the **value** is any valid JSON data type. The key and value are separated by a colon (`:`). If there are multiple key-value pairs, each pair is separated by a comma (`,`). Objects within objects are called **nested objects**.\


    <figure><img src=".gitbook/assets/image (1) (1).png" alt="object example" width="563"><figcaption></figcaption></figure>
*   **Array** - series of values separated by commas. The values don't have to be the same data type.\


    <figure><img src=".gitbook/assets/image (2) (1).png" alt="array example" width="563"><figcaption></figcaption></figure>

### XML

**XML** (Extensible Markup Language) was developed as a markup language but is now used as a general data serialization language. Markup languages are used to format text. XML is less human-readable than JSON. The whitespace is insignificant. Used by REST APIs.

<figure><img src=".gitbook/assets/image (169).png" alt="XML example" width="563"><figcaption></figcaption></figure>

### YAML

**YAML** originally meant Yet Another Markup Language but to distinguish its purpose as a data-serialization language rather than a markup language, it was repurposed to YAML Aint Markup Language. It is used by the network automation tool Ansible. It is very human-readable. Whitespace is significant, indentation is very important. YAML files start with `---`. `-` is used to indicate a list. Keys and values are represented as `key:value`.

<figure><img src=".gitbook/assets/image (170).png" alt="YAML example" width="563"><figcaption></figcaption></figure>

{% file src=".gitbook/assets/Day 60 Flashcards - JSON, XML, _ YAML.apkg" %}
