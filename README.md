
<p align="center">
 <a href="#about">About</a> •
 <a href="#Sumary">Sumary</a> • 
 <a href="#Star Schema for Song Play Analysis">Star Schema for Song Play Analysis</a> • 
 <a href="#how-it-works">How it works</a> • 

</p>


## About

  A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. 
  In this project, a star model was created based on a fact table and four dimensions to analyze the information of which songs users are listening to.

---

## Sumary

This project has the following files
 
 - test.ipynb       -> displays the first few rows of each table to let you check your database.
 - create_tables.py -> drops and creates your tables. You run this file to reset your tables before each time you run your ETL scripts.
 - etl.ipynb        -> reads and processes a single file from song_data and log_data and loads the data into your tables. This notebook contains detailed instructions on the ETL process for each of the tables.
 - etl.py -> reads and processes files from song_data and log_data and loads them into your tables. You can fill this out based on your work in the ETL notebook.       
 - sql_queries.py -> contains all your sql queries, and is imported into the last three files above.
---


## Star Schema for Song Play Analysis

The following tools were used in the construction of the project:

**Fact Table**
1. songplays - records in log data associated with song plays i.e. records with page NextSong
 - songplay_id serial
 - start_time timestamp
 - user_id varchar
 - level varchar
 - song_id varchar 
 - artist_id varchar
 - session_id varchar
 - location varchar
 - user_agent 
**Dimension Tables**
2. users - users in the app 
 - user_id varchar
 - first_name varchar
 - last_name varchar
 - gender varchar
 - level varchar <br>
3. songs - songs in music database
 - song_id varchar
 - title varchar
 - artist_id varchar
 - year int
 - duration numeric <br>
4. artists - artists in music database
 - artist_id varchar 
 - name varchar
 - location varchar
 - latitude varchar 
 - varchar longitude 
5. time - timestamps of records in songplays broken down into specific units
 - start_time timestamp
 - hour int
 - day int
 - week int
 - month int
 - year int 
 - weekday int <br>

 <a href="https://r766469c826263xjupyterllyjhwqkl.udacity-student-workspaces.com/files/ER%20Diagram.jpeg?_xsrf=2%7C7daa2b11%7Cef03046626c85f193dc876808c394742%7C1604860773">
    <img alt="ERDiagram" src="https://r766469c826263xjupyterllyjhwqkl.udacity-student-workspaces.com/files/ER%20Diagram.jpeg?_xsrf=2%7C7daa2b11%7Cef03046626c85f193dc876808c394742%7C1604860773">
    </a> 

### songplays Table
```bash
%sql SELECT * FROM songplays LIMIT 5;
```
<a href="https://r766469c826263xjupyterllyjhwqkl.udacity-student-workspaces.com/files/img/songplays.jpg?_xsrf=2%7C7daa2b11%7Cef03046626c85f193dc876808c394742%7C1604860773">
    <img alt="songplays" src="https://r766469c826263xjupyterllyjhwqkl.udacity-student-workspaces.com/files/img/songplays.jpg?_xsrf=2%7C7daa2b11%7Cef03046626c85f193dc876808c394742%7C1604860773">
    </a> 

### users Table
```bash
%sql SELECT * FROM songplays LIMIT 5;
```
<a href="https://r766469c826263xjupyterllyjhwqkl.udacity-student-workspaces.com/files/img/users.jpg?_xsrf=2%7C7daa2b11%7Cef03046626c85f193dc876808c394742%7C1604860773">
    <img alt="users" src="https://r766469c826263xjupyterllyjhwqkl.udacity-student-workspaces.com/files/img/users.jpg?_xsrf=2%7C7daa2b11%7Cef03046626c85f193dc876808c394742%7C1604860773">
    </a> 

### songs Table
```bash
%sql SELECT * FROM songs LIMIT 5;
```
<a href="https://r766469c826263xjupyterllyjhwqkl.udacity-student-workspaces.com/files/img/songs.jpg?_xsrf=2%7C7daa2b11%7Cef03046626c85f193dc876808c394742%7C1604860773">
    <img alt="songs" src="https://r766469c826263xjupyterllyjhwqkl.udacity-student-workspaces.com/files/img/songs.jpg?_xsrf=2%7C7daa2b11%7Cef03046626c85f193dc876808c394742%7C1604860773">
    </a> 
---

### artists Table
```bash
%sql SELECT * FROM artists LIMIT 5;;
```
<a href="https://r766469c826263xjupyterllyjhwqkl.udacity-student-workspaces.com/files/img/artists.jpg?_xsrf=2%7C7daa2b11%7Cef03046626c85f193dc876808c394742%7C1604860773">
    <img alt="artists" src="https://r766469c826263xjupyterllyjhwqkl.udacity-student-workspaces.com/files/img/artists.jpg?_xsrf=2%7C7daa2b11%7Cef03046626c85f193dc876808c394742%7C1604860773">
    </a> 
---

### time Table
```bash
%sql SELECT * FROM time LIMIT 5;
```
<a href="https://r766469c826263xjupyterllyjhwqkl.udacity-student-workspaces.com/files/img/time.jpg?_xsrf=2%7C7daa2b11%7Cef03046626c85f193dc876808c394742%7C1604860773">
    <img alt="time" src="https://r766469c826263xjupyterllyjhwqkl.udacity-student-workspaces.com/files/img/time.jpg?_xsrf=2%7C7daa2b11%7Cef03046626c85f193dc876808c394742%7C1604860773">
    </a> 
---

## How it works

This project is divided into three parts:
1. run create_tables.py to drop and recreate the database tables
2. run etl.py to load the log files (json) into the database tables
3. run test.ipynb to run SQL commands and view the da

### Running the create_tables.py

```bash

def create_database():
    """
    Creates and connects to the sparkifydb
     
    
    Returns: the connection and cursor to sparkifydb
    
    """
    conn = psycopg2.connect("host=127.0.0.1 dbname=studentdb user=student password=student")
    conn.set_session(autocommit=True)
    cur = conn.cursor()
    
    cur.execute("DROP DATABASE IF EXISTS sparkifydb")
    cur.execute("CREATE DATABASE sparkifydb WITH ENCODING 'utf8' TEMPLATE template0")

    conn.close()    
    
    conn = psycopg2.connect("host=127.0.0.1 dbname=sparkifydb user=student password=student")
    cur = conn.cursor()
    
    print('conexão and database ok')
    
    return cur, conn



def drop_tables(cur, conn):
    """
    Drops each table using the queries in `drop_table_queries` list.
    
     Parameters: 
            cur (cursor)   : A cursor with the database connection
            conn : A data base connection 
    
    """
    for query in drop_table_queries:
        cur.execute(query)
        conn.commit()
    print("drop tables ok")


def create_tables(cur, conn):
    """
    Creates each table using the queries in `create_table_queries` list. 
    
    Parameters: 
            cur (cursor)   : A cursor with the database connection
            conn : A data base connection 
    
    """
    for query in create_table_queries:
        cur.execute(query)
        conn.commit()
    print('create tables ok')


def main():
    """
    Drops (if exists) and Creates the sparkify database. 
    
    Establishes connection with the sparkify database and gets cursor to it.  
    
    Drops all the tables.  
    
    Creates all tables needed. 
    
    Finally, closes the connection. 
    
    """
    cur, conn = create_database()
    
    drop_tables(cur, conn)
    create_tables(cur, conn)

    conn.close()





```

### Running the etl.py

```bash
def process_song_file(cur, filepath):
   ''' 
    loads files with song and artist information and inserts in dimension tables (songs and artists)
    
    Parameters: 
            cur (cursor)   : A cursor with the database connection
            filepath (srt) : string with the song file path 
    
     Returns: None
     
    '''
    df = pd.read_json(filepath, lines=True)

    song_data = df[['song_id','title','artist_id','year','duration']].values[0]
    cur.execute(song_table_insert, song_data)
    
    artist_data = df[['artist_id','artist_name','artist_location','artist_latitude','artist_longitude']].values[0]
    cur.execute(artist_table_insert, artist_data)



def process_log_file(cur, filepath):
    
    ''' 
    loads files with log information and inserts in a fact tables (songplay) and dimension tables (users, time)
    
    Parameters: 
            cur (cursor)   : A cursor with the database connection
            filepath (srt) : string with the log file path 
    
     Returns: None
     
    '''

    df = pd.read_json(filepath, lines=True)

    df = df.loc[df['page']=='NextSong']

    t = t = pd.to_datetime(df['ts'], unit='ms')
    
    time_data = (t.dt.time,t.dt.hour,t.dt.day, t.dt.weekofyear,t.dt.month,t.dt.year,t.dt.weekday)
    column_labels = ('time','hour','day','weekofyear','month','year','weekday')
    time_df = pd.DataFrame.from_dict(dict(zip(column_labels,time_data)))

    for i, row in time_df.iterrows():
        cur.execute(time_table_insert, list(row))

    user_df = df.loc[:,['userId','firstName','lastName','gender','level']]

    for i, row in user_df.iterrows():
        cur.execute(user_table_insert, row)

    for index, row in df.iterrows():
        
        cur.execute(song_select, (row.song, row.artist, row.length))
        results = cur.fetchone()
        
        if results:
            songid, artistid = results
        else:
            songid, artistid = None, None

        songplay_data = (pd.to_datetime(row.ts, unit='ms'), row.userId, row.level, songid, artistid, row.sessionId, row.location, row.userAgent)
        cur.execute(songplay_table_insert, songplay_data)
        
        
        
def process_data(cur, conn, filepath, func):
    
     ''' 
     loads files with log information and inserts in a fact tables (songplay) and dimension tables (users, time)
    
    Parameters: 
            cur (cursor)   : A cursor with the database connection
            filepath (srt) : string with the files path 
            conn : A data base connection 
            func : function responsible for defining which files will be inserted in the database 
                    process_song_file function - load song data files
                    process_log_file function - load  log data files
    
     Returns: None
     
    '''

    # get all files matching extension from directory
    all_files = []
    for root, dirs, files in os.walk(filepath):
        files = glob.glob(os.path.join(root,'*.json'))
        for f in files :
            all_files.append(os.path.abspath(f))

    # get total number of files found
    num_files = len(all_files)
    print('{} files found in {}'.format(num_files, filepath))

    # iterate over files and process
    for i, datafile in enumerate(all_files, 1):
        func(cur, datafile)
        conn.commit()
        print('{}/{} files processed.'.format(i, num_files))


def main():

  """
    
    Establishes connection with the sparkify database and gets cursor to it.  
    
    process all the song files in the path .  
    
    process all the log files in the path. 
    
    Finally, closes the connection. 
    
    """
    
    conn = psycopg2.connect("host=127.0.0.1 dbname=sparkifydb user=student password=student")
    cur = conn.cursor()

    process_data(cur, conn, filepath='data/song_data', func=process_song_file)
    process_data(cur, conn, filepath='data/log_data', func=process_log_file)

    conn.close()


```

---

