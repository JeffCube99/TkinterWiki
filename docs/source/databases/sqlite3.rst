=======
sqlite3
=======

Example Database Class
======================

..  note::

    This class does not contain functions for creating, saving, updating information in the database. It only
    outlines a way to have a class that safely initializes and closes a connection to an sqlite3 database
    when the class is instantiated and deleted.

..  code-block:: python

    class Sqlite3DatabaseExample:
        def __init__(self, database_file_path: str):
            """
            Initializes connection to a database file. If the database file does not exist
            it will be created at the given database_file_path location.

            **Note** In general you should not expose the database location for security purposes.
            :param database_file_path: Path to a (.db) database file
            """
            self._database_connection: sqlite3.Connection = sqlite3.connect(database_file_path)

        def __del__(self):
            """
            Closes the connection to the database. This gives us peace of mind
            as the database connection will be terminated whenever the class
            is deleted or garbage collected.

            **Note** This function does not call the sqlite3 commit() command
            so any uncommitted changes to the database will be lost.
            """
            self._database_connection.close()
