03 - Installing the Libraries and Setting Up
Install the "psycopg2" Python package
pip3 install psycopg2
Create a new file: "sql-psycopg2.py"
touch sql-psycopg2.py


05 - Running Basic Queries
Create a new file called "sql-expression.py"
touch sql-expression.py
Query 1 - select all records from the "Artist" table
select_query = artist_table.select()
Query 2 - select only the "Name" column from the "Artist" table
select_query = artist_table.select().with_only_columns([artist_table.c.Name])
Query 3 - select only 'Queen' from the "Artist" table
select_query = artist_table.select().where(artist_table.c.Name == "Queen")
Query 4 - select only by 'ArtistId' #51 from the "Artist" table
select_query = artist_table.select().where(artist_table.c.ArtistId == 51)
Query 5 - select only the albums with 'ArtistId' #51 on the "Album" table
select_query = album_table.select().where(album_table.c.ArtistId == 51)
Query 6 - select all tracks where the composer is 'Queen' from the "Track" table
select_query = track_table.select().where(track_table.c.Composer == "Queen")


06 - Introducing Class-Based Models
Create a new file called "sql-orm.py"
touch sql-orm.py
Query 1 - select all records from the "Artist" table
artists = session.query(Artist)
for artist in artists:
    print(artist.ArtistId, artist.Name, sep=" | ")
Query 2 - select only the "Name" column from the "Artist" table
artists = session.query(Artist)
for artist in artists:
    print(artist.Name)
Query 3 - select only "Queen" from the "Artist" table
artist = session.query(Artist).filter_by(Name="Queen").first()
print(artist.ArtistId, artist.Name, sep=" | ")
Query 4 - select only by "ArtistId" #51 from the "Artist" table
artist = session.query(Artist).filter_by(ArtistId=51).first()
print(artist.ArtistId, artist.Name, sep=" | ")
Query 5 - select only the albums with "ArtistId" #51 on the "Album" table
albums = session.query(Album).filter_by(ArtistId=51)
for album in albums:
    print(album.AlbumId, album.Title, album.ArtistId, sep=" | ")
Query 6 - select all tracks where the composer is "Queen" from the "Track" table
tracks = session.query(Track).filter_by(Composer="Queen")
for track in tracks:
    print(
        track.TrackId,
        track.Name,
        track.AlbumId,
        track.MediaTypeId,
        track.GenreId,
        track.Composer,
        track.Milliseconds,
        track.Bytes,
        track.UnitPrice,
        sep=" | "
    )