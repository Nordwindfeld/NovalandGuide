=====================================
Randomise Values for the participant
=====================================
There are several ways to randomize numbers and inputs.
In Novaland, we have used the tactic of creating a table and determining the values that have an impact on the game beforehand.
This way, we prevent too many similar results from occurring.

Create and import a CSV Data
____________________________________

There are many different tools that can be used to create CSV data, including Excel, for example.

When creating a CSV file, there are several things to keep in mind:

    1. Delimiter: CSV stands for "comma-separated values," so the values in each row should be separated by commas. However, depending on your locale or data formatting needs, you may need to use a different delimiter, such as a semicolon or tab.

    2. Header row: It's a good practice to include a header row at the top of your CSV file that describes the contents of each column.

    3. Quotes: If any of your values contain commas or other special characters, you should enclose them in double quotes to ensure they are correctly parsed.

    4. Encoding: Make sure to use an appropriate character encoding for your data. UTF-8 is a common encoding that supports a wide range of characters and is widely supported.

    5. Consistency: Ensure that the data in your CSV file is consistent, with the same number of columns in each row and consistent data types (e.g., dates formatted the same way).

    6. Cleanliness: Remove any unnecessary characters, formatting or other data that isn't relevant to the data being recorded in the CSV file.

    7. File extension: Use the .csv file extension to ensure that the file is recognized as a CSV file and can be opened correctly by programs that support CSV files.

Now you can place the CSV file in the Novaland folder and use it from there.

To be able to use the individual values in your project, we will write some code in the init.py file, in which the program reads the values and assigns them to each participant.

First, we need to install the CSV library:

.. code-block:: console

    import csv


Then we write a for-loop that reads all the data from the table and assigns it to the participants.

For Example:

.. code-block:: console

    def creating_session(subsession: Subsession):
        f = open('participants_data.csv', encoding='utf-8-sig')

        rows = list(csv.DictReader(f))
        players = subsession.get_players()
        for i in range(len(players)):
            row = rows[i]
            player = players[i]
            player.Income = int(row['Income'])
            player.Corruption = int(row['Corruption'])
            player.Jobless = int(row['Jobless'])
            player.FireAffected = int(row['FireAffected'])
            player.participant.CSVIncome = int(row['Income'])
            player.participant.CSVCorruption = int(row['Corruption'])
            player.participant.CSVJobless = int(row['Jobless'])
            player.participant.CSVFireAffected = int(row['FireAffected'])



Explanation about the Example Code:

.. code-block:: console

    f = open('participants_data.csv', encoding='utf-8-sig')


The 'open' function takes two arguments: the first is the filename (in this case, 'participants_data.csv') and the second is the mode in which to open the file.
The 'encoding' parameter is used to specify the character encoding used in the file. In this case, 'utf-8-sig' is used, which is a variant of the UTF-8 encoding that includes a byte-order mark (BOM) at the beginning of the file.
The BOM is a special character sequence that indicates the byte order of the data in the file, and it can be used by some programs to determine the file's encoding automatically.

Once the file is opened, the returned file object is assigned to the variable 'f'. The file object can then be used to read data from the file using various methods.

.. code-block:: console

    rows = list(csv.DictReader(f))


The 'DictReader' method reads the file and returns an object that can be used to iterate over the rows in the file.
Each row is represented as a dictionary, where the keys are the column headers from the CSV file and the values are the corresponding values in the row.

The 'f' variable in this code represents a file object that has been opened for reading using the 'open' function earlier in the code.
The 'DictReader' method takes this file object as an argument, which allows it to read the contents of the file.

The resulting list of dictionaries is assigned to the variable 'rows', which can be used to access the data from the CSV file later in the code.
By creating a list of dictionaries, this code makes it easy to access the data by column name (i.e. the keys in each dictionary) rather than by index (i.e. the positions of values in each row).

.. code-block:: console

    players = subsession.get_players()

The line retrieves a list of all the players in the current subsession.
This is done by calling the "get_players()" method on the subsession object, which returns a list of player objects.

.. code-block:: console
    for i in range(len(players)):
        row = rows[i]
        player = players[i]
        player.Income = int(row['Income'])
        player.Corruption = int(row['Corruption'])
        player.Jobless = int(row['Jobless'])
        player.FireAffected = int(row['FireAffected'])
        player.participant.CSVIncome = int(row['Income'])
        player.participant.CSVCorruption = int(row['Corruption'])
        player.participant.CSVJobless = int(row['Jobless'])
        player.participant.CSVFireAffected = int(row['FireAffected'])


The function then gets a list of players from the "subsession" object and loops over them.
For each player, it retrieves the corresponding row of data from the list of dictionaries and sets the player's attributes (Income, Corruption, Jobless, FireAffected) to the values from the row.
The function also sets the values from the row to these participant values (CSVIncome, CSVCorruption, CSVJobless, CSVFireAffected).