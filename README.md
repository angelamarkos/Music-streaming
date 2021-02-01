# Music-streaming

Music streaming data design

Create models.py

1. Create User class
    attribut list:
          id: generate id number for each object
          first_name: str
          last_name: str
          email: str
          password: str
          profile_pics: list
          birth_date: datetime
          level: int, default 0
   
   Optional attributes:
       profile_pics,
       birth_date 
   
   method list:
       validate_user(self) method which should check if not optional fields are not None and email is valid email, 
       and password at least has:
            at least 8 characters
            both uppercase and lowercase letters
            numbers
            at least one special character, e.g., ! @ # ? ]
       create_playelist(self, name)
       delete_playelist(self, name)
       
        
2. Create class Artist that inherit from user:
   attribut list:
       about: str
       listeners_count: int
   method list:
       add_song(self, title: str, artist_name: str, file: string) 
          for now file argument should be just file's path on your computer
       delete_song(self, song_id)
       create_album(self, title, label, year, list_of_song_url=[])
       delete_album(self, album_id)
       
3. Create Song class.
    attribute list:
        id: generate id number for each object
        title: str
        artist: str
        duration: int # seconds
        genre: str
        year: int
        created_by: artist
        streams_count: int
        album: album if no album created default create album with same nam as song (for singles)
        
    method list:
        validate(self): if  created_by is not an Artist objects raise Exception('Access denied.')
        add_to_playlist(self, playlist, user)
        remove_from_playlist(self, playlist, user)
        play(self, user) # if already exists stop previous track
        stop(self, user) # increment sream count if played 30 seconds at least
        download(self) # returns song path for now
    
 4. Create Playlist class
     attribute list:
        id: generate id number for each object
        name: str
        date_added: datetime
        created_by: User
        picture_url: picture_url
     property: count_of_songs
               duration_of_playlist
               genre_list 
     method_list:
        play() play all tracks in playlist in order added_date
        stop() 
     
 5. Create Album class and inherit it from Playlist.
    attribute list:
       label: str
       year: str
    method list:
       validate() if created_by is not Artist object raise Exception('Access denied.')
 
 6. class SongPlayes
    attribute list:
       id: generate id number for each object
       user: User
       song: Song
       start_timestamp: float
       
 7. class PlaylistSong: (this class should help to find out song's playlists and playlist's songs)
    attribut list
        playlist: Playlist
        song: Song
        date_added: datetime
    
    
    
 
Change classes I decribe above as follows: all classes should have

file_path: file where you should save your onjects.__ dict__ info
save all objects in ./data/classname.txt files

methods:
  save(self) should save __ dict__ of objects in file_path as one line
  
  update(self, ** kwargs): update fields from kwargs if there is any keyword that object cass doesn't have raise Exceptions('{class name} does't have field_1, field_2, ...., use fields from {list of available fields name}) and dict in file_path 
  
  delete(self) should delete current onjects from file_path if exist else raise Exception('No {class name} objects founded')
  
  @staticmethod
  filter(** kwargs) should find all "dict" in file_path which have all key values from kwargs and return corresponding objects
  
  example: Song.filter(title='Over and over', genre='Alternative') should return all song objects that hase title 'Over and over' and genre 'Alternative'
  
  @staticmethod
  get(** kwargs)  should find a "dict" in file_path which have all key values from kwargs and return corresponding object,
  if there is multiple objects raise Exception('Multiple {class name} objects founded')   
  if there is no dict in file raise Exception('No {class name} objects founded')
 
  
Hint: to generate id use uuid python module and pass uniq string that decribe your object

Create test.py file and create unittests for your models and test all methods        
 Hint for testing in setUp method create different file path to save your testing objects and in teardown function delete testing file
       
